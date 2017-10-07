---
title: "aaaGuide para usar PolyBase en el almacén de datos de SQL | Documentos de Microsoft"
description: Directrices y recomendaciones para el uso de PolyBase en escenarios de Almacenamiento de datos SQL.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: b05e4c5d528f2fe1c60d6855b5333065f0c908ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a>Guía para el uso de PolyBase en Almacenamiento de datos SQL
Esta guía ofrece información práctica para el uso de PolyBase en el Almacenamiento de datos SQL.

tooget iniciado, vea hello [carga los datos con PolyBase] [ Load data with PolyBase] tutorial.

## <a name="rotating-storage-keys"></a>Rotación de claves de almacenamiento
Desde hora tootime le interesará almacenamiento de blobs de toochange Hola acceso tooyour clave por motivos de seguridad.

Hola tooperform de manera más elegante que esta tarea es toofollow un proceso conocido como "rotación de claves de Hola". Puede que haya observado que dispone de dos claves de almacenamiento para su cuenta de almacenamiento de blobs. Esto es para que puede realizar la transición.

La rotación de las claves de la cuenta de almacenamiento de Azure es un proceso sencillo de tres pasos

1. Cree la segunda credencial de ámbito de la base de datos basada en clave de acceso de almacenamiento secundaria Hola
2. Crear el segundo origen de datos externo basado en esta nueva credencial
3. Quitar y crear tablas externas Hola que señala toohello nuevo origen de datos externo

Cuando haya migrado todas las tablas externas toohello nuevo origen de datos externo, a continuación, puede realizar Hola limpiar tareas:

1. Quitar el primer origen de datos externo
2. Quitar la base de datos primer ámbito credencial basada en clave de acceso de almacenamiento principal de Hola
3. Inicie sesión en Azure y regenerar la clave de acceso principal de hello lista para hello vuela

## <a name="query-azure-blob-storage-data"></a>Consulta de datos en el almacenamiento de blobs de Azure
Consultas en tablas externas usar simplemente el nombre de la tabla de hello como si fuese una tabla relacional.

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> Una consulta en una tabla externa puede producir un error de hello *"consulta anulado: se alcanzó el umbral de rechazo de máximo de Hola durante la lectura desde un origen externo"*. Esto indica que sus datos externos contienen registros *con modificaciones* . Un registro de datos se considera 'sucio' si hello, tipos de datos reales/número de columnas no coinciden con definiciones de columna de Hola de tabla externa de Hola o datos hello no cumplen el formato de archivo externo especificado toohello. toofix esto, asegúrese de que la tabla externa y las definiciones de formato de archivo externo son correctas y que los datos externos ajustan a las definiciones de toothese. En caso de que un subconjunto de registros de datos externos están desfasadas, puede elegir tooreject estos registros para las consultas con las opciones de rechazo de hello en CREATE DDL de tabla externa.
> 
> 

## <a name="load-data-from-azure-blob-storage"></a>Carga de datos del almacenamiento de blobs de Azure
Este ejemplo carga datos de la base de datos Data Warehouse tooSQL de almacenamiento de blobs de Azure.

Almacenar datos directamente quita Hola tiempo de transferencia de datos para las consultas. Almacenamiento de datos con un índice columnstore mejora el rendimiento de consultas para las consultas de análisis por seguridad too10x.

Este ejemplo utiliza datos de tooload de instrucción CREATE TABLE AS SELECT Hola. nueva tabla de Hello hereda columnas de hello mencionadas en consulta Hola. Definición de la tabla externa de hello hereda los tipos de datos de Hola de esas columnas.

CREATE TABLE AS SELECT es un rendimiento muy instrucción de Transact-SQL que carga datos de hello en paralelo tooall Hola nodos de almacenamiento de datos SQL de ejecución.  Se desarrolló originalmente para el motor de procesamiento paralelo masivo (MPP) hello en el sistema de la plataforma de análisis y ahora está en el almacén de datos de SQL.

```sql
-- Load data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

Vea [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].

## <a name="create-statistics-on-newly-loaded-data"></a>Crear estadísticas de los datos recién cargados
Almacenamiento de datos SQL de Azure todavía no permite crear ni actualizar automáticamente las estadísticas.  En orden tooget Hola un mejor rendimiento de las consultas, es importante que las estadísticas se crean en todas las columnas de todas las tablas después de la primera carga de Hola o se producen cambios sustanciales en datos Hola.  Para obtener una explicación detallada de las estadísticas, vea hello [estadísticas] [ Statistics] tema en el grupo de desarrollo de Hola de temas.  A continuación se muestra un ejemplo rápido de cómo cargarán toocreate estadísticas en la tabla de hello en este ejemplo.

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-tooazure-blob-storage"></a>Exportar el almacenamiento de blobs de datos tooAzure
Esta sección muestra cómo el almacenamiento de blobs tooexport datos de tooAzure de almacenamiento de datos SQL. Este ejemplo utiliza CREATE externo TABLE AS SELECT que son una alta rendimiento Transact-SQL instrucción tooexport Hola datos en paralelo desde todos los nodos de proceso de Hola.

Hello en el ejemplo siguiente se crea una tabla externa Weblogs2014 con definiciones de columna y los datos de dbo. Tabla de blogs. definición de tabla externa de Hola se almacena en el almacén de datos de SQL y los resultados de Hola de instrucción SELECT Hola son exportado toohello directory "/ Archivar/log2014 /" en el contenedor de blobs de hello especificado por el origen de datos de Hola. Hola datos se exportan en formato de archivo de texto especificado Hola.

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a>Aislar la carga de usuarios
A menudo hay una necesidad toohave varios usuarios que pueden cargar datos en un almacenamiento de datos de SQL. Dado que hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] requiere permisos de CONTROL de base de datos de hello, terminará con varios usuarios con acceso de control a través de todos los esquemas. toolimit esto, puede usar la instrucción de CONTROL denegar Hola.

Ejemplo: tenemos los esquemas de base de datos schema_A para el departamento A, schema_B para el departamento B y los usuarios de PolyBase user_A y user_B con cargas en los departamentos A y B respectivamente. A ambos se les ha concedido permiso de CONTROL sobre la base de datos.
creadores de Hola de esquema A y B ahora bloquear sus esquemas con DENY:

```sql
   DENY CONTROL ON SCHEMA :: schema_A toouser_B;
   DENY CONTROL ON SCHEMA :: schema_B toouser_A;
```   
 Con esto, userA y UserB deben ahora bloquearse de hello esquema de otro departamento.
 


## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de movimiento de datos de tooSQL almacenamiento de datos, vea hello [información general sobre la migración de datos][data migration overview].

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
