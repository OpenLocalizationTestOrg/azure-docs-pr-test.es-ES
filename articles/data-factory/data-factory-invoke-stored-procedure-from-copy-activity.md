---
title: "aaaInvoke el procedimiento almacenado de actividad de copia de factoría de datos de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de la actividad de copia de tooinvoke un procedimiento almacenado en la base de datos de SQL Azure o SQL Server desde una factoría de datos de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 986377118afb8c08607c2325fcc3ab00b3de9268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a>Invocación del procedimiento almacenado desde la actividad de copia en Azure Data Factory
Cuando se copian datos en [SQL Server](data-factory-sqlserver-connector.md) o [base de datos de SQL Azure](data-factory-azure-sql-connector.md), puede configurar hello **SqlSink** en tooinvoke de actividad de copia un procedimiento almacenado. Puede que desee toouse Hola almacenado procedimiento tooperform es necesario ningún procesamiento adicional (combinar columnas, buscar valores, la inserción en varias tablas, etc.) antes de insertar datos en la tabla de destino de toohello. Esta característica aprovecha los [parámetros con valores de tabla](https://msdn.microsoft.com/library/bb675163.aspx). 

Hola siguiente ejemplo muestra cómo tooinvoke un procedimiento almacenado en un servidor SQL Server de base de datos de una canalización de factoría de datos (actividad de copia):  

## <a name="output-dataset-json"></a>JSON de conjunto de datos de salida
En el conjunto de datos de salida de hello JSON, establezca hello **tipo** a: **SqlServerTable**. Establézcalo demasiado**AzureSqlTable** toouse con una base de datos de SQL Azure. Hola valor para **tableName** propiedad debe coincidir con el nombre de hello del primer parámetro del procedimiento almacenado de Hola.  

```json
{
  "name": "SqlOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlLinkedService",
    "typeProperties": {
      "tableName": "Marketing"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

## <a name="sqlsink-section-in-copy-activity-json"></a>Sección SqlSink del JSON de actividad de copia
Definir hello **SqlSink** sección JSON de la actividad de copia hello como se indica a continuación. tooinvoke un procedimiento almacenado al insertar datos en la base de datos de receptor o el destino de hello, especifica los valores de **SqlWriterStoredProcedureName** y **SqlWriterTableType** propiedades. Para obtener descripciones de estas propiedades, vea [SqlSink sección en el artículo de conector de SQL Server de hello](data-factory-sqlserver-connector.md#sqlsink).

```json
"sink":
{
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing", 
    "storedProcedureParameters":
            {
                "stringData": 
                {
                    "value": "str1"     
                }
            }
}
```

## <a name="stored-procedure-definition"></a>Definición del procedimiento almacenado 
En la base de datos, definir el procedimiento de hello almacenado con hello mismo nombre como **SqlWriterStoredProcedureName**. procedimiento almacenado de Hello administra los datos de entrada de almacén de datos de origen de Hola e inserta datos en una tabla de base de datos de destino de Hola. nombre de Hello del primer parámetro del procedimiento almacenado de hello debe coincidir con tableName Hola definido en el conjunto de datos de hello JSON (Marketing).

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a>Definición de tipo de tabla
En la base de datos, definir el tipo de tabla de hello con hello mismo nombre como **SqlWriterTableType**. esquema de Hola Hola del tipo de tabla debe coincide Hola del conjunto de datos de entrada de Hola.

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a>Pasos siguientes
Revisar los siguientes artículos de conector que para JSON ejemplos completos de Hola: 

- [Azure SQL Database](data-factory-azure-sql-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)
