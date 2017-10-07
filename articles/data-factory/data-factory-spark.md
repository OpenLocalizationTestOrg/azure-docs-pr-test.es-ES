---
title: aaaInvoke Spark programas de Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo programas de Spark tooinvoke desde una factoría de datos de Azure con Hola actividad MapReduce."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a>Invocación de programas Spark desde canalizaciones de Azure Data Factory

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Actividad de Hive](data-factory-hive-activity.md)
> * [Actividad de Pig](data-factory-pig-activity.md)
> * [Actividad MapReduce](data-factory-map-reduce.md)
> * [Actividad de streaming de Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Actividad de Spark](data-factory-spark.md)
> * [Actividad de ejecución de Batch de Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Actividad Actualizar recurso de Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Actividad de procedimiento almacenado](data-factory-stored-proc-activity.md)
> * [Actividad U-SQL de Data Lake Analytics](data-factory-usql-activity.md)
> * [Actividad personalizada de .NET](data-factory-use-custom-activities.md)

## <a name="introduction"></a>Introducción
Actividad de Spark es uno de hello [las actividades de transformación de datos](data-factory-data-transformation-activities.md) compatible con Data Factory de Azure. Esta actividad ejecuta Hola especificado programa Spark en el clúster de Apache Spark en HDInsight de Azure.    

> [!IMPORTANT]
> - La actividad de Spark no admite clústeres de HDInsight Spark que usan una instancia de Azure Data Lake Store como almacenamiento principal.
> - La actividad de Spark admite solo los clústeres de HDInsight Spark existentes (los suyos propios). No admite un servicio vinculado de HDInsight a petición.

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a>Tutorial: creación de una canalización con actividad de Spark
Estos son los pasos típicos de hello toocreate una canalización de factoría de datos con una actividad de Spark.  

1. Creación de una factoría de datos.
2. Crear un toolink de servicio vinculado de almacenamiento de Azure en el almacenamiento de Azure que está asociado a la factoría de datos de toohello de clúster de HDInsight Spark.     
2. Crear un toolink de servicio vinculado de HDInsight de Azure su clúster Spark Apache de factoría de datos de toohello de HDInsight de Azure.
3. Crear un conjunto de datos que hace referencia el servicio de almacenamiento de Azure vinculada de toohello. Actualmente, debe especificar un conjunto de datos de salida para una actividad incluso si no se produce ninguna salida.  
4. Crear una canalización con la actividad de Spark que hace referencia el servicio vinculado de HDInsight de toohello creado en #2. actividad Hello se configura con el conjunto de datos de Hola que creó en el paso anterior de Hola como un conjunto de datos de salida. conjunto de datos de salida de Hello es qué unidades Hola programación (etcetera diariamente, cada hora,.). Por lo tanto, debe especificar el conjunto de datos de salida de hello aunque actividad hello no produce realmente un resultado.

### <a name="prerequisites"></a>Requisitos previos
1. Crear un **cuenta de almacenamiento de Azure para fines generales** siguiendo las instrucciones de tutorial de hello: [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account).  
2. Crear un **clúster Apache Spark en HDInsight de Azure** siguiendo las instrucciones de tutorial de hello: [clúster crear Apache Spark en HDInsight de Azure](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Asociar la cuenta de almacenamiento de Azure Hola que creó en el paso 1 de # con este clúster.  
3. Descargue y revise el archivo de script de python de hello **test.py** situado en: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).  
3.  Cargar **test.py** toohello **pyFiles** carpeta Hola **adfspark** contenedor en el almacenamiento de blobs de Azure. Crear contenedor de Hola y la carpeta de hello si no existen.

### <a name="create-data-factory"></a>Creación de Data Factory
Puede empezar con la creación de factoría de datos de hello en este paso.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Haga clic en **NEW** en el menú de la izquierda hello, haga clic en **datos + análisis**y haga clic en **factoría de datos**.
3. Hola **factoría de datos** hoja, escriba **SparkDF** para hello nombre.

   > [!IMPORTANT]
   > nombre de Hola Hola Azure factoría de datos debe ser **único global**. Si ve el error de hello: **nombre de generador de datos "SparkDF" no está disponible**. Cambiar nombre de Hola Hola factoría de datos (por ejemplo, yournameSparkDFdate y pruebe a crear de nuevo. Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.   
4. Seleccione hello **suscripción de Azure** donde desea Hola datos generador toobe creado.
5. Seleccione un **grupo de recursos** de Azure existente o cree uno nuevo.
6. Seleccione **toodashboard Pin** opción.  
6. Haga clic en **crear** en hello **factoría de datos** hoja.

   > [!IMPORTANT]
   > instancias de la factoría de datos de toocreate, debe ser miembro del programa Hola a [colaborador de la factoría de datos](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol en el nivel de grupo de recursos/suscripción Hola.
7. Vea factoría de datos de Hola se creen en hello **panel** de hello portal de Azure como se indica a continuación:   
8. Una vez creado correctamente la factoría de datos de hello, consulte página de factoría de datos de hello, que muestra Hola contenido Hola factoría de datos. Si no ve la página de factoría de datos de hello, haga clic en icono de saludo de la factoría de datos en el panel de Hola.

    ![Hoja de la Factoría de datos](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a>Crear servicios vinculados
En este paso, creará dos servicios vinculados, una toolink su factoría de datos de Spark clúster tooyour y Hola otro toolink su factoría de datos de almacenamiento de Azure tooyour.  

#### <a name="create-azure-storage-linked-service"></a>Creación de un servicio vinculado de Almacenamiento de Azure
En este paso, vincule la factoría de datos de tooyour de cuenta de almacenamiento de Azure. Un conjunto de datos que cree en un paso más adelante en este tutorial hace referencia servicio toothis vinculado. servicio vinculado de HDInsight que define en el paso siguiente Hola Hola hace referencia servicio toothis vinculado.  

1. Haga clic en **autor e implementar** en hello **factoría de datos** hoja de la factoría de datos. Debería ver Hola Editor de generador de datos.
2. Haga clic en **Nuevo almacén de datos** y elija **Azure Storage**.

   ![Nuevo almacén de datos - Azure Storage - menú](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. Debería ver Hola **script JSON** para crear un almacenamiento de Azure de servicio en el editor de hello vinculado.

   ![Servicio vinculado de Azure Storage](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. Reemplace **nombre-cuenta** y **clave de cuenta** con la clave de acceso y nombre de hello de la cuenta de almacenamiento de Azure. toolearn el proceso tooget el almacenamiento de acceso de clave, vea Hola información acerca de cómo tooview, copiar y regenerar almacenamiento tener acceso a claves de [administrar su cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
5. toodeploy Hola servicio vinculado, haga clic en **implementar** en la barra de comandos de Hola. Después de hello servicio vinculado se ha implementado correctamente, Hola **Draft-1** ventana debería desaparecer y verá **AzureStorageLinkedService** en vista de árbol de Hola Hola izquierda.

#### <a name="create-hdinsight-linked-service"></a>Creación del servicio vinculado de HDInsight
En este paso, creará toolink de servicio vinculado de HDInsight de Azure la factoría de datos de toohello de clúster de HDInsight Spark. clúster de HDInsight de Hello es programa de Spark de hello toorun utilizado especificado en la actividad de Spark hello de canalización de hello en este ejemplo.  

1. Haga clic en **... Más** en la barra de herramientas de hello, haga clic en **nuevo proceso**y, a continuación, haga clic en **clúster de HDInsight**.

    ![Creación del servicio vinculado de HDInsight](media/data-factory-spark/new-hdinsight-linked-service.png)
2. Copie y pegue Hola siguiente fragmento de código toohello **Draft-1** ventana. En el editor de JSON de hello, Hola pasos:
    1. Especificar hello **URI** para hello HDInsight Spark del clúster. Por ejemplo: `https://<sparkclustername>.azurehdinsight.net/`.
    2. Especificar nombre de Hola de hello **usuario** quién tiene clúster de Spark toohello de acceso.
    3. Especificar hello **contraseña** para el usuario.
    4. Especificar hello **servicio vinculado de almacenamiento de Azure** que está asociado con el clúster de HDInsight Spark hello. En este ejemplo, es: **AzureStorageLinkedService**.

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - La actividad de Spark no admite clústeres de HDInsight Spark que usan una instancia de Azure Data Lake Store como almacenamiento principal.
    > - La actividad de Spark admite solo el clúster de HDInsight Spark existente (el suyo propio). No admite un servicio vinculado de HDInsight a petición.

    Vea [servicio vinculado de HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obtener más información acerca de hello HDInsight servicio vinculado.
3.  toodeploy Hola servicio vinculado, haga clic en **implementar** en la barra de comandos de Hola.  

### <a name="create-output-dataset"></a>Creación del conjunto de datos de salida
conjunto de datos de salida de Hello es qué unidades Hola programación (etcetera diariamente, cada hora,.). Por lo tanto, debe especificar un conjunto de datos de salida para la actividad de spark hello en canalización Hola aunque actividad hello realmente no genera ningún resultado. Especificar un conjunto de datos de entrada para la actividad de hello es opcional.

1. Hola **Editor de generador de datos**, haga clic en **... Más** en la barra de comandos de hello, haga clic en **nuevo conjunto de datos**y seleccione **almacenamiento de blobs de Azure**.  
2. Copie y pegue Hola después de la ventana de toohello Draft-1 de fragmentos de código. el fragmento de código de Hello JSON define un conjunto de datos denominado **OutputDataset**. Además, se especifica que los resultados de Hola se almacenen en contenedor de blob de hello denominado **adfspark** y carpeta Hola llamada **pyFiles/salida**. Como se mencionó anteriormente, este conjunto de datos es un conjunto de datos ficticio. programa de Spark Hello en este ejemplo no genera ningún resultado. Hola **disponibilidad** sección especifica ese conjunto de datos de salida de hello se generen diariamente.  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy Hola conjunto de datos, haga clic en **implementar** en la barra de comandos de Hola.


### <a name="create-pipeline"></a>Creación de una canalización
En este paso, crea una canalización con una actividad de **HDInsightSpark**. Actualmente, el conjunto de datos de salida es qué unidades Hola programación, por lo que debe crear un conjunto de datos de salida aunque actividad hello no genera ningún resultado. Si la actividad hello no toma ninguna entrada, puede omitir creación Hola de conjunto de datos entrada. Por lo tanto, no se especifica ningún conjunto de datos de entrada en este ejemplo.

1. Hola **Editor de generador de datos**, haga clic en **... Más** en Hola barra de comandos y, a continuación, haga clic en **nueva canalización**.
2. Reemplace el script de Hola en ventana hello Draft-1 con hello siguiente secuencia de comandos:

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    Tenga en cuenta Hola siguientes puntos:
    - Hola **tipo** propiedad se establece demasiado**HDInsightSpark**.
    - Hola **Ruta_raíz** se establece demasiado**adfspark\\pyFiles** donde adfspark es contenedor de blobs de Azure de Hola y pyFiles es la carpeta correctamente en ese contenedor. En este ejemplo, hello almacenamiento de blobs de Azure es hello uno que esté asociado con el clúster de Spark Hola. Puede cargar Hola archivo tooa almacenamiento de Azure diferente. Si lo hace, cree un toolink de servicio vinculado de almacenamiento de Azure que factoría de datos de toohello de cuenta de almacenamiento. A continuación, especificar nombre de Hola de servicio de hello vinculado como un valor de hello **sparkJobLinkedService** propiedad. Vea [propiedades de la actividad de Spark](#spark-activity-properties) para obtener más información acerca de esta propiedad y otras propiedades compatibles con hello Spark actividad.  
    - Hola **entryFilePath** se establece toohello **test.py**, que es el archivo de python de hello.
    - Hola **getDebugInfo** propiedad se establece demasiado**siempre**, lo que significa que los archivos de registro de hello siempre están generado (éxito o error).

        > [!IMPORTANT]
        > Se recomienda que no establezca esta propiedad demasiado`Always` en un entorno de producción a menos que esté solucionando un problema.
    - Hola **genera** sección tiene un conjunto de datos de salida. Debe especificar un conjunto de datos de salida, incluso si el programa de spark hello no genera ningún resultado. Hola salida dataset unidades Hola programación para canalización hello (etcetera diariamente, cada hora,.).  

        Para obtener más información sobre las propiedades de hello admitidas por las actividades de Spark, consulte [inspirará propiedades de la actividad](#spark-activity-properties) sección.
3. canalización de hello toodeploy, haga clic en **implementar** en la barra de comandos de Hola.

### <a name="monitor-pipeline"></a>Supervisión de la canalización
1. Haga clic en **X** tooclose hojas de Editor de generador de datos y toonavigate página principal de toohello factoría de datos de nuevo. Haga clic en **supervisar y administrar** hello toolaunch supervisión de la aplicación en otra ficha.

    ![Icono Supervisión y administración](media/data-factory-spark/monitor-and-manage-tile.png)
2. Hola de cambio **hora de inicio** filtrar en la parte superior de hello demasiado**2/1/2017**y haga clic en **aplicar**.
3. Debería ver sólo una ventana de actividad como hay solo un día entre hello (2017-02-01) de inicio y finalización (2017-02-02) de canalización de Hola. Confirme que está ese segmento de datos de hello en **listo** estado.

    ![Canalización de Hola de Monitor](media/data-factory-spark/monitor-and-manage-app.png)    
4. Seleccione hello **ventana actividad** toosee detalles acerca de la ejecución de la actividad de Hola. Si se produce un error, puede ver detalles sobre él en el panel derecho de Hola.

### <a name="verify-hello-results"></a>Comprobar los resultados de Hola

1. Inicie **Jupyter Notebook** para el clúster de HDInsight Spark; para ello, navegue a: https://CLUSTERNAME.azurehdinsight.net/jupyter. También puede iniciar el panel del clúster de HDInsight Spark y después inicie **Jupyter Notebook**.
2. Haga clic en **New** -> **PySpark** toostart un nuevo bloc de notas.

    ![Nuevo Jupyter Notebook](media/data-factory-spark/jupyter-new-book.png)
3. Ejecución hello después del comando de copia y pegado de texto hello y presionando **MAYÚS + ENTRAR** final hello de la segunda instrucción de Hola.  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. Confirme que ve los datos de saludo de tabla de hvac Hola:  

    ![Resultados de la consulta Jupyter](media/data-factory-spark/jupyter-notebook-results.png)

Vea la sección [Ejecución de una consulta de Spark SQL](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) para obtener instrucciones detalladas. 

### <a name="troubleshooting"></a>Solución de problemas
Puesto que establece **getDebugInfo** demasiado**siempre**, verá un **registro** subcarpeta en hello **pyFiles** carpeta en el contenedor de blobs de Azure. archivo de registro de Hello en carpeta de registro de hello proporciona detalles adicionales. Este archivo de registro es especialmente útil cuando se produce un error. En un entorno de producción, puede que desee tooset se demasiado**error**.

Para solucionar problemas, Hola pasos:


1. Navegue demasiado`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.

    ![Aplicación de IU de YARN](media/data-factory-spark/yarnui-application.png)  
2. Haga clic en **registros** para uno de hello ejecutar intentos.

    ![Página de aplicación](media/data-factory-spark/yarn-applications.png)
3. Debería ver la información de error adicional en la página de registro de hello.

    ![Error de registro](media/data-factory-spark/yarnui-application-error.png)

Hello las secciones siguientes proporciona información sobre clústeres de Apache Spark de toouse de entidades de factoría de datos y la actividad de Spark en la factoría de datos.

## <a name="spark-activity-properties"></a>Propiedades de la actividad de Spark
Aquí está la definición de JSON de ejemplo de Hola de una canalización con Spark actividad:    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

Hello tabla siguiente describen propiedades JSON de hello utilizadas en hello definición JSON:

| Propiedad | Descripción | Obligatorio |
| -------- | ----------- | -------- |
| name | Nombre de actividad de hello en canalización Hola. | Sí |
| description | Texto que describe qué actividad hello hace. | No |
| type | Esta propiedad se debe establecer tooHDInsightSpark. | Sí |
| linkedServiceName | El nombre del programa Hola a HDInsight vinculados en qué Hola Spark se ejecuta el programa de servicio. | Sí |
| rootPath | contenedor de blobs de Azure de Hola y la carpeta que contiene el archivo de hello Spark. nombre de archivo de Hello distingue mayúsculas de minúsculas. | Sí |
| entryFilePath | Carpeta de raíz de toohello de ruta de acceso relativa del programa Hola Spark/paquete de código. | Sí |
| className | Clase principal de Spark o Java de la aplicación. | No |
| argumentos | Una lista de programas de Spark de toohello argumentos de línea de comandos. | No |
| proxyUser | programa de Spark hello tooexecute de tooimpersonate de la cuenta de usuario de Hola | No |
| sparkConfig | Especificar valores para propiedades de configuración de Spark enumerados en el tema de hello: [configuración Spark - propiedades de la aplicación](https://spark.apache.org/docs/latest/configuration.html#available-properties). | No |
| getDebugInfo | Especifica cuando los archivos de registro de hello Spark son copiado toohello utilizado por el clúster de HDInsight de almacenamiento de Azure (o) especificado por sparkJobLinkedService. Valores permitidos: Ninguno, Siempre o Error. Valor predeterminado: Ninguno. | No |
| sparkJobLinkedService | Hola servicio vinculado de almacenamiento de Azure que contiene registros, las dependencias y archivo de trabajo de hello Spark.  Si no especifica un valor para esta propiedad, se usa almacenamiento de hello asociado con el clúster de HDInsight. | No |

## <a name="folder-structure"></a>Estructura de carpetas
Hola actividad Spark no es compatible con una secuencia de comandos en línea como Pig y realizar actividades de Hive. Los trabajos de Spark también son más ampliable que los de Pig y Hive. Para los trabajos de Spark, puede proporcionar varias dependencias, como paquetes (ubicados en java Hola CLASSPATH), python archivos jar (ubicados en hello PYTHONPATH) y cualquier otro archivo.

Crear Hola siguiendo la estructura de carpetas en Hola Hola servicio vinculado de HDInsight al que hace referencia el almacenamiento de blobs de Azure. A continuación, cargue los archivos dependientes toohello adecuado subcarpetas en carpeta de raíz de hello representado por **entryFilePath**. Por ejemplo, cargar subcarpeta de python archivos toohello pyFiles y jar archivos toohello archivos JAR subcarpeta de la carpeta raíz de Hola. En tiempo de ejecución, el servicio de factoría de datos espera Hola siguiendo la estructura de carpetas en hello almacenamiento de blobs de Azure:     

| Ruta de acceso | Descripción | Obligatorio | Escriba |
| ---- | ----------- | -------- | ---- |
| . | ruta de acceso de Hello raíz del trabajo de Spark hello en el servicio vinculado de almacenamiento de Hola    | Sí | Carpeta |
| &lt;Definida por el usuario&gt; | ruta de acceso de Hola que señala toohello archivo de entrada de trabajo de Spark Hola | Sí | Archivo |
| ./jars | Todos los archivos en esta carpeta se cargan y se colocan en classpath de java de Hola de clúster de Hola | No | Carpeta |
| ./pyFiles | Todos los archivos en esta carpeta se cargan y se colocan en hello PYTHONPATH de clúster de Hola | No | Carpeta |
| ./files | Todos los archivos de esta carpeta se cargan y se colocan en el directorio de trabajo del ejecutor. | No | Carpeta |
| ./archives | Todos los archivos de esta carpeta están sin comprimir. | No | Carpeta |
| ./logs | carpeta de Hola donde se almacenan los registros del clúster de Spark Hola.| No | Carpeta |

Este es un ejemplo de un almacenamiento que contiene dos archivos de trabajo de Spark en hello almacenamiento de blobs de Azure al que hace referencia Hola servicio vinculado de HDInsight.

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
