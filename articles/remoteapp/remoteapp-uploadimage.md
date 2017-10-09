---
title: aaaUpload una imagen personalizada para Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooupload personalizado de la imagen de Azure RemoteApp"
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
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a><span data-ttu-id="c85a0-103">Carga de una imagen personalizada para RemoteApp de Azure</span><span class="sxs-lookup"><span data-stu-id="c85a0-103">Upload a custom image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c85a0-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="c85a0-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="c85a0-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="c85a0-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="c85a0-106">Ahora que ha creado la imagen de plantilla personalizada o haya actualizado con los cambios, debe tooupload esa biblioteca de imágenes de imagen tooyour Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="c85a0-106">Now that you have created your custom template image or have updated it with changes, you need tooupload that image tooyour Azure RemoteApp image library.</span></span> <span data-ttu-id="c85a0-107">Siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="c85a0-107">Use these steps.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="c85a0-108">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="c85a0-108">Before you start</span></span>
1. <span data-ttu-id="c85a0-109">Compruebe la imagen personalizada cumple hello [requisitos de la imagen](remoteapp-imagereqs.md) y [requisitos de la aplicación](remoteapp-appreqs.md).</span><span class="sxs-lookup"><span data-stu-id="c85a0-109">Verify your custom image meets hello [image requirements](remoteapp-imagereqs.md) and [application requirements](remoteapp-appreqs.md).</span></span>
2. <span data-ttu-id="c85a0-110">Instalar hello [módulo Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c85a0-110">Install hello [Azure PowerShell module](/powershell/azure/overview).</span></span>

## <a name="step-by-step-on-how-tooupload-custom-image"></a><span data-ttu-id="c85a0-111">Paso a paso sobre cómo imagen personalizada tooupload</span><span class="sxs-lookup"><span data-stu-id="c85a0-111">Step by step on how tooupload custom image</span></span>
1. <span data-ttu-id="c85a0-112">Abra el Portal de administración de Azure y desplácese toohello página de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="c85a0-112">Open Azure Management Portal and navigate toohello RemoteApp page.</span></span>
2. <span data-ttu-id="c85a0-113">En hello **imágenes de plantilla** , haga clic en **cargar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="c85a0-113">On hello **Template images** tab, click **Upload** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="c85a0-114">Escriba un nombre descriptivo para la imagen y especifique la ubicación de la cuenta de hello almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c85a0-114">Enter a friendly name for your image and specify hello storage account location.</span></span> <span data-ttu-id="c85a0-115">Asegúrese de ubicación de hello es hello misma ubicación que la colección RemoteApp o una ubicación donde desea toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="c85a0-115">Ensure hello location is hello same location as your RemoteApp collection or a location where you want toocreate one.</span></span>
4. <span data-ttu-id="c85a0-116">Cuando se le solicite, descargue Hola script tooyour PC local.</span><span class="sxs-lookup"><span data-stu-id="c85a0-116">When prompted, download hello script tooyour local PC.</span></span>
5. <span data-ttu-id="c85a0-117">Copiar parámetros del comando hello en el Portapapeles de tooyour de cuadro de texto de Hola.</span><span class="sxs-lookup"><span data-stu-id="c85a0-117">Copy hello command parameters in hello text box tooyour clipboard.</span></span>
6. <span data-ttu-id="c85a0-118">Abra una ventana de Windows PowerShell con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="c85a0-118">Open an elevated Windows PowerShell window.</span></span>
7. <span data-ttu-id="c85a0-119">De hello elevado de ventana de Windows PowerShell, vaya toohello mismo directorio donde descargó el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="c85a0-119">From hello elevated Windows PowerShell window, navigate toohello same directory where you downloaded hello script.</span></span>
8. <span data-ttu-id="c85a0-120">Hola pegar copia el comando y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="c85a0-120">Paste hello copied command and press **Enter**.</span></span>
   
   <span data-ttu-id="c85a0-121">se iniciará el proceso de carga de Hola y duración puede depender de muchos factores como la velocidad de la red y el tamaño de imagen de Hola</span><span class="sxs-lookup"><span data-stu-id="c85a0-121">hello upload process will begin and duration may depend on many factors including your network speed and size of hello image</span></span>
9. <span data-ttu-id="c85a0-122">Si la carga no se realiza correctamente debido a la interrupción de la red o cosas como esta, puede reanudar siempre que se inició el proceso de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="c85a0-122">If your upload does not succeed because of network interruption or things like that, you can always resume hello upload process you began.</span></span> <span data-ttu-id="c85a0-123">tooresume una carga, ejecutar script de Hola utilizando de nuevo Hola misma línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="c85a0-123">tooresume an upload, run hello script again using hello same command line.</span></span>

> [!WARNING]
> <span data-ttu-id="c85a0-124">No modifique nunca script de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="c85a0-124">Never modify hello upload script.</span></span> <span data-ttu-id="c85a0-125">Comprobaciones específicas han sido implementado tooensure que Hola imagen cumple los requisitos de imagen hello y requisitos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c85a0-125">Specific checks have been implemented tooensure that hello image meets hello image requirements and application requirements.</span></span>
> 
> 

## <a name="common-problems"></a><span data-ttu-id="c85a0-126">Problemas comunes</span><span class="sxs-lookup"><span data-stu-id="c85a0-126">Common problems</span></span>
* <span data-ttu-id="c85a0-127">Asegúrese de que usa Windows PowerShell y no Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c85a0-127">Make sure you use Windows PowerShell, not Azure PowerShell.</span></span> <span data-ttu-id="c85a0-128">Necesita módulo de PowerShell de Azure de hello tooinstall porque algunos módulos se necesitan durante el proceso de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="c85a0-128">You need tooinstall hello Azure PowerShell module because certain modules are needed during hello upload process.</span></span>
* <span data-ttu-id="c85a0-129">Nunca modifican script hello, validaciones existen para su comodidad.</span><span class="sxs-lookup"><span data-stu-id="c85a0-129">Never alter hello script, validations are there for your convenience.</span></span>
* <span data-ttu-id="c85a0-130">Si el archivo de disco duro virtual de hello obtiene bloqueada durante la carga, copie el archivo hello o tooa nueva carga de ubicación e intente volver a moverlo.</span><span class="sxs-lookup"><span data-stu-id="c85a0-130">If hello vhd file gets locked out during upload, copy hello file or move it tooa new location and attempt upload again.</span></span> <span data-ttu-id="c85a0-131">Es posible que algunos procesos de Windows impidan la carga.</span><span class="sxs-lookup"><span data-stu-id="c85a0-131">There might be some Windows process that is preventing upload.</span></span>  

