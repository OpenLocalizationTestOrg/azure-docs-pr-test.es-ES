---
title: "Incorporación del conector de Yammer a Azure Logic Apps | Microsoft Docs"
description: "Información general del conector de Yammer con parámetros de la API de REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5ae0827-fbb3-45ec-8f45-ad1cc2e7eccc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c7a213343b4fb2b5a89a5052a459061b404a431c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-yammer-connector"></a><span data-ttu-id="2151b-103">Introducción al conector de Yammer</span><span class="sxs-lookup"><span data-stu-id="2151b-103">Get started with the Yammer connector</span></span>
<span data-ttu-id="2151b-104">Conectarse a Yammer para acceder a conversaciones en la red empresarial.</span><span class="sxs-lookup"><span data-stu-id="2151b-104">Connect to Yammer to access conversations in your enterprise network.</span></span> <span data-ttu-id="2151b-105">Con Yammer, puede:</span><span class="sxs-lookup"><span data-stu-id="2151b-105">With Yammer, you can:</span></span>

* <span data-ttu-id="2151b-106">Compilar el flujo de negocio en función de los datos que obtiene de Yammer.</span><span class="sxs-lookup"><span data-stu-id="2151b-106">Build your business flow based on the data you get from Yammer.</span></span> 
* <span data-ttu-id="2151b-107">Usar desencadenadores cuando haya un nuevo mensaje en un grupo o en una fuente que le sigue.</span><span class="sxs-lookup"><span data-stu-id="2151b-107">Use triggers for when there is a new message in a group, or a feed your following.</span></span>
* <span data-ttu-id="2151b-108">Usar acciones para publicar un mensaje, obtener todos los mensajes y mucho más.</span><span class="sxs-lookup"><span data-stu-id="2151b-108">Use actions to post a message, get all messages, and more.</span></span> <span data-ttu-id="2151b-109">Estas acciones obtienen una respuesta y luego dejan el resultado a disposición de otras acciones.</span><span class="sxs-lookup"><span data-stu-id="2151b-109">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="2151b-110">Por ejemplo, cuando aparece un nuevo mensaje, puede enviar un correo electrónico mediante Office 365.</span><span class="sxs-lookup"><span data-stu-id="2151b-110">For example, when a new message appears, you can send an email using Office 365.</span></span>

<span data-ttu-id="2151b-111">Empiece por crear una aplicación lógica ahora. Para ello, consulte [Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="2151b-111">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-yammer"></a><span data-ttu-id="2151b-112">Creación de una conexión a Yammer</span><span class="sxs-lookup"><span data-stu-id="2151b-112">Create a connection to Yammer</span></span>
<span data-ttu-id="2151b-113">Para usar el conector de Yammer, cree primero una **conexión** y, después, especifique los detalles de las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="2151b-113">To use the Yammer connector, you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="2151b-114">Propiedad</span><span class="sxs-lookup"><span data-stu-id="2151b-114">Property</span></span> | <span data-ttu-id="2151b-115">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2151b-115">Required</span></span> | <span data-ttu-id="2151b-116">Descripción</span><span class="sxs-lookup"><span data-stu-id="2151b-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2151b-117">Se necesita el cifrado de tokens</span><span class="sxs-lookup"><span data-stu-id="2151b-117">Token</span></span> |<span data-ttu-id="2151b-118">Sí</span><span class="sxs-lookup"><span data-stu-id="2151b-118">Yes</span></span> |<span data-ttu-id="2151b-119">Proporcionar credenciales de Yammer</span><span class="sxs-lookup"><span data-stu-id="2151b-119">Provide Yammer Credentials</span></span> |

> [!INCLUDE [Steps to create a connection to Yammer](../../includes/connectors-create-api-yammer.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="2151b-120">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="2151b-120">Connector-specific details</span></span>

<span data-ttu-id="2151b-121">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/yammer/).</span><span class="sxs-lookup"><span data-stu-id="2151b-121">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/yammer/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="2151b-122">Más conectores</span><span class="sxs-lookup"><span data-stu-id="2151b-122">More connectors</span></span>
<span data-ttu-id="2151b-123">Volver a la [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="2151b-123">Go back to the [APIs list](apis-list.md).</span></span>