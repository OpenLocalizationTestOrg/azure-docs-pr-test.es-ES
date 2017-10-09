---
title: aaaCreate & Administrar servidores SQL Azure y bases de datos | Documentos de Microsoft
description: "Obtenga información acerca de conceptos de base de datos y servidor de base de datos de SQL Azure y acerca de la creación y administración de servidores y bases de datos mediante Hola portal de Azure, PowerShell, Hola CLI de Azure, Transact-SQL, hello y API de REST."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 0f526e388a5a620349f5a14e8d57a8355ac451ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-sql-database-servers-and-databases"></a>Creación y administración de servidores y bases de datos de Azure SQL Database

Una base de datos SQL de Azure es una base de datos administrada de Microsoft Azure creada dentro de un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) con un conjunto definido de [recursos de proceso y de almacenamiento para diferentes cargas de trabajo](sql-database-service-tiers.md). Una base de datos SQL de Azure está asociada con un servidor lógico de Azure SQL Database, que se crea dentro de una región específica de Azure. 

## <a name="an-azure-sql-database-can-be-a-single-pooled-or-partitioned-database"></a>Una base de datos SQL de Azure puede ser una base de datos única, agrupada o con particiones

Una base de datos SQL de Azure puede ser:

- Una base de datos única con su [propio conjunto de recursos](sql-database-what-is-a-dtu.md#what-are-database-transaction-units-dtus) (DTU).
- Parte de un [grupo elástico de SQL](sql-database-elastic-pool.md) que [comparte un conjunto de recursos](sql-database-what-is-a-dtu.md#what-are-elastic-database-transaction-units-edtus) (eDTU).
- Parte de un [conjunto escalado horizontalmente de bases de datos particionadas](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling), que pueden ser simples o agrupadas.
- Parte de un conjunto de bases de datos que participan en un [modelo de diseño de SaaS multiinquilino](sql-database-design-patterns-multi-tenancy-saas-applications.md) y cuyas bases de datos pueden ser simples o agrupadas (o ambas). 

> [!TIP]
> Para conocer los nombres de base de datos válidos, consulte [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) (Identificadores de base de datos). 
>
 
- intercalación de base de datos predeterminada de Hello utilizado por la base de datos de SQL de Microsoft Azure es **SQL_LATIN1_GENERAL_CP1_CI_AS**, donde **LATIN1_GENERAL** es inglés (Estados Unidos), **CP1** es la página de códigos 1252, **CI** distingue mayúsculas de minúsculas, y **AS** distingue acentos. Para obtener más información acerca de cómo tooset Hola intercalación, vea [COLLATE (Transact-SQL)](https://msdn.microsoft.com/library/ms184391.aspx).
- La Base de datos SQL de Microsoft Azure admite el cliente de protocolo de secuencia de datos tabular (TDS) en la versión 7.3 o posterior.
- Se permiten únicamente las conexiones TCP/IP.

## <a name="what-is-an-azure-sql-logical-server"></a>¿Qué es un servidor lógico de Azure SQL?

Un servidor lógico actúa como punto administrativo central para varias bases de datos, incluidos los [grupos elásticos de SQL](sql-database-elastic-pool.md) , los [inicios de sesión](sql-database-manage-logins.md), las [reglas de firewall](sql-database-firewall-configure.md), las [reglas de auditoría](sql-database-auditing.md), las [directivas de detección de amenazas](sql-database-threat-detection.md) y los [grupos de conmutación por error](sql-database-geo-replication-overview.md). Un servidor lógico puede estar en una región distinta a la de su grupo de recursos. servidor lógico Hola debe existir antes de poder crear base de datos de SQL Azure Hola. Todas las bases de datos en un servidor se crean en hello misma región que el servidor lógico Hola. 


> [!IMPORTANT]
> En la base de datos de SQL, un servidor es una construcción lógica que es distinta de una instancia de SQL Server que esté familiarizado con de Hola a todos en local. En concreto, Hola servicio de base de datos SQL no ofrece ninguna garantía con respecto a la ubicación de las bases de datos de hello relación de los servidores lógicos tootheir y no expone el acceso de nivel de instancia o características.
> 

Cuando se crea un servidor lógico, proporcionar a un servidor de cuenta de inicio de sesión y una contraseña que tenga derechos administrativos toohello base de datos maestra en ese servidor y todas las bases de datos creadas en ese servidor. Esta cuenta inicial es una cuenta de inicio de sesión de SQL. Azure SQL Database admite la autenticación de SQL y la autenticación de Azure Active Directory. Para obtener información sobre inicios de sesión y autenticación, vea [Administrar bases de datos e inicios de sesión en Azure SQL Database](sql-database-manage-logins.md). La autenticación de Windows no es compatible. 

> [!TIP]
> Para conocer cuáles son los nombres de servidor y de grupo de recursos válidos, vea las [reglas y restricciones de nomenclatura](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).
>

Un servidor lógico de Azure Database:

- Se crea dentro de una suscripción de Azure, pero se pueden mover a su suscripción de recursos independiente tooanother
- Recurso primario de Hola para grupos elásticos, bases de datos y almacenamientos de datos
- Proporciona un espacio de nombres para bases de datos, grupos elásticos y almacenamientos de datos.
- Es un contenedor lógico con la semántica de duración seguro - delete Elimina un servidor y lo Hola bases de datos independientes, grupos elásticos y almacenes de datos
- Participa en [control de acceso de Azure basada en roles (RBAC)](/active-directory/role-based-access-control-what-is) -grupos elásticos, bases de datos y almacenamientos de datos dentro de un servidor heredan derechos de acceso del servidor de Hola
- Es un elemento de orden superior de identidad de Hola de grupos elásticos, bases de datos y almacenamientos de datos de recursos de Azure con fines de administración (consulte la dirección URL de hello esquema de bases de datos y los grupos)
- Coloca recursos en una región.
- Proporciona un punto de conexión para el acceso a la base de datos (<serverName>. database.windows.net).
- Proporciona acceso toometadata con respecto a los recursos contenidos a través de las DMV por conexión tooa de base de datos maestra 
- Proporciona el ámbito de Hola para las directivas de administración que se aplican las bases de datos tooits - inicios de sesión, firewall, auditoría, etcetera, de detección de amenazas. 
- Está restringido por una cuota de suscripción de hello primario (seis servidores por suscripción de forma predeterminada, [vea suscripción limita aquí](../azure-subscription-service-limits.md))
- Proporciona el ámbito de hello para la cuota de base de datos y la cuota DTU para recursos de Hola que contiene (por ejemplo, DTU 45.000)
- Es el ámbito de control de versiones de Hola para funciones que se habilitan en recursos independientes 
- Los inicios de sesión de la entidad de seguridad en el nivel de servidor pueden administrar todas las bases de datos en un servidor.
- Puede contener inicios de sesión toothose similar en instancias de SQL Server en su infraestructura local que se les conceda acceso tooone o más bases de datos en el servidor de Hola y puede conceder los derechos administrativos limitados. Para obtener más información, consulte el artículo sobre [inicios de sesión](sql-database-manage-logins.md).

## <a name="azure-sql-databases-protected-by-sql-database-firewall"></a>Protección de bases de datos SQL de Azure con el firewall de SQL Database

toohelp proteger sus datos, un [firewall de base de datos SQL](sql-database-firewall-configure.md) evita que todos los servidores de base de datos de access tooyour o cualquiera de sus bases de datos desde fuera de su servidor de toohello de conexión directamente a través de la conexión de suscripción de Azure. tooenable conectividad adicionales, debe [crear una o varias reglas de firewall](sql-database-firewall-configure.md#creating-and-managing-firewall-rules). Para crear y administrar grupos elásticos de SQL, vea [Grupos elásticos](sql-database-elastic-pool.md).

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-azure-portal"></a>Administrar servidores SQL Azure, las bases de datos y firewalls que usan Hola portal de Azure

Puede crear grupo de recursos de hello Azure base de datos SQL antemano o al crear el propio servidor hello. Existen varios métodos para obtener el nuevo formato SQL del servidor tooa, mediante la creación de un nuevo servidor de SQL server o como parte de la creación de una base de datos. 

### <a name="create-a-blank-sql-server-logical-server"></a>Creación de un servidor SQL en blanco (servidor lógico)

Hola toocreate un servidor (sin una base de datos) de la base de datos de SQL Azure mediante [portal de Azure](https://portal.azure.com), navegue tooa formulario de servidor (servidor lógico) de SQL en blanco. Hello captura de pantalla siguiente muestra un método para abrir un formulario toocreate un servidor SQL lógico en blanco. 

   ![formulario de creación de servidor lógico completado](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

Si se producen formulario toothis mediante otro método, información de hello en forma de hello es idéntica.

### <a name="create-a-blank-or-sample-sql-database"></a>Creación de una base de datos SQL de ejemplo o en blanco

Hola toocreate una base de datos de SQL Azure mediante [portal de Azure](https://portal.azure.com), desplácese tooa formulario de base de datos SQL en blanco y proporcionar Hola la información solicitada. Puede crear del Hola SQL Azure base de datos grupo de recursos y servidor lógico antes de tiempo o durante la creación de hello propia base de datos. Puede crear una base de datos en blanco o de ejemplo basada en Adventure Works LT. 

  ![create database-1](./media/sql-database-get-started-portal/create-database-1.png)

> [IMPORTANTE] Para obtener información sobre la selección de hello tarifa para la base de datos, vea [niveles de servicio](sql-database-service-tiers.md).
>

### <a name="manage-an-existing-sql-server"></a>Administración de un servidor SQL Server existente

toomanage un servidor existente, navegue a servidor toohello mediante una serie de métodos - como los datos de página de base de datos SQL específica, hello **servidores SQL Server** página o hello **todos los recursos** página. Hola siguiente captura de pantalla muestra cómo toobegin configurar un firewall de nivel de servidor desde hello **Introducción** página para un servidor. 

   ![información general del servidor lógico](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

toomanage una base de datos existente, navegue toohello **bases de datos SQL** página y haga clic en la base de datos de hello desea toomanage. Hola siguiente captura de pantalla muestra cómo toobegin configurar un firewall de nivel de servidor para una base de datos desde hello **Introducción** página para una base de datos. 

   ![regla de firewall del servidor](./media/sql-database-get-started-portal/server-firewall-rule.png) 

> [!IMPORTANT]
> propiedades de rendimiento tooconfigure para una base de datos, vea [niveles de servicio](sql-database-service-tiers.md).
>

> [!TIP]
> Para obtener un tutorial de inicio rápido de Azure portal, consulte [crear una base de datos de SQL Azure en el portal de Azure hello](sql-database-get-started-portal.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-powershell"></a>Administración de servidores, bases de datos y firewalls de Azure SQL con PowerShell

toocreate y administrar servidores de SQL Azure, las bases de datos y los servidores de seguridad con Azure PowerShell, use Hola siguientes cmdlets de PowerShell. Si necesita tooinstall o actualice PowerShell, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps). Para crear y administrar grupos elásticos de SQL, vea [Grupos elásticos](sql-database-elastic-pool.md).

| Cmdlet | Descripción |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Crea una base de datos. |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Obtiene una o más bases de datos.|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Establece las propiedades de una base de datos, o mueve una base de datos existente en un grupo elástico.|
|[Remove-AzureRmSqlDatabase](/powershell/module/azurerm.sql/remove-azurermsqldatabase)|Quita una base de datos.|
|[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)|Crea un grupo de recursos.
|[New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver)|Crea un servidor.|
|[Get-AzureRmSqlServer](/powershell/module/azurerm.sql/get-azurermsqlserver)|Devuelve información sobre los servidores.|
|[Set-AzureRmSqlServer](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/set-azurermsqlserver)|Modifica las propiedades de un servidor.|
|[Remove-AzureRmSqlServer](/powershell/module/azurerm.sql/remove-azurermsqlserver)|Quita un servidor.|
|[New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule)|Crea una regla de firewall de nivel de servidor. |
|[Get-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/get-azurermsqlserverfirewallrule)|Obtiene reglas de firewall para un servidor|
|[Set-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/set-azurermsqlserverfirewallrule)|Modifica una regla de firewall en un servidor.|
|[Remove-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/remove-azurermsqlserverfirewallrule)|Obtiene una regla de firewall de un servidor.|

> [!TIP]
> Para obtener un tutorial de inicio rápido de PowerShell, vea [Creación de una sola instancia de Azure SQL Database con PowerShell](sql-database-get-started-portal.md). Para los scripts de ejemplo de PowerShell, consulte [toocreate de PowerShell de usar una instancia única de SQL Azure la base de datos y configurar una regla de firewall](scripts/sql-database-create-and-configure-database-powershell.md) y [Monitor y escala una instancia única de SQL de base de datos mediante PowerShell](scripts/sql-database-monitor-and-scale-database-powershell.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-azure-cli"></a>Administrar servidores SQL Azure, las bases de datos y firewalls que usan Hola CLI de Azure

toocreate y administrar servidores SQL Azure, las bases de datos y los servidores de seguridad con hello [CLI de Azure](/cli/azure/overview), utilice Hola siguiente [base de datos de SQL Azure CLI](/cli/azure/sql/db) comandos. Hola de uso [Shell en la nube](/azure/cloud-shell/overview) toorun Hola CLI en el explorador, o [instalar](/cli/azure/install-azure-cli) en Windows, Linux o Mac OS. Para crear y administrar grupos elásticos de SQL, vea [Grupos elásticos](sql-database-elastic-pool.md).

| Cmdlet | Descripción |
| --- | --- |
|[az sql db create](/cli/azure/sql/db#create) |Crea una base de datos.|
|[az sql db list](/cli/azure/sql/db#list)|Enumera todas las bases de datos y almacenes de datos de un servidor, o todas las bases de datos de un grupo elástico.|
|[az sql db list-editions](/cli/azure/sql/db#list-editions)|Enumera los objetivos de servicio y los límites de almacenamiento disponibles.|
|[az sql db list-usages](/cli/azure/sql/db#list-usages)|Devuelve los usos de la base de datos.|
|[az sql db show](/cli/azure/sql/db#show)|Obtiene una base de datos o un almacenamiento de datos.|
|[az sql db update](/cli/azure/sql/db#update)|Actualiza una base de datos.|
|[az sql db delete](/cli/azure/sql/db#delete)|Quita una base de datos.|
|[az group create](/cli/azure/group#create)|Crea un grupo de recursos.|
|[az sql server create](/cli/azure/sql/server#create)|Crea un servidor.|
|[az sql server list](/cli/azure/sql/server#list)|Enumera los servidores.|
|[az sql server list-usages](/cli/azure/sql/server#list-usages)|Devuelve los usos del servidor.|
|[az sql server show](/cli/azure/sql/server#show)|Obtiene un servidor.|
|[az sql server update](/cli/azure/sql/server#update)|Actualiza un servidor.|
|[az sql server delete](/cli/azure/sql/server#delete)|Permite eliminar un servidor.|
|[az sql server firewall-rule create](/cli/azure/sql/server/firewall-rule#create)|Crea una regla de firewall del servidor.|
|[az sql server firewall-rule list](/cli/azure/sql/server/firewall-rule#list)|Enumera las reglas de firewall de hello en un servidor|
|[az sql server firewall-rule show](/cli/azure/sql/server/firewall-rule#show)|Muestra los detalles de Hola de una regla de firewall|
|[az sql server firewall-rule update](/cli/azure/sql/server/firewall-rule#update)|Actualiza una regla de firewall.|
|[az sql server firewall-rule delete](/cli/azure/sql/server/firewall-rule#delete)|Elimina una regla de firewall.|

> [!TIP]
> Para obtener un tutorial de inicio rápido de CLI de Azure, consulte [crear una base de datos de SQL Azure único con hello Azure CLI](sql-database-get-started-cli.md). Para los scripts de ejemplo de CLI de Azure, consulte [toocreate de CLI de usar una instancia única de SQL Azure la base de datos y configurar una regla de firewall](scripts/sql-database-create-and-configure-database-cli.md) y [toomonitor de CLI de uso y la escala una sola base de datos SQL](scripts/sql-database-monitor-and-scale-database-cli.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-transact-sql"></a>Administración de servidores, bases de datos y firewalls de Azure SQL con Transact-SQL

toocreate y administrar servidores de SQL Azure, las bases de datos y los servidores de seguridad con Transact-SQL, utilice Hola siga los comandos de T-SQL. Puede emitir estos comandos mediante el portal de Azure, Hola [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [código de Visual Studio](https://code.visualstudio.com/docs), o cualquier otro programa que se puede conectar el servidor de base de datos de SQL Azure tooan y pasar Transact-SQL comandos. Para administrar grupos elásticos de SQL, consulte [Grupos elásticos](sql-database-elastic-pool.md).

> [!IMPORTANT]
> No se puede crear ni eliminar un servidor mediante Transact-SQL.
>

| Comando | Descripción |
| --- | --- |
|[CREATE DATABASE (Azure SQL Database)](/sql/t-sql/statements/create-database-azure-sql-database)|Crear una base de datos. Debe ser toocreate de base de datos maestra toohello conectada una nueva base de datos.|
| [ALTER DATABASE (Base de datos SQL de Azure)](/sql/t-sql/statements/alter-database-azure-sql-database) |Modifica una base de datos SQL de Azure. |
|[ALTER DATABASE (Azure SQL Data Warehouse)](/sql/t-sql/statements/alter-database-azure-sql-data-warehouse)|Modifica una instancia de Azure SQL Data Warehouse.|
|[DROP DATABASE (Transact-SQL)](/sql/t-sql/statements/drop-database-transact-sql)|Permite eliminar una base de datos.|
|[sys.database_service_objectives (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Devuelve Hola edition (nivel de servicio), el objetivo de servicio (nivel de precios) y el nombre del grupo elástico, si existe, para una base de datos de SQL Azure o un almacén de datos de SQL Azure. Si una sesión en la base de datos maestra toohello en un servidor de base de datos de SQL Azure, devuelve información sobre todas las bases de datos. Para almacenamiento de datos de SQL Azure, debe ser toohello conectado la base de datos maestra.|
|[sys.dm_db_resource_stats (Azure SQL Database)](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database)| Devuelve el consumo de CPU, E/S y memoria para una base de datos de Azure SQL Database. Hay una fila para cada 15 segundos, incluso si no hay ninguna actividad en la base de datos de Hola.|
|[sys.resource_stats (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database)|Devuelve datos de almacenamiento y uso de CPU para una instancia de Azure SQL Database. datos de Hola se recopilan y se agregan en intervalos de cinco minutos.|
|[sys.database_connection_stats (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-connection-stats-azure-sql-database)|Contiene estadísticas de eventos de conectividad de base de datos de SQL Database, que proporcionan una visión general de los aciertos y errores de conexión a la base de datos. |
|[sys.event_log (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-event-log-azure-sql-database)|Devuelve las conexiones realizadas correctamente a la base de datos de Azure SQL Database, los errores de conexión y los interbloqueos. Puede usar este tootrack información o solucionar problemas de la actividad de base de datos con la base de datos SQL.|
|[sp_set_firewall_rule (Azure SQL Database)](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)|Crea o actualiza la configuración de firewall de nivel de servidor hello para el servidor de base de datos SQL. Este procedimiento almacenado solo está disponible en hello base de datos maestra toohello nivel de servidor inicio de sesión principal. Solo se puede crear una regla de firewall de nivel de servidor mediante Transact-SQL una vez creada la primera regla de firewall de nivel de servidor hello por un usuario con permisos de nivel de Azure|
|[sys.firewall_rules (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database)|Devuelve información sobre la configuración del firewall de nivel de servidor hello asociada con la base de datos de SQL de Microsoft Azure.|
|[sp_delete_firewall_rule (Azure SQL Database)](/sql/relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database)|Quita la configuración del firewall de nivel de servidor del servidor de SQL Database. Este procedimiento almacenado solo está disponible en hello base de datos maestra toohello nivel de servidor inicio de sesión principal.|
|[sp_set_database_firewall_rule (Azure SQL Database)](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)|Crea o actualiza las reglas de firewall de nivel de base de datos de Hola para su base de datos de SQL Azure o el almacenamiento de datos SQL. Las reglas de firewall de base de datos pueden configurarse para la base de datos maestra de Hola y de bases de datos de usuario de base de datos SQL. Las reglas de firewall de base de datos son útiles cuando se usan usuarios de base de datos independientes. |
|[sys.database_firewall_rules (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database)|Devuelve información acerca de la configuración de firewall de nivel de base de datos de hello asociado a la base de datos de SQL de Microsoft Azure. |
|[sp_delete_database_firewall_rule (Azure SQL Database)](/sql/relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database)|Quita las reglas de firewall de nivel de base de datos de la instancia de Azure SQL Database o SQL Data Warehouse. |


> [!TIP]
> Para el tutorial de inicio rápido con SQL Server Management Studio en Microsoft Windows, consulte [base de datos de SQL Azure: Use SQL Server Management Studio tooconnect y consultar datos](sql-database-connect-query-ssms.md). Para obtener un tutorial de inicio rápido con código de Visual Studio en Windows, Linux o macOS hello, consulte [base de datos de SQL Azure: usar Visual Studio Code tooconnect y consultar datos](sql-database-connect-query-vscode.md).

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-rest-api"></a>Administrar servidores SQL Azure, las bases de datos y firewalls con la API de REST de Hola

toocreate y administrar servidores de SQL Azure, las bases de datos y servidores de seguridad mediante API de REST de hello, consulte [API de REST de base de datos de SQL Azure](/rest/api/sql/).

## <a name="next-steps"></a>Pasos siguientes

- toolearn sobre la agrupación de bases de datos de uso de grupos elásticos de SQL, consulte [grupos elásticos](sql-database-elastic-pool.md).
- Para obtener información acerca de hello servicio de base de datos de SQL Azure, consulte [¿qué es la base de datos SQL?](sql-database-technical-overview.md).
- toolearn sobre cómo migrar un tooAzure de base de datos de SQL Server, vea [migrar la base de datos SQL tooAzure](sql-database-cloud-migrate.md).
- Para obtener información sobre las características admitidas, consulte el [artículo que trata sobre dicho tema](sql-database-features.md).
