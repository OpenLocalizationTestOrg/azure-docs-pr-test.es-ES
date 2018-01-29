---
title: Carga de datos desde un archivo .csv en Azure SQL Database (bcp) | Microsoft Docs
description: "Para un tamaño de datos pequeño, utiliza bcp para importar datos en Base de datos SQL de Azure."
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: On Demand
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 2f00a740b3cc59c4e7b3b378c06cfa8cb05e8380
ms.sourcegitcommit: e5355615d11d69fc8d3101ca97067b3ebb3a45ef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/31/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a>Carga de datos desde CSV en Azure SQL Database (archivos planos)
Puede utilizar la herramienta de línea de comandos bcp para importar datos desde un archivo CSV en Base de datos SQL de Azure.

## <a name="before-you-begin"></a>Antes de empezar
### <a name="prerequisites"></a>Requisitos previos
Para completar los pasos de este artículo, necesitará lo siguiente:

* Un servidor lógico de Base de datos SQL de Azure y una base de datos
* La utilidad de línea de comandos bcp instalada
* La utilidad de línea de comandos sqlcmd instalada

Puede descargar las utilidades bcp y SQLCMD del [Centro de descarga de Microsoft][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>Datos en los formatos ASCII o UTF-16
Si va a probar este tutorial con sus propios datos, estos deben utilizar la codificación ASCII o UTF-16, ya que bcp no admite UTF-8. 

## <a name="1-create-a-destination-table"></a>1. Creación de una tabla de destino.
Defina una tabla en SQL Database como tabla de destino. Las columnas de la tabla deben corresponder con los datos de cada fila del archivo de datos.

Para crear una tabla, abra un símbolo del sistema y use sqlcmd.exe para ejecutar el comando siguiente:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
"
```


## <a name="2-create-a-source-data-file"></a>2. Creación de un archivo de datos de origen
Abra el Bloc de notas y copie las líneas de datos siguientes en un nuevo archivo de texto y, después, guarde este archivo en el directorio temporal local, C:\Temp\DimDate2.txt. Estos datos están en formato ASCII.

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

(Opcional) Para exportar sus propios datos desde una base de datos de SQL Server, abra un símbolo del sistema y ejecute el comando siguiente. Reemplace TableName, ServerName, DatabaseName, Username y Password por su propia información.

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-the-data"></a>3. Carga de los datos
Para cargar los datos, abra un símbolo del sistema y ejecute el comando siguiente, pero reemplace los valores de nombre de servidor, nombre de base de datos, nombre de usuario y contraseña por su propia información.

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

Utilice este comando para comprobar que los datos se cargaron correctamente

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

El resultado debería ser similar a este:

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

## <a name="next-steps"></a>Pasos siguientes
Para migrar una base de datos de SQL Server, consulte el artículo sobre la [migración de una base de datos de SQL Server](sql-database-cloud-migrate.md).

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
