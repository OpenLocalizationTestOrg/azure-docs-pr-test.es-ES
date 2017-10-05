---
title: Uso del conector de Slack en Azure Logic Apps | Microsoft Docs
description: "Conéctese a Slack en las aplicaciones lógicas"
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
ms.openlocfilehash: fc5fc128efe01bd0727e3ff30d8938918e89ac3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-slack-connector"></a><span data-ttu-id="d0eab-103">Introducción al conector de Slack</span><span class="sxs-lookup"><span data-stu-id="d0eab-103">Get started with the Slack connector</span></span>
<span data-ttu-id="d0eab-104">Slack es una herramienta de comunicación de equipo, que reúne todas las comunicaciones del equipo en un solo lugar, inmediatamente localizables y disponibles dondequiera que vaya.</span><span class="sxs-lookup"><span data-stu-id="d0eab-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="d0eab-105">Empiece por crear una aplicación lógica ahora. Para ello, consulte [Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d0eab-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-slack"></a><span data-ttu-id="d0eab-106">Creación de una conexión a Slack</span><span class="sxs-lookup"><span data-stu-id="d0eab-106">Create a connection to Slack</span></span>
<span data-ttu-id="d0eab-107">Para usar el conector de Slack, cree primero una **conexión** y, después, especifique los detalles de las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="d0eab-107">To use the Slack connector, you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="d0eab-108">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d0eab-108">Property</span></span> | <span data-ttu-id="d0eab-109">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d0eab-109">Required</span></span> | <span data-ttu-id="d0eab-110">Descripción</span><span class="sxs-lookup"><span data-stu-id="d0eab-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d0eab-111">Se necesita el cifrado de tokens</span><span class="sxs-lookup"><span data-stu-id="d0eab-111">Token</span></span> |<span data-ttu-id="d0eab-112">Sí</span><span class="sxs-lookup"><span data-stu-id="d0eab-112">Yes</span></span> |<span data-ttu-id="d0eab-113">Proporcionar credenciales de Slack</span><span class="sxs-lookup"><span data-stu-id="d0eab-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="d0eab-114">Siga estos pasos para iniciar sesión en Slack y completar la configuración de la **conexión** de Slack en la aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="d0eab-114">Follow these steps to sign into Slack, and complete the configuration of the Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="d0eab-115">Seleccione **Periodicidad**</span><span class="sxs-lookup"><span data-stu-id="d0eab-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="d0eab-116">Seleccione un valor para **Frequency** (Frecuencia) y especifique el correspondiente a **Interval** (Intervalo)</span><span class="sxs-lookup"><span data-stu-id="d0eab-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="d0eab-117">Seleccione **Add an action**(Agregar una acción)</span><span class="sxs-lookup"><span data-stu-id="d0eab-117">Select **Add an action**</span></span>  
   <span data-ttu-id="d0eab-118">![Configurar Slack][1]</span><span class="sxs-lookup"><span data-stu-id="d0eab-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="d0eab-119">Escriba Slack en el cuadro de búsqueda y espere a que la búsqueda devuelva todas las entradas que incluyan Slack en el nombre.</span><span class="sxs-lookup"><span data-stu-id="d0eab-119">Enter Slack in the search box and wait for the search to return all entries with Slack in the name</span></span>
5. <span data-ttu-id="d0eab-120">Seleccione **Slack - exponer mensaje**</span><span class="sxs-lookup"><span data-stu-id="d0eab-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="d0eab-121">Seleccione **Sign in to Slack** (Iniciar sesión en Slack):</span><span class="sxs-lookup"><span data-stu-id="d0eab-121">Select **Sign in to Slack**:</span></span>  
   <span data-ttu-id="d0eab-122">![Configurar Slack][2]</span><span class="sxs-lookup"><span data-stu-id="d0eab-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="d0eab-123">Especifique sus credenciales de Slack para iniciar sesión y autorizar la aplicación</span><span class="sxs-lookup"><span data-stu-id="d0eab-123">Provide your Slack credentials to sign in to authorize the  application</span></span>    
   ![Configurar Slack][3]  
8. <span data-ttu-id="d0eab-125">Se le redirigirá a la página de inicio de sesión de su organización.</span><span class="sxs-lookup"><span data-stu-id="d0eab-125">You'll be redirected to your organization's Log in page.</span></span> <span data-ttu-id="d0eab-126">**Autorice** la interacción de Slack con la aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="d0eab-126">**Authorize** Slack to interact with your logic app:</span></span>      
   <span data-ttu-id="d0eab-127">![Configurar Slack][5]</span><span class="sxs-lookup"><span data-stu-id="d0eab-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="d0eab-128">Una vez completada la autorización se le redirigirá a la aplicación lógica para terminar mediante la configuración de la sección **Slack - obtener todos los mensajes** .</span><span class="sxs-lookup"><span data-stu-id="d0eab-128">After the authorization completes you'll be redirected to your logic app to complete it by configuring the **Slack - Get all messages** section.</span></span> <span data-ttu-id="d0eab-129">Agregue otros desencadenadores y acciones que necesite.</span><span class="sxs-lookup"><span data-stu-id="d0eab-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="d0eab-130">![Configurar Slack][6]</span><span class="sxs-lookup"><span data-stu-id="d0eab-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="d0eab-131">Guarde el trabajo seleccionando **Guardar** en la barra de menús superior.</span><span class="sxs-lookup"><span data-stu-id="d0eab-131">Save your work by selecting **Save** on the menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="d0eab-132">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="d0eab-132">Connector-specific details</span></span>

<span data-ttu-id="d0eab-133">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/slack/).</span><span class="sxs-lookup"><span data-stu-id="d0eab-133">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="d0eab-134">Más conectores</span><span class="sxs-lookup"><span data-stu-id="d0eab-134">More connectors</span></span>
<span data-ttu-id="d0eab-135">Volver a la [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="d0eab-135">Go back to the [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
