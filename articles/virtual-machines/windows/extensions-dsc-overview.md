---
title: "Introducción a la configuración de estado deseado de Azure | Microsoft Docs"
description: "Información general para usar el controlador de extensiones de Microsoft Azure en la Configuración de estado deseado de PowerShell. Incluidos los requisitos previos, arquitectura, cmdlets, etc."
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: c05c2d541a5f526f362f9cd72fe6d878374112b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-the-azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="cee35-104">Introducción al controlador de extensiones de configuración de estado deseado de Azure</span><span class="sxs-lookup"><span data-stu-id="cee35-104">Introduction to the Azure Desired State Configuration extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="cee35-105">El agente de máquina virtual de Azure y las extensiones asociadas forman parte de los servicios de infraestructura de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cee35-105">The Azure VM Agent and associated Extensions are part of the Microsoft Azure Infrastructure Services.</span></span> <span data-ttu-id="cee35-106">Las extensiones de máquina virtual son componentes de software que amplían la funcionalidad de la máquina virtual y simplifican diversas operaciones de administración de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="cee35-106">VM Extensions are software components that extend the VM functionality and simplify various VM management operations.</span></span> <span data-ttu-id="cee35-107">Por ejemplo, puede utilizar la extensión VMAccess para restablecer una contraseña de administrador o la extensión de script personalizado para ejecutar un script en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cee35-107">For example, the VMAccess extension can be used to reset an administrator's password, or the Custom Script extension can be used to execute a script on the VM.</span></span>

<span data-ttu-id="cee35-108">Este artículo presenta la extensión de configuración de estado deseado (DSC) de PowerShell para las máquinas virtuales de Azure como parte del SDK de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cee35-108">This article introduces the PowerShell Desired State Configuration (DSC) Extension for Azure VMs as part of the Azure PowerShell SDK.</span></span> <span data-ttu-id="cee35-109">Puede usar cmdlets nuevos para cargar y aplicar una configuración de DSC de PowerShell en una máquina virtual de Azure habilitada con la extensión DSC de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cee35-109">You can use new cmdlets to upload and apply a PowerShell DSC configuration on an Azure VM enabled with the PowerShell DSC extension.</span></span> <span data-ttu-id="cee35-110">La extensión DSC de PowerShell llama a DSC de PowerShell para aplicar la configuración de DSC recibida en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cee35-110">The PowerShell DSC extension calls into PowerShell DSC to enact the received DSC configuration on the VM.</span></span> <span data-ttu-id="cee35-111">Esta funcionalidad también está disponible a través del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="cee35-111">This functionality is also available through the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cee35-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cee35-112">Prerequisites</span></span>
<span data-ttu-id="cee35-113">**Máquina local** Para interactuar con la extensión de máquina virtual de Azure, será necesario usar Azure Portal o el SDK de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cee35-113">**Local machine** To interact with the Azure VM extension, you need to use either the Azure portal or the Azure PowerShell SDK.</span></span> 

<span data-ttu-id="cee35-114">**Agente invitado** Es preciso que la máquina virtual de Azure afectada por la configuración del DSC tenga un SO que admita Windows Management Framework (WMF) 4.0 o 5.0.</span><span class="sxs-lookup"><span data-stu-id="cee35-114">**Guest Agent** The Azure VM that is configured by the DSC configuration needs to be an OS that supports either Windows Management Framework (WMF) 4.0 or 5.0.</span></span> <span data-ttu-id="cee35-115">La lista completa de las versiones compatibles del SO puede encontrarse en [Release history for the Azure DSC Extension](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/)(Historial de versiones de la extensión DSC de Azure).</span><span class="sxs-lookup"><span data-stu-id="cee35-115">The full list of supported OS versions can be found at the [DSC Extension Version History](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span></span>

## <a name="terms-and-concepts"></a><span data-ttu-id="cee35-116">Términos y conceptos</span><span class="sxs-lookup"><span data-stu-id="cee35-116">Terms and concepts</span></span>
<span data-ttu-id="cee35-117">Esta guía presupone que está familiarizado con los conceptos siguientes:</span><span class="sxs-lookup"><span data-stu-id="cee35-117">This guide presumes familiarity with the following concepts:</span></span>

<span data-ttu-id="cee35-118">Configuración: un documento de configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="cee35-118">Configuration - A DSC configuration document.</span></span> 

<span data-ttu-id="cee35-119">Nodo: un destino para una configuración de DSC.</span><span class="sxs-lookup"><span data-stu-id="cee35-119">Node - A target for a DSC configuration.</span></span> <span data-ttu-id="cee35-120">En este documento, "nodo" siempre hace referencia a una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="cee35-120">In this document, "node" always refers to an Azure VM.</span></span>

<span data-ttu-id="cee35-121">Datos de configuración: un archivo .psd1 que contiene datos del entorno de una configuración</span><span class="sxs-lookup"><span data-stu-id="cee35-121">Configuration Data - A .psd1 file containing environmental data for a configuration</span></span>

## <a name="architectural-overview"></a><span data-ttu-id="cee35-122">Información general acerca de la arquitectura</span><span class="sxs-lookup"><span data-stu-id="cee35-122">Architectural overview</span></span>
<span data-ttu-id="cee35-123">La extensión DSC de Azure usa el marco del agente de máquina virtual de Azure para entregar y aplicar las configuraciones de DSC que se ejecutan en las máquinas virtuales de Azure, así como informar sobre estas.</span><span class="sxs-lookup"><span data-stu-id="cee35-123">The Azure DSC extension uses the Azure VM Agent framework to deliver, enact, and report on DSC configurations running on Azure VMs.</span></span> <span data-ttu-id="cee35-124">La extensión DSC espera un archivo .zip que contiene al menos un documento de configuración y un conjunto de parámetros proporcionados a través del SDK de Azure PowerShell o del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="cee35-124">The DSC extension expects a .zip file containing at least a configuration document, and a set of parameters provided either through the Azure PowerShell SDK or through the Azure portal.</span></span>

<span data-ttu-id="cee35-125">La primera vez que se llama a la extensión, se ejecuta un proceso de instalación.</span><span class="sxs-lookup"><span data-stu-id="cee35-125">When the extension is called for the first time, it runs an installation process.</span></span> <span data-ttu-id="cee35-126">Dicho proceso instala una versión de Windows Management Framework (WMF) usando la siguiente lógica:</span><span class="sxs-lookup"><span data-stu-id="cee35-126">This process installs a version of the Windows Management Framework (WMF) using the following logic:</span></span>

1. <span data-ttu-id="cee35-127">Si el SO de la máquina virtual de Azure es Windows Server 2016, no se realiza ninguna acción.</span><span class="sxs-lookup"><span data-stu-id="cee35-127">If the Azure VM OS is Windows Server 2016, no action is taken.</span></span> <span data-ttu-id="cee35-128">Windows Server 2016 ya tiene instalada la versión más reciente de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cee35-128">Windows Server 2016 already has the latest version of PowerShell installed.</span></span>
2. <span data-ttu-id="cee35-129">Si está especificada la propiedad `wmfVersion` , se instala esta versión de WMF, salvo que sea incompatible con el SO de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cee35-129">If the `wmfVersion` property is specified, that version of the WMF is installed unless it is incompatible with the VM's OS.</span></span>
3. <span data-ttu-id="cee35-130">Si no hay ninguna propiedad `wmfVersion` especificada, se instala la versión aplicable más reciente de WMF.</span><span class="sxs-lookup"><span data-stu-id="cee35-130">If no `wmfVersion` property is specified, the latest applicable version of the WMF is installed.</span></span>

<span data-ttu-id="cee35-131">La instalación de WMF requiere un reinicio.</span><span class="sxs-lookup"><span data-stu-id="cee35-131">Installation of the WMF requires a reboot.</span></span> <span data-ttu-id="cee35-132">Después del reinicio, la extensión descarga el archivo .zip especificado en la propiedad `modulesUrl` .</span><span class="sxs-lookup"><span data-stu-id="cee35-132">After reboot, the extension downloads the .zip file specified in the `modulesUrl` property.</span></span> <span data-ttu-id="cee35-133">Si esta ubicación se encuentra en Almacenamiento de blobs de Azure, se puede especificar un token de SAS en la propiedad `sasToken` para acceder al archivo.</span><span class="sxs-lookup"><span data-stu-id="cee35-133">If this location is in Azure blob storage, a SAS token can be specified in the `sasToken` property to access the file.</span></span> <span data-ttu-id="cee35-134">Después de que el archivo .zip se descargue y descomprima, se ejecuta la función de configuración definida en `configurationFunction` para generar el archivo MOF.</span><span class="sxs-lookup"><span data-stu-id="cee35-134">After the .zip is downloaded and unpacked, the configuration function defined in `configurationFunction` is run to generate the MOF file.</span></span> <span data-ttu-id="cee35-135">Luego, la extensión ejecuta `Start-DscConfiguration -Force` en el archivo MOF generado.</span><span class="sxs-lookup"><span data-stu-id="cee35-135">The extension then runs `Start-DscConfiguration -Force` on the generated MOF file.</span></span> <span data-ttu-id="cee35-136">La extensión de captura de salida y la escribe de nuevo en el canal de estado de Azure.</span><span class="sxs-lookup"><span data-stu-id="cee35-136">The extension captures output and writes it back out to the Azure Status Channel.</span></span> <span data-ttu-id="cee35-137">A partir de ese momento, el LCM de DSC controla la supervisión y la corrección de la forma habitual.</span><span class="sxs-lookup"><span data-stu-id="cee35-137">From this point on, the DSC LCM handles monitoring and correction as normal.</span></span> 

## <a name="powershell-cmdlets"></a><span data-ttu-id="cee35-138">Cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="cee35-138">PowerShell cmdlets</span></span>
<span data-ttu-id="cee35-139">Los cmdlets de PowerShell se pueden utilizar con Azure Resource Manager o el modelo de implementación clásica para empaquetar, publicar y supervisar las implementaciones de la extensión DSC.</span><span class="sxs-lookup"><span data-stu-id="cee35-139">PowerShell cmdlets can be used with Azure Resource Manager or the classic deployment model to package, publish, and monitor DSC extension deployments.</span></span> <span data-ttu-id="cee35-140">Los siguientes cmdlets enumerados son los módulos de implementación clásica, pero "Azure" se puede reemplazar por "AzureRm" para utilizar el modelo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cee35-140">The following cmdlets listed are the classic deployment modules, but "Azure" can be replaced with "AzureRm" to use the Azure Resource Manager model.</span></span> <span data-ttu-id="cee35-141">Por ejemplo, `Publish-AzureVMDscConfiguration` utiliza el modelo de implementación clásica, donde `Publish-AzureRmVMDscConfiguration` usa Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cee35-141">For example,  `Publish-AzureVMDscConfiguration` uses the classic deployment model, where `Publish-AzureRmVMDscConfiguration` uses Azure Resource Manager.</span></span> 

<span data-ttu-id="cee35-142">`Publish-AzureVMDscConfiguration` toma un archivo de configuración, lo examina en busca de recursos de DSC dependientes y crea un archivo .zip que contiene la configuración y los recursos de DSC necesarios para aplicar la configuración.</span><span class="sxs-lookup"><span data-stu-id="cee35-142">`Publish-AzureVMDscConfiguration` takes in a configuration file, scans it for dependent DSC resources, and creates a .zip file containing the configuration and DSC resources needed to enact the configuration.</span></span> <span data-ttu-id="cee35-143">Puede crear también el paquete localmente mediante el parámetro `-ConfigurationArchivePath` .</span><span class="sxs-lookup"><span data-stu-id="cee35-143">It can also create the package locally using the `-ConfigurationArchivePath` parameter.</span></span> <span data-ttu-id="cee35-144">En caso contrario, publica el archivo .zip en Azure Blob Storage y lo protege con un token de SAS.</span><span class="sxs-lookup"><span data-stu-id="cee35-144">Otherwise, it publishes the .zip file to Azure blob storage and secures it with a SAS token.</span></span>

<span data-ttu-id="cee35-145">El archivo .zip que crea este cmdlet tiene el script de configuración. ps1 en la raíz de la carpeta de archivos.</span><span class="sxs-lookup"><span data-stu-id="cee35-145">The .zip file created by this cmdlet has the .ps1 configuration script at the root of the archive folder.</span></span> <span data-ttu-id="cee35-146">Los recursos tienen la carpeta del módulo colocada en la carpeta de archivos.</span><span class="sxs-lookup"><span data-stu-id="cee35-146">Resources have the module folder placed in the archive folder.</span></span> 

<span data-ttu-id="cee35-147">`Set-AzureVMDscExtension` inserta la configuración que necesita la extensión DSC de PowerShell en un objeto de configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cee35-147">`Set-AzureVMDscExtension` injects the settings needed by the PowerShell DSC extension into a VM configuration object.</span></span> <span data-ttu-id="cee35-148">En el modelo de implementación clásica, deben aplicarse los cambios de la máquina virtual a una máquina virtual de Azure con `Update-AzureVM`.</span><span class="sxs-lookup"><span data-stu-id="cee35-148">In the classic deployment model, the VM changes must be applied to an Azure VM with `Update-AzureVM`.</span></span> 

<span data-ttu-id="cee35-149">`Get-AzureVMDscExtension` recupera el estado de la extensión DSC de una máquina virtual concreta.</span><span class="sxs-lookup"><span data-stu-id="cee35-149">`Get-AzureVMDscExtension` retrieves the DSC extension status of a particular VM.</span></span> 

<span data-ttu-id="cee35-150">`Get-AzureVMDscExtensionStatus` recupera el estado de la configuración de DSC aplicada por el controlador de extensiones DSC.</span><span class="sxs-lookup"><span data-stu-id="cee35-150">`Get-AzureVMDscExtensionStatus` retrieves the status of the DSC configuration enacted by the DSC extension handler.</span></span> <span data-ttu-id="cee35-151">Esta acción puede realizarse en una sola máquina virtual o en un grupo de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="cee35-151">This action can be performed on a single VM, or group of VMs.</span></span>

<span data-ttu-id="cee35-152">`Remove-AzureVMDscExtension` quita el controlador de extensiones de una máquina virtual dada.</span><span class="sxs-lookup"><span data-stu-id="cee35-152">`Remove-AzureVMDscExtension` removes the extension handler from a given virtual machine.</span></span> <span data-ttu-id="cee35-153">Este cmdlet **no** quita la configuración, ni desinstala WMF ni cambia la configuración aplicada en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cee35-153">This cmdlet does **not** remove the configuration, uninstall the WMF, or change the applied settings on the virtual machine.</span></span> <span data-ttu-id="cee35-154">Solo quita el controlador de extensiones.</span><span class="sxs-lookup"><span data-stu-id="cee35-154">It only removes the extension handler.</span></span> 

<span data-ttu-id="cee35-155">**Principales diferencias clave en los cmdlets de ASM y Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="cee35-155">**Key differences in ASM and Azure Resource Manager cmdlets**</span></span>

* <span data-ttu-id="cee35-156">Los cmdlets de Azure Resource Manager son sincrónicos.</span><span class="sxs-lookup"><span data-stu-id="cee35-156">Azure Resource Manager cmdlets are synchronous.</span></span> <span data-ttu-id="cee35-157">Los cmdlets de ASM son asincrónicos.</span><span class="sxs-lookup"><span data-stu-id="cee35-157">ASM cmdlets are asynchronous.</span></span>
* <span data-ttu-id="cee35-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version y Location son todos parámetros necesarios en Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cee35-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version, and Location are all required parameters in Azure Resource Manager.</span></span>
* <span data-ttu-id="cee35-159">ArchiveResourceGroupName es un nuevo parámetro opcional de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cee35-159">ArchiveResourceGroupName is a new optional parameter for Azure Resource Manager.</span></span> <span data-ttu-id="cee35-160">Se puede especificar este parámetro cuando la cuenta de almacenamiento pertenezca a un grupo de recursos que no sea el mismo que en el que se crea la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cee35-160">You can specify this parameter when your storage account belongs to a different resource group than the one where the virtual machine is created.</span></span>
* <span data-ttu-id="cee35-161">ConfigurationArchive se denomina ArchiveBlobName en Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cee35-161">ConfigurationArchive is called ArchiveBlobName in Azure Resource Manager</span></span>
* <span data-ttu-id="cee35-162">ContainerName se denomina ArchiveContainerName en Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cee35-162">ContainerName is called ArchiveContainerName in Azure Resource Manager</span></span>
* <span data-ttu-id="cee35-163">StorageEndpointSuffix se denomina ArchiveStorageEndpointSuffix en Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cee35-163">StorageEndpointSuffix is called ArchiveStorageEndpointSuffix in Azure Resource Manager</span></span>
* <span data-ttu-id="cee35-164">El modificador AutoUpdate se ha agregado a Azure Resource Manager para habilitar la actualización automática del controlador de extensiones a la versión más reciente cuando esté disponible, y tal como esté disponible.</span><span class="sxs-lookup"><span data-stu-id="cee35-164">The AutoUpdate switch has been added to Azure Resource Manager to enable automatic updating of the extension handler to the latest version as and when it is available.</span></span> <span data-ttu-id="cee35-165">Tenga en cuenta que este parámetro puede provocar que la máquina virtual se reinicie cuando se lance una nueva versión de WMF.</span><span class="sxs-lookup"><span data-stu-id="cee35-165">Note this parameter has the potential to cause reboots on the VM when a new version of the WMF is released.</span></span> 

## <a name="azure-portal-functionality"></a><span data-ttu-id="cee35-166">Funcionalidad del Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cee35-166">Azure portal functionality</span></span>
<span data-ttu-id="cee35-167">Vaya a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cee35-167">Browse to a VM.</span></span> <span data-ttu-id="cee35-168">En Configuración -> General, haga clic en "Extensiones".</span><span class="sxs-lookup"><span data-stu-id="cee35-168">Under Settings -> General click "Extensions."</span></span> <span data-ttu-id="cee35-169">Se crea un nuevo panel.</span><span class="sxs-lookup"><span data-stu-id="cee35-169">A new pane is created.</span></span> <span data-ttu-id="cee35-170">Haga clic en "Agregar" y seleccione DSC de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cee35-170">Click "Add" and select PowerShell DSC.</span></span>

<span data-ttu-id="cee35-171">El portal necesita una entrada.</span><span class="sxs-lookup"><span data-stu-id="cee35-171">The portal needs input.</span></span>
<span data-ttu-id="cee35-172">**Script o módulos de configuración**: este campo es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="cee35-172">**Configuration Modules or Script**: This field is mandatory.</span></span> <span data-ttu-id="cee35-173">Requiere un archivo .ps1 que contenga un script de configuración o un archivo .zip con un script de configuración .ps1 en la raíz y todos los recursos dependientes en las carpetas de módulos dentro del archivo .zip.</span><span class="sxs-lookup"><span data-stu-id="cee35-173">Requires a .ps1 file containing a configuration script, or a .zip file with a .ps1 configuration script at the root, and all dependent resources in module folders within the .zip.</span></span> <span data-ttu-id="cee35-174">Se puede crear con el cmdlet `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` que se incluye en el SDK de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cee35-174">It can be created with the `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet included in the Azure PowerShell SDK.</span></span> <span data-ttu-id="cee35-175">El archivo .zip se carga en el almacenamiento de blobs de usuario protegido por un token de SAS.</span><span class="sxs-lookup"><span data-stu-id="cee35-175">The .zip file is uploaded into your user blob storage secured by a SAS token.</span></span> 

<span data-ttu-id="cee35-176">**Archivo PSD1 de datos de configuración**: este campo es opcional.</span><span class="sxs-lookup"><span data-stu-id="cee35-176">**Configuration Data PSD1 File**: This field is optional.</span></span> <span data-ttu-id="cee35-177">Si la configuración requiere un archivo de datos de configuración en .psd1, utilice este campo para seleccionarlo y cargarlo en el almacenamiento de blobs de usuario, donde está protegido por un token de SAS.</span><span class="sxs-lookup"><span data-stu-id="cee35-177">If your configuration requires a configuration data file in .psd1, use this field to select it and upload it to your user blob storage, where it is secured by a SAS token.</span></span> 

<span data-ttu-id="cee35-178">**Nombre completo del módulo de configuración**: los archivos .ps1 pueden tener varias funciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="cee35-178">**Module-Qualified Name of Configuration**: .ps1 files can have multiple configuration functions.</span></span> <span data-ttu-id="cee35-179">Escriba el nombre del script .ps1 de configuración seguido de un '\'' y el nombre de la función de configuración.</span><span class="sxs-lookup"><span data-stu-id="cee35-179">Enter the name of the configuration .ps1 script followed by a  '\' and the name of the configuration function.</span></span> <span data-ttu-id="cee35-180">Por ejemplo, si su script .ps1 tiene el nombre "configuration.ps1" y la configuración es "IisInstall", escriba: `configuration.ps1\IisInstall`</span><span class="sxs-lookup"><span data-stu-id="cee35-180">For example, if your .ps1 script has the name "configuration.ps1", and the configuration is "IisInstall", you would enter: `configuration.ps1\IisInstall`</span></span>

<span data-ttu-id="cee35-181">**Argumentos de configuración**: si la función de configuración adopta argumentos, escríbalos aquí con el formato `argumentName1=value1,argumentName2=value2`.</span><span class="sxs-lookup"><span data-stu-id="cee35-181">**Configuration Arguments**: If the configuration function takes arguments, enter them in here in the format `argumentName1=value1,argumentName2=value2`.</span></span> <span data-ttu-id="cee35-182">Tenga en cuenta que se trata de un formato distinto a cómo se aceptan argumentos de configuración a través de los cmdlets de PowerShell o las plantillas de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cee35-182">Note this format is a different format than how configuration arguments are accepted through PowerShell cmdlets or Resource Manager templates.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="cee35-183">Introducción</span><span class="sxs-lookup"><span data-stu-id="cee35-183">Getting started</span></span>
<span data-ttu-id="cee35-184">La extensión DSC de Azure toma documentos de configuración de DSC y los aplica a máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="cee35-184">The Azure DSC extension takes in DSC configuration documents and enacts them on Azure VMs.</span></span> <span data-ttu-id="cee35-185">A continuación encontrará un ejemplo sencillo de una configuración.</span><span class="sxs-lookup"><span data-stu-id="cee35-185">A simple example of a configuration follows.</span></span> <span data-ttu-id="cee35-186">Guárdelo localmente como "IisInstall.ps1":</span><span class="sxs-lookup"><span data-stu-id="cee35-186">Save it locally as "IisInstall.ps1":</span></span>

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

<span data-ttu-id="cee35-187">Los siguientes pasos colocan el script IisInstall.ps1 en la máquina virtual especificada, ejecutan la configuración y devuelven información acerca del estado.</span><span class="sxs-lookup"><span data-stu-id="cee35-187">The following steps place the IisInstall.ps1 script on the specified VM, execute the configuration, and report back on status.</span></span>
###<a name="classic-model"></a><span data-ttu-id="cee35-188">Modelo clásico</span><span class="sxs-lookup"><span data-stu-id="cee35-188">Classic model</span></span>
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish the configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set the VM to run the DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update the configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a><span data-ttu-id="cee35-189">Modelo de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cee35-189">Azure Resource Manager model</span></span>

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish the configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set the VM to run the DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a><span data-ttu-id="cee35-190">Registro</span><span class="sxs-lookup"><span data-stu-id="cee35-190">Logging</span></span>
<span data-ttu-id="cee35-191">Los registros se colocan en:</span><span class="sxs-lookup"><span data-stu-id="cee35-191">Logs are placed in:</span></span>

<span data-ttu-id="cee35-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[número de versión]</span><span class="sxs-lookup"><span data-stu-id="cee35-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Version Number]</span></span>

## <a name="next-steps"></a><span data-ttu-id="cee35-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cee35-193">Next steps</span></span>
<span data-ttu-id="cee35-194">Para más información sobre DSC de PowerShell, [visite el centro de documentación de PowerShell](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="cee35-194">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="cee35-195">Examine la [plantilla de Azure Resource Manager para la extensión de DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cee35-195">Examine the [Azure Resource Manager template for the DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="cee35-196">Para buscar otras funcionalidades que se puedan administrar con DSC de PowerShell, [examine la Galería de PowerShell](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) para encontrar más recursos de DSC.</span><span class="sxs-lookup"><span data-stu-id="cee35-196">To find additional functionality you can manage with PowerShell DSC, [browse the PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

<span data-ttu-id="cee35-197">Para más información sobre cómo pasar parámetros confidenciales a configuraciones, consulte [Cómo pasar las credenciales al controlador de extensiones de la DSC de Azure](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cee35-197">For details on passing sensitive parameters into configurations, see [Manage credentials securely with the DSC extension handler](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

