---
title: "extensiones y características de máquina aaaVirtual para Linux | Documentos de Microsoft"
description: "Obtenga información acerca de qué extensiones están disponibles para máquinas virtuales de Azure, agrupadas por lo que proporcionan o mejoran."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a>Características y extensiones de las máquinas virtuales para Linux

Las extensiones de máquina virtual de Azure son pequeñas aplicaciones que realizan tareas de automatización y configuración posterior a la implementación en máquinas virtuales de Azure. Por ejemplo, si una máquina virtual requiere la instalación de software, la protección antivirus o configuración de Docker, una extensión de máquina virtual puede ser usado toocomplete estas tareas. Extensiones de VM de Azure se pueden ejecutar con hello CLI de Azure, PowerShell, plantillas de Azure Resource Manager y Hola portal de Azure. Las extensiones pueden empaquetar con una nueva implementación de máquina virtual o se pueden ejecutar en cualquier sistema existente.

Este documento proporciona información general sobre las extensiones de VM, requisitos previos para usar las extensiones de VM de Azure e instrucciones sobre cómo administrar toodetect y quitar extensiones de máquina virtual. Este documento proporciona información generalizada porque muchas extensiones de máquina virtual están disponibles, cada una con una configuración potencialmente única. Los detalles específicos de una extensión pueden encontrarse en cada extensión individuales toohello específico de documento.

## <a name="use-cases-and-samples"></a>Casos de uso y ejemplos

Varias extensiones de máquina virtual de Azure diferentes están disponibles, cada una con un caso de uso específico. A continuación, se indican algunos ejemplos:

- Aplicar el estado deseado de PowerShell configuraciones tooa máquina virtual a través Hola extensión de DSC para Linux. Para obtener más información, consulte la sección sobre la [extensión de configuración de estado deseado de Azure](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).
- Configurar la supervisión de una máquina virtual con hello extensión de máquina virtual de agente de supervisión de Microsoft. Para obtener más información, consulte [cómo toomonitor una VM Linux](tutorial-monitoring.md).
- Configurar la supervisión de la infraestructura de Azure con hello Datadog extensión. Para obtener más información, vea hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).
- Configurar un host Docker en una máquina virtual de Azure con la extensión de máquina virtual Docker Hola. Para obtener más información, consulte [Extensión de máquina virtual de Docker](dockerextension.md).

Además extensiones específicas de tooprocess, una extensión de Script personalizado está disponible para máquinas virtuales Windows y Linux. Hola extensión de Script personalizado para Linux permite cualquier toobe de secuencia de comandos de Bash ejecutar en una máquina virtual. Los scripts personalizados resultan útiles para diseñar implementaciones de Azure que requieren una configuración más allá de lo que las herramientas de Azure nativas pueden proporcionar. Para obtener más información, consulte la sección sobre la [extensión de script personalizado de máquina virtual Linux](extensions-customscript.md).


## <a name="prerequisites"></a>Requisitos previos

Cada extensión de máquina virtual puede tener su propio conjunto de requisitos previos. Por ejemplo, hello extensión de máquina virtual Docker tiene un requisito previo de la distribución de Linux compatible. Requisitos de extensiones individuales se detallan en la documentación específica de la extensión de Hola.

### <a name="azure-vm-agent"></a>Agente de máquina virtual de Azure

agente de máquina virtual de Azure de Hello administra las interacciones entre una máquina virtual de Azure y el controlador de tejido de Azure de Hola. agente de máquina virtual de Hello es responsable de muchos aspectos funcionales de la implementación y administración de máquinas virtuales de Azure, incluida la ejecución de extensiones de máquina virtual. agente de máquina virtual de Azure de Hello está preinstalado en imágenes de Azure Marketplace y puede instalarse manualmente en los sistemas operativos compatibles.

Para obtener información sobre las instrucciones de instalación y los sistemas operativos compatibles, consulte [Agente de máquina virtual de Azure](../windows/classic/agents-and-extensions.md).

## <a name="discover-vm-extensions"></a>Detección de extensiones de máquina virtual

Hay muchas extensiones de máquina virtual diferentes disponibles para su uso con máquinas virtuales de Azure. toosee una lista completa, ejecute hello siguiente comando con hello CLI de Azure, reemplazando la ubicación de ejemplo de Hola por ubicación de Hola de su elección.

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a>Ejecución de extensiones de máquina virtual

Las extensiones de máquina virtual de Azure se pueden ejecutar en máquinas virtuales existentes, que son útiles cuando necesita cambios de configuración de toomake o recuperar conectividad en una máquina virtual ya implementada. Las extensiones de máquina virtual también pueden agruparse con las implementaciones de plantilla de Azure Resource Manager. Al usar las extensiones con plantillas de Resource Manager, las máquinas virtuales de Azure se pueden implementar y configurar sin intervención alguna después de la implementación.

Hola siguiendo métodos puede ser toorun usa una extensión en una máquina virtual existente.

### <a name="azure-cli"></a>CLI de Azure

Extensiones de máquina virtual de Azure se pueden ejecutar en una máquina virtual existente mediante el uso de hello `az vm extension set` comando. Este ejemplo ejecuta la extensión de script personalizado de hello en una máquina virtual.

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

Hola script genera resultados similares toohello siguiente texto:

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a>Azure Portal

Extensiones de máquina virtual pueden ser tooan aplicada de máquina virtual existente a través de hello portal de Azure. toodo por lo tanto, seleccione la máquina virtual de hello, elija **extensiones**y haga clic en **agregar**. Seleccionar extensión de Hola que desee desde la lista de Hola de extensiones disponibles y siga las instrucciones de hello en el Asistente de Hola.

Hello siguiente imagen muestra instalación Hola de hello extensión de Script personalizado de Linux de hello portal de Azure.

![Instalar la extensión de script personalizado](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a>Plantillas de Azure Resource Manager

Extensiones de máquina virtual pueden ser plantilla de Azure Resource Manager tooan agregada y ejecutan con la implementación de Hola de plantilla de Hola. Al implementar una extensión con una plantilla, puede crear implementaciones de Azure completamente configuradas. Por ejemplo, hello que JSON siguiente procede de una plantilla de administrador de recursos. plantilla de Hello implementa un conjunto de máquinas virtuales de equilibrio de carga y una base de datos de SQL Azure y, a continuación, instala una aplicación de .NET Core en cada máquina virtual. Hola extensión de máquina virtual se encarga de la instalación de software de Hola.

Para obtener más información, vea Hola completa [plantilla del Administrador de recursos](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

Para más información, consulte [Creación de plantillas de Azure Resource Manager](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).

## <a name="secure-vm-extension-data"></a>Protección de datos de extensión de máquina virtual

Si estás ejecutando una extensión de máquina virtual, puede ser necesario tooinclude información confidencial, como las credenciales y los nombres de cuenta de almacenamiento, las teclas de acceso de cuenta de almacenamiento. Muchas de las extensiones de VM incluyen una configuración protegida, que cifra los datos y los descifra solo dentro de la máquina virtual de destino de Hola. Cada extensión tiene un esquema específico de configuración protegida que se detalla de forma individual en la documentación específica de extensión.

Hola de ejemplo siguiente muestra una instancia de hello extensión de Script personalizado para Linux. Tenga en cuenta que tooexecute de comando hello incluye un conjunto de credenciales. En este ejemplo, no se cifrarán Hola comando tooexecute.


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

Hola móvil **comando tooexecute** propiedad toohello **protegido** configuración protege la cadena de ejecución de Hola.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a>Solución de problemas de extensiones de máquina virtual

Cada extensión de máquina virtual puede tener la extensión de toohello concreto de pasos de solución de problemas. Por ejemplo, cuando se usa la extensión de Script personalizado de hello, detalles de ejecución de script encontrará localmente en la máquina virtual de hello en el que se ejecutó la extensión de Hola. Todos los pasos de solución de problemas específicos de extensión aparecen detallados en la documentación específica de extensión.

Hola siguiendo los pasos de solución de problemas aplica tooall extensiones de máquina virtual.

### <a name="view-extension-status"></a>Consulta del estado de la extensión

Después de una extensión de máquina virtual se ha ejecutado en una máquina virtual, use Hola siguiendo el estado de extensión de tooreturn de comando de CLI de Azure. Reemplace los nombres de parámetros de ejemplo por los suyos propios.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

salida de Hello es similar a Hola siguiente texto:

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

Estado de ejecución de extensión también puede encontrarse en hello portal de Azure. estado de hello tooview de una extensión, la máquina virtual de hello seleccione, elija **extensiones**, y seleccione Hola extensión deseada.

### <a name="rerun-a-vm-extension"></a>Repetición de ejecución de una extensión de máquina virtual

Puede haber casos en que una extensión de máquina virtual necesita toobe vuelva a ejecutar. Puede volver a ejecutar una extensión quitarlo y, a continuación, volver a ejecutar la extensión de hello con un método de ejecución de su elección. tooremove una extensión, al ejecutar el siguiente comando con hello Azure CLI de Hola. Reemplace los nombres de parámetros de ejemplo por los suyos propios.

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

Puede quitar una extensión mediante Hola pasos de hello portal de Azure:

1. Seleccione una máquina virtual.
2. Elija **Extensiones**.
3. Seleccionar extensión de hello deseado.
4. Elija **Desinstalar**.

## <a name="common-vm-extension-reference"></a>Referencia de extensión de máquina virtual común
| Nombre de la extensión | Descripción | Más información |
| --- | --- | --- |
| Extensión de script personalizado para Linux |Ejecución de scripts en una máquina virtual de Azure |[Extensión de script personalizado para Linux](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| Extensión de Docker |Comandos de Docker remotos de hello Docker daemon toosupport de instalación. |[Extensión de máquina virtual de Docker](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| Extensión de acceso a máquina virtual |Recuperar el acceso tooan máquina virtual de Azure |[Extensión de acceso a máquina virtual](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| Extensión de Diagnósticos de Azure |Administración de Diagnósticos de Azure |[Extensión de Diagnósticos de Azure](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Extensión de acceso a máquina virtual de Azure |Administración de usuarios y credenciales |[Extensión de acceso a máquina virtual para Linux](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
