---
title: Niveles de servicio y rendimiento de Azure SQL Database | Microsoft Docs
description: "Comparación de los niveles de servicio y rendimiento de SQL Database en bases de datos únicas e introducción a los grupos elásticos de SQL"
keywords: opciones de base de datos, rendimiento de la base de datos
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: f5c5c596-cd1e-451f-92a7-b70d4916e974
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/30/2017
ms.author: carlrab
ms.openlocfilehash: b27b78788614d32e6c0c4267fe0ce504ebd2f444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-performance-options-are-available-for-an-azure-sql-database"></a>¿Qué opciones de rendimiento están disponibles para una instancia de Azure SQL Database?

[Azure SQL Database](sql-database-technical-overview.md) ofrece cuatro niveles de servicio para bases de datos únicas y [agrupadas](sql-database-elastic-pool.md). Y son: **Básico**, **Estándar**, **Premium** y **Premium RS**. Dentro de cada nivel de servicio, hay varios niveles de rendimiento ([Dtu](sql-database-what-is-a-dtu.md)) y opciones de almacenamiento toohandle diferentes tamaños de las cargas de trabajo y los datos. Niveles más altos de rendimiento proporcionan proceso adicional y recursos de almacenamiento diseñada capacidad y rendimiento de cada vez mayor de toodeliver. Puede cambiar los niveles de servicio, los niveles de rendimiento y el almacenamiento de manera dinámica sin tiempo de inactividad. 
- Los niveles de servicio **Básico**, **Estándar** y **Premium** tienen todos ellos un Acuerdo de Nivel de Servicio de tiempo de actividad del 99,99 %, opciones de continuidad empresarial flexibles, características de seguridad y facturación por hora. 
- Hola **Premium RS** capa proporciona Hola mismos niveles de rendimiento como hello nivel Premium con un SLA reducido porque se ejecuta con un número menor de copias redundantes de una base de datos en Hola otros niveles de servicio. Por lo tanto, en caso de hello de un error del servicio, deberá toorecover la base de datos desde una copia de seguridad con una tooa intervalo de 5 minutos.

> [!IMPORTANT]
> Hola espera características de rendimiento de la base de datos no se ven afectadas por cualquier otra base de datos dentro de Azure y una base de datos de SQL Azure Obtiene un conjunto garantizado de recursos. 

## <a name="choosing-a-service-tier"></a>Selección de un nivel de servicio
Hello tabla siguiente proporciona ejemplos de niveles de hello mejor adecuados para las cargas de trabajo de aplicación diferente.

| Nivel de servicio | Carga de trabajo objetivo |
| :--- | --- |
| **Básico** | Ideal para bases de datos pequeñas, que suelen admitir una sola operación activa en un momento dado. Algunos ejemplos son las bases de datos utilizadas para desarrollo o prueba, o las aplicaciones a pequeña escala que se emplean con poca frecuencia. |
| **Standard** |Hola go toooption para las aplicaciones de nube con requisitos de rendimiento de E/S de bajo toomedium, admite varias consultas simultáneas. Algunos ejemplos son las aplicaciones web o los grupos de trabajo. |
| **Premium** | Diseñado para un alto volumen transaccional con altos requisitos de rendimiento de E/S; admite muchos usuarios simultáneos. Algunos ejemplos son las bases de datos que admiten aplicaciones críticas. |
| **Premium RS** | Diseñado para cargas de trabajo intensivo que no necesitan garantías de hello más altas disponibilidad. Los ejemplos incluyen las pruebas en cargas de trabajo de alto rendimiento, o una carga de trabajo analítico donde la base de datos de hello no es sistema Hola de registro. |
|||

Puede crear bases de datos únicas con recursos dedicados dentro de un nivel de servicio con un [nivel de rendimiento](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) específico o también puede crear bases de datos dentro de un [grupo elástico de SQL](sql-database-service-tiers.md#elastic-pool-service-tiers-and-performance-in-edtus). En un grupo elástico de SQL, los recursos de proceso y almacenamiento de Hola se comparten entre varias bases de datos dentro de un único servidor lógico. 

Los recursos disponibles para las bases de datos únicas se expresan como unidades de transacción de base de datos (DTU) y, para los grupos elásticos de SQL, como unidades de transacción de bases de datos elásticas (eDTU). Para más información sobre las DTU y las eDTU, consulte [¿Qué son las DTU y las eDTU?](sql-database-what-is-a-dtu.md)

toodecide en un nivel de servicio, iniciar mediante la determinación de características de base de datos mínima Hola que necesita:

| **Características del nivel de servicio** | **Básico** | **Standard** | **Premium** | **Premium RS**|
| :-- | --: | --: | --: | --: |
| Tamaño máximo de la base de datos única | 2 GB | 250 GB | 4 TB*  | 500 GB  |
| Tamaño máximo del grupo elástico | 156 GB | 2,9 TB | 4 TB* | 750 GB |
| Tamaño máximo de la base de datos de un grupo elástico | 2 GB | 250 GB | 500 GB | 500 GB |
| Cantidad máxima de bases de datos por grupo | 500  | 500 | 100 | 100 |
| DTU máximas de la base de datos única | 5 | 100 | 4000 | 1000 |
| DTU máximas por base de datos de un grupo elástico | 5 | 3000 | 4000 | 1000 |
| Período de retención de copias de seguridad de base de datos | 7 días | 35 días | 35 días | 35 días |
||||||

> [!IMPORTANT]
> Almacenamiento de información hasta too4 TB está disponible actualmente en hello siguientes regiones: nos East2, oeste de Estados Unidos, nos Gov Virginia, Europa occidental, Alemania Central, sur Asia oriental, este de Japón, Australia Oriental, Canadá Central y este de Canadá. Consulte las [limitaciones actuales de 4 TB](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize)
>

Una vez que haya determinado nivel de servicio adecuado de hello, es nivel de rendimiento de hello toodetermine listo (número de Hola de Dtu) y la cantidad de almacenamiento de Hola para base de datos de Hola. 

- Hola S2 y S3 niveles de rendimiento en hello **estándar** nivel suelen ser un buen punto de partida. 
- Para las bases de datos con los requisitos de CPU o E/S altos, Hola niveles de rendimiento en hello **Premium** capa son el punto de partida adecuado de Hola. 
- Hola **Premium** nivel ofrece más CPU y comienza a las 10 veces más E/S en comparación con mayor nivel de rendimiento toohello en hello **estándar** capa.
- Hola **PremiumRS** nivel ofrece un rendimiento Hola de hello **Premium** capa con un costo menor, pero con un SLA reducido.

> [!IMPORTANT]
> Hola de revisión [grupos elásticos SQL](sql-database-elastic-pool.md) tooshare recursos de proceso y almacenamiento de grupos de tema para obtener detalles de hello sobre las bases de datos están agrupados en elástico SQL. resto de Hola de este tema se centra en los niveles de servicio y niveles de rendimiento para las bases de datos únicos.
>

## <a name="single-database-service-tiers-and-performance-levels"></a>Niveles de servicio de la Base de datos única y niveles de rendimiento
Para las bases de datos únicas, existen varios niveles de rendimiento y cantidades de almacenamiento dentro de cada nivel de servicio. 

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

## <a name="scaling-up-or-scaling-down-a-single-database"></a>Escalado y reducción vertical de una base de datos única

Después de elegir inicialmente un nivel de rendimiento, puede escalar o reducir verticalmente una base de datos única de forma dinámica, en función de la experiencia real.  

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-dynamically-scale-up-or-scale-down/player]
>

Cambiar el nivel de rendimiento o de nivel de servicio de Hola de una base de datos crea una réplica de base de datos original de hello en el nuevo nivel de rendimiento de hello y, a continuación, cambia las conexiones toohello réplica. No se pierdan datos durante este proceso, pero durante Hola breve momento cuando se cambie a través de la réplica de toohello, base de datos de las conexiones toohello están deshabilitados, por lo que se pueden revertir algunas transacciones en tránsito. Hola período de tiempo para cambiar Hola varía, pero suele ser menos de 4 segundos es inferior a 30 segundos 99% de tiempo de presentación. Si hay un gran número de transacciones en tránsito en conexiones de momento Hola están deshabilitadas, hello período de tiempo para cambiar Hola puede ser superior.  

duración de Hola de todo el proceso de escalado vertical depende de ambos tamaño hello y base de datos de nivel de servicio de hello antes y después de cambiar de Hola Hola. Por ejemplo, el cambio de una base de datos de 250 GB dentro de un nivel de servicio Estándar, o bien desde o hacia este, se completará en 6 horas. Para una base de datos de hello mismo tamaño que es cambiar los niveles de rendimiento dentro del nivel de servicio Premium de hello, debe completar dentro de 3 horas.

> [!TIP]
> toocheck en estado de Hola de una base de datos SQL en curso la operación de escalado, puede usar Hola después de consulta: ```select * from sys.dm_operation_status```.
>

* Si va a actualizar el nivel de servicio mayor rendimiento o de tooa, tamaño de base de datos máximo de hello no aumenta a menos que especifique explícitamente un tamaño máximo mayor.
* toodowngrade una base de datos, base de datos de hello debe ser menor que Hola tamaño máximo permitido de nivel de servicio de destino de Hola. 
* Al actualizar una base de datos con [georreplicación](sql-database-geo-replication-portal.md) habilitado, actualizar su nivel de rendimiento deseado de toohello de bases de datos secundarias antes de actualizar la base de datos principal de hello (instrucciones generales). Al actualizar tooa diferentes base de datos secundaria de edición actualizar Hola primero es necesario. 
* Al degradar una base de datos con [georreplicación](sql-database-geo-replication-portal.md) habilitado, cambiar su nivel de rendimiento deseado de bases de datos principales toohello antes de degradar la base de datos secundaria del hello (instrucciones generales). Al degradar tooa diferentes edición instalar versiones anteriores Hola base de datos principal primero es necesario. 

* Hello ofertas de servicio de restauración son diferentes para Hola distintos niveles de servicio. Si cambia toohello **básica** nivel, tendrá un período de retención de copia de seguridad inferior - vea [copias de seguridad de base de datos de SQL de Azure](sql-database-automated-backups.md).
* Hola nuevas propiedades de base de datos de hello no se aplican hasta que se completen los cambios de Hola.


## <a name="current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize"></a>Limitaciones actuales de las bases de datos P11 y P15 con un tamaño máximo de 4 TB

Como se ha indicado anteriormente, se admite un tamaño máximo de 4 TB para bases de datos P11 y P15 en algunas regiones. Hello consideraciones y limitaciones siguientes se aplican tooP11 y bases de datos de P15 con valor maxsize de 4 TB:

- Si elige la opción maxsize de 4 TB de hello al crear una base de datos (con un valor de 4 TB ó 4096 GB), Hola crear comando produce un error con un error si la base de datos de Hola se aprovisiona en una región no compatible.
- Existente P11 y P15 bases de datos ubicados en una de las regiones de hello admitida, puede aumentar Hola maxsize almacenamiento too4 TB. Esto se puede comprobar mediante hello [seleccione DATABASEPROPERTYEX](https://msdn.microsoft.com/library/ms186823.aspx) o mediante la inspección del tamaño de la base de datos de Hola Hola portal de Azure. Actualizar una existente P11 o P15 base de datos solo puede realizarse mediante un inicio de sesión de entidad de seguridad de nivel de servidor o los miembros del rol de base de datos de hello dbmanager. 
- Si una operación de actualización se ejecuta en una configuración de región admitida Hola se actualiza inmediatamente. base de datos de Hello permanece en línea durante el proceso de actualización de Hola. Sin embargo, no puede utilizar Hola completa 4 TB de almacenamiento hasta que se eliminen los archivos de base de datos real de hello actualizado toohello nueva maxsize. Hola período de tiempo necesario depende en tamaño Hola de base de datos de Hola que se está actualizando.  
- Al crear o actualizar una base de datos P11 o P15, solo puede optar entre un tamaño máximo de 1 TB y 4 TB. Actualmente no se admiten tamaños de almacenamiento intermedios. Al crear un P11/P15, opción de almacenamiento predeterminada de Hola de 1 TB está preseleccionada. Para bases de datos ubicadas en una de las regiones de hello admitida, puede aumentar Hola almacenamiento máximo too4TB para una base de datos único nuevo o existente. Para todas las demás regiones, el tamaño máximo no se puede aumentar por encima de 1 TB. precio de Hello no cambia cuando se selecciona 4 TB de almacenamiento incluye.
- Hello maxsize de la base de datos de 4 TB no puede ser modificada too1 TB aunque almacenamiento real Hola utilizado está por debajo de 1 TB. Por lo tanto, no se puede cambiar un tooa P11 - 4 TB/P15 - 4 TB P11 y 1 TB/P15 - 1 TB o un nivel de rendimiento inferior, por ejemplo, tooP1-P6) hasta que proporcionamos opciones de almacenamiento adicional para el resto de Hola de hello niveles de rendimiento. Esta restricción también aplica toohello restauración y copiar escenarios incluidos en el momento, la restauración geográfica, largo-plazo-copia de seguridad y retención y copia de la base de datos. Una vez que una base de datos está configurado con la opción de 4 TB de hello, todas las operaciones de restauración de esta base de datos deben ejecutarse en un P11/P15 con maxsize de 4 TB.
- Al crear o actualizar una base de datos P11/P15 en una región no admitida, hello crear o se produce un error en la operación de actualización con el siguiente mensaje de error de hello: **P11 P15 base de datos y con seguridad too4TB de almacenamiento están disponibles en East2 nosotros, oeste de Estados Unidos, nos Gov Virginia, Europa occidental, centro de Alemania, sudeste de Asia, este de Japón, Australia Oriental, centro de Canadá y este de Canadá.**
- En escenarios de replicación geográfica activa:
   - Configurar una relación de replicación geográfica: si la base de datos principal de hello es P11 o P15, también debe ser hello secondary(ies) P11 o P15; niveles de rendimiento inferior se rechazan como elementos secundarios, puesto que no son capaces de admitir 4 TB.
   - Actualizar base de datos principal hello en una relación de replicación geográfica: cambiar Hola maxsize too4 TB en una base de datos principal desencadena Hola mismo cambia en la base de datos secundaria de Hola. Ambas actualizaciones deben ser correctas para cambio de hello en efecto de hello tootake principal. Región para la opción de 4TB de hello limitaciones (vea más arriba). Si Hola secundaria está en una región que no es compatible con 4 TB, Hola principal no se actualiza.
- No se admite el uso de servicio de importación y exportación de Hola para cargar bases de datos de P11 - 4TB/P15 - 4TB. Usar demasiado SqlPackage.exe[importar](sql-database-import.md) y [exportar](sql-database-export.md) datos.

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-portal"></a>Administrar niveles de servicio de base de datos y los niveles de rendimiento con hello portal de Azure

Hola a tooset o cambio de nivel de servicio, el nivel de rendimiento o la cantidad de almacenamiento de una base de SQL Azure nueva o existente mediante Hola portal de Azure, abra Hola **configurar rendimiento** ventana de la base de datos haciendo clic en  **Nivel de precios (escala Dtu)** : como se muestra en la siguiente captura de pantalla de Hola. 

- Establecer o cambiar el nivel de servicio de hello seleccionando el nivel de servicio de hello para la carga de trabajo. 
- Establecer o cambiar el nivel de rendimiento de hello (**Dtu**) dentro de un nivel de servicio con hello **DTU** control deslizante.
- Establecer o cambiar la cantidad de almacenamiento de hello para el nivel de rendimiento de hello con hello **almacenamiento** control deslizante. 

  ![Configuración del nivel de servicio y rendimiento](./media/sql-database-service-tiers/service-tier-performance-level.png)

> [!IMPORTANT]
> Al seleccionar un nivel de servicio P11 o P15, revise las [limitaciones actuales de las bases de datos P11 y P15 con un tamaño máximo de 4 TB](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize).
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-powershell"></a>Administración de los niveles de servicio y rendimiento de bases de datos únicas mediante PowerShell

tooset o cambiar niveles de servicio de las bases de datos de SQL Azure, los niveles de rendimiento y cantidad de almacenamiento con PowerShell, usan Hola siguientes cmdlets de PowerShell. Si necesita tooinstall o actualice PowerShell, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps). 

| Cmdlet | Descripción |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Crea una base de datos. |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Obtiene una o más bases de datos.|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Establece las propiedades de una base de datos, o mueve una base de datos existente en un grupo elástico.|


> [!TIP]
> Para una secuencia de comandos de ejemplo de PowerShell que supervisa las métricas de rendimiento de Hola de una base de datos, escala tooa mayor nivel de rendimiento y crea una regla de alerta en una de las métricas de rendimiento de hello, vea [Monitor y escala una instancia única de SQL de base de datos usando PowerShell](scripts/sql-database-monitor-and-scale-database-powershell.md).

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-cli"></a>Administrar niveles de servicio de base de datos y los niveles de rendimiento con hello CLI de Azure

tooset o cambiar niveles de servicio de las bases de datos de SQL Azure, los niveles de rendimiento y cantidad de almacenamiento mediante Hola CLI de Azure, use siguiente de hello [base de datos de SQL Azure CLI](/cli/azure/sql/db) comandos. Hola de uso [Shell en la nube](/azure/cloud-shell/overview) toorun Hola CLI en el explorador, o [instalar](/cli/azure/install-azure-cli) en Windows, Linux o Mac OS. Para crear y administrar grupos elásticos de SQL, vea [Grupos elásticos](sql-database-elastic-pool.md).

| Cmdlet | Descripción |
| --- | --- |
|[az sql db create](/cli/azure/sql/db#create) |Crea una base de datos.|
|[az sql db list](/cli/azure/sql/db#list)|Enumera todas las bases de datos y almacenes de datos de un servidor, o todas las bases de datos de un grupo elástico.|
|[az sql db list-editions](/cli/azure/sql/db#list-editions)|Enumera los objetivos de servicio y los límites de almacenamiento disponibles.|
|[az sql db list-usages](/cli/azure/sql/db#list-usages)|Devuelve los usos de la base de datos.|
|[az sql db show](/cli/azure/sql/db#show)|Obtiene una base de datos o un almacenamiento de datos.|
|[az sql db update](/cli/azure/sql/db#update)|Actualiza una base de datos.|

> [!TIP]
> Para una secuencia de comandos de ejemplo de CLI de Azure que escala de un solo nivel de rendimiento de tooa de base de datos SQL de Azure después de consultar información sobre el tamaño de base de datos de Hola Hola, consulte [toomonitor de CLI de uso y la escala una sola base de datos SQL](scripts/sql-database-monitor-and-scale-database-cli.md).
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-transact-sql"></a>Administración de los niveles de servicio y rendimiento de bases de datos únicas mediante Transact-SQL

tooset o cambiar niveles de servicio de las bases de datos de SQL Azure, los niveles de rendimiento y la cantidad de almacenamiento con Transact-SQL, utilizan Hola siga los comandos de T-SQL. Puede emitir estos comandos mediante el portal de Azure, Hola [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [código de Visual Studio](https://code.visualstudio.com/docs), o cualquier otro programa que se puede conectar el servidor de base de datos de SQL Azure tooan y pasar Transact-SQL comandos. 

| Comando | Descripción |
| --- | --- |
|[CREATE DATABASE (Azure SQL Database)](/sql/t-sql/statements/create-database-azure-sql-database)|Crear una base de datos. Debe ser toocreate de base de datos maestra toohello conectada una nueva base de datos.|
| [ALTER DATABASE (Base de datos SQL de Azure)](/sql/t-sql/statements/alter-database-azure-sql-database) |Modifica una base de datos SQL de Azure. |
|[sys.database_service_objectives (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Devuelve Hola edition (nivel de servicio), el objetivo de servicio (nivel de precios) y el nombre del grupo elástico, si existe, para una base de datos de SQL Azure o un almacén de datos de SQL Azure. Si una sesión en la base de datos maestra toohello en un servidor de base de datos de SQL Azure, devuelve información sobre todas las bases de datos. Para almacenamiento de datos de SQL Azure, debe ser toohello conectado la base de datos maestra.|
|[sys.database_usage (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-usage-azure-sql-database)|Muestra el número de hello, el tipo y la duración de bases de datos en un servidor de base de datos de SQL Azure.|

Hello en el ejemplo siguiente se muestra hello maxsize está cambiando mediante el comando ALTER DATABASE de hello:

 ```sql
ALTER DATABASE <myDatabaseName> 
   MODIFY (MAXSIZE = 4096 GB);
```

## <a name="manage-single-databases-using-hello-rest-api"></a>Administrar bases de datos únicos mediante Hola API de REST

tooset o cambiar niveles de servicio de las bases de datos de SQL Azure, los niveles de rendimiento y la cantidad de almacenamiento mediante Hola API de REST, vea [API de REST de base de datos de SQL Azure](/rest/api/sql/).

## <a name="next-steps"></a>Pasos siguientes

* Más información acerca de las [DTU](sql-database-what-is-a-dtu.md).
* toolearn acerca de cómo supervisar el uso DTU, consulte [supervisión y ajuste del rendimiento](sql-database-troubleshoot-performance.md).

