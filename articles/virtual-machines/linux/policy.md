---
title: "Aplicación de seguridad con directivas en máquinas virtuales Linux en Azure | Microsoft Docs"
description: "Aplicación de una directiva a una máquina virtual Linux de Azure Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 06778ab4-f8ff-4eed-ae10-26a276fc3faa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: singhkay
ms.openlocfilehash: 58eaab4fa03afc1e6a5e38bef691cce62a921ea9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="apply-policies-to-linux-vms-with-azure-resource-manager"></a><span data-ttu-id="c06f1-103">Aplicación de directivas a máquinas virtuales con Linux con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c06f1-103">Apply policies to Linux VMs with Azure Resource Manager</span></span>
<span data-ttu-id="c06f1-104">Mediante las directivas, una organización puede aplicar varias convenciones y reglas en toda la empresa.</span><span class="sxs-lookup"><span data-stu-id="c06f1-104">By using policies, an organization can enforce various conventions and rules throughout the enterprise.</span></span> <span data-ttu-id="c06f1-105">La aplicación del comportamiento deseado puede ayudar a reducir el riesgo a la vez que se contribuye al éxito de la organización.</span><span class="sxs-lookup"><span data-stu-id="c06f1-105">Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization.</span></span> <span data-ttu-id="c06f1-106">En este artículo, describimos cómo puede usar las directivas de Azure Resource Manager para definir el comportamiento deseado para las máquinas virtuales de su organización.</span><span class="sxs-lookup"><span data-stu-id="c06f1-106">In this article, we describe how you can use Azure Resource Manager policies to define the desired behavior for your organization's Virtual Machines.</span></span>

<span data-ttu-id="c06f1-107">Para obtener una introducción a las directivas, vea [Uso de directivas para administrar los recursos y controlar el acceso](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="c06f1-107">For an introduction to policies, see [Use Policy to manage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="c06f1-108">Máquinas virtuales permitidas</span><span class="sxs-lookup"><span data-stu-id="c06f1-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="c06f1-109">Para asegurarse de que las máquinas virtuales de la organización son compatibles con una aplicación, puede restringir los sistemas operativos permitidos.</span><span class="sxs-lookup"><span data-stu-id="c06f1-109">To ensure that virtual machines for your organization are compatible with an application, you can restrict the permitted operating systems.</span></span> <span data-ttu-id="c06f1-110">En este ejemplo de directiva siguiente, permitirá que se creen solo máquinas virtuales Ubuntu 14.04.2-LTS.</span><span class="sxs-lookup"><span data-stu-id="c06f1-110">In the following policy example, you allow only Ubuntu 14.04.2-LTS Virtual Machines to be created.</span></span>

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
                "Canonical"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "UbuntuServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "14.04.2-LTS"
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

<span data-ttu-id="c06f1-111">Use un carácter comodín para modificar la directiva anterior para permitir cualquier imagen de Ubuntu LTS:</span><span class="sxs-lookup"><span data-stu-id="c06f1-111">Use a wild card to modify the preceding policy to allow any Ubuntu LTS image:</span></span> 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

<span data-ttu-id="c06f1-112">Para obtener información sobre los campos de directiva, vea [Alias de directiva](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="c06f1-112">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="c06f1-113">Discos administrados</span><span class="sxs-lookup"><span data-stu-id="c06f1-113">Managed disks</span></span>

<span data-ttu-id="c06f1-114">Para requerir el uso de discos administrados, use la siguiente directiva:</span><span class="sxs-lookup"><span data-stu-id="c06f1-114">To require the use of managed disks, use the following policy:</span></span>

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

## <a name="images-for-virtual-machines"></a><span data-ttu-id="c06f1-115">Imágenes para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="c06f1-115">Images for Virtual Machines</span></span>

<span data-ttu-id="c06f1-116">Por motivos de seguridad, puede obligar a que solo las imágenes personalizadas aprobadas se puedan implementar en su entorno.</span><span class="sxs-lookup"><span data-stu-id="c06f1-116">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="c06f1-117">Puede especificar el grupo de recursos que contiene las imágenes aprobadas o las imágenes aprobadas específicas.</span><span class="sxs-lookup"><span data-stu-id="c06f1-117">You can specify either the resource group that contains the approved images, or the specific approved images.</span></span>

<span data-ttu-id="c06f1-118">En el ejemplo siguiente se requieren imágenes de un grupo de recursos aprobado:</span><span class="sxs-lookup"><span data-stu-id="c06f1-118">The following example requires images from an approved resource group:</span></span>

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

<span data-ttu-id="c06f1-119">En el ejemplo siguiente se especifican los identificadores de las imágenes aprobadas:</span><span class="sxs-lookup"><span data-stu-id="c06f1-119">The following example specifies the approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="c06f1-120">Extensiones de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c06f1-120">Virtual Machine extensions</span></span>

<span data-ttu-id="c06f1-121">Puede que desee prohibir el uso de ciertos tipos de extensiones.</span><span class="sxs-lookup"><span data-stu-id="c06f1-121">You may want to forbid usage of certain types of extensions.</span></span> <span data-ttu-id="c06f1-122">Por ejemplo, una extensión puede no ser compatible con determinadas imágenes personalizadas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c06f1-122">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="c06f1-123">En el ejemplo siguiente se muestra cómo bloquear una extensión específica.</span><span class="sxs-lookup"><span data-stu-id="c06f1-123">The following example shows how to block a specific extension.</span></span> <span data-ttu-id="c06f1-124">Utiliza el anunciante y el tipo para determinar qué extensiones se van a bloquear.</span><span class="sxs-lookup"><span data-stu-id="c06f1-124">It uses publisher and type to determine which extension to block.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="c06f1-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c06f1-125">Next steps</span></span>
* <span data-ttu-id="c06f1-126">Después de definir una regla de directiva (como se muestra en los ejemplos anteriores), debe crear la definición de directiva y asignarla a un ámbito.</span><span class="sxs-lookup"><span data-stu-id="c06f1-126">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="c06f1-127">El ámbito puede ser una suscripción, un grupo de recursos o un recurso.</span><span class="sxs-lookup"><span data-stu-id="c06f1-127">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="c06f1-128">Para asignar directivas a través del portal, consulte [Use Azure portal to assign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md) (Uso de Azure Portal para asignar y administrar directivas de recursos).</span><span class="sxs-lookup"><span data-stu-id="c06f1-128">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="c06f1-129">Para asignar directivas a través de la API de REST, PowerShell o la CLI de Azure, consulte [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md) (Asignación y administración de directivas a través de scripts).</span><span class="sxs-lookup"><span data-stu-id="c06f1-129">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="c06f1-130">Para obtener una introducción a las directivas de recursos, consulte [Uso de directivas para administrar los recursos y controlar el acceso](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="c06f1-130">For an introduction to resource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="c06f1-131">Para obtener instrucciones sobre cómo las empresas pueden utilizar Resource Manager para administrar eficazmente las suscripciones, vea [Scaffold empresarial de Azure: Gobierno de suscripción prescriptivo](../../azure-resource-manager/resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="c06f1-131">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
