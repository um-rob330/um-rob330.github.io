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

| Who | Role | When | Where | Notes |
|:----|:-----|:-----|:------|:------|
{%- for oh in site.data.office_hours %}
| {{ oh.who }} | {{ oh.role }} | {{ oh.when }} | {{ oh.where }} | {{ oh.notes | default: "—" }} |
{%- endfor %}

## Live calendar

Cancellations, extra exam-week hours, and one-off changes appear here first.
Times are shown in **{{ site.course.calendar_timezone }}**.

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

## Can't make any of these times?

Email [{{ site.course.instructor_email }}](mailto:{{ site.course.instructor_email }})
with two or three windows that work for you and we'll find one.
