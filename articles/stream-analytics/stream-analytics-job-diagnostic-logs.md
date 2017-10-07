---
title: "aaaTroubleshoot análisis de transmisiones de Azure con registros de diagnóstico | Documentos de Microsoft"
description: "Obtenga información acerca de cómo las tooanalyze diagnósticos registros de análisis de transmisiones de trabajos en Microsoft Azure."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 600fce73636dd137f8f3a137f1d77b59b4a88801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-stream-analytics-by-using-diagnostics-logs"></a>Solución de problemas de Azure Stream Analytics mediante registros de diagnóstico

En ocasiones, un trabajo de Azure Stream Analytics deja de procesarse inesperadamente. Es importante toobe tootroubleshoot capaz de este tipo de evento. evento de Hello puede deberse a un resultado de consulta inesperada, toodevices de conectividad o una interrupción del servicio inesperado. Hello registros de diagnóstico en el análisis de transmisiones pueden ayudarle a identificar la causa de Hola de problemas cuando se producen y reducir el tiempo de recuperación.

## <a name="log-types"></a>Tipos de registro

Stream Analytics ofrece dos tipos de registros: 
* [Registros de actividad](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) (siempre activados). Los registros de actividad proporcionan información sobre las operaciones realizadas en los trabajos.
* [Registros de diagnóstico](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) (configurables). Los registros de diagnóstico proporcionan información más completa sobre todo lo que ocurre con un trabajo. Diagnósticos registra inicial cuando se crea el trabajo de Hola y final cuando se elimina el trabajo de Hola. Tratan los eventos cuando se actualiza el trabajo de Hola y mientras se está ejecutando.

> [!NOTE]
> Puede usar servicios como almacenamiento de Azure, los concentradores de eventos de Azure y Azure Log Analytics tooanalyze de datos no compatible. Se le cobra según Hola precios modelo para esos servicios.
>

## <a name="turn-on-diagnostics-logs"></a>Activación de los registros de diagnóstico

Los registros de diagnóstico están **desactivados** de forma predeterminada. tooturn en los registros de diagnóstico, siga estos pasos:

1.  Inicie sesión en toohello portal de Azure y vaya toohello hoja de trabajo de transmisión por secuencias. En **Supervisión**, seleccione **Registros de diagnóstico**.

    ![Registros de toodiagnostics de navegación de hoja](./media/stream-analytics-job-diagnostic-logs/image1.png)  

2.  Seleccione **Activar diagnósticos**.

    ![Activación de los registros de diagnóstico](./media/stream-analytics-job-diagnostic-logs/image2.png)

3.  En hello **configuración de diagnóstico** página, para **estado**, seleccione **en**.

    ![Cambio de estado de los registros de diagnóstico](./media/stream-analytics-job-diagnostic-logs/image3.png)

4.  Establecer el destino de archivo de hello (cuenta de almacenamiento, centro de eventos, análisis de registros) que desee. A continuación, seleccione las categorías de Hola de registros que desea que toocollect (ejecución, creación). 

5.  Guardar la nueva configuración de diagnósticos de Hola.

configuración de diagnóstico de Hello surte efecto de tootake de unos 10 minutos. Después de eso, Hola registros de inicio que aparecen en el destino de archivo hello configurado (puede verlas en hello **registros de diagnóstico** página):

![Hoja navegación toodiagnostics registros - destinos de archivo](./media/stream-analytics-job-diagnostic-logs/image4.png)

Para más información sobre la configuración de diagnósticos, consulte el artículo sobre la [recopilación y el uso de datos de diagnóstico provenientes de los recursos de Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).

## <a name="diagnostics-log-categories"></a>Categorías de registro de diagnóstico

Actualmente, se capturan dos categorías de registros de diagnóstico:

* **Creación**. Capturas de registren los eventos que están relacionado toojob las operaciones de creación: creación de trabajo, agregar y eliminar entradas y salidas, agregar y actualizar consulta hello, el inicio y trabajo de detención Hola.
* **Ejecución**. Captura los eventos que se producen durante la ejecución del trabajo:
    * Errores de conectividad
    * Errores de procesamiento de datos, como por ejemplo:
        * Definición (tipos de campo no coincidente y valores, los campos que faltan y así sucesivamente) de la consulta de eventos que no se ajustan toohello
        * Errores de evaluación de expresión
    * Otros eventos y errores

## <a name="diagnostics-logs-schema"></a>Esquema de registros de diagnóstico

Todos los registros se almacenan en formato JSON. Cada entrada tiene Hola después de los campos de cadena comunes:

Nombre | Descripción
------- | -------
Twitter en tiempo | Marca de tiempo (en UTC) del registro de hello.
resourceId | Id. de recurso de Hola Hola operación tuvo lugar, en mayúsculas. Incluyen el Id. de suscripción de hello, el grupo de recursos de Hola y el nombre del trabajo de Hola. Por ejemplo, **/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT.STREAMANALYTICS/STREAMINGJOBS/MYSTREAMINGJOB**.
categoría | La categoría del registro: **Ejecución** o **Creación**.
operationName | Nombre de operación de Hola que inició sesión. Por ejemplo, **enviar eventos: toomysqloutput de error de escritura de salida de SQL**.
status | Estado de operación de Hola. Por ejemplo, **Erróneo** o **Correcto**.
level | Nivel de registro. Por ejemplo, **Error**, **Advertencia** o **Información**.
propiedades | Detalle específico de entrada de registro, serializado como una cadena JSON. Para obtener más información, consulte las secciones siguientes de Hola.

### <a name="execution-log-properties-schema"></a>Esquema de propiedades de registros de ejecución

Los registros de ejecución contienen información sobre eventos que se produjeron durante la ejecución del trabajo de Stream Analytics. esquema de Hola de propiedades varía en función de tipo hello de evento. Actualmente, tenemos Hola siguientes tipos de registros de ejecución:

### <a name="data-errors"></a>Errores de datos

Cualquier error que se produce mientras el trabajo de hello está procesando datos está en esta categoría de registros. Estos registros se crean habitualmente durante las operaciones de lectura, serialización y escritura de datos. No incluyen errores de conectividad. Los errores de conectividad se tratan como eventos genéricos.

Nombre | Descripción
------- | -------
Origen | Nombre del trabajo de Hola de había entrada o de salida donde se produjo el error de Hola.
Message | Mensaje asociado con el error de Hola.
Tipo | Tipo de error. Por ejemplo, **DataConversionError**, **CsvParserError** o **ServiceBusPropertyColumnMissingError**.
Datos | Contiene los datos que es útiles tooaccurately encontrar Hola origen error Hola. Tootruncation asunto, según el tamaño.

Función hello **operationName** valor, los errores de datos tienen Hola después de esquema:
* **Eventos de serialización**. Los eventos de serialización se producen durante las operaciones de lectura de eventos. Se producen cuando hello datos en la entrada de hello no satisfagan esquema de la consulta de Hola para uno de estos motivos:
    * *Serializar discordancia de tipos durante el evento (Alemania)*: identifica el campo de Hola que está causando el error de Hola.
    * *No se puede leer un evento, la serialización no válido*: muestra información acerca de la ubicación de hello en los datos de entrada de Hola donde se produjo el error de Hola. Incluye el nombre de entrada de blob, el desplazamiento y una muestra de Hola datos blob.
* **Eventos de envío**. Los eventos de envío se producen durante las operaciones de escritura. Identifican Hola transmisión por secuencias de evento que provocó el error de Hola.

### <a name="generic-events"></a>Eventos genéricos

Los eventos genéricos incluyen todos los demás.

Nombre | Descripción
-------- | --------
Error | (opcional) Información de error. Normalmente, es información de excepciones, si está disponible.
Message| Mensaje de registro.
Tipo | Tipo de mensaje. Asigna la categorización de toointernal de errores. Por ejemplo, **JobValidationError** o **BlobOutputAdapterInitializationFailure**.
Id. de correlación | [GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) que identifica de forma única la ejecución del trabajo Hola. Todas las entradas de registro de ejecución de Hola Hola de tiempo de trabajo se inicia hasta que finaliza el trabajo Hola ha Hola mismo **Id. de correlación** valor.

## <a name="next-steps"></a>Pasos siguientes

* [Introducción tooStream análisis](stream-analytics-introduction.md)
* [Introducción a Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalado de trabajos de Stream Analytics](stream-analytics-scale-jobs.md)
* [Referencia de lenguaje de consulta de Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
