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
# <a name="azure-app-service-deployment-overview"></a>Descripción general de la implementación de Servicio de aplicaciones de Azure
Servicio de aplicaciones de Azure proporciona un conjunto de características enriquecido e integrado para permitir la creación de flujos de trabajo de implementación eficaces y flexibles. La implementación de aplicaciones puede aprovechar opciones como la integración continua, la publicación de control de código fuente local, WebDeploy y FTP. El método recomendado para la implementación de aplicaciones de producción es el intercambio de ranuras de implementación. Las ranuras de implementación representan entornos de ensayo e integración asociados con aplicaciones de producción. Las ranuras de implementación pueden configurarse y dirigirse con tráfico web para su validación, y el tráfico se puede intercambiar bajo demanda para su implementación en producción sin tiempo de inactividad o de preparación automatizada. Los pasos de un flujo de trabajo de implementación se pueden automatizar fácilmente mediante productos de administración de versiones como Release Management para Visual Studio. Esto es útil para la coordinación con otros recursos de la solución (por ejemplo, almacén de datos), periodicidad y replicación en varias unidades de implementación. 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

