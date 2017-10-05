---
title: "Incorporación del conector de Twilio a Azure Logic Apps | Microsoft Docs"
description: "Información general del conector de Twilio con parámetros de la API de REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 43116187-4a2f-42e5-9852-a0d62f08c5fc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a790ac51b0fea7e3fa379d20e0e094e7ce0d7696
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-twilio-connector"></a><span data-ttu-id="b4bfa-103">Introducción al conector de Twilio</span><span class="sxs-lookup"><span data-stu-id="b4bfa-103">Get started with the Twilio connector</span></span>
<span data-ttu-id="b4bfa-104">Conectarse a Twilio para enviar y recibir mensajes SMS, MMS y IP globales.</span><span class="sxs-lookup"><span data-stu-id="b4bfa-104">Connect to Twilio to send and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="b4bfa-105">Con Twilio, puede:</span><span class="sxs-lookup"><span data-stu-id="b4bfa-105">With Twilio, you can:</span></span>

* <span data-ttu-id="b4bfa-106">Compilar el flujo de negocio en función de los datos que obtiene de Twilio.</span><span class="sxs-lookup"><span data-stu-id="b4bfa-106">Build your business flow based on the data you get from Twilio.</span></span> 
* <span data-ttu-id="b4bfa-107">Usar acciones que obtienen un mensaje, enumeran mensajes y mucho más.</span><span class="sxs-lookup"><span data-stu-id="b4bfa-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="b4bfa-108">Estas acciones obtienen una respuesta y luego dejan el resultado a disposición de otras acciones.</span><span class="sxs-lookup"><span data-stu-id="b4bfa-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="b4bfa-109">Por ejemplo, cuando reciba un nuevo mensaje de Twilio, puede usarlo en un flujo de trabajo de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b4bfa-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="b4bfa-110">Para empezar, cree una aplicación lógica; consulte [Creación de su primer flujo de trabajo de aplicación lógica para automatizar los procesos entre aplicaciones de nube y servicios en la nube](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b4bfa-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-twilio"></a><span data-ttu-id="b4bfa-111">Creación de una conexión a Twilio</span><span class="sxs-lookup"><span data-stu-id="b4bfa-111">Create a connection to Twilio</span></span>
<span data-ttu-id="b4bfa-112">Cuando agregue este conector a las aplicaciones lógicas, escriba los siguientes valores de Twilio:</span><span class="sxs-lookup"><span data-stu-id="b4bfa-112">When you add this Connector to your logic apps, enter the following Twilio values:</span></span>

| <span data-ttu-id="b4bfa-113">Propiedad</span><span class="sxs-lookup"><span data-stu-id="b4bfa-113">Property</span></span> | <span data-ttu-id="b4bfa-114">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b4bfa-114">Required</span></span> | <span data-ttu-id="b4bfa-115">Description</span><span class="sxs-lookup"><span data-stu-id="b4bfa-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4bfa-116">Id. de cuenta</span><span class="sxs-lookup"><span data-stu-id="b4bfa-116">Account ID</span></span> |<span data-ttu-id="b4bfa-117">Sí</span><span class="sxs-lookup"><span data-stu-id="b4bfa-117">Yes</span></span> |<span data-ttu-id="b4bfa-118">Escriba el identificador de cuenta de Twilio</span><span class="sxs-lookup"><span data-stu-id="b4bfa-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="b4bfa-119">Token de acceso</span><span class="sxs-lookup"><span data-stu-id="b4bfa-119">Access Token</span></span> |<span data-ttu-id="b4bfa-120">Sí</span><span class="sxs-lookup"><span data-stu-id="b4bfa-120">Yes</span></span> |<span data-ttu-id="b4bfa-121">Escriba el token de acceso de Twilio</span><span class="sxs-lookup"><span data-stu-id="b4bfa-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps to create a connection to Twilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="b4bfa-122">Si no tiene un token de acceso de Twilio, consulte [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity) (Tokens de identidad de usuario y de acceso).</span><span class="sxs-lookup"><span data-stu-id="b4bfa-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="b4bfa-123">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="b4bfa-123">Connector-specific details</span></span>

<span data-ttu-id="b4bfa-124">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/twilio/).</span><span class="sxs-lookup"><span data-stu-id="b4bfa-124">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="b4bfa-125">Más conectores</span><span class="sxs-lookup"><span data-stu-id="b4bfa-125">More connectors</span></span>
<span data-ttu-id="b4bfa-126">Volver a la [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="b4bfa-126">Go back to the [APIs list](apis-list.md).</span></span>