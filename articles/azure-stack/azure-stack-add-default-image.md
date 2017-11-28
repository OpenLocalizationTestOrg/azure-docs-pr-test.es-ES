---
title: marketplace de aaaAdd Hola predeterminado VM imagen toohello pila de Azure | Documentos de Microsoft
description: "Agregue el catálogo de soluciones de hello VM de Windows Server 2016 predeterminada imagen toohello pila de Azure."
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
ms.openlocfilehash: 9b5a6f4e4c73c706b059e3c3622a968b5eef9a27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-hello-windows-server-2016-vm-image-toohello-azure-stack-marketplace"></a><span data-ttu-id="29bad-103">Agregue el catálogo de soluciones de hello VM de Windows Server 2016 imagen toohello pila de Azure</span><span class="sxs-lookup"><span data-stu-id="29bad-103">Add hello Windows Server 2016 VM image toohello Azure Stack marketplace</span></span>

<span data-ttu-id="29bad-104">De forma predeterminada, no hay ninguna imagen de máquina virtual disponible en marketplace de hello pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="29bad-104">By default, there aren’t any virtual machine images available in hello Azure Stack marketplace.</span></span> <span data-ttu-id="29bad-105">Administrador de la nube de Hello Azure pila debe agregar un marketplace de toohello imagen antes de que los usuarios puedan usarlos.</span><span class="sxs-lookup"><span data-stu-id="29bad-105">hello Azure Stack cloud administrator must add an image toohello marketplace before users can use them.</span></span> <span data-ttu-id="29bad-106">Puede agregar el catálogo de soluciones de Windows Server 2016 Hola imagen toohello pila de Azure mediante uno de hello siguiendo dos métodos:</span><span class="sxs-lookup"><span data-stu-id="29bad-106">You can add hello Windows Server 2016 image toohello Azure Stack marketplace by using one of hello following two methods:</span></span>

* <span data-ttu-id="29bad-107">[Agregar imagen de hello descargándolo desde hello Azure Marketplace](#add-the-image-by-downloading-it-from-the-Azure-marketplace) -Utilice esta opción si está trabajando en un escenario conectado y si se ha registrado la instancia de la pila de Azure con Azure.</span><span class="sxs-lookup"><span data-stu-id="29bad-107">[Add hello image by downloading it from hello Azure Marketplace](#add-the-image-by-downloading-it-from-the-Azure-marketplace) - Use this option if you are operating in a connected scenario and if you have registered your Azure Stack instance with Azure.</span></span>

* <span data-ttu-id="29bad-108">[Agregar imagen de hello mediante PowerShell](#add-the-image-by-using-powershell) -Utilice esta opción si ha implementado en una situación sin conexión o en escenarios de pila de Azure con conectividad limitada.</span><span class="sxs-lookup"><span data-stu-id="29bad-108">[Add hello image by using PowerShell](#add-the-image-by-using-powershell) - Use this option if you have deployed Azure Stack in a disconnected scenario or in scenarios with limited connectivity.</span></span>

## <a name="add-hello-image-by-downloading-it-from-hello-azure-marketplace"></a><span data-ttu-id="29bad-109">Agregar imagen de hello descargándolo desde hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="29bad-109">Add hello image by downloading it from hello Azure Marketplace</span></span>

1. <span data-ttu-id="29bad-110">Después de implementar la pila de Azure, inicie sesión en tooyour Kit de desarrollo de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="29bad-110">After deploying Azure Stack, sign in tooyour Azure Stack Development Kit.</span></span>

2. <span data-ttu-id="29bad-111">Haga clic en **Más servicios** > **Marketplace Management** (Administración de Marketplace)  > **Add from Azure** (Agregar desde Azure).</span><span class="sxs-lookup"><span data-stu-id="29bad-111">click **More services** > **Marketplace Management** > **Add from Azure**</span></span> 

3. <span data-ttu-id="29bad-112">Buscar o buscar hello **centro de datos de Windows Server 2016: Eval** imagen > haga clic en **descargar**</span><span class="sxs-lookup"><span data-stu-id="29bad-112">Find or search for hello **Windows Server 2016 Datacenter – Eval** image > click **Download**</span></span>

   ![Descarga de la imagen desde Azure](media/azure-stack-add-default-image/download-image.png)

<span data-ttu-id="29bad-114">Una vez finalizada la descarga de hello, imagen Hola se agrega toohello **Marketplace administración** hoja y se pone a disposición de hello **máquinas virtuales** hoja.</span><span class="sxs-lookup"><span data-stu-id="29bad-114">After hello download completes, hello image is added toohello **Marketplace Management** blade and it is also made available from hello **Virtual Machines** blade.</span></span>

## <a name="add-hello-image-by-using-powershell"></a><span data-ttu-id="29bad-115">Agregar imagen de hello mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="29bad-115">Add hello image by using PowerShell</span></span>

### <a name="prerequisites"></a><span data-ttu-id="29bad-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="29bad-116">Prerequisites</span></span> 

<span data-ttu-id="29bad-117">Ejecute hello siguiendo los requisitos previos de hello [kit de desarrollo de](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), o desde un cliente externo basado en Windows si está [conectado a través de VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="29bad-117">Run hello following prerequisites either from hello [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="29bad-118">Instale los [módulos de Azure PowerShell compatibles con Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="29bad-118">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  

* <span data-ttu-id="29bad-119">Descargar hello [toowork necesarios de herramientas con la pila de Azure](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="29bad-119">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  

* <span data-ttu-id="29bad-120">Vaya toohttps://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 y descargar la evaluación de Windows Server 2016 Hola.</span><span class="sxs-lookup"><span data-stu-id="29bad-120">Go toohttps://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 and download hello Windows Server 2016 evaluation.</span></span> <span data-ttu-id="29bad-121">Cuando se le pida, seleccione hello **ISO** versión de descarga de Hola.</span><span class="sxs-lookup"><span data-stu-id="29bad-121">When prompted, select hello **ISO** version of hello download.</span></span> <span data-ttu-id="29bad-122">Toohello de ruta de acceso de registro Hola descargar ubicación, que se utiliza más adelante en estos pasos.</span><span class="sxs-lookup"><span data-stu-id="29bad-122">Record hello path toohello download location, which is used later in these steps.</span></span> <span data-ttu-id="29bad-123">Este paso requiere conectividad a Internet.</span><span class="sxs-lookup"><span data-stu-id="29bad-123">This step requires internet connectivity.</span></span>  

<span data-ttu-id="29bad-124">Ahora ejecute hello después de marketplace de pasos tooadd Hola imagen toohello pila de Azure:</span><span class="sxs-lookup"><span data-stu-id="29bad-124">Now run hello following steps tooadd hello image toohello Azure Stack marketplace:</span></span>
   
1. <span data-ttu-id="29bad-125">Importar módulos de Azure Connect de pila y ComputeAdmin de hello mediante el uso de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="29bad-125">Import hello Azure Stack Connect and ComputeAdmin modules by using hello following commands:</span></span>

   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import hello Connect and ComputeAdmin modules   
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1

   ```

2. <span data-ttu-id="29bad-126">Inicie sesión en tooyour entorno de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="29bad-126">Sign in tooyour Azure Stack environment.</span></span> <span data-ttu-id="29bad-127">Siguiente ejecución Hola secuencias de comandos en función de si su entorno de pila de Azure se implementa mediante el uso de AAD o AD FS (nombre de inquilino AAD de marca tooreplace seguro hello):</span><span class="sxs-lookup"><span data-stu-id="29bad-127">Run hello following script depending on if your Azure Stack environment is deployed by using AAD or AD FS (Make sure tooreplace hello AAD tenant name):</span></span>  

   <span data-ttu-id="29bad-128">a.</span><span class="sxs-lookup"><span data-stu-id="29bad-128">a.</span></span> <span data-ttu-id="29bad-129">**Azure Active Directory**, usar hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="29bad-129">**Azure Active Directory**, use hello following cmdlet:</span></span>

   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

   Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience "https://graph.windows.net/"

   $TenantID = Get-AzsDirectoryTenantId `
     -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
     -EnvironmentName AzureStackAdmin

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```

   <span data-ttu-id="29bad-130">b.</span><span class="sxs-lookup"><span data-stu-id="29bad-130">b.</span></span> <span data-ttu-id="29bad-131">**Los servicios de federación de Active Directory**, usar hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="29bad-131">**Active Directory Federation Services**, use hello following cmdlet:</span></span>
    
   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external"

   Set-AzureRmEnvironment `
     -Name "AzureStackAdmin" `
     -GraphAudience "https://graph.local.azurestack.external/" `
     -EnableAdfsAuthentication:$true

   $TenantID = Get-AzsDirectoryTenantId `
     -ADFS 
     -EnvironmentName AzureStackAdmin 

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```
   
3. <span data-ttu-id="29bad-132">Agregar el catálogo de soluciones de Windows Server 2016 Hola imagen toohello pila de Azure (asegúrese de que tooreplace hello *Path_to_ISO* con toohello de ruta de acceso de hello ISO WS2016 descargó):</span><span class="sxs-lookup"><span data-stu-id="29bad-132">Add hello Windows Server 2016 image toohello Azure Stack marketplace (Make sure tooreplace hello *Path_to_ISO* with hello path toohello WS2016 ISO you downloaded):</span></span>

   ```PowerShell
   $ISOPath = "<Fully_Qualified_Path_to_ISO>"

   # Add a Windows Server 2016 Evaluation VM Image.
   New-AzsServer2016VMImage `
     -ISOPath $ISOPath

   ```

<span data-ttu-id="29bad-133">tooensure que Hola imagen de máquina virtual de Windows Server 2016 tiene Hola actualización acumulativa más reciente, incluyen hello `IncludeLatestCU` parámetro al ejecutar hello `New-AzsServer2016VMImage` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="29bad-133">tooensure that hello Windows Server 2016 VM image has hello latest cumulative update, include hello `IncludeLatestCU` parameter when running hello `New-AzsServer2016VMImage` cmdlet.</span></span> <span data-ttu-id="29bad-134">Vea hello [parámetros](#parameters) sección para obtener información acerca de los parámetros permitidos para hello `New-AzsServer2016VMImage` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="29bad-134">See hello [Parameters](#parameters) section for information about allowed parameters for hello `New-AzsServer2016VMImage` cmdlet.</span></span> <span data-ttu-id="29bad-135">Se tarda aproximadamente un mercado hora toopublish Hola imagen toohello pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="29bad-135">It takes about an hour toopublish hello image toohello Azure Stack marketplace.</span></span> 

## <a name="parameters"></a><span data-ttu-id="29bad-136">parameters</span><span class="sxs-lookup"><span data-stu-id="29bad-136">Parameters</span></span>

|<span data-ttu-id="29bad-137">Parámetros de New-AzsServer2016VMImage</span><span class="sxs-lookup"><span data-stu-id="29bad-137">New-AzsServer2016VMImage parameters</span></span>|<span data-ttu-id="29bad-138">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="29bad-138">Required?</span></span>|<span data-ttu-id="29bad-139">Descripción</span><span class="sxs-lookup"><span data-stu-id="29bad-139">Description</span></span>|
|-----|-----|------|
|<span data-ttu-id="29bad-140">ISOPath</span><span class="sxs-lookup"><span data-stu-id="29bad-140">ISOPath</span></span>|<span data-ttu-id="29bad-141">Sí</span><span class="sxs-lookup"><span data-stu-id="29bad-141">Yes</span></span>|<span data-ttu-id="29bad-142">Hello toohello de ruta de acceso completa descarga Windows Server 2016 ISO.</span><span class="sxs-lookup"><span data-stu-id="29bad-142">hello fully qualified path toohello downloaded Windows Server 2016 ISO.</span></span>|
|<span data-ttu-id="29bad-143">Net35</span><span class="sxs-lookup"><span data-stu-id="29bad-143">Net35</span></span>|<span data-ttu-id="29bad-144">No</span><span class="sxs-lookup"><span data-stu-id="29bad-144">No</span></span>|<span data-ttu-id="29bad-145">Este parámetro permite tooinstall Hola .NET 3.5 runtime en la imagen de Windows Server 2016 Hola.</span><span class="sxs-lookup"><span data-stu-id="29bad-145">This parameter allows you tooinstall hello .NET 3.5 runtime on hello Windows Server 2016 image.</span></span> <span data-ttu-id="29bad-146">De forma predeterminada, este valor se establece tootrue.</span><span class="sxs-lookup"><span data-stu-id="29bad-146">By default, this value is set tootrue.</span></span> <span data-ttu-id="29bad-147">Es obligatorio que esa imagen hello contiene Hola 3.5 de .NET en tiempo de ejecución tooinstall Hola SQL y MYSQL proveedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="29bad-147">It is mandatory that hello image contains hello .NET 3.5 runtime tooinstall hello SQL and MYSQL resource providers.</span></span> |
|<span data-ttu-id="29bad-148">Versión</span><span class="sxs-lookup"><span data-stu-id="29bad-148">Version</span></span>|<span data-ttu-id="29bad-149">No</span><span class="sxs-lookup"><span data-stu-id="29bad-149">No</span></span>|<span data-ttu-id="29bad-150">Este parámetro permite toochoose si tooadd una **Core** o **completa** o **ambos** imágenes de Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="29bad-150">This parameter allows you toochoose whether tooadd a **Core** or **Full** or **Both** Windows Server 2016 images.</span></span> <span data-ttu-id="29bad-151">De forma predeterminada, este valor se establece demasiado "Full".</span><span class="sxs-lookup"><span data-stu-id="29bad-151">By default, this value is set too"Full."</span></span>|
|<span data-ttu-id="29bad-152">VHDSizeInMB</span><span class="sxs-lookup"><span data-stu-id="29bad-152">VHDSizeInMB</span></span>|<span data-ttu-id="29bad-153">No</span><span class="sxs-lookup"><span data-stu-id="29bad-153">No</span></span>|<span data-ttu-id="29bad-154">Establece el tamaño de hello (en MB) de toobe de imagen de disco duro virtual de hello agrega entorno de Azure pila tooyour.</span><span class="sxs-lookup"><span data-stu-id="29bad-154">Sets hello size (in MB) of hello VHD image toobe added tooyour Azure Stack environment.</span></span> <span data-ttu-id="29bad-155">De forma predeterminada, este valor se establece too40960 MB.</span><span class="sxs-lookup"><span data-stu-id="29bad-155">By default, this value is set too40960 MB.</span></span>|
|<span data-ttu-id="29bad-156">CreateGalleryItem</span><span class="sxs-lookup"><span data-stu-id="29bad-156">CreateGalleryItem</span></span>|<span data-ttu-id="29bad-157">No</span><span class="sxs-lookup"><span data-stu-id="29bad-157">No</span></span>|<span data-ttu-id="29bad-158">Especifica si se debe crear un elemento de Marketplace de imagen de Windows Server 2016 Hola.</span><span class="sxs-lookup"><span data-stu-id="29bad-158">Specifies if a Marketplace item should be created for hello Windows Server 2016 image.</span></span> <span data-ttu-id="29bad-159">De forma predeterminada, este valor se establece tootrue.</span><span class="sxs-lookup"><span data-stu-id="29bad-159">By default, this value is set tootrue.</span></span>|
|<span data-ttu-id="29bad-160">location</span><span class="sxs-lookup"><span data-stu-id="29bad-160">location</span></span> |<span data-ttu-id="29bad-161">No</span><span class="sxs-lookup"><span data-stu-id="29bad-161">No</span></span> |<span data-ttu-id="29bad-162">Especifica la imagen de Windows Server 2016 de hello ubicación toowhich Hola debe publicarse.</span><span class="sxs-lookup"><span data-stu-id="29bad-162">Specifies hello location toowhich hello Windows Server 2016 image should be published.</span></span>|
|<span data-ttu-id="29bad-163">IncludeLatestCU</span><span class="sxs-lookup"><span data-stu-id="29bad-163">IncludeLatestCU</span></span>|<span data-ttu-id="29bad-164">No</span><span class="sxs-lookup"><span data-stu-id="29bad-164">No</span></span>|<span data-ttu-id="29bad-165">Establecer este modificador tooapply hello más reciente Windows Server 2016 actualización acumulativa toohello nuevo disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="29bad-165">Set this switch tooapply hello latest Windows Server 2016 cumulative update toohello new VHD.</span></span>|
|<span data-ttu-id="29bad-166">CUUri</span><span class="sxs-lookup"><span data-stu-id="29bad-166">CUUri</span></span> |<span data-ttu-id="29bad-167">No</span><span class="sxs-lookup"><span data-stu-id="29bad-167">No</span></span> |<span data-ttu-id="29bad-168">Establecer esta actualización acumulativa de valor toochoose Hola Windows Server 2016 desde un URI concreto.</span><span class="sxs-lookup"><span data-stu-id="29bad-168">Set this value toochoose hello Windows Server 2016 cumulative update from a specific URI.</span></span> |
|<span data-ttu-id="29bad-169">CUPath</span><span class="sxs-lookup"><span data-stu-id="29bad-169">CUPath</span></span> |<span data-ttu-id="29bad-170">No</span><span class="sxs-lookup"><span data-stu-id="29bad-170">No</span></span> |<span data-ttu-id="29bad-171">Establecer esta actualización acumulativa de valor toochoose Hola Windows Server 2016 desde una ruta de acceso local.</span><span class="sxs-lookup"><span data-stu-id="29bad-171">Set this value toochoose hello Windows Server 2016 cumulative update from a local path.</span></span> <span data-ttu-id="29bad-172">Esta opción es útil si ha implementado la instancia de la pila de Azure de hello en un entorno desconectado.</span><span class="sxs-lookup"><span data-stu-id="29bad-172">This option is helpful if you have deployed hello Azure Stack instance in a disconnected environment.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="29bad-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="29bad-173">Next steps</span></span>

[<span data-ttu-id="29bad-174">Aprovisionamiento de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="29bad-174">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
