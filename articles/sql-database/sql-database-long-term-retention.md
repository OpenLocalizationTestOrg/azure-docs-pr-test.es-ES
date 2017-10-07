---
title: "aaaStore base de datos de SQL Azure copias de seguridad de los años too10 | Documentos de Microsoft"
description: "Obtenga información acerca de la base de datos de SQL Azure admite almacenar copias de seguridad para too10 años."
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a>Almacenar copias de seguridad de base de datos de SQL Azure para too10 años
Muchas aplicaciones tienen normativas, cumplimiento y otras empresas que requieren las copias de seguridad de base de datos de tooretain más allá de hello 7-35 días proporcionadas por base de datos de SQL Azure con fines [copias de seguridad automáticas](sql-database-automated-backups.md). Mediante la característica de copia de seguridad de retención a largo plazo de Hola, puede almacenar las copias de seguridad de la base de datos SQL en un almacén de servicios de recuperación de Azure para too10 años. Puede almacenar hasta too1, 000 bases de datos por almacén. A continuación, puede seleccionar cualquier copia de seguridad en hello almacén toorestore como una base de datos.

> [!IMPORTANT]
> Retención de copia de seguridad a largo plazo es actualmente en versión preliminar y está disponible en hello siguientes regiones: Australia Oriental, sudeste de Australia, sur de Brasil, Central EE. UU., Asia oriental, UU, UU 2, India Central, sur de India, este de Japón, oeste de Japón, Ee.uu. Central Norte, Norte Europa, sur Central US, sudeste de Asia, Europa occidental y oeste de Estados Unidos.
>

> [!NOTE]
> Puede habilitar la seguridad de bases de datos de too200 por almacén durante un período de 24 horas. Se recomienda que use un almacén independiente para cada impacto de hello toominimize de servidor de este límite. 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a>¿Cómo funciona la retención de copias de seguridad a largo plazo de SQL Database?

Con la retención de copias de seguridad a largo plazo, puede asociar un servidor de bases de datos SQL a un almacén de Azure Recovery Services. 

* Debe crear el almacén de Hola Hola misma suscripción de Azure que crea Hola SQL server y en Hola mismo grupo de recursos y la región geográfico. 
* A continuación, configure una directiva de retención para cualquier base de datos. toobe Hola directiva causas Hola semanal completa de la base de datos las copias de seguridad copia toohello el almacén de servicios de recuperación y se conserva durante el período de retención especificado hello (arriba too10 años). 
* A continuación, puede restaurar base de datos de Hola desde cualquiera de estas copias de seguridad tooa nueva base de datos en cualquier servidor de suscripción de Hola. Almacenamiento de Azure crea una copia de las copias de seguridad existentes, y copia de hello no tiene ningún impacto en el rendimiento en la base de datos existente de Hola.

> [!TIP]
> Para un tooguide cómo, consulte [configurar y restauración de retención de copia de seguridad a largo plazo de base de datos de SQL Azure](sql-database-long-term-backup-retention-configure.md).

## <a name="enable-long-term-backup-retention"></a>Habilitación de la retención de copias de seguridad a largo plazo

tooconfigure retención de copia de seguridad a largo plazo para una base de datos:

1. Cree un almacén de servicios de recuperación de Azure en hello mismo grupo de recursos, región y suscripción que el servidor de base de datos SQL. 
2. Registrar el almacén de hello server toohello.
3. Cree una directiva de protección de Azure Recovery Services.
4. Aplicar Hola protección directiva toohello las bases de datos que requieren la retención de copia de seguridad a largo plazo.

tooconfigure, administrar y restaurar una base de datos de retención de copia de seguridad a largo plazo de copias de seguridad automatizadas en un almacén de servicios de recuperación de Azure, realice una de las siguientes de hello:

* Uso de Hola portal de Azure: haga clic en **retención de copia de seguridad a largo plazo**, seleccione una base de datos y, a continuación, haga clic en **configurar**. 

   ![Seleccionar base de datos para retención de copias de seguridad a largo plazo](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* Uso de PowerShell: Vaya demasiado[configurar y restauración de retención de copia de seguridad a largo plazo de base de datos de SQL Azure](sql-database-long-term-backup-retention-configure.md).

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a>Restaurar una base de datos que se almacena junto con la característica de copia de seguridad de retención a largo plazo de Hola

toorecover desde una copia de seguridad a largo plazo de retención de copia de seguridad:

1. Almacén de Hola de lista donde se almacena la copia de seguridad de Hola.
2. Contenedor de Hola de lista es servidor lógico tooyour asignada.
3. Origen de datos de lista hello en el almacén de Hola que está asignada tooyour base de datos de.
4. Puntos de recuperación hello en el lista que están disponible toorestore.
5. Restaurar base de datos de Hola Hola recuperación toohello de punto de servidor de destino dentro de su suscripción.

tooconfigure, administrar y restaurar una base de datos de retención de copia de seguridad a largo plazo de copias de seguridad automatizadas en un almacén de servicios de recuperación de Azure, realice una de las siguientes de hello:

* Uso de Hola portal de Azure: vaya demasiado[retención de copia de seguridad a largo plazo de administrar mediante Hola portal de Azure](sql-database-long-term-backup-retention-configure.md). 

* Uso de PowerShell: Vaya demasiado[administrar la retención de copia de seguridad a largo plazo con PowerShell](sql-database-long-term-backup-retention-configure.md).

## <a name="get-pricing-for-long-term-backup-retention"></a>Obtención de precios para la retención de copias de seguridad a largo plazo

Retención de copia de seguridad a largo plazo de una base de datos SQL se cobra según toohello [las tasas de precios de servicios de copia de seguridad Azure](https://azure.microsoft.com/pricing/details/backup/).

Después de servidor de base de datos SQL de hello es el almacén de toohello registrado, se le cobra por almacenamiento total de Hola que usa Hola semanal copias de seguridad almacenadas en el almacén de Hola.

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a>Consulta de las copias de seguridad disponibles almacenadas en retención de copias de seguridad a largo plazo

tooconfigure, administrar y restaurar una base de datos de retención de copia de seguridad a largo plazo de copias de seguridad automatizadas en un almacén de servicios de recuperación de Azure mediante Hola portal de Azure, realice una de las siguientes de hello:

* Uso de Hola portal de Azure: vaya demasiado[retención de copia de seguridad a largo plazo de administrar mediante Hola portal de Azure](sql-database-long-term-backup-retention-configure.md). 

* Uso de PowerShell: Vaya demasiado[administrar la retención de copia de seguridad a largo plazo con PowerShell](sql-database-long-term-backup-retention-configure.md).

## <a name="disable-long-term-retention"></a>Deshabilitación de la retención a largo plazo

servicio de recuperación de Hello controla automáticamente la limpieza de Hola de copias de seguridad según Hola proporcionada la directiva de retención. 

las copias de seguridad Hola envío toostop, para un depósito de toohello de base de datos específica, quite la directiva de retención de Hola para esa base de datos.
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> las copias de seguridad de Hola que ya están en el almacén de Hola se ven afectados. Se eliminan automáticamente por el servicio de recuperación de hello cuando expira el período de retención.

## <a name="long-term-backup-retention-faq"></a>Preguntas frecuentes sobre la retención de copias de seguridad a largo plazo

**¿Se puede eliminar manualmente las copias de seguridad específicos en el almacén de hello?**

Actualmente, no. almacén de Hello limpia automáticamente las copias de seguridad cuando ha expirado el período de retención de Hola.

**¿Puedo registrar mi toomore de copias de seguridad de servidor toostore a un depósito?**

No, actualmente puede almacenar un depósito de tooonly de las copias de seguridad a la vez.

**¿Puedo tener un almacén y un servidor en suscripciones distintas?**

No, actualmente el almacén de Hola y servidor deben estar en hello mismo grupo de recursos y de suscripción.

**¿Puedo usar un almacén que he creado en una región que es distinta a la de mi servidor?**

No, el almacén de Hola y servidor deben estar en hello mismo toominimize de región, copie el tiempo y evitar cargos de tráfico.

**¿Cuántas bases de datos puedo guardar en un almacén?**

Actualmente, se admiten la too1, 000 bases de datos por almacén. 

**¿Cuántos almacenes puedo crear por suscripción?**

Puede crear hasta too25 almacenes por suscripción.

**¿Cuántas bases de datos puedo configurar diariamente por almacén?**

Puede configurar 200 bases de datos diariamente por almacén.

**¿La retención de copias de seguridad a largo plazo funciona con grupos elásticos?**

Sí. Cualquier base de datos en bloque de hello puede configurarse con la directiva de retención de Hola.

**¿Se puede elegir tiempo hello en que se creó la copia de seguridad de hello?**

No, base de datos SQL controla Hola programar copia de seguridad toominimize Hola impacto en el rendimiento en las bases de datos.

**Si dispone de cifrado de datos transparente habilitado para la base de datos. ¿Puedo utilizarlo con el almacén de hello?** 

Si, se admite el cifrado de datos transparente. Puede restaurar base de datos de hello del almacén de hello incluso si la base de datos original de hello ya no existe.

**¿Qué ocurre con las copias de seguridad de hello en el almacén de hello si se suspende mi suscripción?** 

Si la suscripción está suspendida, se conservan las copias de seguridad y bases de datos existentes de Hola. Nuevas copias de seguridad no son almacén toohello copiada. Después de reactivar la suscripción de hello, servicio de hello vuelve a copiar el almacén de copias de seguridad toohello. El almacén se convierte en operaciones de restauración toohello accesible mediante copias de seguridad de Hola que se copiaron existe antes de que se suspendió la suscripción de Hola. 

**¿Puedo obtener acceso a archivos de copia de seguridad de base de datos SQL toohello para que puedo descargar o restaurarlas toohello SQL server?**

Actualmente, no.

**Es posible toohave todas las programaciones (diaria, semanal, mensual, anual) dentro de una directiva de retención SQL.**

No, actualmente solo están disponibles varias programaciones para las copias de seguridad de máquinas virtuales.

**¿Qué ocurre si establecemos la retención de copias de seguridad a largo plazo en una base de datos secundaria con replicación geográfica activa?**

Dado que no creamos copias de seguridad de réplicas, actualmente no hay ninguna opción para la retención de copias de seguridad a largo plazo en bases de datos secundarias. Sin embargo, es importante para los usuarios tooset una retención de copia de seguridad a largo plazo en una base de datos de replicación geográfica activa secundaria por estos motivos:
* Cuando se produce una conmutación por error y la base de datos de Hola se convierte en una base de datos principal, se hace una completa de copia de seguridad, que es cargado toovault.
* No hay ningún extra costos toohello cliente para configurar la retención de copia de seguridad a largo plazo en una base de datos secundaria.

## <a name="next-steps"></a>Pasos siguientes
Dado que las copias de seguridad de bases de datos protegen los datos de eliminaciones o daños accidentales, son una parte esencial de cualquier estrategia de recuperación ante desastres y de continuidad empresarial. toolearn aproximadamente Hola otras soluciones de continuidad del negocio de base de datos SQL, consulte [información general sobre la continuidad de negocio](sql-database-business-continuity.md).
