# Azure ARM Template VM Deployment

## Overview

This project demonstrates the use of Azure Resource Manager (ARM) templates to deploy infrastructure as code (IaC). Instead of manually creating Azure resources through the Azure Portal, the infrastructure was defined in JSON templates and deployed using the Azure CLI.

The deployment provisions an Ubuntu Virtual Machine together with its supporting networking resources, including a Virtual Network, Subnet, Network Interface, Public IP Address, and Network Security Group.

---

## Project Objectives

- Deploy Azure resources using ARM templates.
- Parameterize the deployment using a separate parameters file.
- Validate the ARM template before deployment.
- Deploy the infrastructure using the Azure CLI.
- Verify the deployment by connecting to the Virtual Machine using SSH.

---

## Project Files

- `azure-vm-templates.json` – ARM template containing all Azure resources.
- `azure-vm-parameter.json` – Parameters file used during deployment.
- `README.md` – Project documentation.

---

## Deployment Command

```bash
az deployment group create \
  --resource-group divine-cloud-rg \
  --template-file azure-vm-templates.json \
  --parameters azure-vm-parameter.json
```

---

## Validation

Before deployment, the ARM template was validated to identify configuration errors and ensure that all required resources could be created successfully.

---

## Challenges Encountered

### 1. Public IP Configuration

The initial deployment failed because of an issue with the Public IP configuration. The template was updated to correctly configure a Static Public IP before deployment succeeded.

### 2. VM Size Availability

The original VM size (`Standard_B1s`) specified in the template was unavailable in the **South Africa North** region. I used the Azure CLI to list the available VM SKUs and identify supported VM sizes for the selected region.

### 3. Subscription Restrictions

Although some VM sizes were available in the region, they were not supported by my Azure subscription. After testing multiple options, I successfully deployed the Virtual Machine using the **Standard_D2s_v3** VM size.

### 4. Multiple Validation and Deployment Attempts

The deployment did not succeed on the first attempt. Several validation and deployment attempts were required while resolving template configuration errors. Each error was investigated and corrected until the deployment completed successfully.

### 5. SSH Authentication

After the VM was successfully deployed, my first SSH connection failed with a **"Permission denied"** error. After reviewing the deployment parameters, I realized I had entered the wrong administrator password. Using the correct password from the parameter file allowed me to successfully connect to the Ubuntu Virtual Machine via SSH.

---

## Verification

The deployment was successfully verified by:

- Deploying the ARM template using the Azure CLI.
- Confirming that the Virtual Machine appeared in the Azure Portal.
- Successfully connecting to the VM using SSH.
- Verifying that Ubuntu Linux was running on the Virtual Machine.

---

## Skills Demonstrated

- Infrastructure as Code (IaC)
- Azure Resource Manager (ARM) Templates
- Azure CLI
- Azure Virtual Machine Deployment
- Azure Networking
- ARM Template Parameterization
- Deployment Validation
- Azure Troubleshooting
- SSH Remote Access
