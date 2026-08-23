# ROB 330 — course websites

One repository holding every offering of ROB 330 (Localization, Mapping, and
Navigation — The University of Michigan). Each semester is a self-contained
[Jekyll](https://jekyllrb.com) site using the
[Just the Docs](https://just-the-docs.com) theme, published under its own URL:

| Offering | URL | Source |
|:---------|:----|:-------|
| Fall 2026 | `um-rob330.github.io/f26/` | `f26/` |

The root, `um-rob330.github.io`, is a generated landing page listing all offerings.
Past semesters stay live and unchanged forever — rolling over to a new term adds
a directory, it doesn't replace one.

## Repo layout

```
semesters.yml            the list of offerings (single source of truth)
bin/build                builds every semester + the landing page into _site/
bin/new-semester         creates next semester from the current one
Gemfile                  shared gem versions for all semesters
.github/workflows/       builds and deploys on every push to main
f26/                     Fall 2026 site — a complete Jekyll source tree
```

Inside a semester directory:

```
_config.yml                    semester block, course info, theme settings
index.md                       landing page: banner, staff, calendar
syllabus.md                    description, learning objectives, grading, policies
schedule.md                    schedule table, generated from _data/schedule.yml
office-hours.md                hours table + calendar + iCal subscribe links
resources.md                   software setup, references, support services
_lectures/                     one file per lecture     -> /f26/lectures/<slug>/
_checkpoints/                  one file per checkpoint  -> /f26/checkpoints/<slug>/
_data/staff.yml                instructor / GSI / IAs shown on the home page
_data/schedule.yml             week-by-week schedule (edit this, not the table)
_data/office_hours.yml         recurring office hours
_includes/gcal.html            reusable Google Calendar embed
_includes/staff_group.html     renders one staff role as circular cards
_includes/footer_custom.html   site footer
_sass/color_schemes/umich.scss U-M maize & blue palette
_sass/custom/custom.scss       hero, staff cards, schedule table, pills
assets/images/                 banner .gif; staff/ holds headshots
```

Page order in the sidebar comes from `nav_order` in each page's front matter:
Home 1 → Syllabus 2 → Schedule 3 → Office Hours 4 → Resources 5. The `lectures`
and `checkpoints` collections form their own nav groups.

## The one rule

**A semester's directory name, its `baseurl`, and its `semester.code` must all
agree.** `f26/` must declare `baseurl: "/f26"` and `semester.code: "f26"`.

`bin/build` checks this before building and stops with an explanatory error if
they disagree. The reason it's worth a hard check: the output is nested at
`_site/f26/`, so if `baseurl` says anything else, every internal link on the
site points somewhere that doesn't exist — and the build itself still succeeds,
so nothing tells you until you click a link on the live site.

## Rolling over to a new semester

```bash
bin/new-semester w27 "Winter 2027"
```

That copies the current semester's directory, rewrites the `semester:` block and
`baseurl` in the new `_config.yml`, and registers it in `semesters.yml` as the
current offering. It prints a checklist afterward.

It deliberately does **not** touch course content — last term's dates and staff
are copied verbatim, because a wrong-but-plausible date is worse than an
obviously stale one. Review these before announcing the site:

- `w27/_data/schedule.yml` — week dates and topics
- `w27/_data/staff.yml` — instructor, GSI, IAs, and their headshots
- `w27/_data/office_hours.yml` — recurring hours
- `w27/_config.yml` — `calendar_id`, `meeting_times`, `location`
- `w27/_checkpoints/*.md` — `due:` dates; `w27/_lectures/*.md` — `date:` fields
- `w27/assets/images/` — banner and staff photos

Then `bin/build w27` locally, or just push — CI builds every semester.

To build from a term other than the current one: `--from f26`.

## First-time repo setup

1. The repository must be named **`um-rob330.github.io`** and owned by the
   `um-rob330` user or organization. That is what makes the root URL
   `um-rob330.github.io`.
2. **Settings → Pages → Build and deployment → Source → GitHub Actions.**
   This is not optional and it is the single most likely thing to be wrong.
   If Source is left on *Deploy from a branch*, GitHub runs its **legacy Pages
   builder** instead of `.github/workflows/pages.yml`, and the build fails with:

   ```
   The github-pages gem can't satisfy your Gemfile's dependencies.
   ```

   The legacy builder is pinned to Jekyll 3.10 via the `github-pages` gem, so it
   cannot install the Jekyll 4 + Just the Docs versions this site needs. It also
   treats the repo root as one Jekyll site, which would flatten the per-semester
   structure even if the gems did resolve. Telltale signs in the failing log:
   `github-pages v232`, `jekyll v3.10.0`, `Theme: jekyll-theme-primer`.
3. Push to `main`. The workflow builds every semester and deploys. First run
   takes about a minute.

## Per-semester setup

### `_config.yml`

Replace the `TODO` values. `semester:` at the top is the only block that changes
between offerings, and the term is stated there once — everything else reads
`{{ site.semester.label }}`, so there is no second place to forget.

Find remaining placeholders:

```bash
grep -rn "TODO" --include="*.md" --include="*.yml" f26/
```

### Office-hours calendar

1. In Google Calendar, create a calendar **just for office hours** — don't use a
   personal one, since making it public exposes the entire calendar.
2. **Settings → [your calendar] → Access permissions** → check **Make available
   to public**. Choose *See only free/busy* for times without event titles, or
   *See all event details* to show titles.
3. Scroll to **Integrate calendar**, copy the **Calendar ID** (looks like
   `c_a1b2c3...@group.calendar.google.com`), and set `course.calendar_id`.
   `course.calendar_timezone` is already `America/Detroit`.

Until you do this, the calendar renders a labeled placeholder rather than a
broken iframe. It appears on both the home page and `/office-hours/`.

### Banner .gif

1. Put the file in `f26/assets/images/` (e.g. `banner.gif`).
2. Set `course.banner: "/assets/images/banner.gif"`.

The banner slot is pre-sized at 16:5, so adding the image causes no layout
shift. If it's animated, also set `course.banner_static` to a still frame — that
is shown to visitors whose OS is set to "reduce motion", which CSS cannot
otherwise honor for a GIF. Set `course.banner_alt` to a description, or leave it
`""` if the banner is purely decorative (correct for decoration — screen readers
then skip it).

### Course staff

Edit `_data/staff.yml`. Four groups — `instructor`, `gsi`, `ia`, `support` — render
under the headings *Instructor*, *Graduate Student Instructor*, *Instructional
Assistants*, and *Support*. Each person needs a unique `id`, which `_data/office_hours.yml`
references so names cannot drift between the cards and the hours table. Add or
remove list entries; the grid reflows on its own.

**Headshots:** drop a square image in `assets/images/staff/` and set that
person's `photo:` to the filename. Until then a navy circle with their initials
is drawn, so nothing looks broken. ~400×400 px is plenty; non-square images are
center-cropped to the circle rather than squashed.

The first `instructor` entry also supplies the contact links on the syllabus and
office-hours pages, so keep it filled in.

## Adding content

**A lecture** — create `f26/_lectures/lecture-02.md`, copy the front matter from
`lecture-01.md`, bump `nav_order`. To link it from the schedule, set
`lecture: lecture-02` on that week's row in `_data/schedule.yml`.

**A checkpoint** — same pattern in `_checkpoints/`. The `<span class="pill">` at
the top has three states: `pill--open`, `pill--soon`, `pill--closed`.

**A schedule week** — add a row to `_data/schedule.yml`. Set `break: true` for
no-class weeks and the row renders greyed out.

**A callout** — put `{: .note }` (or `.tip`, `.deadline`, `.warning`, `.policy`)
on the line *after* a blockquote:

```markdown
{: .deadline }
> Project proposals are due Friday.
```

**Internal links must go through `relative_url`**, because the site is served
from `/f26/` rather than the domain root:

```markdown
[the schedule]({% raw %}{{ '/schedule/' | relative_url }}{% endraw %})
```

A bare `[the schedule](/schedule/)` resolves to `um-rob330.github.io/schedule/` and
404s. Same for images: `{% raw %}{{ '/assets/images/x.png' | relative_url }}{% endraw %}`.

## Local preview

```bash
bundle install
bin/build                       # all semesters -> _site/
bundle exec jekyll serve -s f26 # live-reload one semester
```

`jekyll serve -s f26` honors that semester's `baseurl`, so the site is at
**http://127.0.0.1:4000/f26/** — not `:4000/`.

Jekyll 4 needs **Ruby ≥ 3.0**; macOS system Ruby (2.6) is too old:

```bash
brew install ruby
echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
exec zsh
```

Or with a version manager:

```bash
brew install rbenv && rbenv init
rbenv install 3.3.5 && rbenv local 3.3.5
```
