---
title: "Tutorial: Crear una factoría de datos de Azure canalización toocopy de datos (portal de Azure) | Documentos de Microsoft"
description: "En este tutorial, utilizará toocreate portal Azure una canalización del generador de datos de Azure con datos toocopy de actividad de copia de una base de datos de SQL Azure del tooan de almacenamiento blob de Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d9317652-0170-4fd3-b9b2-37711272162b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fadd840fe9a15cd8831cdb25dccbd10ac42fa161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-portal-toocreate-a-data-factory-pipeline-toocopy-data"></a>Tutorial: Usar toocreate portal Azure una toocopy de datos de canalización de factoría de datos 
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

En este artículo, aprenderá cómo toouse [portal de Azure](https://portal.azure.com) toocreate una factoría de datos con una canalización que copia datos de una base de datos de SQL Azure del tooan de almacenamiento blob de Azure. Si es nuevo tooAzure factoría de datos, lea hello [tooAzure Introducción factoría de datos](data-factory-introduction.md) artículo antes de realizar este tutorial.   

En este tutorial, creará una canalización con una actividad en ella: la actividad de copia. actividad de copia de Hello copia datos de un almacén de datos de datos admitidos almacén tooa receptor admitidos. Para obtener una lista de almacenes de datos que se admiten como orígenes y receptores, consulte los [almacenes de datos admitidos](data-factory-data-movement-activities.md#supported-data-stores-and-formats). actividad Hello funciona con un servicio disponible globalmente que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable. Para obtener más información acerca de la actividad de copia de hello, consulte [las actividades de movimiento de datos](data-factory-data-movement-activities.md).

pero cualquier canalización puede tener más de una actividad. Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad. Para más información, consulte [Varias actividades en una canalización](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> canalización de datos de Hello en este tutorial copia datos de un almacén de datos de destino de origen datos almacén tooa. Para obtener un tutorial sobre cómo tootransform los datos mediante Data Factory de Azure, consulte [Tutorial: generar una canalización de datos tootransform con clúster de Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Requisitos previos
Complete los requisitos previos descritos en hello [requisitos previos tutoriales](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artículo antes de realizar este tutorial.

## <a name="steps"></a>Pasos
Estos son los pasos de hello que realizar como parte de este tutorial:

1. Cree una **factoría de datos** de Azure. En este paso, creará una factoría de datos llamada ADFTutorialDataFactory. 
2. Crear **servicios vinculados** de factoría de datos de Hola. En este paso, se crean dos servicios vinculados del tipo Azure Storage y Azure SQL Database. 
    
    Hola AzureStorageLinkedService vincula su factoría de datos de toohello de cuenta de almacenamiento de Azure. Crea un contenedor y cargar la cuenta de almacenamiento de datos toothis como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService vincula su factoría de datos de toohello de base de datos de SQL Azure. datos de Hola que se copian desde el almacenamiento de blobs de Hola se almacenan en esta base de datos. Como parte de los [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md), se creó una tabla SQL en esta base de datos.   
3. Crear la entrada y salida **conjuntos de datos** de factoría de datos de Hola.  
    
    servicio de almacenamiento de Azure vinculado de Hello especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en tiempo de ejecución tooconnect tooyour cuenta de almacenamiento de Azure. Y el conjunto de datos de hello blob de entrada especifica el contenedor de Hola y la carpeta de Hola que contiene los datos de entrada de Hola.  

    De forma similar, Hola servicio de base de datos de Azure SQL vinculado especifica cadena de conexión de Hola que usa el servicio de factoría de datos en la base de datos de tiempo de ejecución tooconnect tooyour SQL Azure. Y conjunto de datos de tabla SQL de Hola salida especifica se copia la tabla de hello en bases de datos Hola Hola toowhich Hola del almacenamiento de blobs.
4. Crear un **canalización** de factoría de datos de Hola. En este paso, se crea una canalización con una actividad de copia.   
    
    actividad de copia de Hello copia datos de un blob en la tabla de tooa de almacenamiento de blobs de Azure de hello en la base de datos de SQL Azure Hola. Puede usar una actividad de copia en datos toocopy canalización desde cualquier origen compatibles tooany admitida el destino. Para ver una lista de los almacenes de datos admitidos, consulte el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
5. Canalización de Hola de monitor. En este paso, se **monitor** Hola sectores de conjuntos de datos de entrada y salida mediante el portal de Azure. 

## <a name="create-data-factory"></a>Creación de Data Factory
> [!IMPORTANT]
> Completa [requisitos previos para el tutorial de hello](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) si aún no lo ha hecho.   

Una factoría de datos puede tener una o más canalizaciones. Una canalización puede tener una o más actividades. Por ejemplo, una toocopy de datos de actividad de copia de un almacén de datos de origen tooa destino y un toorun de actividad de Hive de HDInsight un tootransform de script de Hive datos de salida de tooproduct de datos de entrada. Puede empezar con la creación de factoría de datos de hello en este paso.

1. Después de iniciar sesión toohello [portal de Azure](https://portal.azure.com/), haga clic en **New** en el menú de la izquierda hello, haga clic en **datos + análisis**y haga clic en **factoría de datos**. 
   
   ![New->DataFactory](./media/data-factory-copy-activity-tutorial-using-azure-portal/NewDataFactoryMenu.png)    
2. Hola **factoría de datos** hoja:
   
   1. Escriba **ADFTutorialDataFactory** para hello **nombre**. 
      
         ![Hoja Nueva Factoría de datos](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-new-data-factory.png)
      
       nombre de Hola Hola Azure factoría de datos debe ser **único global**. Si recibes Hola tras error, cambie el nombre de Hola de factoría de datos de hello (por ejemplo, yournameADFTutorialDataFactory) e intente crear de nuevo. Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.
      
           Data factory name “ADFTutorialDataFactory” is not available  
      
       ![Nombre de Factoría de datos no disponible](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-not-available.png)
   2. Seleccione su Azure **suscripción** en el que desea factoría de datos de toocreate Hola. 
   3. Para hello **grupo de recursos**, realice una de hello pasos:
      
      - Seleccione **utilizar existente**y seleccione un grupo de recursos existente en la lista desplegable de Hola. 
      - Seleccione **crear nuevo**y escriba el nombre de Hola de un grupo de recursos.   
         
          Algunos de los pasos de hello en este tutorial se supone que usa el nombre de Hola: **ADFTutorialResourceGroup** Hola para grupo de recursos. toolearn acerca de los grupos de recursos, consulte [utilizando recurso agrupa los recursos de Azure de toomanage](../azure-resource-manager/resource-group-overview.md).  
   4. Seleccione hello **ubicación** de factoría de datos de Hola. Solo las regiones compatibles con hello servicio factoría de datos se muestran en la lista desplegable de Hola.
   5. Seleccione **toodashboard Pin**.     
   6. Haga clic en **Crear**.
      
      > [!IMPORTANT]
      > instancias de la factoría de datos de toocreate, debe ser miembro del programa Hola a [colaborador de la factoría de datos](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol en el nivel de grupo de recursos/suscripción Hola.
      > 
      > nombre Hola Hola factoría de datos se puede registrarse como un nombre DNS en hello futuras y, por tanto, se convierten en visible públicamente.                
      > 
      > 
3. En el panel de hello, ve Hola siguiente icono con el estado: **factoría de datos de implementación**. 

    ![icono implementando factoría de datos](media/data-factory-copy-activity-tutorial-using-azure-portal/deploying-data-factory.png)
4. Una vez completada la creación de hello, vea hello **factoría de datos** hoja como se muestra en la imagen de Hola.
   
   ![Página principal de Factoría de datos](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-home-page.png)

## <a name="create-linked-services"></a>Crear servicios vinculados
Crear servicios vinculados en un toolink de factoría de datos almacenan sus datos y se factoría de datos de toohello de servicios de proceso. En este tutorial, no se usa ningún servicio de proceso, como Azure HDInsight o Azure Data Lake Analytics. Se usan dos almacenes de datos del tipo Azure Storage (origen) y Azure SQL Database (destino). 

Por lo tanto, se crean dos servicios vinculados llamados AzureStorageLinkedService y AzureSqlLinkedService del tipo AzureStorage y AzureSqlDatabase.  

Hola AzureStorageLinkedService vincula su factoría de datos de toohello de cuenta de almacenamiento de Azure. Esta cuenta de almacenamiento es hello uno en el que se creó un contenedor y cargar datos de hello como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService vincula su factoría de datos de toohello de base de datos de SQL Azure. datos de Hola que se copian desde el almacenamiento de blobs de Hola se almacenan en esta base de datos. Crear tabla emp de hello en esta base de datos como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).  

### <a name="create-azure-storage-linked-service"></a>Creación de un servicio vinculado de Almacenamiento de Azure
En este paso, vincule la factoría de datos de tooyour de cuenta de almacenamiento de Azure. Especificar nombre de Hola y clave de la cuenta de almacenamiento de Azure en esta sección.  

1. Hola **factoría de datos** hoja, haga clic en **autor e implementar** icono.
   
   ![Mosaico Crear e implementar](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-author-deploy-tile.png) 
2. Vea hello **Editor de generador de datos** como se muestra en hello después de imagen: 

    ![Editor de la Factoría de datos](./media/data-factory-copy-activity-tutorial-using-azure-portal/data-factory-editor.png)
3. En el editor de hello, haga clic en **nuevo almacén de datos** los botones de barra de herramientas de Hola y seleccione **almacenamiento de Azure** desde el menú desplegable de Hola. Debería ver la plantilla JSON de hello para la creación de un servicio de almacenamiento de Azure vinculado en el panel derecho de Hola. 
   
    ![Botón Nuevo almacén de datos del Editor](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-newdatastore-button.png)    
3. Reemplace `<accountname>` y `<accountkey>` con hello cuenta nombre y la cuenta de valores de clave para la cuenta de almacenamiento de Azure. 
   
    ![JSON de almacenamiento de blobs del Editor](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-json.png)    
4. Haga clic en **implementar** en la barra de herramientas de Hola. Debería ver Hola implementado **AzureStorageLinkedService** en el árbol de hello ver ahora. 
   
    ![Implementar almacenamiento de blobs del editor](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-deploy.png)

    Para obtener más información acerca de las propiedades JSON en definición de servicio vinculado de hello, consulte [conector del almacenamiento de blobs de Azure](data-factory-azure-blob-connector.md#linked-service-properties) artículo.

### <a name="create-a-linked-service-for-hello-azure-sql-database"></a>Crear un servicio vinculado de hello base de datos de SQL Azure
En este paso, vincule la factoría de datos de tooyour de base de datos de SQL Azure. Especifique el nombre del servidor SQL Azure hello, nombre de base de datos, nombre de usuario y contraseña de usuario en esta sección. 

1. Hola **Editor de generador de datos**, haga clic en **nuevo almacén de datos** los botones de barra de herramientas de Hola y seleccione **base de datos de SQL Azure** desde el menú desplegable de Hola. Debería ver la plantilla JSON de Hola para crear el servicio de SQL Azure vinculado de hello en el panel derecho de Hola.
2. Reemplace `<servername>`, `<databasename>`, `<username>@<servername>` y `<password>` por los nombres del servidor, la base de datos, la cuenta de usuario y la contraseña de SQL Azure. 
3. Haga clic en **implementar** en Hola toocreate de barra de herramientas e implementar hello **AzureSqlLinkedService**.
4. Confirme que ve **AzureSqlLinkedService** en vista de árbol de hello en **servicios vinculados**.  

    Para más información acerca de estas propiedades JSON, consulte [Conector de Azure SQL Database](data-factory-azure-sql-connector.md#linked-service-properties).

## <a name="create-datasets"></a>Creación de conjuntos de datos
En el paso anterior de hello, crear servicios vinculados toolink su cuenta de almacenamiento de Azure y la factoría de datos de tooyour de base de datos de SQL Azure. En este paso, definirá dos conjuntos de datos con el nombre InputDataset y OutputDataset que representan la entrada y los datos de salida que se almacenan en almacenes de datos de Hola que hace referencia AzureStorageLinkedService y AzureSqlLinkedService respectivamente.

servicio de almacenamiento de Azure vinculado de Hello especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en tiempo de ejecución tooconnect tooyour cuenta de almacenamiento de Azure. Y conjunto de datos de blob de entrada de hello (InputDataset) especifica contenedor de Hola y la carpeta de Hola que contiene los datos de entrada de Hola.  

De forma similar, Hola servicio de base de datos de Azure SQL vinculado especifica cadena de conexión de Hola que usa el servicio de factoría de datos en la base de datos de tiempo de ejecución tooconnect tooyour SQL Azure. Y conjunto de datos de tabla SQL (OututDataset) especifica la tabla de Hola Hola Hola de toowhich de base de datos se copian datos desde almacenamiento de blobs de Hola de salida de hello. 

### <a name="create-input-dataset"></a>Creación de un conjunto de datos de entrada
En este paso, creará un conjunto de datos denominado InputDataset que apunta a un archivo blob tooa (emp.txt) en la carpeta raíz de Hola de un contenedor de blobs (adftutorial) en hello representado por hello AzureStorageLinkedService vinculado servicio de almacenamiento de Azure. Si no especifica un valor para el nombre de archivo de hello (o puede omitirla), datos de todos los blobs en la carpeta de entrada de hello son destino toohello copiada. En este tutorial, especifique un valor para el nombre de archivo de Hola. 

1. Hola **Editor** para hello factoría de datos, haga clic en **... Más**, haga clic en **nuevo conjunto de datos**y haga clic en **almacenamiento de blobs de Azure** desde el menú desplegable de Hola. 
   
    ![Menú Conjunto de datos nuevo](./media/data-factory-copy-activity-tutorial-using-azure-portal/new-dataset-menu.png)
2. Reemplace JSON en el panel derecho de hello con hello siguiente fragmento de JSON: 
   
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
3. Haga clic en **implementar** en Hola toocreate de barra de herramientas e implementar hello **InputDataset** conjunto de datos. Confirme que aparece hello **InputDataset** en la vista de árbol de Hola.

### <a name="create-output-dataset"></a>Creación del conjunto de datos de salida
Hola servicio de base de datos de Azure SQL vinculado especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en la base de datos de tiempo de ejecución tooconnect tooyour SQL Azure. Hola salida SQL tabla conjunto de datos (OututDataset) se crea en este paso especifica se copia la tabla de hello en bases de datos Hola Hola toowhich Hola del almacenamiento de blobs.

1. Hola **Editor** para hello factoría de datos, haga clic en **... Más**, haga clic en **nuevo conjunto de datos**y haga clic en **SQL Azure** desde el menú desplegable de Hola. 
2. Reemplace JSON en el panel derecho de hello con hello siguiente fragmento de JSON:

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
3. Haga clic en **implementar** en Hola toocreate de barra de herramientas e implementar hello **OutputDataset** conjunto de datos. Confirme que aparece hello **OutputDataset** en vista de árbol de hello en **conjuntos de datos**. 

## <a name="create-pipeline"></a>Creación de una canalización
En este paso, creará una canalización con una **actividad de copia** que utiliza **InputDataset** como entrada y **OutputDataset** como salida.

Actualmente, el conjunto de datos de salida es qué unidades Hola programación. En este tutorial, el conjunto de datos de salida es tooproduce configurado un segmento una vez cada hora. canalización de Hello tiene una hora de inicio y la hora de finalización que son un día separado, lo que es de 24 horas. Por lo tanto, 24 segmentos del conjunto de datos de salida generados por la canalización de Hola. 

1. Hola **Editor** para hello factoría de datos, haga clic en **... Más** y, luego, en **Nueva canalización**. Como alternativa, puede hacer clic **canalizaciones** en la vista de árbol de Hola y haga clic en **nueva canalización**.
2. Reemplace JSON en el panel derecho de hello con hello siguiente fragmento de JSON: 

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
    - Las fechas y horas de inicio y de finalización deben estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por ejemplo: 2016-10-14T16:32:41Z. Hola **final** tiempo es opcional, pero se usa en este tutorial. Si no especifica el valor de hello **final** propiedad, se calcula como "**inicio + 48 horas**". canalización de hello toorun indefinidamente, especifique **9999-09-09** como valor de Hola de hello **final** propiedad.
     
    En el anterior ejemplo de Hola, hay 24 segmentos de datos tal y como se produce cada segmento de datos cada hora.

    Para obtener descripciones de las propiedades JSON en una definición de canalización, consulte cómo [crear canalizaciones](data-factory-create-pipelines.md). Para obtener descripciones de las propiedades JSON en una definición de actividad de copia, consulte las [actividades de movimiento de datos](data-factory-data-movement-activities.md). Para ver las descripciones de las propiedades JSON admitidas por BlobSource, consulte el artículo sobre el [conector de Azure Blob](data-factory-azure-blob-connector.md). Para ver las descripciones de las propiedades JSON admitidas por SqlSink, consulte el artículo sobre el [conector de Azure SQL Database](data-factory-azure-sql-connector.md).
3. Haga clic en **implementar** en Hola toocreate de barra de herramientas e implementar hello **ADFTutorialPipeline**. Confirme que ve canalización hello en la vista de árbol de Hola. 
4. Ahora, cierre hello **Editor** hoja haciendo clic en **X**. Haga clic en **X** nuevo toosee hello **factoría de datos** página principal de hello **ADFTutorialDataFactory**.

**¡Enhorabuena!** Ha creado correctamente una factoría de datos de Azure con datos toocopy canalización desde una base de datos de SQL Azure del tooan de almacenamiento blob de Azure. 


## <a name="monitor-pipeline"></a>Supervisión de la canalización
En este paso, utilizará hello toomonitor portal Azure que está sucediendo en una factoría de datos de Azure.    

### <a name="monitor-pipeline-using-monitor--manage-app"></a>Supervisión de una canalización con la Aplicación de supervisión y administración
Hello pasos siguientes muestran cómo toomonitor canalizaciones de la factoría de datos mediante el uso de la aplicación hello de supervisar y administrar: 

1. Haga clic en **Monitor & administrar** de mosaico en la página principal de saludo de la factoría de datos.
   
    ![Icono Supervisión y administración](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-manage-tile.png) 
2. Verá la opción **Aplicación de supervisión y administración** en una pestaña aparte. 

    > [!NOTE]
    > Si ve ese explorador web de hello está atascado en "Autorizar …", siga uno de los procedimientos de hello: Hola desactive **bloquear las cookies de terceros y datos de sitio** casilla de verificación (o) crear una excepción para **login.microsoftonline.com**y, a continuación, vuelva a intentarlo tooopen Hola aplicación.

    ![Aplicación de supervisión y administración](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-and-manage-app.png)
3. Hola de cambio **hora de inicio** y **hora de finalización** tooinclude (2017-05-11) de inicio y finalización (2017-05-12) de la canalización y haga clic en **aplicar**.     
3. Vea hello **ventanas de la actividad** asociados con cada hora entre el inicio de la canalización y finalización veces en la lista de hello en el panel central de Hola. 
4. ventana de actividad en Hola Hola a toosee detalles acerca de una ventana de actividad, seleccione **Windows actividad** lista. 
    ![Detalles de ventana de actividad](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)

    En el Explorador de ventana de actividad en hello derecha, verá que Hola se segmentan en hora UTC actual de toohello (8:12 PM) se procesan (en color verde). no se procesan aún sectores de Hello 8-9 P.M., 9 y 10 p. M., 10-11 P.M., 23: 00 - 12 AM.

    Hola **intentos** sección derecha panel proporciona información acerca de la actividad de hello ejecutar para el segmento de datos Hola Hola. Si se produjo un error, proporciona detalles sobre el error de Hola. Por ejemplo, si Hola de entrada de carpeta o un contenedor no existe y Hola segmento procesamiento se produce un error, verá un mensaje de error que indica que el contenedor de Hola o carpeta no existe.

    ![Intentos de ejecución de la actividad](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-run-attempts.png) 
4. Iniciar **SQL Server Management Studio**, conectar toohello base de datos de SQL Azure y compruebe que se insertan filas de hello en toohello **emp** tabla de base de datos de Hola.
    
    ![resultados de la consulta SQL](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)

Para más información acerca del uso de esta aplicación, consulte [Supervisión y administración de canalizaciones de Azure Data Factory mediante la nueva Aplicación de supervisión y administración](data-factory-monitor-manage-app.md).

### <a name="monitor-pipeline-using-diagram-view"></a>Supervisión de una canalización desde la vista de diagrama
También puede monitor canalizaciones de datos mediante la vista de diagrama de Hola.  

1. Hola **factoría de datos** hoja, haga clic en **diagrama**.
   
    ![Módulo de la factoría de datos: ventana de diagrama](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactoryblade-diagramtile.png)
2. Debería ver Hola diagrama similar toohello después de imagen: 
   
    ![Vista de diagrama](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-diagram-blade.png)  
5. En la vista de diagrama de hello, haga doble clic en **InputDataset** toosee intervalos para el conjunto de datos de Hola.  
   
    ![Conjuntos de datos con InputDataset seleccionado](./media/data-factory-copy-activity-tutorial-using-azure-portal/DataSetsWithInputDatasetFromBlobSelected.png)   
5. Haga clic en **ver más** vincular toosee todos los segmentos de datos de Hola. Verá 24 segmentos de una hora entre las horas de inicio y finalización de la canalización. 
   
    ![Todos los segmentos de datos de entrada](./media/data-factory-copy-activity-tutorial-using-azure-portal/all-input-slices.png)  
   
    Observe que Hola a todos los segmentos de datos de la hora UTC actual de toohello **listo** porque hello **emp.txt** archivo existe todo el tiempo de hello en el contenedor de blob de hello: **adftutorial\input**. segmentos de Hello en ocasiones futuras Hola aún no están en estado listo. Confirme que no hay ningún segmento se mostrarán en hello **recientemente no se pudo sectores** sección final Hola.
6. Hojas de hello cerrar hasta que vea Hola diagrama de vista (o) desplazamiento izquierdo toosee Hola ver. A continuación, haga doble clic en **OutputDataset**. 
8. Haga clic en **ver más** vínculo en hello **tabla** hoja para **OutputDataset** toosee Hola a todos los sectores.

    ![hoja de segmentos de datos](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslices-blade.png) 
9. Observe que todos los intervalos de tiempo UTC actual de toohello Hola mover de **pendientes de ejecución** estado = > **en curso** ==> **listo** estado. Hola sectores de hello anterior (antes de la hora actual) se procesan de toooldest más reciente de forma predeterminada. Por ejemplo, si Hola hora actual es 8:12 PM UTC, Hola para 7 PM - 8 P.M. se procesa antes de segmento de hello 6 P.M. - 7 PM. Hola PM 8-9 P.M. se procesa al final de Hola Hola de intervalo de tiempo de forma predeterminada, que es después de 9 P.M..  
10. Haga clic en cualquier segmento de datos de lista de Hola y debería ver Hola **el segmento de datos** hoja. Los elementos de datos asociados a una ventana de actividad se llaman segmentos. Un segmento puede ser uno o varios archivos.  
    
     ![hoja de segmento de datos](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslice-blade.png)
    
     Si el segmento de hello no está en hello **listo** estado, puede ver segmentos ascendentes de Hola que no están listos y están bloqueando el intervalo actual de Hola de ejecutarse en hello **segmentos ascendentes que no están listos** lista.
11. Hola **el segmento de datos** hoja, debería ver toda la actividad se ejecuta en la lista de hello en parte inferior de Hola. Haga clic en un **actividad ejecutar** toosee hello **detalles de ejecución de la actividad** hoja. 
    
    ![Detalles de ejecución de actividad](./media/data-factory-copy-activity-tutorial-using-azure-portal/ActivityRunDetails.png)

    En esta hoja, verá cómo tardó en la operación de copia de hello largo, el rendimiento es, el número de bytes de datos eran de lectura y la hora de inicio escrito, ejecución, tiempo de ejecución final etcetera.  
12. Haga clic en **X** tooclose todos los módulos de hello hasta que reciba toohello hoja principal para hello **ADFTutorialDataFactory**.
13. (opcional) haga clic en hello **conjuntos de datos** icono o **canalizaciones** hojas de hello tooget de mosaico, ha visto Hola pasos anteriores. 
14. Iniciar **SQL Server Management Studio**, conectar toohello base de datos de SQL Azure y compruebe que se insertan filas de hello en toohello **emp** tabla de base de datos de Hola.
    
    ![resultados de la consulta SQL](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)


## <a name="summary"></a>Resumen
En este tutorial, ha creado un datos toocopy de factoría de datos de Azure desde una base de datos de SQL Azure de tooan de blobs de Azure. Ha utilizado la factoría de datos de Hola Hola toocreate de portal de Azure, servicios vinculados, conjuntos de datos y una canalización. Estos son los pasos de alto nivel de hello realizadas en este tutorial:  

1. Ha creado una **factoría de datos**de Azure.
2. Ha creado **servicios vinculados**.
   1. Un **el almacenamiento de Azure** vinculado toolink de servicio de la cuenta de almacenamiento de Azure que contiene datos de entrada.     
   2. Un **SQL Azure** vinculado toolink de servicio en la base de datos de SQL Azure que contiene los datos de salida de hello. 
3. Ha creado **conjuntos de datos** que describen los datos de entrada y salida de las canalizaciones.
4. Ha creado una **canalización** con una **actividad de copia** con un origen **BlobSource** y un receptor **SqlSink**.  

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha usado Azure Blob Storage como almacén de datos de origen y una base de datos SQL de Azure como almacén de datos de destino en una operación de copia. Hello tabla siguiente proporciona una lista de almacenes de datos que se admiten como orígenes y destinos por actividad de copia de hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn acerca de cómo almacenan datos toocopy de datos, haga clic en vínculo Hola Hola de almacén de datos en la tabla de Hola.
