---
title: el archivo de datos de aaaLoad desde archivo CSV en base de datos de SQL de Azure (copia masiva bcp) | Documentos de Microsoft
description: "Para un tamaño de datos pequeños, utiliza datos de tooimport de bcp en la base de datos de SQL Azure."
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
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a>Carga de datos desde CSV en Azure SQL Database (archivos planos)
Puede usar datos de tooimport de utilidad de línea de comandos de hello bcp desde un archivo CSV en la base de datos de SQL Azure.

## <a name="before-you-begin"></a>Antes de empezar
### <a name="prerequisites"></a>Requisitos previos
Hola toocomplete los pasos de este artículo, es necesario:

* Un servidor lógico de Base de datos SQL de Azure y una base de datos
* utilidad de línea de comandos de Hello bcp instalado
* utilidad de línea de comandos de sqlcmd Hola instalada

Puede descargar las utilidades de bcp y sqlcmd de Hola de hello [Microsoft Download Center][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>Datos en los formatos ASCII o UTF-16
Si está tratando de este tutorial con sus propios datos, necesita los datos toouse Hola ASCII o la codificación UTF-16 dado bcp no es compatible con UTF-8. 

## <a name="1-create-a-destination-table"></a>1. Creación de una tabla de destino.
Definir una tabla de base de datos de SQL como tabla de destino de Hola. columnas de Hello en la tabla de hello deben corresponder toohello datos en cada fila de su archivo de datos.

toocreate una tabla, abra un símbolo del sistema y use sqlcmd.exe toorun Hola siguiente comando:

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

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a>3. Cargar datos de Hola
datos de hello tooload, abra un símbolo del sistema y ejecute hello siguiente comando, reemplazando los valores de hello para nombre del servidor, nombre de base de datos, nombre de usuario y contraseña con su propia información.

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

Utilice este comando tooverify hello se cargaron correctamente los datos

```bcp
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

## <a name="next-steps"></a>Pasos siguientes
toomigrate una base de datos de SQL Server, vea [migración de base de datos de SQL Server](sql-database-cloud-migrate.md).

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
