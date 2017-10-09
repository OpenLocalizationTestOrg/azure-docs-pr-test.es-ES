---
title: "aaaManage los contenedores de volúmenes de StorSimple | Documentos de Microsoft"
description: "Explica cómo puede usar hello StorSimple Manager página tooadd contenedores de volúmenes de servicio, modificar o eliminación un contenedor de volúmenes."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 1c64ce75-1fd3-4d3b-9304-d4dc0fc2b069
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 9b29536e0072306e53ac92bacca78a13d932c2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="d5d07-103">Utilizar contenedores de volúmenes de StorSimple de hello StorSimple Manager servicio toomanage</span><span class="sxs-lookup"><span data-stu-id="d5d07-103">Use hello StorSimple Manager service toomanage StorSimple volume containers</span></span>
## <a name="overview"></a><span data-ttu-id="d5d07-104">Información general</span><span class="sxs-lookup"><span data-stu-id="d5d07-104">Overview</span></span>
<span data-ttu-id="d5d07-105">Este tutorial le explica cómo toouse Hola toocreate de servicio de StorSimple Manager y administrar contenedores de volúmenes de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d5d07-105">This tutorial explains how toouse hello StorSimple Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="d5d07-106">En un dispositivo Microsoft Azure StorSimple, los contenedores de volúmenes contienen uno o varios volúmenes que comparten la configuración de cuentas de almacenamiento, cifrado y consumo de ancho de banda.</span><span class="sxs-lookup"><span data-stu-id="d5d07-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="d5d07-107">Un dispositivo puede tener varios contenedores de volúmenes para todos sus volúmenes.</span><span class="sxs-lookup"><span data-stu-id="d5d07-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="d5d07-108">Un contenedor de volúmenes tiene Hola siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="d5d07-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="d5d07-109">**Volúmenes** : Hola en niveles o anclado localmente los volúmenes de StorSimple que se encuentran dentro del contenedor de volúmenes de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5d07-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> <span data-ttu-id="d5d07-110">Un contenedor de volúmenes puede contener too256 volúmenes de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d5d07-110">A volume container may contain up too256 StorSimple volumes.</span></span>
* <span data-ttu-id="d5d07-111">**Cifrado** : una clave de cifrado que se puede definir para cada contenedor de volúmenes.</span><span class="sxs-lookup"><span data-stu-id="d5d07-111">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="d5d07-112">Esta clave se utiliza para cifrar los datos de Hola que se envían desde el dispositivo de StorSimple toohello de la nube.</span><span class="sxs-lookup"><span data-stu-id="d5d07-112">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="d5d07-113">Se utiliza una clave de grado militar AES-256 bits con clave de hello escrito por el usuario.</span><span class="sxs-lookup"><span data-stu-id="d5d07-113">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="d5d07-114">toosecure los datos, se recomienda habilitar siempre el cifrado de almacenamiento en nube.</span><span class="sxs-lookup"><span data-stu-id="d5d07-114">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="d5d07-115">**Cuenta de almacenamiento** : Hola cuenta de almacenamiento que es el proveedor de servicios de almacenamiento de nube tooyour vinculado.</span><span class="sxs-lookup"><span data-stu-id="d5d07-115">**Storage account** – hello storage account that is linked tooyour cloud storage service provider.</span></span> <span data-ttu-id="d5d07-116">Todos los volúmenes de Hola que residen en un contenedor de volúmenes comparten esta cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d5d07-116">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="d5d07-117">Puede elegir una cuenta de almacenamiento de una lista existente o crear una nueva cuenta al crear el contenedor de volúmenes de hello y, a continuación, especifique las credenciales de acceso de Hola para esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="d5d07-117">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="d5d07-118">**Ancho de banda en la nube** : Hola ancho de banda consumido por dispositivo de hello cuando se envía datos de hello de dispositivo de hello toohello en la nube.</span><span class="sxs-lookup"><span data-stu-id="d5d07-118">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="d5d07-119">Puede aplicar un control del ancho de banda especificando un valor entre 1 y 1000 Mbps al definir este contenedor.</span><span class="sxs-lookup"><span data-stu-id="d5d07-119">You can enforce a bandwidth control by specifying a value between 1 and 1000 Mbps when you define this container.</span></span> <span data-ttu-id="d5d07-120">Si desea Hola dispositivo tooconsume ancho de banda disponible en todos los, establezca este campo tooUnlimited.</span><span class="sxs-lookup"><span data-stu-id="d5d07-120">If you want hello device tooconsume all available bandwidth, set this field tooUnlimited.</span></span> <span data-ttu-id="d5d07-121">También puede crear y aplicar un ancho de banda tooallocate del plantilla de ancho de banda basada en programación.</span><span class="sxs-lookup"><span data-stu-id="d5d07-121">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

![Página Contenedores de volúmenes](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

<span data-ttu-id="d5d07-123">Este procedimientos siguientes explican cómo toouse Hola StorSimple **contenedores de volúmenes** hello toocomplete de página después de las operaciones comunes:</span><span class="sxs-lookup"><span data-stu-id="d5d07-123">This following procedures explain how toouse hello StorSimple **Volume containers** page toocomplete hello following common operations:</span></span>

* <span data-ttu-id="d5d07-124">Agregar un contenedor de volúmenes</span><span class="sxs-lookup"><span data-stu-id="d5d07-124">Add a volume container</span></span> 
* <span data-ttu-id="d5d07-125">Modificar un contenedor de volúmenes</span><span class="sxs-lookup"><span data-stu-id="d5d07-125">Modify a volume container</span></span> 
* <span data-ttu-id="d5d07-126">Eliminar un contenedor de volúmenes</span><span class="sxs-lookup"><span data-stu-id="d5d07-126">Delete a volume container</span></span> 

## <a name="add-a-volume-container"></a><span data-ttu-id="d5d07-127">Agregar un contenedor de volúmenes</span><span class="sxs-lookup"><span data-stu-id="d5d07-127">Add a volume container</span></span>
<span data-ttu-id="d5d07-128">Realizar Hola siguiendo los pasos tooadd un contenedor de volúmenes.</span><span class="sxs-lookup"><span data-stu-id="d5d07-128">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="d5d07-129">Modificar un contenedor de volúmenes</span><span class="sxs-lookup"><span data-stu-id="d5d07-129">Modify a volume container</span></span>
<span data-ttu-id="d5d07-130">Realizar Hola siguiendo los pasos toomodify un contenedor de volúmenes.</span><span class="sxs-lookup"><span data-stu-id="d5d07-130">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="d5d07-131">Eliminar un contenedor de volúmenes</span><span class="sxs-lookup"><span data-stu-id="d5d07-131">Delete a volume container</span></span>
<span data-ttu-id="d5d07-132">Los contenedores de volúmenes contienen volúmenes.</span><span class="sxs-lookup"><span data-stu-id="d5d07-132">A volume container has volumes within it.</span></span> <span data-ttu-id="d5d07-133">Se puede eliminar solo si primero se eliminan todos los volúmenes de hello contenidos en ella.</span><span class="sxs-lookup"><span data-stu-id="d5d07-133">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="d5d07-134">Realizar Hola siguiendo los pasos toodelete un contenedor de volúmenes.</span><span class="sxs-lookup"><span data-stu-id="d5d07-134">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="d5d07-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d5d07-135">Next steps</span></span>
* <span data-ttu-id="d5d07-136">Obtenga más información sobre la [administración de volúmenes de StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="d5d07-136">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span> 
* <span data-ttu-id="d5d07-137">Obtenga más información sobre [utilizando Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d5d07-137">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

