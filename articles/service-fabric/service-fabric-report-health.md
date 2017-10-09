---
title: informes de estado de Service Fabric personalizados aaaAdd | Documentos de Microsoft
description: "Describe cómo informa toosend personalizada del estado de entidades de mantenimiento de tooAzure Service Fabric. Proporciona recomendaciones para diseñar e implementar informes de estado de calidad."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 0a00a7d2-510e-47d0-8aa8-24c851ea847f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 12c9f664e2a457b4e1e8f340873ca60ebcefb097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-service-fabric-health-reports"></a>Incorporación de informes de mantenimiento de Service Fabric personalizados
Azure Service Fabric presenta un [modelo de estado](service-fabric-health-introduction.md) diseñado tooflag clúster en mal estado y las condiciones de aplicación en entidades concretas. usa el modelo de estado de Hello **Informadores mantenimiento** (componentes del sistema y watchdogs). objetivo de Hello es fácil y rápido un diagnóstico más detallado y reparación. Escritores del servicio necesitan toothink por adelantado sobre el estado. Cualquier condición que puede afectar el estado debería aparecer en, sobre todo si puede ayudar a problemas de marca cerrar toohello raíz. información de estado de Hello puede ahorrar tiempo y esfuerzo de la depuración y la investigación. Hello utilidad es especialmente claro una vez que el servicio Hola está en funcionamiento a escala en la nube de hello (privada o Azure).

monitor de Informadores de Service Fabric Hola identifica las condiciones de interés. Informan sobre esas condiciones en función de su vista local. Hola [almacén de estado](service-fabric-health-introduction.md#health-store) agrega datos de estado enviados por todos los toodetermine Informadores si las entidades son globalmente correcto. modelo de Hello es toouse enriquecido, flexible y fácil de toobe previsto. calidad de Hola de informes de estado de hello determina la precisión de Hola de vista de estado de Hola de clúster de Hola. Los falsos positivos que muestran erróneamente problemas pueden afectar negativamente a las actualizaciones u otros servicios que usan datos de mantenimiento. Ejemplos de estos servicios son los servicios de reparación y los mecanismos de alerta. Por lo tanto, algunas consideraciones es informes tooprovide necesarios que capturan las condiciones de interés en hello mejor manera posible.

deben toodesign e implementar componentes de informes, watchdogs y sistema de estado:

* Definir condición de Hola que le interesa, hello y modo de saludo que se está supervisando impacto en la funcionalidad de clúster o una aplicación Hola. En función de esta información, decidir Hola estado de mantenimiento informe propiedad y el estado.
* Determinar hello [entidad](service-fabric-health-introduction.md#health-entities-and-hierarchy) que informe de Hola se aplica a.
* Determinar donde se realiza el reporting hello, desde Hola guardián de servicio o desde una interno o externo.
* Definir un indicador de origen usa tooidentify Hola.
* Elegir una estrategia de generación de informes, periódicamente o en las transiciones. Hola recomienda forma periódicamente, tal y como requiere código más sencillo y menos propenso tooerrors.
* Determinar cuánto informe Hola para condiciones de mal estadas deben permanecer en el almacén de estado de Hola y cómo debe borrarse. Con esta información, decida el comportamiento de toolive y remove de expiración de tiempo del informe de Hola.

Tal y como se ha mencionado, la creación de informes puede realizarse desde:

* Hola supervisa réplicas del servicio de Service Fabric.
* Guardianes internos implementados como un servicio de Service Fabric (por ejemplo, un servicio sin estado de Service Fabric que supervisa las condiciones y los informes de problemas). pueden ser watchdogs Hola implementa un todos los nodos o puede ser servicio de afinidad toohello supervisado.
* Watchdogs internos que se ejecutan en nodos de Service Fabric Hola pero son *no* implementados como servicios de Service Fabric.
* Externo watchdogs ese recurso Hola de sondeo de *fuera* clúster de Service Fabric hello (por ejemplo, servicio de supervisión como Gomez).

> [!NOTE]
> Desde el principio de hello, clúster de Hola se rellena con informes de estado enviados por componentes del sistema Hola. Lea más en [Uso de informes de mantenimiento del sistema para solucionar problemas](service-fabric-understand-and-troubleshoot-with-system-health-reports.md). Hello informes de usuario deben enviarse en [entidades de mantenimiento](service-fabric-health-introduction.md#health-entities-and-hierarchy) que ya se han creado por el sistema de Hola.
> 
> 

Una vez hello diseño informes de estado está desactivada, se pueden enviar fácilmente informes de mantenimiento. Puede usar [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) tooreport estado si el clúster hello no está [segura](service-fabric-cluster-security.md) o si los clientes de fabric hello tiene privilegios de administrador. Reporting puede realizarse a través de hello API por mediante [FabricClient.HealthManager.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth), a través de PowerShell o a través de REST. Los botones de configuración procesan los informes por lotes para un mejor rendimiento.

> [!NOTE]
> Informe de mantenimiento es sincrónico y representa solo Hola trabajo de validación en el lado del cliente de Hola. hecho de que los informes de Hola Hola se acepta una por el cliente de mantenimiento de Hola o hello `Partition` o `CodePackageActivationContext` objetos no significa que se aplica en el almacén de Hola. Se envía de forma asincrónica y posiblemente por lotes con otros informes. Hola está procesando en el servidor de hello todavía puede producir un error: número de secuencia de hello podría ser obsoleto, entidad hello en qué Hola debe aplicarse el informe se ha eliminado, etcetera.
> 
> 

## <a name="health-client"></a>Cliente de mantenimiento
se envían informes de estado de Hello toohello de almacén de estado a través de un cliente de mantenimiento, que se encuentra dentro de los clientes de fabric de Hola. cliente de mantenimiento de Hello puede configurarse con hello después de la configuración:

* **HealthReportSendInterval**: retraso de hello entre informe Hola Hola es agregado toohello tiempo de hello y cliente que se envíe el almacén de estado de toohello. Informes de toobatch usado en un único mensaje, en lugar de enviar un mensaje para cada informe. Hola, procesamiento por lotes mejora el rendimiento. Valor predeterminado: 30 segundos.
* **HealthReportRetrySendInterval**: intervalo de saludo en qué Hola cliente de mantenimiento, vuelve a enviar estado acumulado informa de almacén de estado de toohello. Valor predeterminado: 30 segundos.
* **HealthOperationTimeout**: tiempo de espera de Hola para un mensaje de informe enviado toohello almacén de estado. Si un mensaje de tiempo de espera, cliente de mantenimiento de hello lo reintenta hasta que el almacén de estado de hello confirma que se ha procesado el informe de Hola. Valor predeterminado: dos minutos.

> [!NOTE]
> Cuando se procesan por lotes informes Hola, cliente de tejido de hello debe se mantenga para al menos Hola tooensure HealthReportSendInterval que se envían. Si se pierde el mensaje de Hola o almacén de estado de hello no puede aplicar debido a errores de tootransient, clientes de fabric Hola deben mantenerse activo toogive más un tooretry de oportunidad.
> 
> 

Hola de almacenamiento en búfer en el cliente de hello toma unicidad Hola de informes de hello en consideración. Por ejemplo, si un determinado indicador incorrecto está informando de 100 informes por segundo en hello misma propiedad de hello misma entidad, Hola informes se reemplazan con la última versión de Hola. A lo sumo una dicho informe existe en la cola del cliente Hola. Si se configura el procesamiento por lotes, número Hola de informes envía toohello almacén de estado es simplemente una por intervalo de envío. Este informe es Hola último agregado, que reflejan el estado más reciente de Hola de entidad de Hola.
Especificar parámetros de configuración cuando `FabricClient` se crea pasando [FabricClientSettings](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclientsettings) con hello los valores deseados para las entradas relacionadas con el mantenimiento.

Hello en el ejemplo siguiente se crea a un cliente de tejido y especifica que se deberían enviar informes de hello cuando se agregan. En tiempos de espera y errores que se pueden reintentar, los reintentos se producen cada 40 segundos.

```csharp
var clientSettings = new FabricClientSettings()
{
    HealthOperationTimeout = TimeSpan.FromSeconds(120),
    HealthReportSendInterval = TimeSpan.FromSeconds(0),
    HealthReportRetrySendInterval = TimeSpan.FromSeconds(40),
};
var fabricClient = new FabricClient(clientSettings);
```

Se recomienda mantener el tejido de Hola de forma predeterminada la configuración de cliente, que establece `HealthReportSendInterval` too30 segundos. Esta configuración garantiza un rendimiento óptimo toobatching due. Para los informes importantes que se deban enviar tan pronto como sea posible, utilice `HealthReportSendOptions` con la marca Immediate establecida en `true` en la API [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth). Informes inmediatos omiten Hola intervalo de procesamiento por lotes. Utilice este indicador con cuidado; queremos tootake ventaja del cliente de mantenimiento de hello procesamiento por lotes siempre que sea posible. Envío inmediato también es útil cuando se está cerrando el cliente de tejido de hello (por ejemplo, el proceso de hello ha determinado el estado no válido y debe tooshut hacia abajo de los efectos secundarios de tooprevent). Garantiza un envío de mejor esfuerzo de informes de hello acumulado. Cuando se agrega un informe con la marca de inmediato, cliente de mantenimiento de hello lotes de todos los informes de hello acumulado desde el último envío.

Parámetros de la mismas pueden especificarse cuando se crea un clúster de tooa de conexión a través de PowerShell. Hola ejemplo siguiente inicia un clúster local de tooa de conexión:

```powershell
PS C:\> Connect-ServiceFabricCluster -HealthOperationTimeoutInSec 120 -HealthReportSendIntervalInSec 0 -HealthReportRetrySendIntervalInSec 40
True

ConnectionEndpoint   :
FabricClientSettings : {
                       ClientFriendlyName                   : PowerShell-1944858a-4c6d-465f-89c7-9021c12ac0bb
                       PartitionLocationCacheLimit          : 100000
                       PartitionLocationCacheBucketCount    : 1024
                       ServiceChangePollInterval            : 00:02:00
                       ConnectionInitializationTimeout      : 00:00:02
                       KeepAliveInterval                    : 00:00:20
                       HealthOperationTimeout               : 00:02:00
                       HealthReportSendInterval             : 00:00:00
                       HealthReportRetrySendInterval        : 00:00:40
                       NotificationGatewayConnectionTimeout : 00:00:00
                       NotificationCacheUpdateTimeout       : 00:00:00
                       }
GatewayInformation   : {
                       NodeAddress                          : localhost:19000
                       NodeId                               : 1880ec88a3187766a6da323399721f53
                       NodeInstanceId                       : 130729063464981219
                       NodeName                             : Node.1
                       }
```

De igual forma tooAPI, los informes pueden enviarse mediante `-Immediate` cambiar toobe enviado inmediatamente, sin tener en cuenta hello `HealthReportSendInterval` valor.

Para REST, Hola informes se envían toohello Service Fabric puerta de enlace, que tiene un cliente de fabric interno. De forma predeterminada, este cliente está informes toosend configurado por lotes cada 30 segundos. Puede cambiar el intervalo de lote de saludo con la opción de configuración de clúster de hello `HttpGatewayHealthReportSendInterval` en `HttpGateway`. Como se mencionó, la mejor opción es toosend Hola informes con `Immediate` es true. 

> [!NOTE]
> tooensure que los servicios desautorizados no podrá informar de mantenimiento con las entidades de hello en clúster de hello, configurar las solicitudes de hello server tooaccept solo desde clientes protegidos. Hola `FabricClient` emplea para la notificación debe haber seguridad habilitado toobe toocommunicate pueda con clúster de hello (por ejemplo, con la autenticación Kerberos o certificados). Obtenga más información sobre la [seguridad del clúster](service-fabric-cluster-security.md).
> 
> 

## <a name="report-from-within-low-privilege-services"></a>Informes desde servicios con pocos privilegios
Si Servicios de Service Fabric no tiene clústeres de toohello de acceso de administrador, puede crear informes de mantenimiento en entidades de contexto actual de Hola a través de `Partition` o `CodePackageActivationContext`.

* Para los servicios sin estado, use [IStatelessServicePartition.ReportInstanceHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatelessservicepartition.reportinstancehealth) tooreport en la instancia de servicio actual de Hola.
* Para los servicios con estado, use [IStatefulServicePartition.ReportReplicaHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition.reportreplicahealth) tooreport en la réplica actual.
* Use [IServicePartition.ReportPartitionHealth](https://docs.microsoft.com/dotnet/api/system.fabric.iservicepartition.reportpartitionhealth) tooreport en la entidad de partición actual de Hola.
* Use [CodePackageActivationContext.ReportApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportapplicationhealth) tooreport en la aplicación actual.
* Use [CodePackageActivationContext.ReportDeployedApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedapplicationhealth) tooreport en la aplicación actual Hola implementada en el nodo actual de Hola.
* Use [CodePackageActivationContext.ReportDeployedServicePackageHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedservicepackagehealth) tooreport en un paquete de servicios de aplicación Hola implementada en el nodo actual de Hola.

> [!NOTE]
> Internamente, Hola `Partition` hello y `CodePackageActivationContext` mantenga un cliente de mantenimiento configurado con la configuración predeterminada. Como se explica para hello [cliente mantenimiento](service-fabric-report-health.md#health-client), los informes son por lotes y se envía un temporizador. Hola objetos deben ser mantiene activo toohave un informe de hello toosend de oportunidad.
> 
> 

Puede especificar `HealthReportSendOptions` al enviar informes a través de las API de mantenimiento `Partition` y `CodePackageActivationContext`. Si tiene informes importantes que deben enviarse tan pronto como sea posible, use `HealthReportSendOptions` con la marca Inmediate establecida en `true`. Informes inmediatos omiten Hola intervalo de cliente de estado interno de Hola de procesamiento por lotes. Como se mencionó antes, utilice este indicador con cuidado; queremos tootake ventaja del cliente de mantenimiento de hello procesamiento por lotes siempre que sea posible.

## <a name="design-health-reporting"></a>Informes de estado del diseño
Hello primer paso para generar informes de alta calidad es identificar condiciones de Hola que pueden afectar Hola estado del servicio de Hola. Las condiciones que pueden ayudar a problemas de marca de servicio de Hola o clúster cuando se inicia, o incluso mejor, antes de que ocurra un problema, puede guardar miles de millones de dólares. ventajas de Hello incluyen menor tiempo de inactividad, menos horas de noche dedicado a investigar y solucionar problemas y mayor satisfacción del cliente.

Una vez que se identifican las condiciones de hello, escritores de guardián deben toofigure out toomonitor Hola de manera recomendada para equilibrar la carga y utilidad. Por ejemplo, considere un servicio que realiza cálculos complejos mediante el uso de algunos archivos temporales en un recurso compartido. A continuación se proporciona puede supervisar tooensure de recurso compartido de Hola que hay suficiente espacio. Podría escuchar las notificaciones de cambios en un archivo o un directorio. Podría presentar una advertencia si se alcanza un umbral por adelantado y notifica un error si el recurso compartido de hello está lleno. Una advertencia, pudo iniciar un sistema de reparación limpiar archivos más antiguos en el recurso compartido de Hola. Produce un error, un sistema de reparación podría mover nodo de hello servicio réplica tooanother. Tenga en cuenta cómo se describen los Estados de la condición de hello en términos de mantenimiento: Hola estado de hello condición que se puede considerar correcto (correcto) o mal estado (advertencia o error).

Una vez que se establecen los detalles de supervisión de hello, un sistema de escritura de guardián debe toofigure out cómo tooimplement Hola guardián. Si las condiciones de Hola se pueden determinar desde dentro de servicio de hello, guardián Hola puede formar parte del propio servicio de hello supervisado de. Por ejemplo, el código del servicio de hello puede comprobar el uso del recurso compartido de Hola y de informes, a continuación, cada vez que intente toowrite un archivo. ventaja de Hola de este enfoque es que reporting es sencilla. Se deben tener cuidado tooprevent errores de guardián no afecten a la funcionalidad del servicio Hola.

Generación de informes en el servicio de hello supervisado no siempre es una opción. A continuación se proporciona en el servicio de hello puede no ser capaz de toodetect condiciones de Hola. No puede tener determinación de Hola de toomake de datos o lógicas Hola. sobrecarga de Hola de supervisan las condiciones de hello puede ser alto. condiciones de Hello también pueden no ser servicio tooa específico, pero en su lugar, afectan a las interacciones entre los servicios. Otra opción es toohave watchdogs en clúster de hello como procesos independientes. watchdogs Hola supervisan las condiciones de Hola y el informe, sin que afecte a los servicios principales de Hola de ninguna manera. Por ejemplo, pudieron implementarse estos watchdogs como servicios sin estado en hello misma aplicación, implementada en todos los nodos u Hola mismos nodos como servicio de Hola.

En ocasiones, un guardián que se ejecuta en el clúster de Hola tampoco es una opción. Si condición Hola supervisado es disponibilidad Hola o la funcionalidad del servicio de Hola que los usuarios verán, es mejor watchdogs de hello toohave Hola mismo lugar como clientes de usuario de Hola. No existe, puede probar el funcionamiento de Hola Hola misma forma, los usuarios llamarlos. Por ejemplo, puede tener un guardián que reside fuera de clúster de hello, emite las solicitudes de servicio de toohello y comprueba la latencia de Hola y la exactitud de los resultados de Hola. (Para un servicio de calculadora, por ejemplo, ¿2 + 2 devuelve 4 en un período de tiempo razonable?)

Una vez que los detalles de guardián Hola aún haya finalizado, debería decidir un Id. de origen que identifica de forma única. Si varios watchdogs del programa Hola a mismo tipo vivan en hello clúster, debe informar sobre entidades distintas, o, si le informan de Hola misma entidad, Id. de origen diferente de uso o propiedad. De este modo, los informes podrán coexistir. propiedad Hola de informe de mantenimiento de hello debe reflejar condición Hola supervisado. (Por ejemplo de Hola anterior, podría ser propiedad de hello **ShareSize**.) Si varios informes aplican toohello mismo condición, hello propiedad debe contener información dinámica que permite toocoexist de informes. Por ejemplo, si varios recursos compartidos de necesitan toobe supervisado, nombre de la propiedad de hello puede ser **ShareSize sharename**.

> [!NOTE]
> Hacer *no* usar Hola almacén tookeep información de estado. Solo la información relacionada con el mantenimiento debe notificarse como estado, como esta evaluación de mantenimiento de Hola de impactos de información de una entidad. almacén de estado de Hello no se diseñó como un almacén de propósito general. Utiliza tooaggregate de lógica de evaluación de estado todos los datos en estado de mantenimiento de Hola. Envío de información de toohealth no relacionada (como informes de estado con un estado de mantenimiento de Aceptar) no afecta a Hola agrega el estado, pero puede afectar negativamente al rendimiento de Hola de almacén de estado de Hola.
> 
> 

Hola siguiente punto de decisión es que tooreport de entidad en. La mayoría de casos de hello, condición Hola claramente idetifies Hola entidad. Elija la entidad de hello con mejor granularidad posible. Si una condición afecta a todas las réplicas de una partición, un informe sobre la partición de hello, no en el servicio de Hola. Hay casos excepcionales en los que es necesario dedicar más esfuerzo. Si la condición de hello afecta a una entidad, como una réplica, pero Hola deseo es toohave Hola condición marcado durante más de duración de hello del ciclo de vida de la réplica, a continuación, que se debe notificar en partición de Hola. En caso contrario, cuando se elimina la réplica de hello, almacén de estado de hello limpia todos sus informes. Escritores de guardián deben pensar en duraciones de Hola de entidad de Hola y Hola del informe. Debe quedar claro cuándo se debe limpiar un informe de un almacén (por ejemplo, cuándo deja de aplicarse un error notificado en una entidad).

Veamos un ejemplo que reúne describen los puntos de Hola. Considere una aplicación de Service Fabric compuesta de un servicio persistente con estado maestro y varios servicios sin estado secundario implementados en todos los nodos (un tipo de servicio secundario para cada tipo de tarea). maestro de Hello tiene una cola de procesamiento que contiene toobe de comandos ejecutada por elementos secundarios. elementos secundarios de Hola ejecutan hello las solicitudes entrantes y envían señales de espera de confirmación. Una condición que se va a supervisar es la longitud de Hola de cola de procesamiento maestro Hola. Si la longitud de la cola principal de hello alcanza un umbral, se emite una advertencia. Advertencia de Hello indica que secundarias hello no pueden atender la carga de Hola. Si la cola de hello alcanza la longitud máxima de Hola y se quitan los comandos, se notifica un error, como hello no se puede recuperar el servicio. informes Hello pueden ser una propiedad de hello **QueueStatus**. guardián Hola reside dentro de servicio de hello, y se envía de forma periódica en la réplica principal de hello maestro. Hola tiempo toolive es dos minutos, y que se envíe periódicamente cada 30 segundos. Si Hola principal deja de funcionar, informe de Hola se limpia automáticamente de almacén. Si la réplica de servicio de hello está activo, pero se producirá un interbloqueo o tiene otros problemas, Hola informe expira en el almacén de estado de Hola. En este caso, la entidad de Hola se evalúa en error.

Otra condición que se pueden supervisar es el tiempo de ejecución de las tareas. Hello master distribuye las tareas secundarias toohello basándose en el tipo de tarea de Hola. Según el diseño de hello, master Hola pudo sondear secundarias de hello para el estado de la tarea. También puede esperar a que señales de espera de confirmación de toosend secundarias cuando hayan terminado. En el segundo caso hello, se deben tener cuidado situaciones toodetect donde se pierdan mensajes o dado de elementos secundarios. Una opción es para hello maestro toosend un toohello de solicitud de ping mismo secundaria, que vuelve a enviar su estado. Si no se recibe ningún estado, master Hola considera que un error y reprograma la tarea hello. Este comportamiento se da por supuesto que las tareas de hello son idempotentes.

se puede traducir condición Hola supervisado como una advertencia si no se realiza la tarea hello en un momento determinado (**t1**, por ejemplo, 10 minutos). Si no se realiza una tarea hello en el tiempo (**t2**, por ejemplo, 20 minutos), se puede traducir condición Hola supervisado como Error. Estos informes pueden realizarse de varias maneras:

* réplica principal de Hello maestro informa periódicamente por sí sola. Puede tener una propiedad para todas las tareas pendientes en cola Hola. Si al menos una tarea tarda más tiempo, Hola informar sobre el estado propiedad hello **PendingTasks** es una advertencia o error, según corresponda. Si no hay ninguna tarea pendiente o todas las tareas inició la ejecución, informar del estado de hello es correcto. tareas de Hello son persistentes. Si Hola principal deja de funcionar, principal Hola recién promovido puede continuar tooreport correctamente.
* Otro proceso de guardián (en la nube de Hola o externa) comprueba las tareas de hello (desde fuera, basado en resultados de la tarea de hello deseado) toosee si se completan. Si no respetan los umbrales de Hola, se envía un informe en el servicio maestro Hola. También se envía un informe en cada tarea que incluye el identificador de la tarea de hello, como **PendingTask + taskId**. Los informes solo se deben enviar con estados incorrectos. Establecer tiempo toolive tooa unos minutos y marcar Hola informes toobe quitado cuando expiran tooensure limpieza.
* Hola secundaria que se está ejecutando una tarea notifica si se tarda más tiempo que toorun esperado lo. Informa sobre la instancia de servicio de hello en la propiedad de hello **PendingTasks**. informe de Hello localiza la instancia de servicio de Hola que tiene problemas, pero no captura el situación Hola donde muere instancia Hola. informes de Hola se limpian, a continuación. Puede generar informes sobre el servicio secundario Hola. Si Hola secundaria complete la tarea de hello, instancia secundaria Hola borra informe Hola de almacén de Hola. informe de Hola no captura la situación de Hola donde se pierde el mensaje de confirmación de Hola y Hola tarea no se terminó de punto de vista del patrón de Hola.

Sin embargo, la notificación de Hola se realiza en los casos de Hola que se ha descrito anteriormente, se capturan Hola informes de estado de la aplicación cuando se evalúa el estado.

## <a name="report-periodically-vs-on-transition"></a>Informar periódicamente frente a en transiciones
Mediante el uso de informes de modelo de estado de hello, watchdogs puede enviar informes periódicamente o transiciones. Hola recomienda manera de guardián reporting es periódicamente, dado que el código de hello es mucho más sencillo y menos propenso tooerrors. watchdogs Hola deben procurar toobe tan simple como tooavoid posibles errores que desencadenan informes incorrectos. Los informes de *mal estado* incorrectos afectarán a los escenarios y las evaluaciones de mantenimiento en función del estado, como las actualizaciones. Incorrecta *correcto* informes ocultar los problemas de clúster de hello, que no se desea.

Para informes periódicos, guardián Hola puede implementarse con un temporizador. En una devolución de llamada de temporizador guardián de Hola puede comprobar el estado de Hola y enviar un informe basado en el estado actual de Hola. No hay ningún toosee necesidad qué informes se envió anteriormente o realizar las optimizaciones en términos de mensajería. cliente de mantenimiento de Hello tiene toohelp lógica con un rendimiento de procesamiento por lotes. Mientras el cliente de mantenimiento de Hola se mantiene activo, vuelve a intentar internamente hasta que informe de Hola se reconoce por el almacén de estado de Hola o guardián Hola genera un informe más reciente con hello misma entidad, property y origen.

Los informes en las transiciones requieren un tratamiento especial del estado. guardián Hola supervisa algunas condiciones y emite solo cuando cambien las condiciones de Hola. Hola al revés de este enfoque es que no se necesitan menos informes. inconveniente de Hello es que la lógica de Hola de guardián de hello es compleja. guardián Hola debe mantener las condiciones de Hola o informes de hello, para que puedan ser inspeccionado toodetermine cambios de estado. En la conmutación por error, debe tener cuidado con los informes de agregado, pero aún no se ha enviado toohello almacén de estado. número de secuencia de Hello debe ser creciente. De lo contrario, se rechazan los informes de hello como obsoleto. En casos excepcionales de Hola donde se incurre en pérdida de datos, puede resultar necesario sincronización entre el estado de Hola de indicador de Hola y estado de hello del almacén de estado de Hola.

La creación de informes sobre las transiciones tiene sentido para los servicios que crean informes sobre sí mismos, mediante `Partition` o `CodePackageActivationContext`. Hola al objeto local (réplica o un paquete de servicio implementado / implementado aplicación) es eliminado, se quitan también todas sus informes. La limpieza automática reduce la necesidad de hello para la sincronización entre el indicador y el almacén de estado. Si informe de hello es para la partición primaria o la aplicación principal, se debe tener cuidado en conmutación por error tooavoid obsoletos informes del almacén de estado de Hola. Lógica debe agregarse un estado correcto toomaintain Hola y el informe de hello clara del almacén cuando ya no sea necesario.

## <a name="implement-health-reporting"></a>Implementación de la generación de informes de estado
Una vez hello detalles de la entidad y el informe no están activados, enviar informes de estado puede realizarse a través de la API de hello, PowerShell o REST.

### <a name="api"></a>API
tooreport a través de la API de hello, necesita un tipo de entidad toohello específico de informe de mantenimiento desean tooreport en toocreate. Asigne a Hola informe tooa mantenimiento cliente. O bien, cree una información de estado y páselo toocorrect métodos de generación de informes en `Partition` o `CodePackageActivationContext` tooreport en entidades actuales.

Hello en el ejemplo siguiente se muestra periódico de informes desde un guardián en clúster de Hola. guardián Hola comprueba si un recurso externo puede tener acceso desde dentro de un nodo. recursos de Hola se necesita un manifiesto de servicio dentro de la aplicación hello. Si no está disponible el recurso de hello, hello otros servicios dentro de la aplicación hello pueden funcionar correctamente. Por lo tanto, el informe de Hola se envía en la entidad de paquete de servicio de hello implementado cada 30 segundos.

```csharp
private static Uri ApplicationName = new Uri("fabric:/WordCount");
private static string ServiceManifestName = "WordCount.Service";
private static string NodeName = FabricRuntime.GetNodeContext().NodeName;
private static Timer ReportTimer = new Timer(new TimerCallback(SendReport), null, 30 * 1000, 30 * 1000);
private static FabricClient Client = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });

public static void SendReport(object obj)
{
    // Test whether hello resource can be accessed from hello node
    HealthState healthState = this.TestConnectivityToExternalResource();

    // Send report on deployed service package, as hello connectivity is needed by hello specific service manifest
    // and can be different on different nodes
    var deployedServicePackageHealthReport = new DeployedServicePackageHealthReport(
        ApplicationName,
        ServiceManifestName,
        NodeName,
        new HealthInformation("ExternalSourceWatcher", "Connectivity", healthState));

    // TODO: handle exception. Code omitted for snippet brevity.
    // Possible exceptions: FabricException with error codes
    // FabricHealthStaleReport (non-retryable, hello report is already queued on hello health client),
    // FabricHealthMaxReportsReached (retryable; user should retry with exponential delay until hello report is accepted).
    Client.HealthManager.ReportHealth(deployedServicePackageHealthReport);
}
```

### <a name="powershell"></a>PowerShell
Envíe informes de mantenimiento con **Send-ServiceFabric*EntityType*HealthReport**.

Hello en el ejemplo siguiente se muestra periódico de creación de informes sobre los valores de la CPU en un nodo. se enviarán informes de Hello cada 30 segundos, y tienen un tiempo toolive de dos minutos. Si caducan, Informador de hello tiene problemas, por lo que se evalúa el nodo de hello en error. Cuando Hola CPU está por encima de un umbral, informe de hello tiene un estado de advertencia. Cuando Hola CPU se mantiene por encima de un umbral durante más tiempo Hola configurado, se notificará como un error. En caso contrario, el indicador de hello envía un estado de mantenimiento de Aceptar.

```powershell
PS C:\> Send-ServiceFabricNodeHealthReport -NodeName Node.1 -HealthState Warning -SourceId PowershellWatcher -HealthProperty CPU -Description "CPU is above 80% threshold" -TimeToLiveSec 120

PS C:\> Get-ServiceFabricNodeHealth -NodeName Node.1
NodeName              : Node.1
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='CPU', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 5
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : CPU
                        HealthState           : Warning
                        SequenceNumber        : 130741236814913394
                        SentAt                : 4/21/2015 9:01:21 PM
                        ReceivedAt            : 4/21/2015 9:01:21 PM
                        TTL                   : 00:02:00
                        Description           : CPU is above 80% threshold
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:01:21 PM
```

Hello en el ejemplo siguiente se notifica una advertencia transitoria en una réplica. Primero obtiene el Id. de partición de Hola y Hola, a continuación, Id. de réplica para servicio de Hola que le interesan. A continuación, envía un informe de **PowershellWatcher** en la propiedad de hello **ResourceDependency**. informe de Hello es de interés para solo dos minutos, y se quita del almacén de hello automáticamente.

```powershell
PS C:\> $partitionId = (Get-ServiceFabricPartition -ServiceName fabric:/WordCount/WordCount.Service).PartitionId

PS C:\> $replicaId = (Get-ServiceFabricReplica -PartitionId $partitionId | where {$_.ReplicaRole -eq "Primary"}).ReplicaId

PS C:\> Send-ServiceFabricReplicaHealthReport -PartitionId $partitionId -ReplicaId $replicaId -HealthState Warning -SourceId PowershellWatcher -HealthProperty ResourceDependency -Description "hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes." -TimeToLiveSec 120 -RemoveWhenExpired

PS C:\> Get-ServiceFabricReplicaHealth  -PartitionId $partitionId -ReplicaOrInstanceId $replicaId


PartitionId           : 8f82daff-eb68-4fd9-b631-7a37629e08c0
ReplicaId             : 130740415594605869
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='ResourceDependency', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130740768777734943
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : ResourceDependency
                        HealthState           : Warning
                        SequenceNumber        : 130741243777723555
                        SentAt                : 4/21/2015 9:12:57 PM
                        ReceivedAt            : 4/21/2015 9:12:57 PM
                        TTL                   : 00:02:00
                        Description           : hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:12:32 PM
```

### <a name="rest"></a>REST
Enviar informes de mantenimiento con REST con las solicitudes POST que vaya entidad toohello deseado y tienen en la descripción del informe de estado de hello cuerpo Hola. Por ejemplo, ver cómo se REST toosend [informes de mantenimiento del clúster](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-cluster) o [informes de mantenimiento del servicio](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service). Se admiten todas las entidades.

## <a name="next-steps"></a>Pasos siguientes
En función de los datos de estado de hello, escritores del servicio y los administradores de aplicación/clúster pueden considerar información de maneras tooconsume Hola. Por ejemplo, puede configurar alertas basadas en toocatch graves problemas de estado de mantenimiento antes de que provocan que las interrupciones. Los administradores también pueden establecer automáticamente problemas de toofix de sistemas de reparación de la instalación.

[Introducción tooService estado del tejido supervisión](service-fabric-health-introduction.md)

[Vista de los informes de estado de Service Fabric](service-fabric-view-entities-aggregated-health.md)

[¿Cómo tooreport y comprobación de estado de servicio](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Uso de informes de mantenimiento del sistema para solucionar problemas](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Supervisión y diagnóstico de los servicios localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Actualización de la aplicación de Service Fabric](service-fabric-application-upgrade.md)

