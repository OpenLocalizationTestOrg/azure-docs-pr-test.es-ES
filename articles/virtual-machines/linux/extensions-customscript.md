---
title: "Ejecución de scripts personalizados en VM de Linux en Azure | Microsoft Docs"
description: "Automatización de tareas de configuración de máquinas virtuales Linux mediante la extensión de script personalizado"
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
ms.openlocfilehash: 1dde64aac72c11ccfccf4fdb676279692befaadd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-custom-script-extension-with-linux-virtual-machines"></a><span data-ttu-id="13a15-103">Uso de la extensión de script personalizado de Azure con máquinas virtuales Linux</span><span class="sxs-lookup"><span data-stu-id="13a15-103">Using the Azure Custom Script Extension with Linux Virtual Machines</span></span>
<span data-ttu-id="13a15-104">La extensión de script personalizado descarga y ejecuta scripts en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="13a15-104">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="13a15-105">Esta extensión es útil para la configuración posterior a la implementación, la instalación de software o cualquier otra tarea de configuración o administración.</span><span class="sxs-lookup"><span data-stu-id="13a15-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="13a15-106">Los scripts se pueden descargar desde Azure Storage u otra ubicación de Internet accesible, o se puede proporcionar a la extensión en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="13a15-106">Scripts can be downloaded from Azure storage or other accessible internet location, or provided to the extension run time.</span></span> <span data-ttu-id="13a15-107">La extensión de script personalizado se integra con las plantillas de Azure Resource Manager y también se puede ejecutar mediante la CLI de Azure, PowerShell, Azure Portal o la API de REST de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="13a15-107">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="13a15-108">En este documento se detalla cómo usar la extensión de script personalizado desde la CLI de Azure y una plantilla de Azure Resource Manager, y también detalla los pasos para solucionar problemas en los sistemas Linux.</span><span class="sxs-lookup"><span data-stu-id="13a15-108">This document details how to use the Custom Script Extension from the Azure CLI, and an Azure Resource Manager template, and also details troubleshooting steps on Linux systems.</span></span>

## <a name="extension-configuration"></a><span data-ttu-id="13a15-109">Configuración de la extensión</span><span class="sxs-lookup"><span data-stu-id="13a15-109">Extension Configuration</span></span>
<span data-ttu-id="13a15-110">La configuración de la extensión de script personalizado especifica aspectos como la ubicación del script y el comando que se ejecutará.</span><span class="sxs-lookup"><span data-stu-id="13a15-110">The Custom Script Extension configuration specifies things like script location and the command to be run.</span></span> <span data-ttu-id="13a15-111">Esta configuración se puede almacenar en archivos de configuración o se puede especificar en la línea de comandos o en una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="13a15-111">This configuration can be stored in configuration files, specified on the command line, or in an Azure Resource Manager template.</span></span> <span data-ttu-id="13a15-112">Los datos confidenciales se pueden almacenar en una configuración protegida, que se cifra y se descifra solo dentro de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="13a15-112">Sensitive data can be stored in a protected configuration, which is encrypted and only decrypted inside the virtual machine.</span></span> <span data-ttu-id="13a15-113">La configuración protegida es útil cuando el comando de ejecución incluye secretos tales como una contraseña.</span><span class="sxs-lookup"><span data-stu-id="13a15-113">The protected configuration is useful when the execution command includes secrets such as a password.</span></span>

### <a name="public-configuration"></a><span data-ttu-id="13a15-114">Configuración pública</span><span class="sxs-lookup"><span data-stu-id="13a15-114">Public Configuration</span></span>
<span data-ttu-id="13a15-115">Esquema:</span><span class="sxs-lookup"><span data-stu-id="13a15-115">Schema:</span></span>

<span data-ttu-id="13a15-116">**Nota**: Los nombres de propiedad distinguen entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="13a15-116">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="13a15-117">Use los nombres tal y como se muestra a continuación para evitar problemas de implementación.</span><span class="sxs-lookup"><span data-stu-id="13a15-117">Use the names as seen below to avoid deployment issues.</span></span>

* <span data-ttu-id="13a15-118">**commandToExecute**: (necesario, cadena) script de punto de entrada que se va a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="13a15-118">**commandToExecute**: (required, string) the entry point script to execute</span></span>
* <span data-ttu-id="13a15-119">**fileUris**: (opcional, matriz de cadenas) direcciones URL de los archivos que se van a descargar.</span><span class="sxs-lookup"><span data-stu-id="13a15-119">**fileUris**: (optional, string array) the URLs for files to be downloaded.</span></span>
* <span data-ttu-id="13a15-120">**timestamp** (opcional, entero) use este campo solo para desencadenar una nueva ejecución del script; para ello, cambie el valor de este campo.</span><span class="sxs-lookup"><span data-stu-id="13a15-120">**timestamp** (optional, integer) use this field only to trigger a rerun of the script by changing value of this field.</span></span>

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a><span data-ttu-id="13a15-121">Configuración protegida</span><span class="sxs-lookup"><span data-stu-id="13a15-121">Protected Configuration</span></span>
<span data-ttu-id="13a15-122">Esquema:</span><span class="sxs-lookup"><span data-stu-id="13a15-122">Schema:</span></span>

<span data-ttu-id="13a15-123">**Nota**: Los nombres de propiedad distinguen entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="13a15-123">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="13a15-124">Use los nombres tal y como se muestra a continuación para evitar problemas de implementación.</span><span class="sxs-lookup"><span data-stu-id="13a15-124">Use the names as seen below to avoid deployment issues.</span></span>

* <span data-ttu-id="13a15-125">**commandToExecute**: (opcional, cadena) script de punto de entrada que se va a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="13a15-125">**commandToExecute**: (optional, string) the entry point script to execute.</span></span> <span data-ttu-id="13a15-126">Use este campo si el comando contiene secretos tales como contraseñas.</span><span class="sxs-lookup"><span data-stu-id="13a15-126">Use this field instead if your command contains secrets such as passwords.</span></span>
* <span data-ttu-id="13a15-127">**storageAccountName**: (opcional, string) nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="13a15-127">**storageAccountName**: (optional, string) the name of storage account.</span></span> <span data-ttu-id="13a15-128">Si especifica credenciales de almacenamiento, todos los valores de fileUri deben ser direcciones URL de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="13a15-128">If you specify storage credentials, all fileUris must be URLs for Azure Blobs.</span></span>
* <span data-ttu-id="13a15-129">**storageAccountName**: (opcional, cadena) clave de acceso de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="13a15-129">**storageAccountKey**: (optional, string) the access key of storage account.</span></span>

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a><span data-ttu-id="13a15-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="13a15-130">Azure CLI</span></span>
<span data-ttu-id="13a15-131">Cuando use la CLI de Azure para ejecutar la extensión de script personalizado, cree uno o varios archivos de configuración que contengan como mínimo el URI de archivo y el comando de ejecución del script.</span><span class="sxs-lookup"><span data-stu-id="13a15-131">When using the Azure CLI to run the Custom Script Extension, create a configuration file or files containing at minimum the file uri, and the script execution command.</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="13a15-132">Opcionalmente, la configuración puede especificarse en el comando como una cadena con formato JSON.</span><span class="sxs-lookup"><span data-stu-id="13a15-132">Optionally the settings can be specified in the command as a JSON formatted string.</span></span> <span data-ttu-id="13a15-133">Esto permite especificar la configuración durante la ejecución sin un archivo de configuración independiente.</span><span class="sxs-lookup"><span data-stu-id="13a15-133">This allows the configuration to be specified during execution and without a separate configuration file.</span></span>

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a><span data-ttu-id="13a15-134">Ejemplos de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="13a15-134">Azure CLI Examples</span></span>

<span data-ttu-id="13a15-135">**Ejemplo 1** : configuración pública con archivo de script.</span><span class="sxs-lookup"><span data-stu-id="13a15-135">**Example 1** - Public configuration with script file.</span></span>

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

<span data-ttu-id="13a15-136">Comando de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="13a15-136">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="13a15-137">**Ejemplo 2** : configuración pública sin archivo de script.</span><span class="sxs-lookup"><span data-stu-id="13a15-137">**Example 2** - Public configuration with no script file.</span></span>

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

<span data-ttu-id="13a15-138">Comando de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="13a15-138">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="13a15-139">**Ejemplo 3** : se usa un archivo de configuración pública para especificar el URI del archivo de script y un archivo de configuración protegida para especificar el comando que se ejecutará.</span><span class="sxs-lookup"><span data-stu-id="13a15-139">**Example 3** - A public configuration file is used to specify the script file URI, and a protected configuration file is used to specify the command to be executed.</span></span>

<span data-ttu-id="13a15-140">Archivo de configuración pública:</span><span class="sxs-lookup"><span data-stu-id="13a15-140">Public configuration file:</span></span>

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

<span data-ttu-id="13a15-141">Archivo de configuración protegida:</span><span class="sxs-lookup"><span data-stu-id="13a15-141">Protected configuration file:</span></span>  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

<span data-ttu-id="13a15-142">Comando de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="13a15-142">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a><span data-ttu-id="13a15-143">Plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="13a15-143">Resource Manager Template</span></span>
<span data-ttu-id="13a15-144">La extensión de script personalizado de Azure se puede ejecutar en tiempo de implementación de la máquina virtual mediante una plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="13a15-144">The Azure Custom Script Extension can be run at Virtual Machine deployment time using a Resource Manager template.</span></span> <span data-ttu-id="13a15-145">Para ello, agregue código JSON con el formato correcto a la plantilla de implementación.</span><span class="sxs-lookup"><span data-stu-id="13a15-145">To do so, add properly formatted JSON to the deployment template.</span></span>

### <a name="resource-manager-examples"></a><span data-ttu-id="13a15-146">Ejemplos de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="13a15-146">Resource Manager Examples</span></span>
<span data-ttu-id="13a15-147">**Ejemplo 1** : configuración pública.</span><span class="sxs-lookup"><span data-stu-id="13a15-147">**Example 1** - public configuration.</span></span>

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

<span data-ttu-id="13a15-148">**Ejemplo 2** : comando de ejecución en la configuración protegida.</span><span class="sxs-lookup"><span data-stu-id="13a15-148">**Example 2** - execution command in protected configuration.</span></span>

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

<span data-ttu-id="13a15-149">Vea el ejemplo completo de Music Store de .NET Core: [Music Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db)(Ejemplo de Music Store).</span><span class="sxs-lookup"><span data-stu-id="13a15-149">See the .Net Core Music Store Demo for a complete example - [Music Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="13a15-150">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="13a15-150">Troubleshooting</span></span>
<span data-ttu-id="13a15-151">Cuando la extensión de script personalizado se ejecuta, el script se crea o se descarga en un directorio similar al del ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="13a15-151">When the Custom Script Extension runs, the script is created or downloaded into a directory similar to the following example.</span></span> <span data-ttu-id="13a15-152">La salida del comando se guarda también en este directorio, en los archivos `stdout` y `stderr`.</span><span class="sxs-lookup"><span data-stu-id="13a15-152">The command output is also saved into this directory in `stdout` and `stderr` file.</span></span>

```bash
/var/lib/waagent/custom-script/download/0/
```

<span data-ttu-id="13a15-153">La extensión de script de Azure genera un registro, que se encuentra aquí.</span><span class="sxs-lookup"><span data-stu-id="13a15-153">The Azure Script Extension produces a log, which can be found here.</span></span>

```bash
/var/log/azure/custom-script/handler.log
```

<span data-ttu-id="13a15-154">El estado de ejecución de la extensión de script personalizado también se puede recuperar con la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="13a15-154">The execution state of the Custom Script Extension can also be retrieved with the Azure CLI.</span></span>

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

<span data-ttu-id="13a15-155">La salida tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="13a15-155">The output looks like the following text:</span></span>

```azurecli
info:    Executing command vm extension get
+ Looking up the VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a><span data-ttu-id="13a15-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="13a15-156">Next Steps</span></span>
<span data-ttu-id="13a15-157">Para más información sobre otras extensiones de script de máquina virtual, consulte [Introducción a la extensión de script de Azure para Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="13a15-157">For information on other VM Script Extensions, see [Azure Script Extension overview for Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

