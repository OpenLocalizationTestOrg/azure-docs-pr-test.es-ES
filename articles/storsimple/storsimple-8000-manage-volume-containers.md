---
title: "aaaManage los contenedores de volúmenes de StorSimple en el dispositivo de la serie StorSimple 8000 Hola | Documentos de Microsoft"
description: "Explica cómo puede usar Hola Administrador de dispositivos de StorSimple contenedores de volúmenes de servicio página tooadd, modificar o eliminación un contenedor de volúmenes."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="f1955-103">Utilizar contenedores de volúmenes de StorSimple de toomanage servicio de administrador de dispositivos de StorSimple de Hola</span><span class="sxs-lookup"><span data-stu-id="f1955-103">Use hello StorSimple Device Manager service toomanage StorSimple volume containers</span></span>

## <a name="overview"></a><span data-ttu-id="f1955-104">Información general</span><span class="sxs-lookup"><span data-stu-id="f1955-104">Overview</span></span>
<span data-ttu-id="f1955-105">Este tutorial le explica cómo toouse Hola toocreate de servicio de administrador de dispositivos de StorSimple y administrar contenedores de volúmenes de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f1955-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="f1955-106">En un dispositivo Microsoft Azure StorSimple, los contenedores de volúmenes contienen uno o varios volúmenes que comparten la configuración de cuentas de almacenamiento, cifrado y consumo de ancho de banda.</span><span class="sxs-lookup"><span data-stu-id="f1955-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="f1955-107">Un dispositivo puede tener varios contenedores de volúmenes para todos sus volúmenes.</span><span class="sxs-lookup"><span data-stu-id="f1955-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="f1955-108">Un contenedor de volúmenes tiene Hola siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="f1955-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="f1955-109">**Volúmenes** : Hola en niveles o anclado localmente los volúmenes de StorSimple que se encuentran dentro del contenedor de volúmenes de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1955-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> 
* <span data-ttu-id="f1955-110">**Cifrado** : una clave de cifrado que se puede definir para cada contenedor de volúmenes.</span><span class="sxs-lookup"><span data-stu-id="f1955-110">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="f1955-111">Esta clave se utiliza para cifrar los datos de Hola que se envían desde el dispositivo de StorSimple toohello de la nube.</span><span class="sxs-lookup"><span data-stu-id="f1955-111">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="f1955-112">Se utiliza una clave de grado militar AES-256 bits con clave de hello escrito por el usuario.</span><span class="sxs-lookup"><span data-stu-id="f1955-112">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="f1955-113">toosecure los datos, se recomienda habilitar siempre el cifrado de almacenamiento en nube.</span><span class="sxs-lookup"><span data-stu-id="f1955-113">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="f1955-114">**Cuenta de almacenamiento** : Hola cuenta de almacenamiento de Azure que sea utilizado toostore Hola datos.</span><span class="sxs-lookup"><span data-stu-id="f1955-114">**Storage account** – hello Azure storage account that is used toostore hello data.</span></span> <span data-ttu-id="f1955-115">Todos los volúmenes de Hola que residen en un contenedor de volúmenes comparten esta cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f1955-115">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="f1955-116">Puede elegir una cuenta de almacenamiento de una lista existente o crear una nueva cuenta al crear el contenedor de volúmenes de hello y, a continuación, especifique las credenciales de acceso de Hola para esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="f1955-116">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="f1955-117">**Ancho de banda en la nube** : Hola ancho de banda consumido por dispositivo de hello cuando se envía datos de hello de dispositivo de hello toohello en la nube.</span><span class="sxs-lookup"><span data-stu-id="f1955-117">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="f1955-118">Puede aplicar un control del ancho de banda especificando un valor entre 1 y 1000 Mbps al definir este contenedor.</span><span class="sxs-lookup"><span data-stu-id="f1955-118">You can enforce a bandwidth control by specifying a value between 1 Mbps and 1,000 Mbps when you create this container.</span></span> <span data-ttu-id="f1955-119">Si desea Hola dispositivo tooconsume ancho de banda disponible, establezca este campo demasiado**Unlimited**.</span><span class="sxs-lookup"><span data-stu-id="f1955-119">If you want hello device tooconsume all available bandwidth, set this field too**Unlimited**.</span></span> <span data-ttu-id="f1955-120">También puede crear y aplicar un ancho de banda tooallocate del plantilla de ancho de banda basada en programación.</span><span class="sxs-lookup"><span data-stu-id="f1955-120">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

<span data-ttu-id="f1955-121">Hello procedimientos siguientes explican cómo toouse Hola StorSimple **contenedores de volúmenes** Hola de hoja toocomplete las siguientes operaciones comunes:</span><span class="sxs-lookup"><span data-stu-id="f1955-121">hello following procedures explain how toouse hello StorSimple **Volume containers** blade toocomplete hello following common operations:</span></span>

* <span data-ttu-id="f1955-122">Agregar un contenedor de volúmenes</span><span class="sxs-lookup"><span data-stu-id="f1955-122">Add a volume container</span></span>
* <span data-ttu-id="f1955-123">Modificar un contenedor de volúmenes</span><span class="sxs-lookup"><span data-stu-id="f1955-123">Modify a volume container</span></span>
* <span data-ttu-id="f1955-124">Eliminar un contenedor de volúmenes</span><span class="sxs-lookup"><span data-stu-id="f1955-124">Delete a volume container</span></span>

## <a name="add-a-volume-container"></a><span data-ttu-id="f1955-125">Agregar un contenedor de volúmenes</span><span class="sxs-lookup"><span data-stu-id="f1955-125">Add a volume container</span></span>
<span data-ttu-id="f1955-126">Realizar Hola siguiendo los pasos tooadd un contenedor de volúmenes.</span><span class="sxs-lookup"><span data-stu-id="f1955-126">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="f1955-127">Modificar un contenedor de volúmenes</span><span class="sxs-lookup"><span data-stu-id="f1955-127">Modify a volume container</span></span>
<span data-ttu-id="f1955-128">Realizar Hola siguiendo los pasos toomodify un contenedor de volúmenes.</span><span class="sxs-lookup"><span data-stu-id="f1955-128">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="f1955-129">Eliminar un contenedor de volúmenes</span><span class="sxs-lookup"><span data-stu-id="f1955-129">Delete a volume container</span></span>
<span data-ttu-id="f1955-130">Los contenedores de volúmenes contienen volúmenes.</span><span class="sxs-lookup"><span data-stu-id="f1955-130">A volume container has volumes within it.</span></span> <span data-ttu-id="f1955-131">Se puede eliminar solo si primero se eliminan todos los volúmenes de hello contenidos en ella.</span><span class="sxs-lookup"><span data-stu-id="f1955-131">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="f1955-132">Realizar Hola siguiendo los pasos toodelete un contenedor de volúmenes.</span><span class="sxs-lookup"><span data-stu-id="f1955-132">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="f1955-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f1955-133">Next steps</span></span>
* <span data-ttu-id="f1955-134">Obtenga más información sobre la [administración de volúmenes de StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="f1955-134">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span> 
* <span data-ttu-id="f1955-135">Obtenga más información sobre [utilizando Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f1955-135">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

