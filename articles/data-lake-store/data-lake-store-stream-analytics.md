---
title: "aaaStream datos de análisis de transmisiones en el almacén de Data Lake | Documentos de Microsoft"
description: "Usar datos de análisis de transmisiones de Azure toostream en almacén de Azure Data Lake"
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a>Transmisión de datos del blob de Almacenamiento de Azure al Almacén de Data Lake mediante el Análisis de transmisiones
En este artículo, aprenderá cómo toouse Azure Data Lake almacenar como una salida para un trabajo de análisis de transmisiones de Azure. Este artículo muestra un escenario sencillo que lee los datos de un blob de almacenamiento de Azure (entrada) y escrituras Hola almacén data Lake de tooData (salida).

> [!NOTE]
> En este momento, la creación y configuración de almacén de Data Lake genera para el análisis de transmisiones solo se admite en hello [Portal clásico de Azure](https://manage.windowsazure.com). Por lo tanto, algunas partes de este tutorial usará Hola Portal clásico de Azure.
>
>

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, debe tener el siguiente hello:

* **Una suscripción de Azure**. Consulte [Obtención de una versión de evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).

* **Cuenta de Almacenamiento de Azure**. Usará un contenedor de blob desde estos datos de tooinput de cuenta para un trabajo de análisis de transmisiones. Para este tutorial, suponga que tiene una cuenta de almacenamiento denominada **storageforasa** y llama a un contenedor dentro de la cuenta de hello **storageforasacontainer**. Una vez haya creado el contenedor de hello, cargue un tooit de archivo de datos de ejemplo. 
  
* **Cuenta del Almacén de Azure Data Lake**. Siga las instrucciones de hello en [empezar a trabajar con el almacén de Azure Data Lake con hello Azure Portal](data-lake-store-get-started-portal.md). Supongamos que tiene una cuenta de Data Lake Store llamada **asadatalakestore**. 

## <a name="create-a-stream-analytics-job"></a>Creación de un trabajo de Análisis de transmisiones
Primero debe crear un trabajo de Análisis de transmisiones que incluya un origen de entrada y un destino de salida. Para este tutorial, origen de hello es un contenedor de blobs de Azure y destino de hello es el almacén de Data Lake.

1. Inicio de sesión toohello [Portal de Azure](https://portal.azure.com).

2. En el panel izquierdo de hello, haga clic en **trabajos de análisis de transmisiones**y, a continuación, haga clic en **agregar**.

    ![Creación de un trabajo de Stream Analytics](./media/data-lake-store-stream-analytics/create.job.png "Creación de un trabajo de Stream Analytics")

    > [!NOTE]
    > Asegúrese de que se crea el trabajo en hello misma región que la cuenta de almacenamiento de Hola o se incurrirá en costos adicionales de mover datos entre regiones.
    >

## <a name="create-a-blob-input-for-hello-job"></a>Creación de una entrada de Blob para trabajo Hola

1. Página de Hola abierto para el trabajo de análisis de transmisiones de hello, en el panel izquierdo de hello, haga clic en hello **entradas** ficha y, a continuación, haga clic en **agregar**.

    ![Agregar un trabajo de entrada tooyour](./media/data-lake-store-stream-analytics/create.input.1.png "agregar un trabajo de entrada tooyour")

2. En hello **nueva entrada** hoja, proporcionar Hola después de valores.

    ![Agregar un trabajo de entrada tooyour](./media/data-lake-store-stream-analytics/create.input.2.png "agregar un trabajo de entrada tooyour")

    * Para **alias de entrada**, escriba un nombre único para la entrada de trabajo de Hola.
    * En **Source type** (Tipo de origen), seleccione **Flujo de datos**.
    * En **Origen**, seleccione **Blob storage**.
    * En **Suscripción**, seleccione **Usar almacenamiento de blobs de la suscripción actual**.
    * Para **cuenta de almacenamiento**, seleccione la cuenta de almacenamiento de Hola que creó como parte de los requisitos previos de Hola. 
    * Para **contenedor**, seleccione contenedor Hola que creó en hello seleccionado cuenta de almacenamiento.
    * En **Formato de serialización de eventos**, seleccione **CSV**.
    * En **Delimitador**, seleccione **tabulación**.
    * En **Codificación**, seleccione **UTF-8**.

    Haga clic en **Crear**. portal Hola ahora agrega la entrada de Hola y Hola tooit de conexión de prueba.


## <a name="create-a-data-lake-store-output-for-hello-job"></a>Crear una salida de almacén de Data Lake para trabajo Hola

1. Abrir página hello para el trabajo de análisis de transmisiones de hello, haga clic en hello **salidas** ficha y, a continuación, haga clic en **agregar**.

    ![Agregar un trabajo de salida tooyour](./media/data-lake-store-stream-analytics/create.output.1.png "agregar un trabajo de tooyour de salida")

2. En hello **nueva salida** hoja, proporcionar Hola después de valores.

    ![Agregar un trabajo de salida tooyour](./media/data-lake-store-stream-analytics/create.output.2.png "agregar un trabajo de tooyour de salida")

    * Para **alias de salida**, escriba un un nombre único para la salida del trabajo Hola. Se trata de un nombre descriptivo que se usa en consultas toodirect Hola consulta salida toothis almacén de Data Lake.
    * En **Receptor**, seleccione **Data Lake Store**.
    * Podrá tooauthorize solicitada tener acceso a la cuenta de almacén de tooData Lake. Haga clic en **Autorizar**.

3. En hello **nueva salida** hoja, continuar hello tooprovide después de valores.

    ![Agregar un trabajo de salida tooyour](./media/data-lake-store-stream-analytics/create.output.3.png "agregar un trabajo de tooyour de salida")

    * Para **nombre de la cuenta**, seleccione cuenta del almacén de Data Lake de Hola que ya haya creado en la que desea toobe de salida de hello trabajo enviado a.
    * Para **modelo de prefijo de ruta de acceso**, escriba un toowrite de ruta de archivo especifican de los archivos dentro de hello cuenta de almacén de Data Lake.
    * Para **formato de fecha**, si usó un token de fecha en la ruta de acceso de prefijo de hello, puede seleccionar el formato de fecha de hello en el que se organizan los archivos.
    * Para **formato de hora**, si se usa un símbolo (token) de tiempo en la ruta de acceso de prefijo de hello, especifique el formato de hora de hello en el que se organizan los archivos.
    * En **Formato de serialización de eventos**, seleccione **CSV**.
    * En **Delimitador**, seleccione **tabulación**.
    * En **Codificación**, seleccione **UTF-8**.
    
    Haga clic en **Crear**. portal de Hello ahora agrega la salida de hello y prueba Hola conexión tooit.
    
## <a name="run-hello-stream-analytics-job"></a>Ejecutar trabajo de análisis de transmisiones de Hola

1. toorun un trabajo de análisis de transmisiones, debe ejecutar una consulta de hello **consulta** ficha. Para este tutorial, puede ejecutar la consulta de ejemplo de Hola reemplazando los marcadores de posición de hello con hello trabajo alias de entrada y salidos, como se muestra en la siguiente captura de pantalla de Hola.

    ![Ejecución de una consulta](./media/data-lake-store-stream-analytics/run.query.png "Ejecución de una consulta")

2. Haga clic en **guardar** desde la parte superior de Hola de pantalla de bienvenida y, a continuación, desde hello **Introducción** , haga clic en **iniciar**. En el cuadro de diálogo de hello, seleccione **tiempo personalizada**y, a continuación, establezca Hola fecha y hora actuales.

    ![Establecimiento de la hora del trabajo](./media/data-lake-store-stream-analytics/run.query.2.png "Establecimiento de la hora del trabajo")

    Haga clic en **iniciar** trabajo de hello toostart. Puede pasar hasta el trabajo hello toostart de tooa dos minutos.

3. datos tootrigger Hola trabajo toopick Hola de blob de hello, copie un contenedor de blobs ejemplo toohello de archivo de datos. Puede obtener un archivo de datos de ejemplo de Hola [repositorio de Git de Azure datos Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt). Para este tutorial, vamos a copiar archivo hello **vehicle1_09142014.csv**. Puede usar varios clientes, como [Azure Storage Explorer](http://storageexplorer.com/), contenedor de blobs de tooupload datos tooa.

4. De hello **Introducción** ficha **supervisión**, vea cómo se procesan los datos de Hola.

    ![Supervisión de trabajos](./media/data-lake-store-stream-analytics/run.query.3.png "Supervisión de trabajos")

5. Por último, puede comprobar que datos de salida del trabajo de hello están disponibles en la cuenta de almacén de Data Lake Hola. 

    ![Comprobación de la salida](./media/data-lake-store-stream-analytics/run.query.4.png "Comprobación de la salida")

    En el panel de exploración de datos de hello, observar que hello como resultado escrito tooa la ruta de acceso de carpeta como especificado en hello opciones de salida de almacén de Data Lake (`streamanalytics/job/output/{date}/{time}`).  

## <a name="see-also"></a>Otras referencias
* [Crear un toouse de clúster de HDInsight almacén de Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
