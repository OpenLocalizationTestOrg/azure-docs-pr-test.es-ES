---
title: "Trasladar recursos de la aplicación web a otro grupo de recursos"
description: Se describen los escenarios donde puede trasladar aplicaciones web y servicios de aplicaciones de un grupo de recursos a otro.
services: app-service
documentationcenter: 
author: ZainRizvi
manager: erikre
editor: 
ms.assetid: 22f97607-072e-4d1f-a46f-8d500420c33c
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: zarizvi
ms.openlocfilehash: 1b5059dc052005b6079f70ecf6771a3771df8d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="supported-move-configurations"></a><span data-ttu-id="c8676-103">Configuraciones admitidas para traslados</span><span class="sxs-lookup"><span data-stu-id="c8676-103">Supported Move Configurations</span></span>
<span data-ttu-id="c8676-104">Puede trasladar recursos de aplicaciones web de Azure con la [API Trasladar recursos de Resource Manager](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="c8676-104">You can move Azure Web App resources using the [Resource Manager Move Resources API](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="c8676-105">Las aplicaciones web de Azure admiten actualmente los siguientes escenarios de traslado:</span><span class="sxs-lookup"><span data-stu-id="c8676-105">Azure Web Apps currently supports the following move scenarios:</span></span>

* <span data-ttu-id="c8676-106">Mover todo el contenido de un grupo de recursos (aplicaciones web, planes de App Service y certificados) a otro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c8676-106">Move the entire contents of a resource group (web apps, app service plans, and certificates) to another resource group.</span></span> 
   > [!Note]
   > <span data-ttu-id="c8676-107">Nota: El grupo de recursos de destino no puede contener ningún recurso Microsoft.Web en este escenario.</span><span class="sxs-lookup"><span data-stu-id="c8676-107">The destination resource group can not contain any Microsoft.Web resources in this scenario.</span></span>

* <span data-ttu-id="c8676-108">Trasladar aplicaciones web individuales a un grupo de recursos diferente, manteniéndolas hospedadas en el plan de App Service en que se encuentran actualmente (el plan de App Service se encuentra en el grupo de recursos anterior).</span><span class="sxs-lookup"><span data-stu-id="c8676-108">Move individual web apps to a different resource group, while still hosting them in their current app service plan (the app service plan stays in the old resource group).</span></span>


