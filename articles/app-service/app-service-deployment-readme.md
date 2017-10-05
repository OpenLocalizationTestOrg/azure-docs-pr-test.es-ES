---
title: "Implementación de aplicaciones en Servicio de aplicaciones de Azure"
description: "Obtenga información acerca de cómo implementar aplicaciones en el trabajo de Servicio de aplicaciones"
keywords: "servicio de aplicaciones, servicio de aplicaciones de azure, implementar, implementación"
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: 
ms.assetid: de12cd6e-e124-4e48-90bc-c3a3801305da
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 347e8b5177eac8e08ab0dea701b736b86d23904a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-deployment-overview"></a><span data-ttu-id="b72dc-104">Descripción general de la implementación de Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="b72dc-104">Azure App Service Deployment Overview</span></span>
<span data-ttu-id="b72dc-105">Servicio de aplicaciones de Azure proporciona un conjunto de características enriquecido e integrado para permitir la creación de flujos de trabajo de implementación eficaces y flexibles.</span><span class="sxs-lookup"><span data-stu-id="b72dc-105">Azure App Service provides a rich and integrated feature set to support creating powerful and flexible deployment workflows.</span></span> <span data-ttu-id="b72dc-106">La implementación de aplicaciones puede aprovechar opciones como la integración continua, la publicación de control de código fuente local, WebDeploy y FTP.</span><span class="sxs-lookup"><span data-stu-id="b72dc-106">App deployment can leverage options that include continuous integration or local source control publishing, WebDeploy, and FTP.</span></span> <span data-ttu-id="b72dc-107">El método recomendado para la implementación de aplicaciones de producción es el intercambio de ranuras de implementación.</span><span class="sxs-lookup"><span data-stu-id="b72dc-107">The recommended method for production app deployment is deployment slot swap.</span></span> <span data-ttu-id="b72dc-108">Las ranuras de implementación representan entornos de ensayo e integración asociados con aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="b72dc-108">Deployment slots represent staging and integration environments associated with production apps.</span></span> <span data-ttu-id="b72dc-109">Las ranuras de implementación pueden configurarse y dirigirse con tráfico web para su validación, y el tráfico se puede intercambiar bajo demanda para su implementación en producción sin tiempo de inactividad o de preparación automatizada.</span><span class="sxs-lookup"><span data-stu-id="b72dc-109">Deployment slots can be configured and targeted with web traffic for validation, and traffic can be swapped on demand for deployment to production with no down time and automated warm-up.</span></span> <span data-ttu-id="b72dc-110">Los pasos de un flujo de trabajo de implementación se pueden automatizar fácilmente mediante productos de administración de versiones como Release Management para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b72dc-110">The steps of a deployment workflow can be easily automated via release management products such as Visual Studio Release Management.</span></span> <span data-ttu-id="b72dc-111">Esto es útil para la coordinación con otros recursos de la solución (por ejemplo, almacén de datos), periodicidad y replicación en varias unidades de implementación.</span><span class="sxs-lookup"><span data-stu-id="b72dc-111">This is useful for coordination with other solution resources (e.g. data store), recurrence, and replication across multiple units of deployment.</span></span> 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

