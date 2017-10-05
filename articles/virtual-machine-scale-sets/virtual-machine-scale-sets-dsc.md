---
title: "Uso de la configuración de estado deseado con conjuntos de escalado de máquinas virtuales | Microsoft Docs"
description: "Uso de conjuntos de escalado de máquinas virtuales con la extensión de DSC de Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: c8f047b5-0e6c-4ef3-8a47-f1b284d32942
ms.service: virtual-machine-scale-sets
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 04/05/2017
ms.author: zachal
ms.openlocfilehash: b61b0acf3072569ab733a13defb465c921d26187
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-virtual-machine-scale-sets-with-the-azure-dsc-extension"></a><span data-ttu-id="ba530-103">Uso de conjuntos de escalado de máquinas virtuales con la extensión de DSC de Azure</span><span class="sxs-lookup"><span data-stu-id="ba530-103">Using Virtual Machine Scale Sets with the Azure DSC Extension</span></span>
<span data-ttu-id="ba530-104">Los [conjuntos de escalado de máquinas virtuales](virtual-machine-scale-sets-overview.md) pueden usarse con el controlador de extensiones de [Configuración de estado deseado (DSC) de Azure](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ba530-104">[Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md) can be used with the [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extension handler.</span></span> <span data-ttu-id="ba530-105">Los conjuntos de escalado de máquinas virtuales proporcionan una manera de implementar y administrar un gran número de máquinas virtuales, y se pueden escalar y reducir horizontalmente en respuesta a la carga.</span><span class="sxs-lookup"><span data-stu-id="ba530-105">Virtual machine scale sets provide a way to deploy and manage large numbers of virtual machines, and can elastically scale in and out in response to load.</span></span> <span data-ttu-id="ba530-106">DSC se utiliza para configurar las máquinas virtuales a medida que se conecten, ya que ejecutan el software de producción.</span><span class="sxs-lookup"><span data-stu-id="ba530-106">DSC is used to configure the VMs as they come online so they are running the production software.</span></span>

## <a name="differences-between-deploying-to-virtual-machines-and-virtual-machine-scale-sets"></a><span data-ttu-id="ba530-107">Diferencias entre implementar máquinas virtuales y conjuntos de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="ba530-107">Differences between deploying to Virtual Machines and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="ba530-108">La estructura subyacente de la plantilla para un conjunto de escalado de máquinas virtuales es ligeramente distinta a la de una sola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ba530-108">The underlying template structure for a virtual machine scale set is slightly different from a single VM.</span></span> <span data-ttu-id="ba530-109">En concreto, una sola máquina virtual implementa extensiones en el nodo virtualMachines.</span><span class="sxs-lookup"><span data-stu-id="ba530-109">Specifically, a single VM deploys extensions under the "virtualMachines" node.</span></span> <span data-ttu-id="ba530-110">Hay una entrada del tipo extensions, donde se agrega DSC a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="ba530-110">There is an entry of type "extensions" where DSC is added to the template</span></span>

```
"resources": [
          {
              "name": "Microsoft.Powershell.DSC",
              "type": "extensions",
              "location": "[resourceGroup().location]",
              "apiVersion": "2015-06-15",
              "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "tags": {
                  "displayName": "dscExtension"
              },
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": false,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "DscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }
          }
      ]
```

<span data-ttu-id="ba530-111">Un nodo del conjunto de escalado de máquinas virtuales tiene una sección "properties" con el atributo "extensionProfile" de "VirtualMachineProfile".</span><span class="sxs-lookup"><span data-stu-id="ba530-111">A virtual machine scale set node has a "properties" section with the "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="ba530-112">DSC se agrega en "extensions".</span><span class="sxs-lookup"><span data-stu-id="ba530-112">DSC is added under "extensions"</span></span>

```
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": false,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
```

## <a name="behavior-for-a-virtual-machine-scale-set"></a><span data-ttu-id="ba530-113">Comportamiento de un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="ba530-113">Behavior for a Virtual Machine Scale Set</span></span>
<span data-ttu-id="ba530-114">El comportamiento del conjunto de escalado de máquinas virtuales es idéntico al de una sola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ba530-114">The behavior for a virtual machine scale set is identical to the behavior for a single VM.</span></span> <span data-ttu-id="ba530-115">Cuando se crea una nueva máquina virtual, se aprovisiona automáticamente con la extensión de DSC.</span><span class="sxs-lookup"><span data-stu-id="ba530-115">When a new VM is created, it is automatically provisioned with the DSC extension.</span></span> <span data-ttu-id="ba530-116">Si la extensión requiere una versión más reciente de WMF, se reinicia la máquina virtual antes de conectarse.</span><span class="sxs-lookup"><span data-stu-id="ba530-116">If a newer version of the WMF is required by the extension, the VM reboots before coming online.</span></span> <span data-ttu-id="ba530-117">Cuando se conecta, descarga el archivo .zip de configuración de DSC y lo aprovisiona en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ba530-117">Once it is online, it downloads the DSC configuration .zip and provision it on the VM.</span></span> <span data-ttu-id="ba530-118">Pueden encontrar más información en el artículo de [introducción a la extensión de DSC de Azure](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ba530-118">More details can be found in [the Azure DSC Extension Overview](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba530-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ba530-119">Next steps</span></span>
<span data-ttu-id="ba530-120">Examine la [plantilla de Azure Resource Manager para la extensión de DSC](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ba530-120">Examine the [Azure Resource Manager template for the DSC extension](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="ba530-121">Obtenga información sobre cómo la [extensión de DSC administra de forma segura las credenciales](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ba530-121">Learn how the [DSC extension securely handles credentials](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="ba530-122">Para más información sobre el controlador de extensiones DSC de Azure, consulte [Introducción al controlador de extensiones de configuración de estado deseado de Azure](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ba530-122">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="ba530-123">Para más información sobre DSC de PowerShell, [visite el centro de documentación de PowerShell](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="ba530-123">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

