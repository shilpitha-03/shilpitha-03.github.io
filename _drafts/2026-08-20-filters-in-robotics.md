---
layout: post
title: filters in robotics
date: 2026-08-20 09:00:00-0400
description: an intuition-first tour of the filters that make robots trust their sensors — Bayes, Kalman, EKF, particle, and complementary
tags: robotics state-estimation kalman-filter perception
categories: robotics
related_posts: false
toc:
  sidebar: left
---

<!--
  WRITING NOTES (delete before publishing):
  - This file lives in _drafts/, so it will NOT deploy. Preview with:  jekyll serve --drafts
  - To publish: move this file to _posts/ (keep the YYYY-MM-DD- prefix), then set
    latest_posts.enabled: true in _pages/about.md.
  - The left sidebar table of contents builds itself from the ## and ### headings below.
  - Math: surround with $$ ... $$  (inline if in a paragraph, display if on its own line).
  - Every <!-- ... --> comment marks a spot for you to write. The snippets are live examples
    you can keep, edit, or delete.
-->

<!-- HOOK: 1–2 paragraphs. Open with a concrete robot moment — a drone that must hold
     position while its GPS stutters, a wheeled robot whose encoders drift. The point:
     every sensor lies a little, and filters are how a robot fuses noisy measurements into
     a belief it can act on. State the question the post answers. -->

## Why robots need filters

<!-- The core problem, plainly: sensors are noisy, models are imperfect, and the robot
     still has to commit to ONE estimate of where it is / how fast it's moving.
     Introduce the two ingredients every filter balances:
       - what we PREDICT from motion (the model)
       - what we MEASURE from sensors (the observation)
     Set up "state", "measurement", and "belief" as terms you'll reuse. -->

### The setup: state, motion, and measurement

<!-- Define the state vector x, the motion model, and the measurement model in words first,
     then formalize. Example display math you can keep and adapt: -->

$$
x_k = f(x_{k-1}, u_k) + w_k, \qquad z_k = h(x_k) + v_k
$$

<!-- Explain each symbol: x state, u control input, z measurement, w process noise,
     v measurement noise. Keep it friendly — one sentence per symbol. -->

## The Bayes filter: the idea underneath all of them

<!-- The unifying framework. Predict step (push belief through motion model) and
     update step (reweight belief by measurement). Everything later is a special case. -->

$$
\underbrace{\text{bel}(x_k)}_{\text{posterior}} \;\propto\; \underbrace{p(z_k \mid x_k)}_{\text{measurement}} \int \underbrace{p(x_k \mid x_{k-1}, u_k)}_{\text{motion}}\, \text{bel}(x_{k-1})\, dx_{k-1}
$$

<!-- Walk through predict-then-update in words. Emphasize: Kalman, EKF, and particle
     filters all answer "how do we actually compute this integral?" -->

## The Kalman filter: optimal for the linear-Gaussian world

<!-- The assumptions (linear models, Gaussian noise) and why they make the math close in
     closed form. Give the intuition for the Kalman gain BEFORE the equations:
     "how much do I trust the new measurement vs. my prediction?" -->

### The five equations

<!-- Predict (state + covariance) and update (gain, state, covariance). Number the key one
     so you can reference it later with \eqref{eq:kalman-gain}. -->

\begin{equation}
\label{eq:kalman-gain}
K_k = P_k^- H^\top \left( H P_k^- H^\top + R \right)^{-1}
\end{equation}

<!-- Then explain the gain intuitively: R large (noisy sensor) -> K small -> trust the
     model; P large (uncertain prediction) -> K large -> trust the measurement. -->

### A worked intuition: 1-D position tracking

<!-- Optional but powerful: a tiny 1-D example (tracking position from a noisy range sensor).
     Drop in a code block if you want to show a minimal implementation. Example: -->

```python
# minimal 1-D Kalman update
def update(x, P, z, H, R):
    y = z - H * x                 # innovation (measurement residual)
    S = H * P * H + R             # innovation covariance
    K = P * H / S                 # Kalman gain
    x = x + K * y                 # corrected state
    P = (1 - K * H) * P           # corrected covariance
    return x, P
```

<!-- FIGURE: a plot of true position vs. noisy measurements vs. filtered estimate makes
     this land. Add the image to assets/img/ and reference it like below. -->

<!--
{% include figure.liquid loading="eager" path="assets/img/YOUR-KALMAN-PLOT.png" class="img-fluid rounded z-depth-1" zoomable=true %}
-->

## When the world isn't linear: the Extended Kalman Filter

<!-- Real robot models (headings, ranges, camera projection) are nonlinear. The EKF trick:
     linearize f and h around the current estimate via Jacobians. State the cost:
     it's an approximation, and it can diverge when nonlinearity is strong. -->

### Jacobians and the linearization step

<!-- Show F = df/dx and H = dh/dx as Jacobians. One or two sentences on when linearization
     is "good enough" vs. when it breaks. Mention UKF in a sentence as the sigma-point
     alternative if you want a forward pointer. -->

## When the belief isn't Gaussian: particle filters

<!-- The move from a parametric Gaussian to a cloud of weighted samples. Great for
     multi-modal beliefs (the classic: robot localization in a symmetric hallway).
     Predict = move each particle; update = reweight by measurement likelihood;
     then resample. -->

### Predict, weight, resample

<!-- Describe the three steps and the failure mode (particle depletion). A small table
     comparing the filters helps the reader lock in the trade-offs: -->

| Filter | Belief representation | Handles nonlinearity | Handles multi-modality | Cost |
| :-- | :-- | :--: | :--: | :-- |
| Kalman | single Gaussian | no | no | cheap |
| EKF | single Gaussian | via linearization | no | cheap |
| Particle | weighted samples | yes | yes | expensive |

<!-- Fill / adjust the rows; add UKF or complementary if you cover them. -->

## The unsung workhorse: complementary filters

<!-- The practical one every drone/IMU person meets first. Fuse a fast-but-drifting source
     (gyro) with a slow-but-stable one (accelerometer/magnetometer) using a simple
     frequency split. Why it's everywhere: cheap, no covariance bookkeeping. Tie back to
     your UAV work if you like. -->

$$
\hat{\theta}_k = \alpha \left( \hat{\theta}_{k-1} + \dot{\theta}_{\text{gyro}}\, \Delta t \right) + (1 - \alpha)\, \theta_{\text{accel}}
$$

<!-- One paragraph on choosing alpha (the trust knob between the two sources). -->

## Filters in the wild: where these show up

<!-- Concrete robotics applications. Pull from what you know: UAV obstacle detection /
     state estimation, visual-inertial odometry, SLAM back-ends, sensor fusion for
     localization. 3–5 short bullets, each naming the filter and the job it does. -->

- <!-- e.g. IMU + camera fusion (VIO) -> EKF/UKF -->
- <!-- e.g. Monte Carlo Localization -> particle filter -->
- <!-- e.g. attitude estimation on a flight controller -> complementary filter -->

## Takeaways

<!-- 3–4 sentences. The mental model you want the reader to leave with: it's all the Bayes
     filter; the choice is about what assumptions you can afford (linear? Gaussian?
     uni-modal?) vs. the compute you have. End with a pointer to a follow-up post if you
     plan one (e.g. a from-scratch EKF for a differential-drive robot). -->

## Further reading

<!-- Optional. Link 2–4 sources: Thrun/Burgard/Fox "Probabilistic Robotics", a good
     Kalman intuition post, etc. Use markdown links: [text](url). -->
