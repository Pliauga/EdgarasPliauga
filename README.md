# Edgaras Pliauga

**Epistemic Systems Architect & Cloud Security Engineer** in London. I build autonomous agentic harnesses, AWS tooling, and LLM security infrastructure, mostly in Go and Python. 

My focus is on structural integrity: building systems that force AI models to verify their own claims, and proving where industry-standard tools fail.

---

## Flagship Research & Tooling

### IAM-Chain-Breaker
Autonomous agentic harness for multi-hop AWS IAM privilege escalation. Demonstrates that static AST scanners (Checkov, Trivy) are structurally blind to multi-hop logic, missing >90% of resource-scoped escalation chains. 

The harness models graph reachability, synthesizes least-privilege Permission Boundaries, and validates containment via live wire-execution. Achieved **295/295** parity with live AWS `iam:SimulateCustomPolicy`, blocked 3/3 live wire exploits with zero collateral damage (10,459 decision matrix), and discovered a novel 5.8s post-remediation IAM propagation window. The system ran autonomously for 13 hours on an unmodified DeepSeek model via a strict text-based orchestration harness, achieving zero hallucinations.

`Python` `AWS` `IAM` `Checkov` `Trivy` `Terraform` `Agentic Workflows`
[Whitepaper & Evidence Logs](https://github.com/Pliauga/IAM-chain-breaker)

---

## Other Projects

### Studio-Py
Browser-based Python curriculum for developers who have shipped software but never written Python. 25 modules of runnable code, 24 weeks of structured progression, running entirely client-side.

The runtime is Pyodide (WASM) inside a Web Worker, so every module executes locally with no backend. Terminal output is reactive: it drives halftone density on the module poster. Progress is rendered as an 8-bit snake spine from sliced pixel sprites, and data-structure concepts are explored through 3D sandboxes built with Threlte + Rapier.

`SvelteKit 5` `Pyodide` `WebAssembly` `Three.js` `Threlte` `Rapier`
[Repo](https://github.com/Pliauga/Studio-Py)

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

Zero-egress CLI that reads AWS CloudTrail events (live or offline fixtures) and generates tightened least-privilege IAM policies, either as Terraform `aws_iam_policy_document` HCL or plain IAM JSON. Everything happens in memory locally. Deterministic output via HashiCorp's `hclwrite`. Works as a CLI or as an embedded Go library.

`Go` `CloudTrail` `Terraform` `IAM` `hclwrite`
[Repo](https://github.com/Pliauga/LogZero)

### Onvlo
Local FinOps engine for LLM workloads. Ingests traces into Postgres, models costs with dbt, uses Z-scores to catch runaway agent loops and spend anomalies, alerts to Slack. Has a dashboard script for viewing metrics.

`Python` `PostgreSQL` `dbt` `Slack`
[Repo](https://github.com/Pliauga/Onvlo)

---

## Stack

**Languages:** Go, Python, Bash, SQL, HCL, TypeScript
**Cloud & AI Security:** AWS (IAM, Lambda, API Gateway, S3, SQS, KMS, CloudTrail), Terraform, Terragrunt, LLM Sandboxing, DLP, Agentic Orchestration
**Infra:** Docker, Kubernetes, Helm, Minikube, EKS, Floci, LocalStack
**Frontend/Web:** SvelteKit, Tailwind CSS, Three.js, WebAssembly

---

## Contact

[LinkedIn](https://linkedin.com/in/pliauga/) · [EdPliauga@gmail.com](mailto:EdPliauga@gmail.com)
