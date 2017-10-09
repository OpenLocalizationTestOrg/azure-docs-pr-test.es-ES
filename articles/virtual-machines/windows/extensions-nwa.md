---
title: "extensión de máquina virtual de agente del Monitor de red para Windows aaaAzure | Documentos de Microsoft"
description: "Implementar Hola agente del Monitor de red en la máquina virtual de Windows con una extensión de máquina virtual."
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a>Extensión de máquina virtual del agente de Network Watcher para Windows

## <a name="overview"></a>Información general

[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) es un servicio de supervisión, diagnóstico y análisis del rendimiento de red que permite supervisar redes de Azure. Hola extensión de máquina virtual de agente del Monitor de red es un requisito para algunas de las características del Monitor de red de hello en máquinas virtuales de Azure. Esto incluye la captura del tráfico de red a petición y otra funcionalidad avanzada.

Este Hola de detalles de documento admite plataformas y opciones de implementación para hello extensión de máquina virtual de agente del Monitor de red para Windows.

## <a name="prerequisites"></a>Requisitos previos

### <a name="operating-system"></a>Sistema operativos

Hola extensión del agente de Monitor de red de Windows se pueden ejecutar en Windows Server 2008 R2, 2012, 2012 R2 y 2016 libera. Tenga en cuenta que Hola Nano Server no se admite en este momento.

### <a name="internet-connectivity"></a>Conectividad de Internet

Algunos de hello funcionalidad de agente del Monitor de red requiere a esa máquina virtual de destino de Hola sea toohello conectado Internet. Sin conexiones salientes de hello capacidad tooestablish algunas de las características del agente de Monitor de red Hola pueden funcione incorrectamente o dejan de estar disponibles. Para obtener más información, vea hello [documentación del Monitor de red](../../network-watcher/network-watcher-monitoring-overview.md).

## <a name="extension-schema"></a>Esquema de extensión

Hello JSON siguiente muestra esquema Hola Hola extensión del agente de Monitor de red. extensión de Hello no requiere ni admite cualquier configuración proporcionada por el usuario en este momento y se basa en su configuración predeterminada.

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a>Valores de propiedad

| Nombre | Valor / ejemplo |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.Azure.NetworkWatcher |
| type | NetworkWatcherAgentWindows |
| typeHandlerVersion | 1.4 |


## <a name="template-deployment"></a>Implementación de plantilla

Las extensiones de VM de Azure pueden implementarse con plantillas de Azure Resource Manager. esquema JSON de Hello detallado en la sección anterior de hello puede usarse en un hello toorun de plantilla de Azure Resource Manager extensión del agente de Monitor de red durante la implementación de plantilla Azure Resource Manager.

## <a name="powershell-deployment"></a>Implementación de PowerShell

Hola `Set-AzureRmVMExtension` comando puede ser usado toodeploy Hola agente del Monitor de red máquina virtual extensión tooan máquina virtual existente.

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a>Solución de problemas y soporte técnico

### <a name="troubleshooting"></a>Solución de problemas

Datos acerca del estado de Hola de implementaciones de extensión se pueden recuperar desde Hola portal de Azure y mediante el módulo de PowerShell de Azure de Hola. estado de implementación de hello toosee de extensiones para una máquina virtual determinada, Hola ejecución sigue usando el comando Hola módulo Azure PowerShell.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

Ejecución de la extensión de salida es posterior a toofiles registrados se encuentra en hello directorio:

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a>Soporte técnico

Si necesita más ayuda en cualquier momento en este artículo, puede consulte la documentación de la Guía de usuario del Monitor de red de toohello o póngase en contacto con hello Azure expertos en hello [foros de Azure de MSDN y el desbordamiento de la pila](https://azure.microsoft.com/en-us/support/forums/). Como alternativa, puede registrar un incidente de soporte técnico de Azure. Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/en-us/support/options/) y seleccione la obtención de soporte técnico. Para obtener información acerca del uso de soporte técnico de Azure, lea hello [P+F de soporte de Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).
