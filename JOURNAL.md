## Week 7 ï¿½ Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/116

**Issue title:** SETUP.md is missing Docker Compose startup instructions for Windows users

**Tier:** [x] Tier 1  [ ] Tier 2  [ ] Tier 3

**Problem summary:**
SETUP.md currently assumes a Unix-like environment and doesn't account for
Windows-specific setup steps. Windows users following the guide as written
will hit several silent failure points: make isn't available by default in
PowerShell and requires a separate install, Docker Desktop must be manually
launched (the CLI alone doesn't start the engine), and there's no guidance on
verifying containers are healthy before running migrations. Without these
details, new contributors on Windows can lose significant time debugging
errors (like Postgres authentication failures) that are actually just
symptoms of Docker not being started yet. A successful fix would add a
Windows-specific subsection to SETUP.md covering make installation,
launching Docker Desktop, and confirming docker compose ps shows all
services healthy before proceeding.

**Branch name:** docs/116-windows-docker-setup-instructions

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [ ] Issue added to cohort ledger


## Week 8 — Reproduction & solution planning

**Reproduction commit link:** https://github.com/gholapksh/pathreview/commit/e273ba5

**Reproduction summary:**
I reproduced the documentation gap by executing the SETUP.md steps natively in Windows PowerShell. The environment immediately failed due to the missing make command, and database connection errors occurred because the guide lacks instructions to manually initialize and verify the Docker Desktop engine state before running migrations.

**PLAN.md link:** https://github.com/gholapksh/pathreview/blob/docs/116-windows-docker-setup-instructions/PLAN.md

**Walkthrough video (recommended):** [Not recorded for this turn]

**Blockers or open questions:**
None at the moment. The path forward for updating the documentation layout is clear.
