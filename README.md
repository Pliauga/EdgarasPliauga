# Edgaras Pliauga

Cloud security and DevSecOps engineer in London. I build tooling around AWS, IAM, and LLM security, mostly in Go and Python.

---

## Stack

**Languages:** Go, Python, Bash, SQL, HCL
**Cloud:** AWS (IAM, Lambda, API Gateway, S3, SQS, KMS, CloudTrail), Terraform, Terragrunt
**Infra:** Docker, Kubernetes, Helm, Minikube, EKS, Floci, LocalStack

---

## Projects

### halt.lab
Event-driven AWS security scanner. Watches S3 uploads, flags credentials and risky binaries with Lambda, moves compromised objects into quarantine. Terragrunt for infra with separate dev (Floci) and prod (eu-west-2) configs. Helm chart for the app stack.

Integration tests cover object tagging, quarantine, S3 TLS bucket policies, and SQS DLQ redrives.

`Terragrunt` `Terraform` `AWS` `Helm` `Kubernetes`
[Repo](https://github.com/Pliauga/halt.lab)

### self-healing-k8s
Reference implementation of a Kubernetes cluster that repairs its own failures. Runs on Minikube, designed to move to EKS with Terraform. Three replicas behind a PDB, HPA from 3 to 10, and chaos scenarios that inject real faults: pod eviction, readiness/liveness cascades, CPU load, bad rollouts, node drains.

The design is layered on purpose. Most healing needs no agent at all. Probes and controllers cover the common cases in seconds; an optional agent handles only what they cannot express. Pod replacement goes through the eviction API, never a direct delete, so the PDB is enforced by the API server rather than by convention. `make validate` catches cross-manifest errors that schema validation misses. The Tier 2 agent and the EKS path are on the roadmap.

`Kubernetes` `Minikube` `EKS` `Terraform` `Prometheus`
[Repo](https://github.com/Pliauga/self-healing-k8s)

### Zvix
Security proxy and DLP layer for LLM inference. Sits inline on Lambda + API Gateway (Floci locally) in front of Ollama. Scans prompts on the way in for credential leaks and injection patterns, scans completions on the way out for secret exfiltration. Fails closed: any inspection error returns 500 rather than passing traffic through.

Uses pre-compiled regex instead of an LLM judge. Under 1ms per request, no token cost, stdlib only, deployment artefact under 10KB.

`Python` `Lambda` `API Gateway` `Ollama` `DLP`
[Repo](https://github.com/Pliauga/Zvix)

### LogZero
*Work in progress.*

Zero-egress CLI that reads AWS CloudTrail events (live or offline fixtures) and generates tightened least-privilege IAM policies, either as Terraform `aws_iam_policy_document` HCL or plain IAM JSON. Everything happens in memory locally. Deterministic output via HashiCorp's `hclwrite`. Works as a CLI or as an embedded Go library.

`Go` `CloudTrail` `Terraform` `IAM` `hclwrite`
[Repo](https://github.com/Pliauga/LogZero)

### Onvlo
Local FinOps engine for LLM workloads. Ingests traces into Postgres, models costs with dbt, uses Z-scores to catch runaway agent loops and spend anomalies, alerts to Slack. Has a dashboard script for viewing metrics.

`Python` `PostgreSQL` `dbt` `Slack`
[Repo](https://github.com/Pliauga/Onvlo)

---

## Contact

[LinkedIn](https://linkedin.com/in/pliauga/) · [EdPliauga@gmail.com](mailto:EdPliauga@gmail.com)
