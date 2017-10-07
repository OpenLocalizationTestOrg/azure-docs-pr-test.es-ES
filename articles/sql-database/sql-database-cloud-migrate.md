---
title: "tooAzure base de datos SQL de la migración de base de datos del servidor aaaSQL | Documentos de Microsoft"
description: "Obtenga información sobre SQL Server el tooAzure de la migración de base de datos base de datos de SQL en la nube de Hola. Usar la migración de base de datos migración herramientas tootest compatibilidad toodatabase anterior."
keywords: "migración de base de datos, migración de base de datos de sql server, herramientas de migración de bases de datos, migración de la base de datos, migrar base de datos sql"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 9cf09000-87fc-4589-8543-a89175151bc2
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-migrate
ms.date: 02/08/2017
ms.author: carlrab
ms.openlocfilehash: 3a5e879404dd2da1dd5254a6134e3ee1517648db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-database-migration-toosql-database-in-hello-cloud"></a>TooSQL de migración de base de datos de SQL Server la base de datos en la nube de Hola
En este artículo, aprenderá sobre Hola dos métodos principales para migrar un SQL Server 2005 o posterior tooAzure de base de datos base de datos SQL. Hello primer método es más sencillo, pero requiere algunos, posiblemente considerable, tiempo de inactividad durante la migración de Hola. Hola segundo método es más complejo, pero elimina considerablemente el tiempo de inactividad durante la migración de Hola.

En ambos casos, deberá tooensure esa base de datos de origen de hello es compatible con la base de datos de SQL de Azure con hello [Asistente de migración de datos (DMA)](https://www.microsoft.com/download/details.aspx?id=53595). Se está aproximando V12 de base de datos de SQL [paridad de características](sql-database-features.md) con SQL Server, que no sea de operaciones de nivel de tooserver y entre bases de datos relacionadas con problemas. Las bases de datos y las aplicaciones que se basan en [parcialmente compatibles o funciones no compatibles con](sql-database-transact-sql-information.md) necesita algunos [volver a ingeniería toofix estas incompatibilidades](sql-database-cloud-migrate.md#resolving-database-migration-compatibility-issues) antes de hello SQL Server se puede migrar la base de datos.

> [!NOTE]
> toomigrate una base de datos no es de SQL Server, como Microsoft Access, Sybase, MySQL Oracle y DB2 tooAzure base de datos de SQL, consulte [SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2016/12/22/released-sql-server-migration-assistant-ssma-v7-2/).
> 

## <a name="method-1-migration-with-downtime-during-hello-migration"></a>Método 1: Migración con el tiempo de inactividad durante la migración de Hola

 Utilice este método si puede permitirse algún tiempo de inactividad o va a realizar una migración de prueba de la base de datos de producción para una migración posterior. Para consultar un tutorial, vea [Migración de una base de datos de SQL Server](sql-database-migrate-your-sql-server-database.md).

Hello lista siguiente contiene un flujo de trabajo general de Hola para una migración de base de datos de SQL Server con este método.

  ![Diagrama de migración de VSSSDT](./media/sql-database-cloud-migrate/azure-sql-migration-sql-db.png)

1. Evaluar la base de datos de hello para la compatibilidad con la versión más reciente de Hola de [Asistente de migración de datos (DMA)](https://www.microsoft.com/download/details.aspx?id=53595).
2. Prepare todas las correcciones necesarias como scripts de Transact-SQL.
3. Realizar una copia transaccionalmente coherente de la base de datos de origen de hello migrarse - y asegúrese de que se va a realizar ningún cambio adicional toohello base de datos de origen (o puede aplicar manualmente los cambios una vez completada la migración de hello). Hay muchas tooquiesce métodos una base de datos, desactive toocreating de conectividad de cliente de un [instantánea de base de datos](https://msdn.microsoft.com/library/ms175876.aspx).
4. Implementar Hola Transact-SQL scripts tooapply Hola correcciones toohello base de datos copia.
5. [Exportar](sql-database-export.md) Hola tooa de copia de base de datos. Archivo BACPAC en una unidad local.
6. [Importar](sql-database-import.md) Hola. Archivo BACPAC como una nueva base de datos de SQL Azure mediante cualquiera de varios BACPAC importe tools, con SQLPackage.exe que se va a Hola recomienda herramienta para mejorar el rendimiento.

### <a name="optimizing-data-transfer-performance-during-migration"></a>Optimización del rendimiento de transferencia de datos durante la migración 

Hola lista siguiente contiene recomendaciones para mejorar el rendimiento durante el proceso de importación de Hola.

* Elija hello más alto nivel de servicio y el rendimiento de nivel que el presupuesto permite el rendimiento de la transferencia de toomaximize Hola. Puede reducir el escalado finalizar la migración de hello toosave dinero. 
* Minimizar Hola distancia entre su. BACPAC hello y archivo data center de destino.
* Deshabilite las estadísticas automáticas durante la migración.
* Cree particiones de tablas e índices.
* Quite las vistas indexadas y vuelva a crearlas cuando se haya completado el proceso.
* Quitar base de datos de los datos históricos rara vez consultado tooanother y migrar tooa este datos históricos independiente base de datos de SQL Azure. A continuación, podrá consultar estos datos históricos mediante [consultas elásticas](sql-database-elastic-query-overview.md).

### <a name="optimize-performance-after-hello-migration-completes"></a>Optimizar el rendimiento de una vez completada la migración de Hola

[Actualizar las estadísticas](https://msdn.microsoft.com/library/ms187348.aspx) con un examen completo una vez completada la migración de Hola.

## <a name="method-2-use-transactional-replication"></a>Método 2: Uso de la replicación transaccional

Cuando no puede permitirse tooremove la base de datos de SQL Server de producción mientras se está produciendo la migración de hello, puede usar la replicación transaccional de SQL Server como la solución de migración. toouse este método, la base de datos de origen de hello debe satisfacer hello [requisitos para la replicación transaccional](https://msdn.microsoft.com/library/mt589530.aspx) y ser compatible con la base de datos de SQL Azure. Para más información acerca de la replicación de SQL con AlwaysOn, consulte [Configurar la replicación para grupos de disponibilidad AlwaysOn (SQL Server)](/sql/database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server).

toouse esta solución, se configura la base de datos de SQL Azure como una instancia de SQL Server toohello de suscriptor que desea toomigrate. distribuidor de replicación transaccional Hello sincroniza datos de toobe de base de datos de hello sincronizada (Editor de hello) mientras que las nuevas transacciones continúan se producen. 

Con la replicación transaccional, todos los cambios tooyour datos o esquema se muestran en la base de datos de SQL Azure. Una vez que sincronización hello es completa y está listo toomigrate, cambie la cadena de conexión de Hola de su toopoint aplicaciones ellos tooyour base de datos de SQL Azure. Una vez que la replicación transaccional purga los cambios a la izquierda en la base de datos de origen y todas sus aplicaciones punto tooAzure base de datos, puede desinstalar la replicación transaccional. Base de datos SQL de Azure es ahora su sistema de producción.

 ![Diagrama de SeedCloudTR](./media/sql-database-cloud-migrate/SeedCloudTR.png)

> [!TIP]
> También puede usar la replicación transaccional toomigrate un subconjunto de la base de datos de origen. publicación de Hola que replique tooAzure base de datos SQL puede ser tooa limitado subconjunto de tablas de hello en base de datos de hello está replicando. Para cada tabla que se está replicando, puede limitar tooa subconjunto de datos de Hola de filas de Hola o un subconjunto de columnas de Hola.
>

### <a name="migration-toosql-database-using-transaction-replication-workflow"></a>TooSQL de migración mediante el flujo de trabajo de replicación de transacciones de la base de datos

> [!IMPORTANT]
> Usar versión más reciente de Hola de SQL Server Management Studio tooremain había sincronizado con actualizaciones tooMicrosoft Azure y base de datos SQL. Las versiones anteriores de SQL Server Management Studio no pueden configurar la instancia de Base de datos SQL como suscriptor. [Actualice SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 

1. Configuración de la distribución
   -  [Uso de SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_1)
   -  [Uso de Transact-SQL](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_2)
2. Creación de publicación
   -  [Uso de SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_1)
   -  [Uso de Transact-SQL](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_2)
3. Creación de suscripción
   -  [Uso de SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_0)
   -  [Uso de Transact-SQL](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_1)

### <a name="some-tips-and-differences-for-migrating-toosql-database"></a>Algunas sugerencias y diferencias para migrar tooSQL base de datos

1. Uso de un distribuidor local 
   - Esto provoca un impacto en el rendimiento en el servidor de Hola. 
   - Si el impacto de rendimiento de hello es inaceptable, puede utilizar otro servidor pero agrega complejidad en administración de.
2. Al seleccionar una carpeta de instantáneas, asegúrese de la carpeta de hello seguro de que selecciona es lo suficientemente grande como toohold un BCP de cada tabla que desee tooreplicate. 
3. Bloqueos de creación de instantáneas Hola tablas asociadas hasta que se complete, por lo que programar de forma adecuada la instantánea. 
4. Azure SQL Database solo admite las suscripciones de inserción. Solo puede agregar los suscriptores de base de datos de origen de Hola.

## <a name="resolving-database-migration-compatibility-issues"></a>Solución de problemas de compatibilidad de migración de bases de datos
Hay una amplia variedad de problemas de compatibilidad que pueden surgir, tanto en la versión de Hola de SQL Server en función de complejidad de hello y base de datos de origen de Hola de base de datos de hello que va a migrar. Las versiones anteriores de SQL Server tienen más problemas de compatibilidad. Usar hello recursos siguientes, además tooa dirige búsqueda en Internet mediante el motor de búsqueda de opciones:

* [Características de Base de datos de SQL Server no admitidas en Base de datos SQL de Azure](sql-database-transact-sql-information.md)
* [Funcionalidad del motor de base de datos no incluida en SQL Server 2016](https://msdn.microsoft.com/library/ms144262%28v=sql.130%29)
* [Funcionalidad del motor de base de datos no incluida en SQL Server 2014](https://msdn.microsoft.com/library/ms144262%28v=sql.120%29)
* [Funcionalidad del motor de base de datos no incluida en SQL Server 2012](https://msdn.microsoft.com/library/ms144262%28v=sql.110%29)
* [Funcionalidad del motor de base de datos no incluida en SQL Server 2008 R2](https://msdn.microsoft.com/library/ms144262%28v=sql.105%29)
* [Funcionalidad del motor de base de datos no incluida en SQL Server 2005](https://msdn.microsoft.com/library/ms144262%28v=sql.90%29)

Además toosearching Hola Internet y utilizan estos recursos, utilice hello [foros de la Comunidad de SQL Server de MSDN](https://social.msdn.microsoft.com/Forums/sqlserver/home?category=sqlserver) o [StackOverflow](http://stackoverflow.com/).

## <a name="next-steps"></a>Pasos siguientes
* Usar script de hello en el blog de Azure SQL EMEA ingenieros de hello demasiado[supervisar el uso de tempdb durante la migración](https://blogs.msdn.microsoft.com/azuresqlemea/2016/12/28/lesson-learned-10-monitoring-tempdb-usage/).
* Usar script de hello en el blog de Azure SQL EMEA ingenieros de hello demasiado[supervisar el espacio de registro de transacciones de saludo de la base de datos mientras se está produciendo la migración](https://blogs.msdn.microsoft.com/azuresqlemea/2016/10/31/lesson-learned-7-monitoring-the-transaction-log-space-of-my-database/0).
* Para un equipo de asesoramiento de cliente de SQL Server utilizando los archivos BACPAC, consulte el blog sobre la migración [migración desde SQL Server tooAzure base de datos de SQL mediante archivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Para obtener información sobre cómo trabajar con la hora UTC después de la migración, consulte [Hola de zona horaria modificar predeterminada para la zona horaria local](https://blogs.msdn.microsoft.com/azuresqlemea/2016/07/27/lesson-learned-4-modifying-the-default-time-zone-for-your-local-time-zone/).
* Para obtener información acerca de cómo cambiar el idioma predeterminado de Hola de una base de datos después de la migración, consulte [cómo toochange Hola idioma predeterminado de la base de datos de SQL Azure](https://blogs.msdn.microsoft.com/azuresqlemea/2017/01/13/lesson-learned-16-how-to-change-the-default-language-of-azure-sql-database/).


