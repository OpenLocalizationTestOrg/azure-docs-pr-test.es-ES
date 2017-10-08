---
title: aaaDeploying aplicaciones tooAzure servicio de aplicaciones
description: "Obtenga información acerca de cómo funcionan las aplicaciones de tooDeploy tooApp servicio"
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
ms.openlocfilehash: 925341e12daf3cb05b25199f5c5218e82f062f70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-deployment-overview"></a><span data-ttu-id="91488-104">Descripción general de la implementación de Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="91488-104">Azure App Service Deployment Overview</span></span>
<span data-ttu-id="91488-105">Servicio de aplicaciones de Azure ofrece a un variado y características integradas establecer toosupport crear flujos de trabajo de implementación eficaz y flexible.</span><span class="sxs-lookup"><span data-stu-id="91488-105">Azure App Service provides a rich and integrated feature set toosupport creating powerful and flexible deployment workflows.</span></span> <span data-ttu-id="91488-106">La implementación de aplicaciones puede aprovechar opciones como la integración continua, la publicación de control de código fuente local, WebDeploy y FTP.</span><span class="sxs-lookup"><span data-stu-id="91488-106">App deployment can leverage options that include continuous integration or local source control publishing, WebDeploy, and FTP.</span></span> <span data-ttu-id="91488-107">Hola recomienda el método de implementación de aplicación de producción es intercambio de ranura de implementación.</span><span class="sxs-lookup"><span data-stu-id="91488-107">hello recommended method for production app deployment is deployment slot swap.</span></span> <span data-ttu-id="91488-108">Las ranuras de implementación representan entornos de ensayo e integración asociados con aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="91488-108">Deployment slots represent staging and integration environments associated with production apps.</span></span> <span data-ttu-id="91488-109">Las ranuras de implementación se pueden configurar y de destino con el tráfico de web para la validación y el tráfico se puede intercambiar a petición para tooproduction de implementación con ningún tiempo de inactividad y automatizar la preparación.</span><span class="sxs-lookup"><span data-stu-id="91488-109">Deployment slots can be configured and targeted with web traffic for validation, and traffic can be swapped on demand for deployment tooproduction with no down time and automated warm-up.</span></span> <span data-ttu-id="91488-110">pasos de Hola de un flujo de trabajo de implementación se pueden automatizar fácilmente a través de productos de administración de versión como administración de la versión de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="91488-110">hello steps of a deployment workflow can be easily automated via release management products such as Visual Studio Release Management.</span></span> <span data-ttu-id="91488-111">Esto es útil para la coordinación con otros recursos de la solución (por ejemplo, almacén de datos), periodicidad y replicación en varias unidades de implementación.</span><span class="sxs-lookup"><span data-stu-id="91488-111">This is useful for coordination with other solution resources (e.g. data store), recurrence, and replication across multiple units of deployment.</span></span> 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

