---
title: "aaaAzure integración de análisis de transmisiones y aprendizaje automático | Documentos de Microsoft"
description: "¿Cómo toouse una función definida por el usuario y el aprendizaje automático en un trabajo de análisis de transmisiones"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a>Análisis de opiniones mediante Azure Stream Analytics y Azure Machine Learning
Este artículo describe cómo tooquickly configura un simple trabajo de análisis de transmisiones de Azure que integra el aprendizaje automático de Azure. Usan un modelo de análisis de opiniones de aprendizaje automático de hello datos de texto de la Galería de inteligencia de Cortana tooanalyze transmisión por secuencias y determinar la puntuación de opinión de hello en tiempo real. Hola Cortana Intelligence Suite permite realizar esta tarea sin preocuparse por las complejidades de saludo de la creación de un modelo de análisis de opiniones.

Puede aplicar lo que aprenda de este tooscenarios artículo como los siguientes:

* Análisis de opiniones en tiempo real en datos de Twitter que se están transmitiendo.
* Análisis de registros de chats de clientes con el personal de soporte técnico.
* Evaluación de comentarios en foros, blogs y vídeos. 
* Muchos otros escenarios de puntuación predictiva en tiempo real.

En un escenario real, obtendría datos Hola directamente desde un flujo de datos de Twitter. tutorial de hello toosimplify, hemos escrito, por lo que hello trabajo de análisis de transmisión por secuencias obtiene tweets desde un archivo CSV en almacenamiento de blobs de Azure. Puede crear su propio archivo CSV, o puede usar un archivo CSV de ejemplo, como se muestra en hello después de imagen:

![tweets de ejemplo de un archivo CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

trabajo de análisis de transmisión por secuencias de Hola que cree aplica modelo de análisis de opiniones hello como una función definida por el usuario (UDF) en los datos de texto de ejemplo de Hola de almacén de blobs de Hola. salida de Hello (resultado de hello de análisis de opiniones Hola) se escribe toohello mismo almacén de blob en un archivo CSV diferente. 

Hello en la ilustración siguiente se muestra esta configuración. Como se ha indicado, para un escenario más realista, puede sustituir el almacenamiento de blobs por datos de Twitter que se estén transmitiendo desde una entrada de Azure Event Hubs. Además, puede generar un [Microsoft Power BI](https://powerbi.microsoft.com/) visualización en tiempo real de opiniones agregado Hola.    

![Información general sobre la integración de Stream Analytics Machine Learning](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a>Requisitos previos
Antes de empezar, asegúrese de que tiene Hola siguientes:

* Una suscripción de Azure activa.
* Un archivo CSV con algunos datos. Puede descargar archivo hello mostrado anteriormente desde [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), o bien puede crear su propio archivo. En este artículo, se supone que está usando el archivo hello desde GitHub.

En un nivel alto, tareas de hello toocomplete que se explican en este artículo, Hola siguientes:

1. Crear una cuenta de almacenamiento de Azure y un contenedor de almacenamiento de blobs y cargue un contenedor de toohello del archivo de entrada con formato CSV.
3. Agregar un modelo de análisis de opiniones de área de trabajo de aprendizaje automático de Azure de hello Cortana Intelligence Galería tooyour e implementar este modelo como un servicio web en el área de trabajo de aprendizaje automático de Hola.
5. Crear un trabajo de análisis de transmisiones que llama a este servicio web como una función en las opiniones de orden toodetermine Hola entrada de texto.
6. Iniciar el trabajo de análisis de transmisiones de Hola y compruebe la salida de hello.

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a>Crear un contenedor de almacenamiento y cargar el archivo de entrada de hello CSV
Para este paso, puede usar cualquier archivo CSV, como Hola uno disponible en GitHub.

1. Hola portal de Azure, haga clic en **New** &gt; **almacenamiento** &gt; **cuenta de almacenamiento**.

   ![creación de una nueva cuenta de almacenamiento](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. Proporcione un nombre (`samldemo` en el ejemplo de Hola). nombre de Hello puede usar solo letras minúsculas y números, y debe ser único en Azure. 

3. Especifique un grupo de recursos existente y una ubicación. Para la ubicación, se recomienda que todos los recursos de hello creados en este tutorial, use Hola misma ubicación.

    ![especificación de los detalles de la cuenta de almacenamiento](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. Hola portal de Azure, seleccione la cuenta de almacenamiento de Hola. En la hoja de la cuenta de almacenamiento de hello, haga clic en **contenedores** y, a continuación, haga clic en  **+ &nbsp;contenedor** toocreate el almacenamiento de blobs.

    ![creación de contenedor de blobs](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. Proporcione un nombre para el contenedor de hello (`azuresamldemoblob` en el ejemplo de Hola) y compruebe que **tipo de acceso** se establece demasiado**Blob**. Cuando haya terminado, haga clic en **Aceptar**.

    ![especificación de los detalles del contenedor de blobs](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. Hola **contenedores** hoja, seleccione Hola nuevo contenedor de, que abre una hoja de Hola para ese contenedor.

7. Haga clic en **Cargar**.

    ![botón "Cargar" de un contenedor](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. Hola **cargar blob** hoja, especifique el archivo CSV de Hola que quiere toouse de este tutorial. Para **tipo de Blob**, seleccione **blob en bloques** y conjunto Hola bloque tamaño too4 MB, que es suficiente para este tutorial.

    ![carga del archivo de blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. Haga clic en hello **cargar** situado en parte inferior de Hola de hoja de Hola.

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a>Agregar modelos de análisis de opiniones Hola de hello Galería de inteligencia de Cortana

Ahora que los datos de ejemplo de Hola están en un blob, puede habilitar el modelo de análisis de opiniones hello en Galería de inteligencia de Cortana.

1. Vaya toohello [modelo de análisis predictivo opiniones](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) página Hola Galería de inteligencia de Cortana.  

2. Haga clic en **Abrir en Studio**.  
   
   ![Aprendizaje automático de Análisis de transmisiones, abrir Aprendizaje automático](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. Inicie sesión en el área de trabajo de toogo toohello. Seleccione una ubicación.

4. Haga clic en **ejecutar** final Hola de página Hola. se ejecuta el proceso de Hello, que tarda aproximadamente un minuto.

   ![ejecución del experimento en Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. Después de que se ejecute correctamente el proceso de hello, seleccione **implementar el servicio de Web** final Hola de página Hola.

   ![implementación del experimento como un servicio web en Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. toovalidate que Hola opiniones modelo de análisis es toouse listo, haga clic en hello **prueba** botón. Proporcione algún texto de entrada, como "Me encanta Microsoft". 

   ![prueba del experimento en Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    Si prueba Hola funciona, verá un toohello similar de resultados siguiente ejemplo:

   ![resultados de la prueba en Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. Hola **aplicaciones** columna, haga clic en hello **Excel 2010 o el libro anterior** toodownload vínculo un libro de Excel. libro de Hello contiene clave Hola una API y la dirección URL de Hola que necesite tooset más adelante el trabajo de análisis de transmisiones de Hola.

    ![Aprendizaje automático de Análisis de transmisiones, vista rápida](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a>Crear un trabajo de análisis de transmisiones que usa el modelo de aprendizaje automático de Hola

Ahora puede crear un trabajo de análisis de transmisiones que lee tweets de ejemplo de Hola desde archivo CSV de hello en almacenamiento de blobs. 

### <a name="create-hello-job"></a>Crear trabajo de Hola

1. Vaya toohello [portal de Azure](https://portal.azure.com).  

2. Haga clic en **Nuevo** > **Internet de las cosas** > **Trabajo de Stream Analytics**. 

   ![Ruta de acceso del portal Azure para obtener tooa nuevo trabajo de análisis de transmisiones](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. Nombre de trabajo de hello `azure-sa-ml-demo`, especifique una suscripción, especificar un grupo de recursos existente o cree uno nuevo y seleccione ubicación hello para el trabajo de Hola.

   ![especificación de la configuración del nuevo trabajo de Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a>Configurar entrada de trabajo de Hola
trabajo de Hello obtiene su entrada desde archivo CSV de Hola que carga de almacenamiento de tooblob anterior.

1. Después de que se ha creado un trabajo de hello, en **trabajo topología** en la hoja de trabajo de hello, haga clic en hello **entradas** cuadro.  
   
   ![cuadro "Entradas" de la hoja del trabajo de Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. Hola **entradas** hoja, haga clic en **+ agregar**.

   !['Add' botón para agregar un trabajo de análisis de transmisiones de entrada toohello](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. Rellene hello **nueva entrada** hoja con estos valores:

    * **Alias de entrada**: usar el nombre de hello `datainput`.
    * **Tipo de origen**: seleccione **Flujo de datos**.
    * **Origen**: seleccione **Almacenamiento de blobs**.
    * **Opción de importación**: seleccione **Usar almacenamiento de blobs de la suscripción actual**. 
    * **Cuenta de almacenamiento**. Seleccione la cuenta de almacenamiento de Hola que creó anteriormente.
    * **Contenedor**. Contenedor de hello SELECT que creó anteriormente (`azuresamldemoblob`).
    * **Formato de serialización de eventos**. Seleccione **CSV**.

    ![Configuración de la nueva entrada de trabajo](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. Haga clic en **Crear**.

### <a name="configure-hello-job-output"></a>Configurar la salida de trabajo de Hola
Hola trabajo envía resultados toohello mismo donde se obtiene información de almacenamiento de blobs. 

1. En **trabajo topología** en la hoja de trabajo de hello, haga clic en hello **salidas** cuadro.  
  
   ![Creación de una nueva salida para el trabajo de Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. Hola **salidas** hoja, haga clic en **+ agregar**y, a continuación, agregar una salida con el alias de hello `datamloutput`. 

3. En **Receptor**, seleccione **Almacenamiento de blobs**. Relleno a continuación, en el resto de Hola de hello salida configuración mediante Hola mismos valores que se usa para el almacenamiento de blobs de hello para la entrada:

    * **Cuenta de almacenamiento**. Seleccione la cuenta de almacenamiento de Hola que creó anteriormente.
    * **Contenedor**. Contenedor de hello SELECT que creó anteriormente (`azuresamldemoblob`).
    * **Formato de serialización de eventos**. Seleccione **CSV**.

   ![Configuración de la nueva salida de trabajo](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. Haga clic en **Crear**.   


### <a name="add-hello-machine-learning-function"></a>Agregar la función de aprendizaje automático de hello 
Anteriormente se publica un servicio web de aprendizaje automático modelo tooa. En nuestro escenario, cuando se ejecuta el trabajo de análisis de secuencia de hello, envía cada tweet de ejemplo de servicio de web de entrada toohello Hola para análisis de opiniones. Hola servicio web de aprendizaje automático devuelve una opinión (`positive`, `neutral`, o `negative`) y una probabilidad de tweet Hola está positivo. 

En esta sección del tutorial de hello, definir una función de trabajo de análisis de transmisiones de Hola. función Hello pueda ser invocado toosend un servicio web de toohello de tweet y obtener respuesta de Hola. 

1. Asegúrese de que tiene Hola dirección URL y la API de clave de servicio web que ha descargado anteriormente en el libro de Excel de Hola.

2. Hoja de información general del trabajo toohello devuelto.

3. En **Configuración**, seleccione **Funciones** y luego haga clic en **+ Agregar**.

   ![Agregar un trabajo de análisis de transmisiones de toohello (función)](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. Escriba `sentiment` como Hola función alias y rellene rest Hola de hoja de hello con estos valores:

    * **Tipo de función**: seleccione **Aprendizaje automático de Azure**.
    * **Opción de importación**: seleccione **Importar de una suscripción distinta**. Esto proporciona una oportunidad tooenter Hola URL y una clave.
    * **Dirección URL**: pegar Hola URL del servicio web.
    * **Clave**: pegar en la clave de API de Hola.
  
    ![Configuración para agregar un trabajo de análisis de transmisiones de toohello de función de aprendizaje automático](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. Haga clic en **Crear**.

### <a name="create-a-query-tootransform-hello-data"></a>Crear una consulta de datos de hello tootransform

Análisis de transmisiones usa una entrada de consulta declarativa basado en SQL tooexamine hello y procesarlo. En esta sección, creará una consulta que lee cada tweet de entrada y, a continuación, se llama a análisis de opiniones de tooperform de función de aprendizaje automático de Hola. consulta de Hello, a continuación, envía Hola resultado toohello de salida que definió (almacenamiento de blobs).

1. Hoja de información general del trabajo toohello devuelto.

2.  En **trabajo topología**, haga clic en hello **consulta** cuadro.

    ![Creación de una consulta para el trabajo de Streaming Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. Escriba Hola después de consulta:

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    consulta de Hello invoca la función hello que creó anteriormente (`sentiment`) en el análisis de opiniones tooperform de orden en cada tweet en la entrada de Hola. 

4. Haga clic en **guardar** consulta de hello toosave.


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a>Iniciar el trabajo de análisis de transmisiones de Hola y compruebe la salida de hello

Ahora puede iniciar el trabajo de análisis de transmisiones de Hola.

### <a name="start-hello-job"></a>Iniciar el trabajo de Hola
1. Hoja de información general del trabajo toohello devuelto.

2. Haga clic en **iniciar** princip Hola de hoja de Hola.

    ![Creación de una consulta para el trabajo de Streaming Analytics](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. Hola **Start job**, seleccione **personalizada**y, a continuación, seleccione un día toowhen anterior que cargó el almacenamiento de información de hello CSV archivo tooblob. Cuando haya terminado, haga clic en **Iniciar**.  


### <a name="check-hello-output"></a>Compruebe la salida de hello
1. Trabajo de hello permiten ejecutar durante varios minutos hasta que vea actividad Hola **supervisión** cuadro. 

2. Si tiene una herramienta que suele usar el contenido de hello tooexamine de almacenamiento de blobs, use ese Hola de tooexamine herramienta `azuresamldemoblob` contenedor. Como alternativa, Hola pasos de hello portal de Azure:

    1. En el portal de hello, busque hello `samldemo` almacenamiento de la cuenta y, dentro de la cuenta de hello, buscar hello `azuresamldemoblob` contenedor. Verá dos archivos en el contenedor de hello: Hola archivo que contenga tweets de ejemplo de Hola y un archivo CSV generado por el trabajo de análisis de transmisiones de Hola.
    2. Haga clic en archivo hello generado y, a continuación, seleccione **descargar**. 

   ![Descarga de la salida del trabajo CSV desde el almacenamiento de blobs](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. Abra Hola genera el archivo CSV. Verá algo parecido a Hola siguiente ejemplo:  
   
   ![Aprendizaje automático de Análisis de transmisiones, vista CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a>Visualización de métricas
También puede observar las métricas relacionadas con la función de Aprendizaje automático de Azure. Hola siguiendo las métricas relacionadas con la función se muestra en hello **supervisión** cuadro en la hoja de trabajo de hello:

* **Función solicitudes** indica Hola número de solicitudes enviadas tooa servicio web de aprendizaje automático.  
* **Función eventos** indica el número de Hola de eventos de solicitud de saludo. De forma predeterminada, cada servicio web de aprendizaje automático de tooa de solicitud contiene una too1, 000 eventos.  


## <a name="next-steps"></a>Pasos siguientes

* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Integración de la API de REST y Machine Learning](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [Referencia de API de REST de administración de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)



