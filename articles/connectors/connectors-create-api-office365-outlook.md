---
title: "Conector de Outlook de Office 365 aaaAdd hello en las aplicaciones lógicas | Documentos de Microsoft"
description: "Crear aplicaciones lógicas con interacción de tooenable de conector de Office 365 con Office 365. Por ejemplo: crear, editar y actualizar contactos y elementos de calendario."
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a><span data-ttu-id="5fe65-104">Empezar a trabajar con el conector de Outlook de Office 365 Hola</span><span class="sxs-lookup"><span data-stu-id="5fe65-104">Get started with hello Office 365 Outlook connector</span></span>
<span data-ttu-id="5fe65-105">Conector de Outlook de Office 365 Hola permite la interacción con Outlook en Office 365.</span><span class="sxs-lookup"><span data-stu-id="5fe65-105">hello Office 365 Outlook connector enables interaction with Outlook in Office 365.</span></span> <span data-ttu-id="5fe65-106">Usar este conector toocreate, editar y actualizar contactos y elementos de calendario y también obtener, enviar y responder a tooemail.</span><span class="sxs-lookup"><span data-stu-id="5fe65-106">Use this connector toocreate, edit, and update contacts and calendar items, and also get, send, and reply tooemail.</span></span>

<span data-ttu-id="5fe65-107">Con Office 365 Outlook:</span><span class="sxs-lookup"><span data-stu-id="5fe65-107">With Office 365 Outlook, you:</span></span>

* <span data-ttu-id="5fe65-108">Compilar el flujo de trabajo mediante las características de correo electrónico y el calendario de hello en Office 365.</span><span class="sxs-lookup"><span data-stu-id="5fe65-108">Build your workflow using hello email and calendar features within Office 365.</span></span> 
* <span data-ttu-id="5fe65-109">Utilice desencadenadores toostart el flujo de trabajo cuando se produce un nuevo correo electrónico cuando se actualiza un elemento de calendario y mucho más.</span><span class="sxs-lookup"><span data-stu-id="5fe65-109">Use triggers toostart your workflow when there is a new email, when a calendar item is updated, and more.</span></span>
* <span data-ttu-id="5fe65-110">Usar acciones toosend un correo electrónico, cree un nuevo evento de calendario y mucho más.</span><span class="sxs-lookup"><span data-stu-id="5fe65-110">Use actions toosend an email, create a new calendar event, and more.</span></span> <span data-ttu-id="5fe65-111">Por ejemplo, cuando hay un nuevo objeto de Salesforce (un desencadenador), envíe un correo electrónico tooyour Outlook de Office 365 (acción).</span><span class="sxs-lookup"><span data-stu-id="5fe65-111">For example, when there is a new object in Salesforce (a trigger), send an email tooyour Office 365 Outlook (an action).</span></span> 

<span data-ttu-id="5fe65-112">Este tema muestra cómo toouse Hola conector de Outlook de Office 365 en una aplicación de lógica, y también listas Hola acciones y desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="5fe65-112">This topic shows you how toouse hello Office 365 Outlook connector in a logic app, and also lists hello triggers and actions.</span></span>

> [!NOTE]
> <span data-ttu-id="5fe65-113">Esta versión de Hola artículo aplica tooLogic aplicaciones de la disponibilidad general (GA).</span><span class="sxs-lookup"><span data-stu-id="5fe65-113">This version of hello article applies tooLogic Apps general availability (GA).</span></span>
> 
> 

<span data-ttu-id="5fe65-114">toolearn más información acerca de las aplicaciones lógicas, consulte [¿cuáles son las aplicaciones lógicas](../logic-apps/logic-apps-what-are-logic-apps.md) y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5fe65-114">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="5fe65-115">Conectar tooOffice 365</span><span class="sxs-lookup"><span data-stu-id="5fe65-115">Connect tooOffice 365</span></span>
<span data-ttu-id="5fe65-116">Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero cree un *conexión* toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="5fe65-116">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="5fe65-117">Una conexión proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="5fe65-117">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="5fe65-118">Por ejemplo, tooconnect tooOffice 365 Outlook, primero debe Office 365 *conexión*.</span><span class="sxs-lookup"><span data-stu-id="5fe65-118">For example, tooconnect tooOffice 365 Outlook, you first need an Office 365 *connection*.</span></span> <span data-ttu-id="5fe65-119">toocreate una conexión, escriba las credenciales de Hola que suele usar el servicio de hello tooaccess desea tooconnect a.</span><span class="sxs-lookup"><span data-stu-id="5fe65-119">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="5fe65-120">Por lo que con Office 365 Outlook, escriba Hola credenciales tooyour conexión de Hola de toocreate de cuenta de Office 365.</span><span class="sxs-lookup"><span data-stu-id="5fe65-120">So with Office 365 Outlook, enter hello credentials tooyour Office 365 account toocreate hello connection.</span></span>

## <a name="create-hello-connection"></a><span data-ttu-id="5fe65-121">Crear conexiones de Hola</span><span class="sxs-lookup"><span data-stu-id="5fe65-121">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="5fe65-122">Uso de un desencadenador</span><span class="sxs-lookup"><span data-stu-id="5fe65-122">Use a trigger</span></span>
<span data-ttu-id="5fe65-123">Un desencadenador es un evento que puede ser utilizados toostart de flujo de trabajo Hola definido en una aplicación de la lógica.</span><span class="sxs-lookup"><span data-stu-id="5fe65-123">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="5fe65-124">Desencadenadores "sondean" hello servicio en un intervalo y la frecuencia que desee.</span><span class="sxs-lookup"><span data-stu-id="5fe65-124">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="5fe65-125">[Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="5fe65-125">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="5fe65-126">En la aplicación de la lógica de hello, escriba "office 365" tooget una lista de los desencadenadores de hello:</span><span class="sxs-lookup"><span data-stu-id="5fe65-126">In hello logic app, type "office 365" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. <span data-ttu-id="5fe65-127">Seleccione **Office 365 Outlook - Cuando un evento próximo va a comenzar pronto**.</span><span class="sxs-lookup"><span data-stu-id="5fe65-127">Select **Office 365 Outlook - When an upcoming event is starting soon**.</span></span> <span data-ttu-id="5fe65-128">Si ya existe una conexión, a continuación, seleccione un calendario de la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="5fe65-128">If a connection already exists, then select a calendar from hello drop-down list.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    <span data-ttu-id="5fe65-129">Si son toosign solicitada en, escriba el inicio de sesión de hello en conexión de hello toocreate de detalles.</span><span class="sxs-lookup"><span data-stu-id="5fe65-129">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="5fe65-130">[Crear conexiones de hello](connectors-create-api-office365-outlook.md#create-the-connection) en este tema se enumeran los pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5fe65-130">[Create hello connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="5fe65-131">En este ejemplo, la aplicación de lógica de Hola se ejecuta cuando se actualiza un evento de calendario.</span><span class="sxs-lookup"><span data-stu-id="5fe65-131">In this example, hello logic app runs when a calendar event is updated.</span></span> <span data-ttu-id="5fe65-132">resultados de hello toosee de este desencadenador, agregar otra acción que envía un mensaje de texto.</span><span class="sxs-lookup"><span data-stu-id="5fe65-132">toosee hello results of this trigger, add another action that sends you a text message.</span></span> <span data-ttu-id="5fe65-133">Por ejemplo, agregar hello Twilio *enviar mensaje* acción que se está iniciando textos cuando hello eventos de calendario en 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="5fe65-133">For example, add hello Twilio *Send message* action that texts you when hello calendar event is starting in 15 minutes.</span></span> 
   > 
   > 
3. <span data-ttu-id="5fe65-134">Seleccione hello **editar** botón y establezca hello **frecuencia** y **intervalo** valores.</span><span class="sxs-lookup"><span data-stu-id="5fe65-134">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="5fe65-135">Por ejemplo, si desea Hola desencadenador toopoll cada 15 minutos, a continuación, establezca hello **frecuencia** demasiado**minuto**, conjunto hello y **intervalo** demasiado**15**.</span><span class="sxs-lookup"><span data-stu-id="5fe65-135">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. <span data-ttu-id="5fe65-136">**Guardar** los cambios (esquina superior izquierda de la barra de herramientas de hello).</span><span class="sxs-lookup"><span data-stu-id="5fe65-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="5fe65-137">La aplicación lógica se guarda y se puede habilitar automáticamente.</span><span class="sxs-lookup"><span data-stu-id="5fe65-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="5fe65-138">Uso de una acción</span><span class="sxs-lookup"><span data-stu-id="5fe65-138">Use an action</span></span>
<span data-ttu-id="5fe65-139">Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5fe65-139">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="5fe65-140">[Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="5fe65-140">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="5fe65-141">Seleccione el signo más Hola.</span><span class="sxs-lookup"><span data-stu-id="5fe65-141">Select hello plus sign.</span></span> <span data-ttu-id="5fe65-142">Vea elegir entre varias opciones: **agregar una acción**, **agregar una condición**, o uno de hello **más** opciones.</span><span class="sxs-lookup"><span data-stu-id="5fe65-142">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. <span data-ttu-id="5fe65-143">Elija **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="5fe65-143">Choose **Add an action**.</span></span>
3. <span data-ttu-id="5fe65-144">En el cuadro de texto hello, escriba "office 365" tooget una lista de todas las acciones disponibles Hola.</span><span class="sxs-lookup"><span data-stu-id="5fe65-144">In hello text box, type “office 365” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. <span data-ttu-id="5fe65-145">En nuestro ejemplo, elija **Office 365 Outlook - Crear contacto**.</span><span class="sxs-lookup"><span data-stu-id="5fe65-145">In our example, choose **Office 365 Outlook - Create contact**.</span></span> <span data-ttu-id="5fe65-146">Si ya existe una conexión, a continuación, elija hello **Id. de la carpeta**, **nombre dado**y otras propiedades:</span><span class="sxs-lookup"><span data-stu-id="5fe65-146">If a connection already exists, then choose hello **Folder ID**, **Given Name**, and other properties:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    <span data-ttu-id="5fe65-147">Si se le solicitará información de conexión de hello, a continuación, escriba la conexión de hello detalles toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="5fe65-147">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="5fe65-148">[Crear conexiones de hello](connectors-create-api-office365-outlook.md#create-the-connection) en este tema se describen estas propiedades.</span><span class="sxs-lookup"><span data-stu-id="5fe65-148">[Create hello connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="5fe65-149">En este ejemplo, creamos un nuevo contacto en Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="5fe65-149">In this example, we create a new contact in Office 365 Outlook.</span></span> <span data-ttu-id="5fe65-150">Se puede usar la salida de otro desencadenador toocreate Hola póngase en contacto con.</span><span class="sxs-lookup"><span data-stu-id="5fe65-150">You can use output from another trigger toocreate hello contact.</span></span> <span data-ttu-id="5fe65-151">Por ejemplo, agregar Hola SalesForce *cuando se crea un objeto* desencadenador.</span><span class="sxs-lookup"><span data-stu-id="5fe65-151">For example, add hello SalesForce *When an object is created* trigger.</span></span> <span data-ttu-id="5fe65-152">A continuación, agregue Hola Office 365 Outlook *crear contacto* acción que usa Hola SalesForce campos toocreate Hola nueva nuevo contacto en Office 365.</span><span class="sxs-lookup"><span data-stu-id="5fe65-152">Then add hello Office 365 Outlook *Create contact* action that uses hello SalesForce fields toocreate hello new new contact in Office 365.</span></span> 
   > 
   > 
5. <span data-ttu-id="5fe65-153">**Guardar** los cambios (esquina superior izquierda de la barra de herramientas de hello).</span><span class="sxs-lookup"><span data-stu-id="5fe65-153">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="5fe65-154">La aplicación lógica se guarda y se puede habilitar automáticamente.</span><span class="sxs-lookup"><span data-stu-id="5fe65-154">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="5fe65-155">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="5fe65-155">Connector-specific details</span></span>

<span data-ttu-id="5fe65-156">Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/office365connector/).</span><span class="sxs-lookup"><span data-stu-id="5fe65-156">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/office365connector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5fe65-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5fe65-157">Next Steps</span></span>
<span data-ttu-id="5fe65-158">[Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5fe65-158">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="5fe65-159">Explorar Hola otros conectores disponibles en las aplicaciones lógicas en nuestro [lista de las API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="5fe65-159">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

