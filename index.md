---
layout: home
title: Home
nav_order: 1
description: "Syllabus and course information."
permalink: /
---

# {{ site.course.code }}: {{ site.course.name }}
{: .no_toc }

{{ site.course.term }}
{: .fs-5 .fw-300 }

<div class="course-facts" markdown="0">
  <dl><dt>Meets</dt><dd>{{ site.course.meeting_times }}</dd></dl>
  <dl><dt>Location</dt><dd>{{ site.course.location }}</dd></dl>
  <dl><dt>Credits</dt><dd>{{ site.course.credits }}</dd></dl>
  <dl><dt>Instructor</dt><dd><a href="mailto:{{ site.course.instructor_email }}">{{ site.course.instructor }}</a></dd></dl>
</div>

[View the schedule](/schedule/){: .btn .btn-primary .mr-2 }
[Office hours](/office-hours/){: .btn }

---

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Course description

TODO — one or two paragraphs describing the course: what problem it addresses,
what students will be able to do by the end, and how it fits into the program.

## Learning objectives

By the end of this course, you will be able to:

1. TODO objective one
2. TODO objective two
3. TODO objective three

## Prerequisites

TODO — required courses, and the specific skills you actually expect (e.g.
"comfortable writing a 200-line Python program", "linear algebra through
eigenvectors").

## Textbook and materials

| Type | Title | Required? |
|:-----|:------|:----------|
| Textbook | TODO Title, Author, Edition | Required |
| Reference | TODO Title | Optional |

All readings not in the textbook are linked from the [schedule](/schedule/).

## Grading

| Component | Weight |
|:----------|-------:|
| Assignments | 40% |
| Midterm | 20% |
| Final project | 30% |
| Participation | 10% |
| **Total** | **100%** |

Letter grades: A ≥ 93, A− ≥ 90, B+ ≥ 87, B ≥ 83, B− ≥ 80, C+ ≥ 77, C ≥ 73,
C− ≥ 70, D ≥ 60, F < 60.
{: .fs-3 }

## Course policies

### Late work

TODO — e.g. "Each student has four late days for the term, usable in
one-day increments on assignments. Past that, late work loses 10% per day."

### Collaboration and academic integrity

TODO — state clearly what collaboration is allowed, what must be your own
work, and how AI tools may or may not be used.

{: .policy }
> Work you submit must be your own. Cite every source and collaborator.
> When in doubt, ask before you submit — not after.

### Accommodations

TODO — link to your institution's disability services office and state that
students should contact you early in the term.

## Getting help

1. Bring it to [office hours](/office-hours/) — the fastest path.
2. Post on the course discussion board so classmates benefit from the answer.
3. Email [{{ site.course.instructor_email }}](mailto:{{ site.course.instructor_email }})
   with `{{ site.course.code }}` in the subject line.
