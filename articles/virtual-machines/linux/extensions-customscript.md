---
title: "aaaRun scripts personalizados en máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "Automatizar tareas de configuración de VM de Linux mediante el uso de hello extensión de Script personalizado"
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: f2c273a5fbd4cd1695aea48fa4bd08e691511e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a><span data-ttu-id="738b3-103">Uso de hello extensión de Script personalizado de Azure con las máquinas virtuales Linux</span><span class="sxs-lookup"><span data-stu-id="738b3-103">Using hello Azure Custom Script Extension with Linux Virtual Machines</span></span>
<span data-ttu-id="738b3-104">Extensión de Script personalizado de Hello descarga y ejecuta scripts en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="738b3-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="738b3-105">Esta extensión es útil para la configuración posterior a la implementación, la instalación de software o cualquier otra tarea de configuración o administración.</span><span class="sxs-lookup"><span data-stu-id="738b3-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="738b3-106">Las secuencias de comandos se pueden descargar desde el almacenamiento de Azure u otra ubicación de internet accesible o proporciona extensión toohello tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="738b3-106">Scripts can be downloaded from Azure storage or other accessible internet location, or provided toohello extension run time.</span></span> <span data-ttu-id="738b3-107">Hola extensión de Script personalizado se integra con plantillas de Azure Resource Manager y también se puede ejecutar mediante Hola CLI de Azure, PowerShell, portal de Azure u Hola API de REST de máquina Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="738b3-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="738b3-108">Este documento se explica cómo toouse Hola extensión de Script personalizado de Hola CLI de Azure y una plantilla de Azure Resource Manager y también detalles de la solución de problemas de pasos en los sistemas Linux.</span><span class="sxs-lookup"><span data-stu-id="738b3-108">This document details how toouse hello Custom Script Extension from hello Azure CLI, and an Azure Resource Manager template, and also details troubleshooting steps on Linux systems.</span></span>

## <a name="extension-configuration"></a><span data-ttu-id="738b3-109">Configuración de la extensión</span><span class="sxs-lookup"><span data-stu-id="738b3-109">Extension Configuration</span></span>
<span data-ttu-id="738b3-110">configuración de extensión de Script personalizado de Hello especifica elementos tales como ubicación del script y hello toobe de comando ejecutar.</span><span class="sxs-lookup"><span data-stu-id="738b3-110">hello Custom Script Extension configuration specifies things like script location and hello command toobe run.</span></span> <span data-ttu-id="738b3-111">Esta configuración se puede almacenar en archivos de configuración especificados en la línea de comandos de hello, o en una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="738b3-111">This configuration can be stored in configuration files, specified on hello command line, or in an Azure Resource Manager template.</span></span> <span data-ttu-id="738b3-112">Los datos confidenciales se pueden almacenar en una configuración protegida, que se cifra y descifra solo dentro de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="738b3-112">Sensitive data can be stored in a protected configuration, which is encrypted and only decrypted inside hello virtual machine.</span></span> <span data-ttu-id="738b3-113">configuración protegida Hello es útil al comando de ejecución de hello incluye secretos, como una contraseña.</span><span class="sxs-lookup"><span data-stu-id="738b3-113">hello protected configuration is useful when hello execution command includes secrets such as a password.</span></span>

### <a name="public-configuration"></a><span data-ttu-id="738b3-114">Configuración pública</span><span class="sxs-lookup"><span data-stu-id="738b3-114">Public Configuration</span></span>
<span data-ttu-id="738b3-115">Esquema:</span><span class="sxs-lookup"><span data-stu-id="738b3-115">Schema:</span></span>

<span data-ttu-id="738b3-116">**Nota**: Los nombres de propiedad distinguen entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="738b3-116">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="738b3-117">Utilice nombres de hello tal como se muestra a continuación tooavoid problemas de implementación.</span><span class="sxs-lookup"><span data-stu-id="738b3-117">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="738b3-118">**commandToExecute**: (requerido, string) Hola tooexecute de secuencia de comandos de punto de entrada</span><span class="sxs-lookup"><span data-stu-id="738b3-118">**commandToExecute**: (required, string) hello entry point script tooexecute</span></span>
* <span data-ttu-id="738b3-119">**fileUris**: (opcional, matriz de cadena) hello las direcciones URL para toobe archivos descargan.</span><span class="sxs-lookup"><span data-stu-id="738b3-119">**fileUris**: (optional, string array) hello URLs for files toobe downloaded.</span></span>
* <span data-ttu-id="738b3-120">**marca de tiempo** (entero opcional) use esta tootrigger solo un vuelva a ejecutar script de Hola de campo, cambie el valor de este campo.</span><span class="sxs-lookup"><span data-stu-id="738b3-120">**timestamp** (optional, integer) use this field only tootrigger a rerun of hello script by changing value of this field.</span></span>

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a><span data-ttu-id="738b3-121">Configuración protegida</span><span class="sxs-lookup"><span data-stu-id="738b3-121">Protected Configuration</span></span>
<span data-ttu-id="738b3-122">Esquema:</span><span class="sxs-lookup"><span data-stu-id="738b3-122">Schema:</span></span>

<span data-ttu-id="738b3-123">**Nota**: Los nombres de propiedad distinguen entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="738b3-123">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="738b3-124">Utilice nombres de hello tal como se muestra a continuación tooavoid problemas de implementación.</span><span class="sxs-lookup"><span data-stu-id="738b3-124">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="738b3-125">**commandToExecute**: (opcional, string) Hola tooexecute de secuencia de comandos de punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="738b3-125">**commandToExecute**: (optional, string) hello entry point script tooexecute.</span></span> <span data-ttu-id="738b3-126">Use este campo si el comando contiene secretos tales como contraseñas.</span><span class="sxs-lookup"><span data-stu-id="738b3-126">Use this field instead if your command contains secrets such as passwords.</span></span>
* <span data-ttu-id="738b3-127">**storageAccountName**: (opcional, string) nombre Hola de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="738b3-127">**storageAccountName**: (optional, string) hello name of storage account.</span></span> <span data-ttu-id="738b3-128">Si especifica credenciales de almacenamiento, todos los valores de fileUri deben ser direcciones URL de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="738b3-128">If you specify storage credentials, all fileUris must be URLs for Azure Blobs.</span></span>
* <span data-ttu-id="738b3-129">**storageAccountKey**: (opcional, string) clave de acceso de Hola de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="738b3-129">**storageAccountKey**: (optional, string) hello access key of storage account.</span></span>

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a><span data-ttu-id="738b3-130">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="738b3-130">Azure CLI</span></span>
<span data-ttu-id="738b3-131">Cuando se usa toorun Hola extensión de Script personalizado de hello CLI de Azure, cree un archivo de configuración o archivos que contengan en el uri de archivo mínimo hello y comandos de ejecución de script de Hola.</span><span class="sxs-lookup"><span data-stu-id="738b3-131">When using hello Azure CLI toorun hello Custom Script Extension, create a configuration file or files containing at minimum hello file uri, and hello script execution command.</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="738b3-132">Si lo desea puede especificarse configuración hello en comando hello como una cadena con formato JSON.</span><span class="sxs-lookup"><span data-stu-id="738b3-132">Optionally hello settings can be specified in hello command as a JSON formatted string.</span></span> <span data-ttu-id="738b3-133">Esto permite hello toobe de configuración especificado durante la ejecución y sin un archivo de configuración diferente.</span><span class="sxs-lookup"><span data-stu-id="738b3-133">This allows hello configuration toobe specified during execution and without a separate configuration file.</span></span>

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a><span data-ttu-id="738b3-134">Ejemplos de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="738b3-134">Azure CLI Examples</span></span>

<span data-ttu-id="738b3-135">**Ejemplo 1** : configuración pública con archivo de script.</span><span class="sxs-lookup"><span data-stu-id="738b3-135">**Example 1** - Public configuration with script file.</span></span>

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

<span data-ttu-id="738b3-136">Comando de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="738b3-136">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="738b3-137">**Ejemplo 2** : configuración pública sin archivo de script.</span><span class="sxs-lookup"><span data-stu-id="738b3-137">**Example 2** - Public configuration with no script file.</span></span>

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

<span data-ttu-id="738b3-138">Comando de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="738b3-138">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="738b3-139">**Ejemplo 3** : un archivo de configuración pública es identificador URI de archivo de script de Hola toospecify usado y un archivo de configuración protegida es toospecify usado Hola comando toobe ejecuta.</span><span class="sxs-lookup"><span data-stu-id="738b3-139">**Example 3** - A public configuration file is used toospecify hello script file URI, and a protected configuration file is used toospecify hello command toobe executed.</span></span>

<span data-ttu-id="738b3-140">Archivo de configuración pública:</span><span class="sxs-lookup"><span data-stu-id="738b3-140">Public configuration file:</span></span>

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

<span data-ttu-id="738b3-141">Archivo de configuración protegida:</span><span class="sxs-lookup"><span data-stu-id="738b3-141">Protected configuration file:</span></span>  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

<span data-ttu-id="738b3-142">Comando de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="738b3-142">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a><span data-ttu-id="738b3-143">Plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="738b3-143">Resource Manager Template</span></span>
<span data-ttu-id="738b3-144">Hola extensión de Script personalizado de Azure se puede ejecutar en el momento de la implementación de máquina Virtual mediante una plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="738b3-144">hello Azure Custom Script Extension can be run at Virtual Machine deployment time using a Resource Manager template.</span></span> <span data-ttu-id="738b3-145">toodo por lo tanto, agregue la plantilla de implementación de toohello JSON con el formato correcto.</span><span class="sxs-lookup"><span data-stu-id="738b3-145">toodo so, add properly formatted JSON toohello deployment template.</span></span>

### <a name="resource-manager-examples"></a><span data-ttu-id="738b3-146">Ejemplos de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="738b3-146">Resource Manager Examples</span></span>
<span data-ttu-id="738b3-147">**Ejemplo 1** : configuración pública.</span><span class="sxs-lookup"><span data-stu-id="738b3-147">**Example 1** - public configuration.</span></span>

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

<span data-ttu-id="738b3-148">**Ejemplo 2** : comando de ejecución en la configuración protegida.</span><span class="sxs-lookup"><span data-stu-id="738b3-148">**Example 2** - execution command in protected configuration.</span></span>

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
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
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

<span data-ttu-id="738b3-149">Ver tienda de música de hello .net Core demostración para obtener un ejemplo completo - [demostración de la tienda de música](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span><span class="sxs-lookup"><span data-stu-id="738b3-149">See hello .Net Core Music Store Demo for a complete example - [Music Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="738b3-150">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="738b3-150">Troubleshooting</span></span>
<span data-ttu-id="738b3-151">Cuando se ejecuta la extensión de Script personalizado de Hola, script de Hola se crea o se ha descargado a una toohello similar del directorio siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="738b3-151">When hello Custom Script Extension runs, hello script is created or downloaded into a directory similar toohello following example.</span></span> <span data-ttu-id="738b3-152">También se guarda la salida del comando Hello en este directorio en `stdout` y `stderr` archivo.</span><span class="sxs-lookup"><span data-stu-id="738b3-152">hello command output is also saved into this directory in `stdout` and `stderr` file.</span></span>

```bash
/var/lib/waagent/custom-script/download/0/
```

<span data-ttu-id="738b3-153">Hola extensión de Script de Azure genera un registro, que puede encontrarse aquí.</span><span class="sxs-lookup"><span data-stu-id="738b3-153">hello Azure Script Extension produces a log, which can be found here.</span></span>

```bash
/var/log/azure/custom-script/handler.log
```

<span data-ttu-id="738b3-154">También se puede recuperar el estado de la ejecución de Hola de hello extensión de Script personalizado con hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="738b3-154">hello execution state of hello Custom Script Extension can also be retrieved with hello Azure CLI.</span></span>

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

<span data-ttu-id="738b3-155">salida de Hello es similar a Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="738b3-155">hello output looks like hello following text:</span></span>

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a><span data-ttu-id="738b3-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="738b3-156">Next Steps</span></span>
<span data-ttu-id="738b3-157">Para más información sobre otras extensiones de script de máquina virtual, consulte [Introducción a la extensión de script de Azure para Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="738b3-157">For information on other VM Script Extensions, see [Azure Script Extension overview for Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

