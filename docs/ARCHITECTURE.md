# NEXUS AXIS Control Plane v0.1

## Purpose
Central developer task queue, schedule register, integration catalog and evidence-first promotion flow for Cryptic-Nexus-Axis.

## Pipeline
ORCHBENCH → LIVE_EXECUTION → ADAM_PROOF_GATES → PRODUCTION_VERIFIED → ARCHBENCHSHOP.

The schedule produces **candidate work**, not automatically verified production. Cain and Abel are distinct *proposed* verification operator roles; neither role grants authority or can bypass evidence requirements.

## Components
- GitHub Issues: authoritative development queue.
- `config/integrations.json`: integration inventory and operational status.
- `config/schedule.json`: cadence definitions.
- GitHub Actions: periodic queue health reporting, initially read-only.
- `dashboard/index.html`: static browser task board. Reads public repository issue metadata via GitHub REST when opened; does not store credentials.
- Agents: future least-privilege workers; only permit issue/branch/PR creation with explicit scopes and approval gates.

## Security controls
- No automatic merges, deployments, device commands, package upgrades or secret rotation.
- No public device diagnostic uploads. Do not add raw receipts, .env files, token caches, or home-directory contents.
- Scheduled workflow uses contents:read and issues:read; supply-chain scripts are not remotely downloaded/executed.
- Scheduled jobs should be cancellable from Actions; working agents must have per-task timeout, budget, stop control and auditable outputs.
- Manual approvals and live evidence required for ADAM promotion.
- This is source-level architecture, not production verification.
