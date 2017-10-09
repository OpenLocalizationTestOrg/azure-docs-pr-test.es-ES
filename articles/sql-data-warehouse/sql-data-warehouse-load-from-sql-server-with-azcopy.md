---
title: datos de aaaLoad de SQL Server en almacenamiento de datos de SQL Azure (PolyBase) | Documentos de Microsoft
description: Utiliza bcp tooexport datos desde archivos de tooflat de SQL Server, el almacenamiento de blobs de AZCopy tooimport datos tooAzure y datos de PolyBase tooingest hello en almacenamiento de datos de SQL Azure.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4d42786a-fb28-43c9-9c3b-72d19c0ecc11
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 89e2a91bc97642e9fc18545cb802b42d8dc4ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a>Carga de datos de SQL Server en Almacenamiento de datos SQL de Azure (AZCopy)
Usar bcp y los datos de tooload de utilidades de línea de comandos de AZCopy desde almacenamiento de blobs de SQL Server tooAzure. A continuación, usar datos de Hola de tooload de PolyBase o Data Factory de Azure en almacenamiento de datos de SQL Azure. 

## <a name="prerequisites"></a>Requisitos previos
toostep a través de este tutorial, necesitará:

* Una base de datos de Almacenamiento de datos SQL
* utilidad de línea de comandos bcp Hola instalado
* Hola instalada la utilidad de línea de comandos SQLCMD

> [!NOTE]
> Puede descargar las utilidades de bcp y sqlcmd de Hola de hello [Microsoft Download Center][Microsoft Download Center].
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a>Importación de datos en Almacenamiento de datos SQL
En este tutorial, creará una tabla en el almacén de datos de SQL Azure e importar datos en la tabla de Hola.

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a>Paso 1: Crear una tabla en Almacenamiento de datos SQL de Azure
Desde un símbolo del sistema, use sqlcmd toorun Hola siguiente toocreate consulta una tabla de la instancia:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```

> [!NOTE]
> Vea [información general de la tabla] [ Table Overview] o [sintaxis de CREATE TABLE] [ CREATE TABLE syntax] para obtener más información acerca de cómo crear una tabla en hello y almacenamiento de datos SQL  opciones disponibles en la cláusula WITH de Hola.
> 
> 

### <a name="step-2-create-a-source-data-file"></a>Paso 2: Crear un archivo de datos de origen
Abra el Bloc de notas y copie Hola después de líneas de datos en un nuevo archivo de texto y, a continuación, guarde este archivo tooyour directorio temporal local, C:\Temp\DimDate2.txt.

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

> [!NOTE]
> Es importante tooremember ese bcp.exe no admite la codificación del archivo hello UTF-8. Use archivos ASCII o archivos codificados UTF-16 al usar bcp.exe.
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a>Paso 3: Conectarse e importar datos de Hola
Usar bcp, puede conectarse e importar datos de hello mediante Hola después de reemplazar valores de hello comando según corresponda:

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

También puede comprobar Hola se cargaron los datos mediante la ejecución de hello después de consulta mediante sqlcmd:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

Se debe devolver Hola siguientes resultados:

| DateId | CalendarQuarter | FiscalQuarter |
| --- | --- | --- |
| 20150101 |1 |3 |
| 20150201 |1 |3 |
| 20150301 |1 |3 |
| 20150401 |2 |4 |
| 20150501 |2 |4 |
| 20150601 |2 |4 |
| 20150701 |3 |1 |
| 20150801 |3 |1 |
| 20150801 |3 |1 |
| 20151001 |4 |2 |
| 20151101 |4 |2 |
| 20151201 |4 |2 |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>Paso 4: Crear estadísticas de los datos recién cargados
Almacenamiento de datos SQL de Azure todavía no permite crear ni actualizar automáticamente las estadísticas. En orden tooget Hola un mejor rendimiento de las consultas, es importante que las estadísticas se crean en todas las columnas de todas las tablas después de la primera carga de Hola o se producen cambios sustanciales en datos Hola. Para obtener una explicación detallada de las estadísticas, vea hello [estadísticas] [ Statistics] tema en el grupo de desarrollo de Hola de temas. A continuación se muestra un ejemplo rápido de cómo cargarán toocreate estadísticas en la tabla de hello en este ejemplo

Ejecute hello siguiendo las instrucciones CREATE STATISTICS desde un símbolo del sistema de sqlcmd:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a>Exportación de datos de Almacenamiento de datos SQL
En este tutorial, creará un archivo de datos a partir de una tabla de Almacenamiento de datos SQL. Se exportará datos Hola que hemos creado anteriormente tooa nuevo archivo de datos denominado DimDate2_export.txt.

### <a name="step-1-export-hello-data"></a>Paso 1: Exportar datos de Hola
Mediante la utilidad bcp de hello, puede conectar y exportar datos mediante Hola después de reemplazar valores de hello comando según corresponda:

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
Puede comprobar Hola datos se exportaron correctamente, abra el archivo nuevo de hello. datos de Hello en el archivo hello deben coincidir con texto hello siguiente:

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

> [!NOTE]
> Debido a la naturaleza toohello de sistemas distribuidos, Hola datos orden no sea el mismo Hola entre bases de datos de almacenamiento de datos SQL. Otra opción es hello toouse **queryout** función de bcp toowrite una consulta extraer en lugar de exportar toda la tabla Hola.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Para obtener información general sobre la carga, vea [Carga de datos en SQL Data Warehouse][Load data into SQL Data Warehouse].
Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de Almacenamiento de datos SQL][SQL Data Warehouse development overview].

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
