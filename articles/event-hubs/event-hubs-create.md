---
title: "Creación de centro de eventos de Azure | Microsoft Docs"
description: "Creación de un espacio de nombres de Azure Event Hubs y un centro de eventos con Azure Portal"
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
ms.openlocfilehash: 816bf1426704d3391550e80c0700f1b011683a94
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-the-azure-portal"></a><span data-ttu-id="2297c-103">Creación de un espacio de nombres de Event Hubs y un centro de eventos con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2297c-103">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="2297c-104">Creación de un espacio de nombres de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="2297c-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="2297c-105">Inicie sesión en [Azure Portal][Azure portal] y haga clic en **Nuevo** en la parte superior izquierda de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="2297c-105">Log on to the [Azure portal][Azure portal], and click **New** at the top left of the screen.</span></span>
1. <span data-ttu-id="2297c-106">Haga clic en **Internet de las cosas** y, luego, en **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="2297c-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="2297c-107">En la hoja **Crear espacio de nombres** , especifique el nombre del espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="2297c-107">In the **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="2297c-108">El sistema realiza la comprobación automáticamente para ver si el nombre está disponible.</span><span class="sxs-lookup"><span data-stu-id="2297c-108">The system immediately checks to see if the name is available.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="2297c-109">Después de asegurarse de que el nombre del espacio de nombres está disponible, elija el plan de tarifa (Básico o Estándar).</span><span class="sxs-lookup"><span data-stu-id="2297c-109">After making sure the namespace name is available, choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="2297c-110">Elija también una suscripción de Azure, un grupo de recursos y la ubicación en la que se va a crear el recurso.</span><span class="sxs-lookup"><span data-stu-id="2297c-110">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span> 
1. <span data-ttu-id="2297c-111">Haga clic en **Crear** para crear el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="2297c-111">Click **Create** to create the namespace.</span></span> <span data-ttu-id="2297c-112">Puede que tenga que esperar unos minutos hasta que el sistema aprovisione totalmente los recursos.</span><span class="sxs-lookup"><span data-stu-id="2297c-112">You may have to wait a few minutes for the system to fully provision the resources.</span></span>
2. <span data-ttu-id="2297c-113">En la lista de espacios de nombres del portal, haga clic en el espacio de nombres recién creado.</span><span class="sxs-lookup"><span data-stu-id="2297c-113">In the portal list of namespaces, click the newly created namespace.</span></span>
2. <span data-ttu-id="2297c-114">Haga clic en **Directivas de acceso compartido** y después en **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="2297c-114">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. <span data-ttu-id="2297c-115">Haga clic en el botón Copiar para copiar la cadena de conexión **RootManageSharedAccessKey** al Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="2297c-115">Click the copy button to copy the **RootManageSharedAccessKey** connection string to the clipboard.</span></span> <span data-ttu-id="2297c-116">Guarde esta cadena de conexión en una ubicación temporal, como el Bloc de notas, para usarla más adelante.</span><span class="sxs-lookup"><span data-stu-id="2297c-116">Save this connection string in a temporary location, such as Notepad, to use later.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="2297c-117">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="2297c-117">Create an event hub</span></span>

1. <span data-ttu-id="2297c-118">En la lista de espacios de nombres de Event Hubs, haga clic en el espacio de nombres recién creado.</span><span class="sxs-lookup"><span data-stu-id="2297c-118">In the Event Hubs namespace list, click the newly created namespace.</span></span>      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. <span data-ttu-id="2297c-119">En la hoja del espacio de nombres, haga clic en **Centros de eventos**.</span><span class="sxs-lookup"><span data-stu-id="2297c-119">In the namespace blade, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. <span data-ttu-id="2297c-120">En la parte superior de la hoja, haga clic en **Agregar Centro de eventos**.</span><span class="sxs-lookup"><span data-stu-id="2297c-120">At the top of the blade, click **Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="2297c-121">Escriba el nombre del centro de eventos y, luego, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2297c-121">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub5.png)

<span data-ttu-id="2297c-122">Ya se ha creado el centro de eventos y cuenta con las cadenas de conexión que necesita para enviar y recibir eventos.</span><span class="sxs-lookup"><span data-stu-id="2297c-122">Your event hub is now created, and you have the connection strings you need to send and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2297c-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2297c-123">Next steps</span></span>
<span data-ttu-id="2297c-124">Para aprender más acerca de Event Hubs, consulte estos vínculos:</span><span class="sxs-lookup"><span data-stu-id="2297c-124">To learn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="2297c-125">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="2297c-125">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="2297c-126">Información general de la API de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="2297c-126">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/