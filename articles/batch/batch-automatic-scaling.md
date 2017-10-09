---
title: "escala de aaaAutomatically nodos de cálculo en un grupo de lote de Azure | Documentos de Microsoft"
description: "Habilitar el escalado automático en un toodynamically de grupo en la nube ajuste el número de Hola de nodos de proceso en el grupo de Hola."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: tysonn
ms.assetid: c624cdfc-c5f2-4d13-a7d7-ae080833b779
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: multiple
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6d1e0c5d8e0e56e15a4d3588150f2466a689f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-automatic-scaling-formula-for-scaling-compute-nodes-in-a-batch-pool"></a>Creación de una fórmula de escala automática para escalar nodos de proceso en un grupo de Batch

Azure Batch puede escalar grupos automáticamente en función de los parámetros que defina. Con el escalado automático, lote agrega dinámicamente el grupo de nodos tooa como tarea aumente la demanda y quita nodos de proceso disminuir. Puede ahorrarle tiempo y dinero mediante el ajuste automático de número de Hola de nodos de cálculo usados por la aplicación de lote. 

Habilite el escalado automático en un grupo de nodos de ejecución asociándolo a una *fórmula de escalado automático* que se puede definir. Hola servicio por lotes utiliza a Hola escalado automático el número de Hola de toodetermine fórmulas de nodos de proceso que son necesario tooexecute la carga de trabajo. Los nodos de ejecución pueden ser nodos dedicados o [nodos de prioridad baja](batch-low-pri-vms.md). Lote responde tooservice datos de métricas que se recopilaron periódicamente. Con estos datos de métricas, lote ajusta número Hola de nodos de proceso de grupo de hello en función de la fórmula y en un intervalo configurable.

Puede habilitar el escalado automático al crear un grupo o bien en un grupo existente. También puede cambiar una fórmula existente en un grupo configurado para el escalado automático. Lote le permite tooevaluate las fórmulas antes de asignarlas toopools y toomonitor estado Hola de ajuste de escala automática se ejecuta.

Este artículo describe Hola distintas entidades que forman las fórmulas de escalado automático, incluidas las variables, operadores, las operaciones y funciones. Se describe cómo tooobtain diversas métricas de recursos y tareas de lote de proceso. Puede usar estos tooadjust métricas el número de nodos de la agrupación según el estado de tarea y de uso de recursos. A continuación, se describe cómo tooconstruct una fórmula y habilitación automática de ajuste de escala en un grupo mediante el uso de ambos hello las API de .NET y REST de lote. Por último, terminaremos con algunas fórmulas de ejemplo.

> [!IMPORTANT]
> Cuando se crea una cuenta de lote, puede especificar hello [configuración de la cuenta](batch-api-basics.md#account), que determina si se asignan grupos en una suscripción a un servicio de lote (valor predeterminado de hello), o en su suscripción de usuario. Si ha creado su cuenta de lote con la configuración predeterminada del servicio de lote de hello, su cuenta es tooa limita el número máximo de núcleos que se puede usar para su procesamiento. Hola servicio por lotes escala nodos de proceso solo una toothat límite de núcleos. Por esta razón, Hola servicio por lotes puede no llegó al número de destino de Hola de nodos de proceso especificado por una fórmula de Autoescala. Vea [las cuotas y límites de hello servicio Azure Batch](batch-quota-limit.md) para obtener información sobre cómo ver y aumentar las cuotas de cuenta.
>
>Si ha creado su cuenta con la configuración de suscripción de usuario de hello, su cuenta de recursos compartidos de cuota de núcleos de hello para la suscripción de Hola. Para más información, consulte [Límites de Virtual Machines](../azure-subscription-service-limits.md#virtual-machines-limits) en [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../azure-subscription-service-limits.md).
>
>

## <a name="automatic-scaling-formulas"></a>Fórmulas de escalado automático
Una fórmula de escalado automático es un valor de cadena que el usuario define y contiene una o varias instrucciones. fórmula de Autoescala de Hola se asigna del grupo de tooa [autoScaleFormula] [ rest_autoscaleformula] elemento (REST de lote) o [CloudPool.AutoScaleFormula] [ net_cloudpool_autoscaleformula] propiedad (lote. NET). Hola servicio por lotes utiliza su número de destino de hello toodetermine fórmulas de nodos de proceso en grupo de hello para el siguiente intervalo de procesamiento de Hola. cadena de fórmula de Hello no puede superar los 8 KB, puede incluir los informes de too100 que están separados por punto y coma y pueden incluir saltos de línea y comentarios.

Puede imaginarse que las fórmulas de escalado automático son un "lenguaje" de escalado automático de Batch. Instrucciones fórmulas son expresiones de forma libre que pueden incluir variables definidas por el servicio (variables definidas por el servicio por lotes Hola) y variables definidas por el usuario (variables que defina). Pueden realizar diversas operaciones en estos valores mediante funciones, operadores y tipos integrados. Por ejemplo, una instrucción puede tardar Hola siguiente forma:

```
$myNewVariable = function($ServiceDefinedVariable, $myCustomVariable);
```

Las fórmulas suelen tener varias instrucciones que realizan operaciones en los valores obtenidos en las instrucciones anteriores. Por ejemplo, en primer lugar se obtienen un valor para `variable1`, a continuación, páselo tooa función toopopulate `variable2`:

```
$variable1 = function1($ServiceDefinedVariable);
$variable2 = function2($OtherServiceDefinedVariable, $variable1);
```

Incluya estas instrucciones en el tooarrive de fórmula de escalado automático en un número de destino de nodos de proceso. Los nodos dedicados y los nodos de prioridad baja tienen sus propios valores de destino, por lo que puede definir un destino para cada tipo de nodo. Una fórmula de escalado automático puede incluir un valor de destino para los nodos dedicados, un valor de destino para los nodos de prioridad baja o ambos.

número de destino de Hola de nodos podría estar superior, inferior, o igual que el número actual de Hola de nodos de ese tipo en el grupo de Hola Hola. Batch evalúa la fórmula de escalado automático del grupo según un intervalo específico (consulte [Intervalo de escalado automático](#automatic-scaling-interval)). Lote ajusta el número de destino de Hola de cada tipo de nodo en el número de toohello de grupo de Hola que especifica la fórmula de escalado automático en tiempo de Hola de evaluación.

### <a name="sample-autoscale-formula"></a>Fórmula de escalado automático de muestras

Este es un ejemplo de una fórmula de Autoescala que puede ser toowork ajustada para la mayoría de los escenarios. Hola variables `startingNumberOfVMs` y `maxNumberofVMs` en hello fórmula de ejemplo puede ser ajustado tooyour necesidades. Esta fórmula escala nodos dedicados, pero puede ser modificado tooapply tooscale también nodos de prioridad baja. 

```
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicatedNodes=min(maxNumberofVMs, pendingTaskSamples);
```

Con esta fórmula de escalado automático, grupo de Hola se crea inicialmente con una sola máquina virtual. Hola `$PendingTasks` métrica define el número de Hola de tareas que están en cola o en ejecución. fórmula de Hello busca Hola promedio de las tareas pendientes de hello últimos 180 segundos y establece hello `$TargetDedicatedNodes` variable según corresponda. fórmula de Hello garantiza que número de destino de Hola de nodos dedicados nunca supere el 25 máquinas virtuales. Las tareas nuevas se envían, grupo de hello automáticamente a medida que aumenta. Como tareas se completan, las máquinas virtuales se convierten en uno por uno libre y fórmula de Autoescala de hello disminuye grupo Hola.

## <a name="variables"></a>variables
En las fórmulas de escalado automático puede usar tanto variables **definidas por el servicio** como variables **definidas por el usuario**. se crean variables definidas por el servicio de Hello en toohello servicio por lotes. Algunas variables definidas por el servicio son de lectura y escritura, mientras que otras son de solo lectura. Las variables definidas por el usuario son las que usted define. En la fórmula de ejemplo de Hola se muestra en la sección anterior de hello, `$TargetDedicatedNodes` y `$PendingTasks` son variables definidas por el servicio. Las variables `startingNumberOfVMs` y `maxNumberofVMs` son variables definidas por el usuario.

> [!NOTE]
> Las variables definidas por el servicio van siempre precedidas de un símbolo de dólar ($). Para variables definidas por el usuario, el signo de dólar de hello es opcional.
>
>

Hola las tablas siguientes se muestra ambos lectura / escritura y variables de solo lectura que se definen mediante Hola servicio por lotes.

Puede obtener y establecer valores de hello de estas variables definidas por el servicio de número de hello toomanage de nodos de proceso en un grupo de:

| Variables definidas por el servicio de solo escritura | Descripción |
| --- | --- |
| $TargetDedicatedNodes |número de destino de Hola de dedicado nodos de grupo de Hola de ejecución. número de Hola de nodos dedicados se especifica como un destino como un grupo puede no siempre se consigue un número de hello deseado de nodos. Por ejemplo, si se modifica el número de destino de Hola de nodos dedicados por una evaluación de escalado automático antes de hello grupo alcanza el destino inicial hello, a continuación, grupo hello no puede llegar al destino de Hola. <br /><br /> Un grupo en una cuenta creada con la configuración de servicio por lotes de hello no puede alcance su destino si el destino de hello supera una cuota de nodos o núcleos de la cuenta de lote. Un grupo en una cuenta creada con la configuración de suscripción de usuario de hello no puede alcance su destino si el destino de hello supera la cuota de núcleo compartido de hello para la suscripción de Hola.|
| $TargetLowPriorityNodes |número de destino de Hola de prioridad baja nodos de grupo de Hola de ejecución. número de Hola de nodos de prioridad baja se especifica como un destino como un grupo puede no siempre se consigue un número de hello deseado de nodos. Por ejemplo, si se modifica el número de destino de Hola de nodos de prioridad baja por una evaluación de escalado automático antes de hello grupo alcanza el destino inicial hello, a continuación, grupo hello no puede llegar al destino de Hola. Un grupo puede también no se alcance su destino si el destino de hello supera una cuota de nodos o núcleos de la cuenta de lote. <br /><br /> Para obtener más información sobre los nodos de ejecución de prioridad baja, consulte [Uso de máquinas virtuales de prioridad baja con Batch (versión preliminar)](batch-low-pri-vms.md). |
| $NodeDeallocationOption |acción de Hola que tiene lugar cuando se quitan nodos de proceso de un grupo. Los valores posibles son:<ul><li>**colocarlo en cola**: finaliza las tareas inmediatamente y pone en cola de trabajos de Hola para que se vuelve a programar.<li>**terminar**: finaliza las tareas inmediatamente y elimina de la cola de trabajos de Hola.<li>**taskcompletion**--espera que está ejecutando tareas toofinish y, a continuación, quita el nodo de Hola de grupo de Hola.<li>**retaineddata**--espera a que todos los Hola conservan tarea datos locales en hello nodo toobe limpia antes de quitar el nodo de Hola de grupo de Hola.</ul> |

Puede obtener valor de Hola de estos ajustes de toomake de variables definidas por el servicio que se basan en las métricas de servicio por lotes de hello:

| Variables definidas por el servicio de solo lectura | Description |
| --- | --- |
| $CPUPercent |Porcentaje medio de Hello del uso de CPU. |
| $WallClockSeconds |número de Hola de segundos consumidos. |
| $MemoryBytes |promedio de Hola de megabytes utilizados. |
| $DiskBytes |promedio de Hola de gigabytes usados en los discos locales de Hola. |
| $DiskReadBytes |número de Hola de bytes leídos. |
| $DiskWriteBytes |número de Hola de bytes escritos. |
| $DiskReadOps |se realiza el recuento de Hola de operaciones de lectura en el disco. |
| $DiskWriteOps |recuento de Hola de operaciones de disco de escritura realizadas. |
| $NetworkInBytes |número de Hola de bytes de entrada. |
| $NetworkOutBytes |número de Hola de bytes de salida. |
| $SampleNodeCount |recuento de Hola de nodos de proceso. |
| $ActiveTasks |número de Hola de tareas que son tooexecute listo pero aún no se ejecute. recuento de Hello $ActiveTasks incluye todas las tareas que están en estado activo de Hola y cuyas dependencias se han cumplido. Las tareas que están en estado activo de hello pero no se han cumplido cuyas dependencias se excluyen de recuento de hello $ActiveTasks.|
| $RunningTasks |número de Hola de tareas en un estado de ejecución. |
| $PendingTasks |suma de Hola de $ActiveTasks y $RunningTasks. |
| $SucceededTasks |número de Hola de tareas que finalizaron correctamente. |
| $FailedTasks |número de Hola de tareas que no se pudo. |
| $CurrentDedicatedNodes |número actual de Hola de dedicado nodos de proceso. |
| $CurrentLowPriorityNodes |número actual de Hola de prioridad baja de proceso nodos, incluidos los que se han da. |
| $PreemptedNodeCount | número de Hola de nodos de grupo de Hola que están en un estado de da. |

> [!TIP]
> Hello definida por el servicio de solo lectura, las variables que se muestran en la tabla anterior de hello están *objetos* que proporcionan varios métodos datos tooaccess asociadas a cada una. Para obtener más información, consulte la sección [Obtención de datos de ejemplo](#getsampledata), descrita más adelante en este artículo.
>
>

## <a name="types"></a>Tipos
Estos son los tipos que se admiten en las fórmulas:

* double
* doubleVec
* doubleVecList
* cadena
* marca de tiempo: marca de tiempo es una estructura compuesta que contiene Hola siguientes a miembros:

  * year
  * mes (1-12)
  * día (1-31)
  * día de la semana (en formato de Hola de número; por ejemplo, 1 para el lunes)
  * hora (en formato de número de 24 horas; por ejemplo, 13 significa 1 p.m.)
  * minuto (00-59)
  * segundo (00-59)
* timeinterval

  * TimeInterval_Zero
  * TimeInterval_100ns
  * TimeInterval_Microsecond
  * TimeInterval_Millisecond
  * TimeInterval_Second
  * TimeInterval_Minute
  * TimeInterval_Hour
  * TimeInterval_Day
  * TimeInterval_Week
  * TimeInterval_Year

## <a name="operations"></a>Operaciones
Estas operaciones se permiten en los tipos de Hola que figuran en la sección anterior de Hola.

| Operación | Operadores admitidos | Tipo de resultado |
| --- | --- | --- |
| double *operador* double |+, -, *, / |double |
| double *operador* timeinterval |* |timeinterval |
| doubleVec *operador* double |+, -, *, / |doubleVec |
| doubleVec *operador* doubleVec |+, -, *, / |doubleVec |
| timeinterval *operador* double |*, / |timeinterval |
| timeinterval *operador* timeinterval |+, - |timeinterval |
| timeinterval *operador* timestamp |+ |timestamp |
| timestamp *operador* timeinterval |+ |timestamp |
| timestamp *operador* timestamp |- |timeinterval |
| *operador*double |-, ! |double |
| *operador*timeinterval |- |timeinterval |
| double *operador* double |<, <=, ==, >=, >, != |double |
| string *operador* string |<, <=, ==, >=, >, != |double |
| timestamp *operador* timestamp |<, <=, ==, >=, >, != |double |
| timeinterval *operador* timeinterval |<, <=, ==, >=, >, != |double |
| double *operador* double |&&, &#124;&#124; |double |

Cuando se prueba un valor double con un operador ternario (`double ? statement1 : statement2`), el valor distinto de cero es **true** y cero es **false**.

## <a name="functions"></a>Functions
Estos predefinidos **funciones** están disponibles para toouse en la definición de una fórmula de escala automática.

| Función | Tipo de valor devuelto | Description |
| --- | --- | --- |
| avg(doubleVecList) |double |Devuelve Hola valor promedio de todos los valores de hello doubleVecList. |
| len(doubleVecList) |double |Devuelve Hola longitud del vector de Hola que se crea a partir de hello doubleVecList. |
| lg(double) |double |Devuelve Hola logaritmo en base 2 de hello dobles. |
| lg(doubleVecList) |doubleVec |Devuelve registros todos Hola base 2 de hello doubleVecList. Un vec (Double) se debe pasar explícitamente para el parámetro hello. En caso contrario, se supone la versión de lg(double) dobles de Hola. |
| ln(double) |double |Devuelve Hola logaritmo natural de hello doble. |
| ln(doubleVecList) |doubleVec |Devuelve registros todos Hola base 2 de hello doubleVecList. Un vec (Double) se debe pasar explícitamente para el parámetro hello. En caso contrario, se supone la versión de lg(double) dobles de Hola. |
| log(double) |double |Devuelve Hola logaritmo en base 10 de hello dobles. |
| log(doubleVecList) |doubleVec |Devuelve registros todos hello en base 10 de hello doubleVecList. Un vec (Double) se debe pasar explícitamente para un parámetro double único Hola. En caso contrario, se supone la versión de log(double) dobles de Hola. |
| max(doubleVecList) |double |Devuelve Hola valor máximo en doubleVecList Hola. |
| min(doubleVecList) |double |Devuelve Hola valor mínimo de hello doubleVecList. |
| norm(doubleVecList) |double |Devuelve Hola norma dos del vector de Hola que se crea a partir de hello doubleVecList. |
| percentile(doubleVec v, double p) |double |Devuelve Hola elemento de percentil del vector de hello v. |
| rand() |double |Devuelve un valor aleatorio entre 0,0 y 1,0. |
| range(doubleVecList) |double |Devuelve la diferencia de hello entre los valores máximo y mínimo de Hola de hello doubleVecList. |
| std(doubleVecList) |double |Devuelve Hola desviación estándar de muestra de los valores de hello en hello doubleVecList. |
| stop() | |Detiene la evaluación de expresión de escalado automático de Hola. |
| sum(doubleVecList) |double |Devuelve Hola suma de todos los componentes de Hola de hello doubleVecList. |
| time(string dateTime="") |timestamp |Devuelve marca de tiempo de Hola de hello hora actual si no hay parámetros se pasan u Hola marca de tiempo de la cadena de fecha y hora de hello si se pasa. Los formatos de dateTime compatibles son W3C-DTF y RFC 1123. |
| val(doubleVec v, double i) |double |Devuelve el valor de hello del elemento hello en la posición i del vector v, con el índice inicial de cero. |

Algunas de las funciones de Hola que se describen en la tabla anterior de hello pueden aceptar una lista como argumento. lista separada por comas de Hello es cualquier combinación de *doble* y *doubleVec*. Por ejemplo:

`doubleVecList := ( (double | doubleVec)+(, (double | doubleVec) )* )?`

Hola *doubleVecList* valor es convertido tooa único *doubleVec* antes de evaluación. Por ejemplo, si `v = [1,2,3]`, a continuación, llamar a `avg(v)` es equivalente toocalling `avg(1,2,3)`. Al llamar a `avg(v, 7)` es equivalente toocalling `avg(1,2,3,7)`.

## <a name="getsampledata"></a>Obtención de datos de ejemplo
Las fórmulas de Autoescala actúan en los datos de las métricas (ejemplos) proporcionada por hello servicio por lotes. Una fórmula aumenta o reduce el tamaño del grupo en función de los valores de hello que obtiene del servicio de Hola. variables definidas por el servicio de Hola que se describieron anteriormente son objetos que proporcionan varios métodos tooaccess datos que está asociados a ese objeto. Por ejemplo, hello expresión siguiente muestra un saludo de solicitud tooget últimos cinco minutos de uso de CPU:

```
$CPUPercent.GetSample(TimeInterval_Minute * 5)
```

| Método | Description |
| --- | --- |
| GetSample() |Hola `GetSample()` método devuelve un vector de muestras de datos.<br/><br/>Un ejemplo tiene un valor de 30 segundos de datos de métrica. En otras palabras, las muestras se obtienen cada 30 segundos. Pero tal y como se indica a continuación, hay un retraso entre cuando se recopila una muestra y cuándo es fórmula tooa disponible. Por lo tanto, puede que no todos los ejemplos durante un período de tiempo determinado estén disponibles para la evaluación a través de una fórmula.<ul><li>`doubleVec GetSample(double count)`<br/>Especifica el número de Hola de tooobtain de ejemplos de muestras más recientes de Hola que se han recopilado.<br/><br/>`GetSample(1)`Devuelve la última muestra disponible de Hola. Para las métricas como `$CPUPercent`, sin embargo, esto no se recomienda porque es imposible tooknow *cuando* recopiló el ejemplo hello. Puede ser reciente o, debido a problemas del sistema, puede ser mucho más antiguo. Es mejor en tal toouse casos un intervalo de tiempo, tal y como se muestra a continuación.<li>`doubleVec GetSample((timestamp or timeinterval) startTime [, double samplePercent])`<br/>Especifica un período de tiempo para recopilar datos de muestra. Opcionalmente, especifica porcentaje Hola de ejemplos que deben estar disponibles en hello solicitó el período de tiempo.<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10)`devolvería 20 muestras si están presentes en el historial de hello CPUPercent todos los ejemplos de hello últimos 10 minutos. Sin embargo, si Hola último minuto de historial no estaba disponible, se devolvería sólo 18 ejemplos. En este caso:<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)`produciría un error porque solo el 90 por ciento de los ejemplos de hello están disponibles.<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)` se realizaría correctamente.<li>`doubleVec GetSample((timestamp or timeinterval) startTime, (timestamp or timeinterval) endTime [, double samplePercent])`<br/>Especifica un período de tiempo para recopilar datos, con una hora de inicio y una hora de finalización.<br/><br/>Como se mencionó anteriormente, hay un retraso entre cuando se recopila una muestra y cuándo es fórmula tooa disponible. Tenga en cuenta este retraso al usar hello `GetSample` método. Consulte `GetSamplePercent` a continuación. |
| GetSamplePeriod() |Devuelve el período de Hola de muestras que se realizaron en un conjunto de datos de ejemplo históricos. |
| Count() |Devuelve Hola número total de muestras en el historial de métricas de Hola. |
| HistoryBeginTime() |Devuelve Hola marca de tiempo de muestra de datos disponibles más antigua de Hola de métrica de Hola. |
| GetSamplePercent() |Devuelve Hola porcentaje de muestras que están disponibles para un intervalo de tiempo determinado. Por ejemplo:<br/><br/>`doubleVec GetSamplePercent( (timestamp or timeinterval) startTime [, (timestamp or timeinterval) endTime] )`<br/><br/>Porque hello `GetSample` método produce un error si el porcentaje de Hola de muestras que se devuelve es menor que hello `samplePercent` especificado, puede usar hello `GetSamplePercent` método toocheck primero. A continuación, puede realizar una acción alternativa si están presentes, suficientes muestras sin detener la evaluación de escala automática de Hola. |

### <a name="samples-sample-percentage-and-hello-getsample-method"></a>Hola, porcentaje de ejemplo y ejemplos de *GetSample()* (método)
funcionamiento básico de Hola de una fórmula de Autoescala es tooobtain datos métricos tareas y recursos y, a continuación, ajustar el tamaño de grupo basado en esos datos. Por lo tanto, es importante toohave una idea clara de cómo las fórmulas de Autoescala interactúan con datos de métricas (ejemplos).

**Ejemplos**

Hola servicio por lotes periódicamente toma muestras de métricas de tareas y recursos y hace que las fórmulas de Autoescala de tooyour disponible. Estos ejemplos se registran cada 30 segundos Hola servicio por lotes. Sin embargo, suele haber un retraso entre cuando se registraron esos ejemplos y cuando se ponen a disposición demasiado (y puede ser leídos por) las fórmulas de escalado automático. Además, debido a factores toovarious como red u otros problemas de infraestructura, ejemplos no se pueden grabar para un intervalo determinado.

**Porcentaje de muestras**

Cuando `samplePercent` se pasa toohello `GetSample()` método o hello `GetSamplePercent()` método se llama, _por ciento_ hace referencia tooa comparación entre el número total de posibles Hola de muestras que se registran en hello servicio por lotes y número de Hola de ejemplos de fórmula de Autoescala tooyour disponible.

Echemos un vistazo a un intervalo de tiempo de 10 minutos como ejemplo. Como ejemplos se registran cada 30 segundos dentro de un intervalo de tiempo de 10 minutos, número total máximo de Hola de muestras que se registran por lote sería 20 muestras (2 por minuto). Sin embargo, debido a toohello latencia inherente de hello reporting mecanismo y otros problemas dentro de Azure, puede haber solo 15 ejemplos de fórmula de Autoescala tooyour disponibles para su lectura. Por lo tanto, por ejemplo, durante ese período de 10 minutos, sólo el 75% del número total de Hola de muestras que se registran puede ser fórmula tooyour disponible.

**GetSample() e intervalos de muestra**

Las fórmulas de escalado automático son continuo toobe creciendo y reducir las agrupaciones de &mdash; agregar nodos o quitar nodos. Como nodos cuestan dinero, es conveniente tooensure que las fórmulas utilizan un método de análisis que se basa en datos suficientes inteligente. Por lo tanto, recomendamos que use un análisis de tipo tendencias en las fórmulas. Este tipo aumenta y reduce los grupos basándose en un intervalo de ejemplos recopilados.

por lo tanto, use toodo `GetSample(interval look-back start, interval look-back end)` tooreturn un vector de muestras:

```
$runningTasksSample = $RunningTasks.GetSample(1 * TimeInterval_Minute, 6 * TimeInterval_Minute);
```

Cuando se evalúa Hola por encima de la línea de proceso por lotes, devuelve un intervalo de muestras como un vector de valores. Por ejemplo:

```
$runningTasksSample=[1,1,1,1,1,1,1,1,1,1];
```

Una vez que haya recopilado vector Hola de muestras, a continuación, puede usar funciones como `min()`, `max()`, y `avg()` tooderive valores significativos de hello recopilan intervalo.

Para obtener seguridad adicional, puede forzar una toofail de evaluación de fórmulas si menor que un determinado porcentaje de ejemplo está disponible durante un período de tiempo determinado. Cuando se fuerza un toofail de evaluación de fórmulas, indicar toocease de lote más evaluación de la fórmula de hello si Hola especifica el porcentaje de muestras no está disponible. En este caso, el tamaño del grupo de toohello se realiza ningún cambio. toospecify un porcentaje de muestras para toosucceed de evaluación de hello, necesario especificarla como Hola tercer parámetro demasiado`GetSample()`. En este caso, se especifica un requisito del 75 por ciento de muestras:

```
$runningTasksSample = $RunningTasks.GetSample(60 * TimeInterval_Second, 120 * TimeInterval_Second, 75);
```

Dado que puede haber un retraso en la disponibilidad de ejemplo, es importante tooalways especifique un intervalo de tiempo con una hora de inicio de la devolución de la apariencia que es anterior a un minuto. Tarda aproximadamente un minuto para toopropagate ejemplos a través del sistema de hello, por lo que ejemplos en el intervalo de hello `(0 * TimeInterval_Second, 60 * TimeInterval_Second)` no estén disponibles. Nuevo, puede usar el parámetro de porcentaje de hello de `GetSample()` tooforce un requisito de porcentaje de ejemplo concreto.

> [!IMPORTANT]
> Es **muy recomendable** que **evite confiar *solo* en**  en las fórmulas de escalado automático`GetSample(1)`. Esto es porque `GetSample(1)` esencialmente dice servicio por lotes de toohello, "Dar me Hola última muestra tiene, no importa cuánto tiempo hace que recuperó." Dado que es solo una muestra única, y puede ser un ejemplo anterior, no puede ser representativos de imágenes más grandes de Hola de tareas recientes o estado del recurso. Si usa `GetSample(1)`, asegúrese de que es parte de una instrucción mayor y no Hola punto de datos que depende de la fórmula.
>
>

## <a name="metrics"></a>Métricas
Puede usar tanto métricas de recurso como de tarea al definir una fórmula. Ajustar el número de destino de Hola de dedicado nodos grupo de hello basado en datos de métricas de Hola que recibe y evaluar. Vea hello [Variables](#variables) sección anterior para obtener más información sobre cada métrica.

<table>
  <tr>
    <th>Métrica</th>
    <th>Descripción</th>
  </tr>
  <tr>
    <td><b>Recurso</b></td>
    <td><p>Métricas de recursos se basan en hello CPU, el ancho de banda de hello, el uso de memoria de Hola de nodos de proceso y Hola número de nodos.</p>
        <p> Estas variables definidas por el servicio se usan para realizar ajustes basados en el número de nodos:</p>
    <p><ul>
            <li>$TargetDedicatedNodes</li>
            <li>$TargetLowPriorityNodes</li>
            <li>$CurrentDedicatedNodes</li>
            <li>$CurrentLowPriorityNodes</li>
            <li>$preemptedNodeCount</li>
            <li>$SampleNodeCount</li>
    </ul></p>
    <p>Estas variables definidas por el servicio se usan para realizar ajustes basados en el uso de recursos de nodo:</p>
    <p><ul>
      <li>$CPUPercent</li>
      <li>$WallClockSeconds</li>
      <li>$MemoryBytes</li>
      <li>$DiskBytes</li>
      <li>$DiskReadBytes</li>
      <li>$DiskWriteBytes</li>
      <li>$DiskReadOps</li>
      <li>$DiskWriteOps</li>
      <li>$NetworkInBytes</li>
      <li>$NetworkOutBytes</li></ul></p>
  </tr>
  <tr>
    <td><b>Task</b></td>
    <td><p>Las métricas de la tarea se basan en estado de Hola de tareas, como por ejemplo activo, pendiente y completadas. Hello siguientes variables definidas por el servicio son útiles para realizar ajustes de tamaño del grupo según las métricas de tarea:</p>
    <p><ul>
      <li>$ActiveTasks</li>
      <li>$RunningTasks</li>
      <li>$PendingTasks</li>
      <li>$SucceededTasks</li>
            <li>$FailedTasks</li></ul></p>
        </td>
  </tr>
</table>

## <a name="write-an-autoscale-formula"></a>Escritura de una fórmula de escalado automático
Crear una fórmula de Autoescala que forman las instrucciones que utilizan Hola por encima de los componentes y luego combinar estas instrucciones en una fórmula completa. En esta sección vamos a crear una fórmula de escalado automático de ejemplo que puede tomar algunas decisiones reales de escalado.

En primer lugar, vamos a definir los requisitos de hello para la nueva fórmula de escalado automático. fórmula de Hello debe:

1. Aumentar el número de destino de Hola de nodos de cálculo específico en un grupo si el uso de CPU es alto.
2. Reduzca el número de destino de Hola de nodos de cálculo específico en un grupo cuando el uso de CPU es bajo.
3. Siempre restringir el número máximo de Hola de too400 nodos dedicado.

número de hello tooincrease de nodos durante el uso elevado de CPU, defina la instrucción de Hola que rellena una variable definida por el usuario (`$totalDedicatedNodes`) con un valor que es 110 por ciento del número de destino actual de Hola de nodos dedicados, pero solo si Hola mínimo uso medio de CPU últimos 10 minutos era por encima del 70 por ciento durante Hola. En caso contrario, utilice el valor de hello para el número actual de Hola de nodos dedicados.

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
```

demasiado*disminuir* Hola número de nodos dedicados durante el uso de CPU bajo, Hola Next en nuestro Hola conjuntos fórmulas mismo `$totalDedicatedNodes` por ciento de variable too90 del número de destino actual de Hola de nodos dedicados si hello promedio de uso de CPU Hola últimos 60 minutos en fue 20 por ciento. En caso contrario, usar el valor actual de Hola de `$totalDedicatedNodes` que se rellena en la instrucción de hello anterior.

```
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
```

Ahora limitar número de destino de Hola de máximo de tooa de nodos de proceso dedicado de 400:

```
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

Esta es la fórmula completa de hello:

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

## <a name="create-an-autoscale-enabled-pool-with-net"></a>Crear un grupo habilitado para el escalado automático con .NET

toocreate un grupo con Autoescala habilitada en. NET, siga estos pasos:

1. Crear grupo de hello con [BatchClient.PoolOperations.CreatePool](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.createpool).
2. Conjunto hello [CloudPool.AutoScaleEnabled](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleenabled) propiedad demasiado`true`.
3. Conjunto hello [CloudPool.AutoScaleFormula](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula) propiedad con la fórmula de Autoescala.
4. (Opcional) Conjunto hello [CloudPool.AutoScaleEvaluationInterval](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval) propiedad (el valor predeterminado es 15 minutos).
5. Confirmar el grupo de hello con [CloudPool.Commit](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commit) o [CommitAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commitasync).

Hello fragmento de código siguiente crea un grupo de escalado automático habilitado en. NET. Hello fórmula de Autoescala del grupo establece Hola destino número de nodos dedicado too5 lunes y 1 en todos los días de la semana de Hola. Hola [intervalo de ajuste de escala automático](#automatic-scaling-interval) es establecer too30 minutos. En esta y Hola otros fragmentos de código C# en este artículo, `myBatchClient` es una instancia inicializada correctamente de hello [BatchClient] [ net_batchclient] clase.

```csharp
CloudPool pool = myBatchClient.PoolOperations.CreatePool(
                    poolId: "mypool",
                    virtualMachineSize: "small", // single-core, 1.75 GB memory, 225 GB disk
                    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));    
pool.AutoScaleEnabled = true;
pool.AutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";
pool.AutoScaleEvaluationInterval = TimeSpan.FromMinutes(30);
await pool.CommitAsync();
```

> [!IMPORTANT]
> Cuando se crea un grupo de escalado automático habilitado, no especifique hello _targetDedicatedComputeNodes_ parámetro o hello _targetLowPriorityComputeNodes_ parámetro en hello llamada demasiado **CreatePool**. En su lugar, especifique hello **AutoScaleEnabled** y **AutoScaleFormula** propiedades de grupo de Hola. valores de Hello para estas propiedades determinan número de destino de Hola de cada tipo de nodo. Además, toomanually cambiar el tamaño de un grupo de escalado automático habilitado (por ejemplo, con [BatchClient.PoolOperations.ResizePoolAsync][net_poolops_resizepoolasync]), primero **deshabilitar** el escalado automático en Hola de grupo y, a continuación, cambiar su tamaño.
>
>

Además tooBatch. NET, puede usar cualquiera de hello otro [SDK de lote](batch-apis-tools.md#azure-accounts-for-batch-development), [REST de lote](https://docs.microsoft.com/rest/api/batchservice/), [cmdlets de PowerShell lote](batch-powershell-cmdlets-get-started.md), hello y [lote CLI](batch-cli-get-started.md)tooconfigure Autoescala.


### <a name="automatic-scaling-interval"></a>Intervalo de escalado automático
De forma predeterminada, Hola servicio por lotes ajusta el tamaño de la agrupación según la fórmula de Autoescala de tooits cada 15 minutos. Este intervalo es configurable mediante el uso de hello propiedades de grupo siguientes:

* [CloudPool.AutoScaleEvaluationInterval][net_cloudpool_autoscaleevalinterval] (.NET para Batch)
* [autoScaleEvaluationInterval][rest_autoscaleinterval] (API de REST)

intervalo mínimo de Hello es de cinco minutos y Hola máximo es 168 horas. Si se especifica un intervalo fuera de este intervalo, Hola servicio por lotes devuelve un error de solicitud incorrecta (400).

> [!NOTE]
> Escalado automático no está previsto actualmente toorespond toochanges en menos de un minuto, pero en su lugar es diseñado tooadjust tamaño de Hola de su grupo gradualmente como ejecutar una carga de trabajo.
>
>

## <a name="enable-autoscaling-on-an-existing-pool"></a>Habilitación del escalado automático en un grupo existente

Cada lote SDK proporciona una escala de tooenable de forma automática. Por ejemplo:

* [BatchClient.PoolOperations.EnableAutoScaleAsync][net_enableautoscaleasync] (Batch .NET)
* [Activar la escala automática en un grupo de servidores][rest_enableautoscale] (API de REST)

Cuando se habilita el escalado automático en un grupo existente, tenga en Hola de cuenta siguientes puntos:

* Si el escalado automático está deshabilitado actualmente en el grupo de Hola al emitir Hola solicitud tooenable Autoescala, debe especificar una fórmula de Autoescala válido cuando se emite la solicitud de saludo. También puede especificar un intervalo de evaluación de escalado automático. Si no especifica un intervalo, se utiliza el valor predeterminado de Hola de 15 minutos.
* Si el escalado automático está habilitada en el grupo de hello, puede especificar una fórmula de Autoescala, un intervalo de evaluación o ambos. Debe especificar al menos una de estas propiedades.

  * Si especifica un nuevo intervalo de evaluación de escalado automático, a continuación, se detiene la programación de evaluación de hello existente y se inicia una nueva programación. hora de inicio de la nueva programación de Hello es hora de Hola a qué Hola se emitió solicitud tooenable Autoescala.
  * Si se omite cualquier intervalo de fórmula o evaluación de escalado automático de hello, Hola servicio por lotes continúa valor actual de toouse Hola de dicha configuración.

> [!NOTE]
> Si especifica valores para hello *targetDedicatedComputeNodes* o *targetLowPriorityComputeNodes* parámetros de hello **CreatePool** método cuando creaste Hola bloque en. NET, o para los parámetros comparables de hello en otro idioma, a continuación, esos valores se omiten cuando se evalúa la fórmula de escala automática Hola.
>
>

Este fragmento de código de C# utiliza hello [.NET de lotes] [ net_api] biblioteca tooenable Autoescala en un grupo existente:

```csharp
// Define hello autoscaling formula. This formula sets hello target number of nodes
// too5 on Mondays, and 1 on every other day of hello week
string myAutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";

// Set hello autoscale formula on hello existing pool
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myAutoScaleFormula);
```

### <a name="update-an-autoscale-formula"></a>Actualización de una fórmula de escalado automático

fórmula de hello tooupdate en un grupo existente de escalado automático habilitado, llamada Hola operación tooenable Autoescala nuevo con la nueva fórmula de saludo. Por ejemplo, si ya está habilitado el escalado automático en `myexistingpool` cuando Hola siguiente código de .NET se ejecuta, su fórmula de Autoescala se reemplaza con contenido de Hola de `myNewFormula`.

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myNewFormula);
```

### <a name="update-hello-autoscale-interval"></a>Intervalo de actualización Hola escalado automático

tooupdate el intervalo de evaluación de escalado automático de saludo de un grupo existente de escalado automático habilitado, llamada Hola operación tooenable Autoescala nuevo con el nuevo intervalo de saludo. Por ejemplo, tooset Hola escalado automático evaluación intervalo too60 minutos para un grupo que ya está habilitada para el escalado automático en. NET:

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleEvaluationInterval: TimeSpan.FromMinutes(60));
```

## <a name="evaluate-an-autoscale-formula"></a>Evaluación de una fórmula de escalado automático

Puede evaluar una fórmula antes de aplicarla tooa grupo. De esta manera, puede probar hello toosee fórmulas cómo sus instrucciones evaluación antes de poner fórmula hello en producción.

tooevaluate una fórmula de Autoescala, primero debe habilitar la escala automática en el grupo de hello con una fórmula válida. tootest una fórmula en un grupo que no tiene todavía escalado automático habilitado, utilice Hola una línea fórmula `$TargetDedicatedNodes = 0` cuando se habilita escalado automático. A continuación, use uno de hello después de la fórmula de hello tooevaluate desea tootest:

* [BatchClient.PoolOperations.EvaluateAutoScale](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscale) o [EvaluateAutoScaleAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscaleasync)

    Estos métodos de .NET de lotes requieren Id. de Hola de un grupo existente y una cadena que contiene tooevaluate de fórmula de escalado automático de Hola.

* [Evaluación de una fórmula de escalado automático](https://docs.microsoft.com/rest/api/batchservice/evaluate-an-automatic-scaling-formula)

    En esta solicitud de API de REST, especifique el Id. de grupo de Hola Hola URI y Hola fórmula de Autoescala en hello *autoScaleFormula* elemento Hola del cuerpo de solicitud. respuesta de Hola de operación de hello contiene cualquier información de error que podría ser fórmula toohello relacionados.

En este fragmento de código de [Batch .NET][net_api] se evalúa una fórmula de escalado automático. Si el grupo de hello no tiene Autoescala habilitada, hemos habilitar primero.

```csharp
// First obtain a reference tooan existing pool
CloudPool pool = await batchClient.PoolOperations.GetPoolAsync("myExistingPool");

// If autoscaling isn't already enabled on hello pool, enable it.
// You can't evaluate an autoscale formula on non-autoscale-enabled pool.
if (pool.AutoScaleEnabled == false)
{
    // We need a valid autoscale formula tooenable autoscaling on the
    // pool. This formula is valid, but won't resize hello pool:
    await pool.EnableAutoScaleAsync(
        autoscaleFormula: "$TargetDedicatedNodes = {pool.CurrentDedicatedNodes};",
        autoscaleEvaluationInterval: TimeSpan.FromMinutes(5));

    // Batch limits EnableAutoScaleAsync calls tooonce every 30 seconds.
    // Because we want tooapply our new autoscale formula below if it
    // evaluates successfully, and we *just* enabled autoscaling on
    // this pool, we pause here tooensure we pass that threshold.
    Thread.Sleep(TimeSpan.FromSeconds(31));

    // Refresh hello properties of hello pool so that we've got the
    // latest value for AutoScaleEnabled
    await pool.RefreshAsync();
}

// We must ensure that autoscaling is enabled on hello pool prior to
// evaluating a formula
if (pool.AutoScaleEnabled == true)
{
    // hello formula tooevaluate - adjusts target number of nodes based on
    // day of week and time of day
    string myFormula = @"
        $curTime = time();
        $workHours = $curTime.hour >= 8 && $curTime.hour < 18;
        $isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
        $isWorkingWeekdayHour = $workHours && $isWeekday;
        $TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
    ";

    // Perform hello autoscale formula evaluation. Note that this code does not
    // actually apply hello formula toohello pool.
    AutoScaleRun eval =
        await batchClient.PoolOperations.EvaluateAutoScaleAsync(pool.Id, myFormula);

    if (eval.Error == null)
    {
        // Evaluation success - print hello results of hello AutoScaleRun.
        // This will display hello values of each variable as evaluated by the
        // autoscale formula.
        Console.WriteLine("AutoScaleRun.Results: " +
            eval.Results.Replace("$", "\n    $"));

        // Apply hello formula toohello pool since it evaluated successfully
        await batchClient.PoolOperations.EnableAutoScaleAsync(pool.Id, myFormula);
    }
    else
    {
        // Evaluation failed, output hello message associated with hello error
        Console.WriteLine("AutoScaleRun.Error.Message: " +
            eval.Error.Message);
    }
}
```

Evaluación correcta de la fórmula de saludo que se muestra en este fragmento de código produce resultados similares a:

```
AutoScaleRun.Results:
    $TargetDedicatedNodes=10;
    $NodeDeallocationOption=requeue;
    $curTime=2016-10-13T19:18:47.805Z;
    $isWeekday=1;
    $isWorkingWeekdayHour=0;
    $workHours=0
```

## <a name="get-information-about-autoscale-runs"></a>Obtención de información sobre la ejecución del escalado automático

tooensure que está realizando la fórmula como se esperaba, se recomienda que compruebe periódicamente los resultados de Hola de ejecuciones de escalado automático de Hola que lleva a cabo en el grupo de lote. toodo por lo tanto, get (o actualizar) un toohello de referencia de grupo y examinar las propiedades de Hola de su última ejecución de escalado automático.

En .NET de lote, Hola [CloudPool.AutoScaleRun](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscalerun) propiedad tiene varias propiedades que proporcionan información sobre hello más reciente el escalado automático ejecutarlo realizadas en el grupo de hello:

* [AutoScaleRun.Timestamp](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.timestamp)
* [AutoScaleRun.Results](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.results)
* [AutoScaleRun.Error](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.error)

Hola API de REST, Hola [obtener información acerca de un grupo](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool) solicitud devuelve información sobre el grupo de hello, que incluye hello más reciente el escalado automático ejecuten información en hello [autoScaleRun](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool#bk_autrun) propiedad.

Hello siguiente fragmento de código de C# utiliza la Hola .NET de lote biblioteca tooprint información acerca Hola los ejecutarlo en grupo de escalado automático última _myPool_:

```csharp
await Cloud pool = myBatchClient.PoolOperations.GetPoolAsync("myPool");
Console.WriteLine("Last execution: " + pool.AutoScaleRun.Timestamp);
Console.WriteLine("Result:" + pool.AutoScaleRun.Results.Replace("$", "\n  $"));
Console.WriteLine("Error: " + pool.AutoScaleRun.Error);
```

Resultados del ejemplo de Hola anterior fragmento de código:

```
Last execution: 10/14/2016 18:36:43
Result:
  $TargetDedicatedNodes=10;
  $NodeDeallocationOption=requeue;
  $curTime=2016-10-14T18:36:43.282Z;
  $isWeekday=1;
  $isWorkingWeekdayHour=0;
  $workHours=0
Error:
```

## <a name="example-autoscale-formulas"></a>Ejemplo de fórmulas de escalado automático
Echemos un vistazo a algunas fórmulas que muestran la cantidad de hello tooadjust de maneras diferentes de los recursos de proceso en un grupo.

### <a name="example-1-time-based-adjustment"></a>Ejemplo 1: Ajuste basado en la fecha y hora
Imagine que desea el tamaño del grupo de hello tooadjust según Hola día de semana de Hola y la hora del día. Este ejemplo muestra cómo tooincrease o disminuir el número de Hola de nodos de hello grupo según corresponda.

fórmula de Hello obtiene primero Hola hora actual. Si es un día de la semana (1-5) y dentro del horario laboral (8 A.M. too6 PM), tamaño del grupo de destino de Hola se establece too20 nodos. En caso contrario, estableció too10 nodos.

```
$curTime = time();
$workHours = $curTime.hour >= 8 && $curTime.hour < 18;
$isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
$isWorkingWeekdayHour = $workHours && $isWeekday;
$TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
```

### <a name="example-2-task-based-adjustment"></a>Ejemplo 2: Ajuste basado en tareas
En este ejemplo, el tamaño del grupo de Hola se ajusta según Hola número de tareas en cola Hola. Las cadenas de la fórmula aceptan tanto comentarios como saltos de línea.

```csharp
// Get pending tasks for hello past 15 minutes.
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
// If we have fewer than 70 percent data points, we use hello last sample point,
// otherwise we use hello maximum of last sample point and hello history average.
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1), avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// If number of pending tasks is not 0, set targetVM toopending tasks, otherwise
// half of current dedicated.
$targetVMs = $tasks > 0? $tasks:max(0, $TargetDedicatedNodes/2);
// hello pool size is capped at 20, if target VM value is more than that, set it
// too20. This value should be adjusted according tooyour use case.
$TargetDedicatedNodes = max(0, min($targetVMs, 20));
// Set node deallocation mode - keep nodes active only until tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-3-accounting-for-parallel-tasks"></a>Ejemplo 3: Contabilidad para tareas paralelas
Este ejemplo ajusta el tamaño de bloque de hello según el número de Hola de tareas. Esta fórmula también se toma en hello cuenta [MaxTasksPerComputeNode] [ net_maxtasks] valor que se ha establecido para el grupo de Hola. Este enfoque es útil en aquellas situaciones en las que la [ejecución de tareas paralelas](batch-parallel-node-tasks.md) se ha habilitado en el grupo.

```csharp
// Determine whether 70 percent of hello samples have been recorded in hello past
// 15 minutes; if not, use last sample
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1),avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// Set hello number of nodes tooadd tooone-fourth hello number of active tasks (the
// MaxTasksPerComputeNode property on this pool is set too4, adjust this number
// for your use case)
$cores = $TargetDedicatedNodes * 4;
$extraVMs = (($tasks - $cores) + 3) / 4;
$targetVMs = ($TargetDedicatedNodes + $extraVMs);
// Attempt toogrow hello number of compute nodes toomatch hello number of active
// tasks, with a maximum of 3
$TargetDedicatedNodes = max(0,min($targetVMs,3));
// Keep hello nodes active until hello tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-4-setting-an-initial-pool-size"></a>Ejemplo 4: Configuración de un tamaño de grupo inicial
En este ejemplo de fragmento de código con una fórmula de Autoescala que establece el código C# se muestra hello tooa de tamaño de bloque especificado número de nodos para un período de tiempo inicial. A continuación, ajusta el tamaño del grupo de hello según el número de saludo de la ejecución y tareas activas después de hello inicial del período de tiempo ha transcurrido.

fórmula de Hola Hola siguiente fragmento de código:

* Establece un grupo inicial de hello nodos toofour de tamaño.
* No se ajustar el tamaño de bloque de hello dentro de hello primeros 10 minutos del ciclo de vida del grupo de Hola.
* Después de 10 minutos, obtiene el valor máximo de Hola Hola active y del número de la ejecución de tareas dentro de Hola últimos 60 minutos.
  * Si ambos valores son 0 (lo que indica que no hay ninguna tarea eran active Hola o en ejecución últimos 60 minutos), el tamaño del grupo de Hola se establece too0.
  * Si cualquier valor es mayor que cero, no hay cambios.

```csharp
string now = DateTime.UtcNow.ToString("r");
string formula = string.Format(@"
    $TargetDedicatedNodes = {1};
    lifespan         = time() - time(""{0}"");
    span             = TimeInterval_Minute * 60;
    startup          = TimeInterval_Minute * 10;
    ratio            = 50;

    $TargetDedicatedNodes = (lifespan > startup ? (max($RunningTasks.GetSample(span, ratio), $ActiveTasks.GetSample(span, ratio)) == 0 ? 0 : $TargetDedicatedNodes) : {1});
    ", now, 4);
```

## <a name="next-steps"></a>Pasos siguientes
* [Maximizar el uso de recursos de proceso por lotes de Azure con las tareas de nodo simultáneos](batch-parallel-node-tasks.md) contiene los detalles sobre cómo puede ejecutar varias tareas simultáneamente en nodos de proceso de hello en el grupo. Además tooautoscaling, esta característica puede ayudar toolower duración del trabajo para algunas cargas de trabajo, lo que ahorra dinero.
* Para otro ajuste de eficacia, asegúrese de que las consultas de la aplicación de lote Hola servicio por lotes en hello mayoría de forma óptima. Vea [consultar el servicio de Azure Batch Hola eficazmente](batch-efficient-list-queries.md) toolearn cómo toolimit Hola cantidad de datos que atraviesan el cable Hola al consultar el estado de Hola de potencialmente miles de proceso nodos o tareas.

[net_api]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch
[net_batchclient]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.batchclient
[net_cloudpool_autoscaleformula]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula
[net_cloudpool_autoscaleevalinterval]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval
[net_enableautoscaleasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.enableautoscaleasync
[net_maxtasks]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.maxtaskspercomputenode
[net_poolops_resizepoolasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.resizepoolasync

[rest_api]: https://docs.microsoft.com/rest/api/batchservice/
[rest_autoscaleformula]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_autoscaleinterval]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_enableautoscale]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
