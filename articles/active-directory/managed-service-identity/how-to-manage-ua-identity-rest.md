---
title: How to manage Azure user assigned managed identities using REST
description: Step by step instructions on how to create, list and delete a user assigned managed identity to make REST API calls.
services: active-directory
documentationcenter: 
author: daveba
manager: mtillman
editor: 
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/26/2018
ms.author: daveba
---

# Create, list or delete a user assigned identity using REST API calls

[!INCLUDE[preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]

Managed Identity provides Azure services the ability to authenticate to services that support Azure AD authentication, without needing credentials in your code. 

In this article, you learn how to create, list, and delete a user assigned managed identity using CURL to make REST API calls.

## Prerequisites

- If you're unfamiliar with Managed Service Identity, check out the [overview section](overview.md). **Be sure to review the [difference between a system assigned and user assigned identity](overview.md#how-does-it-work)**.
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.
- If you are using Windows, install the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about) or use the [Azure Cloud Shell](../../cloud-shell/overview.md) in the Azure portal.
- If you use the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about) or a [Linux distribution OS](/cli/azure/install-azure-cli-apt?view=azure-cli-latest), [Install the Azure CLI local console](/azure/install-azure-cli).
- If you are using Azure CLI local console, sign in to Azure using `az login` with an account that is associated with the Azure subscription you would like to deploy or retrieve user assigned managed identity information.
- Retrieve a Bearer access token using `az account get-access-token` to perform the following user assigned managed identity operations.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## Create a user assigned managed identity 

To create a user assigned managed identity, use the following CURL request to the Azure Resource Manager API. Replace the `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, `<USER ASSIGNED IDENTITY NAME>`,`<LOCATION>`, and `<ACCESS TOKEN>` values with your own values:

[!INCLUDE[ua-character-limit](~/includes/managed-identity-ua-character-limits.md)]

```bash
curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroup
s/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY NAME>?api-version=2015-08-31-preview' -X PUT -d '{"loc
ation": "<LOCATION>"}' -H "Content-Type: application/json" -H "Authorization: Bearer <ACCESS TOKEN>"
```

## List user assigned managed identities

To list user assigned managed identities, use the following CURL request to the Azure Resource Manager API.  Replace the `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, and `<ACCESS TOKEN>` values with your own values:

```bash
curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities?api-version=2015-08-31-preview' -H "Authorization: Bearer <ACCESS TOKEN>"
```
## Delete a user assigned managed identity

To delete a user assigned managed identity, use the following CURL request to the Azure Resource Manager API. Replace the `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, and `<ACCESS TOKEN>` parameters values with your own values:

> [!NOTE]
> Deleting a user assigned identity will not remove the reference from any resource it was assigned to. To remove a user assigned managed from a VM using CURL see [Remove a user assigned identity from an Azure VM](qs-configure-rest-vm.md#remove-a-user-assigned identity-from-an-azure-vm).

```bash
curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroup
s/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY NAME>?api-version=2015-08-31-preview' -X DELETE -H "Authorization: Bearer <ACCESS TOKEN>"
```

## Next steps

For information on how to assign a user assigned identity to an Azure VM/VMSS using CURL see, [Configure Managed Identity on an Azure VM using CURL](qs-configure-rest-vm.md#user-assigned-identity) and [Configure Managed Identity on a virtual machine scale set using CURL](qs-configure-rest-vmss.md#user-assigned-identity).


