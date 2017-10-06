---
title: "Tutorial: Crear una canalización con la actividad de copia mediante Visual Studio | Microsoft Docs"
description: "En este tutorial, creará una canalización de Data Factory de Azure con una actividad de copia mediante Visual Studio."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a>Tutorial: Crear una canalización con la actividad de copia mediante Visual Studio
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

En este artículo, aprenderá cómo toouse Hola toocreate de Microsoft Visual Studio una factoría de datos con una canalización que copia datos de una base de datos de SQL Azure del tooan de almacenamiento blob de Azure. Si es nuevo tooAzure factoría de datos, lea hello [tooAzure Introducción factoría de datos](data-factory-introduction.md) artículo antes de realizar este tutorial.   

En este tutorial, creará una canalización con una actividad en ella: la actividad de copia. actividad de copia de Hello copia datos de un almacén de datos de datos admitidos almacén tooa receptor admitidos. Para obtener una lista de almacenes de datos que se admiten como orígenes y receptores, consulte los [almacenes de datos admitidos](data-factory-data-movement-activities.md#supported-data-stores-and-formats). actividad Hello funciona con un servicio disponible globalmente que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable. Para obtener más información acerca de la actividad de copia de hello, consulte [las actividades de movimiento de datos](data-factory-data-movement-activities.md).

pero cualquier canalización puede tener más de una actividad. Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad. Para más información, consulte [Varias actividades en una canalización](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE] 
> canalización de datos de Hello en este tutorial copia datos de un almacén de datos de destino de origen datos almacén tooa. Para obtener un tutorial sobre cómo tootransform los datos mediante Data Factory de Azure, consulte [Tutorial: generar una canalización de datos tootransform con clúster de Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Requisitos previos
1. Lea [Tutorial de introducción](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) hello completa y artículo **prerequisite** pasos.       
2. instancias de la factoría de datos de toocreate, debe ser miembro del programa Hola a [colaborador de la factoría de datos](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol en el nivel de grupo de recursos/suscripción Hola.
3. Debe tener instalado en el equipo siguiente de hello: 
   * Visual Studio 2013 o Visual Studio 2015.
   * Descargue el SDK de Azure para Visual Studio 2013 o Visual Studio 2015. Navegue demasiado[página de descargas de Azure](https://azure.microsoft.com/downloads/) y haga clic en **VS 2013** o **VS 2015** en hello **.NET** sección.
   * Descargue el complemento de Data Factory de Azure más reciente de Hola para Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) o [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). También puede actualizar Hola complemento mediante Hola pasos: en el menú de hello, haga clic en **herramientas** -> **extensiones y actualizaciones** -> **en línea**  ->  **Galería de visual Studio** -> **herramientas de generador de datos de Microsoft Azure para Visual Studio** -> **actualización**.

## <a name="steps"></a>Pasos
Estos son los pasos de hello que realizar como parte de este tutorial:

1. Crear **servicios vinculados** de factoría de datos de Hola. En este paso, se crean dos servicios vinculados del tipo Azure Storage y Azure SQL Database. 
    
    Hola AzureStorageLinkedService vincula su factoría de datos de toohello de cuenta de almacenamiento de Azure. Crea un contenedor y cargar la cuenta de almacenamiento de datos toothis como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService vincula su factoría de datos de toohello de base de datos de SQL Azure. datos de Hola que se copian desde el almacenamiento de blobs de Hola se almacenan en esta base de datos. Como parte de los [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md), se creó una tabla SQL en esta base de datos.     
2. Crear la entrada y salida **conjuntos de datos** de factoría de datos de Hola.  
    
    servicio de almacenamiento de Azure vinculado de Hello especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en tiempo de ejecución tooconnect tooyour cuenta de almacenamiento de Azure. Y el conjunto de datos de hello blob de entrada especifica el contenedor de Hola y la carpeta de Hola que contiene los datos de entrada de Hola.  

    De forma similar, Hola servicio de base de datos de Azure SQL vinculado especifica cadena de conexión de Hola que usa el servicio de factoría de datos en la base de datos de tiempo de ejecución tooconnect tooyour SQL Azure. Y conjunto de datos de tabla SQL de Hola salida especifica se copia la tabla de hello en bases de datos Hola Hola toowhich Hola del almacenamiento de blobs.
3. Crear un **canalización** de factoría de datos de Hola. En este paso, se crea una canalización con una actividad de copia.   
    
    actividad de copia de Hello copia datos de un blob en la tabla de tooa de almacenamiento de blobs de Azure de hello en la base de datos de SQL Azure Hola. Puede usar una actividad de copia en datos toocopy canalización desde cualquier origen compatibles tooany admitida el destino. Para ver una lista de los almacenes de datos admitidos, consulte el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
4. Cree una **factoría de datos** de Azure al implementar entidades de Data Factory (servicios vinculados, conjuntos de datos o tablas y canalizaciones). 

## <a name="create-visual-studio-project"></a>Creación de un proyecto de Visual Studio
1. Inicie **Visual Studio 2015**. Haga clic en **archivo**, seleccione demasiado**New**y haga clic en **proyecto**. Debería ver Hola **nuevo proyecto** cuadro de diálogo.  
2. Hola **nuevo proyecto** cuadro de diálogo, seleccione hello **DataFactory** plantilla y haga clic en **proyecto vacío de la factoría de datos**.  
   
    ![Cuadro de diálogo Nuevo proyecto](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. Especifique nombre Hola de proyecto de hello, la ubicación para la solución de Hola y el nombre de solución de hello y, a continuación, haga clic en **Aceptar**.
   
    ![Explorador de soluciones](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a>Crear servicios vinculados
Crear servicios vinculados en un toolink de factoría de datos almacenan sus datos y se factoría de datos de toohello de servicios de proceso. En este tutorial, no se usa ningún servicio de proceso, como Azure HDInsight o Azure Data Lake Analytics. Se usan dos almacenes de datos del tipo Azure Storage (origen) y Azure SQL Database (destino). 

Por lo tanto, se crean dos servicios vinculados del tipo AzureStorage y AzureSqlDatabase.  

Hola almacenamiento de Azure vinculados a los vínculos de servicio su factoría de datos de almacenamiento de Azure cuenta toohello. Esta cuenta de almacenamiento es hello uno en el que se creó un contenedor y cargar datos de hello como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

SQL Azure había vinculado a los vínculos de servicio su factoría de datos de toohello de base de datos de SQL Azure. datos de Hola que se copian desde el almacenamiento de blobs de Hola se almacenan en esta base de datos. Crear tabla emp de hello en esta base de datos como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Servicios vinculados vinculan almacenes de datos o generador de datos de Azure de tooan de servicios de proceso. Vea [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) de Hola a todos los orígenes y receptores admitidos por hello actividad de copia. Vea [servicios vinculados de proceso](data-factory-compute-linked-services.md) para lista de hello de servicios de proceso admitidos factoría de datos. En este tutorial no se usan servicios de proceso. 

### <a name="create-hello-azure-storage-linked-service"></a>Crear servicio vinculado de almacenamiento de Azure de Hola
1. En **el Explorador de soluciones**, haga clic en **servicios vinculados**, seleccione demasiado**agregar**y haga clic en **nuevo elemento**.      
2. Hola **Agregar nuevo elemento** cuadro de diálogo, seleccione **servicio vinculado de almacenamiento de Azure** en lista de Hola y haga clic en **agregar**. 
   
    ![Nuevo servicio vinculado](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. Reemplace `<accountname>` y `<accountkey>`* con nombre Hola de su cuenta de almacenamiento de Azure y su clave. 
   
    ![Servicio vinculado de Almacenamiento de Azure](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. Guardar hello **AzureStorageLinkedService1.json** archivo.

    Para obtener más información acerca de las propiedades JSON en definición de servicio vinculado de hello, consulte [conector del almacenamiento de blobs de Azure](data-factory-azure-blob-connector.md#linked-service-properties) artículo.

### <a name="create-hello-azure-sql-linked-service"></a>Crear servicio de SQL Azure vinculado Hola
1. Haga doble clic en **servicios vinculados** nodo Hola **el Explorador de soluciones** nuevo, seleccione demasiado**agregar**y haga clic en **nuevo elemento**. 
2. Esta vez, seleccione **Servicios vinculados de SQL Azure** y haga clic en **Agregar**. 
3. Hola **AzureSqlLinkedService1.json archivo**, reemplace `<servername>`, `<databasename>`, `<username@servername>`, y `<password>` con nombres de su servidor SQL Azure, la base de datos, la cuenta de usuario y la contraseña.    
4. Guardar hello **AzureSqlLinkedService1.json** archivo. 
    
    Para más información acerca de estas propiedades JSON, consulte [Conector de Azure SQL Database](data-factory-azure-sql-connector.md#linked-service-properties).


## <a name="create-datasets"></a>Creación de conjuntos de datos
En el paso anterior de hello, crear servicios vinculados toolink su cuenta de almacenamiento de Azure y la factoría de datos de tooyour de base de datos de SQL Azure. En este paso, definirá dos conjuntos de datos con el nombre InputDataset y OutputDataset que representan la entrada y los datos de salida que se almacenan en almacenes de datos de Hola que hace referencia AzureStorageLinkedService1 y AzureSqlLinkedService1 respectivamente.

servicio de almacenamiento de Azure vinculado de Hello especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en tiempo de ejecución tooconnect tooyour cuenta de almacenamiento de Azure. Y conjunto de datos de blob de entrada de hello (InputDataset) especifica contenedor de Hola y la carpeta de Hola que contiene los datos de entrada de Hola.  

De forma similar, Hola servicio de base de datos de Azure SQL vinculado especifica cadena de conexión de Hola que usa el servicio de factoría de datos en la base de datos de tiempo de ejecución tooconnect tooyour SQL Azure. Y conjunto de datos de tabla SQL (OututDataset) especifica la tabla de Hola Hola Hola de toowhich de base de datos se copian datos desde almacenamiento de blobs de Hola de salida de hello. 

### <a name="create-input-dataset"></a>Creación de un conjunto de datos de entrada
En este paso, creará un conjunto de datos denominado InputDataset que apunta a un archivo blob tooa (emp.txt) en la carpeta raíz de Hola de un contenedor de blobs (adftutorial) en hello representado por hello AzureStorageLinkedService1 vinculado servicio de almacenamiento de Azure. Si no especifica un valor para el nombre de archivo de hello (o puede omitirla), datos de todos los blobs en la carpeta de entrada de hello son destino toohello copiada. En este tutorial, especifique un valor para el nombre de archivo de Hola. 

A continuación, use el término de Hola "tablas" en lugar de "conjuntos de datos". Una tabla es un conjunto de datos rectangular y es Hola único tipo de conjunto de datos admitido ahora mismo. 

1. Haga clic en **tablas** en hello **el Explorador de soluciones**, seleccione demasiado**agregar**y haga clic en **nuevo elemento**.
2. Hola **Agregar nuevo elemento** cuadro de diálogo, seleccione **Azure Blob**y haga clic en **agregar**.   
3. Reemplazar texto JSON de hello con hello después de texto y guarde hello **AzureBlobLocation1.json** archivo. 

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
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
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

### <a name="create-output-dataset"></a>Creación del conjunto de datos de salida
En este paso se crea un conjunto de datos de salida denominado **OutputDataset**. Este conjunto de datos señala tooa table de SQL de base de datos de SQL Azure de hello representado por **AzureSqlLinkedService1**. 

1. Haga clic en **tablas** en hello **el Explorador de soluciones** nuevo, seleccione demasiado**agregar**y haga clic en **nuevo elemento**.
2. Hola **Agregar nuevo elemento** cuadro de diálogo, seleccione **SQL Azure**y haga clic en **agregar**. 
3. Reemplazar texto JSON de hello con hello después de JSON y guardar hello **AzureSqlTableLocation1.json** archivo.

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
       "linkedServiceName": "AzureSqlLinkedService1",
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

## <a name="create-pipeline"></a>Creación de una canalización
En este paso, creará una canalización con una **actividad de copia** que utiliza **InputDataset** como entrada y **OutputDataset** como salida.

Actualmente, el conjunto de datos de salida es qué unidades Hola programación. En este tutorial, el conjunto de datos de salida es tooproduce configurado un segmento una vez cada hora. canalización de Hello tiene una hora de inicio y la hora de finalización que son un día separado, lo que es de 24 horas. Por lo tanto, 24 segmentos del conjunto de datos de salida generados por la canalización de Hola. 

1. Haga clic en **canalizaciones** en hello **el Explorador de soluciones**, seleccione demasiado**agregar**y haga clic en **nuevo elemento**.  
2. Seleccione **canalización de datos de copia** en hello **Agregar nuevo elemento** cuadro de diálogo y haga clic en **agregar**. 
3. Reemplazar Hola JSON con hello después de JSON y guardar hello **CopyActivity1.json** archivo.

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
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - En la sección de actividades de hello, hay sólo una actividad cuyo **tipo** se establece demasiado**copia**. Para obtener más información acerca de la actividad de copia de hello, consulte [las actividades de movimiento de datos](data-factory-data-movement-activities.md). En las soluciones de Data Factory, también puede usar [actividades de transformación de datos](data-factory-data-transformation-activities.md).
    - Entrada de actividad hello se establece demasiado**InputDataset** y salida de actividad hello se establece demasiado**OutputDataset**. 
    - Hola **typeProperties** sección, **BlobSource** se especifica como tipo de origen de Hola y **SqlSink** se especifica como el tipo de receptor de Hola. Para obtener una lista completa de los almacenes de datos compatibles con la actividad de copia de hello como orígenes y receptores, vea [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn cómo almacenar toouse datos compatibles especificados como un origen/receptor, haga clic en el vínculo hello en la tabla de Hola.  
     
    Reemplazar el valor de Hola de hello **iniciar** propiedad con hello día actual y **final** valor con hello día siguiente. Puede especificar sólo parte de fecha de Hola y omitir la parte de hora de Hola de hello fecha y hora. Por ejemplo, "2016-02-03", que es equivalente demasiado "2016-02-03T00:00:00Z"
     
    Las fechas y horas de inicio y de finalización deben estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por ejemplo: 2016-10-14T16:32:41Z. Hola **final** tiempo es opcional, pero se usa en este tutorial. 
     
    Si no especifica el valor de hello **final** propiedad, se calcula como "**inicio + 48 horas**". canalización de hello toorun indefinidamente, especifique **9999-09-09** como valor de Hola de hello **final** propiedad.
     
    En el anterior ejemplo de Hola, hay 24 segmentos de datos tal y como se produce cada segmento de datos cada hora.

    Para obtener descripciones de las propiedades JSON en una definición de canalización, consulte cómo [crear canalizaciones](data-factory-create-pipelines.md). Para obtener descripciones de las propiedades JSON en una definición de actividad de copia, consulte las [actividades de movimiento de datos](data-factory-data-movement-activities.md). Para ver las descripciones de las propiedades JSON admitidas por BlobSource, consulte el artículo sobre el [conector de Azure Blob](data-factory-azure-blob-connector.md). Para ver las descripciones de las propiedades JSON admitidas por SqlSink, consulte el artículo sobre el [conector de Azure SQL Database](data-factory-azure-sql-connector.md).

## <a name="publishdeploy-data-factory-entities"></a>Publicación e implementación de las entidades de Data Factory
En este paso, se publican las entidades de Data Factory (servicios vinculados, conjuntos de datos y canalización) que se crearon anteriormente. También especificar nombre de Hola de hello toobe de factoría de datos nuevo creado toohold estas entidades.  

1. Haga clic en el proyecto en el Explorador de soluciones de Hola y haga clic en **publicar**. 
2. Si ve **iniciar sesión en la cuenta de Microsoft tooyour** cuadro de diálogo, escriba sus credenciales de cuenta de hello que tenga la suscripción de Azure y haga clic en **iniciar sesión en**.
3. Debería ver Hola después el cuadro de diálogo:
   
   ![Cuadro de diálogo Publicar](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. En la página de generador de datos de configuración de hello, Hola lo siguiente: 
   
   1. Seleccione la opción **Crear la nueva factoría de datos** .
   2. Escriba **VSTutorialFactory** para **Nombre**.  
      
      > [!IMPORTANT]
      > nombre de Hola Hola Azure factoría de datos debe ser único globalmente. Si recibe un error indicando nombre Hola de factoría de datos al publicar, cambiar nombre de Hola de factoría de datos de hello (por ejemplo, yournameVSTutorialFactory) e intente publicar de nuevo. Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.        
      > 
      > 
   3. Seleccione la suscripción de Azure para hello **suscripción** campo.
      
      > [!IMPORTANT]
      > Si no ve ninguna suscripción, asegúrese de que inició sesión mediante una cuenta que sea un administrador o Coadministrador de suscripción de Hola.  
      > 
      > 
   4. Seleccione hello **grupo de recursos** para toobe de factoría de datos de hello creado. 
   5. Seleccione hello **región** de factoría de datos de Hola. Solo las regiones compatibles con hello servicio factoría de datos se muestran en la lista desplegable de Hola.
   6. Haga clic en **siguiente** tooswitch toohello **publicar elementos** página.
      
       ![Configurar página de Data Factory](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. Hola **publicar elementos** página, asegúrese de que todas las factorías de datos de entidades están seleccionadas y haga clic en Hola **siguiente** tooswitch toohello **resumen** página.
   
   ![Página Publicar elementos](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. Revise el resumen de Hola y haga clic en **siguiente** Hola de proceso y la vista de la implementación del hello toostart **estado de implementación**.
   
   ![Página Publicar resumen](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. Hola **estado de implementación** página, debería ver estado de Hola Hola del proceso de implementación. Después de que se realice la implementación de hello, haga clic en Finalizar.
 
   ![Página Estado de la implementación](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

Tenga en cuenta Hola siguientes puntos: 

* Si recibe el error hello: "esta suscripción no está registrado toouse de espacio de nombres Microsoft.DataFactory", siga uno de los procedimientos de Hola e intente publicar de nuevo: 
  
  * En Azure PowerShell, ejecute hello después de proveedor del comando tooregister Hola factoría de datos. 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    Puede ejecutar Hola después comando tooconfirm ese Hola factoría de datos de proveedor está registrado. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Inicio de sesión mediante Hola suscripción de Azure en hello [portal de Azure](https://portal.azure.com) y navegar por hoja de la factoría de datos de tooa crear una factoría de datos en el portal de Azure hello (o). Esta acción registra automáticamente proveedor Hola para usted.
* nombre Hola Hola factoría de datos se puede registrarse como un nombre DNS en hello futuras y, por tanto, se convierten en visible públicamente.

> [!IMPORTANT]
> instancias de la factoría de datos de toocreate, deberá toobe un administrador o Coadministrador de hello suscripción de Azure

## <a name="monitor-pipeline"></a>Supervisión de la canalización
Desplácese toohello página de inicio de la factoría de datos:

1. Inicie sesión demasiado[portal de Azure](https://portal.azure.com).
2. Haga clic en **más servicios** en Hola menú izquierdo y haga clic en **factorías de datos**.

    ![Examinar factorías de datos](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. Comience a escribir el nombre de saludo de la factoría de datos.

    ![Nombre de la factoría de datos](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. Haga clic en la factoría de datos en la página Hola resultados lista toosee Hola principal de la factoría de datos.

    ![Página principal de Factoría de datos](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. Siga las instrucciones de [supervisar conjuntos de datos y canalización](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor canalización de Hola y conjuntos de datos ha creado en este tutorial. Actualmente, Visual Studio no permite supervisar canalizaciones de Data Factory. 

## <a name="summary"></a>Resumen
En este tutorial, ha creado un datos toocopy de factoría de datos de Azure desde una base de datos de SQL Azure de tooan de blobs de Azure. Ha utilizado la factoría de datos de Visual Studio toocreate hello, servicios vinculados, conjuntos de datos y una canalización. Estos son los pasos de alto nivel de hello realizadas en este tutorial:  

1. Ha creado una **factoría de datos**de Azure.
2. Ha creado **servicios vinculados**.
   1. Un **el almacenamiento de Azure** vinculado toolink de servicio de la cuenta de almacenamiento de Azure que contiene datos de entrada.     
   2. Un **SQL Azure** vinculado toolink de servicio en la base de datos de SQL Azure que contiene los datos de salida de hello. 
3. Ha creado **conjuntos de datos**que describen los datos de entrada y salida para las canalizaciones.
4. Ha creado una **canalización** con una **actividad de copia** con un origen **BlobSource** y un receptor **SqlSink**. 

toosee toouse una actividad de Hive de HDInsight tootransform de datos mediante el clúster de HDInsight de Azure, vea [ Tutorial: generar los datos primera canalización tootransform con clúster de Hadoop](data-factory-build-your-first-pipeline.md).

Se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad. Para más información, consulte [Programación y ejecución en Data Factory](data-factory-scheduling-and-execution.md). 

## <a name="view-all-data-factories-in-server-explorer"></a>Presentación de todas las factorías de datos en el explorador de servidores
Esta sección describe cómo toouse Hola Explorador de servidores en Visual Studio tooview todos los generadores de datos de hello en su suscripción de Azure y crear un proyecto de Visual Studio basado en un generador de datos existente. 

1. En **Visual Studio**, haga clic en **vista** en Hola menú y haga clic en **Explorador de servidores**.
2. En la ventana del explorador de servidores de hello, expanda **Azure** y expanda **factoría de datos**. Si ve **iniciar sesión en tooVisual Studio**, escriba Hola **cuenta** asociada a su suscripción de Azure y haga clic en **continuar**. Escriba la **contraseña** y haga clic en **Iniciar sesión**. Visual Studio intenta tooget información acerca de todos los generadores de datos de Azure en su suscripción. Vea Estado Hola de esta operación en hello **lista de tareas del generador de datos** ventana.

    ![Explorador de servidores](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a>Creación de un proyecto de Visual Studio para una factoría de datos existente

- Haga clic en una factoría de datos en el Explorador de servidores y seleccione **exportar factoría de datos tooNew proyecto** toocreate un proyecto de Visual Studio basado en un generador de datos existente.

    ![Exportar el proyecto de VS de tooa de generador de datos](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

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


## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha usado Azure Blob Storage como almacén de datos de origen y una base de datos SQL de Azure como almacén de datos de destino en una operación de copia. Hello tabla siguiente proporciona una lista de almacenes de datos que se admiten como orígenes y destinos por actividad de copia de hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn acerca de cómo almacenan datos toocopy de datos, haga clic en vínculo Hola Hola de almacén de datos en la tabla de Hola.
