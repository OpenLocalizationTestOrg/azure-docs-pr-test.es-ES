---
title: "Introducción al administrador de datos de Azure StorSimple aaaMicrosoft | Documentos de Microsoft"
description: "Proporciona información general de hello servicio de administrador de datos de StorSimple (vista previa privada)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a><span data-ttu-id="1d726-103">Información general sobre el servicio StorSimple Data Manager (versión preliminar privada)</span><span class="sxs-lookup"><span data-stu-id="1d726-103">StorSimple Data Manager overview (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="1d726-104">Información general</span><span class="sxs-lookup"><span data-stu-id="1d726-104">Overview</span></span>

<span data-ttu-id="1d726-105">StorSimple de Microsoft Azure es una solución de almacenamiento de nube híbrida que direcciones Hola complejidades de los datos no estructurados que suelen estar asociadas con recursos compartidos de archivos.</span><span class="sxs-lookup"><span data-stu-id="1d726-105">Microsoft Azure StorSimple is a hybrid cloud storage solution that addresses hello complexities of unstructured data commonly associated with file shares.</span></span> <span data-ttu-id="1d726-106">StorSimple usa almacenamiento en la nube como solución local de una extensión de hello y automáticamente de capas de datos a través de un almacenamiento local hello y almacenamiento en la nube.</span><span class="sxs-lookup"><span data-stu-id="1d726-106">StorSimple uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="1d726-107">Integra la protección de datos, con local e instantáneas en la nube, elimina la necesidad de Hola de una infraestructura de almacenamiento desorganizados.</span><span class="sxs-lookup"><span data-stu-id="1d726-107">Integrated data protection, with local and cloud snapshots, eliminates hello need for a sprawling storage infrastructure.</span></span> <span data-ttu-id="1d726-108">Archivado y recuperación ante desastres también es sin problemas con la nube de hello actúa como una ubicación fuera del sitio.</span><span class="sxs-lookup"><span data-stu-id="1d726-108">Archival and disaster recovery is also seamless with hello cloud acting as an offsite location.</span></span>

<span data-ttu-id="1d726-109">Servicios de transformación de datos de Hola que estamos incorporando en este documento, se permite tooseamlessly acceso hello StorSimple datos en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d726-109">hello data transformation service that we are introducing in this document, allows you tooseamlessly access hello StorSimple data in hello cloud.</span></span> <span data-ttu-id="1d726-110">Este servicio proporciona datos de las API tooextract de StorSimple y presentar tooother Azure servicios en formatos que pueden utilizarse con facilidad.</span><span class="sxs-lookup"><span data-stu-id="1d726-110">This service provides APIs tooextract data from StorSimple and present it tooother Azure services in formats that can be readily consumed.</span></span> <span data-ttu-id="1d726-111">formatos de Hello admitidos en esta versión preliminar son blobs de Azure y los activos de servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="1d726-111">hello formats supported in this preview are Azure blobs and Azure Media Services assets.</span></span> <span data-ttu-id="1d726-112">Esta transformación permite tooeasily conectar servicios como datos de toooperate de servicios multimedia de Azure, HDInsight de Azure, aprendizaje automático de Azure y búsqueda de Azure en el dispositivo de StorSimple 8000 series local.</span><span class="sxs-lookup"><span data-stu-id="1d726-112">This transformation enables you tooeasily wire up services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search toooperate data on StorSimple 8000 series on-premises device.</span></span>

<span data-ttu-id="1d726-113">A continuación se muestra un diagrama de bloques de alto nivel que lo ilustra.</span><span class="sxs-lookup"><span data-stu-id="1d726-113">A high-level block diagram illustrating this is shown below.</span></span>

![Diagrama de alto nivel](./media//storsimple-data-manager-overview/high-level-diagram.png)

<span data-ttu-id="1d726-115">En este documento se explica cómo puede suscribirse a una versión preliminar privada de este servicio.</span><span class="sxs-lookup"><span data-stu-id="1d726-115">This document explains how you can sign up for a private preview of this service.</span></span> <span data-ttu-id="1d726-116">También se explica cómo puede usar esta aplicación de servicio toowrite que usan datos de StorSimple y otros servicios de Azure en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d726-116">It also explains how you can use this service toowrite applications that use StorSimple data and other Azure services in hello cloud.</span></span>

## <a name="sign-up-for-data-manager-preview"></a><span data-ttu-id="1d726-117">Suscripción para una versión preliminar de Data Manager</span><span class="sxs-lookup"><span data-stu-id="1d726-117">Sign up for Data Manager preview</span></span>
<span data-ttu-id="1d726-118">Antes de registrarse para el servicio de administrador de datos de hello, revise Hola siguiendo los requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="1d726-118">Before you sign up for hello Data Manager service, review hello following prerequisites.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="1d726-119">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1d726-119">Prerequisites</span></span>

<span data-ttu-id="1d726-120">En este ejercicio se supone que dispone de:</span><span class="sxs-lookup"><span data-stu-id="1d726-120">This exercise assumes that you have</span></span>
* <span data-ttu-id="1d726-121">una suscripción a Azure activa</span><span class="sxs-lookup"><span data-stu-id="1d726-121">an active Azure subscription.</span></span>
* <span data-ttu-id="1d726-122">acceso tooa registrado el dispositivo de StorSimple 8000 series</span><span class="sxs-lookup"><span data-stu-id="1d726-122">access tooa registered StorSimple 8000 series device</span></span>
* <span data-ttu-id="1d726-123">todos los Hola claves asociadas con el dispositivo de la serie StorSimple 8000 Hola.</span><span class="sxs-lookup"><span data-stu-id="1d726-123">all hello keys associated with hello StorSimple 8000 series device.</span></span>

### <a name="sign-up"></a><span data-ttu-id="1d726-124">Suscripción</span><span class="sxs-lookup"><span data-stu-id="1d726-124">Sign up</span></span>

<span data-ttu-id="1d726-125">Hola, Administrador de datos de StorSimple está en vista previa privada.</span><span class="sxs-lookup"><span data-stu-id="1d726-125">hello StorSimple Data Manager is in private preview.</span></span> <span data-ttu-id="1d726-126">Lleve a cabo Hola siguiendo los pasos toosign para disfrutar de una vista previa privada de este servicio:</span><span class="sxs-lookup"><span data-stu-id="1d726-126">Perform hello following steps toosign up for a private preview of this service:</span></span>

1.  <span data-ttu-id="1d726-127">Inicie sesión en hello portal de Azure con la extensión de administrador de datos de StorSimple de hello en: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span><span class="sxs-lookup"><span data-stu-id="1d726-127">Log into hello Azure portal with hello StorSimple Data Manager extension at: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span></span> <span data-ttu-id="1d726-128">Utilice la toolog las credenciales de Azure en.</span><span class="sxs-lookup"><span data-stu-id="1d726-128">Use your Azure credentials toolog in.</span></span>

2.  <span data-ttu-id="1d726-129">Haga clic en hello  **+**  toocreate icono un servicio.</span><span class="sxs-lookup"><span data-stu-id="1d726-129">Click hello **+** icon toocreate a service.</span></span> <span data-ttu-id="1d726-130">Haga clic en **almacenamiento** y, a continuación, haga clic en **vea todos los** en la hoja de Hola que se abre.</span><span class="sxs-lookup"><span data-stu-id="1d726-130">Click **Storage** and then click **See All** in hello blade that opens up.</span></span>

    ![Buscar icono de StorSimple Data Manager](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. <span data-ttu-id="1d726-132">Verá el icono de administrador de datos de StorSimple de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d726-132">You see hello StorSimple Data Manager icon.</span></span>

    ![Seleccionar icono de StorSimple Data Manager](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. <span data-ttu-id="1d726-134">Haga clic en el icono de StorSimple Data Manager y, después, en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="1d726-134">Click StorSimple Data Manager icon and then click **Create**.</span></span> <span data-ttu-id="1d726-135">Seleccione la suscripción de Hola que desee tooenable de vista previa privada de hello y, a continuación, haga clic en **suscribirme!**</span><span class="sxs-lookup"><span data-stu-id="1d726-135">Pick hello subscription that you want tooenable for hello private preview and then click **Sign me up!**</span></span>

    ![Suscribirme](./media/storsimple-data-manager-overview/sign-me-up.png)

5. <span data-ttu-id="1d726-137">Este modo envía una solicitud tooonboard.</span><span class="sxs-lookup"><span data-stu-id="1d726-137">This sends a request tooonboard you.</span></span> <span data-ttu-id="1d726-138">Dicha incorporación se realizará lo antes posible.</span><span class="sxs-lookup"><span data-stu-id="1d726-138">We will onboard you as soon as possible.</span></span> <span data-ttu-id="1d726-139">Una vez habilitada la suscripción, ya se puede crear un servicio StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="1d726-139">After your subscription is enabled, you can create a StorSimple Data Manager service.</span></span>

6. <span data-ttu-id="1d726-140">tooeasily tener acceso a servicio de administrador de datos de StorSimple de hello, haga clic en toopin de icono de estrella de Hola tooyour favoritos.</span><span class="sxs-lookup"><span data-stu-id="1d726-140">tooeasily access hello StorSimple Data Manager service, click hello star icon toopin it tooyour favorites.</span></span>

    ![Acceder a StorSimple Data Manager](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a><span data-ttu-id="1d726-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1d726-142">Next steps</span></span>

<span data-ttu-id="1d726-143">[Usar los datos de interfaz de usuario de administrador de datos de StorSimple tootransform](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="1d726-143">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
