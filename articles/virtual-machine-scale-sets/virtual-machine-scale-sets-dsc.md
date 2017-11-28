---
title: "aaaUsing deseado estado con Virtual Machine escala conjuntos de configuración | Documentos de Microsoft"
description: "Usar conjuntos de escalas de máquina Virtual con hello extensión de DSC de Azure"
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
ms.openlocfilehash: a35f1ca6700aa4889978032aa512882db50d6573
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a><span data-ttu-id="fc40c-103">Usar conjuntos de escalas de máquina Virtual con hello extensión de DSC de Azure</span><span class="sxs-lookup"><span data-stu-id="fc40c-103">Using Virtual Machine Scale Sets with hello Azure DSC Extension</span></span>
<span data-ttu-id="fc40c-104">[Conjuntos de escalas de máquina virtual](virtual-machine-scale-sets-overview.md) puede utilizarse con hello [configuración de estado deseado (DSC) de Azure](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) controlador de extensión.</span><span class="sxs-lookup"><span data-stu-id="fc40c-104">[Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md) can be used with hello [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extension handler.</span></span> <span data-ttu-id="fc40c-105">Conjuntos de escalas de máquina virtual proporcionan una manera toodeploy y administración un gran número de máquinas virtuales y elásticamente pueden escalar de entrada y salida en tooload de respuesta.</span><span class="sxs-lookup"><span data-stu-id="fc40c-105">Virtual machine scale sets provide a way toodeploy and manage large numbers of virtual machines, and can elastically scale in and out in response tooload.</span></span> <span data-ttu-id="fc40c-106">DSC es hello tooconfigure usa máquinas virtuales que incluyen en línea, por lo que se está ejecutando software de producción de hello.</span><span class="sxs-lookup"><span data-stu-id="fc40c-106">DSC is used tooconfigure hello VMs as they come online so they are running hello production software.</span></span>

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a><span data-ttu-id="fc40c-107">Diferencias entre implementar tooVirtual máquinas y conjuntos de escalas de máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="fc40c-107">Differences between deploying tooVirtual Machines and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="fc40c-108">Hola de estructura de plantilla subyacente de un conjunto de escalas de máquina virtual es ligeramente diferente de una sola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fc40c-108">hello underlying template structure for a virtual machine scale set is slightly different from a single VM.</span></span> <span data-ttu-id="fc40c-109">En concreto, en una sola máquina virtual se implementa extensiones en el nodo de "virtualMachines" Hola.</span><span class="sxs-lookup"><span data-stu-id="fc40c-109">Specifically, a single VM deploys extensions under hello "virtualMachines" node.</span></span> <span data-ttu-id="fc40c-110">Hay una entrada del tipo "extensiones" donde DSC se agrega la plantilla de toohello</span><span class="sxs-lookup"><span data-stu-id="fc40c-110">There is an entry of type "extensions" where DSC is added toohello template</span></span>

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

<span data-ttu-id="fc40c-111">Un nodo de conjunto de escala de máquina virtual tiene una sección "propiedades" con "VirtualMachineProfile", "extensionProfile" atributo hello.</span><span class="sxs-lookup"><span data-stu-id="fc40c-111">A virtual machine scale set node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="fc40c-112">DSC se agrega en "extensions".</span><span class="sxs-lookup"><span data-stu-id="fc40c-112">DSC is added under "extensions"</span></span>

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

## <a name="behavior-for-a-virtual-machine-scale-set"></a><span data-ttu-id="fc40c-113">Comportamiento de un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="fc40c-113">Behavior for a Virtual Machine Scale Set</span></span>
<span data-ttu-id="fc40c-114">comportamiento de Hola para un conjunto de escalas de máquina virtual es idéntico toohello comportamiento para una sola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fc40c-114">hello behavior for a virtual machine scale set is identical toohello behavior for a single VM.</span></span> <span data-ttu-id="fc40c-115">Cuando se crea una nueva máquina virtual, se aprovisiona automáticamente con hello extensión de DSC.</span><span class="sxs-lookup"><span data-stu-id="fc40c-115">When a new VM is created, it is automatically provisioned with hello DSC extension.</span></span> <span data-ttu-id="fc40c-116">Si una versión más reciente de hello que WMF se requiere por extensión hello, Hola VM se reinicia antes de ponerse en línea.</span><span class="sxs-lookup"><span data-stu-id="fc40c-116">If a newer version of hello WMF is required by hello extension, hello VM reboots before coming online.</span></span> <span data-ttu-id="fc40c-117">Una vez que está en línea, descarga Hola DSC configuración .zip y aprovisionar en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fc40c-117">Once it is online, it downloads hello DSC configuration .zip and provision it on hello VM.</span></span> <span data-ttu-id="fc40c-118">Pueden encontrar más detalles en [Hola Introducción a la extensión DSC Azure](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc40c-118">More details can be found in [hello Azure DSC Extension Overview](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc40c-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fc40c-119">Next steps</span></span>
<span data-ttu-id="fc40c-120">Examinar hello [plantilla de administrador de recursos de Azure para la extensión de hello DSC](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc40c-120">Examine hello [Azure Resource Manager template for hello DSC extension](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="fc40c-121">Obtenga información acerca de cómo Hola [extensión de DSC administra de forma segura las credenciales](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc40c-121">Learn how hello [DSC extension securely handles credentials](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="fc40c-122">Para obtener más información sobre el controlador de extensión de DSC de Azure de hello, consulte [controlador de extensión de configuración de estado deseado de Azure de introducción toohello](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc40c-122">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="fc40c-123">Para obtener más información sobre PowerShell DSC, [visite el centro de documentación de PowerShell de hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="fc40c-123">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

