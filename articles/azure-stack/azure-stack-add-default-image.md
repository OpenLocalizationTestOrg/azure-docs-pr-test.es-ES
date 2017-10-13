---
title: "Agregación de la imagen de máquina virtual predeterminada en Marketplace de Azure Stack | Microsoft Docs"
description: "Agregue la imagen predeterminada de máquina virtual Windows Server 2016 en Marketplace de Azure Stack."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 43781cb025865df1d228376f57412f3d482d3ad0
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2017
---
# <a name="add-the-windows-server-2016-vm-image-to-the-azure-stack-marketplace"></a><span data-ttu-id="5131d-103">Agregación de la imagen de máquina virtual Windows Server 2016 en Marketplace de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5131d-103">Add the Windows Server 2016 VM image to the Azure Stack marketplace</span></span>

<span data-ttu-id="5131d-104">De forma predeterminada, no hay ninguna imagen de máquina virtual disponible en Marketplace de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5131d-104">By default, there aren’t any virtual machine images available in the Azure Stack marketplace.</span></span> <span data-ttu-id="5131d-105">El operador de Azure Stack debe agregar una imagen en Marketplace antes de que los usuarios puedan usarla.</span><span class="sxs-lookup"><span data-stu-id="5131d-105">The Azure Stack operator must add an image to the marketplace before users can use them.</span></span> <span data-ttu-id="5131d-106">Puede agregar la imagen de Windows Server 2016 en Marketplace de Azure Stack mediante uno de los dos métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5131d-106">You can add the Windows Server 2016 image to the Azure Stack marketplace by using one of the following two methods:</span></span>

* <span data-ttu-id="5131d-107">[Agregar la imagen mediante la descarga desde Azure Marketplace](#add-the-image-by-downloading-it-from-the-Azure-marketplace): utilice esta opción si está trabajando en un escenario conectado y ha registrado la instancia de Azure Stack en Azure.</span><span class="sxs-lookup"><span data-stu-id="5131d-107">[Add the image by downloading it from the Azure Marketplace](#add-the-image-by-downloading-it-from-the-Azure-marketplace) - Use this option if you are operating in a connected scenario and if you have registered your Azure Stack instance with Azure.</span></span>

* <span data-ttu-id="5131d-108">[Agregar la imagen mediante el uso de PowerShell](#add-the-image-by-using-powershell): utilice esta opción si ha implementado Azure Stack en un escenario sin conexión o en escenarios con conectividad limitada.</span><span class="sxs-lookup"><span data-stu-id="5131d-108">[Add the image by using PowerShell](#add-the-image-by-using-powershell) - Use this option if you have deployed Azure Stack in a disconnected scenario or in scenarios with limited connectivity.</span></span>

## <a name="add-the-image-by-downloading-it-from-the-azure-marketplace"></a><span data-ttu-id="5131d-109">Agregación de la imagen mediante la descarga de Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="5131d-109">Add the image by downloading it from the Azure Marketplace</span></span>

1. <span data-ttu-id="5131d-110">Después de implementar Azure Stack, inicie sesión en Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="5131d-110">After deploying Azure Stack, sign in to your Azure Stack Development Kit.</span></span>

2. <span data-ttu-id="5131d-111">Haga clic en **Más servicios** > **Marketplace Management** (Administración de Marketplace)  > **Add from Azure** (Agregar desde Azure).</span><span class="sxs-lookup"><span data-stu-id="5131d-111">click **More services** > **Marketplace Management** > **Add from Azure**</span></span> 

3. <span data-ttu-id="5131d-112">Busque la imagen **Windows Server 2016 Datacenter – Eval** > haga clic en **Descargar**</span><span class="sxs-lookup"><span data-stu-id="5131d-112">Find or search for the **Windows Server 2016 Datacenter – Eval** image > click **Download**</span></span>

   ![Descarga de la imagen desde Azure](media/azure-stack-add-default-image/download-image.png)

<span data-ttu-id="5131d-114">Una vez finalizada la descarga, la imagen se agrega a la hoja **Marketplace Management** y se pone a disposición desde la hoja **Máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="5131d-114">After the download completes, the image is added to the **Marketplace Management** blade and it is also made available from the **Virtual Machines** blade.</span></span>

## <a name="add-the-image-by-using-powershell"></a><span data-ttu-id="5131d-115">Agregación de la imagen mediante el uso de PowerShell</span><span class="sxs-lookup"><span data-stu-id="5131d-115">Add the image by using PowerShell</span></span>

### <a name="prerequisites"></a><span data-ttu-id="5131d-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5131d-116">Prerequisites</span></span> 

<span data-ttu-id="5131d-117">Implemente los siguientes requisitos previos desde el [kit de desarrollo](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) o desde un cliente externo basado en Windows, si está [conectado a través de VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="5131d-117">Run the following prerequisites either from the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="5131d-118">Instale los [módulos de Azure PowerShell compatibles con Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="5131d-118">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  

* <span data-ttu-id="5131d-119">Descargue las [herramientas necesarias para trabajar con Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="5131d-119">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span>  

* <span data-ttu-id="5131d-120">Vaya a https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 y descargue la evaluación de Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="5131d-120">Go to https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 and download the Windows Server 2016 evaluation.</span></span> <span data-ttu-id="5131d-121">Cuando se le solicite, seleccione la versión **ISO** de la descarga.</span><span class="sxs-lookup"><span data-stu-id="5131d-121">When prompted, select the **ISO** version of the download.</span></span> <span data-ttu-id="5131d-122">Tome nota de la ruta de acceso a la ubicación de la descarga, que se utilizará más adelante en estos pasos.</span><span class="sxs-lookup"><span data-stu-id="5131d-122">Record the path to the download location, which is used later in these steps.</span></span> <span data-ttu-id="5131d-123">Este paso requiere conectividad a Internet.</span><span class="sxs-lookup"><span data-stu-id="5131d-123">This step requires internet connectivity.</span></span>  

<span data-ttu-id="5131d-124">Ahora, ejecute los pasos siguientes para agregar la imagen en Marketplace de Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="5131d-124">Now run the following steps to add the image to the Azure Stack marketplace:</span></span>
   
1. <span data-ttu-id="5131d-125">Importe los módulos Connect y ComputeAdmin de Azure Stack mediante los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5131d-125">Import the Azure Stack Connect and ComputeAdmin modules by using the following commands:</span></span>

   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import the Connect and ComputeAdmin modules   
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1

   ```

2. <span data-ttu-id="5131d-126">Inicie sesión en el entorno de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5131d-126">Sign in to your Azure Stack environment.</span></span> <span data-ttu-id="5131d-127">Ejecute el siguiente script en función de si su entorno de Azure Stack se implementó mediante el uso de AAD o AD FS (asegúrese de reemplazar los valores de tenantName, GraphAudience endpoint y ArmEndpoint de AAD según la configuración de su entorno):</span><span class="sxs-lookup"><span data-stu-id="5131d-127">Run the following script depending on if your Azure Stack environment is deployed by using AAD or AD FS (Make sure to replace the AAD tenantName, GraphAudience endpoint and ArmEndpoint values as per your environment configuration):</span></span>  

   <span data-ttu-id="5131d-128">a.</span><span class="sxs-lookup"><span data-stu-id="5131d-128">a.</span></span> <span data-ttu-id="5131d-129">**Azure Active Directory**, use el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5131d-129">**Azure Active Directory**, use the following cmdlet:</span></span>

   ```PowerShell
   # For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external. To get this value for Azure Stack integrated systems, contact your service provider.
   $ArmEndpoint = "<Resource Manager endpoint for your environment>"

   # For Azure Stack development kit, this value is set to https://graph.windows.net/. To get this value for Azure Stack integrated systems, contact your service provider.
   $GraphAudience = "<GraphAuidence endpoint for your environment>"
   
   # Create the Azure Stack operator's AzureRM environment by using the following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint $ArmEndpoint

   Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience $GraphAudience

   $TenantID = Get-AzsDirectoryTenantId `
     -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
     -EnvironmentName AzureStackAdmin

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```

   <span data-ttu-id="5131d-130">b.</span><span class="sxs-lookup"><span data-stu-id="5131d-130">b.</span></span> <span data-ttu-id="5131d-131">**Servicios de federación de Active Directory**, use el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5131d-131">**Active Directory Federation Services**, use the following cmdlet:</span></span>
    
   ```PowerShell
   # For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external. To get this value for Azure Stack integrated systems, contact your service provider.
   $ArmEndpoint = "<Resource Manager endpoint for your environment>"

   # For Azure Stack development kit, this value is set to https://graph.local.azurestack.external/. To get this value for Azure Stack integrated systems, contact your service provider.
   $GraphAudience = "<GraphAuidence endpoint for your environment>"

   # Create the Azure Stack operator's AzureRM environment by using the following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint $ArmEndpoint

   Set-AzureRmEnvironment `
     -Name "AzureStackAdmin" `
     -GraphAudience $GraphAudience `
     -EnableAdfsAuthentication:$true

   $TenantID = Get-AzsDirectoryTenantId `
     -ADFS 
     -EnvironmentName AzureStackAdmin 

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```
   
3. <span data-ttu-id="5131d-132">Agregar la imagen de Windows Server 2016 en Marketplace de Azure Stack (asegúrese de reemplazar la *Ruta_de_acceso_a_ISO* por la ruta de acceso al archivo ISO WS2016 que descargó):</span><span class="sxs-lookup"><span data-stu-id="5131d-132">Add the Windows Server 2016 image to the Azure Stack marketplace (Make sure to replace the *Path_to_ISO* with the path to the WS2016 ISO you downloaded):</span></span>

   ```PowerShell
   $ISOPath = "<Fully_Qualified_Path_to_ISO>"

   # Add a Windows Server 2016 Evaluation VM Image.
   New-AzsServer2016VMImage `
     -ISOPath $ISOPath

   ```

<span data-ttu-id="5131d-133">Para asegurarse de que la imagen de máquina virtual Windows Server 2016 tiene la actualización acumulativa más reciente, incluya el parámetro `IncludeLatestCU` al ejecutar el cmdlet `New-AzsServer2016VMImage`.</span><span class="sxs-lookup"><span data-stu-id="5131d-133">To ensure that the Windows Server 2016 VM image has the latest cumulative update, include the `IncludeLatestCU` parameter when running the `New-AzsServer2016VMImage` cmdlet.</span></span> <span data-ttu-id="5131d-134">Consulte la sección [Parámetros](#parameters) para obtener información acerca de los parámetros permitidos para el cmdlet `New-AzsServer2016VMImage`.</span><span class="sxs-lookup"><span data-stu-id="5131d-134">See the [Parameters](#parameters) section for information about allowed parameters for the `New-AzsServer2016VMImage` cmdlet.</span></span> <span data-ttu-id="5131d-135">Se tarda aproximadamente una hora en publicar la imagen en Marketplace de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5131d-135">It takes about an hour to publish the image to the Azure Stack marketplace.</span></span> 

## <a name="parameters"></a><span data-ttu-id="5131d-136">parameters</span><span class="sxs-lookup"><span data-stu-id="5131d-136">Parameters</span></span>

|<span data-ttu-id="5131d-137">Parámetros de New-AzsServer2016VMImage</span><span class="sxs-lookup"><span data-stu-id="5131d-137">New-AzsServer2016VMImage parameters</span></span>|<span data-ttu-id="5131d-138">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="5131d-138">Required?</span></span>|<span data-ttu-id="5131d-139">Descripción</span><span class="sxs-lookup"><span data-stu-id="5131d-139">Description</span></span>|
|-----|-----|------|
|<span data-ttu-id="5131d-140">ISOPath</span><span class="sxs-lookup"><span data-stu-id="5131d-140">ISOPath</span></span>|<span data-ttu-id="5131d-141">Sí</span><span class="sxs-lookup"><span data-stu-id="5131d-141">Yes</span></span>|<span data-ttu-id="5131d-142">La ruta de acceso completa a la imagen ISO de Windows Server 2016 descargada.</span><span class="sxs-lookup"><span data-stu-id="5131d-142">The fully qualified path to the downloaded Windows Server 2016 ISO.</span></span>|
|<span data-ttu-id="5131d-143">Net35</span><span class="sxs-lookup"><span data-stu-id="5131d-143">Net35</span></span>|<span data-ttu-id="5131d-144">No</span><span class="sxs-lookup"><span data-stu-id="5131d-144">No</span></span>|<span data-ttu-id="5131d-145">Este parámetro permite instalar el runtime de .NET 3.5 en la imagen de Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="5131d-145">This parameter allows you to install the .NET 3.5 runtime on the Windows Server 2016 image.</span></span> <span data-ttu-id="5131d-146">De forma predeterminada, este valor se establece en true.</span><span class="sxs-lookup"><span data-stu-id="5131d-146">By default, this value is set to true.</span></span>|
|<span data-ttu-id="5131d-147">Versión</span><span class="sxs-lookup"><span data-stu-id="5131d-147">Version</span></span>|<span data-ttu-id="5131d-148">No</span><span class="sxs-lookup"><span data-stu-id="5131d-148">No</span></span>|<span data-ttu-id="5131d-149">Este parámetro le permite elegir si desea agregar una imagen de Windows Server 2016 **Básica** o **Completa** o **Ambas**.</span><span class="sxs-lookup"><span data-stu-id="5131d-149">This parameter allows you to choose whether to add a **Core** or **Full** or **Both** Windows Server 2016 images.</span></span> <span data-ttu-id="5131d-150">De forma predeterminada, este valor se establece en "Full".</span><span class="sxs-lookup"><span data-stu-id="5131d-150">By default, this value is set to "Full."</span></span>|
|<span data-ttu-id="5131d-151">VHDSizeInMB</span><span class="sxs-lookup"><span data-stu-id="5131d-151">VHDSizeInMB</span></span>|<span data-ttu-id="5131d-152">No</span><span class="sxs-lookup"><span data-stu-id="5131d-152">No</span></span>|<span data-ttu-id="5131d-153">Establece el tamaño (en MB) de la imagen de disco duro virtual que se va a agregar a su entorno de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5131d-153">Sets the size (in MB) of the VHD image to be added to your Azure Stack environment.</span></span> <span data-ttu-id="5131d-154">De forma predeterminada, este valor se establece en 40.960 MB.</span><span class="sxs-lookup"><span data-stu-id="5131d-154">By default, this value is set to 40960 MB.</span></span>|
|<span data-ttu-id="5131d-155">CreateGalleryItem</span><span class="sxs-lookup"><span data-stu-id="5131d-155">CreateGalleryItem</span></span>|<span data-ttu-id="5131d-156">No</span><span class="sxs-lookup"><span data-stu-id="5131d-156">No</span></span>|<span data-ttu-id="5131d-157">Especifica si se debe crear un elemento de Marketplace para la imagen de Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="5131d-157">Specifies if a Marketplace item should be created for the Windows Server 2016 image.</span></span> <span data-ttu-id="5131d-158">De forma predeterminada, este valor se establece en true.</span><span class="sxs-lookup"><span data-stu-id="5131d-158">By default, this value is set to true.</span></span>|
|<span data-ttu-id="5131d-159">location</span><span class="sxs-lookup"><span data-stu-id="5131d-159">location</span></span> |<span data-ttu-id="5131d-160">No</span><span class="sxs-lookup"><span data-stu-id="5131d-160">No</span></span> |<span data-ttu-id="5131d-161">Especifica la ubicación en la que se debe publicar la imagen de Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="5131d-161">Specifies the location to which the Windows Server 2016 image should be published.</span></span>|
|<span data-ttu-id="5131d-162">IncludeLatestCU</span><span class="sxs-lookup"><span data-stu-id="5131d-162">IncludeLatestCU</span></span>|<span data-ttu-id="5131d-163">No</span><span class="sxs-lookup"><span data-stu-id="5131d-163">No</span></span>|<span data-ttu-id="5131d-164">Establezca este modificador para aplicar la actualización acumulativa más reciente de Windows Server 2016 en el nuevo disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="5131d-164">Set this switch to apply the latest Windows Server 2016 cumulative update to the new VHD.</span></span>|
|<span data-ttu-id="5131d-165">CUUri</span><span class="sxs-lookup"><span data-stu-id="5131d-165">CUUri</span></span> |<span data-ttu-id="5131d-166">No</span><span class="sxs-lookup"><span data-stu-id="5131d-166">No</span></span> |<span data-ttu-id="5131d-167">Establezca este valor para elegir la actualización acumulativa de Windows Server 2016 desde un identificador URI concreto.</span><span class="sxs-lookup"><span data-stu-id="5131d-167">Set this value to choose the Windows Server 2016 cumulative update from a specific URI.</span></span> |
|<span data-ttu-id="5131d-168">CUPath</span><span class="sxs-lookup"><span data-stu-id="5131d-168">CUPath</span></span> |<span data-ttu-id="5131d-169">No</span><span class="sxs-lookup"><span data-stu-id="5131d-169">No</span></span> |<span data-ttu-id="5131d-170">Establezca este valor para elegir la actualización acumulativa de Windows Server 2016 desde una ruta de acceso local.</span><span class="sxs-lookup"><span data-stu-id="5131d-170">Set this value to choose the Windows Server 2016 cumulative update from a local path.</span></span> <span data-ttu-id="5131d-171">Esta opción es útil si ha implementado la instancia de Azure Stack en un entorno desconectado.</span><span class="sxs-lookup"><span data-stu-id="5131d-171">This option is helpful if you have deployed the Azure Stack instance in a disconnected environment.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="5131d-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5131d-172">Next steps</span></span>

[<span data-ttu-id="5131d-173">Aprovisionamiento de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5131d-173">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
