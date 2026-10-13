# crypticnews.org — Automation and Site Hosting Design (v0.1)

## Verified account boundary
Cloudflare returned an active `crypticnews.org` zone on a Free Website plan during design review. **No Cloudflare Pages/Workers project, GitHub Pages domain binding, production DNS routing, origin validation or deployment was verified.** This document does not authorize a DNS change.

## Site decision
| Workload | Build and runtime |
|---|---|
| Editorial pages / long-form docs / changelogs | Jekyll or other static generator, GitHub Actions to build |
| WebGL canvas, nested layers, videos, dynamic UI | Vite/React or plain HTML/JS, built in GitHub Actions, run in visitors' browsers |
| Dynamic authenticated APIs, agent orchestration | Cloudflare Workers / durable state / D1, after access and costs verified |
| Background tasks | Scheduled events + queues + bounded Workflows, not recursive GitHub Actions |
| AI model evaluations | Separately authorized model/API jobs, no unbounded token usage |
| Multi-repo code changes | Individual draft PR per repo; human review and ADAM live verification |

## Why not an unlimited loop?
A `schedule` trigger is a periodic event, not a persistent process, and GitHub or Cloudflare impose quotas, limits and cancellation policies. No agent may continuously self-dispatch solely to evade ChatGPT or provider task limits. Instead, use an idempotency key, queue, retry/backoff, checkpoint, finite budget, stop mechanism and completed/failed states.

## Cadence
- Daily: inspect queue health (read only); currently authored in `.github/workflows/queue-health.yml`.
- On every pull request: source size / asset bound checks via `axis-dashboard-quality.yml`.
- Monday and Friday: planned proposals and evidence reviews; configuration alone does not schedule them.
- Production deploy: separate manual approval and protected environment, after explicit target selection.

## Architecture and acceptance
1. `Issue` contains requested behavior, acceptance criteria, data scope, estimated cost and owner.
2. `Agent task manifest` caps attempts (3), duration (900 seconds) and concurrency (2), forbids production writes.
3. `Branch + draft PR` carries implementation. Sandbox checks cannot be confused with production proof.
4. `ADAM gates`: DISCOVER → OBSERVE → NORMALIZE → CLASSIFY → VERIFY → FINGERPRINT → LOOKUP_REMEDY → AUTHORIZE → APPLY → REVERIFY → RECONCILE → PROMOTE. Use runtime-specific gates where applicable.
5. `Review`: Cain and Abel are separately-defined proposed verification operator roles, neither bypasses evidence.
6. `Release`: protected environment, human confirmation, rollback handle and deployed receipt.
7. `Audit`: source commit, CI logs, browser tests, real endpoint checks, explicit evidence labels.

## Deployment selection (not activated)
**GitHub Pages:** only static site output; Jekyll is optional when Actions performs a custom build. `templates/axis-workflow/pages-static-template.yml` is an optional manual-deploy example. Copy intentionally and set repository Pages publishing source to GitHub Actions. Publishing a site does not provision backend APIs.

**Cloudflare:** for CrypticNews's interactive public frontend, prefer static assets served by Workers/Pages plus separately deployed authenticated Workers APIs. Prefer one deployment ownership path per site; do not configure both GitHub Pages and Cloudflare deployments to fight over DNS. If using GitHub Actions to deploy Cloudflare, provision a least-privilege API token in GitHub Actions secrets and use a protected environment (never commit the token). Preview deploys should not get production credentials.

## Template/skill distribution
Read `skills/nexus-axis-automation/SKILL.md` into a compatible agent's workspace and use the caller workflow in `.github/workflows` for source checks. The skill is documentation until an agent explicitly installs/loads it; it does not add an OpenAI task or bypass its limits.

## Unverified
No real Cloudflare deployment, no browser performance audit, no actual Actions run, no Termux device integration, no deployed agents, and no domain-to-project linkage are claimed.
