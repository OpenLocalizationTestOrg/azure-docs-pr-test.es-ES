---
title: "límites de capacidad de almacenamiento de datos aaaSQL | Documentos de Microsoft"
description: "Valores máximos para las conexiones, bases de datos, tablas y consultas de Almacenamiento de datos SQL."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: e1eac122-baee-4200-a2ed-f38bfa0f67ce
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 8619cb997f0955d649d447cb8ca15cd742cc70b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-capacity-limits"></a>Límites de capacidad de Almacenamiento de datos SQL
Hello en las tablas siguientes contienen valores de hello máximo permitido para diversos componentes de almacenamiento de datos de SQL Azure.

## <a name="workload-management"></a>Administración de cargas de trabajo
| Categoría | Descripción | Máxima |
|:--- |:--- |:--- |
| [Unidades de almacenamiento de datos (DWU)][Data Warehouse Units (DWU)] |Máximo de DWU para una sola instancia de SQL Data Warehouse |6000 |
| [Unidades de almacenamiento de datos (DWU)][Data Warehouse Units (DWU)] |Máximo de DWU para un único servidor SQL |6000 de forma predeterminada<br/><br/> De forma predeterminada, cada servidor de SQL server (por ejemplo, myserver.database.windows.net) tiene una cuota de DTU de 45.000 que permite que un too6000 DWU. Esta cuota es simplemente un límite de seguridad. Puede aumentar la cuota por [crear una incidencia de soporte técnico] [ creating a support ticket] y seleccionando *cuota* como tipo de solicitud de saludo.  toocalculate necesita, multiplique la DTU Hola 7.5 por total de hello DWU necesarios. Puede ver el consumo de DTU actual de la hoja de hello SQL server en el portal de Hola. Bases de datos en pausa y continuó cuentan para la cuota de DTU Hola. |
| Conexión de base de datos |Sesiones abiertas simultáneas |1024<br/><br/>Se admite un máximo de conexiones activas de 1024, cada uno de los cuales puede enviar la base de datos del almacén de datos SQL de tooa de solicitudes en hello mismo tiempo. Tenga en cuenta que no hay límites en hello número de consultas que realmente se pueden ejecutar simultáneamente. Cuando se supera el límite de simultaneidad de hello, solicitud de hello entra en una cola interna mientras espera a que toobe procesado. |
| Conexión de base de datos |Memoria máxima para instrucciones preparadas |20 MB |
| [Administración de cargas de trabajo][Workload management] |N.º máximo de consultas simultáneas |32<br/><br/> De forma predeterminada, SQL Data Warehouse puede ejecutar un máximo de 32 consultas simultáneas y pone en cola las restantes.<br/><br/>puede disminuir el nivel de simultaneidad de Hello cuando los usuarios se asignan tooa superior clase de recursos o al almacenamiento de datos de SQL está configurado con DWU baja. Algunas consultas, como las consultas DMV, siempre se permiten toorun. |
| [Tempdb][Tempdb] |Tamaño máximo de Tempdb |399 GB por DW100. Por lo tanto en Tempdb DWU1000 es TB de tamaño too3.99 |

## <a name="database-objects"></a>Objetos de base de datos
| Categoría | Descripción | Máxima |
|:--- |:--- |:--- |
| Base de datos |Tamaño máximo |240 TB comprimidos en un disco<br/><br/>Este espacio es independiente del espacio de tempdb o de registro y, por tanto, este espacio es tablas toopermanent dedicado.  La compresión del almacén de columnas en clúster se estima en 5X.  Esta compresión permite Hola base de datos toogrow tooapproximately 1 PB cuando todas las tablas de almacén de columnas agrupado (tipo de tabla predeterminado de hello). |
| Tabla |Tamaño máximo |60 TB comprimidos en disco |
| Tabla |Tablas por base de datos |2 mil millones |
| Tabla |Columnas por tabla |1024 columnas |
| Tabla |Bytes por columna |Depende de la columna de [tipo de datos][data type].  El límite es 8000 para los tipos de datos char, 4000 para nvarchar o 2 GB para los tipos de datos MAX. |
| Tabla |Bytes por fila, tamaño definido |8060 bytes<br/><br/>número de Hola de bytes por fila se calcula en hello misma manera que lo es para SQL Server con la compresión de página. Al igual que SQL Server, almacenamiento de datos SQL admite almacenamiento de desbordamiento de fila, lo que habilita **columnas de longitud variable** toobe inserción no consecutiva. Cuando las filas de longitud variable se insertan filas no consecutivas, sólo la raíz de 24 bytes se almacena en el registro principal de Hola. Para obtener más información, vea hello [desbordamiento de fila datos superior a 8 KB] [ Row-Overflow Data Exceeding 8 KB] artículo de MSDN. |
| Tabla |Particiones por tabla |15 000<br/><br/>Para obtener un rendimiento alto, se recomienda minimizando el número de Hola de particiones necesita mientras mantiene la ejecución de sus requisitos empresariales. Como Hola aumenta el número de particiones, sobrecarga de hello para el lenguaje de definición de datos (DDL) y las operaciones de lenguaje de manipulación de datos (DML) crece y provoca un rendimiento más lento. |
| Tabla |Caracteres por valor de límite de partición |4000 |
| Índice |Índices no agrupados por tabla |999<br/><br/>Se aplica solo tablas toorowstore. |
| Índice |Índices agrupados por tabla |1<br><br/>Se aplica a las tablas de almacén de filas y de almacén de columnas de tooboth. |
| Índice |Tamaño de clave de índice |900 bytes<br/><br/>Se aplica solo índices toorowstore.<br/><br/>Si los datos existentes en las columnas de Hola Hola no superar los 900 bytes cuando se crea el índice de hello, pueden crearse índices en columnas varchar con un tamaño máximo de más de 900 bytes. Sin embargo, más adelante se inserte o se producirá un error en las acciones de actualización en las columnas de Hola que provocan el tamaño total de hello tooexceed 900 bytes. |
| Índice |Columnas de clave por índice |16<br/><br/>Se aplica solo índices toorowstore. Los índices de almacén de columnas agrupados incluyen todas las columnas. |
| Estadísticas |Tamaño de hello combina valores de columna. |900 bytes |
| Estadísticas |Columnas por objeto de estadísticas |32 |
| Estadísticas |Estadísticas creadas en columnas por tabla |30 000 |
| Procedimientos almacenados |Niveles máximos de anidamiento |8 |
| Ver |Columnas por vista |1024 |

## <a name="loads"></a>Cargas
| Categoría | Descripción | Máxima |
|:--- |:--- |:--- |
| Cargas de PolyBase |MB por fila |1<br/><br/>Cargas de Polybase tooloading limitado filas ambos menor que 1MB y no se puede cargar tooVARCHR(MAX), nvarchar (max) o varbinary (max).<br/><br/> |

## <a name="queries"></a>Consultas
| Categoría | Descripción | Máxima |
|:--- |:--- |:--- |
| Consultar |Consultas en cola en tablas de usuario |1000 |
| Consultar |Consultas simultáneas en vistas de sistema |100 |
| Consultar |Consultas en cola en vistas de sistema |1000 |
| Consultar |Parámetros máximos |2098 |
| Lote |Tamaño máximo |65 536*4096 |
| Resultados de SELECT |Columnas por fila |4096<br/><br/>Nunca pueden tener más de 4096 columnas por fila en hello seleccione resultado. No hay ninguna garantía de que pueda tener siempre 4096. Si el plan de consulta de hello requiere una tabla temporal, se podrían aplicar 1024 columnas por tabla máximo de Hola. |
| SELECT |Subconsultas anidadas |32<br/><br/>Nunca se pueden tener más de 32 subconsultas anidadas en una instrucción SELECT. No hay ninguna garantía de que siempre pueda tener 32. Por ejemplo, una combinación puede introducir una subconsulta en el plan de consulta de Hola. número de Hola de subconsultas también estar limitado por la memoria disponible. |
| SELECT |Columnas por JOIN |1024 columnas<br/><br/>Nunca pueden tener más de 1024 columnas Hola combinación. No hay ninguna garantía de que siempre pueda tener 1024. Si el plan de combinaciones de hello requiere una tabla temporal con más columnas que el resultado de la combinación de hello, Hola 1024 límite aplica toohello de tabla temporal. |
| SELECT |Bytes por columnas GROUP BY |8060<br/><br/>columnas de Hola de cláusula GROUP BY Hola pueden tener un máximo de 8060 bytes. |
| SELECT |Bytes por columnas ORDER BY |8060 bytes<br/><br/>columnas de Hola de cláusula ORDER BY Hola pueden tener un máximo de 8060 bytes. |
| Identificadores y constantes por instrucción |Número de identificadores y constantes de referencia. |65 535<br/><br/>Almacenamiento de datos SQL limita el número Hola de identificadores y constantes que pueden incluirse en una única expresión de una consulta. Este límite es 65 535 GB. Si se supera este número se produce el error de SQL Server 8632. Para más información, vea [Internal error: An expression services limit has been reached][Internal error: An expression services limit has been reached] (Error interno: se ha alcanzado el límite de servicios de una expresión). |

## <a name="metadata"></a>Metadatos
| Vista de sistema | Número máximo de filas |
|:--- |:--- |
| sys.dm_pdw_component_health_alerts |10.000 |
| sys.dm_pdw_dms_cores |100 |
| sys.dm_pdw_dms_workers |Número total de trabajadores DMS para hello últimas 1000 solicitudes de SQL. |
| sys.dm_pdw_errors |10.000 |
| sys.dm_pdw_exec_requests |10.000 |
| sys.dm_pdw_exec_sessions |10.000 |
| sys.dm_pdw_request_steps |Número total de pasos para las solicitudes SQL de hello 1000 más reciente que se almacenan en sys.dm_pdw_exec_requests. |
| sys.dm_pdw_os_event_logs |10.000 |
| sys.dm_pdw_sql_requests |Hola últimas 1000 solicitudes de SQL que se almacenan en sys.dm_pdw_exec_requests. |

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información de referencia, vea [Información general de referencia de Almacenamiento de datos SQL][SQL Data Warehouse reference overview].

<!--Image references-->

<!--Article references-->
[Data Warehouse Units (DWU)]: ./sql-data-warehouse-overview-what-is.md
[SQL Data Warehouse reference overview]: ./sql-data-warehouse-overview-reference.md
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Tempdb]: ./sql-data-warehouse-tables-temporary.md
[data type]: ./sql-data-warehouse-tables-data-types.md
[creating a support ticket]: /sql-data-warehouse-get-started-create-support-ticket.md

<!--MSDN references-->
[Row-Overflow Data Exceeding 8 KB]: https://msdn.microsoft.com/library/ms186981.aspx
[Internal error: An expression services limit has been reached]: https://support.microsoft.com/kb/913050
