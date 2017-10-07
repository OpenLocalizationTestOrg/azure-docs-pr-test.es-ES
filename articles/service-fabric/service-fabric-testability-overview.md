---
title: "Introducción al servicio de análisis de aaaFault | Documentos de Microsoft"
description: "Este artículo describe Hola servicio de análisis de errores de Service Fabric para inducir a errores y ejecutar escenarios de prueba en los servicios."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: timlt
editor: vturecek
ms.assetid: 1f064276-293a-4989-a513-e0d0b9fdf703
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: anmola
ms.openlocfilehash: deac16ec830aa10d4e488e60691faa9ef2b6cd33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-fault-analysis-service"></a>Introducción toohello servicio de análisis de errores
Hola error Analysis Services está diseñado para probar los servicios que se basan en Microsoft Azure Service Fabric. Con hello error Analysis Services puede inducir a errores significativos y ejecutar escenarios de prueba completada en sus aplicaciones. Estos errores y escenarios de probar y validar Hola numerosos Estados y transiciones que experimentará un servicio a lo largo de su duración, en forma controlada, segura y coherente.

Las acciones son errores individuales hello como destino un servicio para probarlo. Un programador del servicio puede utilizar como bloques de creación toowrite complicado escenarios. Por ejemplo:

* Reinicie un nodo toosimulate cualquier número de situaciones donde se reinicia una máquina o una máquina virtual.
* Mueve una réplica del equilibrio de carga de servicio con estado toosimulate, conmutación por error o actualización de la aplicación.
* Invocar la pérdida de quórum en un toocreate una situación donde las operaciones de escritura no pueden continuar porque no hay suficientes datos nuevos de tooaccept de "copia de seguridad" o "secundario" réplicas de servicio con estado.
* Invocar la pérdida de datos en un toocreate una situación donde todo el estado en memoria se borra completamente fuera de servicio con estado.

Los escenarios son operaciones complejas compuestas por una o varias acciones. Hola error Analysis Services proporciona dos escenarios completos integrados:

* Escenario de caos
* Escenario de conmutación por error

## <a name="testing-as-a-service"></a>Prueba como servicio
Hola error Analysis Services es un servicio de sistema de Service Fabric que se iniciará automáticamente con un clúster de Service Fabric. Este servicio actúa como host de hello para la inyección de código de error, la ejecución de escenario de prueba y análisis de mantenimiento. 

![Servicio de análisis de errores][0]

Cuando se inicia un escenario de prueba o acción de error, se envía un comando toohello servicio de análisis de errores toorun Hola acción o prueba escenario de error. Hola error Analysis Services está activo para que pueda ejecutar escenarios y errores de forma confiable y validar los resultados. Por ejemplo, un escenario de prueba de larga duración se puede ejecutar confiable con hello error Analysis Services. Y porque se están ejecutando pruebas dentro de clúster de hello, servicio de hello puede examinar estado Hola de clúster de Hola y su tooprovide de servicios información más detallada acerca de los errores.

## <a name="testing-distributed-systems"></a>Prueba de los sistemas distribuidos
Service Fabric realiza trabajo Hola de escritura y administración de aplicaciones distribuidas escalables que mucho más fácil. Hola error Analysis Services facilita las pruebas en una aplicación distribuida del mismo modo más fácil. Hay tres puntos principales que deben toobe ha resuelto durante las pruebas:

1. Simular/generar errores que pueden producirse en situaciones del mundo real: uno de los aspectos importantes de Hola de Service Fabric es que hace que las aplicaciones distribuidas toorecover de distintos errores. Sin embargo, tootest que Hola aplicación es capaz de toorecover de estos errores, necesitamos toosimulate/generar en mecanismo estos errores reales en un entorno de pruebas controlado.
2. Hola capacidad toogenerate correlacionado errores: básicos errores de sistema de hello, como errores de red y de máquina, son tooproduce fácil individualmente. Generar un número significativo de escenarios que pueden suceder en Hola mundo real como resultado de las interacciones de Hola de estos errores individuales no es trivial.
3. Experiencia unificada a través de varios niveles de desarrollo e implementación: existen muchos sistemas de inserción de errores que pueden realizar varios tipos de errores. Sin embargo, la experiencia de hello en todos estos es deficiente al mover de escenarios de desarrollador de un solo cuadro, hello toorunning igual pruebas en entornos de prueba de gran tamaño, toousing para la prueba en producción.

Aunque hay muchas toosolve mecanismos estos problemas, un sistema que Hola igual con garantías necesarias--todos forma Hola desde un entorno de desarrollo de un solo cuadro, tootest en clústeres de producción, es que faltan. Hola error Analysis Services ayuda a los desarrolladores de aplicaciones de hello concentrarse en probar su lógica de negocios. Hola error Analysis Services proporciona que todas las funcionalidades de hello necesaria la interacción de hello tootest del servicio de hello con sistema distribuido de hello subyacente.

### <a name="simulatinggenerating-real-world-failure-scenarios"></a>Simulación/generación de escenarios de error reales
solidez de hello tootest de un sistema distribuido frente a errores, necesitamos un errores de toogenerate mecanismo. Mientras que en teoría, generar un error como un nodo inactivo parece sencillo, que se inicia alcanzando Hola mismo conjunto de problemas de coherencia que está tratando de toosolve Service Fabric. Por ejemplo, si lo deseamos tooshut hacia abajo un nodo, Hola necesaria flujo de trabajo es siguiente hello:

1. Desde el cliente de hello, emitir una solicitud de cierre del nodo.
2. Envío (nodo) Hola solicitud toohello derecho.
   
    a. Si no se encuentra el nodo de hello, debe indicar un error.
   
    b. Si se encuentra el nodo de hello, debe devolver solo si el nodo de Hola se apaga.

Error de hello tooverify desde una perspectiva de prueba, prueba Hola debe tooknow que cuando sea inducido este error, error de Hola que sucede en realidad. garantía de Hola que proporciona Service Fabric es que ninguno de los nodos Hola irá hacia abajo o ya estaba hacia abajo al comando hello alcanzado nodo Hola. En ambos caso Hola prueba debe ser capaz de toocorrectly razón acerca del estado de Hola y succeed o fail correctamente en su validación. Un sistema que se implementa fuera Hola de Service Fabric toodo mismo conjunto de errores podrían Hola acierto que muchas de red, el hardware y los problemas de software, lo que evitaría que proporciona garantías anteriores. En presencia de Hola de problemas de hello indicadas antes, Service Fabric se reconfigurar Hola clúster estado toowork alrededor de los problemas de Hola y Hola, por tanto, el servicio de análisis de errores seguirá toogive capaz de hello derecho establecido de garantías.

### <a name="generating-required-events-and-scenarios"></a>Generación de los eventos y los escenarios requeridos
Mientras que simule un error de reales de forma coherente es difícil toostart con, Hola capacidad toogenerate correlacionado errores es incluso más difícil. Por ejemplo, una pérdida de datos ocurre en un servicio con estado persistente cuando se producen Hola siguientes cosas:

1. Solo un quórum de escritura de réplicas de hello están al día en la replicación. Todas las réplicas secundarias de hello retrasen Hola principal.
2. quórum de escritura de Hello deja de funcionar debido a las réplicas de hello va hacia abajo (vence tooa el paquete de código o nodo bajan).
3. quórum de escritura de Hello no se vuelven a estar en porque datos Hola para réplicas de Hola se pierde (debido a daños toodisk o restaurar la máquina).

Producir estos errores correlacionados en Hola mundo real, pero no con tanta frecuencia como errores individuales. Hola tootest de capacidad para estos escenarios antes de que ocurran en producción es fundamental. Incluso más importante es Hola capacidad toosimulate estos escenarios con cargas de trabajo de producción en circunstancias controladas (en medio de Hola de día de hello con todos los ingenieros de papel). Que es mucho mejor que cuando se tiene producir por hello primera vez en producción a las 2:00 A.M.

### <a name="unified-experience-across-different-environments"></a>Experiencia unificada en distintos entornos
Hola tradicionalmente ha consistido toocreate tres conjuntos diferentes de experiencias, uno para el entorno de desarrollo de hello, uno para las pruebas y otro para producción. modelo de Hello era:

1. En el entorno de desarrollo de hello, generan las transiciones de estado que permiten a las pruebas unitarias de métodos individuales.
2. En el entorno de prueba de hello, generan errores tooallow-to-end realice pruebas que ejecuten diversos escenarios de error.
3. Mantener tooprevent buen estado del entorno de producción Hola los errores no natural y tooensure que no hay respuesta humana extremadamente rápido toofailure.

En el tejido de servicio, a través de hello error Analysis Service, proponemos tooturn esto alrededor y use Hola igual metodología de tooproduction de entorno de desarrollo. Hay dos tooachieve formas esto:

1. tooinduce controla los errores, usar hello API de servicios de análisis de errores de un entorno de un solo cuadro tooproduction de manera Hola todos los clústeres.
2. Hola toogive clúster fiebre que provoca errores automática de inducción automática de errores, utilice Hola error Analysis Services toogenerate. Tasa de Hola control de errores a través de configuración permite Hola mismo toobe de servicio probado de forma diferente en entornos diferentes.

Con Service Fabric, aunque sería diferente en distintos entornos de hello, escala de Hola de errores de los mecanismos reales de hello sería idénticos. Esto permite un mucho más rápida implementación de código hello y canalización capacidad tootest Hola servicios con cargas reales.

## <a name="using-hello-fault-analysis-service"></a>Uso de hello error Analysis Services
**C#**

Características del servicio de análisis de errores se encuentran en espacio de nombres de hello System.Fabric Hola paquete Microsoft.ServiceFabric NuGet. características del servicio de análisis de errores de toouse hello, incluyen paquetes de nuget de Hola como una referencia en el proyecto.

**PowerShell**

toouse PowerShell, debe instalar Hola SDK del servicio de Fabric. Después de hello que está instalado el SDK, hello ServiceFabric PowerShell módulo es auto cargado para toouse.

## <a name="next-steps"></a>Pasos siguientes
toocreate realmente servicios de nube escala, es crítico tooensure, tanto antes como después de la implementación, que servicios pueden resistir errores del mundo real. En servicios Hola hoy en día, Hola tooinnovate capacidad rápidamente y mover rápidamente código tooproduction es muy importante. Hola error Analysis Services le ayuda a servicio a los desarrolladores toodo exactamente eso.

Empezar a probar las aplicaciones y servicios mediante integradas de hello [probar escenarios de](service-fabric-testability-scenarios.md), o crear sus propios escenarios de prueba con hello [acciones de error](service-fabric-testability-actions.md) proporcionada por hello error Analysis Services.

<!--Image references-->
[0]: ./media/service-fabric-testability-overview/faultanalysisservice.png
