---
title: aaaMonitor, diagnosticar y solucionar problemas de almacenamiento | Documentos de Microsoft
description: "Usar características como el análisis de almacenamiento, el registro de cliente y otro tooidentify herramientas de otros fabricantes, diagnosticar y solución problemas relacionados con el almacenamiento de Azure."
services: storage
documentationcenter: 
author: fhryo-msft
manager: jahogg
editor: tysonn
ms.assetid: da57e844-705d-449d-8ed5-5607d2a6170b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: fhryo-msft
ms.openlocfilehash: 294a0bd27bd03913e01a719c0175cab827d58225
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-diagnose-and-troubleshoot-microsoft-azure-storage"></a>Supervisión, diagnóstico y solución de problemas de Almacenamiento de Microsoft Azure
[!INCLUDE [storage-selector-portal-monitoring-diagnosing-troubleshooting](../../includes/storage-selector-portal-monitoring-diagnosing-troubleshooting.md)]

## <a name="overview"></a>Información general
Diagnosticar y solucionar problemas en una aplicación distribuida que está hospedada en un entorno de nube puede ser más complicado que en los entornos tradicionales. Las aplicaciones se pueden implementar en una infraestructura de PaaS o IaaS, en una ubicación local, en un dispositivo móvil o en varios de estos elementos combinados. Normalmente, el tráfico de red de su aplicación puede atravesar redes públicas y privadas y su aplicación puede usar varias tecnologías de almacenamiento, como tablas de almacenamiento de Microsoft Azure, Blobs, colas o almacena los archivos de datos de adición tooother tal como relacional y las bases de datos del documento.

toomanage dichas aplicaciones correctamente debe supervisarlos de forma proactiva y entender cómo toodiagnose y solucionar problemas de todos los aspectos de los mismos y sus tecnologías dependientes. Como un usuario de servicios de almacenamiento de Azure, debe continuamente supervisar servicios de almacenamiento de hello usa la aplicación de cualquier cambio inesperado en el comportamiento (por ejemplo, más lento que los tiempos de respuesta habitual) y usar el registro toocollect más datos y tooanalyze un problema en profundidad. información de diagnóstico de Hello que obtener de supervisión y registro le ayudará a toodetermine Hola causa principal del programa Hola a emitir la aplicación que se encontró. A continuación, puede solucionar el problema de Hola y determinar los pasos adecuados de Hola que puede seguir tooremediate. Almacenamiento de Azure es un servicio de Azure de núcleo y constituye una parte importante de la mayoría de Hola de soluciones que los clientes implementar toohello infraestructura de Azure. Almacenamiento de Azure incluye capacidades toosimplify supervisar, diagnosticar y solucionar problemas de almacenamiento en las aplicaciones basadas en la nube.

> [!NOTE]
> Cuentas de almacenamiento con un tipo de replicación de almacenamiento con redundancia de zona (ZRS) no tiene las métricas de Hola o capacidad de registro habilitada en este momento. 
> 
> 

Una guía práctica tooend-to-end para solucionar problemas de las aplicaciones de almacenamiento de Azure, consulte [solución de problemas mediante las métricas de almacenamiento de Azure y registro, AzCopy y analizador de mensajes End-to-End](storage-e2e-troubleshooting.md).

* [Introducción]
  * [Organización de la guía]
* [el servicio de almacenamiento de supervisión]
  * [Supervisión del estado del servicio]
  * [Supervisión de la capacidad]
  * [Supervisión de la disponibilidad]
  * [Supervisión del rendimiento]
* [diagnosticar problemas de almacenamiento]
  * [Problemas de estado del servicio]
  * [Problemas de rendimiento]
  * [Diagnóstico de errores]
  * [Problemas del emulador de almacenamiento]
  * [Herramientas de registro de almacenamiento]
  * [Uso de herramientas de registro de red]
* [seguimiento to-end]
  * [Correlación de datos de registro]
  * [Id. de solicitud de cliente]
  * [Id. de solicitud de servidor]
  * [Marcas de tiempo]
* [Guía de solución de problemas]
  * [métricas muestran AverageE2ELatency alta y baja AverageServerLatency]
  * [Métricas muestran AverageE2ELatency baja y baja AverageServerLatency pero cliente hello está experimentando una latencia alta]
  * [Las métricas muestran una AverageServerLatency alta]
  * [Observa retrasos inesperados en la entrega de mensajes de una cola]
  * [métricas muestran un aumento en PercentThrottlingError]
  * [métricas muestran un aumento en PercentTimeoutError]
  * [Las métricas muestran un aumento de PercentNetworkError]
  * [cliente de Hello está recibiendo mensajes de HTTP 403 (prohibido)]
  * [cliente de Hello está recibiendo mensajes de HTTP 404 (no encontrado)]
  * [cliente de Hello está recibiendo mensajes de HTTP 409 (conflicto)]
  * [métricas muestran PercentSuccess baja o las entradas del registro de análisis tienen operaciones con estado de la transacción de ClientOtherErrors]
  * [Las métricas de capacidad muestran un aumento inesperado en el uso de la capacidad de almacenamiento]
  * [Se producen reinicios inesperados de máquinas virtuales que tienen muchos VHD adjuntos]
  * [El problema surge de mediante el emulador de almacenamiento de hello para el desarrollo o de prueba]
  * [Se están produciendo problemas para instalar hello Azure SDK para .NET]
  * [Tiene otro problema distinto relacionado con un servicio de almacenamiento]
* [apéndices]
  * [apéndice 1: tráfico HTTP y HTTPS toocapture utilizando Fiddler]
  * [apéndice 2: el tráfico de red de uso Wireshark toocapture]
  * [apéndice 3: el tráfico de red usando el analizador de mensajes de Microsoft toocapture]
  * [Apéndice 4: Usar tooview métricas y registro de datos de Excel]
  * [apéndice 5: supervisar con Application Insights para Visual Studio Team Services]

## <a name="introduction"></a>Introducción
Problemas relacionados con esta guía se muestra cómo toouse funciones, como análisis de almacenamiento de Azure y de registro de cliente de hello biblioteca de cliente de almacenamiento de Azure, otro tooidentify herramientas de otros fabricantes, diagnosticar y solucionar problemas de almacenamiento de Azure.

![][1]

*Figura 1. Supervisión, diagnóstico y solución de problemas*

Esta guía está previsto toobe leer principalmente por los desarrolladores de servicios en línea que usan servicios de almacenamiento de Azure y los profesionales de TI responsables de administrar dichos servicios en línea. Hola objetivos de esta guía son:

* toohelp mantener el estado de Hola y el rendimiento de las cuentas de almacenamiento de Azure.
* tooprovide procesos necesarios de Hola y decidir si un problema o un problema en una aplicación se relaciona tooAzure almacenamiento de toohelp de herramientas.
* tooprovide, con las instrucciones para solucionar problemas relacionados con tooAzure almacenamiento.

### <a name="how-this-guide-is-organized"></a>Organización de la guía
Hola sección "[el servicio de almacenamiento de supervisión]" describe cómo toomonitor Hola de estado y rendimiento de los servicios de almacenamiento de Azure con las métricas de análisis de almacenamiento de Azure (las métricas de almacenamiento).

Hola sección "[diagnosticar problemas de almacenamiento]" describe cómo emite toodiagnose mediante el análisis de registro de almacenamiento Azure (registro de almacenamiento). También describe cómo tooenable registro del lado cliente utilizando Hola utilidades en una de las bibliotecas de cliente de hello como Hola biblioteca cliente de almacenamiento para .NET o hello Azure SDK para Java.

Hola sección "[seguimiento to-end]" se describe cómo puede correlacionar información de hello contenida en varios archivos de registro y datos de métricas.

Hola sección "[Guía de solución de problemas]" proporciona una guía de solución de problemas para algunos de hello relativas al almacenamiento problemas comunes que puede surgir.

Hola "[apéndices]" incluyen información sobre el uso de otras herramientas como Wireshark y Netmon para analizar los datos del paquete, Fiddler para analizar los mensajes HTTP/HTTPS, de red y el analizador de mensajes de Microsoft para correlacionar datos del registro.

## <a name="monitoring-your-storage-service"></a>Supervisión del servicio de almacenamiento
Si conoce la supervisión de rendimiento de Windows, las métricas de Almacenamiento son algo así como los contadores del monitor de rendimiento de Windows, pero en Almacenamiento de Azure. En las métricas de almacenamiento encontrará un conjunto completo de métricas (contadores en la terminología de Monitor de rendimiento de Windows), como la disponibilidad del servicio, el número total de solicitudes tooservice o porcentaje de solicitudes correctas tooservice (para obtener una lista completa de hello las métricas disponibles, consulte <a href="http://msdn.microsoft.com/library/azure/hh343264.aspx" target="_blank">esquema de tabla de métricas de análisis de almacenamiento</a> en MSDN). Puede especificar si desea toocollect de servicio de almacenamiento de Hola y métricas agregadas cada hora o cada minuto. Para obtener más información sobre cómo las métricas de tooenable y monitor las cuentas de almacenamiento, vea <a href="http://go.microsoft.com/fwlink/?LinkId=510865" target="_blank">habilitar las métricas de almacenamiento</a> en MSDN.

Puede elegir qué métricas por hora que desee toodisplay en Hola Portal clásico de Azure y configurar las reglas que notificar a los administradores por correo electrónico cada vez que una métrica por hora supera un umbral determinado (para obtener más información, consulte la página de hello <a href="http://msdn.microsoft.com/library/azure/dn306638.aspx" target="_blank">Cómo: Recibir notificaciones de alerta y administrar reglas de alerta en Azure</a>). servicio de almacenamiento de Hello recopila las métricas con un esfuerzo, pero no puede registrar cada operación de almacenamiento.

Figura 2 muestra la página de Monitor de Hola Hola Portal clásico de Azure donde puede ver las métricas como disponibilidad, número total de solicitudes y las cifras de latencia promedio para una cuenta de almacenamiento. Una regla de notificación también se configuró tooalert administrador si disponibilidad cae por debajo de un nivel determinado. Ver estos datos, un área posibles con fines de investigación es porcentaje de éxito del servicio de tabla de hello está por debajo del 100% (para obtener más información, vea la sección de Hola "[métricas muestran PercentSuccess baja o las entradas del registro de análisis tienen operaciones con estado de la transacción de ClientOtherErrors]").

![][2]

*Figura 2 ver las métricas de almacenamiento en hello Portal clásico de Azure*

Debe supervisar de manera continua el tooensure de las aplicaciones de Azure que están activados y realizar correctamente; para ello:

* Establecimiento de algunas métricas de línea de base para la aplicación que se permiten los datos actuales de toocompare e identificar cualquier cambio significativo en el comportamiento de Hola de almacenamiento de Azure y la aplicación. valores de Hello las métricas de línea de base de será, en muchos casos, específica de la aplicación y se deben establecer cuando la aplicación de prueba de rendimiento.
* Grabación de métricas por minuto y usarlas toomonitor activamente para errores inesperados y las anomalías como picos en los recuentos de errores o los tipos de solicitud.
* Grabación métricas por hora y lo utiliza como promedios toomonitor promedio de los recuentos de errores y las tasas de solicitud.
* Investigando posibles problemas mediante herramientas de diagnóstico, como se describe más adelante en la sección Hola "[diagnosticar problemas de almacenamiento]."

gráficos de Hello en la figura 3 muestran ¿cómo Hola promedio que se produce para las métricas por hora puede ocultar picos de actividad. métricas por hora de Hello aparecen tooshow una tasa constante de solicitudes, al minuto Hola métricas revelan las fluctuaciones de Hola que realmente están teniendo lugar.

![][3]

Hello resto de esta sección describen las métricas, debe supervisar y por qué.

### <a name="monitoring-service-health"></a>Supervisión del estado del servicio
Puede usar hello [Portal clásico de Azure](https://manage.windowsazure.com) Hola de mantenimiento de hello tooview del servicio de almacenamiento de hello (y otros servicios de Azure) en todas las regiones de Azure alrededor de Hola a todos. Esto le permite toosee inmediatamente si un problema fuera de su control está afectando a Hola servicio de almacenamiento en región de Hola que use para la aplicación.

Hola Portal clásico de Azure también puede proporcionar a las notificaciones de incidentes que afectan a Hola varios servicios de Azure.
Nota: Esta información estaba disponible anteriormente, junto con los datos históricos, en Hola panel de servicios de Azure en <a href="http://status.azure.com" target="_blank">http://status.azure.com</a>.

Mientras que el Portal de Azure clásico de Hola recopila información de estado desde dentro de hello Azure centros de datos (horizontal interior supervisión), también puede adoptar un enfoque fuera de toogenerate las transacciones sintéticas que periódicamente tienen acceso a su hospedado de Azure aplicación Web desde varias ubicaciones. Hola servicios ofrecidos por <a href="http://www.keynote.com/solutions/monitoring/web-monitoring" target="_blank">Keynote</a>, <a href="https://www.gomeznetworks.com/?g=1" target="_blank">Gomez</a>, y Application Insights para Visual Studio Team Services son ejemplos de este enfoque en el exterior. Para obtener más información acerca de Application Insights para Visual Studio Team Services, consulte el apéndice de hello "[apéndice 5: supervisar con Application Insights para Visual Studio Team Services]."

### <a name="monitoring-capacity"></a>Supervisión de la capacidad
Las métricas de almacenamiento solo almacena las métricas de capacidad para servicio de blob de hello porque normalmente cuenta blobs de mayor proporción de Hola de los datos almacenados (en tiempo de Hola de escritura, no es capacidad de Hola de toomonitor toouse posible las métricas de almacenamiento de las tablas y colas) . Puede encontrar estos datos en hello **$MetricsCapacityBlob** tabla si ha habilitado la supervisión de hello servicio Blob. Las métricas de almacenamiento registra estos datos una vez al día, y se puede utilizar el valor de Hola de hello **RowKey** toodetermine si fila hello contiene una entidad que está relacionado con datos toouser (valor **datos**) o (de datos de análisis valor **análisis**). Cada entidad almacenado contiene información sobre la cantidad de Hola de almacenamiento usado (**capacidad** medido en bytes) y el número actual de Hola de contenedores (**ContainerCount**) y los blobs ( **ObjectCount**) en uso en la cuenta de almacenamiento de Hola. Para obtener más información acerca de las métricas de capacidad de hello almacenadas en hello **$MetricsCapacityBlob** de tabla, vea <a href="http://msdn.microsoft.com/library/azure/hh343264.aspx" target="_blank">esquema de tabla de métricas de análisis de almacenamiento</a> en MSDN.

> [!NOTE]
> Debe supervisar estos valores para las advertencias prematuras que se aproximan a los límites de capacidad de saludo de la cuenta de almacenamiento. Hola Portal clásico de Azure, en hello **Monitor** página para su cuenta de almacenamiento, puede agregar reglas de alerta toonotify si supera el uso del almacenamiento agregado o cae por debajo de los umbrales que especifique.
> 
> 

Para obtener ayuda acerca de la estimación del tamaño de Hola de varios objetos de almacenamiento como blobs, vea el blog de hello <a href="http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx" target="_blank">descripción Azure la facturación del almacenamiento: ancho de banda, transacciones y capacidad</a>.

### <a name="monitoring-availability"></a>Supervisión de la disponibilidad
Debe supervisar la disponibilidad de hello de servicios de almacenamiento de hello en su cuenta de almacenamiento mediante la supervisión de valor de Hola Hola **disponibilidad** Hola de columna en tablas de métricas por hora o minuto: **$ MetricsHourPrimaryTransactionsBlob**, **$MetricsHourPrimaryTransactionsTable**, **$MetricsHourPrimaryTransactionsQueue**, **$ MetricsMinutePrimaryTransactionsBlob**, **$MetricsMinutePrimaryTransactionsTable**, **$MetricsMinutePrimaryTransactionsQueue**, **$ MetricsCapacityBlob**. Hola **disponibilidad** columna contiene un valor de porcentaje que indica la disponibilidad de Hola de operación de hello API representado por fila de Hola o servicio hello (hello **RowKey** muestra si la fila de hello contiene métricas para servicio de Hola como un todo o de una operación de API específica).

Si el valor es inferior al 100%, significa que algunas solicitudes de almacenamiento no se están realizando correctamente. Puede ver por qué se producen errores mediante el examen de Hola otras columnas de datos de métricas de Hola que mostrar los números de Hola de solicitudes con distintos tipos de error como **error ServerTimeoutError**. Debe esperar toosee **disponibilidad** otoño temporalmente inferiores al 100% por razones como transitorio tiempos de espera mientras el servicio de Hola pasa solicitudes de equilibrio de carga de las particiones toobetter; Hola lógica en la aplicación cliente de reintento debe administrar estas condiciones intermitentes. página de Hello <a href="http://msdn.microsoft.com/library/azure/hh343260.aspx" target="_blank"> </a> listas Hola tipos de transacciones que incluye las métricas de almacenamiento en su **disponibilidad** cálculo.

Hola Portal clásico de Azure, en hello **Monitor** página para su cuenta de almacenamiento, puede agregar reglas de alerta toonotify si **disponibilidad** para un servicio cae por debajo del umbral especificado.

Hola "[Guía de solución de problemas]" sección de esta guía describen algunos tooavailability relacionados de almacenamiento servicio problemas comunes.

### <a name="monitoring-performance"></a>Supervisión del rendimiento
rendimiento de hello toomonitor de servicios de almacenamiento de hello, puede usar Hola siguientes métricas de hello cada hora y minuto tablas de métricas.

* Hola valores de hello **AverageE2ELatency** y **AverageServerLatency** mostrar el servicio de almacenamiento de Hola de tiempo medio de Hola o tipo de operación de API tarda tooprocess solicitudes. **AverageE2ELatency** es una medida de latencia de extremo a extremo que incluye la solicitud de hello tooread tiempo hello y enviar la respuesta de hello en solicitud de adición al toohello tiempo tooprocess Hola (por lo tanto incluye latencia de red una vez que la solicitud de Hola alcance de servicio de almacenamiento de hello); **AverageServerLatency** es una medida del tiempo de procesamiento de hello solo y, por tanto, se excluye alguna latencia de red relacionados con toocommunicating con cliente de Hola. Consulte la sección de Hola "[métricas muestran AverageE2ELatency alta y baja AverageServerLatency]" más adelante en esta guía para obtener una explicación de por qué podría ser una diferencia significativa entre estos dos valores.
* Hola valores de hello **TotalIngress** y **TotalEgress** columnas muestran la cantidad total de Hola de datos, en bytes, que entran en tooand va fuera de su servicio de almacenamiento o a través de un tipo específico de operación de API.
* Hola valores de hello **TotalRequests** está recibiendo columna Mostrar hello número total de solicitudes que Hola servicio de almacenamiento de la operación de API. **TotalRequests** es Hola número total de solicitudes que recibe servicio de almacenamiento de Hola.

Normalmente, deberá supervisar estos valores para ver si se produce algún cambio inesperado: son indicadores de que existe un error que se tiene que investigar.

Hola Portal clásico de Azure, en hello **Monitor** página para su cuenta de almacenamiento, puede agregar reglas de alerta toonotify si cualquiera de las métricas de rendimiento de Hola para este servicio quede por debajo o supere un umbral que especifique.

Hola "[Guía de solución de problemas]" sección de esta guía describen algunos tooperformance relacionados de almacenamiento servicio problemas comunes.

## <a name="diagnosing-storage-issues"></a>Diagnóstico de problemas de almacenamiento
Hay varias maneras de descubrir que existe un problema en la aplicación, entre ellas:

* Un error importante que provoca Hola aplicación toocrash o toostop en funcionamiento.
* Cambios importantes de los valores de línea de base de las métricas de Hola se está supervisando como se describe en la sección anterior de Hola "[el servicio de almacenamiento de supervisión]."
* Informes de usuarios de la aplicación que comuniquen que alguna operación concreta no se completó como se esperaba o que alguna característica no está funcionando.
* Errores generados dentro de la aplicación que aparecen en los archivos de registro o en algún otro método de notificación.

Normalmente, los servicios de almacenamiento de tooAzure relacionados con problemas se dividen en uno de cuatro amplias categorías:

* La aplicación tiene un problema de rendimiento, ya sea notificados por los usuarios o revela cambios en las métricas de rendimiento de Hola.
* Hay un problema con la infraestructura de almacenamiento de Azure de hello en una o varias regiones.
* La aplicación es encontrar un error, ya sea notificados por los usuarios o revela un aumento en uno de métricas de recuento de errores de Hola que se supervisan.
* Durante el desarrollo y prueba, puede estar usando el emulador de almacenamiento local de hello; se pueden producir algunos problemas que se relacionan específicamente toousage Hola del emulador de almacenamiento.

Hello las secciones siguientes describen los pasos de hello debe seguir toodiagnose y solucionar problemas en cada una de estas cuatro categorías. Hola sección "[Guía de solución de problemas]" más adelante en esta guía proporciona información más detallada para algunos problemas comunes que pueden producirse.

### <a name="service-health-issues"></a>Problemas de estado del servicio
Los problemas de estado del servicio suelen estar fuera de su control. Hola Portal clásico de Azure proporciona información sobre los problemas en curso con servicios de Azure incluidos los servicios de almacenamiento. Si ha elegido para el almacenamiento con redundancia geográfica con acceso de lectura al crear la cuenta de almacenamiento, a continuación, en caso de hello de los datos no esté disponible en la ubicación principal de hello, la aplicación podría cambiar temporalmente toohello copia de solo lectura en la ubicación secundaria Hola. toodo esto, la aplicación debe ser capaz de tooswitch entre el uso de ubicaciones de almacenamiento principal y secundaria de Hola y ser capaz de toowork en un modo de funcionalidad reducida con datos de solo lectura. las bibliotecas de cliente de almacenamiento de Azure de Hello permiten toodefine una directiva de reintentos que se puede leer desde el almacenamiento secundario en caso de que se produce un error en una lectura de almacenamiento principal. La aplicación también necesita toobe en cuenta que los datos de hello en la ubicación secundaria hello estén coherentes. Para obtener más información, consulte el blog de hello <a href="http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/04/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx" target="_blank">opciones de redundancia de almacenamiento de Azure y almacenamiento con redundancia geográfica acceso de lectura</a>.

### <a name="performance-issues"></a>Problemas de rendimiento
rendimiento de Hola de una aplicación puede ser subjetiva, especialmente desde la perspectiva del usuario. Por lo tanto, es importante toohave previsto métricas disponibles toohelp identificar donde puede haber un problema de rendimiento. Muchos factores pueden afectar al rendimiento de Hola de un servicio de almacenamiento de Azure desde la perspectiva de aplicación de cliente de Hola. Estos factores pueden llevarse a cabo en el servicio de almacenamiento de hello, en cliente de Hola o de infraestructura de red de hello; por lo tanto, es importante toohave una estrategia para identificar el origen de hello del problema de rendimiento de Hola.

Después de haber identificado la ubicación probable de Hola de hello causa del problema de rendimiento de Hola de métricas de hello, también puede, a continuación, toofind de archivos de registro de uso Hola detallada toodiagnose de información y solucionar problemas de hello aún más.

Hola sección "[Guía de solución de problemas]" más adelante en esta guía proporciona más información sobre algunos rendimiento comunes relacionados con los problemas que surjan.

### <a name="diagnosing-errors"></a>Diagnóstico de errores
Los usuarios de la aplicación pueden avisarle de errores notificados por la aplicación de cliente de Hola. Las métricas de Almacenamiento también registran los recuentos de diferentes tipos de errores de los servicios de almacenamiento, como **NetworkError**, **ClientTimeoutError** o **AuthorizationError**. Las métricas de Almacenamiento solamente registran los recuentos de diversos tipos de errores, pero puede obtener más detalles sobre cada una de las solicitudes examinando los registros del lado servidor, del lado cliente y de la red. Por lo general, código de estado HTTP de hello devuelto por el servicio de almacenamiento de hello le proporcionará un valor que indica el motivo del error de solicitud de saludo.

> [!NOTE]
> Recuerde que debe esperar toosee algunos errores intermitentes: por ejemplo, los errores debido a condiciones de red tootransient o los errores de aplicación.
> 
> 

Hello recursos siguientes en MSDN son útiles para entender los códigos de estado y de error relacionados con el almacenamiento de información:

* <a href="http://msdn.microsoft.com/library/azure/dd179357.aspx" target="_blank">Códigos de error comunes de la API de REST</a>
* <a href="http://msdn.microsoft.com/library/azure/dd179439.aspx" target="_blank">Códigos de error del servicio BLOB</a>
* <a href="http://msdn.microsoft.com/library/azure/dd179446.aspx" target="_blank">Códigos de error del servicio Cola</a>
* <a href="http://msdn.microsoft.com/library/azure/dd179438.aspx" target="_blank">Códigos de error del servicio Tabla</a>

### <a name="storage-emulator-issues"></a>Problemas del emulador de almacenamiento
Hello Azure SDK incluye un emulador de almacenamiento que se puede ejecutar en una estación de trabajo de desarrollo. Este emulador simula la mayor parte del comportamiento de hello de servicios de almacenamiento de Azure de Hola y es útil durante el desarrollo y prueba, lo que le toorun las aplicaciones que utilizan servicios de almacenamiento de Azure sin Hola necesitan para una suscripción de Azure y una cuenta de almacenamiento de Azure.

Hola "[Guía de solución de problemas]" sección de esta guía describen algunos problemas comunes que se encuentran con el emulador de almacenamiento de Hola.

### <a name="storage-logging-tools"></a>Herramientas de registro de almacenamiento
El registro de Almacenamiento proporciona el registro del lado servidor de las solicitudes de almacenamiento de la cuenta de almacenamiento de Azure. Para obtener más información acerca de cómo el registro de servidor tooenable y Hola de acceso a datos del registro, consulte <a href="http://go.microsoft.com/fwlink/?LinkId=510867" target="_blank">utilizando el registro de servidor</a> en MSDN.

Hola biblioteca de cliente de almacenamiento para .NET permite toocollect los datos del registro de cliente que está relacionada con las operaciones de toostorage realizadas por la aplicación. Para obtener más información acerca de cómo tooenable registro del lado cliente y Hola de acceso a datos del registro, consulte <a href="http://go.microsoft.com/fwlink/?LinkId=510868" target="_blank">del lado cliente registro utilizando Hola biblioteca cliente de almacenamiento</a> en MSDN.

> [!NOTE]
> En algunos casos (por ejemplo, los errores de autorización de SAS), un usuario puede notificar un error para el que no puede encontrar ningún dato de solicitud en hello registros de almacenamiento de servidor. Puede usar funciones de registro de hello de hello biblioteca cliente de almacenamiento tooinvestigate si es causa de Hola de problema de hello en el cliente de Hola o usar la red de hello tooinvestigate de herramientas de supervisión de red.
> 
> 

### <a name="using-network-logging-tools"></a>Uso de herramientas de registro de red
Puede capturar el tráfico de hello entre tooprovide de cliente y servidor hello detallada información acerca de hello datos Hola cliente y el servidor son intercambiar y Hola subyacentes de las condiciones de red. Algunas herramientas útiles de redes son:

* Fiddler (<a href="http://www.telerik.com/fiddler" target="_blank">http://www.telerik.com/fiddler</a>) es un proxy que permite a los encabezados de hello tooexamine y datos de carga de mensajes de solicitud y respuesta HTTP y HTTPS de depuración de web gratuita. Para obtener más información, vea "[apéndice 1: tráfico HTTP y HTTPS toocapture utilizando Fiddler]".
* Monitor de red (Netmon) de Microsoft (<a href="http://www.microsoft.com/download/details.aspx?id=4865" target="_blank">http://www.microsoft.com/download/details.aspx?id=4865</a>) y Wireshark (<a href="http://www.wireshark.org/" target="_blank">http://www.wireshark.org/</a>) son redes libre analizadores de protocolo que permiten se tooview paquete información detallada para una amplia variedad de protocolos de red. Para obtener más información acerca de Wireshark, vea "[apéndice 2: el tráfico de red de uso Wireshark toocapture]".
* Analizador de mensajes de Microsoft es una herramienta de Microsoft que reemplaza a Netmon y que, además, toocapturing red datos del paquete, le ayuda a tooview y analizar datos de registro de hello capturados desde otras herramientas. Para obtener más información, vea "[apéndice 3: el tráfico de red usando el analizador de mensajes de Microsoft toocapture]".
* Si desea tooperform una toocheck de prueba de la conectividad básica que el equipo cliente puede conectarse toohello de servicio de almacenamiento de Azure a través de red de hello, no puede hacerlo mediante el estándar de hello **ping** herramienta en el cliente de Hola. Sin embargo, puede usar hello **tcping** herramienta toocheck conectividad. **Tcping** está disponible para descargar en <a href="http://www.elifulkerson.com/projects/tcping.php" target="_blank">http://www.elifulkerson.com/projects/tcping.php</a>.

En muchos casos, los datos de registro de hello de hello biblioteca cliente de almacenamiento y el registro de almacenamiento será suficiente toodiagnose un problema, pero en algunos escenarios, puede que necesite hello más información que pueden proporcionar estas herramientas de registro de la red. Por ejemplo, mediante Fiddler tooview HTTP y HTTPS permite los mensajes que los datos de encabezado y la carga de tooview envíe tooand desde Hola servicios de almacenamiento, lo que le permitiría tooexamine cómo una aplicación cliente vuelve a intentar las operaciones de almacenamiento. Analizadores de protocolo como Wireshark funcionan en nivel de paquete de hello habilitar datos TCP tooview, lo que permitirían tootroubleshoot perdido paquetes y problemas de conectividad. El Analizador de mensajes puede operar en los niveles HTTP y TCP.

## <a name="end-to-end-tracing"></a>Seguimiento integral
La traza de un extremo a otro con diversos archivos de registro es una técnica útil para investigar problemas potenciales. Puede utilizar información de fecha y hora de Hola de los datos de métricas como una indicación de que toostart examina los archivos de registro de hello para hello detallada información que le ayudará a solucionar el problema de Hola.

### <a name="correlating-log-data"></a>Correlación de datos de registro
Al ver los registros de aplicaciones cliente, red realiza el seguimiento y el registro de almacenamiento de servidor es crítico toobe toocorrelate capaz de solicitudes a través de hello diferentes archivos de registro. archivos de registro de Hello incluyen un número de campos diferentes que son útiles como identificadores de correlación. Id. de solicitud de cliente Hello es hello más útiles toouse toocorrelate entradas de los campos en los registros diferentes Hola. Sin embargo en ocasiones, puede ser útil toouse Id. de solicitud de servidor de Hola o las marcas de tiempo. Hello las secciones siguientes proporcionan más detalles acerca de estas opciones.

### <a name="client-request-id"></a>Id. de solicitud de cliente
Hola biblioteca cliente de almacenamiento genera automáticamente un Id. de solicitud de cliente único para cada solicitud.

* Hola crea registros de cliente que Hola biblioteca cliente de almacenamiento, Id. de solicitud de cliente hello aparece en hello **Id. de solicitud de cliente** campo de cada entrada del registro relacionada con la solicitud de toohello.
* En un seguimiento de red como una captura Fiddler, Id. de solicitud de cliente hello está visible en los mensajes de solicitud como hello **x-ms-client-request-id** valor del encabezado HTTP.
* En el registro de registro de almacenamiento de servidor de hello, Id. de solicitud de cliente de Hola aparece en la columna de Id. de solicitud de cliente de Hola.

> [!NOTE]
> Es posible para varias de las solicitudes tooshare Hola mismo Id. de solicitud de cliente porque el cliente de hello puede asignar este valor (aunque Hola biblioteca cliente de almacenamiento asigna automáticamente un nuevo valor). En el caso de hello de reintentos de cliente hello, todos los intentos de comparten Hola mismo Id. de solicitud de cliente. En caso de hello de un lote enviado desde el cliente de hello, lote hello tiene un identificador de solicitud de cliente único.
> 
> 

### <a name="server-request-id"></a>Identificador de solicitud de servidor
servicio de almacenamiento de Hello genera automáticamente el Id. de solicitud de servidor.

* En el registro de registro de almacenamiento de servidor de hello, Id. de solicitud de servidor hello aparece hello **encabezado de Id. de solicitud** columna.
* En un seguimiento de red como una captura Fiddler, Id. de solicitud de servidor hello aparece en los mensajes de respuesta como hello **x-ms-request-id** valor del encabezado HTTP.
* Hola crea registros de cliente que Hola biblioteca cliente de almacenamiento, Id. de solicitud de servidor hello aparece en hello **texto de la operación** columna de entrada del registro de hello muestra los detalles de la respuesta del servidor hello.

> [!NOTE]
> servicio de almacenamiento de Hello siempre asigna a un único servidor solicitud de tooevery de Id. de solicitud que recibe, por lo que cada reintento de cliente de Hola y cada operación que se incluyen en un lote tienen un identificador de solicitud de servidor único.
> 
> 

Si hello biblioteca cliente de almacenamiento produce un **StorageException** en el cliente de hello, Hola **RequestInformation** propiedad contiene un **objeto RequestResult** objeto que incluya un **ServiceRequestID** propiedad. También puede acceder a los objetos **RequestResult** desde una instancia de **OperationContext**.

Hola ejemplo de código siguiente muestra cómo tooset personalizado **ClientRequestId** valor adjuntando un **OperationContext** objeto servicio de almacenamiento de hello solicitud toohello. También muestra cómo hello tooretrieve **ServerRequestId** valor de mensaje de respuesta de saludo.

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Create an Operation Context that includes custom ClientRequestId string based on constants defined within hello application along with a Guid.
OperationContext oc = new OperationContext();
oc.ClientRequestID = String.Format("{0} {1} {2} {3}", HOSTNAME, APPNAME, USERID, Guid.NewGuid().ToString());

try
{
    CloudBlobContainer container = blobClient.GetContainerReference("democontainer");
    ICloudBlob blob = container.GetBlobReferenceFromServer("testImage.jpg", null, null, oc);  
    var downloadToPath = string.Format("./{0}", blob.Name);
    using (var fs = File.OpenWrite(downloadToPath))
    {
        blob.DownloadToStream(fs, null, null, oc);
        Console.WriteLine("\t Blob downloaded toofile: {0}", downloadToPath);
    }
}
catch (StorageException storageException)
{
    Console.WriteLine("Storage exception {0} occurred", storageException.Message);
    // Multiple results may exist due tooclient side retry logic - each retried operation will have a unique ServiceRequestId
    foreach (var result in oc.RequestResults)
    {
            Console.WriteLine("HttpStatus: {0}, ServiceRequestId {1}", result.HttpStatusCode, result.ServiceRequestID);
    }
}
```

### <a name="timestamps"></a>Marcas de tiempo
También puede utilizar las marcas de tiempo toolocate relacionadas con las entradas del registro, pero tenga cuidado cualquier de sesgo de reloj entre el cliente de Hola y el servidor que puedan existir. Debe buscar más o menos de 15 minutos para la coincidencia de entradas de servidor en función de la marca de tiempo de hello en el cliente de Hola. Recuerde que Hola blob los metadatos de blobs de hello métricas contenedor indican el intervalo de tiempo de Hola para las métricas de hello almacenadas en el blob de hello; Esto es útil si tiene muchos blobs de métricas para hello mismo horas o minutos.

## <a name="troubleshooting-guidance"></a>Guía de solución de problemas
En esta sección le ayudará con diagnóstico de Hola y solución de problemas de algunos problemas comunes de hello de la aplicación puede producirse al usar servicios de almacenamiento de Azure Hola. Use la lista de Hola por debajo del problema específico de toolocate Hola información tooyour relevante.

**Árbol de decisión de solución de problemas**

- - -
¿El problema relaciona rendimiento toohello de uno de los servicios de almacenamiento de hello?

* [métricas muestran AverageE2ELatency alta y baja AverageServerLatency]
* [Métricas muestran AverageE2ELatency baja y baja AverageServerLatency pero cliente hello está experimentando una latencia alta]
* [Las métricas muestran una AverageServerLatency alta]
* [Observa retrasos inesperados en la entrega de mensajes de una cola]

- - -
¿El problema relaciona toohello disponibilidad de uno de los servicios de almacenamiento de hello?

* [métricas muestran un aumento en PercentThrottlingError]
* [métricas muestran un aumento en PercentTimeoutError]
* [Las métricas muestran un aumento de PercentNetworkError]

- - -
¿La aplicación cliente recibe una respuesta HTTP 4XX (por ejemplo, 404) de un servicio de almacenamiento?

* [cliente de Hello está recibiendo mensajes de HTTP 403 (prohibido)]
* [cliente de Hello está recibiendo mensajes de HTTP 404 (no encontrado)]
* [cliente de Hello está recibiendo mensajes de HTTP 409 (conflicto)]

- - -
[métricas muestran PercentSuccess baja o las entradas del registro de análisis tienen operaciones con estado de la transacción de ClientOtherErrors]

- - -
[Las métricas de capacidad muestran un aumento inesperado en el uso de la capacidad de almacenamiento]

- - -
[Se producen reinicios inesperados de máquinas virtuales que tienen muchos VHD adjuntos]

- - -
[El problema surge de mediante el emulador de almacenamiento de hello para el desarrollo o de prueba]

- - -
[Se están produciendo problemas para instalar hello Azure SDK para .NET]

- - -
[Tiene otro problema distinto relacionado con un servicio de almacenamiento]

- - -
### <a name="metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency"></a>Las métricas muestran una AverageE2ELatency alta y una AverageServerLatency baja
Hello más potentes de ilustración de la herramienta de supervisión de Portal de Azure clásico de hello muestran un ejemplo donde hello **AverageE2ELatency** es significativamente mayor que hello **AverageServerLatency**.

![][4]

Tenga en cuenta que el servicio de almacenamiento de Hola solamente calcula métrica hello **AverageE2ELatency** para las solicitudes correctas y, a diferencia de **AverageServerLatency**, incluye el tiempo de Hola Hola cliente lleva a cabo toosend Hola datos y recibir la confirmación de servicio de almacenamiento de Hola. Por lo tanto, una diferencia entre **AverageE2ELatency** y **AverageServerLatency** podría ser cualquiera debido toohello cliente aplicación que se va a lentos toorespond o due tooconditions en red Hola.

> [!NOTE]
> También puede ver **E2ELatency** y **ServerLatency** para las operaciones de almacenamiento individual en el registro de almacenamiento de hello registrar los datos.
> 
> 

#### <a name="investigating-client-performance-issues"></a>Investigación de problemas de rendimiento del cliente
Las posibles razones para cliente hello responde lentamente incluyen tener un número limitado de conexiones disponibles o subprocesos. Es posible que el problema de hello tooresolve capaz de modificando hello toobe de código de cliente más eficaz (por ejemplo, utilizando el servicio de almacenamiento de las llamadas asincrónicas toohello), o bien usar una máquina Virtual más grande (con más memoria y más núcleos).

Para los servicios de tabla y cola de hello, algoritmo de Nagle hello también puede hacer que alta **AverageE2ELatency** en comparación demasiado**AverageServerLatency**: para obtener más información, consulte Hola entrada <a href="http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx" target="_blank">de Nagle El algoritmo no es descriptivo hacia las solicitudes de pequeñas</a> en hello Blog del equipo de almacenamiento de Microsoft Azure. Puede deshabilitar el algoritmo de Nagle hello en el código mediante el uso de hello **ServicePointManager** clase Hola **System.Net** espacio de nombres. Debe hacerlo antes de realizar cualquier tabla de toohello de llamadas o los servicios de cola en la aplicación, ya que esto no afecta a las conexiones que ya están abiertos. Hello en el ejemplo siguiente se procede de hello **Application_Start** método en un rol de trabajo.

```csharp
var storageAccount = CloudStorageAccount.Parse(connStr);
ServicePoint tableServicePoint = ServicePointManager.FindServicePoint(storageAccount.TableEndpoint);
tableServicePoint.UseNagleAlgorithm = false;
ServicePoint queueServicePoint = ServicePointManager.FindServicePoint(storageAccount.QueueEndpoint);
queueServicePoint.UseNagleAlgorithm = false;
```

Debe comprobar Hola registros del lado cliente toosee cuántas solicitudes de envío de la aplicación cliente y busque .NET generales relacionados con los cuellos de botella de rendimiento en el cliente, como CPU, colección de elementos no utilizados. NET, uso de la red o memoria (como un valor de inicio punto de solución de problemas de aplicaciones cliente. NET, consulte <a href="http://msdn.microsoft.com/library/7fe0dd2y(v=vs.110).aspx" target="_blank">depuración, seguimiento y generación de perfiles</a> en MSDN).

#### <a name="investigating-network-latency-issues"></a>Investigación de problemas de latencia de red
Normalmente, una latencia alta-to-end causada por red hello es debido a condiciones de tootransient. Puede investigar los problemas de red tanto transitorios como persistentes, como los paquetes descartados, con herramientas como Wireshark o el Analizador de mensajes de Microsoft.

Para obtener más información acerca del uso de Wireshark tootroubleshoot problemas de la red, consulte "[apéndice 2: el tráfico de red de uso Wireshark toocapture]."

Para obtener más información acerca del uso de problemas de red de tootroubleshoot de analizador de mensajes de Microsoft, vea "[apéndice 3: el tráfico de red usando el analizador de mensajes de Microsoft toocapture]."

### <a name="metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency"></a>Métricas muestran AverageE2ELatency baja y baja AverageServerLatency pero cliente hello está experimentando una latencia alta
En este escenario, hello más probable es un retraso en las solicitudes de almacenamiento de hello alcanzar el servicio de almacenamiento de Hola. Debería investigar por qué las solicitudes de cliente de hello no están realizando él a través del servicio blob toohello.

Las posibles razones para retrasar el envío de solicitudes de cliente de Hola incluyen tener un número limitado de conexiones disponibles o subprocesos. También debe comprobar si el cliente de hello realiza varios reintentos e investigue la razón de hello si éste es el caso de hello. Puede hacerlo mediante programación con la búsqueda en hello **OperationContext** objeto asociado a la solicitud de Hola y Hola recuperar **ServerRequestId** valor. Para obtener más información, vea el ejemplo de código de hello en la sección de Hola "[Id. de solicitud de servidor]."

Si no hay ningún problema en el cliente de hello, debería investigar posibles problemas de red, como la pérdida de paquetes. Puede usar herramientas como problemas de red tooinvestigate Wireshark o analizador de mensajes de Microsoft.

Para obtener más información acerca del uso de Wireshark tootroubleshoot problemas de la red, consulte "[apéndice 2: el tráfico de red de uso Wireshark toocapture]."

Para obtener más información acerca del uso de problemas de red de tootroubleshoot de analizador de mensajes de Microsoft, vea "[apéndice 3: el tráfico de red usando el analizador de mensajes de Microsoft toocapture]."

### <a name="metrics-show-high-AverageServerLatency"></a>Las métricas muestran una AverageServerLatency alta
En caso de hello de alta **AverageServerLatency** para las solicitudes de descarga de blobs, debe usar Hola registro de almacenamiento registra toosee si hay solicitudes repetidas de hello mismo blob (o conjunto de blobs). Las solicitudes de carga para blobs, debería investigar qué bloque tamaño Hola cliente utiliza (por ejemplo, bloques de menos de 64 KB de tamaño puede dar lugar a sobrecargas a menos que se lee de hello también estén incluidos en menos de 64K fragmenta), y si va a cargar varios clientes bloquea toohello mismo BLOB en paralelo. También debe comprobar las métricas por minuto de Hola para picos en el número de Hola de solicitudes que dan como resultado que superen Hola por segundo objetivos de escalabilidad: consulte también "[métricas muestran un aumento en PercentTimeoutError]."

Si ve el alto **AverageServerLatency** para las solicitudes de descarga de blob cuando no existe se repiten las solicitudes Hola mismo blob o un conjunto de blobs, a continuación, debe considere la posibilidad de almacenamiento en caché estos blobs mediante caché de Azure u Hola entrega de contenido de Azure Red (CDN). Para las solicitudes de carga, puede mejorar el rendimiento de hello mediante el uso de un tamaño de bloque. Para las consultas tootables, es también posible tooimplement caché del cliente en los clientes que realizan Hola mismo operaciones de consulta y Hola donde los datos no cambian con frecuencia.

Alta **AverageServerLatency** valores también pueden ser un síntoma de tablas mal diseñados o las consultas que el resultado de las operaciones de recorrido o que siga Hola anexarán/antepongan antipatrón. Consulte “[métricas muestran un aumento en PercentThrottlingError]” para más información.

> [!NOTE]
> Encontrará una lista de comprobación completa aquí: [Lista de comprobación de rendimiento y escalabilidad de Almacenamiento de Microsoft Azure](storage-performance-checklist.md).
> 
> 

### <a name="you-are-experiencing-unexpected-delays-in-message-delivery"></a>Observa retrasos inesperados en la entrega de mensajes de una cola
Si experimenta un retraso entre el momento de Hola una aplicación agrega mensajes tooa hello y cola uno se convierte en disponible tooread de cola de hello, a continuación debe tomar Hola siguiendo el problema de hello toodiagnose de pasos:

* Compruebe la aplicación hello correctamente consiste en Agregar toohello cola de mensajes de Hola. Compruebe que aplicación hello no está reintentando hello **AddMessage** método varias veces antes de poder continuar. registros de la biblioteca cliente de almacenamiento de Hello mostrará los repetidos reintentos de operaciones de almacenamiento.
* Compruebe que no hay ningún reloj desfase entre el rol de trabajo de Hola que agrega toohello cola de mensajes de Hola y rol de trabajo de Hola que lee mensajes de bienvenida de cola de Hola que hace que aparezcan como si hay un retraso en el procesamiento.
* Compruebe si se producen errores en rol de trabajo de Hola que lee mensajes de saludo de cola de Hola. Si un cliente de cola llama hello **GetMessage** método produce un error pero toorespond con una confirmación, mensaje de bienvenida de permanecerán visible en la cola de Hola hasta hello **invisibilityTimeout** expire. En este momento, mensajes de bienvenida deja de estar disponible para el procesamiento de nuevo.
* Compruebe si la longitud de la cola de Hola está aumentando con el tiempo. Esto puede ocurrir si no tiene suficiente tooprocess disponibles de los trabajadores todos Hola mensajes que otros procesos que va a colocar en cola Hola. También debe comprobar Hola métricas toosee si hello y delete se producen errores en las solicitudes de eliminación de cola recuento de mensajes, lo que podría indicar repite el mensaje de bienvenida de intentos fallidos toodelete.
* Examine los registros de registro de almacenamiento de Hola para cualquier operación de cola que tenga mayor de lo esperado **E2ELatency** y **ServerLatency** valores durante un período más largo de tiempo de lo habitual.

### <a name="metrics-show-an-increase-in-PercentThrottlingError"></a>Las métricas muestran un aumento de PercentThrottlingError
Limitación de errores se produce cuando se superan los objetivos de escalabilidad de Hola de un servicio de almacenamiento. servicio de almacenamiento de Hello tiene este tooensure que ningún inquilino o cliente único puede usar servicio de hello en gastos de Hola de otros usuarios. Para obtener más información, consulte <a href="http://msdn.microsoft.com/library/azure/dn249410.aspx" target="_blank">Objetivos de escalabilidad y rendimiento del almacenamiento de Azure</a> para ver detalles sobre los objetivos de escalabilidad de las cuentas de almacenamiento y los objetivos de rendimiento de las particiones que hay dentro de las cuentas de almacenamiento.

Si hello **PercentThrottlingError** métrica mostrar un aumento de porcentaje de Hola de solicitudes que se están produciendo un error de limitación, deberá tooinvestigate uno de los dos escenarios:

* [Aumento transitorio de PercentThrottlingError]
* [Aumento permanente del error PercentThrottlingError]

Un aumento en **PercentThrottlingError** a menudo se produce en hello al mismo tiempo que un aumento en número de Hola de las solicitudes de almacenamiento o cuando haya inicialmente cargar probar la aplicación. También se puede manifestar en cliente hello como "503 servidor ocupado" o mensajes de estado HTTP de "tiempo de espera de operación 500" de las operaciones de almacenamiento.

#### <a name="transient-increase-in-PercentThrottlingError"></a>Aumento transitorio de PercentThrottlingError
Si está viendo los picos en el valor de Hola de **PercentThrottlingError** que coincida con los períodos de gran actividad para la aplicación hello, debe implementar un exponencial (no lineal) retroceso estrategia de reintentos en el cliente: Esto reducirá la carga inmediata de hello en partición de Hola y ayudar a su toosmooth aplicación los picos de tráfico. Para obtener más información acerca de cómo las directivas de reintento tooimplement mediante Hola biblioteca cliente de almacenamiento, consulte <a href="http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.retrypolicies.aspx" target="_blank">Microsoft.WindowsAzure.Storage.RetryPolicies Namespace</a> en MSDN.

> [!NOTE]
> También puede ver picos en el valor de Hola de **PercentThrottlingError** que no coinciden con períodos de gran actividad para la aplicación hello: Hola aquí en la causa más probable es servicio de almacenamiento de hello mover particiones tooimprove carga equilibrio.
> 
> 

#### <a name="permanent-increase-in-PercentThrottlingError"></a>Aumento permanente del error PercentThrottlingError
Si ve un valor continuadamente alto para **PercentThrottlingError** siguiendo un aumento permanente en los volúmenes de transacciones o al realizar la carga inicial pruebas en su aplicación, es necesario tooevaluate cómo la aplicación utiliza las particiones de almacenamiento y se está aproximando a destinos de escalabilidad de Hola para una cuenta de almacenamiento. Por ejemplo, si ve errores en una cola (que se cuenta como una sola partición) de limitación, a continuación, puede utilizar las transacciones de colas adicionales toospread hello en varias particiones. Si ve errores en una tabla de limitación, debe tooconsider mediante un toospread de esquema de partición diferente las transacciones en varias particiones mediante el uso de una gama más amplia de valores de clave de partición. Una causa común de este problema es Hola anteponer/anexar antipatrón donde seleccionar fecha de hello como clave de partición de hello y, a continuación, todos los datos en un día determinado se escriben tooone partición: bajo una carga, esto puede provocar un cuello de botella de escritura. Debe pensar en usar otro diseño de particiones o evaluar si usar el almacenamiento de BLOB puede ser una solución más adecuada. También debe comprobar si Hola limitación se produce como resultado de picos máximos en el tráfico e investigar formas de suavizado en el patrón de solicitudes.

Si distribuye las transacciones en varias particiones, debe ser consciente de los límites de escalabilidad de hello establecido para la cuenta de almacenamiento de Hola. Por ejemplo, si utiliza diez colas cada máximo de Hola de procesamiento de 2.000 mensajes de 1KB por segundo, es posible que en hello límite general de 20.000 mensajes por segundo para la cuenta de almacenamiento de Hola. Si necesita más de 20.000 entidades por segundo tooprocess, considere la posibilidad de usar varias cuentas de almacenamiento. También debe tener en cuenta que el tamaño de las solicitudes de Hola y entidades tiene un impacto en el cuando el servicio de almacenamiento de hello limita los clientes: si tiene más grandes de las solicitudes y las entidades, puede limitar antes.

Diseño de consulta ineficaz también puede producir límites de escalabilidad de hello toohit para las particiones de tabla. Por ejemplo, una consulta con un filtro que selecciona solo uno por ciento de las entidades de hello en una partición, pero que examina todas las entidades de hello en una partición deberán tooaccess cada entidad. Todas las entidades leer contará para el número total de Hola de transacciones en esa partición; por lo tanto, se pueden llegar fácilmente a los objetivos de escalabilidad de Hola.

> [!NOTE]
> Las pruebas de rendimiento deberían revelar todos los diseños de consulta ineficientes de la aplicación.
> 
> 

### <a name="metrics-show-an-increase-in-PercentTimeoutError"></a>Las métricas muestran un aumento de PercentTimeoutError
Las métricas muestran un aumento de **PercentTimeoutError** en uno de los servicios de almacenamiento. En hello mismo tiempo, hello cliente recibe un gran volumen de mensajes de estado HTTP de "tiempo de espera de operación 500" de las operaciones de almacenamiento.

> [!NOTE]
> Puede ver los errores de tiempo de espera temporalmente como servicio de almacenamiento de hello carga de las solicitudes de saldos moviendo un servidor nuevo de tooa de particiones.
> 
> 

Hola **PercentTimeoutError** métrica es una agregación de hello siguientes métricas: **error ClientTimeoutError**, **error AnonymousClientTimeoutError**,  **Error SASClientTimeoutError**, **error ServerTimeoutError**, **error AnonymousServerTimeoutError**, y **error SASServerTimeoutError**.

los tiempos de espera del servidor de Hola se deben a un error en el servidor de Hola. los tiempos de espera del cliente de Hello suceder debido a una operación en el servidor de hello superó el tiempo de espera de hello especificado por el cliente de hello; Por ejemplo, un cliente con hello biblioteca cliente de almacenamiento puede establecer un tiempo de espera para una operación mediante hello **ServerTimeout** propiedad de hello **QueueRequestOptions** clase.

Tiempos de espera de indican un problema con el servicio de almacenamiento de Hola que requiere mayor investigación. Puede usar las métricas toosee si está alcanzando límites de escalabilidad de Hola para servicio de Hola y tooidentify los picos de tráfico que podrían estar causando el problema. Si el problema de hello es intermitente, es posible due equilibrio tooload actividad en el servicio de Hola. Si el problema de hello es persistente y no está causado por la aplicación alcanzar los límites de escalabilidad de hello del servicio de Hola, debería generar un problema de soporte técnico. Para los tiempos de espera de cliente, debe decidir si el tiempo de espera de Hola se establece tooan de valor adecuado en el cliente de Hola y cualquier valor de tiempo de espera de cambio Hola establecidas en el cliente de Hola o investigar cómo puede mejorar el rendimiento de Hola de operaciones de hello en el servicio de almacenamiento de hello, para ejemplo de optimización de las consultas de tabla o reduciendo el tamaño de Hola de los mensajes.

### <a name="metrics-show-an-increase-in-PercentNetworkError"></a>Las métricas muestran un aumento de PercentNetworkError
Las métricas muestran un aumento de **PercentNetworkError** en uno de los servicios de almacenamiento. Hola **PercentNetworkError** métrica es una agregación de hello siguientes métricas: **error NetworkError**, **error AnonymousNetworkError**, y  **Error SASNetworkError**. Se producen cuando el servicio de almacenamiento de hello detecta un error de red cuando Hola cliente realiza una solicitud de almacenamiento.

Hello causa más común de este error es un cliente desconectar antes de que expire un tiempo de espera en el servicio de almacenamiento de Hola. Debería investigar el código de hello en su toounderstand cliente razón y el momento cliente de Hola se desconecta del servicio de almacenamiento de Hola. También puede utilizar Wireshark, analizador de mensajes de Microsoft o problemas de conectividad de red Tcping tooinvestigate de cliente de Hola. Estas herramientas se describen en hello [apéndices].

### <a name="the-client-is-receiving-403-messages"></a>cliente de Hello está recibiendo mensajes de HTTP 403 (prohibido)
Si la aplicación cliente está produciendo errores HTTP 403 (prohibido), una causa probable es que ese cliente hello está usando un expiradas firma de acceso compartido (SAS) cuando envía una solicitud de almacenamiento (aunque otras causas posibles incluyen las claves sesgo, no es válido de reloj y vacía encabezados). Si una clave SAS expirada es la causa de hello, no verá las entradas de datos de registro del registro de almacenamiento de hello en el servidor. Hello tabla siguiente muestra un ejemplo de registro de cliente de hello generado por hello biblioteca de cliente de almacenamiento que se muestra que se produzca este problema:

| Origen | Nivel de detalle | Nivel de detalle | Id. de solicitud de cliente | Texto de operación |
| --- | --- | --- | --- | --- |
| Microsoft.WindowsAzure.Storage |Información |3 |85d077ab-… |Iniciando operación con ubicación Primary según modo de ubicación PrimaryOnly. |
| Microsoft.WindowsAzure.Storage |Información |3 |85d077ab -… |A partir de sincrónico solicitar toohttps://domemaildist.blob.core.windows.netazureimblobcontainer/blobCreatedViaSAS.txt?sv=2014-02-14&amp;sr = c&amp;si = mypolicy&amp;sig = OFnd4Rd7z01fIvh % 2BmcR6zbudIH2F5Ikm % 2FyhNYZEmJNQ % 3D&amp;api-version = 2014-02-14. |
| Microsoft.WindowsAzure.Storage |Información |3 |85d077ab -… |Esperando respuesta. |
| Microsoft.WindowsAzure.Storage |Warning (Advertencia) |2 |85d077ab -… |Excepción que se produce mientras se espera respuesta: servidor remoto hello devolvió un error: (403) prohibido... |
| Microsoft.WindowsAzure.Storage |Información |3 |85d077ab -… |Respuesta recibida. Código de estado = 403, Id. de solicitud = 9d67c64a-64ed-4b0d-9515-3b14bbcdc63d, Content-MD5 = , ETag = . |
| Microsoft.WindowsAzure.Storage |Warning (Advertencia) |2 |85d077ab -… |Excepción que se produce durante la operación de hello: servidor remoto hello devolvió un error: (403) prohibido... |
| Microsoft.WindowsAzure.Storage |Información |3 |85d077ab -… |Comprobando si se debe reintentar la operación de Hola. Número de reintentos = 0, código de estado HTTP = 403, excepción = Hola servidor remoto devolvió un error: (403) prohibido... |
| Microsoft.WindowsAzure.Storage |Información |3 |85d077ab -… |ubicación siguiente Hola se estableció tooPrimary, según el modo de ubicación de Hola. |
| Microsoft.WindowsAzure.Storage |Error |1 |85d077ab -… |La directiva de reintentos no permitió un reintento. Error con el servidor remoto hello devolvió un error: (403) prohibido. |

En este escenario, debería investigar por qué caduca el token de SAS de hello antes de cliente de hello envía al servidor de token toohello de hello:

* Por lo general, no debe establecer una hora de inicio cuando se crea una SAS para un cliente toouse inmediatamente. Si hay pequeñas diferencias de reloj entre el host de hello generar Hola SAS utilizando Hola hora actual y el servicio de almacenamiento de hello, entonces es posible que tooreceive de servicio de almacenamiento de hello una SAS que todavía no es válida.
* En las SAS, no debe establecer tiempos de expiración muy breves. Una vez más, las diferencias de reloj pequeño entre el host de hello generar Hola SAS y servicio de almacenamiento de hello puede provocar tooa SAS aparentemente caduca antes de lo esperado.
* Hola parámetro version en la clave SAS de hello (por ejemplo **sv = 2012-02-12**) coincidir con la versión de Hola de Hola que usa la biblioteca de cliente de almacenamiento. Debe utilizar siempre la versión más reciente de Hola de hello biblioteca cliente de almacenamiento. Para obtener más información sobre el control de versiones de token de SAS, consulte [What's new for Microsoft Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/14/what-s-new-for-microsoft-azure-storage-at-teched-2014.aspx)(Novedades de Almacenamiento de Microsoft Azure).
* * Si vuelve a generar las claves de acceso de almacenamiento (haga clic en **administrar claves de acceso** en cualquier página de su cuenta de almacenamiento en el Portal de Azure clásico hello) podría invalidar los tokens SAS existentes. Esto puede ser un problema si generar tokens SAS con una hora de expiración largo para toocache de las aplicaciones de cliente.

Si usa tokens SAS en toogenerate Hola biblioteca cliente de almacenamiento, es fácil toobuild un token válido. Sin embargo, si usa Hola API de REST de almacenamiento y crear tokens SAS de Hola a mano lea detenidamente el tema de hello <a href="http://msdn.microsoft.com/library/azure/ee395415.aspx" target="_blank">delegar el acceso con una firma de acceso compartido</a> en MSDN.

### <a name="the-client-is-receiving-404-messages"></a>cliente de Hello está recibiendo mensajes de HTTP 404 (no encontrado)
Si la aplicación de cliente de hello recibe un mensaje de HTTP 404 (no encontrado) de servidor hello, esto implica que Hola objeto Hola el cliente estaba intentando toouse (por ejemplo, una entidad, tabla, blob, contenedor o cola) no existe en el servicio de almacenamiento de Hola. Hay varios motivos posibles, por ejemplo:

* [cliente de Hello u otro proceso haya eliminado previamente objeto Hola]
* [Un problema de autorización de Firma de acceso compartido (SAS)]
* [Código de JavaScript del lado cliente no tiene el objeto de permiso tooaccess Hola]
* [Error de red]

#### <a name="client-previously-deleted-the-object"></a>cliente de Hello u otro proceso haya eliminado previamente objeto Hola
En escenarios donde está intentando cliente hello tooread, actualizar o eliminar datos en un servicio de almacenamiento suele ser fácil tooidentify en hello en el servidor registra una operación anterior que elimine objeto hello en cuestión del servicio de almacenamiento de Hola. Muy a menudo, los datos de registro de hello muestran ese objeto de hello eliminado otro usuario o proceso. En el registro de registro de almacenamiento de servidor de Hola Hola tipo de operación y las columnas de clave del objeto solicitado muestran cuando un cliente elimina un objeto.

En el escenario de Hola donde un cliente está intentando tooinsert un objeto, puede no ser tan evidente por qué esto da como resultado una respuesta HTTP 404 (no encontrado) dado que hello cliente es crear un nuevo objeto. Sin embargo, si cliente hello es crear un blob debe ser toofind capaz de contenedor de blobs de Hola, cliente hello es crear un mensaje debe ser capaz de toofind una cola, y si el cliente de hello consiste en Agregar una fila debe ser capaz de toofind tabla de Hola.

Puede usar el registro del lado cliente Hola de hello biblioteca cliente de almacenamiento toogain que una más detallada descripción de cuando el cliente de hello envía solicitudes específicas toohello servicio de almacenamiento.

Hello siguiente registro del lado cliente generado por la biblioteca de cliente de almacenamiento de hello muestra hello problema al cliente hello no encuentra el contenedor de hello para el blob de saludo que está creando. Este registro incluye detalles de hello las siguientes operaciones de almacenamiento:

| Id. de solicitud | Operación |
| --- | --- |
| 07b26a5d-... |**DeleteIfExists** contenedor de blobs de método toodelete Hola. Tenga en cuenta que esta operación incluye un **HEAD** solicitar toocheck existencia de Hola de contenedor de Hola. |
| e2d06d78… |**CreateIfNotExists** contenedor de blobs de método toocreate Hola. Tenga en cuenta que esta operación incluye un **HEAD** solicitud que comprueba la existencia de Hola de contenedor de Hola. Hola **HEAD** devuelve un mensaje de 404 pero continúa. |
| de8b1c3c-... |**UploadFromStream** blob de método toocreate Hola. Hola **colocar** se produce un error en la solicitud con un mensaje 404 |

Entradas del registro:

| Id. de solicitud | Texto de operación |
| --- | --- |
| 07b26a5d-... |Iniciando la solicitud sincrónica toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer. |
| 07b26a5d-... |StringToSign = HEAD............x-ms-client-request-id:07b26a5d-....x-ms-date:Tue, 03 Jun 2014 10:33:11 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |Esperando respuesta. |
| 07b26a5d-... |Respuesta recibida. Status code = 200, Request ID = eeead849-...Content-MD5 = , ETag =    &quot;0x8D14D2DC63D059B&quot;. |
| 07b26a5d-... |Encabezados de respuesta se han procesado correctamente, continuando con el resto de Hola de operación de Hola. |
| 07b26a5d-... |Descargando el cuerpo de respuesta. |
| 07b26a5d-... |Operación completada correctamente. |
| 07b26a5d-... |Iniciando la solicitud sincrónica toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer. |
| 07b26a5d-... |StringToSign = DELETE............x-ms-client-request-id:07b26a5d-....x-ms-date:Tue, 03 Jun 2014 10:33:12    GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |Esperando respuesta. |
| 07b26a5d-... |Respuesta recibida. Código de estado = 202, Id. de solicitud = 6ab2a4cf-..., Content-MD5 = , ETag = . |
| 07b26a5d-... |Encabezados de respuesta se han procesado correctamente, continuando con el resto de Hola de operación de Hola. |
| 07b26a5d-... |Descargando el cuerpo de respuesta. |
| 07b26a5d-... |Operación completada correctamente. |
| e2d06d78-... |Iniciando la solicitud asincrónica toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer.</td> |
| e2d06d78-... |StringToSign = HEAD............x-ms-client-request-id:e2d06d78-....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |Esperando respuesta. |
| de8b1c3c-... |Iniciando la solicitud sincrónica toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer/blobCreated.txt. |
| de8b1c3c-... |StringToSign = PUT...64.qCmF+TQLPhq/YYK50mP9ZQ==........x-ms-blob-type:BlockBlob.x-ms-client-request-id:de8b1c3c-....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer/blobCreated.txt. |
| de8b1c3c-... |Preparar los datos de la solicitud de toowrite. |
| e2d06d78-... |Excepción que se produce mientras se espera respuesta: servidor remoto hello devolvió un error: (404) no se encuentra... |
| e2d06d78-... |Respuesta recibida. Código de estado = 404, Id. de solicitud = 353ae3bc-..., Content-MD5 = , ETag = . |
| e2d06d78-... |Encabezados de respuesta se han procesado correctamente, continuando con el resto de Hola de operación de Hola. |
| e2d06d78-... |Descargando el cuerpo de respuesta. |
| e2d06d78-... |Operación completada correctamente. |
| e2d06d78-... |Iniciando la solicitud asincrónica toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer. |
| e2d06d78-... |StringToSign = PUT...0.........x-ms-client-request-id:e2d06d78-....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |Esperando respuesta. |
| de8b1c3c-... |Escribiendo datos de solicitud. |
| de8b1c3c-... |Esperando respuesta. |
| e2d06d78-... |Excepción que se produce mientras se espera respuesta: servidor remoto hello devolvió un error: (409) conflicto... |
| e2d06d78-... |Respuesta recibida. Código de estado = 409, Id. de solicitud = c27da20e-..., Content-MD5 = , ETag = . |
| e2d06d78-... |Descargando el cuerpo de respuesta del error. |
| de8b1c3c-... |Excepción que se produce mientras se espera respuesta: servidor remoto hello devolvió un error: (404) no se encuentra... |
| de8b1c3c-... |Respuesta recibida. Código de estado = 404, Id. de solicitud = 0eaeab3e-..., Content-MD5 = , ETag = . |
| de8b1c3c-... |Excepción que se produce durante la operación de hello: servidor remoto hello devolvió un error: (404) no se encuentra... |
| de8b1c3c-... |La directiva de reintentos no permitió un reintento. Error con el servidor remoto hello devolvió un error: (404) no se encuentra... |
| e2d06d78-... |La directiva de reintentos no permitió un reintento. Error con el servidor remoto hello devolvió un error: (409) conflicto... |

En este ejemplo, el registro de hello muestra ese cliente hello es una intercalación de las solicitudes de hello **CreateIfNotExists** método (... e2d06d78 de Id. de solicitud) con las solicitudes de Hola de hello **UploadFromStream** () (método) de8b1c3c-...); Esto ocurre porque la aplicación de cliente de hello es invocar estos métodos de forma asincrónica. Debe modificar el código asincrónico de hello en hello tooensure de cliente que crea el contenedor de hello antes de intentar tooupload cualquier blob tooa de datos en ese contenedor. Lo ideal es que cree todos los contenedores de antemano.

#### <a name="SAS-authorization-issue"></a>Un problema de autorización de Firma de acceso compartido (SAS)
Si trata de aplicación de cliente hello toouse una clave SAS que no incluya Hola permisos necesarios para la operación de hello, servicio de almacenamiento de hello devuelve a un cliente de toohello de mensaje HTTP 404 (no encontrado). En hello mismo tiempo, también verá un valor distinto de cero para **error SASAuthorizationError** de métricas de Hola.

Hello en la tabla siguiente muestra un mensaje de registro de servidor de ejemplo de archivo de registro de registro de almacenamiento de hello:

| Nombre | Valor |
| --- | --- |
| Hora de inicio de la solicitud | 2014-05-30T06:17:48.4473697Z |
| Tipo de operación     | GetBlobProperties            |
| Estado de la solicitud     | SASAuthorizationError        |
| Código de estado HTTP   | 404                          |
| Tipo de autenticación| Sas                          |
| Tipo de servicio       | Blob                         |
| URL de la solicitud        | https://domemaildist.blob.core.windows.net/azureimblobcontainer/blobCreatedViaSAS.txt |
| nbsp;              |   ?sv=2014-02-14&sr=c&si=mypolicy&sig=XXXXX&;api-version=2014-02-14 |
| Encabezado de id. de solicitud  | a1f348d5-8032-4912-93ef-b393e5252a3b |
| Id. de solicitud de cliente  | 2d064953-8436-4ee0-aa0c-65cb874f7929 |

Debería investigar por qué intenta tooperform una operación no tiene permisos para la aplicación cliente.

#### <a name="JavaScript-code-does-not-have-permission"></a>Código de JavaScript del lado cliente no tiene el objeto de permiso tooaccess Hola
Si está utilizando a un cliente de JavaScript y el servicio de almacenamiento de hello devuelve mensajes de HTTP 404, busque Hola siguientes errores de JavaScript en el Explorador de hello:

```
SEC7120: Origin http://localhost:56309 not found in Access-Control-Allow-Origin header.
SCRIPT7002: XMLHttpRequest: Network Error 0x80070005, Access is denied.
```

> [!NOTE]
> Puede usar herramientas de desarrollo F12 de hello en Internet Explorer tootrace Hola mensajes intercambiados entre el Explorador de Hola y el servicio de almacenamiento de hello cuando esté solucionando problemas de JavaScript del lado cliente.
> 
> 

Estos errores se producen porque el Explorador de web Hola implementa hello <a href="http://www.w3.org/Security/wiki/Same_Origin_Policy" target="_blank">directiva de mismo origen</a> procede de restricción de seguridad que impide que una página web de la llamada a una API en un dominio distinto de la página de Hola Hola dominio.

toowork alrededor de hello problema de JavaScript, puede configurar recursos entre orígenes de uso compartido (CORS) para el cliente de Hola de servicio de almacenamiento de hello tiene acceso a. Para más información, consulte <a href="http://msdn.microsoft.com/library/azure/dn535601.aspx" target="_blank">Compatibilidad con Uso compartido de recursos entre orígenes (CORS) para los Servicios de almacenamiento de Azure</a> en MSDN.

Hola siguiendo el ejemplo de código muestra cómo tooconfigure el blob service tooallow JavaScript que se ejecuta en hello tooaccess de dominio de Contoso un blob en el servicio de almacenamiento de blobs:

```csharp
CloudBlobClient client = new CloudBlobClient(blobEndpoint, new StorageCredentials(accountName, accountKey));
// Set hello service properties.
ServiceProperties sp = client.GetServiceProperties();
sp.DefaultServiceVersion = "2013-08-15";
CorsRule cr = new CorsRule();
cr.AllowedHeaders.Add("*");
cr.AllowedMethods = CorsHttpMethods.Get | CorsHttpMethods.Put;
cr.AllowedOrigins.Add("http://www.contoso.com");
cr.ExposedHeaders.Add("x-ms-*");
cr.MaxAgeInSeconds = 5;
sp.Cors.CorsRules.Clear();
sp.Cors.CorsRules.Add(cr);
client.SetServiceProperties(sp);
```

#### <a name="network-failure"></a>Error de red
En algunas circunstancias, paquetes de red perdidas pueden provocar servicio de almacenamiento de toohello devolverá a cliente de toohello de mensajes HTTP 404. Por ejemplo, cuando la aplicación cliente está eliminando una entidad de servicio de la tabla de hello verá cliente hello producir una excepción de almacenamiento reporting un "HTTP 404 (no encontrado)" mensajes de estado de servicio de la tabla de Hola. Cuando se investiga tabla hello en el servicio de almacenamiento de tabla de hello, verá que el servicio de Hola eliminara entidad hello cuando se le solicite.

detalles de la excepción de Hello en el cliente de hello incluyen Id. de solicitud de hello (7e84f12d...) asignado por el servicio de la tabla de hello para la solicitud de hello: puede usar esta detalles de la solicitud de la información toolocate hello en los registros de almacenamiento de servidor hello mediante la búsqueda en hello  **encabezado de Id. de solicitud** columna en el archivo de registro de hello. También podría utilizar Hola métricas tooidentify cuando errores como este se producen y, a continuación, buscar en archivos de registro de hello en función de las métricas de hello tiempo Hola registran este error. Esta muestra de entrada de registro que Hola delete error con un mensaje de estado de "Cliente otro Error HTTP (404)". Hello misma entrada de registro también incluye Id. de solicitud de hello generado por el cliente de Hola Hola **Id. de solicitud de cliente** columna (813ea74f...).

registro del lado servidor Hello también incluye otra entrada con hello mismo **Id. de solicitud de cliente** para la operación de eliminación de valor (813ea74f...) para una correcta Hola misma entidad y de Hola mismo cliente. Esta operación de eliminación correcta tuvo lugar muy poco tiempo antes de la solicitud de error al eliminar Hola.

Hola más probable de este escenario es ese cliente hello enviado una solicitud de eliminación de servicio tabla de hello entidad toohello, que se realizó correctamente, pero no recibió una confirmación del servidor hello (quizás debido tooa problema de red temporal). cliente de Hello, a continuación, reintentó automáticamente la operación de hello (utilizando Hola mismo **Id. de solicitud de cliente**), y este reintento error porque ya se eliminó la entidad de Hola.

Si este problema se produce con frecuencia, debería investigar por qué el cliente hello no puede tooreceive confirmaciones de servicio de la tabla de Hola. Si el problema de hello es intermitente, debe intercepta el error de "HTTP (404) no encontrado" hello y registrarlo en el cliente de hello, pero permitir Hola cliente toocontinue.

### <a name="the-client-is-receiving-409-messages"></a>cliente de Hello está recibiendo mensajes de HTTP 409 (conflicto)
Hello tabla siguiente muestra un extracto del registro del lado servidor hello para dos operaciones de cliente: **DeleteIfExists** seguido inmediatamente por **CreateIfNotExists** utilizando Hola el mismo nombre de contenedor de blob. Tenga en cuenta que cada cliente operación da como resultado dos solicitudes enviadas toohello server, en primer lugar un **GetContainerProperties** toocheck solicitud si existe el contenedor de hello, seguido de hello **DeleteContainer** o  **CreateContainer** solicitud.

| Timestamp | Operación | Resultado | Nombre del contenedor | Id. de solicitud de cliente |
| --- | --- | --- | --- | --- |
| 05:10:13.7167225 |GetContainerProperties |200 |mmcont |c9f52c89-… |
| 05:10:13.8167325 |DeleteContainer |202 |mmcont |c9f52c89-… |
| 05:10:13.8987407 |GetContainerProperties |404 |mmcont |bc881924-… |
| 05:10:14.2147723 |CreateContainer |409 |mmcont |bc881924-… |

elimina Hello código de aplicación de cliente de hello y, a continuación, inmediatamente vuelve a crear un contenedor de blob mediante Hola homónimas: Hola **CreateIfNotExists** método (solicitud de cliente ID bc881924-...) al final se produce un error con hello HTTP 409 (conflicto) error. Cuando un cliente elimina contenedores de blobs, tablas o las colas que hay un breve período antes de nombre de hello vuelva a estar disponible.

aplicación de cliente de Hello debe usar nombres de contenedor único cada vez que crea nuevos contenedores si Hola eliminar y volver a crear patrón es habitual.

### <a name="metrics-show-low-percent-success"></a>Las métricas muestran un PercentSuccess bajo o las entradas de registro de análisis tienen operaciones con el estado de transacción ClientOtherErrors
Hola **PercentSuccess** métrica captura el porcentaje de Hola de operaciones que se obtuvieron resultados satisfactorios en función de su código de estado HTTP. Las operaciones con códigos de estado de 2XX cuentan como correctas, mientras que las operaciones con códigos de estado en intervalos 3XX, 4XX y 5XX se cuentan como Hola incorrecta e inferior **PercentSucess** valor de métrica. En archivos de registro de almacenamiento de servidor de hello, estas operaciones se registran con un estado de transacción **ClientOtherErrors**.

Es importante toonote que estas operaciones se han completado correctamente y, por tanto, no afectan a otras métricas, como la disponibilidad. Algunos ejemplos de operaciones que se ejecutan correctamente, pero que pueden provocar códigos de estado HTTP incorrectos:

* **ResourceNotFound** (no encontrado 404), por ejemplo de una operación GET solicitud tooa blob que no existe.
* **ResouceAlreadyExists** (409 Conflicto), por ejemplo, de un **CreateIfNotExist** operación donde recursos Hola ya existe.
* **ConditionNotMet** (no modificado 304), por ejemplo, de una operación condicional, como cuando un cliente envía una **ETag** valor y HTTP **If-None-Match** encabezado toorequest una imagen solo si se ha actualizado desde la última operación de Hola.

Puede encontrar una lista de códigos de error comunes de API de REST que devuelven los servicios de almacenamiento de hello en la página de hello <a href="http://msdn.microsoft.com/library/azure/dd179357.aspx" target="_blank">códigos de Error de API de REST comunes</a>.

### <a name="capacity-metrics-show-an-unexpected-increase"></a>Las métricas de capacidad muestran un aumento inesperado en el uso de la capacidad de almacenamiento
Si ve repentinos, cambios inesperados en el uso de la capacidad de su cuenta de almacenamiento, puede investigar los motivos de hello mirando las métricas de disponibilidad; Por ejemplo, un aumento en número de Hola de solicitudes de eliminación no podría provocar tooan aumento en la cantidad de Hola de almacenamiento de blobs que se va a utilizar como operaciones de limpieza específico de aplicación que podría haber esperado toobe liberar espacio no funcione según lo esperado (para ejemplo, dado que han expirado tokens SAS de hello utilizados para la liberación de espacio).

### <a name="you-are-experiencing-unexpected-reboots"></a>Se producen reinicios inesperados de Máquinas virtuales de Azure que tienen muchos VHD adjuntos
Si una máquina Virtual (VM) de Azure tiene un gran número de discos duros virtuales conectados que se encuentran en hello misma cuenta de almacenamiento, podría superar los objetivos de escalabilidad de Hola de una cuenta de almacenamiento individuales provocando Hola VM toofail. Debe comprobar las métricas de minuto de Hola Hola cuenta de almacenamiento (**TotalRequests**/**TotalIngress**/**TotalEgress**) para picos que superan los objetivos de escalabilidad de Hola de una cuenta de almacenamiento. Consulte la sección de Hola "[métricas muestran un aumento en PercentThrottlingError]" para obtener ayuda para determinar si la limitación se ha producido en su cuenta de almacenamiento.

En general, cada entrada individual o la operación de salida en un disco duro virtual de una máquina Virtual se traduce demasiado**página obtenga** o **Put Page** operaciones en hello subyacente blob en páginas. Por lo tanto, puede usar Hola IOPS calculadas para su entorno tootune cuántos discos duros virtuales que puede tener en una única cuenta de almacenamiento en función de un comportamiento específico de la aplicación hello. No recomendamos tener más de 40 discos en una sola cuenta de almacenamiento. Vea <a href="http://msdn.microsoft.com/library/azure/dn249410.aspx" target="_blank">objetivos de rendimiento y escalabilidad de almacenamiento de Azure</a> para obtener detalles de los objetivos de escalabilidad actual de hello las cuentas de almacenamiento, en particular Hola solicitud total tasa total de ancho de banda y para el tipo de saludo de la cuenta de almacenamiento que usa .
Si se supera los objetivos de escalabilidad de hello para la cuenta de almacenamiento, debería colocar los VHD en actividad del hello de tooreduce de cuentas de varios almacenamiento diferente en cada cuenta individual.

### <a name="your-issue-arises-from-using-the-storage-emulator"></a>El problema surge de mediante el emulador de almacenamiento de hello para el desarrollo o de prueba
Normalmente utilizará el emulador de almacenamiento de Hola durante el desarrollo y probar tooavoid Hola requisito para una cuenta de almacenamiento de Azure. Hola problemas comunes que pueden producirse cuando se usa el emulador de almacenamiento de hello son:

* [Función "X" no funciona en el emulador de almacenamiento de Hola]
* [Error "valor de Hola para uno de los encabezados HTTP de Hola no está en formato correcto de hello" al usar Hola emulador de almacenamiento]
* [Emulador en ejecución Hola almacenamiento requiere privilegios administrativos]

#### <a name="feature-X-is-not-working"></a>Función "X" no funciona en el emulador de almacenamiento de Hola
emulador de almacenamiento de Hello no admite todas las características de hello de servicios de almacenamiento de Azure de hello como servicio de archivos de Hola. Para obtener más información, consulte <a href="http://msdn.microsoft.com/library/azure/gg433135.aspx" target="_blank">hello las diferencias entre el emulador de almacenamiento y los servicios de almacenamiento de Azure</a> en MSDN.

Para aquellas características que Hola almacenamiento emulador no admite, usar el servicio de almacenamiento de Azure de hello en nube de Hola.

#### <a name="error-HTTP-header-not-correct-format"></a>Error "valor de Hola para uno de los encabezados HTTP de Hola no está en formato correcto de hello" al usar Hola emulador de almacenamiento
Va a probar la aplicación que utilizan Hola biblioteca cliente de almacenamiento contra Hola almacenamiento local emulador y llamadas a métodos como **CreateIfNotExists** producirá un error error Hola mensaje "valor de Hola para uno de los encabezados de hello HTTP no está en formato de Hello correcto." Esto indica que Hola versión Hola del emulador de almacenamiento que usa no admite la versión de Hola de biblioteca de cliente de almacenamiento de Hola que usa. Hola biblioteca cliente de almacenamiento agrega el encabezado de hello **x-ms-version** tooall Hola solicita hace. Si el emulador de almacenamiento de hello no reconocer el valor de hello en hello **x-ms-version** encabezado, se rechaza la solicitud de saludo.

Puede usar valor Hola cliente de bibliotecas de almacenamiento registros toosee Hola de hello **encabezado x-ms-version** está enviando. También puede ver el valor de Hola de hello **encabezado x-ms-version** si utiliza solicitudes de Fiddler tootrace Hola desde la aplicación cliente.

Este suele ser el caso si instalar y usar la versión más reciente de Hola de hello biblioteca cliente de almacenamiento sin actualizar el emulador de almacenamiento de Hola. Debe instalar la versión más reciente de Hola Hola del emulador de almacenamiento o usar almacenamiento en nube en lugar de emulador de hello para el desarrollo y prueba.

#### <a name="storage-emulator-requires-administrative-privileges"></a>Emulador en ejecución Hola almacenamiento requiere privilegios administrativos
Se pedirá las credenciales de administrador cuando se ejecuta el emulador de almacenamiento de Hola. Esto sólo ocurre cuando se inicializan emulador de almacenamiento de Hola para hello primera vez. Después de haber inicializado emulador de almacenamiento de hello, no necesita privilegios de administrador toorun vuelva a.

Para obtener más información, consulte <a href="http://msdn.microsoft.com/library/azure/gg433132.aspx" target="_blank">Initialize Hola emulador de almacenamiento por hello mediante la herramienta de línea de comandos</a> en MSDN (también se puede inicializar el emulador de almacenamiento de hello en Visual Studio, lo que también requiere privilegios de administrador).

### <a name="you-are-encountering-problems-installing-the-Windows-Azure-SDK"></a>Se están produciendo problemas para instalar hello Azure SDK para .NET
Cuando intente tooinstall Hola SDK, no puede tratar de emulador de almacenamiento de hello tooinstall en el equipo local. registro de instalación de Hello contiene uno de los siguientes mensajes de Hola:

* CAQuietExec: Error: instancia de SQL no se puede tooaccess
* CAQuietExec: Error: no se puede toocreate base de datos

causa de Hello es un problema con la instalación de LocalDB existente. De forma predeterminada, emulador de almacenamiento de hello usa LocalDB toopersist datos cuando simula los servicios de almacenamiento de Azure Hola. Puede restablecer la instancia de LocalDB mediante la ejecución de hello siga los comandos en una ventana del símbolo del sistema antes de intentar tooinstall Hola SDK.

```
sqllocaldb stop v11.0
sqllocaldb delete v11.0
delete %USERPROFILE%\WAStorageEmulatorDb3*.*
sqllocaldb create v11.0
```

Hola **eliminar** comando quita los archivos de base de datos antiguos de las instalaciones anteriores Hola del emulador de almacenamiento.

### <a name="you-have-a-different-issue-with-a-storage-service"></a>Tiene otro problema distinto relacionado con un servicio de almacenamiento
Si secciones de solución de problemas anteriores hello no incluyen problema hello que tiene con un servicio de almacenamiento, debería adoptar Hola sigue toodiagnosing de enfoque y solucionar el problema.

* Compruebe su toosee de métricas si hay algún cambio en el comportamiento esperado de la línea de base. De las métricas de hello, es posible que pueda toodetermine si el problema de hello es temporal o permanente, y qué operaciones de almacenamiento Hola problema está afectando a.
* Puede utilizar información de las métricas de hello toohelp buscar los datos de registro de servidor para obtener más información acerca de los errores que se producen. Esta información puede ayudarle a solucionar problemas y resolver el problema de Hola.
* Si información de hello en los registros de servidor hello no es suficiente problema de hello tootroubleshoot correctamente, puede utilizar Hola biblioteca cliente de almacenamiento registros del lado cliente tooinvestigate Hola comportamiento de la aplicación cliente y las herramientas como Fiddler, Wireshark, y el analizador de mensajes de Microsoft tooinvestigate la red.

Para obtener más información acerca del uso de Fiddler, vea "[apéndice 1: tráfico HTTP y HTTPS toocapture utilizando Fiddler]."

Para obtener más información acerca del uso de Wireshark, vea "[apéndice 2: el tráfico de red de uso Wireshark toocapture]."

Para obtener más información acerca de cómo utilizar el analizador de mensajes de Microsoft, vea "[apéndice 3: el tráfico de red usando el analizador de mensajes de Microsoft toocapture]."

## <a name="appendices"></a>Apéndices
apéndices Hola describen varias herramientas que pueden resultarle útiles para diagnosticar y solucionar problemas con el almacenamiento de Azure (y otros servicios). Estas herramientas no forman parte de Almacenamiento de Azure y algunas son productos de terceros. Por lo tanto, herramientas de Hola se describe en estos apéndices no están cubiertas por un contrato de soporte técnico que pudiera haber suscrito con Microsoft Azure o almacenamiento de Azure y, por tanto, como parte del proceso de evaluación, debe examinar opciones de licencia y soporte técnico de hello disponibles en proveedores de Hola de estas herramientas.

### <a name="appendix-1"></a>Apéndice 1: Usar Fiddler toocapture HTTP y el tráfico HTTPS
Fiddler es una herramienta útil para analizar el tráfico HTTP y HTTPS de hello entre la aplicación de cliente y Hola que usa el servicio de almacenamiento de Azure. Puede descargar Fiddler desde <a href="http://www.telerik.com/fiddler" target="_blank">http://www.telerik.com/fiddler</a>.

> [!NOTE]
> Fiddler puede descodificar el tráfico HTTPS; se debe leer detenidamente la documentación de Fiddler hello toounderstand cómo lo hace esto y las implicaciones de seguridad de toounderstand Hola.
> 
> 

Este apéndice proporciona una breve explicación de cómo tooconfigure Fiddler toocapture tráfico entre el equipo local de Hola donde se ha instalado a Fiddler y Hola servicios de almacenamiento de Azure.

Una vez iniciado Fiddler, empezará a capturar el tráfico HTTP y HTTPS de la máquina local. siguiente Hola es algunos comandos útiles para controlar Fiddler:

* Dejar de capturar tráfico y empezar a capturarlo. En el menú principal de hello, vaya demasiado**archivo** y, a continuación, haga clic en **capturar tráfico** tootoggle captura activar y desactivar.
* Guardar los datos de tráfico capturados. En el menú principal de hello, vaya demasiado**archivo**, haga clic en **guardar**y, a continuación, haga clic en **todas las sesiones**: Esto permite tráfico de hello toosave en un archivo de sesión. Puede volver a cargar un archivo de sesión más adelante para el análisis o enviarlo si solicitó la admisión de tooMicrosoft.

cantidad de hello toolimit de tráfico que captura de Fiddler, puede usar los filtros que configure en hello **filtros** Hola de ficha siguiente captura de pantalla muestra un filtro que captura solo toohello el tráfico enviado  **contosoemaildist.Table.Core.Windows.NET** punto de conexión de almacenamiento:

![][5]

### <a name="appendix-2"></a>Apéndice 2: Uso de tráfico de red de Wireshark toocapture
Wireshark es un analizador de protocolos de red que permite tooview paquete información detallada para una amplia variedad de protocolos de red. Puede descargar Wireshark de <a href="http://www.wireshark.org/" target="_blank">http://www.wireshark.org/</a>.

Hello siguiente procedimiento muestra cómo toocapture paquete información detallada para el tráfico de la máquina local Hola donde instaló el servicio de tabla Wireshark toohello en su cuenta de almacenamiento de Azure.

1. Inicie Wireshark en la máquina local.
2. Hola **iniciar** sección, interfaz de red local de hello select u otras interfaces que son toohello conectado internet.
3. Haga clic en **Capture Options**(Opciones de captura).
4. Agregar un filtro toohello **filtro de captura** cuadro de texto. Por ejemplo, **host contosoemaildist.table.core.windows.net** configurará Wireshark toocapture sólo paquetes envían tooor de extremo de servicio de tabla Hola Hola **contosoemaildist** almacenamiento cuenta. Para ver una lista completa de los filtros de captura, consulte <a href="http://wiki.wireshark.org/CaptureFilters" target="_blank">http://wiki.wireshark.org/CaptureFilters</a>.
   
   ![][6]
5. Haga clic en **Iniciar**. Wireshark ahora capturará todos los tooor de envío de paquetes Hola de extremo de servicio de tabla de Hola que usa la aplicación cliente en el equipo local.
6. Cuando haya terminado, en haga clic en el menú principal de hello **capturar** y, a continuación, **detener**.
7. Hola toosave captura datos en un archivo de captura Wireshark, en haga clic en el menú principal de hello **archivo** y, a continuación, **guardar**.

WireShark resaltará cualquier error que existen en hello **packetlist** ventana. También puede usar hello **experto información** ventana (haga clic en **analizar**, a continuación, **experto en información**) tooview un resumen de errores y advertencias.

![][7]

También puede elegir datos TCP de hello tooview como capa de aplicación Hola la ve, haga doble clic en datos TCP de Hola y seleccione **siga flujo TCP**. Resulta especialmente útil si capturó el volcado sin un filtro de captura. Obtenga más información <a href="http://www.wireshark.org/docs/wsug_html_chunked/ChAdvFollowTCPSection.html" target="_blank">aquí</a>.

![][8]

> [!NOTE]
> Para obtener más información acerca del uso de Wireshark, vea hello <a href="http://www.wireshark.org/docs/wsug_html_chunked/" target="_blank">manual del usuario de Wireshark</a>.
> 
> 

### <a name="appendix-3"></a>Apéndice 3: Uso de tráfico de red de toocapture de analizador de mensajes de Microsoft
Puede usar analizador de mensajes de Microsoft toocapture HTTP y el tráfico HTTPS en un tooFiddler de manera similar y capturar el tráfico de red en un tooWireshark de manera similar.

#### <a name="configure-a-web-tracing-session-using-microsoft-message-analyzer"></a>Configurar una sesión de traza web con el Analizador de mensajes de Microsoft
tooconfigure una sesión de seguimiento de web para el tráfico HTTP y HTTPS con el analizador de mensajes de Microsoft, ejecutar la aplicación analizador de mensajes de Microsoft de hello y, a continuación, en hello **archivo** menú, haga clic en **/seguimiento de captura**. En la lista Hola de escenarios de seguimiento disponibles, seleccione **Proxy Web**. A continuación, en hello **configuración del escenario de seguimiento** panel Hola **HostnameFilter** cuadro de texto, agregue nombres de Hola de los extremos de almacenamiento (puede buscar estos nombres Hola Portal clásico de Azure). Por ejemplo, si hello nombre de la cuenta de almacenamiento de Azure es **contosodata**, debe agregar Hola después toohello **HostnameFilter** cuadro de texto:

```
contosodata.blob.core.windows.net contosodata.table.core.windows.net contosodata.queue.core.windows.net
```

> [!NOTE]
> Un carácter de espacio separa los nombres de host de Hola.
> 
> 

Cuando esté listo toostart recopilar datos de seguimiento, haga clic en hello **Start With** botón.

Para obtener más información acerca de hello analizador de mensajes de Microsoft **Proxy Web** de seguimiento, vea <a href="http://technet.microsoft.com/library/jj674814.aspx" target="_blank">PEF WebProxy proveedor</a> en TechNet.

Hola integrado **Proxy Web** seguimiento de analizador de mensajes de Microsoft se basa en Fiddler; puede capturar el tráfico HTTPS de cliente y mostrar mensajes HTTPS sin cifrar. Hola **Proxy Web** seguimiento funciona mediante la configuración de un servidor proxy local para todo el tráfico HTTP y HTTPS que proporciona acceso toounencrypted mensajes.

#### <a name="diagnosing-network-issues-using-microsoft-message-analyzer"></a>Diagnóstico de problemas de red con el Analizador de mensajes de Microsoft
Además toousing Hola analizador de mensajes de Microsoft **Proxy Web** toocapture detalles del seguimiento de Hola tráfico HTTP/HTTPs entre la aplicación de cliente de Hola y el servicio de almacenamiento de hello, también puede usar Hola integrada  **Nivel de vínculo local** toocapture red paquete información de seguimiento. Esto permite toocapture datos similares toothat que se puede capturar con Wireshark y diagnosticar problemas de red, como los paquetes perdidos.

Hello captura de pantalla siguiente muestra un ejemplo **capa de vínculo Local** seguimiento junto con algunos **informativo** mensajes de Hola **DiagnosisTypes** columna. Al hacer clic en un icono de hello **DiagnosisTypes** columna muestra los detalles de Hola de mensaje de bienvenida. En este ejemplo, servidor hello retransmite mensajes #305 porque no recibió una confirmación de cliente hello:

![][9]

Cuando se crea la sesión de seguimiento de hello en Analizador de mensajes de Microsoft, puede especificar la cantidad de Hola de tooreduce de filtros de ruido en seguimiento de Hola. En hello **capturar / seguimiento** página donde se define el seguimiento de hello, haga clic en hello **configurar** vincular a continuación demasiado**PacketCapture-Microsoft-Windows-NDIS**. Hola siguiente captura de pantalla muestra una configuración que filtra el tráfico TCP para las direcciones IP de Hola de tres de los servicios de almacenamiento:

![][10]

Para obtener más información acerca de hello seguimiento de nivel de vínculo Local de analizador de mensajes de Microsoft, consulte <a href="http://technet.microsoft.com/library/jj659264.aspx" target="_blank">PacketCapture de NDIS de PEF proveedor</a> en TechNet.

### <a name="appendix-4"></a>Apéndice 4: Usar tooview métricas y registro de datos de Excel
Muchas herramientas le permiten datos de métricas de almacenamiento de hello toodownload desde el almacenamiento de tabla de Azure en un formato delimitado que se convierte datos de hello tooload fácil en Excel para ver y el análisis. Los datos de registro de Almacenamiento del almacenamiento de BLOB de Azure ya están en un formato delimitado que puede cargar en Excel. Sin embargo, tendrá los encabezados de columna apropiados tooadd basados en información de hello en <a href="http://msdn.microsoft.com/library/azure/hh343259.aspx" target="_blank">formato de registro de análisis de almacenamiento</a> y <a href="http://msdn.microsoft.com/library/azure/hh343264.aspx" target="_blank">esquema de tabla de métricas de análisis de almacenamiento</a>.

tooimport los datos de registro de almacenamiento en Excel después de descargarlo desde el almacenamiento de blobs:

* En hello **datos** menú, haga clic en **de texto**.
* Archivo de registro toohello de examen que desee tooview y haga clic en **importación**.
* En el paso 1 de hello **Asistente para importar texto**, seleccione **delimitado**.

En el paso 1 de hello **Asistente para importar texto**, seleccione **punto y coma** como Hola solo delimitador y elija comillas dobles como hello **calificador de texto**. A continuación, haga clic en **finalizar** y elija donde tooplace Hola datos del libro.

### <a name="appendix-5"></a>Apéndice 5: Supervisión de Visual Studio Team Services mediante Application Insights
También puede utilizar la característica de hello Application Insights para Visual Studio Team Services como parte de la supervisión del rendimiento y disponibilidad. Esta herramienta puede:

* Comprobar que el servicio web está disponible y responde adecuadamente. Si la aplicación es un sitio web o una aplicación para dispositivos que utiliza un servicio web, puede probar la dirección URL de cada pocos minutos desde ubicaciones alrededor de Hola a todos y le indicará si hay un problema.
* Diagnosticar rápidamente los problemas de rendimiento o las excepciones del servicio web. Averigüe si la CPU u otros recursos se están ampliando, observe el seguimiento de la pila de las excepciones y busque fácilmente en los seguimientos de registros. Si hello disminución del rendimiento de la aplicación por debajo de los límites aceptables, podemos enviarle un correo electrónico. Puede supervisar servicios web de .NET y de Java.

En hello tiempo de la escritura de Application Insights está en vista previa. Podrá encontrar más información en <a href="http://msdn.microsoft.com/library/azure/dn481095.aspx" target="_blank">Application Insights para Visual Studio Team Services en MSDN</a>.

<!--Anchors-->
[Introducción]: #introduction
[Organización de la guía]: #how-this-guide-is-organized

[el servicio de almacenamiento de supervisión]: #monitoring-your-storage-service
[Supervisión del estado del servicio]: #monitoring-service-health
[Supervisión de la capacidad]: #monitoring-capacity
[Supervisión de la disponibilidad]: #monitoring-availability
[Supervisión del rendimiento]: #monitoring-performance

[diagnosticar problemas de almacenamiento]: #diagnosing-storage-issues
[Problemas de estado del servicio]: #service-health-issues
[Problemas de rendimiento]: #performance-issues
[Diagnóstico de errores]: #diagnosing-errors
[Problemas del emulador de almacenamiento]: #storage-emulator-issues
[Herramientas de registro de almacenamiento]: #storage-logging-tools
[Uso de herramientas de registro de red]: #using-network-logging-tools

[seguimiento to-end]: #end-to-end-tracing
[Correlación de datos de registro]: #correlating-log-data
[Id. de solicitud de cliente]: #client-request-id
[Id. de solicitud de servidor]: #server-request-id
[Marcas de tiempo]: #timestamps

[Guía de solución de problemas]: #troubleshooting-guidance
[métricas muestran AverageE2ELatency alta y baja AverageServerLatency]: #metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency
[Métricas muestran AverageE2ELatency baja y baja AverageServerLatency pero cliente hello está experimentando una latencia alta]: #metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency
[Las métricas muestran una AverageServerLatency alta]: #metrics-show-high-AverageServerLatency
[Observa retrasos inesperados en la entrega de mensajes de una cola]: #you-are-experiencing-unexpected-delays-in-message-delivery

[métricas muestran un aumento en PercentThrottlingError]: #metrics-show-an-increase-in-PercentThrottlingError
[Aumento transitorio de PercentThrottlingError]: #transient-increase-in-PercentThrottlingError
[Aumento permanente del error PercentThrottlingError]: #permanent-increase-in-PercentThrottlingError
[métricas muestran un aumento en PercentTimeoutError]: #metrics-show-an-increase-in-PercentTimeoutError
[Las métricas muestran un aumento de PercentNetworkError]: #metrics-show-an-increase-in-PercentNetworkError

[cliente de Hello está recibiendo mensajes de HTTP 403 (prohibido)]: #the-client-is-receiving-403-messages
[cliente de Hello está recibiendo mensajes de HTTP 404 (no encontrado)]: #the-client-is-receiving-404-messages
[cliente de Hello u otro proceso haya eliminado previamente objeto Hola]: #client-previously-deleted-the-object
[Un problema de autorización de Firma de acceso compartido (SAS)]: #SAS-authorization-issue
[Código de JavaScript del lado cliente no tiene el objeto de permiso tooaccess Hola]: #JavaScript-code-does-not-have-permission
[Error de red]: #network-failure
[cliente de Hello está recibiendo mensajes de HTTP 409 (conflicto)]: #the-client-is-receiving-409-messages

[métricas muestran PercentSuccess baja o las entradas del registro de análisis tienen operaciones con estado de la transacción de ClientOtherErrors]: #metrics-show-low-percent-success
[Las métricas de capacidad muestran un aumento inesperado en el uso de la capacidad de almacenamiento]: #capacity-metrics-show-an-unexpected-increase
[Se producen reinicios inesperados de máquinas virtuales que tienen muchos VHD adjuntos]: #you-are-experiencing-unexpected-reboots
[El problema surge de mediante el emulador de almacenamiento de hello para el desarrollo o de prueba]: #your-issue-arises-from-using-the-storage-emulator
[Función "X" no funciona en el emulador de almacenamiento de Hola]: #feature-X-is-not-working
[Error "valor de Hola para uno de los encabezados HTTP de Hola no está en formato correcto de hello" al usar Hola emulador de almacenamiento]: #error-HTTP-header-not-correct-format
[Emulador en ejecución Hola almacenamiento requiere privilegios administrativos]: #storage-emulator-requires-administrative-privileges
[Se están produciendo problemas para instalar hello Azure SDK para .NET]: #you-are-encountering-problems-installing-the-Windows-Azure-SDK
[Tiene otro problema distinto relacionado con un servicio de almacenamiento]: #you-have-a-different-issue-with-a-storage-service

[apéndices]: #appendices
[apéndice 1: tráfico HTTP y HTTPS toocapture utilizando Fiddler]: #appendix-1
[apéndice 2: el tráfico de red de uso Wireshark toocapture]: #appendix-2
[apéndice 3: el tráfico de red usando el analizador de mensajes de Microsoft toocapture]: #appendix-3
[Apéndice 4: Usar tooview métricas y registro de datos de Excel]: #appendix-4
[apéndice 5: supervisar con Application Insights para Visual Studio Team Services]: #appendix-5

<!--Image references-->
[1]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/overview.png
[2]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/portal-screenshot.png
[3]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/hour-minute-metrics.png
[4]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/high-e2e-latency.png
[5]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/fiddler-screenshot.png
[6]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/wireshark-screenshot-1.png
[7]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/wireshark-screenshot-2.png
[8]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/wireshark-screenshot-3.png
[9]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/mma-screenshot-1.png
[10]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/mma-screenshot-2.png
