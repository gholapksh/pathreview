## Solution plan

**Issue:** [SETUP.md is missing Docker Compose startup instructions for Windows users](https://github.com/ascherj/pathreview/issues/116)

### Understand
The root cause is that SETUP.md assumes a Unix-like shell environment and that the Docker daemon is implicitly active. On Windows (native PowerShell), make is completely unavailable by default, leading to immediate command-not-found errors. Additionally, Docker Desktop must be manually initiated by the user; otherwise, subsequent commands silently fail or throw obscure connection errors. The expected behavior is a seamless onboarding experience for Windows users; the actual behavior is an immediate blocker at the environment spin-up stage.

### Map
Files to be modified:
* SETUP.md — The main markdown onboarding guide where the new Windows subsection and troubleshooting tips will live.

### Plan
1. **Document make alternatives for Windows:** Research and add instructions for installing make via Windows package managers (winget or choco) or document the raw docker compose equivalents so users can bypass make entirely.
2. **Add Docker Desktop lifecycle steps:** Insert explicit visual cues/instructions to launch the Docker Desktop GUI application and wait for the "Engine Running" status indicator before using the terminal.
3. **Draft a service health verification step:** Provide instructions to use docker compose ps to verify that the Postgres database and app containers are fully healthy before running migrations.
4. **Test and refine layout:** Review the Markdown layout inside SETUP.md to ensure clear visual separation (e.g., using tabs or clean headers) so Unix users aren't confused by Windows steps and vice versa.

### Inputs & outputs
* **Inputs:** Raw setup commands executed in a standard native Windows PowerShell environment.
* **Outputs:** An updated, robust SETUP.md file that guides a Windows user from a fresh clone to a fully operational local setup at localhost:5173 with zero unguided errors.

### Risks & unknowns
* **Execution Policies:** Some Windows users have restrictive PowerShell Execution Policies that might block package manager installations or custom scripts. 
* **WSL vs. Native PowerShell:** Windows users might try to mix WSL (Windows Subsystem for Linux) environments with native PowerShell paths, which could cause Docker socket binding conflicts. I need to make sure my instructions explicitly state they apply to native Windows host setups.

### Edge cases
* **Docker Engine not running:** The guide must handle the scenario where the user runs the startup commands while Docker Desktop is closed, explicitly detailing the expected error message and fix.
* **Port conflicts:** If a Windows user already has a local instance of PostgreSQL running natively on port 5432, the Docker container will fail to bind. I should add a quick troubleshooting note for identifying and stopping conflicting local services.
