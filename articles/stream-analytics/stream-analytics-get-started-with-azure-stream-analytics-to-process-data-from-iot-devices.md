---
title: "aaaIoT flujos de datos en tiempo real y análisis de transmisiones de Azure | Documentos de Microsoft"
description: "Flujos de datos y SensorTags de IoT con análisis de transmisiones y procesamiento de datos en tiempo real"
keywords: "solución de IoT, introducción a IoT"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 3e829055-75ed-469f-91f5-f0dc95046bdb
ms.service: stream-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 422e6b719d0289880aa7f17fdc585e2b768c63d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-stream-analytics-tooprocess-data-from-iot-devices"></a>Empezar a trabajar con datos de análisis de transmisiones de Azure tooprocess desde dispositivos de IoT
En este tutorial, aprenderá cómo datos de toogather de la lógica de procesamiento de transmisiones de toocreate desde dispositivos de Internet de las cosas (IoT). Se usará un toodemonstrate de casos de uso de Internet de las cosas (IoT) reales, cómo toobuild la solución rápida y económica.

## <a name="prerequisites"></a>Requisitos previos
* [Suscripción de Azure](https://azure.microsoft.com/pricing/free-trial/)
* Archivos de datos y consultas de ejemplo que se pueden descargar desde [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)

## <a name="scenario"></a>Escenario
Contoso, que es una empresa en el espacio de automatización industrial de hello, ha automatizada por completo su proceso de fabricación. maquinaria de Hello en esta planta tiene sensores que son capaces de emitir los flujos de datos en tiempo real. En este escenario, un administrador de planta de producción desea toohave información en tiempo real de toolook de datos del sensor de Hola para patrones y realizar acciones en ellos. Usaremos Hola lenguaje de consulta de análisis de secuencia (SAQL) en patrones interesantes de hello sensor datos toofind de flujo de entrada de Hola de datos.

Estos datos provienen de un dispositivo SensorTag de Texas Instruments.

![SensorTag de Texas Instruments](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-01.jpg)

carga de Hola de datos de hello está en formato JSON y Hola siguiente aspecto:

    {
        "time": "2016-01-26T20:47:53.0000000",  
        "dspl": "sensorE",  
        "temp": 123,  
        "hmdt": 34  
    }  

En un escenario real, podría haber cientos de estos sensores generando eventos en forma de secuencia. Idealmente, un dispositivo de puerta de enlace se ejecutaría código toopush estos eventos demasiado[centros de eventos de Azure](https://azure.microsoft.com/services/event-hubs/) o [centros de IoT de Azure](https://azure.microsoft.com/services/iot-hub/). El trabajo de análisis de transmisiones se recopile estos eventos desde los centros de eventos y ejecutar consultas de análisis en tiempo real en secuencias de Hola. A continuación, podría enviar Hola resultados tooone de hello [admiten salidas](stream-analytics-define-outputs.md).

Para facilitar su uso, esta guía de introducción proporciona un archivo con datos de ejemplo que se capturan desde dispositivos de SensorTag reales. Puede ejecutar consultas en los datos de ejemplo de Hola y ver los resultados. En los tutoriales posteriores, obtendrá información sobre cómo tooconnect su tooinputs y salidas de trabajo e implementarlos toohello servicio de Azure.

## <a name="create-a-stream-analytics-job"></a>Creación de un trabajo de Análisis de transmisiones
1. Hola [portal de Azure](http://portal.azure.com), haga clic en el signo más hello y, a continuación, escriba **análisis de transmisiones** Hola texto ventana toohello a la derecha. A continuación, seleccione **trabajo de análisis de transmisiones** en la lista de resultados de Hola.
   
    ![Crear un nuevo trabajo de Análisis de transmisiones](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-02.png)
2. Escriba un nombre de trabajo único y comprobar la suscripción de hello es Hola uno correcto para su trabajo. A continuación, cree un grupo de recursos o seleccione uno existente en su suscripción.
3. Después seleccione una ubicación para el trabajo. De velocidad de procesamiento y la reducción de costos de transferencia de datos seleccionando Hola se recomienda la misma ubicación que el grupo de recursos de Hola y cuenta de almacenamiento previsto.
   
    ![Detalles de la creación de un trabajo de Stream Analytics](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03.png)
   
   > [!NOTE]
   > Debe crear esta cuenta de almacenamiento solo una vez por región. Este almacenamiento se compartirá entre todos los trabajos de Stream Analytics que se creen en esa región.
   > 
   > 
4. Hola cuadro tooplace su trabajo en el panel y, a continuación, haga clic en **crear**.
   
    ![creación de trabajo en curso](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03a.png)
5. Debería ver una 'implementación iniciada...' mostrada en hello parte superior derecha de la ventana del explorador. Pronto cambiará ventana tooa completado, tal y como se muestra a continuación.
   
    ![creación de trabajo en curso](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03b.png)

### <a name="create-an-azure-stream-analytics-query"></a>Creación de una consulta de Azure Stream Analytics
Después de que el trabajo se tooopen de tiempo del que lo creó y crear una consulta. Haciendo clic en el icono de Hola para puedan acceder fácilmente a su trabajo.

![Icono de trabajo](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-04.png)

Hola **trabajo topología** panel, haga clic en hello **consulta** cuadro toogo toohello Editor de consultas. Hola **consulta** editor permite consulta tooenter código T-SQL que realiza la transformación de Hola a través de los datos de eventos de Hola entrantes.

![Cuadro Consulta](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-05.png)

### <a name="query-archive-your-raw-data"></a>Consulta: archivado de los datos sin procesar
forma más sencilla de Hola de consulta es una consulta de paso a través que archiva todos los tooits de datos de entrada designados de salida. Descargue el archivo de datos de ejemplo de Hola [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot) tooa ubicación en el equipo. 

1. Pegue la consulta de Hola de archivo de hello PassThrough.txt. 
   
    ![Flujo de entrada de prueba](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06.png)
2. Haga clic en siguiente tooyour entrada de hello tres puntos y seleccione **cargar datos de ejemplo de archivo** cuadro.
   
    ![Flujo de entrada de prueba](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06a.png)
3. Un panel se abre en hello derecha como consecuencia, en ella datos seleccione hello HelloWorldASA InputStream.json desde la ubicación de descarga de archivos y haga clic en **Aceptar** final Hola del panel de Hola.
   
    ![Flujo de entrada de prueba](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06b.png)
4. A continuación, haga clic en hello **probar** engranaje en hello área superior izquierda de la ventana hello y procesar la consulta de prueba en el conjunto de datos de ejemplo de Hola. Se abrirá una ventana de resultados por debajo de la consulta como procesamiento de Hola se complete.
   
    ![Resultados de prueba](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-07.png)

### <a name="query-filter-hello-data-based-on-a-condition"></a>Consulta: Datos del filtro Hola basados en una condición
Probemos resultados de hello toofilter basadas en una condición. Nos gustaría tooshow resultados para solamente aquellos eventos que proceden de "sensorA." consulta de Hello es en el archivo de hello Filtering.txt.

![Filtrado de un flujo de datos](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-08.png)

Tenga en cuenta que Hola consulta entre mayúsculas y minúsculas compara un valor de cadena. Haga clic en hello **prueba** engranaje tooexecute consulta de Hola de nuevo. consulta de Hello debe devolver 389 filas fuera 1860 eventos.

![Segundos resultados de salida de la prueba de consulta](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-09.png)

### <a name="query-alert-tootrigger-a-business-workflow"></a>Consulta: Alerta tootrigger un flujo de trabajo de negocios
Aumentemos el grado de detalle de la consulta. Para cada tipo de sensor, se desea toomonitor temperatura media por la ventana de 30 segundos y mostrar los resultados sólo si la temperatura media de hello es superior a 100 grados. Se escribirán siguiente Hola de consulta y, a continuación, haga clic en **prueba** resultados de toosee Hola. consulta de Hello es en el archivo de hello ThresholdAlerting.txt.

![Consulta de filtro de 30 segundos](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-10.png)

Ahora debería ver los resultados que contengan sólo 245 filas y nombres de sensores donde la temperatura media de hello es superior a 100. Esta consulta agrupa el flujo de Hola de eventos por **dspl**, que es nombre de sensor de hello, más un **ventana de saltos de tamaño constante** de 30 segundos. Las consultas temporales deben indicar cómo queremos tooprogress de tiempo. Mediante el uso de hello **TIMESTAMP BY** cláusula, especificamos hello **OUTPUTTIME** veces tooassociate de columna con todos los cálculos temporales. Para obtener información detallada, lea los artículos de MSDN de hello sobre [administración del tiempo](https://msdn.microsoft.com/library/azure/mt582045.aspx) y [funciones basadas en ventanas](https://msdn.microsoft.com/library/azure/dn835019.aspx).

### <a name="query-detect-absence-of-events"></a>Consulta: detección de la ausencia de eventos
¿Cómo podemos escribimos una toofind consulta una falta de eventos de entrada? Averigüemos Hola última vez que un sensor envía datos y, a continuación, no envió los eventos para hello siguiente minuto. consulta de Hello es en el archivo de hello AbsenseOfEvent.txt.

![Detección de la ausencia de eventos](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-11.png)

Aquí usamos un **LEFT OUTER** unir toohello flujos de datos mismas (autocombinación). Para una combinación **INNER**, solo se devuelve un resultado cuando se encuentra una coincidencia.  Para una **LEFT OUTER** combinación, si un evento de hello parte izquierda de la combinación de hello es no coincidente, se devuelve una fila que tiene un valor NULL para todas las columnas del lado derecho de Hola de Hola. Esta técnica es muy útil toofind una ausencia de eventos. Para más información acerca de [JOIN](https://msdn.microsoft.com/library/azure/dn835026.aspx), consulte la documentación de MSDN.

## <a name="conclusion"></a>Conclusión
finalidad de Hola de este tutorial es toodemonstrate cómo toowrite distintas consultas de lenguaje de consulta de análisis de transmisiones y ver resultados en el Explorador de Hola. Sin embargo, se trata solo de una introducción. Es mucho más lo que puede hacer con Stream Analytics. Análisis de transmisiones admite una variedad de entradas y salidas y puede incluso usar las funciones de toomake de aprendizaje automático de Azure, una herramienta sólida para analizar los flujos de datos. Puede iniciar tooexplore más información sobre análisis de transmisiones mediante nuestro [aprender a asignar](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/). Para obtener más información acerca de cómo toowrite consultas, lea el artículo de hello sobre [patrones comunes de consulta](stream-analytics-stream-analytics-query-patterns.md).

