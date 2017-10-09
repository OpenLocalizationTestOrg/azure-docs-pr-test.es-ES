---
title: "aaaBuild su primera factoría de datos (portal de Azure) | Documentos de Microsoft"
description: "En este tutorial, creará una canalización de factoría de datos de Azure de ejemplo mediante el Editor de generador de datos en hello portal de Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a>Tutorial: Compilación de la primera instancia de Azure Data Factory con Azure Portal
> [!div class="op_single_selector"]
> * [Introducción y requisitos previos](data-factory-build-your-first-pipeline.md)
> * [Portal de Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Plantilla de Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API DE REST](data-factory-build-your-first-pipeline-using-rest-api.md)


En este artículo, aprenderá cómo toouse [portal de Azure](https://portal.azure.com/) toocreate su primera factoría de datos de Azure. tutorial de hello toodo mediante otra herramientas y SDK, seleccione una de las opciones de Hola de lista desplegable de Hola. 

canalización de Hello en este tutorial tiene una actividad: **actividad de HDInsight Hive**. Esta actividad ejecuta un script de hive en un clúster de HDInsight de Azure que las transformaciones de entrada de datos de salida de datos tooproduce. canalización de Hello es toorun programado una vez que un mes entre Hola especificado horas de inicio y finalización. 

> [!NOTE]
> canalización de datos de Hello en este tutorial transforma los datos de salida de tooproduce de datos de entrada. Para obtener un tutorial sobre cómo toocopy los datos mediante Data Factory de Azure, consulte [Tutorial: copiar los datos de la base de datos del almacenamiento de blobs tooSQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> pero cualquier canalización puede tener más de una actividad. Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad. Para más información, consulte [Programación y ejecución en Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

## <a name="prerequisites"></a>Requisitos previos
1. Lea [Tutorial de introducción](data-factory-build-your-first-pipeline.md) hello completa y artículo **prerequisite** pasos.
2. En este artículo no proporciona una información general conceptual de hello servicio Data Factory de Azure. Se recomienda que pase por [tooAzure Introducción factoría de datos](data-factory-introduction.md) artículo para obtener una descripción detallada del servicio de Hola.  

## <a name="create-data-factory"></a>Creación de Data Factory
Una factoría de datos puede tener una o más canalizaciones. Una canalización puede tener una o más actividades. Por ejemplo, una toocopy de datos de actividad de copia de un almacén de datos de origen tooa destino y un toorun de actividad de Hive de HDInsight un tootransform de script de Hive datos de salida de tooproduct de datos de entrada. Puede empezar con la creación de factoría de datos de hello en este paso.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Haga clic en **NEW** en el menú de la izquierda hello, haga clic en **datos + análisis**y haga clic en **factoría de datos**.

   ![Hoja Creación](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. Hola **factoría de datos** hoja, escriba **GetStartedDF** para hello nombre.

   ![Hoja Nueva Factoría de datos](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > nombre de Hola Hola Azure factoría de datos debe ser **único global**. Si recibe el error hello: **nombre de generador de datos "GetStartedDF" no está disponible**. Cambie el nombre Hola Hola factoría de datos (por ejemplo, yournameGetStartedDF) e intente crear de nuevo. Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.
   >
   > nombre de Hola Hola factoría de datos se puede registrar como un **DNS** asigne un nombre en el futuro de hello y, por tanto, se convierten en visible públicamente.
   >
   >
4. Seleccione hello **suscripción de Azure** donde desea Hola datos generador toobe creado.
5. Seleccione un **grupo de recursos** existente o cree uno nuevo. Para ver tutorial Hola, cree un grupo de recursos denominado: **ADFGetStartedRG**.
6. Seleccione hello **ubicación** de factoría de datos de Hola. Solo las regiones compatibles con hello servicio factoría de datos se muestran en la lista desplegable de Hola.
7. Seleccione **toodashboard Pin**. 
8. Haga clic en **crear** en hello **factoría de datos** hoja.

   > [!IMPORTANT]
   > instancias de la factoría de datos de toocreate, debe ser miembro del programa Hola a [colaborador de la factoría de datos](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol en el nivel de grupo de recursos/suscripción Hola.
   >
   >
7. En el panel de hello, ve Hola siguiente icono con el estado: implementación factoría de datos.    

   ![Creación de estado de la factoría de datos](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. ¡Enhorabuena! Ya creó correctamente su primera factoría de datos. Una vez creado correctamente la factoría de datos de hello, consulte página de factoría de datos de hello, que muestra Hola contenido Hola factoría de datos.     

    ![Hoja de la Factoría de datos](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

Antes de crear una canalización de factoría de datos de hello, necesita toocreate algunas entidades de la factoría de datos en primer lugar. En primer lugar crear servicios vinculados toolink datos almacenes/calcula tooyour almacenarán, definen la entrada y salida de datos de entrada/salida de toorepresent de conjuntos de datos en almacenes de datos vinculado como los datos, a continuación, crear canalización Hola con una actividad que usa estos conjuntos de datos.

## <a name="create-linked-services"></a>Crear servicios vinculados
En este paso, vincular su cuenta de almacenamiento de Azure y un generador de datos a petición tooyour de clúster de HDInsight de Azure. Hola cuenta de almacenamiento de Azure que contiene datos de entrada y salidas de la canalización de hello en este ejemplo de Hola. Hola servicio vinculado de HDInsight es toorun usa un script de Hive especificado en la actividad de hello de canalización de hello en este ejemplo. Identificar las actividades que [almacén de datos](data-factory-data-movement-activities.md)/[servicios de proceso](data-factory-compute-linked-services.md) se usan en el escenario y vincular esos factoría de datos de servicios toohello mediante la creación de servicios vinculados.  

### <a name="create-azure-storage-linked-service"></a>Creación de un servicio vinculado de Almacenamiento de Azure
En este paso, vincule la factoría de datos de tooyour de cuenta de almacenamiento de Azure. En este tutorial, utilice Hola misma cuenta de almacenamiento de Azure hello HQL y datos de entrada/salida de toostore los archivos de scripts.

1. Haga clic en **autor e implementar** en hello **factoría de datos** hoja para **GetStartedDF**. Debería ver Hola Editor de generador de datos.

   ![Icono Crear e implementar](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. Haga clic en **Nuevo almacén de datos** y elija **Azure Storage**.

   ![Nuevo almacén de datos - Azure Storage - menú](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. Debería ver Hola script JSON para crear un almacenamiento de Azure vinculada servicio en el editor de Hola.

   ![Servicio vinculado de Azure Storage](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. Reemplace **nombre de la cuenta** con nombre de saludo de la cuenta de almacenamiento de Azure y **clave de cuenta** por clave de acceso de Hola de hello cuenta de almacenamiento de Azure. toolearn el proceso tooget el almacenamiento de acceso de clave, vea Hola información acerca de cómo tooview, copiar y regenerar almacenamiento tener acceso a claves de [administrar su cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
5. Haga clic en **implementar** en toodeploy Hola vinculado servicio la barra de comandos de Hola.

    ![Botón Implementar](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   Después de hello servicio vinculado se ha implementado correctamente, Hola **Draft-1** ventana debería desaparecer y verá **AzureStorageLinkedService** en vista de árbol de Hola Hola izquierda.

    ![Servicio vinculado de Almacenamiento en el menú](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a>Creación de un servicio vinculado de HDInsight de Azure
En este paso, vincular un generador de datos a petición tooyour de clúster de HDInsight. clúster de HDInsight de Hello automáticamente está creado en tiempo de ejecución y eliminar después de hacerlo inactivos y procesamiento para el período de tiempo especificado de Hola.

1. Hola **Editor de generador de datos**, haga clic en **... Más** y en **Nuevo proceso**; después, seleccione **On-demand HDInsight cluster** (Clúster de HDInsight a petición).

    ![Nuevo proceso](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. Copie y pegue Hola siguiente fragmento de código toohello **Draft-1** ventana. fragmento JSON de Hello describe propiedades Hola Hola toocreate usado clúster de HDInsight a petición.

    ```JSON
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:

   | Propiedad | Descripción |
   |:--- |:--- |
   | ClusterSize |Especifica el tamaño de Hola Hola del clúster de HDInsight. |
   | TimeToLive | Especifica ese tiempo de inactividad de hello para el clúster de HDInsight de hello, antes de eliminarla. |
   | linkedServiceName | Especifica la cuenta de almacenamiento de Hola que es toostore usado Hola registros generados por HDInsight. |

    Tenga en cuenta Hola siguientes puntos:

   * Hello factoría de datos se crea un **basados en Linux** clúster de HDInsight automáticamente con hello JSON. Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .
   * Puede usar **su propio clúster de HDInsight** en lugar de usar un clúster de HDInsight a petición. Para más información, consulte [Servicio vinculado de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .
   * clúster de HDInsight de Hello crea un **contenedor predeterminado** en almacenamiento de blobs de Hola que especificó en hello JSON (**linkedServiceName**). HDInsight no elimine este contenedor cuando se elimina el clúster de Hola. Este comportamiento es así por diseño. Con el servicio vinculado de HDInsight a petición se crea un clúster de HDInsight cada vez se procesa un segmento, a menos que haya un clúster existente activo (**timeToLive**). clúster de Hola se elimina automáticamente cuando se realiza un procesamiento Hola.

       A medida que se procesen más segmentos, verá numerosos contenedores en su Almacenamiento de blobs de Azure. Si no se necesita para solucionar problemas de trabajos de hello, quizá le interese toodelete ellos el costo de almacenamiento de tooreduce Hola. nombres de Hola de estos contenedores siguen un patrón: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Usar herramientas como [Explorador de almacenamiento de Microsoft](http://storageexplorer.com/) almacenamiento de blobs de contenedores de toodelete en Azure.

     Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .
3. Haga clic en **implementar** en toodeploy Hola vinculado servicio la barra de comandos de Hola.

    ![Implementación de servicio vinculado de HDInsight a petición](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. Confirme que ve ambos **AzureStorageLinkedService** y **HDInsightOnDemandLinkedService** en vista de árbol de Hola Hola izquierda.

    ![Vista de árbol con servicios vinculados](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a>Creación de conjuntos de datos
En este paso, creación de conjuntos de datos toorepresent Hola entrada y salida de datos para el procesamiento de Hive. Estos conjuntos de datos, consulte toohello **AzureStorageLinkedService** ha creado anteriormente en este tutorial. Hola tooan de puntos de servicio vinculado cuenta de almacenamiento de Azure y los conjuntos de datos especifiquen contenedor, carpeta, nombre de archivo en el almacenamiento de Hola que contiene la entrada y salida de datos.   

### <a name="create-input-dataset"></a>Creación de un conjunto de datos de entrada
1. Hola **Editor de generador de datos**, haga clic en **... Más** en la barra de comandos de hello, haga clic en **nuevo conjunto de datos**y seleccione **almacenamiento de blobs de Azure**.

    ![Nuevo conjunto de datos](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. Copie y pegue Hola después de la ventana de toohello Draft-1 de fragmentos de código. En el fragmento JSON de hello, desea crear un conjunto de datos denominado **AzureBlobInput** que representa los datos de entrada para una actividad de canalización de Hola. Además, especifica que los datos de entrada de Hola se encuentran en contenedor de blob de hello denominado **adfgetstarted** y carpeta Hola llamada **inputdata**.

    ```JSON
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
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
    Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:

   | Propiedad | Descripción |
   |:--- |:--- |
   | type |propiedad de tipo Hello se establece demasiado**AzureBlob** porque los datos residen en un almacenamiento de blobs de Azure. |
   | linkedServiceName |Hace referencia a toohello **AzureStorageLinkedService** que creó anteriormente. |
   | folderPath | Especifica el blob de hello **contenedor** hello y **carpeta** que contiene la entrada de blobs. | 
   | fileName |Esta propiedad es opcional. Si se omite esta propiedad, se seleccionan todos los archivos de Hola de hello folderPath. En este tutorial, solo Hola **input.log** se procesa. |
   | type |archivos de registro de Hello están en formato de texto, por lo que usamos **TextFormat**. |
   | columnDelimiter |columnas en los archivos de registro de hello se delimitan mediante **carácter de coma (`,`)** |
   | frecuencia/intervalo |la frecuencia debe establecer demasiado**mes** y el intervalo es **1**, lo que significa que Hola entrada sectores están disponibles cada mes. |
   | external | Esta propiedad se establece demasiado**true** si no se generan datos de entrada de hello esta canalización. En este tutorial, hello input.log no genera archivo esta canalización, por lo que establecemos Hola propiedad tootrue. |

    Para más información acerca de estas propiedades JSON, consulte el [artículo sobre el conector de blob de Azure](data-factory-azure-blob-connector.md#dataset-properties).
3. Haga clic en **implementar** en el conjunto de datos de toodeploy Hola que acaba de crear la barra de comandos de Hola. Debería ver el conjunto de datos de hello en vista de árbol de Hola Hola izquierda.

### <a name="create-output-dataset"></a>Creación del conjunto de datos de salida
Ahora, cree Hola salida dataset toorepresent Hola salida datos almacenados en hello almacenamiento de blobs de Azure.

1. Hola **Editor de generador de datos**, haga clic en **... Más** en la barra de comandos de hello, haga clic en **nuevo conjunto de datos**y seleccione **almacenamiento de blobs de Azure**.  
2. Copie y pegue Hola después de la ventana de toohello Draft-1 de fragmentos de código. En el fragmento JSON de hello, desea crear un conjunto de datos denominado **AzureBlobOutput**y especificar la estructura de Hola de datos de hello generada por script de Hive Hola. Además, se especifica que los resultados de Hola se almacenen en contenedor de blob de hello denominado **adfgetstarted** y carpeta Hola llamada **partitioneddata**. Hola **disponibilidad** sección especifica ese conjunto de datos de salida de hello se genera mensualmente.

    ```JSON
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
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
    Vea **crear conjunto de datos de entrada de hello** sección para obtener una descripción de estas propiedades. No establezca propiedad externa hello en un conjunto de datos de salida como conjunto de datos de hello es generado por el servicio de factoría de datos de Hola.
3. Haga clic en **implementar** en el conjunto de datos de toodeploy Hola que acaba de crear la barra de comandos de Hola.
4. Compruebe que ese conjunto de datos de Hola se creó correctamente.

    ![Vista de árbol con servicios vinculados](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a>Creación de una canalización
En este paso, creará la primera canalización con una actividad **HDInsightHive** . Segmento de entrada está disponible mensual (frecuencia: mes, intervalo: 1), segmento de salida se genera mensualmente y Hola programador propiedad actividad hello también está configurada toomonthly. debe coincidir con la configuración de Hello para el conjunto de datos de salida de Hola y el programador de la actividad de Hola. Actualmente, el conjunto de datos de salida es qué unidades Hola programación, por lo que debe crear un conjunto de datos de salida aunque actividad hello no genera ningún resultado. Si la actividad hello no toma ninguna entrada, puede omitir creación Hola de conjunto de datos entrada. propiedades de Hello utilizadas en hello después de JSON se explican al final de Hola de esta sección.

1. Hola **Editor de generador de datos**, haga clic en **puntos suspensivos (...) Más comandos** y, a continuación, haga clic en **nueva canalización**.

    ![Botón Nueva canalización](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. Copie y pegue Hola después de la ventana de toohello Draft-1 de fragmentos de código.

   > [!IMPORTANT]
   > Reemplace **storageaccountname** con el nombre de Hola de su cuenta de almacenamiento en hello JSON.
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
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
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    En el fragmento JSON de hello, desea crear una canalización que consta de una actividad única que usa Hive tooprocess datos en un clúster de HDInsight.

    archivo de script de Hive de Hello, **partitionweblogs.hql**, se almacena en hello cuenta de almacenamiento de Azure (especificado por scriptLinkedService hello, denominado **AzureStorageLinkedService**) y en  **secuencia de comandos** carpeta en el contenedor de hello **adfgetstarted**.

    Hola **define** sección es la configuración de en tiempo de ejecución de hello toospecify utilizado que se pasa el script de hive toohello como valores de configuración de Hive (por ejemplo ${hiveconf: inputtable}, ${hiveconf:partitionedtable}).

    Hola **iniciar** y **final** propiedades de canalización de hello especifica el periodo activo de Hola de canalización de Hola.

    En JSON de la actividad de hello, especifique ese script de Hive Hola se ejecuta en proceso Hola especificado por hello **linkedServiceName** : **HDInsightOnDemandLinkedService**.

   > [!NOTE]
   > Consulte la sección "JSON de canalización" en [canalizaciones y actividades de Data Factory de Azure](data-factory-create-pipelines.md) para obtener más información sobre propiedades JSON que se usan en el ejemplo de Hola.
   >
   >
3. Confirmar siguiente hello:

   1. **Input.log** archivo existe en hello **inputdata** carpeta de hello **adfgetstarted** contenedor Hola almacenamiento de blobs de Azure
   2. **partitionweblogs.hql** archivo existe en hello **script** carpeta de hello **adfgetstarted** contenedor Hola almacenamiento de blobs de Azure. Requisito previo de hello completa los pasos de hello [Tutorial Introducción](data-factory-build-your-first-pipeline.md) si no ve estos archivos.
   3. Confirme que ha reemplazado **storageaccountname** con el nombre de Hola de su cuenta de almacenamiento en Hola de canalización JSON.
4. Haga clic en **implementar** en la canalización de hello toodeploy la barra de comandos de Hola. Desde hello **iniciar** y **final** veces se establecen en los último hello y **isPaused** es toofalse de conjunto, canalización Hola ejecuciones (actividad de canalización de hello) inmediatamente después de implementar.
5. Confirme que ve canalización hello en la vista de árbol de Hola.

    ![Vista de árbol con canalización](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. Enhorabuena, ya creó correctamente su primera canalización.

## <a name="monitor-pipeline"></a>Supervisión de la canalización
### <a name="monitor-pipeline-using-diagram-view"></a>Supervisión de una canalización desde la vista de diagrama
1. Haga clic en **X** tooclose Editor de generador de datos hojas toonavigate hacer copia de hoja de la factoría de datos de toohello y haga clic en **diagrama**.

    ![Icono Diagrama](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. En la vista de diagrama de hello, verá información general de las canalizaciones de Hola y conjuntos de datos usados en este tutorial.

    ![Vista de diagrama](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. tooview todas las actividades de canalización de hello, menú contextual "canalización" Hola, diagrama y haga clic en abrir canalización.

    ![Menú Abrir canalización](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. Confirme que ve actividad HDInsightHive de hello en canalización Hola.

    ![Vista Abrir canalización](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    toonavigate realizar copias toohello vista anterior, haga clic en **factoría de datos** en el menú de la ruta de navegación de hello en la parte superior de Hola.
5. Hola **vista de diagrama**, haga doble clic en el conjunto de datos de hello **AzureBlobInput**. Confirme que dicho sector Hola está en **listo** estado. Pueden tardar unos minutos para tooshow de segmento de hello en estado listo. Si no se realiza después de que espere unos instantes, ver si el archivo de entrada de hello (input.log) colocado en el contenedor de derecho de hello (adfgetstarted) y la carpeta (inputdata).

   ![Segmento de entrada con estado Listo](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. Haga clic en **X** tooclose **AzureBlobInput** hoja.
7. Hola **vista de diagrama**, haga doble clic en el conjunto de datos de hello **AzureBlobOutput**. Vea dicho sector Hola que se está procesando actualmente.

   ![Dataset](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. Cuando se realiza el procesamiento, verá que el segmento de hello en **listo** estado.

   ![Dataset](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > La creación de un clúster de HDInsight a petición normalmente tarda algún tiempo (20 minutos aproximadamente). Por consiguiente, esperan canalización Hola tardar demasiado **aproximadamente 30 minutos** tooprocess Hola segmento.
   >
   >

9. Cuando se encuentra el segmento de hello en **listo** de estado, compruebe hello **partitioneddata** carpeta Hola **adfgetstarted** contenedor en el almacenamiento de blobs para hello los datos de salida.  

   ![datos de salida](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. Haga clic en hello segmento toosee detalles sobre él en un **el segmento de datos** hoja.

   ![Detalles de segmento de datos](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. Haga clic en una actividad que se ejecutan en hello **lista ejecuta la actividad** toosee detalles sobre la actividad de ejecución (actividad de Hive en nuestro escenario) un **detalles de ejecución de la actividad** ventana.   

   ![Detalles de ejecución de actividad](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   Desde archivos de registro de hello, puede ver información de estado y de consulta de Hive de Hola que se ejecutó. Estos registros son útiles para solucionar cualquier problema.
   Para más información, consulte el artículo [Supervisión y administración de canalizaciones mediante las hojas del Portal de Azure](data-factory-monitor-manage-pipelines.md) .

> [!IMPORTANT]
> archivo de entrada de Hola se elimina al segmento de Hola se procesa correctamente. Por lo tanto, si desea toorerun Hola sector u Hola tutorial nuevo, cargar toohello inputdata carpeta de hello archivo de entrada (input.log) del contenedor de adfgetstarted Hola.
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a>Supervisión de una canalización con la Aplicación de supervisión y administración
También puede utilizar el Monitor de & Administrar aplicación toomonitor sus canalizaciones. Para más información acerca del uso de esta aplicación, consulte [Supervisión y administración de canalizaciones de Azure Data Factory mediante la nueva Aplicación de supervisión y administración](data-factory-monitor-manage-app.md).

1. Haga clic en **Monitor & administrar** de mosaico en la página principal de saludo de la factoría de datos.

    ![Icono Supervisión y administración](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. Debería ver la **aplicación de supervisión y administración**. Hola de cambio **hora de inicio** y **hora de finalización** toomatch inicio y finalización de la canalización y haga clic en **aplicar**.

    ![Aplicación de supervisión y administración](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. Seleccione una ventana actividad Hola **Windows actividad** lista toosee detalles sobre él.

    ![Detalles de ventana de actividad](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

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

## <a name="see-also"></a>Otras referencias
| Tema. | Descripción |
|:--- |:--- |
| [Procesos](data-factory-create-pipelines.md) |En este artículo le ayudará a comprender las canalizaciones y actividades de Data Factory de Azure y cómo toouse les tooconstruct-to-end orientadas a datos los flujos de trabajo para su escenario o una empresa. |
| [Conjuntos de datos](data-factory-create-datasets.md) |Este artículo le ayuda a comprender los conjuntos de datos de Data Factory de Azure. |
| [Programación y ejecución con Data Factory](data-factory-scheduling-and-execution.md) |En este artículo se explica los aspectos de programación y la ejecución de hello Data Factory de Azure del modelo de aplicación. |
| [Supervisión y administración de canalizaciones de Data Factory de Azure mediante la nueva Aplicación de supervisión y administración](data-factory-monitor-manage-app.md) |Este artículo describe cómo administrar toomonitor y depurar las canalizaciones utilizando Hola supervisión y administración de aplicaciones. |
