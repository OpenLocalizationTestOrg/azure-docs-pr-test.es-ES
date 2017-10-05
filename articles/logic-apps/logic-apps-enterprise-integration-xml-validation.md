---
title: "Validación de documentos XML: Azure Logic Apps | Microsoft Docs"
description: "Validación de documentos XML con esquemas para Azure Logic Apps y escenarios B2B mediante Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8558efffa354cc4bb93820c837077ee997924c95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="validate-xml-for-enterprise-integration"></a><span data-ttu-id="02da0-103">Validación de documentos XML para la integración de empresas</span><span class="sxs-lookup"><span data-stu-id="02da0-103">Validate XML for enterprise integration</span></span>

<span data-ttu-id="02da0-104">A menudo, en los escenarios B2B, los asociados de un contrato deben asegurarse que los mensajes que intercambian son válidos para que pueda comenzar el procesamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="02da0-104">Often in B2B scenarios, the partners in an agreement must make sure that the messages they exchange are valid before data processing can start.</span></span> <span data-ttu-id="02da0-105">En Enterprise Integration Pack, puede usar el conector de validación XML para validar documentos con un esquema predefinido.</span><span class="sxs-lookup"><span data-stu-id="02da0-105">You can validate documents against a predefined schema by using the use the XML Validation connector in the Enterprise Integration Pack.</span></span>

## <a name="validate-a-document-with-the-xml-validation-connector"></a><span data-ttu-id="02da0-106">Validación de un documento con el conector de validación XML</span><span class="sxs-lookup"><span data-stu-id="02da0-106">Validate a document with the XML Validation connector</span></span>

1. <span data-ttu-id="02da0-107">Cree una aplicación lógica y [vincúlela a la cuenta de integración](../logic-apps/logic-apps-enterprise-integration-accounts.md "Aprenda a vincular una cuenta de integración a una aplicación lógica") que contenga el esquema que utilizará para validar los datos XML.</span><span class="sxs-lookup"><span data-stu-id="02da0-107">Create a logic app, and [link the app to the integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that has the schema you want to use for validating XML data.</span></span>

2. <span data-ttu-id="02da0-108">Agregue un desencadenador **Request - When an HTTP request is received** (Solicitar: cuando se reciba una solicitud HTTP) a la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="02da0-108">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. <span data-ttu-id="02da0-109">Agregue la acción **XML Validation** (Validación XML), pero seleccione antes **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="02da0-109">To add the **XML Validation** action, choose **Add an action**.</span></span>

4. <span data-ttu-id="02da0-110">Escriba *xml* en el cuadro de búsqueda para filtrar todas las acciones hasta encontrar la que desea usar.</span><span class="sxs-lookup"><span data-stu-id="02da0-110">To filter all the actions to the one that you want, enter *xml* in the search box.</span></span> <span data-ttu-id="02da0-111">Seleccione **XML Validation** (Validación XML).</span><span class="sxs-lookup"><span data-stu-id="02da0-111">Choose **XML Validation**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. <span data-ttu-id="02da0-112">Para especificar el contenido XML que desea validar, seleccione **CONTENIDO**.</span><span class="sxs-lookup"><span data-stu-id="02da0-112">To specify the XML content that you want to validate, select **CONTENT**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. <span data-ttu-id="02da0-113">Elija la etiqueta Cuerpo como el contenido que quiere validar.</span><span class="sxs-lookup"><span data-stu-id="02da0-113">Select the body tag as the content that you want to validate.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. <span data-ttu-id="02da0-114">Para especificar el esquema que desea usar para validar la entrada de *contenido* anterior, elija **NOMBRE DE ESQUEMA**.</span><span class="sxs-lookup"><span data-stu-id="02da0-114">To specify the schema you want to use for validating the previous *content* input, choose **SCHEMA NAME**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. <span data-ttu-id="02da0-115">Guarde el trabajo</span><span class="sxs-lookup"><span data-stu-id="02da0-115">Save your work</span></span>  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

<span data-ttu-id="02da0-116">Con esto, ha terminado de configurar el conector de validación.</span><span class="sxs-lookup"><span data-stu-id="02da0-116">You are now done with setting up your validation connector.</span></span> <span data-ttu-id="02da0-117">En una aplicación real, podría almacenar los datos validados en una aplicación de línea de negocio (LOB) como SalesForce.</span><span class="sxs-lookup"><span data-stu-id="02da0-117">In a real world application, you might want to store the validated data in a line-of-business (LOB) app like SalesForce.</span></span> <span data-ttu-id="02da0-118">Para enviar la salida validada a Salesforce, agregue una acción.</span><span class="sxs-lookup"><span data-stu-id="02da0-118">To send the validated output to Salesforce, add an action.</span></span>

<span data-ttu-id="02da0-119">Para probar la acción de validación realice una solicitud al punto de conexión HTTP.</span><span class="sxs-lookup"><span data-stu-id="02da0-119">To test your validation action, make a request to the HTTP endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02da0-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="02da0-120">Next steps</span></span>
[<span data-ttu-id="02da0-121">Más información sobre Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="02da0-121">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Información sobre Enterprise Integration Pack")   

