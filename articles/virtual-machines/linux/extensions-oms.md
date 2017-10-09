---
title: "extensión de máquina virtual de Azure para Linux aaaOMS | Documentos de Microsoft"
description: "Implementar el agente de OMS de hello en máquina virtual de Linux con una extensión de máquina virtual."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a>Extensión de máquina virtual de OMS para Linux

## <a name="overview"></a>Información general

Operations Management Suite (OMS) proporciona funcionalidades de corrección de alertas, supervisión y envío de alertas a todos los recursos locales y en la nube. Hola extensión de máquina virtual de agente de OMS para Linux se publica y compatible con Microsoft. extensión de Hello instala el agente OMS de hello en máquinas virtuales de Azure e inscribe máquinas virtuales en un área de trabajo OMS existente. Este Hola de detalles de documento admite plataformas, configuraciones y opciones de implementación para hello extensión de máquina virtual OMS para Linux.

## <a name="prerequisites"></a>Requisitos previos

### <a name="operating-system"></a>Sistema operativos

Hola extensión del agente de OMS se pueden ejecutar con las distribuciones de Linux.

| Distribución | Versión |
|---|---|
| CentOS Linux | 5, 6 y 7 |
| Oracle Linux | 5, 6 y 7 |
| Red Hat Enterprise Linux Server | 5, 6 y 7 |
| Debian GNU/Linux | 6, 7 y 8 |
| Ubuntu | 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS |
| SUSE Linux Enterprise Server | 11 y 12 |

### <a name="internet-connectivity"></a>Conectividad de Internet

Hola extensión del agente de OMS para Linux requiere esa máquina virtual de destino de hello es toohello conectado internet. 

## <a name="extension-schema"></a>Esquema de extensión

Hello JSON siguiente muestra esquema Hola Hola extensión del agente de OMS. extensión de Hello requiere Hola área de trabajo área de trabajo y el identificador de clave de área de trabajo OMS Hola destino; Estos valores se pueden encontrar en el portal de OMS Hola. Porque la clave de área de trabajo de hello debe tratarse como datos confidenciales, se deben almacenar en una configuración protegida. Datos de configuración de extensión protegido de VM de Azure cifrados y solo descifrados en la máquina virtual de destino de Hola. Tenga en cuenta que **workspaceId** y **workspaceKey** distinguen mayúsculas de minúsculas.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a>Valores de propiedad

| Nombre | Valor / ejemplo |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.EnterpriseCloud.Monitoring |
| type | OmsAgentForLinux |
| typeHandlerVersion | 1.4 |
| workspaceId (p.ej) | 6f680a37-00c6-41c7-a93f-1437e3462574 |
| workspaceKey (p. ej.) | z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ== |


## <a name="template-deployment"></a>Implementación de plantilla

Las extensiones de VM de Azure pueden implementarse con plantillas de Azure Resource Manager. Las plantillas son ideales al implementar una o varias máquinas virtuales que requieren la configuración de implementación de post como tooOMS de incorporación. Una plantilla de administrador de recursos de ejemplo que incluye la extensión de máquina virtual de agente de OMS de hello puede encontrarse en hello [Galería de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm). 

configuración de JSON de Hola para una extensión de máquina virtual puede anidada dentro de recurso de la máquina virtual de hello, o se coloca en la raíz de Hola o de nivel superior de una plantilla JSON del Administrador de recursos. colocación de Hola de configuración de JSON de hello afecta al valor de Hola de nombre de recurso de Hola y el tipo. Para obtener más información, consulte el artículo sobre cómo [establecer el nombre y el tipo de recursos secundarios](../../azure-resource-manager/resource-manager-template-child-resource.md). 

Hello en el ejemplo siguiente se supone extensión OMS Hola está anidada dentro de recurso de la máquina virtual de Hola. Cuando se anidan los recursos de extensión de hello, Hola JSON se coloca en hello `"resources": []` objeto de máquina virtual de Hola.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

Al colocar extensión Hola JSON en raíz de Hola de plantilla de hello, el nombre del recurso de hello incluye una máquina virtual de referencia toohello primario, y tipo hello refleja configuración anidados Hola.  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a>Implementación de la CLI de Azure

Hola CLI de Azure puede ser usado toodeploy Hola VM de agente de OMS extensión tooan máquina virtual existente. Reemplazar la clave OMS de Hola y el Id. de OMS con los de su área de trabajo OMS. 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a>Solución de problemas y asistencia

### <a name="troubleshoot"></a>Solución de problemas

Datos acerca del estado de Hola de implementaciones de extensión se pueden recuperar desde Hola portal de Azure y mediante el uso de hello CLI de Azure. estado de implementación de hello toosee de extensiones para una máquina virtual determinada, ejecute hello después de usar el comando Hola CLI de Azure.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

Ejecución de la extensión de salida se ha iniciado toohello siguiente archivo:

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a>Códigos de error y su significado

| Código de error | Significado | Acción posible |
| :---: | --- | --- |
| 10 | Máquina virtual ya está conectado tooan área de trabajo OMS | tooconnect Hola VM toohello área de trabajo especificado en el esquema de extensión de hello, establezca stopOnMultipleConnections toofalse en la configuración pública o quite esta propiedad. Esta máquina virtual se factura una vez por cada área de trabajo a la que se conecta. |
| 11 | Extensión de configuración no válido proporcionado toohello | Siga Hola anteriores ejemplos tooset todos los valores de propiedad necesarios para la implementación. |
| 12 | el Administrador de paquetes de saludo dpkg está bloqueado | Asegúrese de que todas las operaciones de actualización de dpkg en la máquina de hello termine e intente de nuevo. |
| 20 | | Habilitar llamado antes de tiempo | [Hola actualización agente Linux de Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello última versión disponible. |
| 51 | Esta extensión no se admite en el sistema operativo de la máquina virtual de Hola | |
| 55 | No se puede conectar el servicio de Microsoft Operations Management Suite toohello | Compruebe que Hola sistema disponga de acceso a Internet o que se ha proporcionado un proxy HTTP válido. Además, compruebe validez de Hola de hello Id. de área de trabajo. |

Información adicional de solución de problemas puede encontrarse en hello [Guía de solución de problemas del agente de OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).

### <a name="support"></a>Soporte técnico

Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en hello [foros de Azure de MSDN y el desbordamiento de la pila](https://azure.microsoft.com/en-us/support/forums/). Como alternativa, puede registrar un incidente de soporte técnico de Azure. Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/en-us/support/options/) y seleccione la obtención de soporte técnico. Para obtener información acerca del uso de soporte técnico de Azure, lea hello [P+F de soporte de Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).
