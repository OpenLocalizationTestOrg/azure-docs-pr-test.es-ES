---
title: aplicaciones de App-V aaaUsing con Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información acerca de cómo las aplicaciones de App-V toouse en Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="2dfed-103">Uso de aplicaciones App-V en RemoteApp de Azure</span><span class="sxs-lookup"><span data-stu-id="2dfed-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2dfed-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="2dfed-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="2dfed-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="2dfed-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="2dfed-106">Puede usar aplicaciones App-V en una colección híbrida de Azure RemoteApp, que requiera unión a dominio.</span><span class="sxs-lookup"><span data-stu-id="2dfed-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="2dfed-107">Antes de comenzar, asegúrese de cliente de App-V 5.1 de Hola de tooinstall seguro con las últimas actualizaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="2dfed-107">Before you get started, make sure tooinstall hello App-V 5.1 client with hello latest updates.</span></span> <span data-ttu-id="2dfed-108">Deberá toocreate un [imagen personalizada](remoteapp-create-custom-image.md) que incluye el cliente de App-V Hola.</span><span class="sxs-lookup"><span data-stu-id="2dfed-108">You will need toocreate a [custom image](remoteapp-create-custom-image.md) that includes hello App-V client.</span></span>  

<span data-ttu-id="2dfed-109">Es fácil toouse su infraestructura de App-V con Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="2dfed-109">It’s easy toouse your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="2dfed-110">Dado que una colección híbrida se implementa en una red virtual de Azure que tiene el controlador de dominio de acceso tooyour y hello las máquinas virtuales están unidos a un dominio, puede aprovechar su existente aplicación App-v infraestructura e implementación métodos tooeasyily host App-V en Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="2dfed-110">Since a hybrid collection is deployed into an Azure VNET that has access tooyour domain controller and hello VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods tooeasyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="2dfed-111">Estas son algunas consideraciones que debe tener en cuenta en función de tipo de Hola de implementación de App-V que tiene actualmente:</span><span class="sxs-lookup"><span data-stu-id="2dfed-111">Here are some considerations that you should be aware of based on hello type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="2dfed-112">Opciones de configuración</span><span class="sxs-lookup"><span data-stu-id="2dfed-112">Configuration options</span></span> |  | <span data-ttu-id="2dfed-113">Positive</span><span class="sxs-lookup"><span data-stu-id="2dfed-113">Positive</span></span> | <span data-ttu-id="2dfed-114">Negative</span><span class="sxs-lookup"><span data-stu-id="2dfed-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2dfed-115">Método de entrega</span><span class="sxs-lookup"><span data-stu-id="2dfed-115">Delivery method</span></span> |<span data-ttu-id="2dfed-116">Streaming (a petición)</span><span class="sxs-lookup"><span data-stu-id="2dfed-116">Streaming (on-demand)</span></span> |<span data-ttu-id="2dfed-117">Aplicación siempre es hello más reciente y actualizado</span><span class="sxs-lookup"><span data-stu-id="2dfed-117">App is always hello latest and fresh</span></span> |<span data-ttu-id="2dfed-118">Primera latencia</span><span class="sxs-lookup"><span data-stu-id="2dfed-118">First time latency</span></span> |
| <span data-ttu-id="2dfed-119">Montado</span><span class="sxs-lookup"><span data-stu-id="2dfed-119">Mounted</span></span> |<span data-ttu-id="2dfed-120">Más rápido; aplicación ya está presente en hello VM</span><span class="sxs-lookup"><span data-stu-id="2dfed-120">Fastest; app is already present on hello VM</span></span> |<span data-ttu-id="2dfed-121">Sobredimensionamiento: se usa el espacio de la imagen (límite de 127 GB)</span><span class="sxs-lookup"><span data-stu-id="2dfed-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="2dfed-122">Almacenamiento de ubicación de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="2dfed-122">App location storage</span></span> |<span data-ttu-id="2dfed-123">Contenido compartido</span><span class="sxs-lookup"><span data-stu-id="2dfed-123">Shared content</span></span> |<span data-ttu-id="2dfed-124">La aplicación se ejecuta en la memoria de la instancia de RemoteApp de Azure.</span><span class="sxs-lookup"><span data-stu-id="2dfed-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="2dfed-125">Come memoria y conexión buena toostreaming (archivo) del servidor donde reside la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="2dfed-125">Eats memory and good connection toostreaming (file) server where hello app resides</span></span> |
| <span data-ttu-id="2dfed-126">Disco (en caché)</span><span class="sxs-lookup"><span data-stu-id="2dfed-126">Disk (Cached)</span></span> |<span data-ttu-id="2dfed-127">Ejecución rápida</span><span class="sxs-lookup"><span data-stu-id="2dfed-127">Fast execution.</span></span> <span data-ttu-id="2dfed-128">La aplicación no depende de la disponibilidad del origen del contenido.</span><span class="sxs-lookup"><span data-stu-id="2dfed-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="2dfed-129">Sobredimensionamiento: se usa el espacio de la imagen (límite de 127 GB)</span><span class="sxs-lookup"><span data-stu-id="2dfed-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="2dfed-130">Destinatarios</span><span class="sxs-lookup"><span data-stu-id="2dfed-130">Targeting</span></span> |<span data-ttu-id="2dfed-131">Usuario</span><span class="sxs-lookup"><span data-stu-id="2dfed-131">User</span></span> |<span data-ttu-id="2dfed-132">Requiere la infraestructura de App-V independiente completa.</span><span class="sxs-lookup"><span data-stu-id="2dfed-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="2dfed-133">Global (equipo)</span><span class="sxs-lookup"><span data-stu-id="2dfed-133">Global (machine)</span></span> |<span data-ttu-id="2dfed-134">Publique previamente o seleccione el destino mediante el servidor de publicación</span><span class="sxs-lookup"><span data-stu-id="2dfed-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="2dfed-135">Necesita tooupdate la imagen de Azure si desea que tooupdate Hola aplicación (enorme).</span><span class="sxs-lookup"><span data-stu-id="2dfed-135">Need tooupdate your Azure image if you want tooupdate hello app (huge).</span></span> <span data-ttu-id="2dfed-136">Ocupa espacio en la imagen.</span><span class="sxs-lookup"><span data-stu-id="2dfed-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="2dfed-137">Después de crear la imagen personalizada y su colección híbrida, publicar la aplicación, asignar a usuarios y disfrute de las aplicaciones de App-V existentes hospedadas en Azure RemoteApp entregado tooany dispositivo en cualquier parte.</span><span class="sxs-lookup"><span data-stu-id="2dfed-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered tooany device anywhere.</span></span>

