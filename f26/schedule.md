---
layout: default
title: Schedule
nav_order: 3
permalink: /schedule/
---

# Schedule
{: .no_toc }

Week-by-week topics, readings, and due dates. This table is generated from
`_data/schedule.yml` — edit that file, not this page.

{: .note }
> The schedule is subject to change. Changes are announced in class and
> reflected here; this page is always the current version.

<div class="schedule-table" markdown="0">
<table>
  <thead>
    <tr>
      <th>Week</th>
      <th>Dates</th>
      <th>Topic</th>
      <th>Readings</th>
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
| TODO | Add/drop deadline |
| TODO | Midterm exam |
| TODO | Final project proposal due |
| TODO | Final project due |
