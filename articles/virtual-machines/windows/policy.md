---
title: "seguridad de aaaEnforce con las directivas en máquinas virtuales de Windows Azure | Documentos de Microsoft"
description: "¿Cómo tooapply una máquina Virtual de Azure Resource Manager Windows tooan de directiva"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0b71ba54-01db-43ad-9bca-8ab358ae141b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: kasing
ms.openlocfilehash: b31c8a03ecf8eed6a929f97fe4146ea14364404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="apply-policies-toowindows-vms-with-azure-resource-manager"></a>Aplicar directivas tooWindows máquinas virtuales con el Administrador de recursos de Azure
Mediante el uso de directivas, una organización puede aplicar varias reglas de empresa de Hola y convenciones. Cumplimiento del comportamiento deseado de Hola puede ayudar a mitigar el riesgo mientras contribuye éxito de toohello de organización de Hola. En este artículo se describe cómo puede utilizar comportamiento de Azure Resource Manager directivas toodefine Hola deseado para las máquinas virtuales de su organización.

Para una toopolicies introducción, consulte [recursos toomanage de directiva de uso y controlar el acceso](../../azure-resource-manager/resource-manager-policy.md).

## <a name="permitted-virtual-machines"></a>Máquinas virtuales permitidas
tooensure que las máquinas virtuales para su organización son compatibles con una aplicación, puede restringir Hola permitida sistemas operativos. Hola siguiente ejemplo de directiva, permitir solo toobe de máquinas virtuales de Windows Server 2012 R2 Datacenter creado:

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "in": [
          "Microsoft.Compute/disks",
          "Microsoft.Compute/virtualMachines",
          "Microsoft.Compute/VirtualMachineScaleSets"
        ]
      },
      {
        "not": {
          "allOf": [
            {
              "field": "Microsoft.Compute/imagePublisher",
              "in": [
                "MicrosoftWindowsServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "WindowsServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "2012-R2-Datacenter"
              ]
            },
            {
              "field": "Microsoft.Compute/imageVersion",
              "in": [
                "latest"
              ]
            }
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

Use un Hola de toomodify comodín anterior directiva tooallow cualquier imagen de Windows Server Datacenter:

```json
{
  "field": "Microsoft.Compute/imageSku",
  "like": "*Datacenter"
}
```

Use anyOf toomodify Hola anterior directiva tooallow cualquier Windows Server 2012 R2 Datacenter o imagen superior:

```json
{
  "anyOf": [
    {
      "field": "Microsoft.Compute/imageSku",
      "like": "2012-R2-Datacenter*"
    },
    {
      "field": "Microsoft.Compute/imageSku",
      "like": "2016-Datacenter*"
    }
  ]
}
```

Para obtener información sobre los campos de directiva, vea [Alias de directiva](../../azure-resource-manager/resource-manager-policy.md#aliases).

## <a name="managed-disks"></a>Discos administrados

toorequire Hola uso de discos administrados, Hola de uso después de la directiva:

```json
{
  "if": {
    "anyOf": [
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/virtualMachines"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/osDisk.uri",
            "exists": true
          }
        ]
      },
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/VirtualMachineScaleSets"
          },
          {
            "anyOf": [
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osDisk.vhdContainers",
                "exists": true
              },
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl",
                "exists": true
              }
            ]
          }
        ]
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="images-for-virtual-machines"></a>Imágenes para las máquinas virtuales

Por motivos de seguridad, puede obligar a que solo las imágenes personalizadas aprobadas se puedan implementar en su entorno. Puede especificar el grupo de recursos de Hola que contiene imágenes de hello aprobado, o imágenes aprobadas específico de Hola.

Hola siguiente ejemplo requiere imágenes desde un grupo de recursos aprobados:

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in": [
                    "Microsoft.Compute/virtualMachines",
                    "Microsoft.Compute/VirtualMachineScaleSets"
                ]
            },
            {
                "not": {
                    "field": "Microsoft.Compute/imageId",
                    "contains": "resourceGroups/CustomImage"
                }
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
} 
```

Hello en el ejemplo siguiente se especifica la imagen de hello aprobado identificadores:

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a>Extensiones de máquina virtual

Puede que desee tooforbid uso de ciertos tipos de extensiones. Por ejemplo, una extensión puede no ser compatible con determinadas imágenes personalizadas de máquina virtual. Hola siguiente ejemplo se muestra cómo tooblock una extensión específica. Usa toodetermine publicador y tipo que tooblock de extensión.

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Compute/virtualMachines/extensions"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/publisher",
                "equals": "Microsoft.Compute"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/type",
                "equals": "{extension-type}"

      }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```


## <a name="azure-hybrid-use-benefit"></a>Ventaja de uso híbrido de Azure

Cuando tenga una licencia local, puede guardar precio de la licencia de hello en sus máquinas virtuales. Cuando no tiene licencia de hello, debería prohíba opción Hola. Hola después directiva prohíbe el uso de Azure híbrida uso beneficio (AHUB):

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in":[ "Microsoft.Compute/virtualMachines","Microsoft.Compute/VirtualMachineScaleSets"]
            },
            {
                "field": "Microsoft.Compute/licenseType",
                "exists": true
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```

## <a name="next-steps"></a>Pasos siguientes
* Después de definir una regla de directiva (como se muestra en hello anteriores ejemplos), se necesita la definición de la directiva de toocreate hello y se asigna tooa ámbito. Hola ámbito puede ser una suscripción, el grupo de recursos o el recurso. directivas de tooassign a través del portal de hello, vea [tooassign portal de Azure de uso y administrar las directivas de recursos](../../azure-resource-manager/resource-manager-policy-portal.md). directivas de tooassign a través de la API de REST, PowerShell o CLI de Azure, consulte [asignar y administrar las directivas a través de la secuencia de comandos](../../azure-resource-manager/resource-manager-policy-create-assign.md).
* Una directivas tooresource de introducción, consulte [información general de directivas de recursos](../../azure-resource-manager/resource-manager-policy.md).
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](../../azure-resource-manager/resource-manager-subscription-governance.md).
