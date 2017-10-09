---
title: "copia de aaaRepeatable de factoría de datos de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooavoid duplicados aunque un segmento que copia los datos se ejecute más de una vez."
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
ms.openlocfilehash: 79a3fde2b700bf0a0e167479d6a86c5bee1bf7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a>Copia repetible en Azure Data Factory

## <a name="repeatable-read-from-relational-sources"></a>Lectura repetible de orígenes relacionales
Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos. En Azure Data Factory, puede volver a ejecutar un segmento manualmente. También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error. Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento.  
 
> [!NOTE]
> Hello en los ejemplos siguientes son para SQL Azure pero tooany aplicables almacén de datos que admite conjuntos de datos rectangular. Es posible que tenga hello tooadjust **tipo** de hello y origen **consulta** propiedad (por ejemplo: consulta en lugar de sqlReaderQuery) para los datos de hello almacenar.   

Por lo general, al leer de almacenes relacionales, desea solo datos de hello tooread correspondiente toothat segmento. Un toodo de manera por lo que sería mediante el uso de hello WindowStart y WindowEnd variables del sistema disponibles en Data Factory de Azure. Leer sobre las variables de Hola y funciones de factoría de datos de Azure aquí en hello [factoría de datos de Azure: funciones y Variables del sistema](data-factory-functions-variables.md) artículo. Ejemplo: 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
Esta consulta lee los datos que se encuentra en el intervalo de duración del segmento hello (WindowStart -> WindowEnd) de la tabla MyTable de Hola. Vuelva a ejecutar de este segmento aseguraría también siempre que Hola se leen los mismos datos. 

En otros casos, puede que quieran tooread Hola toda la tabla y puede definir hello sqlReaderQuery como se indica a continuación:

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a>Escritura repetible tooSqlSink
Cuando se copian datos demasiado**Azure SQL o SQL Server** desde otros almacenes de datos, necesita tookeep repetibilidad en mente tooavoid resultados imprevistos. 

Cuando se copian datos tooAzure base de datos SQL o SQL Server, actividad de copia de hello anexa la tabla de datos toohello receptor de forma predeterminada. Supongamos, se copian datos desde un CSV (valores separados por comas) archivo que contiene dos registros toohello en una base de datos de Azure SQL o SQL Server en la tabla siguiente. Cuando se ejecuta un segmento, Hola dos registros son copiados toohello table de SQL. 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

Suponga que encuentra errores en el archivo de código fuente y actualiza la cantidad de Hola de Tube hacia abajo de too4 2. Si se vuelve a ejecutar el segmento de datos de Hola durante ese período manualmente, encontrará dos nuevos registros anexan tooAzure base de datos SQL o SQL Server. En este ejemplo se da por supuesto que ninguna de las columnas de hello en la tabla de hello tiene restricción de clave principal de Hola.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid este comportamiento, necesita una semántica UPSERT toospecify mediante uno de hello siguiendo dos mecanismos:

### <a name="mechanism-1-using-sqlwritercleanupscript"></a>Mecanismo 1: Uso de sqlWriterCleanupScript
Puede usar hello **sqlWriterCleanupScript** propiedad tooclean los datos de tabla de receptor de hello antes de insertar datos de hello cuando se ejecuta un segmento. 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

Cuando se ejecuta un segmento, script de limpieza de Hola se ejecuta primero los datos toodelete correspondiente segmento toohello de tabla SQL Hola. actividad de copia de Hello, a continuación, inserta datos en hello Table de SQL. Si se vuelve a ejecutar el segmento de hello, se actualiza la cantidad de hello según lo deseado.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

Imagine Hola registro arandela sin formato se quita de hello original csv. A continuación, volver a ejecutar el segmento de Hola generaría Hola siguiente resultado: 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

actividad de copia de Hello ejecutó Hola limpieza script toodelete Hola datos correspondientes para dicho sector. A continuación, debe leer Hola entrada desde archivo csv de hello (que, a continuación, se incluye un único registro) y se inserta en hello tabla. 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a>Mecanismo 2: Uso de sliceIdentifierColumnName
> [!IMPORTANT]
> sliceIdentifierColumnName no se admite en este momento para Azure SQL Data Warehouse. 

repetibilidad de Hello segundo mecanismo tooachieve es tener una columna dedicada (sliceIdentifierColumnName) en el destino de hello tabla. Esta columna se usaría por factoría de datos de Azure tooensure Hola origen y destino permanecen sincronizadas. Este enfoque funciona cuando se produce la flexibilidad de cambiar o definir el esquema de tabla SQL de destino de Hola. 

Esta columna se utiliza por factoría de datos de Azure para fines de capacidad de repetición y, en el proceso de hello Data Factory de Azure no cualquier esquema cambia toohello tabla. Forma toouse este enfoque:

1. Definir una columna de tipo **binario (32)** en el destino de hello Table de SQL. No debería haber ninguna restricción en esta columna. En este ejemplo, llamaremos a esta columna AdfSliceIdentifier.


    Tabla de origen:

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    Tabla de destino: 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. Usarlo en la actividad de copia de hello como sigue:
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

Factoría de datos de Azure rellena esta columna según su necesidad tooensure Hola origen y destino están sincronizadas. valores de Hello de esta columna no deben utilizarse fuera de este contexto. 

Toomechanism similar 1, actividad de copia limpia automáticamente los datos de Hola para hello proporcionada segmento desde el destino de hello Table de SQL. A continuación, inserta datos de origen en la tabla de destino de toohello. 

## <a name="next-steps"></a>Pasos siguientes
Revisar los siguientes artículos de conector que para JSON ejemplos completos de Hola: 

- [Azure SQL Database](data-factory-azure-sql-connector.md)
- [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)