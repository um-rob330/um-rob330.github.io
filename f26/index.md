---
layout: home
title: Home
nav_order: 1
description: "ROB 330 at The University of Michigan — full-stack autonomous navigation and mapping for mobile robots."
permalink: /
---

<div class="hero">
  {%- if site.course.banner and site.course.banner != "" -%}
  <div class="hero__media">
    <img
      class="hero__img hero__img--motion"
      src="{{ site.course.banner | relative_url }}"
      alt="{{ site.course.banner_alt }}">
    {%- if site.course.banner_static and site.course.banner_static != "" -%}
    <img
      class="hero__img hero__img--static"
      src="{{ site.course.banner_static | relative_url }}"
      alt="{{ site.course.banner_alt }}">
    {%- endif -%}
  </div>
  {%- else -%}
  <div class="hero__media hero__media--placeholder">
    <span class="hero__placeholder-text">
      Banner image / <code>.gif</code> goes here — set <code>course.banner</code> in <code>_config.yml</code>
    </span>
  </div>
  {%- endif -%}

  <h1 class="hero__title">{{ site.course.code }} {{ site.semester.label }} at {{ site.course.institution }}</h1>
  <div class="hero__rule" aria-hidden="true"></div>
</div>

{{ site.course.description_catalog }}
{: .fs-5 .fw-300 .hero__lede }

[Syllabus]({{ '/syllabus/' | relative_url }}){: .btn .btn-primary .mr-2 }
[Schedule]({{ '/schedule/' | relative_url }}){: .btn }

---

## Course staff

{% include staff_group.html group=site.data.staff.instructor heading="Instructor" %}

{% include staff_group.html group=site.data.staff.gsi heading="Graduate Student Instructor" %}

{% include staff_group.html group=site.data.staff.ia heading="Instructional Assistants" %}

{% include staff_group.html group=site.data.staff.support heading="Support" %}

---

## Office hours

Cancellations and one-off changes appear here first. Times are shown in
**{{ site.course.calendar_timezone_label }}**.

{% include gcal.html mode="WEEK" height="600" title="ROB 330 office hours calendar" %}

See the [office hours page]({{ '/office-hours/' | relative_url }}) for the recurring schedule by staff
member, room and Zoom details, and how to subscribe to this calendar.
{: .fs-3 }
