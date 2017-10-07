---
title: Ejemplo de secuencia de comandos de CLI - aaaAzure crear una cuenta de lote | Documentos de Microsoft
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
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a><span data-ttu-id="54cad-103">Crear una cuenta de lote con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="54cad-103">Create a Batch account with hello Azure CLI</span></span>

<span data-ttu-id="54cad-104">Este script crea una cuenta de lote de Azure y muestra cómo varias propiedades de cuenta de hello pueden consultar y actualizar.</span><span class="sxs-lookup"><span data-stu-id="54cad-104">This script creates an Azure Batch account and shows how various properties of hello account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54cad-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="54cad-105">Prerequisites</span></span>

<span data-ttu-id="54cad-106">Instalación Hola CLI de Azure utilizando instrucciones de hello proporcionadas en hello [Guía de instalación de CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="54cad-106">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="54cad-107">Script de ejemplo de la cuenta de Batch</span><span class="sxs-lookup"><span data-stu-id="54cad-107">Batch account sample script</span></span>

<span data-ttu-id="54cad-108">Cuando se crea una cuenta de lote, de forma predeterminada los nodos de proceso se asignan internamente por hello servicio por lotes.</span><span class="sxs-lookup"><span data-stu-id="54cad-108">When you create a Batch account, by default its compute nodes are assigned internally by hello Batch service.</span></span> <span data-ttu-id="54cad-109">Nodos de proceso asignadas será cuota de núcleos independiente de tooa de asunto y cuenta de hello se puede autenticar mediante credenciales de clave compartida o un símbolo (token) de Active directorio de Azure.</span><span class="sxs-lookup"><span data-stu-id="54cad-109">Allocated compute nodes will be subject tooa separate core quota and hello account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="54cad-110">Cuenta de Batch con un script de ejemplo de suscripción de usuario</span><span class="sxs-lookup"><span data-stu-id="54cad-110">Batch account using user subscription sample script</span></span>

<span data-ttu-id="54cad-111">También puede optar por lotes toohave crear sus nodos de proceso en su propia suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="54cad-111">You can also opt toohave Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="54cad-112">Las cuentas que se asignan a proceso nodos en su suscripción deben ser autenticados mediante un símbolo (token) de Azure Active Directory y los nodos de proceso de hello asignados contará para la cuota de suscripción.</span><span class="sxs-lookup"><span data-stu-id="54cad-112">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and hello compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="54cad-113">toocreate una cuenta en este modo, al crear la cuenta de hello, uno debe especificar una referencia de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="54cad-113">toocreate an account in this mode, one must specify a Key Vault reference when creating hello account.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a><span data-ttu-id="54cad-114">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="54cad-114">Clean up deployment</span></span>

<span data-ttu-id="54cad-115">Después de ejecutar cualquiera de Hola por encima de las secuencias de comandos de ejemplo, ejecute hello después comando tooremove el grupo de recursos y todos ellos relacionados con recursos (incluidas las cuentas de lote, las cuentas de almacenamiento de Azure y almacenes de claves de Azure).</span><span class="sxs-lookup"><span data-stu-id="54cad-115">After you run either of hello above sample scripts, run hello following command tooremove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="54cad-116">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="54cad-116">Script explanation</span></span>

<span data-ttu-id="54cad-117">Este script utiliza Hola siguientes comandos toocreate un grupo de recursos, cuenta de lote y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="54cad-117">This script uses hello following commands toocreate a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="54cad-118">Cada comando de la tabla de hello vincula documentación específica del toocommand.</span><span class="sxs-lookup"><span data-stu-id="54cad-118">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="54cad-119">Comando</span><span class="sxs-lookup"><span data-stu-id="54cad-119">Command</span></span> | <span data-ttu-id="54cad-120">Notas</span><span class="sxs-lookup"><span data-stu-id="54cad-120">Notes</span></span> |
|---|---|
| [<span data-ttu-id="54cad-121">az group create</span><span class="sxs-lookup"><span data-stu-id="54cad-121">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="54cad-122">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="54cad-122">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="54cad-123">az batch account create</span><span class="sxs-lookup"><span data-stu-id="54cad-123">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="54cad-124">Crea la cuenta de lote de Hola.</span><span class="sxs-lookup"><span data-stu-id="54cad-124">Creates hello Batch account.</span></span>  |
| [<span data-ttu-id="54cad-125">az batch account set</span><span class="sxs-lookup"><span data-stu-id="54cad-125">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="54cad-126">Actualiza las propiedades del programa Hola a cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="54cad-126">Updates properties of hello Batch account.</span></span>  |
| [<span data-ttu-id="54cad-127">az batch account show</span><span class="sxs-lookup"><span data-stu-id="54cad-127">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="54cad-128">Recupera detalles de hello especifican cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="54cad-128">Retrieves details of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="54cad-129">az batch account keys list</span><span class="sxs-lookup"><span data-stu-id="54cad-129">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="54cad-130">Recupera las teclas de acceso de Hola de hello especifican cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="54cad-130">Retrieves hello access keys of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="54cad-131">az batch account login</span><span class="sxs-lookup"><span data-stu-id="54cad-131">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="54cad-132">Autentica contra Hola especificado cuenta para la interacción de CLI más de lote.</span><span class="sxs-lookup"><span data-stu-id="54cad-132">Authenticates against hello specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="54cad-133">az storage account create</span><span class="sxs-lookup"><span data-stu-id="54cad-133">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="54cad-134">Crea una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="54cad-134">Creates a storage account.</span></span> |
| [<span data-ttu-id="54cad-135">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="54cad-135">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="54cad-136">Crea un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="54cad-136">Creates a key vault.</span></span> |
| [<span data-ttu-id="54cad-137">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="54cad-137">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="54cad-138">Actualizar directiva de seguridad de Hola de almacén de claves especificado Hola.</span><span class="sxs-lookup"><span data-stu-id="54cad-138">Update hello security policy of hello specified key vault.</span></span> |
| [<span data-ttu-id="54cad-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="54cad-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="54cad-140">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="54cad-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="54cad-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="54cad-141">Next steps</span></span>

<span data-ttu-id="54cad-142">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="54cad-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="54cad-143">Encontrará más ejemplos de secuencias de comandos de CLI de lote en hello [documentación de CLI de lote de Azure](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="54cad-143">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
