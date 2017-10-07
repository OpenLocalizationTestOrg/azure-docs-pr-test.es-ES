---
title: "aaaIntroduction tooStream análisis | Documentos de Microsoft"
description: "Obtenga información sobre análisis de transmisiones, un servicio administrado que le ayuda a analizar los datos de transmisión por secuencias desde Internet de las cosas (IoT) hello en tiempo real."
keywords: "análisis como servicio, servicios administrados, procesamiento de transmisiones, análisis de transmisiones, qué es stream analytics"
services: stream-analytics
documentationcenter: 
author: jenniehubbard
manager: jhubbard
editor: cgronlun
ms.assetid: 613c9b01-d103-46e0-b0ca-0839fee94ca8
ms.service: stream-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/08/2017
ms.author: jhubbard
ms.openlocfilehash: 6dd7ea1d358bcc94e927a3e699a2771a25104d72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-stream-analytics"></a>¿Qué es Stream Analytics?

Azure Stream Analytics es un motor de procesamiento de eventos totalmente administrado que le permite configurar cálculos analíticos en tiempo real sobre datos en streaming. Hola datos pueden proceder de dispositivos, sensores, sitios web, las fuentes de redes sociales, aplicaciones, sistemas de infraestructura y más. 

## <a name="what-can-i-do-with-stream-analytics"></a>¿Qué se puede hacer con Stream Analytics?

Usar tooexamine grandes volúmenes de datos que fluyen desde los dispositivos o los procesos de análisis de transmisiones, extraer información de flujo de datos de Hola y buscar las relaciones, las tendencias y patrones. En función de lo que aparece en los datos de hello, a continuación, puede realizar tareas de la aplicación. Por ejemplo, puede generar alertas, iniciar los flujos de trabajo de automatización, fuente tooa información reporting herramienta como Power BI o almacenar datos para analizarlo más adelante. 

Ejemplos:

* Análisis y alertas personalizados y en tiempo real de valores bursátiles que ofrecen las empresas de servicios financieros.
* Detección de fraudes en tiempo real basada en el examen de datos de transacciones. 
* Servicios de protección de datos e identidades.
* Análisis de datos generados por sensores y accionadores insertados en objetos físicos (Internet de las cosas o IoT).
* Análisis clickstream de Internet.
* Aplicaciones de administración de las relaciones con el cliente (CRM) que emiten alertas cuando la experiencia del cliente en un período de tiempo se ve mermada.

## <a name="how-does-stream-analytics-work"></a>¿Cómo funciona Stream Analytics?

Este diagrama muestra la canalización de análisis de transmisiones de hello, que muestra cómo se ingestión datos, analizar y, a continuación, se envían para su presentación o acción. 

![Canalización de Stream Analytics](./media/stream-analytics-introduction/stream_analytics_intro_pipeline.png)

Stream Analytics comienza con un origen de datos en streaming. datos de Hello pueden ingestión en Azure desde un dispositivo mediante un concentrador de eventos de Azure o el centro de IoT. También se pueden extraer datos de Hola desde un almacén de datos como el almacenamiento de blobs de Azure. 

secuencia de hello tooexamine, se crea un análisis de transmisiones *trabajo* que especifica donde provienen los datos de Hola. trabajo de Hello también especifica un *transformación*&mdash;cómo toolook de datos, los patrones o relaciones. Para esta tarea, Stream Analytics admite un lenguaje de consulta similar a SQL que le permite filtrar, ordenar, agregar y combinar datos en streaming durante un período de tiempo.

Por último, trabajo Hola especifica un datos de salida toosend Hola transformado a. Esto le permite controlar qué toodo en información de respuesta toohello ha analizado. Por ejemplo, en tooanalysis de respuesta, puede:

* Enviar un comando toochange configuración del dispositivo. 
* Cola de tooa de datos que se supervisa mediante un proceso que realiza una acción en función de lo que encuentre de envío. 
* Panel de Power BI tooa de datos para los informes de envío.
* Enviar datos toostorage como almacén de Data Lake, base de datos de SQL Server o almacenamiento en tablas o blobs de Azure.

Puede supervisar este trabajo y ajustar la cantidad de eventos que procesa por segundo mientras se ejecuta. También puede hacer que los trabajos generen registros de diagnóstico para solucionar problemas.

## <a name="key-capabilities-and-benefits"></a>Ventajas y principales capacidades

Análisis de transmisiones es fácil toouse diseñada toobe, flexible y escalable tooany trabajo tamaño y económica.

### <a name="connectivity-toomany-inputs-and-outputs"></a>Conectividad toomany entradas y salidas

Análisis de transmisiones se conecta directamente demasiado[centros de eventos de Azure](https://azure.microsoft.com/services/event-hubs/) y [centro de IoT de Azure](https://azure.microsoft.com/services/iot-hub/) para la ingesta de secuencia y hello [servicio de almacenamiento de blobs de Azure](https://docs.microsoft.com/azure/storage/storage-introduction#blob-storage-accounts) tooingest los datos históricos. Si obtiene datos de Event Hubs, puede combinar Stream Analytics con otros orígenes de datos y motores de procesamiento.

La entrada de trabajo también puede incluir datos de referencia (datos estáticos o que cambian con lentitud). Puede combinar la transmisión por secuencias datos toothis referencia datos tooperform búsqueda operaciones Hola igual que lo haría con las consultas de base de datos.

Redirija la salida del trabajo de Stream Analytics en muchas direcciones. Puede escribir toostorage como blobs de almacenamiento de Azure o tablas, base de datos de SQL Azure, Azure Lake almacenes de datos o base de datos de Azure Cosmos. Desde allí, pueden pasar datos hello para el análisis por lotes a través de HDInsight de Azure. Puede enviar Hola salida tooanother servicio para su uso por otro proceso, como colas, temas de Service Bus de Azure o centros de eventos. Puede enviar tooPower de salida de hello BI para visualización.

### <a name="ease-of-use"></a>Facilidad de uso

transformaciones de toodefine, utiliza una sencilla declarativa [lenguaje de consulta de análisis de transmisiones](https://msdn.microsoft.com/library/azure/dn834998.aspx) que le permite crear análisis sofisticados con ninguna programación. lenguaje de consulta de Hello toma datos de transmisión por secuencias como entrada. Puede filtrar y ordenar datos hello, agregar valores, realizar cálculos, combinar datos (dentro de una secuencia o tooreference de datos) y usar funciones geoespaciales. Puede editar las consultas en el portal de hello, con IntelliSense y la comprobación de sintaxis, y puede probar las consultas que utilizan datos de ejemplo que puede extraer de la secuencia en directo de Hola.

### <a name="extensible-query-language"></a>Lenguaje de consulta extensible

Puede ampliar las capacidades de Hola de lenguaje de consulta de hello definiendo y invocar funciones adicionales. Puede definir las llamadas a funciones en hello aprendizaje automático de Azure servicio tootake aprovechar soluciones de aprendizaje automático de Azure. También puede integrar las funciones JavaScript definido por el usuario (UDF) en los cálculos complejos de orden tooperform como parte de una consulta de análisis de transmisiones.

### <a name="scalability"></a>Escalabilidad

Análisis de transmisiones puede controlar la too1 GB de datos entrantes por segundo. Integración con [centros de eventos de Azure](https://azure.microsoft.com/services/event-hubs/) y [centro de IoT de Azure](https://azure.microsoft.com/services/iot-hub/) permite trabajos tooingest millones de eventos por segundo que provienen de dispositivos conectados, clickstreams y archivos de registro, tooname algunas. Usar la característica de partición de Hola de centros de eventos, se pueden dividir los cálculos en pasos lógicos, cada uno con hello capacidad adicional toobe particiones tooincrease escalabilidad.

### <a name="low-cost"></a>Bajo costo

Como un servicio en la nube, análisis de transmisiones está optimizado toolet empezar a bajo costo. Pagar a medida que avance basándose en la cantidad de hello y uso de unidad de streaming de datos procesada por el sistema de Hola. Uso se deriva en función de volumen de Hola de eventos procesados y cantidad de Hola de capacidad de proceso aprovisiona en hello clúster toohandle trabajos de análisis de transmisiones.

### <a name="reliability-quick-recovery-and-repeatability"></a>Confiabilidad, recuperación rápida y capacidad de repetición

Como un servicio administrado en la nube de hello, análisis de transmisiones ayuda a evitar la pérdida de datos y proporciona continuidad del negocio. Si se producen errores, el servicio de hello proporciona capacidades de recuperación integradas. Con capacidad de hello toointernally mantener el estado, servicio de hello proporciona resultados repetibles asegurarse de sea tooarchive posibles eventos y volver a aplicar el procesamiento en un futuro hello, siempre obtendrá Hola mismos resultados. Esto le permite toogo en un momento e investigar los cálculos al realizar el análisis de causa raíz, análisis de escenarios condicionales y así sucesivamente.

## <a name="next-steps"></a>Pasos siguientes

* Empiece [experimentando con entradas y consultas desde dispositivos de IoT](stream-analytics-get-started-with-azure-stream-analytics-to-process-data-from-iot-devices.md).
* Crear un [soluciones de análisis de transmisiones de extremo a extremo](stream-analytics-real-time-fraud-detection.md) que examina toolook de metadatos de teléfono para llamadas fraudulentas.
* Obtén información sobre lenguaje de consulta similar a SQL para el análisis de transmisiones de hello y conceptos únicos como [funciones de ventana](stream-analytics-window-functions.md).
* Obtenga información acerca de cómo demasiado[escalar trabajos de análisis de transmisiones](stream-analytics-scale-jobs.md). 
* Obtenga información acerca de cómo demasiado[integrar el análisis de transmisiones y aprendizaje automático de Azure](stream-analytics-machine-learning-integration-tutorial.md).
* Encuentre respuestas tooyour preguntas de análisis de transmisiones de hello [foro de análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

