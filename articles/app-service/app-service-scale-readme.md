---
title: 'Servicio de aplicaciones de Azure: escalado de aplicaciones de Servicio de aplicaciones'
description: "Obtenga información acerca de hello pormenores de escalar la aplicación de servicio de aplicaciones."
keywords: servicio de aplicaciones, servicio de aplicaciones de azure, escala, escalable, plan del servicio de aplicaciones, costo del servicio de aplicaciones
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a>Servicio de aplicaciones de Azure: escalado de aplicaciones de Servicio de aplicaciones
Las aplicaciones hospedadas en el Servicio de aplicaciones de Azure pueden [alcanzar una escala enorme](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).
Sin embargo, el escalado de una aplicación es un problema complejo que no tiene una solución de "talla única". toocorrectly escalar la aplicación 3 áreas clave que contribuyen al éxito de las aplicaciones de tooyour:

1. Comprensión de la arquitectura de la aplicación y sus puntos débiles.
   * ¿Se trata de una aplicación con estado? ¿O sin estado?
   * ¿Cuáles son todos los componentes de hello de la aplicación?
     * ¿Dónde están los cuellos de botella de hello en la aplicación hello?
   * Cuando la carga es aplicación tooyour aplicado, ¿qué interrumpirá la primera?
2. Hola descripción espera que los requisitos de carga y rendimiento.
   * ¿Necesita aplicación hello tooserve mil usuarios? ¿o un millón?
   * ¿Procederá el tráfico de una sola ubicación geográfica o será global?
   * ¿Hay variaciones estacionales? ¿Picos de tráfico?
   * ¿Con qué rapidez debe responder aplicación hello? ¿Un segundo? ¿Un milisegundo?
3. Descripción correctamente Aproveche Hola plataforma y la aplicación de hospedaje.
   * ¿Qué características deben aprovechar tooachieve mis objetivos de escala?

Esta sección le ayudará a comprender todos los factores de Hola y ayuda idear una estrategia que aprovecha las ventajas de hello tooachieve de características de servicio de aplicaciones necesario los objetivos de escalabilidad.

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

