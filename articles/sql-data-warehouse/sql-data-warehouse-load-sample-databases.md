---
title: datos de ejemplo de aaaLoad en almacenamiento de datos SQL | Documentos de Microsoft
description: Carga de datos de ejemplo en Almacenamiento de datos SQL
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 3459c42f3aae51c27fd35db7874faf99e1e577e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a>Carga de datos de ejemplo en Almacenamiento de datos SQL
Siga estas tooload pasos sencillos y base de datos de ejemplo Adventure Works de Hola de consultas. Estas secuencias de comandos en primer lugar utilizan sqlcmd toorun SQL que se crea tablas y vistas. Una vez que se han creado las tablas, las secuencias de comandos de hello utilizará los datos de tooload de bcp.  Si aún no tiene sqlcmd y bcp instalado, siga estos vínculos demasiado[instalar bcp] [ install bcp] y demasiado[instalar sqlcmd][install sqlcmd].

## <a name="load-sample-data"></a>Carga de datos de ejemplo
1. Descargar hello [Scripts de ejemplo de Adventure Works para almacenamiento de datos SQL] [ Adventure Works Sample Scripts for SQL Data Warehouse] archivo zip.
2. Extraiga los archivos de hello del directorio de tooa zip descargado en el equipo local.
3. Edite Hola extraído archivo aw_create.bat y establezca Hola después de las variables que se encuentra al principio de hello del archivo de Hola.  No ser seguro tooleave ningún espacio en blanco entre ="hello" y el parámetro hello.  A continuación, puede ver ejemplos del aspecto que deberían tener las modificaciones.
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. Desde un símbolo del sistema de Windows, ejecute aw_create.bat Hola editado.  Asegúrese de que se encuentra en el directorio de Hola donde guardó la versión editada de aw_create.bat.
   Este script le permitirá hacer lo siguiente:
   
   * Anular cualquier tabla o vista de Adventure Works que ya exista en la base de datos.
   * Crear vistas y tablas de Adventure Works Hola
   * Cargar cada tabla de Adventure Works con bcp.
   * Validar Hola recuentos de filas para cada tabla de Adventure Works
   * Recopilar estadísticas en cada columna de cada tabla de Adventure Works.

## <a name="query-sample-data"></a>Datos de ejemplo de consultas
Una vez que carga algunos datos de ejemplo en Almacenamiento de datos SQL, puede ejecutar rápidamente algunas consultas.  toorun una consulta, conectar la base de datos de Adventure Works de tooyour recién creado en el almacenamiento de datos de SQL de Azure con Visual Studio como SSDT, como se describe en hello [consulta con Visual Studio] [ query with Visual Studio] documento.

Ejemplo de simple seleccione instrucción tooget toda la información de empleados de Hola Hola:

```sql
SELECT * FROM DimEmployee;
```

Ejemplo de una consulta más compleja con construcciones como toolook GROUP BY en la cantidad total de Hola para todas las ventas en cada día:

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

Ejemplo de una instrucción SELECT con una toofilter de cláusula WHERE las órdenes de antes de una fecha determinada:

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

Almacenamiento de datos SQL admite casi todas las construcciones T-SQL compatibles con SQL Server.  Todas las diferencias existentes se registran en nuestra documentación sobre la [migración del código][migrate code].

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha tenido una oportunidad tootry algunas consultas con datos de ejemplo, consulte cómo demasiado[desarrollar][develop], [cargar][load], o [ migrar] [ migrate] tooSQL almacenamiento de datos.

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip
