---
title: "Hola aaaUse conector demora en las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Conectar tooSlack en las aplicaciones lógicas"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a><span data-ttu-id="1d3f5-103">Empezar a trabajar con conector demora Hola</span><span class="sxs-lookup"><span data-stu-id="1d3f5-103">Get started with hello Slack connector</span></span>
<span data-ttu-id="1d3f5-104">Slack es una herramienta de comunicación de equipo, que reúne todas las comunicaciones del equipo en un solo lugar, inmediatamente localizables y disponibles dondequiera que vaya.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="1d3f5-105">Empiece por crear una aplicación lógica ahora. Para ello, consulte [Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1d3f5-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tooslack"></a><span data-ttu-id="1d3f5-106">Crear una conexión tooSlack</span><span class="sxs-lookup"><span data-stu-id="1d3f5-106">Create a connection tooSlack</span></span>
<span data-ttu-id="1d3f5-107">Conector de demora de hello toouse, cree primero un **conexión** especifique los detalles de Hola de estas propiedades:</span><span class="sxs-lookup"><span data-stu-id="1d3f5-107">toouse hello Slack connector, you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="1d3f5-108">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1d3f5-108">Property</span></span> | <span data-ttu-id="1d3f5-109">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1d3f5-109">Required</span></span> | <span data-ttu-id="1d3f5-110">Descripción</span><span class="sxs-lookup"><span data-stu-id="1d3f5-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1d3f5-111">Se necesita el cifrado de tokens</span><span class="sxs-lookup"><span data-stu-id="1d3f5-111">Token</span></span> |<span data-ttu-id="1d3f5-112">Sí</span><span class="sxs-lookup"><span data-stu-id="1d3f5-112">Yes</span></span> |<span data-ttu-id="1d3f5-113">Proporcionar credenciales de Slack</span><span class="sxs-lookup"><span data-stu-id="1d3f5-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="1d3f5-114">Siga estos pasos toosign en Slack y la configuración de hello completa de hello demora **conexión** en la aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="1d3f5-114">Follow these steps toosign into Slack, and complete hello configuration of hello Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="1d3f5-115">Seleccione **Periodicidad**</span><span class="sxs-lookup"><span data-stu-id="1d3f5-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="1d3f5-116">Seleccione un valor para **Frequency** (Frecuencia) y especifique el correspondiente a **Interval** (Intervalo)</span><span class="sxs-lookup"><span data-stu-id="1d3f5-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="1d3f5-117">Seleccione **Add an action**(Agregar una acción)</span><span class="sxs-lookup"><span data-stu-id="1d3f5-117">Select **Add an action**</span></span>  
   <span data-ttu-id="1d3f5-118">![Configurar Slack][1]</span><span class="sxs-lookup"><span data-stu-id="1d3f5-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="1d3f5-119">Escriba demora en el cuadro de búsqueda de Hola y espere Hola búsqueda tooreturn todas las entradas con demora en nombre de Hola</span><span class="sxs-lookup"><span data-stu-id="1d3f5-119">Enter Slack in hello search box and wait for hello search tooreturn all entries with Slack in hello name</span></span>
5. <span data-ttu-id="1d3f5-120">Seleccione **Slack - exponer mensaje**</span><span class="sxs-lookup"><span data-stu-id="1d3f5-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="1d3f5-121">Seleccione **iniciar sesión en tooSlack**:</span><span class="sxs-lookup"><span data-stu-id="1d3f5-121">Select **Sign in tooSlack**:</span></span>  
   <span data-ttu-id="1d3f5-122">![Configurar Slack][2]</span><span class="sxs-lookup"><span data-stu-id="1d3f5-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="1d3f5-123">Proporcione su toosign credenciales demora en la aplicación de hello tooauthorize</span><span class="sxs-lookup"><span data-stu-id="1d3f5-123">Provide your Slack credentials toosign in tooauthorize hello  application</span></span>    
   ![Configurar Slack][3]  
8. <span data-ttu-id="1d3f5-125">Podrá registro de la organización tooyour redirigida en la página.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-125">You'll be redirected tooyour organization's Log in page.</span></span> <span data-ttu-id="1d3f5-126">**Autorizar** toointeract demora con la aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="1d3f5-126">**Authorize** Slack toointeract with your logic app:</span></span>      
   <span data-ttu-id="1d3f5-127">![Configurar Slack][5]</span><span class="sxs-lookup"><span data-stu-id="1d3f5-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="1d3f5-128">Una vez completa la autorización de hello estará tooyour redirigida lógica aplicación toocomplete, mediante la configuración de hello **una demora: obtener todos los mensajes** sección.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-128">After hello authorization completes you'll be redirected tooyour logic app toocomplete it by configuring hello **Slack - Get all messages** section.</span></span> <span data-ttu-id="1d3f5-129">Agregue otros desencadenadores y acciones que necesite.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="1d3f5-130">![Configurar Slack][6]</span><span class="sxs-lookup"><span data-stu-id="1d3f5-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="1d3f5-131">Guarde su trabajo mediante la selección **guardar** en la barra de menús de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="1d3f5-131">Save your work by selecting **Save** on hello menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="1d3f5-132">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="1d3f5-132">Connector-specific details</span></span>

<span data-ttu-id="1d3f5-133">Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/slack/).</span><span class="sxs-lookup"><span data-stu-id="1d3f5-133">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="1d3f5-134">Más conectores</span><span class="sxs-lookup"><span data-stu-id="1d3f5-134">More connectors</span></span>
<span data-ttu-id="1d3f5-135">Volver atrás toohello [lista de las API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="1d3f5-135">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
