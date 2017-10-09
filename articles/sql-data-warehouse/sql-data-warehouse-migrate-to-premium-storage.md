---
title: aaaMigrate toopremium almacenamiento del almacenamiento de los datos existentes de Azure | Documentos de Microsoft
description: "Instrucciones para migrar un almacenamiento de toopremium de almacén de datos existente"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a>Migrar el almacenamiento de toopremium de almacén de datos
Azure SQL Data Warehouse ha introducido recientemente [Premium Storage para poder predecir el rendimiento de manera más eficaz][premium storage for greater performance predictability]. Ahora pueden ser almacenamientos actualmente en almacenamiento estándar los datos existentes migran toopremium almacenamiento. Puede aprovechar las ventajas de la migración automática, o si prefiere toocontrol cuando toomigrate (que implican cierto tiempo de inactividad), puede hacer Hola migración usted mismo.

Si tiene más de un almacén de datos, usar hello [programación de la migración automática] [ automatic migration schedule] toodetermine cuando también se migrarán.

## <a name="determine-storage-type"></a>Determinación del tipo de almacenamiento
Si ha creado un almacén de datos antes de hello siguiendo las fechas, están usando actualmente almacenamiento estándar.

| **Región** | **Almacenamiento de datos creado antes de esta fecha** |
|:--- |:--- |
| Australia Oriental |Premium Storage no está disponible todavía |
| Este de China |1 de noviembre de 2016 |
| Norte de China |1 de noviembre de 2016 |
| Centro de Alemania |1 de noviembre de 2016 |
| Noreste de Alemania |1 de noviembre de 2016 |
| India occidental |Premium Storage no está disponible todavía |
| Oeste de Japón |Premium Storage no está disponible todavía |
| Centro-Norte de EE. UU |10 de noviembre de 2016 |

## <a name="automatic-migration-details"></a>Información de la migración automática
De forma predeterminada, se migrará la base de datos automáticamente entre 6:00 P.M. y las 6:00 A.M. en hora local de su región durante Hola [programación de la migración automática][automatic migration schedule]. Durante la migración de hello será inutilizable el almacenamiento de datos existente. migración de Hello tardará aproximadamente una hora por terabyte de almacenamiento de cada almacén de datos. No se le cobrará durante cualquier parte de la migración automática de Hola.

> [!NOTE]
> Una vez completada la migración de hello, será el almacenamiento de datos nuevo en línea y se puede usar.
>
>

Microsoft está llevando a cabo Hola después de la migración de hello toocomplete pasos (estos archivos no requieren ninguna intervención por parte del usuario). Para este ejemplo, imagine que su almacenamiento de datos del almacenamiento estándar actualmente se llama "MiAD".

1. Microsoft cambia el nombre "MyDW" demasiado "MyDW_DO_NOT_USE_ [Timestamp]".
2. Microsoft pausa "MiAD_DO_NOT_USE_[Marca de tiempo]". Durante este tiempo, se crea una copia de seguridad. Es posible que observe que se llevan a cabo varias tareas de pausa y reanudación si se producen problemas durante este proceso.
3. Microsoft crea un nuevo almacén de datos denominado "MyDW" en almacenamiento premium, desde la copia de seguridad de hello realizada en el paso 2. "MyDW" no aparecerá hasta que una vez completada la restauración de Hola.
4. Una vez completada la restauración de hello, "MyDW" devuelve toohello unidades del almacenamiento de datos mismo y estado (en pausa o activa) que se encontraba antes de la migración de Hola.
5. Una vez completada la migración de hello, Microsoft elimina "MyDW_DO_NOT_USE_ [Timestamp]".

> [!NOTE]
> Hello valores siguientes no se mantienen como parte de la migración de hello:
>
> * Auditoría de nivel de base de datos de hello debe toobe vuelve a habilitar.
> * Las reglas de Firewall en el nivel de base de datos de hello necesitan toobe agregarse de nuevo. Las reglas de Firewall en el nivel de servidor hello no se ven afectadas.
>
>

### <a name="automatic-migration-schedule"></a>programa de migración automática
Migraciones automáticas se producen entre las 6:00 P.M. y las 6:00 A.M. (hora local por región) durante Hola siguiendo la programación de interrupción.

| **Región** | **Fecha de inicio estimada** | **Fecha de finalización estimada** |
|:--- |:--- |:--- |
| Australia Oriental |Sin determinar |Sin determinar |
| Este de China |9 de enero de 2017 |13 de enero de 2017 |
| Norte de China |9 de enero de 2017 |13 de enero de 2017 |
| Centro de Alemania |9 de enero de 2017 |13 de enero de 2017 |
| Noreste de Alemania |9 de enero de 2017 |13 de enero de 2017 |
| India occidental |Sin determinar |Sin determinar |
| Oeste de Japón |Sin determinar |Sin determinar |
| Centro-Norte de EE. UU |9 de enero de 2017 |13 de enero de 2017 |

## <a name="self-migration-toopremium-storage"></a>Almacenamiento de migración automática toopremium
Si desea toocontrol cuando se producirá el tiempo de inactividad, puede usar Hola siguiendo los pasos toomigrate un almacén de datos existente en el almacenamiento de toopremium de almacenamiento estándar. Si elige esta opción, debe completar la migración automática de Hola de antes de que comience la migración automática de hello en dicha región. Esto garantiza que evitar los riesgos de la migración automática de hello causando un conflicto (consulte toohello [programación de la migración automática][automatic migration schedule]).

### <a name="self-migration-instructions"></a>Instrucciones de migración manual
toomigrate los datos del almacenamiento de usted mismo, usar copia de seguridad de Hola y restauración características. parte de restauración de Hola de migración de hello es tootake esperado alrededor de una hora por terabyte de almacenamiento al almacenamiento de datos. Si desea que hello tookeep mismo nombre una vez completada la migración, siga hello [toorename pasos durante la migración][steps toorename during migration].

1. [Detenga][Pause] el almacenamiento de datos. Esto realiza una copia de seguridad automática.
2. Lleve a cabo la [restauración][Restore] a partir de la instantánea más reciente.
3. Elimine el almacenamiento de datos existente del almacenamiento estándar. **Si se produce un error toodo este paso, se le cobrará por ambos almacenes de datos.**

> [!NOTE]
> Hello valores siguientes no se mantienen como parte de la migración de hello:
>
> * Auditoría de nivel de base de datos de hello debe toobe vuelve a habilitar.
> * Las reglas de Firewall en el nivel de base de datos de hello necesitan toobe agregarse de nuevo. Las reglas de Firewall en el nivel de servidor hello no se ven afectadas.
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a>Cambio del nombre del almacenamiento de datos durante la migración (opcional)
Dos bases de datos no puede tener el mismo servidor lógico de Hola Hola el mismo nombre. Almacenamiento de datos SQL admite ahora Hola capacidad toorename un almacenamiento de datos.

Para este ejemplo, imagine que su almacenamiento de datos del almacenamiento estándar actualmente se llama "MiAD".

1. Cambiar el nombre "MyDW" mediante Hola siguiente comando ALTER DATABASE. (En este ejemplo, se podrá cambiarlo "MyDW_BeforeMigration.")  Este comando detiene todas las transacciones existentes y debe realizarse en hello toosucceed de base de datos maestra.
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. [Detenga][Pause] "MyDW_BeforeMigration". Esto realiza una copia de seguridad automática.
3. [Restaurar] [ Restore] desde la instantánea más reciente de una base de datos con nombre de Hola usa toobe (por ejemplo, "MyDW").
4. Elimine "MyDW_BeforeMigration". **Si se produce un error toodo este paso, se le cobrará por ambos almacenes de datos.**


## <a name="next-steps"></a>Pasos siguientes
Almacenamiento toopremium los cambios de hello, también tendrá un mayor número de archivos de blob de base de datos en la arquitectura subyacente de Hola de su almacén de datos. ventajas de rendimiento de hello toomaximize de este cambio, vuelva a generar los índices de almacén de columnas agrupado mediante el uso de hello siguiente secuencia de comandos. script de Hola funciona forzar el uso de algunos de los blobs adicionales de toohello de datos existente. Si no realiza ninguna acción, volverá a datos Hola naturalmente distribuir con el tiempo como cargar más datos en las tablas.

**Requisitos previos:**

- Hello almacenamiento de datos debe ejecutarse con unidades de almacenamiento de datos de 1000 o superior (vea [capacidad de cálculo de escala][scale compute power]).
- usuario que ejecuta el script de Hola Hola debe ser una en hello [mediumrc rol] [ mediumrc role] o superior. tooadd un rol de usuario toothis, ejecute el siguiente hello:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

Si tiene algún problema con el almacenamiento de datos, [crear una incidencia de soporte técnico] [ create a support ticket] y hacer referencia a "almacenamiento de migración toopremium" como posible causa de Hola.

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
