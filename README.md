# 🛡️ End-to-End-Azure-DevOps-IaC-Pipeline

A professional-grade Infrastructure as Code (IaC) repository showcasing a **hardened, production-ready CI/CD lifecycle** for Azure Resource Group Governance using Terraform and Azure DevOps.

---

## 🏗 Project Overview
This project demonstrates an automated delivery engine for Azure infrastructure, ensuring every change is **Secure, Compliant, and Cost-Effective**.

### 📂 Directory Layout
```text
.
├── terraform/
│   ├── modules/            # Reusable Dynamic Child Modules
│   │   └── resource_group/ # Dynamic RG creation with naming validation
│   └── env/
│       └── dev/            # Development Configuration (Root Module)
├── pipelines/
│   └── azure-pipelines.yml # Direct, Hardened CI/CD Pipeline
└── README.md
```

---

## 🛠 Prerequisites (Mandatory Setup)

Before running the pipeline, ensure the following are configured in your environment:

### 1. Self-Hosted Build Agent (Required)
- This pipeline is designed to run on a **Self-Hosted Agent** (configured in the `Default` pool).
- Ensure your agent has `Terraform`, `Python/Pip`,`tar` and `Curl` installed.
- *Why?* Enterprise environments use self-hosted agents for security and to keep traffic within a private network.

### 2. Azure Backend State
You must manually create the following resources to store the Terraform `.tfstate` file:
- **Resource Group**: e.g., `rg-terraform-mgmt`
- **Storage Account**: e.g., `stterraformstate001`
- **Container**: `tfstate`
- Update the `backend*` variables in `azure-pipelines.yml` with your specific names.

### 3. Azure DevOps Configuration
- **Service Connection**: Create an ARM Service Connection named **`Azure-Service-Connection`**.
- **Environment**: Create an ADO Environment named **`production-gate`** and add a **Manual Approval** check.
- **Infracost API Key**: Sign up at Infracost.io and add the key as a secret variable named **`INFRACOST_API_KEY`** in your pipeline.

---

## 🚀 How to Use this Repository

1.  **Fork** this repository to your GitHub account.
2.  **Import** the Forked Repo into your **Azure DevOps Project**.
3.  Update the **variables** in `/pipelines/azure-pipelines.yml` to match your Azure backend details.
4.  Create a **New Pipeline** pointing to the existing YAML file: `/pipelines/azure-pipelines.yml`.
5.  **Run Pipeline!**

---

## 🛡 The Pipeline Workflow (Step-by-Step)
`Init` ➔ `Fmt` ➔ `Validate` ➔ `Security Scan (TFSec/Checkov)` ➔ `Plan` ➔ `Compliance Check (Terrascan)` ➔ `Cost Estimate (Infracost)` ➔ `Manual Approval` ➔ `Apply`

---
**Author:** Mahendra kumar
**Focus:** Cloud Infrastructure | DevSecOps | SRE  
*Showcased for LinkedIn Portfolio - 2024*
