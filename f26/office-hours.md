---
layout: default
title: Office Hours
nav_order: 5
permalink: /office-hours/
---

# Office hours
{: .no_toc }

Come with a specific question, the code or writing you've already tried, and
what you expected to happen. You do not need an appointment unless noted.

## Recurring hours

{% comment %}
  NOTE: this block deliberately uses plain comment tags rather than the
  whitespace-trimming (hyphenated) form. Trimming eats the blank lines around
  the block, which glues the table header onto the preceding heading and breaks
  the table. Also: never write literal Liquid tag syntax inside a comment —
  Liquid still tokenizes it and the build dies with a terminator error.

  Name and role are looked up from _data/staff.yml by the `staff` id, so this
  table cannot disagree with the staff cards on the home page. Only `when`,
  `where`, and `notes` come from _data/office_hours.yml.

  Liquid iterates a hash as [key, value] pairs, so `group[0]` is the staff group
  name ("instructor", "gsi", "ia") and `group[1]` is its array of people. The
  group name is what supplies the Role column.

  An unknown id renders a loud marker rather than a blank cell — and bin/build
  fails before it ever reaches a reader.

  A row for a service rather than a person (e.g. a room's drop-in hours) sets
  `who:` instead of `staff:`. That skips the staff.yml lookup entirely — the
  Who column shows the literal text and Role is left blank, since it isn't a
  staff role.
{% endcomment %}

| Who | Role | When | Where | Notes |
|:----|:-----|:-----|:------|:------|
{%- for oh in site.data.office_hours -%}
  {%- if oh.who %}
| {{ oh.who }} | — | {{ oh.when }} | {{ oh.where }} | {{ oh.notes | default: "—" }} |
  {%- else -%}
    {%- assign person = nil -%}
    {%- assign group_key = "" -%}
    {%- for group in site.data.staff -%}
      {%- for p in group[1] -%}
        {%- if p.id == oh.staff -%}
          {%- assign person = p -%}
          {%- assign group_key = group[0] -%}
        {%- endif -%}
      {%- endfor -%}
    {%- endfor -%}
    {%- case group_key -%}
      {%- when "instructor" -%}{%- assign role = "Instructor" -%}
      {%- when "gsi" -%}{%- assign role = "Graduate Student Instructor" -%}
      {%- when "ia" -%}{%- assign role = "Instructional Assistant" -%}
      {%- when "support" -%}{%- assign role = "Support" -%}
      {%- else -%}{%- assign role = "—" -%}
    {%- endcase %}
| {% if person %}{{ person.name }}{% else %}**⚠ unknown staff id `{{ oh.staff }}`**{% endif %} | {{ role }} | {{ oh.when }} | {{ oh.where }} | {{ oh.notes | default: "—" }} |
  {%- endif -%}
{%- endfor %}

## Live calendar

Cancellations, extra exam-week hours, and one-off changes appear here first.
Times are shown in **{{ site.course.calendar_timezone_label }}**.

{% include gcal.html mode="WEEK" height="640" title="Office hours calendar" %}

### Subscribe

Add these hours to your own calendar so changes sync automatically:

- **Google Calendar** — open the calendar above, then click the **+ Google Calendar**
  button in its bottom-right corner.
- **Apple Calendar / Outlook** — subscribe to the iCal feed:
  `https://calendar.google.com/calendar/ical/{{ site.course.calendar_id | url_encode }}/public/basic.ics`

{: .tip }
> The week before a deadline fills up fast. If you need a slot then, come
> early in the week rather than the day before.
