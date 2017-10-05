---
title: "Incorporación del conector de usuarios de Office 365 a sus Logic Apps | Microsoft Docs"
description: "Información general del conector de Usuarios de Office 365 con parámetros de la API de REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2146481-9105-4f56-b4c2-7ae340cb922f
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 330f733440932a769eb0fe6031cd0d947a820080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office-365-users-connector"></a><span data-ttu-id="1233e-103">Introducción al conector de Usuarios de Office 365</span><span class="sxs-lookup"><span data-stu-id="1233e-103">Get started with the Office 365 Users connector</span></span>
<span data-ttu-id="1233e-104">Conéctese a Usuarios de Office 365 para obtener perfiles, buscar usuarios, etc.</span><span class="sxs-lookup"><span data-stu-id="1233e-104">Connect to Office 365 Users to get profiles, search users, and more.</span></span> <span data-ttu-id="1233e-105">Con Usuarios de Office 365, puede:</span><span class="sxs-lookup"><span data-stu-id="1233e-105">With Office 365 Users, you can:</span></span>

* <span data-ttu-id="1233e-106">Compilar el flujo de su negocio en función de los datos que obtiene de Usuarios de Office 365.</span><span class="sxs-lookup"><span data-stu-id="1233e-106">Build your business flow based on the data you get from Office 365 Users.</span></span> 
* <span data-ttu-id="1233e-107">Usar acciones que obtienen informes directos, obtienen el perfil de usuario de un administrador, etc.</span><span class="sxs-lookup"><span data-stu-id="1233e-107">Use actions that get direct reports, get a manager's user profile, and more.</span></span> <span data-ttu-id="1233e-108">Estas acciones obtienen una respuesta y luego dejan el resultado a disposición de otras acciones.</span><span class="sxs-lookup"><span data-stu-id="1233e-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="1233e-109">Por ejemplo, obtenga informes directos de la persona y, luego, tome esta información y actualice una base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1233e-109">For example, get a person's direct reports, and then take this information and update a SQL Azure database.</span></span> 

<span data-ttu-id="1233e-110">Puede empezar creando una aplicación lógica ahora. Para ello, consulte [Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1233e-110">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-office-365-users"></a><span data-ttu-id="1233e-111">Creación de una conexión a Usuarios de Office 365</span><span class="sxs-lookup"><span data-stu-id="1233e-111">Create a connection to Office 365 Users</span></span>
<span data-ttu-id="1233e-112">Al agregar este conector a las aplicaciones lógicas, debe iniciar sesión en su cuenta de Usuarios de Office 365 y permitir que estas se conecten a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="1233e-112">When you add this connector to your logic apps, you must sign-in to your Office 365 Users account and allow logic apps to connect to your account.</span></span>

> [!INCLUDE [Steps to create a connection to Office 365 Users](../../includes/connectors-create-api-office365users.md)]
> 
> 

<span data-ttu-id="1233e-113">Después de crear la conexión, especifique las propiedades de Usuarios de Office 365, como el identificador de usuario.</span><span class="sxs-lookup"><span data-stu-id="1233e-113">After you create the connection, you enter the Office 365 Users properties, like the user ID.</span></span> <span data-ttu-id="1233e-114">En la **referencia de la API de REST** de este tema se describen estas propiedades.</span><span class="sxs-lookup"><span data-stu-id="1233e-114">The **REST API reference** in this topic describes these properties.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="1233e-115">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="1233e-115">Connector-specific details</span></span>

<span data-ttu-id="1233e-116">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/officeusers/).</span><span class="sxs-lookup"><span data-stu-id="1233e-116">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/officeusers/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="1233e-117">Más conectores</span><span class="sxs-lookup"><span data-stu-id="1233e-117">More connectors</span></span>
<span data-ttu-id="1233e-118">Volver a la [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="1233e-118">Go back to the [APIs list](apis-list.md).</span></span>