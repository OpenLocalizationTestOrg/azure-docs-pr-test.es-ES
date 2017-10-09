---
title: aaaCreate B2B solutions - Azure Logic Apps | Documentos de Microsoft
description: "Recibir datos en las aplicaciones lógicas mediante las características de hello B2B Hola paquete de integración empresarial"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a><span data-ttu-id="93e5d-103">Recibir datos en las aplicaciones lógicas con características de B2B Hola Hola paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="93e5d-103">Receive data in logic apps with hello B2B features in hello Enterprise Integration Pack</span></span>

<span data-ttu-id="93e5d-104">Después de crear una cuenta de la integración con socios comerciales y acuerdos, está listo toocreate un flujo de trabajo de toobusiness (B2B) para la aplicación lógica con hello [paquete de integración empresarial](logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="93e5d-104">After you create an integration account that has partners and agreements, you are ready toocreate a business toobusiness (B2B) workflow for your logic app with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93e5d-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="93e5d-105">Prerequisites</span></span>

<span data-ttu-id="93e5d-106">toouse Hola AS2 y X12 acciones, debe tener una cuenta de integración empresarial.</span><span class="sxs-lookup"><span data-stu-id="93e5d-106">toouse hello AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="93e5d-107">Obtenga información acerca de [toocreate una integración de Enterprise cuenta y cómo](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="93e5d-107">Learn [how toocreate an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="93e5d-108">Creación de una aplicación lógica con conectores B2B</span><span class="sxs-lookup"><span data-stu-id="93e5d-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="93e5d-109">Siga estos aplicación lógica de toocreate un B2B de pasos que usa Hola AS2 y X12 datos tooreceive de acciones de un socio comercial:</span><span class="sxs-lookup"><span data-stu-id="93e5d-109">Follow these steps toocreate a B2B logic app that uses hello AS2 and X12 actions tooreceive data from a trading partner:</span></span>

1. <span data-ttu-id="93e5d-110">Crear una aplicación de lógica, a continuación, [vincular su cuenta de integración de aplicaciones tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="93e5d-110">Create a logic app, then [link your app tooyour integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="93e5d-111">Agregar un **solicitar - se recibe la solicitud HTTP de un cuando** aplicación lógica de desencadenador tooyour.</span><span class="sxs-lookup"><span data-stu-id="93e5d-111">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="93e5d-112">Hola tooadd **descodificar AS2** acción, seleccione **agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="93e5d-112">tooadd hello **Decode AS2** action, select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="93e5d-113">toofilter todos los toohello de acciones que desea, escriba la palabra Hola **as2** en el cuadro de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="93e5d-113">toofilter all actions toohello one that you want, enter hello word **as2** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="93e5d-114">Seleccione hello **AS2 - mensaje AS2 descodificar** acción.</span><span class="sxs-lookup"><span data-stu-id="93e5d-114">Select hello **AS2 - Decode AS2 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="93e5d-115">Agregar hello **cuerpo** que desea toouse como entrada.</span><span class="sxs-lookup"><span data-stu-id="93e5d-115">Add hello **Body** that you want toouse as input.</span></span> <span data-ttu-id="93e5d-116">En este ejemplo, seleccione el cuerpo de saludo de solicitud HTTP de Hola que desencadenadores Hola aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="93e5d-116">In this example, select hello body of hello HTTP request that triggers hello logic app.</span></span> <span data-ttu-id="93e5d-117">O escriba una expresión que se dirige encabezados Hola Hola **ENCABEZADOS** campo:</span><span class="sxs-lookup"><span data-stu-id="93e5d-117">Or enter an expression that inputs hello headers in hello **HEADERS** field:</span></span>

    <span data-ttu-id="93e5d-118">@triggerOutputs()['headers']</span><span class="sxs-lookup"><span data-stu-id="93e5d-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="93e5d-119">Agregar Hola necesario **encabezados** para AS2, que puede encontrar en los encabezados de solicitud de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="93e5d-119">Add hello required **Headers** for AS2, which you can find in hello HTTP request headers.</span></span> <span data-ttu-id="93e5d-120">En este ejemplo, seleccione los encabezados de Hola de solicitud HTTP de hello esa aplicación de lógica de hello de desencadenador.</span><span class="sxs-lookup"><span data-stu-id="93e5d-120">In this example, select hello headers of hello HTTP request that trigger hello logic app.</span></span>

8. <span data-ttu-id="93e5d-121">Ahora, agregue la acción del mensaje Hola Decode X12.</span><span class="sxs-lookup"><span data-stu-id="93e5d-121">Now add hello Decode X12 message action.</span></span> <span data-ttu-id="93e5d-122">Seleccione **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="93e5d-122">Select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="93e5d-123">toofilter todos los toohello de acciones que desea, escriba la palabra Hola **x12** en el cuadro de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="93e5d-123">toofilter all actions toohello one that you want, enter hello word **x12** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="93e5d-124">Seleccione hello **X12-descodificar X12 mensaje** acción.</span><span class="sxs-lookup"><span data-stu-id="93e5d-124">Select hello **X12 - Decode X12 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="93e5d-125">Ahora debe especificar la acción de entrada toothis Hola.</span><span class="sxs-lookup"><span data-stu-id="93e5d-125">Now you must specify hello input toothis action.</span></span> <span data-ttu-id="93e5d-126">Esta entrada es la salida de hello de acción de AS2 anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="93e5d-126">This input is hello output from hello previous AS2 action.</span></span>

    <span data-ttu-id="93e5d-127">contenido real del mensaje de Hola está en un objeto JSON y está codificada en base64, por lo que debe especificar una expresión como entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="93e5d-127">hello actual message content is in a JSON object and is base64 encoded, so you must specify an expression as hello input.</span></span> 
    <span data-ttu-id="93e5d-128">Escriba Hola siguiente expresión en hello **X12 planos mensaje de archivo tooDECODE** campo de entrada:</span><span class="sxs-lookup"><span data-stu-id="93e5d-128">Enter hello following expression in hello **X12 FLAT FILE MESSAGE tooDECODE** input field:</span></span>
    
    <span data-ttu-id="93e5d-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="93e5d-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="93e5d-130">Ahora, agregue pasos de datos de hello X12 toodecode reciben de hello socio comercial y los elementos en un objeto JSON de salida.</span><span class="sxs-lookup"><span data-stu-id="93e5d-130">Now add steps toodecode hello X12 data received from hello trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="93e5d-131">se ha recibido el asociado de hello toonotify que Hola datos, se puede volver a enviar una respuesta que contiene Hola notificación de disposición de mensaje AS2 (MDN) en una acción de respuesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="93e5d-131">toonotify hello partner that hello data was received, you can send back a response containing hello AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="93e5d-132">Hola tooadd **respuesta** acción, elija **agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="93e5d-132">tooadd hello **Response** action, choose **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="93e5d-133">toofilter todos los toohello de acciones que desea, escriba la palabra Hola **respuesta** en el cuadro de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="93e5d-133">toofilter all actions toohello one that you want, enter hello word **response** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="93e5d-134">Seleccione hello **respuesta** acción.</span><span class="sxs-lookup"><span data-stu-id="93e5d-134">Select hello **Response** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="93e5d-135">tooaccess Hola MDN de salida de hello de hello **mensaje Decode X12** acción, respuesta de conjunto hello **cuerpo** campo con esta expresión:</span><span class="sxs-lookup"><span data-stu-id="93e5d-135">tooaccess hello MDN from hello output of hello **Decode X12 message** action, set hello response **BODY** field with this expression:</span></span>

    <span data-ttu-id="93e5d-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="93e5d-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="93e5d-137">Guarde el trabajo.</span><span class="sxs-lookup"><span data-stu-id="93e5d-137">Save your work.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="93e5d-138">Con esto, ya ha terminado de configurar la aplicación lógica de B2B.</span><span class="sxs-lookup"><span data-stu-id="93e5d-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="93e5d-139">En una aplicación real, le podría interesar toostore Hola descodificados X12 datos en un línea de negocio (LOB) aplicación o almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="93e5d-139">In a real world application, you might want toostore hello decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="93e5d-140">tooconnect sus propias aplicaciones LOB y usar estas API en la aplicación lógica, puede agregar más acciones o escribir API personalizadas.</span><span class="sxs-lookup"><span data-stu-id="93e5d-140">tooconnect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="93e5d-141">Características y casos de uso</span><span class="sxs-lookup"><span data-stu-id="93e5d-141">Features and use cases</span></span>

* <span data-ttu-id="93e5d-142">Hola AS2 y X12 descodificar y codificar acciones permiten intercambiar datos entre los socios comerciales mediante el uso de protocolos estándar del sector en las aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="93e5d-142">hello AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="93e5d-143">datos de tooexchange con socios comerciales, puede usar AS2 y X12 con o sin entre sí.</span><span class="sxs-lookup"><span data-stu-id="93e5d-143">tooexchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="93e5d-144">Hola B2B acciones ayudarle a crear los socios comerciales y acuerdos fácilmente en su cuenta de integración y usarlos en una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="93e5d-144">hello B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="93e5d-145">Al ampliar la aplicación lógica con otras acciones, podrá enviar y recibir datos entre otras aplicaciones y servicios como Salesforce.</span><span class="sxs-lookup"><span data-stu-id="93e5d-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="93e5d-146">Más información</span><span class="sxs-lookup"><span data-stu-id="93e5d-146">Learn more</span></span>
[<span data-ttu-id="93e5d-147">Obtener más información sobre Hola paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="93e5d-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
