---
title: "Conector de aaaSMTP en las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Cree aplicaciones lógicas con el Servicio de aplicaciones de Azure. Conecte el correo electrónico de toosend tooSMTP."
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
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a><span data-ttu-id="d22f0-104">Empezar a trabajar con el conector SMTP de Hola</span><span class="sxs-lookup"><span data-stu-id="d22f0-104">Get started with hello SMTP connector</span></span>
<span data-ttu-id="d22f0-105">Conecte el correo electrónico de toosend tooSMTP.</span><span class="sxs-lookup"><span data-stu-id="d22f0-105">Connect tooSMTP toosend email.</span></span>

<span data-ttu-id="d22f0-106">toouse [cualquier conector](apis-list.md), primero debe toocreate una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="d22f0-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="d22f0-107">Por tanto, puede comenzar [creando una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d22f0-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosmtp"></a><span data-ttu-id="d22f0-108">Conectar tooSMTP</span><span class="sxs-lookup"><span data-stu-id="d22f0-108">Connect tooSMTP</span></span>
<span data-ttu-id="d22f0-109">Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero debe toocreate una *conexión* toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="d22f0-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="d22f0-110">Una [conexión](connectors-overview.md) proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="d22f0-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="d22f0-111">Por ejemplo, tooconnect tooSMTP, primero debe SMTP *conexión*.</span><span class="sxs-lookup"><span data-stu-id="d22f0-111">For example, tooconnect tooSMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="d22f0-112">toocreate una conexión, escriba las credenciales de Hola que suele usar tooaccess se conectan a un servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d22f0-112">toocreate a connection, enter hello credentials you normally use tooaccess hello service you connect to.</span></span> <span data-ttu-id="d22f0-113">Por lo tanto, en el ejemplo de Hola SMTP, escriba nombre de la conexión de hello credenciales tooyour, dirección del servidor SMTP y tooSMTP de conexión de usuario inicio de sesión información toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="d22f0-113">So, in hello SMTP example, enter hello credentials tooyour connection name, SMTP server address, and user login information toocreate hello connection tooSMTP.</span></span>  

### <a name="create-a-connection-toosmtp"></a><span data-ttu-id="d22f0-114">Crear una conexión tooSMTP</span><span class="sxs-lookup"><span data-stu-id="d22f0-114">Create a connection tooSMTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="d22f0-115">Uso de un desencadenador de SMTP</span><span class="sxs-lookup"><span data-stu-id="d22f0-115">Use an SMTP trigger</span></span>
<span data-ttu-id="d22f0-116">Un desencadenador es un evento que puede ser utilizados toostart de flujo de trabajo Hola definido en una aplicación de la lógica.</span><span class="sxs-lookup"><span data-stu-id="d22f0-116">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="d22f0-117">[Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="d22f0-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="d22f0-118">En este ejemplo, dado que SMTP no tiene un desencadenador de su propio, usaremos hello **Salesforce - cuando se crea un objeto** desencadenador.</span><span class="sxs-lookup"><span data-stu-id="d22f0-118">In this example, because SMTP does not have a trigger of its own, we'll use hello **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="d22f0-119">Este desencadenador se activa al crear un objeto en Salesforce.</span><span class="sxs-lookup"><span data-stu-id="d22f0-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="d22f0-120">En nuestro ejemplo, configuraremos lo modo que cada vez que se crea un nuevo cliente potencial en Salesforce, un *enviar correo electrónico* acción tiene lugar mediante el conector de hello SMTP con una notificación de hello nuevo cliente potencial que se está creando.</span><span class="sxs-lookup"><span data-stu-id="d22f0-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via hello SMTP connector with a notification of hello new lead being created.</span></span>

1. <span data-ttu-id="d22f0-121">Escriba *salesforce* en el cuadro de búsqueda de hello en el Diseñador de aplicaciones de lógica de hello, a continuación, seleccione hello **Salesforce - cuando se crea un objeto** desencadenador.</span><span class="sxs-lookup"><span data-stu-id="d22f0-121">Enter *salesforce* in hello search box on hello logic apps designer then select hello **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="d22f0-122">Hola **cuando se crea un objeto** se muestra el control.</span><span class="sxs-lookup"><span data-stu-id="d22f0-122">hello **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="d22f0-123">Seleccione hello **tipo de objeto** , a continuación, seleccione *provocar* de lista de Hola de objetos.</span><span class="sxs-lookup"><span data-stu-id="d22f0-123">Select hello **Object Type** then select *Lead* from hello list of objects.</span></span> <span data-ttu-id="d22f0-124">En este paso está indicando que va a crear un desencadenador que enviará una notificación a su aplicación lógica cada vez que se cree un nuevo cliente potencial en Salesforce.</span><span class="sxs-lookup"><span data-stu-id="d22f0-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="d22f0-125">se ha creado el desencadenador de Hola.</span><span class="sxs-lookup"><span data-stu-id="d22f0-125">hello trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="d22f0-126">Uso de una acción de SMTP</span><span class="sxs-lookup"><span data-stu-id="d22f0-126">Use an SMTP action</span></span>
<span data-ttu-id="d22f0-127">Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d22f0-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="d22f0-128">[Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="d22f0-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="d22f0-129">Ahora que hello desencadenador se ha agregado, siga estos acción de tooadd SMTP de pasos que se produce cuando se crea un nuevo cliente potencial en Salesforce.</span><span class="sxs-lookup"><span data-stu-id="d22f0-129">Now that hello trigger has been added, follow these steps tooadd an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="d22f0-130">Seleccione **+ nuevo paso** acción de hello tooadd le gustaría tootake cuando se crea un nuevo cliente potencial.</span><span class="sxs-lookup"><span data-stu-id="d22f0-130">Select **+ New Step** tooadd hello action you would like tootake when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="d22f0-131">Seleccione **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="d22f0-131">Select **Add an action**.</span></span> <span data-ttu-id="d22f0-132">Este cuadro de búsqueda de hello abre donde puede buscar cualquier acción desea que tootake.</span><span class="sxs-lookup"><span data-stu-id="d22f0-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="d22f0-133">Escriba *smtp* toosearch para acciones relacionadas tooSMTP.</span><span class="sxs-lookup"><span data-stu-id="d22f0-133">Enter *smtp* toosearch for actions related tooSMTP.</span></span>  
4. <span data-ttu-id="d22f0-134">Seleccione **SMTP - enviar correo electrónico** como Hola tootake acción cuando se crea el nuevo cliente potencial de Hola.</span><span class="sxs-lookup"><span data-stu-id="d22f0-134">Select **SMTP - Send Email** as hello action tootake when hello new lead is created.</span></span> <span data-ttu-id="d22f0-135">se abre el bloque de control de acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="d22f0-135">hello action control block opens.</span></span> <span data-ttu-id="d22f0-136">Tendrá tooestablish la conexión de smtp en el bloque de diseñador Hola si aún no lo hecho previamente.</span><span class="sxs-lookup"><span data-stu-id="d22f0-136">You will have tooestablish your smtp connection in hello designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="d22f0-137">Entrada de la información de correo electrónico deseado en hello **SMTP - enviar correo electrónico** bloque.</span><span class="sxs-lookup"><span data-stu-id="d22f0-137">Input your desired email information in hello **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="d22f0-138">Guardar su trabajo en orden tooactivate el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d22f0-138">Save your work in order tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="d22f0-139">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="d22f0-139">Connector-specific details</span></span>

<span data-ttu-id="d22f0-140">Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/smtpconnector/).</span><span class="sxs-lookup"><span data-stu-id="d22f0-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="d22f0-141">Más conectores</span><span class="sxs-lookup"><span data-stu-id="d22f0-141">More connectors</span></span>
<span data-ttu-id="d22f0-142">Volver atrás toohello [lista de las API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="d22f0-142">Go back toohello [APIs list](apis-list.md).</span></span>
