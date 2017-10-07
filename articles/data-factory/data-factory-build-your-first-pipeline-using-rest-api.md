---
title: "aaaBuild su primera factoría de datos (REST) | Documentos de Microsoft"
description: "En este tutorial se crea un ejemplo de canalización de Data Factory de Azure con la API de REST de Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 5d8e39bd598cca35f91d501bad74e8a8436f8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a>Tutorial: Compilación de la primera instancia de Azure Data Factory con la API de REST de Data Factory
> [!div class="op_single_selector"]
> * [Introducción y requisitos previos](data-factory-build-your-first-pipeline.md)
> * [Portal de Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Plantilla de Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API DE REST](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


En este artículo, use API de REST de factoría de datos toocreate su primera factoría de datos de Azure. tutorial de hello toodo mediante otra herramientas y SDK, seleccione una de las opciones de Hola de lista desplegable de Hola.

canalización de Hello en este tutorial tiene una actividad: **actividad de HDInsight Hive**. Esta actividad ejecuta un script de hive en un clúster de HDInsight de Azure que las transformaciones de entrada de datos de salida de datos tooproduce. canalización de Hello es toorun programado una vez que un mes entre Hola especificado horas de inicio y finalización.

> [!NOTE]
> Este artículo no cubre Hola todas las API de REST. Para obtener documentación completa sobre la API de REST, consulte la [referencia de la API de REST de Data Factory](/rest/api/datafactory/).
> 
> pero cualquier canalización puede tener más de una actividad. Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad. Para más información, consulte [Programación y ejecución en Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).


## <a name="prerequisites"></a>Requisitos previos
* Lea [Tutorial de introducción](data-factory-build-your-first-pipeline.md) hello completa y artículo **prerequisite** pasos.
* Instale [Curl](https://curl.haxx.se/dlwiz/) en su máquina. Usar herramienta de hello CURL con REST comandos toocreate una factoría de datos.
* Siga las instrucciones de [este artículo](../azure-resource-manager/resource-group-create-service-principal-portal.md) para:
  1. Cree una aplicación web denominada **ADFGetStartedApp** en Azure Active Directory.
  2. Obtenga el **Id. de cliente** y la **Clave secreta**.
  3. Obtenga el **Identificador de inquilino**.
  4. Asignar Hola **ADFGetStartedApp** aplicación toohello **colaborador de la factoría de datos** rol.
* Instale [Azure PowerShell](/powershell/azure/overview).
* Iniciar **PowerShell** y ejecución Hola siguiente comando. Mantenga Azure PowerShell abierta hasta final de Hola de este tutorial. Si cerrar y volver a abrir, se necesitan toorun comandos de Hola de nuevo.
  1. Ejecutar **AzureRmAccount de inicio de sesión** y escriba el nombre de usuario de Hola y la contraseña que usa toosign en toohello portal de Azure.
  2. Ejecutar **AzureRmSubscription Get** tooview todos Hola suscripciones para esta cuenta.
  3. Ejecutar **Get-AzureRmSubscription - SubscriptionName NameOfAzureSubscription | Conjunto AzureRmContext** suscripción de hello tooselect que desea toowork con. Reemplace **NameOfAzureSubscription** con el nombre de Hola de su suscripción de Azure.
* Crear un grupo de recursos de Azure denominado **ADFTutorialResourceGroup** ejecutando Hola siguiente comando en hello PowerShell:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   Algunos de los pasos de hello en este tutorial se supone que usa el grupo de recursos de hello llamado ADFTutorialResourceGroup. Si utiliza un grupo de recursos diferente, necesita toouse Hola nombre de su grupo de recursos en lugar de ADFTutorialResourceGroup en este tutorial.

## <a name="create-json-definitions"></a>Creación de definiciones de JSON
Crear siguientes archivos JSON en carpeta Hola donde se encuentra curl.exe.

### <a name="datafactoryjson"></a>datafactory.json
> [!IMPORTANT]
> Nombre debe ser único globalmente, por lo que puede tooprefix/sufijo ADFCopyTutorialDF toomake, un nombre único.
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> Reemplace **accountname** y **accountkey** por el nombre y la clave de su cuenta de almacenamiento de Azure. toolearn el proceso tooget el almacenamiento de acceso de clave, vea Hola información acerca de cómo tooview, copiar y regenerar almacenamiento tener acceso a claves de [administrar su cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
>
>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="hdinsightondemandlinkedservicejson"></a>hdinsightondemandlinkedservice.json

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
| ClusterSize |Tamaño de clúster de HDInsight Hola. |
| TimeToLive |Especifica ese tiempo de inactividad de hello para el clúster de HDInsight de hello, antes de eliminarla. |
| linkedServiceName |Especifica la cuenta de almacenamiento de Hola que es toostore usado Hola registros generados por HDInsight |

Tenga en cuenta Hola siguientes puntos:

* Hello factoría de datos se crea un **basados en Linux** clúster de HDInsight automáticamente con hello por encima de JSON. Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .
* Puede usar **su propio clúster de HDInsight** en lugar de usar un clúster de HDInsight a petición. Para más información, consulte [Servicio vinculado de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .
* clúster de HDInsight de Hello crea un **contenedor predeterminado** en almacenamiento de blobs de Hola que especificó en hello JSON (**linkedServiceName**). HDInsight no elimine este contenedor cuando se elimina el clúster de Hola. Este comportamiento es así por diseño. Con el servicio de vinculado de HDInsight a petición, se crea un clúster de HDInsight cada vez que se procesa un segmento a menos que haya un clúster existente en vivo (**timeToLive**) y se elimina cuando se realiza un procesamiento Hola.

    A medida que se procesen más segmentos, verá numerosos contenedores en su Almacenamiento de blobs de Azure. Si no se necesita para solucionar problemas de trabajos de hello, quizá le interese toodelete ellos el costo de almacenamiento de tooreduce Hola. nombres de Hola de estos contenedores siguen un patrón: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Usar herramientas como [Explorador de almacenamiento de Microsoft](http://storageexplorer.com/) almacenamiento de blobs de contenedores de toodelete en Azure.

Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .

### <a name="inputdatasetjson"></a>inputdataset.json

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

Hola JSON define un conjunto de datos denominado **AzureBlobInput**, que representa los datos de entrada para una actividad de canalización de Hola. Además, especifica que los datos de entrada de Hola se encuentran en contenedor de blob de hello denominado **adfgetstarted** y carpeta Hola llamada **inputdata**.

Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:

| Propiedad | Descripción |
|:--- |:--- |
| type |propiedad de tipo Hello se establece tooAzureBlob porque los datos residen en el almacenamiento de blobs de Azure. |
| linkedServiceName |se refiere toohello StorageLinkedService que creó anteriormente. |
| fileName |Esta propiedad es opcional. Si se omite esta propiedad, se seleccionan todos los archivos de Hola de hello folderPath. En este caso, se procesa solo hello input.log. |
| type |archivos de registro de Hello están en formato de texto, por lo que usamos TextFormat. |
| columnDelimiter |las columnas en los archivos de registro de hello se delimitan por un carácter de coma () |
| frecuencia/intervalo |la frecuencia debe establecer tooMonth y interval es 1, lo que significa que están disponibles los segmentos de entrada de hello mensualmente. |
| external |Esta propiedad se establece tootrue si servicio de factoría de datos de hello no genera datos de entrada de saludo. |

### <a name="outputdatasetjson"></a>outputdataset.json

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

Hola JSON define un conjunto de datos denominado **AzureBlobOutput**, que representa los datos de salida para una actividad de canalización de Hola. Además, especifica que los resultados de Hola se almacenan en contenedor de blob de hello denominado **adfgetstarted** y carpeta Hola llamada **partitioneddata**. Hola **disponibilidad** sección especifica ese conjunto de datos de salida de hello se genera mensualmente.

### <a name="pipelinejson"></a>pipeline.json
> [!IMPORTANT]
> Reemplace **storageaccountname** por el nombre de la cuenta de Almacenamiento de Azure.
>
>

```JSON
{
    "name": "MyFirstPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                "scriptLinkedService": "AzureStorageLinkedService",
                "defines": {
                    "inputtable": "wasb://adfgetstarted@<stroageaccountname>.blob.core.windows.net/inputdata",
                    "partitionedtable": "wasb://adfgetstarted@<stroageaccountname>t.blob.core.windows.net/partitioneddata"
                }
            },
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }],
        "start": "2017-07-10T00:00:00Z",
        "end": "2017-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

En el fragmento JSON de hello, desea crear una canalización que consta de una actividad única que usa datos de tooprocess de Hive en un clúster de HDInsight.

archivo de script de Hive de Hello, **partitionweblogs.hql**, se almacena en hello cuenta de almacenamiento de Azure (especificado por scriptLinkedService hello, denominado **StorageLinkedService**) y en **secuencias de comandos**  carpeta en el contenedor de hello **adfgetstarted**.

Hola **define** sección especifica los valores de tiempo de ejecución que se pasan el script de hive toohello como valores de configuración de Hive (por ejemplo ${hiveconf: inputtable}, ${hiveconf:partitionedtable}).

Hola **iniciar** y **final** propiedades de canalización de hello especifica el periodo activo de Hola de canalización de Hola.

En JSON de la actividad de hello, especifique ese script de Hive Hola se ejecuta en proceso Hola especificado por hello **linkedServiceName** : **HDInsightOnDemandLinkedService**.

> [!NOTE]
> Consulte la sección "JSON de canalización" en [canalizaciones y actividades de Data Factory de Azure](data-factory-create-pipelines.md) para obtener más información sobre propiedades JSON que se usan en el anterior ejemplo de Hola.
>
>

## <a name="set-global-variables"></a>Definición de variables globales
En Azure PowerShell, ejecute hello después de comandos después de reemplazar los valores de hello con su propio:

> [!IMPORTANT]
> Consulte la sección [Requisitos previos](#prerequisites) para obtener instrucciones sobre cómo obtener el identificador de cliente, el secreto del cliente, el identificador de inquilino y el identificador de suscripción.
>
>

```PowerShell
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "FirstDataFactoryREST"
```


## <a name="authenticate-with-aad"></a>Autenticación con AAD

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a>Creación de Data Factory
En este paso, creará una instancia de Data Factory de Azure llamada **LogProcessingFactory**. Una factoría de datos puede tener una o más canalizaciones. Una canalización puede tener una o más actividades. Por ejemplo, una actividad de copia toocopy datos de un almacén de datos de origen tooa destino y un toorun de actividad de Hive de HDInsight una tootransform de datos de script de Hive. Ejecute hello después de la factoría de datos de comandos toocreate hello:

1. Asignar Hola comando toovariable denominado **cmd**.

    Confirmar ese nombre Hola Hola factoría de datos que especifique aquí (ADFCopyTutorialDF) coincidencias Hola nombre especificado en hello **datafactory.json**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. Ejecutar comandos de hello mediante **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Ver los resultados de Hola. Si se ha creado correctamente la factoría de datos de hello, vea Hola JSON de factoría de datos de Hola Hola **resultados**; en caso contrario, verá un mensaje de error.

    ```PowerShell
    Write-Host $results
    ```

Tenga en cuenta Hola siguientes puntos:

* nombre de Hola de hello Data Factory de Azure debe ser único globalmente. Si ve errores de hello en los resultados: **nombre de generador de datos "FirstDataFactoryREST" no está disponible**, Hola lo siguiente:
  1. Cambiar el nombre de hello (por ejemplo, yournameFirstDataFactoryREST) en hello **datafactory.json** archivo. Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.
  2. En el primer comando de Hola Hola donde **$cmd** se asigna un valor variable, reemplace FirstDataFactoryREST con el nombre nuevo de Hola y ejecute el comando de Hola.
  3. Resultados de la ejecución toocreate de API de REST de hello dos comandos siguientes tooinvoke Hola Hola datos generador e impresión Hola de operación de Hola.
* instancias de la factoría de datos de toocreate, deberá toobe un colaborador o administrador de hello suscripción de Azure
* nombre Hola Hola factoría de datos se puede registrarse como un nombre DNS en hello futuras y, por tanto, están visible públicamente.
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

Antes de crear una canalización, necesita toocreate algunas entidades de la factoría de datos en primer lugar. En primer lugar crear datos de servicios vinculados toolink almacenes/calcula tooyour y almacén de datos, definen una entrada generar conjuntos de datos toorepresent datos en almacenes de datos vinculado.

## <a name="create-linked-services"></a>Crear servicios vinculados
En este paso, vincular su cuenta de almacenamiento de Azure y un generador de datos a petición tooyour de clúster de HDInsight de Azure. Hola cuenta de almacenamiento de Azure que contiene datos de entrada y salidas de la canalización de hello en este ejemplo de Hola. Hola servicio vinculado de HDInsight es toorun usa un script de Hive especificado en la actividad de hello de canalización de hello en este ejemplo.

### <a name="create-azure-storage-linked-service"></a>Creación de un servicio vinculado de Almacenamiento de Azure
En este paso, vincule la factoría de datos de tooyour de cuenta de almacenamiento de Azure. Con este tutorial, utilice Hola misma cuenta de almacenamiento de Azure hello HQL y datos de entrada/salida de toostore los archivos de scripts.

1. Asignar Hola comando toovariable denominado **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Ejecutar comandos de hello mediante **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Ver los resultados de Hola. Si Hola vinculado se ha creado correctamente el servicio, vea Hola JSON para el servicio de hello vinculado en hello **resultados**; en caso contrario, verá un mensaje de error.

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a>Creación de un servicio vinculado de HDInsight de Azure
En este paso, vincular un generador de datos a petición tooyour de clúster de HDInsight. clúster de HDInsight de Hello automáticamente está creado en tiempo de ejecución y eliminar después de hacerlo inactivos y procesamiento para el período de tiempo especificado de Hola. Puede usar su propio clúster de HDInsight en lugar de usar un clúster de HDInsight a petición. Consulte [Servicios vinculados de procesos](data-factory-compute-linked-services.md) para más información.

1. Asignar Hola comando toovariable denominado **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. Ejecutar comandos de hello mediante **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Ver los resultados de Hola. Si Hola vinculado se ha creado correctamente el servicio, vea Hola JSON para el servicio de hello vinculado en hello **resultados**; en caso contrario, verá un mensaje de error.

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a>Creación de conjuntos de datos
En este paso, creación de conjuntos de datos toorepresent Hola entrada y salida de datos para el procesamiento de Hive. Estos conjuntos de datos, consulte toohello **StorageLinkedService** ha creado anteriormente en este tutorial. Hola tooan de puntos de servicio vinculado cuenta de almacenamiento de Azure y los conjuntos de datos especifiquen contenedor, carpeta, nombre de archivo en el almacenamiento de Hola que contiene la entrada y salida de datos.

### <a name="create-input-dataset"></a>Creación de un conjunto de datos de entrada
En este paso, creará Hola conjunto de datos de entrada toorepresent entrada los datos almacenados en almacenamiento de blobs de Azure de Hola.

1. Asignar Hola comando toovariable denominado **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. Ejecutar comandos de hello mediante **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Ver los resultados de Hola. Si se ha creado correctamente el conjunto de datos de hello, vea hello JSON para el conjunto de datos de Hola Hola **resultados**; en caso contrario, verá un mensaje de error.

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a>Creación del conjunto de datos de salida
En este paso, creará Hola salida dataset toorepresent salida los datos almacenados en hello almacenamiento de blobs de Azure.

1. Asignar Hola comando toovariable denominado **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. Ejecutar comandos de hello mediante **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Ver los resultados de Hola. Si se ha creado correctamente el conjunto de datos de hello, vea hello JSON para el conjunto de datos de Hola Hola **resultados**; en caso contrario, verá un mensaje de error.

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a>Creación de una canalización
En este paso, creará la primera canalización con una actividad **HDInsightHive** . Segmento de entrada está disponible mensual (frecuencia: mes, intervalo: 1), segmento de salida se genera mensualmente y Hola programador propiedad actividad hello también está configurada toomonthly. debe coincidir con la configuración de Hello para el conjunto de datos de salida de Hola y el programador de la actividad de Hola. Actualmente, el conjunto de datos de salida es qué unidades Hola programación, por lo que debe crear un conjunto de datos de salida aunque actividad hello no genera ningún resultado. Si la actividad hello no toma ninguna entrada, puede omitir creación Hola de conjunto de datos entrada.

Confirme que aparece hello **input.log** archivo Hola **adfgetstarted/inputdata** carpeta Hola almacenamiento de blobs de Azure y ejecución Hola después de la canalización de comandos toodeploy Hola de. Desde hello **iniciar** y **final** veces se establecen en los último hello y **isPaused** es toofalse de conjunto, canalización Hola ejecuciones (actividad de canalización de hello) inmediatamente después de implementar.

1. Asignar Hola comando toovariable denominado **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. Ejecutar comandos de hello mediante **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Ver los resultados de Hola. Si se ha creado correctamente el conjunto de datos de hello, vea hello JSON para el conjunto de datos de Hola Hola **resultados**; en caso contrario, verá un mensaje de error.

    ```PowerShell
    Write-Host $results
    ```
4. Enhorabuena, ya creó correctamente su primera canalización con Azure PowerShell.

## <a name="monitor-pipeline"></a>Supervisión de la canalización
En este paso, utilice sectores de toomonitor de API de REST de factoría de datos se está generados en la canalización de Hola.

```PowerShell
$ds ="AzureBlobOutput"

$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};

$results2 = Invoke-Command -scriptblock $cmd;

IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

> [!IMPORTANT]
> La creación de un clúster de HDInsight a petición normalmente tarda algún tiempo (20 minutos aproximadamente). Por consiguiente, esperan Hola canalización tootake **aproximadamente 30 minutos** tooprocess Hola segmento.
>
>

Ejecute Invoke-Command Hola y Hola siguiente hasta que vea sector hello en **listo** estado o **error** estado. Al segmento de hello está en estado listo, comprobar hello **partitioneddata** carpeta Hola **adfgetstarted** contenedor en el almacenamiento de blobs para hello los datos de salida.  creación de Hello de un clúster de HDInsight a petición normalmente tarda algún tiempo.

![datos de salida](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> archivo de entrada de Hola se elimina al segmento de Hola se procesa correctamente. Por lo tanto, si desea toorerun Hola sector u Hola tutorial nuevo, cargar toohello inputdata carpeta de hello archivo de entrada (input.log) del contenedor de adfgetstarted Hola.
>
>

También puede utilizar Azure toomonitor portal sectores y solucione cualquier problema. Consulte más detalles en la sección sobre la [supervisión de canalizaciones con el Portal de Azure](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) .

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
| [Referencia de API de REST de Data Factory](/rest/api/datafactory/) |Consulte la documentación completa sobre los cmdlets de Factoría de datos |
| [Procesos](data-factory-create-pipelines.md) |En este artículo le ayudará a comprender las canalizaciones y actividades de Data Factory de Azure y cómo toouse les tooconstruct-to-end orientadas a datos los flujos de trabajo para su escenario o una empresa. |
| [Conjuntos de datos](data-factory-create-datasets.md) |Este artículo le ayuda a comprender los conjuntos de datos de Data Factory de Azure. |
| [Programación y ejecución](data-factory-scheduling-and-execution.md) |En este artículo se explica los aspectos de programación y la ejecución de hello Data Factory de Azure del modelo de aplicación. |
| [Supervisión y administración de canalizaciones de Data Factory de Azure mediante la nueva Aplicación de supervisión y administración](data-factory-monitor-manage-app.md) |Este artículo describe cómo administrar toomonitor y depurar las canalizaciones utilizando Hola supervisión y administración de aplicaciones. |
