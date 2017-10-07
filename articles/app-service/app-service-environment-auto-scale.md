---
title: aaaAutoscaling y v1 de entorno del servicio de aplicaciones
description: "Escalado automático y entorno del Servicio de aplicaciones"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: c23af2d8-d370-4b1f-9b3e-8782321ddccb
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 1a03cf494309e80596b64471d1a067b2f64a9fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a>Escalado automático y App Service Environment v1

> [!NOTE]
> Este artículo trata sobre Hola v1 de entorno del servicio de aplicaciones.  Hay una versión más reciente de hello entorno del servicio de aplicación que es más fácil toouse y se ejecuta en una infraestructura más eficaz. toolearn más información acerca de la nueva versión de hello iniciar con hello [toohello Introducción entono](../app-service/app-service-environment/intro.md).
> 

Los entornos del Servicio de aplicaciones de Azure admiten el *escalado automático*. Puede usar el escalado automático basado en métricas o programación grupos de trabajo individuales.

![Opciones de escalado automático para un grupo de trabajo.][intro]

Ajuste automático optimiza el uso de recursos automáticamente aumentar y reducir un toofit de entorno de servicio de aplicaciones su perfil de presupuesto y carga.

## <a name="configure-worker-pool-autoscale"></a>Configuración del escalado automático de grupo de trabajo
Puede tener acceso a funcionalidad de escalado automático de Hola de hello **configuración** ficha de grupo de trabajo de Hola.

![Pestaña Configuración de grupo de trabajo de Hola.][settings-scale]

Desde allí, Hola interfaz debe ser bastante conocido porque es Hola planear la misma experiencia que verá al escalar un servicio de aplicaciones. 

![Configuración de la escala manual.][scale-manual]

También puede configurar un perfil de escalado automático.

![Configuración del escalado automático.][scale-profile]

Perfiles de escalado automático son límites de tooset útil sobre la escala. De este modo tener una experiencia de rendimiento coherente, mediante el establecimiento de un valor de escala de límite inferior (1) y un techo de gasto predecible, mediante el establecimiento de un límite superior (2).

![Configuración de la escala en el perfil.][scale-profile2]

Después de definir un perfil, puede agregar tooscale de reglas de escalado automático hacia arriba o hacia abajo, número de Hola de instancias de grupo de trabajo de hello dentro de los límites de hello definidas por el perfil de Hola. Las reglas de escalado automático se basan en las métricas.

![Regla de escala.][scale-rule]

 Cualquier grupo de trabajo o las métricas de front-end pueden ser toodefine usa reglas de escalado automático. Estas métricas son Hola mismas métricas puede supervisar en los gráficos de hoja de recursos de Hola o establecer alertas para.

## <a name="autoscale-example"></a>Ejemplo de escalado automático
La mejor manera de ilustrar el escalado automático de un entorno del Servicio de aplicaciones es mediante un escenario.

Este artículo explica todas las consideraciones de hello necesarios al configurar escalado automático. Hola artículo le guiará a través de hello las interacciones que surte reproducción al factor de escala automática entornos de servicio de aplicaciones que se hospedan en el entorno del servicio de aplicaciones.

### <a name="scenario-introduction"></a>Introducción al escenario
Frank es un administrador del sistema para una empresa que ha migrado una parte de las cargas de trabajo de Hola que administra tooan entorno de servicio de aplicaciones.

Hello es el entorno de servicio de aplicaciones Configurar escala toomanual como sigue:

* **Servidores front-end** : 3
* **Grupo de trabajo 1**: 10
* **Grupo de trabajo 2**: 5
* **Grupo de trabajo 3**: 5

El grupo de trabajo 1 se usa para las cargas de trabajo de producción, en tanto que los grupos de trabajo 2 y 3 se usan para las cargas de trabajo de control de calidad y desarrollo.

Hello aplicación planes de servicio para preguntas y respuestas y desarrollo están configurados toomanual escala. producción de Hello plan de servicio de aplicaciones se establece tooautoscale toodeal con variaciones en la carga y el tráfico.

Frank está muy familiarizado con la aplicación hello. Sabe que las horas punta Hola de carga son entre las 9:00 A.M. y 6:00 P.M. porque se trata de una aplicación de línea de negocio (LOB) que los empleados usan mientras están en office Hola. El uso cae después, una vez que los usuarios han terminado la jornada. Fuera de horas punta, hay cierta carga porque los usuarios pueden acceder de forma remota aplicación hello mediante sus dispositivos móviles o equipos domésticos. producción de Hello plan de servicio de aplicaciones ya está configurado tooautoscale según el uso de CPU con hello siguientes reglas:

![Configuración específica para las aplicaciones LOB.][asp-scale]

| **Perfil de escalado automático: Días laborables: plan del Servicio de aplicaciones** | **Perfil de escalado automático: Fines de semana: plan del Servicio de aplicaciones** |
| --- | --- |
| **Nombre:** perfil Día laborable |**Nombre:** perfil Fin de semana |
| **Escalar por:** Reglas de rendimiento y programación |**Escalar por:** Reglas de rendimiento y programación |
| **Perfil:** Días laborables |**Perfil:** Fin de semana |
| **Tipo:** periodicidad |**Tipo:** periodicidad |
| **Intervalo de destino:** 5 instancias too20 |**Intervalo de destino:** 3 instancias too10 |
| **Días:** lunes, martes, miércoles, jueves, viernes |**Días:** sábado, domingo |
| **Hora de inicio:** 9:00 |**Hora de inicio:** 9:00 |
| **Zona horaria:** UTC-08 |**Zona horaria:** UTC-08 |
|  | |
| **Regla de escalado automático (escalar verticalmente)** |**Regla de escalado automático (escalar verticalmente)** |
| **Recurso:** Producción (entorno del Servicio de aplicaciones) |**Recurso:** Producción (entorno del Servicio de aplicaciones) |
| **Métrica:** % de CPU |**Métrica:** % de CPU |
| **Operación:** Mayor que 60% |**Operación:** Mayor que 80% |
| **Duración:** 5 minutos |**Duración:** 10 minutos |
| **Agregación de tiempo:** media |**Agregación de tiempo:** media |
| **Acción:** Aumentar recuento en 2 |**Acción:** Aumentar recuento en 1 |
| **Tiempo de finalización (minutos):** 15 |**Tiempo de finalización (minutos):** 20 |
|  | |
| **Regla de escalado automático (reducir verticalmente)** |**Regla de escalado automático (reducir verticalmente)** |
| **Recurso:** Producción (entorno del Servicio de aplicaciones) |**Recurso:** Producción (entorno del Servicio de aplicaciones) |
| **Métrica:** % de CPU |**Métrica:** % de CPU |
| **Operación:** menor que el 30 % |**Operación:** menor que el 20 % |
| **Duración:** 10 minutos |**Duración:** 15 minutos |
| **Agregación de tiempo:** media |**Agregación de tiempo:** media |
| **Acción:** Reducir recuento en 1 |**Acción:** Reducir recuento en 1 |
| **Tiempo de finalización (minutos):** 20 |**Tiempo de finalización (minutos):** 10 |

### <a name="app-service-plan-inflation-rate"></a>Tasa de inflación del plan del Servicio de aplicaciones
Planes de servicio de aplicaciones que están configurado tooautoscale hacerlo a una velocidad máxima por hora. Esta velocidad se calculen según en valores de hello proporcionados en la regla de escalado automático de Hola.

Descripción y calcular Hola *tasa de inflación del plan de servicio de aplicaciones* es importante para el escalado automático de entorno de servicio de aplicaciones porque el grupo de trabajo de tooa de cambios de escala no son instantáneos.

Hola tasa de inflación del plan de servicio de aplicaciones se calcula como sigue:

![Cálculo de la tasa de inflación del plan del Servicio de aplicaciones.][ASP-Inflation]

En función de hello escalado automático: regla escalar vertical para el perfil de día de la semana de Hola de producción de hello plan de servicio de aplicaciones:

![Tasa de inflación del plan del Servicio de aplicaciones para los días laborables basándose en el escalado automático: regla escalar verticalmente.][Equation1]

En caso de hello de hello escalado automático: escalar vertical de la regla para el perfil de fin de semana de Hola de producción de hello plan de servicio de aplicaciones, la fórmula de Hola se resolverá en:

![Tasa de inflación del plan del Servicio de aplicaciones para los fines de semana basado en el escalado automático: regla escalar verticalmente.][Equation2]

Este valor también se puede calcular para operaciones de reducción vertical.

En función de hello escalado automático: regla de escala hacia abajo para el perfil de día de la semana de Hola de producción de hello plan de servicio de aplicaciones, esto sería similar al siguiente:

![Tasa de inflación del plan del Servicio de aplicaciones para los días laborables basándose en el escalado automático: regla reducir verticalmente.][Equation3]

En caso de hello de hello escalado automático: regla de escala hacia abajo para el perfil de fin de semana de Hola de producción de hello plan de servicio de aplicaciones, la fórmula de Hola se resolverá en:  

![Tasa de inflación del plan del Servicio de aplicaciones para los fines de semana basado en el escalado automático: regla reducir verticalmente.][Equation4]

producción de Hello plan de servicio de aplicaciones puede crecer en una velocidad máxima de ocho instancias por hora durante la semana de Hola y cuatro instancias por hora durante un fin de semana Hola. Puede liberar instancias a una velocidad máxima de cuatro instancias por hora durante la semana de Hola y seis instancias por hora durante los fines de semana.

Si varios planes de servicio de aplicaciones se hospedan en un grupo de trabajo, tendrá que hello toocalculate *total tasa de inflación* como suma Hola de tasa de inflación de Hola para hello todos los planes de servicio de aplicaciones que se va a hospedar en ese grupo de trabajo.

![Cálculo de la tasa de inflación total para varios planes del Servicio de aplicaciones hospedados en un grupo de trabajo.][ASP-Total-Inflation]

### <a name="use-hello-app-service-plan-inflation-rate-toodefine-worker-pool-autoscale-rules"></a>Hola servicio de aplicaciones de uso previsto reglas de escalado automático de grupo de trabajo de tasa de inflación toodefine
Los grupos de trabajo que hospedan los planes de servicio de aplicaciones que están configurado tooautoscale deben asignarse a un búfer de la capacidad. búfer de Hello permite toogrow de operaciones de escalado automático de Hola y reducir el plan de servicio de aplicaciones, según sea necesario. mínimo de búfer de Hello sería Hola calcula la tasa de inflación Total de Plan de servicio de aplicación.

Dado que las operaciones de escalado del entorno de servicio de aplicaciones tienen algún tooapply tiempo, cualquier cambio tenga en cuenta más cambios en la demanda que pudieron ocurrir mientras está en curso una operación de escala. tooaccommodate esta latencia, se recomienda que use Hola calcula la tasa de inflación Total de Plan de servicio de aplicación como el número mínimo de Hola de instancias que se agregan para cada operación de escalado automático.

Con esta información, puede definir los Frank Hola siguiendo perfil de escalado automático y reglas:

![Ejemplo de reglas de perfil de escalado automático para línea de negocio.][Worker-Pool-Scale]

| **Perfil de escalado automático: Días laborables** | **Perfil de escalado automático: Fines de semana** |
| --- | --- |
| **Nombre:** perfil Día laborable |**Nombre:** perfil Fin de semana |
| **Escalar por:** Reglas de rendimiento y programación |**Escalar por:** Reglas de rendimiento y programación |
| **Perfil:** Días laborables |**Perfil:** Fin de semana |
| **Tipo:** periodicidad |**Tipo:** periodicidad |
| **Intervalo de destino:** 13 instancias too25 |**Intervalo de destino:** 6 instancias too15 |
| **Días:** lunes, martes, miércoles, jueves, viernes |**Días:** sábado, domingo |
| **Hora de inicio:** 7:00 |**Hora de inicio:** 9:00 |
| **Zona horaria:** UTC-08 |**Zona horaria:** UTC-08 |
|  | |
| **Regla de escalado automático (escalar verticalmente)** |**Regla de escalado automático (escalar verticalmente)** |
| **Recurso:** Grupo de trabajo 1 |**Recurso:** Grupo de trabajo 1 |
| **Métrica:** WorkersAvailable |**Métrica:** WorkersAvailable |
| **Operación:** Menor que 8 |**Operación:** Menor que 3 |
| **Duración:** 20 minutos |**Duración:** 30 minutos |
| **Agregación de tiempo:** media |**Agregación de tiempo:** media |
| **Acción:** Aumentar recuento en 8 |**Acción:** Aumentar recuento en 3 |
| **Tiempo de finalización (minutos):** 180 |**Tiempo de finalización (minutos):** 180 |
|  | |
| **Regla de escalado automático (reducir verticalmente)** |**Regla de escalado automático (reducir verticalmente)** |
| **Recurso:** Grupo de trabajo 1 |**Recurso:** Grupo de trabajo 1 |
| **Métrica:** WorkersAvailable |**Métrica:** WorkersAvailable |
| **Operación:** Mayor que 8 |**Operación:** Mayor que 3 % |
| **Duración:** 20 minutos |**Duración:** 15 minutos |
| **Agregación de tiempo:** media |**Agregación de tiempo:** media |
| **Acción:** Reducir recuento en 2 |**Acción:** Reducir recuento en 3 |
| **Tiempo de finalización (minutos):** 120 |**Tiempo de finalización (minutos):** 120 |

intervalo de destino definido en el perfil de Hola Hola se calcula instancias mínimo Hola definidas en el perfil para el plan de servicio de aplicación hello + búfer.

intervalo máximo de Hello sería la suma de Hola de todos los intervalos máximo de Hola para todos los planes de servicio de aplicaciones que se hospeda en el grupo de trabajo de Hola.

Hola recuento de aumento para escalar Hola reglas debe ser tooat conjunto mínimo de 1 X la tasa de inflación de Plan de servicio de aplicación de escala de seguridad.

Recuento de disminución puede ser ajustado toosomething entre 1/2 X o 1 X Hola tasa de inflación de Plan de servicio de aplicación de escala hacia abajo.

### <a name="autoscale-for-front-end-pool"></a>Escalado automático para un grupo de servidores front-end
Las reglas de escalado automático de front-end son más sencillas que las de los grupos de trabajo. En primer lugar, debe  
Asegúrese de que la duración de medición de Hola y temporizadores de enfriamiento Hola, tenga en cuenta que las operaciones de escala en un plan de servicio de aplicaciones no son instantáneas.

En este escenario, Frank sabe esa tasa de errores de hello aumenta después de utilización de CPU del 80% de llegar a servidores front-end y establece escalado automático de hello en instancias de tooincrease de reglas como se indica a continuación:

![Configuración del escalado automático para un grupo de servidores front-end.][Front-End-Scale]

| **Perfil de escalado automático: Servidores front-end** |
| --- |
| **Nombre:** Escalado automático: Servidores front-end |
| **Escalar por:** Reglas de rendimiento y programación |
| **Perfil:** Todos los días |
| **Tipo:** periodicidad |
| **Intervalo de destino:** 3 instancias too10 |
| **Días:** Todos los días |
| **Hora de inicio:** 9:00 |
| **Zona horaria:** UTC-08 |
|  |
| **Regla de escalado automático (escalar verticalmente)** |
| **Recurso:** Grupo de servidores front-end |
| **Métrica:** % de CPU |
| **Operación:** Mayor que 60% |
| **Duración:** 20 minutos |
| **Agregación de tiempo:** media |
| **Acción:** Aumentar recuento en 3 |
| **Tiempo de finalización (minutos):** 120 |
|  |
| **Regla de escalado automático (reducir verticalmente)** |
| **Recurso:** Grupo de trabajo 1 |
| **Métrica:** % de CPU |
| **Operación:** menor que el 30 % |
| **Duración:** 20 minutos |
| **Agregación de tiempo:** media |
| **Acción:** Reducir recuento en 3 |
| **Tiempo de finalización (minutos):** 120 |

<!-- IMAGES -->
[intro]: ./media/app-service-environment-auto-scale/introduction.png
[settings-scale]: ./media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: ./media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: ./media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: ./media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: ./media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: ./media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: ./media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: ./media/app-service-environment-auto-scale/equation1.png
[Equation2]: ./media/app-service-environment-auto-scale/equation2.png
[Equation3]: ./media/app-service-environment-auto-scale/equation3.png
[Equation4]: ./media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: ./media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: ./media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: ./media/app-service-environment-auto-scale/fe-scale.png
