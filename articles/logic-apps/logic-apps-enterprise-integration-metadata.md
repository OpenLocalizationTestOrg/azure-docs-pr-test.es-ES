---
title: "Administración de metadatos de artefactos de la cuenta de integración: Azure Logic Apps | Microsoft Docs"
description: "Agregue o recupere metadatos de artefactos de cuentas de integración para Azure Logic Apps"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 28bb8296ddd820ec5aa9793dc0928b4b1e67bf6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a><span data-ttu-id="bfef4-103">Administración de metadatos de artefactos en cuentas de integración para aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="bfef4-103">Manage artifact metadata in integration accounts for logic apps</span></span>

<span data-ttu-id="bfef4-104">Puede definir metadatos personalizados para artefactos en cuentas de integración y recuperar metadatos durante el tiempo de ejecución para su aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="bfef4-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span></span> <span data-ttu-id="bfef4-105">Por ejemplo, puede especificar metadatos para artefactos como asociados, acuerdos, esquemas y asignaciones: todos almacenan metadatos usando pares de clave-valor.</span><span class="sxs-lookup"><span data-stu-id="bfef4-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span></span> <span data-ttu-id="bfef4-106">Actualmente, los artefactos no pueden crear metadatos a través de la interfaz de usuario, pero puede usar API de REST para crear metadatos.</span><span class="sxs-lookup"><span data-stu-id="bfef4-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs to create metadata.</span></span> <span data-ttu-id="bfef4-107">Para agregar metadatos al crear o seleccionar un asociado, acuerdo o esquema en Azure Portal, elija **Editar como JSON**.</span><span class="sxs-lookup"><span data-stu-id="bfef4-107">To add metadata when you create or select a partner, agreement, or schema in the Azure portal, choose **Edit as JSON**.</span></span> <span data-ttu-id="bfef4-108">Para recuperar metadatos de artefactos en aplicaciones lógicas, puede usar la característica	 Búsqueda de artefactos de la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="bfef4-108">To retrieve artifact metadata in logic apps, you can use the Integration Account Artifact Lookup feature.</span></span>

## <a name="add-metadata-to-artifacts-in-integration-accounts"></a><span data-ttu-id="bfef4-109">Adición de metadatos a artefactos en cuentas de integración</span><span class="sxs-lookup"><span data-stu-id="bfef4-109">Add metadata to artifacts in integration accounts</span></span>

1. <span data-ttu-id="bfef4-110">Cree una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="bfef4-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>

2. <span data-ttu-id="bfef4-111">Agregue un artefacto a su cuenta de integración, por ejemplo, un [asociado](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), un [acuerdo](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements) o un [esquema](logic-apps-enterprise-integration-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="bfef4-111">Add an artifact to your integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span></span>

3.  <span data-ttu-id="bfef4-112">Seleccione el artefacto, elija **Editar como JSON** y escriba los detalles de los metadatos.</span><span class="sxs-lookup"><span data-stu-id="bfef4-112">Select the artifact, choose **Edit as JSON**, and enter metadata details.</span></span>

    ![Introducción de los metadatos](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a><span data-ttu-id="bfef4-114">Recuperación de metadatos de artefactos para aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="bfef4-114">Retrieve metadata from artifacts for logic apps</span></span>

1. <span data-ttu-id="bfef4-115">Cree una [aplicación lógica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="bfef4-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="bfef4-116">Cree un [vínculo desde su aplicación lógica a su cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span><span class="sxs-lookup"><span data-stu-id="bfef4-116">Create a [link from your logic app to your integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span></span> 

3. <span data-ttu-id="bfef4-117">En Diseñador de aplicación lógica, agregue un desencadenador como *Solicitud* o *HTTP* a su aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="bfef4-117">In Logic App Designer, add a trigger like *Request* or *HTTP* to your logic app.</span></span>

4.  <span data-ttu-id="bfef4-118">Elija **Paso siguiente** > **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="bfef4-118">Choose **Next Step** > **Add an action**.</span></span> <span data-ttu-id="bfef4-119">Busque una *integración* para poder encontrar y seleccionar **Búsqueda de artefactos de la cuenta de integración**.</span><span class="sxs-lookup"><span data-stu-id="bfef4-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span></span>

    ![Seleccione Búsqueda de artefactos de la cuenta de integración.](media/logic-apps-enterprise-integration-metadata/image2.png)

5. <span data-ttu-id="bfef4-121">Seleccione **Tipo de artefacto** y proporcione el **nombre del artefacto**.</span><span class="sxs-lookup"><span data-stu-id="bfef4-121">Select the **Artifact Type**, and provide the **Artifact Name**.</span></span>

    ![Seleccione el tipo de artefacto y proporcione el nombre del artefacto.](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a><span data-ttu-id="bfef4-123">Ejemplo: recuperación de metadatos de asociados</span><span class="sxs-lookup"><span data-stu-id="bfef4-123">Example: Retrieve partner metadata</span></span>

<span data-ttu-id="bfef4-124">Los metadatos del asociado tienen estos detalles de `routingUrl`:</span><span class="sxs-lookup"><span data-stu-id="bfef4-124">Partner metadata has these `routingUrl` details:</span></span>

![Búsqueda de metadatos de "routingURL" de asociado](media/logic-apps-enterprise-integration-metadata/image6.png)

1. <span data-ttu-id="bfef4-126">En su aplicación lógica, agregue su desencadenador, una acción **Cuenta de integración: Búsqueda de artefactos de la cuenta de integración** para su asociado y un **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="bfef4-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span></span>

    ![Adición de un desencadenador, una búsqueda de artefactos y un "HTTP" a su aplicación lógica](media/logic-apps-enterprise-integration-metadata/image4.png)

2. <span data-ttu-id="bfef4-128">Para recuperar el identificador URI, vaya a la vista de código de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="bfef4-128">To retrieve the URI, go to Code View for your logic app.</span></span> <span data-ttu-id="bfef4-129">La definición de su aplicación lógica debería ser similar a la de este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bfef4-129">Your logic app definition should look like this example:</span></span>

    ![Buscar lookup](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a><span data-ttu-id="bfef4-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bfef4-131">Next steps</span></span>
* [<span data-ttu-id="bfef4-132">Más información sobre los contratos</span><span class="sxs-lookup"><span data-stu-id="bfef4-132">Learn more about agreements</span></span>](logic-apps-enterprise-integration-agreements.md "Información sobre los contratos de integración de empresas")  
