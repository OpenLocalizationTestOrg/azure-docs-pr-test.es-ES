---
title: temas de aaaAll para el servicio de almacenamiento de datos SQL | Documentos de Microsoft
description: "Tabla de todos los temas de hello Azure servicio denominado almacén de datos de SQL que existen en http://azure.microsoft.com/documentation/articles/, título y descripción."
services: sql-data-warehouse
documentationcenter: 
author: barbkess
manager: jhubbard
editor: 
ms.assetid: a26a6dec-9c08-4415-8f58-4ee1dd41f718
ms.service: sql-data-warehouse
ms.workload: sql-data-warehouse
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: reference
ms.date: 03/30/2017
ms.author: barbkess
ms.openlocfilehash: 6f71d35b76b50764a5904525445675dafaa56b85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="all-topics-for-azure-sql-data-warehouse-service"></a>Todos los temas del servicio Almacenamiento de datos SQL de Azure
Este tema enumeran todos los temas que se aplica directamente a toohello **almacenamiento de datos SQL** servicio de Azure. Puede buscar en esta página Web para las palabras clave mediante **CTRL+f**, temas de hello toofind de interés actual.

## <a name="new"></a>Nuevo
| &nbsp; | Título | Descripción |
| ---:|:--- |:--- |
| 1 |[Copias de seguridad de SQL Data Warehouse](sql-data-warehouse-backups.md) |Obtenga información acerca de las copias de seguridad de base de datos integrada de almacenamiento de datos de SQL que le permiten toorestore un punto de restauración del almacén de datos de SQL Azure tooa o una región geográfica diferente. |

## <a name="updated-articles-sql-data-warehouse"></a>Artículos actualizados, SQL Data Warehouse
En esta sección se enumera los artículos que se han actualizado recientemente, donde hello actualizar fue grande o importantes. Para cada artículo actualizado, un fragmento de código aproximada de hello agregado se muestra el texto de marcado. se actualizaron los artículos de Hola dentro del intervalo de fechas de Hola de **2016-08-22** demasiado**/ 10/2016-05**.

| &nbsp; | Artículo | Texto actualizado, fragmento | Se actualiza cuando |
| ---:|:--- |:--- |:--- |
| 2 |[Load data from Azure blob storage into SQL Data Warehouse (PolyBase) [Carga de datos de Almacenamiento de blobs de Azure en Almacenamiento de datos SQL (PolyBase)]](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md) |bytes/tootrack y archivos seleccionar r.command, s.request_id, r.status, count (distinct input_name) como nbr_files, sum (s.bytes_processed) / 1024/1024 como gb_processed de sys.dm_pdw_exec_requests r combinación interna sys.dm_pdw_dms_external_work s en r.request_id = s.request_id r WHERE. label  = 'CTAS : Load  cso . DimProduct  '  OR r. label  = 'CTAS : Load  cso . FactOnlineSales  ' GROUP BY  r.command,  s.request_id,  r.status ORDER BY  nbr_files desc,  gb_processed desc; |2016-09-07 |
| 3 |[SQL Data Warehouse](sql-data-warehouse-restore-database-overview.md) |** ¿Puedo restaurar un almacén de datos en pausa? ** toorestore un almacenamiento de datos que esté en pausa, necesita toofirst ponerlo en línea. Una vez que el almacén de datos de hello es nuevo en línea, tendrá de toochoose de puntos de restauración de siete días. ** Restaurar tooa con redundancia geográfica región ** si se usa el almacenamiento con redundancia geográfica de hello, puede restaurar Hola datos almacenamiento tooyour emparejados centro de datos en una región geográfica diferente. almacenamiento de datos de Hola se restaura desde la copia de seguridad diaria Hola último. ** Restaurar puede restaurar un punto de restauración de base de datos tooany de hello últimos siete días de la escala de tiempo **. Las instantáneas iniciar cada cuatro horas tooeight y están disponibles durante siete días. Cuando una instantánea tiene una antigüedad superior a siete días, caduca y su punto de restauración ya no está disponible. ** Restauración costos ** Hola almacenamiento cargo para almacenamiento de datos de hello restaurado se factura a velocidad de almacenamiento Premium de Azure de Hola. Si hace una pausa un almacenamiento de datos restaurada, se le cobra por almacenamiento a velocidad de hello almacenamiento Premium de Azure. ventaja de Hello de la pausa no es que estás cargo |2016-09-29 |

## <a name="get-started"></a>Primeros pasos
| &nbsp; | Título | Descripción |
| ---:|:--- |:--- |
| 4 |[Autenticación tooAzure almacenamiento de datos SQL](sql-data-warehouse-authentication.md) |Azure Active Directory (AAD) y SQL Server authentication tooAzure almacenamiento de datos SQL. |
| 5 |[Procedimientos recomendados para Almacenamiento de datos SQL de Azure](sql-data-warehouse-best-practices.md) |Recomendaciones y procedimientos recomendados que debe saber para desarrollar soluciones de Almacenamiento de datos SQL de Azure. Esto le ayudará a tener éxito. |
| 6 |[Controladores de Almacenamiento de datos SQL de Azure](sql-data-warehouse-connection-strings.md) |Cadenas de conexión y controladores de Almacenamiento de datos SQL |
| 7 |[Conectar tooAzure almacenamiento de datos SQL](sql-data-warehouse-connect-overview.md) |Cómo cadena de conexión y el nombre de servidor hello toofind de su tooAzure almacenamiento de datos de SQL |
| 8 |[Análisis de datos con Aprendizaje automático de Azure](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md) |Usar aprendizaje toobuild un modelo basado en datos almacenados en el almacén de datos de SQL Azure de aprendizaje de automático predictivo. |
| 9 |[Consulta de Almacenamiento de datos SQL de Azure (sqlcmd)](sql-data-warehouse-get-started-connect-sqlcmd.md) |Consultar el almacenamiento de datos de SQL Azure con sqlcmd Hola utilidad de línea de comandos. |
| 10 |[Creación de una base de datos de Almacenamiento de datos SQL mediante Transact-SQL (TSQL)](sql-data-warehouse-get-started-create-database-tsql.md) |Obtenga información acerca de cómo toocreate un Azure SQL del almacenamiento de datos con TSQL |
| 11 |[¿Cómo toocreate compatibilidad vale para almacenamiento de datos SQL](sql-data-warehouse-get-started-create-support-ticket.md) |¿Cómo toocreate una compatibilidad con vales en el almacén de datos de SQL Azure. |
| 12 |[Carga de datos con la Factoría de datos de Azure](sql-data-warehouse-get-started-load-with-azure-data-factory.md) |Obtenga información acerca de los datos de tooload con Data Factory de Azure |
| 13 |[Carga de datos con PolyBase en Almacenamiento de datos SQL](sql-data-warehouse-get-started-load-with-polybase.md) |Obtenga información acerca de qué es PolyBase y cómo toouse para escenarios de almacenamiento de datos. |
| 14 |[Creación de una instancia de Almacenamiento de datos SQL de Azure](sql-data-warehouse-get-started-provision.md) |Obtenga información acerca de cómo toocreate un almacenamiento de datos de SQL Azure en Hola portal de Azure |
| 15 |[Creación de Almacenamiento de datos SQL con Powershell](sql-data-warehouse-get-started-provision-powershell.md) |Creación de Almacenamiento de datos SQL con Powershell |
| 16 |[Visualización de datos con Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md) |Visualización de datos de Almacenamiento de datos SQL con Power BI |
| 17 |[Consultas en Almacenamiento de datos SQL de Azure (Visual Studio)](sql-data-warehouse-query-visual-studio.md) |Consultas en Almacenamiento de datos SQL con Visual Studio. |

## <a name="develop"></a>Desarrollo
| &nbsp; | Título | Description |
| ---:|:--- |:--- |
| 18 |[Optimización de transacciones para Almacenamiento de datos SQL](sql-data-warehouse-develop-best-practices-transactions.md) |Guía de procedimientos recomendados sobre la escritura de actualizaciones de transacciones eficientes en Almacenamiento de datos SQL de Azure |
| 19 |[Simultaneidad y administración de cargas de trabajo en Almacenamiento de datos SQL](sql-data-warehouse-develop-concurrency.md) |Obtenga información sobre la simultaneidad y la administración de cargas de trabajo en Almacenamiento de datos SQL de Azure para el desarrollo de soluciones. |
| 20 | |[Create Table As Select (CTAS) en Almacenamiento de datos SQL](sql-data-warehouse-develop-ctas.md) |Sugerencias para codificar con hello crear tabla de la opción de instrucción (CTAS) en el almacén de datos de SQL Azure para desarrollar soluciones. |
| 21 |[SQL dinámico en Almacenamiento de datos SQL](sql-data-warehouse-develop-dynamic-sql.md) |Sugerencias para usar SQL dinámico en Almacenamiento de datos SQL Azure para desarrollar soluciones. |
| 22 |[Opciones de Group by en Almacenamiento de datos SQL](sql-data-warehouse-develop-group-by-options.md) |Sugerencias para implementar opciones de Group by en Almacenamiento de datos SQL de Azure para el desarrollo de soluciones. |
| 23 |[Usar consultas de tooinstrument de etiquetas en el almacén de datos de SQL](sql-data-warehouse-develop-label.md) |Sugerencias para usar las consultas de tooinstrument de etiquetas en el almacén de datos de SQL Azure para desarrollar soluciones. |
| 24 |[Bucles en Almacenamiento de datos SQL](sql-data-warehouse-develop-loops.md) |Sugerencias para los bucles de Transact-SQL en Almacenamiento de datos SQL de Azure para el desarrollo de soluciones. |
| 25 |[Procedimientos almacenados en el Almacenamiento de datos SQL](sql-data-warehouse-develop-stored-procedures.md) |Sugerencias para implementar procedimientos almacenados en el Almacenamiento de datos SQL Azure para el desarrollo de soluciones. |
| 26 |[Transacciones en el Almacenamiento de datos SQL](sql-data-warehouse-develop-transactions.md) |Sugerencias para implementar transacciones en el Almacenamiento de datos SQL Azure para el desarrollo de soluciones. |
| 27 |[Esquemas definidos por el usuario en el Almacenamiento de datos SQL](sql-data-warehouse-develop-user-defined-schemas.md) |Sugerencias para usar los esquemas Transact-SQL en el Almacenamiento de datos SQL Azure para desarrollar soluciones. |
| 28 |[Asignación de variables en el Almacenamiento de datos SQL](sql-data-warehouse-develop-variable-assignment.md) |Sugerencias para la asignación de variables de Transact-SQL en el Almacenamiento de datos SQL Azure para desarrollar soluciones. |
| 29 |[Vistas en el Almacenamiento de datos SQL](sql-data-warehouse-develop-views.md) |Sugerencias para usar las vistas Transact-SQL en el Almacenamiento de datos SQL Azure para desarrollar soluciones. |
| 30 |[Decisiones de diseño y técnicas de codificación para el Almacenamiento de datos SQL](sql-data-warehouse-overview-develop.md) |Conceptos de desarrollo, decisiones de diseño, recomendaciones y técnicas de codificación para el Almacenamiento de datos SQL. |

## <a name="manage"></a>Manage
| &nbsp; | Título | Description |
| ---:|:--- |:--- |
| 31 |[Administración de la potencia de proceso en Almacenamiento de datos SQL de Azure (información general)](sql-data-warehouse-manage-compute-overview.md) |Funcionalidades de escalado horizontal del rendimiento en Almacenamiento de datos SQL de Azure. Escalar horizontalmente mediante el ajuste a Dwu o pausar y reanudar los costos de toosave de recursos de proceso. |
| 32 |[Administración de la potencia de proceso en Almacenamiento de datos SQL de Azure (Portal de Azure)](sql-data-warehouse-manage-compute-portal.md) |Capacidad de proceso de tareas del portal Azure toomanage. Escalado de los recursos de proceso ajustando DWU. O bien, puede pausar y reanudar los costos de toosave de recursos de proceso. |
| 33 |[Administración de la potencia de proceso en Almacenamiento de datos SQL de Azure (PowerShell)](sql-data-warehouse-manage-compute-powershell.md) |Capacidad de proceso de PowerShell tareas toomanage. Escalado de los recursos de proceso ajustando DWU. O bien, puede pausar y reanudar los costos de toosave de recursos de proceso. |
| 34 |[Administración de la potencia de proceso en Almacenamiento de datos SQL de Azure (REST)](sql-data-warehouse-manage-compute-rest-api.md) |Capacidad de proceso de PowerShell tareas toomanage. Escalado de los recursos de proceso ajustando DWU. O bien, puede pausar y reanudar los costos de toosave de recursos de proceso. |
| 35 |[Administración de la potencia de proceso en Almacenamiento de datos SQL de Azure (T-SQL)](sql-data-warehouse-manage-compute-tsql.md) |Transact-SQL (T-SQL) tareas tooscale rendimiento mediante el ajuste a Dwu. Ahorre costes reduciendo el escalado fuera de horas punta. |
| 36 |[Supervisión de la carga de trabajo mediante DMV](sql-data-warehouse-manage-monitor.md) |Obtenga información acerca de cómo toomonitor la carga de trabajo mediante DMV. |
| 37 |[Administración de base datos en Almacenamiento de datos SQL de Azure](sql-data-warehouse-overview-manage.md) |Información general de administración de bases de datos de Almacenamiento de datos SQL Incluye herramientas de administración, DWU y rendimiento de escalado horizontal, solución de problemas de rendimiento de las consultas, el establecimiento de directivas de seguridad y la restauración una base de datos de daños en los datos o de un apagón regional. |
| 38 |[Supervisión de las consultas de usuario en Almacenamiento de datos SQL de Azure](sql-data-warehouse-overview-manage-user-queries.md) |Información general sobre consideraciones de hello, prácticas recomendadas y tareas para supervisar las consultas de usuario en el almacén de datos de SQL Azure |
| 39 |[SQL Data Warehouse](sql-data-warehouse-restore-database-overview.md) |Información general de opciones de restauración de base de datos de Hola para recuperar una base de datos en el almacén de datos de SQL Azure. |
| 40 |[Restauración de instancias de Almacenamiento de datos SQL de Azure (Portal)](sql-data-warehouse-restore-database-portal.md) |Tareas del Portal de Azure para restaurar una instancia de Almacenamiento de datos SQL de Azure. |
| 41 |[Restauración de instancias de Almacenamiento de datos SQL de Azure (PowerShell)](sql-data-warehouse-restore-database-powershell.md) |Tareas de PowerShell para restaurar una instancia de Almacenamiento de datos SQL de Azure. |
| 42 |[Restauración de instancias de Almacenamiento de datos SQL de Azure (API de REST)](sql-data-warehouse-restore-database-rest-api.md) |Tareas de la API de REST para restaurar una instancia de Almacenamiento de datos SQL de Azure. |

## <a name="tables-and-indexes"></a>Tablas e índices
| &nbsp; | Título | Description |
| ---:|:--- |:--- |
| 43 |[Tipos de datos de las tablas en el Almacenamiento de datos SQL](sql-data-warehouse-tables-data-types.md) |Introducción a los tipos de datos de Almacenamiento de datos SQL de Azure. |
| 44 |[Distribución de tablas en Almacenamiento de datos SQL](sql-data-warehouse-tables-distribute.md) |Introducción a la distribución de tablas en Almacenamiento de datos SQL de Azure. |
| 45 |[Indexación de tablas en Almacenamiento de datos SQL](sql-data-warehouse-tables-index.md) |Introducción a la indexación de tablas en Almacenamiento de datos SQL de Azure. |
| 46 |[Información general de tablas en Almacenamiento de datos SQL](sql-data-warehouse-tables-overview.md) |Introducción a las tablas de Almacenamiento de datos SQL de Azure. |
| 47 |[Creación de particiones de tablas en Almacenamiento de datos SQL](sql-data-warehouse-tables-partition.md) |Introducción a la creación de particiones en tablas en Almacenamiento de datos SQL de Azure. |
| 48 |[Administración de estadísticas en tablas en Almacenamiento de datos SQL](sql-data-warehouse-tables-statistics.md) |Introducción a las estadísticas de tablas en Almacenamiento de datos SQL de Azure. |
| 49 |[Tablas temporales en el Almacenamiento de datos SQL](sql-data-warehouse-tables-temporary.md) |Introducción a las tablas temporales en Almacenamiento de datos SQL de Azure. |

## <a name="integrate"></a>Integrate
| &nbsp; | Título | Description |
| ---:|:--- |:--- |
| 50 |[Uso de Factoría de datos de Azure con Almacenamiento de datos SQL](sql-data-warehouse-integrate-azure-data-factory.md) |Sugerencias para usar Factoría de datos de Azure (ADF) con Almacenamiento de datos SQL para el desarrollo de soluciones. |
| 51 |[Uso de Aprendizaje automático de Azure con Almacenamiento de datos SQL](sql-data-warehouse-integrate-azure-machine-learning.md) |Tutorial para usar Aprendizaje automático de Azure con Almacenamiento de datos SQL de Azure para el desarrollo de soluciones. |
| 52 |[Uso de Análisis de transmisiones de Azure con Almacenamiento de datos SQL](sql-data-warehouse-integrate-azure-stream-analytics.md) |Sugerencias para usar Análisis de transmisiones de Azure con Almacenamiento de datos SQL de Azure para el desarrollo de soluciones. |
| 53 |[Uso de Power BI con Almacenamiento de datos SQL](sql-data-warehouse-integrate-power-bi.md) |Sugerencias para usar Power BI con Almacenamiento de datos SQL de Azure para el desarrollo de soluciones. |
| 54 |[Aprovechamiento de otros servicios con Almacenamiento de datos SQL](sql-data-warehouse-overview-integrate.md) |Herramientas y asociados con soluciones que se integran con Almacenamiento de datos SQL. |

## <a name="load"></a>Carga
| &nbsp; | Título | Description |
| ---:|:--- |:--- |
| 55 |[Carga de datos del Almacenamiento de blobs de Azure en Almacenamiento de datos SQL de Azure (Data Factory de Azure)](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md) |Obtenga información acerca de los datos de tooload con Data Factory de Azure |
| 56 |[Load data from Azure blob storage into SQL Data Warehouse (PolyBase) [Carga de datos de Almacenamiento de blobs de Azure en Almacenamiento de datos SQL (PolyBase)]](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md) |Obtenga información acerca de cómo toouse datos de tooload de PolyBase de Azure almacenamiento de blobs en almacenamiento de datos de SQL. Cargar algunas tablas de datos públicos en el esquema de almacenamiento de datos de Contoso Retail Hola. |
| 57 |[Carga de datos de SQL Server en Almacenamiento de datos SQL de Azure (AZCopy)](sql-data-warehouse-load-from-sql-server-with-azcopy.md) |Utiliza bcp tooexport datos desde archivos de tooflat de SQL Server, el almacenamiento de blobs de AZCopy tooimport datos tooAzure y datos de PolyBase tooingest hello en almacenamiento de datos de SQL Azure. |
| 58 |[Carga de datos de SQL Server en Almacenamiento de datos SQL de Azure (archivos planos)](sql-data-warehouse-load-from-sql-server-with-bcp.md) |Un pequeño tamaño de datos, se utiliza bcp tooexport datos de archivos de SQL Server tooflat e importar los datos de hello directamente en el almacenamiento de datos de SQL Azure. |
| 59 |[Carga de datos de SQL Server en Almacenamiento de datos SQL de Azure (SSIS)](sql-data-warehouse-load-from-sql-server-with-integration-services.md) |Muestra cómo toocreate datos de toomove paquete SQL Server Integration Services (SSIS) desde una gran variedad de datos de orígenes tooSQL almacenamiento de datos. |
| 60 |[Carga de datos con PolyBase en Almacenamiento de datos SQL](sql-data-warehouse-load-from-sql-server-with-polybase.md) |Utiliza bcp tooexport datos desde archivos de tooflat de SQL Server, el almacenamiento de blobs de AZCopy tooimport datos tooAzure y datos de PolyBase tooingest hello en almacenamiento de datos de SQL Azure. |
| 61 |[Guía para el uso de PolyBase en Almacenamiento de datos SQL](sql-data-warehouse-load-polybase-guide.md) |Directrices y recomendaciones para el uso de PolyBase en escenarios de Almacenamiento de datos SQL. |
| 62 |[Carga de datos de ejemplo en Almacenamiento de datos SQL](sql-data-warehouse-load-sample-databases.md) |Carga de datos de ejemplo en Almacenamiento de datos SQL |
| 63 |[Carga de datos con bcp](sql-data-warehouse-load-with-bcp.md) |Obtenga información acerca de qué bcp es y cómo toouse para escenarios de almacenamiento de datos. |
| 64 |[Carga de datos en Almacenamiento de datos SQL de Azure](sql-data-warehouse-overview-load.md) |Obtenga información acerca de escenarios comunes de Hola de carga en el almacén de datos SQL de datos. Estos incluyen el uso de PolyBase, el almacenamiento de blobs de Azure, archivos planos y el envío de discos. También puede usar herramientas de otros fabricantes. |

## <a name="migrate"></a>Migrar
| &nbsp; | Título | Description |
| ---:|:--- |:--- |
| 65 |[Migrar su tooSQL de código SQL almacenamiento de datos](sql-data-warehouse-migrate-code.md) |Sugerencias para migrar su tooAzure de código SQL almacenamiento de datos SQL para desarrollar soluciones. |
| 66 |[Migración de los datos](sql-data-warehouse-migrate-data.md) |Sugerencias para migrar el almacenamiento de datos SQL de datos tooAzure para desarrollar soluciones. |
| 67 |[Utilidad de migración de Almacenamiento de datos (vista previa)](sql-data-warehouse-migrate-migration-utility.md) |Migrar tooSQL almacenamiento de datos. |
| 68 |[Migrar el almacenamiento de datos de esquema tooSQL](sql-data-warehouse-migrate-schema.md) |Sugerencias para migrar el almacenamiento de datos SQL de esquema tooAzure para desarrollar soluciones. |
| 69 |[Migrar el almacenamiento de datos de solución tooSQL](sql-data-warehouse-overview-migrate.md) |Guía de migración para poner la plataforma de almacenamiento de datos SQL de solución tooAzure. |

## <a name="partners"></a>Asociados
| &nbsp; | Título | Description |
| ---:|:--- |:--- |
| 70 |[Partners de inteligencia empresarial de Almacenamiento de datos SQL](sql-data-warehouse-partner-business-intelligence.md) |Lista de los asociados de inteligencia empresarial con soluciones compatibles con Almacenamiento de datos SQL. |
| 71 |[Socios de integración de datos de Almacenamiento de datos SQL](sql-data-warehouse-partner-data-integration.md) |Lista de terceros asociados con soluciones de integración de datos compatibles con Almacenamiento de datos SQL de Azure. |
| 72 |[Partners de administración de datos de Almacenamiento de datos SQL](sql-data-warehouse-partner-data-management.md) |Lista de los asociados de administración de datos externos con soluciones compatibles con Almacenamiento de datos SQL. |

## <a name="reference"></a>Referencia
| &nbsp; | Título | Description |
| ---:|:--- |:--- |
| 73 |[Temas de referencia de Almacenamiento de datos SQL](sql-data-warehouse-overview-reference.md) |Vínculos al contenido de referencia de Almacenamiento de datos SQL. |
| 74 |[Cmdlets de PowerShell y API de REST para Almacenamiento de datos SQL](sql-data-warehouse-reference-powershell-cmdlets.md) |Encontrar Hola superiores cmdlets de PowerShell para almacenamiento de datos de SQL de Azure e incluye toopause y reanudar una base de datos. |
| 75 |[Elementos de lenguaje](sql-data-warehouse-reference-tsql-language-elements.md) |Lista de contenido de tooreference de vínculos de elementos de lenguaje Transact-SQL Hola utilizado para almacén de datos de SQL. |
| 76 |[Temas de Transact-SQL](sql-data-warehouse-reference-tsql-statements.md) |Contenido de tooreference de vínculos de temas de Transact-SQL de hello utilizados por el almacenamiento de datos SQL. |
| 77 |[Vistas de sistema](sql-data-warehouse-reference-tsql-system-views.md) |Vincula el contenido de las vistas de toosystem para almacenamiento de datos de SQL. |

## <a name="security"></a>Seguridad
| &nbsp; | Título | Description |
| ---:|:--- |:--- |
| 78 |[SQL Data Warehouse: compatibilidad con clientes de nivel inferior para enmascaramiento de datos dinámicos y auditoría](sql-data-warehouse-auditing-downlevel-clients.md) |Obtenga información sobre compatibilidad de Almacenamiento de datos SQL con clientes de nivel inferior para auditoría de datos. |
| 79 |[Auditoría en Almacenamiento de datos SQL de Azure](sql-data-warehouse-auditing-overview.md) |Introducción a la auditoría en Almacenamiento de datos SQL de Azure |
| 80 |[Introducción al cifrado de datos transparente (TDE) en Almacenamiento de datos SQL](sql-data-warehouse-encryption-tde.md) |Cifrado de datos transparente (TDE) en SQL Data Warehouse |
| 81 |[Introducción al cifrado de datos transparente (TDE)](sql-data-warehouse-encryption-tde-tsql.md) |Cifrado de datos transparente (TDE) en SQL Data Warehouse (T-SQL) |
| 82 |[Proteger una base de datos en Almacenamiento de datos SQL](sql-data-warehouse-overview-manage-security.md) |Sugerencias para proteger una base de datos en Almacenamiento de datos SQL de Azure para desarrollar soluciones. |

## <a name="miscellaneous"></a>Varios
| &nbsp; | Título | Description |
| ---:|:--- |:--- |
| 83 |[Instalación de Visual Studio y SSDT para SQL Data Warehouse](sql-data-warehouse-install-visual-studio.md) |Instalación de herramientas de desarrollo de Visual Studio y SQL Server Data Tools (SSDT) para Almacenamiento de datos SQL de Azure |
| 84 |[Migración tooPremium detalles de almacenamiento](sql-data-warehouse-migrate-to-premium-storage.md) |Instrucciones para migrar un almacenamiento de toopremium de almacenamiento de datos SQL existente |
| 85 |[Introducción a la detección de amenazas](sql-data-warehouse-security-threat-detection.md) |¿Cómo tooget a usar la detección de amenazas |
| 86 |[Límites de capacidad de Almacenamiento de datos SQL](sql-data-warehouse-service-capacity-limits.md) |Valores máximos para las conexiones, bases de datos, tablas y consultas de Almacenamiento de datos SQL. |
| 87 |[Solución de problemas de Almacenamiento de datos SQL de Azure](sql-data-warehouse-troubleshoot.md) |Cómo solucionar los problemas de Almacenamiento de datos SQL de Azure. |

