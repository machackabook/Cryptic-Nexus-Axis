# Cryptic Nexus Axis

Rootless Termux + Acode orchestration system with an evidence-first development control plane.

**[Enhancement dashboard](dashboard/index.html)** · **[Issues queue](https://github.com/machackabook/Cryptic-Nexus-Axis/issues)** · **[Workflow](.github/workflows/queue-health.yml)**

## Initial control plane
- Daily 08:17 UTC GitHub Actions read-only queue report.
- GitHub Issues serve as centralized feature, bug, and enhancement queue.
- Static dashboard displays public issues and roadmap. GitHub Pages deployment is not yet enabled.
- Agent workers and dynamic integration are planned, not deployed.
- No auto-merges, upgrades, device execution, or production promotion without live ADAM gates.

See [architecture](docs/ARCHITECTURE.md), [schedule](config/schedule.json), and [integrations](config/integrations.json).

**Status:** Source initialized. CI and mobile runtime unverified.
