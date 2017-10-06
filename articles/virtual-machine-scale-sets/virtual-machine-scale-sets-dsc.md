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
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a>Usar conjuntos de escalas de máquina Virtual con hello extensión de DSC de Azure
[Conjuntos de escalas de máquina virtual](virtual-machine-scale-sets-overview.md) puede utilizarse con hello [configuración de estado deseado (DSC) de Azure](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) controlador de extensión. Conjuntos de escalas de máquina virtual proporcionan una manera toodeploy y administración un gran número de máquinas virtuales y elásticamente pueden escalar de entrada y salida en tooload de respuesta. DSC es hello tooconfigure usa máquinas virtuales que incluyen en línea, por lo que se está ejecutando software de producción de hello.

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a>Diferencias entre implementar tooVirtual máquinas y conjuntos de escalas de máquina Virtual
Hola de estructura de plantilla subyacente de un conjunto de escalas de máquina virtual es ligeramente diferente de una sola máquina virtual. En concreto, en una sola máquina virtual se implementa extensiones en el nodo de "virtualMachines" Hola. Hay una entrada del tipo "extensiones" donde DSC se agrega la plantilla de toohello

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

Un nodo de conjunto de escala de máquina virtual tiene una sección "propiedades" con "VirtualMachineProfile", "extensionProfile" atributo hello. DSC se agrega en "extensions".

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

## <a name="behavior-for-a-virtual-machine-scale-set"></a>Comportamiento de un conjunto de escalado de máquinas virtuales
comportamiento de Hola para un conjunto de escalas de máquina virtual es idéntico toohello comportamiento para una sola máquina virtual. Cuando se crea una nueva máquina virtual, se aprovisiona automáticamente con hello extensión de DSC. Si una versión más reciente de hello que WMF se requiere por extensión hello, Hola VM se reinicia antes de ponerse en línea. Una vez que está en línea, descarga Hola DSC configuración .zip y aprovisionar en hello máquina virtual. Pueden encontrar más detalles en [Hola Introducción a la extensión DSC Azure](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-steps"></a>Pasos siguientes
Examinar hello [plantilla de administrador de recursos de Azure para la extensión de hello DSC](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Obtenga información acerca de cómo Hola [extensión de DSC administra de forma segura las credenciales](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Para obtener más información sobre el controlador de extensión de DSC de Azure de hello, consulte [controlador de extensión de configuración de estado deseado de Azure de introducción toohello](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Para obtener más información sobre PowerShell DSC, [visite el centro de documentación de PowerShell de hello](https://msdn.microsoft.com/powershell/dsc/overview). 

