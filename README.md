# Course website

A [Jekyll](https://jekyllrb.com) site using the
[Just the Docs](https://just-the-docs.com) theme, built for GitHub Pages, with
an embedded Google Calendar for office hours.

## What's here

```
_config.yml              site + course settings (start here)
index.md                 home page / syllabus
schedule.md              schedule table, generated from _data/schedule.yml
office-hours.md          office hours table + live Google Calendar
resources.md             software setup, references, support services
_lectures/               one Markdown file per lecture  -> /lectures/<slug>/
_assignments/            one Markdown file per assignment -> /assignments/<slug>/
_data/schedule.yml       the week-by-week schedule (edit this, not the table)
_data/office_hours.yml   recurring office hours
_includes/gcal.html      reusable Google Calendar embed
_sass/custom/custom.scss visual customizations
.github/workflows/       builds and deploys on every push to main
```

## First-time setup

### 1. Fill in `_config.yml`

Replace every `TODO` and `USERNAME`. The two that matter most:

- `url` / `baseurl` — for a repo named `<username>.github.io`, use
  `baseurl: ""`. For a project repo like `<username>/my-course`, use
  `baseurl: "/my-course"`.
- `course.calendar_id` — see step 3.

Then search the repo for remaining placeholders:

```bash
grep -rn "TODO\|USERNAME" --include="*.md" --include="*.yml" .
```

### 2. Turn on GitHub Pages

Push to GitHub, then: **Settings → Pages → Build and deployment → Source →
GitHub Actions**. The included workflow does the rest; every push to `main`
redeploys. The first run takes about a minute.

### 3. Wire up the office-hours calendar

1. In Google Calendar, create a calendar just for office hours (don't use your
   personal one — the whole calendar becomes public).
2. **Settings → [your calendar] → Access permissions** → check
   **Make available to public**. Set the dropdown to
   *See only free/busy* if you want times without event titles, or
   *See all event details* to show titles.
3. Scroll to **Integrate calendar** and copy the **Calendar ID**
   (looks like `c_a1b2c3...@group.calendar.google.com`). Paste it into
   `course.calendar_id` in `_config.yml`, and set
   `course.calendar_timezone` to an
   [IANA timezone](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)
   such as `America/New_York`.

Until you do this, the office-hours page shows a labeled placeholder box
instead of a broken iframe.

## Adding content

**A lecture** — create `_lectures/lecture-02.md`, copy the front matter from
`lecture-01.md`, and bump `nav_order`. To link it from the schedule, set
`lecture: lecture-02` on that week's row in `_data/schedule.yml`.

**An assignment** — same pattern in `_assignments/`. The `<span class="pill">`
at the top has three states: `pill--open`, `pill--soon`, `pill--closed`.

**A schedule week** — add a row to `_data/schedule.yml`. Set `break: true` for
no-class weeks and they render greyed out.

**A callout** — put `{: .note }` (or `.tip`, `.deadline`, `.warning`,
`.policy`) on the line *after* a blockquote:

```markdown
{: .deadline }
> Project proposals are due Friday.
```

## Local preview

Optional — GitHub Actions builds the site for you. But if you want to see
changes before pushing:

```bash
bundle install
bundle exec jekyll serve --livereload
# -> http://127.0.0.1:4000
```

Jekyll 4 needs **Ruby ≥ 3.0**. Your system Ruby is 2.6, which is too old, so
install a newer one first:

```bash
brew install ruby
echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
exec zsh
```

Or with a version manager (cleaner if you juggle Ruby projects):

```bash
brew install rbenv && rbenv init
rbenv install 3.3.5 && rbenv local 3.3.5
```

`Gemfile.lock` is gitignored on purpose so the Actions build always resolves
fresh gems; commit it if you'd rather pin exact versions.
