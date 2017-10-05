---
title: Conector de SMTP en Azure Logic Apps | Microsoft Docs
description: "Cree aplicaciones lógicas con el Servicio de aplicaciones de Azure. Conexión a SMTP para envío de correo electrónico."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1cf96bbf8bd215d7ddb3c99860a5cb4e668be3c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-smtp-connector"></a><span data-ttu-id="ec62d-104">Introducción al conector de SMTP</span><span class="sxs-lookup"><span data-stu-id="ec62d-104">Get started with the SMTP connector</span></span>
<span data-ttu-id="ec62d-105">Conexión a SMTP para envío de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="ec62d-105">Connect to SMTP to send email.</span></span>

<span data-ttu-id="ec62d-106">Para poder usar [un conector](apis-list.md), primero debe crear una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="ec62d-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="ec62d-107">Por tanto, puede comenzar [creando una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ec62d-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-smtp"></a><span data-ttu-id="ec62d-108">Conexión a SMTP</span><span class="sxs-lookup"><span data-stu-id="ec62d-108">Connect to SMTP</span></span>
<span data-ttu-id="ec62d-109">Para que la aplicación lógica pueda acceder a un servicio, primero debe crear una *conexión* con dicho servicio.</span><span class="sxs-lookup"><span data-stu-id="ec62d-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="ec62d-110">Una [conexión](connectors-overview.md) proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="ec62d-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="ec62d-111">Por ejemplo, para conectarse a SMTP, primero es preciso crear una *conexión* a SMTP.</span><span class="sxs-lookup"><span data-stu-id="ec62d-111">For example, to connect to SMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="ec62d-112">Para crear una conexión, escriba las credenciales que utiliza normalmente para acceder al servicio al que se conecta.</span><span class="sxs-lookup"><span data-stu-id="ec62d-112">To create a connection, enter the credentials you normally use to access the service you connect to.</span></span> <span data-ttu-id="ec62d-113">Por lo tanto, en el ejemplo de SMTP, escriba las credenciales de su nombre de conexión, la dirección del servidor SMTP y la información de inicio de sesión de usuario para crear una conexión a SMTP.</span><span class="sxs-lookup"><span data-stu-id="ec62d-113">So, in the SMTP example, enter the credentials to your connection name, SMTP server address, and user login information to create the connection to SMTP.</span></span>  

### <a name="create-a-connection-to-smtp"></a><span data-ttu-id="ec62d-114">Creación de una conexión a SMTP</span><span class="sxs-lookup"><span data-stu-id="ec62d-114">Create a connection to SMTP</span></span>
> [!INCLUDE [Steps to create a connection to SMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="ec62d-115">Uso de un desencadenador de SMTP</span><span class="sxs-lookup"><span data-stu-id="ec62d-115">Use an SMTP trigger</span></span>
<span data-ttu-id="ec62d-116">Un desencadenador es un evento que se puede utilizar para iniciar el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="ec62d-116">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="ec62d-117">[Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="ec62d-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="ec62d-118">En este ejemplo, como SMTP no tiene un desencadenador propio, usaremos el desencadenador **Salesforce - When an object is created (Salesforce - Cuando se crea un objeto)**.</span><span class="sxs-lookup"><span data-stu-id="ec62d-118">In this example, because SMTP does not have a trigger of its own, we'll use the **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="ec62d-119">Este desencadenador se activa al crear un objeto en Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ec62d-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="ec62d-120">En nuestro ejemplo, vamos a configurarlo para que cada vez que se crea un cliente potencial en Salesforce, se produzca una acción *Enviar correo electrónico* a través del conector SMTP con una notificación sobre el cliente potencial que se está creando.</span><span class="sxs-lookup"><span data-stu-id="ec62d-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via the SMTP connector with a notification of the new lead being created.</span></span>

1. <span data-ttu-id="ec62d-121">Escriba *salesforce* en el cuadro de búsqueda del diseñador de Logic Apps y seleccione el desencadenador **Salesforce - When an object is created** (Salesforce: cuando se crea un archivo).</span><span class="sxs-lookup"><span data-stu-id="ec62d-121">Enter *salesforce* in the search box on the logic apps designer then select the **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="ec62d-122">Se muestra el control **When an object is created** (Cuando se crea un objeto).</span><span class="sxs-lookup"><span data-stu-id="ec62d-122">The **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="ec62d-123">Seleccione el **tipo de objeto** y luego *Lead* (Cliente potencial) en la lista de objetos.</span><span class="sxs-lookup"><span data-stu-id="ec62d-123">Select the **Object Type** then select *Lead* from the list of objects.</span></span> <span data-ttu-id="ec62d-124">En este paso está indicando que va a crear un desencadenador que enviará una notificación a su aplicación lógica cada vez que se cree un nuevo cliente potencial en Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ec62d-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="ec62d-125">Se ha creado el desencadenador.</span><span class="sxs-lookup"><span data-stu-id="ec62d-125">The trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="ec62d-126">Uso de una acción de SMTP</span><span class="sxs-lookup"><span data-stu-id="ec62d-126">Use an SMTP action</span></span>
<span data-ttu-id="ec62d-127">Una acción es una operación que se lleva a cabo mediante el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="ec62d-127">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="ec62d-128">[Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="ec62d-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="ec62d-129">Ahora que se ha agregado el desencadenador, siga estos pasos para agregar una acción de SMTP que se produzca cuando se crea un cliente potencial en Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ec62d-129">Now that the trigger has been added, follow these steps to add an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="ec62d-130">Seleccione **+ Nuevo paso** para agregar la acción que quiere que se ejecute cuando se cree un cliente potencial.</span><span class="sxs-lookup"><span data-stu-id="ec62d-130">Select **+ New Step** to add the action you would like to take when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="ec62d-131">Seleccione **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="ec62d-131">Select **Add an action**.</span></span> <span data-ttu-id="ec62d-132">Se abrirá el cuadro de búsqueda en el que podrá buscar cualquier acción que quiera realizar.</span><span class="sxs-lookup"><span data-stu-id="ec62d-132">This opens the search box where you can search for any action you would like to take.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="ec62d-133">Escriba *smtp* para buscar todas las acciones relacionadas con SMTP.</span><span class="sxs-lookup"><span data-stu-id="ec62d-133">Enter *smtp* to search for actions related to SMTP.</span></span>  
4. <span data-ttu-id="ec62d-134">Seleccione **SMTP - Send Email (SMTP - Enviar correo electrónico)** como la acción que se realizará cuando se crea el cliente potencial.</span><span class="sxs-lookup"><span data-stu-id="ec62d-134">Select **SMTP - Send Email** as the action to take when the new lead is created.</span></span> <span data-ttu-id="ec62d-135">Se abre el bloque de control de acción.</span><span class="sxs-lookup"><span data-stu-id="ec62d-135">The action control block opens.</span></span> <span data-ttu-id="ec62d-136">Tendrá que establecer la conexión de SMTP en el bloque de diseñador si no lo ha hecho previamente.</span><span class="sxs-lookup"><span data-stu-id="ec62d-136">You will have to establish your smtp connection in the designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="ec62d-137">Indique la información de correo electrónico que quiera en el bloque **SMTP - Send Email (SMTP - Enviar correo electrónico)**.</span><span class="sxs-lookup"><span data-stu-id="ec62d-137">Input your desired email information in the **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="ec62d-138">Guarde el trabajo para activar el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ec62d-138">Save your work in order to activate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="ec62d-139">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="ec62d-139">Connector-specific details</span></span>

<span data-ttu-id="ec62d-140">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/smtpconnector/).</span><span class="sxs-lookup"><span data-stu-id="ec62d-140">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="ec62d-141">Más conectores</span><span class="sxs-lookup"><span data-stu-id="ec62d-141">More connectors</span></span>
<span data-ttu-id="ec62d-142">Volver a la [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="ec62d-142">Go back to the [APIs list](apis-list.md).</span></span>