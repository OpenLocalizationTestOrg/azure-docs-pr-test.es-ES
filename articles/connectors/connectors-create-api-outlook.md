---
title: Conector de Outlook.com en Azure Logic Apps | Microsoft Docs
description: "Cree aplicaciones lógicas con el Servicio de aplicaciones de Azure. El conector de Outlook.com permite administrar su correo, calendarios y contactos. Puede realizar diversas acciones como enviar correo, programar reuniones, agregar contactos, etc."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 87113c85-d158-4dd5-9ed5-5748130003d6
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: bde1629504c97cf6706b42219570ffa6243073dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-outlookcom-connector"></a><span data-ttu-id="e5f07-105">Get started with the Outlook.com connector (Introducción al conector de Outlook.com)</span><span class="sxs-lookup"><span data-stu-id="e5f07-105">Get started with the Outlook.com connector</span></span>
<span data-ttu-id="e5f07-106">El conector de Outlook.com permite administrar su correo, calendarios y contactos.</span><span class="sxs-lookup"><span data-stu-id="e5f07-106">Outlook.com connector allows you to manage your mail, calendars, and contacts.</span></span> <span data-ttu-id="e5f07-107">Puede realizar diversas acciones como enviar correo, programar reuniones, agregar contactos, etc.</span><span class="sxs-lookup"><span data-stu-id="e5f07-107">You can perform various actions such as send mail, schedule meetings, add contacts, etc.</span></span>

<span data-ttu-id="e5f07-108">Puede empezar creando una aplicación lógica ahora. Para ello, consulte [Creación de una nueva aplicación lógica mediante la conexión de servicios de SaaS](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e5f07-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-outlookcom"></a><span data-ttu-id="e5f07-109">Creación de una conexión a Outlook.com</span><span class="sxs-lookup"><span data-stu-id="e5f07-109">Create a connection to Outlook.com</span></span>
<span data-ttu-id="e5f07-110">Para crear aplicaciones lógicas con Outlook.com, primero debe crear una **conexión** y, después, especificar los detalles de las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="e5f07-110">To create Logic apps with Outlook.com, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="e5f07-111">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e5f07-111">Property</span></span> | <span data-ttu-id="e5f07-112">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="e5f07-112">Required</span></span> | <span data-ttu-id="e5f07-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="e5f07-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e5f07-114">Se necesita el cifrado de tokens</span><span class="sxs-lookup"><span data-stu-id="e5f07-114">Token</span></span> |<span data-ttu-id="e5f07-115">Sí</span><span class="sxs-lookup"><span data-stu-id="e5f07-115">Yes</span></span> |<span data-ttu-id="e5f07-116">Proporcionar las credenciales de Outlook.com</span><span class="sxs-lookup"><span data-stu-id="e5f07-116">Provide Outlook.com Credentials</span></span> |

<span data-ttu-id="e5f07-117">Después de crear la conexión, puede usarla para ejecutar las acciones y escuchar los desencadenadores descritos en este artículo.</span><span class="sxs-lookup"><span data-stu-id="e5f07-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span>

> [!INCLUDE [Steps to create a connection to Outlook.com](../../includes/connectors-create-api-outlook.md)]
>

## <a name="connector-specific-details"></a><span data-ttu-id="e5f07-118">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="e5f07-118">Connector-specific details</span></span>

<span data-ttu-id="e5f07-119">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/outlook/).</span><span class="sxs-lookup"><span data-stu-id="e5f07-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/outlook/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="e5f07-120">Más conectores</span><span class="sxs-lookup"><span data-stu-id="e5f07-120">More connectors</span></span>
<span data-ttu-id="e5f07-121">Volver a la [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e5f07-121">Go back to the [APIs list](apis-list.md).</span></span>