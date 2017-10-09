---
title: "aaaBuild su primera factoría de datos (PowerShell) | Documentos de Microsoft"
description: "En este tutorial, creará un de ejemplo de canalización de Data Factory de Azure mediante Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 626260798b56d590577b3c4b24f7cf52873c9f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a>Tutorial: Compilación de la primera instancia de Azure Data Factory con Azure PowerShell
> [!div class="op_single_selector"]
> * [Introducción y requisitos previos](data-factory-build-your-first-pipeline.md)
> * [Portal de Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Plantilla de Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API DE REST](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

En este artículo, use PowerShell de Azure toocreate su primera factoría de datos de Azure. tutorial de hello toodo mediante otra herramientas y SDK, seleccione una de las opciones de Hola de lista desplegable de Hola.

canalización de Hello en este tutorial tiene una actividad: **actividad de HDInsight Hive**. Esta actividad ejecuta un script de hive en un clúster de HDInsight de Azure que las transformaciones de entrada de datos de salida de datos tooproduce. canalización de Hello es toorun programado una vez que un mes entre Hola especificado horas de inicio y finalización. 

> [!NOTE]
> canalización de datos de Hello en este tutorial transforma los datos de salida de tooproduce de datos de entrada. No copia datos de un almacén de datos de destino de origen datos almacén tooa. Para obtener un tutorial sobre cómo toocopy los datos mediante Data Factory de Azure, consulte [Tutorial: copiar los datos de la base de datos del almacenamiento de blobs tooSQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> pero cualquier canalización puede tener más de una actividad. Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad. Para más información, consulte [Programación y ejecución en Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

## <a name="prerequisites"></a>Requisitos previos
* Lea [Tutorial de introducción](data-factory-build-your-first-pipeline.md) hello completa y artículo **prerequisite** pasos.
* Siga las instrucciones de [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) artículo tooinstall versión más reciente de PowerShell de Azure en el equipo.
* (opcional) Este artículo no cubre todos los cmdlets de factoría de datos de Hola. Vea [Referencia de cmdlets de factoría de datos](/powershell/module/azurerm.datafactories) para obtener la documentación completa sobre los cmdlets de la factoría de datos.

## <a name="create-data-factory"></a>Creación de Data Factory
En este paso, usar Azure PowerShell toocreate una factoría de datos de Azure denominado **FirstDataFactoryPSH**. Una factoría de datos puede tener una o más canalizaciones. Una canalización puede tener una o más actividades. Por ejemplo, una toocopy de datos de actividad de copia de un almacén de datos de origen tooa destino y un toorun de actividad de Hive de HDInsight un tootransform de script de Hive datos de entrada. Puede empezar con la creación de factoría de datos de hello en este paso.

1. Inicie PowerShell de Azure y ejecute el siguiente comando de Hola. Mantenga Azure PowerShell abierta hasta final de Hola de este tutorial. Si se cierre y vuelva a abrir, deberá toorun estos comandos nuevo.
   * Ejecute el siguiente comando de Hola y escriba el nombre de usuario de Hola y la contraseña que usa toosign en toohello portal de Azure.
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * Ejecute hello después comando tooview todas las suscripciones de Hola para esta cuenta.
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * Ejecute hello después de suscripción de hello tooselect de comando que desee toowork con. Esta suscripción debe ser Hola igual que la que usó en el portal de Azure Hola Hola.
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. Crear un grupo de recursos de Azure denominado **ADFTutorialResourceGroup** ejecutando Hola siguiente comando:
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    Algunos de los pasos de hello en este tutorial se supone que usa el grupo de recursos de hello llamado ADFTutorialResourceGroup. Si utiliza un grupo de recursos diferente, deberá toouse, en lugar de ADFTutorialResourceGroup en este tutorial.
3. Ejecute hello **New-AzureRmDataFactory** cmdlet que crea un generador de datos denominado **FirstDataFactoryPSH**.

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
Tenga en cuenta Hola siguientes puntos:

* nombre de Hola de hello Data Factory de Azure debe ser único globalmente. Si recibe el error hello **nombre de generador de datos "FirstDataFactoryPSH" no está disponible**, cambie el nombre de hello (por ejemplo, yournameFirstDataFactoryPSH). Use este nombre en lugar de ADFTutorialFactoryPSH mientras lleva a cabo los pasos de este tutorial. Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.
* instancias de la factoría de datos de toocreate, deberá toobe un colaborador o administrador de hello suscripción de Azure
* nombre Hola Hola factoría de datos se puede registrarse como un nombre DNS en hello futuras y, por tanto, se convierten en visible públicamente.
* Si recibe el error hello: "**esta suscripción no tiene espacio de nombres registrado toouse Microsoft.DataFactory**", siga uno de los procedimientos de Hola e intente publicar de nuevo:

  * En Azure PowerShell, ejecute hello después de proveedor del comando tooregister Hola factoría de datos:

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      Puede ejecutar Hola después comando tooconfirm ese Hola factoría de datos de proveedor está registrado:

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Inicio de sesión mediante Hola suscripción de Azure en hello [portal de Azure](https://portal.azure.com) y navegar por hoja de la factoría de datos de tooa crear una factoría de datos en el portal de Azure hello (o). Esta acción registra automáticamente proveedor Hola para usted.

Antes de crear una canalización, necesita toocreate algunas entidades de la factoría de datos en primer lugar. En primer lugar crear servicios vinculados toolink datos almacenes/calcula tooyour almacenarán, definen la entrada y salida de datos de entrada/salida de toorepresent de conjuntos de datos en almacenes de datos vinculado como los datos, a continuación, crear canalización Hola con una actividad que usa estos conjuntos de datos.

## <a name="create-linked-services"></a>Crear servicios vinculados
En este paso, vincular su cuenta de almacenamiento de Azure y un generador de datos a petición tooyour de clúster de HDInsight de Azure. Hola cuenta de almacenamiento de Azure que contiene datos de entrada y salidas de la canalización de hello en este ejemplo de Hola. Hola servicio vinculado de HDInsight es toorun usa un script de Hive especificado en la actividad de hello de canalización de hello en este ejemplo. Identificar qué datos del almacén o proceso servicios se usan en el escenario y vinculan esos factoría de datos de servicios toohello mediante la creación de servicios vinculados.

### <a name="create-azure-storage-linked-service"></a>Creación de un servicio vinculado de Almacenamiento de Azure
En este paso, vincule la factoría de datos de tooyour de cuenta de almacenamiento de Azure. Usar hello misma cuenta de almacenamiento de Azure hello HQL y datos de entrada/salida de toostore los archivos de scripts.

1. Cree un archivo JSON con el nombre StorageLinkedService.json en la carpeta de hello C:\ADFGetStarted con hello después de contenido. Crear carpeta de hello ADFGetStarted si aún no existe.

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
    Reemplace **nombre de la cuenta** con nombre de saludo de la cuenta de almacenamiento de Azure y **clave de cuenta** por clave de acceso de Hola de hello cuenta de almacenamiento de Azure. toolearn el proceso tooget el almacenamiento de acceso de clave, vea Hola información acerca de cómo tooview, copiar y regenerar almacenamiento tener acceso a claves de [administrar su cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
2. En Azure PowerShell, cambie toohello ADFGetStarted carpeta.
3. Puede usar hello **AzureRmDataFactoryLinkedService New** cmdlet que crea un servicio vinculado. Este cmdlet y otros cmdlets de factoría de datos que se usa en este tutorial requiere que los valores de toopass para hello *ResourceGroupName* y *DataFactoryName* parámetros. Como alternativa, puede usar **Get AzureRmDataFactory** tooget una **DataFactory** objeto y pasar el objeto de hello sin escribir *ResourceGroupName* y  *DataFactoryName* cada vez que ejecute un cmdlet. Siguiente ejecución Hola comando salida de hello tooassign de hello **Get AzureRmDataFactory** cmdlet tooa **$df** variable.

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. Ahora, ejecute hello **New-AzureRmDataFactoryLinkedService** cmdlet que crea Hola vinculado **StorageLinkedService** servicio.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    Si no se había ejecutado hello **Get AzureRmDataFactory** hello asignado y cmdlet de salida toohello **$df** variable, tendría toospecify valores de hello *ResourceGroupName*y *DataFactoryName* parámetros tal y como se indica a continuación.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    Si cierra Azure PowerShell en medio de Hola de tutorial de hello, tendrá que hello toorun **AzureRmDataFactory Get** cmdlet próxima vez que inicie el tutorial de Azure PowerShell toocomplete Hola.

### <a name="create-azure-hdinsight-linked-service"></a>Creación de un servicio vinculado de HDInsight de Azure
En este paso, vincular un generador de datos a petición tooyour de clúster de HDInsight. clúster de HDInsight de Hello automáticamente está creado en tiempo de ejecución y eliminar después de hacerlo inactivos y procesamiento para el período de tiempo especificado de Hola. Puede usar su propio clúster de HDInsight en lugar de usar un clúster de HDInsight a petición. Consulte [Servicios vinculados de procesos](data-factory-compute-linked-services.md) para más información.

1. Cree un archivo JSON denominado **HDInsightOnDemandLinkedService**.json Hola **C:\ADFGetStarted** carpeta con hello siguen contenido.

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
                "linkedServiceName": "StorageLinkedService"
            }
        }
    }
    ```
    Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:

   | Propiedad | Descripción |
   |:--- |:--- |
   | ClusterSize |Especifica el tamaño de Hola Hola del clúster de HDInsight. |
   | TimeToLive |Especifica ese tiempo de inactividad de hello para el clúster de HDInsight de hello, antes de eliminarla. |
   | linkedServiceName |Especifica la cuenta de almacenamiento de Hola que es toostore usado Hola registros generados por HDInsight |

    Tenga en cuenta Hola siguientes puntos:

   * Hello factoría de datos se crea un **basados en Linux** clúster de HDInsight automáticamente con hello JSON. Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .
   * Puede usar **su propio clúster de HDInsight** en lugar de usar un clúster de HDInsight a petición. Para más información, consulte [Servicio vinculado de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .
   * clúster de HDInsight de Hello crea un **contenedor predeterminado** en almacenamiento de blobs de Hola que especificó en hello JSON (**linkedServiceName**). HDInsight no elimine este contenedor cuando se elimina el clúster de Hola. Este comportamiento es así por diseño. Con el servicio vinculado de HDInsight a petición se crea un clúster de HDInsight cada vez se procesa un segmento, a menos que haya un clúster existente activo (**timeToLive**). clúster de Hola se elimina automáticamente cuando se realiza un procesamiento Hola.

       A medida que se procesen más segmentos, verá numerosos contenedores en su Almacenamiento de blobs de Azure. Si no se necesita para solucionar problemas de trabajos de hello, quizá le interese toodelete ellos el costo de almacenamiento de tooreduce Hola. nombres de Hola de estos contenedores siguen un patrón: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Usar herramientas como [Explorador de almacenamiento de Microsoft](http://storageexplorer.com/) almacenamiento de blobs de contenedores de toodelete en Azure.

     Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .
2. Ejecute hello **AzureRmDataFactoryLinkedService New** cmdlet que crea Hola vinculado servicio denominado HDInsightOnDemandLinkedService.
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a>Creación de conjuntos de datos
En este paso, creación de conjuntos de datos toorepresent Hola entrada y salida de datos para el procesamiento de Hive. Estos conjuntos de datos, consulte toohello **StorageLinkedService** ha creado anteriormente en este tutorial. Hola tooan de puntos de servicio vinculado cuenta de almacenamiento de Azure y los conjuntos de datos especifiquen contenedor, carpeta, nombre de archivo en el almacenamiento de Hola que contiene la entrada y salida de datos.

### <a name="create-input-dataset"></a>Creación de un conjunto de datos de entrada
1. Cree un archivo JSON denominado **InputTable.json** en hello **C:\ADFGetStarted** carpeta con hello siguen contenido:

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
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
    Hola JSON define un conjunto de datos denominado **AzureBlobInput**, que representa los datos de entrada para una actividad de canalización de Hola. Además, especifica que los datos de entrada de Hola se encuentran en contenedor de blob de hello denominado **adfgetstarted** y carpeta Hola llamada **inputdata**.

    Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:

   | Propiedad | Descripción |
   |:--- |:--- |
   | type |propiedad de tipo Hello se establece tooAzureBlob porque los datos residen en el almacenamiento de blobs de Azure. |
   | linkedServiceName |se refiere toohello StorageLinkedService que creó anteriormente. |
   | fileName |Esta propiedad es opcional. Si se omite esta propiedad, se seleccionan todos los archivos de Hola de hello folderPath. En este caso, se procesa solo hello input.log. |
   | type |archivos de registro de Hello están en formato de texto, por lo que usamos TextFormat. |
   | columnDelimiter |columnas en los archivos de registro de hello están delimitadas por caracteres de Hola por comas (,). |
   | frecuencia/intervalo |la frecuencia debe establecer tooMonth y interval es 1, lo que significa que están disponibles los segmentos de entrada de hello mensualmente. |
   | external |Esta propiedad se establece tootrue si servicio de factoría de datos de hello no genera datos de entrada de saludo. |
2. Ejecute el siguiente comando en el conjunto de datos de Azure PowerShell toocreate Hola factoría de datos de Hola:

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a>Creación del conjunto de datos de salida
Ahora, cree Hola salida dataset toorepresent Hola salida datos almacenados en hello almacenamiento de blobs de Azure.

1. Cree un archivo JSON denominado **OutputTable.json** en hello **C:\ADFGetStarted** carpeta con hello siguen contenido:

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
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
    Hola JSON define un conjunto de datos denominado **AzureBlobOutput**, que representa los datos de salida para una actividad de canalización de Hola. Además, especifica que los resultados de Hola se almacenan en contenedor de blob de hello denominado **adfgetstarted** y carpeta Hola llamada **partitioneddata**. Hola **disponibilidad** sección especifica ese conjunto de datos de salida de hello se genera mensualmente.
2. Ejecute el siguiente comando en el conjunto de datos de Azure PowerShell toocreate Hola factoría de datos de Hola:

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a>Creación de una canalización
En este paso, creará la primera canalización con una actividad **HDInsightHive** . Segmento de entrada está disponible mensual (frecuencia: mes, intervalo: 1), segmento de salida se genera mensualmente y Hola programador propiedad actividad hello también está configurada toomonthly. debe coincidir con la configuración de Hello para el conjunto de datos de salida de Hola y el programador de la actividad de Hola. Actualmente, el conjunto de datos de salida es qué unidades Hola programación, por lo que debe crear un conjunto de datos de salida aunque actividad hello no genera ningún resultado. Si la actividad hello no toma ninguna entrada, puede omitir creación Hola de conjunto de datos entrada. propiedades de Hello utilizadas en hello después de JSON se explican al final de Hola de esta sección.

1. Cree un archivo JSON denominado MyFirstPipelinePSH.json en la carpeta de hello C:\ADFGetStarted con hello siguiente contenido:

   > [!IMPORTANT]
   > Reemplace **storageaccountname** con el nombre de Hola de su cuenta de almacenamiento en hello JSON.
   >
   >

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
                        "scriptLinkedService": "StorageLinkedService",
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

    archivo de script de Hive de Hello, **partitionweblogs.hql**, se almacena en hello cuenta de almacenamiento de Azure (especificado por scriptLinkedService hello, denominado **StorageLinkedService**) y en **secuencias de comandos**  carpeta en el contenedor de hello **adfgetstarted**.

    Hola **define** sección es configuración en tiempo de ejecución de toospecify usado Hola que ser pasa el script de hive toohello como valores de configuración de Hive (por ejemplo ${hiveconf: inputtable}, ${hiveconf:partitionedtable}).

    Hola **iniciar** y **final** propiedades de canalización de hello especifica el periodo activo de Hola de canalización de Hola.

    En JSON de la actividad de hello, especifique ese script de Hive Hola se ejecuta en proceso Hola especificado por hello **linkedServiceName** : **HDInsightOnDemandLinkedService**.

   > [!NOTE]
   > Consulte la sección "JSON de canalización" en [canalizaciones y actividades de Data Factory de Azure](data-factory-create-pipelines.md) para obtener más información acerca de las propiedades JSON que se usan en el ejemplo de Hola.

2. Confirme que aparece hello **input.log** archivo Hola **adfgetstarted/inputdata** carpeta Hola almacenamiento de blobs de Azure y ejecución Hola después de la canalización de comandos toodeploy Hola de. Desde hello **iniciar** y **final** veces se establecen en los último hello y **isPaused** es toofalse de conjunto, canalización Hola ejecuciones (actividad de canalización de hello) inmediatamente después de implementar.

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. Enhorabuena, ya creó correctamente su primera canalización con Azure PowerShell.

## <a name="monitor-pipeline"></a>Supervisión de la canalización
En este paso, utilice toomonitor de PowerShell de Azure que está sucediendo en una factoría de datos de Azure.

1. Ejecutar **Get AzureRmDataFactory** y asignar Hola salida tooa **$df** variable.

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. Ejecutar **Get AzureRmDataFactorySlice** tooget obtener más información acerca de todos los sectores de hello **EmpSQLTable**, que es la tabla de salida de hello de canalización de Hola.

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    Tenga en cuenta que Hola StartDateTime que especifique aquí es hello que igual especificado en JSON de la canalización de Hola de hora de inicio. Este es el resultado de ejemplo de Hola:

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. Ejecutar **AzureRmDataFactoryRun Get** tooget Hola detalles de actividad se ejecuta durante un determinado segmento.

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    Este es el resultado de ejemplo de Hola: 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    Puede mantener ejecutar este cmdlet hasta que vea en el sector de hello **listo** estado o **error** estado. Al segmento de hello está en estado listo, comprobar hello **partitioneddata** carpeta Hola **adfgetstarted** contenedor en el almacenamiento de blobs para hello los datos de salida.  La creación de un clúster de HDInsight a petición normalmente requiere algo de tiempo.

    ![datos de salida](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> La creación de un clúster de HDInsight a petición normalmente tarda algún tiempo (20 minutos aproximadamente). Por consiguiente, esperan Hola canalización tootake **aproximadamente 30 minutos** tooprocess Hola segmento.
>
> archivo de entrada de Hola se elimina al segmento de Hola se procesa correctamente. Por lo tanto, si desea toorerun Hola sector u Hola tutorial nuevo, cargar toohello inputdata carpeta de hello archivo de entrada (input.log) del contenedor de adfgetstarted Hola.
>
>

## <a name="summary"></a>Resumen
En este tutorial, ha creado un datos tooprocess de factoría de datos de Azure mediante la ejecución de script de Hive en un clúster de hadoop de HDInsight. Utiliza el Editor de generador de datos de Hola Hola toodo portal Azure Hola siguiendo los pasos:

1. Ha creado una **factoría de datos**de Azure.
2. Ha creado dos **servicios vinculados**:
   1. **Almacenamiento de Azure** vinculado servicio toolink el almacenamiento de blobs de Azure que contiene la factoría de datos de archivos de entrada/salida toohello.
   2. **HDInsight de Azure** toolink de servicio vinculado a petición una factoría de datos a petición toohello de clúster de Hadoop de HDInsight. Factoría de datos de Azure crea un Hadoop de HDInsight los datos de entrada de tooprocess just-in-time de clúster y generan datos de salida.
3. Crea dos **conjuntos de datos**, que describen los datos de entrada y salidos de actividad de Hive de HDInsight en la canalización de Hola.
4. Ha creado una **canalización** con una actividad de **Hive de HDInsight**.

## <a name="next-steps"></a>Pasos siguientes
En este artículo, creó una canalización con una actividad de transformación (actividad de HDInsight) que ejecuta un script de Hive en un clúster de HDInsight de Azure a petición. toosee toouse una toocopy de datos de actividad de copia de un tooAzure de Blob de Azure SQL, vea [Tutorial: copiar los datos de un tooAzure de Blob de Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="see-also"></a>Otras referencias
| Tema. | Descripción |
|:--- |:--- |
| [Referencia para cmdlets de Factoría de datos](/powershell/module/azurerm.datafactories) |Consulte la documentación completa sobre los cmdlets de Factoría de datos |
| [Procesos](data-factory-create-pipelines.md) |En este artículo le ayudará a comprender las canalizaciones y actividades de Data Factory de Azure y cómo toouse les tooconstruct-to-end orientadas a datos los flujos de trabajo para su escenario o una empresa. |
| [Conjuntos de datos](data-factory-create-datasets.md) |Este artículo le ayuda a comprender los conjuntos de datos de Data Factory de Azure. |
| [Programación y ejecución](data-factory-scheduling-and-execution.md) |En este artículo se explica los aspectos de programación y la ejecución de hello Data Factory de Azure del modelo de aplicación. |
| [Supervisión y administración de canalizaciones de Data Factory de Azure mediante la nueva Aplicación de supervisión y administración](data-factory-monitor-manage-app.md) |Este artículo describe cómo administrar toomonitor y depurar las canalizaciones utilizando Hola supervisión y administración de aplicaciones. |
