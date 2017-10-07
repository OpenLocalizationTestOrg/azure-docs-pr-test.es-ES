---
title: aaaTroubleshooting almacenamiento de datos de SQL de Azure | Documentos de Microsoft
description: "Cómo solucionar los problemas de Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 51f1e444-9ef7-4e30-9a88-598946c45196
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/30/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 3c53a39f77057fe0bcc053a0b896555abf397515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-sql-data-warehouse"></a>Solución de problemas de Azure SQL Data Warehouse
Este tema se enumeran algunos de Hola preguntas más frecuentes de solución de problemas nos llegan de nuestros clientes.

## <a name="connecting"></a>Conexión
| Problema | Resolución |
|:--- |:--- |
| Error de inicio de sesión del usuario 'NT AUTHORITY\ANONYMOUS LOGON'. (Microsoft SQL Server, error: 18456) |Este error se produce cuando un usuario AAD trata de la base de datos maestra de tooconnect toohello, pero no tiene un usuario en master.  toocorrect este problema especifique Hola almacenamiento de datos de SQL desea tooconnect tooat tiempo de la conexión o agregar base de datos maestra de hello usuario toohello.  Consulte el artículo [Información general sobre seguridad][Security overview] para obtener más detalles. |
| servidor Hello "MyUserName" entidad de seguridad no es capaz de tooaccess Hola "maestra" de la base de datos en el contexto de seguridad actual de Hola. No se puede abrir la base de datos predeterminada del usuario. Error de inicio de sesión. Error de inicio de sesión del usuario 'MyUserName'. (Microsoft SQL Server, error: 916) |Este error se produce cuando un usuario AAD trata de la base de datos maestra de tooconnect toohello, pero no tiene un usuario en master.  toocorrect este problema especifique Hola almacenamiento de datos de SQL desea tooconnect tooat tiempo de la conexión o agregar base de datos maestra de hello usuario toohello.  Consulte el artículo [Información general sobre seguridad][Security overview] para obtener más detalles. |
| Error CTAIP |Este error puede producirse cuando se ha creado un inicio de sesión en la base de datos maestra de hello SQL server, pero no está en la base de datos de almacenamiento de datos SQL de Hola.  Si se produce este error, eche un vistazo a hello [información general sobre seguridad] [ Security overview] artículo.  Este artículo explica cómo toocreate crear un inicio de sesión y un usuario en el patrón y, a continuación, cómo Hola a toocreate un usuario de base de datos de almacenamiento de datos SQL. |
| Bloqueado por el firewall |Bases de datos SQL Azure están protegidas por tooensure de firewalls de nivel de servidor y base de datos solo conocida las direcciones IP tienen base de datos de access tooa. firewalls de Hello son seguros de forma predeterminada, lo que significa que debe habilitar explícitamente y la dirección IP o intervalo de direcciones para que puedan conectarse.  tooconfigure el firewall para el acceso, siga los pasos de hello en [configurar el acceso de firewall de servidor para la dirección IP de cliente] [ Configure server firewall access for your client IP] en hello [aprovisionamiento instrucciones] [Provisioning instructions]. |
| No se puede conectar con una herramienta o un controlador |Recomienda el uso de almacenamiento de datos SQL [SSMS][SSMS], [SSDT para Visual Studio][SSDT for Visual Studio], o [sqlcmd] [ sqlcmd] tooquery los datos. Para obtener más detalles sobre los controladores y tooSQL conexión almacenamiento de datos, vea [controladores de almacenamiento de datos de SQL Azure] [ Drivers for Azure SQL Data Warehouse] y [conectar tooAzure almacenamiento de datos SQL] [ Connect tooAzure SQL Data Warehouse] artículos. |

## <a name="tools"></a>Herramientas
| Problema | Resolución |
|:--- |:--- |
| El Explorador de objetos de Visual Studio no muestra usuarios de AAD |Este es un problema conocido.  Como alternativa, ver los usuarios de hello en [sys.database_principals][sys.database_principals].  Vea [tooAzure almacenamiento de datos SQL de autenticación] [ Authentication tooAzure SQL Data Warehouse] toolearn más acerca del uso de Azure Active Directory con el almacenamiento de datos de SQL. |
|Manual de scripting, utilizar el Asistente de scripting de Hola o conectarse a través de SSMS es lentos, bloqueados o productoras errores| Asegúrese de que los usuarios se han creado en la base de datos maestra Hola. En Opciones de scripting, también Asegúrese de que dicha edición del motor de Hola se establece como "Edición de almacenamiento de datos de Microsoft Azure SQL" y tipo de motor es "Microsoft Azure SQL Database".|

## <a name="performance"></a>Rendimiento
| Problema | Resolución |
|:--- |:--- |
| Solución de problemas de rendimiento de consultas |Si está tratando de tootroubleshoot una consulta determinada, comience con [aprender cómo toomonitor las consultas][Learning how toomonitor your queries]. |
| Un bajo rendimiento de las consultas y unos planes mal diseñados suelen ser el resultado de la falta de estadísticas |causa más común de Hola de un rendimiento bajo es la falta de estadísticas en las tablas.  Vea [mantener las estadísticas de tabla] [ Statistics] para obtener más información acerca de cómo toocreate estadísticas y por qué son críticos tooyour rendimiento. |
| Baja simultaneidad o consultas en cola |Descripción de [administración de cargas de trabajo] [ Workload management] es importante en orden toounderstand cómo toobalance la asignación de memoria con la simultaneidad. |
| ¿Cómo tooimplement los procedimientos recomendados |Hola lugar toostart toolearn formas tooimprove consulta un rendimiento óptimo es [prácticas recomendadas de almacenamiento de datos SQL] [ SQL Data Warehouse best practices] artículo. |
| ¿Cómo tooimprove rendimiento con escalado |A veces el rendimiento de la solución tooimproving hello es toosimply agregar más consultas de tooyour de energía por de proceso [ajuste de escala en el almacenamiento de datos de SQL][Scaling your SQL Data Warehouse]. |
| Bajo rendimiento de las consultas como resultado de poca calidad del índice |A veces la velocidad de las consultas se puede reducir debido a la [baja calidad del índice de almacén de columnas][Poor columnstore index quality].  Consulte este artículo para obtener más información y cómo demasiado[regeneración de índices de calidad de segmento tooimprove][Rebuild indexes tooimprove segment quality]. |

## <a name="system-management"></a>Administración del sistema
| Problema | Resolución |
|:--- |:--- |
| Msg 40847: No pudo realizar la operación de Hola porque servidor superaría Hola permitida la cuota de la unidad de transacción de base de datos de 45000. |Reduzca hello [DWU] [ DWU] de base de datos de Hola que estamos toocreate o [solicitar un aumento de la cuota][request a quota increase]. |
| Investigación del uso del espacio |Vea [tamaños de tabla] [ Table sizes] toounderstand el uso del espacio de saludo del sistema. |
| Ayuda con la administración de tablas |Vea hello [información general de la tabla] [ Overview] artículo para obtener ayuda con la administración de las tablas.  Este artículo también incluye vínculos a temas más detallados como [tipos de datos de tabla][Data types], [distribución de una tabla][Distribute], [indexación de una tabla][Index], [creación de particiones de una tabla][Partition], [mantenimiento de estadísticas de tabla][Statistics] y [tablas temporales][Temporary]. |
|Barra de progreso de datos transparente (TDE) de cifrado no se está actualizando en hello Portal de Azure|Puede ver el estado de Hola de TDE a través de [powershell](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption).|

## <a name="polybase"></a>PolyBase
| Problema | Resolución |
|:--- |:--- |
| Se produce un error en la carga porque hay filas de gran tamaño |Actualmente la compatibilidad con filas de gran tamaño no está disponible en Polybase.  Esto significa que si la tabla contiene varchar (max), nvarchar (max) o varbinary (max), las tablas externas no pueden ser utilizado tooload los datos.  Cargas de filas de gran tamaño es actualmente solo admite a través de la factoría de datos de Azure (con BCP), análisis de transmisiones de Azure, SSIS, BCP o hello clase SQLBulkCopy. NET. La compatibilidad con filas de gran tamaño en PolyBase se agregará en una versión futura. |
| La carga de la tabla bcp con el tipo de datos MAX está dando error |Hay un problema conocido que requiere que se coloquen varchar (max), nvarchar (max) o varbinary (max) al final de Hola de tabla de hello en algunos escenarios.  Intente mover el final de toohello máximo columnas de tabla de Hola. |

## <a name="differences-from-sql-database"></a>Diferencias con respecto a SQL Database
| Problema | Resolución |
|:--- |:--- |
| Características de SQL Database no admitidas |Consulte [Características no compatibles de las tablas][Unsupported table features]. |
| Tipos de datos de SQL Database no admitidos |Consulte [Tipos de datos no admitidos][Unsupported data types]. |
| Limitaciones de DELETE y UPDATE |Vea [soluciones alternativas de actualización][UPDATE workarounds], [soluciones alternativas DELETE] [ DELETE workarounds] y [toowork utilizando CTAS alrededor de actualización no compatible y Sintaxis de DELETE][Using CTAS toowork around unsupported UPDATE and DELETE syntax]. |
| No se admite la instrucción MERGE |Consulte las [soluciones alternativas para MERGE][MERGE workarounds]. |
| Limitaciones de procedimientos almacenados |Vea [almacenados limitaciones de procedimiento] [ Stored procedure limitations] toounderstand algunas de las limitaciones de Hola de procedimientos almacenados. |
| Los UDF no admiten instrucciones SELECT |Se trata de una limitación actual de nuestros UDF.  Vea [CREATE FUNCTION] [ CREATE FUNCTION] de sintaxis de Hola se admiten. |

## <a name="next-steps"></a>Pasos siguientes
Si está fuese no se puede toofind un problema de tooyour de solución los casos anteriores, aquí tiene algunos otros recursos que puede probar.

* [Blogs]
* [Solicitud de función]
* [Vídeos]
* [Blogs del equipo de CAT]
* [Creación de una incidencia de soporte técnico]
* [Foro de MSDN]
* [Foro Stack Overflow]
* [Twitter]

<!--Image references-->

<!--Article references-->
[Security overview]: ./sql-data-warehouse-overview-manage-security.md
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx
[SSDT for Visual Studio]: ./sql-data-warehouse-install-visual-studio.md
[Drivers for Azure SQL Data Warehouse]: ./sql-data-warehouse-connection-strings.md
[Connect tooAzure SQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Creación de una incidencia de soporte técnico]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Scaling your SQL Data Warehouse]: ./sql-data-warehouse-manage-compute-overview.md
[DWU]: ./sql-data-warehouse-overview-what-is.md
[request a quota increase]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Learning how toomonitor your queries]: ./sql-data-warehouse-manage-monitor.md
[Provisioning instructions]: ./sql-data-warehouse-get-started-provision.md
[Configure server firewall access for your client IP]: ./sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[Table sizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries
[Unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuild indexes tooimprove segment quality]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Using CTAS toowork around unsupported UPDATE and DELETE syntax]: ./sql-data-warehouse-develop-ctas.md#using-ctas-to-work-around-unsupported-features
[UPDATE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[DELETE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[MERGE workarounds]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[Stored procedure limitations]: ./sql-data-warehouse-develop-stored-procedures.md#limitations
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md
[Working around hello PolyBase UTF-8 requirement]: ./sql-data-warehouse-load-polybase-guide.md#working-around-the-polybase-utf-8-requirement

<!--MSDN references-->
[sys.database_principals]: https://msdn.microsoft.com/library/ms187328.aspx
[CREATE FUNCTION]: https://msdn.microsoft.com/library/mt203952.aspx
[sqlcmd]: https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-get-started-connect-sqlcmd/

<!--Other Web references-->
[Blogs]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[Blogs del equipo de CAT]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Solicitud de función]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Foro de MSDN]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse
[Foro Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Vídeos]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
