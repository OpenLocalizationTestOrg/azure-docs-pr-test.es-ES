---
title: aaaTools para el almacenamiento de la pila de Azure
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
ms.openlocfilehash: 184a1a51b4267e913aae823df31df3704d8e7b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tools-for-azure-stack-storage"></a><span data-ttu-id="7c8a5-103">Herramientas de Azure Stack Storage</span><span class="sxs-lookup"><span data-stu-id="7c8a5-103">Tools for Azure Stack Storage</span></span>

<span data-ttu-id="7c8a5-104">Pila de Microsoft Azure proporciona un conjunto de servicios de almacenamiento de Hola para discos, blobs, tablas, colas y funcionalidad de administración de cuentas.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-104">Microsoft Azure Stack provides a set of hello storage services for disks, blobs, tables, queues, and account management functionality.</span></span> <span data-ttu-id="7c8a5-105">Puede usar un conjunto de herramientas de almacenamiento de Azure si desea toomanage o mover datos tooor pila del almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-105">You can use a set of Azure Storage tools if you want toomanage or move data tooor from Azure Stack Storage.</span></span> <span data-ttu-id="7c8a5-106">Este artículo proporciona una introducción rápida de herramientas de hello disponibles.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-106">This article provides a quick overview of hello tools available.</span></span>

<span data-ttu-id="7c8a5-107">depende de la herramienta Hola que mejor se adapte a sus requisitos:</span><span class="sxs-lookup"><span data-stu-id="7c8a5-107">hello tool that works best for you depends on your requirements:</span></span>
* [<span data-ttu-id="7c8a5-108">AzCopy</span><span class="sxs-lookup"><span data-stu-id="7c8a5-108">AzCopy</span></span>](#azcopy)

    <span data-ttu-id="7c8a5-109">Una utilidad de línea de comandos específicos del almacenamiento que puede descargar toocopy datos de un objeto tooanother dentro de la cuenta de almacenamiento, o entre cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-109">A storage-specific command-line utility that you can download toocopy data from one object tooanother within your storage account, or between storage accounts.</span></span>

* [<span data-ttu-id="7c8a5-110">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c8a5-110">Azure PowerShell</span></span>](#azure-powershell)

    <span data-ttu-id="7c8a5-111">Un shell de línea de comandos basado en tareas y un lenguaje de scripts diseñado especialmente para la administración del sistema.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-111">A task-based command-line shell and scripting language designed especially for system administration.</span></span>

* [<span data-ttu-id="7c8a5-112">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="7c8a5-112">Azure CLI</span></span>](#azure-cli)

    <span data-ttu-id="7c8a5-113">Una herramienta de código abierto, multiplataforma que proporciona un conjunto de comandos para trabajar con las plataformas de Azure y Azure pila Hola.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-113">An open-source, cross-platform tool that provides a set of commands for working with hello Azure and Azure Stack platforms.</span></span>

* [<span data-ttu-id="7c8a5-114">Explorador de Microsoft Azure Storage (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="7c8a5-114">Microsoft Storage Explorer (Preview)</span></span>](#microsoft-azure-storage-explorer)

    <span data-ttu-id="7c8a5-115">Una aplicación independiente de toouse fácil con una interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-115">An easy toouse standalone app with a user interface.</span></span>

<span data-ttu-id="7c8a5-116">Debido a diferencias de servicios de almacenamiento de toohello entre Azure y la pila de Azure, puede haber algunos requisitos específicos para cada herramienta que se describe en las secciones siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-116">Due toohello Storage services differences between Azure and Azure Stack, there might be some specific requirements for each tool described in hello following sections.</span></span> <span data-ttu-id="7c8a5-117">Para ver una comparación entre Azure Stack Storage y Azure Storage, consulte [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md) (Azure Stack Storage: diferencias y consideraciones).</span><span class="sxs-lookup"><span data-stu-id="7c8a5-117">For a comparison between Azure Stack storage and Azure storage, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>


## <a name="azcopy"></a><span data-ttu-id="7c8a5-118">AzCopy</span><span class="sxs-lookup"><span data-stu-id="7c8a5-118">AzCopy</span></span>
<span data-ttu-id="7c8a5-119">AzCopy es una tooand de datos de utilidad de línea de comandos diseñada toocopy desde el almacenamiento de blobs de Microsoft Azure y la tabla mediante comandos simples con un rendimiento óptimo.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-119">AzCopy is a command-line utility designed toocopy data tooand from Microsoft Azure Blob and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="7c8a5-120">Puede copiar datos de una tooanother de objeto dentro de la cuenta de almacenamiento, o entre cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-120">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span> <span data-ttu-id="7c8a5-121">Hay dos versiones de Hola AzCopy: AzCopy en Windows y AzCopy en Linux.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-121">There are two version of hello AzCopy: AzCopy on Windows and AzCopy on Linux.</span></span> <span data-ttu-id="7c8a5-122">Pila de Azure solo admite la versión de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-122">Azure Stack only supports hello Windows version.</span></span> 
 
### <a name="download-and-install-azcopy"></a><span data-ttu-id="7c8a5-123">Descarga e instalación de AzCopy</span><span class="sxs-lookup"><span data-stu-id="7c8a5-123">Download and install AzCopy</span></span> 
<span data-ttu-id="7c8a5-124">[Descargar](https://aka.ms/azcopyforazurestack) Hola admitida la versión de Windows de AzCopy para la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-124">[Download](https://aka.ms/azcopyforazurestack) hello supported Windows version of AzCopy for Azure Stack.</span></span> <span data-ttu-id="7c8a5-125">Puede instalar y usar AzCopy en Hola de pila de Azure igual que Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-125">You can install and use AzCopy on Azure Stack hello same way as Azure.</span></span> <span data-ttu-id="7c8a5-126">más información, consulte toolearn [transferir datos con la utilidad de línea de comandos de AzCopy hello](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="7c8a5-126">toolearn more, see [Transfer data with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="azcopy-command-examples-for-data-transfer"></a><span data-ttu-id="7c8a5-127">Ejemplos del comando AzCopy para la transferencia de datos</span><span class="sxs-lookup"><span data-stu-id="7c8a5-127">AzCopy command examples for data transfer</span></span>
<span data-ttu-id="7c8a5-128">Hello en los ejemplos siguientes muestra algunos escenarios típicos para copiar datos tooand de blobs de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-128">hello following examples demonstrate a few typical scenarios for copying data tooand from Azure Stack blobs.</span></span> <span data-ttu-id="7c8a5-129">más información, consulte toolearn [transferir datos con la utilidad de línea de comandos de AzCopy hello](../storage/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="7c8a5-129">toolearn more, see [Transfer data with hello AzCopy Command-Line Utility](../storage/storage-use-azcopy.md).</span></span> 
#### <a name="download-all-blobs-toolocal-disk"></a><span data-ttu-id="7c8a5-130">Descargue todos los blobs toolocal disco</span><span class="sxs-lookup"><span data-stu-id="7c8a5-130">Download all blobs toolocal disk</span></span>
```azcopy
AzCopy.exe /source:https://myaccount.blob.local.azurestack.external/mycontainer /dest:C:\myfolder /sourcekey:<key> /S
```
#### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="7c8a5-131">Cargar archivo único directorio toovirtual</span><span class="sxs-lookup"><span data-stu-id="7c8a5-131">Upload single file toovirtual directory</span></span> 
```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.local.azurestack.external/mycontainer/vd /DestKey:key /Pattern:abc.txt
```
#### <a name="move-data-between-azure-and-azure-stack-storage"></a><span data-ttu-id="7c8a5-132">Movimiento de datos entre Azure y Azure Stack Storage</span><span class="sxs-lookup"><span data-stu-id="7c8a5-132">Move data between Azure and Azure Stack Storage</span></span> 
<span data-ttu-id="7c8a5-133">No se admite la transferencia de datos asincrónica entre Azure Storage y Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-133">Asynchronous data transfer between Azure Storage and Azure Stack is not supported.</span></span> <span data-ttu-id="7c8a5-134">necesita transferencia de hello toospecify con hello `/SyncCopy` opción.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-134">you need toospecify hello transfer with hello `/SyncCopy` option.</span></span> 
```azcopy 
Azcopy /Source:https://myaccount.blob.local.azurestack.external/mycontainer /Dest:https://myaccount2.blob.core.windows.net/mycontainer2 /SourceKey:AzSKey /DestKey:Azurekey /S /SyncCopy
```

### <a name="azcopy-known-issues"></a><span data-ttu-id="7c8a5-135">Problemas conocidos de Azcopy</span><span class="sxs-lookup"><span data-stu-id="7c8a5-135">Azcopy Known issues</span></span>
* <span data-ttu-id="7c8a5-136">Las operaciones de AzCopy en File Storage no están disponible porque File Storage aún no está disponible en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-136">Any AzCopy operation on File storage is not available because File Storage is not yet available in Azure Stack.</span></span>
* <span data-ttu-id="7c8a5-137">No se admite la transferencia de datos asincrónica entre Azure Storage y Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-137">Asynchronous data transfer between Azure Storage and Azure Stack is not supported.</span></span> <span data-ttu-id="7c8a5-138">Puede especificar Hola transferencia con hello `/SyncCopy` opción datos de hello toocopy.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-138">You can specify hello transfer with hello `/SyncCopy` option toocopy hello data.</span></span>
* <span data-ttu-id="7c8a5-139">no se admite la versión de Linux de Hola de Azcopy para el almacenamiento de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-139">hello Linux version of Azcopy is not supported for Azure Stack Storage.</span></span> 

## <a name="azure-powershell"></a><span data-ttu-id="7c8a5-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c8a5-140">Azure PowerShell</span></span>
<span data-ttu-id="7c8a5-141">Azure PowerShell es un módulo que proporciona cmdlets para administrar servicios tanto en Azure como en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-141">Azure PowerShell is a module that provides cmdlets for managing services on both Azure and Azure Stack.</span></span> <span data-ttu-id="7c8a5-142">Se trata de un shell de línea de comandos basado en tareas y un lenguaje de scripts especialmente diseñados para administración del sistema.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-142">It's a task-based command-line shell and scripting language designed especially for system administration.</span></span>

### <a name="install-and-configure-powershell-for-azure-stack"></a><span data-ttu-id="7c8a5-143">Instalación y configuración de PowerShell para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="7c8a5-143">Install and Configure PowerShell for Azure Stack</span></span>
<span data-ttu-id="7c8a5-144">Módulos de PowerShell de Azure compatibles de pila de Azure son necesario toowork con la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-144">Azure Stack compatible Azure PowerShell modules are required toowork with Azure Stack.</span></span> <span data-ttu-id="7c8a5-145">Para obtener más información, consulte [instale PowerShell para Azure pila](azure-stack-powershell-install.md) y [configurar el entorno de PowerShell del usuario de hello Azure pila](azure-stack-powershell-configure-user.md) toolearn más.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-145">For more information, see [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) and [Configure hello Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md) toolearn more.</span></span>

### <a name="powershell-sample-script-for-azure-stack"></a><span data-ttu-id="7c8a5-146">Script de ejemplo de PowerShell para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="7c8a5-146">PowerShell Sample script for Azure Stack</span></span> 
<span data-ttu-id="7c8a5-147">En este ejemplo se supone que ha [instalado PowerShell para Azure Stack](azure-stack-powershell-install.md) correctamente.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-147">This sample assume you have successfully [Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> <span data-ttu-id="7c8a5-148">Este script le ayudarán conplete configuración de Hola y pedir que credenciales de su inquilino de Azure pila tooadd su entorno de PowerShell cuenta toohello local.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-148">This script will help you conplete hello configuration and ask your Azure Stack tenant credentials tooadd your account toohello local PowerShell environemnt.</span></span> <span data-ttu-id="7c8a5-149">A continuación, Hola script establezca el valor predeterminado de hello suscripción de Azure, crear una nueva cuenta de almacenamiento de Azure, cree un nuevo contenedor en esta nueva cuenta de almacenamiento y cargar un contenedor de toothat de archivo (blob) de imagen existente.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-149">Then, hello script will set hello default Azure subscription, create a new storage account in Azure, create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="7c8a5-150">Después de script de Hola enumera todos los blobs en ese contenedor, creará un nuevo directorio de destino en el equipo local y descargar el archivo de imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-150">After hello script lists all blobs in that container, it will create a new destination directory in your local computer and download hello image file.</span></span>

1. <span data-ttu-id="7c8a5-151">Instale los [módulos de Azure PowerShell compatibles con Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="7c8a5-151">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
2. <span data-ttu-id="7c8a5-152">Descargar hello [toowork necesarios de herramientas con la pila de Azure](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="7c8a5-152">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  
3. <span data-ttu-id="7c8a5-153">Abra **Windows PowerShell ISE** y **ejecutar como administrador**, haga clic en **archivo** > **New** toocreate un nuevo archivo de script.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-153">Open **Windows PowerShell ISE** and **Run as Administrator**, click **File** > **New** toocreate a new script file.</span></span>
4. <span data-ttu-id="7c8a5-154">Copie el siguiente script de Hola y pegue toohello nuevo archivo de script.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-154">Copy hello script below and paste toohello new script file.</span></span>
5. <span data-ttu-id="7c8a5-155">Actualice las variables de secuencia de comandos de hello en función de las opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-155">Update hello script variables based on your configuration settings.</span></span> 
6. <span data-ttu-id="7c8a5-156">Nota: esta secuencia de comandos tiene toobe se ejecutan en la raíz de Hola de descargado **AzureStack_Tools**.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-156">Note: this script has toobe run under hello root of downloaded **AzureStack_Tools**.</span></span> 

```PowerShell 
# begin

$ARMEvnName = "AzureStackUser" # set AzureStackUser as your Azure Stack environemnt name
$ARMEndPoint = "https://management.local.azurestack.external" 
$GraphAudiance = "https://graph.windows.net/" 
$AADTenantName = "<myDirectoryTenantName>.onmicrosoft.com" 

$SubscriptionName = "basic" # Update with hello name of your subscription.
$ResourceGroupName = "myTestRG" # Give a name tooyour new resource group.
$StorageAccountName = "azsblobcontainer" # Give a name tooyour new storage account. It must be lowercase!
$Location = "Local" # Choose "Local" as an example.
$ContainerName = "photo" # Give a name tooyour new container.
$ImageToUpload = "C:\temp\Hello.jpg" # Prepare an image file and a source directory in your local computer.
$DestinationFolder = "C:\temp\downlaod" # A destination directory in your local computer.

# Import hello Connect PowerShell module"
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
Import-Module .\Connect\AzureStack.Connect.psm1

# Configure hello PowerShell environment
# Register an AzureRM environment that targets your Azure Stack instance
Add-AzureRmEnvironment -Name $ARMEvnName -ARMEndpoint $ARMEndPoint 

# Set hello GraphEndpointResourceId value
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

# Download blobs from hello container:
# Get a reference tooa list of all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName

# Create hello destination directory.
New-Item -Path $DestinationFolder -ItemType Directory -Force  

# Download blobs into hello local destination directory.
$blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder

# end
```

### <a name="powershell-known-issues"></a><span data-ttu-id="7c8a5-157">Problemas conocidos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c8a5-157">PowerShell Known Issues</span></span> 
<span data-ttu-id="7c8a5-158">Hola actual compatible con Azure PowerShell versión del módulo para la pila de Azure es 1.2.10.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-158">hello current compatible Azure PowerShell module version for Azure Stack is 1.2.10.</span></span> <span data-ttu-id="7c8a5-159">Es diferente de la versión más reciente de Hola de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-159">It’s different from hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="7c8a5-160">La principal diferencia afecta al funcionamiento de los servicios de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="7c8a5-160">This difference impacts storage services operation:</span></span>

* <span data-ttu-id="7c8a5-161">formato de valor devuelto de Hola de `Get-AzureRmStorageAccountKey` en la versión 1.2.10 tiene dos propiedades: `Key1` y `Key2`, mientras que la versión de Azure actual Hola devuelve una matriz que contiene todas las claves de cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-161">hello return value format of `Get-AzureRmStorageAccountKey` in version 1.2.10 has two properties: `Key1` and `Key2`, while hello current Azure version returns an array containing all hello account keys.</span></span>
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
   <span data-ttu-id="7c8a5-162">Para más información, consulte [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).</span><span class="sxs-lookup"><span data-stu-id="7c8a5-162">For more information, see [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).</span></span>

## <a name="azure-cli"></a><span data-ttu-id="7c8a5-163">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="7c8a5-163">Azure CLI</span></span>
<span data-ttu-id="7c8a5-164">Hola CLI de Azure es la experiencia de línea de comandos de Azure para administrar recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-164">hello Azure CLI is Azure’s command-line experience for managing Azure resources.</span></span> <span data-ttu-id="7c8a5-165">Puede instalar en Windows, Linux y Mac OS y ejecútelo desde la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-165">You can install it on macOS, Linux, and Windows and run it from hello command line.</span></span> 

<span data-ttu-id="7c8a5-166">CLI de Azure está optimizado para administrar recursos de Azure desde la línea de comandos de Hola y para generar scripts de automatización que trabajan con hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-166">Azure CLI is optimized for managing and administering Azure resources from hello command line, and for building automation scripts that work against hello Azure Resource Manager.</span></span> <span data-ttu-id="7c8a5-167">Ofrece muchas Hola mismas funciones que se encuentra en el portal de Azure pila hello, incluido el acceso de datos enriquecidos.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-167">It provides many of hello same functions found in hello Azure Stack portal, including rich data access.</span></span>

<span data-ttu-id="7c8a5-168">Azure Stack requiere la versión 2.0 de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-168">Azure Stack requires Azure CLI version 2.0.</span></span> <span data-ttu-id="7c8a5-169">Para más información acerca de cómo instalar y Azure PowerShell con Azure Stack, consulte [Install and configure Azure Stack CLI](azure-stack-connect-cli.md) (Instalación y configuración de la CLI de Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="7c8a5-169">For more information about installing and configuring Azure CLI with Azure Stack, see [Install and configure Azure Stack CLI](azure-stack-connect-cli.md).</span></span> <span data-ttu-id="7c8a5-170">Para obtener más información acerca de cómo toouse hello Azure CLI 2.0 tooperform varias tareas trabajar con recursos de la cuenta de almacenamiento de la pila de Azure, consulte [Using hello CLI2.0 de Azure con el almacenamiento de Azure](../storage/storage-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="7c8a5-170">For more information about how toouse hello Azure CLI 2.0 tooperform several tasks working with resources in your Azure Stack Storage account, see [Using hello Azure CLI2.0 with Azure Storage](../storage/storage-azure-cli.md)</span></span>

### <a name="azure-cli-sample-script-for-azure-stack"></a><span data-ttu-id="7c8a5-171">Script de ejemplo de la CLI de Azure para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="7c8a5-171">Azure CLI sample script for Azure Stack</span></span> 
<span data-ttu-id="7c8a5-172">Cuando haya completado la instalación de CLI de Hola y configuración, puede intentar Hola siguiendo los pasos toowork con un toointeract de secuencia de comandos de shell pequeño ejemplo con los recursos de almacenamiento de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-172">Once you complete hello CLI installation and configuration, you can try hello following steps toowork with a small shell sample script toointeract with Azure Stack Storage resources.</span></span> <span data-ttu-id="7c8a5-173">script de Hola primero crea un nuevo contenedor en la cuenta de almacenamiento, a continuación, carga un contenedor existente de toothat de archivo (como un blob), enumera todos los blobs en el contenedor de Hola y por último, descarga tooa destino de archivo de hello en el equipo local que especifique.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-173">hello script first creates a new container in your storage account, then uploads an existing file (as a blob) toothat container, lists all blobs in hello container, and finally, downloads hello file tooa destination on your local computer that you specify.</span></span> <span data-ttu-id="7c8a5-174">Antes de ejecutar este script, asegúrese de que se haya conectado correctamente y de inicio de sesión toohello destino pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-174">Before you run this script, make sure you successfully connect and login toohello target Azure Stack.</span></span> 
1. <span data-ttu-id="7c8a5-175">Abra el editor de texto, a continuación, copie y pegue Hola anteponer la secuencia de comandos en el editor de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-175">Open your favorite text editor, then copy and paste hello preceding script into hello editor.</span></span>
2. <span data-ttu-id="7c8a5-176">Actualizar tooreflect de variables del script de Hola las opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-176">Update hello script's variables tooreflect your configuration settings.</span></span> 
3. <span data-ttu-id="7c8a5-177">Después de actualizar las variables necesarias de hello, Guardar script de Hola y salir del editor.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-177">After you've updated hello necessary variables, save hello script and exit your editor.</span></span> <span data-ttu-id="7c8a5-178">Hola siguiente da por sentado que ha denominado el my_storage_sample.sh de secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-178">hello next steps assume you've named your script my_storage_sample.sh.</span></span>
4. <span data-ttu-id="7c8a5-179">Marcar el script de Hola como archivo ejecutable, si es necesario:`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="7c8a5-179">Mark hello script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>
5. <span data-ttu-id="7c8a5-180">Ejecutar script de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-180">Execute hello script.</span></span> <span data-ttu-id="7c8a5-181">Por ejemplo, en Bash: `./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="7c8a5-181">For example, in Bash: `./my_storage_sample.sh`</span></span>

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

echo "Creating hello resource group..."
az group create --name $AZURESTACK_RESOURCE_GROUP --location $AZURESTACK_RG_LOCATION

echo "Creating hello storage account..."
az storage account create --name $AZURESTACK_STORAGE_ACCOUNT_NAME --resource-group $AZURESTACK_RESOURCE_GROUP --account-type Standard_LRS

echo "Creating hello blob container..."
az storage container create --name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Uploading hello file..."
az storage blob upload --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --file $FILE_TO_UPLOAD --name $AZURESTACK_STORAGE_BLOB_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Listing hello blobs..."
az storage blob list --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --output table

echo "Downloading hello file..."
az storage blob download --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --name $AZURESTACK_STORAGE_BLOB_NAME --file $DESTINATION_FILE --output table

echo "Done"
```

## <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="7c8a5-182">Explorador de almacenamiento de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="7c8a5-182">Microsoft Azure Storage Explorer</span></span>

<span data-ttu-id="7c8a5-183">El Explorador de Microsoft Azure Storage es una aplicación independiente de Microsoft</span><span class="sxs-lookup"><span data-stu-id="7c8a5-183">Microsoft Azure Storage Explorer is a standalone app from Microsoft.</span></span> <span data-ttu-id="7c8a5-184">Permite trabajar de tooeasily con datos de almacenamiento de Azure y Azure pila de almacenamiento en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-184">It allows you tooeasily work with both Azure Storage and Azure Stack Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="7c8a5-185">Si desea un toomanage fácilmente los datos de almacenamiento de la pila de Azure, considere la posibilidad de mediante el Explorador de almacenamiento de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8a5-185">If you want an easy way toomanage your Azure Stack Storage data, then consider using Microsoft Azure Storage Explorer.</span></span>

<span data-ttu-id="7c8a5-186">Para obtener más información acerca de cómo configurar Azure Storage Explorer toowork con la pila de Azure, consulte [conectar Explorador de almacenamiento tooan suscripción de Azure pila](azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="7c8a5-186">For more information about configuring Azure Storage Explorer toowork with Azure Stack, see [Connect Storage Explorer tooan Azure Stack subscription](azure-stack-storage-connect-se.md).</span></span>

<span data-ttu-id="7c8a5-187">Para más información acerca del Explorador de Microsoft Azure Storage, consulte [Introducción al Explorador de Storage (versión preliminar)](../vs-azure-tools-storage-manage-with-storage-explorer.md)</span><span class="sxs-lookup"><span data-stu-id="7c8a5-187">For more information about Microsoft Azure Storage Explorer, see [Get started with Storage Explorer (Preview)](../vs-azure-tools-storage-manage-with-storage-explorer.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c8a5-188">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7c8a5-188">Next steps</span></span>
* [<span data-ttu-id="7c8a5-189">Conectar Explorador de almacenamiento tooan Azure pila suscripción</span><span class="sxs-lookup"><span data-stu-id="7c8a5-189">Connect Storage Explorer tooan Azure Stack subscription</span></span>](azure-stack-storage-connect-se.md)
* [<span data-ttu-id="7c8a5-190">Introducción al Explorador de Storage (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="7c8a5-190">Get started with Storage Explorer (Preview)</span></span>](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* <span data-ttu-id="7c8a5-191">[Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md) (Azure Stack Storage: diferencias y consideraciones)</span><span class="sxs-lookup"><span data-stu-id="7c8a5-191">[Azure-consistent storage: differences and considerations](azure-stack-acs-differences.md)</span></span>
* [<span data-ttu-id="7c8a5-192">Introducción tooMicrosoft almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="7c8a5-192">Introduction tooMicrosoft Azure Storage</span></span>](../storage/common/storage-introduction.md)

