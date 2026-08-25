---
layout: default
title: Syllabus
nav_order: 2
description: "Course description, learning objectives, grading, and policies."
permalink: /syllabus/
---

{%- assign lead = site.data.staff.instructor | first -%}

# Syllabus
{: .no_toc }

{{ site.course.code }} · {{ site.course.name }} · {{ site.semester.label }}
{: .fs-5 .fw-300 }

<div class="course-facts" markdown="0">
  <dl><dt>Meets</dt><dd>{{ site.course.meeting_times }}</dd></dl>
  <dl><dt>Location</dt><dd>{{ site.course.location }}</dd></dl>
  <dl><dt>Credits</dt><dd>{{ site.course.credits }}</dd></dl>
  <dl><dt>Instructor</dt><dd><a href="mailto:{{ lead.email }}">{{ lead.name }}</a></dd></dl>
</div>

[View the schedule]({{ '/schedule/' | relative_url }}){: .btn .btn-primary .mr-2 }
[Office hours]({{ '/office-hours/' | relative_url }}){: .btn }

---

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Course description

{{ site.course.description_catalog }}
{: .fs-5 .fw-300 }

### What that looks like week to week
{: .text-delta }

<!-- The paragraph above is the official catalog description, pulled from
     course.description_catalog in _config.yml. The two paragraphs below are the
     expanded version — delete them if you'd rather the syllabus carry only the
     catalog text. -->

This course develops a full-stack autonomous navigation and mapping system for
a mobile robot, from wheel encoders to a complete map-and-navigate demonstration.
We work bottom-up: pose estimation by dead reckoning from odometry, probabilistic
measurement models for LiDAR, path planning over occupancy grids, and
simultaneous localization and mapping (SLAM).

We will implement mapping, localization, and navigation algorithms in physical
hardware using the [MBots](https://mbot.robotics.umich.edu/).

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

## Prerequisites

**Advisory prerequisite:** none.

**Enforced prerequisites:** all three groups below, with a minimum grade of
**C−** in each.

| Requirement | Satisfied by | What this course does with it |
|:------------|:-------------|:------------------------------|
| Programming and data structures | **EECS 280** | You will write, debug, and profile substantial code against real sensor data (objectives 2.2, 4.2, 5.2, 6.3) |
| Probability and statistics | **IOE 265**, **EECS 301**, or **BIOMEDE 241** | Measurement and motion models, noise and outlier terms, filtering, and error characterization (1.1, 2.4, 3.2, 6.1) |
| Linear algebra | **ROB 101**, **MATH 214**, **217**, **417**, or **419** | Rigid-body transforms in SE(2)/SE(3), least squares, essential-matrix decomposition (1.2, 3.3, 4.1, 4.3) |

### What that means in practice
{: .text-delta }

Coming in, you should be comfortable:

- Writing and debugging a program of a few hundred lines, and reading someone
  else's — you will be handed a partial stack and asked to complete it.
- Multiplying and inverting matrices, and knowing what an eigenvector and a
  least-squares solution are. You do not need to have seen SVD; we introduce it
  where it's needed.
- Reasoning with a probability distribution, a conditional probability, and a
  Gaussian — its mean, its covariance, and what a covariance's off-diagonal
  terms mean.

<!-- VERIFY: this paragraph is a promise to students about what they can arrive
     not knowing. Adjust it to match how much scaffolding your labs actually
     provide. Note the language gap: EECS 280 is taught in C++, so if the labs
     are Python-based, most students will be learning Python alongside the
     robotics content — budget lab time accordingly or say so here. -->
You are **not** expected to arrive knowing ROS 2, and no prior robotics course is
required. We build up the frame conventions, tooling, and message plumbing in the
first weeks — see [Resources]({{ '/resources/' | relative_url }}) for the setup
you'll do before the first lab.

{: .tip }
> If you satisfy the prerequisites on paper but any of the practical list above
> feels shaky, come to [office hours]({{ '/office-hours/' | relative_url }}) in
> week 1 rather than week 6. The material compounds — module 6 assumes you have
> module 2 working — so early gaps get expensive.

## Textbook and materials

**There is no required textbook for this course**; however, readings may be
suggested from the textbook
[Thrun, S., Burgard, W., & Fox, D. (2005). *Probabilistic robotics*. The MIT
Press.](https://robots.stanford.edu/probabilistic-robotics/) The instructors may
provide additional references.

Suggested readings are listed week by week on the
[schedule]({{ '/schedule/' | relative_url }}), and further references are
collected on the [Resources]({{ '/resources/' | relative_url }}) page.

{: .note }
> Nothing you need to buy. Where a reading is assigned, it will be linked or
> distributed — check the [schedule]({{ '/schedule/' | relative_url }}) rather
> than assuming you need the book.

## Grading

| Component | Weight |
|:----------|-------:|
| Checkpoints | 40% |
| Midterm | 20% |
| Final project | 30% |
| Participation | 10% |
| **Total** | **100%** |

Letter grades: A ≥ 93, A− ≥ 90, B+ ≥ 87, B ≥ 83, B− ≥ 80, C+ ≥ 77, C ≥ 73,
C− ≥ 70, D ≥ 60, F < 60.
{: .fs-3 }

## Course policies

### Late work

Checkpoints lose **10% of the earned score per day late**, counted in whole days
from the deadline, for up to **four days**. After four days the checkpoint is not
accepted and receives no credit. A submission at 12:01 am is one day late.

<!-- VERIFY: decide whether weekend days count toward the penalty, and delete
     whichever sentence below does not apply. -->
Weekend days count the same as weekdays.

{: .warning }
> **Hardware failure is not automatically an extension**, but it is also not
> your fault. If your robot breaks, a sensor fails, or the lab is inaccessible,
> tell the staff **before the deadline** — we will work out a revised date. What
> does not work is reporting it afterward, because by then we cannot distinguish
> a hardware problem from a scheduling one.

Every deadline is 11:59 pm Ann Arbor time on the date listed on the
[schedule]({{ '/schedule/' | relative_url }}).

### Collaboration and academic integrity

Robotics is a collaborative field and debugging a robot with someone else is one
of the better ways to learn. The line this course draws:

**Encouraged**

- Discussing concepts, algorithms, and derivations with anyone.
- Helping a classmate diagnose a hardware or environment problem — a
  miswired encoder, a dead battery, a build error.
- Comparing *results* and asking why yours differ.

**Not allowed**

- Submitting code you did not write, including a classmate's, a previous term's,
  or code from a public repository, unless the checkpoint says otherwise.
- Sharing your solution code with a classmate who has not submitted yet.
- Submitting data you did not collect. **Every trajectory, scan, and image you
  report must come from your own robot on your own run.** This is the integrity
  rule most specific to this course, and the easiest one to violate without
  meaning to — borrowing a lab partner's rosbag because your run failed is
  fabrication, not collaboration.

**Always**

- Name every collaborator and cite every outside source in your submission's
  `README`. Attribution costs you nothing; its absence is the problem.

<!-- VERIFY: this is the middle-ground AI policy. Tighten or loosen it to match
     what you actually intend to enforce, and check it against any department- or
     college-level AI policy that supersedes it. -->
**Generative AI tools** (ChatGPT, Claude, Copilot, and similar) may be used to
explain concepts, review your own code, and help interpret error messages. They
may **not** be used to generate code or written analysis that you submit as your
own. If you use them at all, say so in your `README` — one line naming the tool
and what you used it for. Undisclosed use is treated as any other undisclosed
source.

{: .policy }
> Work you submit must be your own, and so must your data. Cite every source and
> collaborator. When in doubt, ask before you submit — not after.

Suspected violations are reported through the
<!-- VERIFY: name the correct body for your school — e.g. the College of
     Engineering Honor Council for CoE courses. -->
College of Engineering Honor Council.

### Accommodations

The University of Michigan is committed to equal access. If you have a
disability, chronic condition, or temporary impairment that affects your
participation in this course, you are entitled to accommodations.

Work with
<!-- VERIFY: confirm the office name and URL — these change. As of writing:
     Services for Students with Disabilities, ssd.umich.edu -->
[Services for Students with Disabilities (SSD)](https://ssd.umich.edu) to
establish a Verified Individualized Services and Accommodations (VISA) letter,
then send it to the instructor. **Contact us as early in the term as you can.**
Accommodations are not applied retroactively, and some — extended time on a
hardware lab, or alternative arrangements for lab access — take planning to set
up well.

You do not need to disclose your diagnosis to anyone in this course, including
the instructor. The VISA letter is sufficient.

{: .note }
> This applies to more than exams. If any part of the course — lab bench height,
> equipment handling, timed hardware demos, visual inspection of a robot's
> behavior — creates a barrier, tell us. Some of it we can simply change.

## Getting help

1. Come to class!
2. Bring it to [office hours]({{ '/office-hours/' | relative_url }}) — the fastest path.
3. Post to [Piazza]({{ site.course.piazza_url }}) so classmates benefit from the answer.
4. Email course staff with {{ site.course.code }} in the subject line.
