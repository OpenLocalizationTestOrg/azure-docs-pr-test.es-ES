---
title: Aprenda a migrar desde una red virtual de RemoteApp a una red virtual de Azure | Microsoft Docs
description: Aprenda a migrar desde una red virtual de RemoteApp a una red virtual de Azure
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
ms.openlocfilehash: 10b5f4844a38fe97852dee8634e8cf54f1a23a1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-a-hybrid-collection-from-a-remoteapp-vnet-to-an-azure-vnet"></a><span data-ttu-id="47e54-103">Migración de una colección híbrida de una red virtual de RemoteApp a una red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="47e54-103">How to migrate a hybrid collection from a RemoteApp VNET to an Azure VNET</span></span>
> [!IMPORTANT]
> <span data-ttu-id="47e54-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="47e54-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="47e54-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="47e54-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="47e54-106">¡Buenas noticias!</span><span class="sxs-lookup"><span data-stu-id="47e54-106">Good news!</span></span> <span data-ttu-id="47e54-107">Ahora tiene la posibilidad de implementar colecciones híbridas de RemoteApp directamente en sus redes virtuales de Azure (VNET) existentes, con lo que deja de ser necesario crear redes virtuales específicas para RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="47e54-107">We have enabled you to deploy hybrid RemoteApp collections directly into your existing Azure virtual networks (VNETs) instead of creating RemoteApp-specific VNETs.</span></span> <span data-ttu-id="47e54-108">Esto le permite aprovechar las últimas características de la red virtual (por ejemplo, ExpressRoute) y proporcionar a las colecciones híbridas acceso de red directo a otros servicios y máquinas virtuales de Azure implementados en esa red virtual.</span><span class="sxs-lookup"><span data-stu-id="47e54-108">This lets you take advantage of the latest VNET features (like ExpressRoute) and give your hybrid collections direct network access to other Azure services and virtual machines deployed to that VNET.</span></span>  <span data-ttu-id="47e54-109">(Esto le permite disfrutar de un mejor rendimiento y mayor facilidad de configuración con respecto a las instalaciones de red virtual a red virtual).</span><span class="sxs-lookup"><span data-stu-id="47e54-109">(This gets you better performance and easier setup than VNET-to-VNET configurations).</span></span>

<span data-ttu-id="47e54-110">Supongamos que ya ha creado una colección de RemoteApp híbrida denominada *OriginalCollection* con una red virtual de RemoteApp llamada *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="47e54-110">Let’s say that you’ve already created a hybrid RemoteApp collection called *OriginalCollection* with a RemoteApp VNET called *RemoteAppVNET*.</span></span> <span data-ttu-id="47e54-111">Estos son los pasos para migrarla a una nueva red virtual de Azure denominada *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="47e54-111">Here are the steps to migrate it to a new Azure VNET called *AzureVNET*.</span></span>

1. <span data-ttu-id="47e54-112">En la pestaña **Redes** del [Portal de administración](http://manage.windowsazure.com/), cree una red virtual denominada *AzureVNET* usando los mismos valores de ubicación, configuración de DNS y espacio de direcciones (para al menos una de las subredes de *AzureVNET*) que utilizó para *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="47e54-112">On the **Networks** tab in the [management portal](http://manage.windowsazure.com/), create a VNET called *AzureVNET*, using the same location, DNS configuration, and address space (for at least one of the *AzureVNET* subnets) as you used for *RemoteAppVNET*.</span></span>
2. <span data-ttu-id="47e54-113">Configure *AzureVNET* para hospedar o tener conectividad de red para la implementación de Active Directory a la que la colección *OriginalCollection* está unida mediante dominio.</span><span class="sxs-lookup"><span data-stu-id="47e54-113">Configure *AzureVNET* to either host or have network connectivity to the Active Directory deployment that *OriginalCollection* is domain joined to.</span></span>
3. <span data-ttu-id="47e54-114">En la pestaña **RemoteApps** , cree una nueva colección de RemoteApp denominada *New Collection*.</span><span class="sxs-lookup"><span data-stu-id="47e54-114">On the **RemoteApps** tab, create a new RemoteApp collection called *New Collection*.</span></span> <span data-ttu-id="47e54-115">(Use la opción **Crear con red virtual**, no **Creación rápida**).</span><span class="sxs-lookup"><span data-stu-id="47e54-115">(Use the **Create with VNET** option, not **Quick Create**.)</span></span>
4. <span data-ttu-id="47e54-116">Configure *NewCollection* para que se implemente en una subred en *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="47e54-116">Configure *NewCollection* to be deployed to a subnet in *AzureVNET*.</span></span>
5. <span data-ttu-id="47e54-117">Configure *NewCollection* para que utilice la misma imagen y la misma información de unión a un dominio que las empleadas para *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="47e54-117">Configure *NewCollection* to use the same image and domain join information as you used for *OriginalCollection*.</span></span>
6. <span data-ttu-id="47e54-118">Después de unas horas, *NewCollection* aparecerá en la lista de colecciones con un estado activo.</span><span class="sxs-lookup"><span data-stu-id="47e54-118">After a few hours, *NewCollection* will show up in your collection list with an Active state.</span></span>

<span data-ttu-id="47e54-119">Ahora, si NO es necesario migrar ninguna información de usuario de la colección original a la nueva colección, siga estos pasos a continuación:</span><span class="sxs-lookup"><span data-stu-id="47e54-119">Now, if you DON’T need to migrate any user information from the original collection to the new collection, do these steps next:</span></span>

1. <span data-ttu-id="47e54-120">Elimine *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="47e54-120">Delete *OriginalCollection*.</span></span>
2. <span data-ttu-id="47e54-121">Elimine *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="47e54-121">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="47e54-122">¡Y ya está!</span><span class="sxs-lookup"><span data-stu-id="47e54-122">And, you’re done!</span></span>

<span data-ttu-id="47e54-123">Como alternativa, en caso de que SÍ tenga que migrar información de usuario de la colección original a la colección nueva, siga estos pasos a continuación:</span><span class="sxs-lookup"><span data-stu-id="47e54-123">Alternately, if you DO need to migrate user information from the original collection to the new collection, do these steps next:</span></span>

1. <span data-ttu-id="47e54-124">Envíe un correo electrónico a [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) con el identificador de la suscripción de Azure, el nombre de la colección original y el nombre de la nueva colección, y solicite la migración de la información de usuario.</span><span class="sxs-lookup"><span data-stu-id="47e54-124">Send an email to [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) with your Azure subscription ID, the name of your original collection, and the name of your new collection, and ask them to migrate your user information.</span></span>
2. <span data-ttu-id="47e54-125">En el plazo de dos días hábiles, el equipo de RemoteApp moverá la lista de acceso de usuarios y todos los documentos y configuraciones de usuario de la colección original a la nueva colección.</span><span class="sxs-lookup"><span data-stu-id="47e54-125">Within 2 business days the RemoteApp team will move the user access list and all user documents and user settings from the original collection to the new collection.</span></span>
3. <span data-ttu-id="47e54-126">Elimine *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="47e54-126">Delete *OriginalCollection*.</span></span>
4. <span data-ttu-id="47e54-127">Elimine *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="47e54-127">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="47e54-128">Y ahora, ¡ya ha terminado!</span><span class="sxs-lookup"><span data-stu-id="47e54-128">And now, you’re done!</span></span>

<span data-ttu-id="47e54-129">Si tiene alguna pregunta o necesita ayuda especial, envíe un correo electrónico a [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span><span class="sxs-lookup"><span data-stu-id="47e54-129">If you have any questions or need special assistance, please email [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span></span>

