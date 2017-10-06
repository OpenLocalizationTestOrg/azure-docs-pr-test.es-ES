---
title: "extensión de máquina virtual de agente del Monitor de red para Linux aaaAzure | Documentos de Microsoft"
description: "Implementar Hola agente del Monitor de red en la máquina virtual de Linux con una extensión de máquina virtual."
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a>Extensión de máquina virtual del agente de Network Watcher para Linux

## <a name="overview"></a>Información general

[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) es un servicio de supervisión, diagnóstico y análisis del rendimiento de red que permite supervisar redes de Azure. Hola extensión de máquina virtual de agente del Monitor de red es un requisito para algunas de las características del Monitor de red de hello en máquinas virtuales de Azure. Esto incluye la captura del tráfico de red a petición y otra funcionalidad avanzada.

Este Hola de detalles de documento admite opciones de implementación y plataformas para hello extensión de máquina virtual de agente del Monitor de red para Linux.

## <a name="prerequisites"></a>Requisitos previos

### <a name="operating-system"></a>Sistema operativos

Hola extensión del agente de Monitor de red se pueden ejecutar con las distribuciones de Linux:

| Distribución | Versión |
|---|---|
| Ubuntu | 16.04 LTS, 14.04 LTS y 12.04 LTS |
| Debian | 7 y 8 |
| Redhat | 6.x y 7.x |
| Oracle Linux | 7x |
| Suse | 11 y 12 |
| OpenSuse | 7.0 |
| CentOS | 7.0 |

Tenga en cuenta que CoreOS no se admite en este momento.

### <a name="internet-connectivity"></a>Conectividad de Internet

Algunos de hello funcionalidad de agente del Monitor de red requiere a esa máquina virtual de destino de Hola sea toohello conectado Internet. Sin conexiones salientes de hello capacidad tooestablish algunas de las características del agente de Monitor de red Hola pueden funcione incorrectamente o dejan de estar disponibles. Para obtener más información, vea hello [documentación del Monitor de red](https://review.docs.microsoft.com/en-us/azure/network-watcher/).

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
        "type": "NetworkWatcherAgentLinux",
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
| type | NetworkWatcherAgentLinux |
| typeHandlerVersion | 1.4 |

## <a name="template-deployment"></a>Implementación de plantilla

Las extensiones de VM de Azure pueden implementarse con plantillas de Azure Resource Manager. esquema JSON de Hello detallado en la sección anterior de hello puede usarse en un hello toorun de plantilla de Azure Resource Manager extensión del agente de Monitor de red durante la implementación de plantilla Azure Resource Manager.

## <a name="azure-cli-deployment"></a>Implementación de la CLI de Azure

Hola CLI de Azure puede ser usado toodeploy Hola VM de agente del Monitor de red extensión tooan máquina virtual existente.

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a>Solución de problemas y soporte técnico

### <a name="troubleshooting"></a>Solución de problemas

Datos acerca del estado de Hola de implementaciones de extensión se pueden recuperar desde Hola portal de Azure y mediante el uso de hello CLI de Azure. estado de implementación de hello toosee de extensiones para una máquina virtual determinada, ejecute hello después de usar el comando Hola CLI de Azure.

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

Ejecución de la extensión de salida es posterior a toofiles registrados se encuentra en hello directorio:

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a>Soporte técnico

Si necesita más ayuda en cualquier momento en este artículo, puede consulte la documentación del Monitor de red toohello o póngase en contacto con hello Azure expertos en hello [foros de Azure de MSDN y el desbordamiento de la pila](https://azure.microsoft.com/en-us/support/forums/). Como alternativa, puede registrar un incidente de soporte técnico de Azure. Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/en-us/support/options/) y seleccione la obtención de soporte técnico. Para obtener información acerca del uso de soporte técnico de Azure, lea hello [P+F de soporte de Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).
