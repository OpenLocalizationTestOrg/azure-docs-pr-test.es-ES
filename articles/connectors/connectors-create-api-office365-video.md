---
title: Uso del conector de Office 365 Video en Logic Apps | Microsoft Docs
description: "Introducción al uso del conector de Office 365 Video en las aplicaciones lógicas del Servicio de aplicaciones de Microsoft Azure"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 738e5aa7-2523-4116-8b65-211b9063852d
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: f0e3613d4a3fd5478787c0365eb7a0bcde886c81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office365-video-connector"></a><span data-ttu-id="f372c-103">Introducción al conector de Office 365 Video</span><span class="sxs-lookup"><span data-stu-id="f372c-103">Get started with the Office365 Video connector</span></span>
<span data-ttu-id="f372c-104">Conéctese a Office 365 Video para conseguir información acerca de un vídeo Office 365 específico, obtener una lista de vídeos y mucho más.</span><span class="sxs-lookup"><span data-stu-id="f372c-104">Connect to Office 365 Video to get information about an Office 365 video, get a list of videos, and more.</span></span> <span data-ttu-id="f372c-105">Con Office 365 Video puede:</span><span class="sxs-lookup"><span data-stu-id="f372c-105">With Office 365 Video, you can:</span></span>

* <span data-ttu-id="f372c-106">Compilar el flujo de su negocio en función de los datos que obtiene de Office 365 Video.</span><span class="sxs-lookup"><span data-stu-id="f372c-106">Build your business flow based on the data you get from Office 365 Video.</span></span> 
* <span data-ttu-id="f372c-107">Usar acciones que comprueban el estado del portal de vídeo, obtener una lista de todos los vídeos en un canal y mucho más.</span><span class="sxs-lookup"><span data-stu-id="f372c-107">Use actions that check the video portal status, get a list of all video in a channel, and more.</span></span> <span data-ttu-id="f372c-108">Estas acciones obtienen una respuesta y luego dejan el resultado a disposición de otras acciones.</span><span class="sxs-lookup"><span data-stu-id="f372c-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="f372c-109">Por ejemplo, puede utilizar el conector de Búsqueda de Bing para buscar vídeos de Office 365 y, después, usar el conector de Office 365 Video para conseguir información sobre ese vídeo.</span><span class="sxs-lookup"><span data-stu-id="f372c-109">For example, you can use the Bing Search connector to search for Office 365 videos, and then use the Office 365 video connector to get information about that video.</span></span> <span data-ttu-id="f372c-110">Si el vídeo cumple sus requisitos, puede publicarlo en Facebook.</span><span class="sxs-lookup"><span data-stu-id="f372c-110">If the video meets your requirements, you can post this video on Facebook.</span></span> 

<span data-ttu-id="f372c-111">Puede empezar creando una aplicación lógica ahora. Para ello, consulte [Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f372c-111">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-office365-video-connector"></a><span data-ttu-id="f372c-112">Creación de una conexión al conector de Office 365 Video</span><span class="sxs-lookup"><span data-stu-id="f372c-112">Create a connection to Office365 Video connector</span></span>
<span data-ttu-id="f372c-113">Al agregar este conector a las aplicaciones lógicas, debe iniciar sesión en su cuenta de Office 365 Video y permitir que estas se conecten a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="f372c-113">When you add this connector to your logic apps, you must sign-in to your Office 365 Video account and allow logic apps to connect to your account.</span></span>

> [!INCLUDE [Steps to create a connection to Office 365 Video](../../includes/connectors-create-api-office365video.md)]
> 
> 

<span data-ttu-id="f372c-114">Después de crear la conexión, especifique las propiedades del vídeo de Office 365, como el nombre de inquilino o el identificador del canal.</span><span class="sxs-lookup"><span data-stu-id="f372c-114">After you create the connection, you enter the Office 365 video properties, like the tenant name or channel ID.</span></span> 


## <a name="connector-specific-details"></a><span data-ttu-id="f372c-115">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="f372c-115">Connector-specific details</span></span>

<span data-ttu-id="f372c-116">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/office365videoconnector/).</span><span class="sxs-lookup"><span data-stu-id="f372c-116">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/office365videoconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="f372c-117">Más conectores</span><span class="sxs-lookup"><span data-stu-id="f372c-117">More connectors</span></span>
<span data-ttu-id="f372c-118">Volver a la [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="f372c-118">Go back to the [APIs list](apis-list.md).</span></span>