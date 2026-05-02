# 🚀 Terraform 10‑Day Learning Roadmap

## 📘 Overview
This repository contains a **10‑day structured roadmap** to learn Terraform Language through hands‑on projects.  
Each day introduces new concepts, paired with a practical project and direct documentation references.

---

## 📂 Roadmap Table

| **Day** | **Topics to Learn** | **Hands‑On Project** | **Official Docs (Direct Links)** |
|---------|---------------------|-----------------------|----------------------------------|
| **Day 1: Basics** | HCL syntax, blocks, file organization | Build a **multi‑AZ VPC** with public/private subnets and Internet/NAT gateways. | [Configuration Syntax](https://developer.hashicorp.com/terraform/language/syntax/configuration) |
| **Day 2: Arguments & Meta‑Arguments** | Required, optional, computed, meta‑arguments (`count`, `for_each`, `depends_on`, `provider`, `lifecycle`) | Deploy an **auto‑scaling group of EC2 instances** using `count` and `for_each`. | [Meta‑arguments](https://developer.hashicorp.com/terraform/language/meta-arguments) |
| **Day 3: Expressions & Data Sources** | Literals, references, functions, conditionals, for expressions, dynamic blocks, data sources | Build a **VPC with subnets** using `cidrsubnet()` and fetch AMI IDs via a **data source**. | [Expressions](https://developer.hashicorp.com/terraform/language/expressions) / [Functions](https://developer.hashicorp.com/terraform/language/functions) / [Data Sources](https://developer.hashicorp.com/terraform/language/data-sources) |
| **Day 4: File Structure & Modules** | Core files (`main.tf`, `variables.tf`, `outputs.tf`, `provider.tf`), supporting files, root vs child modules | Create a **network module** (VPC, subnets, gateways) and reuse it across multiple environments. | [Modules](https://developer.hashicorp.com/terraform/language/modules) |
| **Day 5: Providers & Resources** | Provider configuration, resource blocks, dependencies, multiple providers | Configure **AWS + random provider** to generate unique resource names. | [Providers](https://developer.hashicorp.com/terraform/language/providers) / [Resources](https://developer.hashicorp.com/terraform/language/resources) |
| **Day 6: Variables, Locals & Outputs** | Input variables, defaults, sensitive variables, locals, outputs | Build a **parameterized Kubernetes cluster module** with locals for naming conventions and outputs for kubeconfig. | [Variables](https://developer.hashicorp.com/terraform/language/values/variables) / [Locals](https://developer.hashicorp.com/terraform/language/values/locals) / [Outputs](https://developer.hashicorp.com/terraform/language/values/outputs) |
| **Day 7: State & Backends** | Local vs remote state, backends (S3, GCS, Azure), state locking, state commands (`list`, `show`), import | Configure **Terraform Cloud remote state** with workspaces and import an existing AWS RDS instance. | [State](https://developer.hashicorp.com/terraform/language/state) / [Backends](https://developer.hashicorp.com/terraform/language/settings/backends) / [Import](https://developer.hashicorp.com/terraform/language/import) |
| **Day 8: Provisioners** | Local‑exec, remote‑exec, error handling | Deploy EC2 and use **remote‑exec to bootstrap Docker + Nginx**, then verify with local‑exec curl tests. | [Provisioners](https://developer.hashicorp.com/terraform/language/resources/provisioners) |
| **Day 9: Workspaces** | Creating workspaces, switching, managing environments | Set up **dev, staging, prod workspaces** with different variable sets and backend configs. | [Workspaces](https://developer.hashicorp.com/terraform/language/state/workspaces) |
| **Day 10: Security, Sensitive Data & Stacks** | Sensitive variables, avoiding secrets in code, Vault integration, stacks for layered deployments | Build a **multi‑stack setup**: network stack, compute stack, app stack, all secured with Vault secrets. | [Sensitive Data](https://developer.hashicorp.com/terraform/language/state/sensitive-data) / [Stacks](https://developer.hashicorp.com/terraform/cloud-docs/workspaces/stack) |
