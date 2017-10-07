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
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="01930-103">Implementación de aplicaciones con plantillas de Azure Resource Manager para máquinas virtuales Windows</span><span class="sxs-lookup"><span data-stu-id="01930-103">Application deployment with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="01930-104">Una vez que ha identificado todos los requisitos de infraestructura Azure y convertir en una plantilla de implementación, implementación de aplicaciones reales de hello debe toobe dirigido.</span><span class="sxs-lookup"><span data-stu-id="01930-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, hello actual application deployment needs toobe addressed.</span></span> <span data-ttu-id="01930-105">Implementación de la aplicación hace referencia tooinstalling archivos binarios de aplicación real de hello en recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="01930-105">Application deployment here is referring tooinstalling hello actual application binaries onto Azure resources.</span></span> <span data-ttu-id="01930-106">Para el ejemplo de Hola a tienda de música, .net Core y IIS necesita toobe instalado y configurado en cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="01930-106">For hello Music Store sample, .Net Core and IIS need toobe installed and configured on each virtual machine.</span></span> <span data-ttu-id="01930-107">Hola tienda de música binarios necesitan toobe instalado en la máquina virtual de Hola y Hola base de datos de almacén de música crean previamente.</span><span class="sxs-lookup"><span data-stu-id="01930-107">hello Music Store binaries need toobe installed onto hello virtual machine, and hello Music Store database pre-created.</span></span>

<span data-ttu-id="01930-108">Este documento detalla cómo las extensiones de máquina Virtual pueden automatizar la aplicación implementación y configuración tooAzure máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="01930-108">This document details how Virtual Machine extensions can automate application deployment and configuration tooAzure virtual machines.</span></span> <span data-ttu-id="01930-109">Se resaltan todas las dependencias y configuraciones únicas.</span><span class="sxs-lookup"><span data-stu-id="01930-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="01930-110">Para la mejor experiencia de hello, implementar previamente una instancia de hello solución tooyour suscripción de Azure y trabajar junto con la plantilla de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="01930-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="01930-111">plantilla de Hello completa puede encontrarse aquí: [implementación de la tienda de música en Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="01930-111">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="01930-112">Script de configuración</span><span class="sxs-lookup"><span data-stu-id="01930-112">Configuration script</span></span>
<span data-ttu-id="01930-113">Las extensiones de máquina virtual son programas especializados que se ejecuta en máquinas virtuales tooprovide automatización de las configuraciones.</span><span class="sxs-lookup"><span data-stu-id="01930-113">Virtual Machine extensions are specialized programs that execute against virtual machines tooprovide configuration automation.</span></span> <span data-ttu-id="01930-114">Hay extensiones disponibles para muchos fines específicos, como antivirus, configuración de registro y configuración de Docker.</span><span class="sxs-lookup"><span data-stu-id="01930-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="01930-115">Hola extensión de Script personalizado puede ser usado toorun una secuencia de comandos en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="01930-115">hello Custom Script extension can be used toorun any script against a virtual machine.</span></span> <span data-ttu-id="01930-116">Con el ejemplo de Hola a tienda de música, se seguridad de máquinas virtuales de Windows hello de toohello secuencia de comandos personalizada extensión tooconfigure e instalar aplicación de tienda de música de hello.</span><span class="sxs-lookup"><span data-stu-id="01930-116">With hello Music Store sample, it is up toohello custom script extension tooconfigure hello Windows virtual machines and install hello Music Store application.</span></span>

<span data-ttu-id="01930-117">Antes de que detalla cómo se declaran las extensiones de máquina virtual en una plantilla de Azure Resource Manager, examine el script de Hola que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="01930-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine hello script that is run.</span></span> <span data-ttu-id="01930-118">Este script configura la máquina virtual toohost Hola aplicación de tienda de música de hello Windows.</span><span class="sxs-lookup"><span data-stu-id="01930-118">This script configures hello Windows virtual machine toohost hello Music Store application.</span></span> <span data-ttu-id="01930-119">Cuando se ejecuta, el script de Hola instala el software que necesite todos los, instalar la aplicación hello de la tienda de música desde control de código fuente y preparar la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="01930-119">When run, hello script installs all needed software, install hello Music store application from source control, and prepare hello database.</span></span> 

> <span data-ttu-id="01930-120">Este ejemplo es para fines de demostración.</span><span class="sxs-lookup"><span data-stu-id="01930-120">This sample is for demonstration purposes.</span></span>

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

## <a name="vm-script-extension"></a><span data-ttu-id="01930-121">Extensión de script de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="01930-121">VM Script Extension</span></span>
<span data-ttu-id="01930-122">Extensiones de máquina virtual se puede ejecutar en una máquina virtual en tiempo de compilación mediante la inclusión de recursos de extensión de hello en la plantilla de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="01930-122">VM Extensions can be run against a virtual machine at build time by including hello extension resource in hello Azure Resource Manager template.</span></span> <span data-ttu-id="01930-123">extensión de Hola se puede agregar con el Asistente para agregar recursos de Visual Studio de hello, o mediante la inserción de un valor JSON válido en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="01930-123">hello extension can be added with hello Visual Studio Add Resource wizard, or by inserting valid JSON into hello template.</span></span> <span data-ttu-id="01930-124">Hola recursos de extensión de Script está anidada dentro de hello recursos de máquina Virtual; Esto puede verse en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="01930-124">hello Script Extension resource is nested inside hello Virtual Machine resource; this can be seen in hello following example.</span></span>

<span data-ttu-id="01930-125">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [extensión de Script de máquina virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span><span class="sxs-lookup"><span data-stu-id="01930-125">Follow this link toosee hello JSON sample within hello Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span></span> 

<span data-ttu-id="01930-126">Tenga en cuenta que en hello siguiente JSON que Hola script se almacena en GitHub.</span><span class="sxs-lookup"><span data-stu-id="01930-126">Notice in hello below JSON that hello script is stored in GitHub.</span></span> <span data-ttu-id="01930-127">Este script también podría almacenarse en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="01930-127">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="01930-128">Además, las plantillas de Azure Resource Manager permiten Hola script toobe de cadena de ejecución construido de forma que los valores de parámetros de plantilla se pueden utilizar como parámetros para la ejecución del script.</span><span class="sxs-lookup"><span data-stu-id="01930-128">Also, Azure Resource Manager templates allow hello script execution string toobe constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="01930-129">En este caso se proporcionan datos al implementar plantillas de hello y, a continuación, se pueden utilizar estos valores cuando se ejecute el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="01930-129">In this case data is provided when deploying hello templates, and these values can then be used when executing hello script.</span></span>

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

<span data-ttu-id="01930-130">Como se mencionó anteriormente, también es posible toostore personalizado scripts en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="01930-130">As mentioned above, it is also possible toostore your custom scripts in Azure Blob storage.</span></span> <span data-ttu-id="01930-131">Hay dos opciones para almacenar recursos de script de Hola en almacenamiento de blobs; establecer Hola contenedor/script público y siga Hola aproximarse al igual que la mostrada anteriormente, o también se pueden conservar en el almacenamiento de blobs privado que requiere tooprovide hello storageAccountName y storageAccountKey toohello CustomScriptExtension definición de recursos.</span><span class="sxs-lookup"><span data-stu-id="01930-131">There are two options for storing hello script resources in blob storage; either make hello container/script public and follow hello same approach as above, or it can also be kept in private blob storage which requires you tooprovide hello storageAccountName and storageAccountKey toohello CustomScriptExtension resource definition.</span></span>

<span data-ttu-id="01930-132">En el siguiente ejemplo de Hola hemos optado un paso adicional.</span><span class="sxs-lookup"><span data-stu-id="01930-132">In hello example below we have gone a step further.</span></span> <span data-ttu-id="01930-133">Aunque es posible tooprovide nombre de la cuenta de almacenamiento de Hola y la clave como un parámetro o variable durante la implementación, las plantillas de administrador de recursos proporcionan hello `listKeys` función que puede obtener la cuenta de almacenamiento de hello clave mediante programación e insértelo en toohello plantilla automáticamente durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="01930-133">While it is possible tooprovide hello storage account name and key as a parameter or variable during deployment, Resource Manager templates provide hello `listKeys` function that can obtain hello storage account key programmatically and insert it in toohello template for you at deployment time.</span></span>

<span data-ttu-id="01930-134">En el ejemplo de Hola definición de recursos CustomScriptExtension más adelante, nuestro script personalizado ya está cargado tooan cuenta de almacenamiento de Azure denominada `mystorageaccount9999` que existe en otro grupo de recursos denominado `mysa999rgname`.</span><span class="sxs-lookup"><span data-stu-id="01930-134">In hello example CustomScriptExtension resource definition below, our custom script has already been uploaded tooan Azure storage account called `mystorageaccount9999` which exists in another Resource Group called `mysa999rgname`.</span></span> <span data-ttu-id="01930-135">Cuando se implementa una plantilla que contiene este recurso, Hola `listKeys` función obtiene la clave de cuenta de almacenamiento de Hola Hola cuenta de almacenamiento mediante programación `mystorageaccount9999` en el grupo de recursos de hello `mysa999rgname` y lo inserta en la plantilla de toohello para que podamos.</span><span class="sxs-lookup"><span data-stu-id="01930-135">When we deploy a template containing this resource, hello `listKeys` function programmatically obtains hello storage account key for hello storage account `mystorageaccount9999` in hello Resource Group `mysa999rgname` and inserts it in toohello template for us.</span></span>

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

<span data-ttu-id="01930-136">ventaja principal de Hola de este enfoque es que no requiere toochange la plantilla o parámetros de implementación en caso de hello de Hola cambiar clave de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="01930-136">hello main benefit of this approach is that it does not require you toochange your template or deployment parameters in hello event of hello storage account key changing.</span></span>

<span data-ttu-id="01930-137">Para obtener más información sobre el uso de la extensión de script personalizado de hello, consulte [las extensiones de script personalizado con el Administrador de recursos plantillas](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="01930-137">For more information on using hello custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="01930-138">siguiente paso</span><span class="sxs-lookup"><span data-stu-id="01930-138">Next Step</span></span>
<hr>

[<span data-ttu-id="01930-139">Más plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="01930-139">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

