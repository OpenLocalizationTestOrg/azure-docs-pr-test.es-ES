---
title: "implementación de Mobile Engagement aaaAzure para la aplicación de juegos"
description: "Tooimplement de escenario de aplicación de juegos Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a>Implementación de Mobile Engagement con una aplicación de juegos
## <a name="overview"></a>Información general
Una nueva empresa de juegos ha lanzado una aplicación de juego de estrategia/juego de rol dedicada a la pesca. juego Hola ha estado ejecutando durante 6 meses. Este juego es una enorme se ejecuta correctamente y tiene millones de descargas y retención de hello es muy alta tooother comparados inicio juego aplicaciones. En la reunión de revisión trimestral de hello, las partes interesadas acuerdan que necesitan tooincrease ingresos medios por usuario (ARPU). Los módulos premium en el juego están disponibles como ofertas especiales. Estos módulos de juegos permiten la apariencia de los usuarios tooupgrade Hola y el rendimiento de sus líneas de pesca y cebos para o enfrenta en juego Hola. Sin embargo, las ventas de módulos son muy bajas. Por lo que deciden primer cliente de hello tooanalyze experiencia con una herramienta de análisis y, a continuación, toodevelop una interacción programa tooincrease ventas mediante avanzado segmentación.

En función de hello [Azure Mobile Engagement - Guía de introducción a los procedimientos recomendados](mobile-engagement-getting-started-best-practices.md) , crear una estrategia de contratación.

## <a name="objectives-and-kpis"></a>Objetivos y KPI
Cumplir con las partes interesadas para el juego de Hola. Todos los equipos acuerdan un objetivo principal - tooincrease ventas de paquete premium en un 15%. Crear unidad y los indicadores clave de rendimiento (KPI) empresariales toomeasure este objetivo

* ¿En qué nivel de juego Hola se compran estos paquetes?
* ¿Qué es ingresos de Hola por usuario, por sesión, por semana y al mes?
* ¿Qué tipos de compra favoritos Hola?

Parte 1 de hello [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explica cómo toodefine Hola objetivos y los KPI. 

Con hello que KPI comerciales ya definido, Hola Mobile producto Manager crea la retención y tendencias de KPI de contratación toodetermine nuevo usuario.

* Supervisar la retención y usar a través de hello siguientes intervalos: diariamente, cada 2 días, semanales, mensuales y cada tres meses.
* Recuentos de usuarios activos
* clasificación de aplicación Hola Hola almacenar

En función de las recomendaciones del equipo de TI de hello, Hola siguientes KPI técnica se agregaron hello tooanswer siguientes preguntas:

* ¿Cuál es la ruta de acceso de los usuarios (qué página visitan, cuánto tiempo pasan los usuarios en ella)?
* Número de bloqueos o errores encontrados por sesión
* ¿Qué versiones de sistema operativo ejecutan mis usuarios?
* ¿Qué es el tamaño medio de Hola de pantalla para Mis usuarios?
* ¿Qué tipo de conectividad de Internet tienen mis usuarios?

Para cada KPI Hola Mobile producto Manager especifica los datos de Hola que necesita y donde se encuentra en la guía.

## <a name="engagement-program-and-integration"></a>Programa de compromiso e integración
Antes de compilar un programa de interacción avanzada, Hola Director de proyecto móvil responsable de proyecto de Hola debe tener un conocimiento profundo de cómo y cuándo productos son consumidos por los usuarios de Hola.

Después de 3 meses, Hola Director de proyecto móvil ha recopilado suficiente tooenhance datos sus ventas de notificación de inserción de la aplicación. Descubre que:

* primera compra de Hello generalmente se produce en el nivel de hello 14. Durante el 90% de los casos, compra hello es nuevas armas legendario para $3.
* En el 80% de los casos, los usuarios que hayan realizado ninguna compra, continuar con el producto de Hola y hacer más compras.
* Los usuarios que han superado el nivel de hello 20, inicie toospend más de 10 $/ semana.
* Los usuarios suelen toobuy paquetes de premium en nivel 16, 24 y 32.

Gracias a analysis toothis Hola Director de proyecto móvil decide toocreate inserción específico notificación secuencias tooincrease en las ventas de la aplicación. Crea tres secuencias push denominadas: Programa de bienvenida, Programa de ventas y Programa de inactivos. Para obtener más información, consulte toohello [guías](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
