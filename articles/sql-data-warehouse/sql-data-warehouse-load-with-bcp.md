---
title: datos de tooload aaaUse bcp en almacenamiento de datos SQL | Documentos de Microsoft
description: "Obtenga información acerca de qué bcp es y cómo toouse para escenarios de almacenamiento de datos."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: f9467d11-fcd6-4131-a65a-2022d2c32d24
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 09a2980585097644924c71899f9e74fb32fbc26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-bcp"></a>Carga de datos con BCP
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Factoría de datos](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

**[BCP] [ bcp]**  es una utilidad de carga masiva de línea de comandos que le permite toocopy datos entre SQL Server, archivos de datos y almacenamiento de datos SQL. Usar bcp tooimport grandes cantidades de filas en tablas de almacenamiento de datos SQL o tooexport datos de tablas de SQL Server a archivos de datos. Excepto cuando se usa con la opción queryout de hello, bcp no requiere ningún conocimiento de Transact-SQL.

bcp es una manera rápida y sencilla toomove más pequeños conjuntos de datos dentro y fuera de una base de datos de almacenamiento de datos SQL. cantidad exacta de Hola de datos que se recomienda tooload/extract mediante bcp dependerá en su centro de datos de Azure toohello de conexión de red.  Por lo general, las tablas de dimensiones se pueden cargar y extraer fácilmente con bcp; sin embargo, no se recomienda bcp para cargar o extraer grandes volúmenes de datos.  Polybase es hello recomendada herramienta para cargar y extraer grandes volúmenes de datos como lo hace un mejor trabajo para aprovechar la arquitectura de procesamiento paralelo masivo Hola de almacenamiento de datos SQL.

Con bcp puede:

* Use una utilidad de línea de comandos simple tooload de datos en almacenamiento de datos de SQL.
* Utilizar la utilidad de línea de comandos simple tooextract datos de almacenamiento de datos SQL.

Este tutorial le mostrará cómo:

* Importar datos en una tabla mediante bcp de hello en comando
* Exportar datos de tabla usar Hola bcp out comando

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

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
