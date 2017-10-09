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
# <a name="apply-resource-policies-toostorage-accounts"></a>Aplicar las cuentas toostorage de directivas de recursos
En este tema se muestra varios [las directivas de recursos](resource-manager-policy.md) puede aplicar tooAzure cuentas de almacenamiento. Estas directivas garantizan la coherencia hello las cuentas de almacenamiento implementada en su organización. 

## <a name="define-permitted-storage-account-types"></a>Definición de tipos de cuenta de almacenamiento permitidos

Hello siguiente directiva restringe que [tipos de cuenta de almacenamiento](../storage/common/storage-redundancy.md) pueden implementarse:

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

Una regla de directiva similar con un parámetro para aceptar Hola permitida SKU está disponible como una definición de directiva integrado. directiva integrada Hello tiene un identificador de recurso Hola de `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`. 

## <a name="define-permitted-access-tier"></a>Definición del nivel de acceso permitido

Hello siguiente directiva especifica tipo hello de [nivel de acceso a](../storage/blobs/storage-blob-storage-tiers.md) que se puede especificar las cuentas de almacenamiento:

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

## <a name="ensure-encryption-is-enabled"></a>Comprobación de que esté habilitado el cifrado

Hello directiva siguiente requiere que todos los tooenable de cuentas de almacenamiento [cifrado del servicio de almacenamiento](../storage/common/storage-service-encryption.md):

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

Esta regla de directiva también está disponible como una definición de directiva integrado con el Id. de recurso de Hola de `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.

## <a name="next-steps"></a>Pasos siguientes
* Después de definir una regla de directiva (como se muestra en hello anteriores ejemplos), se necesita la definición de la directiva de toocreate hello y se asigna tooa ámbito. Hola ámbito puede ser una suscripción, el grupo de recursos o el recurso. directivas de tooassign a través del portal de hello, vea [tooassign portal de Azure de uso y administrar las directivas de recursos](resource-manager-policy-portal.md). directivas de tooassign a través de la API de REST, PowerShell o CLI de Azure, consulte [asignar y administrar las directivas a través de la secuencia de comandos](resource-manager-policy-create-assign.md). 
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).

