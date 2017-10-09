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
# <a name="apply-policies-toowindows-vms-with-azure-resource-manager"></a><span data-ttu-id="10b3a-103">Aplicar directivas tooWindows máquinas virtuales con el Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="10b3a-103">Apply policies tooWindows VMs with Azure Resource Manager</span></span>
<span data-ttu-id="10b3a-104">Mediante el uso de directivas, una organización puede aplicar varias reglas de empresa de Hola y convenciones.</span><span class="sxs-lookup"><span data-stu-id="10b3a-104">By using policies, an organization can enforce various conventions and rules throughout hello enterprise.</span></span> <span data-ttu-id="10b3a-105">Cumplimiento del comportamiento deseado de Hola puede ayudar a mitigar el riesgo mientras contribuye éxito de toohello de organización de Hola.</span><span class="sxs-lookup"><span data-stu-id="10b3a-105">Enforcement of hello desired behavior can help mitigate risk while contributing toohello success of hello organization.</span></span> <span data-ttu-id="10b3a-106">En este artículo se describe cómo puede utilizar comportamiento de Azure Resource Manager directivas toodefine Hola deseado para las máquinas virtuales de su organización.</span><span class="sxs-lookup"><span data-stu-id="10b3a-106">In this article, we describe how you can use Azure Resource Manager policies toodefine hello desired behavior for your organization’s Virtual Machines.</span></span>

<span data-ttu-id="10b3a-107">Para una toopolicies introducción, consulte [recursos toomanage de directiva de uso y controlar el acceso](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="10b3a-107">For an introduction toopolicies, see [Use Policy toomanage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="10b3a-108">Máquinas virtuales permitidas</span><span class="sxs-lookup"><span data-stu-id="10b3a-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="10b3a-109">tooensure que las máquinas virtuales para su organización son compatibles con una aplicación, puede restringir Hola permitida sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="10b3a-109">tooensure that virtual machines for your organization are compatible with an application, you can restrict hello permitted operating systems.</span></span> <span data-ttu-id="10b3a-110">Hola siguiente ejemplo de directiva, permitir solo toobe de máquinas virtuales de Windows Server 2012 R2 Datacenter creado:</span><span class="sxs-lookup"><span data-stu-id="10b3a-110">In hello following policy example, you allow only Windows Server 2012 R2 Datacenter Virtual Machines toobe created:</span></span>

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

<span data-ttu-id="10b3a-111">Use un Hola de toomodify comodín anterior directiva tooallow cualquier imagen de Windows Server Datacenter:</span><span class="sxs-lookup"><span data-stu-id="10b3a-111">Use a wild card toomodify hello preceding policy tooallow any Windows Server Datacenter image:</span></span>

```json
{
  "field": "Microsoft.Compute/imageSku",
  "like": "*Datacenter"
}
```

<span data-ttu-id="10b3a-112">Use anyOf toomodify Hola anterior directiva tooallow cualquier Windows Server 2012 R2 Datacenter o imagen superior:</span><span class="sxs-lookup"><span data-stu-id="10b3a-112">Use anyOf toomodify hello preceding policy tooallow any Windows Server 2012 R2 Datacenter or higher image:</span></span>

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

<span data-ttu-id="10b3a-113">Para obtener información sobre los campos de directiva, vea [Alias de directiva](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="10b3a-113">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="10b3a-114">Discos administrados</span><span class="sxs-lookup"><span data-stu-id="10b3a-114">Managed disks</span></span>

<span data-ttu-id="10b3a-115">toorequire Hola uso de discos administrados, Hola de uso después de la directiva:</span><span class="sxs-lookup"><span data-stu-id="10b3a-115">toorequire hello use of managed disks, use hello following policy:</span></span>

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

## <a name="images-for-virtual-machines"></a><span data-ttu-id="10b3a-116">Imágenes para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="10b3a-116">Images for Virtual Machines</span></span>

<span data-ttu-id="10b3a-117">Por motivos de seguridad, puede obligar a que solo las imágenes personalizadas aprobadas se puedan implementar en su entorno.</span><span class="sxs-lookup"><span data-stu-id="10b3a-117">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="10b3a-118">Puede especificar el grupo de recursos de Hola que contiene imágenes de hello aprobado, o imágenes aprobadas específico de Hola.</span><span class="sxs-lookup"><span data-stu-id="10b3a-118">You can specify either hello resource group that contains hello approved images, or hello specific approved images.</span></span>

<span data-ttu-id="10b3a-119">Hola siguiente ejemplo requiere imágenes desde un grupo de recursos aprobados:</span><span class="sxs-lookup"><span data-stu-id="10b3a-119">hello following example requires images from an approved resource group:</span></span>

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

<span data-ttu-id="10b3a-120">Hello en el ejemplo siguiente se especifica la imagen de hello aprobado identificadores:</span><span class="sxs-lookup"><span data-stu-id="10b3a-120">hello following example specifies hello approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="10b3a-121">Extensiones de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="10b3a-121">Virtual Machine extensions</span></span>

<span data-ttu-id="10b3a-122">Puede que desee tooforbid uso de ciertos tipos de extensiones.</span><span class="sxs-lookup"><span data-stu-id="10b3a-122">You may want tooforbid usage of certain types of extensions.</span></span> <span data-ttu-id="10b3a-123">Por ejemplo, una extensión puede no ser compatible con determinadas imágenes personalizadas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="10b3a-123">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="10b3a-124">Hola siguiente ejemplo se muestra cómo tooblock una extensión específica.</span><span class="sxs-lookup"><span data-stu-id="10b3a-124">hello following example shows how tooblock a specific extension.</span></span> <span data-ttu-id="10b3a-125">Usa toodetermine publicador y tipo que tooblock de extensión.</span><span class="sxs-lookup"><span data-stu-id="10b3a-125">It uses publisher and type toodetermine which extension tooblock.</span></span>

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


## <a name="azure-hybrid-use-benefit"></a><span data-ttu-id="10b3a-126">Ventaja de uso híbrido de Azure</span><span class="sxs-lookup"><span data-stu-id="10b3a-126">Azure Hybrid Use Benefit</span></span>

<span data-ttu-id="10b3a-127">Cuando tenga una licencia local, puede guardar precio de la licencia de hello en sus máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="10b3a-127">When you have an on-premise license, you can save hello license fee on your virtual machines.</span></span> <span data-ttu-id="10b3a-128">Cuando no tiene licencia de hello, debería prohíba opción Hola.</span><span class="sxs-lookup"><span data-stu-id="10b3a-128">When you don't have hello license, you should forbid hello option.</span></span> <span data-ttu-id="10b3a-129">Hola después directiva prohíbe el uso de Azure híbrida uso beneficio (AHUB):</span><span class="sxs-lookup"><span data-stu-id="10b3a-129">hello following policy forbids usage of Azure Hybrid Use Benefit (AHUB):</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="10b3a-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="10b3a-130">Next steps</span></span>
* <span data-ttu-id="10b3a-131">Después de definir una regla de directiva (como se muestra en hello anteriores ejemplos), se necesita la definición de la directiva de toocreate hello y se asigna tooa ámbito.</span><span class="sxs-lookup"><span data-stu-id="10b3a-131">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="10b3a-132">Hola ámbito puede ser una suscripción, el grupo de recursos o el recurso.</span><span class="sxs-lookup"><span data-stu-id="10b3a-132">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="10b3a-133">directivas de tooassign a través del portal de hello, vea [tooassign portal de Azure de uso y administrar las directivas de recursos](../../azure-resource-manager/resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="10b3a-133">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="10b3a-134">directivas de tooassign a través de la API de REST, PowerShell o CLI de Azure, consulte [asignar y administrar las directivas a través de la secuencia de comandos](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="10b3a-134">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="10b3a-135">Una directivas tooresource de introducción, consulte [información general de directivas de recursos](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="10b3a-135">For an introduction tooresource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="10b3a-136">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](../../azure-resource-manager/resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="10b3a-136">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
