---
title: "Tutorial: Use la API de REST toocreate una canalización del generador de datos de Azure | Documentos de Microsoft"
description: "En este tutorial, use API de REST toocreate una canalización del generador de datos de Azure con una toocopy de datos de actividad de copia desde un almacenamiento de blobs de Azure una base de datos de SQL Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: aa6c9b035101c4ff9acff90117ca6e3e7067f418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a>Tutorial: Use la API de REST toocreate un toocopy de datos de canalización de factoría de datos de Azure 
> [!div class="op_single_selector"]
> * [Introducción y requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Asistente para copia](data-factory-copy-data-wizard-tutorial.md)
> * [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Plantilla de Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API DE REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API de .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

En este artículo, aprenderá cómo toouse REST API toocreate una factoría de datos con una canalización que copia datos de una base de datos de SQL Azure del tooan de almacenamiento blob de Azure. Si es nuevo tooAzure factoría de datos, lea hello [tooAzure Introducción factoría de datos](data-factory-introduction.md) artículo antes de realizar este tutorial.   

En este tutorial, creará una canalización con una actividad en ella: la actividad de copia. actividad de copia de Hello copia datos de un almacén de datos de datos admitidos almacén tooa receptor admitidos. Para obtener una lista de almacenes de datos que se admiten como orígenes y receptores, consulte los [almacenes de datos admitidos](data-factory-data-movement-activities.md#supported-data-stores-and-formats). actividad Hello funciona con un servicio disponible globalmente que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable. Para obtener más información acerca de la actividad de copia de hello, consulte [las actividades de movimiento de datos](data-factory-data-movement-activities.md).

pero cualquier canalización puede tener más de una actividad. Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad. Para más información, consulte [Varias actividades en una canalización](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE]
> Este artículo no cubre Hola todas las API de REST de factoría de datos. Consulte [Referencia de API de REST de Data Factory](/rest/api/datafactory/) para ver la documentación completa sobre los cmdlets de Data Factory.
>  
> canalización de datos de Hello en este tutorial copia datos de un almacén de datos de destino de origen datos almacén tooa. Para obtener un tutorial sobre cómo tootransform los datos mediante Data Factory de Azure, consulte [Tutorial: generar una canalización de datos tootransform con clúster de Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Requisitos previos
* Vaya a través de [Tutorial Introducción](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) hello completa y **prerequisite** pasos.
* Instale [Curl](https://curl.haxx.se/dlwiz/) en su máquina. Usar herramienta de hello Curl con REST comandos toocreate una factoría de datos. 
* Siga las instrucciones de [este artículo](../azure-resource-manager/resource-group-create-service-principal-portal.md) para: 
  1. Cree una aplicación web denominada **ADFCopyTutorialApp** en Azure Active Directory.
  2. Obtenga el **Id. de cliente** y la **Clave secreta**. 
  3. Obtenga el **Identificador de inquilino**. 
  4. Asignar Hola **ADFCopyTutorialApp** aplicación toohello **colaborador de la factoría de datos** rol.  
* Instale [Azure PowerShell](/powershell/azure/overview).  
* Iniciar **PowerShell** y Hola lo siguiente. Mantenga Azure PowerShell abierta hasta final de Hola de este tutorial. Si cerrar y volver a abrir, se necesitan toorun comandos de Hola de nuevo.
  
  1. Ejecute el siguiente comando de Hola y escriba el nombre de usuario de Hola y la contraseña que usa toosign en toohello portal de Azure:
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. Ejecute hello después comando tooview todas las suscripciones de Hola para esta cuenta:

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. Ejecute hello después de suscripción de hello tooselect de comando que desee toowork con. Reemplace  **&lt;NameOfAzureSubscription** &gt; con el nombre de Hola de su suscripción de Azure. 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. Crear un grupo de recursos de Azure denominado **ADFTutorialResourceGroup** ejecutando Hola siguiente comando en hello PowerShell:  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      Si ya existe el grupo de recursos de hello, especifique si tooupdate se (Y) o mantener un nivel tan (N). 
     
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
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> Reemplace **accountname** y **accountkey** por el nombre y la clave de su cuenta de almacenamiento de Azure. toolearn cómo tooget el almacenamiento de tener acceso a clave, consulte [ver, copiar y regenerar almacenamiento de claves de acceso](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).

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

Para más información acerca de las propiedades JSON, consulte [servicio vinculado Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service).

### <a name="azuersqllinkedservicejson"></a>azuersqllinkedservice.json
> [!IMPORTANT]
> Reemplace **servername**, **databasename**, **nombre de usuario**, y **contraseña** con el nombre del servidor SQL Azure, nombre de base de datos SQL, usuario cuenta y contraseña de cuenta de hello.  
> 
>

```JSON
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

Para más información acerca de las propiedades JSON, consulte [servicio vinculado Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties).

### <a name="inputdatasetjson"></a>inputdataset.json

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
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
    "type": "AzureBlob",
    "linkedServiceName": "AzureStorageLinkedService",
    "typeProperties": {
      "folderPath": "adftutorial/",
      "fileName": "emp.txt",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ","
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:

| Propiedad | Descripción |
|:--- |:--- |
| type | propiedad de tipo Hello se establece demasiado**AzureBlob** porque los datos residen en un almacenamiento de blobs de Azure. |
| linkedServiceName | Hace referencia a toohello **AzureStorageLinkedService** que creó anteriormente. |
| folderPath | Especifica el blob de hello **contenedor** hello y **carpeta** que contiene la entrada de blobs. En este tutorial, adftutorial es el contenedor de blob de Hola y carpeta es la carpeta raíz de Hola. | 
| fileName | Esta propiedad es opcional. Si se omite esta propiedad, se seleccionan todos los archivos de hello folderPath. En este tutorial, **emp.txt** se especificó para hello nombre de archivo, por lo que sólo ese archivo se recoge para su procesamiento. |
| formato -> tipo |archivo de entrada de Hello es hello en formato de texto, por lo que usamos **TextFormat**. |
| columnDelimiter | columnas de Hello en el archivo de entrada de Hola se delimitan mediante **carácter de coma (`,`)**. |
| frecuencia/intervalo | frecuencia de Hola se establece demasiado**hora** e intervalo está establecido demasiado**1**, lo que significa que Hola entrada sectores están disponibles **cada hora**. En otras palabras, Hola servicio Data Factory busca datos de entrada cada hora en carpeta de raíz de hello del contenedor de blobs (**adftutorial**) que especificó. Busca datos Hola Hola canalización inicio y finalización horas, no antes o después de esas horas.  |
| external | Esta propiedad se establece demasiado**true** si no se generan datos de hello esta canalización. datos de entrada de Hello en este tutorial están en el archivo emp.txt de hello, que no se genera esta canalización, por lo que se establece esta propiedad tootrue. |

Para más información acerca de estas propiedades JSON, consulte el [artículo sobre el conector de blob de Azure](data-factory-azure-blob-connector.md#dataset-properties).

### <a name="outputdatasetjson"></a>outputdataset.json

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
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
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "emp"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:

| Propiedad | Descripción |
|:--- |:--- |
| type | propiedad de tipo Hello se establece demasiado**AzureSqlTable** porque datos están la tabla de tooa copiado en una base de datos de SQL Azure. |
| linkedServiceName | Hace referencia a toohello **AzureSqlLinkedService** que creó anteriormente. |
| tableName | Hola especificado **tabla** toowhich Hola datos se copian. | 
| frecuencia/intervalo | Hello frecuencia se establece demasiado**hora** y el intervalo es **1**, lo que significa que se producen los sectores de salida de hello **cada hora** entre el inicio de la canalización de Hola y de finalización veces, no antes o Después de esas horas.  |

Hay tres columnas: **identificador**, **FirstName**, y **LastName** : en la tabla emp de hello en la base de datos de Hola. Id. es una columna de identidad, por lo que necesita solo toospecify **FirstName** y **LastName** aquí.

Para más información acerca de estas propiedades JSON, consulte el artículo sobre el [conector de Azure SQL Database](data-factory-azure-sql-connector.md#dataset-properties).

### <a name="pipelinejson"></a>pipeline.json

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data tooAzure SQL database",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2017-05-11T00:00:00Z",
    "end": "2017-05-12T00:00:00Z"
  }
}
```

Tenga en cuenta Hola siguientes puntos:

- En la sección de actividades de hello, hay sólo una actividad cuyo **tipo** se establece demasiado**copia**. Para obtener más información acerca de la actividad de copia de hello, consulte [las actividades de movimiento de datos](data-factory-data-movement-activities.md). En las soluciones de Data Factory, también puede usar [actividades de transformación de datos](data-factory-data-transformation-activities.md).
- Entrada de actividad hello se establece demasiado**AzureBlobInput** y salida de actividad hello se establece demasiado**AzureSqlOutput**. 
- Hola **typeProperties** sección, **BlobSource** se especifica como tipo de origen de Hola y **SqlSink** se especifica como el tipo de receptor de Hola. Para obtener una lista completa de los almacenes de datos compatibles con la actividad de copia de hello como orígenes y receptores, vea [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn cómo almacenar toouse datos compatibles especificados como un origen/receptor, haga clic en el vínculo hello en la tabla de Hola.  
 
Reemplazar el valor de Hola de hello **iniciar** propiedad con hello día actual y **final** valor con hello día siguiente. Puede especificar sólo parte de fecha de Hola y omitir la parte de hora de Hola de hello fecha y hora. Por ejemplo, "2017-02-03", que es equivalente demasiado "2017-02-03T00:00:00Z"
 
Las fechas y horas de inicio y de finalización deben estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por ejemplo: 2016-10-14T16:32:41Z. Hola **final** tiempo es opcional, pero se usa en este tutorial. 
 
Si no especifica el valor de hello **final** propiedad, se calcula como "**inicio + 48 horas**". canalización de hello toorun indefinidamente, especifique **9999-09-09** como valor de Hola de hello **final** propiedad.
 
En el anterior ejemplo de Hola, hay 24 segmentos de datos tal y como se produce cada segmento de datos cada hora.

Para obtener descripciones de las propiedades JSON en una definición de canalización, consulte cómo [crear canalizaciones](data-factory-create-pipelines.md). Para obtener descripciones de las propiedades JSON en una definición de actividad de copia, consulte las [actividades de movimiento de datos](data-factory-data-movement-activities.md). Para ver las descripciones de las propiedades JSON admitidas por BlobSource, consulte el artículo sobre el [conector de Azure Blob](data-factory-azure-blob-connector.md). Para ver las descripciones de las propiedades JSON admitidas por SqlSink, consulte el artículo sobre el [conector de Azure SQL Database](data-factory-azure-sql-connector.md).

## <a name="set-global-variables"></a>Definición de variables globales
En Azure PowerShell, ejecute hello después de comandos después de reemplazar los valores de hello con su propio:

> [!IMPORTANT]
> Consulte la sección [Requisitos previos](#prerequisites) para obtener instrucciones sobre cómo obtener el identificador de cliente, el secreto del cliente, el identificador de inquilino y el identificador de suscripción.   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

Ejecute hello siguiente comando después de actualizar el nombre de Hola Hola factoría de datos que usa: 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a>Autenticación con AAD
Siguiente ejecución Hola comando tooauthenticate con Azure Active Directory (AAD): 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a>Creación de Data Factory
En este paso, creará una instancia de Data Factory de Azure llamada **ADFCopyTutorialDF**. Una factoría de datos puede tener una o más canalizaciones. Una canalización puede tener una o más actividades. Por ejemplo, una toocopy de datos de actividad de copia de un origen de datos de destino tooa almacenar. Datos de salida de tooproduct de datos de entrada de un toorun de actividad de Hive de HDInsight un tootransform de script de Hive. Ejecute hello después de la factoría de datos de comandos toocreate hello: 

1. Asignar Hola comando toovariable denominado **cmd**. 
   
    > [!IMPORTANT]
    > Confirmar ese nombre Hola Hola factoría de datos que especifique aquí (ADFCopyTutorialDF) coincidencias Hola nombre especificado en hello **datafactory.json**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. Ejecutar comandos de hello mediante **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Ver los resultados de Hola. Si se ha creado correctamente la factoría de datos de hello, vea Hola JSON de factoría de datos de Hola Hola **resultados**; en caso contrario, verá un mensaje de error.  
   
    ```
    Write-Host $results
    ```

Tenga en cuenta Hola siguientes puntos:

* nombre de Hola de hello Data Factory de Azure debe ser único globalmente. Si ve errores de hello en los resultados: **nombre de generador de datos "ADFCopyTutorialDF" no está disponible**, Hola lo siguiente:  
  
  1. Cambiar el nombre de hello (por ejemplo, yournameADFCopyTutorialDF) en hello **datafactory.json** archivo.
  2. En el primer comando de Hola Hola donde **$cmd** se asigna un valor variable, reemplace ADFCopyTutorialDF con el nombre nuevo de Hola y ejecute el comando de Hola. 
  3. Resultados de la ejecución toocreate de API de REST de hello dos comandos siguientes tooinvoke Hola Hola datos generador e impresión Hola de operación de Hola. 
     
     Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.
* instancias de la factoría de datos de toocreate, deberá toobe un colaborador o administrador de hello suscripción de Azure
* nombre Hola Hola factoría de datos se puede registrarse como un nombre DNS en hello futuras y, por tanto, están visible públicamente.
* Si recibe el error hello: "**esta suscripción no tiene espacio de nombres registrado toouse Microsoft.DataFactory**", siga uno de los procedimientos de Hola e intente publicar de nuevo: 
  
  * En Azure PowerShell, ejecute hello después de proveedor del comando tooregister Hola factoría de datos: 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    Puede ejecutar Hola después comando tooconfirm ese Hola factoría de datos de proveedor está registrado. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Inicio de sesión mediante Hola suscripción de Azure en hello [portal de Azure](https://portal.azure.com) y navegar por hoja de la factoría de datos de tooa crear una factoría de datos en el portal de Azure hello (o). Esta acción registra automáticamente proveedor Hola para usted.

Antes de crear una canalización, necesita toocreate algunas entidades de la factoría de datos en primer lugar. En primer lugar crear origen de toolink servicios vinculados y tooyour datos de almacenes de datos de destino almacenar. A continuación, defina los conjuntos de datos de entrada y salida toorepresent datos en almacenes de datos vinculado. Finalmente, cree la canalización de Hola a una actividad que usa estos conjuntos de datos.

## <a name="create-linked-services"></a>Crear servicios vinculados
Crear servicios vinculados en un toolink de factoría de datos almacenan sus datos y se factoría de datos de toohello de servicios de proceso. En este tutorial, no se usa ningún servicio de proceso, como Azure HDInsight o Azure Data Lake Analytics. Se usan dos almacenes de datos del tipo Azure Storage (origen) y Azure SQL Database (destino). Por lo tanto, se crean dos servicios vinculados llamados AzureStorageLinkedService y AzureSqlLinkedService del tipo AzureStorage y AzureSqlDatabase.  

Hola AzureStorageLinkedService vincula su factoría de datos de toohello de cuenta de almacenamiento de Azure. Esta cuenta de almacenamiento es hello uno en el que se creó un contenedor y cargar datos de hello como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService vincula su factoría de datos de toohello de base de datos de SQL Azure. datos de Hola que se copian desde el almacenamiento de blobs de Hola se almacenan en esta base de datos. Crear tabla emp de hello en esta base de datos como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).  

### <a name="create-azure-storage-linked-service"></a>Creación de un servicio vinculado de Almacenamiento de Azure
En este paso, vincule la factoría de datos de tooyour de cuenta de almacenamiento de Azure. Especificar nombre de Hola y clave de la cuenta de almacenamiento de Azure en esta sección. Vea [servicio vinculado de almacenamiento de Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obtener más información sobre JSON toodefine de propiedades que se usan un almacenamiento de Azure servicio vinculado.  

1. Asignar Hola comando toovariable denominado **cmd**. 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Ejecutar comandos de hello mediante **Invoke-Command**.

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Ver los resultados de Hola. Si Hola vinculado se ha creado correctamente el servicio, vea Hola JSON para el servicio de hello vinculado en hello **resultados**; en caso contrario, verá un mensaje de error.

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a>Creación de un servicio vinculado SQL de Azure
En este paso, vincule la factoría de datos de tooyour de base de datos de SQL Azure. Especifique el nombre del servidor SQL Azure hello, nombre de base de datos, nombre de usuario y contraseña de usuario en esta sección. Vea [servicio vinculado de SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) para obtener más información acerca de toodefine de propiedades que se usan JSON SQL Azure servicio vinculado.

1. Asignar Hola comando toovariable denominado **cmd**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
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
En el paso anterior de hello, crear servicios vinculados toolink su cuenta de almacenamiento de Azure y la factoría de datos de tooyour de base de datos de SQL Azure. En este paso, definirá dos conjuntos de datos con el nombre AzureBlobInput y AzureSqlOutput que representan la entrada y los datos de salida que se almacenan en almacenes de datos de Hola que hace referencia AzureStorageLinkedService y AzureSqlLinkedService respectivamente.

servicio de almacenamiento de Azure vinculado de Hello especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en tiempo de ejecución tooconnect tooyour cuenta de almacenamiento de Azure. Y conjunto de datos de blob de entrada de hello (AzureBlobInput) especifica contenedor de Hola y la carpeta de Hola que contiene los datos de entrada de Hola.  

De forma similar, Hola servicio de base de datos de Azure SQL vinculado especifica cadena de conexión de Hola que usa el servicio de factoría de datos en la base de datos de tiempo de ejecución tooconnect tooyour SQL Azure. Y conjunto de datos de tabla SQL (OututDataset) especifica la tabla de Hola Hola Hola de toowhich de base de datos se copian datos desde almacenamiento de blobs de Hola de salida de hello. 

### <a name="create-input-dataset"></a>Creación de un conjunto de datos de entrada
En este paso, creará un conjunto de datos denominado AzureBlobInput que apunta a un archivo blob tooa (emp.txt) en la carpeta raíz de Hola de un contenedor de blobs (adftutorial) en hello representado por hello AzureStorageLinkedService vinculado servicio de almacenamiento de Azure. Si no especifica un valor para el nombre de archivo de hello (o puede omitirla), datos de todos los blobs en la carpeta de entrada de hello son destino toohello copiada. En este tutorial, especifique un valor para el nombre de archivo de Hola. 

1. Asignar Hola comando toovariable denominado **cmd**. 

    ```PowerSHell   
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
Hola servicio de base de datos de Azure SQL vinculado especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en la base de datos de tiempo de ejecución tooconnect tooyour SQL Azure. Hola salida SQL tabla conjunto de datos (OututDataset) se crea en este paso especifica se copia la tabla de hello en bases de datos Hola Hola toowhich Hola del almacenamiento de blobs.

1. Asignar Hola comando toovariable denominado **cmd**.

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
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
En este paso, creará una canalización con una **actividad de copia** que utiliza **AzureBlobInput** como entrada y **AzureSqlOutput** como salida.

Actualmente, el conjunto de datos de salida es qué unidades Hola programación. En este tutorial, el conjunto de datos de salida es tooproduce configurado un segmento una vez cada hora. canalización de Hello tiene una hora de inicio y la hora de finalización que son un día separado, lo que es de 24 horas. Por lo tanto, 24 segmentos del conjunto de datos de salida generados por la canalización de Hola. 

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

**¡Enhorabuena!** Ha creado correctamente una factoría de datos de Azure, con una canalización que copia datos de base de datos SQL de tooAzure de almacenamiento de blobs de Azure.

## <a name="monitor-pipeline"></a>Supervisión de la canalización
En este paso, utilice sectores de toomonitor de API de REST de factoría de datos se está generados en la canalización de Hola.

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> Asegúrese de que Hola inicial y final horas después de hello especificado en comando coincidencia Hola inicio y finalización de la canalización de Hola. 

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=2017-05-11T00%3a00%3a00.0000000Z"&"end=2017-05-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
```

```PowerShell
$results2 = Invoke-Command -scriptblock $cmd;
```

```PowerShell
IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

Ejecute Invoke-Command Hola y Hola siguiente hasta que vea un segmento en **listo** estado o **error** estado. Al segmento de hello está en estado listo, comprobar hello **emp** tabla en la base de datos de SQL Azure para datos de salida de hello. 

Para cada sector, dos filas de datos de archivo de código fuente de hello son tabla emp de toohello copiados en la base de datos de SQL Azure Hola. Por lo tanto, verá 24 nuevos registros en la tabla emp de hello cuando se han procesado correctamente todos los sectores de hello (en estado listo). 

## <a name="summary"></a>Resumen
En este tutorial, ha utilizado la API de REST toocreate un Azure generador toocopy datos desde una base de datos de SQL Azure de tooan de blobs de Azure. Estos son los pasos de alto nivel de hello realizadas en este tutorial:  

1. Ha creado una **factoría de datos**de Azure.
2. Ha creado **servicios vinculados**.
   1. Un almacenamiento de Azure había vinculada servicio toolink su cuenta de almacenamiento de Azure que contiene datos de entrada.     
   2. SQL Azure había vinculado toolink servicio base de datos SQL de Azure que contiene los datos de salida de hello. 
3. Ha creado **conjuntos de datos**que describen los datos de entrada y salida para las canalizaciones.
4. Ha creado una **canalización** con una actividad de copia con un origen BlobSource y un receptor SqlSink. 

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha usado Azure Blob Storage como almacén de datos de origen y una base de datos SQL de Azure como almacén de datos de destino en una operación de copia. Hello tabla siguiente proporciona una lista de almacenes de datos que se admiten como orígenes y destinos por actividad de copia de hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn acerca de cómo almacenan datos toocopy de datos, haga clic en vínculo Hola Hola de almacén de datos en la tabla de Hola.
