---
title: datos de aaaLoad de SQL Server en almacenamiento de datos de SQL Azure (copia masiva bcp) | Documentos de Microsoft
description: "Un pequeño tamaño de datos, se utiliza bcp tooexport datos de archivos de SQL Server tooflat e importar los datos de hello directamente en el almacenamiento de datos de SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: a03b5403d123e8814ae73a7cce8e6851c8b264a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a>Carga de datos de SQL Server en Almacenamiento de datos SQL de Azure (archivos planos)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

Para conjuntos de datos pequeños, puede usar datos de tooexport Hola bcp utilidad de línea de comandos de SQL Server y, a continuación, cargarlo directamente del almacenamiento de datos SQL tooAzure.

En este tutorial, usará bcp para:

* Exportar una tabla a partir de SQL Server mediante la utilidad bcp Hola comando (o crear un archivo de ejemplo simple)
* Tabla de Hola de importación de un almacén de datos de archivo sin formato tooSQL.
* Crear estadísticas en datos cargado de saludo.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a>Antes de empezar
### <a name="prerequisites"></a>Requisitos previos
toostep a través de este tutorial, necesitará:

* Una base de datos de Almacenamiento de datos SQL
* utilidad de línea de comandos de Hello bcp instalado
* utilidad de línea de comandos de sqlcmd Hola instalada

Puede descargar las utilidades de bcp y sqlcmd de Hola de hello [Microsoft Download Center][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>Datos en los formatos ASCII o UTF-16
Si está tratando de este tutorial con sus propios datos, necesita los datos toouse Hola ASCII o la codificación UTF-16 dado bcp no es compatible con UTF-8. 

PolyBase admite UTF-8, pero aún no es compatible con UTF-16. Tenga en cuenta que si desea que bcp toocombine con PolyBase necesitará tootransform Hola datos tooUTF-8 después de que se exportó desde SQL Server. 

## <a name="1-create-a-destination-table"></a>1. Creación de una tabla de destino.
Definir una tabla en el almacén de datos de SQL que será la tabla de destino de Hola para carga Hola. columnas de Hello en la tabla de hello deben corresponder toohello datos en cada fila de su archivo de datos.

toocreate una tabla, abra un símbolo del sistema y use sqlcmd.exe toorun Hola siguiente comando:

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


## <a name="2-create-a-source-data-file"></a>2. Creación de un archivo de datos de origen
Abra el Bloc de notas y copie Hola después de líneas de datos en un nuevo archivo de texto y, a continuación, guarde este archivo tooyour directorio temporal local, C:\Temp\DimDate2.txt. Estos datos están en formato ASCII.

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

(Opcional) tooexport sus propios datos de una base de datos de SQL Server, abra un símbolo del sistema y ejecute el siguiente comando de Hola. Reemplace TableName, ServerName, DatabaseName, Username y Password por su propia información.

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a>3. Cargar datos de Hola
datos de hello tooload, abra un símbolo del sistema y ejecute hello siguiente comando, reemplazando los valores de hello para nombre del servidor, nombre de base de datos, nombre de usuario y contraseña con su propia información.

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

Utilice este comando tooverify hello se cargaron correctamente los datos

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

resultados de Hello deberían tener este aspecto:

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

## <a name="4-create-statistics"></a>4. Creación de estadísticas
Almacenamiento de datos SQL de Azure aún no admite la creación o actualización automáticas de estadísticas. tooget Hola mejor rendimiento de las consultas, es importante toocreate estadísticas en todas las columnas de todas las tablas después de la primera carga de Hola o después de que se producen cambios sustanciales en datos Hola. Para ver una explicación detallada de las estadísticas, vea [Estadísticas][Statistics]. 

Siguiente ejecución Hola comando toocreate estadísticas en la tabla recién cargada.

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a>5. Exportación de datos de Almacenamiento de datos SQL
Para divertirse, puede exportar datos de Hola que acabo de cargar volver fuera del almacén de datos SQL.  Hola comando tooexport es exactamente Hola igual a la exportación de SQL Server.

Sin embargo, hay una diferencia en los resultados de Hola. Puesto que los datos de Hola se almacenan en ubicaciones distribuidas en almacenamiento de datos de SQL, al exportar datos en cada nodo de ejecución se escribe en archivo de salida de toohello de datos. orden de Hola de datos de hello en el archivo de salida de hello es probable que toobe diferente del orden de Hola de los datos de hello en el archivo de entrada de Hola.

### <a name="export-a-table-and-compare-exported-results"></a>Exportación de una tabla y comparación de los resultados exportados
toosee Hola datos exportados, abra un símbolo del sistema y ejecute este comando con sus propios parámetros. NombreDeServidor es Hola nombre del servidor lógico SQL Azure.

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
Puede comprobar Hola datos se exportaron correctamente, abra el archivo nuevo de hello. datos de Hello en el archivo hello deben coincidir con el texto hello siguiente, pero es probable que se va a ordenar en un orden diferente:

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

### <a name="export-hello-results-of-a-query"></a>Exportar resultados de Hola de una consulta
Puede usar hello **queryout** función de los resultados de hello tooexport de bcp de una consulta en lugar de exportar toda la tabla Hola. 

## <a name="next-steps"></a>Pasos siguientes
Para obtener información general sobre la carga, vea [Carga de datos en SQL Data Warehouse][Load data into SQL Data Warehouse].
Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de Almacenamiento de datos SQL][SQL Data Warehouse development overview].
Consulte la [información general sobre las tablas][Table Overview] o la [sintaxis de CREATE TABLE][CREATE TABLE syntax] para obtener más información sobre cómo crear una tabla en SQL Data Warehouse.

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
