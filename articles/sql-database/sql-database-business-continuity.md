---
title: "continuidad del negocio aaaCloud: recuperación de base de datos: base de datos SQL | Documentos de Microsoft"
description: "Obtenga información acerca de cómo la Base de datos SQL de Azure permite la continuidad del negocio en la nube y la recuperación de la base de datos, y ayuda a que las aplicaciones críticas de la nube se sigan ejecutando."
keywords: "continuidad del negocio, continuidad del negocio en la nube, recuperación de desastres de la base de datos, recuperación de la base de datos"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 18e5d3f1-bfe5-4089-b6fd-76988ab29822
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/15/2017
ms.author: sashan
ms.openlocfilehash: c9a6ff86fbbc04ce839a4fca79594b573b71644c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-business-continuity-with-azure-sql-database"></a>Introducción a la continuidad empresarial con Base de datos SQL de Azure

Esta información general describe las capacidades de Hola que base de datos de SQL Azure proporciona continuidad del negocio y recuperación ante desastres. Obtenga información acerca de opciones, recomendaciones y los tutoriales para recuperarse de eventos potencialmente perjudiciales que pudieron provocar la pérdida de datos o causar toobecome no está disponible para su base de datos y aplicaciones. Obtenga información acerca de qué toodo cuando un error del usuario o aplicación afecta a la integridad de los datos, una región de Azure tiene una interrupción o la aplicación requiere mantenimiento.

## <a name="sql-database-features-that-you-can-use-tooprovide-business-continuity"></a>Características de base de datos de SQL que se puede usar la continuidad del negocio tooprovide

Base de datos SQL ofrece diversas funcionalidades de continuidad empresarial, incluidas las copias de seguridad automatizadas y la replicación de base de datos opcional. Cada una de ellas posee distintas características que abarcan los conceptos de tiempo de recuperación calculado (ERT) y pérdida de datos potencial de transacciones recientes. Cuando entienda estas opciones, puede elegir las que más relevantes considere y, en la mayoría de los escenarios, utilizarlas juntas con distintos objetivos. Cuando desarrolle su plan de continuidad del negocio, necesita toounderstand Hola máximo aceptable tiempo antes de aplicación hello totalmente recupera después evento perturbador Hola; éste es el objetivo de tiempo de recuperación (RTO). También necesita toounderstand cantidad máxima de Hola de aplicación de Hola de actualizaciones (intervalo de tiempo) de datos reciente puede tolerar perder la recuperación tras evento perturbador Hola; éste es el objetivo de punto de recuperación (RPO).

Hola siguiente tabla compara hello ERT y el RPO para escenarios más comunes de hello tres.

| Capacidad | Nivel Basic | Nivel Standard | Nivel Premium |
| --- | --- | --- | --- |
| Restauración a un momento dado a partir de una copia de seguridad |Cualquier punto de restauración en 7 días |Cualquier punto de restauración en 35 días |Cualquier punto de restauración en 35 días |
| Restauración geográfica de las copias de seguridad con replicación geográfica |ERT < 12h, RPO < 1 h |ERT < 12h, RPO < 1 h |ERT < 12h, RPO < 1 h |
| Restauración de datos del Almacén de copia de seguridad de Azure |ERT < 12 h, RPO < 1 h |ERT < 12 h, RPO < 1 h |ERT < 12 h, RPO < 1 h |
| Replicación geográfica activa |ERT < 30 s, RPO < 5 s |ERT < 30 s, RPO < 5 s |ERT < 30 s, RPO < 5 s |

### <a name="use-database-backups-toorecover-a-database"></a>Usar copias de seguridad de base de datos toorecover una base de datos

Base de datos SQL realiza automáticamente una combinación de copias de seguridad de base de datos completa semanal, copias de seguridad diferenciales cada hora y registro de transacciones las copias de seguridad cada cinco: diez minutos tooprotect su negocio frente a pérdidas de datos. Estas copias de seguridad se almacenan en el almacenamiento con redundancia geográfica para 35 días para las bases de datos en niveles de servicio Standard y Premium de Hola y 7 días para bases de datos de nivel de servicio Basic Hola. Para más información, consulte el artículo sobre [niveles de servicio](sql-database-service-tiers.md). Si el período de retención de hello para el nivel de servicio no cumple sus requisitos empresariales, puede aumentar el período de retención de Hola por [cambiar el nivel de servicio de hello](sql-database-service-tiers.md). Hello las copias de seguridad completas y diferenciales de base de datos también están replicado tooa [centro de datos emparejado](../best-practices-availability-paired-regions.md) para protección contra una interrupción del centro de datos. Para más información, consulte [copias de seguridad automáticas de bases de datos](sql-database-automated-backups.md).

Si el período de retención integrados de hello no es suficiente para la aplicación, puede ampliarlo mediante la configuración de una directiva de retención a largo plazo de base de datos. Para más información, consulte [retención a largo plazo](sql-database-long-term-retention.md).

Puede usar estos toorecover de copias de seguridad de base de datos automática una base de datos de varios eventos potencialmente perjudiciales, tanto dentro de su centro de datos y el centro de datos de tooanother. Usar copias de seguridad de base de datos automática, Hola estimado de tiempo de recuperación depende de varios factores, incluido el número total de Hola de bases de datos de recuperación en hello mismo región en hello al mismo tiempo, Hola tamaño de base de datos, tamaño del registro de transacciones de hello y ancho de banda de red. tiempo de recuperación de Hello suele ser inferior a 12 horas. Al recuperar la región de datos de tooanother, posible pérdida de datos hello es hora de too1 limitado por el almacenamiento con redundancia geográfica de Hola de copias de seguridad diferencial de la base de datos por hora.

> [!IMPORTANT]
> toorecover utilizando copias de seguridad automáticas, debe ser miembro del rol de colaborador de SQL Server de Hola o propietario de la suscripción de hello: vea [RBAC: roles integrados](../active-directory/role-based-access-built-in-roles.md). Puede recuperar con hello portal de Azure, PowerShell o API de REST de Hola. No puede utilizar Transact-SQL.
>

Utilice las copias de seguridad automatizadas como mecanismo de recuperación y de continuidad empresarial si se cumplen los siguientes requisitos en su aplicación:

* No se considera crítica.
* No tiene un Acuerdo de Nivel de Servicio vinculante, por lo que no incurrirá en responsabilidades financieras en caso de tiempos de inactividad de 24 horas o más.
* Tiene una baja tasa de cambio de datos (bajas transacciones por hora) y la pérdida de tooan hora del cambio es una pérdida aceptable de datos.
* Los costos son un factor fundamental.

Si necesita recuperaciones más rápidas, utilice la [replicación geográfica activa](sql-database-geo-replication-overview.md) (se describe a continuación). Si necesita toobe toorecover capaz de datos de un período de más de 35 días, use [retención de copia de seguridad a largo plazo](sql-database-long-term-retention.md). 

### <a name="use-active-geo-replication-and-auto-failover-groups-in-preview-tooreduce-recovery-time-and-limit-data-loss-associated-with-a-recovery"></a>Use active replicación geográfica y la conmutación por error automática grupos (en vista previa) tooreduce recuperación tiempo y límite de pérdida de datos asociada con la recuperación

Además toousing copias de seguridad de base de datos para la base de datos de recuperación si se produce una interrupción del negocio, puede usar [replicación geográfica activa](sql-database-geo-replication-overview.md) tooconfigure un toohave de base de datos de toofour legible bases de datos secundarias en regiones de Hola de su elección. Estas bases de datos secundarias se mantienen sincronizados con hello base de datos principal utilizando un mecanismo de replicación asincrónica. Esta característica es usado tooprotect contra la interrupción del negocio si se produce una interrupción del centro de datos o durante una actualización de la aplicación. Replicación geográfica activa también puede ser tooprovide utilizados mejor rendimiento de las consultas para los usuarios de toogeographically distribuido de consultas de solo lectura.

tooenable automatizada y conmutación por error transparente debe organizar las bases de datos de replicación geográfica en grupos que usan hello [grupo de conmutación por error automática](sql-database-geo-replication-overview.md) característica de base de datos de SQL (en vista previa).

Si la base de datos principal de Hola se queda sin conexión inesperadamente o necesita tootake en modo sin conexión para las actividades de mantenimiento, rápidamente puede promocionar principal hello toobecome secundaria (también denominado una conmutación por error) y configurar principal de las aplicaciones tooconnect toohello promocionado. Si la aplicación conecta a bases de datos de toohello mediante el agente de escucha del grupo de conmutación por error de hello, no necesita configuración de cadena de conexión de SQL de toochange Hola después de la conmutación por error. Con las conmutaciones por error planeadas no se pierden datos. Con una conmutación por error no planeada, puede haber algunas pequeña cantidad de pérdida de datos muy reciente transacciones debido toohello naturaleza de la replicación asincrónica. Uso de grupos de conmutación por error automática (en vista previa), puede personalizar Hola conmutación por error directiva toominimize Hola posible pérdida de datos. Después de una conmutación por error, puede posterior conmutación por recuperación: correspondiente plan tooa o al centro de datos de hello vuelve a estar conectado. En todos los casos, los usuarios experimentan una pequeña cantidad de tiempo de inactividad y necesitan tooreconnect.

> [!IMPORTANT]
> toouse la replicación geográfica activa y los grupos de conmutación por error automática (en vista previa), debe ser propietario de la suscripción de Hola o tener permisos administrativos en SQL Server. Puede configurar y conmutar por error utilizando Hola portal de Azure, PowerShell u Hola API de REST con permisos de suscripción de Azure o mediante Transact-SQL con permisos de SQL Server.
> 

Use la replicación geográfica activa y los grupos de conmutación automática por error (versión preliminar) si su aplicación cumple alguno de estos criterios:

* Es crítica.
* Tiene un SLA que no se permite que se produzcan tiempos de inactividad de más de 24 horas.
* El tiempo de inactividad incurrirá en responsabilidades financieras.
* Tiene una tasa de cambio de datos elevada y no se acepta perder una hora de datos.
* costo adicional de Hola de replicación geográfica activa es menor que la responsabilidad financiera potencial de Hola y pérdida de asociados de negocios.

>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-protecting-important-DBs-from-regional-disasters-is-easy/player]
>

## <a name="recover-a-database-after-a-user-or-application-error"></a>Recuperación de bases de datos tras un error del usuario o la aplicación
Nadie es perfecto. Un usuario podría eliminar de forma involuntaria algunos datos, una tabla importante o, incluso, una base de datos entera. O bien, una aplicación podría sobrescribir accidentalmente los datos correctos con datos incorrectos debido tooan defecto de la aplicación.

Estas son las opciones de recuperación que tiene para este caso.

### <a name="perform-a-point-in-time-restore"></a>Realización de una restauración a un momento dado
Puede usar copias de seguridad de hello automatizada toorecover una copia de su tooa de base de datos conocido buen punto en el tiempo, siempre que la hora está dentro del período de retención de base de datos de Hola. Una vez restaurada la base de datos de hello, puede reemplazar base de datos original de hello con base de datos de hello restaurar o copiar datos Hola necesitado desde los datos de hello restaurar en la base de datos original de Hola. Si la base de datos de hello usa replicación geográfica activa, se recomienda copiar datos de hello necesario de copia de hello restaurado en la base de datos original de Hola. Si reemplaza la base de datos original de Hola con base de datos de hello restaurar, es necesario tooreconfigure y resincronizar la replicación geográfica activa (que puede tardar bastante tiempo en una base de datos grande).

Para obtener más información y para obtener pasos detallados para restaurar un punto de tooa de base de datos en tiempo de mediante Hola portal de Azure o con PowerShell, vea [restauración a un punto en el momento](sql-database-recovery-using-backups.md#point-in-time-restore). Transact-SQL no se puede utilizar para este fin.

### <a name="restore-a-deleted-database"></a>Restauración de una base de datos eliminada
Si se elimina la base de datos de hello, pero no se eliminó el servidor lógico de hello, puede restaurar el punto de toohello de hello Eliminar base de datos en el que se ha eliminado. Esto restaura un toohello de copia de seguridad de base de datos lógico misma SQL server desde el que se ha eliminado. Puede restaurarla mediante el nombre original de Hola o proporcionar un nuevo nombre o la base de datos de hello restaurado.

Para obtener más información y para obtener pasos detallados para restaurar una base de datos eliminada mediante Hola portal de Azure o con PowerShell, vea [restaurar una base de datos eliminada](sql-database-recovery-using-backups.md#deleted-database-restore). Transact-SQL no se puede utilizar para este fin.

> [!IMPORTANT]
> Si se elimina el servidor lógico de hello, no se puede recuperar una base de datos eliminada.
>
>

### <a name="restore-from-azure-backup-vault"></a>Restauración de datos del Almacén de copia de seguridad de Azure
Si se produjo una pérdida de datos de hello fuera Hola de período de retención actual para copias de seguridad automatizadas y la base de datos está configurado para la retención a largo plazo, puede restaurar una copia de seguridad semanal en la nueva base de datos de almacén de copia de seguridad de Azure tooa. En este momento, puede reemplazar base de datos original de hello con base de datos de hello restaurar o copiar datos de hello necesitado de base de datos de hello restaurado en la base de datos original de Hola. Si necesita una versión anterior de la actualización de importantes de la aplicación de base de datos anterior tooa tooretrieve, satisfacer una solicitud de auditores o un pedido legal, que puede crear una base de datos mediante una copia de seguridad completa guardado en hello almacén de copia de seguridad de Azure.  Para más información, consulte [retención a largo plazo](sql-database-long-term-retention.md).

## <a name="recover-a-database-tooanother-region-from-an-azure-regional-data-center-outage"></a>Recuperarse de una región de tooanother de base de datos de una interrupción del centro de datos regional de Azure
<!-- Explain this scenario -->

Aunque es poco habitual, en los centros de datos de Azure pueden producirse interrupciones. Cuando esto ocurre, provoca también una interrupción en el negocio que podría extenderse solo unos pocos minutos o, incluso, horas.

* Una opción es toowait para su toocome de base de datos en línea cuando la interrupción del centro de datos de hello está por encima. Esto funciona para las aplicaciones que pueden permitirse toohave Hola base de datos sin conexión. Por ejemplo, un proyecto de desarrollo o prueba gratuita no necesita toowork en constantemente. Cuando un centro de datos tiene una interrupción del servicio, no sabrá cuánto tiempo puede durar interrupción hello, por lo que esta opción solo funciona si no necesita la base de datos durante un tiempo.
* Otra opción es tooeither producirá un error en la región de datos de tooanother si está usando replicación geográfica activa u Hola recuperar una base de datos con copias de seguridad de base de datos con redundancia geográfica (restauración geográfica). La conmutación por error solo lleva unos segundos, mientras que la recuperación de una base de datos a partir de copias de seguridad dura horas.

Cuando realiza la acción, cuánto tiempo tarda toorecover y cuánto pérdida de datos que se producen depende de cómo decidir toouse estas características de continuidad de negocio en la aplicación. De hecho, puede elegir toouse una combinación de copias de seguridad de base de datos y la replicación geográfica activa según sus requisitos de aplicación. Para ver una explicación de las consideraciones de diseño de las aplicaciones para bases de datos independientes y grupos elásticos con estas características de continuidad empresarial, consulte [Diseño de una aplicación para la recuperación ante desastres](sql-database-designing-cloud-solutions-for-disaster-recovery.md) y [Estrategias de recuperación ante desastres para aplicaciones que usan el grupo elástico](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).

Hello secciones siguientes proporcionan una visión general de hello pasos toorecover con las copias de seguridad de base de datos o la replicación geográfica activa. Para obtener pasos detallados incluida la planificación de requisitos y pasos posteriores a la recuperación, obtener información acerca de cómo toosimulate una tooperform de interrupción una recuperación ante desastres llegarse, consulte [recuperar una base de datos SQL de una interrupción](sql-database-disaster-recovery.md).

### <a name="prepare-for-an-outage"></a>Preparativos para interrupciones
Independientemente de la característica de continuidad de hello empresarial que se utiliza, debe:

* Identifique y prepare el servidor de destino de hello, incluidas las reglas de firewall de nivel de servidor, los inicios de sesión y permisos de nivel de base de datos maestra.
* Determinar cómo tooredirect los clientes y toohello nuevo servidor de aplicaciones de cliente
* Documentar otras dependencias, como las alertas y la configuración de auditoría

Si no se prepara correctamente, el proceso de conectar las aplicaciones después de una conmutación por error o una recuperación de base de datos llevará más tiempo y, probablemente, también haya que solucionar problemas en momentos de estrés, por lo que no es nada recomendable.

### <a name="fail-over-tooa-geo-replicated-secondary-database"></a>Conmutar por base de datos de tooa replicación geográfica secundaria
Si usa grupos de conmutación automática por error (versión preliminar) y la replicación geográfica activa como el mecanismo de recuperación, puede configurar una directiva de conmutación automática por error o usar la [conmutación por error manual](sql-database-disaster-recovery.md#fail-over-to-geo-replicated-secondary-database). Una vez iniciada, Hola conmutación por error causas Hola secundaria toobecome Hola nuevas transacciones nuevas toorecord principal y está listo y responder tooqueries - con la mínima pérdida de datos para los datos de hello aún no se han replicado. Para obtener información sobre cómo diseñar el proceso de conmutación por error de hello, consulte [diseñar una aplicación para la recuperación ante desastres de nube](sql-database-designing-cloud-solutions-for-disaster-recovery.md).

> [!NOTE]
> Al centro de datos de Hola se pone en línea primarios antiguo Hola automáticamente volver a conectar toohello nuevo elemento principal y se convierten en bases de datos secundarias. Si necesita región original de toorelocate hello toohello atrás principal, puede iniciar manualmente una conmutación por error planeada (conmutación por recuperación). 
> 

### <a name="perform-a-geo-restore"></a>Realización de restauraciones geográficas
Si utiliza copias de seguridad automatizadas con replicación de almacenamiento con redundancia geográfica como mecanismo de recuperación, [inicie una recuperación de base de datos mediante la restauración geográfica](sql-database-disaster-recovery.md#recover-using-geo-restore). Recuperación normalmente tiene lugar dentro de 12 horas, con pérdida de datos de la hora de tooone determinada cuando hello última por hora copia de seguridad diferencial con tomada y replicada. Hasta que se complete la recuperación de hello, Hola o base de datos no se puede toorecord todas las transacciones responde consultas tooany. Aunque esto restaura la base de datos toohello último disponible punto en el tiempo, restauración hello tooany de replicación geográfica secundaria punto en el tiempo no se admite actualmente.

> [!NOTE]
> Si el centro de datos de hello vuelve a conectarse antes de cambiar la aplicación a través de la base de datos recuperada toohello, puede cancelar la recuperación de Hola.  
>
>

### <a name="perform-post-failover--recovery-tasks"></a>Realización de tareas posteriores a la recuperación y conmutación por error
Tras la recuperación de cualquier mecanismo de recuperación, debe realizar Hola siguientes tareas adicionales antes de que los usuarios y las aplicaciones estén realizar copias de seguridad y ejecutando:

* Redirigir los clientes y toohello nuevo servidor de aplicaciones de cliente y base de datos restaurada
* Asegúrese de reglas de firewall de nivel de servidor adecuadas en su lugar para los usuarios tooconnect (o use [firewalls de nivel de base de datos](sql-database-firewall-configure.md#creating-and-managing-firewall-rules))
* No se olvide de emplear permisos de nivel de base de datos maestra e inicios de sesión apropiados (o use [usuarios contenidos](https://msdn.microsoft.com/library/ff929188.aspx)).
* Configure la auditoría según corresponda.
* Configure las alertas según corresponda.

## <a name="upgrade-an-application-with-minimal-downtime"></a>Actualice una aplicación con el mínimo tiempo de inactividad posible.
A veces, debe desconectar una aplicación debido a un mantenimiento planeado, por ejemplo, para actualizarla. [Administrar las actualizaciones de la aplicación](sql-database-manage-application-rolling-upgrade.md) describe el funcionamiento de tooenable de replicación geográfica activa toouse actualizaciones sucesivas de la nube aplicación toominimize el tiempo de inactividad durante las actualizaciones y proporcionar una ruta de recuperación si algo va mal. 

## <a name="next-steps"></a>Pasos siguientes
Para ver una explicación de las consideraciones de diseño de las aplicaciones para bases de datos independientes y grupos elásticos, consulte [Diseño de una aplicación para la recuperación ante desastres en la nube](sql-database-designing-cloud-solutions-for-disaster-recovery.md) y [Estrategias de recuperación ante desastres para aplicaciones que usan el grupo elástico](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
