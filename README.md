# DevSecOps: SAST & DAST Pipeline (OpenText Fortify)

Automated security testing pipeline integrating **SAST (Static Application Security Testing)** and **DAST (Dynamic Application Security Testing)** into the software delivery lifecycle, using **OpenText Fortify** (SSC, ScanCentral SAST, WebInspect).

## Overview

This project demonstrates a real-world DevSecOps setup where security scanning is fully integrated into CI/CD, vulnerabilities are automatically tracked, and remediation is assigned without manual intervention.

**Core components:**
- **Fortify SSC** — central vulnerability management and reporting
- **ScanCentral SAST** — distributed static code analysis
- **OpenText WebInspect (DAST)** — dynamic scanning of running applications
- **GitLab CI/CD** — pipeline automation with `fcli`
- **Git-flow** — branch-based scan triggers (feature → SAST, release → DAST)

## Architecture Evolution

### v1 — Direct scanning (without ScanCentral)
Initial setup where SAST and DAST scanners were integrated directly into the CI/CD pipeline without centralized orchestration.

![Git-flow process](docs/images/v1-without-scancentral/git-flow%20process.png)
![SAST architecture](docs/images/v1-without-scancentral/SAST%20arhitecture.png)
![DAST architecture](docs/images/v1-without-scancentral/DAST%20architecture.png)

### v2 — Centralized scanning (with ScanCentral)
Scaled architecture using OpenText ScanCentral as a central scan management layer, enabling distributed scanning across multiple sensors/controllers.

*(diagrams to be added)*

## How It Works

1. Developer creates a merge request from `feature` branch into `develop`
2. Pipeline automatically triggers **SAST** scan via ScanCentral
3. Results are published to Fortify SSC
4. If critical/high vulnerabilities are found — notification sent, pipeline can block or require manual override
5. On `release` branch — **DAST** scan triggers against the running application
6. Security specialist reviews findings in SSC and assigns remediation tasks to developers

## CI/CD Examples

- [`examples/gitlab-ci-sast.yml`](examples/gitlab-ci-sast.yml) — SAST automation in GitLab CI
<!-- - [`examples/github-actions-sast.yml`](examples/github-actions-sast.yml) — same pipeline adapted for GitHub Actions -->

> Note: all examples use generic placeholders (`${SSC_URL}`, `secrets.SSC_TOKEN`) instead of real infrastructure values.

## Tech Stack

`Fortify SSC` · `ScanCentral SAST` · `OpenText WebInspect` · `GitLab CI/CD` · `fcli` · `GitLab Runner` · `Bash`

## Author

**Adil** — Information Security Engineer  
Focused on AppSec tooling, DevSecOps pipeline automation, and vulnerability management.