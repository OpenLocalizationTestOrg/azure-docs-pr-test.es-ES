---
title: "aaaAzure extensión del Script personalizado para Windows | Documentos de Microsoft"
description: "Automatizar tareas de configuración de máquina virtual de Windows con la extensión de Script personalizado de Hola"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/16/2017
ms.author: nepeters
ms.openlocfilehash: 97e065242e9fed116ee20b074f4e302a0cd10585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows"></a>Extensión de la secuencia de comandos personalizada para Windows

Extensión de Script personalizado de Hello descarga y ejecuta scripts en máquinas virtuales de Azure. Esta extensión es útil para la configuración posterior a la implementación, la instalación de software o cualquier otra tarea de configuración o administración. Las secuencias de comandos pueden descargarse desde el almacenamiento de Azure o GitHub, o proporcionarse toohello portal de Azure en tiempo de ejecución de extensión. Hola extensión de Script personalizado se integra con plantillas de Azure Resource Manager y también se puede ejecutar mediante Hola CLI de Azure, PowerShell, portal de Azure u Hola API de REST de máquina Virtual de Azure.

Este documento detalla cómo toouse Hola extensión de Script personalizado utilizando Hola módulo Azure PowerShell, las plantillas de administrador de recursos de Azure y detalles de la solución de problemas de pasos en los sistemas Windows.

## <a name="prerequisites"></a>Requisitos previos

### <a name="operating-system"></a>Sistema operativo

Hola extensión de Script personalizado para Windows se pueden ejecutar en Windows Server 2008 R2, 2012, 2012 R2 y 2016 libera.

### <a name="script-location"></a>Ubicación del script

script de Hola debe toobe almacenado en almacenamiento de blobs de Azure, o cualquier otra ubicación accesible a través de una dirección URL válida.

### <a name="internet-connectivity"></a>Conectividad de Internet

Hello extensión para ventanas de Script personalizado requiere esa máquina virtual de destino de hello es toohello conectado internet. 

## <a name="extension-schema"></a>Esquema de extensión

Hello JSON siguiente muestra esquema Hola Hola extensión de Script personalizado. extensión de Hello requiere una ubicación de la secuencia de comandos (almacenamiento de Azure u otra ubicación con dirección URL válida) y un tooexecute de comando. Si utiliza almacenamiento de Azure como origen de la secuencia de comandos de hello, se requiere una clave de nombre y la cuenta de la cuenta de almacenamiento de Azure. Estos elementos se deben tratar como datos confidenciales y especificados en la configuración de configuración protegida de extensiones de Hola. Datos de configuración de extensión protegido de VM de Azure cifrados y solo descifrados en la máquina virtual de destino de Hola.

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
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a>Valores de propiedad

| Nombre | Valor / ejemplo |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.Compute |
| type | extensions |
| typeHandlerVersion | 1.9 |
| fileUris (p. ej.) | https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1 |
| commandToExecute (p. ej.) | powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 |
| storageAccountName (p. ej.) | examplestorageacct |
| storageAccountKey (p. ej.) | TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg== |

**Nota**: Los nombres de propiedad distinguen entre mayúsculas y minúsculas. Utilice nombres de hello tal como se muestra anteriormente tooavoid problemas de implementación.

## <a name="template-deployment"></a>Implementación de plantilla

Las extensiones de VM de Azure pueden implementarse con plantillas de Azure Resource Manager. esquema JSON de Hello detallado en la sección anterior de hello puede usarse en un hello toorun de plantilla de Azure Resource Manager extensión de Script personalizado durante la implementación de plantilla Azure Resource Manager. Una plantilla de ejemplo que incluya Hola extensión de Script personalizado puede encontrarse aquí, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="powershell-deployment"></a>Implementación de PowerShell

Hola `Set-AzureRmVMCustomScriptExtension` comando puede ser usado tooadd Hola Script personalizado extensión tooan máquina virtual existente. Para más información, consulte [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a>Solución de problemas y soporte técnico

### <a name="troubleshoot"></a>Solución de problemas

Datos acerca del estado de Hola de implementaciones de extensión se pueden recuperar desde Hola portal de Azure y mediante el módulo de PowerShell de Azure de Hola. estado de implementación de hello toosee de extensiones para una máquina virtual determinada, ejecute el siguiente comando de Hola.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Ejecución de la extensión de salida es toofiles registrado en hello posterior directorio en la máquina virtual de destino de Hola.
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

Hola especifica los archivos se descargan en hello después de directorio en la máquina virtual de destino de Hola.
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
donde `<n>` es un entero decimal que puede variar entre las ejecuciones de extensión de Hola.  Hola `1.*` Hola real, actual coincide con el valor `typeHandlerVersion` valor de extensión de Hola.  Por ejemplo, pudieron ser reales del directorio hello `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.  

Al ejecutar hello `commandToExecute` comando extensión Hola activados este directorio (p. ej., `...\Downloads\2`) como directorio de trabajo actual de Hola. Este uso de hello habilita de archivos de rutas de acceso relativas toolocate Hola descarga a través de hello `fileURIs` propiedad. Consulte la tabla de hello siguiente para obtener ejemplos.

Puesto que la ruta de acceso de descarga absoluta Hola puede variar con el tiempo, es mejor tooopt para rutas de acceso de archivo o script relativa en hello `commandToExecute` cadena, siempre que sea posible. Por ejemplo:
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

Información de ruta de acceso después de que se conserva el primer segmento URI Hola para los archivos se descarga a través de Hola `fileUris` lista de propiedades.  Tal y como se muestra en la siguiente tabla se hello, archivos descargados se asignan a la estructura de descarga subdirectorios tooreflect Hola de hello `fileUris` valores.  

#### <a name="examples-of-downloaded-files"></a>Ejemplos de archivos descargados

| URI en fileUris | Ubicación descargada relativa | Ubicación descargada absoluta * |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

\*Como anteriormente, las rutas de acceso absoluta al directorio de hello cambia con el período de duración de Hola de hello VM, pero no dentro de una ejecución única de la extensión CustomScript de Hola.

### <a name="support"></a>Soporte técnico

Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en hello [foros de Azure de MSDN y el desbordamiento de la pila] (https://azure.microsoft.com/en-us/support/forums/). Como alternativa, puede registrar un incidente de soporte técnico de Azure. Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/en-us/support/options/) y seleccione la obtención de soporte técnico. Para obtener información acerca del uso de soporte técnico de Azure, lea hello [P+F de soporte de Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).
