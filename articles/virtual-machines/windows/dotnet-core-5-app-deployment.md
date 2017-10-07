---
title: "Implementación de aplicación con extensiones de máquina Virtual aaaAutomating | Documentos de Microsoft"
description: "Tutorial de DotNet Core para máquinas virtuales de Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 79c91304-6c1b-4354-a185-fecc129b139d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6d52537fbd4e935f19d3864def11484f519f8598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a>Implementación de aplicaciones con plantillas de Azure Resource Manager para máquinas virtuales Windows

Una vez que ha identificado todos los requisitos de infraestructura Azure y convertir en una plantilla de implementación, implementación de aplicaciones reales de hello debe toobe dirigido. Implementación de la aplicación hace referencia tooinstalling archivos binarios de aplicación real de hello en recursos de Azure. Para el ejemplo de Hola a tienda de música, .net Core y IIS necesita toobe instalado y configurado en cada máquina virtual. Hola tienda de música binarios necesitan toobe instalado en la máquina virtual de Hola y Hola base de datos de almacén de música crean previamente.

Este documento detalla cómo las extensiones de máquina Virtual pueden automatizar la aplicación implementación y configuración tooAzure máquinas virtuales. Se resaltan todas las dependencias y configuraciones únicas. Para la mejor experiencia de hello, implementar previamente una instancia de hello solución tooyour suscripción de Azure y trabajar junto con la plantilla de hello Azure Resource Manager. plantilla de Hello completa puede encontrarse aquí: [implementación de la tienda de música en Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="configuration-script"></a>Script de configuración
Las extensiones de máquina virtual son programas especializados que se ejecuta en máquinas virtuales tooprovide automatización de las configuraciones. Hay extensiones disponibles para muchos fines específicos, como antivirus, configuración de registro y configuración de Docker. Hola extensión de Script personalizado puede ser usado toorun una secuencia de comandos en una máquina virtual. Con el ejemplo de Hola a tienda de música, se seguridad de máquinas virtuales de Windows hello de toohello secuencia de comandos personalizada extensión tooconfigure e instalar aplicación de tienda de música de hello.

Antes de que detalla cómo se declaran las extensiones de máquina virtual en una plantilla de Azure Resource Manager, examine el script de Hola que se ejecuta. Este script configura la máquina virtual toohost Hola aplicación de tienda de música de hello Windows. Cuando se ejecuta, el script de Hola instala el software que necesite todos los, instalar la aplicación hello de la tienda de música desde control de código fuente y preparar la base de datos de Hola. 

> Este ejemplo es para fines de demostración.

```PowerShell
<#
    .SYNOPSIS
        Downloads and configures .Net Core Music Store application sample across IIS and Azure SQL DB.
#>

Param (
    [string]$user,
    [string]$password,
    [string]$sqlserver
)

# Firewall
netsh advfirewall firewall add rule name="http" dir=in action=allow protocol=TCP localport=80

# Folders
New-Item -ItemType Directory c:\temp
New-Item -ItemType Directory c:\music

# Install iis
Install-WindowsFeature web-server -IncludeManagementTools

# Install dot.net core sdk
Invoke-WebRequest http://go.microsoft.com/fwlink/?LinkID=615460 -outfile c:\temp\vc_redistx64.exe
Start-Process c:\temp\vc_redistx64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkID=809122 -outfile c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe
Start-Process c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkId=817246 -outfile c:\temp\DotNetCore.WindowsHosting.exe
Start-Process c:\temp\DotNetCore.WindowsHosting.exe -ArgumentList '/quiet' -Wait

# Download music app
Invoke-WebRequest  https://github.com/Microsoft/dotnet-core-sample-templates/raw/master/dotnet-core-music-windows/music-app/music-store-azure-demo-pub.zip -OutFile c:\temp\musicstore.zip
Expand-Archive C:\temp\musicstore.zip c:\music

# Azure SQL connection sting in environment variable
[Environment]::SetEnvironmentVariable("Data:DefaultConnection:ConnectionString", "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30",[EnvironmentVariableTarget]::Machine)

# Pre-create database
$env:Data:DefaultConnection:ConnectionString = "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30"
Start-Process 'C:\Program Files\dotnet\dotnet.exe' -ArgumentList 'c:\music\MusicStore.dll'

# Configure iis
Remove-WebSite -Name "Default Web Site"
Set-ItemProperty IIS:\AppPools\DefaultAppPool\ managedRuntimeVersion ""
New-Website -Name "MusicStore" -Port 80 -PhysicalPath C:\music\ -ApplicationPool DefaultAppPool
& iisreset
```

## <a name="vm-script-extension"></a>Extensión de script de máquina virtual
Extensiones de máquina virtual se puede ejecutar en una máquina virtual en tiempo de compilación mediante la inclusión de recursos de extensión de hello en la plantilla de hello Azure Resource Manager. extensión de Hola se puede agregar con el Asistente para agregar recursos de Visual Studio de hello, o mediante la inserción de un valor JSON válido en la plantilla de Hola. Hola recursos de extensión de Script está anidada dentro de hello recursos de máquina Virtual; Esto puede verse en el siguiente ejemplo de Hola.

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [extensión de Script de máquina virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339). 

Tenga en cuenta que en hello siguiente JSON que Hola script se almacena en GitHub. Este script también podría almacenarse en Azure Blob Storage. Además, las plantillas de Azure Resource Manager permiten Hola script toobe de cadena de ejecución construido de forma que los valores de parámetros de plantilla se pueden utilizar como parámetros para la ejecución del script. En este caso se proporcionan datos al implementar plantillas de hello y, a continuación, se pueden utilizar estos valores cuando se ejecute el script de Hola.

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

Como se mencionó anteriormente, también es posible toostore personalizado scripts en el almacenamiento de blobs de Azure. Hay dos opciones para almacenar recursos de script de Hola en almacenamiento de blobs; establecer Hola contenedor/script público y siga Hola aproximarse al igual que la mostrada anteriormente, o también se pueden conservar en el almacenamiento de blobs privado que requiere tooprovide hello storageAccountName y storageAccountKey toohello CustomScriptExtension definición de recursos.

En el siguiente ejemplo de Hola hemos optado un paso adicional. Aunque es posible tooprovide nombre de la cuenta de almacenamiento de Hola y la clave como un parámetro o variable durante la implementación, las plantillas de administrador de recursos proporcionan hello `listKeys` función que puede obtener la cuenta de almacenamiento de hello clave mediante programación e insértelo en toohello plantilla automáticamente durante la implementación.

En el ejemplo de Hola definición de recursos CustomScriptExtension más adelante, nuestro script personalizado ya está cargado tooan cuenta de almacenamiento de Azure denominada `mystorageaccount9999` que existe en otro grupo de recursos denominado `mysa999rgname`. Cuando se implementa una plantilla que contiene este recurso, Hola `listKeys` función obtiene la clave de cuenta de almacenamiento de Hola Hola cuenta de almacenamiento mediante programación `mystorageaccount9999` en el grupo de recursos de hello `mysa999rgname` y lo inserta en la plantilla de toohello para que podamos.

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
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://mystorageaccount9999.blob.core.windows.net/container/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]",
      "storageAccountName": "mystorageaccount9999",
      "storageAccountKey": "[listKeys(resourceId('mysa999rgname','Microsoft.Storage/storageAccounts', mystorageaccount9999), '2015-06-15').key1]"
    }
  }
}
```

ventaja principal de Hola de este enfoque es que no requiere toochange la plantilla o parámetros de implementación en caso de hello de Hola cambiar clave de cuenta de almacenamiento.

Para obtener más información sobre el uso de la extensión de script personalizado de hello, consulte [las extensiones de script personalizado con el Administrador de recursos plantillas](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-step"></a>siguiente paso
<hr>

[Más plantillas de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates)

