# AGENTS.md — Simple Pi Stats Dashboard

Tool-agnostic project brief for AI coding agents (Claude Code, Codex, Cursor,
Copilot, and anything else that reads `AGENTS.md`) working in this repository.

## Project overview

A Grafana dashboard for monitoring Raspberry Pi system performance, paired
with the [Telegraf](https://www.influxdata.com/time-series-platform/telegraf/)
agent config that feeds it. There is no application code and no build step —
the repo ships two config artifacts:

- **`Simple Pi Stats.json`** — a Grafana dashboard export. This is the actual
  deliverable; people import it into their own Grafana instance.
- **`telegraf.conf`** — a reference Telegraf agent config that collects the
  CPU, disk, network, memory, and system metrics the dashboard's panels
  query, and writes them to InfluxDB.

Metrics flow: Telegraf (using `telegraf.conf`) → InfluxDB → Grafana panel
queries defined in `Simple Pi Stats.json`.

## Repo structure

```
.
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   └── feature_request.md
│   ├── dependabot.yml               # GitHub Actions updates only, monthly, grouped
│   └── workflows/
│       ├── cron_branch_cleaner.yml  # daily: deletes merged branches >7 days old off develop/master
│       └── cron_stale_cleanup.yml   # daily: labels issues stale after 30 days, closes 5 days later
├── Dashboard.jpg                    # screenshot embedded in README
├── LICENSE                          # Unlicense (public domain)
├── README.md
├── Simple Pi Stats.json             # the Grafana dashboard export (the deliverable)
└── telegraf.conf                    # reference Telegraf agent config
```

## Non-negotiables

- **This is a config/data repo, not an application.** No package manager, no
  build step, no test suite. "Testing" a change means importing the dashboard
  JSON into a real (or throwaway) Grafana instance, or pointing Telegraf at
  `telegraf.conf` and confirming it starts cleanly.
- **`Simple Pi Stats.json` is a Grafana export.** When adding or editing a
  panel, export via Grafana's "Export for sharing externally" so the
  `__inputs`/`__requires` datasource-variable blocks stay intact — editing the
  JSON by hand and dropping those breaks the datasource picker on import.
- **`telegraf.conf` and the dashboard are coupled.** Every panel query
  assumes a specific Telegraf input plugin is enabled (`inputs.cpu`,
  `inputs.disk`, `inputs.net`, etc.). Removing or renaming an input plugin
  silently breaks whatever panel reads it — check both files together.
- **Don't commit secrets.** `telegraf.conf`'s `[[outputs.influxdb]]` block
  currently points at a private LAN address (`192.168.0.242`) from the
  original setup — treat it as a placeholder to call out in docs, not a
  value to "fix" toward some other address you invent, and never replace it
  with a real credential-bearing URL.
- Don't add a build step, linter config, or package manifest "to be safe" —
  the two-file, no-tooling shape is intentional for a dashboard/config repo
  this small.

## Commit conventions

**Every commit must follow [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/).**

```
<type>(<optional scope>): <imperative description>

<optional body explaining why>

<optional footers>
```

- Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`,
  `ci`, `chore`, `revert`.
- Scopes used here: `dashboard`, `telegraf`, `docs`, `ci`, `deps`.
- Imperative mood, no trailing period, subject ≤ 72 chars.
- Breaking = a panel that requires a Telegraf input plugin not already
  documented as required, or a change to the InfluxDB output shape existing
  Telegraf configs would need to change to match. Use `type(scope)!:` and/or
  a `BREAKING CHANGE:` footer.
- One logical change per commit; PR titles use the same format.

```
feat(dashboard): add swap usage panel
fix(telegraf): correct percpu flag on inputs.cpu
docs: document the InfluxDB output URL placeholder
ci(deps): bump branch cleaner action to v3
```

## CI / automation

- **Dependabot** (`.github/dependabot.yml`) only tracks the `github-actions`
  ecosystem — the dashboard JSON and `telegraf.conf` aren't package manifests
  it can version. Runs monthly, grouped into one PR, commit prefix `ci`.
- **`cron_branch_cleaner.yml`** runs daily and deletes branches merged into
  `develop`/`master` more than 7 days ago. Don't rely on a merged feature
  branch surviving past that window.
- **`cron_stale_cleanup.yml`** runs daily and marks issues stale after 30 days
  of inactivity, closing them 5 days after that.

## License

[Unlicense](LICENSE) — public domain. Contributions are accepted under the
same terms.
