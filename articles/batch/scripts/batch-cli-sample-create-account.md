---
title: "Ejemplo de script de la CLI de Azure: creación de una cuenta de Batch | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: creación de una cuenta de Batch"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 698978fd717091c49a1375e222f46f4325431223
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-batch-account-with-the-azure-cli"></a><span data-ttu-id="6c862-103">Creación de una cuenta de Batch con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="6c862-103">Create a Batch account with the Azure CLI</span></span>

<span data-ttu-id="6c862-104">Este script crea una cuenta de Azure Batch y muestra cómo se pueden consultar y actualizar las distintas propiedades de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="6c862-104">This script creates an Azure Batch account and shows how various properties of the account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c862-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6c862-105">Prerequisites</span></span>

<span data-ttu-id="6c862-106">Instale la CLI de Azure con las instrucciones que se encuentran en la [guía de instalación de la CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli) si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="6c862-106">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="6c862-107">Script de ejemplo de la cuenta de Batch</span><span class="sxs-lookup"><span data-stu-id="6c862-107">Batch account sample script</span></span>

<span data-ttu-id="6c862-108">Cuando crea una cuenta de Batch, la configuración predeterminada indica que el servicio de Batch asigna de forma interna sus nodos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="6c862-108">When you create a Batch account, by default its compute nodes are assigned internally by the Batch service.</span></span> <span data-ttu-id="6c862-109">Los nodos de ejecución asignados estarán sujetos a una cuota de núcleos independiente y la cuenta se puede autenticar ya sea a través de credenciales clave compartidas o un token de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6c862-109">Allocated compute nodes will be subject to a separate core quota and the account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

<span data-ttu-id="6c862-110">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Creación de cuenta")]</span><span class="sxs-lookup"><span data-stu-id="6c862-110">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]</span></span>

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="6c862-111">Cuenta de Batch con un script de ejemplo de suscripción de usuario</span><span class="sxs-lookup"><span data-stu-id="6c862-111">Batch account using user subscription sample script</span></span>

<span data-ttu-id="6c862-112">También puede optar porque Batch cree los nodos de ejecución en su propia suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c862-112">You can also opt to have Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="6c862-113">Las cuentas que asignan nodos de ejecución en la suscripción se deben autenticar a través de un token de Azure Active Directory y los nodos de ejecución asignados se contabilizarán en la cuota de suscripciones.</span><span class="sxs-lookup"><span data-stu-id="6c862-113">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and the compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="6c862-114">Para crear una cuenta de este modo, debe especificar una referencia de Key Vault cuando cree la cuenta.</span><span class="sxs-lookup"><span data-stu-id="6c862-114">To create an account in this mode, one must specify a Key Vault reference when creating the account.</span></span>

<span data-ttu-id="6c862-115">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Creación de una cuenta con suscripción de usuario")]</span><span class="sxs-lookup"><span data-stu-id="6c862-115">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6c862-116">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="6c862-116">Clean up deployment</span></span>

<span data-ttu-id="6c862-117">Después de ejecutar cualquiera de los scripts de ejemplo anteriores, ejecute el comando siguiente para quitar el grupo de recursos y todos los recursos relacionados (incluidas cuentas Batch, cuentas de Azure Storage y Azure Key Vault).</span><span class="sxs-lookup"><span data-stu-id="6c862-117">After you run either of the above sample scripts, run the following command to remove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6c862-118">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="6c862-118">Script explanation</span></span>

<span data-ttu-id="6c862-119">Este script usa los siguientes comandos para crear un grupo de recursos, una cuenta de Batch y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="6c862-119">This script uses the following commands to create a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="6c862-120">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="6c862-120">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="6c862-121">Comando</span><span class="sxs-lookup"><span data-stu-id="6c862-121">Command</span></span> | <span data-ttu-id="6c862-122">Notas</span><span class="sxs-lookup"><span data-stu-id="6c862-122">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6c862-123">az group create</span><span class="sxs-lookup"><span data-stu-id="6c862-123">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6c862-124">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="6c862-124">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6c862-125">az batch account create</span><span class="sxs-lookup"><span data-stu-id="6c862-125">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="6c862-126">Crea la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="6c862-126">Creates the Batch account.</span></span>  |
| [<span data-ttu-id="6c862-127">az batch account set</span><span class="sxs-lookup"><span data-stu-id="6c862-127">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="6c862-128">Actualiza las propiedades de la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="6c862-128">Updates properties of the Batch account.</span></span>  |
| [<span data-ttu-id="6c862-129">az batch account show</span><span class="sxs-lookup"><span data-stu-id="6c862-129">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="6c862-130">Recupera los detalles de la cuenta de Batch especificada.</span><span class="sxs-lookup"><span data-stu-id="6c862-130">Retrieves details of the specified Batch account.</span></span>  |
| [<span data-ttu-id="6c862-131">az batch account keys list</span><span class="sxs-lookup"><span data-stu-id="6c862-131">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="6c862-132">Recupera las claves de acceso de la cuenta de Batch especificada.</span><span class="sxs-lookup"><span data-stu-id="6c862-132">Retrieves the access keys of the specified Batch account.</span></span>  |
| [<span data-ttu-id="6c862-133">az batch account login</span><span class="sxs-lookup"><span data-stu-id="6c862-133">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="6c862-134">Realiza la autenticación respecto de la cuenta de Batch especificada para una mayor interacción de la CLI.</span><span class="sxs-lookup"><span data-stu-id="6c862-134">Authenticates against the specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="6c862-135">az storage account create</span><span class="sxs-lookup"><span data-stu-id="6c862-135">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="6c862-136">Crea una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="6c862-136">Creates a storage account.</span></span> |
| [<span data-ttu-id="6c862-137">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="6c862-137">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="6c862-138">Crea un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="6c862-138">Creates a key vault.</span></span> |
| [<span data-ttu-id="6c862-139">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="6c862-139">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="6c862-140">Actualiza la directiva de seguridad del almacén de Key Vault especificado.</span><span class="sxs-lookup"><span data-stu-id="6c862-140">Update the security policy of the specified key vault.</span></span> |
| [<span data-ttu-id="6c862-141">az group delete</span><span class="sxs-lookup"><span data-stu-id="6c862-141">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="6c862-142">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="6c862-142">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6c862-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6c862-143">Next steps</span></span>

<span data-ttu-id="6c862-144">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6c862-144">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6c862-145">Puede encontrar ejemplos de script adicionales de la CLI de Batch en la [documentación de la CLI de Azure Batch](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6c862-145">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
