---
title: "Agregación de una imagen de máquina virtual a Azure Stack | Microsoft Docs"
description: "Agregar la imagen personalizada de máquina virtual Windows o Linux de su organización para uso de los inquilinos"
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
ms.openlocfilehash: 793f6c0f1ad92cec4cbb56662685ca151f90b48c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="make-a-custom-virtual-machine-image-available-in-azure-stack"></a><span data-ttu-id="94734-103">Hacer que una imagen de máquina virtual personalizada esté disponible en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="94734-103">Make a custom virtual machine image available in Azure Stack</span></span>

<span data-ttu-id="94734-104">Pila de Azure permite a los administradores de nube poner imágenes de máquina virtual personalizada a disposición de sus usuarios.</span><span class="sxs-lookup"><span data-stu-id="94734-104">Azure Stack enables cloud administrators to make custom virtual machine images available to their users.</span></span> <span data-ttu-id="94734-105">Las plantillas de Azure Resource Manager pueden hacer referencia a estas imágenes y pueden ser agregadas a la interfaz de usuario de Azure Marketplace con la creación de un elemento de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="94734-105">These images can be referenced by Azure Resource Manager templates or added to the Azure Marketplace UI with the creation of a Marketplace item.</span></span> 

## <a name="add-a-vm-image-to-marketplace-with-powershell"></a><span data-ttu-id="94734-106">Agregación de una imagen de máquina virtual a Marketplace con PowerShell</span><span class="sxs-lookup"><span data-stu-id="94734-106">Add a VM image to marketplace with PowerShell</span></span>

<span data-ttu-id="94734-107">Implemente los siguientes requisitos previos desde el [kit de desarrollo](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) o desde un cliente externo basado en Windows, si está [conectado a través de VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)</span><span class="sxs-lookup"><span data-stu-id="94734-107">Run the following prerequisites either from the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)</span></span>

* <span data-ttu-id="94734-108">[Instale PowerShell para Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="94734-108">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>  

* <span data-ttu-id="94734-109">Descargue las [herramientas necesarias para trabajar con Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="94734-109">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span>  

* <span data-ttu-id="94734-110">Prepare una imagen de disco duro virtual del sistema operativo Windows o Linux en formato VHD (no VHDX).</span><span class="sxs-lookup"><span data-stu-id="94734-110">Prepare a Windows or Linux operating system virtual hard disk image in VHD format (not VHDX).</span></span>
   
   * <span data-ttu-id="94734-111">Para imágenes de Windows, el artículo [Carga de una imagen de máquina virtual Windows en Azure para implementaciones de Resource Manager](../virtual-machines/windows/upload-generalized-managed.md) contiene instrucciones de preparación de la imagen en la sección **Preparación del disco duro virtual para la carga**.</span><span class="sxs-lookup"><span data-stu-id="94734-111">For Windows images, the article [Upload a Windows VM image to Azure for Resource Manager deployments](../virtual-machines/windows/upload-generalized-managed.md) contains image preparation instructions in the **Prepare the VHD for upload** section.</span></span>
   * <span data-ttu-id="94734-112">Para imágenes de Linux, siga los pasos para preparar la imagen o use una imagen de Linux de Azure Stack existente como se describe en el artículo [Implementación de máquinas virtuales Linux en Azure Stack](azure-stack-linux.md).</span><span class="sxs-lookup"><span data-stu-id="94734-112">For Linux images, follow the steps to prepare the image or use an existing Azure Stack Linux image as described in the article [Deploy Linux virtual machines on Azure Stack](azure-stack-linux.md).</span></span>  

<span data-ttu-id="94734-113">Ahora, ejecute los pasos siguientes para agregar la imagen en Marketplace de Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="94734-113">Now run the following steps to add the image to the Azure Stack marketplace:</span></span>

1. <span data-ttu-id="94734-114">Importe los módulos Connect y ComputeAdmin:</span><span class="sxs-lookup"><span data-stu-id="94734-114">Import the Connect and ComputeAdmin modules:</span></span>
   
   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import the Connect and ComputeAdmin modules
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1
   ``` 

2. <span data-ttu-id="94734-115">Inicie sesión en el entorno de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="94734-115">Sign in to your Azure Stack environment.</span></span> <span data-ttu-id="94734-116">Ejecute el siguiente script en función de si su entorno de Azure Stack se implementó mediante el uso de AAD o AD FS (asegúrese de reemplazar el nombre del inquilino de AAD):</span><span class="sxs-lookup"><span data-stu-id="94734-116">Run the following script depending on if your Azure Stack environment is deployed by using AAD or AD FS (Make sure to replace the AAD tenant name):</span></span> 

   <span data-ttu-id="94734-117">a.</span><span class="sxs-lookup"><span data-stu-id="94734-117">a.</span></span> <span data-ttu-id="94734-118">**Azure Active Directory**, use el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="94734-118">**Azure Active Directory**, use the following cmdlet:</span></span>

   ```PowerShell
   # Create the Azure Stack cloud administrator's AzureRM environment by using the following cmdlet:
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

   <span data-ttu-id="94734-119">b.</span><span class="sxs-lookup"><span data-stu-id="94734-119">b.</span></span> <span data-ttu-id="94734-120">**Servicios de federación de Active Directory**, use el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="94734-120">**Active Directory Federation Services**, use the following cmdlet:</span></span>
    
   ```PowerShell
   # Create the Azure Stack cloud administrator's AzureRM environment by using the following cmdlet:
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
    
3. <span data-ttu-id="94734-121">Agregue la imagen de máquina virtual invocando el cmdlet `Add-AzsVMImage`.</span><span class="sxs-lookup"><span data-stu-id="94734-121">Add the VM image by invoking the `Add-AzsVMImage` cmdlet.</span></span> <span data-ttu-id="94734-122">En el cmdlet Add-AzsVMImage, especifique Windows o Linux como valor de osType.</span><span class="sxs-lookup"><span data-stu-id="94734-122">In the Add-AzsVMImage cmdlet, specify the osType as Windows or Linux.</span></span> <span data-ttu-id="94734-123">Incluya el publicador, oferta, SKU y versión de la imagen de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="94734-123">Include the publisher, offer, SKU, and version for the VM image.</span></span> <span data-ttu-id="94734-124">Consulte la sección [Parámetros](#parameters) para obtener información acerca de los parámetros permitidos.</span><span class="sxs-lookup"><span data-stu-id="94734-124">See the [Parameters](#parameters) section for information about the allowed parameters.</span></span> <span data-ttu-id="94734-125">Estos parámetros se utilizan en las plantillas de Azure Resource Manager para hacer referencia a la imagen de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="94734-125">These parameters are used by Azure Resource Manager templates to reference the VM image.</span></span> <span data-ttu-id="94734-126">A continuación se muestra un ejemplo de la invocación del script:</span><span class="sxs-lookup"><span data-stu-id="94734-126">Following is an example invocation of the script:</span></span>
     
     ```powershell
     Add-AzsVMImage `
       -publisher "Canonical" `
       -offer "UbuntuServer" `
       -sku "14.04.3-LTS" `
       -version "1.0.0" `
       -osType Linux `
       -osDiskLocalPath 'C:\Users\AzureStackAdmin\Desktop\UbuntuServer.vhd' `
     ```

<span data-ttu-id="94734-127">El comando hace lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="94734-127">The command does the following:</span></span>

* <span data-ttu-id="94734-128">Se autentica en el entorno de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="94734-128">Authenticates to the Azure Stack environment</span></span>
* <span data-ttu-id="94734-129">Carga el disco duro virtual local en una cuenta de almacenamiento temporal recién creada</span><span class="sxs-lookup"><span data-stu-id="94734-129">Uploads the local VHD to a newly created temporary storage account</span></span>
* <span data-ttu-id="94734-130">Agrega la imagen de la máquina virtual en el repositorio de imágenes de máquina virtual y</span><span class="sxs-lookup"><span data-stu-id="94734-130">Adds the VM image to the VM image repository and</span></span>
* <span data-ttu-id="94734-131">Crea un elemento de Marketplace</span><span class="sxs-lookup"><span data-stu-id="94734-131">Creates a Marketplace item</span></span>

<span data-ttu-id="94734-132">Para comprobar que el comando se ejecutó correctamente, vaya a Marketplace en el portal y, a continuación, compruebe que la imagen de máquina virtual está disponible en la categoría **Máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="94734-132">To verify that the command ran successfully, go to Marketplace in the portal, and then verify that the VM image is available in the **Virtual Machines** category.</span></span>

![Imagen de máquina virtual agregada correctamente](./media/azure-stack-add-vm-image/image5.PNG) 

## <a name="remove-a-vm-image-with-powershell"></a><span data-ttu-id="94734-134">Eliminación de una imagen de máquina virtual con PowerShell</span><span class="sxs-lookup"><span data-stu-id="94734-134">Remove a VM image with PowerShell</span></span>

<span data-ttu-id="94734-135">Cuando ya no necesite la imagen de máquina virtual que ha cargado anteriormente, puede eliminarla de Marketplace mediante el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="94734-135">When you no longer need the virtual machine image that you have uploaded earlier, you can delete it from the marketplace by using the following cmdlet:</span></span>

```powershell
Remove-AzsVMImage `
  -publisher "Canonical" `
  -offer "UbuntuServer" `
  -sku "14.04.3-LTS" `
  -version "1.0.0" `
```

## <a name="parameters"></a><span data-ttu-id="94734-136">parameters</span><span class="sxs-lookup"><span data-stu-id="94734-136">Parameters</span></span>

| <span data-ttu-id="94734-137">Parámetro</span><span class="sxs-lookup"><span data-stu-id="94734-137">Parameter</span></span> | <span data-ttu-id="94734-138">Descripción</span><span class="sxs-lookup"><span data-stu-id="94734-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="94734-139">**publisher**</span><span class="sxs-lookup"><span data-stu-id="94734-139">**publisher**</span></span> |<span data-ttu-id="94734-140">El segmento de nombre del publicador de la imagen de máquina virtual que utilizan los usuarios al implementar la imagen.</span><span class="sxs-lookup"><span data-stu-id="94734-140">The publisher name segment of the VM image that users use when deploying the image.</span></span> <span data-ttu-id="94734-141">Un ejemplo es 'Microsoft'.</span><span class="sxs-lookup"><span data-stu-id="94734-141">An example is ‘Microsoft’.</span></span> <span data-ttu-id="94734-142">No incluya un espacio u otros caracteres especiales en este campo.</span><span class="sxs-lookup"><span data-stu-id="94734-142">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="94734-143">**offer**</span><span class="sxs-lookup"><span data-stu-id="94734-143">**offer**</span></span> |<span data-ttu-id="94734-144">El segmento de nombre de la oferta de la imagen de máquina virtual que utilizan los usuarios al implementar la imagen de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="94734-144">The offer name segment of the VM Image that users use when deploying the VM image.</span></span> <span data-ttu-id="94734-145">Un ejemplo es 'WindowsServer'.</span><span class="sxs-lookup"><span data-stu-id="94734-145">An example is ‘WindowsServer’.</span></span> <span data-ttu-id="94734-146">No incluya un espacio u otros caracteres especiales en este campo.</span><span class="sxs-lookup"><span data-stu-id="94734-146">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="94734-147">**sku**</span><span class="sxs-lookup"><span data-stu-id="94734-147">**sku**</span></span> |<span data-ttu-id="94734-148">El segmento de nombre de SKU de la imagen de máquina virtual que utilizan los usuarios al implementar la imagen de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="94734-148">The SKU name segment of the VM Image that users use when deploying the VM image.</span></span> <span data-ttu-id="94734-149">Un ejemplo es 'Datacenter2016'.</span><span class="sxs-lookup"><span data-stu-id="94734-149">An example is ‘Datacenter2016’.</span></span> <span data-ttu-id="94734-150">No incluya un espacio u otros caracteres especiales en este campo.</span><span class="sxs-lookup"><span data-stu-id="94734-150">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="94734-151">**version**</span><span class="sxs-lookup"><span data-stu-id="94734-151">**version**</span></span> |<span data-ttu-id="94734-152">La versión de la imagen de máquina virtual que utilizan los usuarios al implementar la imagen de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="94734-152">The version of the VM Image that users use when deploying the VM image.</span></span> <span data-ttu-id="94734-153">Esta versión está en el formato *\#.\#.\#*.</span><span class="sxs-lookup"><span data-stu-id="94734-153">This version is in the format *\#.\#.\#*.</span></span> <span data-ttu-id="94734-154">Un ejemplo es '1.0.0'.</span><span class="sxs-lookup"><span data-stu-id="94734-154">An example is ‘1.0.0’.</span></span> <span data-ttu-id="94734-155">No incluya un espacio u otros caracteres especiales en este campo.</span><span class="sxs-lookup"><span data-stu-id="94734-155">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="94734-156">**osType**</span><span class="sxs-lookup"><span data-stu-id="94734-156">**osType**</span></span> |<span data-ttu-id="94734-157">El valor de osType de la imagen debe ser 'Windows' o 'Linux'.</span><span class="sxs-lookup"><span data-stu-id="94734-157">The osType of the image must be either ‘Windows’ or ‘Linux’.</span></span> |
| <span data-ttu-id="94734-158">**osDiskLocalPath**</span><span class="sxs-lookup"><span data-stu-id="94734-158">**osDiskLocalPath**</span></span> |<span data-ttu-id="94734-159">La ruta de acceso local al archivo VHD del disco de sistema operativo que se va a cargar como una imagen de máquina virtual en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="94734-159">The local path to the OS disk VHD that you are uploading as a VM image to Azure Stack.</span></span> |
| <span data-ttu-id="94734-160">**dataDiskLocalPaths**</span><span class="sxs-lookup"><span data-stu-id="94734-160">**dataDiskLocalPaths**</span></span> |<span data-ttu-id="94734-161">Una matriz opcional de las rutas de acceso locales para los discos de datos que se pueden cargar como parte de la imagen de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="94734-161">An optional array of the local paths for data disks that can be uploaded as part of the VM image.</span></span> |
| <span data-ttu-id="94734-162">**CreateGalleryItem**</span><span class="sxs-lookup"><span data-stu-id="94734-162">**CreateGalleryItem**</span></span> |<span data-ttu-id="94734-163">Una marca booleana que determina si se crea un elemento en Marketplace.</span><span class="sxs-lookup"><span data-stu-id="94734-163">A Boolean flag that determines whether to create an item in Marketplace.</span></span> <span data-ttu-id="94734-164">De forma predeterminada, se establece en true.</span><span class="sxs-lookup"><span data-stu-id="94734-164">By default, it is set to true.</span></span> |
| <span data-ttu-id="94734-165">**title**</span><span class="sxs-lookup"><span data-stu-id="94734-165">**title**</span></span> |<span data-ttu-id="94734-166">El nombre para mostrar del elemento de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="94734-166">The display name of Marketplace item.</span></span> <span data-ttu-id="94734-167">De forma predeterminada, se establece en Publicador-Oferta-SKU de la imagen de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="94734-167">By default, it is set to the Publisher-Offer-Sku of the VM image.</span></span> |
| <span data-ttu-id="94734-168">**descripción**</span><span class="sxs-lookup"><span data-stu-id="94734-168">**description**</span></span> |<span data-ttu-id="94734-169">La descripción del elemento de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="94734-169">The description of the Marketplace item.</span></span> |
| <span data-ttu-id="94734-170">**ubicación**</span><span class="sxs-lookup"><span data-stu-id="94734-170">**location**</span></span> |<span data-ttu-id="94734-171">La ubicación en la que debe publicarse la imagen de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="94734-171">The location to which the VM image should be published.</span></span> <span data-ttu-id="94734-172">De forma predeterminada, este valor se establece en local.</span><span class="sxs-lookup"><span data-stu-id="94734-172">By default, this value is set to local.</span></span>|
| <span data-ttu-id="94734-173">**osDiskBlobURI**</span><span class="sxs-lookup"><span data-stu-id="94734-173">**osDiskBlobURI**</span></span> |<span data-ttu-id="94734-174">Opcionalmente, este script también acepta un identificador URI de Blob Storage para disco de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="94734-174">Optionally, this script also accepts a Blob storage URI for osDisk.</span></span> |
| <span data-ttu-id="94734-175">**dataDiskBlobURIs**</span><span class="sxs-lookup"><span data-stu-id="94734-175">**dataDiskBlobURIs**</span></span> |<span data-ttu-id="94734-176">Opcionalmente, este script también acepta una matriz de identificadores URI de Blob Storage para agregar discos de datos a la imagen.</span><span class="sxs-lookup"><span data-stu-id="94734-176">Optionally, this script also accepts an array of Blob storage URIs for adding data disks to the image.</span></span> |

## <a name="add-a-vm-image-through-the-portal"></a><span data-ttu-id="94734-177">Agregación de una imagen de máquina virtual a través del portal</span><span class="sxs-lookup"><span data-stu-id="94734-177">Add a VM image through the portal</span></span>

> [!NOTE]
> <span data-ttu-id="94734-178">Este método requiere la creación del elemento de Marketplace por separado.</span><span class="sxs-lookup"><span data-stu-id="94734-178">This method requires creating the Marketplace item separately.</span></span>

<span data-ttu-id="94734-179">Un requisito de las imágenes es que se pueda hacer referencia a ellas con un identificador URI de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="94734-179">One requirement of images is that they can be referenced by a Blob storage URI.</span></span> <span data-ttu-id="94734-180">Prepare una imagen de sistema operativo Windows o Linux en formato VHD (no VHDX) y, a continuación, cargue la imagen en una cuenta de almacenamiento en Azure o Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="94734-180">Prepare a Windows or Linux operating system image in VHD format (not VHDX), and then upload the image to a storage account in Azure or Azure Stack.</span></span> <span data-ttu-id="94734-181">Si la imagen ya se ha cargado en Blob Storage en Azure o Azure Stack, puede omitir el paso 1.</span><span class="sxs-lookup"><span data-stu-id="94734-181">If your image is already uploaded to the Blob storage in Azure or Azure Stack, you can skip step1.</span></span>

1. <span data-ttu-id="94734-182">[Carga de una imagen de máquina virtual Windows en Azure para implementaciones de Resource Manager](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) o, para una imagen de Linux, siga las instrucciones descritas en el artículo [Implementación de máquinas virtuales Linux en Azure Stack](azure-stack-linux.md).</span><span class="sxs-lookup"><span data-stu-id="94734-182">[Upload a Windows VM image to Azure for Resource Manager deployments](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) or for a Linux image, follow the instructions described in the [Deploy Linux virtual machines on Azure Stack](azure-stack-linux.md) article.</span></span> <span data-ttu-id="94734-183">Debe comprender las siguientes consideraciones antes de cargar la imagen:</span><span class="sxs-lookup"><span data-stu-id="94734-183">You should understand the following considerations before you upload the image:</span></span>

   * <span data-ttu-id="94734-184">Es más eficaz cargar una imagen en Blob Storage de Azure Stack que en Azure Blob Storage porque se tarda menos tiempo en insertar la imagen en el repositorio de imágenes de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="94734-184">It's more efficient to upload an image to Azure Stack Blob storage than to Azure Blob storage because it takes less time to push the image to the Azure Stack image repository.</span></span> 
   
   * <span data-ttu-id="94734-185">Al cargar la [imagen de máquina virtual Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), asegúrese de sustituir el paso **Inicio de sesión en Azure** por el paso [Configuración del entorno de PowerShell del operador de Azure Stack](azure-stack-powershell-configure-admin.md).</span><span class="sxs-lookup"><span data-stu-id="94734-185">When uploading the [Windows VM image](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), make sure to substitute the **Login to Azure** step with the [Configure the Azure Stack operator's PowerShell environment](azure-stack-powershell-configure-admin.md)  step.</span></span>  

   * <span data-ttu-id="94734-186">Tome nota del identificador URI de Blob Storage donde se carga la imagen, que se encuentra en el siguiente formato:  *&lt;storageAccount&gt;/&lt;blobContainer&gt; / &lt;targetVHDName&gt;*.vhd</span><span class="sxs-lookup"><span data-stu-id="94734-186">Make a note of the Blob storage URI where you upload the image, which is in the following format: *&lt;storageAccount&gt;/&lt;blobContainer&gt;/&lt;targetVHDName&gt;*.vhd</span></span>

   * <span data-ttu-id="94734-187">Para hacer el blob accesible de forma anónima, vaya al contenedor de blob de la cuenta de almacenamiento donde cargó el disco duro virtual de la imagen de máquina virtual en **Blob,** y, a continuación, seleccione **Directiva de acceso**.</span><span class="sxs-lookup"><span data-stu-id="94734-187">To make the blob anonymously accessible, go to the storage account blob container where the VM image VHD was uploaded to **Blob,** and then select **Access Policy**.</span></span> <span data-ttu-id="94734-188">Si lo desea, puede generar una firma de acceso compartido para el contenedor e incluirla como parte del identificador URI del blob.</span><span class="sxs-lookup"><span data-stu-id="94734-188">If you want, you can instead generate a shared access signature for the container and include it as part of the blob URI.</span></span>

   ![Navegación a blobs de la cuenta de almacenamiento](./media/azure-stack-add-vm-image/image1.png)

   ![Establecimiento del acceso del blob en público](./media/azure-stack-add-vm-image/image2.png)

2. <span data-ttu-id="94734-191">Inicie sesión en la pila de Azure como un administrador de la nube > en el menú, haga clic en **más servicios** > **proveedores de recursos** > seleccione **proceso**  >  **Imágenes de máquina virtual** > **agregar**</span><span class="sxs-lookup"><span data-stu-id="94734-191">Sign in to Azure Stack as a cloud administrator > From the menu, click **More services** > **Resource Providers** > select  **Compute** > **VM images** > **Add**</span></span>

3. <span data-ttu-id="94734-192">En la hoja **Agregar una imagen de máquina virtual**, escriba el publicador, oferta, SKU y versión de la imagen de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="94734-192">On the **Add a VM Image** blade, enter the publisher, offer, SKU, and version of the virtual machine image.</span></span> <span data-ttu-id="94734-193">Estos segmentos del nombre hacen referencia a la imagen de máquina virtual en las plantillas de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="94734-193">These name segments refer to the VM image in Resource Manager templates.</span></span> <span data-ttu-id="94734-194">Asegúrese de seleccionar el valor de **osType** correctamente.</span><span class="sxs-lookup"><span data-stu-id="94734-194">Make sure to select the **osType** correctly.</span></span> <span data-ttu-id="94734-195">En **Identificador URI del blob del disco de sistema operativo**, escriba el identificador URI del blob donde se cargó la imagen y haga clic en **Crear** para empezar a crear la imagen de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="94734-195">For **OD Disk Blob URI**, enter the Blob URI where the image was uploaded and click **Create** to begin creating the VM Image.</span></span>
   
   ![Inicio de la creación de la imagen](./media/azure-stack-add-vm-image/image4.png)

   <span data-ttu-id="94734-197">Cuando la imagen se crea correctamente, el estado de la imagen de máquina virtual cambia a 'Correcto'.</span><span class="sxs-lookup"><span data-stu-id="94734-197">When the image is successfully created, the VM image status changes to ‘Succeeded’.</span></span>

4. <span data-ttu-id="94734-198">Para que la imagen de máquina virtual esté disponible con más facilidad para su consumo por el usuario en la interfaz de usuario, es mejor [crear un elemento de Marketplace](azure-stack-create-and-publish-marketplace-item.md).</span><span class="sxs-lookup"><span data-stu-id="94734-198">To make the virtual machine image more readily available for user consumption in the UI, it is best to [create a Marketplace item](azure-stack-create-and-publish-marketplace-item.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="94734-199">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="94734-199">Next steps</span></span>

[<span data-ttu-id="94734-200">Aprovisionamiento de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="94734-200">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)