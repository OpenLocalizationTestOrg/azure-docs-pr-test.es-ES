---
title: Aprenda a usar el conector de Twitter en Logic Apps | Microsoft Docs
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
ms.openlocfilehash: be8163043535833ce45b3d50939a537406cf8152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-twitter-connector"></a><span data-ttu-id="621da-103">Introducción al conector de Twitter</span><span class="sxs-lookup"><span data-stu-id="621da-103">Get started with the Twitter connector</span></span>
<span data-ttu-id="621da-104">Con el conector de Twitter puede:</span><span class="sxs-lookup"><span data-stu-id="621da-104">With the Twitter connector you can:</span></span>

* <span data-ttu-id="621da-105">Publicar y obtener tweets</span><span class="sxs-lookup"><span data-stu-id="621da-105">Post tweets and get tweets</span></span>
* <span data-ttu-id="621da-106">Acceder a escalas de tiempo, amigos y seguidores</span><span class="sxs-lookup"><span data-stu-id="621da-106">Access timelines, friends and followers</span></span>
* <span data-ttu-id="621da-107">Ejecutar cualquiera de las demás acciones y desencadenadores que se describen a continuación</span><span class="sxs-lookup"><span data-stu-id="621da-107">Perform any of the other actions and triggers described below</span></span>  

<span data-ttu-id="621da-108">Para poder usar [un conector](apis-list.md), primero debe crear una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="621da-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="621da-109">Por tanto, puede comenzar [creando una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="621da-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>  

## <a name="connect-to-twitter"></a><span data-ttu-id="621da-110">Conexión a Twitter</span><span class="sxs-lookup"><span data-stu-id="621da-110">Connect to Twitter</span></span>
<span data-ttu-id="621da-111">Para que la aplicación lógica pueda acceder a un servicio, primero debe crear una *conexión* con dicho servicio.</span><span class="sxs-lookup"><span data-stu-id="621da-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="621da-112">Una [conexión](connectors-overview.md) proporciona conectividad entre una aplicación lógica y otro servicio.</span><span class="sxs-lookup"><span data-stu-id="621da-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-twitter"></a><span data-ttu-id="621da-113">Creación de una conexión a Twitter</span><span class="sxs-lookup"><span data-stu-id="621da-113">Create a connection to Twitter</span></span>
> [!INCLUDE [Steps to create a connection to Twitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a><span data-ttu-id="621da-114">Uso de un desencadenador de Twitter</span><span class="sxs-lookup"><span data-stu-id="621da-114">Use a Twitter trigger</span></span>
<span data-ttu-id="621da-115">Un desencadenador es un evento que se puede utilizar para iniciar el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="621da-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="621da-116">[Más información sobre los desencadenadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="621da-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="621da-117">En este ejemplo, le mostraré cómo usar el desencadenador **When a new tweet is posted (Cuando se publica un nuevo tweet)** para buscar #Seattle y, si se encuentra #Seattle, actualizar un archivo en Dropbox con el texto del tweet.</span><span class="sxs-lookup"><span data-stu-id="621da-117">In this example, I will show you how to use the **When a new tweet is posted**  trigger to search for #Seattle and, if #Seattle is found, update a file in Dropbox with the text from the tweet.</span></span> <span data-ttu-id="621da-118">En un ejemplo de la empresa, puede buscar el nombre de su compañía y actualizar una base de datos SQL con el texto del tweet.</span><span class="sxs-lookup"><span data-stu-id="621da-118">In an enterprise example, you could search for the name of your company and update a SQL database with the text from the tweet.</span></span>

1. <span data-ttu-id="621da-119">Escriba *twitter* en el cuadro de búsqueda del Diseñador de Logic Apps y seleccione el desencadenador **Twitter - When a new tweet is posted (Twitter - Cuando se publica un nuevo tweet)**.</span><span class="sxs-lookup"><span data-stu-id="621da-119">Enter *twitter* in the search box on the logic apps designer then select the **Twitter - When a new tweet is posted**  trigger</span></span>   
   <span data-ttu-id="621da-120">![Imagen de desencadenador de Twitter 1](./media/connectors-create-api-twitter/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="621da-120">![Twitter trigger image 1](./media/connectors-create-api-twitter/trigger-1.png)</span></span>  
2. <span data-ttu-id="621da-121">Escriba *#Seattle* en el control **Buscar texto**.</span><span class="sxs-lookup"><span data-stu-id="621da-121">Enter *#Seattle* in the **Search Text** control</span></span>  
   <span data-ttu-id="621da-122">![Imagen de desencadenador de Twitter 2](./media/connectors-create-api-twitter/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="621da-122">![Twitter trigger image 2](./media/connectors-create-api-twitter/trigger-2.png)</span></span> 

<span data-ttu-id="621da-123">En este punto, la aplicación lógica se ha configurado con un desencadenador que iniciará una ejecución de los otros desencadenadores y acciones en el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="621da-123">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="621da-124">Para que una aplicación lógica sea funcional, debe contener al menos un desencadenador y una acción.</span><span class="sxs-lookup"><span data-stu-id="621da-124">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="621da-125">Siga los pasos que se describen en la sección siguiente para agregar una acción.</span><span class="sxs-lookup"><span data-stu-id="621da-125">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="621da-126">Agregar una condición</span><span class="sxs-lookup"><span data-stu-id="621da-126">Add a condition</span></span>
<span data-ttu-id="621da-127">Puesto que solo estamos interesados en tweets de usuarios con más de 50 seguidores, primero se debe agregar a la aplicación lógica una condición que confirme el número de seguidores.</span><span class="sxs-lookup"><span data-stu-id="621da-127">Since we are only interested in tweets from users with more than 50 users, a condition that confirms the number of followers must first be added to the logic app.</span></span>  

1. <span data-ttu-id="621da-128">Seleccione **+ Nuevo paso** para agregar la acción que quiere que se ejecute cuando se encuentre #Seattle en un nuevo tweet.</span><span class="sxs-lookup"><span data-stu-id="621da-128">Select **+ New step** to add the action you would like to take when #Seattle is found in a new tweet</span></span>  
   <span data-ttu-id="621da-129">![Imagen de acción de Twitter 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="621da-129">![Twitter action image 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span></span>  
2. <span data-ttu-id="621da-130">Seleccione el vínculo **Agregar una condición**.</span><span class="sxs-lookup"><span data-stu-id="621da-130">Select the **Add a condition** link.</span></span>  
   <span data-ttu-id="621da-131">![Imagen de condición de Twitter 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span><span class="sxs-lookup"><span data-stu-id="621da-131">![Twitter condition image 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span></span>  
   <span data-ttu-id="621da-132">Se abrirá el control **Condición** donde puede comprobar las condiciones como *es igual a*, *es menor que*, *es mayor que*, *contiene*, etc.</span><span class="sxs-lookup"><span data-stu-id="621da-132">This opens the **Condition** control where you can check conditions such as *is equal to*, *is less than*, *is greater than*, *contains*, etc.</span></span>  
   <span data-ttu-id="621da-133">![Imagen de condición de Twitter 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span><span class="sxs-lookup"><span data-stu-id="621da-133">![Twitter condition image 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span></span>   
3. <span data-ttu-id="621da-134">Seleccione el control **Elegir un valor**.</span><span class="sxs-lookup"><span data-stu-id="621da-134">Select the **Choose a value** control.</span></span>  
   <span data-ttu-id="621da-135">En este control, puede seleccionar una o varias de las propiedades de cualquier acción o desencadenador anterior como el valor cuya condición se evaluará como True o False.</span><span class="sxs-lookup"><span data-stu-id="621da-135">In this control, you can select one or more of the properties from any previous actions or triggers as the value whose condition will be evaluated to true or false.</span></span>
   <span data-ttu-id="621da-136">![Imagen de condición de Twitter 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span><span class="sxs-lookup"><span data-stu-id="621da-136">![Twitter condition image 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span></span>   
4. <span data-ttu-id="621da-137">Seleccione **…** para expandir la lista de propiedades y ver todas las propiedades que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="621da-137">Select the **...** to expand the list of properties so you can see all the properties that are available.</span></span>        
   <span data-ttu-id="621da-138">![Imagen de condición de Twitter 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span><span class="sxs-lookup"><span data-stu-id="621da-138">![Twitter condition image 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span></span>   
5. <span data-ttu-id="621da-139">Seleccione la propiedad **Número de seguidores**.</span><span class="sxs-lookup"><span data-stu-id="621da-139">Select the **Followers count** property.</span></span>    
   <span data-ttu-id="621da-140">![Imagen de condición de Twitter 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span><span class="sxs-lookup"><span data-stu-id="621da-140">![Twitter condition image 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span></span>   
6. <span data-ttu-id="621da-141">Observe que la propiedad de número de seguidores ahora está en el control de valor.</span><span class="sxs-lookup"><span data-stu-id="621da-141">Notice the Followers count property is now in the value control.</span></span>    
   ![Imagen de condición de Twitter 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. <span data-ttu-id="621da-143">Seleccione **es mayor que** de la lista de operadores.</span><span class="sxs-lookup"><span data-stu-id="621da-143">Select **is greater than** from the operators list.</span></span>    
   <span data-ttu-id="621da-144">![Imagen de condición de Twitter 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span><span class="sxs-lookup"><span data-stu-id="621da-144">![Twitter condition image 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span></span>   
8. <span data-ttu-id="621da-145">Escriba 50 como el operando para el operador *es mayor que*.</span><span class="sxs-lookup"><span data-stu-id="621da-145">Enter 50 as the operand for the *is greater than* operator.</span></span>  
   <span data-ttu-id="621da-146">Se agrega la condición.</span><span class="sxs-lookup"><span data-stu-id="621da-146">The condition is now added.</span></span> <span data-ttu-id="621da-147">Guarde su trabajo mediante el vínculo **Guardar** en el menú superior.</span><span class="sxs-lookup"><span data-stu-id="621da-147">Save your work using the **Save** link on the menu above.</span></span>    
   <span data-ttu-id="621da-148">![Imagen de condición de Twitter 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span><span class="sxs-lookup"><span data-stu-id="621da-148">![Twitter condition image 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span></span>   

## <a name="use-a-twitter-action"></a><span data-ttu-id="621da-149">Uso de una acción de Twitter</span><span class="sxs-lookup"><span data-stu-id="621da-149">Use a Twitter action</span></span>
<span data-ttu-id="621da-150">Una acción es una operación que se lleva a cabo mediante el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="621da-150">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="621da-151">[Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="621da-151">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="621da-152">Ahora que ha agregado un desencadenador, siga estos pasos para incorporar una acción que publicará un nuevo tweet con el contenido de los tweets detectados por el desencadenador.</span><span class="sxs-lookup"><span data-stu-id="621da-152">Now that you have added a trigger, follow these steps to add an action that will post a new tweet with the contents of the tweets found by the trigger.</span></span> <span data-ttu-id="621da-153">Para los fines de este tutorial, solo se publicarán tweets de los usuarios con más de 50 seguidores.</span><span class="sxs-lookup"><span data-stu-id="621da-153">For the purposes of this walk-through only tweets from users with more than 50 followers will be posted.</span></span>  

<span data-ttu-id="621da-154">En el paso siguiente, agregará una acción de Twitter que publicará un tweet utilizando algunas de las propiedades de cada tweet publicado por un usuario que tenga más de 50 seguidores.</span><span class="sxs-lookup"><span data-stu-id="621da-154">In the next step, you will add a Twitter action that will post a tweet using some of the properties of each tweet that has been posted by a user who has more than 50 followers.</span></span>  

1. <span data-ttu-id="621da-155">Seleccione **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="621da-155">Select **Add an action**.</span></span> <span data-ttu-id="621da-156">Esto abre el control de búsqueda, donde puede buscar otras acciones y desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="621da-156">This opens the search control where you can search for other actions and triggers.</span></span>  
   <span data-ttu-id="621da-157">![Imagen de condición de Twitter 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span><span class="sxs-lookup"><span data-stu-id="621da-157">![Twitter condition image 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span></span>   
2. <span data-ttu-id="621da-158">Escriba *twitter* en el cuadro de búsqueda, después, seleccione la acción **Twitter - Post a tweet (Twitter - Publicar un tweet)**.</span><span class="sxs-lookup"><span data-stu-id="621da-158">Enter *twitter* into the search box then select the **Twitter - Post a tweet** action.</span></span> <span data-ttu-id="621da-159">Se abrirá el control **Post a tweet (Publicar un tweet)** donde especificará todos los detalles para el tweet publicado.</span><span class="sxs-lookup"><span data-stu-id="621da-159">This opens the **Post a tweet** control where you will enter all details for the tweet being posted.</span></span>      
   <span data-ttu-id="621da-160">![Imagen de acción de Twitter 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span><span class="sxs-lookup"><span data-stu-id="621da-160">![Twitter action image 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span></span>   
3. <span data-ttu-id="621da-161">Seleccione el control **Tweet text (Texto del tweet)**.</span><span class="sxs-lookup"><span data-stu-id="621da-161">Select the **Tweet text** control.</span></span> <span data-ttu-id="621da-162">Todos los resultados de las acciones y desencadenadores anteriores de la aplicación lógica ya están visibles.</span><span class="sxs-lookup"><span data-stu-id="621da-162">All outputs from previous actions and triggers in the logic app are now visible.</span></span> <span data-ttu-id="621da-163">Puede seleccionar cualquiera de ellos y usarlos como parte del texto del tweet del nuevo tweet.</span><span class="sxs-lookup"><span data-stu-id="621da-163">You can select any of these and use them as part of the tweet text of the new tweet.</span></span>     
   <span data-ttu-id="621da-164">![Imagen de acción de Twitter 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="621da-164">![Twitter action image 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span></span>   
4. <span data-ttu-id="621da-165">Seleccione **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="621da-165">Select **User name**</span></span>   
5. <span data-ttu-id="621da-166">Escriba *dice:* en el control del texto del tweet.</span><span class="sxs-lookup"><span data-stu-id="621da-166">Enter *says:* in the tweet text control.</span></span> <span data-ttu-id="621da-167">Hágalo justo después del nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="621da-167">Do this just after User name.</span></span>  
6. <span data-ttu-id="621da-168">Seleccione *Tweet text (Texto del tweet)*.</span><span class="sxs-lookup"><span data-stu-id="621da-168">Select *Tweet text*.</span></span>       
   <span data-ttu-id="621da-169">![Imagen de acción de Twitter 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span><span class="sxs-lookup"><span data-stu-id="621da-169">![Twitter action image 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span></span>   
7. <span data-ttu-id="621da-170">Guarde el trabajo y envíe un tweet con el hashtag #Seattle para activar el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="621da-170">Save your work and send a tweet with the #Seattle hashtag to activate your workflow.</span></span>  


## <a name="connector-specific-details"></a><span data-ttu-id="621da-171">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="621da-171">Connector-specific details</span></span>

<span data-ttu-id="621da-172">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/twitterconnector/).</span><span class="sxs-lookup"><span data-stu-id="621da-172">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/twitterconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="621da-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="621da-173">Next steps</span></span>
[<span data-ttu-id="621da-174">Creación de una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="621da-174">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

