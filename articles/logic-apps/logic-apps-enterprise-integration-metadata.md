---
title: "integración de aaaManage cuenta artefacto de metadatos: las aplicaciones lógicas de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 8de71bffa9f9975d5409716b2208fa6c3a9545d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a><span data-ttu-id="390d0-103">Administración de metadatos de artefactos en cuentas de integración para aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="390d0-103">Manage artifact metadata in integration accounts for logic apps</span></span>

<span data-ttu-id="390d0-104">Puede definir metadatos personalizados para artefactos en cuentas de integración y recuperar metadatos durante el tiempo de ejecución para su aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="390d0-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span></span> <span data-ttu-id="390d0-105">Por ejemplo, puede especificar metadatos para artefactos como asociados, acuerdos, esquemas y asignaciones: todos almacenan metadatos usando pares de clave-valor.</span><span class="sxs-lookup"><span data-stu-id="390d0-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span></span> <span data-ttu-id="390d0-106">Actualmente, los artefactos no pueden crear metadatos a través de la interfaz de usuario, pero puede usar las API de REST toocreate metadatos.</span><span class="sxs-lookup"><span data-stu-id="390d0-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs toocreate metadata.</span></span> <span data-ttu-id="390d0-107">metadatos de tooadd al crear o seleccionar un partner, contrato o esquema Hola portal de Azure, elija **editar como JSON**.</span><span class="sxs-lookup"><span data-stu-id="390d0-107">tooadd metadata when you create or select a partner, agreement, or schema in hello Azure portal, choose **Edit as JSON**.</span></span> <span data-ttu-id="390d0-108">tooretrieve artefacto metadatos en aplicaciones lógicas, puede usar características de búsqueda de artefactos de cuenta de integración de Hola.</span><span class="sxs-lookup"><span data-stu-id="390d0-108">tooretrieve artifact metadata in logic apps, you can use hello Integration Account Artifact Lookup feature.</span></span>

## <a name="add-metadata-tooartifacts-in-integration-accounts"></a><span data-ttu-id="390d0-109">Agregar metadatos tooartifacts en cuentas de integración</span><span class="sxs-lookup"><span data-stu-id="390d0-109">Add metadata tooartifacts in integration accounts</span></span>

1. <span data-ttu-id="390d0-110">Cree una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="390d0-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>

2. <span data-ttu-id="390d0-111">Agregar una cuenta de integración de tooyour de artefacto, por ejemplo, un [asociado](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [acuerdo](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), o [esquema](logic-apps-enterprise-integration-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="390d0-111">Add an artifact tooyour integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span></span>

3.  <span data-ttu-id="390d0-112">Seleccione el artefacto de hello, elija **editar como JSON**y escriba los detalles de los metadatos.</span><span class="sxs-lookup"><span data-stu-id="390d0-112">Select hello artifact, choose **Edit as JSON**, and enter metadata details.</span></span>

    ![Introducción de los metadatos](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a><span data-ttu-id="390d0-114">Recuperación de metadatos de artefactos para aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="390d0-114">Retrieve metadata from artifacts for logic apps</span></span>

1. <span data-ttu-id="390d0-115">Cree una [aplicación lógica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="390d0-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="390d0-116">Crear un [vínculo desde su cuenta de lógica de aplicación tooyour integración](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span><span class="sxs-lookup"><span data-stu-id="390d0-116">Create a [link from your logic app tooyour integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span></span> 

3. <span data-ttu-id="390d0-117">En el Diseñador de la lógica de aplicaciones, agregar un desencadenador como *solicitar* o *HTTP* tooyour aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="390d0-117">In Logic App Designer, add a trigger like *Request* or *HTTP* tooyour logic app.</span></span>

4.  <span data-ttu-id="390d0-118">Elija **Paso siguiente** > **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="390d0-118">Choose **Next Step** > **Add an action**.</span></span> <span data-ttu-id="390d0-119">Busque una *integración* para poder encontrar y seleccionar **Búsqueda de artefactos de la cuenta de integración**.</span><span class="sxs-lookup"><span data-stu-id="390d0-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span></span>

    ![Seleccione Búsqueda de artefactos de la cuenta de integración.](media/logic-apps-enterprise-integration-metadata/image2.png)

5. <span data-ttu-id="390d0-121">Seleccione hello **tipo de artefacto**y proporcionar hello **nombre del artefacto**.</span><span class="sxs-lookup"><span data-stu-id="390d0-121">Select hello **Artifact Type**, and provide hello **Artifact Name**.</span></span>

    ![Seleccione el tipo de artefacto y proporcione el nombre del artefacto.](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a><span data-ttu-id="390d0-123">Ejemplo: recuperación de metadatos de asociados</span><span class="sxs-lookup"><span data-stu-id="390d0-123">Example: Retrieve partner metadata</span></span>

<span data-ttu-id="390d0-124">Los metadatos del asociado tienen estos detalles de `routingUrl`:</span><span class="sxs-lookup"><span data-stu-id="390d0-124">Partner metadata has these `routingUrl` details:</span></span>

![Búsqueda de metadatos de "routingURL" de asociado](media/logic-apps-enterprise-integration-metadata/image6.png)

1. <span data-ttu-id="390d0-126">En su aplicación lógica, agregue su desencadenador, una acción **Cuenta de integración: Búsqueda de artefactos de la cuenta de integración** para su asociado y un **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="390d0-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span></span>

    ![Agregar el desencadenador, la búsqueda de artefactos y la aplicación de lógica de "HTTP" tooyour](media/logic-apps-enterprise-integration-metadata/image4.png)

2. <span data-ttu-id="390d0-128">Hola tooretrieve URI, vaya tooCode vista para la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="390d0-128">tooretrieve hello URI, go tooCode View for your logic app.</span></span> <span data-ttu-id="390d0-129">La definición de su aplicación lógica debería ser similar a la de este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="390d0-129">Your logic app definition should look like this example:</span></span>

    ![Buscar lookup](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a><span data-ttu-id="390d0-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="390d0-131">Next steps</span></span>
* [<span data-ttu-id="390d0-132">Más información sobre los contratos</span><span class="sxs-lookup"><span data-stu-id="390d0-132">Learn more about agreements</span></span>](logic-apps-enterprise-integration-agreements.md "Información sobre los contratos de integración de empresas")  
