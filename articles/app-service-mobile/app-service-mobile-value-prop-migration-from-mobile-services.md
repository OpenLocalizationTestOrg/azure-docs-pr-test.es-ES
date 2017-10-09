---
title: "aaaI usar servicios móviles, ¿cómo ayuda servicio de aplicaciones?"
description: "Obtenga información acerca de qué ventajas de servicio de aplicaciones aporta tooyour proyectos de servicios móviles existentes."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 26b68a11-8352-4f78-acd2-e4e0ec177781
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 315cc6eedcdca6c3f9f9bb9fd5ec7baf655b7e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started"></a>Uso de Servicios móviles: ¿cómo ayuda el Servicio de aplicaciones?
## <a name="overview"></a>Información general
Servicios móviles existentes es seguro y seguirá siendo compatible. Sin embargo hay números de hello ventajas *servicio de aplicaciones de Azure* plataforma proporciona para su aplicación móvil que no están disponibles hoy en día con servicios móviles:

* Oferta más simple, más fácil y más rentable para las aplicaciones que incluyen clientes móviles y web
* Nuevas características de host como trabajos web, CNAME personalizado y una mejor supervisión
* Integración inmediata con Administrador de tráfico
* Recursos de conectividad tooyour locales y redes privadas virtuales mediante red virtual en suma tooHybrid conexiones
* Supervisión, alertas y solución de problemas para su aplicación mediante NewRelic o AppInsights
* Más completo espectro de recursos de proceso subyacente de Hola y precios
* Escalado automático integrado, equilibrio de carga y supervisión del rendimiento
* Capacidades de prueba en producción, reversión, copia de seguridad y almacenamiento provisional incorporadas

## <a name="new-hosting-features"></a>Nuevas características de hospedaje
En *servicio de aplicaciones de Azure* hello *aplicación móvil* código de back-end se ejecuta en Hola mismo contenedor como aplicación Web y API App. Por lo tanto pueden sacar provecho de todas las características de hello en este contenedor, incluidos algunos de los que no se encuentra actualmente en servicios móviles:

* Adición de lógica de back-end de ejecución continua a través de trabajos web
* Garantía de que el código de back-end siempre está ejecutándose
* Usar personalizado tooprovide CNAME descriptivo y estable nombres tooyour extremos móvil de back-end
* Escala geográfica de la aplicación con Administrador de tráfico
* Se incluyen las bibliotecas y los paquetes que desee.
* (Para. NET) Aproveche todas las características de ASP.NET, incluido MVC.
* (Para Node.js) Aproveche cualquier biblioteca de JavaScript puro del ecosistema de nodo de hello, incluidas las bibliotecas comunes de MVC.

## <a name="access-on-premises-data-using-vnet"></a>Acceso a datos locales con red virtual
Con servicios móviles de hoy en día que ya puede utilizar conexiones híbridas tooaccess recursos locales. Sin embargo, hay situaciones en las que es preferible una solución de VPN. Con *Servicio de aplicaciones de Azure* puede usar la red virtual de Azure para el código de back-end de la aplicación móvil.

## <a name="use-your-favorite-backend-language"></a>Uso del lenguaje de back-end favorito
*Servicio de aplicaciones de Azure* ofertas más amplias y mayor compatibilidad para plataformas ASP.NET y Node.js, incluidos el acceso toohello tiempos de ejecución más reciente.

## <a name="set-up-automatic-scale"></a>Configuración de la escala automática
Con Servicios móviles, todas las instancias de su código de back-end se ejecutaban en máquinas virtuales pequeñas. *Servicio de aplicaciones de Azure* permite tooselect tamaño de Hola de las máquinas virtuales de un conjunto mucho más completa de opciones. Puede también rápidamente escalar vertical u horizontalmente toohandle ninguna carga de cliente entrantes, en función de diferentes métricas de rendimiento.

## <a name="be-in-hello-know"></a>Ser Hola "sabe"
Reaccionar tooissues en tiempo real con alertas y supervisión tooautomatically notificar a usted y su equipo. Integrar el análisis de las aplicaciones avanzadas y funcionalidad de supervisión de New Relic y AppInsights tooget incluso transmite una visión sobre el rendimiento de la aplicación móvil. Con *servicio de aplicaciones de Azure* ahora puede configurar alertas basadas en gran variedad de métricas de rendimiento, ya sea mediante programación y a través de hello Portal de Azure.

## <a name="keep-your-assets-safe"></a>Proteja los activos
Realice una copia de seguridad automática del back-end y la base de datos. El código y los datos es seguro frente a desastres y fácilmente restaurada, permitiéndole toorun su negocio con confianza.

## <a name="ready-stage-go"></a>Preparado, listo, ¡ya!
Con *Servicio de aplicaciones de Azure* ahora puede crear varios entornos de ensayo y prueba privados para las aplicaciones móviles. Utilizarlos tooperform pruebas antes de implementar. Intercambiar tooproduction sin tiempo de inactividad. Las aplicaciones Web están previamente cargadas, garantizar la mejor experiencia de usuario Hola.

Para comenzar a aprovechar el *Servicio de aplicaciones* en su servicio móvil existente, siga este [tutorial](app-service-mobile-migrating-from-mobile-services.md).
