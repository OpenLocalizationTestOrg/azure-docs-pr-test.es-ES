---
title: "aaaVirtual máquina extensiones y características de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de qué extensiones están disponibles para máquinas virtuales de Azure, agrupadas por lo que proporcionan o mejoran."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 61ccfd696b38e9be1026d836d5796c2346fd650f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a>Características y extensiones de las máquinas virtuales para Windows

Las extensiones de máquina virtual de Azure son pequeñas aplicaciones que realizan tareas de automatización y configuración posterior a la implementación en máquinas virtuales de Azure. Por ejemplo, si una máquina virtual requiere la instalación de software, la protección antivirus o configuración de Docker, una extensión de máquina virtual puede ser usado toocomplete estas tareas. Extensiones de VM de Azure pueden realizarse mediante el uso de hello CLI de Azure, PowerShell, plantillas de Azure Resource Manager y Hola portal de Azure. Las extensiones pueden empaquetar con una nueva implementación de máquina virtual o se pueden ejecutar en cualquier sistema existente.

Este documento proporciona información general sobre las extensiones de máquina virtual, requisitos previos para usar las extensiones de máquina virtual e instrucciones sobre cómo administrar toodetect y quitar extensiones de máquina virtual. Este documento proporciona información generalizada porque muchas extensiones de máquina virtual están disponibles, cada una con una configuración potencialmente única. Los detalles específicos de una extensión pueden encontrarse en cada extensión individuales toohello específico de documento.

## <a name="use-cases-and-samples"></a>Casos de uso y ejemplos

Hay muchas extensiones de máquina virtual de Azure diferentes disponibles, cada una con un caso de uso específico. Algunos casos de uso de ejemplo son:

- Máquina virtual de estado deseado de PowerShell configuraciones tooa se aplican mediante el uso de extensión de DSC de Hola para Windows. Para obtener más información, consulte la sección sobre la [extensión de configuración de estado deseado de Azure](extensions-dsc-overview.md).
- Configurar la supervisión de la máquina virtual con la extensión de máquina virtual de agente de supervisión de Microsoft de Hola. Para obtener más información, consulte [tooLog de máquinas virtuales de Azure conectarse análisis](../../log-analytics/log-analytics-azure-vm-extension.md).
- Configurar la supervisión de la infraestructura de Azure con hello Datadog extensión. Para obtener más información, vea hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).
- Configure una máquina virtual de Azure mediante Chef. Para obtener más información, consulte [Automatización de la implementación de la máquina virtual de Azure con Chef](chef-automation.md).

Además extensiones específicas de tooprocess, una extensión de Script personalizado está disponible para máquinas virtuales Windows y Linux. extensión de Script personalizado para Windows Hello permite cualquier toobe de script de PowerShell que ejecute en una máquina virtual. Esto resulta útil al diseñar implementaciones de Azure que requieren una configuración más allá de lo que las herramientas de Azure nativas pueden proporcionar. Para obtener más información, consulte la sección sobre la [extensión de script personalizado de máquina virtual Windows](extensions-customscript.md).


## <a name="prerequisites"></a>Requisitos previos

Cada extensión de máquina virtual puede tener su propio conjunto de requisitos previos. Por ejemplo, hello extensión de máquina virtual Docker tiene un requisito previo de la distribución de Linux compatible. Requisitos de extensiones individuales se detallan en la documentación específica de la extensión de Hola.

### <a name="azure-vm-agent"></a>Agente de máquina virtual de Azure
agente de máquina virtual de Azure de Hello administra la interacción entre una máquina virtual de Azure y el controlador de tejido de Azure de Hola. agente de máquina virtual de Hello es responsable de muchos aspectos funcionales de la implementación y administración de máquinas virtuales de Azure, incluida la ejecución de extensiones de máquina virtual. agente de máquina virtual de Azure de Hello está preinstalado en imágenes de Azure Marketplace y se puede instalar en sistemas operativos compatibles.

Para obtener información sobre las instrucciones de instalación y los sistemas operativos compatibles, consulte [Agente de máquina virtual de Azure](agent-user-guide.md).

## <a name="discover-vm-extensions"></a>Detección de extensiones de máquina virtual
Hay muchas extensiones de máquina virtual diferentes disponibles para su uso con máquinas virtuales de Azure. toosee una lista completa, ejecute hello siguiente comando con el módulo de PowerShell de administrador de recursos de Azure de Hola. Establecer ubicación de hello deseado de toospecify seguro de si ejecuta este comando.

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a>Ejecución de extensiones de máquina virtual

Extensiones de máquina virtual de Azure se pueden ejecutar en máquinas virtuales existentes, lo que resulta útil cuando necesita cambios de configuración de toomake o recuperar conectividad en una máquina virtual ya implementada. Las extensiones de máquina virtual también pueden agruparse con las implementaciones de plantilla de Azure Resource Manager. Mediante el uso de las extensiones con plantillas de administrador de recursos, puede habilitar máquinas virtuales de Azure toobe implementado y configurado sin necesidad de hello sea necesaria la intervención posterior a la implementación.

Hola siguiendo métodos puede ser toorun usa una extensión en una máquina virtual existente.

### <a name="powershell"></a>PowerShell

Existen varios comandos de PowerShell para ejecutar extensiones individuales. toosee una lista, ejecute hello siga los comandos de PowerShell.

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

Esto proporciona la siguiente toohello similar de salida:

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

Hello en el ejemplo siguiente se usa toodownload de extensión de Script personalizado de hello una secuencia de comandos desde un repositorio de GitHub en la máquina virtual de destino de hello y, a continuación, ejecute el script de Hola. Para obtener más información sobre la extensión de Script personalizado de hello, consulte [Introducción a la extensión Script personalizado](extensions-customscript.md).

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

En este ejemplo, hello extensión de acceso de VM es la contraseña administrativa de hello tooreset utilizadas de una máquina virtual de Windows. Para obtener más información sobre Hola extensión de acceso a máquinas virtuales, consulte [servicio de restablecimiento de escritorio remoto en una VM de Windows](reset-rdp.md).

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

Hola `Set-AzureRmVMExtension` comando puede ser usado toostart cualquier extensión de máquina virtual. Para obtener más información, vea hello [referencia de conjunto AzureRmVMExtension](https://msdn.microsoft.com/en-us/library/mt603745.aspx).


### <a name="azure-portal"></a>Azure Portal

Una extensión de máquina virtual puede ser tooan aplicada de máquina virtual existente a través de hello portal de Azure. toodo por lo tanto, seleccione la máquina virtual de hello desea toouse, elija **extensiones**y haga clic en **agregar**. Esto proporciona una lista de extensiones disponibles. Seleccione Hola uno que desee y siga los pasos de hello en el Asistente de Hola.

Hello siguiente imagen muestra instalación Hola de hello extensión de Microsoft Antimalware de hello portal de Azure.

![Instalar la extensión de antimalware](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a>Plantillas de Azure Resource Manager

Extensiones de máquina virtual pueden ser plantilla de Azure Resource Manager tooan agregada y ejecutan con la implementación de Hola de plantilla de Hola. La implementación de extensiones con una plantilla es útil para crear implementaciones de Azure completamente configuradas. Por ejemplo, hello que JSON siguiente procede de una plantilla de administrador de recursos que implementa un conjunto de máquinas virtuales de equilibrio de carga y una base de datos de SQL Azure y, a continuación, instala una aplicación de .NET Core en cada máquina virtual. Hola extensión de máquina virtual se encarga de la instalación de software de Hola.

Para obtener más información, vea hello [plantilla de administrador de recursos completo](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

Para obtener más información, consulte [Creación de plantillas de Azure Resource Manager con extensiones de máquina virtual Windows](template-description.md#extensions).

## <a name="secure-vm-extension-data"></a>Protección de datos de extensión de máquina virtual

Si estás ejecutando una extensión de máquina virtual, puede ser necesario tooinclude información confidencial, como las credenciales y los nombres de cuenta de almacenamiento, las teclas de acceso de cuenta de almacenamiento. Muchas de las extensiones de VM incluyen una configuración protegida, que cifra los datos y los descifra solo dentro de la máquina virtual de destino de Hola. Cada extensión tiene un esquema específico de configuración protegida que se detallará en la documentación específica de extensión.

Hola de ejemplo siguiente muestra una instancia de hello extensión de Script personalizado para Windows. Tenga en cuenta que tooexecute de comando hello incluye un conjunto de credenciales. En este ejemplo, no se cifrarán Hola comando tooexecute.


```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

Proteger la cadena de ejecución de hello moviendo hello **comando tooexecute** propiedad toohello **protegido** configuración.

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

## <a name="troubleshoot-vm-extensions"></a>Solución de problemas de extensiones de máquina virtual

Cada extensión de máquina virtual puede tener unos pasos de solución de problemas específicos. Por ejemplo, cuando se usa la extensión de Script personalizado de hello, detalles de ejecución de script encontrará localmente en la máquina virtual de hello en el que se ejecutó la extensión de Hola. Todos los pasos de solución de problemas específicos de extensión aparecen detallados en la documentación específica de extensión.

Hola siguiendo los pasos de solución de problemas aplica tooall extensiones de máquina virtual.

### <a name="view-extension-status"></a>Consulta del estado de la extensión

Después de una extensión de máquina virtual se ha ejecutado en una máquina virtual, use Hola siguiendo el estado de extensión de tooreturn de comandos de PowerShell. Reemplace los nombres de parámetros de ejemplo por los suyos propios. Hola `Name` parámetro toma el nombre de hello dado toohello extensión en tiempo de ejecución.

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

salida de Hello aspecto Hola siguiente:

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

Estado de ejecución de extensión también puede encontrarse en hello portal de Azure. estado de hello tooview de una extensión, la máquina virtual de hello seleccione, elija **extensiones**, y seleccione Hola extensión deseada.

### <a name="rerun-vm-extensions"></a>Repetición de ejecución de extensiones de máquina virtual

Puede haber casos en que una extensión de máquina virtual necesita toobe vuelva a ejecutar. Para ello, quite la extensión hello y, a continuación, volver a ejecutar la extensión de hello con un método de ejecución de su elección. tooremove una extensión, ejecute hello siguiente comando con el módulo de Azure PowerShell Hola. Reemplace los nombres de parámetros de ejemplo por los suyos propios.

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

También se puede quitar una extensión mediante Hola portal de Azure. toodo para:

1. Seleccione una máquina virtual.
2. Seleccione **Extensiones**.
3. Elija la extensión de hello deseado.
4. Seleccione **Desinstalar**.

## <a name="common-vm-extensions-reference"></a>Referencia de extensiones de máquina virtual comunes
| Nombre de la extensión | Descripción | Más información |
| --- | --- | --- |
| Extensión de la secuencia de comandos personalizada para Windows |Ejecución de scripts en una máquina virtual de Azure |[Extensión de la secuencia de comandos personalizada para Windows](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Extensión de DSC para Windows |Extensión DSC (configuración de estado deseado) de PowerShell |[Extensión DSC para Windows](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Extensión de Diagnósticos de Azure |Administración de Diagnósticos de Azure |[Extensión de Diagnósticos de Azure](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Extensión de acceso a máquina virtual de Azure |Administración de usuarios y credenciales |[Extensión de acceso a máquina virtual para Linux](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
