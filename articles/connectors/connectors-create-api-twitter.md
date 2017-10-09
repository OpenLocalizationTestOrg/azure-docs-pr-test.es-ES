---
title: "aaaLearn cómo toouse Hola conector de Twitter en las aplicaciones lógicas | Documentos de Microsoft"
description: "Información general del conector de Twitter con parámetros de la API de REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a><span data-ttu-id="9db55-103">Empezar a trabajar con el conector de Twitter de Hola</span><span class="sxs-lookup"><span data-stu-id="9db55-103">Get started with hello Twitter connector</span></span>
<span data-ttu-id="9db55-104">Con el conector de Twitter de hello hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9db55-104">With hello Twitter connector you can:</span></span>

* <span data-ttu-id="9db55-105">Publicar y obtener tweets</span><span class="sxs-lookup"><span data-stu-id="9db55-105">Post tweets and get tweets</span></span>
* <span data-ttu-id="9db55-106">Acceder a escalas de tiempo, amigos y seguidores</span><span class="sxs-lookup"><span data-stu-id="9db55-106">Access timelines, friends and followers</span></span>
* <span data-ttu-id="9db55-107">Realice cualquiera de hello otras acciones y desencadenadores que se describe a continuación</span><span class="sxs-lookup"><span data-stu-id="9db55-107">Perform any of hello other actions and triggers described below</span></span>  

<span data-ttu-id="9db55-108">toouse [cualquier conector](apis-list.md), primero debe toocreate una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="9db55-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="9db55-109">Por tanto, puede comenzar [creando una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9db55-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>  

## <a name="connect-tootwitter"></a><span data-ttu-id="9db55-110">Conectar tooTwitter</span><span class="sxs-lookup"><span data-stu-id="9db55-110">Connect tooTwitter</span></span>
<span data-ttu-id="9db55-111">Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero debe toocreate una *conexión* toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="9db55-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="9db55-112">Una [conexión](connectors-overview.md) proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="9db55-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tootwitter"></a><span data-ttu-id="9db55-113">Crear una conexión tooTwitter</span><span class="sxs-lookup"><span data-stu-id="9db55-113">Create a connection tooTwitter</span></span>
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a><span data-ttu-id="9db55-114">Uso de un desencadenador de Twitter</span><span class="sxs-lookup"><span data-stu-id="9db55-114">Use a Twitter trigger</span></span>
<span data-ttu-id="9db55-115">Un desencadenador es un evento que puede ser utilizados toostart de flujo de trabajo Hola definido en una aplicación de la lógica.</span><span class="sxs-lookup"><span data-stu-id="9db55-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="9db55-116">[Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="9db55-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="9db55-117">En este ejemplo, le mostrará cómo hello toouse **cuando se registra un nuevo tweet** desencadena toosearch para #Seattle y, si se encuentra #Seattle, actualizar un archivo en Dropbox con texto hello tweet Hola.</span><span class="sxs-lookup"><span data-stu-id="9db55-117">In this example, I will show you how toouse hello **When a new tweet is posted**  trigger toosearch for #Seattle and, if #Seattle is found, update a file in Dropbox with hello text from hello tweet.</span></span> <span data-ttu-id="9db55-118">En un ejemplo de la empresa, podría buscar Hola nombre de su empresa y actualizar una base de datos SQL con texto hello tweet Hola.</span><span class="sxs-lookup"><span data-stu-id="9db55-118">In an enterprise example, you could search for hello name of your company and update a SQL database with hello text from hello tweet.</span></span>

1. <span data-ttu-id="9db55-119">Escriba *twitter* en el cuadro de búsqueda de hello en el Diseñador de aplicaciones de lógica de hello, a continuación, seleccione hello **Twitter - cuando se registra un nuevo tweet** desencadenador</span><span class="sxs-lookup"><span data-stu-id="9db55-119">Enter *twitter* in hello search box on hello logic apps designer then select hello **Twitter - When a new tweet is posted**  trigger</span></span>   
   <span data-ttu-id="9db55-120">![Imagen de desencadenador de Twitter 1](./media/connectors-create-api-twitter/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="9db55-120">![Twitter trigger image 1](./media/connectors-create-api-twitter/trigger-1.png)</span></span>  
2. <span data-ttu-id="9db55-121">Escriba *#Seattle* en hello **texto de búsqueda** control</span><span class="sxs-lookup"><span data-stu-id="9db55-121">Enter *#Seattle* in hello **Search Text** control</span></span>  
   <span data-ttu-id="9db55-122">![Imagen de desencadenador de Twitter 2](./media/connectors-create-api-twitter/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="9db55-122">![Twitter trigger image 2](./media/connectors-create-api-twitter/trigger-2.png)</span></span> 

<span data-ttu-id="9db55-123">En este punto, la aplicación lógica se ha configurado con un desencadenador que se iniciará una ejecución del programa Hola a otros desencadenadores y acciones de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9db55-123">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="9db55-124">Para que una toobe de aplicación lógica funcional, debe contener al menos un desencadenador y una acción.</span><span class="sxs-lookup"><span data-stu-id="9db55-124">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="9db55-125">Siga los pasos de Hola Hola siguiente sección tooadd una acción.</span><span class="sxs-lookup"><span data-stu-id="9db55-125">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="9db55-126">Agregar una condición</span><span class="sxs-lookup"><span data-stu-id="9db55-126">Add a condition</span></span>
<span data-ttu-id="9db55-127">Puesto que sólo estamos interesados en tweets de los usuarios con más de 50 usuarios, una condición que se confirma el número de Hola de seguidores se debe agregar primero toohello aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="9db55-127">Since we are only interested in tweets from users with more than 50 users, a condition that confirms hello number of followers must first be added toohello logic app.</span></span>  

1. <span data-ttu-id="9db55-128">Seleccione **+ nuevo paso** acción de hello tooadd le gustaría tootake cuando #Seattle se encuentra en un tweet nueva</span><span class="sxs-lookup"><span data-stu-id="9db55-128">Select **+ New step** tooadd hello action you would like tootake when #Seattle is found in a new tweet</span></span>  
   <span data-ttu-id="9db55-129">![Imagen de acción de Twitter 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="9db55-129">![Twitter action image 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span></span>  
2. <span data-ttu-id="9db55-130">Seleccione hello **agregar una condición** vínculo.</span><span class="sxs-lookup"><span data-stu-id="9db55-130">Select hello **Add a condition** link.</span></span>  
   <span data-ttu-id="9db55-131">![Imagen de condición de Twitter 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span><span class="sxs-lookup"><span data-stu-id="9db55-131">![Twitter condition image 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span></span>  
   <span data-ttu-id="9db55-132">Se abrirá hello **condición** control donde puede comprobar las condiciones como *es igual a*, *es menor que*, *es mayor que*, *contiene*, etcetera.</span><span class="sxs-lookup"><span data-stu-id="9db55-132">This opens hello **Condition** control where you can check conditions such as *is equal to*, *is less than*, *is greater than*, *contains*, etc.</span></span>  
   <span data-ttu-id="9db55-133">![Imagen de condición de Twitter 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span><span class="sxs-lookup"><span data-stu-id="9db55-133">![Twitter condition image 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span></span>   
3. <span data-ttu-id="9db55-134">Seleccione hello **elegir un valor** control.</span><span class="sxs-lookup"><span data-stu-id="9db55-134">Select hello **Choose a value** control.</span></span>  
   <span data-ttu-id="9db55-135">En este control, puede seleccionar una o varias de las propiedades de Hola de las acciones anteriores o los desencadenadores como valor de hello cuya condición será evaluada tootrue o false.</span><span class="sxs-lookup"><span data-stu-id="9db55-135">In this control, you can select one or more of hello properties from any previous actions or triggers as hello value whose condition will be evaluated tootrue or false.</span></span>
   <span data-ttu-id="9db55-136">![Imagen de condición de Twitter 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span><span class="sxs-lookup"><span data-stu-id="9db55-136">![Twitter condition image 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span></span>   
4. <span data-ttu-id="9db55-137">Seleccione hello **...**  tooexpand lista de Hola de propiedades para que pueda ver todas las propiedades de Hola que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="9db55-137">Select hello **...** tooexpand hello list of properties so you can see all hello properties that are available.</span></span>        
   <span data-ttu-id="9db55-138">![Imagen de condición de Twitter 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span><span class="sxs-lookup"><span data-stu-id="9db55-138">![Twitter condition image 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span></span>   
5. <span data-ttu-id="9db55-139">Seleccione hello **recuento seguidores** propiedad.</span><span class="sxs-lookup"><span data-stu-id="9db55-139">Select hello **Followers count** property.</span></span>    
   <span data-ttu-id="9db55-140">![Imagen de condición de Twitter 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span><span class="sxs-lookup"><span data-stu-id="9db55-140">![Twitter condition image 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span></span>   
6. <span data-ttu-id="9db55-141">Tenga en cuenta seguidores de hello propiedad count es ahora en el control de valores de hello.</span><span class="sxs-lookup"><span data-stu-id="9db55-141">Notice hello Followers count property is now in hello value control.</span></span>    
   ![Imagen de condición de Twitter 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. <span data-ttu-id="9db55-143">Seleccione **es mayor que** desde la lista de operadores de Hola.</span><span class="sxs-lookup"><span data-stu-id="9db55-143">Select **is greater than** from hello operators list.</span></span>    
   <span data-ttu-id="9db55-144">![Imagen de condición de Twitter 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span><span class="sxs-lookup"><span data-stu-id="9db55-144">![Twitter condition image 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span></span>   
8. <span data-ttu-id="9db55-145">Escriba 50 como Hola operando para hello *es mayor que* operador.</span><span class="sxs-lookup"><span data-stu-id="9db55-145">Enter 50 as hello operand for hello *is greater than* operator.</span></span>  
   <span data-ttu-id="9db55-146">Ahora se agrega la condición de Hola.</span><span class="sxs-lookup"><span data-stu-id="9db55-146">hello condition is now added.</span></span> <span data-ttu-id="9db55-147">Guardar su trabajo con hello **guardar** vínculo en el menú de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="9db55-147">Save your work using hello **Save** link on hello menu above.</span></span>    
   <span data-ttu-id="9db55-148">![Imagen de condición de Twitter 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span><span class="sxs-lookup"><span data-stu-id="9db55-148">![Twitter condition image 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span></span>   

## <a name="use-a-twitter-action"></a><span data-ttu-id="9db55-149">Uso de una acción de Twitter</span><span class="sxs-lookup"><span data-stu-id="9db55-149">Use a Twitter action</span></span>
<span data-ttu-id="9db55-150">Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9db55-150">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="9db55-151">[Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="9db55-151">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="9db55-152">Ahora que ha agregado un desencadenador, siga estas tooadd pasos una acción que se va a registrar un nuevo tweet con contenido de Hola de tweets de hello encontrados por el desencadenador de Hola.</span><span class="sxs-lookup"><span data-stu-id="9db55-152">Now that you have added a trigger, follow these steps tooadd an action that will post a new tweet with hello contents of hello tweets found by hello trigger.</span></span> <span data-ttu-id="9db55-153">Para los fines de Hola de este tutorial se expondrá solo tweets de los usuarios con más de 50 seguidores.</span><span class="sxs-lookup"><span data-stu-id="9db55-153">For hello purposes of this walk-through only tweets from users with more than 50 followers will be posted.</span></span>  

<span data-ttu-id="9db55-154">En el paso siguiente de hello, agregará una acción de Twitter que registrará un tweet usar algunas de las propiedades de Hola de cada tweet que se ha publicado por un usuario que tenga más de 50 seguidores.</span><span class="sxs-lookup"><span data-stu-id="9db55-154">In hello next step, you will add a Twitter action that will post a tweet using some of hello properties of each tweet that has been posted by a user who has more than 50 followers.</span></span>  

1. <span data-ttu-id="9db55-155">Seleccione **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="9db55-155">Select **Add an action**.</span></span> <span data-ttu-id="9db55-156">Esto abre el control de búsqueda de Hola donde puede buscar otras acciones y desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="9db55-156">This opens hello search control where you can search for other actions and triggers.</span></span>  
   <span data-ttu-id="9db55-157">![Imagen de condición de Twitter 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span><span class="sxs-lookup"><span data-stu-id="9db55-157">![Twitter condition image 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span></span>   
2. <span data-ttu-id="9db55-158">Escriba *twitter* en el cuadro de búsqueda de hello, a continuación, seleccione hello **de Twitter: registrar un tweet** acción.</span><span class="sxs-lookup"><span data-stu-id="9db55-158">Enter *twitter* into hello search box then select hello **Twitter - Post a tweet** action.</span></span> <span data-ttu-id="9db55-159">Se abrirá hello **registrar un tweet** control donde se incluirá todos los detalles de tweet Hola expuesta.</span><span class="sxs-lookup"><span data-stu-id="9db55-159">This opens hello **Post a tweet** control where you will enter all details for hello tweet being posted.</span></span>      
   <span data-ttu-id="9db55-160">![Imagen de acción de Twitter 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span><span class="sxs-lookup"><span data-stu-id="9db55-160">![Twitter action image 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span></span>   
3. <span data-ttu-id="9db55-161">Seleccione hello **Tweet texto** control.</span><span class="sxs-lookup"><span data-stu-id="9db55-161">Select hello **Tweet text** control.</span></span> <span data-ttu-id="9db55-162">Todos los resultados de las acciones anteriores y los desencadenadores de aplicación lógica de hello están visibles.</span><span class="sxs-lookup"><span data-stu-id="9db55-162">All outputs from previous actions and triggers in hello logic app are now visible.</span></span> <span data-ttu-id="9db55-163">Puede seleccionar cualquiera de ellos y usarlas como parte del texto de tweet Hola de nuevo tweet de Hola.</span><span class="sxs-lookup"><span data-stu-id="9db55-163">You can select any of these and use them as part of hello tweet text of hello new tweet.</span></span>     
   <span data-ttu-id="9db55-164">![Imagen de acción de Twitter 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="9db55-164">![Twitter action image 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span></span>   
4. <span data-ttu-id="9db55-165">Seleccione **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="9db55-165">Select **User name**</span></span>   
5. <span data-ttu-id="9db55-166">Escriba *dice:* Hola tweet control de texto.</span><span class="sxs-lookup"><span data-stu-id="9db55-166">Enter *says:* in hello tweet text control.</span></span> <span data-ttu-id="9db55-167">Hágalo justo después del nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="9db55-167">Do this just after User name.</span></span>  
6. <span data-ttu-id="9db55-168">Seleccione *Tweet text (Texto del tweet)*.</span><span class="sxs-lookup"><span data-stu-id="9db55-168">Select *Tweet text*.</span></span>       
   <span data-ttu-id="9db55-169">![Imagen de acción de Twitter 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span><span class="sxs-lookup"><span data-stu-id="9db55-169">![Twitter action image 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span></span>   
7. <span data-ttu-id="9db55-170">Guarde el trabajo y enviar un tweet con hello #Seattle hashtag tooactivate el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9db55-170">Save your work and send a tweet with hello #Seattle hashtag tooactivate your workflow.</span></span>  


## <a name="connector-specific-details"></a><span data-ttu-id="9db55-171">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="9db55-171">Connector-specific details</span></span>

<span data-ttu-id="9db55-172">Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/twitterconnector/).</span><span class="sxs-lookup"><span data-stu-id="9db55-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twitterconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9db55-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9db55-173">Next steps</span></span>
[<span data-ttu-id="9db55-174">Creación de una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="9db55-174">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

