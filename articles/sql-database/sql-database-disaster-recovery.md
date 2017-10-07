---
title: "recuperación ante desastres de bases de datos aaaSQL | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toorecover una base de datos de un centro de datos regional suministro o con Hola base de datos de SQL Azure la replicación geográfica activa y las capacidades de restauración geográfica."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 4800960e-3f9d-40ce-9e55-fb7f2784c067
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: sashan
ms.openlocfilehash: bae08485863067748107ec4808e52d8e88e2de0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-database-or-failover-tooa-secondary"></a>Restaurar tooa secundario para una base de datos de SQL Azure o conmutación por error
La base de datos de SQL Azure ofrece Hola después de capacidades para recuperarse de una interrupción del servicio:

* [Replicación geográfica activa](sql-database-geo-replication-overview.md)
* [Restauración geográfica](sql-database-recovery-using-backups.md#point-in-time-restore)

toolearn sobre escenarios de continuidad empresarial y características de hello compatibles con estos escenarios, vea [continuidad del negocio](sql-database-business-continuity.md).

### <a name="prepare-for-hello-event-of-an-outage"></a>Preparar para eventos de Hola de una interrupción del servicio
Para lograr el éxito con la región de datos de recuperación tooanother con replicación geográfica activa o las copias de seguridad con redundancia geográfica, necesita tooprepare un servidor en otro datos center interrupción toobecome Hola nuevo servidor principal debe Hola necesita surgen así como tener pasos bien definidos probado y documentado tooensure una recuperación sin problemas. Estos son algunos de los pasos correspondientes a la fase de preparación:

* Identifique el servidor lógico de hello en otra región toobecome Hola nuevo servidor principal. Con la replicación geográfica activa, esta será al menos uno y quizás cada uno de los servidores secundarios de Hola. Para la restauración geográfica, esto suele ser un servidor en hello [región emparejada](../best-practices-availability-paired-regions.md) de región de hello en el que se encuentra la base de datos.
* Identificar y, opcionalmente, definir, las reglas de firewall de nivel de servidor de hello necesarios en los usuarios tooaccess Hola nueva base de datos principal.
* Determinar cómo se van tooredirect usuarios toohello nuevo servidor principal, como cambiar las cadenas de conexión o cambiando las entradas de DNS.
* Identificar y, opcionalmente, crear, Hola inicios de sesión que deben estar presente en la base de datos maestra de hello en el nuevo servidor principal de Hola y asegúrese de que estos inicios de sesión tienen los permisos adecuados en la base de datos maestra de hello, si lo hay. Para obtener más información, consulte [Administración de la seguridad de Base de datos SQL de Azure después de la recuperación ante desastres](sql-database-geo-replication-security-config.md)
* Identificar las reglas de alerta que necesitan toobe toomap actualizada toohello nueva base de datos principal.
* Configuración de auditoría de Hola de documento en la base de datos principal Hola actual
* Realice [maniobras de recuperación ante desastres](sql-database-disaster-recovery-drills.md). toosimulate una interrupción para la restauración geográfica, puede eliminar o cambiar el nombre de error de conectividad de la aplicación de toocause de hello origen base de datos. toosimulate una interrupción del servicio de replicación geográfica activa, puede deshabilitar aplicación de hello web o máquina virtual conectada toohello base de datos o de conmutación por error Hola base de datos toocause conectividad errores de aplicación.

## <a name="when-tooinitiate-recovery"></a>Cuando tooinitiate recuperación
operación de recuperación de Hello afecta aplicación hello. Es necesario cambiar la cadena de conexión de SQL de Hola o redirección con DNS y dar lugar a pérdida de datos permanente. Por lo tanto, debe realizarse solo una vez interrupción hello toolast es probable que más de objetivo de tiempo de recuperación de la aplicación. Una vez hello aplicación tooproduction implementado debe realizar la supervisión regular de estado de la aplicación hello y usar hello es garantizar la sobresuscripción tooassert puntos que Hola de recuperación de datos siguientes:

1. Error de conectividad permanente de base de datos toohello capa de aplicación de Hola.
2. Hola portal de Azure, muestra una alerta sobre un incidente en la región de hello con gran impacto.
3. servidor de base de datos de SQL Azure de Hello está marcado como degradado.

Dependiendo de su responsabilidad de negocio de toodowntime y posibles de tolerancia de aplicación puede considerar Hola siguientes opciones de recuperación.

Hola de uso [obtener base de datos recuperable](https://msdn.microsoft.com/library/dn800985.aspx) (*LastAvailableBackupDate*) punto de restauración de replicación geográfica más reciente de tooget Hola.

## <a name="wait-for-service-recovery"></a>Espera para la recuperación del servicio
Hello Azure los equipos trabajan minuciosamente toorestore disponibilidad del servicio tal y como rápidamente como sea posible, pero dependiendo de la causa raíz de hello puede tardar horas o días.  Si su aplicación tolera mucho tiempo de inactividad puede esperar simplemente hello toocomplete de recuperación. En este caso, no se requieren acciones por su parte. Puede ver el estado actual del servicio hello en nuestro [panel de estado del servicio de Azure](https://azure.microsoft.com/status/). Después de la recuperación de Hola de región de Hola se restaurará la disponibilidad de su aplicación.

## <a name="fail-over-toogeo-replicated-secondary-database"></a>Conmutar por error toogeo con replicación de base de datos secundaria
Si el tiempo de inactividad de la aplicación puede dar lugar a responsabilidades civiles, debería utilizar bases de datos con replicación geográfica en la aplicación. Se habilitará la disponibilidad de restauración tooquickly hello las aplicaciones en una región distinta en el caso de una interrupción. Obtenga información acerca de cómo demasiado[configurar la replicación geográfica](sql-database-geo-replication-portal.md).

disponibilidad de toorestore del programa Hola a bases de datos necesita tooinitiate Hola mediante uno de los métodos de hello admitida la conmutación por error toohello replicación geográfica secundaria.

Use uno de hello siguiendo guías toofail a través de la base de datos de tooa replicación geográfica secundaria:

* [Conmutar por error tooa georreplicadas base de datos secundaria mediante el Portal de Azure](sql-database-geo-replication-portal.md)
* [Conmutar por error tooa replicación geográfica secundaria mediante PowerShell](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
* [Conmutar por error tooa georreplicadas base de datos secundaria mediante T-SQL](sql-database-geo-replication-transact-sql.md)

## <a name="recover-using-geo-restore"></a>Recuperación mediante la restauración geográfica
Si el tiempo de inactividad de la aplicación no da como resultado la responsabilidad de negocio puede usar [georestauración](sql-database-recovery-using-backups.md) como un método toorecover las bases de datos de aplicación. Crea una copia de base de datos de Hola desde su última copia de seguridad con redundancia geográfica.

## <a name="configure-your-database-after-recovery"></a>Configuración de la base de datos después de realizar la recuperación
Si usas conmutación por error de replicación geográfica o la restauración geográfica toorecover desde una interrupción, debe asegurarse de que Hola conectividad toohello nuevas bases de datos está configurado correctamente para que se puede reanudar la función de aplicación normal de hello. Esto es una lista de comprobación de tareas tooget listos para la producción de base de datos recuperada.

### <a name="update-connection-strings"></a>Actualización de cadenas de conexión
Dado que la base de datos recuperada residen en un servidor diferente, deberá tooupdate servidor toothat toopoint cadena de conexión a la aplicación.

Para obtener más información acerca de cómo cambiar las cadenas de conexión, vea el lenguaje de desarrollo adecuada de Hola para su [biblioteca de conexiones de](sql-database-libraries.md).

### <a name="configure-firewall-rules"></a>Configuración de las reglas del firewall
Necesita toomake Asegúrese de que las reglas de firewall de hello configurado en servidor y en la coincidencia de la base de datos de hello aquellos que se han configurado en el servidor principal de Hola y base de datos principal. Para obtener más información, consulte [Configuración del firewall (Base de datos SQL de Azure)](sql-database-configure-firewall-settings.md).

### <a name="configure-logins-and-database-users"></a>Configuración de inicios de sesión de y de usuarios de la base de datos
Necesita toomake seguro de que todos los inicios de sesión de hello utilizados por la aplicación existen en el servidor de Hola que hospeda la base de datos recuperada. Para obtener más información, consulte [Configuración de seguridad para Replicación geográfica activa o estándar](sql-database-geo-replication-security-config.md).

> [!NOTE]
> Debe configurar y probar las reglas de firewall del servidor y los inicios de sesión (y sus permisos) durante una maniobra de recuperación ante desastres. Estos objetos de nivel de servidor y su configuración no estén disponibles durante la interrupción de Hola.
> 
> 

### <a name="setup-telemetry-alerts"></a>Configuración de alertas de telemetría
Debe toomake que la configuración de regla de alerta existente estén actualizados toomap toohello recuperado hello y base de datos de otro servidor.

Para obtener más información sobre las reglas de alerta de las bases de datos, consulte [Recibir notificaciones de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) y [Realización de seguimiento del estado](../monitoring-and-diagnostics/insights-service-health.md).

### <a name="enable-auditing"></a>Habilitar auditoría
Si la auditoría está tooaccess requiere la base de datos, necesita tooenable auditoría después de una recuperación de base de datos de Hola. Para obtener más información, consulte [este artículo sobre la realización de auditorías en las bases de datos](sql-database-auditing.md).

## <a name="next-steps"></a>Pasos siguientes
* toolearn acerca de las copias de seguridad de base de datos de SQL de Azure automatizada, vea [copias de seguridad automáticas de base de datos SQL](sql-database-automated-backups.md)
* toolearn sobre escenarios de recuperación y diseño de continuidad de negocio, vea [escenarios de continuidad](sql-database-business-continuity.md)
* toolearn sobre el uso de copias de seguridad automatizadas para la recuperación, vea [restaurar una base de datos de copias de seguridad de hello iniciadas por el servicio](sql-database-recovery-using-backups.md)

