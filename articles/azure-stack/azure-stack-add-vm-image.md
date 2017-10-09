---
title: "aaaAdding una máquina virtual de la imagen tooAzure pila | Documentos de Microsoft"
description: "Agregar los imagen personalizada de Windows o Linux VM de su organización para los inquilinos toouse"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: e5a4236b-1b32-4ee6-9aaa-fcde297a020f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 26dd6c289664c4d64d5932f4396ae778f3f1e1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="make-a-custom-virtual-machine-image-available-in-azure-stack"></a><span data-ttu-id="42e96-103">Hacer que una imagen de máquina virtual personalizada esté disponible en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="42e96-103">Make a custom virtual machine image available in Azure Stack</span></span>

<span data-ttu-id="42e96-104">Azure habilita la pila en la nube a los usuarios de los administradores toomake máquina virtual personalizada imágenes tootheir disponible.</span><span class="sxs-lookup"><span data-stu-id="42e96-104">Azure Stack enables cloud administrators toomake custom virtual machine images available tootheir users.</span></span> <span data-ttu-id="42e96-105">Estas imágenes pueden hacer referencia a plantillas del Administrador de recursos de Azure o agregan toothe interfaz de usuario de Azure Marketplace con creación de hello de un elemento de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="42e96-105">These images can be referenced by Azure Resource Manager templates or added toothe Azure Marketplace UI with hello creation of a Marketplace item.</span></span> 

## <a name="add-a-vm-image-toomarketplace-with-powershell"></a><span data-ttu-id="42e96-106">Agregar un toomarketplace de imagen de máquina virtual con PowerShell</span><span class="sxs-lookup"><span data-stu-id="42e96-106">Add a VM image toomarketplace with PowerShell</span></span>

<span data-ttu-id="42e96-107">Ejecute hello siguiendo los requisitos previos de hello [kit de desarrollo de](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), o desde un cliente externo basado en Windows si está [conectado a través de VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)</span><span class="sxs-lookup"><span data-stu-id="42e96-107">Run hello following prerequisites either from hello [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)</span></span>

* <span data-ttu-id="42e96-108">[Instale PowerShell para Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="42e96-108">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>  

* <span data-ttu-id="42e96-109">Descargar hello [toowork necesarios de herramientas con la pila de Azure](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="42e96-109">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  

* <span data-ttu-id="42e96-110">Prepare una imagen de disco duro virtual del sistema operativo Windows o Linux en formato VHD (no VHDX).</span><span class="sxs-lookup"><span data-stu-id="42e96-110">Prepare a Windows or Linux operating system virtual hard disk image in VHD format (not VHDX).</span></span>
   
   * <span data-ttu-id="42e96-111">Para las imágenes de Windows, Hola artículo [cargar una tooAzure de imagen de máquina virtual de Windows para las implementaciones del Administrador de recursos](../virtual-machines/windows/upload-generalized-managed.md) contiene instrucciones de preparación de imagen de hello **Hola preparar VHD para la carga** sección.</span><span class="sxs-lookup"><span data-stu-id="42e96-111">For Windows images, hello article [Upload a Windows VM image tooAzure for Resource Manager deployments](../virtual-machines/windows/upload-generalized-managed.md) contains image preparation instructions in hello **Prepare hello VHD for upload** section.</span></span>
   * <span data-ttu-id="42e96-112">Para las imágenes de Linux, siga los pasos de Hola para preparar la imagen de Hola o usar una imagen de Linux de la pila de Azure existente tal como se describe en el artículo hello [máquinas virtuales Linux implementar en Azure pila](azure-stack-linux.md).</span><span class="sxs-lookup"><span data-stu-id="42e96-112">For Linux images, follow hello steps to prepare hello image or use an existing Azure Stack Linux image as described in hello article [Deploy Linux virtual machines on Azure Stack](azure-stack-linux.md).</span></span>  

<span data-ttu-id="42e96-113">Ahora ejecute hello después de marketplace de pasos tooadd Hola imagen toohello pila de Azure:</span><span class="sxs-lookup"><span data-stu-id="42e96-113">Now run hello following steps tooadd hello image toohello Azure Stack marketplace:</span></span>

1. <span data-ttu-id="42e96-114">Importar módulos de conectar y ComputeAdmin de hello:</span><span class="sxs-lookup"><span data-stu-id="42e96-114">Import hello Connect and ComputeAdmin modules:</span></span>
   
   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import hello Connect and ComputeAdmin modules
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1
   ``` 

2. <span data-ttu-id="42e96-115">Inicie sesión en tooyour entorno de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="42e96-115">Sign in tooyour Azure Stack environment.</span></span> <span data-ttu-id="42e96-116">Siguiente ejecución Hola secuencias de comandos en función de si su entorno de pila de Azure se implementa mediante el uso de AAD o AD FS (nombre de inquilino AAD de marca tooreplace seguro hello):</span><span class="sxs-lookup"><span data-stu-id="42e96-116">Run hello following script depending on if your Azure Stack environment is deployed by using AAD or AD FS (Make sure tooreplace hello AAD tenant name):</span></span> 

   <span data-ttu-id="42e96-117">a.</span><span class="sxs-lookup"><span data-stu-id="42e96-117">a.</span></span> <span data-ttu-id="42e96-118">**Azure Active Directory**, usar hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="42e96-118">**Azure Active Directory**, use hello following cmdlet:</span></span>

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

   <span data-ttu-id="42e96-119">b.</span><span class="sxs-lookup"><span data-stu-id="42e96-119">b.</span></span> <span data-ttu-id="42e96-120">**Los servicios de federación de Active Directory**, usar hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="42e96-120">**Active Directory Federation Services**, use hello following cmdlet:</span></span>
    
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
    
3. <span data-ttu-id="42e96-121">Agregar imagen de máquina virtual de hello invocando hello `Add-AzsVMImage` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="42e96-121">Add hello VM image by invoking hello `Add-AzsVMImage` cmdlet.</span></span> <span data-ttu-id="42e96-122">En el cmdlet Add-AzsVMImage de hello, especifique Hola osType como Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="42e96-122">In hello Add-AzsVMImage cmdlet, specify hello osType as Windows or Linux.</span></span> <span data-ttu-id="42e96-123">Incluir publicador hello, oferta, SKU y versión de imagen de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="42e96-123">Include hello publisher, offer, SKU, and version for hello VM image.</span></span> <span data-ttu-id="42e96-124">Vea hello [parámetros](#parameters) sección para obtener información acerca de hello permitida parámetros.</span><span class="sxs-lookup"><span data-stu-id="42e96-124">See hello [Parameters](#parameters) section for information about hello allowed parameters.</span></span> <span data-ttu-id="42e96-125">Imagen de máquina virtual de Azure Resource Manager plantillas tooreference Hola utiliza estos parámetros.</span><span class="sxs-lookup"><span data-stu-id="42e96-125">These parameters are used by Azure Resource Manager templates tooreference hello VM image.</span></span> <span data-ttu-id="42e96-126">La siguiente es una invocación de ejemplo del script de Hola:</span><span class="sxs-lookup"><span data-stu-id="42e96-126">Following is an example invocation of hello script:</span></span>
     
     ```powershell
     Add-AzsVMImage `
       -publisher "Canonical" `
       -offer "UbuntuServer" `
       -sku "14.04.3-LTS" `
       -version "1.0.0" `
       -osType Linux `
       -osDiskLocalPath 'C:\Users\AzureStackAdmin\Desktop\UbuntuServer.vhd' `
     ```

<span data-ttu-id="42e96-127">comando de Hola Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="42e96-127">hello command does hello following:</span></span>

* <span data-ttu-id="42e96-128">Autentica el entorno de Azure pila toohello</span><span class="sxs-lookup"><span data-stu-id="42e96-128">Authenticates toohello Azure Stack environment</span></span>
* <span data-ttu-id="42e96-129">Carga tooa Hola de disco duro virtual local recién creado la cuenta de almacenamiento temporal</span><span class="sxs-lookup"><span data-stu-id="42e96-129">Uploads hello local VHD tooa newly created temporary storage account</span></span>
* <span data-ttu-id="42e96-130">Agrega el repositorio de imágenes VM de toohello imagen VM de Hola y</span><span class="sxs-lookup"><span data-stu-id="42e96-130">Adds hello VM image toohello VM image repository and</span></span>
* <span data-ttu-id="42e96-131">Crea un elemento de Marketplace</span><span class="sxs-lookup"><span data-stu-id="42e96-131">Creates a Marketplace item</span></span>

<span data-ttu-id="42e96-132">tooverify que el comando de Hola se ejecutó correctamente, vaya tooMarketplace en el portal de hello y, a continuación, compruebe dicha imagen VM Hola está disponible en hello **máquinas virtuales** categoría.</span><span class="sxs-lookup"><span data-stu-id="42e96-132">tooverify that hello command ran successfully, go tooMarketplace in hello portal, and then verify that hello VM image is available in hello **Virtual Machines** category.</span></span>

![Imagen de máquina virtual agregada correctamente](./media/azure-stack-add-vm-image/image5.PNG) 

## <a name="remove-a-vm-image-with-powershell"></a><span data-ttu-id="42e96-134">Eliminación de una imagen de máquina virtual con PowerShell</span><span class="sxs-lookup"><span data-stu-id="42e96-134">Remove a VM image with PowerShell</span></span>

<span data-ttu-id="42e96-135">Cuando ya no necesita hello imagen de máquina virtual que ha cargado anteriormente, puede eliminarla del marketplace de hello mediante el uso de hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="42e96-135">When you no longer need hello virtual machine image that you have uploaded earlier, you can delete it from hello marketplace by using hello following cmdlet:</span></span>

```powershell
Remove-AzsVMImage `
  -publisher "Canonical" `
  -offer "UbuntuServer" `
  -sku "14.04.3-LTS" `
  -version "1.0.0" `
```

## <a name="parameters"></a><span data-ttu-id="42e96-136">parameters</span><span class="sxs-lookup"><span data-stu-id="42e96-136">Parameters</span></span>

| <span data-ttu-id="42e96-137">Parámetro</span><span class="sxs-lookup"><span data-stu-id="42e96-137">Parameter</span></span> | <span data-ttu-id="42e96-138">Descripción</span><span class="sxs-lookup"><span data-stu-id="42e96-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="42e96-139">**publisher**</span><span class="sxs-lookup"><span data-stu-id="42e96-139">**publisher**</span></span> |<span data-ttu-id="42e96-140">segmento de nombre de publicador Hola de imagen de VM de Hola que los usuarios usan al implementar la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="42e96-140">hello publisher name segment of hello VM image that users use when deploying hello image.</span></span> <span data-ttu-id="42e96-141">Un ejemplo es 'Microsoft'.</span><span class="sxs-lookup"><span data-stu-id="42e96-141">An example is ‘Microsoft’.</span></span> <span data-ttu-id="42e96-142">No incluya un espacio u otros caracteres especiales en este campo.</span><span class="sxs-lookup"><span data-stu-id="42e96-142">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="42e96-143">**offer**</span><span class="sxs-lookup"><span data-stu-id="42e96-143">**offer**</span></span> |<span data-ttu-id="42e96-144">segmento de nombre de la oferta de Hola de imagen de máquina virtual que los usuarios usan al implementar la imagen de máquina virtual de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="42e96-144">hello offer name segment of hello VM Image that users use when deploying hello VM image.</span></span> <span data-ttu-id="42e96-145">Un ejemplo es 'WindowsServer'.</span><span class="sxs-lookup"><span data-stu-id="42e96-145">An example is ‘WindowsServer’.</span></span> <span data-ttu-id="42e96-146">No incluya un espacio u otros caracteres especiales en este campo.</span><span class="sxs-lookup"><span data-stu-id="42e96-146">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="42e96-147">**sku**</span><span class="sxs-lookup"><span data-stu-id="42e96-147">**sku**</span></span> |<span data-ttu-id="42e96-148">segmento de nombre de SKU de Hola de imagen de máquina virtual que los usuarios usan al implementar la imagen de máquina virtual de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="42e96-148">hello SKU name segment of hello VM Image that users use when deploying hello VM image.</span></span> <span data-ttu-id="42e96-149">Un ejemplo es 'Datacenter2016'.</span><span class="sxs-lookup"><span data-stu-id="42e96-149">An example is ‘Datacenter2016’.</span></span> <span data-ttu-id="42e96-150">No incluya un espacio u otros caracteres especiales en este campo.</span><span class="sxs-lookup"><span data-stu-id="42e96-150">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="42e96-151">**version**</span><span class="sxs-lookup"><span data-stu-id="42e96-151">**version**</span></span> |<span data-ttu-id="42e96-152">versión de Hola de imagen de máquina virtual que los usuarios usan al implementar la imagen de máquina virtual de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="42e96-152">hello version of hello VM Image that users use when deploying hello VM image.</span></span> <span data-ttu-id="42e96-153">Esta versión está en formato de hello  *\#.\#. \#*.</span><span class="sxs-lookup"><span data-stu-id="42e96-153">This version is in hello format *\#.\#.\#*.</span></span> <span data-ttu-id="42e96-154">Un ejemplo es '1.0.0'.</span><span class="sxs-lookup"><span data-stu-id="42e96-154">An example is ‘1.0.0’.</span></span> <span data-ttu-id="42e96-155">No incluya un espacio u otros caracteres especiales en este campo.</span><span class="sxs-lookup"><span data-stu-id="42e96-155">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="42e96-156">**osType**</span><span class="sxs-lookup"><span data-stu-id="42e96-156">**osType**</span></span> |<span data-ttu-id="42e96-157">Hola osType de imagen de hello debe ser 'Windows' o 'Linux'.</span><span class="sxs-lookup"><span data-stu-id="42e96-157">hello osType of hello image must be either ‘Windows’ or ‘Linux’.</span></span> |
| <span data-ttu-id="42e96-158">**osDiskLocalPath**</span><span class="sxs-lookup"><span data-stu-id="42e96-158">**osDiskLocalPath**</span></span> |<span data-ttu-id="42e96-159">disco toohello SO de ruta de acceso local de Hello disco duro virtual que se va a cargar como un tooAzure de imagen VM pila.</span><span class="sxs-lookup"><span data-stu-id="42e96-159">hello local path toohello OS disk VHD that you are uploading as a VM image tooAzure Stack.</span></span> |
| <span data-ttu-id="42e96-160">**dataDiskLocalPaths**</span><span class="sxs-lookup"><span data-stu-id="42e96-160">**dataDiskLocalPaths**</span></span> |<span data-ttu-id="42e96-161">Una matriz opcional de rutas de acceso local de Hola para discos de datos que se pueden cargar como parte de la imagen de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="42e96-161">An optional array of hello local paths for data disks that can be uploaded as part of hello VM image.</span></span> |
| <span data-ttu-id="42e96-162">**CreateGalleryItem**</span><span class="sxs-lookup"><span data-stu-id="42e96-162">**CreateGalleryItem**</span></span> |<span data-ttu-id="42e96-163">Un indicador booleano que determina si un elemento de Marketplace toocreate.</span><span class="sxs-lookup"><span data-stu-id="42e96-163">A Boolean flag that determines whether toocreate an item in Marketplace.</span></span> <span data-ttu-id="42e96-164">De forma predeterminada, se establece tootrue.</span><span class="sxs-lookup"><span data-stu-id="42e96-164">By default, it is set tootrue.</span></span> |
| <span data-ttu-id="42e96-165">**title**</span><span class="sxs-lookup"><span data-stu-id="42e96-165">**title**</span></span> |<span data-ttu-id="42e96-166">Hola nombre para mostrar del elemento de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="42e96-166">hello display name of Marketplace item.</span></span> <span data-ttu-id="42e96-167">De forma predeterminada, se establece toohello Sku de oferta de publicador de la imagen de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="42e96-167">By default, it is set toohello Publisher-Offer-Sku of hello VM image.</span></span> |
| <span data-ttu-id="42e96-168">**descripción**</span><span class="sxs-lookup"><span data-stu-id="42e96-168">**description**</span></span> |<span data-ttu-id="42e96-169">Descripción de Hello del elemento de Marketplace de Hola.</span><span class="sxs-lookup"><span data-stu-id="42e96-169">hello description of hello Marketplace item.</span></span> |
| <span data-ttu-id="42e96-170">**ubicación**</span><span class="sxs-lookup"><span data-stu-id="42e96-170">**location**</span></span> |<span data-ttu-id="42e96-171">debe publicarse la imagen de máquina virtual de Hello ubicación toowhich Hola.</span><span class="sxs-lookup"><span data-stu-id="42e96-171">hello location toowhich hello VM image should be published.</span></span> <span data-ttu-id="42e96-172">De forma predeterminada, este valor se establece toolocal.</span><span class="sxs-lookup"><span data-stu-id="42e96-172">By default, this value is set toolocal.</span></span>|
| <span data-ttu-id="42e96-173">**osDiskBlobURI**</span><span class="sxs-lookup"><span data-stu-id="42e96-173">**osDiskBlobURI**</span></span> |<span data-ttu-id="42e96-174">Opcionalmente, este script también acepta un identificador URI de Blob Storage para disco de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="42e96-174">Optionally, this script also accepts a Blob storage URI for osDisk.</span></span> |
| <span data-ttu-id="42e96-175">**dataDiskBlobURIs**</span><span class="sxs-lookup"><span data-stu-id="42e96-175">**dataDiskBlobURIs**</span></span> |<span data-ttu-id="42e96-176">Opcionalmente, este script también acepta una matriz de almacenamiento de blobs de URI para agregar imagen de toohello de discos de datos.</span><span class="sxs-lookup"><span data-stu-id="42e96-176">Optionally, this script also accepts an array of Blob storage URIs for adding data disks toohello image.</span></span> |

## <a name="add-a-vm-image-through-hello-portal"></a><span data-ttu-id="42e96-177">Agregar una imagen de máquina virtual a través del portal de Hola</span><span class="sxs-lookup"><span data-stu-id="42e96-177">Add a VM image through hello portal</span></span>

> [!NOTE]
> <span data-ttu-id="42e96-178">Este método requiere crear elemento de Marketplace de Hola por separado.</span><span class="sxs-lookup"><span data-stu-id="42e96-178">This method requires creating hello Marketplace item separately.</span></span>

<span data-ttu-id="42e96-179">Un requisito de las imágenes es que se pueda hacer referencia a ellas con un identificador URI de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="42e96-179">One requirement of images is that they can be referenced by a Blob storage URI.</span></span> <span data-ttu-id="42e96-180">Preparar una imagen de sistema operativo Windows o Linux en formato de disco duro virtual (no VHDX) y, a continuación, cargue la cuenta de almacenamiento tooa Hola de imagen en Azure o Azure pila.</span><span class="sxs-lookup"><span data-stu-id="42e96-180">Prepare a Windows or Linux operating system image in VHD format (not VHDX), and then upload hello image tooa storage account in Azure or Azure Stack.</span></span> <span data-ttu-id="42e96-181">Si la imagen ya está cargado toohello almacenamiento de blobs en Azure o la pila de Azure, puede omitir el paso 1.</span><span class="sxs-lookup"><span data-stu-id="42e96-181">If your image is already uploaded toohello Blob storage in Azure or Azure Stack, you can skip step1.</span></span>

1. <span data-ttu-id="42e96-182">[Cargar un tooAzure de imagen de máquina virtual de Windows para las implementaciones del Administrador de recursos](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) o una imagen de Linux, siga las instrucciones de hello descritas en hello [máquinas virtuales Linux implementar en Azure pila](azure-stack-linux.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="42e96-182">[Upload a Windows VM image tooAzure for Resource Manager deployments](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) or for a Linux image, follow hello instructions described in hello [Deploy Linux virtual machines on Azure Stack](azure-stack-linux.md) article.</span></span> <span data-ttu-id="42e96-183">Debe conocer Hola siguientes consideraciones antes de cargar imagen de hello:</span><span class="sxs-lookup"><span data-stu-id="42e96-183">You should understand hello following considerations before you upload hello image:</span></span>

   * <span data-ttu-id="42e96-184">Resulta más eficaz tooupload un almacenamiento de blobs de la pila de imagen tooAzure que tooAzure almacenamiento de blobs porque toma menos repositorio de imágenes tiempo toopush Hola imagen toohello pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="42e96-184">It's more efficient tooupload an image tooAzure Stack Blob storage than tooAzure Blob storage because it takes less time toopush hello image toohello Azure Stack image repository.</span></span> 
   
   * <span data-ttu-id="42e96-185">Al cargar hello [imagen de máquina virtual de Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), que seguro Hola toosubstitute **tooAzure de inicio de sesión** paso con hello [configurar el entorno de PowerShell del operador de hello Azure pila](azure-stack-powershell-configure-admin.md)paso.</span><span class="sxs-lookup"><span data-stu-id="42e96-185">When uploading hello [Windows VM image](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), make sure toosubstitute hello **Login tooAzure** step with hello [Configure hello Azure Stack operator's PowerShell environment](azure-stack-powershell-configure-admin.md)  step.</span></span>  

   * <span data-ttu-id="42e96-186">Tome nota de hello URI donde cargar imagen de hello, que se encuentra en hello siguiendo el formato de almacenamiento de blobs:  *&lt;storageAccount&gt;/&lt;blobContainer&gt; / &lt;targetVHDName&gt;*.vhd</span><span class="sxs-lookup"><span data-stu-id="42e96-186">Make a note of hello Blob storage URI where you upload hello image, which is in hello following format: *&lt;storageAccount&gt;/&lt;blobContainer&gt;/&lt;targetVHDName&gt;*.vhd</span></span>

   * <span data-ttu-id="42e96-187">toomake Hola accesible de forma anónima, vaya toohello cuenta blob en contenedor de almacenamiento blob donde hello VM imagen VHD se cargó demasiado**Blob,** y, a continuación, seleccione **directiva de acceso**.</span><span class="sxs-lookup"><span data-stu-id="42e96-187">toomake hello blob anonymously accessible, go toohello storage account blob container where hello VM image VHD was uploaded too**Blob,** and then select **Access Policy**.</span></span> <span data-ttu-id="42e96-188">Si lo desea, puede generar una firma de acceso compartido para el contenedor de Hola e incluirlo como parte del URI del blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="42e96-188">If you want, you can instead generate a shared access signature for hello container and include it as part of hello blob URI.</span></span>

   ![Navegue toostorage blobs de cuenta](./media/azure-stack-add-vm-image/image1.png)

   ![Set blob acceso toopublic](./media/azure-stack-add-vm-image/image2.png)

2. <span data-ttu-id="42e96-191">Inicie sesión en tooAzure pila como un administrador de la nube > en el menú de hello, haga clic en **más servicios** > **proveedores de recursos** > seleccione **proceso**  >  **Imágenes de máquina virtual** > **agregar**</span><span class="sxs-lookup"><span data-stu-id="42e96-191">Sign in tooAzure Stack as a cloud administrator > From hello menu, click **More services** > **Resource Providers** > select  **Compute** > **VM images** > **Add**</span></span>

3. <span data-ttu-id="42e96-192">En hello **agregar una imagen de VM** hoja, escriba publicador hello, oferta, SKU y versión de imagen de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="42e96-192">On hello **Add a VM Image** blade, enter hello publisher, offer, SKU, and version of hello virtual machine image.</span></span> <span data-ttu-id="42e96-193">Estos segmentos de nombre de referencia toohello imagen de máquina virtual en las plantillas de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="42e96-193">These name segments refer toohello VM image in Resource Manager templates.</span></span> <span data-ttu-id="42e96-194">Asegúrese de que tooselect el **osType** correctamente.</span><span class="sxs-lookup"><span data-stu-id="42e96-194">Make sure tooselect the **osType** correctly.</span></span> <span data-ttu-id="42e96-195">Para **URI de Blob del disco OD**, escriba Hola URI de Blob donde se cargó la imagen y haga clic en **crear** toobegin crear la imagen de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="42e96-195">For **OD Disk Blob URI**, enter hello Blob URI where the image was uploaded and click **Create** toobegin creating the VM Image.</span></span>
   
   ![BEGIN toocreate Hola imagen](./media/azure-stack-add-vm-image/image4.png)

   <span data-ttu-id="42e96-197">Cuando se crea correctamente la imagen de hello, Hola estado de la imagen VM cambia too'Succeeded'.</span><span class="sxs-lookup"><span data-stu-id="42e96-197">When hello image is successfully created, hello VM image status changes too‘Succeeded’.</span></span>

4. <span data-ttu-id="42e96-198">toomake Hola imagen de máquina virtual más fácilmente disponible para consumo del usuario en la interfaz de usuario de hello, lo mejor es demasiado[crear un elemento de Marketplace](azure-stack-create-and-publish-marketplace-item.md).</span><span class="sxs-lookup"><span data-stu-id="42e96-198">toomake hello virtual machine image more readily available for user consumption in hello UI, it is best too[create a Marketplace item](azure-stack-create-and-publish-marketplace-item.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="42e96-199">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="42e96-199">Next steps</span></span>

[<span data-ttu-id="42e96-200">Aprovisionamiento de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="42e96-200">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)