# Acme SaaS fake GitHub history demo

This repository contains a synthetic GitHub history for the J1 "Audit DevOps" demo.

The goal is to give the instructor a repo that looks like the Acme SaaS case from the slides:

- 30 devs on a B2B SaaS.
- Production releases roughly every 3 months.
- 1 incident on 3 deployments.
- Manual release knowledge concentrated in one senior.
- Dev and Ops blame each other.
- Automation arrives late in the story.

The history is intentionally fake, but the commits and tags are real Git objects. It is designed to support a live DORA audit in front of students.

## How to use it in class

Open the GitHub repo and show these views:

1. **Commits**: show that work accumulates between release commits.
2. **Tags**: show quarterly releases and hotfix tags.
3. **Actions**: show the CI workflow as the "improvement" that arrives late.
4. **Files**: show the app is small; the delivery process is the interesting part, not the code.

Then ask students to estimate:

- Deployment Frequency.
- Lead Time for Changes.
- MTTR.
- Change Failure Rate.

Important: use Git commit/tag dates for the synthetic timeline. GitHub Releases were created after the fact for navigation convenience, so their GitHub "published" timestamps reflect the setup date, not the fake Acme production dates.

## Suggested commands

```bash
git log --oneline --decorate --date=short --pretty=format:'%h %ad %d %s'
git tag --list --sort=creatordate
git show v1.0.0 --stat
git show v1.0.1 --stat
```

If the repo has been pushed to GitHub:

```bash
gh repo view
gh run list --limit 10
gh api 'repos/:owner/:repo/tags'
```

Avoid using `gh release list` for date calculations in this demo. It shows when the GitHub Release objects were created, not the backdated synthetic tag dates.

## Synthetic release timeline

| Date | Git object | Meaning | DORA signal |
|---|---|---|---|
| 2025-10-31 | `v1.0.0` | Quarterly production drop | Low deployment frequency |
| 2025-11-01 | `v1.0.1` | Urgent hotfix after release | Change failure |
| 2025-11-02 | `v1.0.2` | Rollback of dashboard export | MTTR / recovery proxy |
| 2026-01-30 | `v1.1.0` | Next quarterly production drop | Long lead time |
| 2026-02-01 | `v1.1.1` | Login regression hotfix | Change failure |
| 2026-04-30 | `v1.2.0` | Third quarterly production drop | Low deployment frequency |
| 2026-05-01 | `v1.2.1` | Healthcheck/deploy hotfix | Recovery signal |

## Instructor narrative

Start with this framing:

> "This repo is not here to impress us technically. It is deliberately small. The interesting part is the delivery pattern: long gaps, big releases, hotfixes after release, and automation arriving only after repeated pain."

Then guide students:

1. Count releases over the observed period.
2. Identify which releases caused follow-up hotfixes or reverts.
3. Compare the gap between feature commits and release tags.
4. Decide which data is missing.

## Expected DORA reading

For the Acme-style history, students should conclude:

| Metric | Expected reading |
|---|---|
| Deployment Frequency | Low: roughly quarterly production releases |
| Lead Time for Changes | Low/Medium: changes wait weeks or months for release |
| MTTR | Medium/Low: recovery measured in hours/days and depends on manual action |
| Change Failure Rate | Poor: about 1 release out of 3 needs hotfix/rollback |

## What is intentionally missing

This fake history does not fully model GitHub Issues, PR comments, production alerts, or deploy logs. Use that absence as a teaching point:

> "A real DORA audit needs better instrumentation than a Git log. GitHub gives clues; production systems give evidence."

## Resetting the demo

If you need a clean view, use a fresh clone from GitHub. Do not rewrite the public history during class. The fake history is meant to be stable so students can reproduce the same observations.
