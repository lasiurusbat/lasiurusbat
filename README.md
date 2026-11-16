## Hi, I'm Vedad 👋

**Cloud & DevOps Engineer** in the Frankfurt area. I build and run small production platforms on AWS: infrastructure in Terraform, delivery through GitHub Actions with OIDC (no long-lived keys), and monitoring on top.

Before DevOps I spent a decade in technical production work on 3D/CGI pipelines, which is where my habits come from: careful troubleshooting, thinking in pipelines, and Scrum and Kanban.

**[Portfolio](https://vedad-dizdarevic.dev)** · **[CV (PDF)](https://vedad-dizdarevic.dev/cv/Vedad_Dizdarevic_CV_EN.pdf)** · **[Lebenslauf (PDF)](https://vedad-dizdarevic.dev/cv/Vedad_Dizdarevic_CV_DE.pdf)** · **[LinkedIn](https://www.linkedin.com/in/vedad-dizdarevic-b154305/)** · **[hello@vedad-dizdarevic.dev](mailto:hello@vedad-dizdarevic.dev)**

> **Available now.** I'd prefer a full-time role but can also freelance. Hybrid in the Frankfurt area (up to 3 days on site) or remote within the EU. EU work permit.

---

### What I've built

Each project has a full case study on my site. Some source repositories are private; the case studies show the architecture, the trade-offs and what's still missing.

#### [Sorted](https://vedad-dizdarevic.dev/projects/sorted/): the AWS platform behind a live multi-tenant SaaS
A support-ticket SaaS, live and commercially available at [sorted.onl](https://sorted.onl). I built its AWS platform alone and run it alone.
- One Terraform module builds both dev and prod: VPC with private subnets, ALB, ECS Fargate, RDS PostgreSQL, ECR, Secrets Manager, CloudWatch Logs
- Pushing a git tag builds the images in GitHub Actions and pushes them to ECR with immutable tags, through OIDC with no stored AWS keys
- Terraform `fmt`, `validate`, shellcheck and 22 offline Terraform tests run on every PR
- Email runs on SES in both directions (KMS-encrypted S3, SNS webhooks) with an ECS task role instead of API keys
- Dev costs 64% less, measured on the AWS bill. Multi-AZ is designed and is three Terraform flags away (not yet running)

`AWS` `ECS Fargate` `RDS` `SES` `Terraform` `GitHub Actions` `OIDC` `Cloudflare` `Grafana Cloud` · source private

#### [Portfolio site](https://vedad-dizdarevic.dev/projects/this-site/): a private S3 bucket behind a Cloudflare Worker
My portfolio, run as a small production platform. Source: [app](https://github.com/lasiurusbat/vedad-dizdarevic-dev-app) · [infra](https://github.com/lasiurusbat/vedad-dizdarevic-dev-infra)
- AWS and Cloudflare in Terraform, with plan output posted as a PR comment, Trivy/Checkov scans and a gated apply
- Three OIDC roles, each trusted by one repository; the Worker's one IAM key is rotated automatically by a scheduled workflow
- The Worker sets six security headers, and every deploy is checked on the live domain
- Quality gates fail the build: Playwright, axe, Lighthouse, html-validate, page-weight budgets, gitleaks
- CloudWatch alarms to SNS, Better Stack uptime checks and a runbook in which every rollback has been tried

`Terraform` `Cloudflare Workers` `S3` `Lambda` `SES` `GitHub Actions` `Astro`

#### [Rain Alert](https://vedad-dizdarevic.dev/projects/rainalert/): from git tag to a checked release, on free tiers
A live rain forecast app at [rainalert.live](https://rainalert.live). Source: [RainAlert](https://github.com/lasiurusbat/RainAlert)
- Pushing a tag builds one Docker image, tests it inside the container, ships that same image to Render through Docker Hub and checks the new version on the live site
- Pull requests, including those from forks and Dependabot, can never push an image or deploy
- A server-side cache and a fallback API with a call budget keep it within the free weather APIs' rate limits

`Docker` `GitHub Actions` `Docker Hub` `Render` `Python`

#### [WhoCalledBack](https://vedad-dizdarevic.dev/projects/whocalledback/): Raspberry Pi first, AWS serverless next *(in progress)*
A multi-tenant job-search tracker, designed for the cloud without paying for the cloud while I build it.
- One codebase for a Raspberry Pi 5 and AWS Lambda (both arm64). Four ports are swapped per environment: ElasticMQ/SQS, cron/EventBridge Scheduler, AES-GCM/KMS, none/SES
- A push to the staging branch builds arm64 images into GHCR with no stored credentials and runs them in hardened Docker Compose behind Tailscale
- Postgres row-level security keeps tenants apart; database roles are created only in migrations
- Phase 1 runs on the Pi for €0. The AWS phase is designed but not built yet

`Raspberry Pi` `Docker Compose` `GHCR` `Tailscale` `PostgreSQL RLS` `AWS Lambda (planned)` · source private

#### More
- **[sre-project](https://github.com/lasiurusbat/sre-project)**: a Kubernetes GitOps platform on EKS. Argo CD delivers Ghost with MySQL; Prometheus, Grafana, Fluent Bit and Splunk handle observability. I fixed an EBS CSI driver IRSA misconfiguration and Argo CD sync failures along the way. The cluster has been shut down, so the repository is the record.
- **[Ads-Platform](https://github.com/lasiurusbat/Ads-Platform)**: a three-tier AWS deployment (ALB → ECS Fargate → RDS) in Terraform, with a GitLab CI/CD pipeline and Grafana alerting for RDS connections.
- **[GitLab](https://gitlab.com/lasiurusbat/cars-api)**: a multi-region Terraform project, plus pipelines for a Spring Boot app on Elastic Beanstalk and a Gatsby site.

---

### Toolbox

| Area | Tools |
|---|---|
| **Cloud (AWS)** | ECS/Fargate, ECR, RDS, ALB, VPC, IAM (OIDC, least privilege), S3, Lambda, SES, SNS, KMS, Secrets Manager, CloudWatch, EventBridge, EKS |
| **Infrastructure as Code** | Terraform: modules, multiple environments and regions, S3 remote state, Terraform tests |
| **Edge** | Cloudflare: DNS, Workers, WAF rules, Turnstile |
| **Containers** | Docker (multi-stage builds), Docker Compose, Kubernetes (EKS), Argo CD (GitOps), Helm |
| **CI/CD** | GitHub Actions (OIDC to AWS, tag-driven releases, required checks), GitLab CI/CD |
| **Observability** | Prometheus, Grafana, CloudWatch, Fluent Bit, Splunk, Sentry, Better Stack |
| **Security** | gitleaks, Trivy, Checkov, CSP and security headers, key rotation |
| **Code** | Bash, Python, TypeScript/Node.js, SQL |

### Certifications

- **DevOps Engineer diploma**, DataScientest, 2024 ([verify](https://document-factory.datascientest.com/verify/4f75a618-8b74-4aff-9899-a807efeb870e))
- **Docker & Kubernetes: The Practical Guide**, Udemy, 2026 ([verify](https://www.udemy.com/certificate/UC-409a5c62-6975-4f5e-8261-7cca40522b39/))
- **AWS Certified Solutions Architect – Associate**: preparing for the exam

### Languages

Bosnian/Serbian/Croatian (native), English and German (both fluent). The portfolio is in both English and German: **[English](https://vedad-dizdarevic.dev)** · **[Deutsch](https://vedad-dizdarevic.dev/de/)**
