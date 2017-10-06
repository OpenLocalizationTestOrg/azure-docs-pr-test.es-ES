---
title: aaaSQL actividad de procedimiento almacenado de servidor
description: "Obtenga información acerca de cómo puede usar la actividad de procedimiento almacenado de SQL Server de hello tooinvoke un procedimiento almacenado en una base de datos de SQL Azure o el almacenamiento de datos de SQL Azure desde una canalización del generador de datos."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a>Actividad de procedimiento almacenado de SQL Server
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

## <a name="overview"></a>Información general
Usar las actividades de transformación de datos en una factoría de datos [canalización](data-factory-create-pipelines.md) tootransform y procesar datos sin formato en las predicciones y visión. Hello actividad de procedimiento almacenado es una de las actividades de transformación de Hola que admite factoría de datos. En este artículo se basa en hello [las actividades de transformación de datos](data-factory-data-transformation-activities.md) artículo, que presenta una descripción general de transformación de datos y las actividades de transformación de hello compatible de factoría de datos.

Puede utilizar tooinvoke de actividad de procedimiento almacenado Hola un procedimiento almacenado en uno de hello después de datos se almacena en su empresa o en una máquina virtual (VM) de Azure: 

- Azure SQL Database
- Almacenamiento de datos SQL de Azure
- Base de datos de SQL Server.  Si está utilizando SQL Server, instale Data Management Gateway en el mismo equipo que hospeda Hola base de datos o en un equipo independiente que tiene la base de datos de access toohello de Hola. La puerta de enlace de administración de datos es un componente que conecta orígenes de datos locales o en la máquina virtual de Azure con servicios en la nube de forma segura y administrada. Consulte el artículo [Data Management Gateway](data-factory-data-management-gateway.md) para obtener detalles.

> [!IMPORTANT]
> Cuando se copian datos en la base de datos de SQL Azure o SQL Server, puede configurar hello **SqlSink** en tooinvoke de actividad de copia un procedimiento almacenado mediante el uso de hello **sqlWriterStoredProcedureName** propiedad. Para más información, consulte [Invocación del procedimiento almacenado desde la actividad de copia en Azure Data Factory](data-factory-invoke-stored-procedure-from-copy-activity.md). Para obtener más información acerca de la propiedad de hello, consulte los siguientes artículos de conector: [base de datos de SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties). No se admite la invocación de un procedimiento almacenado al copiar datos en Azure SQL Data Warehouse mediante una actividad de copia. Sin embargo, puede utilizar tooinvoke de actividad de procedimiento almacenado de hello un procedimiento almacenado en el almacén de datos de SQL. 
>  
> Cuando se copian datos de base de datos de SQL Azure o SQL Server o almacenamiento de datos de SQL Azure, puede configurar **SqlSource** en tooinvoke de actividad de copia una tooread de datos de procedimiento almacenado de base de datos de origen de hello mediante hello  **sqlReaderStoredProcedureName** propiedad. Para obtener más información, vea Hola siguientes artículos de conector: [base de datos de SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [almacenamiento de datos de SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          


Hola siguiendo el tutorial utiliza Hola actividad de procedimiento almacenado en un tooinvoke de canalización un procedimiento almacenado en una base de datos de SQL Azure. 

## <a name="walkthrough"></a>Tutorial
### <a name="sample-table-and-stored-procedure"></a>Procedimiento almacenado y tabla de ejemplo
1. Cree Hola siguiente **tabla** en la base de datos de SQL Azure con SQL Server Management Studio o cualquier otra herramienta que está familiarizado con. columna de datetimestamp Hello es Hola fecha y hora en que cuando se genera el identificador correspondiente Hola.

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    Id. es Hola único identificado y column de datetimestamp de Hola Hola fecha y hora en que cuando se genera el identificador correspondiente Hola.
    
    ![Datos de ejemplo](./media/data-factory-stored-proc-activity/sample-data.png)

    En este ejemplo, procedimiento almacenado de hello está en una base de datos de SQL Azure. Si hello procedimiento almacenado está en un almacén de datos de SQL Azure y base de datos de SQL Server, el enfoque de hello es similar. Para una base de datos de SQL Server, debe instalar una [Puerta de enlace de administración de datos](data-factory-data-management-gateway.md).
2. Cree Hola siguiente **procedimiento almacenado** que inserta datos en toohello **tabla de muestra**.

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > **Nombre** y **mayúsculas y minúsculas** de hello parámetro (fecha y hora en este ejemplo) debe coincidir con el de los parámetros especificados en hello canalización/JSON de la actividad. En la consulta Hola definición del procedimiento almacenado, asegúrese de que  **@**  se utiliza como un prefijo de parámetro hello.

### <a name="create-a-data-factory"></a>Crear una factoría de datos
1. Inicie sesión demasiado[portal de Azure](https://portal.azure.com/).
2. Haga clic en **NEW** en el menú de la izquierda hello, haga clic en **Intelligence + análisis**y haga clic en **factoría de datos**.

    ![Nueva factoría de datos](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. Hola **factoría de datos** hoja, escriba **SProcDF** para hello nombre. Los nombres de Azure Data Factory son **únicos globalmente**. Necesita tooprefix Hola nombre hello factoría de datos con el nombre, la creación correcta de hello tooenable de fábrica de Hola.

   ![Nueva factoría de datos](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. Seleccione la **suscripción de Azure**.
5. Para **grupo de recursos**, realice una de hello pasos:
   1. Haga clic en **crear nuevo** y escriba un nombre para el grupo de recursos de Hola.
   2. Haga clic en **Usar existente** y seleccione un grupo de recursos existente.  
6. Seleccione hello **ubicación** de factoría de datos de Hola.
7. Seleccione **toodashboard Pin** para que puedan ver factoría de datos de hello en el panel de hello próxima vez que inicie sesión.
8. Haga clic en **crear** en hello **factoría de datos** hoja.
9. Vea factoría de datos de Hola se creen en hello **panel** de hello portal de Azure. Una vez creado correctamente la factoría de datos de hello, consulte página de factoría de datos de hello, que muestra Hola contenido Hola factoría de datos.

   ![Página principal de Data Factory](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a>Crear un servicio vinculado SQL de Azure.
Después de crear la factoría de datos de hello, se crea un servicio de SQL Azure vinculado que se vincula la base de datos de SQL Azure, que contiene la tabla de la tabla de muestra de Hola y procedimiento almacenado de sp_sample, tooyour factoría de datos.

1. Haga clic en **autor e implementar** en hello **factoría de datos** hoja para **SProcDF** toolaunch Hola Editor de generador de datos.
2. Haga clic en **nuevo almacén de datos** en Hola barra de comandos y elija **base de datos de SQL Azure**. Debería ver Hola script JSON para crear una SQL Azure vinculado servicio en el editor de Hola.

   ![Nuevo almacén de datos](media/data-factory-stored-proc-activity/new-data-store.png)
3. Hola script JSON, asegúrese de hello siguientes cambios:

   1. Reemplace `<servername>` con el nombre de Hola de su servidor de base de datos de SQL Azure.
   2. Reemplace `<databasename>` con base de datos de hello en el que creó hello y tabla de Hola de procedimiento almacenado.
   3. Reemplace `<username@servername>` con cuenta de usuario de Hola que tiene la base de datos de access toohello.
   4. Reemplace `<password>` con contraseña hello para la cuenta de usuario de Hola.

      ![Nuevo almacén de datos](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. toodeploy Hola servicio vinculado, haga clic en **implementar** en la barra de comandos de Hola. Confirme que aparece hello AzureSqlLinkedService en el árbol de hello ver Hola izquierda.

    ![vista de árbol con servicios vinculados](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a>Crear un conjunto de datos de salida
Debe especificar que un conjunto de datos de salida para una actividad de procedimiento almacenado incluso si el procedimiento almacenado de hello no produce ningún dato. Eso es porque su Hola del resultado de conjunto de datos que controla la programación de Hola de actividad de hello (¿con qué frecuencia hello actividad se ejecuta - cada hora, diariamente, etcetera.). Hello conjunto de datos de salida debe usar un **servicio vinculado** que hace referencia tooan base de datos de SQL Azure o un almacén de datos de SQL Azure o una base de datos de SQL Server en el que desea Hola toorun de procedimiento almacenado. Hello conjunto de datos de salida puede actuar como un resultado de hello de manera toopass del procedimiento de hello almacenan para su posterior procesamiento por otra actividad ([encadenamiento actividades](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) de canalización de Hola. Sin embargo, factoría de datos no escribe automáticamente Hola un resultado de un conjunto de datos de toothis de procedimiento almacenado. Es el procedimiento almacenado Hola esa tabla SQL tooa de escrituras que Hola puntos de conjunto de datos de salida a. En algunos casos, puede ser el conjunto de datos de salida de hello un **conjunto de datos ficticio** (procedimiento almacenado de un conjunto de datos que señala tooa tabla que no contienen realmente salida de hello). Se usa este conjunto de datos ficticio solo toospecify programación de Hola para ejecutar Hola actividad de procedimiento almacenado. 

1. Haga clic en **... Más** en la barra de herramientas de hello, haga clic en **nuevo conjunto de datos**y haga clic en **SQL Azure**. **Nuevo conjunto de datos** en el comando de hello barra y seleccione **SQL Azure**.

    ![vista de árbol con servicios vinculados](media/data-factory-stored-proc-activity/new-dataset.png)
2. Copie y pegue la siguiente secuencia de comandos JSON en el editor de JSON toohello de Hola.

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy Hola conjunto de datos, haga clic en **implementar** en la barra de comandos de Hola. Confirme que aparece Hola conjunto de datos en la vista de árbol de Hola.

    ![vista de árbol con servicios vinculados](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a>Crear una canalización con una actividad SqlServerStoredProcedure
Ahora, vamos a crear una canalización con una actividad de procedimiento almacenado. 

Tenga en cuenta Hola propiedades siguientes: 

- Hola **tipo** propiedad se establece demasiado**SqlServerStoredProcedure**. 
- Hola **storedProcedureName** en tipo de las propiedades se establecen demasiado**sp_sample** (nombre de hello procedimiento almacenado).
- Hola **storedProcedureParameters** sección contiene un parámetro denominado **DataTime**. Nombre y mayúsculas y minúsculas del parámetro hello en JSON deben coincidir con nombre de Hola y mayúsculas y minúsculas del parámetro hello en la definición del procedimiento almacenado de Hola. Si necesita pasar null para un parámetro, use la sintaxis de hello: `"param1": null` (en minúsculas).
 
1. Haga clic en **... Más** Hola barra de comandos y haga clic en **nueva canalización**.
2. Copiar y pegar Hola siguiente fragmento de JSON:   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. canalización de hello toodeploy, haga clic en **implementar** en la barra de herramientas de Hola.  

### <a name="monitor-hello-pipeline"></a>Canalización de Hola de Monitor
1. Haga clic en **X** tooclose Editor de generador de datos hojas toonavigate hacer copia de hoja de la factoría de datos de toohello y haga clic en **diagrama**.

    ![icono Diagrama](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. Hola **vista de diagrama**, verá información general de las canalizaciones de Hola y conjuntos de datos utilizan en este tutorial.

    ![icono Diagrama](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. Hola vista de diagrama, haga doble clic en el conjunto de datos de hello `sprocsampleout`. Vea intervalos de hello en estado listo. Debería haber cinco segmentos porque un segmento se genera para cada hora entre la hora de inicio de Hola y hora de finalización de hello JSON.

    ![icono Diagrama](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. Cuando se encuentra en un segmento **listo** estado, ejecute un `select * from sampletable` consultarlo tooverify de base de datos de SQL Azure Hola que Hola datos se insertó en la tabla de toohello por procedimiento almacenado de Hola.

   ![Datos de salida](./media/data-factory-stored-proc-activity/output.png)

   Vea [canalización de hello Monitor](data-factory-monitor-manage-pipelines.md) para obtener información detallada sobre la supervisión de las canalizaciones de factoría de datos de Azure.  


## <a name="specify-an-input-dataset"></a>Especificación de un conjunto de datos de entrada
En el tutorial de hello, actividad de procedimiento almacenado no tiene los conjuntos de datos de entrada. Si especifica un conjunto de datos de entrada, hello actividad de procedimiento almacenado no se ejecuta hasta Hola segmento del conjunto de datos de entrada está disponible (en estado listo). conjunto de datos de Hello puede ser un conjunto de datos externo (que no se crea por otra actividad de hello misma canalización) o un conjunto de datos interno generado por una actividad de nivel superior (actividad de Hola que se ejecuta antes que esta actividad). Puede especificar varios conjuntos de datos de entrada para la actividad de procedimiento almacenado de Hola. Si lo hace, hello actividad de procedimiento almacenado se ejecuta sólo cuando todos los sectores de conjunto de datos de entrada de hello están disponibles (en estado listo). conjunto de datos de entrada de Hola no puede ser consumida en el procedimiento de hello almacenado como un parámetro. Es solo usa toocheck Hola dependencia antes de actividad de procedimiento almacenado de saludo inicial.

## <a name="chaining-with-other-activities"></a>Encadenamiento con otras actividades
Si desea toochain una actividad de nivel superior con esta actividad, especifique la salida de hello de actividad de nivel superior de hello como una entrada de esta actividad. Al hacerlo, hello actividad de procedimiento almacenado no se ejecuta hasta que finaliza la actividad de nivel superior de hello y conjunto de datos de salida de hello de actividad de nivel superior de hello está disponible (en estado listo). Puede especificar los conjuntos de datos de salida de varias actividades de nivel superior como los conjuntos de datos de actividad de procedimiento almacenado de Hola. Al hacerlo, Hola actividad de procedimiento almacenado se ejecuta solo cuando todos los sectores de conjunto de datos de entrada de hello están disponibles.  

En el siguiente ejemplo de Hola, salida de hello de actividad de copia de hello es: OutputDataset, que es una entrada de hello actividad de procedimiento almacenado. Por lo tanto, hello actividad de procedimiento almacenado no se ejecuta hasta que finaliza la actividad de copia de Hola y Hola OutputDataset segmento está disponible (en estado listo). Si especifica varios conjuntos de datos de entrada, hello actividad de procedimiento almacenado no se ejecuta hasta que estén disponibles todos los sectores de conjunto de datos de entrada de hello (en estado listo). no se puede usar conjuntos de datos de entrada de Hello directamente como actividad de procedimiento almacenado de toohello de parámetros. 

Para obtener más información sobre cómo encadenar actividades, vea [Varias actividades en una canalización](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline).

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

De forma similar, toolink Hola almacén actividad de procedimiento con **actividades de dirección descendente** (hello las actividades que se ejecutan una vez completadas hello actividades de procedimiento almacenado), especificar el conjunto de datos de salida de hello de la actividad de procedimiento almacenado de Hola como un entrada de actividad de nivel inferior hello en canalización Hola.

> [!IMPORTANT]
> Cuando se copian datos en la base de datos de SQL Azure o SQL Server, puede configurar hello **SqlSink** en tooinvoke de actividad de copia un procedimiento almacenado mediante el uso de hello **sqlWriterStoredProcedureName** propiedad. Para más información, consulte [Invocación del procedimiento almacenado desde la actividad de copia en Azure Data Factory](data-factory-invoke-stored-procedure-from-copy-activity.md). Para obtener más información acerca de la propiedad de hello, vea Hola siguientes artículos de conector: [base de datos de SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).
>  
> Cuando se copian datos de base de datos de SQL Azure o SQL Server o almacenamiento de datos de SQL Azure, puede configurar **SqlSource** en tooinvoke de actividad de copia una tooread de datos de procedimiento almacenado de base de datos de origen de hello mediante hello  **sqlReaderStoredProcedureName** propiedad. Para obtener más información, vea Hola siguientes artículos de conector: [base de datos de SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [almacenamiento de datos de SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          

## <a name="json-format"></a>Formato JSON
Este es el formato JSON de Hola para definir una actividad de procedimiento almacenado:

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

Hello en la tabla siguiente describe estas propiedades JSON:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| name | Nombre de actividad de Hola |Sí |
| description |Texto que describe qué actividad Hola se usa para |No |
| type | Se debe establecer en: **SqlServerStoredProcedure** | Sí |
| inputs | Opcional. Si especifica un conjunto de datos de entrada, debe estar disponible (en estado "Listo") para hello almacenado toorun de actividad de procedimiento. conjunto de datos de entrada de Hola no puede ser consumida en el procedimiento de hello almacenado como un parámetro. Es solo usa toocheck Hola dependencia antes de actividad de procedimiento almacenado de saludo inicial. |No |
| outputs | Debe especificar un conjunto de datos para una actividad de procedimiento almacenado. Conjunto de datos de salida especifica hello **programación** para hello almacenados actividad de procedimiento (cada hora, semanalmente, mensualmente, etcetera). <br/><br/>Hello conjunto de datos de salida debe usar un **servicio vinculado** que hace referencia tooan base de datos de SQL Azure o un almacén de datos de SQL Azure o una base de datos de SQL Server en el que desea Hola toorun de procedimiento almacenado. <br/><br/>Hello conjunto de datos de salida puede actuar como un resultado de hello de manera toopass del procedimiento de hello almacenan para su posterior procesamiento por otra actividad ([encadenamiento actividades](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) de canalización de Hola. Sin embargo, factoría de datos no escribe automáticamente Hola un resultado de un conjunto de datos de toothis de procedimiento almacenado. Es el procedimiento almacenado Hola esa tabla SQL tooa de escrituras que Hola puntos de conjunto de datos de salida a. <br/><br/>En algunos casos, puede ser el conjunto de datos de salida de hello un **conjunto de datos ficticio**, que se usa solo la programación de hello toospecify para ejecutar Hola actividad de procedimiento almacenado. |Sí |
| storedProcedureName |Especifique el nombre de hello del procedimiento de hello almacenado en la base de datos de SQL Azure de Hola o base de datos de almacenamiento de datos de SQL Azure o SQL Server que se representa mediante el servicio vinculado de Hola que Hola usos de la tabla de salida. |Sí |
| storedProcedureParameters |Especifique valores para los parámetros del procedimiento almacenado. Si necesitas toopass null para un parámetro, use la sintaxis de hello: "param1": null (todas las minúsculas). Vea Hola después toolearn de ejemplo sobre el uso de esta propiedad. |No |

## <a name="passing-a-static-value"></a>Pasar un valor estático
Ahora, veamos agregar otra columna con el nombre 'Escenario' en tabla de Hola que contiene un valor estático denominado 'Ejemplo de documento'.

![Datos de ejemplo 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

**Tabla:**

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

**Procedimiento almacenado:**

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

Ahora, pasar hello **escenario** hello y parámetro de valor de hello actividad de procedimiento almacenado. Hola **typeProperties** sección Hola anterior ejemplo parece Hola siguiente fragmento de código:

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

**Conjuntos de datos de Data Factory:**

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Canalización de Data Factory**

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```