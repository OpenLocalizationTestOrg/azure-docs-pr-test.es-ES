---
title: Requisitos de imagen de Azure RemoteApp | Microsoft Docs
description: "Obtenga información sobre los requisitos para crear imágenes que se usarán con Azure RemoteApp"
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
ms.openlocfilehash: 75b0f8d6b25a80f11002b683152cfb294cbb68bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a><span data-ttu-id="18cdd-103">Requisitos para las imágenes Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="18cdd-103">Requirements for Azure RemoteApp images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="18cdd-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="18cdd-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="18cdd-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="18cdd-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="18cdd-106">Azure RemoteApp usa una imagen de Windows Server 2012 R2 para hospedar todos los programas que desea compartir con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="18cdd-106">Azure RemoteApp uses a Windows Server 2012 R2 image to host all the programs that you want to share with your users.</span></span> <span data-ttu-id="18cdd-107">Para crear una imagen personalizada, puede comenzar con una imagen existente o [crear una nueva](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="18cdd-107">To create a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span></span>

> [!TIP]
> <span data-ttu-id="18cdd-108">¿Sabía que la suscripción de Azure RemoteApp le permite acceder a una imagen de Windows Server 2012 R2 en la galería de máquinas virtuales de Azure, y que puede usarla para crear su propia imagen de plantilla?</span><span class="sxs-lookup"><span data-stu-id="18cdd-108">Did you know that your Azure RemoteApp subscription gives you access to a Windows Server 2012 R2 image in the Azure VM gallery that you can use to create your own template image?</span></span> <span data-ttu-id="18cdd-109">[Compruébelo](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="18cdd-109">[Check it out](remoteapp-image-on-azurevm.md).</span></span>  
> 
> 

<span data-ttu-id="18cdd-110">Los requisitos para la imagen que se pueden cargar para usarse con RemoteApp de Azure son:</span><span class="sxs-lookup"><span data-stu-id="18cdd-110">The requirements for the image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="18cdd-111">Las aplicaciones personalizadas no almacenan datos de manera local en la imagen.</span><span class="sxs-lookup"><span data-stu-id="18cdd-111">Custom applications don’t store data locally on the image.</span></span> <span data-ttu-id="18cdd-112">Estas imágenes no tienen estado y solo deben contener aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="18cdd-112">These images are stateless and should only contain applications.</span></span>
* <span data-ttu-id="18cdd-113">La imagen no contiene datos que se puedan perder.</span><span class="sxs-lookup"><span data-stu-id="18cdd-113">The image does not contain data that can be lost.</span></span>
* <span data-ttu-id="18cdd-114">El tamaño de la imagen debe ser un múltiplo de MB.</span><span class="sxs-lookup"><span data-stu-id="18cdd-114">The image size should be a multiple of MBs.</span></span> <span data-ttu-id="18cdd-115">Si se intenta cargar una imagen que no es un múltiplo exacto, la carga no se realizará.</span><span class="sxs-lookup"><span data-stu-id="18cdd-115">If you try to upload an image that is not an exact multiple, the upload will fail.</span></span>
* <span data-ttu-id="18cdd-116">El tamaño de imagen debe ser de 127 GB o menos.</span><span class="sxs-lookup"><span data-stu-id="18cdd-116">The image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="18cdd-117">Debe estar en un archivo VHD (los archivos VHDX no se admiten actualmente).</span><span class="sxs-lookup"><span data-stu-id="18cdd-117">It must be on a VHD file (VHDX files are not currently supported).</span></span>
* <span data-ttu-id="18cdd-118">El disco duro virtual no debe ser una máquina virtual de generación 2.</span><span class="sxs-lookup"><span data-stu-id="18cdd-118">The VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="18cdd-119">El archivo VHD puede ser de tamaño fijo o expandirse dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="18cdd-119">The VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="18cdd-120">Se recomienda un archivo VHD que se expanda dinámicamente porque tarda menos tiempo en cargarse en Azure que un archivo VHD de tamaño fijo.</span><span class="sxs-lookup"><span data-stu-id="18cdd-120">A dynamically expanding VHD is recommended because it takes less time to upload to Azure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="18cdd-121">El disco se debe inicializar usando el estilo de particiones Registro de arranque maestro (MBR, Master Boot Record).</span><span class="sxs-lookup"><span data-stu-id="18cdd-121">The disk must be initialized using the Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="18cdd-122">El estilo de particiones de tabla de particiones GUID (GPT) no se admite.</span><span class="sxs-lookup"><span data-stu-id="18cdd-122">The GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="18cdd-123">El archivo VHD debe contener una sola instalación de Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="18cdd-123">The VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="18cdd-124">Puede contener varios volúmenes, pero uno de ellos con una instalación de Windows.</span><span class="sxs-lookup"><span data-stu-id="18cdd-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="18cdd-125">El rol Host de sesión de Escritorio remoto (RDSH, Remote Desktop Session Host) y la característica Experiencia de escritorio deben estar instalados.</span><span class="sxs-lookup"><span data-stu-id="18cdd-125">The Remote Desktop Session Host (RDSH) role and the Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="18cdd-126">El rol Agente de conexión a Escritorio remoto *no* debe instalarse.</span><span class="sxs-lookup"><span data-stu-id="18cdd-126">The Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="18cdd-127">El Sistema de cifrado de archivos (EFS, Encrypting File System) debe estar instalado.</span><span class="sxs-lookup"><span data-stu-id="18cdd-127">The Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="18cdd-128">La imagen debe estar preparada con sysprep con los parámetros **/oobe /generalize /shutdown** (No USE el parámetro **/mode:vm**).</span><span class="sxs-lookup"><span data-stu-id="18cdd-128">The image must be SYSPREPed using the parameters **/oobe /generalize /shutdown** (DO NOT use the **/mode:vm** parameter).</span></span>
* <span data-ttu-id="18cdd-129">No se admite la carga de su VHD desde una cadena de instantáneas.</span><span class="sxs-lookup"><span data-stu-id="18cdd-129">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="18cdd-130">Consulte [Creación de una imagen de Azure RemoteApp](remoteapp-imageoptions.md) para obtener más información sobre la creación de imágenes para Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="18cdd-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span></span>

