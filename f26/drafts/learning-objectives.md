<!--
  DRAFT — pulled out of syllabus.md on 2026-08-25 and parked here for later.
  This directory is listed in _config.yml's `exclude:`, so nothing under
  f26/drafts/ is built or published, no matter what front matter it has.

  To restore: paste the section below back into syllabus.md between
  "## Prerequisites" and whatever now precedes it (currently the MBots
  hardware paragraph under "What that looks like week to week").
-->

## Learning objectives

Objectives are written against [Bloom's revised taxonomy](https://en.wikipedia.org/wiki/Bloom%27s_taxonomy);
the cognitive level of each is marked in brackets. *Remember*-level knowledge
(terminology, standard formulations) is a prerequisite for the work rather than
an assessed outcome, so the objectives below begin at *Understand*.

### Course-level outcomes
{: .text-delta }

By the end of this course, you will be able to:

1. **[Understand]** **Explain** the probabilistic formulation of mobile-robot
   state estimation — motion models, measurement models, and the assumptions
   each makes — and **describe** where each assumption breaks on real hardware.

2. **[Apply]** **Implement** a dead-reckoning pose estimator from wheel-encoder
   data on a physical differential-drive robot, reporting pose in an explicitly
   documented frame convention.

3. **[Apply]** **Calibrate** a camera and a LIDAR and **transform** their
   measurements into the robot body frame through a correct, documented chain
   of rigid-body transforms.

4. **[Apply]** **Implement** a visual-odometry pipeline — feature extraction,
   correspondence, and relative-pose estimation — that recovers incremental
   motion from real image sequences.

5. **[Analyze]** **Characterize** error accumulation in a state estimator,
   **distinguishing** systematic sources (miscalibration, unmodeled kinematics)
   from stochastic ones (sensor noise, wheel slip), using measured ground truth.

6. **[Apply]** **Deploy** global and sampling-based path planners on an
   occupancy-grid map, together with a local controller that avoids obstacles
   sensed at runtime.

7. **[Analyze]** **Compare** planning and SLAM algorithms with respect to
   completeness, optimality, computational cost, and degradation under sensing
   and actuation uncertainty — and **diagnose** observed failures from logged data.

8. **[Evaluate]** **Benchmark** competing approaches against ground truth using
   standard metrics, and **justify** a selection for a stated operating
   environment and compute budget.

9. **[Create]** **Design, integrate, and demonstrate** a complete autonomous
   navigation stack on physical hardware that builds a map of an unknown indoor
   environment and drives to commanded goals without collision.

### Module-level objectives
{: .text-delta }

#### 1 · Foundations: frames, transforms, and kinematics

| # | Objective | Level |
|:--|:----------|:------|
| 1.1 | **Describe** the frame conventions of a mobile robot (world, odom, base, sensor) and **explain** why estimation is defined relative to a frame graph. | Understand |
| 1.2 | **Compose and invert** rigid-body transforms in SE(2) and SE(3) to relate a measurement to any frame in the chain. | Apply |
| 1.3 | **Derive** the forward-kinematic model of a differential-drive platform from wheel geometry. | Understand |
| 1.4 | **Detect** frame errors (sign, order, stale transform) from the geometric symptoms they produce in visualized data. | Analyze |

#### 2 · Dead reckoning from odometry

| # | Objective | Level |
|:--|:----------|:------|
| 2.1 | **Explain** how encoder counts become a pose estimate, and **identify** the integration scheme's contribution to error. | Understand |
| 2.2 | **Implement** encoder-based dead reckoning on hardware and **publish** a live pose estimate. | Apply |
| 2.3 | **Calibrate** wheel radius and track width from a repeatable trajectory test (e.g. UMBmark-style square path). | Apply |
| 2.4 | **Quantify** drift as a function of path length and heading change, and **attribute** it to systematic versus stochastic sources. | Analyze |
| 2.5 | **Argue** from measured data why dead reckoning alone cannot support long-duration navigation. | Evaluate |

#### 3 · Sensor modeling: LIDAR and cameras

| # | Objective | Level |
|:--|:----------|:------|
| 3.1 | **Explain** the measurement principle and dominant error sources of a scanning LIDAR and of a passive camera. | Understand |
| 3.2 | **Formulate** a probabilistic range measurement model (beam model and likelihood field), **stating** what each mixture component represents. | Understand |
| 3.3 | **Apply** the pinhole model with lens distortion to project between image and camera coordinates. | Apply |
| 3.4 | **Estimate** camera intrinsics and distortion coefficients from a calibration target, and **assess** the fit from reprojection residuals. | Apply |
| 3.5 | **Predict** sensor failure modes from environment properties — specular and glass surfaces, low texture, motion blur, rolling shutter, exposure limits. | Analyze |
| 3.6 | **Select** a sensor suite for a stated environment and **defend** the choice against cost, range, and compute constraints. | Evaluate |

#### 4 · Visual odometry

| # | Objective | Level |
|:--|:----------|:------|
| 4.1 | **Explain** the geometry relating two views: epipolar constraint, essential and fundamental matrices, triangulation. | Understand |
| 4.2 | **Implement** feature detection, description, and matching with outlier rejection (RANSAC) on real imagery. | Apply |
| 4.3 | **Estimate** relative camera motion by essential-matrix decomposition or PnP, and **chain** estimates into a trajectory. | Apply |
| 4.4 | **Explain** monocular scale ambiguity and **evaluate** the strategies that resolve it (stereo baseline, known geometry, sensor fusion). | Analyze |
| 4.5 | **Compare** visual and wheel odometry on the same hardware run, and **explain** which failure regimes each one covers for the other. | Evaluate |

#### 5 · Path planning

| # | Objective | Level |
|:--|:----------|:------|
| 5.1 | **Represent** an environment as an occupancy grid and **explain** the role of configuration-space inflation. | Understand |
| 5.2 | **Implement** a graph search planner (Dijkstra, A\*) with an admissible heuristic and **verify** optimality on known cases. | Apply |
| 5.3 | **Implement** a sampling-based planner (RRT / RRT\*) and **explain** the probabilistic-completeness guarantee it does and does not provide. | Apply |
| 5.4 | **Contrast** planners on optimality, completeness, memory, and runtime, and **predict** which suits a given map and compute budget. | Analyze |
| 5.5 | **Integrate** a global planner with a local reactive controller and **demonstrate** goal-reaching with obstacle avoidance on hardware. | Create |

#### 6 · Simultaneous localization and mapping

| # | Objective | Level |
|:--|:----------|:------|
| 6.1 | **Formulate** SLAM as joint estimation over robot poses and map structure, and **explain** why the two are correlated. | Understand |
| 6.2 | **Distinguish** filtering-based SLAM from pose-graph optimization, and **describe** the front-end / back-end division of labor. | Understand |
| 6.3 | **Implement or configure** a scan-matching front end and **produce** an occupancy-grid map from a hardware run. | Apply |
| 6.4 | **Explain** loop closure as a constraint on the pose graph and **demonstrate** its effect on global map consistency. | Apply |
| 6.5 | **Diagnose** SLAM failures from logs and visualization — data-association errors, false or missed loop closures, degenerate geometry, sensor dropout. | Analyze |
| 6.6 | **Assess** map and trajectory quality with quantitative metrics (e.g. absolute trajectory error, relative pose error) rather than visual impression. | Evaluate |

#### 7 · Full-stack integration

| # | Objective | Level |
|:--|:----------|:------|
| 7.1 | **Architect** a navigation stack as communicating components with defined interfaces, rates, and frame conventions. | Create |
| 7.2 | **Integrate** perception, estimation, mapping, planning, and control into a system that maps an unknown space and navigates it autonomously. | Create |
| 7.3 | **Analyze** end-to-end system behavior under real-time constraints — latency, dropped messages, compute saturation. | Analyze |
| 7.4 | **Critique** a peer team's design and **defend** your own tradeoffs with quantitative evidence. | Evaluate |
| 7.5 | **Document** hardware experiments so a peer can reproduce your results on the same platform. | Apply |

### How the levels are distributed
{: .text-delta }

| Bloom level | Share of objectives | Assessed primarily by |
|:------------|:--------------------|:----------------------|
| Understand | ~25% | Concept quizzes, short written derivations |
| Apply | ~35% | Hardware lab implementations |
| Analyze | ~20% | Error characterization and failure-diagnosis reports |
| Evaluate | ~12% | Benchmarking write-ups, design reviews |
| Create | ~8% | Final integrated navigation project |

The weighting is deliberate for a junior-level course: *Apply* dominates because
the content is implemented on hardware, while *Analyze* and *Evaluate* carry the
work of turning "it ran" into "I know why it ran, and when it won't." *Create*
concentrates in the final project, where the pieces become one system.
{: .fs-3 }
