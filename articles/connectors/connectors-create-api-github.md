---
title: Conector de GitHub en Azure Logic Apps | Microsoft Docs
description: "Cree aplicaciones lógicas con el Servicio de aplicaciones de Azure. GitHub es un servicio de hospedaje del repositorio Git basado en la Web. Ofrece toda la funcionalidad de administración de código fuente (SCM) y control de revisiones distribuidas de Git, además de agregar sus propias características."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8f873e6c-f4c0-4c2e-a5bd-2e953efe5e2b
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: d4614b0ceff0ec0d36dbb1a136551f985f2fc1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-github-connector"></a><span data-ttu-id="a4839-105">Introducción al conector GitHub</span><span class="sxs-lookup"><span data-stu-id="a4839-105">Get started with the GitHub connector</span></span>
<span data-ttu-id="a4839-106">GitHub es un servicio de hospedaje del repositorio Git basado en la Web.</span><span class="sxs-lookup"><span data-stu-id="a4839-106">GitHub is a web-based Git repository hosting service.</span></span> <span data-ttu-id="a4839-107">Ofrece toda la funcionalidad de administración de código fuente (SCM) y control de revisiones distribuidas de Git, además de agregar sus propias características.</span><span class="sxs-lookup"><span data-stu-id="a4839-107">It offers all of the distributed revision control and source code management (SCM) functionality of Git as well as adding its own features.</span></span>

<span data-ttu-id="a4839-108">Puede empezar creando una aplicación lógica ahora. Para ello, consulte [Creación de una nueva aplicación lógica mediante la conexión de servicios de SaaS](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a4839-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-github"></a><span data-ttu-id="a4839-109">Creación de una conexión a GitHub</span><span class="sxs-lookup"><span data-stu-id="a4839-109">Create a connection to GitHub</span></span>
<span data-ttu-id="a4839-110">Para crear Logic Apps con GitHub, primero necesita crear una **conexión** y, después, especificar los detalles de las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="a4839-110">To create Logic apps with GitHub, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="a4839-111">Propiedad</span><span class="sxs-lookup"><span data-stu-id="a4839-111">Property</span></span> | <span data-ttu-id="a4839-112">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="a4839-112">Required</span></span> | <span data-ttu-id="a4839-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="a4839-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a4839-114">Se necesita el cifrado de tokens</span><span class="sxs-lookup"><span data-stu-id="a4839-114">Token</span></span> |<span data-ttu-id="a4839-115">Sí</span><span class="sxs-lookup"><span data-stu-id="a4839-115">Yes</span></span> |<span data-ttu-id="a4839-116">Proporcionar las credenciales de GitHub</span><span class="sxs-lookup"><span data-stu-id="a4839-116">Provide GitHub Credentials</span></span> |

<span data-ttu-id="a4839-117">Después de crear la conexión, puede usarla para ejecutar las acciones y escuchar los desencadenadores descritos en este artículo.</span><span class="sxs-lookup"><span data-stu-id="a4839-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span> 

> [!INCLUDE [Steps to create a connection to GitHub](../../includes/connectors-create-api-github.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="a4839-118">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="a4839-118">Connector-specific details</span></span>

<span data-ttu-id="a4839-119">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/github/).</span><span class="sxs-lookup"><span data-stu-id="a4839-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/github/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="a4839-120">Más conectores</span><span class="sxs-lookup"><span data-stu-id="a4839-120">More connectors</span></span>
<span data-ttu-id="a4839-121">Volver a la [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="a4839-121">Go back to the [APIs list](apis-list.md).</span></span>