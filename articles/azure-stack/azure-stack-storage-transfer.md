---
title: Herramientas de Azure Stack Storage
description: "Obtenga información acerca de las herramientas de transferencia de datos de Azure Stack Storage"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/16/2017
ms.author: xiaofmao
ms.openlocfilehash: 01069b8b7488ae0caaec4ae608c36b0f361e544c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="tools-for-azure-stack-storage"></a><span data-ttu-id="a9d74-103">Herramientas de Azure Stack Storage</span><span class="sxs-lookup"><span data-stu-id="a9d74-103">Tools for Azure Stack Storage</span></span>

<span data-ttu-id="a9d74-104">Microsoft Azure Stack proporciona un conjunto de servicios de almacenamiento para discos, blobs, tablas, colas y funcionalidad de administración de cuentas.</span><span class="sxs-lookup"><span data-stu-id="a9d74-104">Microsoft Azure Stack provides a set of the storage services for disks, blobs, tables, queues, and account management functionality.</span></span> <span data-ttu-id="a9d74-105">Puede usar un conjunto de herramientas de Azure Storage si desea administrar o mover datos a Azure Stack Storage, o desde él.</span><span class="sxs-lookup"><span data-stu-id="a9d74-105">You can use a set of Azure Storage tools if you want to manage or move data to or from Azure Stack Storage.</span></span> <span data-ttu-id="a9d74-106">En este artículo se proporciona una descripción general de las herramientas disponibles.</span><span class="sxs-lookup"><span data-stu-id="a9d74-106">This article provides a quick overview of the tools available.</span></span>

<span data-ttu-id="a9d74-107">La herramienta que mejor se adapte a usted depende de sus requisitos:</span><span class="sxs-lookup"><span data-stu-id="a9d74-107">The tool that works best for you depends on your requirements:</span></span>
* [<span data-ttu-id="a9d74-108">AzCopy</span><span class="sxs-lookup"><span data-stu-id="a9d74-108">AzCopy</span></span>](#azcopy)

    <span data-ttu-id="a9d74-109">Una utilidad de línea de comandos específica para el almacenamiento que se puede descargar para copiar datos de un objeto a otro dentro de la cuenta de almacenamiento o entre cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a9d74-109">A storage-specific command-line utility that you can download to copy data from one object to another within your storage account, or between storage accounts.</span></span>

* [<span data-ttu-id="a9d74-110">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9d74-110">Azure PowerShell</span></span>](#azure-powershell)

    <span data-ttu-id="a9d74-111">Un shell de línea de comandos basado en tareas y un lenguaje de scripts diseñado especialmente para la administración del sistema.</span><span class="sxs-lookup"><span data-stu-id="a9d74-111">A task-based command-line shell and scripting language designed especially for system administration.</span></span>

* [<span data-ttu-id="a9d74-112">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a9d74-112">Azure CLI</span></span>](#azure-cli)

    <span data-ttu-id="a9d74-113">Una herramienta multiplataforma de código abierto que proporciona un conjunto de comandos para trabajar con las plataformas Azure y Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a9d74-113">An open-source, cross-platform tool that provides a set of commands for working with the Azure and Azure Stack platforms.</span></span>

* [<span data-ttu-id="a9d74-114">Explorador de Microsoft Azure Storage (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="a9d74-114">Microsoft Storage Explorer (Preview)</span></span>](#microsoft-azure-storage-explorer)

    <span data-ttu-id="a9d74-115">Una aplicación independiente fácil de usar con una interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="a9d74-115">An easy to use standalone app with a user interface.</span></span>

<span data-ttu-id="a9d74-116">Dadas las diferencias en los servicios de Storage entre Azure y Azure Stack, puede haber requisitos específicos para cada herramienta que se describe en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="a9d74-116">Due to the Storage services differences between Azure and Azure Stack, there might be some specific requirements for each tool described in the following sections.</span></span> <span data-ttu-id="a9d74-117">Para ver una comparación entre Azure Stack Storage y Azure Storage, consulte [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md) (Azure Stack Storage: diferencias y consideraciones).</span><span class="sxs-lookup"><span data-stu-id="a9d74-117">For a comparison between Azure Stack storage and Azure storage, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>


## <a name="azcopy"></a><span data-ttu-id="a9d74-118">AzCopy</span><span class="sxs-lookup"><span data-stu-id="a9d74-118">AzCopy</span></span>
<span data-ttu-id="a9d74-119">AzCopy es una utilidad de línea de comandos diseñada para copiar datos hacia y desde los servicios Microsoft Azure Blob Storage y Table Storage mediante sencillos comandos con un rendimiento óptimo.</span><span class="sxs-lookup"><span data-stu-id="a9d74-119">AzCopy is a command-line utility designed to copy data to and from Microsoft Azure Blob and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="a9d74-120">También puede copiar datos de un objeto a otro dentro de la cuenta de almacenamiento o entre cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a9d74-120">You can copy data from one object to another within your storage account, or between storage accounts.</span></span> <span data-ttu-id="a9d74-121">Hay dos versiones de AzCopy: AzCopy en Windows y AzCopy en Linux.</span><span class="sxs-lookup"><span data-stu-id="a9d74-121">There are two version of the AzCopy: AzCopy on Windows and AzCopy on Linux.</span></span> <span data-ttu-id="a9d74-122">Azure Stack solo admite la versión de Windows.</span><span class="sxs-lookup"><span data-stu-id="a9d74-122">Azure Stack only supports the Windows version.</span></span> 
 
### <a name="download-and-install-azcopy"></a><span data-ttu-id="a9d74-123">Descarga e instalación de AzCopy</span><span class="sxs-lookup"><span data-stu-id="a9d74-123">Download and install AzCopy</span></span> 
<span data-ttu-id="a9d74-124">[Descargue](https://aka.ms/azcopyforazurestack) la versión compatible con Windows de AzCopy para Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a9d74-124">[Download](https://aka.ms/azcopyforazurestack) the supported Windows version of AzCopy for Azure Stack.</span></span> <span data-ttu-id="a9d74-125">AzCopy se puede instalar y usar en Azure Stack del mismo modo que Azure.</span><span class="sxs-lookup"><span data-stu-id="a9d74-125">You can install and use AzCopy on Azure Stack the same way as Azure.</span></span> <span data-ttu-id="a9d74-126">Para más información, consulte [Transferencia de datos con AzCopy en Windows](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="a9d74-126">To learn more, see [Transfer data with the AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="azcopy-command-examples-for-data-transfer"></a><span data-ttu-id="a9d74-127">Ejemplos del comando AzCopy para la transferencia de datos</span><span class="sxs-lookup"><span data-stu-id="a9d74-127">AzCopy command examples for data transfer</span></span>
<span data-ttu-id="a9d74-128">Los ejemplos siguientes muestran varios escenarios habituales para copiar datos a los blobs de Azure Stack y desde ellos.</span><span class="sxs-lookup"><span data-stu-id="a9d74-128">The following examples demonstrate a few typical scenarios for copying data to and from Azure Stack blobs.</span></span> <span data-ttu-id="a9d74-129">Para más información, consulte [Transferencia de datos con AzCopy en Windows](../storage/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="a9d74-129">To learn more, see [Transfer data with the AzCopy Command-Line Utility](../storage/storage-use-azcopy.md).</span></span> 
#### <a name="download-all-blobs-to-local-disk"></a><span data-ttu-id="a9d74-130">Descarga de todos los blobs en el disco local</span><span class="sxs-lookup"><span data-stu-id="a9d74-130">Download all blobs to local disk</span></span>
```azcopy
AzCopy.exe /source:https://myaccount.blob.local.azurestack.external/mycontainer /dest:C:\myfolder /sourcekey:<key> /S
```
#### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="a9d74-131">Carga de un solo archivo en el directorio virtual</span><span class="sxs-lookup"><span data-stu-id="a9d74-131">Upload single file to virtual directory</span></span> 
```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.local.azurestack.external/mycontainer/vd /DestKey:key /Pattern:abc.txt
```
#### <a name="move-data-between-azure-and-azure-stack-storage"></a><span data-ttu-id="a9d74-132">Movimiento de datos entre Azure y Azure Stack Storage</span><span class="sxs-lookup"><span data-stu-id="a9d74-132">Move data between Azure and Azure Stack Storage</span></span> 
<span data-ttu-id="a9d74-133">No se admite la transferencia de datos asincrónica entre Azure Storage y Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a9d74-133">Asynchronous data transfer between Azure Storage and Azure Stack is not supported.</span></span> <span data-ttu-id="a9d74-134">La transferencia se debe especificar con la opción `/SyncCopy`.</span><span class="sxs-lookup"><span data-stu-id="a9d74-134">you need to specify the transfer with the `/SyncCopy` option.</span></span> 
```azcopy 
Azcopy /Source:https://myaccount.blob.local.azurestack.external/mycontainer /Dest:https://myaccount2.blob.core.windows.net/mycontainer2 /SourceKey:AzSKey /DestKey:Azurekey /S /SyncCopy
```

### <a name="azcopy-known-issues"></a><span data-ttu-id="a9d74-135">Problemas conocidos de Azcopy</span><span class="sxs-lookup"><span data-stu-id="a9d74-135">Azcopy Known issues</span></span>
* <span data-ttu-id="a9d74-136">Las operaciones de AzCopy en File Storage no están disponible porque File Storage aún no está disponible en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a9d74-136">Any AzCopy operation on File storage is not available because File Storage is not yet available in Azure Stack.</span></span>
* <span data-ttu-id="a9d74-137">No se admite la transferencia de datos asincrónica entre Azure Storage y Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a9d74-137">Asynchronous data transfer between Azure Storage and Azure Stack is not supported.</span></span> <span data-ttu-id="a9d74-138">Puede especificar la transferencia con la opción `/SyncCopy` para copiar los datos.</span><span class="sxs-lookup"><span data-stu-id="a9d74-138">You can specify the transfer with the `/SyncCopy` option to copy the data.</span></span>
* <span data-ttu-id="a9d74-139">No se admite la versión Linux de Azcopy para Azure Stack Storage.</span><span class="sxs-lookup"><span data-stu-id="a9d74-139">The Linux version of Azcopy is not supported for Azure Stack Storage.</span></span> 

## <a name="azure-powershell"></a><span data-ttu-id="a9d74-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9d74-140">Azure PowerShell</span></span>
<span data-ttu-id="a9d74-141">Azure PowerShell es un módulo que proporciona cmdlets para administrar servicios tanto en Azure como en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a9d74-141">Azure PowerShell is a module that provides cmdlets for managing services on both Azure and Azure Stack.</span></span> <span data-ttu-id="a9d74-142">Se trata de un shell de línea de comandos basado en tareas y un lenguaje de scripts especialmente diseñados para administración del sistema.</span><span class="sxs-lookup"><span data-stu-id="a9d74-142">It's a task-based command-line shell and scripting language designed especially for system administration.</span></span>

### <a name="install-and-configure-powershell-for-azure-stack"></a><span data-ttu-id="a9d74-143">Instalación y configuración de PowerShell para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a9d74-143">Install and Configure PowerShell for Azure Stack</span></span>
<span data-ttu-id="a9d74-144">Los módulos de Azure PowerShell compatibles con Azure Stack se requieren para trabajar con Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a9d74-144">Azure Stack compatible Azure PowerShell modules are required to work with Azure Stack.</span></span> <span data-ttu-id="a9d74-145">Para más información, consulte [Instalación de PowerShell para Azure Stack](azure-stack-powershell-install.md) y [Configuración del entorno de PowerShell del usuario de Azure Stack](azure-stack-powershell-configure-user.md).</span><span class="sxs-lookup"><span data-stu-id="a9d74-145">For more information, see [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) and [Configure the Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md) to learn more.</span></span>

### <a name="powershell-sample-script-for-azure-stack"></a><span data-ttu-id="a9d74-146">Script de ejemplo de PowerShell para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a9d74-146">PowerShell Sample script for Azure Stack</span></span> 
<span data-ttu-id="a9d74-147">En este ejemplo se supone que ha [instalado PowerShell para Azure Stack](azure-stack-powershell-install.md) correctamente.</span><span class="sxs-lookup"><span data-stu-id="a9d74-147">This sample assume you have successfully [Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> <span data-ttu-id="a9d74-148">Este script le ayudará a completar la configuración y a pedir las credenciales de su inquilino de Azure Stack para agregar su cuenta al entorno local de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9d74-148">This script will help you conplete the configuration and ask your Azure Stack tenant credentials to add your account to the local PowerShell environemnt.</span></span> <span data-ttu-id="a9d74-149">A continuación, el script establecerá la suscripción predeterminada de Azure, creará un una nueva cuenta de almacenamiento en Azure, creará un nuevo contenedor en dicha cuenta de almacenamiento y cargará un archivo de imagen existente (blob) en dicho contenedor.</span><span class="sxs-lookup"><span data-stu-id="a9d74-149">Then, the script will set the default Azure subscription, create a new storage account in Azure, create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="a9d74-150">Una vez el script ha enumerado todos los blobs en ese contenedor, creará un nuevo directorio de destino en el equipo local y descargará el archivo de imagen.</span><span class="sxs-lookup"><span data-stu-id="a9d74-150">After the script lists all blobs in that container, it will create a new destination directory in your local computer and download the image file.</span></span>

1. <span data-ttu-id="a9d74-151">Instale los [módulos de Azure PowerShell compatibles con Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="a9d74-151">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
2. <span data-ttu-id="a9d74-152">Descargue las [herramientas necesarias para trabajar con Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="a9d74-152">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span>  
3. <span data-ttu-id="a9d74-153">Abra **Windows PowerShell ISE** y haga clic en **Ejecutar como administrador**, **Archivo** > **Nuevo** para crear un archivo de script nuevo.</span><span class="sxs-lookup"><span data-stu-id="a9d74-153">Open **Windows PowerShell ISE** and **Run as Administrator**, click **File** > **New** to create a new script file.</span></span>
4. <span data-ttu-id="a9d74-154">Copie el siguiente script y péguelo en el archivo de script nuevo.</span><span class="sxs-lookup"><span data-stu-id="a9d74-154">Copy the script below and paste to the new script file.</span></span>
5. <span data-ttu-id="a9d74-155">Actualice las variables del script en función de su configuración.</span><span class="sxs-lookup"><span data-stu-id="a9d74-155">Update the script variables based on your configuration settings.</span></span> 
6. <span data-ttu-id="a9d74-156">Nota: Este script tiene que ejecutarse bajo la raíz del **AzureStack_Tools** descargado.</span><span class="sxs-lookup"><span data-stu-id="a9d74-156">Note: this script has to be run under the root of downloaded **AzureStack_Tools**.</span></span> 

```PowerShell 
# begin

$ARMEvnName = "AzureStackUser" # set AzureStackUser as your Azure Stack environemnt name
$ARMEndPoint = "https://management.local.azurestack.external" 
$GraphAudiance = "https://graph.windows.net/" 
$AADTenantName = "<myDirectoryTenantName>.onmicrosoft.com" 

$SubscriptionName = "basic" # Update with the name of your subscription.
$ResourceGroupName = "myTestRG" # Give a name to your new resource group.
$StorageAccountName = "azsblobcontainer" # Give a name to your new storage account. It must be lowercase!
$Location = "Local" # Choose "Local" as an example.
$ContainerName = "photo" # Give a name to your new container.
$ImageToUpload = "C:\temp\Hello.jpg" # Prepare an image file and a source directory in your local computer.
$DestinationFolder = "C:\temp\downlaod" # A destination directory in your local computer.

# Import the Connect PowerShell module"
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
Import-Module .\Connect\AzureStack.Connect.psm1

# Configure the PowerShell environment
# Register an AzureRM environment that targets your Azure Stack instance
Add-AzureRmEnvironment -Name $ARMEvnName -ARMEndpoint $ARMEndPoint 

# Set the GraphEndpointResourceId value
Set-AzureRmEnvironment -Name $ARMEvnName -GraphEndpoint $GraphAudiance

# Login
$TenantID = Get-AzsDirectoryTenantId -AADTenantName $AADTenantName -EnvironmentName $ARMEvnName
Login-AzureRmAccount -EnvironmentName $ARMEvnName -TenantId $TenantID 

# Set a default Azure subscription.
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Create a new Resource Group 
New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

# Create a new storage account.
New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS

# Set a default storage account.
Set-AzureRmCurrentStorageAccount -StorageAccountName $StorageAccountName -ResourceGroupName $ResourceGroupName 

# Create a new container.
New-AzureStorageContainer -Name $ContainerName -Permission Off

# Upload a blob into a container.
Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload

# List all blobs in a container.
Get-AzureStorageBlob -Container $ContainerName

# Download blobs from the container:
# Get a reference to a list of all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName

# Create the destination directory.
New-Item -Path $DestinationFolder -ItemType Directory -Force  

# Download blobs into the local destination directory.
$blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder

# end
```

### <a name="powershell-known-issues"></a><span data-ttu-id="a9d74-157">Problemas conocidos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9d74-157">PowerShell Known Issues</span></span> 
<span data-ttu-id="a9d74-158">La versión actual del módulo Azure PowerShell compatible con Azure Stack es 1.2.10.</span><span class="sxs-lookup"><span data-stu-id="a9d74-158">The current compatible Azure PowerShell module version for Azure Stack is 1.2.10.</span></span> <span data-ttu-id="a9d74-159">Tiene ciertas diferencias con la versión más reciente de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9d74-159">It’s different from the latest version of Azure PowerShell.</span></span> <span data-ttu-id="a9d74-160">La principal diferencia afecta al funcionamiento de los servicios de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="a9d74-160">This difference impacts storage services operation:</span></span>

* <span data-ttu-id="a9d74-161">El formato del valor de retorno de `Get-AzureRmStorageAccountKey` en la versión 1.2.10 tiene dos propiedades: `Key1` y `Key2`, mientras que la versión actual de Azure devuelve una matriz que contiene todas las claves de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="a9d74-161">The return value format of `Get-AzureRmStorageAccountKey` in version 1.2.10 has two properties: `Key1` and `Key2`, while the current Azure version returns an array containing all the account keys.</span></span>
   ```
   # This command gets a specific key for a Storage account, 
   # and works for Azure PowerShell version 1.4, and later versions.
   (Get-AzureRmStorageAccountKey -ResourceGroupName "RG01" `
   -AccountName "MyStorageAccount").Value[0]

   # This command gets a specific key for a Storage account, 
   # and works for Azure PowerShell version 1.3.2, and previous versions.
   (Get-AzureRmStorageAccountKey -ResourceGroupName "RG01" `
   -AccountName "MyStorageAccount").Key1

   ```
   <span data-ttu-id="a9d74-162">Para más información, consulte [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).</span><span class="sxs-lookup"><span data-stu-id="a9d74-162">For more information, see [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).</span></span>

## <a name="azure-cli"></a><span data-ttu-id="a9d74-163">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a9d74-163">Azure CLI</span></span>
<span data-ttu-id="a9d74-164">La CLI de Azure es la forma de usar la línea de comandos de Azure para administrar los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a9d74-164">The Azure CLI is Azure’s command-line experience for managing Azure resources.</span></span> <span data-ttu-id="a9d74-165">Puede instalarla en macOS, Linux y Windows, y ejecutarla desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="a9d74-165">You can install it on macOS, Linux, and Windows and run it from the command line.</span></span> 

<span data-ttu-id="a9d74-166">La CLI de Azure está optimizada para administrar recursos de Azure desde la línea de comandos y para compilar scripts de automatización que funcionen con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a9d74-166">Azure CLI is optimized for managing and administering Azure resources from the command line, and for building automation scripts that work against the Azure Resource Manager.</span></span> <span data-ttu-id="a9d74-167">Proporciona muchas de las funciones que se encuentran en Azure Stack Portal, lo que incluye el acceso a datos enriquecidos.</span><span class="sxs-lookup"><span data-stu-id="a9d74-167">It provides many of the same functions found in the Azure Stack portal, including rich data access.</span></span>

<span data-ttu-id="a9d74-168">Azure Stack requiere la versión 2.0 de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="a9d74-168">Azure Stack requires Azure CLI version 2.0.</span></span> <span data-ttu-id="a9d74-169">Para más información acerca de cómo instalar y Azure PowerShell con Azure Stack, consulte [Install and configure Azure Stack CLI](azure-stack-connect-cli.md) (Instalación y configuración de la CLI de Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="a9d74-169">For more information about installing and configuring Azure CLI with Azure Stack, see [Install and configure Azure Stack CLI](azure-stack-connect-cli.md).</span></span> <span data-ttu-id="a9d74-170">Para más información acerca de cómo utilizar la CLI de Azure 2.0 para realizar varias tareas relativas al trabajo con recursos de su cuenta de Azure Stack Storage, consulte [Uso de la CLI de Azure 2.0 con Azure Storage](../storage/storage-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="a9d74-170">For more information about how to use the Azure CLI 2.0 to perform several tasks working with resources in your Azure Stack Storage account, see [Using the Azure CLI2.0 with Azure Storage](../storage/storage-azure-cli.md)</span></span>

### <a name="azure-cli-sample-script-for-azure-stack"></a><span data-ttu-id="a9d74-171">Script de ejemplo de la CLI de Azure para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a9d74-171">Azure CLI sample script for Azure Stack</span></span> 
<span data-ttu-id="a9d74-172">Cuando haya completado la instalación y configuración de la CLI, puede probar los siguientes pasos para trabajar con un pequeño script de ejemplo de shell pequeño para interactuar con los recursos de Azure Stack Storage.</span><span class="sxs-lookup"><span data-stu-id="a9d74-172">Once you complete the CLI installation and configuration, you can try the following steps to work with a small shell sample script to interact with Azure Stack Storage resources.</span></span> <span data-ttu-id="a9d74-173">En primer lugar, el script crea un contenedor nuevo en la cuenta de almacenamiento, después, carga un archivo existente (como un blob) en dicho contenedor, enumera todos los blobs del contenedor y, por último, descarga el archivo en el destino del equipo local que especifique.</span><span class="sxs-lookup"><span data-stu-id="a9d74-173">The script first creates a new container in your storage account, then uploads an existing file (as a blob) to that container, lists all blobs in the container, and finally, downloads the file to a destination on your local computer that you specify.</span></span> <span data-ttu-id="a9d74-174">Antes de ejecutar este script, asegúrese de que se conecta a inicia sesión correctamente con el servicio Azure Stack de destino.</span><span class="sxs-lookup"><span data-stu-id="a9d74-174">Before you run this script, make sure you successfully connect and login to the target Azure Stack.</span></span> 
1. <span data-ttu-id="a9d74-175">Abra el editor de texto que prefiera; copie y pegue el script anterior en el editor.</span><span class="sxs-lookup"><span data-stu-id="a9d74-175">Open your favorite text editor, then copy and paste the preceding script into the editor.</span></span>
2. <span data-ttu-id="a9d74-176">Actualice las variables del script para incluir sus opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="a9d74-176">Update the script's variables to reflect your configuration settings.</span></span> 
3. <span data-ttu-id="a9d74-177">Después de actualizar las variables necesarias, guarde el script y salga del editor.</span><span class="sxs-lookup"><span data-stu-id="a9d74-177">After you've updated the necessary variables, save the script and exit your editor.</span></span> <span data-ttu-id="a9d74-178">En los siguientes pasos se da por hecho que ha llamado al script my_storage_sample.sh.</span><span class="sxs-lookup"><span data-stu-id="a9d74-178">The next steps assume you've named your script my_storage_sample.sh.</span></span>
4. <span data-ttu-id="a9d74-179">Marque el script como archivo ejecutable si es necesario: `chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="a9d74-179">Mark the script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>
5. <span data-ttu-id="a9d74-180">Ejecute el script.</span><span class="sxs-lookup"><span data-stu-id="a9d74-180">Execute the script.</span></span> <span data-ttu-id="a9d74-181">Por ejemplo, en Bash: `./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="a9d74-181">For example, in Bash: `./my_storage_sample.sh`</span></span>

```bash
#!/bin/bash
# A simple Azure Stack Storage example script

export AZURESTACK_RESOURCE_GROUP=<resource_group_name>
export AZURESTACK_RG_LOCATION="local"
export AZURESTACK_STORAGE_ACCOUNT_NAME=<storage_account_name>
export AZURESTACK_STORAGE_CONTAINER_NAME=<container_name>
export AZURESTACK_STORAGE_BLOB_NAME=<blob_name>
export FILE_TO_UPLOAD=<file_to_upload>
export DESTINATION_FILE=<destination_file>

echo "Creating the resource group..."
az group create --name $AZURESTACK_RESOURCE_GROUP --location $AZURESTACK_RG_LOCATION

echo "Creating the storage account..."
az storage account create --name $AZURESTACK_STORAGE_ACCOUNT_NAME --resource-group $AZURESTACK_RESOURCE_GROUP --account-type Standard_LRS

echo "Creating the blob container..."
az storage container create --name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Uploading the file..."
az storage blob upload --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --file $FILE_TO_UPLOAD --name $AZURESTACK_STORAGE_BLOB_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Listing the blobs..."
az storage blob list --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --output table

echo "Downloading the file..."
az storage blob download --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --name $AZURESTACK_STORAGE_BLOB_NAME --file $DESTINATION_FILE --output table

echo "Done"
```

## <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="a9d74-182">Explorador de almacenamiento de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a9d74-182">Microsoft Azure Storage Explorer</span></span>

<span data-ttu-id="a9d74-183">El Explorador de Microsoft Azure Storage es una aplicación independiente de Microsoft</span><span class="sxs-lookup"><span data-stu-id="a9d74-183">Microsoft Azure Storage Explorer is a standalone app from Microsoft.</span></span> <span data-ttu-id="a9d74-184">que permite trabajar fácilmente con los datos de Azure Storage y Azure Stack Storage en Windows, macOS y Linux.</span><span class="sxs-lookup"><span data-stu-id="a9d74-184">It allows you to easily work with both Azure Storage and Azure Stack Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="a9d74-185">Si desea una manera fácil de administrar los datos de Azure Stack Storage, considere la posibilidad de usar el Explorador de Microsoft Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="a9d74-185">If you want an easy way to manage your Azure Stack Storage data, then consider using Microsoft Azure Storage Explorer.</span></span>

<span data-ttu-id="a9d74-186">Para más información acerca de cómo configurar el Explorador de Azure Storage para que funcione con Azure Stack, consulte [Connect Storage Explorer to an Azure Stack subscription](azure-stack-storage-connect-se.md) (Conexión del Explorador de Storage a una suscripción de Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="a9d74-186">For more information about configuring Azure Storage Explorer to work with Azure Stack, see [Connect Storage Explorer to an Azure Stack subscription](azure-stack-storage-connect-se.md).</span></span>

<span data-ttu-id="a9d74-187">Para más información acerca del Explorador de Microsoft Azure Storage, consulte [Introducción al Explorador de Storage (versión preliminar)](../vs-azure-tools-storage-manage-with-storage-explorer.md)</span><span class="sxs-lookup"><span data-stu-id="a9d74-187">For more information about Microsoft Azure Storage Explorer, see [Get started with Storage Explorer (Preview)](../vs-azure-tools-storage-manage-with-storage-explorer.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9d74-188">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a9d74-188">Next steps</span></span>
* [<span data-ttu-id="a9d74-189">Conexión del Explorador de Storage a una suscripción de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a9d74-189">Connect Storage Explorer to an Azure Stack subscription</span></span>](azure-stack-storage-connect-se.md)
* [<span data-ttu-id="a9d74-190">Introducción al Explorador de Storage (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="a9d74-190">Get started with Storage Explorer (Preview)</span></span>](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* <span data-ttu-id="a9d74-191">[Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md) (Azure Stack Storage: diferencias y consideraciones)</span><span class="sxs-lookup"><span data-stu-id="a9d74-191">[Azure-consistent storage: differences and considerations](azure-stack-acs-differences.md)</span></span>
* [<span data-ttu-id="a9d74-192">Introducción a Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a9d74-192">Introduction to Microsoft Azure Storage</span></span>](../storage/common/storage-introduction.md)

