# Phase 2C – Azure CLI VNet Deployment

## Objective

Deploy and validate an Azure Virtual Network architecture using Azure CLI.

---

## Architecture Components

- Resource Group
- Virtual Network (VNet)
- Subnets
- Network Security Groups
- Virtual Machines
- Routing

---

## Lab Deployment Steps

---

### Step 1 – Create Resource Group

Create the resource group for the lab environment.

```bash
az group create \
  --name rg-vnet-lab \
  --location eastus

Validation

az group show --name rg-vnet-lab --output table

---
End of Step 1
---

---

### Step 2 – Create Virtual Network


No progress commentary.

---

# Section 3 — Microsoft-Style Technical Table

| Field | Interchangeable Terms | Explanation | Use Case | Analogy |
|------|------|------|------|------|
| Documentation Runbook | Deployment Guide | Step-by-step instructions to deploy infrastructure | Infrastructure teams | Construction blueprint |
| Lab Skeleton | Template | Initial structure before implementation | Standardized labs | House framing |
| CLI Deployment | Infrastructure via command line | Azure resources created via CLI | DevOps workflows | Power tools vs hand tools |
| Validation Command | Verification step | Confirms resources exist | Troubleshooting | Inspecting finished work |

---

### Step 3 – Create Subnets



### Step 4 – Deploy Virtual Machines



### Step 5 – Validate Connectivity
