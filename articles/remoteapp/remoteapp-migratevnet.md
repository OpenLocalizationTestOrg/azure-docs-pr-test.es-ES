---
title: aaaHow toomigrate desde una red virtual de Azure de RemoteApp VNET tooan | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomigrate desde una red virtual de Azure de RemoteApp VNET tooan"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: c0f8617556c6f1e33eca8322febf67ff33937ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-a-hybrid-collection-from-a-remoteapp-vnet-tooan-azure-vnet"></a><span data-ttu-id="f234d-103">¿Cómo toomigrate una colección híbrida de una red virtual de Azure de RemoteApp VNET tooan</span><span class="sxs-lookup"><span data-stu-id="f234d-103">How toomigrate a hybrid collection from a RemoteApp VNET tooan Azure VNET</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f234d-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="f234d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f234d-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="f234d-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f234d-106">¡Buenas noticias!</span><span class="sxs-lookup"><span data-stu-id="f234d-106">Good news!</span></span> <span data-ttu-id="f234d-107">Hemos habilitado toodeploy colecciones de RemoteApp híbrida directamente en sus existentes redes virtuales de Azure (redes virtuales) en lugar de crear redes virtuales específicos de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f234d-107">We have enabled you toodeploy hybrid RemoteApp collections directly into your existing Azure virtual networks (VNETs) instead of creating RemoteApp-specific VNETs.</span></span> <span data-ttu-id="f234d-108">Esto le permite aprovechar las ventajas del programa Hola a las características más recientes de red virtual (por ejemplo, ExpressRoute) y proporcionar servicios de Azure a su tooother de acceso híbrido colecciones directa a la red y máquinas virtuales implementadas toothat red virtual.</span><span class="sxs-lookup"><span data-stu-id="f234d-108">This lets you take advantage of hello latest VNET features (like ExpressRoute) and give your hybrid collections direct network access tooother Azure services and virtual machines deployed toothat VNET.</span></span>  <span data-ttu-id="f234d-109">(Esto le permite disfrutar de un mejor rendimiento y mayor facilidad de configuración con respecto a las instalaciones de red virtual a red virtual).</span><span class="sxs-lookup"><span data-stu-id="f234d-109">(This gets you better performance and easier setup than VNET-to-VNET configurations).</span></span>

<span data-ttu-id="f234d-110">Supongamos que ya ha creado una colección de RemoteApp híbrida denominada *OriginalCollection* con una red virtual de RemoteApp llamada *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="f234d-110">Let’s say that you’ve already created a hybrid RemoteApp collection called *OriginalCollection* with a RemoteApp VNET called *RemoteAppVNET*.</span></span> <span data-ttu-id="f234d-111">Presentamos Hola pasos toomigrate tooa nueva red virtual de Azure denominado *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="f234d-111">Here are hello steps toomigrate it tooa new Azure VNET called *AzureVNET*.</span></span>

1. <span data-ttu-id="f234d-112">En hello **redes** ficha hello [portal de administración de](http://manage.windowsazure.com/), crear una red virtual denominada *AzureVNET*con Hola la misma ubicación, la configuración de DNS y el espacio de direcciones (para al menos uno Hola *AzureVNET* subredes) que utilizó para *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="f234d-112">On hello **Networks** tab in hello [management portal](http://manage.windowsazure.com/), create a VNET called *AzureVNET*, using hello same location, DNS configuration, and address space (for at least one of hello *AzureVNET* subnets) as you used for *RemoteAppVNET*.</span></span>
2. <span data-ttu-id="f234d-113">Configurar *AzureVNET* tooeither hospedar o debe tener la implementación de Active Directory de toohello de conectividad de red que *OriginalCollection* está unido a un dominio a.</span><span class="sxs-lookup"><span data-stu-id="f234d-113">Configure *AzureVNET* tooeither host or have network connectivity toohello Active Directory deployment that *OriginalCollection* is domain joined to.</span></span>
3. <span data-ttu-id="f234d-114">En hello **RemoteApps** ficha, cree una nueva colección de RemoteApp denominada *nueva colección*.</span><span class="sxs-lookup"><span data-stu-id="f234d-114">On hello **RemoteApps** tab, create a new RemoteApp collection called *New Collection*.</span></span> <span data-ttu-id="f234d-115">(Hola de uso **crear con red virtual** opción, no **creación rápida**.)</span><span class="sxs-lookup"><span data-stu-id="f234d-115">(Use hello **Create with VNET** option, not **Quick Create**.)</span></span>
4. <span data-ttu-id="f234d-116">Configurar *NewCollection* toobe implementado subred tooa en *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="f234d-116">Configure *NewCollection* toobe deployed tooa subnet in *AzureVNET*.</span></span>
5. <span data-ttu-id="f234d-117">Configurar *NewCollection* toouse Hola misma imagen e información de unión de dominio que utilizó para *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="f234d-117">Configure *NewCollection* toouse hello same image and domain join information as you used for *OriginalCollection*.</span></span>
6. <span data-ttu-id="f234d-118">Después de unas horas, *NewCollection* aparecerá en la lista de colecciones con un estado activo.</span><span class="sxs-lookup"><span data-stu-id="f234d-118">After a few hours, *NewCollection* will show up in your collection list with an Active state.</span></span>

<span data-ttu-id="f234d-119">Ahora, si no necesita toomigrate cualquier información de usuario de hello original colección toohello nueva colección, siga estos pasos a continuación:</span><span class="sxs-lookup"><span data-stu-id="f234d-119">Now, if you DON’T need toomigrate any user information from hello original collection toohello new collection, do these steps next:</span></span>

1. <span data-ttu-id="f234d-120">Elimine *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="f234d-120">Delete *OriginalCollection*.</span></span>
2. <span data-ttu-id="f234d-121">Elimine *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="f234d-121">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="f234d-122">¡Y ya está!</span><span class="sxs-lookup"><span data-stu-id="f234d-122">And, you’re done!</span></span>

<span data-ttu-id="f234d-123">Como alternativa, si necesita información de usuario de toomigrate de hello original colección toohello nueva colección, siga estos pasos a continuación:</span><span class="sxs-lookup"><span data-stu-id="f234d-123">Alternately, if you DO need toomigrate user information from hello original collection toohello new collection, do these steps next:</span></span>

1. <span data-ttu-id="f234d-124">Enviar un correo electrónico demasiado[ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) con el identificador de suscripción de Azure, Hola nombre de la colección original y el nombre de saludo de la nueva colección de y pídale que toomigrate la información del usuario.</span><span class="sxs-lookup"><span data-stu-id="f234d-124">Send an email too[remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) with your Azure subscription ID, hello name of your original collection, and hello name of your new collection, and ask them toomigrate your user information.</span></span>
2. <span data-ttu-id="f234d-125">Próximos 2 días laborables equipo de RemoteApp Hola moverá lista de acceso de usuario de Hola y todos los documentos de usuario y configuración de usuario de hello original colección toohello nueva colección.</span><span class="sxs-lookup"><span data-stu-id="f234d-125">Within 2 business days hello RemoteApp team will move hello user access list and all user documents and user settings from hello original collection toohello new collection.</span></span>
3. <span data-ttu-id="f234d-126">Elimine *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="f234d-126">Delete *OriginalCollection*.</span></span>
4. <span data-ttu-id="f234d-127">Elimine *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="f234d-127">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="f234d-128">Y ahora, ¡ya ha terminado!</span><span class="sxs-lookup"><span data-stu-id="f234d-128">And now, you’re done!</span></span>

<span data-ttu-id="f234d-129">Si tiene alguna pregunta o necesita ayuda especial, envíe un correo electrónico a [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span><span class="sxs-lookup"><span data-stu-id="f234d-129">If you have any questions or need special assistance, please email [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span></span>

