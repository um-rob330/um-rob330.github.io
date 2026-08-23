---
layout: default
title: Checkpoint 5
nav_order: 6
parent: Checkpoints
permalink: /checkpoints/checkpoint5/
---

### Contents
* TOC
{:toc}

## Overview

In Checkpoint 2 you built a SLAM system whose only exteroceptive sensor was a
2D LIDAR: range measurements at a known height, matched against an occupancy
grid. It works, it is metrically accurate, and it cannot tell a wall from a
bookshelf.

This checkpoint replaces the LIDAR with the camera. You will estimate motion
from images, build a map with a visual SLAM system, compare it honestly against
the LIDAR map you already trust, and then use a vision-language model to
navigate to a goal named in plain English rather than given as grid coordinates.

The through-line: **a camera measures appearance, not geometry.** Everything that
follows — scale ambiguity, appearance-based loop closure, semantic maps, language
grounding — comes from that one difference.

{: .warning }
> **Compute.** None of the models in Tasks 5.2, 5.4, or 5.5 run in real time on
> the Raspberry Pi 5. The intended architecture is to keep the MBot as the sensor
> and actuator, and run heavy perception on a laptop or lab workstation as a
> separate ROS 2 node over the network. Record a bag on the robot, process it off
> board, and only close the loop on hardware once the pipeline works. Task 5.5
> describes the node split.
>
> <!-- TODO: confirm what compute students have. If the lab provides a GPU
>      workstation, name it and the access procedure here. If not, cap Task 5.4
>      and 5.5 at CPU-sized models and say so. -->

<!-- TODO: add a system diagram once the node split is finalized, e.g.
     assets/images/checkpoints/checkpoint5-architecture.png -->

## Task 5.1 Visual odometry from the MBot camera

Estimate the robot's incremental motion from consecutive camera frames, with no
LIDAR and no wheel encoders in the loop.

You already have the pieces from Checkpoint 4: a calibrated camera with known
intrinsics and distortion coefficients. Reuse that calibration — do not redo it.

### TODO

1. Work in the package `mbot_vslam`.
   <!-- TODO: confirm the package name and whether starter code is provided.
        If you ship a skeleton, list the files and their TODO markers the way
        Checkpoints 1–3 do. -->
   - Detect and describe features in each frame (ORB is a reasonable default;
     GFTT + optical flow is a lighter alternative on the Pi).
   - Match features between consecutive frames and reject outliers with RANSAC.
   - Recover the relative pose from the essential matrix, and chain the relative
     poses into a trajectory.
2. Compile and source your workspace:
    ```bash
    cd ~/mbot_ros_labs
    colcon build --packages-select mbot_vslam
    source install/setup.bash
    ```
   - {: .text-red-200} **Important: source the workspace in every terminal after
     each build, or ROS will keep running your old code.**
3. Publish your estimated trajectory so it can be visualized alongside
   `/odom` in RViz or Foxglove.

### The scale problem

A single camera cannot recover absolute scale. Translate one metre or ten and,
with the scene scaled to match, the images are identical — so your trajectory is
correct only up to an unknown multiplier.

Resolve it using something you already have: the wheel odometry from
Checkpoint 1 provides a metric distance over the same interval. Estimate the
scale factor that best aligns your visual translation with wheel-measured
translation over a straight segment, then apply it.

{: .required_for_report }
Plot your monocular visual-odometry trajectory against wheel odometry for the
same run, before and after scale correction. State the scale factor you
recovered and how you estimated it.

### Where it fails

Drive the robot through each of these and record what happens:

- **Pure rotation in place.** Almost no translation baseline, so triangulation
  is degenerate.
- **A blank wall.** Too few features to match.
- **Fast motion.** Motion blur destroys descriptors.

{: .required_for_report }
For each of the three cases above, describe the failure you observed and explain
it in terms of the geometry or the image formation — not just "it drifted".

## Task 5.2 Visual SLAM: mapping and loop closure

Visual odometry drifts without bound, exactly as wheel odometry did in
Checkpoint 1. A SLAM system adds a map and loop closures that correct
accumulated error.

The key difference from Checkpoint 2: your LIDAR system recognized a revisited
place by *geometry* (scan matching against the grid). A visual system recognizes
it by *appearance* — a bag-of-words or learned descriptor over the image.

### TODO

1. Run a visual SLAM system on a bag recorded from the MBot camera.
   <!-- TODO: pick and pin one. RTAB-Map is ROS 2-native, handles monocular +
        odometry input, and does appearance-based loop closure out of the box.
        ORB-SLAM3 is a common alternative with more setup friction.
        Record the exact package version and launch file here. -->
2. Drive a loop that returns to its starting point, and record the bag with
   camera, `/odom`, and `/scan` all present — you need the LIDAR for Task 5.3.
3. Identify the frame at which loop closure fires. Capture the trajectory
   immediately before and immediately after.

{: .required_for_report }
Show the trajectory before and after loop closure on the same axes. Explain what
the optimizer changed and why the correction is distributed across the whole
loop rather than applied only at the point of closure.

## Task 5.3 Compare V-SLAM against your LIDAR SLAM

You now have two independent estimates of the same run. Neither is ground truth,
which is the honest starting point for any comparison.

### TODO

1. Align the two trajectories and compute **absolute trajectory error (ATE)** and
   **relative pose error (RPE)**, treating your Checkpoint 2 LIDAR SLAM output as
   the reference.
   - The `evo` toolkit handles alignment and both metrics.
2. Report the numbers with units, and state clearly what the reference actually
   is — "error relative to LIDAR SLAM" is not "error relative to truth".

{: .required_for_report }
A table of ATE and RPE, plus two or three sentences on which system you would
deploy in the competition environment and why. A defensible answer may well be
"LIDAR, because the arena has low-texture walls" — the reasoning is what is
graded, not the choice.

## Task 5.4 Modern SLAM: learned and implicit maps

No implementation. This task is reading and analysis, because the map
representation you have used so far — an occupancy grid — is only one option, and
the field has largely moved on.

Read enough of the following to answer the questions below.

| Direction | Representative work | What it changes |
|:----------|:--------------------|:----------------|
| Learned dense front end | DROID-SLAM | Replaces hand-engineered matching with a learned iterative bundle adjustment |
| Neural implicit maps | iMAP, NICE-SLAM | The map is the weights of a network, not a grid |
| Gaussian-splatting SLAM | SplaTAM, MonoGS | The map is a set of 3D Gaussians; supports photorealistic re-rendering |
| Learned local features | SuperPoint + SuperGlue, LightGlue | Drop-in replacements for ORB that survive viewpoint and lighting change |
| Open-vocabulary maps | VLMaps, ConceptFusion | Map cells carry language-aligned features, not just occupancy |

<!-- TODO: replace with the specific papers and sections you want read, and add
     them to the schedule as that week's reading. -->

{: .required_for_report }
Answer both:
<br> 1. Pick one representation from the table and compare it to your occupancy
grid on three axes: memory footprint, what queries it answers cheaply, and how it
degrades when tracking is lost.
<br> 2. Name one thing every method in that table still needs that the classical
pipeline also needed. Explain why it has not gone away.

## Task 5.5 Vision-language navigation

Finally, remove grid coordinates from the interface. Instead of publishing a
`/goal_pose`, you will say *"go to the blue cone"* and the robot will work out
where that is.

{: .note }
> **Scope.** Full vision-language navigation — following multi-step route
> instructions in an unseen building — is an open research problem and is not what
> this task asks. You will build the tractable core of it: **language-conditioned
> goal selection**, in the style of VLMaps. Instructions with spatial relations
> ("the cone *behind* the table") are out of scope and are worth discussing in
> your report as a limitation.

### Architecture

The MBot stays thin; the model runs off board:

```
MBot (Pi 5)                        Laptop / workstation
────────────────                   ─────────────────────────
camera  ──/image_raw──────────────► open-vocab detector node
/scan, /odom ─────────────────────► semantic mapper node
                                        │
/goal_pose ◄────────────────────────────┘
     │
     └──► A* planner from Checkpoint 3 ──► motion controller
```

Nothing downstream of `/goal_pose` is new. You are adding a component that turns
language into a goal cell and handing it to the planner you already trust.

### TODO

1. **Build a semantic map.** For each keyframe, run an open-vocabulary detector
   (OWL-ViT or YOLO-World are reasonable CPU-feasible choices) or compute CLIP
   embeddings over image regions. Project each detection into your occupancy grid
   using the camera pose from Task 5.2 and range from `/scan`, and store the
   label or embedding at that cell.
   <!-- TODO: pin the model and version, and say whether weights are provided
        locally or downloaded. Note the download size for students on wifi. -->
2. **Ground a phrase to a cell.** Given a text query, embed it and score map
   cells by similarity to the stored features. Take the best-scoring reachable
   free cell as the goal.
3. **Publish and drive.** Publish that cell as `/goal_pose` and let the
   Checkpoint 3 planner execute. Verify the robot reaches the named object.
4. Test at least four phrases, including one object that is **not** present in
   the environment.

{: .required_for_report }
Report all four queries with the goal cell selected and whether the robot
reached the intended object. For the absent object, state what your system did —
and what it *should* do. A system that confidently drives to the best of several
bad matches is worse than one that declines to move, and explaining why is part
of this task.

### Discussion

{: .required_for_report }
Two or three paragraphs on where this pipeline breaks, drawing on what you
observed:
<br> 1. Which failures come from perception, and which from grounding?
<br> 2. What would you need in order to handle "go to the cone *nearest the
door*"?
<br> 3. Your semantic map is built from your V-SLAM poses. What happens to the
grounding when tracking is lost, and how would you detect that at runtime?

## Checkpoint Submission

<!-- TODO: set the due date, submission mechanics, and whether this is a team or
     individual checkpoint, matching the other checkpoints. Add the due date to
     _data/schedule.yml so it appears on the Schedule page. -->

Submit through [Canvas]({{ site.course.lms_url }}):

1. Your report, covering every `Required for report` item above.
2. Your code for Tasks 5.1, 5.2, and 5.5.
3. A short video of the robot reaching a goal named in natural language.

{: .deadline }
> Late work follows the policy on the
> [syllabus]({{ '/syllabus/#late-work' | relative_url }}).
