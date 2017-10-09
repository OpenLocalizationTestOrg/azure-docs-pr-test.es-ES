---
title: datos de aaaMove de un tooSQL de SQL Server local Azure con Data Factory de Azure | Documentos de Microsoft
description: "Configurar una canalización ADF que se compone de dos actividades de migración de datos que juntos se mueven datos a diario entre las bases de datos locales y en la nube de Hola."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a>Mover los datos de un servidor SQL local tooSQL Azure con Data Factory de Azure
Este tema muestra cómo toomove datos desde una base de datos de SQL Server local, tooa base de datos de SQL Azure a través de almacenamiento de blobs de Azure mediante Hola factoría de datos de Azure (ADF).

Para una tabla que resume las distintas opciones para mover datos tooan base de datos de SQL Azure, vea [mover datos tooan base de datos de SQL Azure para el aprendizaje automático de Azure](machine-learning-data-science-move-sql-azure.md).

## <a name="intro"></a>Introducción: ¿Qué es ADF y cuándo debe ser toomigrate usa datos?
Factoría de datos de Azure es un servicio de integración de datos en la nube totalmente administrado que organiza y automatiza el movimiento de Hola y la transformación de datos. concepto clave de Hello en el modelo ADF hello es la canalización. Una canalización es una agrupación lógica de actividades, cada uno de los cuales define Hola acciones tooperform en datos de hello incluidos en conjuntos de datos. Servicios vinculados son información de hello toodefine usado necesaria para los recursos de datos de Data Factory tooconnect toohello.

Con ADF, servicios de procesamiento de datos existentes se pueden formular en las canalizaciones de datos que están administrados y de alta disponibilidad en la nube de Hola. Estas canalizaciones de datos pueden ser tooingest programada, preparar, transformar, analizar y publicar datos y ADF administra y organiza datos complejos de Hola y dependencias de procesamiento. Soluciones pueden estar en la nube rápidamente compilado e implementado en hello, conectar un número creciente de local y orígenes de datos en la nube.

Considere el uso de ADF en estos casos:

* Cuando datos necesidades toobe continuamente migrado en un escenario híbrido que tenga acceso a ambos locales y recursos de la nube
* Cuando se lleva a cabo datos Hola o necesidades toobe modificado o tiene lógica de negocios agrega tooit al que se está migrando.

ADF permite Hola de programación y la supervisión de trabajos mediante scripts sencillos de JSON que administran el movimiento de Hola de datos de forma periódica. La ADF también tiene otras capacidades como la compatibilidad con operaciones complejas. Para obtener más información sobre ADF, consulte documentación de hello en [factoría de datos de Azure (ADF)](https://azure.microsoft.com/services/data-factory/).

## <a name="scenario"></a>Hola escenario
Configuramos una canalización ADF que se compone de dos actividades de migración de datos. Juntos se mueven datos a diario entre una base de datos SQL local y una base de datos de SQL Azure en la nube de Hola. Hola dos actividades son:

* copiar los datos de una base de datos de SQL Server local tooan cuenta de almacenamiento de blobs de Azure
* copiar datos de hello almacenamiento de blobs de Azure cuenta tooan base de datos de SQL Azure.

> [!NOTE]
> Hola pasos que se muestran aquí se han adaptado del hello más tutorial proporcionado por el equipo ADF hello: [mover datos entre orígenes locales y en la nube con Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) hace referencia a toohello secciones relevantes de ese tema se proporcionan cuando corresponda.
>
>

## <a name="prereqs"></a>Requisitos previos
En este tutorial se asume que dispone de:

* Una **suscripción de Azure**. Si no tiene una suscripción, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Una **cuenta de almacenamiento de Azure**. Usar una cuenta de almacenamiento de Azure para almacenar datos de hello en este tutorial. Si no tiene una cuenta de almacenamiento de Azure, vea hello [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artículo. Una vez haya creado la cuenta de almacenamiento de hello, necesita tooobtain Hola cuenta clave usa el almacenamiento de información de tooaccess Hola. Consulte [Administración de la cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Acceso tooan **base de datos de SQL Azure**. Si debe configurar una base de datos de SQL Azure, Hola tpoic [Introducción a la base de datos de SQL de Microsoft Azure ](../sql-database/sql-database-get-started.md) proporciona información acerca de cómo tooprovision una nueva instancia de una base de datos de SQL Azure.
* **Azure PowerShell** instalado y configurado de forma local. Para obtener instrucciones, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

> [!NOTE]
> Este procedimiento utiliza hello [portal de Azure](https://portal.azure.com/).
>
>

## <a name="upload-data"></a>Carga Hola datos tooyour SQL Server local
Usamos hello [conjunto de datos de Nueva York Taxi](http://chriswhong.com/open-data/foil_nyc_taxi/) proceso de migración de toodemonstrate Hola. Hello NYC Taxi conjunto de datos está disponible, como se indicó en esa entrada en el almacenamiento de blobs de Azure [NYC Taxi datos](http://www.andresmh.com/nyctaxitrips/). datos de Hello tienen dos archivos, archivo de trip_data.csv hello, que contiene detalles de ida y vuelta, y archivo de trip_far.csv hello, que contiene detalles de tarifa de Hola de pago para cada recorrido. En [Descripción del conjunto de datos de carreras de taxi de Nueva York](machine-learning-data-science-process-sql-walkthrough.md#dataset), se proporciona un ejemplo y una descripción de estos archivos.

Puede adaptar procedimiento Hola proporcionada aquí tooa conjunto de sus propios datos, o bien, siga los pasos de hello tal como se describe mediante el uso de hello NYC Taxi conjunto de datos. Hola tooupload NYC Taxi conjunto de datos en la base de datos de SQL Server local, siga procedimiento Hola descrito en [importar masivamente datos en la base de datos de SQL Server](machine-learning-data-science-process-sql-walkthrough.md#dbload). Estas instrucciones son para un servidor de SQL Server en una máquina Virtual de Azure, pero Hola procedimiento Hola para cargar toohello local de SQL Server es igual.

## <a name="create-adf"></a> Crear una factoría de datos de Azure
Hola instrucciones para crear un nuevo generador de datos de Azure y un grupo de recursos en hello [portal de Azure](https://portal.azure.com/) se proporcionan [crear un generador de datos de Azure](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory). Nombre hello nueva ADF instancia *adfdsp* y grupo de recursos de nombre hello creado *adfdsprg*.

## <a name="install-and-configure-up-hello-data-management-gateway"></a>Instalar y configurar Hola Data Management Gateway
tooenable sus canalizaciones en un generador de datos de Azure toowork con un servidor local de SQL, deberá tooadd como una factoría de datos de toohello de servicio vinculado. toocreate un servicio vinculado para un servidor local de SQL, debe:

* Descargue e instale Microsoft Data Management Gateway en el equipo local de Hola.
* configurar el servicio de hello vinculado para puerta de enlace de hello local datos origen toouse Hola.

Hola Data Management Gateway serializa y deserializa datos de origen y el receptor de hello en equipo Hola donde estén hospedados.

Para obtener instrucciones de instalación e información detallada sobre Data Management Gateway, consulte [Movimiento de datos entre orígenes locales y la nube con Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)

## <a name="adflinkedservices"></a>Crear servicios vinculados tooconnect toohello recursos de datos
Un servicio vinculado define información de hello necesaria para el recurso de datos de Data Factory de Azure tooconnect tooa. procedimiento paso a paso de Hola para crear servicios vinculados se proporciona en [crear servicios vinculados](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).

Tenemos tres recursos en este escenario para los que se necesitan servicios vinculados.

1. [Servicio vinculado para SQL Server local](#adf-linked-service-onprem-sql)
2. [Servicio vinculado para el almacenamiento de blobs de Azure](#adf-linked-service-blob-store)
3. [Servicio vinculado para la base de datos SQL de Azure](#adf-linked-service-azure-sql)

### <a name="adf-linked-service-onprem-sql"></a>Servicio vinculado para la base de datos SQL Server local
toocreate Hola vinculado servicio para hello local de SQL Server:

* Haga clic en hello **almacén de datos** en la página de aterrizaje de ADF hello en el Portal de Azure clásico
* Seleccione **SQL** y escriba hello *nombre de usuario* y *contraseña* las credenciales de hello SQL Server local. Necesita tooenter Hola servername como un **nombre de la instancia de la barra diagonal inversa completo servername (nombreDeServidor ombreDeInstancia)**. Hola de nombre de servicio vinculado *adfonpremsql*.

### <a name="adf-linked-service-blob-store"></a>Servicio vinculado de blob
toocreate Hola servicio vinculado para la cuenta de almacenamiento de blobs de Azure de hello:

* Haga clic en hello **almacén de datos** en la página de aterrizaje de ADF hello en el Portal de Azure clásico
* Seleccione **Azure Storage Account**
* Escriba el nombre de clave y el contenedor de la cuenta del almacenamiento de blobs de Azure Hola. Hola de nombre de servicio vinculado *adfds*.

### <a name="adf-linked-service-azure-sql"></a>Servicio vinculado para la base de datos SQL de Azure
toocreate Hola servicio vinculado de hello base de datos de SQL Azure:

* Haga clic en hello **almacén de datos** en la página de aterrizaje de ADF hello en el Portal de Azure clásico
* Seleccione **SQL Azure** y escriba hello *nombre de usuario* y *contraseña* credenciales para hello base de datos de SQL Azure. Hola *nombre de usuario* debe especificarse como  *user@servername* .   

## <a name="adf-tables"></a>Definir y crear tablas toospecify cómo tooaccess Hola conjuntos de datos
Crear tablas que especifican estructura hello, la ubicación y la disponibilidad de los conjuntos de datos de hello con hello procedimientos basados en script. Archivos JSON son tablas de hello toodefine usado. Para obtener más información sobre la estructura de Hola de estos archivos, consulte [conjuntos de datos](../data-factory/data-factory-create-datasets.md).

> [!NOTE]
> Debe ejecutar hello `Add-AzureAccount` cmdlet antes de ejecutar hello [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) tooconfirm de cmdlet que Hola suscripción de Azure derecha está seleccionada para la ejecución del comando de Hola. Para obtener documentación sobre este cmdlet, consulte [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).
>
>

las definiciones basadas en JSON de Hello en tablas de hello usan hello después de nombres:

* Hola **nombre de la tabla** en hello local SQL server es *nyctaxi_data*
* Hola **nombre del contenedor** en hello almacenamiento de blobs de Azure es cuenta *containername*  

Se necesitan tres definiciones de tabla para esta canalización de ADF:

1. [Tabla de SQL local](#adf-table-onprem-sql)
2. [Tabla Blob ](#adf-table-blob-store)
3. [Tabla SQL de Azure](#adf-table-azure-sql)

> [!NOTE]
> Estos procedimientos usar toodefine de PowerShell de Azure y crear hello las actividades ADF. Pero estas tareas pueden realizarse también mediante Hola portal de Azure. Para más información, consulte [Creación de conjuntos de datos](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).
>
>

### <a name="adf-table-onprem-sql"></a>Tabla de SQL local
definición de la tabla de Hola para hello local de SQL Server se especifica en hello el archivo JSON siguiente:

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

nombres de columna de Hello no se incluyeron. Puede Sub-seleccionar en nombres de columna de hello incluyéndolos aquí (para obtener más información Compruebe hello [documentación de ADF](../data-factory/data-factory-data-movement-activities.md) tema.

Copiar la definición de JSON de Hola de tabla de hello en un archivo denominado *onpremtabledef.json* y guardar archivos conoce la ubicación de tooa (aquí supone toobe *C:\temp\onpremtabledef.json*). Crear tabla de hello en ADF con hello siguiente cmdlet de PowerShell de Azure:

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <a name="adf-table-blob-store"></a>Tabla Blob
Definición de la tabla de Hola para hello de salida blob se encuentra en la siguiente hello (Esto asigna datos de hello ingerida de blob de tooAzure local):

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

Copiar la definición de JSON de Hola de tabla de hello en un archivo denominado *bloboutputtabledef.json* y guardar archivos conoce la ubicación de tooa (aquí supone toobe *C:\temp\bloboutputtabledef.json*). Crear tabla de hello en ADF con hello siguiente cmdlet de PowerShell de Azure:

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <a name="adf-table-azure-sq"></a>Tabla SQL de Azure
Definición de tabla Hola Hola salida de SQL Azure es siguiente hello (este esquema asigna datos de hello procedentes de blob de hello):

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

Copiar la definición de JSON de Hola de tabla de hello en un archivo denominado *AzureSqlTable.json* y guardar archivos conoce la ubicación de tooa (aquí supone toobe *C:\temp\AzureSqlTable.json*). Crear tabla de hello en ADF con hello siguiente cmdlet de PowerShell de Azure:

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <a name="adf-pipeline"></a>Definir y crear la canalización de Hola
Especifique las actividades de Hola que pertenecen toohello de canalización y crear canalización Hola con hello procedimientos basados en script. Un archivo JSON es propiedades de canalización de hello toodefine usado.

* Hello script se da por supuesto que hello **nombre de la canalización** es *AMLDSProcessPipeline*.
* Tenga en cuenta que se debe establecer periodicidad Hola de hello canalización toobe ejecutado en cada día base y el uso Hola tiempo de ejecución predeterminado para el trabajo de hello (12 a.m. hora UTC).

> [!NOTE]
> Hello procedimientos siguientes utilice toodefine de PowerShell de Azure y crear la canalización ADF Hola. Sin embargo, esta tarea también se puede realizar en Azure Portal. Para más información, consulte [Creación de una canalización](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).
>
>

Usar definiciones de tabla de Hola proporcionado anteriormente, definición de la canalización de Hola para hello que ADF se especifica como sigue:

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data tooSql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

Copie esta definición JSON de canalización de hello en un archivo denominado *pipelinedef.json* y guardar archivos conoce la ubicación de tooa (aquí supone toobe *C:\temp\pipelinedef.json*). Crear canalización Hola de ADF con hello siguiente cmdlet de PowerShell de Azure:

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

Confirmar que puede ver canalización hello en hello ADF Hola Portal clásico de Azure se mostrarán como sigue (al hacer clic en el diagrama de hello)

![Canalización de ADF](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <a name="adf-pipeline-start"></a>Iniciar Hola canalización
canalización de Hello ahora se pueden ejecutar con hello siguiente comando:

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

Hola *startdate* y *enddate* toobe reemplazado con fechas de hello real entre los que desea Hola canalización toorun los valores de parámetro tienen.

Una vez que se ejecuta la canalización de hello, debe ser capaz de toosee Hola datos aparezcan de contenedor de hello seleccionado para el blob de hello, un archivo por día.

Tenga en cuenta que no hemos aprovechado funcionalidad de Hola que proporciona datos ADF toopipe incrementalmente. Para obtener más información sobre cómo toodo esta y otras funcionalidades proporcionadas por ADF, vea Hola [documentación de ADF](https://azure.microsoft.com/services/data-factory/).
