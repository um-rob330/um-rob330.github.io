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

## Prerequisites

Advisory prerequisite: none.

Enforced Prerequisite: EECS 280 and (IOE 265 or EECS 301 or BIOMEDE 241) and
(ROB 101 or MATH 214 or MATH 217 or MATH 417 or MATH 419). Minimum grade
requirement of “C-” for enforced prerequisite.

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
