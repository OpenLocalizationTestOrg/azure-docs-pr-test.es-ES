---
title: requisitos de imagen de RemoteApp aaaAzure | Documentos de Microsoft
description: "Obtenga información acerca de los requisitos de Hola para crear toobe de imágenes que se usa con Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a><span data-ttu-id="bded5-103">Requisitos para las imágenes Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="bded5-103">Requirements for Azure RemoteApp images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bded5-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="bded5-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="bded5-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="bded5-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="bded5-106">RemoteApp de Azure utiliza un toohost de imagen de Windows Server 2012 R2 en todos los programas de Hola que desee tooshare con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="bded5-106">Azure RemoteApp uses a Windows Server 2012 R2 image toohost all hello programs that you want tooshare with your users.</span></span> <span data-ttu-id="bded5-107">toocreate una imagen personalizada, puede empezar con una imagen existente o [crear una nueva](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="bded5-107">toocreate a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span></span>

> [!TIP]
> <span data-ttu-id="bded5-108">¿Sabía que su proporciona de suscripción de Azure RemoteApp en que acceso tooa de imagen de Windows Server 2012 R2 Hola Galería de máquinas virtuales de Azure puede usar toocreate en su propia imagen de plantilla?</span><span class="sxs-lookup"><span data-stu-id="bded5-108">Did you know that your Azure RemoteApp subscription gives you access tooa Windows Server 2012 R2 image in hello Azure VM gallery that you can use toocreate your own template image?</span></span> <span data-ttu-id="bded5-109">[Compruébelo](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="bded5-109">[Check it out](remoteapp-image-on-azurevm.md).</span></span>  
> 
> 

<span data-ttu-id="bded5-110">requisitos de Hello para la imagen de Hola que se pueden cargar para su uso con Azure RemoteApp son:</span><span class="sxs-lookup"><span data-stu-id="bded5-110">hello requirements for hello image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="bded5-111">Las aplicaciones personalizadas no almacenan datos localmente en la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="bded5-111">Custom applications don’t store data locally on hello image.</span></span> <span data-ttu-id="bded5-112">Estas imágenes no tienen estado y solo deben contener aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bded5-112">These images are stateless and should only contain applications.</span></span>
* <span data-ttu-id="bded5-113">imagen de Hello no contiene datos que se pueden perder.</span><span class="sxs-lookup"><span data-stu-id="bded5-113">hello image does not contain data that can be lost.</span></span>
* <span data-ttu-id="bded5-114">tamaño de la imagen de Hello debe ser un múltiplo de MB.</span><span class="sxs-lookup"><span data-stu-id="bded5-114">hello image size should be a multiple of MBs.</span></span> <span data-ttu-id="bded5-115">Si intentas tooupload una imagen que no es un múltiplo exacto, se producirá un error en la carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="bded5-115">If you try tooupload an image that is not an exact multiple, hello upload will fail.</span></span>
* <span data-ttu-id="bded5-116">tamaño de la imagen de Hello debe ser 127 GB o menor.</span><span class="sxs-lookup"><span data-stu-id="bded5-116">hello image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="bded5-117">Debe estar en un archivo VHD (los archivos VHDX no se admiten actualmente).</span><span class="sxs-lookup"><span data-stu-id="bded5-117">It must be on a VHD file (VHDX files are not currently supported).</span></span>
* <span data-ttu-id="bded5-118">Hola VHD no debe ser una máquina virtual de generación 2.</span><span class="sxs-lookup"><span data-stu-id="bded5-118">hello VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="bded5-119">Hola VHD puede ser de tamaño fijo o de expansión dinámica.</span><span class="sxs-lookup"><span data-stu-id="bded5-119">hello VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="bded5-120">Un disco duro virtual de expansión dinámica se recomienda porque toma menos tooAzure tooupload de tiempo que un archivo de disco duro virtual de tamaño fijo.</span><span class="sxs-lookup"><span data-stu-id="bded5-120">A dynamically expanding VHD is recommended because it takes less time tooupload tooAzure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="bded5-121">disco de Hello debe inicializarse con estilo de partición de registro de arranque maestro (MBR) Hola.</span><span class="sxs-lookup"><span data-stu-id="bded5-121">hello disk must be initialized using hello Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="bded5-122">no se admite el estilo de partición GPT (tabla) de particiones GUID Hola.</span><span class="sxs-lookup"><span data-stu-id="bded5-122">hello GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="bded5-123">Hola VHD debe contener una única instalación de Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="bded5-123">hello VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="bded5-124">Puede contener varios volúmenes, pero uno de ellos con una instalación de Windows.</span><span class="sxs-lookup"><span data-stu-id="bded5-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="bded5-125">deben estar instalados el rol de Host de sesión de escritorio remoto (RDSH) de Hola y la característica experiencia de escritorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="bded5-125">hello Remote Desktop Session Host (RDSH) role and hello Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="bded5-126">rol de agente de conexión a Escritorio remoto de Hello debe *no* instalarse.</span><span class="sxs-lookup"><span data-stu-id="bded5-126">hello Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="bded5-127">Sistema de archivos cifrados (EFS) de Hello debe deshabilitarse.</span><span class="sxs-lookup"><span data-stu-id="bded5-127">hello Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="bded5-128">Hello imagen debe estar preparada con Sysprep mediante parámetros de hello **/oobe /generalize /shutdown** (no usar hello **/mode: VM** parámetro).</span><span class="sxs-lookup"><span data-stu-id="bded5-128">hello image must be SYSPREPed using hello parameters **/oobe /generalize /shutdown** (DO NOT use hello **/mode:vm** parameter).</span></span>
* <span data-ttu-id="bded5-129">No se admite la carga de su VHD desde una cadena de instantáneas.</span><span class="sxs-lookup"><span data-stu-id="bded5-129">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="bded5-130">Consulte [Creación de una imagen de Azure RemoteApp](remoteapp-imageoptions.md) para obtener más información sobre la creación de imágenes para Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bded5-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span></span>

