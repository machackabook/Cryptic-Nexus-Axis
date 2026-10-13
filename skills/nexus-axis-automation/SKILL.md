---
name: nexus-axis-automation
description: Plan and review bounded, evidence-first GitHub Actions and Cloudflare agent automation for CrypticNews and NEXUS AXIS sites. Use for scheduled enhancements, repository task queues, reusable CI, agent proposals, dynamic front-end deployments, or ADAM gates.
---

# NEXUS AXIS Automation Skill v0.1

This is a **repository-distributed agent instruction skill**, not a separately installed ChatGPT plugin. An agent must explicitly load this file; committing it does not register a background scheduler.

## Decision procedure
1. Discover the target repository, branch, current deployment route, project type (Jekyll static / prebuilt static / Vite or React / Worker API), owner consent and baseline evidence. Never assume crypticnews.org DNS points to the repo or Worker.
2. Classify every change as one of: research, source proposal, CI build, preview deploy, production deploy, device operation. Do not conflate them.
3. Choose execution:
   - GitHub Actions for source events, reproducible tests, build artifacts and release proposals.
   - Jekyll only for static docs/articles/changelogs.
   - Browser/WebGL/React/Vite for graphics-heavy client apps.
   - Cloudflare Workers + D1/Queues/Workflows for authenticated APIs, queues and bounded durable jobs after explicit provisioning and review.
   - Hugging Face Jobs only if available and a separate job budget, data policy and permission scope are approved.
4. Create a GitHub issue and a scoped branch/PR. Never push directly to main, enable auto-merge, or deploy on a scheduled research-only job.
5. Enforce finite job policy: max 3 attempts, max 900 seconds per agent job, one task run per idempotency key, explicit approval for writes outside proposal branches, and STOP / cancellation controls.
6. Apply **ORCHBENCH → LIVE_EXECUTION → ADAM_PROOF_GATES → PRODUCTION_VERIFIED → ARCHBENCHSHOP**. Cain/Abel are proposed separate reviewers, not a bypass or proof of deployment.
7. Report affected files, evidence level (DESIGN, SOURCE_CHECK, CI_EXECUTED, DEVICE_OBSERVED, DEPLOYED_VERIFIED), exact next step and rollback.
8. Never expose or commit passwords, access tokens, signing keys, private device receipts, raw environment dumps or personal data.

## Self-improvement and limits
- Agents may propose modifications to their own workflow through PRs, but may not merge or elevate their own permissions.
- Do not build self-dispatching workflow loops to evade any platform usage limits. Use event queues, deduplication, backpressure, concurrency limits and provider budgets.
- GitHub scheduled workflows only run from the default branch and can be delayed or disabled by inactivity. They are not an always-on daemon.
- Cloudflare and GitHub capacities and costs remain subject to current plan limits.
- A generated skill file does not automatically install in OpenAI, Acode, Termux, or a third-party agent framework.

## Reusable assets
- `.github/workflows/axis-reusable-site-quality.yml` — read-only quality gate usable through workflow_call.
- `.github/workflows/axis-dashboard-quality.yml` — demonstration caller.
- `templates/axis-workflow/pages-static-template.yml` — optional manual GitHub Pages static deployment example. It does not deploy while stored in templates.
- `templates/axis-workflow/agent-task.example.json` — bounded agent-run manifest.
- `docs/CRYPTICNEWS_AUTOMATION.md` — architecture, activation and review checklist.
