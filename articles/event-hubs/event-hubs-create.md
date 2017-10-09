---
title: aaaCreate un concentrador de eventos de Azure | Documentos de Microsoft
description: Crear un espacio de nombres de los centros de eventos de Azure y un concentrador de eventos mediante Hola portal de Azure
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a><span data-ttu-id="b9373-103">Crear un espacio de nombres de los centros de eventos y un concentrador de eventos mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b9373-103">Create an Event Hubs namespace and an event hub using hello Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="b9373-104">Creación de un espacio de nombres de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b9373-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="b9373-105">Inicie sesión en toohello [portal de Azure][Azure portal]y haga clic en **New** en hello parte superior izquierda de la pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="b9373-105">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
1. <span data-ttu-id="b9373-106">Haga clic en **Internet de las cosas** y, luego, en **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="b9373-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="b9373-107">Hola **crear espacio de nombres** hoja, escriba un nombre de espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="b9373-107">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="b9373-108">sistema de Hello comprueba inmediatamente toosee si Hola nombre está disponible.</span><span class="sxs-lookup"><span data-stu-id="b9373-108">hello system immediately checks toosee if hello name is available.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="b9373-109">Después de realizar el nombre de espacio de nombres de hello seguro está disponible, elija Hola tarifa (básico o estándar).</span><span class="sxs-lookup"><span data-stu-id="b9373-109">After making sure hello namespace name is available, choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="b9373-110">Además, elija una suscripción de Azure, el grupo de recursos y la ubicación en el recurso que hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="b9373-110">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> 
1. <span data-ttu-id="b9373-111">Haga clic en **crear** el espacio de nombres de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="b9373-111">Click **Create** toocreate hello namespace.</span></span> <span data-ttu-id="b9373-112">Puede que tenga toowait unos minutos para los recursos Hola Hola sistema toofully aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="b9373-112">You may have toowait a few minutes for hello system toofully provision hello resources.</span></span>
2. <span data-ttu-id="b9373-113">En la lista de portales de Hola de espacios de nombres, haga clic en hello que acaba de crear espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="b9373-113">In hello portal list of namespaces, click hello newly created namespace.</span></span>
2. <span data-ttu-id="b9373-114">Haga clic en **Directivas de acceso compartido** y después en **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="b9373-114">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. <span data-ttu-id="b9373-115">Haga clic en Hola de hello copia botón toocopy **RootManageSharedAccessKey** Portapapeles de toohello de cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="b9373-115">Click hello copy button toocopy hello **RootManageSharedAccessKey** connection string toohello clipboard.</span></span> <span data-ttu-id="b9373-116">Guarde esta cadena de conexión en una ubicación temporal, como el Bloc de notas, toouse más tarde.</span><span class="sxs-lookup"><span data-stu-id="b9373-116">Save this connection string in a temporary location, such as Notepad, toouse later.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="b9373-117">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="b9373-117">Create an event hub</span></span>

1. <span data-ttu-id="b9373-118">En la lista de espacio de nombres de los centros de eventos de hello, haga clic en el espacio de nombres de hello recién creado.</span><span class="sxs-lookup"><span data-stu-id="b9373-118">In hello Event Hubs namespace list, click hello newly created namespace.</span></span>      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. <span data-ttu-id="b9373-119">En la hoja de espacio de nombres de hello, haga clic en **centros de eventos**.</span><span class="sxs-lookup"><span data-stu-id="b9373-119">In hello namespace blade, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. <span data-ttu-id="b9373-120">En la parte superior de Hola de hoja de hello, haga clic en **agregar concentrador de eventos**.</span><span class="sxs-lookup"><span data-stu-id="b9373-120">At hello top of hello blade, click **Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="b9373-121">Escriba el nombre del centro de eventos y, luego, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b9373-121">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub5.png)

<span data-ttu-id="b9373-122">Ahora se crea el centro de eventos y de que las cadenas de conexión de Hola que necesita toosend y recibe eventos.</span><span class="sxs-lookup"><span data-stu-id="b9373-122">Your event hub is now created, and you have hello connection strings you need toosend and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9373-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b9373-123">Next steps</span></span>
<span data-ttu-id="b9373-124">toolearn más información acerca de los centros de eventos, visite estos vínculos:</span><span class="sxs-lookup"><span data-stu-id="b9373-124">toolearn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="b9373-125">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b9373-125">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="b9373-126">Información general de la API de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b9373-126">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/