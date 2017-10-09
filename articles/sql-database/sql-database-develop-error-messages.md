---
title: "códigos de error de aaaSQL: error de conexión de base de datos | Documentos de Microsoft"
description: "Obtenga información acerca de los códigos de error de SQL de las aplicaciones cliente de la Base de datos SQL, como los errores de conexión de base de datos más comunes, los problemas de copia de la base de datos y los errores generales. "
keywords: "código de error de SQL, acceder a SQL, error de conexión de base de datos, códigos de error de SQL"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 2a23e4ca-ea93-4990-855a-1f9f05548202
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 683a7d72c935742f3f9f9a0c683e5d8161167d6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sql-error-codes-for-sql-database-client-applications-database-connection-error-and-other-issues"></a>Códigos de error para las aplicaciones cliente de la Base de datos SQL: error de conexión de base de datos y otros problemas.
<!--
Old Title on MSDN:  Error Messages (Azure SQL Database)
ShortId on MSDN:  ff394106.aspx
Dx 4cff491e-9359-4454-bd7c-fb72c4c452ca
-->


En este artículo se enumeran los códigos de error de SQL de la aplicación cliente de Base de datos SQL, incluidos los errores de conexión de base de datos, los errores transitorios, los errores de regulación de recursos, los problemas de copia de la base de datos, el grupo elástico y otros errores. Mayoría de las categorías es tooAzure determinada base de datos SQL y no aplica tooMicrosoft SQL Server.

## <a name="database-connection-errors-transient-errors-and-other-temporary-errors"></a>Errores de conexión de base de datos, errores transitorios y otros errores temporales
Hello siguiente tabla recogen códigos de error SQL de Hola para errores de pérdida de conexión y otros errores transitorios que pueden producirse cuando la aplicación trata de tooaccess base de datos SQL. Para los tutoriales de introducción acerca de cómo tooconnect tooAzure base de datos de SQL, consulte [conectar tooAzure base de datos SQL](sql-database-libraries.md).

### <a name="most-common-database-connection-errors-and-transient-fault-errors"></a>Errores de conexión de base de datos y errores transitorios más comunes
Hola infraestructura de Azure tiene Hola capacidad toodynamically volver a configurar los servidores cuando surgen de cargas de trabajo en hello servicio de base de datos SQL.  Este comportamiento dinámico podría hacer que su cliente programa toolose su tooSQL de conexión base de datos. Este tipo de condición de error se conoce como *error transitorio*.

Se recomienda encarecidamente que el programa de cliente tiene lógica de reintento para que puede restablecer una conexión después de dar Hola errores transitorios tiempo toocorrect propio.  Se recomienda un retraso de 5 segundos antes del primer reintento. Reintentar después de un retraso inferior a 5 segundos corre el riesgo de servicio en la nube Hola abrumador. Para cada reintento subsiguientes retraso Hola debe crecer exponencialmente, tooa máximo de 60 segundos.

Los errores transitorios de manifiesto normalmente como uno de los siguientes mensajes de error de los programas de cliente de hello:

* La base de datos &lt;db_name&gt; del servidor &lt;Azure_instance&gt; no está disponible actualmente. Vuelva a intentar la conexión de hello más tarde. Si persiste el problema de hello, póngase en contacto con soporte al cliente y proporcióneles Hola Id. de seguimiento de sesión de &lt;session_id&gt;
* La base de datos &lt;db_name&gt; del servidor &lt;Azure_instance&gt; no está disponible actualmente. Vuelva a intentar la conexión de hello más tarde. Si persiste el problema de hello, póngase en contacto con soporte al cliente y proporcióneles Hola Id. de seguimiento de sesión de &lt;session_id&gt;. (Microsoft SQL Server, error: 40613)
* Host de hello remoto forzó el cierre una conexión existente.
* System.Data.Entity.Core.EntityCommandExecutionException: Se produjo un error al ejecutar la definición de comando Hola. Vea Hola la excepción interna para obtener más información. ---> System.Data.SqlClient.SqlException: se produjo un error de nivel de transporte al recibir los resultados del servidor de Hola. (proveedor: proveedor de sesión, error: 19: La conexión física es inservible)
* Una base de datos secundaria de la tooa del intento de conexión no se pudo como base de datos de hello está en proceso de Hola de reconfguration y está ocupado aplicar nuevas páginas en medio de Hola de una transacción activa en la base de datos principal de Hola. 

Para obtener ejemplos de lógica de reintento, vea:

* [Bibliotecas de conexiones para la base de datos SQL y SQL Server](sql-database-libraries.md) 
* [Errores de conexión de toofix de acciones y los errores transitorios en base de datos SQL](sql-database-connectivity-issues.md)

Obtener una explicación de hello *período de bloqueo* para los clientes que utilizan ADO.NET está disponible en [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).

### <a name="transient-fault-error-codes"></a>Códigos de errores transitorios
Hello siguientes errores son transitorios y deben reintentarse en lógica de la aplicación 

| Código de error | Gravedad | Descripción |
| ---:| ---:|:--- |
| 4060 |16 |No se puede abrir la base de datos "%. & #x2a; %.*ls" solicitada por el inicio de sesión de Hola. Error de inicio de sesión de Hola. |
| 40197 |17 |servicio de Hello ha encontrado un error al procesar la solicitud. Vuelva a intentarlo. Código de error %d.<br/><br/>Recibirá este error, al servicio Hola está inactivo debido a toosoftware o actualizaciones de hardware, errores de hardware o cualquier otro problema de conmutación por error. código de error de Hello (%d) incrustado en el mensaje de saludo de error 40197 proporciona información adicional sobre el tipo de saludo de error o conmutación por error que se ha producido. Algunos ejemplos de errores de hello códigos incrustados dentro del mensaje de saludo de error 40197 son 40020, 40143, 40166 y 40540.<br/><br/>Servidor de base de datos SQL de reconexión tooyour conectará automáticamente tooa copia correcta de la base de datos. La aplicación debe detectar el error 40197, registro Hola incrustado código de error (%d) dentro de mensaje de Hola para solucionar problemas e intente conectarse de nuevo tooSQL base de datos hasta que Hola recursos están disponibles, y la conexión se establezca de nuevo. |
| 40501 |20 | |servicio de Hello está ocupado actualmente. Vuelva a intentar la solicitud de hello tras 10 segundos. Identificador de incidente: %ls. Código: %d.<br/><br/>*Nota:* Para obtener más información, consulte:<br/>• [Límites de recursos de Base de datos SQL](sql-database-resource-limits.md). |
| 40613 |17 |La base de datos '%.&#x2a;ls' en el servidor '%.&#x2a;ls' no está disponible actualmente. Vuelva a intentar la conexión de hello más tarde. Si persiste el problema de hello, póngase en contacto con soporte al cliente y proporcióneles Hola Id. de seguimiento de sesión de '%. & #x2a; ls'. |
| 49918 |16 |No se puede procesar la solicitud. No hay suficientes recursos tooprocess la solicitud.<br/><br/>servicio de Hello está ocupado actualmente. Vuelva a intentar la solicitud de hello más tarde. |
| 49919 |16 |No se procesar, crear ni actualizar la solicitud. Hay demasiadas operaciones de creación o actualización en curso para la suscripción "%ld".<br/><br/>Hola servicio está ocupado procesando varios crear o actualizar las solicitudes de la suscripción o el servidor. Actualmente las solicitudes están bloqueadas para la optimización de recursos. Consulta [sys.dm_operation_status](https://msdn.microsoft.com/library/dn270022.aspx) para las operaciones pendientes. Espere a que se completen solicitudes de creación o actualización pendientes o elimine una de las solicitudes pendientes y vuelva a intentar la solicitud más tarde. |
| 49920 |16 |No se puede procesar la solicitud. Hay demasiadas operaciones en curso para la suscripción "%ld".<br/><br/>servicio de Hello está ocupado procesando varias solicitudes para esta suscripción. Actualmente las solicitudes están bloqueadas para la optimización de recursos. Consulta [sys.dm_operation_status](https://msdn.microsoft.com/library/dn270022.aspx) para el estado de la operación. Espere a que las solicitudes pendientes se hayan completado o elimine una de las solicitudes pendientes y vuelva a intentar la solicitud más tarde. |
| 4221 |16 |Error de inicio de sesión tooread-base de datos secundaria debido espera toolong en 'HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING'. Hola réplica no está disponible para el inicio de sesión porque faltan las versiones de fila para las transacciones que estaban en curso cuando se recicla la réplica de Hola. Hola problema puede resolverse por revertir o confirmar las transacciones activas de hello en la réplica principal de Hola. Repeticiones de esta condición pueden reducirse al evitar las transacciones de escritura de larga duración en hello principal. |

## <a name="database-copy-errors"></a>Errores de copia de base de datos
Hola siguientes errores puede encontrarse al copiar una base de datos en la base de datos de SQL Azure. Para más información, vea [Copiar una base de datos SQL de Azure](sql-database-copy.md).

| Código de error | Gravedad | Descripción |
| ---:| ---:|:--- |
| 40635 |16 |El cliente con la dirección IP '%.&#x2a;ls' está deshabilitado temporalmente. |
| 40637 |16 |Crear copia de base de datos está deshabilitado actualmente. |
| 40561 |16 |Error al copiar la base de datos. Cualquier base de datos de origen o destino de hello no existe. |
| 40562 |16 |Error al copiar la base de datos. se quitó la base de datos de origen de Hola. |
| 40563 |16 |Error al copiar la base de datos. se quitó la base de datos de destino de Hola. |
| 40564 |16 |No se pudo copiar base de datos debido a error interno de tooan. Quite la base de datos de destino e inténtelo de nuevo. |
| 40565 |16 |Error al copiar la base de datos. Copia de no más de 1 base de datos simultáneas de Hola se permite el mismo origen. Quite la base de datos de destino y vuelva a intentarlo más adelante. |
| 40566 |16 |No se pudo copiar base de datos debido a error interno de tooan. Quite la base de datos de destino e inténtelo de nuevo. |
| 40567 |16 |No se pudo copiar base de datos debido a error interno de tooan. Quite la base de datos de destino e inténtelo de nuevo. |
| 40568 |16 |Error al copiar la base de datos. La base de datos de origen ha dejado de estar disponible. Quite la base de datos de destino e inténtelo de nuevo. |
| 40569 |16 |Error al copiar la base de datos. La base de datos de destino ha dejado de estar disponible. Quite la base de datos de destino e inténtelo de nuevo. |
| 40570 |16 |No se pudo copiar base de datos debido a error interno de tooan. Quite la base de datos de destino y vuelva a intentarlo más adelante. |
| 40571 |16 |No se pudo copiar base de datos debido a error interno de tooan. Quite la base de datos de destino y vuelva a intentarlo más adelante. |

## <a name="resource-governance-errors"></a>Errores de regulación de recursos
Hola siguientes errores está provocado por el uso excesivo de recursos mientras se trabaja con la base de datos de SQL Azure. Por ejemplo:

* Una transacción ha permanecido abierta durante demasiado tiempo.
* Una transacción contiene demasiados bloqueos.
* Una aplicación consume demasiada memoria.
* Una aplicación consume demasiado espacio en `TempDb` .

Temas relacionados:

* Encontrará información más detallada aquí: [Límites de recursos de Base de datos SQL de Azure](sql-database-resource-limits.md)

| Código de error | Gravedad | Descripción |
| ---:| ---:|:--- |
| 10928 |20 |Id. de recurso: %d. límite de %s Hola para base de datos de hello es %d y se ha alcanzado. Para más información, vea [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637).<br/><br/>recursos de Hola que ha alcanzado el límite de Hola indica mediante Hola Id. de recurso. Para los subprocesos de trabajo, Hola Id. de recurso = 1. Para las sesiones, Hola Id. de recurso = 2.<br/><br/>*Nota:* para obtener más información sobre este error y cómo tooresolve, consulte:<br/>• [Límites de recursos de Base de datos SQL](sql-database-resource-limits.md). |
| 10929 |20 |Id. de recurso: %d. garantía mínima de Hello %s es %d, límite máximo es %d y uso actual de Hola de base de datos de hello es %d. Sin embargo, el servidor de hello está actualmente demasiado ocupado toosupport solicitudes mayores que %d para esta base de datos. Para más información, vea [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637). De lo contrario, Inténtelo de nuevo más tarde.<br/><br/>recursos de Hola que ha alcanzado el límite de Hola indica mediante Hola Id. de recurso. Para los subprocesos de trabajo, Hola Id. de recurso = 1. Para las sesiones, Hola Id. de recurso = 2.<br/><br/>*Nota:* para obtener más información sobre este error y cómo tooresolve, consulte:<br/>• [Límites de recursos de Base de datos SQL](sql-database-resource-limits.md). |
| 40544 |20 | |base de datos de Hello ha alcanzado su cuota de tamaño. Cree particiones o elimine datos, quite índices o consulte la documentación de Hola para ver posibles soluciones. |
| 40549 |16 |La sesión terminó porque tiene una transacción de larga duración. Intente reducir la transacción. |
| 40550 |16 |Hola sesión ha terminado porque ha adquirido demasiados bloqueos. Intente leer o modificar menos filas en una sola transacción. |
| 40551 |16 |Hola sesión ha terminado debido a exceso `TEMPDB` uso. Intente modificar el uso del espacio de tabla temporal de consulta tooreduce Hola.<br/><br/>*Sugerencia:* si está usando objetos temporales, puede ahorrar espacio en hello `TEMPDB` base de datos colocando objetos temporales después de sesión de hello ya no los necesite. |
| 40552 |16 |Hola sesión ha terminado debido al uso de espacio de registro de transacciones excesivo. Intente modificar menos filas en una sola transacción.<br/><br/>*Sugerencia:* si realiza inserciones masivas mediante hello `bcp.exe` utilidad o hello `System.Data.SqlClient.SqlBulkCopy` clase, pruebe a usar hello `-b batchsize` o `BatchSize` número de hello toolimit de opciones de filas se han copiado toohello server en cada transacción. Si se regenera un índice con hello `ALTER INDEX` (instrucción), pruebe a utilizar hello `REBUILD WITH ONLINE = ON` opción. |
| 40553 |16 |Hola sesión ha terminado debido al uso excesivo de memoria. Intente modificar la consulta tooprocess menos filas.<br/><br/>*Sugerencia:* reducir el número de Hola de `ORDER BY` y `GROUP BY` operaciones en el código de Transact-SQL reduce los requisitos de memoria de saludo de la consulta. |

## <a name="elastic-pool-errors"></a>Errores de grupos elásticos
Hola siguientes errores es toocreating relacionado y uso de grupos de Elastics.

| ErrorNumber | ErrorSeverity | ErrorFormat | ErrorInserts | ErrorCause | ErrorCorrectiveAction |
|:--- |:--- |:--- |:--- |:--- |:--- |
| 1132 |EX_RESOURCE |grupo elástico Hola ha alcanzado su límite de almacenamiento. uso de almacenamiento de Hello para el grupo elástico hello no puede superar los MB (%d). |Límite de espacio del grupo elástico en MB. |Se intentó una base de datos de toowrite datos tooa cuando se ha alcanzado el límite de almacenamiento de Hola de grupo elástico Hola. |Considere la posibilidad de Dtu de hello creciente de grupo elástico Hola si es posible en orden tooincrease su límite de almacenamiento, reducir almacenamiento de hello usado por las bases de datos individuales dentro de grupo elástico de hello o bien quitar las bases de datos de grupo elástico Hola. |
| 10929 |EX_USER |garantía mínima de Hello %s es %d, límite máximo es %d y uso actual de Hola de base de datos de hello es %d. Sin embargo, el servidor de hello está actualmente demasiado ocupado toosupport solicitudes mayores que %d para esta base de datos. Vea [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637) para obtener ayuda. De lo contrario, Inténtelo de nuevo más tarde. |Número mínimo de DTU por cada base de datos; número máximo de DTU por base de datos. |Hola número total de trabajos simultáneos (solicitudes) a través de todas las bases de datos de límite de grupo de hello grupo elástico tooexceed ha intentado Hola. |Por favor, considere la posibilidad de aumentar su límite de trabajo de hello Dtu de grupo elástico Hola si es posible en orden tooincrease o quitar las bases de datos de grupo elástico de Hola. |
| 40844 |EX_USER |La base de datos '%ls' del servidor '%ls' es una base de datos de la versión '%ls' de un grupo elástico y no puede tener una relación de copia continua. |Nombre de la base de datos, versión de base de datos, nombre del servidor. |Se emitió un comando StartDatabaseCopy para una base de datos que no es Premium de un grupo elástico. |Próximamente |
| 40857 |EX_USER |Grupo elástico no encontrado para el servidor: '%ls', nombre del grupo elástico: '%ls'. |Nombre del servidor; nombre del grupo elástico. |Grupo elástico especificado no existe en el servidor especificado de Hola. |Especifique un nombre de grupo elástico válido. |
| 40858 |EX_USER |El grupo elástico '%ls' ya existe en el servidor: '%ls' |Nombre de grupo elástico, nombre del servidor. |Grupo elástico especificado ya existe en el servidor lógico de hello especificado. |Proporcione un nuevo nombre de grupo elástico. |
| 40859 |EX_USER |El grupo elástico no admite el nivel de servicio '%ls'. |Nivel de servicio de grupo elástico. |El nivel de servicio especificado no se admite para el aprovisionamiento de grupo elástico. |Proporcionar la edición correcta de Hola o deje el nivel de servicio de servicio capa toouse en blanco Hola de forma predeterminada. |
| 40860 |EX_USER |La combinación del grupo elástico '%ls' y del objetivo de servicio '%ls' no es válida. |Nombre del grupo flexible; nombre del objetivo de nivel de servicio. |El grupo elástico y el objetivo de servicio pueden especificarse juntos solo si se especifica el objetivo de servicio como "ElasticPool". |Especifique la combinación correcta de grupo elástico y objetivo de servicio. |
| 40861 |EX_USER |edición de la base de datos de Hello ' %. *ls' no pueden ser diferentes de nivel de servicio de grupo elástico de Hola que es ' %.* ls'. |Versión de la base de datos, nivel de servicio del grupo elástico. |edición de la base de datos de Hello es diferente de nivel de servicio del grupo elástico de Hola. |No especifique una edición de base de datos que es diferente de nivel de servicio del grupo elástico de Hola.  Tenga en cuenta que esa edición de base de datos de hello no es necesario toobe especificado. |
| 40862 |EX_USER |Nombre de grupo elástico debe especificar si se especifica el objetivo de servicio del grupo elástico de Hola. |None |El objetivo del servicio de grupo elástico no identifica de manera única un grupo elástico. |Especifique el nombre del grupo elástico de hello si usa el objetivo de servicio del grupo elástico de Hola. |
| 40864 |EX_USER |Hola Dtu de grupo elástico Hola debe ser como mínimo (%d) en Dtu de nivel de servicio ' %. * ls'. |Número de DTU del grupo elástico; nivel de servicio del grupo elástico. |Se intentó una tooset hello Dtu de grupo elástico de Hola por debajo del límite mínimo de Hola. |Vuelva a intentar establecer hello Dtu para hello grupo elástico tooat menos límite mínimo de Hola. |
| 40865 |EX_USER |Hola Dtu de grupo elástico hello no puede superar (%d) en Dtu de nivel de servicio ' %. * ls'. |Número de DTU del grupo elástico; nivel de servicio del grupo elástico. |Se intentó una tooset hello Dtu de grupo elástico de Hola por encima del límite máximo de Hola. |Vuelva a intentar establecer mayor que el límite máximo de Hola Hola Dtu para toono de grupo elástico Hola. |
| 40867 |EX_USER |Hola DTU máx. por base de datos debe ser al menos (%d) de nivel de servicio ' %. * ls'. |Número máximo de DTU por base de datos, nivel de servicio del grupo elástico. |Intentar tooset hello DTU máx. por base de datos por debajo de hello admite límite. |Por favor, considere el uso de nivel de servicio de grupo elástico de Hola que admite la configuración de hello deseado. |
| 40868 |EX_USER |Hola DTU máx. por base de datos no puede superar (%d) de nivel de servicio ' %. * ls'. |Número máximo de DTU por base de datos, nivel de servicio del grupo elástico. |Intentar tooset hello DTU máx. por base de datos más allá de hello admite límite. |Por favor, considere el uso de nivel de servicio de grupo elástico de Hola que admite la configuración de hello deseado. |
| 40870 |EX_USER |Hola DTU mín. por base de datos no puede superar (%d) de nivel de servicio ' %. * ls'. |Número mínimo de DTU por base de datos, nivel de servicio del grupo elástico. |Intentar tooset hello DTU mín. por base de datos más allá de hello admite límite. |Por favor, considere el uso de nivel de servicio de grupo elástico de Hola que admite la configuración de hello deseado. |
| 40873 |EX_USER |número de Hola de bases de datos (%d) y DTU mín. por base de datos (%d) no puede superar hello Dtu de grupo elástico de hello (%d). |Número de bases de datos del grupo elástico; número mínimo de DTU por base de datos; número de DTU del grupo elástico. |Se intentó una toospecify DTU mínima para bases de datos de grupo elástico Hola que supera hello Dtu de grupo elástico Hola. |Considere la posibilidad de aumentar hello Dtu de grupo elástico de hello, o reducir hello DTU mín. por base de datos o bien, reducir el número de Hola de bases de datos de grupo elástico de Hola. |
| 40877 |EX_USER |No se puede eliminar un grupo elástico a menos que no contenga ninguna base de datos. |None |grupo elástico Hello contiene uno o más bases de datos y, por tanto, no se puede eliminar. |Por favor, quitar las bases de datos de grupo elástico de hello en orden toodelete se. |
| 40881 |EX_USER |Hola grupo elástico ' %. * ls' ha alcanzado el límite del número de base de datos.  límite de cantidad de base de datos de Hola de grupo elástico hello no puede superar (%d) para un grupo elástico con (%d) Dtu. |Nombre del grupo elástico; límite de bases de datos del grupo elástico; número de eDTU del grupo de recursos. |Agregar grupo de tooelastic de base de datos cuando se alcanza el límite del número de base de datos de Hola de grupo elástico de Hola o lo intentan toocreate. |Por favor, considere aumentar el límite de la base de datos de hello Dtu de grupo elástico Hola si es posible en orden tooincrease o quitar las bases de datos de grupo elástico Hola. |
| 40889 |EX_USER |Hola Dtu o límite de almacenamiento para el grupo elástico hello ' %. * ls' no se puede reducir desde que no proporcionaría suficiente espacio de almacenamiento para sus bases de datos. |Nombre del grupo elástico. |Intento de límite de almacenamiento de hello toodecrease de grupo elástico de Hola por debajo de su uso de almacenamiento. |Considere la posibilidad de reducir el uso de almacenamiento de Hola de bases de datos individuales en el grupo elástico de Hola o quitar bases de datos de grupo de hello en orden tooreduce su Dtu o almacenamiento de límite. |
| 40891 |EX_USER |Hola DTU mín. por base de datos (%d) no puede superar el número máximo DTU de Hola por base de datos (%d). |Número mínimo de DTU por base de datos; número máximo de DTU por base de datos. |Se intentó una tooset hello DTU mín. por base de datos mayor que hello DTU máx. por base de datos. |Asegúrese de hello DTU mín. por las bases de datos no supere los hello DTU máx. por base de datos. |
| TBD |EX_USER |tamaño de almacenamiento de Hola para una base de datos individual en un grupo elástico no puede superar el tamaño máximo de hello permitido por ' %. * ls' grupo elástico de nivel de servicio. |Nivel de servicio de grupo elástico. |tamaño máximo de Hola para base de datos de hello excede el tamaño máximo de hello permitido por nivel de servicio del grupo elástico de Hola. |Establezca el tamaño máximo de Hola de base de datos de hello dentro de los límites de Hola de hello tamaño máximo permitido por nivel de servicio del grupo elástico de Hola. |

Temas relacionados:

* [Creación de un grupo elástico (C#)](sql-database-elastic-pool-manage-csharp.md) 
* [Administración de un grupo de bases de datos elásticas (C#)](sql-database-elastic-pool-manage-csharp.md) 
* [Creación de un grupo de bases de datos elásticas (PowerShell)](sql-database-elastic-pool-manage-powershell.md) 
* [Supervisión y administración de un grupo elástico (PowerShell)](sql-database-elastic-pool-manage-powershell.md)

## <a name="general-errors"></a>Errores generales
Hola siguientes errores no pertenecen a las categorías anteriores.

| Código de error | Gravedad | Descripción |
| ---:| ---:|:--- |
| 15006 |16 |<AdministratorLogin> no es un nombre válido porque contiene caracteres no válidos. |
| 18452 |14 |Error de inicio de sesión. es de un dominio de confianza Hello inicio de sesión y no se puede usar con Windows authentication.%. & #x2a; ls (inicios de sesión de Windows no se admiten en esta versión de SQL Server). |
| 18456 |14 |Error de inicio de sesión para el usuario ' %. #x2a;ls'.%. & #x2a; % ls. & #x2a; ls (error de inicio de sesión de hello para el usuario "%. & #x2a; ls". Error de cambio de contraseña de Hola. El cambio de contraseña durante el inicio de sesión no se admite en esta versión de SQL Server.) |
| 18470 |14 |Error de inicio de sesión del usuario '%.&#x2a;ls'. Motivo: cuenta de hello es disabled.%. & #x2a; ls |
| 40014 |16 |No se puede usar varias bases de datos en hello misma transacción. |
| 40054 |16 |No se admiten las tablas sin un índice agrupado en esta versión de SQL Server. Crear un índice agrupado e inténtelo de nuevo. |
| 40133 |15 |No se admite esta operación en esta versión de SQL Server. |
| 40506 |16 |El SID especificado no es válido para esta versión de SQL Server. |
| 40507 |16 |No se puede invocar '%.&#x2a;ls' con parámetros en esta versión de SQL Server. |
| 40508 |16 |Instrucción USE no es compatible tooswitch entre bases de datos. Use la nueva conexión tooconnect tooa otra base de datos. |
| 40510 |16 |No se admite la instrucción '%.&#x2a;ls' en esta versión de SQL Server. |
| 40511 |16 |No se admite la instrucción integrada '%.&#x2a;ls' en esta versión de SQL Server. |
| 40512 |16 |No se admite la característica desusada '%ls' en esta versión de SQL Server. |
| 40513 |16 |No se admite la variable del servidor '%.&#x2a;ls' en esta versión de SQL Server. |
| 40514 |16 |No se admite '%ls' en esta versión de SQL Server. |
| 40515 |16 |Nombre de referencia toodatabase o del servidor en ' %. & #x2a; ls' no se admite en esta versión de SQL Server. |
| 40516 |16 |Los objetos temporales globales no se admiten en esta versión de SQL Server. |
| 40517 |16 |No se admite la opción de palabra clave o instrucción '%.&#x2a;ls' en esta versión de SQL Server. |
| 40518 |16 |No se admite el comando DBCC '%.&#x2a;ls' en esta versión de SQL Server. |
| 40520 |16 |La clase protegible '%S_MSG' no se admite en esta versión de SQL Server. |
| 40521 |16 |Clase protegible '% S_MSG' no se admite en el ámbito del servidor hello en esta versión de SQL Server. |
| 40522 |16 |El tipo de entidad de seguridad de base de datos '%.&#x2a;ls' no se admite en esta versión de SQL Server. |
| 40523 |16 |La creación de usuario implícita '%.&#x2a;ls' no se admite en esta versión de SQL Server. Cree explícitamente usuario Hola antes de usarlo. |
| 40524 |16 |El tipo de datos '%.&#x2a;ls' no se admite en esta versión de SQL Server. |
| 40525 |16 |WITH '%ls' no se admite en esta versión de SQL Server. |
| 40526 |16 |El proveedor de conjuntos de filas '%.&#x2a;ls' no se admite en esta versión de SQL Server. |
| 40527 |16 |Los servidores vinculados no se admiten en esta versión de SQL Server. |
| 40528 |16 |Los usuarios no pueden ser toocertificates asignadas, las claves asimétricas o inicios de sesión de Windows en esta versión de SQL Server. |
| 40529 |16 |La función integrada '%.&#x2a;ls' en el contexto de suplantación no se admite en esta versión de SQL Server. |
| 40532 |11 |No se puede abrir el servidor "%. & #x2a; %.*ls" solicitada por el inicio de sesión de Hola. Error de inicio de sesión de Hola. |
| 40553 |16 |Hola sesión ha terminado debido al uso excesivo de memoria. Intente modificar la consulta tooprocess menos filas.<br/><br/>*Nota:* reducir el número de Hola de `ORDER BY` y `GROUP BY` operaciones en el código de Transact-SQL ayuda a reducir los requisitos de memoria de saludo de la consulta. |
| 40604 |16 |Podría no CREATE/ALTER DATABASE porque superaría la cuota de Hola de servidor hello. |
| 40606 |16 |Adjuntar base de datos no se admite en esta versión de SQL Server. |
| 40607 |16 |Los inicios de sesión de Windows no se admiten en esta versión de SQL Server. |
| 40611 |16 |Los servidores pueden tener como máximo 128 reglas de firewall definidas. |
| 40614 |16 |La dirección IP de inicio de la regla de firewall no puede superar la dirección IP final. |
| 40615 |16 |No se puede abrir el servidor '{0}' solicitado por el inicio de sesión de Hola. Cliente con la dirección IP '{1}' no tiene servidor de hello tooaccess.  acceso de tooenable, usar hello Portal de la base de datos de SQL o ejecute sp_set_firewall_rule en la base de datos maestra de hello toocreate una regla de firewall para esta dirección IP o intervalo de direcciones.  Puede tardar minutos toofive para este efecto tootake de cambio. |
| 40617 |16 |nombre de regla de firewall de Hola que comienza con <rule name> es demasiado largo. La longitud máxima es 128. |
| 40618 |16 |nombre de regla de firewall de Hello no puede estar vacío. |
| 40620 |16 |Error de inicio de sesión de Hello para el usuario "%. & #x2a; ls". Error de cambio de contraseña de Hola. El cambio de contraseña durante el inicio de sesión no se admite en esta versión de SQL Server. |
| 40627 |20 |La operación en el servidor '{0}' y la base de datos '{1}' está en curso. Espere algunos minutos antes de volver a intentarlo. |
| 40630 |16 |Error de validación de contraseña. Hola contraseña no cumple los requisitos de directiva porque es demasiado corta. |
| 40631 |16 |contraseña de Hola que especificó es demasiado largo. Hola debe tener no más de 128 caracteres. |
| 40632 |16 |Error de validación de contraseña. contraseña de Hello no cumple los requisitos de directiva porque no es bastante compleja. |
| 40636 |16 |No se puede usar un nombre de base de datos reservado '%.&#x2a;ls' en esta operación. |
| 40638 |16 |Id. de suscripción <identificador_de_suscripción> no válido. La suscripción no existe. |
| 40639 |16 |Solicitud no es conforme tooschema: <schema error>. |
| 40640 |20 | |servidor de Hello detectó una excepción inesperada. |
| 40641 |16 |Hola especifica la ubicación no es válida. |
| 40642 |17 |Hola servidor actualmente está demasiado ocupado. Inténtelo de nuevo más tarde. |
| 40643 |16 |Hola especifica el valor del encabezado x-ms-version no es válido. |
| 40644 |14 |Tooauthorize error acceso toohello especifica la suscripción. |
| 40645 |16 |El nombre de servidor <servername> no puede estar vacío ni ser NULL. Solo puede se compone de letras minúsculas 'a'-'z', números de hello 0-9 y guión Hola. guión de Hello no puede producir o final Hola nombre. |
| 40646 |16 |El id. de suscripción no puede estar vacío. |
| 40647 |16 |La suscripción <subscription-id no tiene nombre de servidor. |
| 40648 |17 |Se han realizado demasiadas solicitudes. Inténtelo de nuevo más tarde. |
| 40649 |16 |Se ha especificado un content-type no válido. Solo se admite application/xml. |
| 40650 |16 |Suscripción < id-suscripción > no existe o no está preparada para el funcionamiento de Hola. |
| 40651 |16 |No se pudo toocreate server porque la suscripción Hola < id-suscripción > está deshabilitada. |
| 40652 |16 |No se puede mover ni crear un servidor. La suscripción <subscription-id> superará la cuota de servidor. |
| 40671 |17 |Error de comunicación entre la puerta de enlace de Hola y el servicio de administración de Hola. Inténtelo de nuevo más tarde. |
| 40852 |16 |No se puede abrir la base de datos ' %. *ls' en el servidor ' %.* ls' solicitado por el inicio de sesión de Hola. Base de datos de Access toohello solo se permite usar una cadena de conexión con seguridad habilitada. tooaccess esta base de datos, modifique la toocontain de cadenas de conexión 'segura' en el servidor de hello FQDN -.database.windows 'nombreDeServidor'.net debe ser modificada too'server nombre ' base de datos. `secure`. windows.net. |
| 45168 |16 |Hola sistema SQL Azure está bajo carga y está colocando un límite superior en operaciones DB CRUD simultáneas para un único servidor (por ejemplo, crear base de datos). servidor Hello especificado en el mensaje de error de hello ha superado el número máximo de Hola de conexiones simultáneas. Inténtelo de nuevo más tarde. |
| 45169 |16 |Hola sistema SQL azure está bajo carga y está colocando un límite superior en el número de Hola de operaciones CRUD de servidor simultáneas para una sola suscripción (por ejemplo, create server). suscripción de Hola especificado en error Hola mensaje superó el número máximo de Hola de conexiones simultáneas y se denegó la solicitud de saludo. Inténtelo de nuevo más tarde. |

## <a name="related-links"></a>Vínculos relacionados
* [Características de Azure SQL Database](sql-database-features.md)
* [Límites de recursos de Base de datos SQL](sql-database-resource-limits.md)

