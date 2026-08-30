---
layout: default
title: Schedule
nav_order: 3
permalink: /schedule/
---

# Schedule
{: .no_toc }

Week-by-week topics, readings, and due dates.

{: .note }
> The schedule is subject to change (will announce in class).

<div class="schedule-table" markdown="0">
<table>
  <thead>
    <tr>
      <th>Week</th>
      <th>Dates</th>
      <th>Class and recommended progress</th>
      <th>PrairieLearn</th>
      <th>Due</th>
    </tr>
  </thead>
  <tbody>
  {%- for row in site.data.schedule %}
    <tr{% if row.break %} class="is-break"{% endif %}>
      <td>{{ row.week }}</td>
      <td>{{ row.dates }}</td>
      <td>
        {%- if row.lecture and row.lecture != "" -%}
          {%- assign lecture_url = "/lectures/" | append: row.lecture | append: "/" -%}
          <a href="{{ lecture_url | relative_url }}">{{ row.topic }}</a>
        {%- else -%}
          {{ row.topic }}
        {%- endif -%}
      </td>
      <td>{{ row.readings | default: "—" }}</td>
      <td>{{ row.due | default: "—" }}</td>
    </tr>
  {%- endfor %}
  </tbody>
</table>
</div>

## Key dates
{: .text-delta }

| Date | Event |
|:-----|:------|
| Sep. 10 | Checkpoint 0 — MBot Intro Assignment due |
| Sep. 21 | Add/drop deadline |
| Sep. 27 | Checkpoint 1 — Setpoint Challenge report and videos due |
| Oct. 25 | Checkpoint 2 — SLAM Challenge report and maze-run video due |
| Oct. 26 | Midterm written exam |
| Oct. 28 | Midterm oral exam |
| Nov. 18 | Checkpoint 3 — Escape Challenge report and video due |
| Nov. 24 | Checkpoint 4 — Camera Calibration video due |
| Dec. 9 | Final written and oral exams |
| Dec. 11 | Course evaluation due |
| Dec. 13 | Checkpoint 5 due |
