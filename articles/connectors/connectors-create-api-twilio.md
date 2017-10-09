---
title: "aaaAdd Hola conector Twilio en las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Información general de hello Twilio conector con parámetros de la API de REST"
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
ms.openlocfilehash: b2b487f34bc76bee24b4237a71ee767d0d22ff7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twilio-connector"></a><span data-ttu-id="5341a-103">Empezar a trabajar con el conector de Twilio Hola</span><span class="sxs-lookup"><span data-stu-id="5341a-103">Get started with hello Twilio connector</span></span>
<span data-ttu-id="5341a-104">Conecte tooTwilio toosend y recibir mensajes SMS y MMS, IP globales.</span><span class="sxs-lookup"><span data-stu-id="5341a-104">Connect tooTwilio toosend and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="5341a-105">Con Twilio, puede:</span><span class="sxs-lookup"><span data-stu-id="5341a-105">With Twilio, you can:</span></span>

* <span data-ttu-id="5341a-106">Genera el flujo de negocios basado en datos de hello que obtendrá de Twilio.</span><span class="sxs-lookup"><span data-stu-id="5341a-106">Build your business flow based on hello data you get from Twilio.</span></span> 
* <span data-ttu-id="5341a-107">Usar acciones que obtienen un mensaje, enumeran mensajes y mucho más.</span><span class="sxs-lookup"><span data-stu-id="5341a-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="5341a-108">Estas acciones obtención una respuesta y, a continuación, asegúrese de salida de hello disponibles para las demás acciones.</span><span class="sxs-lookup"><span data-stu-id="5341a-108">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="5341a-109">Por ejemplo, cuando reciba un nuevo mensaje de Twilio, puede usarlo en un flujo de trabajo de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="5341a-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="5341a-110">Para empezar, cree una aplicación lógica; consulte [Creación de su primer flujo de trabajo de aplicación lógica para automatizar los procesos entre aplicaciones de nube y servicios en la nube](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5341a-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tootwilio"></a><span data-ttu-id="5341a-111">Crear una conexión tooTwilio</span><span class="sxs-lookup"><span data-stu-id="5341a-111">Create a connection tooTwilio</span></span>
<span data-ttu-id="5341a-112">Cuando se agregan este conector tooyour las aplicaciones lógicas, escriba Hola después Twilio valores:</span><span class="sxs-lookup"><span data-stu-id="5341a-112">When you add this Connector tooyour logic apps, enter hello following Twilio values:</span></span>

| <span data-ttu-id="5341a-113">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5341a-113">Property</span></span> | <span data-ttu-id="5341a-114">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="5341a-114">Required</span></span> | <span data-ttu-id="5341a-115">Description</span><span class="sxs-lookup"><span data-stu-id="5341a-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5341a-116">Id. de cuenta</span><span class="sxs-lookup"><span data-stu-id="5341a-116">Account ID</span></span> |<span data-ttu-id="5341a-117">Sí</span><span class="sxs-lookup"><span data-stu-id="5341a-117">Yes</span></span> |<span data-ttu-id="5341a-118">Escriba el identificador de cuenta de Twilio</span><span class="sxs-lookup"><span data-stu-id="5341a-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="5341a-119">Token de acceso</span><span class="sxs-lookup"><span data-stu-id="5341a-119">Access Token</span></span> |<span data-ttu-id="5341a-120">Sí</span><span class="sxs-lookup"><span data-stu-id="5341a-120">Yes</span></span> |<span data-ttu-id="5341a-121">Escriba el token de acceso de Twilio</span><span class="sxs-lookup"><span data-stu-id="5341a-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps toocreate a connection tooTwilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="5341a-122">Si no tiene un token de acceso de Twilio, consulte [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity) (Tokens de identidad de usuario y de acceso).</span><span class="sxs-lookup"><span data-stu-id="5341a-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="5341a-123">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="5341a-123">Connector-specific details</span></span>

<span data-ttu-id="5341a-124">Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/twilio/).</span><span class="sxs-lookup"><span data-stu-id="5341a-124">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="5341a-125">Más conectores</span><span class="sxs-lookup"><span data-stu-id="5341a-125">More connectors</span></span>
<span data-ttu-id="5341a-126">Volver atrás toohello [lista de las API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="5341a-126">Go back toohello [APIs list](apis-list.md).</span></span>
