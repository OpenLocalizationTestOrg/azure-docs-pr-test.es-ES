---
title: las directivas de recursos de aaaAzure las cuentas de almacenamiento | Documentos de Microsoft
description: "Describe las directivas del Administrador de recursos de Azure para administrar la implementación de Hola de cuentas de almacenamiento."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: tomfitz
ms.openlocfilehash: d37fc4bcf7cdec71b0e14f6231fc138bfb6a7893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toostorage-accounts"></a><span data-ttu-id="efb0f-103">Aplicar las cuentas toostorage de directivas de recursos</span><span class="sxs-lookup"><span data-stu-id="efb0f-103">Apply resource policies toostorage accounts</span></span>
<span data-ttu-id="efb0f-104">En este tema se muestra varios [las directivas de recursos](resource-manager-policy.md) puede aplicar tooAzure cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="efb0f-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooAzure storage accounts.</span></span> <span data-ttu-id="efb0f-105">Estas directivas garantizan la coherencia hello las cuentas de almacenamiento implementada en su organización.</span><span class="sxs-lookup"><span data-stu-id="efb0f-105">These policies ensure consistency for hello storage accounts deployed in your organization.</span></span> 

## <a name="define-permitted-storage-account-types"></a><span data-ttu-id="efb0f-106">Definición de tipos de cuenta de almacenamiento permitidos</span><span class="sxs-lookup"><span data-stu-id="efb0f-106">Define permitted storage account types</span></span>

<span data-ttu-id="efb0f-107">Hello siguiente directiva restringe que [tipos de cuenta de almacenamiento](../storage/common/storage-redundancy.md) pueden implementarse:</span><span class="sxs-lookup"><span data-stu-id="efb0f-107">hello following policy restricts which [storage account types](../storage/common/storage-redundancy.md) can be deployed:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/sku.name",
          "in": [
            "Standard_LRS",
            "Standard_GRS"
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

<span data-ttu-id="efb0f-108">Una regla de directiva similar con un parámetro para aceptar Hola permitida SKU está disponible como una definición de directiva integrado.</span><span class="sxs-lookup"><span data-stu-id="efb0f-108">A similar policy rule with a parameter for accepting hello allowed SKUs is available as a built-in policy definition.</span></span> <span data-ttu-id="efb0f-109">directiva integrada Hello tiene un identificador de recurso Hola de `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span><span class="sxs-lookup"><span data-stu-id="efb0f-109">hello built-in policy has hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span></span> 

## <a name="define-permitted-access-tier"></a><span data-ttu-id="efb0f-110">Definición del nivel de acceso permitido</span><span class="sxs-lookup"><span data-stu-id="efb0f-110">Define permitted access tier</span></span>

<span data-ttu-id="efb0f-111">Hello siguiente directiva especifica tipo hello de [nivel de acceso a](../storage/blobs/storage-blob-storage-tiers.md) que se puede especificar las cuentas de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="efb0f-111">hello following policy specifies hello type of [access tier](../storage/blobs/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="ensure-encryption-is-enabled"></a><span data-ttu-id="efb0f-112">Comprobación de que esté habilitado el cifrado</span><span class="sxs-lookup"><span data-stu-id="efb0f-112">Ensure encryption is enabled</span></span>

<span data-ttu-id="efb0f-113">Hello directiva siguiente requiere que todos los tooenable de cuentas de almacenamiento [cifrado del servicio de almacenamiento](../storage/common/storage-service-encryption.md):</span><span class="sxs-lookup"><span data-stu-id="efb0f-113">hello following policy requires all storage accounts tooenable [Storage service encryption](../storage/common/storage-service-encryption.md):</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/enableBlobEncryption",
          "equals": "true"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

<span data-ttu-id="efb0f-114">Esta regla de directiva también está disponible como una definición de directiva integrado con el Id. de recurso de Hola de `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span><span class="sxs-lookup"><span data-stu-id="efb0f-114">This policy rule is also available as a built-in policy definition with hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="efb0f-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="efb0f-115">Next steps</span></span>
* <span data-ttu-id="efb0f-116">Después de definir una regla de directiva (como se muestra en hello anteriores ejemplos), se necesita la definición de la directiva de toocreate hello y se asigna tooa ámbito.</span><span class="sxs-lookup"><span data-stu-id="efb0f-116">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="efb0f-117">Hola ámbito puede ser una suscripción, el grupo de recursos o el recurso.</span><span class="sxs-lookup"><span data-stu-id="efb0f-117">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="efb0f-118">directivas de tooassign a través del portal de hello, vea [tooassign portal de Azure de uso y administrar las directivas de recursos](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="efb0f-118">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="efb0f-119">directivas de tooassign a través de la API de REST, PowerShell o CLI de Azure, consulte [asignar y administrar las directivas a través de la secuencia de comandos](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="efb0f-119">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="efb0f-120">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="efb0f-120">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

