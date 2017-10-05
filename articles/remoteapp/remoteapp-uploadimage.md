---
title: Carga de una imagen personalizada en Azure RemoteApp | Microsoft Docs
description: "Obtenga información sobre cómo cargar una imagen personalizada para RemoteApp de Azure"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 5a235fac88d6e95ea294bda197641108acb4a09f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a><span data-ttu-id="fce71-103">Carga de una imagen personalizada para RemoteApp de Azure</span><span class="sxs-lookup"><span data-stu-id="fce71-103">Upload a custom image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fce71-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="fce71-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="fce71-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="fce71-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="fce71-106">Ahora que ha creado la imagen de plantilla personalizada o que la actualizado con cambios, es necesario cargar esa imagen a la biblioteca de imágenes de Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fce71-106">Now that you have created your custom template image or have updated it with changes, you need to upload that image to your Azure RemoteApp image library.</span></span> <span data-ttu-id="fce71-107">Siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="fce71-107">Use these steps.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="fce71-108">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="fce71-108">Before you start</span></span>
1. <span data-ttu-id="fce71-109">Compruebe que la imagen personalizada cumple con los [requisitos de imagen](remoteapp-imagereqs.md) y los [requisitos de aplicación](remoteapp-appreqs.md).</span><span class="sxs-lookup"><span data-stu-id="fce71-109">Verify your custom image meets the [image requirements](remoteapp-imagereqs.md) and [application requirements](remoteapp-appreqs.md).</span></span>
2. <span data-ttu-id="fce71-110">Instale el [módulo de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fce71-110">Install the [Azure PowerShell module](/powershell/azure/overview).</span></span>

## <a name="step-by-step-on-how-to-upload-custom-image"></a><span data-ttu-id="fce71-111">Procedimiento paso a paso para cargar una imagen personalizada</span><span class="sxs-lookup"><span data-stu-id="fce71-111">Step by step on how to upload custom image</span></span>
1. <span data-ttu-id="fce71-112">Abra el Portal de administración de Azure y navegue a la página RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fce71-112">Open Azure Management Portal and navigate to the RemoteApp page.</span></span>
2. <span data-ttu-id="fce71-113">En la pestaña **Imágenes de plantilla**, haga clic en **Cargar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="fce71-113">On the **Template images** tab, click **Upload** at the bottom of the page.</span></span>
3. <span data-ttu-id="fce71-114">Escriba un nombre descriptivo para la imagen y especifique la ubicación de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fce71-114">Enter a friendly name for your image and specify the storage account location.</span></span> <span data-ttu-id="fce71-115">Asegúrese de que la ubicación es la misma que para la colección de RemoteApp o una ubicación donde desea crear una.</span><span class="sxs-lookup"><span data-stu-id="fce71-115">Ensure the location is the same location as your RemoteApp collection or a location where you want to create one.</span></span>
4. <span data-ttu-id="fce71-116">Cuando se le solicite, descargue el script a su equipo local.</span><span class="sxs-lookup"><span data-stu-id="fce71-116">When prompted, download the script to your local PC.</span></span>
5. <span data-ttu-id="fce71-117">Copie los parámetros de comando del cuadro de texto en el portapapeles.</span><span class="sxs-lookup"><span data-stu-id="fce71-117">Copy the command parameters in the text box to your clipboard.</span></span>
6. <span data-ttu-id="fce71-118">Abra una ventana de Windows PowerShell con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="fce71-118">Open an elevated Windows PowerShell window.</span></span>
7. <span data-ttu-id="fce71-119">Desde la ventana de Windows PowerShell con privilegios elevados, navegue al mismo directorio al que descargó el script.</span><span class="sxs-lookup"><span data-stu-id="fce71-119">From the elevated Windows PowerShell window, navigate to the same directory where you downloaded the script.</span></span>
8. <span data-ttu-id="fce71-120">Pegue el comando copiado y presione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="fce71-120">Paste the copied command and press **Enter**.</span></span>
   
   <span data-ttu-id="fce71-121">Comenzará el proceso de carga y la duración podría depender de muchos factores, incluida la velocidad de la red y el tamaño de la imagen.</span><span class="sxs-lookup"><span data-stu-id="fce71-121">The upload process will begin and duration may depend on many factors including your network speed and size of the image</span></span>
9. <span data-ttu-id="fce71-122">Si la carga no se realiza correctamente debido a una interrupción de la red o algún factor similar, siempre puede reanudar el proceso de carga que comenzó.</span><span class="sxs-lookup"><span data-stu-id="fce71-122">If your upload does not succeed because of network interruption or things like that, you can always resume the upload process you began.</span></span> <span data-ttu-id="fce71-123">Para reanudar una carga, ejecute nuevamente el script con la misma línea de comando.</span><span class="sxs-lookup"><span data-stu-id="fce71-123">To resume an upload, run the script again using the same command line.</span></span>

> [!WARNING]
> <span data-ttu-id="fce71-124">No modifique nunca el script de carga.</span><span class="sxs-lookup"><span data-stu-id="fce71-124">Never modify the upload script.</span></span> <span data-ttu-id="fce71-125">Se han implementado comprobaciones específicas para garantizar que la imagen cumple con los requisitos de imagen y los requisitos de aplicación.</span><span class="sxs-lookup"><span data-stu-id="fce71-125">Specific checks have been implemented to ensure that the image meets the image requirements and application requirements.</span></span>
> 
> 

## <a name="common-problems"></a><span data-ttu-id="fce71-126">Problemas comunes</span><span class="sxs-lookup"><span data-stu-id="fce71-126">Common problems</span></span>
* <span data-ttu-id="fce71-127">Asegúrese de que usa Windows PowerShell y no Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fce71-127">Make sure you use Windows PowerShell, not Azure PowerShell.</span></span> <span data-ttu-id="fce71-128">Debe instalar el módulo Azure PowerShell porque se necesitan ciertos módulos durante el proceso de carga.</span><span class="sxs-lookup"><span data-stu-id="fce71-128">You need to install the Azure PowerShell module because certain modules are needed during the upload process.</span></span>
* <span data-ttu-id="fce71-129">Nunca modifique el script: las validaciones existen para su comodidad.</span><span class="sxs-lookup"><span data-stu-id="fce71-129">Never alter the script, validations are there for your convenience.</span></span>
* <span data-ttu-id="fce71-130">Si el archivo vhd se bloquea durante la carga, cópielo o muévalo a una nueva ubicación e intente volver a cargarlo.</span><span class="sxs-lookup"><span data-stu-id="fce71-130">If the vhd file gets locked out during upload, copy the file or move it to a new location and attempt upload again.</span></span> <span data-ttu-id="fce71-131">Es posible que algunos procesos de Windows impidan la carga.</span><span class="sxs-lookup"><span data-stu-id="fce71-131">There might be some Windows process that is preventing upload.</span></span>  

