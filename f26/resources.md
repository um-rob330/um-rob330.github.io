---
layout: default
title: Resources
nav_order: 6
has_children: true
permalink: /resources/
---

# Resources
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Software setup

Everyone works from the same environment so that a bug you hit is a bug we can
reproduce. Do this before the first lab.

{: .warning }
> <!-- VERIFY: the stock MBot software stack is LCM-based, not ROS 2. Confirm
>      which image your section uses and pin the versions below. If you are
>      bridging LCM to ROS 2, add that step; if you are running a ROS 2-native
>      MBot image, note where students get it. -->
> **Version pinning is not filled in yet.** Confirm the MBot image and ROS 2
> distribution for this term before the first lab, and replace the `TODO`
> versions below.

### 1. Development machine

| Requirement | Version |
|:------------|:--------|
| OS | Ubuntu TODO LTS (native, or via VM) |
| ROS 2 | TODO distro |
| Python | 3.TODO |
| Git | any recent |

<!-- VERIFY: many courses provide a prebuilt VM or container to avoid a week of
     install support. If yours does, link it here and delete the manual steps. -->

### 2. ROS 2

Follow the official install for your Ubuntu release, then verify:

```bash
source /opt/ros/TODO/setup.bash
ros2 doctor          # should report no serious issues
ros2 topic list      # should not error
```

Add the source line to your `~/.bashrc` so every new shell has it.

### 3. Python environment

```bash
python3 -m venv ~/rob330-venv
source ~/rob330-venv/bin/activate
pip install -r requirements.txt   # numpy, opencv-python, matplotlib, scipy
```

{: .tip }
> Activate the venv *before* building, and use the same one all term. Mixing a
> system NumPy with a venv OpenCV produces import errors that look like code
> bugs but aren't.

### 4. MBot

<!-- VERIFY: fill in from your platform docs — flashing the image, network
     setup, and how students pair with a specific robot. -->

```bash
# TODO: clone the course MBot workspace
git clone TODO_MBOT_REPO ~/rob330
cd ~/rob330 && TODO_BUILD_COMMAND
```

Check the robot is alive before you debug anything else:

```bash
# TODO: adapt to your stack
ros2 topic echo /odom --once     # wheel odometry publishing?
ros2 topic echo /scan --once     # LIDAR publishing?
ros2 run rviz2 rviz2             # see the frames
```

{: .note }
> **Camera.** Modules 3 and 4 (sensor modeling, visual odometry) need one, and
> not every MBot configuration ships with a camera. Confirm your robot has the
> camera module attached and publishing before the visual-odometry lab.

### 5. Debugging tools you will actually use

| Tool | For |
|:-----|:----|
| `rviz2` | Seeing frames, scans, and paths — the fastest way to spot a transform error |
| `ros2 bag record` / `play` | Capturing a hardware run so you can debug offline instead of re-running the robot |
| `ros2 topic hz` | Checking a sensor is publishing at the rate you assumed |
| `tf2_tools view_frames` | Dumping the frame tree when a transform is missing or stale |
| `plotjuggler` | Plotting logged signals over time |

{: .tip }
> Record a bag of every graded run. When a result looks wrong at 2 am, replaying
> a bag beats rebooting a robot — and objective 7.5 asks you to make your
> experiments reproducible anyway.

## Reference material

| Resource | What it's good for |
|:---------|:-------------------|
| [Thrun, Burgard & Fox, *Probabilistic robotics*](https://robots.stanford.edu/probabilistic-robotics/) | The measurement and motion models behind modules 2, 3, and 6. Suggested, not required — see the [syllabus]({{ '/syllabus/#textbook-and-materials' | relative_url }}) |
| Szeliski, *Computer Vision: Algorithms and Applications* (free PDF) | Camera models, features, two-view geometry for modules 3–4 |
| Hartley & Zisserman, *Multiple View Geometry* | The definitive treatment of epipolar geometry; a reference, not a first read |
| LaValle, *Planning Algorithms* (free online) | Module 5 — configuration space and sampling-based planners |
| [ROS 2 documentation](https://docs.ros.org) | TF2, message types, CLI tools |
| [MBot software library (doxygen)](https://rob550-docs.github.io/doxygen_docs/) | Generated API reference for the MBot libraries |
| Grisetti et al., *A Tutorial on Graph-Based SLAM* | The clearest short introduction to the module 6 back end |

<!-- VERIFY: check which of these your library provides electronically, and
     whether you want to name specific chapters per week on the schedule. -->

## Supplementary reading

- Olson, *AprilTag: A robust and flexible visual fiducial system* — how fiducials
  give you ground truth without a motion-capture rig.
- Censi, *An ICP variant using a point-to-line metric* — a readable entry point
  to scan matching if module 6's front end interests you.
- Cadena et al., *Past, Present, and Future of SLAM: Towards the Robust-Perception
  Age* — where the field is, once you know the basics.

## Academic support

<!-- VERIFY: confirm each office name and URL — these move. Names below are
     current U-M offices as of writing. -->

- **[Services for Students with Disabilities (SSD)](https://ssd.umich.edu)** —
  accommodations; see the [syllabus]({{ '/syllabus/#accommodations' | relative_url }}).
- **[Counseling and Psychological Services (CAPS)](https://caps.umich.edu)** —
  free, confidential counseling for enrolled students.
- **[Sweetland Center for Writing](https://lsa.umich.edu/sweetland)** — one-on-one
  help with your lab write-ups, which are a real part of your grade.
- **Engineering academic advising** — TODO link for your program.
- **[Piazza]({{ site.course.piazza_url }})** — course
  discussion board. Ask here before email: your classmates see the answer too.

{: .note }
> Asking for help early is a strategy, not a confession. Every resource on this
> page exists because students before you used it.
