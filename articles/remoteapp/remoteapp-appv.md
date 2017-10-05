---
title: Uso de aplicaciones de App-V con Azure RemoteApp| Microsoft Docs
description: "Obtenga información sobre cómo usar aplicaciones de App-V en Azure RemoteApp."
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
ms.openlocfilehash: e55bb8db83c04025c46b383a9ebbef4399178116
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="8d873-103">Uso de aplicaciones App-V en RemoteApp de Azure</span><span class="sxs-lookup"><span data-stu-id="8d873-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8d873-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="8d873-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8d873-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="8d873-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8d873-106">Puede usar aplicaciones App-V en una colección híbrida de Azure RemoteApp, que requiera unión a dominio.</span><span class="sxs-lookup"><span data-stu-id="8d873-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="8d873-107">Antes de empezar, asegúrese de instalar el cliente de App-V 5.1 con las actualizaciones más recientes.</span><span class="sxs-lookup"><span data-stu-id="8d873-107">Before you get started, make sure to install the App-V 5.1 client with the latest updates.</span></span> <span data-ttu-id="8d873-108">Deberá crear una [imagen personalizada](remoteapp-create-custom-image.md) que incluya el cliente de App-V.</span><span class="sxs-lookup"><span data-stu-id="8d873-108">You will need to create a [custom image](remoteapp-create-custom-image.md) that includes the App-V client.</span></span>  

<span data-ttu-id="8d873-109">Es fácil de usar su infraestructura de App-V existente con Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8d873-109">It’s easy to use your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="8d873-110">Puesto que se implementa una colección híbrida en una red virtual de Azure que tiene acceso a su controlador de dominio y las máquinas virtuales están unidas a un dominio, puede aprovechar sus métodos de infraestructura e implementación de App-v existentes para hospedar fácilmente la aplicación de App-V en Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8d873-110">Since a hybrid collection is deployed into an Azure VNET that has access to your domain controller and the VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods to easyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="8d873-111">Estas son algunas consideraciones que deben tenerse en cuenta según el tipo de implementación de App-V que tiene actualmente:</span><span class="sxs-lookup"><span data-stu-id="8d873-111">Here are some considerations that you should be aware of based on the type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="8d873-112">Opciones de configuración</span><span class="sxs-lookup"><span data-stu-id="8d873-112">Configuration options</span></span> |  | <span data-ttu-id="8d873-113">Positive</span><span class="sxs-lookup"><span data-stu-id="8d873-113">Positive</span></span> | <span data-ttu-id="8d873-114">Negative</span><span class="sxs-lookup"><span data-stu-id="8d873-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8d873-115">Método de entrega</span><span class="sxs-lookup"><span data-stu-id="8d873-115">Delivery method</span></span> |<span data-ttu-id="8d873-116">Streaming (a petición)</span><span class="sxs-lookup"><span data-stu-id="8d873-116">Streaming (on-demand)</span></span> |<span data-ttu-id="8d873-117">La aplicación siempre es la más reciente y actualizada.</span><span class="sxs-lookup"><span data-stu-id="8d873-117">App is always the latest and fresh</span></span> |<span data-ttu-id="8d873-118">Primera latencia</span><span class="sxs-lookup"><span data-stu-id="8d873-118">First time latency</span></span> |
| <span data-ttu-id="8d873-119">Montado</span><span class="sxs-lookup"><span data-stu-id="8d873-119">Mounted</span></span> |<span data-ttu-id="8d873-120">Más rápido; la aplicación ya está presente en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8d873-120">Fastest; app is already present on the VM</span></span> |<span data-ttu-id="8d873-121">Sobredimensionamiento: se usa el espacio de la imagen (límite de 127 GB)</span><span class="sxs-lookup"><span data-stu-id="8d873-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="8d873-122">Almacenamiento de ubicación de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="8d873-122">App location storage</span></span> |<span data-ttu-id="8d873-123">Contenido compartido</span><span class="sxs-lookup"><span data-stu-id="8d873-123">Shared content</span></span> |<span data-ttu-id="8d873-124">La aplicación se ejecuta en la memoria de la instancia de RemoteApp de Azure.</span><span class="sxs-lookup"><span data-stu-id="8d873-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="8d873-125">Consume memoria y una buena conexión al servidor (archivo) de streaming en el que se encuentra la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8d873-125">Eats memory and good connection to streaming (file) server where the app resides</span></span> |
| <span data-ttu-id="8d873-126">Disco (en caché)</span><span class="sxs-lookup"><span data-stu-id="8d873-126">Disk (Cached)</span></span> |<span data-ttu-id="8d873-127">Ejecución rápida</span><span class="sxs-lookup"><span data-stu-id="8d873-127">Fast execution.</span></span> <span data-ttu-id="8d873-128">La aplicación no depende de la disponibilidad del origen del contenido.</span><span class="sxs-lookup"><span data-stu-id="8d873-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="8d873-129">Sobredimensionamiento: se usa el espacio de la imagen (límite de 127 GB)</span><span class="sxs-lookup"><span data-stu-id="8d873-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="8d873-130">Destinatarios</span><span class="sxs-lookup"><span data-stu-id="8d873-130">Targeting</span></span> |<span data-ttu-id="8d873-131">Usuario</span><span class="sxs-lookup"><span data-stu-id="8d873-131">User</span></span> |<span data-ttu-id="8d873-132">Requiere la infraestructura de App-V independiente completa.</span><span class="sxs-lookup"><span data-stu-id="8d873-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="8d873-133">Global (equipo)</span><span class="sxs-lookup"><span data-stu-id="8d873-133">Global (machine)</span></span> |<span data-ttu-id="8d873-134">Publique previamente o seleccione el destino mediante el servidor de publicación</span><span class="sxs-lookup"><span data-stu-id="8d873-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="8d873-135">Debe actualizar la imagen de Azure si desea actualizar la aplicación (enorme).</span><span class="sxs-lookup"><span data-stu-id="8d873-135">Need to update your Azure image if you want to update the app (huge).</span></span> <span data-ttu-id="8d873-136">Ocupa espacio en la imagen.</span><span class="sxs-lookup"><span data-stu-id="8d873-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="8d873-137">Después de crear su imagen personalizada y colección híbrida, publique su aplicación, asigne usuarios y disfrute de sus aplicaciones de App-V existentes hospedadas en Azure RemoteApp entregadas a cualquier dispositivo en cualquier lugar.</span><span class="sxs-lookup"><span data-stu-id="8d873-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered to any device anywhere.</span></span>

