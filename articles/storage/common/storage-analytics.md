---
title: "aaaUse toocollect registros y métricas de datos de análisis de almacenamiento de Azure | Documentos de Microsoft"
description: "Análisis de almacenamiento le permite tootrack los datos de las métricas para todos los servicios de almacenamiento y toocollect se registra para el almacenamiento de Blob, cola y tabla."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7894993b-ca42-4125-8f17-8f6dfe3dca76
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: aba1a236cb69fa2e60bcb8fda5d34841e36e379a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storage-analytics"></a>Storage Analytics

El análisis de almacenamiento de Azure realiza el registro y proporciona datos de métricas para una cuenta de almacenamiento. Puede utilizar este solicitudes de tootrace de datos, analizar las tendencias de uso y diagnosticar problemas con su cuenta de almacenamiento.

toouse análisis de almacenamiento, debe habilitarla individualmente para cada servicio que desee toomonitor. Puede habilitarlo desde hello [Portal de Azure](https://portal.azure.com). Para obtener más información, consulte [supervisar una cuenta de almacenamiento en el Portal de Azure hello](storage-monitor-storage-account.md). También puede habilitar el análisis de almacenamiento mediante programación a través de la API de REST de Hola o biblioteca de cliente de Hola. Hola de uso [obtener propiedades del servicio Blob](https://msdn.microsoft.com/library/hh452239.aspx), [obtener propiedades del servicio cola](https://msdn.microsoft.com/library/hh452243.aspx), [obtener propiedades del servicio tabla](https://msdn.microsoft.com/library/hh452238.aspx), y [obtener propiedades del servicio archivo](https://msdn.microsoft.com/library/mt427369.aspx) operations tooenable análisis de almacenamiento para cada servicio.

Hello datos agregados se almacenan en un blob conocido (para el registro) y en tablas conocidas (para las métricas), que pueden tener acceso mediante el servicio de Blob de Hola y API del servicio tabla.

Análisis de almacenamiento tiene un límite de 20 TB en la cantidad de Hola de datos almacenados, que son independientes del límite total de hello para la cuenta de almacenamiento. Para obtener más información sobre las directivas de facturación y retención de datos, consulte [Facturación del análisis de almacenamiento](https://msdn.microsoft.com/library/hh360997.aspx). Para obtener más información sobre los límites de las cuentas de almacenamiento, consulte [Objetivos de escalabilidad y rendimiento del almacenamiento de Azure](storage-scalability-targets.md).

Para obtener una guía detallada sobre el uso de análisis de almacenamiento y otra herramientas tooidentify, diagnosticar y solucionar problemas relacionados con el almacenamiento de Azure, vea [supervisar, diagnosticar y solucionar problemas de almacenamiento de Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="about-storage-analytics-logging"></a>Acerca del registro del análisis de almacenamiento
Análisis de almacenamiento registra información detallada acerca del servicio de almacenamiento de tooa de solicitudes correctas e incorrectas. Esta información puede ser problemas de toodiagnose con un servicio de almacenamiento y las solicitudes individuales de toomonitor usado. Las solicitudes se registran en función de la mejor opción.

Solo se crean entradas del registro si hay actividad del servicio de almacenamiento. Por ejemplo, si una cuenta de almacenamiento tiene actividad en el servicio Blob pero no en sus servicios de tabla o cola, se creará solo los registros que pertenezcan toohello servicio Blob.

El registro del análisis de cuentas no está disponible para Azure File Storage.

### <a name="logging-authenticated-requests"></a>Registrar solicitudes de autenticación
se registra los siguientes tipos de solicitudes autenticadas de Hello:

* Solicitudes correctas
* Solicitudes erróneas, incluyendo errores de tiempo de espera, de limitación, de red, de autorización, etc
* Solicitudes que utilizan una firma de acceso compartido (SAS), incluyendo las solicitudes correctas y las erróneas
* Datos de tooanalytics de solicitudes.

Las solicitudes realizadas por el propio análisis de almacenamiento, como la creación o eliminación del registro, no se registran. Una lista completa de los datos registrado de saludo se documenta en hello [operaciones de registro de análisis de almacenamiento y mensajes de estado](https://msdn.microsoft.com/library/hh343260.aspx) y [formato de registro de análisis de almacenamiento](https://msdn.microsoft.com/library/hh343259.aspx) temas.

### <a name="logging-anonymous-requests"></a>Registrar solicitudes anónimas
se registra los siguientes tipos de solicitudes anónimas de Hello:

* Solicitudes correctas
* Errores del servidor
* Errores de tiempo de espera para el cliente y el servidor
* Solicitudes GET erróneas con el código de error 304 (Sin modificar)

El resto de solicitudes anónimas erróneas no se registran. Una lista completa de los datos registrado de saludo se documenta en hello [operaciones de registro de análisis de almacenamiento y mensajes de estado](https://msdn.microsoft.com/library/hh343260.aspx) y [formato de registro de análisis de almacenamiento](https://msdn.microsoft.com/library/hh343259.aspx) temas.

### <a name="how-logs-are-stored"></a>Cómo se almacenan los registros
Todos los registros se almacenan en blobs en bloques en un contenedor denominado $logs, que se crea automáticamente cuando se habilita el análisis de almacenamiento para una cuenta de almacenamiento. contenedor de Hello $logs se encuentra en espacio de nombres de blob de Hola de cuenta de almacenamiento de hello, por ejemplo: `http://<accountname>.blob.core.windows.net/$logs`. Este contenedor no se puede eliminar una vez habilitado el análisis de almacenamiento, aunque su contenido sí se puede eliminar.

> [!NOTE]
> contenedor de Hello $logs no se muestra cuando se realizan una operación de lista de contenedores, como hello [ListContainers](https://msdn.microsoft.com/library/azure/dd179352.aspx) método. Se debe tener acceso a él directamente. Por ejemplo, puede usar hello [ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx) blobs método tooaccess Hola Hola `$logs` contenedor.
> A medida que se registran las solicitudes, el análisis de almacenamiento cargará los resultados intermedios como bloques. Periódicamente, el análisis de almacenamiento confirmará estos bloques para que estén disponibles como blobs.
> 
> 

Registros duplicados existan registros creados en hello misma hora. Puede determinar si un registro es un duplicado comprobando hello **RequestId** y **operación** número.

### <a name="log-naming-conventions"></a>Convenciones de nomenclatura de los registros
Cada registro se escribirá en hello siguiendo el formato.

    <service-name>/YYYY/MM/DD/hhmm/<counter>.log

Hello siguiente tabla describe cada atributo de nombre de registro de hello.

| Atributo | Description |
| --- | --- |
| <service-name> |nombre de Hello del servicio de almacenamiento de Hola. Por ejemplo: blob, tabla o cola |
| AAAA |año de cuatro dígitos de Hello para el registro de hello. Por ejemplo: 2011 |
| MM |mes de dos dígitos de Hello para el registro de hello. Por ejemplo: 07. |
| DD |mes de dos dígitos de Hello para el registro de hello. Por ejemplo: 07. |
| hh |hora de dos dígitos de Hola que indica Hola a partir de la hora de hello inicia sesión, en formato de 24 horas UTC. Por ejemplo: 18. |
| MM |número de dos dígitos de Hola que indica Hola a partir de minuto para los registros de Hola. Este valor no se admite en la versión actual de hello del análisis de almacenamiento y su valor siempre será 00. |
| <counter> |Un contador con seis dígitos de base cero que indica el número de Hola de blobs de registro generado para el servicio de almacenamiento de hello en un período de tiempo de hora. Este contador se inicia en 000000. Por ejemplo: 000001. |

Hola es un nombre de registro de ejemplo completo que combina los ejemplos anteriores de Hola.

    blob/2011/07/31/1800/000001.log

Hola aquí te mostramos un URI que puede ser el registro anterior de tooaccess usado Hola de ejemplo.

    https://<accountname>.blob.core.windows.net/$logs/blob/2011/07/31/1800/000001.log

Cuando se registra una solicitud de almacenamiento, el nombre del registro de hello resultante correlaciona hora toohello cuando Hola solicitó la operación se completó. Por ejemplo, si una solicitud GetBlob se completó a las 6:30 P.M. 31/7/2011, registro de hello se escribirá con hello después de prefijo:`blob/2011/07/31/1800/`

### <a name="log-metadata"></a>Metadatos del registro
Todos los blobs del registro se almacenan con metadatos que pueden ser utilizado tooidentify contiene el blob de Hola de datos de registro. Hello en la tabla siguiente describe cada atributo de metadatos.

| Atributo | Description |
| --- | --- |
| LogType |Describe si el registro de hello contiene información relacionada tooread, escritura o las operaciones de eliminación. Este valor puede incluir un tipo o una combinación de los tres, separados por comas. Ejemplo 1: escritura; Ejemplo 2: lectura, escritura; Ejemplo 3: lectura, escritura, eliminación. |
| StartTime |Hola a primera hora de una entrada de registro de hello, expresada en forma de Hola de aaaa-MM-ddTHH. Por ejemplo: 2011-07-31T18:21:46Z. |
| EndTime |Hola a última hora de una entrada de registro de hello, expresada en forma de Hola de aaaa-MM-ddTHH. Por ejemplo: 2011-07-31T18:22:09Z. |
| LogVersion |versión de Hola del formato de registro de hello. Actualmente el valor de hello solo admitido es 1.0. |

Hello lista siguiente muestra metadatos completos de ejemplo con los ejemplos anteriores de Hola.

* LogType=escritura
* StartTime=2011-07-31T18:21:46Z
* EndTime=2011-07-31T18:22:09Z
* LogVersion=1.0

### <a name="accessing-logging-data"></a>Obtener acceso a los datos de registro
Todos los datos de hello `$logs` contenedor son accesibles mediante el uso de API del servicio de Blob de hello, incluidas las API de .NET proporcionadas por Hola Hola biblioteca de administrada de Azure. Administrador de cuenta de almacenamiento de Hello puede leer y eliminar registros, pero no se puede crear o actualizarlos. Los metadatos del registro de hello y nombre del registro pueden utilizarse al consultar un registro. Es posible que tooappear de registros de una hora determinada en el orden correcto, pero Hola metadatos siempre especifican Hola timespan de entradas de registro en un registro. Por consiguiente, se puede utilizar una combinación de nombres y metadatos de registro al buscar un registro concreto.

## <a name="about-storage-analytics-metrics"></a>Acerca de las métricas del análisis de almacenamiento
Análisis de almacenamiento puede almacenar métricas que incluyen datos de estadísticas y la capacidad de transacciones agregados acerca del servicio de almacenamiento de tooa de solicitudes. Las transacciones se notifican en nivel de operación Hola API, así como a nivel de servicio de almacenamiento de Hola y capacidad se notifica en el nivel de servicio de almacenamiento de Hola. Datos de métricas que pueden ser utilizados tooanalyze uso de servicios de almacenamiento, diagnosticar problemas con las solicitudes realizadas en el servicio de almacenamiento de Hola y el rendimiento de hello tooimprove de las aplicaciones que utilizan un servicio.

toouse análisis de almacenamiento, debe habilitarla individualmente para cada servicio que desee toomonitor. Puede habilitarlo desde hello [Portal de Azure](https://portal.azure.com). Para obtener más información, consulte [supervisar una cuenta de almacenamiento en el Portal de Azure hello](storage-monitor-storage-account.md). También puede habilitar el análisis de almacenamiento mediante programación a través de la API de REST de Hola o biblioteca de cliente de Hola. Hola de uso **obtener propiedades del servicio** operaciones tooenable análisis de almacenamiento para cada servicio.

### <a name="transaction-metrics"></a>Métricas de transacciones
Se registra un conjunto sólido de datos a intervalos de cada hora o de cada minuto para cada servicio de almacenamiento y operación de API que se ha solicitado, incluidos entradas/salidas, disponibilidad, errores y porcentajes de solicitudes por categorías. Puede ver una lista completa de los detalles de la transacción de Hola Hola [esquema de tabla de métricas de análisis de almacenamiento](https://msdn.microsoft.com/library/hh343264.aspx) tema.

Los datos de transacciones se registran en dos niveles: nivel de servicio de Hola y el nivel de operación de API de Hola. En el nivel de servicio de hello, las estadísticas de todas las resumen solicitan operaciones API que se escriben tooa tabla entidad cada hora incluso si no hay solicitudes realizadas toohello servicio. En el nivel de la operación de API de hello, las estadísticas son entidad tooan escrito solo si se solicitó la operación de Hola durante esa hora.

Por ejemplo, si realiza una **GetBlob** operación en el servicio de Blob, las métricas del análisis de almacenamiento se registrar las solicitudes de hello e incluirla en hello agregado datos para ambos Hola servicio de Blob, así como hello **GetBlob** operación. Sin embargo, si no hay ningún **GetBlob** se solicitó la operación durante la hora de hello, una entidad no se escribirán toohello `$MetricsTransactionsBlob` para esa operación.

Las métricas de transacciones se registran para las solicitudes del usuario y para las solicitudes realizadas por el análisis de almacenamiento. Por ejemplo, se registran las solicitudes realizadas por los registros de análisis de almacenamiento toowrite y entidades de tabla. Para obtener más información sobre cómo se facturan estas solicitudes, consulte [Facturación y análisis de almacenamiento](https://msdn.microsoft.com/library/hh360997.aspx).

### <a name="capacity-metrics"></a>Métricas de capacidad
> [!NOTE]
> Actualmente, las métricas de capacidad solo están disponibles para hello servicio Blob. Las métricas de capacidad de servicio de la tabla de Hola y el servicio cola estarán disponibles en versiones futuras del análisis de almacenamiento.
> 
> 

Los datos de capacidad se registran diariamente para la instancia de Blob service de una cuenta de almacenamiento, y se escriben dos entidades de tabla. Una entidad proporciona estadísticas para los datos de usuario y Hola otro proporciona estadísticas sobre hello `$logs` contenedor de blob utilizado por el análisis de almacenamiento. Hola `$MetricsCapacityBlob` tabla incluye Hola siguientes estadísticas:

* **Capacidad**: cantidad de Hola de almacenamiento utilizado por el servicio de Blob de la cuenta de almacenamiento de hello, en bytes.
* **ContainerCount**: Hola número de contenedores de blob en el servicio de Blob de la cuenta de almacenamiento de Hola.
* **ObjectCount**: Hola número de blobs de bloque o en páginas confirmados y sin confirmar en el servicio de Blob de la cuenta de almacenamiento de Hola.

Para obtener más información acerca de las métricas de capacidad de hello, consulte [esquema de tabla de métricas de análisis de almacenamiento](https://msdn.microsoft.com/library/hh343264.aspx).

### <a name="how-metrics-are-stored"></a>Cómo se almacenan las métricas
Todos los datos de las métricas para cada uno de los servicios de almacenamiento de Hola se almacenan en tres tablas reservadas para ese servicio: una tabla para obtener información de la transacción, una tabla para obtener información de transacción minuto y otra tabla para obtener información de capacidad. La información sobre transacciones y transacciones por minuto consta de datos de solicitudes y respuestas, y la información sobre capacidad consta de datos de uso del almacenamiento. Pueden tener acceso a las métricas por hora, métricas por minuto y capacidad de servicio de Blob de una cuenta de almacenamiento en tablas que se denominan como se describe en hello en la tabla siguiente.

| Nivel de métricas | Nombres de tabla | Versiones compatibles |
| --- | --- | --- |
| Métricas por horas, ubicación principal |$MetricsTransactionsBlob  <br/>$MetricsTransactionsTable <br/> $MetricsTransactionsQueue |Las versiones anteriores too2013-08-15 solamente. Aunque todavía se admiten estos nombres, se recomienda cambiar tablas de hello toousing enumeradas a continuación. |
| Métricas por horas, ubicación principal |$MetricsHourPrimaryTransactionsBlob <br/>$MetricsHourPrimaryTransactionsTable <br/>$MetricsHourPrimaryTransactionsQueue |Todas las versiones, incluida 2013-08-15. |
| Métricas por minutos, ubicación principal |$MetricsMinutePrimaryTransactionsBlob <br/>$MetricsMinutePrimaryTransactionsTable <br/>$MetricsMinutePrimaryTransactionsQueue |Todas las versiones, incluida 2013-08-15. |
| Métricas por horas, ubicación secundaria |$MetricsHourSecondaryTransactionsBlob  <br/>$MetricsHourSecondaryTransactionsTable <br/>$MetricsHourSecondaryTransactionsQueue |Todas las versiones, incluida 2013-08-15. Debe estar habilitada la replicación con redundancia geográfica con acceso de lectura. |
| Métricas por minutos, ubicación secundaria |$MetricsMinuteSecondaryTransactionsBlob  <br/>$MetricsMinuteSecondaryTransactionsTable <br/>$MetricsMinuteSecondaryTransactionsQueue |Todas las versiones, incluida 2013-08-15. Debe estar habilitada la replicación con redundancia geográfica con acceso de lectura. |
| Capacidad (solo servicio Blob) |$MetricsCapacityBlob |Todas las versiones, incluida 2013-08-15. |

Estas tablas se crean automáticamente cuando se habilita el análisis de almacenamiento para una cuenta de almacenamiento. Se accede a estos a través de hello espacio de nombres de cuenta de almacenamiento de hello, por ejemplo:`https://<accountname>.table.core.windows.net/Tables("$MetricsTransactionsBlob")`

### <a name="accessing-metrics-data"></a>Obtener acceso a los datos de las métricas
Pueden tener acceso a todos los datos en tablas de métricas de Hola mediante las API del servicio de tabla de Hola, incluidas las API de .NET proporcionadas por Hola Hola biblioteca de administrada de Azure. Administrador de cuenta de almacenamiento de Hello puede leer y eliminar entidades de tabla, pero no se puede crear o actualizarlos.

## <a name="billing-for-storage-analytics"></a>Facturación para análisis de almacenamiento
Todos los datos de las métricas se escriben servicios Hola de una cuenta de almacenamiento. Como resultado, cada una de las operaciones de escritura realizadas por el análisis de almacenamiento es facturable. Además, la cantidad de Hola de almacenamiento utilizado por los datos de métricas también es facturable.

Hola siguiendo las acciones realizadas por el análisis de almacenamiento es facturable:

* Blobs de toocreate de solicitudes para el registro. 
* Entidades de tabla de toocreate de solicitudes para las métricas.

Si ha configurado una directiva de retención de datos, no se le cobrarán las transacciones de eliminación cuando el análisis de almacenamiento elimine los antiguos datos de métricas y de registro. Sin embargo, las transacciones de eliminación desde un cliente sí son facturables. Para obtener más información acerca de las directivas de retención, consulte [Establecer una directiva de retención de datos de análisis de almacenamiento](https://msdn.microsoft.com/library/azure/hh343263.aspx).

### <a name="understanding-billable-requests"></a>Descripción de las solicitudes facturables
Todas las solicitudes realizadas a servicio de almacenamiento de la cuenta de tooan es facturable o no facturables. Análisis de almacenamiento registra cada solicitud realizada tooa servicio, incluido un mensaje de estado que indica cómo se controló la solicitud de saludo. De forma similar, el análisis de almacenamiento guarda las métricas para las operaciones de API de hello y un servicio de ese servicio, incluidos los porcentajes de Hola y el recuento de ciertos mensajes de estado. Juntas, estas características pueden ayudarle a analizar las solicitudes facturables, realizar mejoras en la aplicación y diagnosticar problemas con los servicios de tooyour de solicitudes. Para obtener más información sobre la facturación, consulte [Descripción de la facturación del almacenamiento de Azure: ancho de banda, transacciones y capacidad](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx).

Al examinar los datos de análisis de almacenamiento, puede utilizar tablas de Hola Hola [operaciones de registro de análisis de almacenamiento y mensajes de estado](https://msdn.microsoft.com/library/azure/hh343260.aspx) toodetermine tema qué solicitudes son facturables. A continuación, puede comparar los registros y toosee de mensajes de estado de las métricas datos toohello si se le cobró por una solicitud determinada. También puede utilizar tablas de hello en hello anterior tema tooinvestigate de disponibilidad para un servicio de almacenamiento o la operación de API determinada.

## <a name="next-steps"></a>Pasos siguientes
### <a name="setting-up-storage-analytics"></a>Configuración del análisis de almacenamiento
* [Supervisar una cuenta de almacenamiento en hello Portal de Azure](storage-monitor-storage-account.md)
* [Habilitar y configurar el análisis de almacenamiento](https://msdn.microsoft.com/library/hh360996.aspx)

### <a name="storage-analytics-logging"></a>Registro del análisis de almacenamiento
* [Acerca del registro del análisis de almacenamiento](https://msdn.microsoft.com/library/hh343262.aspx)
* [Formato del registro del análisis de almacenamiento](https://msdn.microsoft.com/library/hh343259.aspx)
* [Operaciones y mensajes de estado registrados por el análisis de almacenamiento](https://msdn.microsoft.com/library/hh343260.aspx)

### <a name="storage-analytics-metrics"></a>Métricas del análisis de almacenamiento
* [Acerca de las métricas del análisis de almacenamiento](https://msdn.microsoft.com/library/hh343258.aspx)
* [Esquema de las tablas de métricas del análisis de almacenamiento](https://msdn.microsoft.com/library/hh343264.aspx)
* [Operaciones y mensajes de estado registrados por el análisis de almacenamiento](https://msdn.microsoft.com/library/hh343260.aspx)  

