# Phase 2C – Azure CLI VNet Deployment

## Section 1 - Objective

Deploy and validate an Azure Virtual Network architecture using Azure CLI.

---

## Section 2 - Architecture Components

- Resource Group
- Virtual Network (VNet)
- Subnets
- Network Security Groups
- Virtual Machines
- Routing

---

## Section 3 - Lab Deployment Steps

---

### Step 1 – Create Resource Group

Create the resource group for the lab environment.

```bash
az group create \
  --name rg-vnet-lab \
  --location eastus

#### Validation



az group show --name rg-vnet-lab --output table

---
End of Step 1
---



---

### Step 2 – Create Virtual Network

az network vnet create \
    --resource-group "RG-Azure-Bash-CLI-WestUS" \
    --name "VNet-Core-WestUS" \
    --address-prefix "10.2.0.0/16" \
    --location "westus"

#### Validation

az network vnet show \
    --resource-group "RG-Azure-Bash-CLI-WestUS" \
    --name "VNet-Core-WestUS" \
    --output table

---
End of Step 2
---

### Step 3 – Create Subnets

####Creation

az network vnet subnet create \
    --resource-group "RG-Azure-Bash-CLI-WestUS" \
    --vnet-name "VNet-Core-WestUS" \
    --name "Subnet-App" \
    --address-prefix "10.2.1.0/24" \
    --verbose \
    --output table

az network vnet subnet create
    --resource-group "RG-Azure-Bash-CLI-WestUS" \
    --vnet-name "VNet-Core-WestUS" \
    --name "Subnet-DB" \
    --address-prefix "10.2.1.0/24" \
    --verbose \
    --output table

az network vnet subnet create
    --resource-group "RG-Azure-Bash-CLI-WestUS" \
    --vnet-name "VNet-Core-WestUS" \
    --name "Subnet-DB" \
    --address-prefix "10.2.2.0/24" \
    --verbose \
    --output table

az network vnet subnet create
    --resource-group "RG-Azure-Bash-CLI-WestUS" \
    --vnet-name "VNet-Core-WestUS" \
    --name "Subnet-Management" \
    --address-prefix "10.2.3.0/24" \
    --verbose \
    --output table

#### Validation

az network vnet subnet list \
    --resource-group "RG"Azure-Bash-CLI-WestUS"
    --vnet-name "VNet-Core-WestUS"
    --verbose
    --output table \

---
End of Step 3
---

### Step 4 – Deploy Virtual Machines



### Step 5 – Validate Connectivity



## Section 4 - Microsoft-Style Technical Table

| Field | Interchangeable Terms | Explanation | Use Case | Analogy |
|------|------|------|------|------|
| Documentation Runbook | Deployment Guide | Step-by-step instructions to deploy infrastructure | Infrastructure teams | Construction blueprint |
| Lab Skeleton | Template | Initial structure before implementation | Standardized labs | House framing |
| CLI Deployment | Infrastructure via command line | Azure resources created via CLI | DevOps workflows | Power tools vs hand tools |
| Validation Command | Verification step | Confirms resources exist | Troubleshooting | Inspecting finished work |

---

## Section 5 - Errors Encountered During Deployment

## Section 6 - Successful Command Output (Verbose Mode)

