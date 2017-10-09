---
title: aaaUse Hola toocreate del Kit de herramientas de Marketplace y publicar elementos de marketplace | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooquickly crear elementos de marketplace con hello Kit de herramientas de publicación"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: ByronR
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/14/2017
ms.author: helaw
ms.openlocfilehash: c1cf9ad1da44787901297eec12faf2a3dea82a6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#  <a name="add-marketplace-items-using-publishing-tool"></a><span data-ttu-id="3a4aa-103">Agregar elementos de Marketplace con la herramienta de publicación</span><span class="sxs-lookup"><span data-stu-id="3a4aa-103">Add marketplace items using publishing tool</span></span>
<span data-ttu-id="3a4aa-104">Agregar el contenido toohello [Azure Marketplace de pila](azure-stack-marketplace.md) hace que su tooyou disponibles de soluciones y los inquilinos para la implementación.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-104">Adding your content toohello [Azure Stack Marketplace](azure-stack-marketplace.md) makes your solutions available tooyou and your tenants for deployment.</span></span>  <span data-ttu-id="3a4aa-105">Hola Kit de herramientas de Marketplace crea archivos de paquetes de Azure Marketplace (.azpkg) basados en plantillas del Administrador de recursos de Azure IaaS o extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-105">hello Marketplace Toolkit creates Azure Marketplace Packages (.azpkg) files based on your IaaS Azure Resource Manager templates or VM Extensions.</span></span>  <span data-ttu-id="3a4aa-106">También puede usar archivos de hello Kit de herramientas de Marketplace toopublish .azpkg, creado con la herramienta de Hola o mediante [manual](azure-stack-create-and-publish-marketplace-item.md) pasos.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-106">You can also use hello Marketplace Toolkit toopublish .azpkg files, either created with hello tool or using [manual](azure-stack-create-and-publish-marketplace-item.md) steps.</span></span>  <span data-ttu-id="3a4aa-107">En este tema le guía por descargar herramienta hello, creación de un elemento de marketplace basado en una plantilla de máquina virtual y, a continuación, publicar ese toohello elemento Azure Marketplace de pila.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-107">This topic guides you through downloading hello tool, creating a marketplace item based on a VM template, and then publishing that item toohello Azure Stack Marketplace.</span></span>     


## <a name="prerequisites"></a><span data-ttu-id="3a4aa-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3a4aa-108">Prerequisites</span></span>
 - <span data-ttu-id="3a4aa-109">Debe ejecutar el Kit de herramientas de hello en el host de la pila de Azure de Hola o tener [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) conectividad de la máquina de Hola donde se ejecuta la herramienta de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-109">You must run hello toolkit on hello Azure Stack host or have [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) connectivity from hello machine where you run hello tool.</span></span>

 - <span data-ttu-id="3a4aa-110">Descargar hello [plantillas de inicio rápido de Azure pila](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip) y extraer.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-110">Download hello [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip) and extract.</span></span>

 - <span data-ttu-id="3a4aa-111">Descargar hello [herramienta de empaquetado de la Galería de Azure](http://aka.ms/azurestackmarketplaceitem) (AzureGalleryPackage.exe).</span><span class="sxs-lookup"><span data-stu-id="3a4aa-111">Download hello [Azure Gallery Packaging tool](http://aka.ms/azurestackmarketplaceitem) (AzureGalleryPackage.exe).</span></span> 

 - <span data-ttu-id="3a4aa-112">Publicar toohello marketplace requiere iconos y un archivo en miniatura.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-112">Publishing toohello marketplace requires icons and a thumbnail file.</span></span>  <span data-ttu-id="3a4aa-113">Puede utilizar su propia o guardar hello [ejemplo](azure-stack-marketplace-publisher.md#support-files) archivos localmente en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-113">You can use your own, or save hello [sample](azure-stack-marketplace-publisher.md#support-files) files locally for this example.</span></span>

## <a name="download-hello-tool"></a><span data-ttu-id="3a4aa-114">Descargar la herramienta de Hola</span><span class="sxs-lookup"><span data-stu-id="3a4aa-114">Download hello tool</span></span>
<span data-ttu-id="3a4aa-115">Hello Kit de herramientas de Marketplace puede ser [descargado desde el repositorio de herramientas de la pila de Azure de hello](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="3a4aa-115">hello Marketplace Toolkit can be [downloaded from hello Azure Stack Tools repo](azure-stack-powershell-download.md).</span></span>


##  <a name="create-marketplace-items"></a><span data-ttu-id="3a4aa-116">Crear elementos de Marketplace</span><span class="sxs-lookup"><span data-stu-id="3a4aa-116">Create marketplace items</span></span>
<span data-ttu-id="3a4aa-117">En esta sección, utilice Hola Kit de herramientas de Marketplace toocreate un paquete de elemento de marketplace en formato .azpkg.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-117">In this section, you use hello Marketplace Toolkit toocreate a marketplace item package in .azpkg format.</span></span>  

### <a name="provide-marketplace-information-with-wizard"></a><span data-ttu-id="3a4aa-118">Proporcionar información de Marketplace con el Asistente</span><span class="sxs-lookup"><span data-stu-id="3a4aa-118">Provide marketplace information with wizard</span></span>
1. <span data-ttu-id="3a4aa-119">Ejecute hello Kit de herramientas de Marketplace desde una sesión de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3a4aa-119">Run hello Marketplace Toolkit from a PowerShell session:</span></span>
```PowerShell
    .\MarketplaceToolkit.ps1
```

2. <span data-ttu-id="3a4aa-120">Haga clic en hello **solución** ficha.  Esta pantalla acepta información sobre el elemento de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-120">Click hello **Solution** tab.  This screen accepts information about your marketplace item.</span></span> <span data-ttu-id="3a4aa-121">Escriba información sobre el elemento como se desee tooappear en marketplace Hola.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-121">Enter information about your item as you want it tooappear in hello marketplace.</span></span>  <span data-ttu-id="3a4aa-122">También puede especificar un [archivo de parámetros](azure-stack-marketplace-publisher.md#use-a-parameters-file) formulario de hello tooprepopulate.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-122">You can also specify a [parameters file](azure-stack-marketplace-publisher.md#use-a-parameters-file) tooprepopulate hello form.</span></span>  
    
    ![captura de pantalla de la primera pantalla del kit de herramientas de Marketplace](./media/azure-stack-marketplace-publisher/image7.png)
3. <span data-ttu-id="3a4aa-124">Haga clic en **Examinar** y seleccione un archivo de imagen para cada campo de icono y captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-124">Click **Browse** and select an image file for each icon and screenshot field.</span></span>  <span data-ttu-id="3a4aa-125">Puede utilizar sus propios iconos u Hola iconos de ejemplo Hola [archivos auxiliares](azure-stack-marketplace-publisher.md#support-files) sección.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-125">You can use your own icons, or hello sample icons in hello [support files](azure-stack-marketplace-publisher.md#support-files) section.</span></span>
4. <span data-ttu-id="3a4aa-126">Una vez que se rellenan todos los campos, seleccione "Vista previa de la solución" para una vista previa de la solución de hello dentro de hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-126">Once all fields are populated, select "Preview Solution" for a preview of hello solution within hello Marketplace.</span></span>  <span data-ttu-id="3a4aa-127">Puede revisar y editar texto hello, imágenes y captura de pantalla antes de hacer clic **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-127">You can revise and edit hello text, images, and screenshot before clicking **Next**.</span></span>  

### <a name="import-template-and-create-package"></a><span data-ttu-id="3a4aa-128">Importar la plantilla y crear el paquete</span><span class="sxs-lookup"><span data-stu-id="3a4aa-128">Import template and create package</span></span>
<span data-ttu-id="3a4aa-129">En esta sección, importar plantilla hello y trabajar con entradas de la solución.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-129">In this section, you import hello template and work with input for your solution.</span></span>

1.  <span data-ttu-id="3a4aa-130">Haga clic en **examinar** y seleccione hello *azuredeploy.json* desde la carpeta de 101-Simple-VM de Windows hello en hello descargar plantillas.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-130">Click **Browse** and select hello *azuredeploy.json* from hello 101-Simple-Windows-VM folder in hello downloaded templates.</span></span>

    ![captura de pantalla de la segunda pantalla del kit de herramientas de Marketplace](./media/azure-stack-marketplace-publisher/image8.png)
2.  <span data-ttu-id="3a4aa-132">Asistente para la implementación Hello se rellena una con un *básica* elementos de paso y entrada para cada parámetro especificado en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-132">hello Deployment Wizard is populated with a *Basic* step and input items for each parameter specified in hello template.</span></span>  <span data-ttu-id="3a4aa-133">Puede agregar pasos adicionales y mover entradas entre pasos.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-133">You can add additional steps and move inputs between steps.</span></span>  <span data-ttu-id="3a4aa-134">Por ejemplo, puede que quiera pasos “Configuración de front-end” y “Configuración de back-end” para la solución.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-134">As an example, you may want "Front-End Configuration" and "Back-End Configuration" steps for your solution.</span></span>
3.  <span data-ttu-id="3a4aa-135">Especifique Hola ruta de acceso tooAzureGalleryPackager.exe.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-135">Specify hello path tooAzureGalleryPackager.exe.</span></span>  
4.  <span data-ttu-id="3a4aa-136">Haga clic en **crear** y Hola Kit de herramientas de Marketplace empaqueta la solución en un archivo .azpkg.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-136">Click **Create** and hello Marketplace Toolkit packages your solution into an .azpkg file.</span></span>  <span data-ttu-id="3a4aa-137">Una vez que haya finalizado, el Asistente de hello muestra archivo de solución de tooyour de ruta de acceso de Hola y conceda a Hola toocontinue opción publicar su pila tooAzure de paquete.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-137">Once complete, hello wizard displays hello path tooyour solution file and give you hello option toocontinue publishing your package tooAzure Stack.</span></span>


## <a name="publish-marketplace-items"></a><span data-ttu-id="3a4aa-138">Publicar elementos de Marketplace</span><span class="sxs-lookup"><span data-stu-id="3a4aa-138">Publish marketplace items</span></span>
<span data-ttu-id="3a4aa-139">En esta sección, publicar Hola marketplace elemento tooyour Azure Marketplace de pila.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-139">In this section, you publish hello marketplace item tooyour Azure Stack Marketplace.</span></span>

![captura de pantalla de la primera pantalla del kit de herramientas de Marketplace](./media/azure-stack-marketplace-publisher/image9.png)

1.  <span data-ttu-id="3a4aa-141">Asistente de Hello requiere información toopublish la solución:</span><span class="sxs-lookup"><span data-stu-id="3a4aa-141">hello wizard requires information toopublish your solution:</span></span>
    
    |<span data-ttu-id="3a4aa-142">Campo</span><span class="sxs-lookup"><span data-stu-id="3a4aa-142">Field</span></span>|<span data-ttu-id="3a4aa-143">Descripción</span><span class="sxs-lookup"><span data-stu-id="3a4aa-143">Description</span></span>|
    |-----|-----|
    | <span data-ttu-id="3a4aa-144">Service Admin Name (Nombre del administrador de servicios)</span><span class="sxs-lookup"><span data-stu-id="3a4aa-144">Service Admin Name</span></span> | <span data-ttu-id="3a4aa-145">Cuenta del administrador del servicio</span><span class="sxs-lookup"><span data-stu-id="3a4aa-145">Service Administrator account.</span></span>  <span data-ttu-id="3a4aa-146">Ejemplo: ServiceAdmin@mydomain.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="3a4aa-146">Example:  ServiceAdmin@mydomain.onmicrosoft.com</span></span> |
    | <span data-ttu-id="3a4aa-147">Password</span><span class="sxs-lookup"><span data-stu-id="3a4aa-147">Password</span></span> | <span data-ttu-id="3a4aa-148">Contraseña de cuenta del administrador de servicios.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-148">Password for Service Administrator account.</span></span> |
    | <span data-ttu-id="3a4aa-149">Punto de conexión de API</span><span class="sxs-lookup"><span data-stu-id="3a4aa-149">API Endpoint</span></span> | <span data-ttu-id="3a4aa-150">Punto de conexión de Azure Resource Manager de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-150">Azure Stack Azure Resource Manager endpoint.</span></span>  <span data-ttu-id="3a4aa-151">Ejemplo: management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="3a4aa-151">Example: management.local.azurestack.external</span></span> |
2.  <span data-ttu-id="3a4aa-152">Haga clic en **publicar** y se muestra el registro de hello de publicación.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-152">Click **Publish** and hello publishing log is displayed.</span></span>
3.  <span data-ttu-id="3a4aa-153">Se está toodeploy ahora se puede el elemento publicado a través del portal de Azure pila Hola.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-153">You are now able toodeploy your published item via hello Azure Stack portal.</span></span>


## <a name="use-a-parameters-file"></a><span data-ttu-id="3a4aa-154">Usar un archivo de parámetros</span><span class="sxs-lookup"><span data-stu-id="3a4aa-154">Use a parameters file</span></span>
<span data-ttu-id="3a4aa-155">También puede utilizar un archivo toocomplete Hola marketplace elemento información de parámetros de.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-155">You can also use a parameters file toocomplete hello marketplace item information.</span></span>  

<span data-ttu-id="3a4aa-156">Hello Marketplace Kit de herramientas incluye un *solution.parameters.ps1* toocreate puede utilizar su propio archivo de parámetros.</span><span class="sxs-lookup"><span data-stu-id="3a4aa-156">hello Marketplace Toolkit includes a *solution.parameters.ps1* you can use toocreate your own parameters file.</span></span>


## <a name="support-files"></a><span data-ttu-id="3a4aa-157">Archivos auxiliares</span><span class="sxs-lookup"><span data-stu-id="3a4aa-157">Support files</span></span>
| <span data-ttu-id="3a4aa-158">Descripción</span><span class="sxs-lookup"><span data-stu-id="3a4aa-158">Description</span></span> | <span data-ttu-id="3a4aa-159">Muestra</span><span class="sxs-lookup"><span data-stu-id="3a4aa-159">Sample</span></span> |
| ----- | ----- |
| <span data-ttu-id="3a4aa-160">Icono .png de 40 × 40</span><span class="sxs-lookup"><span data-stu-id="3a4aa-160">40x40 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image1.png) |
| <span data-ttu-id="3a4aa-161">Icono .png de 90 × 90</span><span class="sxs-lookup"><span data-stu-id="3a4aa-161">90x90 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image2.png) |
| <span data-ttu-id="3a4aa-162">Icono .png de 115 × 115</span><span class="sxs-lookup"><span data-stu-id="3a4aa-162">115x115 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image3.png) |
| <span data-ttu-id="3a4aa-163">Icono .png de 255 × 115</span><span class="sxs-lookup"><span data-stu-id="3a4aa-163">255x115 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image4.png) |
| <span data-ttu-id="3a4aa-164">Vista en miniatura .png de 533 × 324</span><span class="sxs-lookup"><span data-stu-id="3a4aa-164">533x324 .png thumbnail</span></span> | ![](./media/azure-stack-marketplace-publisher/image5.png) |


