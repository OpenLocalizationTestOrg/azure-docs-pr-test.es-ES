---
title: "aaaBest prácticas para almacenamiento de datos de SQL de Azure | Documentos de Microsoft"
description: "Recomendaciones y procedimientos recomendados que debe saber para desarrollar soluciones de Almacenamiento de datos SQL de Azure. Esto le ayudará a tener éxito."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 7b698cad-b152-4d33-97f5-5155dfa60f79
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 1f42908fc03e1ca52278a6853d1afe9543d648b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-sql-data-warehouse"></a>Procedimientos recomendados para Almacenamiento de datos SQL de Azure
Este artículo es una colección de las muchas prácticas recomendadas que le ayudarán a obtener un rendimiento óptimo tooachieve desde el almacenamiento de datos de SQL Azure.  Algunos de los conceptos de hello en este artículo son tooexplain básica y fácil, son más avanzados en otros conceptos y se acaba scratch superficie hello en este artículo.  Hola de este artículo sirve toogive algunos conocimiento básico de orientación y tooraise de toofocus áreas importantes que compilar el almacenamiento de datos.  Cada sección presenta el concepto de tooa y a continuación, elija toomore detallada de los artículos concepto de Hola que cubren de forma más minuciosa.

Si acaba de empezar con el Almacenamiento de datos SQL de Azure, no se preocupe por la amplitud del contenido de este artículo.  secuencia de Hola de temas de hello es principalmente en orden de Hola de importancia.  Si inicias centrándose en hello primero algunos conceptos, estará en buen estado.  Según se vaya familiarizando y se sienta cómodo con SQL Date Warehouse, vuelva y eche un vistazo a los demás temas.  No tarda largos para todo toomake sentido.

## <a name="reduce-cost-with-pause-and-scale"></a>Menos costos gracias a las características de pausa y escalado
Una característica clave de almacenamiento de datos SQL es Hola capacidad toopause cuando no se usa, que se deja de facturar Hola de recursos de proceso.  Otra característica clave es tooscale recursos de hello capacidad.  Poner en pausa y ajuste de escala se pueden realizar a través del portal de Azure de Hola o mediante comandos de PowerShell.  Familiarizarse con estas características que pueden reducir en gran medida el costo de Hola de su almacén de datos cuando no está en uso.  Si desea que siempre el almacenamiento de datos accesibles, puede que desee tooconsider reduce verticalmente el tamaño más pequeño toohello, un DW100 en lugar de poner en pausa.

Consulte también [Pausa del proceso][Pause compute resources], [Reanudación del proceso][Resume compute resources], [Escalado de proceso].

## <a name="drain-transactions-before-pausing-or-scaling"></a>Vaciado de las transacciones antes de aplicar la pausa o el escalado
Al pausar o escalar el almacenamiento de datos de SQL, entre bastidores de hello que las consultas se cancelan cuando se inicia Hola pausar o escalar la solicitud.  Cancelar una consulta SELECT simple es una operación rápida y no tiene casi ningún impacto toohello tarda toopause o escala la instancia.  Sin embargo, consultas transaccionales, que modifica la estructura de datos u Hola de datos de hello, no pueden ser capaz de toostop rápidamente.  **Por definición, las consultas sobre transacciones deben completarse íntegramente o deshacerse los cambios.**  Revertir el trabajo Hola completado por una consulta transaccional puede tomar como larga, o incluso más, cambio original Hola Hola consulta se había aplicado.  Por ejemplo, si se cancela una consulta que estaba eliminando filas y ya se ha ejecutado durante una hora, pudieron tomar Hola sistema un hora tooinsert Hola atrás las filas que se eliminaron.  Si ejecuta pausa o un ajuste de escala mientras las transacciones están en tránsito, la pausa o escalar puede parecer tootake mucho tiempo porque pausar y ajuste de escala con toowait para toocomplete de reversión de Hola para poder continuar.

Consulte también [Transacciones en SQL Data Warehouse][Understanding transactions], [Optimización de transacciones en SQL Data Warehouse][Optimizing transactions]

## <a name="maintain-statistics"></a>Mantenimiento de estadísticas
A diferencia de SQL Server, que automáticamente detecta y crea o actualiza las estadísticas en columnas, SQL Data Warehouse requiere el mantenimiento manual de las estadísticas.  Mientras que tenemos previsto toochange se optimizan en hello futura, para ahora le interesará toomaintain su tooensure de estadísticas que Hola planes del almacén de datos de SQL.  planes de Hello creados por el optimizador de hello solo son tan eficaces como las estadísticas disponibles de Hola.  **Las estadísticas muestreadas en todas las columnas es una manera sencilla de tooget inició la creación con las estadísticas.**  Es igualmente importante tooupdate estadísticas como cambios significativos ocurrir tooyour datos.  Un enfoque conservador puede ser tooupdate las estadísticas de cada día o después de cada carga.  Siempre hay ventajas y desventajas de rendimiento y Hola costo toocreate y actualice las estadísticas. Si encuentra está tardando demasiado toomaintain todas las estadísticas, puede que desee tootry toobe más selectivo con respecto a las columnas que tienen estadísticas o las columnas que necesita una actualización frecuente.  Por ejemplo, conviene tooupdate columnas de fecha, donde pueden ser nuevos valores agregados, diaria. **Dispondrá de hello máximas ventajas por cuentan con estadísticas en las columnas que intervienen en las combinaciones, las columnas utilizadas en Hola donde se encuentran cláusula y columnas en GROUP BY.**

Consulte también [Administración de estadísticas en tablas en SQL Data Warehouse][Manage table statistics], [CREATE STATISTICS][CREATE STATISTICS] y [UPDATE STATISTICS][UPDATE STATISTICS]

## <a name="group-insert-statements-into-batches"></a>Agrupación de instrucciones INSERT en lotes
Una tabla pequeña tooa de carga de un solo uso con una instrucción INSERT o incluso una recarga periódica de una búsqueda puede realizar correctamente para sus necesidades con una instrucción como `INSERT INTO MyLookup VALUES (1, 'Type 1')`.  Sin embargo, si necesita tooload miles o millones de filas a lo largo del día de hello, es posible que las inserciones de singleton solo no pueden seguir.  En su lugar, desarrolle los procesos para que escriben tooa archivo y otro proceso periódicamente vengan y carga este archivo.

Consulte también [INSERT][INSERT]

## <a name="use-polybase-tooload-and-export-data-quickly"></a>Use PolyBase tooload y exportar datos rápidamente
Almacenamiento de datos SQL admite la carga y exportación de datos con varias herramientas, como Data Factory de Azure, PolyBase y BCP.  Para pequeñas cantidades de datos donde el rendimiento no es clave, cualquier herramienta le sirve.  Sin embargo, cuando se cargan o exportar grandes volúmenes de datos o se necesita un rendimiento rápido, PolyBase es Hola mejor opción.  PolyBase es tooleverage diseñada Hola MPP (masivo procesamiento en paralelo) arquitectura de almacenamiento de datos SQL y, por tanto, se cargará y exportar magnitudes de datos más rápido que cualquier otra herramienta.  Lo que haya cargado con PolyBase se ejecuta con la consulta CTAS o de selección.  **Usar CTAS minimizará el registro de transacciones y tooload de manera más rápida de hello los datos.**  Data Factory de Azure también admite datos cargados con PolyBase.  PolyBase admite distintos de formatos de archivo, como Gzip.  **rendimiento de toomaximize cuando ocupando gzip archivos de texto, salto en 60 o más archivos toomaximize el paralelismo de la carga.**  Para conseguir un rendimiento total más rápido, cargue los datos simultáneamente.

Consulte también [Carga de datos en Azure SQL Data Warehouse][Load data], [Guía para el uso de PolyBase en SQL Data Warehouse][Guide for using PolyBase], [Azure SQL Data Warehouse loading patterns and strategies][Azure SQL Data Warehouse loading patterns and strategies] (Patrones y estrategias de carga de Azure SQL Data Warehouse), [Carga de datos en SQL Data Warehouse con Data Factory][Load Data with Azure Data Factory], [Movimiento de datos hacia y desde SQL Data Warehouse mediante Azure Data Factory][Move data with Azure Data Factory], [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT], [Create Table As Select (CTAS) en SQL Data Warehouse][Create table as select (CTAS)]

## <a name="load-then-query-external-tables"></a>Carga y consulta de tablas externas
Polybase, también conocido como tablas externas, puede ser datos de tooload de manera más rápidos de hello, no es óptimo para las consultas. Las tablas de Polybase en SQL Data Warehouse solo admiten actualmente archivos de blobs de Azure. Estos archivos no tienen recursos de proceso que los respalde.  Como resultado, almacenamiento de datos de SQL no se puede descargar este trabajo y, por tanto, debe leer todo el archivo hello cargándolo tootempdb datos de pedidos tooread Hola.  Por lo tanto, si tiene varias consultas que consultará estos datos, es mejor tooload estos datos una vez y tiene consultas Utilice tabla local Hola.

Consulte también [Guía para el uso de PolyBase en SQL Data Warehouse][Guide for using PolyBase]

## <a name="hash-distribute-large-tables"></a>Distribución Hash para tablas grandes
De forma predeterminada, las tablas se distribuyen según el patrón Round Robin.  Esto facilita a tooget de los usuarios que se inició la creación de tablas sin necesidad de toodecide cómo deben distribuirse sus tablas.  Las tablas round robin pueden ser suficientes para algunas cargas de trabajo, pero en la mayoría de los casos, la selección de una columna de distribución funcionará mucho opción.  Hola ejemplo más común de cuando una tabla distribuida por una columna ahora superan una tabla de operación por turnos es cuando se combinan dos tablas de hechos de gran tamaño.  Por ejemplo, si tiene una tabla de pedidos, que se distribuye por id_pedido, y una tabla de transacciones, que también se distribuye por id_pedido, cuando se une a la tabla de transacciones de pedidos tabla tooyour en id_pedido, esta consulta se convierte en una consulta de paso a través, lo que significa se eliminan las operaciones de movimiento de datos.  Menos pasos suponen consultas más rápidas.  Menos movimiento de datos también se traduce en consultas más rápidas.  En esta explicación es sólo la punta superficie Hola. Al cargar una tabla distribuida, asegúrese de que los datos entrantes no se ordenan en la clave de distribución de hello tal como esto reduce la carga.  Vea Hola siguiente vincula durante gran parte más detalles sobre cómo seleccionar una columna de distribución puede mejorar el rendimiento, así como el modo toodefine una tabla en la cláusula WITH de saludo de la instrucción CREATE TABLES distribuida.

Consulte también [Información general de tablas en SQL Data Warehouse][Table overview], [Distribución de tablas en SQL Data Warehouse][Table distribution], [Selección de la distribución de tablas][Selecting table distribution], [CREATE TABLE][CREATE TABLE], [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="do-not-over-partition"></a>Sin particiones excesivas
Crear particiones de datos puede ser muy eficaz para el mantenimiento de los datos mediante la modificación de particiones o exámenes de optimización, pero el exceso de particiones puede ralentizar las consultas.  A menudo una estrategia de división con granularidad alta que puede funcionar bien en SQL Server no funciona correctamente en SQL Data Warehouse.  Tener demasiados particiones también puede reducir efectividad de Hola de índices de almacén de columnas agrupado si cada partición tiene menos de 1 millón de filas.  Tenga en cuenta que entre bastidores de hello, almacenamiento de datos SQL divide los datos automáticamente en 60 bases de datos, por lo que si crea una tabla con 100 particiones, se produce realmente en 6000 particiones.  Cada carga de trabajo es diferente para que hello mejor consejo es tooexperiment con las particiones toosee qué funciona mejor para la carga de trabajo.  Considere la posibilidad de reducir la granularidad respecto a lo que le funcionaba en SQL Server.  Por ejemplo, puede usar particiones semanales o mensuales, en lugar de diarias.

Consulte también cómo [Creación de particiones de tablas en SQL Data Warehouse][Table partitioning]

## <a name="minimize-transaction-sizes"></a>Reducción del tamaño de las transacciones
Las instrucciones INSERT, UPDATE Y DELETE se ejecutan en las transacciones y, cuando fallan, deben deshacerse.  Hola toominimize posible para una reversión largo, minimizar los tamaños de transacción siempre que sea posible.  Puede hacerlo si divide las instrucciones INSERT, UPDATE y DELETE en partes.  Por ejemplo, si tiene una instrucción INSERT que espera tootake 1 hora, si es posible, dividir Hola INSERT en 4 partes, que se ejecutarán cada uno de ellos en 15 minutos.  Aproveche el registro mínimo algunos casos especiales, como CTAS, TRUNCATE, DROP TABLE o INSERT tooempty tablas tooreduce riesgo de reversión.  Reversiones de tooeliminate de otra manera es toouse metadatos solo las operaciones como la modificación de particiones para la administración de datos.  Por ejemplo, en su lugar que ejecutan una toodelete de la instrucción DELETE todas las filas en una tabla que era Hola order_date en octubre de 2001, puede dividir los datos mensuales y enciéndala partición Hola con datos de una partición vacía de otra tabla (vea ALTER Ejemplos de la tabla).  Para las tablas sin particiones considere utilizando una CTAS toowrite Hola de datos que desee tookeep en una tabla, en lugar de usar DELETE.  Si un CTAS toma Hola la misma cantidad de tiempo, es un toorun operación mucho más segura ya que tiene el registro de transacciones mínimas y puede cancelarse rápidamente si es necesario.

Consulte también [Transacciones en SQL Data Warehouse][Understanding transactions], [Optimización de transacciones para SQL Data Warehouse][Optimizing transactions], [Creación de particiones de tablas en SQL Data Warehouse][Table partitioning], [TRUNCATE TABLE][TRUNCATE TABLE], [ALTER TABLE][ALTER TABLE], [Create table as select (CTAS) en SQL Data Warehouse][Create table as select (CTAS)]

## <a name="use-hello-smallest-possible-column-size"></a>Usar tamaño más pequeño de columnas posible de Hola
Al definir el DDL, con tipo datos más pequeño, Hola que será compatible con los datos mejorará el rendimiento de las consultas.  Esto tiene especial importancia para las columnas CHAR y VARCHAR.  Si el valor más largo de hello en una columna es de 25 caracteres, a continuación, defina la columna como VARCHAR(25).  Evite la definición de la longitud de todos los caracteres columnas tooa predeterminados.  Defina las columnas como VARCHAR en lugar de NVARCHAR cuando no se necesite nada más.

Consulte también [Información general de tablas en SQL Data Warehouse][Table overview], [Tipos de datos de las tablas en SQL Data Warehouse][Table data types], [CREATE TABLE][CREATE TABLE]

## <a name="use-temporary-heap-tables-for-transient-data"></a>Uso de tablas de apilamiento temporal para datos transitorios
Cuando temporalmente aterrizaje datos en almacenamiento de datos de SQL, es posible que el uso de una tabla de montón hará que Hola proceso general con mayor rapidez.  Si va a cargar datos toostage solo antes de ejecutar transformaciones más, cargar Hola tabla tooheap tabla será mucho más rápido que cargar Hola datos tooa en el clúster de tabla de almacén de columnas.  Además, cargar datos tooa tabla temp también cargará mucho más rápido que cargar un almacenamiento de tabla toopermanent.  Tablas temporales comenzar con un símbolo "#" y solo son accesibles por sesión de Hola que crea, por lo que solo funcionen en escenarios limitados.   Tablas de montón se definen en la cláusula WITH de Hola de CREATE TABLE.  Si utiliza una tabla temporal, recuerde demasiado toocreate estadísticas en la tabla temporal.

Consulte también [Tablas temporales en SQL Data Warehouse][Temporary tables], [CREATE TABLE][CREATE TABLE], [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="optimize-clustered-columnstore-tables"></a>Optimización de tablas de almacén de columnas agrupadas
Índices de almacén de columnas agrupado son una de las maneras más eficientes de hello que puede almacenar los datos en el almacén de datos de SQL Azure.  De forma predeterminada, las tablas de Almacenamiento de datos SQL se crean como almacén de columnas agrupadas.  tooget Hola un rendimiento óptimo para las consultas en tablas de almacén de columnas, de gran calidad buena segmento es importante.  Cuando las filas se escriben toocolumnstore tablas bajo presión de memoria, puede sufrir calidad de segmento de almacén de columnas.  La calidad de segmento se puede medir por el número de filas de un grupo de filas comprimido.  Vea hello [causas de bajo almacén de columnas de índice calidad] [ Causes of poor columnstore index quality] en hello [índices de tabla] [ Table indexes] artículo para obtener instrucciones paso a paso en detectar y mejorar la calidad de segmento para las tablas de almacén de columnas agrupado.  Dado que segmentos de almacén de columnas de alta calidad es importante, es identificadores de toouse a los usuarios una buena idea que se encuentran en la clase de recurso mediana o grande de hello para cargar los datos.  Hola menos a Dwu usar, Hola mayor Hola clase de recurso le interesará tooyour tooassign carga de usuario.

Puesto que las tablas de almacén de columnas por lo general no insertan datos en un segmento de almacén de columnas comprimido hasta que hay más de 1 millón de filas por tabla y cada tabla de almacenamiento de datos SQL se divide en 60 tablas, como regla general, las tablas de almacén de columnas no beneficiarán una consulta a menos que la tabla de hello tiene más de 60 millones de filas.  Para la tabla con menos de 60 millones de filas, puede que no tenga ningún sentido toohave un índice de almacén de columnas.  Pero tampoco molesta.  Además, si se crean particiones de los datos, a continuación, le interesará tooconsider que cada partición necesitará toobenefit de toohave 1 millón de filas de un índice de almacén de columnas agrupado.  Si una tabla tiene 100 particiones, entonces será necesario al menos 6 millones de toohave toobenefit de filas desde un almacén de columnas agrupado (60 distribuciones * 100 particiones * 1 millón de filas).  Si la tabla no tiene 6 millones de filas en este ejemplo, reduzca el número de Hola de particiones o considere la posibilidad de usar una tabla de montón en su lugar.  También puede ser que vale la pena toosee experimentando si se puede obtener un mejor rendimiento con una tabla de montón con los índices secundarios en lugar de una tabla de almacén de columnas.  Las tablas de almacén de columnas aún no admiten índices secundarios.

Al consultar una tabla de almacén de columnas, las consultas se ejecutarán más rápido si selecciona solo las columnas de Hola que necesita.  

Consulte también [Indexación de tablas en SQL Data Warehouse][Table indexes], [Guía de índices de almacén de columnas][Columnstore indexes guide] y [Regeneración de índices de almacén de columnas][Rebuilding columnstore indexes]

## <a name="use-larger-resource-class-tooimprove-query-performance"></a>Use el mayor rendimiento de consulta tooimprove los recursos (clase)
Almacenamiento de datos de SQL utiliza grupos de recursos como un tooqueries de memoria de manera tooallocate.  Desde el principio de hello, todos los usuarios se asignan toohello clase de recursos pequeño que concede 100 MB de memoria por la distribución.  Puesto que siempre hay 60 distribuciones y cada distribución tiene un mínimo de 100 MB, memoria total del sistema Hola amplia asignación es 6.000 MB o justo debajo de 6 GB.  Algunas consultas, como combinaciones de gran tamaño o tablas de almacén de columnas de tooclustered de carga, puede beneficiarse de las asignaciones de memoria mayor.  Algunas consultas, como los exámenes puros, no sufrirán cambios.  Hola flip lado, utilizando las clases de recursos mayor afecta simultaneidad, por lo que deberá tootake esto en cuenta antes de mover todos de la clase de recursos grande de usuarios tooa.

Consulte también [Simultaneidad y administración de cargas de trabajo en SQL Data Warehouse][Concurrency and workload management]

## <a name="use-smaller-resource-class-tooincrease-concurrency"></a>Usar la clase de recursos menor tooIncrease simultaneidad
Si observa que las consultas de usuario parecen toohave un retraso largo, es posible los usuarios se ejecutan en las clases de recursos más grandes y consumen mucha ranuras de simultaneidad causando otro tooqueue consultas una.  toosee si se pone en cola las consultas de los usuarios, ejecute `SELECT * FROM sys.dm_pdw_waits` toosee si no se devuelve ninguna fila.

Consulte también [Simultaneidad y administración de cargas de trabajo en SQL Data Warehouse][Concurrency and workload management], [sys.dm_pdw_waits][sys.dm_pdw_waits]

## <a name="use-dmvs-toomonitor-and-optimize-your-queries"></a>Use DMV toomonitor y optimizar las consultas
Almacenamiento de datos de SQL tiene varias DMV que pueden ser la ejecución de la consulta de toomonitor usado.  Hola supervisión siguiente artículo guiará a través de instrucciones paso a paso sobre cómo consultar toolook detalles Hola de una ejecución.  con la opción de etiqueta de hello con las consultas puede ayudar a las consultas de búsqueda tooquickly en estas DMV.

Consulte también [Supervisión de la carga de trabajo mediante DMV][Monitor your workload using DMVs], [LABEL][LABEL], [OPTION][OPTION], [sys.dm_exec_sessions][sys.dm_exec_sessions], [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests], [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps], [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], [sys.dm_pdw_dms_workers], [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN], [sys.dm_pdw_waits][sys.dm_pdw_waits]

## <a name="other-resources"></a>Otros recursos:
Consulte también el artículo [Solución de problemas de Azure SQL Data Warehouse][Troubleshooting] para conocer los problemas comunes y sus soluciones.

Si no encontró lo que buscaba en este artículo, pruebe a usar "Buscar documentos" en el lado izquierdo de Hola de este toosearch página todos los de documentos de almacenamiento de datos de SQL Azure Hola Hola.  Hola [foro de MSDN de almacenamiento de datos de SQL de Azure] [ Azure SQL Data Warehouse MSDN Forum] se crea como un lugar para que tooask preguntas de los usuarios tooother y toohello grupo de producto de almacenamiento de datos de SQL.  Este tooensure foro que se van a responder las preguntas por otro usuario o uno de nosotros nos supervisar de forma activa.  Si prefiere tooask sus preguntas acerca del desbordamiento de pila, también tenemos una [foro de desbordamiento de Azure SQL Data Warehouse pila][Azure SQL Data Warehouse Stack Overflow Forum].

Por último, use hello [comentarios de almacenamiento de datos de SQL Azure] [ Azure SQL Data Warehouse Feedback] toomake característica solicitudes de página.  Añadir sus solicitudes o valoraciones positivas sobre otras solicitudes realmente nos ayuda a priorizar las características.

<!--Image references-->

<!--Article references-->
[Create a support ticket]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Create table as select (CTAS)]: ./sql-data-warehouse-develop-ctas.md
[Table overview]: ./sql-data-warehouse-tables-overview.md
[Table data types]: ./sql-data-warehouse-tables-data-types.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexes]: ./sql-data-warehouse-tables-index.md
[Causes of poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuilding columnstore indexes]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Manage table statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary tables]: ./sql-data-warehouse-tables-temporary.md
[Guide for using PolyBase]: ./sql-data-warehouse-load-polybase-guide.md
[Load data]: ./sql-data-warehouse-overview-load.md
[Move data with Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[Load data with Azure Data Factory]: ./sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Monitor your workload using DMVs]: ./sql-data-warehouse-manage-monitor.md
[Pause compute resources]: ./sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Resume compute resources]: ./sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[Escalado de proceso]: ./sql-data-warehouse-manage-compute-overview.md#scale-compute
[Understanding transactions]: ./sql-data-warehouse-develop-transactions.md
[Optimizing transactions]: ./sql-data-warehouse-develop-best-practices-transactions.md
[Troubleshooting]: ./sql-data-warehouse-troubleshoot.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->
[ALTER TABLE]: https://msdn.microsoft.com/library/ms190273.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[CREATE TABLE AS SELECT]: https://msdn.microsoft.com/library/mt204041.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: https://msdn.microsoft.com/library/mt204017.aspx
[INSERT]: https://msdn.microsoft.com/library/ms174335.aspx
[OPTION]: https://msdn.microsoft.com/library/ms190322.aspx
[TRUNCATE TABLE]: https://msdn.microsoft.com/library/ms177570.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx
[sys.dm_exec_sessions]: https://msdn.microsoft.com/library/ms176013.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_request_steps]: https://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: https://msdn.microsoft.com/library/mt203889.aspx
[sys.dm_pdw_dms_workers]: https://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_waits]: https://msdn.microsoft.com/library/mt203893.aspx
[Columnstore indexes guide]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
[Selecting table distribution]: https://blogs.msdn.microsoft.com/sqlcat/2015/08/11/choosing-hash-distributed-table-vs-round-robin-distributed-table-in-azure-sql-dw-service/
[Azure SQL Data Warehouse Feedback]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Azure SQL Data Warehouse MSDN Forum]: https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=AzureSQLDataWarehouse
[Azure SQL Data Warehouse Stack Overflow Forum]:  http://stackoverflow.com/questions/tagged/azure-sqldw
[Azure SQL Data Warehouse loading patterns and strategies]: https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies
