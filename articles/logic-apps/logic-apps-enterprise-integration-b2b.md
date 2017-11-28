---
title: "Creación de soluciones B2B: Azure Logic Apps | Microsoft Docs"
description: "Recepción de datos en aplicaciones lógicas mediante las características B2B de Enterprise Integration Pack"
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
ms.openlocfilehash: 0625787ddcbc0091e70b111f687e25929720ad15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="receive-data-in-logic-apps-with-the-b2b-features-in-the-enterprise-integration-pack"></a><span data-ttu-id="64c14-103">Recepción de datos en aplicaciones lógicas con las características B2B de Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="64c14-103">Receive data in logic apps with the B2B features in the Enterprise Integration Pack</span></span>

<span data-ttu-id="64c14-104">Después de crear una cuenta de integración que tiene asociados y contratos, está listo para crear un flujo de trabajo de negocio a negocio (B2B) para la aplicación lógica mediante [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64c14-104">After you create an integration account that has partners and agreements, you are ready to create a business to business (B2B) workflow for your logic app with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64c14-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="64c14-105">Prerequisites</span></span>

<span data-ttu-id="64c14-106">Para utilizar las acciones AS2 y X12, debe disponer de una cuenta de Enterprise Integration.</span><span class="sxs-lookup"><span data-stu-id="64c14-106">To use the AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="64c14-107">Aprenda a [crear una cuenta de Enterprise Integration](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="64c14-107">Learn [how to create an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="64c14-108">Creación de una aplicación lógica con conectores B2B</span><span class="sxs-lookup"><span data-stu-id="64c14-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="64c14-109">Siga estos pasos para crear una aplicación lógica de B2B que use las acciones AS2 y X12 para recibir datos de un socio comercial:</span><span class="sxs-lookup"><span data-stu-id="64c14-109">Follow these steps to create a B2B logic app that uses the AS2 and X12 actions to receive data from a trading partner:</span></span>

1. <span data-ttu-id="64c14-110">Cree una aplicación lógica y [vincúlela a su cuenta de integración](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="64c14-110">Create a logic app, then [link your app to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="64c14-111">Agregue un desencadenador **Request - When an HTTP request is received** (Solicitar: cuando se reciba una solicitud HTTP) a la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="64c14-111">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="64c14-112">Para agregar la acción **Decode AS2** (Descodificar AS2), seleccione **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="64c14-112">To add the **Decode AS2** action, select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="64c14-113">Escriba la palabra **as2** en el cuadro de búsqueda para filtrar todas las acciones por la que desee usar.</span><span class="sxs-lookup"><span data-stu-id="64c14-113">To filter all actions to the one that you want, enter the word **as2** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="64c14-114">Seleccione la acción **AS2 - Decode AS2 message** (AS2: decodificar mensaje de AS2).</span><span class="sxs-lookup"><span data-stu-id="64c14-114">Select the **AS2 - Decode AS2 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="64c14-115">Agregue el **cuerpo** que desea usar como entrada.</span><span class="sxs-lookup"><span data-stu-id="64c14-115">Add the **Body** that you want to use as input.</span></span> <span data-ttu-id="64c14-116">En este ejemplo, seleccione el cuerpo de la solicitud HTTP que desencadena la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="64c14-116">In this example, select the body of the HTTP request that triggers the logic app.</span></span> <span data-ttu-id="64c14-117">O escriba una expresión que introduzca los encabezados en el campo **HEADERS**:</span><span class="sxs-lookup"><span data-stu-id="64c14-117">Or enter an expression that inputs the headers in the **HEADERS** field:</span></span>

    <span data-ttu-id="64c14-118">@triggerOutputs()['headers']</span><span class="sxs-lookup"><span data-stu-id="64c14-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="64c14-119">Agregue los **encabezados** de AS2 que puede encontrar en los encabezados de la solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="64c14-119">Add the required **Headers** for AS2, which you can find in the HTTP request headers.</span></span> <span data-ttu-id="64c14-120">En este ejemplo, seleccione los encabezados de la solicitud HTTP que desencadena la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="64c14-120">In this example, select the headers of the HTTP request that trigger the logic app.</span></span>

8. <span data-ttu-id="64c14-121">Ahora agregue la acción Decode X12 message (Descodificar mensaje de X12).</span><span class="sxs-lookup"><span data-stu-id="64c14-121">Now add the Decode X12 message action.</span></span> <span data-ttu-id="64c14-122">Seleccione **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="64c14-122">Select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="64c14-123">Escriba la palabra **x12** en el cuadro de búsqueda para filtrar todas las acciones por la que desee usar.</span><span class="sxs-lookup"><span data-stu-id="64c14-123">To filter all actions to the one that you want, enter the word **x12** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="64c14-124">Seleccione la acción **X12 - Decode X12 message** (X12: descodificar mensaje de X12)</span><span class="sxs-lookup"><span data-stu-id="64c14-124">Select the **X12 - Decode X12 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="64c14-125">Ahora debe especificar la entrada para esta acción.</span><span class="sxs-lookup"><span data-stu-id="64c14-125">Now you must specify the input to this action.</span></span> <span data-ttu-id="64c14-126">Esta entrada es la salida de la acción anterior de AS2.</span><span class="sxs-lookup"><span data-stu-id="64c14-126">This input is the output from the previous AS2 action.</span></span>

    <span data-ttu-id="64c14-127">El contenido real del mensaje está en un objeto JSON y está codificado en base64, por lo que debe especificar una expresión como entrada.</span><span class="sxs-lookup"><span data-stu-id="64c14-127">The actual message content is in a JSON object and is base64 encoded, so you must specify an expression as the input.</span></span> 
    <span data-ttu-id="64c14-128">Escriba la siguiente expresión en el campo de entrada **X12 FLAT FILE MESSAGE TO DECODE**:</span><span class="sxs-lookup"><span data-stu-id="64c14-128">Enter the following expression in the **X12 FLAT FILE MESSAGE TO DECODE** input field:</span></span>
    
    <span data-ttu-id="64c14-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="64c14-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="64c14-130">Ahora, agregue los pasos para descodificar los datos X12 recibidos del socio comercial y dé salida a los elementos en un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="64c14-130">Now add steps to decode the X12 data received from the trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="64c14-131">Para notificar al asociado la recepción de los datos, puede volver a enviar una respuesta que contenga la notificación de disposición del mensaje (MDN) AS2 en una acción de respuesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="64c14-131">To notify the partner that the data was received, you can send back a response containing the AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="64c14-132">Para agregar la acción **Response** (Respuesta), debe seleccionar **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="64c14-132">To add the **Response** action, choose **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="64c14-133">Escriba la palabra **response** en el cuadro de búsqueda para filtrar todas las acciones por la que desee usar.</span><span class="sxs-lookup"><span data-stu-id="64c14-133">To filter all actions to the one that you want, enter the word **response** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="64c14-134">Seleccione la acción **Response** (Respuesta).</span><span class="sxs-lookup"><span data-stu-id="64c14-134">Select the **Response** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="64c14-135">Establezca el campo **BODY** de la respuesta mediante la expresión siguiente para acceder a la MDN de la salida de la acción **Decode X12 message**:</span><span class="sxs-lookup"><span data-stu-id="64c14-135">To access the MDN from the output of the **Decode X12 message** action, set the response **BODY** field with this expression:</span></span>

    <span data-ttu-id="64c14-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="64c14-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="64c14-137">Guarde el trabajo.</span><span class="sxs-lookup"><span data-stu-id="64c14-137">Save your work.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="64c14-138">Con esto, ya ha terminado de configurar la aplicación lógica de B2B.</span><span class="sxs-lookup"><span data-stu-id="64c14-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="64c14-139">En una aplicación real, puede almacenar los datos X12 descodificados en un almacén de datos o una aplicación de línea de negocio (LOB).</span><span class="sxs-lookup"><span data-stu-id="64c14-139">In a real world application, you might want to store the decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="64c14-140">Puede agregar más acciones o escribir API personalizadas que se conecten a sus propias aplicaciones LOB, así como emplear estas API en su aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="64c14-140">To connect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="64c14-141">Características y casos de uso</span><span class="sxs-lookup"><span data-stu-id="64c14-141">Features and use cases</span></span>

* <span data-ttu-id="64c14-142">Las acciones de descodificación y codificación de AS2 y X12 le permiten intercambiar datos entre los socios comerciales mediante protocolos estándar de la industria en aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="64c14-142">The AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="64c14-143">Puede utilizar AS2 y X12 de forma independiente o conjunta para intercambiar datos con socios comerciales.</span><span class="sxs-lookup"><span data-stu-id="64c14-143">To exchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="64c14-144">Las acciones B2B le ayudan a crear fácilmente socios comerciales y contratos en la cuenta de integración, así como a usarlos en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="64c14-144">The B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="64c14-145">Al ampliar la aplicación lógica con otras acciones, podrá enviar y recibir datos entre otras aplicaciones y servicios como Salesforce.</span><span class="sxs-lookup"><span data-stu-id="64c14-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="64c14-146">Más información</span><span class="sxs-lookup"><span data-stu-id="64c14-146">Learn more</span></span>
[<span data-ttu-id="64c14-147">Más información acerca de Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="64c14-147">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
