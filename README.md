

# Abstract

Autonomous Underwater Vehicles (AUVs) rely heavily on accurate navigation for deep-water exploration and research. Conventional Kalman Filters, while widely used in inertial navigation, face challenges when applied to systems evolving on nonlinear manifolds, often leading to inconsistency and degraded performance in long-duration missions. This knowledge gap motivates the development of Invariant Kalman Filters (IKFs), which exploit the underlying Lie group structure of motion dynamics to achieve improved consistency, stability, and robustness.

In this study, we investigate the application of the Invariant Kalman Filter for underwater navigation using data collected off the coast of Haifa, Israel, with the Snapir AUV. Snapir is a modified ECA Group A18D mid-size AUV designed for deep-water missions up to 3000 meters and 21 hours of endurance. It is equipped with a high-performance iXblue Phins Subsea fiber-optic gyroscope-based inertial navigation system and a Teledyne RDI Work Horse Navigator Doppler Velocity Log (DVL), enabling precise measurements of orientation, acceleration, and velocity. The IKF framework is tailored to fuse these measurements while respecting the systems nonlinear structure

Preliminary results are expected to demonstrate improved navigation accuracy and reduced drift compared to conventional Extended Kalman Filter approaches, particularly during long-duration and deep-water missions where GPS signals are unavailable. The research holds significance for advancing underwater navigation technology, enhancing the reliability of AUV-based oceanographic surveys, and enabling more effective scientific and industrial exploration in challenging subsea environments.


# Introduction to the Navigation Problem

The inertial navigation problem is concerned with estimating the position, velocity, and orientation of a platform using onboard sensors. In practice, this is achieved by integrating data from inertial measurement units (IMUs), and refining these estimates with external measurements such as GNSS, GPS, Doppler Velocity Log (DVL), or other aiding sensors. Accurate state estimation in this context is crucial for applications ranging from autonomous vehicles to aerospace systems, where reliability and robustness are paramount.

A classical approach to this estimation problem is the Extended Kalman Filter (EKF)\autocite{groves9101092}. In the EKF framework, the system dynamics are propagated forward in time and linearized around the current state estimate, while sensor models are incorporated to correct the estimate when new measurements become available. Despite its widespread success, this method has well-known limitations: the linearization process introduces a strong dependence of the system matrix on the current estimate, which can lead to inconsistency and reduced robustness, especially under poor initial conditions.

Recent advances\autocite{barrau2015invariantextendedkalmanfilter} leverage **Lie group theory** to reformulate the estimation problem, leading to the development of the Invariant Kalman Filter (IKF)\autocite{barrau:tel-01344622}. Unlike the classical EKF, the IKF describes error propagation in a way that is consistent with the underlying geometry of the state space. This formulation significantly reduces the dependence of the system matrix on the current estimate, yielding improved stability and accuracy. Moreover, while the EKF assumes error distributions that are well approximated by ellipsoids, the IKF naturally accommodates banana-shaped distributions, which more closely reflect the true uncertainty structure in inertial navigation.

This distinction is particularly important in scenarios where high-quality IMUs are available but the initial conditions are poor. In such cases, the invariant framework can maintain filter consistency without relying on the traditional two-stage process of coarse and fine alignment. Instead, a single IKF can provide a robust solution that adapts naturally to the navigation problem&rsquo;s geometry and measurement structure. To my knowledge, most contributions in this area have remained primarily theoretical. With access to the Snapir AUV and Ariel AUV, I am in a unique position to carry out experimental validation, providing practical demonstrations of the theory in real-world underwater navigation scenarios.


# Research Goals

While the benefits of respecting the geometric structure of navigation dynamics have been well recognized in theoretical works on Lie groups and invariant filtering, practical adoption has been limited. The majority of operational navigation systems continue to rely on classical EKF-based architectures or their unscented and iterated variants, largely due to their familiarity, availability of mature software implementations, and established performance in standard conditions.

Recent research in state estimation has been dominated by two trends:

-   **Data-driven enhancements** \autocite{YAMPOLSKY2025104525}, where machine learning models (e.g., deep neural networks, Gaussian processes) are used to augment prediction or measurement models.
-   **Adaptive filtering approaches** \autocite{COHEN2025110221}\autocite{NA11028550}, including auto-regressive and statistical learning techniques for bias estimation and noise covariance tuning

Although these approaches have improved performance in certain cases, they generally maintain the traditional state-space formulation in $\mathbb{R}^n$, and thus inherit its limitations when applied to inherently geometric systems like inertial navigation. By contrast, the Invariant Kalman Filter provides a principled way to integrate system symmetries into the estimation process, yielding error dynamics that are independent of the estimated trajectory and more robust to large initialization errors.

To date, there is a shortage of empirical studies that:

-   Quantitatively compare IKF performance against both conventional and learning-augmented Kalman filters in realistic navigation scenarios.
-   Investigate the use of data-driven and adaptive estimation strategies-such as neural augmentation, Gaussian processes, or online noise adaptation-formulated directly on Lie groups, thereby preserving the underlying geometric structure of navigation dynamics
-   Provide a systematic observability analysis of the Invariant Kalman Filter, clarifying its advantages and limitations relative to classical formulations.

**This research will address these gaps by systematically comparing invariant filtering to established alternatives and by developing methodologies for integrating modern learning-based and adaptive techniques within the Lie group framework.**


# Dataset

Experimental validation will use real-world navigation data collected by our team from the autonomous submarine Snapir. The dataset is publicly available at: <https://github.com/ansfl/A-KIT>. It contains synchronized measurements from an onboard Inertial Measurement Unit (IMU), aiding sensors DVL, and ground-truth reference trajectories obtained from post-processing. This dataset provides a realistic and challenging evaluation environment due to its underwater setting, which is characterized by GNSS-denied navigation, variable sensor quality, and complex vehicle dynamics.


# Evaluation Procedure

The experimental procedure will involve:

-   Preprocessing and time synchronization of sensor measurements.
-   Implementing the two filters (EKF, , IKF) under a common navigation framework to ensure fair comparison.
-   Running each filter over multiple mission segments, including high-dynamic maneuvers, long aiding-sensor outages, and bias-drift conditions.
-   Quantitatively evaluating performance using metrics such as:
    1.  Root Mean Square Error (RMSE) in position, velocity, and orientation.
    2.  Filter consistency, measured via Normalized Estimation Error Squared (NEES).


# Theoretical Background


## Introduction to Invariant Kalman Filtering

\printbibliography

