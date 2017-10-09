---
title: "Preguntas más frecuentes de base de datos de SQL aaaAzure | Documentos de Microsoft"
description: "Los clientes de preguntas de respuestas toocommon pregunte acerca de las bases de datos en la nube y base de datos de SQL Azure, sistema de administración de bases de datos relacionales (RDBMS) de Microsoft y base de datos como un servicio en nube de Hola."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 1da12abc-0646-43ba-b564-e3b049a6487f
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 02/07/2017
ms.author: sashan;carlrab
ms.openlocfilehash: 04c02f96e6e91cf314221134ee0ef6d24217ef45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-faq"></a>Preguntas más frecuentes sobre la Base de datos SQL

## <a name="what-is-hello-current-version-of-sql-database"></a>¿Qué es la versión actual de Hola de base de datos SQL?
versión actual de Hola de base de datos SQL es V12. Se ha retirado la versión V11.

## <a name="what-is-hello-sla-for-sql-database"></a>¿Qué es Hola SLA para la base de datos SQL?
Por lo menos garantizamos 99,99% de los clientes de tiempo de hello tendrá conectividad entre su Basic simples o flexible, estándar o Premium Microsoft Azure SQL Database y nuestra puerta de enlace de Internet. Para más información, consulte [Acuerdo de Nivel de Servicio](http://azure.microsoft.com/support/legal/sla/).

## <a name="how-do-i-reset-hello-password-for-hello-server-admin"></a>¿Cómo se puede restablecer contraseña Hola Hola, Administrador de servidor?
Hola [portal de Azure](https://portal.azure.com) haga clic en **servidores SQL Server**, seleccione servidor de hello en lista de hello y, a continuación, haga clic en **restablecer contraseña**.

## <a name="how-do-i-manage-databases-and-logins"></a>¿Cómo se administran las bases de datos e inicios de sesión?
Consulte [Administrar bases de datos e inicios de sesión](sql-database-manage-logins.md).

## <a name="how-do-i-make-sure-only-authorized-ip-addresses-are-allowed-tooaccess-a-server"></a>¿Cómo puedo asegurarme de que solo las direcciones IP autorizadas son permiten tooaccess un servidor?
Vea [Configuración del firewall en Base de datos SQL](sql-database-configure-firewall-settings.md).

## <a name="how-does-hello-usage-of-sql-database-show-up-on-my-bill"></a>¿Cómo se muestra el uso de Hola de base de datos de SQL en mi factura?
Facturas de la base de datos SQL en una tarifa por hora predecible en función de nivel de servicio de hello + rendimiento nivel para las bases de datos únicas o Edtu por grupo elástico. El uso real se procesa y se prorratea por horas, por lo que su factura podría mostrar fracciones de una hora. Por ejemplo, si una base de datos existe durante 12 horas al mes, la factura mostrará un uso de 0,5 días. Además, se interrumpen los niveles de servicio y nivel de rendimiento y Edtu por grupo out en hello bill toomake, número de hello toosee más fácil de días de base de datos que usarán para cada uno en un solo mes.

## <a name="what-if-a-single-database-is-active-for-less-than-an-hour-or-uses-a-higher-service-tier-for-less-than-an-hour"></a>¿Qué ocurre si una base de datos única está activa durante menos de una hora o usa un nivel de servicio mayor durante menos de una hora?
Se le facturará para cada hora con que una base de datos existe hello más alto nivel de servicio y rendimiento de nivel se aplica durante esa hora, independientemente del uso o la base de datos de hello estaba activo durante menos de una hora. Por ejemplo, si crea una base de datos única y la elimina a los cinco minutos, se le efectuará un cargo de una hora por usar la base de datos. 

Ejemplos

* Si crea una base de datos básico y, a continuación, actualizar inmediatamente tooStandard S1, se le cobrará a velocidad de S1 estándar de Hola para hello primera hora.
* Si actualiza una base de datos desde tooPremium básica a las 10:00 p.m. y la actualización finaliza a la 1:35 a.m. en hello siguiente día, se le cobrará a velocidad de hello Premium a partir de 1:00 a.m. 
* Si degradar una base de datos Premium tooBasic a las 11:00 a.m. termina a las 2:15 p.m. y, a continuación, base de datos de Hola se aplican cargos en tasa Premium de hello hasta las 3:00 p.m., tras el cual se cobra a velocidades de hello básico.

## <a name="how-does-elastic-pool-usage-show-up-on-my-bill-and-what-happens-when-i-change-edtus-per-pool"></a>¿Cómo se muestra el uso del grupo elástico en la factura y qué ocurre al cambiar a eDTU por grupo?
Grupo elástico gastos mostrar en la factura como Dtu elástica (Edtu) en incrementos de Hola se muestra en Edtu por grupo en [Hola página de precios](https://azure.microsoft.com/pricing/details/sql-database/). No se realizan cargos por base de datos para los grupos elásticos. Se le facturará por cada hora que un grupo existe en la eDTU máxima de hello, independientemente del uso o grupo de hello estaba activo durante menos de una hora. 

Ejemplos

* Si crea un grupo elástico estándar con 200 Edtu a las 11:18 a.m., Agregar grupo de toohello de cinco bases de datos, se le cobra por 200 Edtu hora completa de hello, comenzando en 11 a. m. a través del resto de hello del día de Hola.
* En día 2, 5:05 a.m., 1 de la base de datos empieza a utilizar 50 Edtu y se mantiene constante hasta el día de Hola. Las bases de datos 2 a 5 fluctúan entre 0 y 80 eDTU. Durante el día de hello, agregue cinco otras bases de datos que utilizan distintos Edtu a lo largo del día de Hola. El día 2 es un día completo por el que se facturan 200 eDTU. 
* El día 3, a las 5 a.m. agrega otras 15 bases de datos. Uso de la base de datos aumenta a lo largo de hello día toohello punto que decide tooincrease Edtu de grupo Hola de 200 too400 a las 8:05 p.m. Cargos a nivel de eDTU de hello 200 estaban en vigor hasta 20: 00 horas y aumenta la Edtu too400 para hello restantes cuatro horas. 

## <a name="elastic-pool-billing-and-pricing-information"></a>Información de precios y facturación de grupos elásticos
Grupos elásticos se facturan por hello siguientes características:

* Un grupo elástico se factura tras su creación, incluso cuando no hay ninguna base de datos en bloque de Hola.
* Los grupos elásticos se facturan por horas. Esto es Hola mismo medición frecuencia como para los niveles de rendimiento de las bases de datos únicos.
* Si un grupo elástico es cuyo tamaño ha cambiado tooa nuevo número de Edtu, a continuación, grupo de hello no se cobra según toohello nuevo período de Edtu hasta que se complete Hola cambiar el tamaño de la operación. Esto sigue Hola mismo patrón como cambiar el nivel de rendimiento de Hola de bases de datos únicos.
* precio de Hola de un grupo elástico se basa en el número de Hola de Edtu de grupo de Hola. precio de Hola de un grupo elástico es independiente del número de Hola y el uso de bases de datos elástica Hola dentro de él.
* El precio se calcula por (número de eDTU de grupo) x (precio unitario por eDTU).

Hola de precio de eDTU para un grupo elástico es superior hello DTU precio para una sola base de datos en hello mismo nivel de servicio. Para obtener información detallada, vea [Precios de bases de datos SQL](https://azure.microsoft.com/pricing/details/sql-database/). 

niveles de servicio y Edtu de hello toounderstand, consulte [opciones de base de datos SQL y el rendimiento](sql-database-service-tiers.md).

## <a name="how-does-hello-use-of-active-geo-replication-in-an-elastic-pool-show-up-on-my-bill"></a>¿Cómo usa Hola de replicación geográfica activa en un grupo elástico aparecen en mi factura?
A diferencia de las bases de datos únicas, el uso de [replicación geográfica activa](sql-database-geo-replication-overview.md) con bases de datos elásticas no afecta a la facturación.  Solo se le cobra por Edtu Hola aprovisionados para cada uno de los grupos de hello (grupo primario y secundario)

## <a name="how-does-hello-use-of-hello-auditing-feature-impact-my-bill"></a>¿Cómo hello usa de impacto de la característica de auditoría de hello mi factura?
La auditoría se basa en hello servicio de base de datos SQL sin adicional, costo y es Premium RS, Premium y Standard, tooBasic disponible las bases de datos. Sin embargo, toostore Hola registros de auditoría, Hola auditoría esta función emplea una cuenta de almacenamiento de Azure y las tarifas por tablas y colas de almacenamiento de Azure se aplican en función de tamaño de Hola de su registro de auditoría.

## <a name="how-do-i-find-hello-right-service-tier-and-performance-level-for-single-databases-and-elastic-pools"></a>¿Cómo busco nivel de rendimiento y de nivel de servicio correcto Hola para bases de datos únicas y grupos elásticos?
Hay unos tooyou disponible de herramientas. 

* Bases de datos local, use hello [Asesor de ajuste de tamaño de DTU](http://dtucalculator.azurewebsites.net/) toorecommend Hola bases de datos y Dtu necesarias y evaluar varias bases de datos para grupos elásticos.
* En caso de que una base de datos única se beneficie de estar en un grupo, el motor inteligente de Azure recomienda un grupo elástico si ve un patrón de uso histórico que lo garantiza. Vea [supervisar y administrar un grupo elástico con hello portal de Azure](sql-database-elastic-pool-manage-portal.md). Para obtener más información acerca de cómo toodo Hola matemáticas usted mismo, consulte [consideraciones de precio y el rendimiento para un grupo elástico](sql-database-elastic-pool.md)
* toosee si necesita toodial una sola base de datos hacia arriba o hacia abajo, consulte [Guía de rendimiento para las bases de datos únicos](sql-database-performance-guidance.md).

## <a name="how-often-can-i-change-hello-service-tier-or-performance-level-of-a-single-database"></a>¿Con qué frecuencia se puede cambiar nivel de rendimiento o de servicio de Hola de una sola base de datos?
Puede cambiar el nivel de servicio de hello (entre Basic, Standard, Premium y Premium RS) u Hola nivel de rendimiento dentro de un nivel de servicio (por ejemplo, S1 tooS2) tantas veces como desee. Bases de datos de versiones anteriores, puede cambiar a nivel de rendimiento o de servicio de hello un total de cuatro veces en un período de 24 horas.

## <a name="how-often-can-i-adjust-hello-edtus-per-pool"></a>¿Con qué frecuencia se puede ajustar hello Edtu por grupo?
Tan a menudo como desee.

## <a name="how-long-does-it-take-toochange-hello-service-tier-or-performance-level-of-a-single-database-or-move-a-database-in-and-out-of-an-elastic-pool"></a>¿Durante cuánto tiempo toman toochange Hola servicio nivel de rendimiento o de una sola base de datos o mover una base de datos dentro y fuera de un grupo elástico?
Cambiar el nivel de servicio de Hola de una base de datos y mover de entrada y salida de un grupo requieren hello toobe de base de datos copiado en la plataforma de hello como una operación en segundo plano. Cambiar nivel de servicio de hello puede tardar desde unos minutos tooseveral horas según tamaño Hola de bases de datos de Hola. En ambos casos, las bases de datos de hello permanecen en línea y disponibles durante el movimiento de Hola. Para obtener más información acerca de cómo cambiar las bases de datos únicos, vea [nivel de servicio de Hola de cambio de una base de datos](sql-database-service-tiers.md). 

## <a name="when-should-i-use-a-single-database-vs-elastic-databases"></a>¿Cuándo se deben usar bases de datos elásticas y cuándo una base de datos única?
En general, los grupos elásticos están diseñados para un [patrón de aplicación de software como servicio (SaaS)](sql-database-design-patterns-multi-tenancy-saas-applications.md) típico, donde hay una base de datos por cliente o inquilino. Compras de bases de datos individuales y variable de hello toomeet en exceso y una memoria máxima demanda de cada base de datos a menudo no es rentable será. Con los grupos, administrar el rendimiento colectivo Hola de grupo de Hola y las bases de datos de Hola escalar hacia arriba y abajo automáticamente. El motor inteligente de Azure recomendará un grupo para las bases de datos si un patrón de uso lo garantiza. Para más información, consulte la [guía de grupos elásticos](sql-database-elastic-pool.md).

## <a name="what-does-it-mean-toohave-up-too200-of-your-maximum-provisioned-database-storage-for-backup-storage"></a>¿Qué significa toohave too200% de su almacenamiento de base de datos aprovisionado máximo para el almacenamiento de copia de seguridad?
Almacenamiento de copia de seguridad es almacenamiento Hola asociado con las copias de seguridad automatizadas de la base de datos que se usan para [punto-de--restauración a un momento](sql-database-recovery-using-backups.md#point-in-time-restore) y [georestauración](sql-database-recovery-using-backups.md#geo-restore). Base de datos de SQL de Microsoft Azure proporciona too200% de su almacenamiento de base de datos aprovisionado máximo de almacenamiento de copia de seguridad sin costo adicional alguno. Por ejemplo, si tiene una instancia de base de datos de tipo Estándar con un tamaño de base de datos aprovisionado de 250 GB, se le proporcionarán 500 GB para almacenar sus copias de seguridad sin coste adicional. Si la base de datos supera Hola proporcionada almacenamiento de copia de seguridad, puede elegir período de retención de hello tooreduce póngase en contacto con soporte técnico de Azure o paga por el almacenamiento de copia de seguridad extra de hello facturará de acuerdo con la tasa de almacenamiento geográficamente redundante con acceso de lectura (RA-GRS) estándar. Para obtener más información sobre la facturación RA-GRS, consulte los Detalles de los precios de almacenamiento.

## <a name="im-moving-from-webbusiness-toohello-new-service-tiers-what-do-i-need-tooknow"></a>Traslado de Web/Business toohello nuevos niveles de servicio, ¿qué necesito tooknow?
Las bases de datos Web y Business de Azure se han retirado. niveles de Basic, Standard, Premium, RS Premium y flexible de Hello reemplazan Hola retirar las bases de datos Web y Business. 

## <a name="what-is-an-expected-replication-lag-when-geo-replicating-a-database-between-two-regions-within-hello-same-azure-geography"></a>¿Qué es un intervalo de replicación esperado cuando la replicación geográfica una base de datos entre dos regiones dentro de Hola igual geography Azure?
Se actualmente estamos soporta un RPO de cinco segundos y retrasos de la replicación de hello ha sido menor que cuando Hola geográfica secundarias se hospedan en hello que Azure recomienda región emparejada y hello en el mismo nivel de servicio.

## <a name="what-is-an-expected-replication-lag-when-geo-secondary-is-created-in-hello-same-region-as-hello-primary-database"></a>¿Qué es un retardo de replicación esperado cuando geográfica secundaria se crea en Hola mismo región como base de datos principal de hello?
Basado en datos empíricas, no hay demasiada diferencia entre intra-region y retraso en la replicación entre región cuando se usa hello que Azure recomienda región emparejada. 

## <a name="if-there-is-a-network-failure-between-two-regions-how-does-hello-retry-logic-work-when-geo-replication-is-set-up"></a>¿Si se produce un error de red entre dos regiones, la lógica de reintento de hello funciona cuando se configura la replicación geográfica?
Si se produce una desconexión, se vuelva a intentar cada 10 segundos toore-establecer conexiones.

## <a name="what-can-i-do-tooguarantee-that-a-critical-change-on-hello-primary-database-is-replicated"></a>¿Qué puedo hacer tooguarantee que se replica un cambio crítico en la base de datos principal de hello?
Hola geográfica-base de datos secundaria es una réplica async y no intentamos tookeep en sincronización completa con hello principal. Pero se proporciona una replicación de Hola de tooensure de método tooforce sincronización de cambios importantes (por ejemplo, las actualizaciones de contraseña). Sincronización forzada afecta al rendimiento porque se bloquea el subproceso que realiza la llamada de hello hasta que se replican todas las transacciones confirmadas. Para más información, consulte [sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx). 

## <a name="what-tools-are-available-toomonitor-hello-replication-lag-between-hello-primary-database-and-geo-secondary"></a>¿Qué herramientas están disponibles toomonitor Hola intervalo de replicación entre la base de datos principal de Hola y de replicación geográfica secundaria?
Se exponen los retrasos de replicación en tiempo real de hello entre la base de datos principal de Hola y geográfica secundarias a través de una DMV. Para más información, consulte [sys.dm_geo_replication_link_status](https://msdn.microsoft.com/library/mt575504.aspx).

## <a name="toomove-a-database-tooa-different-server-in-hello-same-subscription"></a>un servidor diferente de tooa de base de datos en hello toomove misma suscripción
* Hola [portal de Azure](https://portal.azure.com), haga clic en **bases de datos SQL**, seleccione una base de datos de lista de hello y, a continuación, haga clic en **copia**. Para más información, consulte [Copia de una Base de datos SQL de Azure](sql-database-copy.md) .

## <a name="toomove-a-database-between-subscriptions"></a>toomove una base de datos entre las suscripciones
* Hola [portal de Azure](https://portal.azure.com), haga clic en **servidores SQL Server** y, a continuación, seleccione servidor de Hola que hospeda la base de datos de lista de Hola. Haga clic en **mover**y, a continuación, seleccione toomove de recursos de Hola y Hola toomove de suscripción a.
