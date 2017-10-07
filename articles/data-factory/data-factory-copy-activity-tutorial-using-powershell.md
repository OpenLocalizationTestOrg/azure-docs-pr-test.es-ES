---
title: "Tutorial: Crear una canalización de datos de toomove mediante el uso de PowerShell de Azure | Documentos de Microsoft"
description: "En este tutorial, creará una canalización de Azure Data Factory con una actividad de copia mediante Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a>Tutorial: Creación de una canalización de Data Factory para mover datos mediante Azure PowerShell
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

En este artículo, aprenderá cómo toouse PowerShell toocreate una factoría de datos con una canalización que copia datos de una base de datos de SQL Azure del tooan de almacenamiento blob de Azure. Si es nuevo tooAzure factoría de datos, lea hello [tooAzure Introducción factoría de datos](data-factory-introduction.md) artículo antes de realizar este tutorial.   

En este tutorial, creará una canalización con una actividad en ella: la actividad de copia. actividad de copia de Hello copia datos de un almacén de datos de datos admitidos almacén tooa receptor admitidos. Para obtener una lista de almacenes de datos que se admiten como orígenes y receptores, consulte los [almacenes de datos admitidos](data-factory-data-movement-activities.md#supported-data-stores-and-formats). actividad Hello funciona con un servicio disponible globalmente que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable. Para obtener más información acerca de la actividad de copia de hello, consulte [las actividades de movimiento de datos](data-factory-data-movement-activities.md).

pero cualquier canalización puede tener más de una actividad. Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad. Para más información, consulte [Varias actividades en una canalización](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE]
> Este artículo no cubre todos los cmdlets de factoría de datos de Hola. Vea [Referencia de cmdlets de Data Factory](/powershell/module/azurerm.datafactories) para obtener la documentación completa sobre estos cmdlets.
> 
> canalización de datos de Hello en este tutorial copia datos de un almacén de datos de destino de origen datos almacén tooa. Para obtener un tutorial sobre cómo tootransform los datos mediante Data Factory de Azure, consulte [Tutorial: generar una canalización de datos tootransform con clúster de Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Requisitos previos
- Complete los requisitos previos descritos en hello [requisitos previos tutoriales](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artículo.
- Instale **Azure PowerShell**. Siga las instrucciones de hello en [cómo tooinstall y configurar Azure PowerShell](../powershell-install-configure.md).

## <a name="steps"></a>Pasos
Estos son los pasos de hello que realizar como parte de este tutorial:

1. Cree una **factoría de datos** de Azure. En este paso, creará una factoría de datos llamada ADFTutorialDataFactoryPSH. 
2. Crear **servicios vinculados** de factoría de datos de Hola. En este paso, se crean dos servicios vinculados del tipo Azure Storage y Azure SQL Database. 
    
    Hola AzureStorageLinkedService vincula su factoría de datos de toohello de cuenta de almacenamiento de Azure. Crea un contenedor y cargar la cuenta de almacenamiento de datos toothis como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService vincula su factoría de datos de toohello de base de datos de SQL Azure. datos de Hola que se copian desde el almacenamiento de blobs de Hola se almacenan en esta base de datos. Como parte de los [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md), se creó una tabla SQL en esta base de datos.   
3. Crear la entrada y salida **conjuntos de datos** de factoría de datos de Hola.  
    
    servicio de almacenamiento de Azure vinculado de Hello especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en tiempo de ejecución tooconnect tooyour cuenta de almacenamiento de Azure. Y el conjunto de datos de hello blob de entrada especifica el contenedor de Hola y la carpeta de Hola que contiene los datos de entrada de Hola.  

    De forma similar, Hola servicio de base de datos de Azure SQL vinculado especifica cadena de conexión de Hola que usa el servicio de factoría de datos en la base de datos de tiempo de ejecución tooconnect tooyour SQL Azure. Y conjunto de datos de tabla SQL de Hola salida especifica se copia la tabla de hello en bases de datos Hola Hola toowhich Hola del almacenamiento de blobs.
4. Crear un **canalización** de factoría de datos de Hola. En este paso, se crea una canalización con una actividad de copia.   
    
    actividad de copia de Hello copia datos de un blob en la tabla de tooa de almacenamiento de blobs de Azure de hello en la base de datos de SQL Azure Hola. Puede usar una actividad de copia en datos toocopy canalización desde cualquier origen compatibles tooany admitida el destino. Para ver una lista de los almacenes de datos admitidos, consulte el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
5. Canalización de Hola de monitor. En este paso, se **monitor** Hola sectores de conjuntos de datos de entrada y salida mediante el uso de PowerShell.

## <a name="create-a-data-factory"></a>Crear una factoría de datos
> [!IMPORTANT]
> Completa [requisitos previos para el tutorial de hello](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) si aún no lo ha hecho.   

Una factoría de datos puede tener una o más canalizaciones. Una canalización puede tener una o más actividades. Por ejemplo, una toocopy de datos de actividad de copia de un almacén de datos de origen tooa destino y un toorun de actividad de Hive de HDInsight un tootransform de script de Hive datos de salida de tooproduct de datos de entrada. Puede empezar con la creación de factoría de datos de hello en este paso.

1. Inicie **PowerShell**. Mantenga Azure PowerShell abierta hasta final de Hola de este tutorial. Si cerrar y volver a abrir, se necesitan toorun comandos de Hola de nuevo.

    Ejecute el siguiente comando de Hola y escriba el nombre de usuario de Hola y la contraseña que usa toosign en toohello portal de Azure:

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    Ejecute hello después comando tooview todas las suscripciones de Hola para esta cuenta:

    ```PowerShell
    Get-AzureRmSubscription
    ```

    Ejecute hello después de suscripción de hello tooselect de comando que desee toowork con. Reemplace  **&lt;NameOfAzureSubscription** &gt; con el nombre de Hola de su suscripción de Azure:

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. Crear un grupo de recursos de Azure denominado **ADFTutorialResourceGroup** ejecutando Hola siguiente comando:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    Algunos de los pasos de hello en este tutorial se supone que usa grupo de recursos de hello llamado **ADFTutorialResourceGroup**. Si utiliza un grupo de recursos diferente, deberá toouse, en lugar de ADFTutorialResourceGroup en este tutorial.
3. Ejecute hello **New-AzureRmDataFactory** una factoría de datos con el nombre del cmdlet toocreate **ADFTutorialDataFactoryPSH**:  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    Puede que ya se esté usando este nombre. Por lo tanto, asegúrese de nombre Hola Hola factoría de datos único mediante la adición de un prefijo o sufijo (por ejemplo: ADFTutorialDataFactoryPSH05152017) y vuelva a ejecutar el comando Hola.  

Tenga en cuenta Hola siguientes puntos:

* nombre de Hola Hola Azure factoría de datos debe ser único globalmente. Si recibes Hola tras error, cambie el nombre de hello (por ejemplo, yournameADFTutorialDataFactoryPSH). Use este nombre en lugar de ADFTutorialFactoryPSH mientras lleva a cabo los pasos de este tutorial. Consulte [Data Factory: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Data Factory.

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* instancias de la factoría de datos de toocreate, debe ser un colaborador o administrador de hello suscripción de Azure.
* nombre Hola Hola factoría de datos puede registrado como un nombre DNS en hello futuras y por lo tanto, están visible públicamente.
* Es posible que reciba Hola siguiente error: "**esta suscripción no tiene espacio de nombres registrado toouse Microsoft.DataFactory.**" Siga uno de los procedimientos de Hola e intente publicar de nuevo:

  * En Azure PowerShell, ejecute hello después de proveedor del comando tooregister Hola factoría de datos:

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    Ejecute hello después comando tooconfirm ese Hola factoría de datos de proveedor está registrado:

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Inicio de sesión mediante el uso de Hola toohello de suscripción de Azure [portal de Azure](https://portal.azure.com). Visite tooa hoja de factoría de datos o crear una factoría de datos en hello portal de Azure. Esta acción registra automáticamente proveedor Hola para usted.

## <a name="create-linked-services"></a>Crear servicios vinculados
Crear servicios vinculados en un toolink de factoría de datos almacenan sus datos y se factoría de datos de toohello de servicios de proceso. En este tutorial, no se usa ningún servicio de proceso, como Azure HDInsight o Azure Data Lake Analytics. Se usan dos almacenes de datos del tipo Azure Storage (origen) y Azure SQL Database (destino). 

Por lo tanto, se crean dos servicios vinculados llamados AzureStorageLinkedService y AzureSqlLinkedService del tipo AzureStorage y AzureSqlDatabase.  

Hola AzureStorageLinkedService vincula su factoría de datos de toohello de cuenta de almacenamiento de Azure. Esta cuenta de almacenamiento es hello uno en el que se creó un contenedor y cargar datos de hello como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService vincula su factoría de datos de toohello de base de datos de SQL Azure. datos de Hola que se copian desde el almacenamiento de blobs de Hola se almacenan en esta base de datos. Crear tabla emp de hello en esta base de datos como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a>Creación de un servicio vinculado para una cuenta de almacenamiento de Azure
En este paso, vincule la factoría de datos de tooyour de cuenta de almacenamiento de Azure.

1. Cree un archivo JSON denominado **AzureStorageLinkedService.json** en **C:\ADFGetStartedPSH** carpeta con hello siguen contenido: (crear Hola carpeta ADFGetStartedPSH si aún no existe.)

    > [!IMPORTANT]
    > Reemplace &lt;accountname&gt; y &lt;accountkey&gt; con nombre y clave de la cuenta de almacenamiento de Azure antes de guardar el archivo hello. 

    ```json
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
2. En **Azure PowerShell**, cambiar toohello **ADFGetStartedPSH** carpeta.
4. Ejecute hello **New-AzureRmDataFactoryLinkedService** cmdlet toocreate Hola servicio vinculado: **AzureStorageLinkedService**. Este cmdlet y otros cmdlets de factoría de datos que se usa en este tutorial requiere que los valores de toopass para hello **ResourceGroupName** y **DataFactoryName** parámetros. Como alternativa, puede pasar Hola DataFactory devueltas mediante el cmdlet New-AzureRmDataFactory Hola sin escribir ResourceGroupName y DataFactoryName cada vez que se ejecuta un cmdlet. 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    Este es el resultado de ejemplo de Hola:

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    Otra manera de crear este servicio vinculado es toospecify nombre de grupo de recursos y el nombre de generador de datos en lugar de especificar el objeto de hello DataFactory.  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a>Creación de un servicio vinculado para una instancia de Azure SQL Database
En este paso, vincule la factoría de datos de tooyour de base de datos de SQL Azure.

1. Cree un archivo JSON denominado AzureSqlLinkedService.json en la carpeta C:\ADFGetStartedPSH con hello siguiente contenido:

    > [!IMPORTANT]
    > Reemplace &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; y &lt;password&gt; por los nombres del servidor SQL Azure, de la base de datos, de la cuenta de usuario y de la contraseña.
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. Ejecute hello después comando toocreate un servicio vinculado:

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    Este es el resultado de ejemplo de Hola:

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   Confirme que **permitir acceso a servicios de tooAzure** esté activada para el servidor de base de datos SQL. tooverify y activarla, Hola lo siguiente:

    1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com)
    2. Haga clic en **más servicios >** Hola izquierda y haga clic en **servidores SQL Server** en hello **bases de datos** categoría.
    3. Seleccione el servidor en la lista de Hola de servidores SQL Server.
    4. En la hoja de hello SQL server, haga clic en **mostrar configuraciones de firewall** vínculo.
    5. Hola **configuración del Firewall** hoja, haga clic en **ON** para **permitir acceso a servicios de tooAzure**.
    6. Haga clic en **guardar** en la barra de herramientas de Hola. 

## <a name="create-datasets"></a>Creación de conjuntos de datos
En el paso anterior de hello, crear servicios vinculados toolink su cuenta de almacenamiento de Azure y la factoría de datos de tooyour de base de datos de SQL Azure. En este paso, definirá dos conjuntos de datos con el nombre InputDataset y OutputDataset que representan la entrada y los datos de salida que se almacenan en almacenes de datos de Hola que hace referencia AzureStorageLinkedService y AzureSqlLinkedService respectivamente.

servicio de almacenamiento de Azure vinculado de Hello especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en tiempo de ejecución tooconnect tooyour cuenta de almacenamiento de Azure. Y conjunto de datos de blob de entrada de hello (InputDataset) especifica contenedor de Hola y la carpeta de Hola que contiene los datos de entrada de Hola.  

De forma similar, Hola servicio de base de datos de Azure SQL vinculado especifica cadena de conexión de Hola que usa el servicio de factoría de datos en la base de datos de tiempo de ejecución tooconnect tooyour SQL Azure. Y conjunto de datos de tabla SQL (OututDataset) especifica la tabla de Hola Hola Hola de toowhich de base de datos se copian datos desde almacenamiento de blobs de Hola de salida de hello. 

### <a name="create-an-input-dataset"></a>Creación de un conjunto de datos de entrada
En este paso, creará un conjunto de datos denominado InputDataset que apunta a un archivo blob tooa (emp.txt) en la carpeta raíz de Hola de un contenedor de blobs (adftutorial) en hello representado por hello AzureStorageLinkedService vinculado servicio de almacenamiento de Azure. Si no especifica un valor para el nombre de archivo de hello (o puede omitirla), datos de todos los blobs en la carpeta de entrada de hello son destino toohello copiada. En este tutorial, especifique un valor para el nombre de archivo de Hola.  

1. Cree un archivo JSON denominado **InputDataset.json** en hello **C:\ADFGetStartedPSH** carpeta, con hello siguen contenido:

    ```json
    {
        "name": "InputDataset",
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
                "fileName": "emp.txt",
                "folderPath": "adftutorial/",
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
2. Ejecute hello siguiendo el conjunto de datos de comando toocreate Hola factoría de datos.

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    Este es el resultado de ejemplo de Hola:

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a>Crear un conjunto de datos de salida
En esta parte del paso de hello, se crea un conjunto de datos de salida denominado **OutputDataset**. Este conjunto de datos señala tooa table de SQL de base de datos de SQL Azure de hello representado por **AzureSqlLinkedService**. 

1. Cree un archivo JSON denominado **OutputDataset.json** en hello **C:\ADFGetStartedPSH** carpeta con hello siguen contenido:

    ```json
    {
        "name": "OutputDataset",
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
2. Ejecute hello siguiendo el conjunto de datos de la factoría de datos de comando toocreate Hola.

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    Este es el resultado de ejemplo de Hola:

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a>Crear una canalización
En este paso, creará una canalización con una **actividad de copia** que utiliza **InputDataset** como entrada y **OutputDataset** como salida.

Actualmente, el conjunto de datos de salida es qué unidades Hola programación. En este tutorial, el conjunto de datos de salida es tooproduce configurado un segmento una vez cada hora. canalización de Hello tiene una hora de inicio y la hora de finalización que son un día separado, lo que es de 24 horas. Por lo tanto, 24 segmentos del conjunto de datos de salida generados por la canalización de Hola. 


1. Cree un archivo JSON denominado **ADFTutorialPipeline.json** en hello **C:\ADFGetStartedPSH** carpeta, con hello siguen contenido:

    ```json   
    {
      "name": "ADFTutorialPipeline",
      "properties": {
        "description": "Copy data from a blob tooAzure SQL table",
        "activities": [
          {
            "name": "CopyFromBlobToSQL",
            "type": "Copy",
            "inputs": [
              {
                "name": "InputDataset"
              }
            ],
            "outputs": [
              {
                "name": "OutputDataset"
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
    - Entrada de actividad hello se establece demasiado**InputDataset** y salida de actividad hello se establece demasiado**OutputDataset**. 
    - Hola **typeProperties** sección, **BlobSource** se especifica como tipo de origen de Hola y **SqlSink** se especifica como el tipo de receptor de Hola. Para obtener una lista completa de los almacenes de datos compatibles con la actividad de copia de hello como orígenes y receptores, vea [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn cómo almacenar toouse datos compatibles especificados como un origen/receptor, haga clic en el vínculo hello en la tabla de Hola.  
     
    Reemplazar el valor de Hola de hello **iniciar** propiedad con hello día actual y **final** valor con hello día siguiente. Puede especificar sólo parte de fecha de Hola y omitir la parte de hora de Hola de hello fecha y hora. Por ejemplo, "2016-02-03", que es equivalente demasiado "2016-02-03T00:00:00Z"
     
    Las fechas y horas de inicio y de finalización deben estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por ejemplo: 2016-10-14T16:32:41Z. Hola **final** tiempo es opcional, pero se usa en este tutorial. 
     
    Si no especifica el valor de hello **final** propiedad, se calcula como "**inicio + 48 horas**". canalización de hello toorun indefinidamente, especifique **9999-09-09** como valor de Hola de hello **final** propiedad.
     
    En el anterior ejemplo de Hola, hay 24 segmentos de datos tal y como se produce cada segmento de datos cada hora.

    Para obtener descripciones de las propiedades JSON en una definición de canalización, consulte cómo [crear canalizaciones](data-factory-create-pipelines.md). Para obtener descripciones de las propiedades JSON en una definición de actividad de copia, consulte las [actividades de movimiento de datos](data-factory-data-movement-activities.md). Para ver las descripciones de las propiedades JSON admitidas por BlobSource, consulte el artículo sobre el [conector de Azure Blob](data-factory-azure-blob-connector.md). Para ver las descripciones de las propiedades JSON admitidas por SqlSink, consulte el artículo sobre el [conector de Azure SQL Database](data-factory-azure-sql-connector.md).
2. Ejecute hello después de la tabla de factoría de datos de comando toocreate Hola.

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    Este es el resultado de ejemplo de Hola: 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

**¡Enhorabuena!** Ha creado correctamente una factoría de datos de Azure con datos toocopy canalización desde una base de datos de SQL Azure del tooan de almacenamiento blob de Azure. 

## <a name="monitor-hello-pipeline"></a>Canalización de Hola de Monitor
En este paso, utilice toomonitor de PowerShell de Azure que está sucediendo en una factoría de datos de Azure.

1. Reemplace &lt;DataFactoryName&gt; con el nombre de saludo de la factoría de datos y ejecute **AzureRmDataFactory Get**y asignar Hola salida tooa $df variable.

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    Por ejemplo:
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    A continuación, ejecute impresión Hola contenido $df toosee Hola después de salida: 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. Ejecutar **Get AzureRmDataFactorySlice** tooget obtener más información acerca de todos los sectores de hello **OutputDataset**, que es el conjunto de datos de salida de hello de canalización de Hola.  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   Esta configuración debe coincidir con hello **iniciar** valor en JSON de la canalización de Hola. Debería ver 24 sectores, uno para cada hora de 12 AM de Hola día actual too12 ESTOY de hello día siguiente.

   A continuación, presentamos tres intervalos de ejemplo de salida de hello: 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. Ejecutar **Get AzureRmDataFactoryRun** tooget Hola detalles de actividad se ejecuta durante un **específico** segmento. Copiar valor de fecha y hora de Hola de salida de hello de hello comando toospecify Hola valor anterior para el parámetro de StartDateTime Hola. 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   Este es el resultado de ejemplo de Hola: 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

Consulte [Referencia de cmdlets de Data Factory](/powershell/module/azurerm.datafactories) para obtener la documentación completa sobre los cmdlets de Data Factory.

## <a name="summary"></a>Resumen
En este tutorial, ha creado un datos toocopy de factoría de datos de Azure desde una base de datos de SQL Azure de tooan de blobs de Azure. Ha utilizado la factoría de datos de PowerShell toocreate hello, servicios vinculados, conjuntos de datos y una canalización. Estos son los pasos de alto nivel de hello realizadas en este tutorial:  

1. Ha creado una **factoría de datos**de Azure.
2. Ha creado **servicios vinculados**.

   a. Un **el almacenamiento de Azure** vinculado toolink de servicio de su cuenta de almacenamiento de Azure que contiene datos de entrada.     
   b. Un **SQL Azure** vinculado toolink de servicio en la base de datos SQL que contiene los datos de salida de hello.
3. Ha creado **conjuntos de datos** que describen los datos de entrada y salida de las canalizaciones.
4. Crea un **canalización** con **actividad de copia**, con **BlobSource** como origen de Hola y **SqlSink** como receptor de Hola.

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha usado Azure Blob Storage como almacén de datos de origen y una base de datos SQL de Azure como almacén de datos de destino en una operación de copia. Hello tabla siguiente proporciona una lista de almacenes de datos que se admiten como orígenes y destinos por actividad de copia de hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn acerca de cómo almacenan datos toocopy de datos, haga clic en vínculo Hola Hola de almacén de datos en la tabla de Hola. 

