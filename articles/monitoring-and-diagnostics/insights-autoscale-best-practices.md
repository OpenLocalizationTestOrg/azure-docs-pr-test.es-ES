---
title: "prácticas recomendadas de aaaBest para el escalado automático | Documentos de Microsoft"
description: "Patrones de escalado automático en Azure para Web Apps, conjunto de escalado de máquinas virtuales y Cloud Services"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 9fa2b94b-dfa5-4106-96ff-74fd1fba4657
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: ancav
ms.openlocfilehash: eb731c15e440af93a2675210583878814d0d8818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-autoscale"></a>Procedimientos recomendados de escalado automático
En este artículo se explica tooautoscale de prácticas recomendada en Azure. Azure escalado automático de Monitor se aplica solo demasiado[conjuntos de escalas de máquina Virtual](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [servicios en la nube](https://azure.microsoft.com/services/cloud-services/), y [servicio de aplicaciones: aplicaciones Web](https://azure.microsoft.com/services/app-service/web/). Otros servicios de Azure usan distintos métodos de escalado.

## <a name="autoscale-concepts"></a>Conceptos de escalado automático
* Un recurso solo puede tener *una* configuración de escalado automático.
* Una configuración de escalado automático puede tener uno o varios perfiles y cada perfil, a su vez, puede tener una o varias reglas de escalado automático.
* Una configuración de Autoescala escala instancias horizontalmente, que es *out* aumentando instancias de Hola y *en* reduciendo el número de Hola de instancias.
  Una configuración de escalado automático presenta unos valores máximo, mínimo y predeterminado de instancias.
* Un trabajo de escalado automático siempre lee Hola asociado tooscale métrica activando, si alcanzó el umbral configurado de Hola de escalabilidad horizontal o en escala. En [Métricas comunes de escalado automático de Azure Monitor](insights-autoscale-common-metrics.md) encontrará una lista de métricas por las que el escalado automático puede escalar.
* Todos los umbrales se calculan en el nivel de instancia. Por ejemplo, "escala a través de 1 instancia al promedio de CPU > 80% al recuento de instancias es 2", significa escalado horizontal cuando Hola promedio de CPU en todas las instancias es superior al 80%.
* Las notificaciones de error siempre se reciben por correo electrónico. En concreto, Hola propietario, Colaborador y los lectores de recurso de destino de Hola reciban correo electrónico. Además, siempre se recibe un correo electrónico de *recuperación* cuando el escalado automático se recupere de un error y comience a funcionar con normalidad.
* Pueden participar en tooreceive una notificación de acción de escala correctamente a través de correo electrónico y webhook.

## <a name="autoscale-best-practices"></a>Procedimientos recomendados de escalado automático
Usar hello seguir las prácticas recomendadas que usen el escalado automático.

### <a name="ensure-hello-maximum-and-minimum-values-are-different-and-have-an-adequate-margin-between-them"></a>Asegúrese de valores máximos y mínimos de hello son diferentes y tienen un margen suficiente entre ellos
Si tiene una configuración que tenga como mínimo = 2, máximo = 2 y el recuento de instancias actual de hello es 2, no se puede producir ninguna acción de escala. Mantener un margen suficiente entre los recuentos de instancias máximo y mínimo de hello, que son inclusivos. El escalado automático siempre escala entre estos límites.

### <a name="manual-scaling-is-reset-by-autoscale-min-and-max"></a>El escalado manual se restablece al valor máximo y mínimo de escalado automático.
Si actualizar Hola instancia recuento tooa valor anterior o por debajo del máximo de hello, Hola motor de escalado automático automáticamente manualmente escala mínima atrás toohello (si está por debajo) o hello máximo (si está por encima). Por ejemplo, establecer intervalo de hello entre 3 y 6. Si tiene una instancia en ejecución, motor de escalado automático de hello escala too3 instancias en su siguiente ejecución. Del mismo modo, podría escala de 8 instancias encenderlo too6 su siguiente ejecución.  Ajuste manual de tamaño es muy temporal a menos que restablezca también las reglas de escalado automático de Hola.

### <a name="always-use-a-scale-out-and-scale-in-rule-combination-that-performs-an-increase-and-decrease"></a>Use siempre una combinación de reglas de escalado horizontal y reducción horizontal que realice un aumento y una disminución.
Si usa solo una parte de la combinación de hello, escalado automático escala de que solo out, o bien en hasta el máximo de hello, o como mínimo, se alcanza.

### <a name="do-not-switch-between-hello-azure-portal-and-hello-azure-classic-portal-when-managing-autoscale"></a>No cambie entre Hola portal de Azure y Hola portal de Azure clásico al administrar el escalado automático
Para los servicios de nube y servicios de aplicaciones (aplicaciones Web), utilice toocreate de portal de Azure (portal.azure.com) de Hola y administrar la configuración de escalado automático. Para conjuntos de escalas de máquina Virtual utilice toocreate de PowerShell, CLI o API de REST y administrar la configuración de escalado automático. No se intercambian entre el portal de Azure clásico (manage.windowsazure.com) de Hola y Hola portal de Azure (portal.azure.com) al administrar configuraciones de escalado automático. Hola portal de Azure clásico y su back-end subyacente tiene limitaciones. Mueva el escalado automático de Azure toomanage portal toohello mediante una interfaz gráfica de usuario. Opciones de Hello son toouse Hola Autoescala PowerShell, la CLI o la API de REST (a través del explorador de recursos de Azure).

### <a name="choose-hello-appropriate-statistic-for-your-diagnostics-metric"></a>Elija estadística adecuada de hello para la métrica de diagnósticos
Para las métricas de diagnóstico, puede elegir entre *Media*, *mínimo*, *máximo* y *Total* como una métrica tooscale por. estadística de Hello más común es *Media*.

### <a name="choose-hello-thresholds-carefully-for-all-metric-types"></a>Elija los umbrales de hello cuidadosamente para todos los tipos de métrica
Es recomendable tener cuidado a la hora de elegir los diferentes umbrales de escalado y reducción horizontal en función de las situaciones prácticas.

Se *no se recomienda* Hola a opciones de escalado automático como ejemplos de hello siguientes con valores de umbral igual o muy similar para y en condiciones:

* Aumentar las instancias en 1 cuando el número de subprocesos < = 600
* Disminuir las instancias en 1 cuando el número de subprocesos > = 600

Veamos un ejemplo de lo que puede provocar el comportamiento de tooa que puede parecer confuso. Considere la posibilidad de hello después de la secuencia.

1. Suponga que hay 2 toobegin de instancias con y, a continuación, promedio de Hola de subprocesos por instancia crece too625.
2. El escalado automático escala horizontalmente agregando una tercera instancia.
3. A continuación, se supone que el número de subprocesos de promedio de Hola a través de la instancia está too575.
4. Antes de escalar hacia abajo, escalado automático intenta tooestimate qué estado final Hola será si escala en. Por ejemplo, 575 x 3 (número de instancias actual) = 1725/2 (número final de instancias al reducir verticalmente) = 862,5 subprocesos. Esto significa escalado automático tendría tooimmediately escalabilidad nuevo incluso después de que escalan en, si Hola subproceso promedio recuento sigue siendo Hola mismo o incluso cae solo una cantidad reducida. Sin embargo, si escalado una vez más, debería repetir el proceso completo de hello, iniciales tooan de bucle infinito.
5. tooavoid esta situación (lo que se denomina "aleteo"), escalado automático no se escala hacia abajo en absoluto. En su lugar, se omite y se vuelve a evaluar condición de hello nuevo trabajo de hello siguiente tiempo Hola del servicio se ejecute. Esto puede confundir a muchas personas porque escalado automático no aparecería toowork cuando el recuento de subprocesos promedio de hello 575.

Estimación durante la escala es previsto tooavoid "oscilante" situaciones, donde las acciones de escala y escalado horizontal continuamente avanzar y retroceder. Tenga este comportamiento en cuenta al elegir Hola mismos umbrales para la implementación escalada y en.

Se recomienda elegir un margen suficiente entre Hola de escalado horizontal y de los umbrales. Por ejemplo, considere la posibilidad de hello siguiendo la mejor combinación de regla.

* Aumentar las instancias en 1 cuando el porcentaje de CPU > = 80
* Disminuir las instancias en 1 cuando el porcentaje de CPU > = 60

En este caso  

1. Suponga que hay 2 toostart de instancias con.
2. Si deja de Hola % de CPU promedio en todas las instancias too80, escalado automático admita la ampliación horizontal al agregar una tercera instancia.
3. Ahora suponga que a través de tiempo Hola CPU % está too60.
4. De escala regla del escalado automático calcula el estado final de hello si estuviera en tooscale. Por ejemplo, 60 x 3 (número de instancias actual) = 180/2 (número final de instancias al reducir verticalmente) = 90. Por lo tanto escalado automático no escala de ya que tendría tooscale horizontal nuevo inmediatamente. En su lugar, omite la reducción vertical.
5. las comprobaciones de escalado automático de tiempo siguiente Hello, Hola CPU continúa toofall too50. Lo nuevo - estima la instancia de 50 x 3 = 150 / 2 instancias = 75, que por debajo del umbral de escalado horizontal de Hola de 80, por lo que se escala en instancias de too2 correctamente.

### <a name="considerations-for-scaling-threshold-values-for-special-metrics"></a>Consideraciones para establecer valores de umbral de escalado en métricas especiales
 Para obtener métricas especiales, como métrica de la longitud de cola de Bus de servicio o de almacenamiento, umbral de hello es promedio de Hola de mensajes disponibles por número actual de instancias. Elija cuidadosamente Hola elija el valor de umbral de Hola para esta métrica.

Vamos a mostrar con una tooensure de ejemplo que comprende el comportamiento de hello mejor.

* Aumentar las instancias en 1 cuando el número de mensajes de la cola de almacenamiento > = 50
* Disminuir las instancias en 1 cuando el número de mensajes de la cola de almacenamiento < = 10

Considere la posibilidad de hello sigue secuencia:

1. Hay dos instancias de la cola de almacenamiento.
2. Siguen apareciendo mensajes y cuando revise la cola de almacenamiento de hello, número total de hello lee 50. Se supone que el escalado automático tendría que iniciar una acción de escalado horizontal. Sin embargo, vemos que sigue siendo de 50/2 = 25 mensajes por instancia. Por lo tanto, el escalado horizontal no se ha producido. Para hello primer toohappen de escalabilidad horizontal, número total de mensajes de Hola en cola de almacenamiento de hello debe ser 100.
3. A continuación, se supone que recuento total de mensajes de Hola llega a 100.
4. Se agrega una instancia de cola de almacenamiento 3rd debido a acción de escalado horizontal de tooa.  Hello siguiente acción de escalado horizontal no se realizará hasta Hola total número de mensajes en cola de hello alcanza 150 ya 150/3 = 50.
5. Número de Hola de mensajes en cola de hello obtiene ahora más pequeño. Con 3 instancias, Hola primera escala de acción que se produce cuando hello total de mensajes en todas las colas de suma too30 porque 30/3 = 10 mensajes por instancia, que es el umbral de escala en Hola.

### <a name="considerations-for-scaling-when-multiple-profiles-are-configured-in-an-autoscale-setting"></a>Consideraciones de escalado cuando hay varios perfiles configurados en una configuración de escalado automático
En una configuración de escalado automático, puede elegir un perfil predeterminado, que se aplica siempre (independientemente de programaciones o períodos de tiempo), o bien optar por perfil periódico o por un perfil para un período fijo con una fecha y un intervalo de tiempo.

Cuando el servicio de escalado automático procesarlos, siempre se comprueba en hello siguiendo el orden:

1. Perfil de fecha fija
2. Perfil periódico
3. Perfil predeterminado ("Siempre")

Si se cumple una condición de perfil, escalado automático no condición de comprobación Hola siguiente perfil por debajo de él. El escalado automático solo procesa un perfil cada vez. Esto significa que si desea tooalso incluyen una condición de procesamiento de un perfil de nivel inferior, debe incluir esas reglas también en el perfil actual de Hola.

Analicemos esto con un ejemplo:

Hola imagen siguiente muestra una configuración de escalado automático con un perfil predeterminado de instancias mínimos = 2 y máximas de instancias = 10. En este ejemplo, las reglas son configurado tooscale horizontal cuando Hola el número de mensajes en cola de hello es mayor que 10 y escala de cuando Hola el número de mensajes en cola de hello es menor que 3. Ahora pueden escalar recursos Hola entre 2 y 10 instancias.

Además, hay un perfil periódico establecido para el lunes. Está configurado para un número de instancias mínimo = 2 y un número de instancias máximo = 12. Esto significa que el lunes, Hola primera hora escalado automático comprueba esta condición, si el recuento de instancias de hello es 2, se escala toohello nuevo mínimo de 3. Escalado automático continúa toofind esta condición de perfil coincidente (lunes), siempre y cuando procesa solo basada en CPU Hola escala-out/in reglas configuradas para este perfil. En este momento, no comprueba para la longitud de cola de Hola. Sin embargo, si también desea longitud de cola de hello condición toobe activa, debe también incluir esas reglas de perfil predeterminado de hello en el perfil lunes.

De forma similar, cuando escalado automático cambia el perfil predeterminado de toohello atrás, en primer lugar comprueba si se cumplen las condiciones mínimo y máximo de Hola. Si el número de Hola de instancias en tiempo de hello es 12, se escala en too10, Hola máximo permitido para el perfil predeterminado de Hola.

![configuración de escalado automático](./media/insights-autoscale-best-practices/insights-autoscale-best-practices-2.png)

### <a name="considerations-for-scaling-when-multiple-rules-are-configured-in-a-profile"></a>Consideraciones de escalado cuando hay varias reglas configuradas en un perfil
Hay casos en que se pueden tener tooset varias reglas en un perfil. Hola siguiendo el conjunto de reglas de escalado automático se usa mediante el uso de servicios cuando se establecen varias reglas.

Al *escalar horizontalmente*, el escalado automático se ejecuta si se cumple cualquier regla.
En *de escala*, escalado automático requieren que todas las reglas toobe cumplen.

tooillustrate, suponga que ha Hola siguiendo 4 reglas de escalado automático:

* Con una CPU < 30 %, se reduce horizontalmente en 1
* Con una memoria < 50 %, se reduce horizontalmente en 1
* Con una CPU> 75 %, se escala horizontalmente en 1
* Con una memoria > 75 %, se escala horizontalmente en 1

A continuación, se produce Hola seguimiento:

* Con una CPU del 76 % y una memoria del 50 %, se escala horizontalmente.
* Con una CPU del 50 % y una memoria del 76 %, se escala horizontalmente.

Hola en otra parte, si la CPU es 25% y memoria es hace de escalado automático de 51% **no** en escala. En tooscale, CPU debe ser 29% y memoria 49%.

### <a name="always-select-a-safe-default-instance-count"></a>Seleccione siempre un número predeterminado de instancias seguro
recuento de instancias predeterminadas de Hello es importante de escalado automático escala el recuento de toothat del servicio cuando las métricas no están disponibles. Por tanto, seleccione un número predeterminado de instancias que sea seguro para sus cargas de trabajo.

### <a name="configure-autoscale-notifications"></a>Configure notificaciones de escalado automático
Escalado automático notifica a los administradores de Hola y colaboradores de recurso de Hola por correo electrónico si se produce alguna de hello condiciones siguientes:

* servicio de escalado automático se produce un error tootake una acción.
* Las métricas no están disponibles para el escalado automático servicio toomake una decisión de escala.
* Las métricas están disponible (recuperación) nuevo toomake una decisión de escala.
  Además toohello condiciones anteriores, puede configurar tooget de notificaciones de correo electrónico o webhook una notificación para las acciones de la escala correcta.
  
También puede utilizar un estado de hello toomonitor alerta de registro de actividad del motor de escalado automático de Hola. Presentamos ejemplos[crear una alerta de registro de actividad toomonitor todas las operaciones de motor de escalado automático en su suscripción](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert) o demasiado[crear una alerta de registro de actividad toomonitor todos no pudo escalar de escalado automático en / escalar horizontalmente las operaciones en su suscripción](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).

## <a name="next-steps"></a>Pasos siguientes
- [Crear una alerta de registro de actividad toomonitor todas las operaciones de motor de escalado automático en su suscripción.](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [Crear una alerta de registro de actividad toomonitor todos no pudo escalar de escalado automático en / escalar horizontalmente las operaciones en la suscripción](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)
