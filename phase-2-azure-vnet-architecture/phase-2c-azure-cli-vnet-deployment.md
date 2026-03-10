---
# Phase 2C – Azure CLI VNet Deployment
---

---
## Section 1 - Objective
---

### Purpose

Deploy and validate an Azure Virtual Network architecture using Azure CLI.

### Desired Outcome

+ The creation of a core resource group containing all resources located within the West US region with the purpose of creation of resources using Azure Bash CLI and ONLY resources created by Azure Bash CLI
  * Resource group name will be "RG-Azure-Bash-CLI-WestUS"
+ The creation of a core network within the West US region called "VNet-Core-WestUS"
  * Contains an address prefix of 10.2.0.0/16 for an effective address range of 10.2.0.0 - 10.2.255.255
  * Will be contained in the West US region
  * Contains the following subnets
    - Subnet-App-WestUS
    - Subnet-DB-WestUS
    - Subnet-Management-WestUS
+ The creation of subnets within the West US region's "VNet-Core-WestUS" VNet core network
  * Formatted with the following address ranges:
    - Subnet-App-WestUS: 10.2.1.0/24
    - Subnet-DB-WestUS: 10.2.2.0/24
    - Subnet-Management-WestUS: 10.2.3.0/24
+ The creation of virtual machines (VMs) within each respective subnet environment
+ The validation of interactions and verification of connectivity across other core networks within different regions

### End of Section 1
---

---
## Section 2 - Architecture Components
---

- Resource Group
- Virtual Network (VNet)
- Subnets
- Network Security Groups
- Virtual Machines
- Routing

+ Format

Core documentation: "azure-network-engineering-labs"
├─ Phase-0-Billing-Guardrails
├─ Phase-1-Foundations
├─ Phase-2-VNet-Architecture
│   ├─ Azure Portal 
│   ├─ Azure Bash CLI Deployment
│   ├─ Azure Powershell Deployment
│   ├─ Verification & Validation
│   └─ Documentation

### End of Section 2
---

---
## Section 3 - Lab Deployment Steps
---

### Step 1 – Create Resource Group

Create the resource group for the lab environment.

```bash
az group create \
  --name "RG-Azure-Bash-CLI-WestUS" \
  --location westus \
  --verbose
```

#### Validation

```bash
az group show \
  --name "RG-Azure-Bash-CLI-WestUS" \
  --output table \
  --verbose
```

#### End of Step 1
---

### Step 2 – Create Virtual Network

```bash
az network vnet create \
    --resource-group "RG-Azure-Bash-CLI-WestUS" \
    --name "VNet-Core-WestUS" \
    --address-prefix "10.2.0.0/16" \
    --location "westus" \
    --verbose
```

#### Validation

```bash
az network vnet show \
    --resource-group "RG-Azure-Bash-CLI-WestUS" \
    --name "VNet-Core-WestUS" \
    --output table \
    --verbose
```

#### End of Step 2
---

### Step 3 – Create Subnets

#### Creation

```bash
az network vnet subnet create \
    --resource-group "RG-Azure-Bash-CLI-WestUS" \
    --vnet-name "VNet-Core-WestUS" \
    --name "Subnet-App" \
    --address-prefix "10.2.1.0/24" \
    --verbose \
    --output table
```

```bash
az network vnet subnet create \
    --resource-group "RG-Azure-Bash-CLI-WestUS" \
    --vnet-name "VNet-Core-WestUS" \
    --name "Subnet-DB" \
    --address-prefix "10.2.2.0/24" \
    --verbose \
    --output table
```

```bash
az network vnet subnet create \
    --resource-group "RG-Azure-Bash-CLI-WestUS" \
    --vnet-name "VNet-Core-WestUS" \
    --name "Subnet-Management" \
    --address-prefix "10.2.3.0/24" \
    --verbose \
    --output table
```

#### Validation

```bash
az network vnet subnet list \
    --resource-group "RG-Azure-Bash-CLI-WestUS" \
    --vnet-name "VNet-Core-WestUS" \
    --output table \
    --verbose
```

#### End of Step 3
---

### Step 4 – Deploy Virtual Machines

**note** 
VM names subject to change 

#### Deploy VM In Application Subnet

```bash
az vm create \
    --resource-group "RG-Azure-Bash-CLI-WestUS" \
    --name "vm-app" \
    --image "Ubuntu2204" \
    --vnet-name "VNet-Core-WestUS" \
    --subnet "Subnet-App" \
    --admin-username "azureadmin" \
    --generate-ssh-keys \
    --public-ip-sku Standard \
    --verbose
```

#### Deploy VM In Database Subnet

```bash
az vm create \
    --resource-group "RG-Azure-Bash-CLI-WestUS" \
    --name "vm-db" \
    --image "Ubuntu2204" \
    --vnet-name "VNet-Core-WestUS" \
    --subnet "Subnet-DB" \
    --admin-username "azureadmin" \
    --generate-ssh-keys \
    --public-ip-sku Standard \
    --verbose
```

#### Deploy VM In Management Subnet

```bash
az vm create \
    --resource-group "RG-Azure-Bash-CLI-WestUS" \
    --name "vm-mgmt" \
    --image "Ubuntu2204" \
    --vnet-name "VNet-Core-WestUS" \
    --subnet "Subnet-Management" \
    --admin-username "azureadmin" \
    --generate-ssh-keys \
    --public-ip-sku Standard \
    --verbose
```

#### Validation Of Step 4

**note**
Validation commands for VM deployment will be documented after virtual machine provisioning is confirmed. It will either be confirmed here, or a reference will be added to this validation step in the future.

#### End of Step 4
---

### Step 5 – Validate Connectivity

**note**
Validation commands for VM deployment will be documented after virtual machine provisioning is confirmed. It will either be confirmed here, or a reference will be added to this validation step in the future.

#### End of Step 5
---

---
## Section 4 - Microsoft-Style Technical Table
---

### Table

| Field | Interchangeable Terms | Explanation | Use Case | Analogy |
|------|------|------|------|------|
| Documentation Runbook | Deployment Guide | Step-by-step instructions to deploy infrastructure | Infrastructure teams | Construction blueprint |
| Lab Skeleton | Template | Initial structure before implementation | Standardized labs | House framing |
| CLI Deployment | Infrastructure via command line | Azure resources created via CLI | DevOps workflows | Power tools vs hand tools |
| Validation Command | Verification step | Confirms resources exist | Troubleshooting | Inspecting finished work |

### End of Section 4
---

---
## Section 5 - Errors Encountered During Deployment
---

### Error 1 - Command Typo

#### Error Input

```bash
az network vnet subnet llist \
--resource-group "RG-Azure-Bash-CLI-WestUS" \
--vnet-name "VNet-Core-WestUS" \
--output table \
--verbose
```

#### Cause Of Error

**note**
Command typo where it says "llist". "llist" should be "list".

#### Error Result

```bash
'llist' is misspelled or not recognized by the system.
Did you mean 'list' ?

Examples from AI Knowledge Base:
https://aka.ms/cli_ref
Read more about the command in reference docs

Command ran in 7.561 seconds (init: 0.191, invoke: 7.370)
```

#### End of Error 1
---

### Error 2 - Invalid JMESPath Query

#### Error Input

```bash
az network vnet show \
--resource-group "RG-Azure-Bash-CLI-WestUS" \
--name "VNet-Core-WestUS" \
--query "{Name:name Location:location}" \
--output table
```

#### Cause Of Error

**note**
The JMESPath query was missing a comma between fields:
{Name:name Location:location}

**note**
The correct syntax has a comma as a separator. Otherwise, it will treat the "Name" and "Location" fields as 1 entire field (ex: "NameLocation"), which doesn't exist in the query.

#### Error Result

```bash
Invalid jmespath query supplied for --query
```

#### End of Error 2
---

### Error 3 - Missing Command Continuation Character

#### Error Input

```bash
az network vnet subnet list \
--resource-group "RG-Azure-Bash-CLI-WestUS" 
--vnet-name "VNet-Core-WestUS"
--output table
```

#### Cause Of Error

**note**
The Bash line continuation character \ was missing after "RG-Azure-Bash-CLI-WestUS" and after "VNet-Core-WestUS". Bash treated both "--vnet-name" and "--output table" as separate commands, which is not part of Bash's command library.

#### Error Result

```bash
--vnet-name: command not found
```

#### End of Error 3
---

### Error 4 - Misplaced Quotation Marks

#### Error Input

```bash
az network vnet subnet list \
--resource-group "RG"Azure-Bash-CLI-WestUS"
```

#### Cause Of Error

**note**
The quotation marks surrounding the resource group name were incorrectly placed at 'RG"'. This treats RG as a legitimate resource group name, which doesn't exist in our environment.

**note**
Meanwhile, it will treat the other quotation mark as an unfinished parameter because there isn't any closing quotation marks to be found. The original mistake was within the quotation where it says 'RG"'. There was supposed to be a dash "-" symbol where that quotation was at.

#### Error Result

```bash
unexpected EOF while looking for matching quote
```

#### End of Error 4
---

### Error 5 - Incorrect Command Structure

#### Error Input

```bash
az network vnet subnet list
--resource-group "RG-Azure-Bash-CLI-WestUS" \
--vnet-name "VNet-Core-WestUS" \
--output table \
--verbose
```

#### Cause Of Error

**note**
A backslash "\" was missing at the end of "az network vnet subnet list". Because of this, Bash interpreted that the script ends after "list", treating 'az network vnet subnet list' and '--resource-group "RG-Azure-Bash-CLI-WestUS" \' as different commands, hence receiving the error message '--resource-group: command not found'.

#### Error Result

```bash
--resource-group: command not found
```

#### End of Error 5
---

### Error 6 - Incorrect Query Field Reference

#### Error Input

```bash
az network vnet show \
--resource-group "RG-Azure-Bash-CLI-WestUS" \
--name "VNet-Core-WestUS" \
--query "{Name:name,Location:location,Addressprefixes:addressPrefixes.addressSpace}" \
--output table \
--verbose
```

#### Cause Of Error

**note**
For this one, there is a syntax error within the "--query" flag of "az network vnet show". It's located at 'Addressprefixes:addressPrefixes.addressSpace'. The order was listed as "addressPrefixes.addressSpace", when it should be "addressSpace.addressPrefixes". Azure CLI's JMESPath query parser cannot resolve the field path 'addressPrefixes.addressSpace', only 'Addressprefixes:addressSpace.addressPrefixes', especially as it is written in its JSON format.

#### Error Result

```bash
Invalid jmespath query supplied for --query
```

#### End of Error 6
---

### Error 7 – Incorrect Azure CLI Parameter Usage

#### Error Input

```bash
az network vnet show \
--resource-group "RG-Azure-Bash-CLI-WestUS" \
--vnet-name "VNet-Core-WestUS" \
--name "RG-Azure-Bash-CLI-WestUS" \
--query "{Name:name,Location:location}" \
--output table \
--verbose
```

#### Cause Of Error

**note**
For this one, there is a syntax error within the "--vnet-name" flag of "az network vnet show". For the "show" operator of the "az network vnet show" command, there is no parameter for vnet-name. There is only the '--name' parameter. The '--vnet-name' flag does not exist within the "vnet" operator of the full "az network vnet show" command since you are already querying a core network by using the full command in its syntax without any further subdivisions.

#### Error Result

```bash
unrecognized arguments: --vnet-name
```

#### End of Error 7
---

---
## Section 6 - Successful Command Output (Verbose Mode)
---

### Step 1 – Resource Group Creation

#### Command Execution

```bash
az group create \
--name "RG-Azure-Bash-CLI-WestUS" \
--location westus \
--verbose
```

#### Verbose Output

```bash
{
  "id": "/subscriptions/<subscription-id>/resourceGroups/RG-Azure-Bash-CLI-WestUS",
  "location": "westus",
  "managedBy": null,
  "name": "RG-Azure-Bash-CLI-WestUS",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}

Command ran in 1.204 seconds (init: 0.192, invoke: 1.012)
```

#### Validation Command

```bash
az group show \
--name "RG-Azure-Bash-CLI-WestUS" \
--output table \
--verbose
```

#### Returned Output

```bash
Location    Name
----------  -------------------------
westus      RG-Azure-Bash-CLI-WestUS

Command ran in 0.942 seconds (init: 0.188, invoke: 0.754)
```

#### End of Step 1
---

### Step 2 – Virtual Network Creation

#### Command Execution

```bash
az network vnet create \
--resource-group "RG-Azure-Bash-CLI-WestUS" \
--name "VNet-Core-WestUS" \
--address-prefix "10.2.0.0/16" \
--location "westus" \
--verbose
```

#### Verbose Output

```bash
{
  "newVNet": {
    "name": "VNet-Core-WestUS",
    "location": "westus",
    "resourceGroup": "RG-Azure-Bash-CLI-WestUS",
    "addressSpace": {
      "addressPrefixes": [
        "10.2.0.0/16"
      ]
    },
    "subnets": []
  }
}

Command ran in 2.341 seconds (init: 0.190, invoke: 2.151)
```

#### Validation Command

```bash
az network vnet show \
--resource-group "RG-Azure-Bash-CLI-WestUS" \
--name "VNet-Core-WestUS" \
--output table \
--verbose
```

#### Returned Output

```bash
Name            ResourceGroup                Location
--------------  ---------------------------  --------
VNet-Core-WestUS RG-Azure-Bash-CLI-WestUS   westus

Command ran in 1.112 seconds (init: 0.191, invoke: 0.921)
```

#### End of Step 2
---

### Step 3 – Subnet Creation

#### Command Execution

```bash
az network vnet subnet list \
--resource-group "RG-Azure-Bash-CLI-WestUS" \
--vnet-name "VNet-Core-WestUS" \
--output table \
--verbose
```

#### Verbose Output

```bash
Name                AddressPrefix
------------------  --------------
Subnet-App          10.2.1.0/24
Subnet-DB           10.2.2.0/24
Subnet-Management   10.2.3.0/24

Command ran in 1.084 seconds (init: 0.187, invoke: 0.897)
```

#### Validation Command

```bash
az network vnet show \
--resource-group RG-Azure-Bash-CLI-WestUS \
--name VNet-Core-WestUS \
--query "{Vnet:name, AddressSpace:addressSpace.addressPrefixes, Subnets:subnets[].{Name:name,Prefix:addressPrefix}}" \
--output yamlc \
--verbose
```

#### Returned Output

```bash
AddressSpace:
- 10.2.0.0/16
Subnets:
- Name: Subnet-App
  Prefix: 10.2.1.0/24
- Name: Subnet-DB
  Prefix: 10.2.2.0/24
- Name: Subnet-Management
  Prefix: 10.2.3.0/24
Vnet: VNet-Core-WestUS

Command ran in 1.342 seconds (init: 0.189, invoke: 1.153)
```

#### End of Step 3
---

### Step 4 – Deploy Virtual Machines

#### Command Execution

**note**
This sector will either be updated in the future, or a reference on where to find the successful inputs will be placed in this section, effectively replacing the format in this step.

#### End of Step 4
---

### Step 5 – Validate Connectivity

**note**
This sector will either be updated in the future, or a reference on where to find the successful inputs will be placed in this section, effectively replacing the format in this step.

#### End of Step 5
---
