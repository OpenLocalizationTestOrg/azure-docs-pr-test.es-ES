---
title: aaaUsing particiones de Recovery Manager toofix asignar problemas | Documentos de Microsoft
description: Utilice los problemas de hello RecoveryManager clase toosolve con mapas de particiones
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 45520ca3-6903-4b39-88ba-1d41b22da9fe
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: ddove
ms.openlocfilehash: 2218fb15122f1df466e65483480461e366317f2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-recoverymanager-class-toofix-shard-map-problems"></a>Uso de los problemas de asignación de particiones de la clase toofix de hello RecoveryManager
Hola [RecoveryManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.aspx) clase proporciona a las aplicaciones de ADO.Net Hola capacidad tooeasily detectar y corregir las incoherencias entre el mapa de particiones global de hello (GSM) y el mapa de particiones locales de hello (LSM) en un entorno de base de datos particionada. 

Hola GSM y LSM pista Hola asignación de cada base de datos en un entorno particionado. En ocasiones, se produce una interrupción entre Hola GSM y Hola LSM. En ese caso, utilice hello RecoveryManager clase toodetect y reparar salto Hola.

Hola RecoveryManager clase forma parte del programa Hola a [biblioteca de cliente de base de datos elástica](sql-database-elastic-database-client-library.md). 

![Mapa de particiones][1]

Para definiciones de términos, consulte el [Glosario de herramientas de base de datos elástica](sql-database-elastic-scale-glossary.md). Cómo Hola toounderstand **ShardMapManager** toomanage usa datos en una solución particionada, consulte [administración de mapa de particiones](sql-database-elastic-scale-shard-map-management.md).

## <a name="why-use-hello-recovery-manager"></a>¿Por qué usar el Administrador de recuperación Hola?
En un entorno de base de datos particionada, hay un inquilino por base de datos y muchas bases de datos por servidor. También puede haber muchos servidores en el entorno de Hola. Cada base de datos está asignada en el mapa de particiones de hello, por lo que pueden ser llamadas de base de datos y servidor correctos toohello enrutado. Se realiza el seguimiento de las bases de datos según tooa **clave de particionamiento**, y se asigna cada partición un **intervalo de valores de clave**. Por ejemplo, una clave de particionamiento puede representar los nombres de cliente hello de "D" demasiado "f" Hola la asignación de todas las particiones (también conocido como bases de datos) y sus rangos de asignación están incluidos en hello **mapa de particiones global (GSM)**. Cada base de datos también contiene una asignación de intervalos de hello contenidos en la partición de Hola que se conoce como hello **mapa de particiones locales (LSM)**. Cuando una aplicación se conecta tooa particiones, asignación de Hola se almacena en caché con la aplicación hello para la recuperación rápida. Hola LSM es toovalidate usado en caché datos. 

Hello GSM y LSM pueden no estar sincronizados para hello siguientes motivos:

1. eliminación de Hola de una partición cuyo intervalo se considera toono más estar en uso o cambiar el nombre de una partición. La eliminación de una partición da como resultado una **asignación de particiones huérfana**. De igual forma, una base de datos cuyo nombre cambió puede provocar una asignación de particiones huérfanas. Según el propósito de Hola de cambio de hello, particiones de hello quizás necesite toobe quitado o ubicación de la partición de hello necesita toobe actualizado. toorecover una base de datos eliminada, consulte [restaurar una base de datos eliminada](sql-database-recovery-using-backups.md).
2. Se produce un evento de conmutación por error geográfica. toocontinue, uno debe actualizar el nombre del servidor de Hola y nombre de base de datos de administrador de mapa de particiones en la aplicación hello y, a continuación, detalles de la asignación de particiones de actualización Hola para todas las particiones en un mapa de particiones. Si se produce una conmutación geográfica, dicha lógica de recuperación debería automatizarse dentro de flujo de trabajo de conmutación por error de Hola. La automatización de las acciones de recuperación permite una capacidad de administración sin contacto para bases de datos habilitadas geográficamente y evita acciones humanas manuales. toolearn sobre toorecover opciones una base de datos si se produce una interrupción del centro de datos, vea [continuidad del negocio](sql-database-business-continuity.md) y [recuperación ante desastres](sql-database-disaster-recovery.md).
3. Una partición o hello ShardMapManager base de datos es tooan restaurada anteriores un momento dado. toolearn sobre el punto de recuperación a un momento mediante copias de seguridad, consulte [recuperación mediante copias de seguridad](sql-database-recovery-using-backups.md).

Para obtener más información sobre herramientas de base de datos de elástico de base de datos de SQL de Azure, la replicación geográfica y restauración, vea Hola siguiente: 

* [Información general: continuidad del negocio en la nube y recuperación ante desastres con la Base de datos SQL](sql-database-business-continuity.md) 
* [Introducción a las herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md)  
* [Administración de ShardMap](sql-database-elastic-scale-shard-map-management.md)

## <a name="retrieving-recoverymanager-from-a-shardmapmanager"></a>Recuperación de RecoveryManager desde un ShardMapManager
Hola primer paso es una instancia de RecoveryManager toocreate. Hola [GetRecoveryManager método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getrecoverymanager.aspx) devuelve Hola recovery manager para hello actual [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) instancia. tooaddress se asignan las incoherencias de particiones de hello, primero debe recuperar hello RecoveryManager para el mapa de particiones determinado de Hola. 

   ```
    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString,  
             ShardMapManagerLoadPolicy.Lazy);
             RecoveryManager rm = smm.GetRecoveryManager(); 
   ```

En este ejemplo, se inicializa hello RecoveryManager de hello ShardMapManager. Hola ShardMapManager que contiene un ShardMap también ya está inicializado. 

Puesto que este código de aplicación manipula propia asignación de particiones hello, Hola credenciales que se usan en el método de fábrica de hello (Hola anterior ejemplo, smmConnectionString) debe ser las credenciales que tienen permisos de lectura y escritura en base de datos de hello GSM al que hace referencia Hola cadena de conexión. Estas credenciales son suelen ser diferentes de las conexiones de tooopen de credenciales que se usan para el enrutamiento dependiente de los datos. Para obtener más información, consulte [con credenciales de cliente de base de datos elástica hello](sql-database-elastic-scale-manage-credentials.md).

## <a name="removing-a-shard-from-hello-shardmap-after-a-shard-is-deleted"></a>Quitar una partición de hello ShardMap después de elimina una partición
Hola [DetachShard método](https://msdn.microsoft.com/library/azure/dn842083.aspx) desasocia hello tiene particiones de mapa de particiones de Hola y elimina las asignaciones asociadas a la partición de Hola.  

* parámetro de ubicación de Hello es la ubicación de particiones de hello, específicamente el nombre del servidor y el nombre de base de datos de partición Hola va a separar. 
* parámetro de Hello shardMapName es el nombre de mapa de particiones de Hola. Esto solo es necesario cuando se administran varias asignaciones de particiones por hello mismo administrador de mapa de particiones. Opcional. 


> [!IMPORTANT]
> Use esta técnica solo si está seguro de que el rango de hello para la asignación de hello actualizado está vacío. métodos de Hello anteriores no comprobar los datos para que se va a mover el intervalo de hello, por lo que es mejor tooinclude comprueba en el código.
>

Este ejemplo quita particiones de mapa de particiones de Hola. 

   ```
   rm.DetachShard(s.Location, customerMap);
   ``` 

mapa de particiones de Hello refleja la ubicación de particiones de Hola Hola GSM antes de la eliminación de Hola de particiones de Hola. Porque se eliminó la partición de hello, se supone esto fue intencionado, y el intervalo de claves de particionamiento de hello ya no está en uso. De lo contrario, puede ejecutar la restauración a un momento dado. partición de hello toorecover de un momento anterior. (En ese caso, revise Hola siguiendo las incoherencias de sección toodetect particiones). toorecover, consulte [punto de recuperación a un momento](sql-database-recovery-using-backups.md).

Ya que se supone la eliminación de la base de datos de hello era intencionada, hello acción de limpieza administrativas final es particiones de toodelete Hola entrada toohello en el Administrador de mapa de particiones de Hola. Esto evita que la aplicación hello de escriban sin querer intervalo tooa de información que no se esperaba.

## <a name="toodetect-mapping-differences"></a>diferencias de asignación de toodetect
Hola [DetectMappingDifferences método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.detectmappingdifferences.aspx) selecciona y devuelve uno de los mapas de particiones de hello (ya sea locales o globales) como origen de Hola de verdad y reconcilia los asignaciones en ambas asignaciones de particiones (GSM y LSM).

   ```
   rm.DetectMappingDifferences(location, shardMapName);
   ```

* Hola *ubicación* especifica el nombre del servidor de Hola y el nombre de la base de datos. 
* Hola *shardMapName* parámetro es el nombre de asignación de particiones de Hola. Esto solo es necesario si se administran varias asignaciones de particiones por hello mismo administrador de mapa de particiones. Opcional. 

## <a name="tooresolve-mapping-differences"></a>diferencias de asignación de tooresolve
Hola [ResolveMappingDifferences método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.resolvemappingdifferences.aspx) selecciona uno de los mapas de particiones de hello (ya sea locales o globales) como origen de Hola de verdad y reconcilia los asignaciones en ambas asignaciones de particiones (GSM y LSM).

   ```
   ResolveMappingDifferences (RecoveryToken, MappingDifferenceResolution.KeepShardMapping);
   ```

* Hola *RecoveryToken* parámetro enumera las diferencias de hello en asignaciones de hello entre hello LSM para particiones específicas de Hola y Hola GSM. 
* Hola [MappingDifferenceResolution enumeración](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.mappingdifferenceresolution.aspx) es método de hello tooindicate usado para resolver la diferencia de hello entre las asignaciones de particiones de Hola. 
* **MappingDifferenceResolution.KeepShardMapping** se recomienda que cuando Hola LSM contiene asignación precisa de hello y, por tanto, debe usarse la asignación de hello en particiones de Hola. Esto suele ser el caso de hello si se produce una conmutación por error: partición de hello ahora reside en un servidor nuevo. Puesto que la partición de hello en primer lugar debe quitarse de hello GSM (mediante el método de hello RecoveryManager.DetachShard), una asignación ya no existe en hello GSM. Por lo tanto, Hola LSM debe ser usado toore-establecer asignación de particiones de Hola.

## <a name="attach-a-shard-toohello-shardmap-after-a-shard-is-restored"></a>Adjuntar un toohello particiones ShardMap después de restaura una partición
Hola [AttachShard método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.attachshard.aspx) adjunta Hola mapa de particiones de toohello de partición determinado. A continuación, detecta cualquier incoherencia de mapa de particiones y actualiza la partición de hello asignaciones toomatch hello en el momento de Hola de restauración de la partición de Hola. Se supone que esa base de datos de hello es también tooreflect cuyo nombre ha cambiado Hola base de datos nombre original (antes de que se restauró la partición de hello), puesto que la restauración de un momento dado de hello tiene como valor predeterminado tooa nueva base de datos anexado con marca de tiempo de Hola. 

   ```
   rm.AttachShard(location, shardMapName)
   ``` 

* Hola *ubicación* parámetro es el nombre del servidor de Hola y el nombre de base de datos de particiones de Hola que se va a adjuntar. 
* Hola *shardMapName* parámetro es el nombre de asignación de particiones de Hola. Esto solo es necesario cuando se administran varias asignaciones de particiones por hello mismo administrador de mapa de particiones. Opcional. 

Este ejemplo agrega un mapa de particiones de toohello de partición que se ha restaurado recientemente de un momento dado anterior. Puesto que se ha restaurado la partición de hello (es decir Hola asignación de particiones de Hola Hola LSM), es potencialmente incoherente con la entrada de partición de Hola Hola GSM. Fuera de este código de ejemplo, partición de Hola se restauró y cambiar toohello nombre original de la base de datos de Hola. Puesto que se restauró, se supone asignación Hola Hola LSM es asignación confianza Hola. 

   ```
   rm.AttachShard(s.Location, customerMap); 
   var gs = rm.DetectMappingDifferences(s.Location); 
      foreach (RecoveryToken g in gs) 
       { 
       rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
       } 
   ```

## <a name="updating-shard-locations-after-a-geo-failover-restore-of-hello-shards"></a>Actualizar ubicaciones de particiones tras una conmutación geográfica (restore) de particiones de Hola
Si se produce una conmutación geográfica, base de datos secundaria de Hola se realiza escribir accesible y se convierte en la base de datos principal Hola nueva. Hola nombre del servidor de hello y, potencialmente, base de datos de hello (dependiendo de la configuración), puede ser diferente de la réplica principal original Hola. Hola, por tanto, las entradas de asignación de particiones de Hola Hola GSM y debe corregirse LSM. De forma similar, si hello base de datos es restaurada tooa otro nombre o ubicación o tooan punto anterior en el tiempo, esto podría dar lugar a incoherencias en asignaciones de particiones de Hola. Hola Shard Map Manager controla la distribución de Hola de base de datos de las conexiones abiertas toohello correcta. Distribución se basa en datos de hello en mapa de particiones de Hola y el valor de Hola de clave de particionamiento de Hola que es el destino de saludo de solicitud de aplicaciones de Hola. Después de una conmutación geográfica, esta información debe actualizarse con el nombre del servidor precisa de hello, nombre de base de datos y asignación de particiones de base de datos recuperada de Hola. 

## <a name="best-practices"></a>Prácticas recomendadas
Conmutación por error geográfica y recuperación son operaciones suelen ser administradas por un administrador de la nube de aplicación Hola intencionadamente utilizando una de las características de continuidad del negocio de bases de datos de SQL Azure. Planificación de continuidad del negocio requiere procesos, procedimientos y medidas tooensure que operaciones comerciales puedan continuar sin interrupción. Hola métodos disponibles como parte del programa Hola RecoveryManager clase debe utilizarse dentro de este hello tooensure de flujo de trabajo GSM y LSM se mantengan protegidos en función de la acción de recuperación de hello realizada. Hay cinco pasos básicos tooproperly garantizar Hola GSM y LSM reflejan información precisa de hello después de un evento de conmutación por error. Hola tooexecute de código de aplicación que estos pasos se pueden integrar en el flujo de trabajo y las herramientas existentes. 

1. Recuperar hello RecoveryManager de hello ShardMapManager. 
2. Separar la partición antigua de Hola de mapa de particiones de Hola.
3. Adjuntar Hola nueva partición toohello mapa de particiones, incluida la ubicación de hello nueva partición.
4. Detectar incoherencias en hello asignación entre Hola GSM y LSM. 
5. Resolver las diferencias entre Hola GSM y Hola LSM, que confía Hola LSM. 

Este ejemplo realiza Hola pasos:

1. Quita particiones de mapa de particiones que refleja las ubicaciones de particiones antes del evento de conmutación por error de Hola Hola.
2. Adjunta particiones toohello mapa de particiones reflejan Hola nuevas particiones ubicaciones (parámetro hello "Configuration.SecondaryServer" es el nombre del servidor nuevo de hello pero Hola mismo nombre de base de datos).
3. Recupera los tokens de recuperación de hello mediante la detección de diferencias de asignación entre Hola GSM y Hola LSM para cada partición. 
4. Resuelve las incoherencias de Hola que confía asignación Hola de hello LSM de cada partición. 
   
   ```
   var shards = smm.GetShards(); 
   foreach (shard s in shards) 
   { 
     if (s.Location.Server == Configuration.PrimaryServer) 
   
         { 
          ShardLocation slNew = new ShardLocation(Configuration.SecondaryServer, s.Location.Database); 
   
          rm.DetachShard(s.Location); 
   
          rm.AttachShard(slNew); 
   
          var gs = rm.DetectMappingDifferences(slNew); 
   
          foreach (RecoveryToken g in gs) 
            { 
               rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
            } 
        } 
    } 
   ```

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-database-recovery-manager/recovery-manager.png

