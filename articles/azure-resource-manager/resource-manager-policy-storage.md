---
title: Directivas de recursos de Azure para cuentas de almacenamiento | Microsoft Docs
description: "Se describen las directivas de Azure Resource Manager para administrar la implementación de cuentas de almacenamiento."
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
ms.openlocfilehash: 6612ee61f5c50e743241b92030660cea7ae7094d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="apply-resource-policies-to-storage-accounts"></a><span data-ttu-id="077ae-103">Aplicación de directivas de recursos a cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="077ae-103">Apply resource policies to storage accounts</span></span>
<span data-ttu-id="077ae-104">En este tema se muestran varias [directivas de recursos](resource-manager-policy.md) que puede aplicar a cuentas de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="077ae-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply to Azure storage accounts.</span></span> <span data-ttu-id="077ae-105">Estas directivas garantizan la coherencia de las cuentas de almacenamiento implementada en la organización.</span><span class="sxs-lookup"><span data-stu-id="077ae-105">These policies ensure consistency for the storage accounts deployed in your organization.</span></span> 

## <a name="define-permitted-storage-account-types"></a><span data-ttu-id="077ae-106">Definición de tipos de cuenta de almacenamiento permitidos</span><span class="sxs-lookup"><span data-stu-id="077ae-106">Define permitted storage account types</span></span>

<span data-ttu-id="077ae-107">La siguiente directiva restringe qué [tipos de cuenta de almacenamiento](../storage/common/storage-redundancy.md) se pueden implementar:</span><span class="sxs-lookup"><span data-stu-id="077ae-107">The following policy restricts which [storage account types](../storage/common/storage-redundancy.md) can be deployed:</span></span>

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

<span data-ttu-id="077ae-108">Una regla de directiva similar con un parámetro para aceptar las SKU permitidas está disponible como una definición de directiva integrada.</span><span class="sxs-lookup"><span data-stu-id="077ae-108">A similar policy rule with a parameter for accepting the allowed SKUs is available as a built-in policy definition.</span></span> <span data-ttu-id="077ae-109">La directiva integrada tiene el identificador de recurso `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span><span class="sxs-lookup"><span data-stu-id="077ae-109">The built-in policy has the resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span></span> 

## <a name="define-permitted-access-tier"></a><span data-ttu-id="077ae-110">Definición del nivel de acceso permitido</span><span class="sxs-lookup"><span data-stu-id="077ae-110">Define permitted access tier</span></span>

<span data-ttu-id="077ae-111">La siguiente directiva especifica el tipo de [nivel de acceso](../storage/blobs/storage-blob-storage-tiers.md) que se puede especificar para las cuentas de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="077ae-111">The following policy specifies the type of [access tier](../storage/blobs/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span></span>

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

## <a name="ensure-encryption-is-enabled"></a><span data-ttu-id="077ae-112">Comprobación de que esté habilitado el cifrado</span><span class="sxs-lookup"><span data-stu-id="077ae-112">Ensure encryption is enabled</span></span>

<span data-ttu-id="077ae-113">La siguiente directiva requiere que todas las cuentas de almacenamiento habiliten el [cifrado del servicio Storage](../storage/common/storage-service-encryption.md):</span><span class="sxs-lookup"><span data-stu-id="077ae-113">The following policy requires all storage accounts to enable [Storage service encryption](../storage/common/storage-service-encryption.md):</span></span>

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

<span data-ttu-id="077ae-114">Esta regla de directiva también está disponible como una definición de directiva integrada con el identificador de recurso `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span><span class="sxs-lookup"><span data-stu-id="077ae-114">This policy rule is also available as a built-in policy definition with the resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="077ae-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="077ae-115">Next steps</span></span>
* <span data-ttu-id="077ae-116">Después de definir una regla de directiva (como se muestra en los ejemplos anteriores), debe crear la definición de directiva y asignarla a un ámbito.</span><span class="sxs-lookup"><span data-stu-id="077ae-116">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="077ae-117">El ámbito puede ser una suscripción, un grupo de recursos o un recurso.</span><span class="sxs-lookup"><span data-stu-id="077ae-117">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="077ae-118">Para asignar directivas a través del portal, consulte [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) (Uso de Azure Portal para asignar y administrar directivas de recursos).</span><span class="sxs-lookup"><span data-stu-id="077ae-118">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="077ae-119">Para asignar directivas a través de la API de REST, PowerShell o la CLI de Azure, consulte [Assign and manage policies through script](resource-manager-policy-create-assign.md) (Asignación y administración de directivas a través de scripts).</span><span class="sxs-lookup"><span data-stu-id="077ae-119">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="077ae-120">Para obtener instrucciones sobre cómo las empresas pueden utilizar Resource Manager para administrar eficazmente las suscripciones, vea [Scaffold empresarial de Azure: Gobierno de suscripción prescriptivo](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="077ae-120">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

