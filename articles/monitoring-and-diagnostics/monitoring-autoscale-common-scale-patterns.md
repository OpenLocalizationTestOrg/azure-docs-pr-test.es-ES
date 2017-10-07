---
title: "aaaOverview de patrones comunes de escalado automático | Documentos de Microsoft"
description: "Obtenga información acerca de que algunas tooauto patrones comunes de hello escalan el recurso de Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a>Información general sobre los patrones comunes de escalado automático
Este artículo describen algunos tooscale patrones comunes de hello el recurso de Azure.

Azure Autoescala de Monitor aplica solo tooVirtual conjuntos de escala de máquina (VMSS), servicios en la nube, planes de servicio de aplicaciones y entornos del servicio de aplicación. 

# <a name="lets-get-started"></a>Introducción

En este artículo se asume que está familiarizado con el escalado automático. También puede [obtener iniciada tooscale aquí el recurso][1]. siguiente Hola es algunos de los patrones comunes de escala de Hola.

## <a name="scale-based-on-cpu"></a>Escala en función de la CPU

Tiene una aplicación web (rol de VMSS o de servicio en la nube) y: 

- Desea tooscale fuera y de CPU en función de la escala.
- Además, desea tooensure hay un número mínimo de instancias. 
- Además, le interesará tooensure que establece un número de toohello de límite máximo de instancias que se pueda adaptar a.

![Escala en función de la CPU][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a>Escalado distinto entre los días de la semana y los fines de semana

Tiene una aplicación web (rol de VMSS o de servicio en la nube) y:

- Desea 3 instancias de forma predeterminada (en días de la semana).
- No esperar un tráfico de los fines de semana y, por tanto, desea tooscale too1 instancia los fines de semana.

![Escalado distinto entre los días de la semana y los fines de semana][3]

## <a name="scale-differently-during-holidays"></a>Escalado distinto durante festividades

Tiene una aplicación web (rol de VMSS o de servicio en la nube) y: 

- Desea tooscale arriba/abajo según el uso de CPU de forma predeterminada
- Sin embargo, durante la temporada de vacaciones (o los días específicos que son importantes para su empresa) desea que los valores predeterminados de toooverride hello y tiene más capacidad a su disposición.

![Escalado distinto durante festividades][4]

## <a name="scale-based-on-custom-metric"></a>Escalado en función de métricas personalizadas

Tiene un front-end web y un nivel de API que se comunica con hello back-end. 

- Desea capa de hello API tooscale basado en eventos personalizados de front-end de hello (ejemplo: desea tooscale el proceso de pago según el número de Hola de elementos de hello carro de la compra)

![Escalado en función de métricas personalizadas][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png