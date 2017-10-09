---
title: "aaaValidate XML: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Validar XML con esquemas para los escenarios de aplicaciones de la lógica de Azure y B2B mediante Hola paquete de integración empresarial"
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
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a><span data-ttu-id="6e3fb-103">Validación de documentos XML para la integración de empresas</span><span class="sxs-lookup"><span data-stu-id="6e3fb-103">Validate XML for enterprise integration</span></span>

<span data-ttu-id="6e3fb-104">A menudo en escenarios de B2B, socios de hello en un acuerdo deben asegurarse que los mensajes de Hola intercambian son válidos para que pueda comenzar el procesamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="6e3fb-104">Often in B2B scenarios, hello partners in an agreement must make sure that hello messages they exchange are valid before data processing can start.</span></span> <span data-ttu-id="6e3fb-105">Puede validar documentos con respecto a un esquema predefinido mediante el conector de validación de XML de Hola de uso de Hola Hola paquete de integración empresarial.</span><span class="sxs-lookup"><span data-stu-id="6e3fb-105">You can validate documents against a predefined schema by using hello use hello XML Validation connector in hello Enterprise Integration Pack.</span></span>

## <a name="validate-a-document-with-hello-xml-validation-connector"></a><span data-ttu-id="6e3fb-106">Validar un documento con el conector de validación XML Hola</span><span class="sxs-lookup"><span data-stu-id="6e3fb-106">Validate a document with hello XML Validation connector</span></span>

1. <span data-ttu-id="6e3fb-107">Crear una aplicación de lógica, y [vincular la cuenta de toohello de integración de aplicación Hola](../logic-apps/logic-apps-enterprise-integration-accounts.md "Obtenga información acerca de una aplicación de la lógica de la cuenta tooa integración toolink") con esquema Hola desea toouse para validar datos XML.</span><span class="sxs-lookup"><span data-stu-id="6e3fb-107">Create a logic app, and [link hello app toohello integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app") that has hello schema you want toouse for validating XML data.</span></span>

2. <span data-ttu-id="6e3fb-108">Agregar un **solicitar - se recibe la solicitud HTTP de un cuando** aplicación lógica de desencadenador tooyour.</span><span class="sxs-lookup"><span data-stu-id="6e3fb-108">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. <span data-ttu-id="6e3fb-109">Hola tooadd **validación XML** acción, elija **agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="6e3fb-109">tooadd hello **XML Validation** action, choose **Add an action**.</span></span>

4. <span data-ttu-id="6e3fb-110">toofilter todos Hola toohello de acciones que desea, escriba *xml* en el cuadro de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e3fb-110">toofilter all hello actions toohello one that you want, enter *xml* in hello search box.</span></span> <span data-ttu-id="6e3fb-111">Seleccione **XML Validation** (Validación XML).</span><span class="sxs-lookup"><span data-stu-id="6e3fb-111">Choose **XML Validation**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. <span data-ttu-id="6e3fb-112">Seleccione toospecify Hola contenido XML que desea toovalidate, **contenido**.</span><span class="sxs-lookup"><span data-stu-id="6e3fb-112">toospecify hello XML content that you want toovalidate, select **CONTENT**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. <span data-ttu-id="6e3fb-113">Seleccionar etiqueta body de hello como contenido que desea toovalidate Hola.</span><span class="sxs-lookup"><span data-stu-id="6e3fb-113">Select hello body tag as hello content that you want toovalidate.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. <span data-ttu-id="6e3fb-114">esquema de hello toospecify desea toouse para validar Hola anterior *contenido* de entrada, elija **nombre de esquema**.</span><span class="sxs-lookup"><span data-stu-id="6e3fb-114">toospecify hello schema you want toouse for validating hello previous *content* input, choose **SCHEMA NAME**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. <span data-ttu-id="6e3fb-115">Guarde el trabajo</span><span class="sxs-lookup"><span data-stu-id="6e3fb-115">Save your work</span></span>  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

<span data-ttu-id="6e3fb-116">Con esto, ha terminado de configurar el conector de validación.</span><span class="sxs-lookup"><span data-stu-id="6e3fb-116">You are now done with setting up your validation connector.</span></span> <span data-ttu-id="6e3fb-117">En una aplicación real, conviene toostore datos de hello validado en una aplicación de línea de negocio (LOB) como SalesForce.</span><span class="sxs-lookup"><span data-stu-id="6e3fb-117">In a real world application, you might want toostore hello validated data in a line-of-business (LOB) app like SalesForce.</span></span> <span data-ttu-id="6e3fb-118">toosend Hola tooSalesforce resultado validado, agregar una acción.</span><span class="sxs-lookup"><span data-stu-id="6e3fb-118">toosend hello validated output tooSalesforce, add an action.</span></span>

<span data-ttu-id="6e3fb-119">tootest su acción de validación, cree un punto de conexión de toohello HTTP de solicitud.</span><span class="sxs-lookup"><span data-stu-id="6e3fb-119">tootest your validation action, make a request toohello HTTP endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e3fb-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6e3fb-120">Next steps</span></span>
[<span data-ttu-id="6e3fb-121">Obtener más información sobre Hola paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="6e3fb-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial")   

