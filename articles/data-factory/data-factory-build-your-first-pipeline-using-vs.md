---
title: "aaaBuild su primera factoría de datos (Visual Studio) | Documentos de Microsoft"
description: "En este tutorial, creará un de ejemplo de canalización de Data Factory de Azure mediante Visual Studio."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 0c5eb01b685d978d80916da0293cc2d3701b2d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a>Tutorial: Creación de una instancia de Data Factory mediante Visual Studio
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [Introducción y requisitos previos](data-factory-build-your-first-pipeline.md)
> * [Portal de Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Plantilla de Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API DE REST](data-factory-build-your-first-pipeline-using-rest-api.md)

Este tutorial muestra cómo toocreate una factoría de datos de Azure mediante Visual Studio. Crear un proyecto de Visual Studio con plantilla de proyecto de hello factoría de datos, definir entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización) en formato JSON y, a continuación, publicar o implementar el estos nube toohello de entidades. 

canalización de Hello en este tutorial tiene una actividad: **actividad de HDInsight Hive**. Esta actividad ejecuta un script de hive en un clúster de HDInsight de Azure que las transformaciones de entrada de datos de salida de datos tooproduce. canalización de Hello es toorun programado una vez que un mes entre Hola especificado horas de inicio y finalización. 

> [!NOTE]
> Este tutorial no muestra cómo copiar datos mediante Azure Data Factory. Para obtener un tutorial sobre cómo toocopy los datos mediante Data Factory de Azure, consulte [Tutorial: copiar los datos de la base de datos del almacenamiento de blobs tooSQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> pero cualquier canalización puede tener más de una actividad. Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad. Para más información, consulte [Programación y ejecución en Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).


## <a name="walkthrough-create-and-publish-data-factory-entities"></a>Tutorial: Creación y publicación de entidades de Data Factory
Estos son los pasos de hello que realizar como parte de este tutorial:

1. Cree dos servicios vinculados: **AzureStorageLinkedService1** y **HDInsightOnDemandLinkedService1**. 
   
    En este tutorial, los datos de entrada y salidos para la actividad de hive hello son en Hola mismo almacenamiento de blobs de Azure. Use un petición HDInsight clúster tooprocess datos de entrada tooproduce datos de salida existentes. clúster de HDInsight a petición Hola se crea automáticamente para usted Data Factory de Azure en tiempo de ejecución cuando los datos de entrada de hello están listo toobe procesado. Es necesario toolink los datos se almacenan o calcula tooyour factoría de datos para que el servicio de factoría de datos de hello puede conectarse toothem en tiempo de ejecución. Por lo tanto, vincular su factoría de datos de cuenta de almacenamiento de Azure toohello mediante hello AzureStorageLinkedService1 y vincular un clúster de HDInsight a petición mediante hello HDInsightOnDemandLinkedService1. Al publicar, especifique nombre Hola Hola datos generador toobe creado o un generador de datos existente.  
2. Crear dos conjuntos de datos: **InputDataset** y **OutputDataset**, que representan los datos de entrada/salida de hello que se almacenan en hello almacenamiento de blobs de Azure. 
   
    Estas definiciones de conjunto de datos, consulte servicio vinculado de almacenamiento de Azure de toohello creado en el paso anterior de Hola. Para hello InputDataset, especifique el contenedor de blobs de hello (adfgetstarted) y Hola carpeta (inptutdata) que contiene un blob con datos de entrada de Hola. Para hello OutputDataset, especifique el contenedor de blobs de hello (adfgetstarted) y carpeta hello (partitioneddata) que contiene los datos de salida de hello. Especifique también otras propiedades como estructura, disponibilidad y directiva.
3. Cree una canalización llamada **MyFirstPipeline**. 
  
    En este tutorial, canalización de hello tiene sólo una actividad: **actividad de Hive de HDInsight**. Esta transformación de actividad de entrada de datos de salida de datos tooproduce mediante la ejecución de un script de hive en un clúster de HDInsight a petición. toolearn más información acerca de la actividad de hive, consulte [actividad de Hive](data-factory-hive-activity.md) 
4. Cree una instancia de Data Factory denominada **DataFactoryUsingVS**. Implementar la factoría de datos de Hola y todas las entidades de la factoría de datos (servicios vinculados, tablas y canalización de hello).
5. Después de publicar, use hojas de portal de Azure y canalización de hello toomonitor de supervisión y administración de aplicaciones. 
  
### <a name="prerequisites"></a>Requisitos previos
1. Lea [Tutorial de introducción](data-factory-build-your-first-pipeline.md) hello completa y artículo **prerequisite** pasos. También puede seleccionar hello **información general y requisitos previos** opción en la lista desplegable de hello en el artículo toohello de hello tooswitch superior. Después de completar los requisitos previos de hello, cambie toothis atrás artículo mediante la selección **Visual Studio** opción en la lista desplegable de Hola.
2. instancias de la factoría de datos de toocreate, debe ser miembro del programa Hola a [colaborador de la factoría de datos](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol en el nivel de grupo de recursos/suscripción Hola.  
3. Debe tener instalado en el equipo siguiente de hello:
   * Visual Studio 2013 o Visual Studio 2015.
   * Descargue el SDK de Azure para Visual Studio 2013 o Visual Studio 2015. Navegue demasiado[página de descargas de Azure](https://azure.microsoft.com/downloads/) y haga clic en **VS 2013** o **VS 2015** en hello **.NET** sección.
   * Descargue el complemento de Data Factory de Azure más reciente de Hola para Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) o [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). También puede actualizar Hola complemento mediante Hola pasos: en el menú de hello, haga clic en **herramientas** -> **extensiones y actualizaciones** -> **en línea**  ->  **Galería de visual Studio** -> **herramientas de generador de datos de Microsoft Azure para Visual Studio** -> **actualización**.

Ahora, vamos a usar Visual Studio toocreate un generador de datos de Azure.

### <a name="create-visual-studio-project"></a>Creación de un proyecto de Visual Studio
1. Inicie **Visual Studio 2013** o **Visual Studio 2015**. Haga clic en **archivo**, seleccione demasiado**New**y haga clic en **proyecto**. Debería ver Hola **nuevo proyecto** cuadro de diálogo.  
2. Hola **nuevo proyecto** cuadro de diálogo, seleccione hello **DataFactory** plantilla y haga clic en **proyecto vacío de la factoría de datos**.   

    ![Cuadro de diálogo Nuevo proyecto](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. Escriba un **nombre** para el proyecto de hello, **ubicación**y el nombre de hello **solución**y haga clic en **Aceptar**.

    ![Explorador de soluciones](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a>Crear servicios vinculados
En este paso se crean dos servicios vinculados: **Azure Storage** y **HDInsight a petición**. 

Hola almacenamiento de Azure había vinculada a vínculos de servicio su factoría de datos de almacenamiento de Azure cuenta toohello proporcionando información de conexión de Hola. Servicio de factoría de datos utiliza la cadena de conexión de Hola desde configuración de servicio vinculado de hello tooconnect toohello almacenamiento de Azure en tiempo de ejecución. Este almacenamiento contiene entrada y salida los datos de canalización de Hola y Hola hive utilizado por la actividad de hive Hola de archivo de script. 

Con el servicio de vinculado de HDInsight a petición, Hola clúster de HDInsight se crea automáticamente en tiempo de ejecución, cuando los datos de entrada de hello tooprocessed listo. clúster de Hola se elimina después de hacerlo inactivos y procesamiento para el período de tiempo especificado de Hola. 

> [!NOTE]
> Cree una factoría de datos especificando su nombre y la configuración en tiempo de presentación de la solución de la factoría de datos de publicación.

#### <a name="create-azure-storage-linked-service"></a>Creación de un servicio vinculado de Almacenamiento de Azure
1. Haga clic en **servicios vinculados** Hola Explorador de soluciones, seleccione demasiado**agregar**y haga clic en **nuevo elemento**.      
2. Hola **Agregar nuevo elemento** cuadro de diálogo, seleccione **servicio vinculado de almacenamiento de Azure** en lista de Hola y haga clic en **agregar**.
    ![Servicio vinculado de Azure Storage](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)
3. Reemplace `<accountname>` y `<accountkey>` con el nombre de Hola de su cuenta de almacenamiento de Azure y su clave. toolearn el proceso tooget el almacenamiento de acceso de clave, vea Hola información acerca de cómo tooview, copiar y regenerar almacenamiento tener acceso a claves de [administrar su cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
    ![Servicio vinculado de Azure Storage](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)
4. Guardar hello **AzureStorageLinkedService1.json** archivo.

#### <a name="create-azure-hdinsight-linked-service"></a>Creación de un servicio vinculado de HDInsight de Azure
1. Hola **el Explorador de soluciones**, haga clic en **servicios vinculados**, seleccione demasiado**agregar**y haga clic en **nuevo elemento**.
2. Seleccione **HDInsight On Demand Linked Service** (Servicio vinculado de HDInsight a petición) y haga clic en **Agregar**.
3. Reemplace hello **JSON** con hello después JSON:

     ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
        "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:

    Propiedad | Descripción
    -------- | ----------- 
    ClusterSize | Especifica el tamaño de Hola de hello clúster de Hadoop de HDInsight.
    TimeToLive | Especifica ese tiempo de inactividad de hello para el clúster de HDInsight de hello, antes de eliminarla.
    linkedServiceName | Especifica la cuenta de almacenamiento de Hola que es registros de hello toostore usado generadas por clúster de Hadoop de HDInsight. 

    > [!IMPORTANT]
    > clúster de HDInsight de Hello crea un **contenedor predeterminado** en almacenamiento de blobs de Hola que especificó en hello JSON (linkedServiceName). HDInsight no elimine este contenedor cuando se elimina el clúster de Hola. Este comportamiento es así por diseño. Con el servicio vinculado de HDInsight a petición se crea un clúster de HDInsight cada vez que se procesa un segmento, a menos que haya un clúster existente activo (timeToLive). clúster de Hola se elimina automáticamente cuando se realiza un procesamiento Hola.
    > 
    > A medida que se procesen más segmentos, verá numerosos contenedores en su Almacenamiento de blobs de Azure. Si no se necesita para solucionar problemas de trabajos de hello, quizá le interese toodelete ellos el costo de almacenamiento de tooreduce Hola. nombres de Hola de estos contenedores siguen un patrón: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`. Usar herramientas como [Explorador de almacenamiento de Microsoft](http://storageexplorer.com/) almacenamiento de blobs de contenedores de toodelete en Azure.

    Para más información sobre las propiedades JSON, consulte [Servicios vinculados de procesos](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). 
4. Guardar hello **HDInsightOnDemandLinkedService1.json** archivo.

### <a name="create-datasets"></a>Creación de conjuntos de datos
En este paso, creación de conjuntos de datos toorepresent Hola entrada y salida de datos para el procesamiento de Hive. Estos conjuntos de datos, consulte toohello **AzureStorageLinkedService1** ha creado anteriormente en este tutorial. Hola tooan de puntos de servicio vinculado cuenta de almacenamiento de Azure y los conjuntos de datos especifiquen contenedor, carpeta, nombre de archivo en el almacenamiento de Hola que contiene la entrada y salida de datos.   

#### <a name="create-input-dataset"></a>Creación de un conjunto de datos de entrada
1. Hola **el Explorador de soluciones**, haga clic en **tablas**, seleccione demasiado**agregar**y haga clic en **nuevo elemento**.
2. Seleccione **Azure Blob** de lista de hello, cambiar nombre de Hola de archivo hello demasiado**InputDataSet.json**y haga clic en **agregar**.
3. Reemplace hello **JSON** en el editor de hello con hello siguiente fragmento de JSON:

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
            "typeProperties": {
                "fileName": "input.log",
                "folderPath": "adfgetstarted/inputdata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            },
            "external": true,
            "policy": {}
        }
    }
    ```
    Este fragmento de JSON define un conjunto de datos denominado **AzureBlobInput** que representa datos de entrada para la actividad de hive hello en canalización Hola. Especifica que los datos de entrada de Hola se encuentran en contenedor de blob de hello denominado `adfgetstarted` y carpeta Hola llamada `inputdata`.

    Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:

    Propiedad | Descripción |
    -------- | ----------- |
    type |propiedad de tipo Hello se establece demasiado**AzureBlob** porque los datos residen en el almacenamiento de blobs de Azure.
    linkedServiceName | Se refiere toohello AzureStorageLinkedService1 que creó anteriormente.
    fileName |Esta propiedad es opcional. Si se omite esta propiedad, se seleccionan todos los archivos de Hola de hello folderPath. En este caso, se procesa solo hello input.log.
    type | archivos de registro de Hello están en formato de texto, por lo que usamos TextFormat. |
    columnDelimiter | las columnas en los archivos de registro de hello están delimitadas por coma de hello (`,`)
    frecuencia/intervalo | la frecuencia debe establecer tooMonth y interval es 1, lo que significa que están disponibles los segmentos de entrada de hello mensualmente.
    external | Esta propiedad se establece tootrue si no se generan datos de entrada de hello para la actividad de hello canalización Hola. Esta propiedad solo se especifica en los conjuntos de datos de entrada. Para hello entrada conjunto de datos de la primera actividad de hello siempre establézcala tootrue.
4. Guardar hello **InputDataset.json** archivo.

#### <a name="create-output-dataset"></a>Creación del conjunto de datos de salida
Ahora, cree Hola salida dataset toorepresent salida los datos almacenados en hello almacenamiento de blobs de Azure.

1. Hola **el Explorador de soluciones**, haga clic en **tablas**, seleccione demasiado**agregar**y haga clic en **nuevo elemento**.
2. Seleccione **Azure Blob** de lista de hello, cambiar nombre de Hola de archivo hello demasiado**OutputDataset.json**y haga clic en **agregar**.
3. Reemplace hello **JSON** en el editor de hello con hello después JSON:
    
    ```json
    {
        "name": "AzureBlobOutput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
            "typeProperties": {
                "folderPath": "adfgetstarted/partitioneddata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            }
        }
    }
    ```
    el fragmento de código de Hello JSON define un conjunto de datos denominado **AzureBlobOutput** que representa los datos generados por la actividad de hive hello en canalización Hola de salida. Especifica que se encuentra ubicada actividad de hive hello generan la información de salida de hello en contenedor de blob de hello denominado `adfgetstarted` y carpeta Hola llamada `partitioneddata`. 
    
    Hola **disponibilidad** sección especifica ese conjunto de datos de salida de hello se genera mensualmente. programación de hello unidades y conjunto de datos de salida Hola de canalización de Hola. canalización de Hola se ejecuta mensualmente entre sus horas de inicio y finalización. 

    Vea **crear conjunto de datos de entrada de hello** sección para obtener una descripción de estas propiedades. No establecer propiedad externo de hello en un conjunto de datos de salida como conjunto de datos de hello es generado por la canalización de Hola.
4. Guardar hello **OutputDataset.json** archivo.

### <a name="create-pipeline"></a>Creación de una canalización
Servicio vinculado de almacenamiento de Azure de Hola y conjuntos de datos de entrada y salida se han creado hasta ahora. Ahora, cree una canalización con una actividad **HDInsightHive**. Hola **entrada** hive Hola actividad se establece demasiado**AzureBlobInput** y **salida** se establece demasiado**AzureBlobOutput**. Un segmento de un conjunto de datos de entrada está disponible mensual (frecuencia: mes, intervalo: 1), y Hola salida segmento se genera mensualmente demasiado. 

1. Hola **el Explorador de soluciones**, haga clic en **canalizaciones**, seleccione demasiado**agregar**y haga clic en **nuevo elemento.**
2. Seleccione **canalización de transformación de Hive** en lista de Hola y haga clic en **agregar**.
3. Reemplace hello **JSON** con hello siguiente fragmento de código:

    > [!IMPORTANT]
    > Reemplace `<storageaccountname>` con el nombre de saludo de la cuenta de almacenamiento.

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService1",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2016-04-01T00:00:00Z",
            "end": "2016-04-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    > [!IMPORTANT]
    > Reemplace `<storageaccountname>` con el nombre de saludo de la cuenta de almacenamiento.

    el fragmento de código de Hello JSON define una canalización que consta de una sola actividad (actividad de Hive). Esta actividad ejecuta un datos de entrada de tooprocess de script de Hive en un datos de salida a petición tooproduce de clúster de HDInsight. En la sección de actividades de Hola Hola de canalización de JSON, vea sólo una actividad en la matriz de hello con el tipo establecido demasiado**HDInsightHive**. 

    En Propiedades de tipo hello que son la actividad de Hive tooHDInsight específico, puede especificar qué servicio vinculado de almacenamiento de Azure tiene el archivo de script de hive hello, archivo de script de toohello de ruta de acceso de hello y archivo de script de toohello de parámetros. 

    archivo de script de Hive de Hello, **partitionweblogs.hql**, se almacena en la cuenta de almacenamiento de Azure de hello (especificado mediante scriptLinkedService Hola) y en hello `script` carpeta en el contenedor de hello `adfgetstarted`.

    Hola `defines` sección es la configuración de en tiempo de ejecución de hello toospecify utilizado que se pasa el script de hive toohello como valores de configuración de Hive (por ejemplo `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.

    Hola **iniciar** y **final** propiedades de canalización de hello especifica el periodo activo de Hola de canalización de Hola. Configurar hello toobe de conjunto de datos generado de mes, por lo tanto, solo una vez que se genera el segmento canalización hello (porque el mes de hello es el mismo en las fechas de inicio y fin).

    En JSON de la actividad de hello, especifique ese script de Hive Hola se ejecuta en proceso Hola especificado por hello **linkedServiceName** : **HDInsightOnDemandLinkedService**.
4. Guardar hello **HiveActivity1.json** archivo.

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a>Adición de partitionweblogs.hql e input.log como una dependencia
1. Haga clic en **dependencias** en hello **el Explorador de soluciones** ventana, señale demasiado**agregar**y haga clic en **elemento existente**.  
2. Navegue toohello **C:\ADFGettingStarted** y seleccione **partitionweblogs.hql**, **input.log** archivos y haga clic en **agregar**. Crea estos dos archivos como parte de los requisitos previos de hello [Tutorial Introducción](data-factory-build-your-first-pipeline.md).

Cuando se publica la solución de hello en el paso siguiente de hello, Hola **partitionweblogs.hql** archivo está cargado toohello **script** carpeta Hola `adfgetstarted` contenedor de blobs.   

### <a name="publishdeploy-data-factory-entities"></a>Publicación e implementación de las entidades de Data Factory
En este paso, publicar las entidades de la factoría de datos de hello (servicios vinculados, conjuntos de datos y canalización) en su toohello proyecto servicio Data Factory de Azure. En proceso de Hola de publicación, se especifica nombre hello de la factoría de datos. 

1. Haga clic en el proyecto en el Explorador de soluciones de Hola y haga clic en **publicar**.
2. Si ve **iniciar sesión en la cuenta de Microsoft tooyour** cuadro de diálogo, escriba sus credenciales de cuenta de hello que tenga la suscripción de Azure y haga clic en **iniciar sesión en**.
3. Debería ver Hola después el cuadro de diálogo:

   ![Cuadro de diálogo Publicar](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. Hola **factoría de datos de configuración** página, Hola lo siguiente:

    ![Publicar: nueva configuración de Data Factory](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. Seleccione la opción **Crear la nueva factoría de datos** .
   2. Escriba un nombre único **nombre** de factoría de datos de Hola. Por ejemplo: **DataFactoryUsingVS09152016**. nombre de Hello debe ser único globalmente.
   3. Seleccione Hola suscripción derecho para hello **suscripción** campo. 
        > [!IMPORTANT]
        > Si no ve ninguna suscripción, asegúrese de que inició sesión mediante una cuenta que sea un administrador o Coadministrador de suscripción de Hola.
   4. Seleccione hello **grupo de recursos** para toobe de factoría de datos de hello creado.
   5. Seleccione hello **región** de factoría de datos de Hola.
   6. Haga clic en **siguiente** tooswitch toohello **publicar elementos** página. (Presione **ficha** toomove fuera Hola de hello nombre campo tooif **siguiente** botón está deshabilitado.)

    > [!IMPORTANT]
    > Si recibe el error hello **nombre de generador de datos "DataFactoryUsingVS" no está disponible** al publicar, cambie el nombre de hello (por ejemplo, yournameDataFactoryUsingVS). Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.   
1. Hola **publicar elementos** página, asegúrese de que todas las factorías de datos de entidades están seleccionadas y haga clic en Hola **siguiente** tooswitch toohello **resumen** página.

    ![Página Publicar elementos](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. Revise el resumen de Hola y haga clic en **siguiente** Hola de proceso y la vista de la implementación del hello toostart **estado de implementación**.

    ![Página de resumen](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. Hola **estado de implementación** página, debería ver estado de Hola Hola del proceso de implementación. Después de que se realice la implementación de hello, haga clic en Finalizar.

Toonote puntos importantes:

- Si recibe el error hello: **esta suscripción no tiene espacio de nombres registrado toouse Microsoft.DataFactory**, siga uno de los procedimientos de Hola e intente publicar de nuevo:
    - En Azure PowerShell, ejecute hello después de proveedor del comando tooregister Hola factoría de datos.
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        Puede ejecutar Hola después comando tooconfirm ese Hola factoría de datos de proveedor está registrado.

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - Inicio de sesión mediante Hola suscripción de Azure en toohello [portal de Azure](https://portal.azure.com) y navegar por hoja de la factoría de datos de tooa crear una factoría de datos en el portal de Azure hello (o). Esta acción registra automáticamente proveedor Hola para usted.
- nombre Hola Hola factoría de datos se puede registrarse como un nombre DNS en hello futuras y, por tanto, se convierten en visible públicamente.
- instancias de la factoría de datos de toocreate, deberá toobe un administrador o Coadministrador de hello suscripción de Azure

### <a name="monitor-pipeline"></a>Supervisión de la canalización
En este paso, supervisar canalización hello mediante la vista de diagrama de la factoría de datos de Hola. 

#### <a name="monitor-pipeline-using-diagram-view"></a>Supervisión de una canalización desde la vista de diagrama
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/), Hola lo siguiente:
   1. Haga clic en **More services** (Más servicios) y en **Fábricas de datos**.
       
        ![Examinar factorías de datos](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. Nombre de hello SELECT de la factoría de datos (por ejemplo: **DataFactoryUsingVS09152016**) de lista de Hola de factorías de datos.
   
       ![Seleccione su factoría de datos](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. En la página principal de saludo de la factoría de datos, haga clic en **diagrama**.

    ![Icono Diagrama](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. En la vista de diagrama de hello, verá información general de las canalizaciones de Hola y conjuntos de datos usados en este tutorial.

    ![Vista de diagrama](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. tooview todas las actividades de canalización de hello, menú contextual "canalización" Hola, diagrama y haga clic en abrir canalización.

    ![Menú Abrir canalización](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. Confirme que ve actividad HDInsightHive de hello en canalización Hola.

    ![Vista Abrir canalización](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    toonavigate realizar copias toohello vista anterior, haga clic en **factoría de datos** en el menú de la ruta de navegación de hello en la parte superior de Hola.
6. Hola **vista de diagrama**, haga doble clic en el conjunto de datos de hello **AzureBlobInput**. Confirme que dicho sector Hola está en **listo** estado. Pueden tardar unos minutos para tooshow de segmento de hello en estado listo. Si no se realiza después de que espere unos instantes, ver si tiene archivos de entrada de hello (input.log) colocadas en contenedor derecho hello (`adfgetstarted`) y la carpeta (`inputdata`). Y asegúrese de que ese hello **externo** propiedad en el conjunto de datos de entrada de Hola se establece demasiado**true**. 

   ![Segmento de entrada con estado Listo](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. Haga clic en **X** tooclose **AzureBlobInput** hoja.
8. Hola **vista de diagrama**, haga doble clic en el conjunto de datos de hello **AzureBlobOutput**. Vea dicho sector Hola que se está procesando actualmente.

   ![Dataset](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. Cuando se realiza el procesamiento, verá que el segmento de hello en **listo** estado.

   > [!IMPORTANT]
   > La creación de un clúster de HDInsight a petición normalmente tarda algún tiempo (20 minutos aproximadamente). Por consiguiente, esperan Hola canalización tootake **aproximadamente 30 minutos** tooprocess Hola segmento.  
   
    ![Dataset](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. Cuando se encuentra el segmento de hello en **listo** de estado, compruebe hello `partitioneddata` carpeta Hola `adfgetstarted` contenedor en el almacenamiento de blobs para hello los datos de salida.  

    ![datos de salida](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. Haga clic en hello segmento toosee detalles sobre él en un **el segmento de datos** hoja.

    ![Detalles de segmento de datos](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. Haga clic en una actividad que se ejecutan en hello **lista ejecuta la actividad** toosee detalles sobre la actividad de ejecución (actividad de Hive en nuestro escenario) un **detalles de ejecución de la actividad** ventana. 
  
    ![Detalles de ejecución de actividad](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    Desde archivos de registro de hello, puede ver información de estado y de consulta de Hive de Hola que se ejecutó. Estos registros son útiles para solucionar cualquier problema.  

Vea [supervisar conjuntos de datos y canalización](data-factory-monitor-manage-pipelines.md) para obtener instrucciones sobre cómo canalización de toouse hello toomonitor portal Azure hello y conjuntos de datos ha creado en este tutorial.

#### <a name="monitor-pipeline-using-monitor--manage-app"></a>Supervisión de una canalización con la Aplicación de supervisión y administración
También puede utilizar el Monitor de & Administrar aplicación toomonitor sus canalizaciones. Para más información acerca del uso de esta aplicación, consulte [Supervisión y administración de canalizaciones de Azure Data Factory mediante la nueva Aplicación de supervisión y administración](data-factory-monitor-manage-app.md).

1. Haga clic en el icono Supervisión y administración.

    ![Icono Supervisión y administración](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. Debería ver la Aplicación de supervisión y administración. Hola de cambio **hora de inicio** y **hora de finalización** toomatch inicio (04-01-2016 12:00 A.M.) y de finalización (04-02-2016 12:00 A.M.) de la canalización y haga clic en **aplicar**.

    ![Aplicación de supervisión y administración](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. toosee obtener más información acerca de una ventana de actividad, selecciónelo en hello **lista de ventanas de la actividad** toosee detalles sobre él.
    ![Detalles de ventana de actividad](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)

> [!IMPORTANT]
> archivo de entrada de Hola se elimina al segmento de Hola se procesa correctamente. Por lo tanto, si desea toorerun Hola sector u Hola tutorial nuevo, cargar Hola archivo de entrada (input.log) toohello `inputdata` carpeta de hello `adfgetstarted` contenedor.

### <a name="additional-notes"></a>Notas adicionales
- Una factoría de datos puede tener una o más canalizaciones. Una canalización puede tener una o más actividades. Por ejemplo, una toocopy de datos de actividad de copia de un almacén de datos de origen tooa destino y un toorun de actividad de Hive de HDInsight un tootransform de script de Hive datos de entrada. Vea [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) de Hola a todos los orígenes y receptores admitidos por hello actividad de copia. Vea [servicios vinculados de proceso](data-factory-compute-linked-services.md) para lista de hello de servicios de proceso admitidos factoría de datos.
- Servicios vinculados vinculan almacenes de datos o generador de datos de Azure de tooan de servicios de proceso. Vea [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) de Hola a todos los orígenes y receptores admitidos por hello actividad de copia. Vea [servicios vinculados de proceso](data-factory-compute-linked-services.md) para lista de hello de servicios de proceso admitidos factoría de datos y [las actividades de transformación](data-factory-data-transformation-activities.md) que puede ejecutar en ellos.
- Vea [mover datos desde / Blob tooAzure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obtener más información sobre propiedades JSON que se usan en hello almacenamiento de Azure vinculada definición del servicio.
- Puede usar su propio clúster de HDInsight en lugar de usar un clúster de HDInsight a petición. Consulte [Servicios vinculados de procesos](data-factory-compute-linked-services.md) para más información.
-  Hello factoría de datos se crea un **basados en Linux** clúster de HDInsight automáticamente con hello anterior JSON. Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .
- clúster de HDInsight de Hello crea un **contenedor predeterminado** en almacenamiento de blobs de Hola que especificó en hello JSON (linkedServiceName). HDInsight no elimine este contenedor cuando se elimina el clúster de Hola. Este comportamiento es así por diseño. Con el servicio vinculado de HDInsight a petición se crea un clúster de HDInsight cada vez que se procesa un segmento, a menos que haya un clúster existente activo (timeToLive). clúster de Hola se elimina automáticamente cuando se realiza un procesamiento Hola.
    
    A medida que se procesen más segmentos, verá numerosos contenedores en su Almacenamiento de blobs de Azure. Si no se necesita para solucionar problemas de trabajos de hello, quizá le interese toodelete ellos el costo de almacenamiento de tooreduce Hola. nombres de Hola de estos contenedores siguen un patrón: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`. Usar herramientas como [Explorador de almacenamiento de Microsoft](http://storageexplorer.com/) almacenamiento de blobs de contenedores de toodelete en Azure.
- Actualmente, el conjunto de datos de salida es qué unidades Hola programación, por lo que debe crear un conjunto de datos de salida aunque actividad hello no genera ningún resultado. Si la actividad hello no toma ninguna entrada, puede omitir creación Hola de conjunto de datos entrada. 
- Este tutorial no muestra cómo copiar datos mediante Azure Data Factory. Para obtener un tutorial sobre cómo toocopy los datos mediante Data Factory de Azure, consulte [Tutorial: copiar los datos de la base de datos del almacenamiento de blobs tooSQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).


## <a name="use-server-explorer-tooview-data-factories"></a>Use fábricas de datos de tooview de explorador de servidores
1. En **Visual Studio**, haga clic en **vista** en Hola menú y haga clic en **Explorador de servidores**.
2. En la ventana del explorador de servidores de hello, expanda **Azure** y expanda **factoría de datos**. Si ve **iniciar sesión en tooVisual Studio**, escriba Hola **cuenta** asociada a su suscripción de Azure y haga clic en **continuar**. Escriba la **contraseña** y haga clic en **Iniciar sesión**. Visual Studio intenta tooget información acerca de todos los generadores de datos de Azure en su suscripción. Vea Estado Hola de esta operación en hello **lista de tareas del generador de datos** ventana.

    ![Explorador de servidores](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. Puede haga clic en una factoría de datos y seleccione **exportar factoría de datos tooNew proyecto** toocreate un proyecto de Visual Studio basado en un generador de datos existente.

    ![Exportación de la factoría de datos](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a>Actualización de herramientas de Factoría de datos para Visual Studio
Hola tooupdate herramientas de Data Factory de Azure para Visual Studio, siga los pasos:

1. Haga clic en **herramientas** en el menú de Hola y seleccione **extensiones y actualizaciones**.
2. Seleccione **actualizaciones** en Hola panel izquierdo y, a continuación, seleccione **Galería de Visual Studio**.
3. Seleccione **Herramientas de Factoría de datos de Azure para Visual Studio** y haga clic en **Actualizar**. Si no ve esta entrada, ya tiene la versión más reciente de Hola de herramientas de Hola.

## <a name="use-configuration-files"></a>Uso de archivos de configuración
Puede usar archivos de configuración de propiedades de tooconfigure de Visual Studio para servicios/tablas/canalizaciones vinculadas diferente para cada entorno.

Considere la posibilidad de hello después de la definición de JSON para un servicio vinculado de almacenamiento de Azure. toospecify **connectionString** con valores diferentes para accountname y accountkey en función de hello entorno (desarrollo/prueba/producción) toowhich va a implementar las entidades de la factoría de datos. Puede conseguir este comportamiento mediante el uso del archivo de configuración independiente para cada entorno.

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a>Adición de un archivo de configuración
Agregue un archivo de configuración para cada entorno mediante la realización de hello pasos:   

1. Haga clic en proyecto de la factoría de datos de hello en la solución de Visual Studio, seleccione demasiado**agregar**y haga clic en **nuevo elemento**.
2. Seleccione **Config** en hello lista de plantillas instaladas de hello izquierda, seleccione **archivo de configuración**, escriba un **nombre** para la configuración de Hola de archivo y haga clic en **Agregar**.

    ![Adición de archivo de configuración](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. Agregar parámetros de configuración y sus valores de hello siguiendo el formato:

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    En este ejemplo se configura la propiedad connectionString de un servicio vinculado de Almacenamiento de Azure y un servicio vinculado de SQL de Azure. Observe que la sintaxis de Hola para especificar el nombre es [JsonPath](http://goessner.net/articles/JsonPath/).   

    Si JSON tiene una propiedad que tiene una matriz de valores como se muestra en el siguiente código de hello:  

    ```json
    "structure": [
          {
              "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
        }
    ],
    ```

    Configure las propiedades como se muestra en hello (indización de base cero uso) el archivo de configuración siguiente:

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a>Nombres de propiedad con espacios
Si un nombre de propiedad contiene espacios, utilice corchetes como se muestra en el siguiente ejemplo (nombre de servidor de base de datos) de Hola:

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a>Implementación de la solución mediante una configuración
Al publicar las entidades de la factoría de datos de Azure en VS, puede especificar configuración de Hola que desee toouse para esa operación de publicación.

entidades de toopublish en un proyecto de Data Factory de Azure mediante el archivo de configuración:   

1. Haga clic en proyecto de la factoría de datos y haga clic en **publicar** toosee hello **publicar elementos** cuadro de diálogo.
2. Seleccione un generador de datos existente o especificar valores para la creación de una factoría de datos en hello **factoría de datos de configuración** página y haga clic en **siguiente**.   
3. En hello **publicar elementos** página: verá una lista desplegable con las configuraciones disponibles para hello **Seleccionar configuración de implementación** campo.

    ![Selección de archivo de configuración](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. Seleccione hello **archivo de configuración** que haría como toouse y haga clic en **siguiente**.
5. Confirme que aparece el nombre de Hola de archivo JSON en hello **resumen** página y haga clic en **siguiente**.
6. Haga clic en **finalizar** una vez finalizada la operación de implementación de Hola.

Cuando se implementa, valores de Hola Hola del archivo de configuración son tooset usa valores de propiedades en archivos JSON de hello antes de que las entidades de hello son tooAzure implementado el servicio de factoría de datos.   

## <a name="use-azure-key-vault"></a>Uso de Azure Key Vault
No es aconsejable y a menudo con la directiva toocommit datos confidenciales como repositorio de código de toohello de cadenas de conexión. Vea [seguros publicar ADF](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) ejemplo en GitHub toolearn sobre cómo almacenar información confidencial en el almacén de claves de Azure y usarlo al publicar las entidades de la factoría de datos. Hola seguros publicar la extensión para Visual Studio permite Hola secretos toobe almacenado en el almacén de claves y sólo toothem de referencias se especifican en los servicios vinculados / configuraciones de implementación. Estas referencias se resuelven al publicar tooAzure de entidades de factoría de datos. Estos archivos se pueden confirmar toosource repositorio sin exponer los secretos.

## <a name="summary"></a>Resumen
En este tutorial, ha creado un datos tooprocess de factoría de datos de Azure mediante la ejecución de script de Hive en un clúster de hadoop de HDInsight. Utiliza el Editor de generador de datos de Hola Hola toodo portal Azure Hola siguiendo los pasos:  

1. Ha creado una **factoría de datos**de Azure.
2. Ha creado dos **servicios vinculados**:
   1. **Almacenamiento de Azure** vinculado servicio toolink el almacenamiento de blobs de Azure que contiene la factoría de datos de archivos de entrada/salida toohello.
   2. **HDInsight de Azure** toolink de servicio vinculado a petición una factoría de datos a petición toohello de clúster de Hadoop de HDInsight. Factoría de datos de Azure crea un Hadoop de HDInsight los datos de entrada de tooprocess just-in-time de clúster y generan datos de salida.
3. Crea dos **conjuntos de datos**, que describen los datos de entrada y salidos de actividad de Hive de HDInsight en la canalización de Hola.
4. Ha creado una **canalización** con una actividad de **Hive de HDInsight**.  

## <a name="next-steps"></a>Pasos siguientes
En este artículo, creó una canalización con una actividad de transformación (actividad de HDInsight) que ejecuta un script de Hive en un clúster de HDInsight a petición. toosee toouse una toocopy de datos de actividad de copia de un tooAzure de Blob de Azure SQL, vea [Tutorial: copiar los datos de un tooAzure de blobs de Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad. Para más información, consulte [Programación y ejecución en Data Factory](data-factory-scheduling-and-execution.md). 


## <a name="see-also"></a>Otras referencias
| Tema. | Descripción |
|:--- |:--- |
| [Procesos](data-factory-create-pipelines.md) |En este artículo le ayudará a comprender las canalizaciones y actividades de Data Factory de Azure y cómo toouse les tooconstruct flujos de trabajo de datos para su escenario o una empresa. |
| [Conjuntos de datos](data-factory-create-datasets.md) |Este artículo le ayuda a comprender los conjuntos de datos de Data Factory de Azure. |
| [Transformación y análisis con Data Factory de Azure](data-factory-data-transformation-activities.md) |En este artículo se proporciona una lista de actividades de transformación de datos (por ejemplo, la transformación de Hive para HDInsight usada en este tutorial), que se admiten en Data Factory de Azure. |
| [Programación y ejecución con Data Factory](data-factory-scheduling-and-execution.md) |En este artículo se explica los aspectos de programación y la ejecución de hello Data Factory de Azure del modelo de aplicación. |
| [Supervisión y administración de canalizaciones de Data Factory de Azure mediante la nueva Aplicación de supervisión y administración](data-factory-monitor-manage-app.md) |Este artículo describe cómo administrar toomonitor y depurar las canalizaciones utilizando Hola supervisión y administración de aplicaciones. |
