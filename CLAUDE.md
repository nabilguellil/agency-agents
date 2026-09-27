# CLAUDE.md

## Task observer (one-skill-to-rule-them-all)

The `task-observer` skill lives in `.claude/skills/task-observer/`. Its
workspace is kept inside this repository so observations survive ephemeral
cloud sessions. `[REPO ROOT]` below means the top level of this git
repository (`git rev-parse --show-toplevel`; `/home/user/agency-agents` in
Claude Code cloud sessions) — resolve it that way, never from the current
working directory.

Before the first tool call of any session — and before writing or
proposing a plan, not merely before executing one — invoke the
task-observer skill AND execute its Session Start Protocol (storage
check, frontmatter scan, review trigger). Loading the skill and running
the protocol are separate steps; a session that loads the file and stops
has activated nothing. Any turn that will involve a tool call counts; do
not classify the session as "too simple" from its opening message.

Select skills on the DECISION the request is about, not on the artefact it
arrived as. Name what the user is deciding, then match the installed skill
descriptions against that — a request handed over as a file to review
still needs the skill whose description names its subject.

After completing each task, check the observation records written this
session and report a one-line summary (ids and titles, or "none logged
and why"). This is the activation backstop: it forces a look at the log,
so a session that silently skipped the protocol is discovered at the
first task boundary instead of never.

Loading a skill is not complete until you have queried the observation
log for OPEN observations naming it and read their bodies:
  find "[REPO ROOT]/.skill-observer/skill-observations/observation-log" -maxdepth 1 \
    -name '*.md' -exec grep -l "skill:.*<skill-name>" {} +
(Use find, not a bare *.md glob. Under zsh an unmatched glob is an error,
so on an empty log the command never runs and the enclosing block aborts.)
Apply their insights to the current work — meaning: let them change what
you do in THIS task. Editing the skill file, or writing the rule into any
other file a later session reads, is acting on the observation and waits
for the review. See "Log, don't act" in SKILL.md. Run this at every skill
load, however many skills load in one session.

The task-observer workspace for this project is:
  [REPO ROOT]/.skill-observer
Every path the skill uses derives from that root and nothing else:
  [REPO ROOT]/.skill-observer/skill-observations/observation-log/   (the log)
  [REPO ROOT]/.skill-observer/skill-observations/cross-cutting-principles.md
  [REPO ROOT]/.skill-observer/skill-updates/                        (staging root)
  [REPO ROOT]/.skill-observer/skill-updates/PENDING.md              (staging manifest)
Never resolve any of them from the current working directory. Never place
the workspace inside a skills-discovery directory (`.claude/skills/`). This
pinned path is the single shared location; do not derive one per session,
tool or checkout.

Persistence: cloud containers are wiped when a session ends, so any files
written under `.skill-observer/` must be committed and pushed along with the
session's other work. Keep the workspace in the dot-prefixed folder — a
non-dot top-level directory is treated as an agent division and fails
`scripts/check-divisions.sh`.
