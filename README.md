# Online Shop 🛍️ — Dockerized Deployment on AWS EC2

[![Stars](https://img.shields.io/github/stars/aliahmadshah56/ecommerce-app)](https://github.com/aliahmadshah56/ecommerce-app)
![Forks](https://img.shields.io/github/forks/aliahmadshah56/ecommerce-app)
![GitHub last commit](https://img.shields.io/github/last-commit/aliahmadshah56/ecommerce-app?color=red)
[![GitHub Profile](https://img.shields.io/badge/GitHub-aliahmadshah56-blue?logo=github&style=flat)](https://github.com/aliahmadshah56)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Welcome to the **Online Shop** project — a fully functional e-commerce application deployed end-to-end as part of my hands-on DevOps portfolio work. This repository demonstrates foundational-to-intermediate DevOps skills across three key areas:

- **Git & GitHub**
- **Linux**
- **Docker**

The original application code and hackathon brief are from the **Train With Shubham Hackathon Phase 1**. This repo documents my own containerization and deployment work on top of it — building the Docker setup, debugging real infrastructure issues, and shipping it live on AWS EC2.

---

### Content

- [**Situation**](#situation)
- [**Task**](#task)
- [**Action**](#action)
- [**Result**](#result--resume)

## Guidelines & Resources

- [CONTRIBUTING.md](CONTRIBUTING.md): Guidelines for code contributions, commit messages, and overall coding standards.
- [COMMANDS.md](COMMANDS.md): Commands used throughout the project, from configuration to deployment (excluding Git commands).
- [ROADMAP.md](ROADMAP.md): Project vision, future enhancements, and milestones.
- **Repository Documentation:** See the `src` directory for application logic, and configuration files such as `vite.config.js` and `index.css`.

---

### Situation

As part of the **Train With Shubham Hackathon Phase 1**, I took on deploying an Online Shopping Portal to the internet. The goal was to make the application easily accessible, reliable, and scalable enough to handle real user traffic — using DevOps automation tools to streamline the deployment process, reduce manual effort, and improve overall system performance. This involved setting up the necessary infrastructure, automating the deployment, and ensuring the application could run smoothly in a real environment.

---

### Task

- Develop the required infrastructure for the Online Shopping Portal
- Clone and configure the codebase while ensuring security and accessibility
- Strategize a `Deployment Plan` for bringing the application to the internet

All while ensuring:

- Gathering the resources needed to build the project
- Implementing automation where possible
- Using `Docker` to containerize a real-world application
- Getting genuine hands-on experience with DevOps tools
- Debugging infrastructure issues methodically rather than guessing
- Building on a solid cloud/DevOps foundation

---

### Action

> What I actually did:

- Reviewed the project's [ROADMAP.md](ROADMAP.md) and [CONTRIBUTING.md](CONTRIBUTING.md) to understand the codebase and standards
- Set up SSH access to an AWS EC2 (Ubuntu) instance and connected via MobaXterm, resolving `.pem` key permission issues specific to NTFS/WSL environments
- Reviewed and used the project's Dockerfile — a **multi-stage build** (`node:20-alpine` for building, `nginx:alpine` for serving) — which keeps the final production image lean by shipping only the compiled static assets, not the Node.js toolchain or source code
- Configured and ran the app via **Docker Compose**, including:
  - Diagnosing and fixing a host↔container **port mapping mismatch** (Compose was mapping `5173`, while the Nginx container actually listens on port `80`)
  - Fixing the **health check**, switching from `curl` (not available in `nginx:alpine` by default) to `wget --spider`, pointed at the app's dedicated `/health` endpoint
  - Installing the `docker compose` CLI plugin manually on the EC2 instance after discovering it wasn't available via the default `apt` repository
- Verified the custom `nginx.conf`, which handles SPA routing (`try_files` fallback), gzip compression, and static asset caching
- Configured the EC2 **Security Group** to allow inbound HTTP traffic on port 80
- Set up **SSH-based GitHub authentication** on the EC2 instance (instead of Personal Access Tokens, which are prone to revocation) and pushed the working project to this repository
- Deployed and verified the application was reachable via the EC2 instance's public IP

---

### Result / Resume

- Successfully deployed the `Online Shopping Portal` to the internet on `Amazon EC2`, making it accessible to real users
- Debugged and resolved real infrastructure issues: port mapping mismatches, missing `docker compose` plugin, healthcheck tool incompatibility with a minimal Alpine image
- Used a **multi-stage Docker build** to keep the production image minimal — excluding the Node.js build environment and source code from the final image
- Configured Docker Compose with health checks, a custom bridge network, and a restart policy for resilience
- Set up secure, token-free GitHub authentication via SSH keys directly from the deployment server

---

Happy Learning :)
