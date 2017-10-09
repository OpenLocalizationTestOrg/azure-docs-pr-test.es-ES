---
title: aaaOverview de captura de los centros de eventos de Azure | Documentos de Microsoft
description: "Captura de datos de telemetría con Event Hubs Capture"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: sethm;darosa
ms.openlocfilehash: 0238cae712a0ed7bdf3e87ee93a069a553cb65df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-event-hubs-capture"></a>Azure Event Hubs Capture

Captura de los centros de eventos Azure permite tooautomatically entregar Hola transmisión de datos en los centros de eventos tooan [almacenamiento de blobs de Azure](https://azure.microsoft.com/services/storage/blobs/) o [almacén de Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) cuenta de su elección, con hello flexibilidad adicional especificar un intervalo de tiempo o tamaño. Configuración de captura es rápido, no hay ningún toorun los costos administrativos y se escala automáticamente con los concentradores de eventos [unidades de rendimiento](event-hubs-features.md#capacity). Captura de los centros de eventos es tooload Hola de manera más fácil la transmisión de datos en Azure y permite toofocus en procesamiento de datos en lugar de en la captura de datos.

Captura de los centros de eventos permite tooprocess en tiempo real y canalizaciones basadas en lotes en Hola mismo flujo. lo que permite crear soluciones que crecen a la par que sus necesidades. Si va a compilar sistemas basados en lote hoy en día con un ojo para procesarlas en tiempo real en el futuro, o si desea tooadd una solución de en tiempo real de ruta de acceso frío eficaz tooan existente, captura de los centros de eventos hace que trabajar con la transmisión de datos.

## <a name="how-event-hubs-capture-works"></a>Cómo funciona Event Hubs Capture

Los concentradores de eventos es un búfer duradero de tiempo de retención para la entrada de telemetría, registro distribuida tooa similar. Hola tooscaling clave en los centros de eventos es hello [modelo de consumidor con particiones](event-hubs-features.md#partitions). Cada partición es un segmento de datos independiente y se consume de forma independiente. Con el tiempo que estos datos quede anticuado desactivado, según el período de retención configurable de Hola. Como consecuencia, un centro de eventos determinado nunca llega a estar "demasiado lleno".

Captura de los centros de eventos permite toospecify su propia cuenta de almacenamiento Blob de Azure y el contenedor o la cuenta de almacén de Data Lake de Azure, que son utilizados toostore Hola capturar datos. Estas cuentas pueden estar en hello misma región como el centro de eventos o en otra región, agregar toohello flexibilidad de la característica de captura de los centros de eventos de Hola.

Los datos capturados se escriben en el formato de [Apache Avro][Apache Avro], que es un formato compacto, rápido y binario que proporciona estructuras de datos enriquecidos con un esquema insertado. Este formato se usa ampliamente en el ecosistema de Hadoop de Hola y análisis de transmisiones, Data Factory de Azure. En este mismo artículo encontrará más información acerca de cómo trabajar con Avro.

### <a name="capture-windowing"></a>Ventanas de captura

Captura de los centros de eventos permite tooset de una captura de toocontrol de ventana. Esta ventana es un tamaño mínimo y la configuración del tiempo con una "primera wins directivas", lo que significa que Hola causas de primer desencadenador que se encontró una operación de captura. Si dispone de hasta quince minutos, 100 MB ventana Captura y enviar 1 MB por segundo, desencadenadores de ventana de hello tamaño antes de la ventana de tiempo de Hola. Cada partición captura de forma independiente y escribe un blob en bloques completado en tiempo de Hola de captura, con el nombre de la hora de hello en qué Hola se encontró el intervalo de captura. convención de nomenclatura de almacenamiento de Hello es como sigue:

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a>Unidades de escala del toothroughput

El tráfico de los Event Hubs lo controlan las [unidades de procesamiento](event-hubs-features.md#capacity). Una sola unidad de procesamiento permite una entrada de 1 MB/s o 1000 eventos por segundo y una salida que duplica esas cifras. Standard Event Hubs se puede configurar con entre 1 y 20 unidades de procesamiento, y puede adquirir más a través de una solicitud de aumento de cuota al [equipo de soporte técnico][support request]. El uso por encima de las unidades de procesamiento adquiridas está limitado. Captura de los centros de eventos copia los datos directamente desde el almacenamiento de los concentradores de eventos interno de Hola, omitiendo las cuotas de salida de unidad de rendimiento y guardar la salida para otros lectores de procesamiento, como análisis de transmisiones o Spark.

Una vez configurado, Event Hubs Capture se ejecuta automáticamente cuando se envía el primer evento y continúa ejecutándose. toomake resulta más sencillo para su tooknow de procesamiento en dirección descendente que está trabajando el proceso de hello, centros de eventos escribe archivos vacíos cuando no hay ningún dato. Este proceso proporciona un marcador y una cadencia predecibles que puede alimentar sus procesadores de lotes.

## <a name="setting-up-event-hubs-capture"></a>Configuración de Event Hubs Capture

Puede configurar la captura en tiempo de creación de base de datos central Hola eventos con hello [portal de Azure](https://portal.azure.com), o usando plantillas del Administrador de recursos de Azure. Para obtener más información, vea Hola siguientes artículos:

- [Habilitar la captura de los centros de eventos mediante Hola portal de Azure](event-hubs-capture-enable-through-portal.md)
- [Creación de un espacio de nombres de Event Hubs con un centro de eventos y habilitación de la característica Capture mediante una plantilla de Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a>Explorar archivos Hola capturado y trabajar con Avro

Captura de los centros de eventos crea archivos en el formato Avro, tal como se especifica en la ventana de tiempo de hello configurado. Dichos archivos se pueden ver en cualquier herramienta, como el [Explorador de Azure Storage][Azure Storage Explorer]. Puede descargar Hola localmente archivos toowork en ellos.

archivos de Hello generados por captura de los centros de eventos tienen Hola después de un esquema de Avro:

![][3]

Un archivo de Avro tooexplore de manera sencilla consiste en usar hello [Avro herramientas] [ Avro Tools] jar de Apache. Después de descargar este jar, puede ver el esquema Hola de un determinado archivo Avro ejecutando el siguiente comando de hello:

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

Este comando devuelve

```
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

También puede utilizar herramientas de Avro tooconvert Hola archivo tooJSON formato y realizar otras tareas de procesamiento.

tooperform más avanzada de procesamiento, descargue e instalación Avro para su elección de plataforma. En hello el momento de redactar este artículo, hay implementaciones disponibles para C, C++, C\#, Java, NodeJS, Perl, PHP, Python y Ruby.

Apache Avro tiene guías de introducción para [Java][Java] y [Python][Python] muy completas. También puede leer hello [introducción con la captura de los centros de eventos](event-hubs-capture-python.md) artículo.

## <a name="how-event-hubs-capture-is-charged"></a>Cómo se factura Event Hubs Capture

Se mide la captura de los centros de eventos del mismo modo toothroughput unidades: como un cargo por hora. cargo de Hello es directamente proporcional toohello número de unidades de rendimiento adquiridas para el espacio de nombres de Hola. Como las unidades de rendimiento se incrementado y reducidas, metros de captura de los centros de eventos aumentar y disminuir tooprovide coincidencia de rendimiento. metros Hola se producen conjuntamente. Para conocer los precios detallados, consulte [Precios de Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/). 

## <a name="next-steps"></a>Pasos siguientes

Captura de los centros de eventos es datos de tooget de manera más fáciles de hello en Azure. Con Azure Data Lake, Azure Data Factory y Azure HDInsight, se puede realizar el procesamiento por lotes y cualquier otro análisis mediante las plataformas y herramientas conocidas a la escala que necesite.

Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:

* [Get started sending and receiving events (Introducción al envío y la recepción de eventos)](event-hubs-dotnet-framework-getstarted-send.md)
* Una [aplicación de ejemplo completa que usa Event Hubs][sample application that uses Event Hubs]
* [Información general de Event Hubs][Event Hubs overview]

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
