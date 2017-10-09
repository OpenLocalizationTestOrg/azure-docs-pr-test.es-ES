---
title: "aaaAn aplicación de Proxy de aplicación tarda demasiado tooload | Documentos de Microsoft"
description: "Solucionar problemas de rendimiento de carga de página con hello Proxy de aplicación de Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c7a51f96840966a1d88933fa4e30f39479d8a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="an-application-proxy-application-takes-too-long-tooload"></a>Una aplicación de Proxy de aplicación tarda demasiado tooload

En este artículo le ayudarán a toounderstand ¿por qué una aplicación de Proxy de aplicación de Azure AD puede tardar un tooload mucho tiempo y qué puede hacer tooresolve este problema.

## <a name="overview"></a>Información general
Si están trabajando sus aplicaciones y ver una latencia elevada, puede haber algunos ajustes menores en la topología de red que puede considerar la velocidad de hello tooimprove. Para obtener una evaluación de diferentes topologías, vea hello [documento de consideraciones de red](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).

Si estas consideraciones no le sirven de ayuda, desgraciadamente ahora no disponemos de otras recomendaciones de optimización del rendimiento. Como Hola servicio Proxy de aplicación expande toomore centros de datos que pueden ser tooyou más cercano, latencia de toosee mejorado, puede iniciar directamente. centros de la lista completa de hello toosee de datos de Azure, puede ver hello [página de prueba de latencia](http://www.azurespeed.com/Azure/Latency). 

Hello centros de datos con el servicio de Proxy de aplicación Hola pueden encontrarse con hello [herramienta de prueba de puertos de conector](https://aadap-portcheck.connectorporttest.msappproxy.net/). 

## <a name="feedback-on-application-proxy-data-center-locations"></a>Comentarios sobre las ubicaciones de los centros de datos de Proxy de aplicación 
Puede haber centros de datos de Azure que todavía no incluyen el Proxy de aplicación pero conducirían mejora de gran latencia tooa para usted. ubicación en el centro de datos de Hello < aadapfeedback@microsoft.com > por lo que podemos usar su tooplan comentarios tal y como se expanda.

Estamos trabajando en algunas capacidades adicionales que le ayudan a mejorar la latencia de Hola para los inquilinos que ven actualmente largas latencias y estar seguro de documentación de tooshare una vez disponibles.

## <a name="next-steps"></a>Pasos siguientes
[Trabajo con servidores proxy locales existentes](application-proxy-working-with-proxy-servers.md)
