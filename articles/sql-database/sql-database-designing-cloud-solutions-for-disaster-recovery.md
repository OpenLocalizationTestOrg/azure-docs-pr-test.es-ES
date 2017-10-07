---
title: servicio de alta disponibilidad aaaDesign con la base de datos de SQL de Azure | Documentos de Microsoft
description: "Obtenga información sobre el diseño de aplicaciones para servicios de alta disponibilidad con Azure SQL Database."
keywords: "recuperación ante desastres en la nube, soluciones de recuperación ante desastres, copia de seguridad de datos de aplicación, planificación de continuidad del negocio"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: e8a346ac-dd08-41e7-9685-46cebca04582
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 04/21/2017
ms.author: sashan
ms.openlocfilehash: 815f754ba7014cd8a1108a2d84c2a8f71d7030a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="designing-highly-available-services-using-azure-sql-database"></a>Diseño de servicios de alta disponibilidad con Azure SQL Database

Al compilar e implementar servicios de alta disponibilidad en la base de datos de SQL Azure, use [conmutación por error de grupos y la replicación geográfica activa](sql-database-geo-replication-overview.md) tooregional errores de tooprovide resistencia e interrupciones graves y habilitar recuperación rápida toohello bases de datos secundarias. En este artículo se centra en los patrones de aplicación comunes y se describen las ventajas de Hola y ventajas y desventajas de cada opción según los requisitos de la implementación de la aplicación hello, los acuerdo de nivel de servicio de hello tiene como destino, la latencia de tráfico y los costos. Para saber cómo utilizar la replicación geográfica activa con los grupos elásticos, consulte [Estrategias de recuperación ante desastres para aplicaciones que usan el grupo elástico de Base de datos SQL](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).

## <a name="design-pattern-1-active-passive-deployment-for-cloud-disaster-recovery-with-a-co-located-database"></a>Patrón de diseño 1: implementación activa-pasiva para la recuperación ante desastres en la nube con una base de datos colocada
Esta opción es ideal para las aplicaciones con hello siguientes características:

* Instancia activa de una única región de Azure.
* Dependencia fuerte en toodata de acceso de lectura y escritura (RW)
* No es aceptable debido costo toolatency y el tráfico entre regiones conectividad entre la aplicación web de Hola y de base de datos de Hola    

En este caso, la topología de implementación de aplicación Hola está optimizada para administrar desastres regionales cuando todos los componentes de la aplicación están teniendo problemas y necesitan toofailover como una unidad. Para la redundancia geográfica, base de datos de Hola y lógica de la aplicación hello son tooanother replicada región pero no se usan para la carga de trabajo de aplicación de hello en condiciones normales de Hola. aplicación de Hello en la región secundaria Hola debería ser toouse configurado SQL conexión cadena toohello base de datos secundaria. El Administrador de tráfico está configurado toouse [método de enrutamiento de conmutación por error](../traffic-manager/traffic-manager-configure-failover-routing-method.md).  

> [!NOTE]
> [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) se usa en este artículo únicamente con fines ilustrativos. Puede usar cualquier solución de equilibrio de carga que admita el método de enrutamiento de conmutación por error.    
>

Hola siguiente diagrama ilustra esta configuración antes de una interrupción.

![Configuración de replicación geográfica de SQL Database. Recuperación ante desastres en la nube.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-1.png)

Después de una interrupción en la región principal de hello, servicio de base de datos SQL de hello detecta esa base de datos principal de hello no es accesible y desencadenar una conmutación por error toohello base de datos secundaria según los parámetros de Hola de directiva de conmutación por error automática de Hola. Dependiendo de su SLA de la aplicación, puede decidir tooconfigure un período de gracia entre la detección de Hola de interrupción de Hola y conmutación por error de hello propio. Configuración de un período de gracia reduce el riesgo de Hola de casos de toohello de pérdida de datos donde interrupción hello es grave y disponibilidad en la región de hello no se puede restaurar rápidamente. Si conmutación por error de punto de conexión de Hola se inicia mediante el Administrador de tráfico Hola antes de desencadenadores de grupo de conmutación por error de Hola Hola conmutación por error de base de datos de hello, aplicación web de hello no es base de datos pueda tooreconnect toohello. tooreconnect de intento de la aplicación Hello supera automáticamente tan pronto como finaliza la conmutación por error de base de datos de Hola. 

> [!NOTE]
> tooachieve totalmente había coordinada conmutación por error de la aplicación hello y bases de datos de hello, debe diseñar su propio método de supervisión y usar la conmutación por error manual de los extremos de la aplicación hello web y bases de datos de Hola.
>

Una vez completada la conmutación por error de saludo de la aplicación hello extremos y base de datos de hello, aplicación hello iniciará volver a procesar las solicitudes de usuario de hello en la región de hello B y permanecerá coexisten con base de datos de hello porque la base de datos principal de hello ahora está en región de B. Este escenario se muestra en hello siguiente diagrama. En todos los diagramas, las líneas continuas indican conexiones activas, las líneas de puntos indican conexiones suspendidas y las señales de detención indican desencadenadores de acción.

![Replicación geográfica: Base de datos conmutación por error toosecondary. Copia de seguridad de datos de la aplicación.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-2.png)

Si se produce una interrupción en la región secundaria de hello, se suspende Hola vínculo de replicación entre Hola principal y la base de datos secundaria de hello pero Hola conmutación por error no se desencadena porque no se ve afectada la base de datos principal de Hola. no se cambia en este caso, la disponibilidad de la aplicación Hello pero aplicación hello funciona expuesto y, por tanto, en un riesgo más alto en el caso de ambas regiones producirá un error en sucesión.

> [!NOTE]
> Recuperación ante desastres se recomienda la configuración de hello con regiones de tootwo limitado de implementación de aplicación. Se trata porque la mayoría de hello regiones geográficas de Azure tienen solo dos regiones. Esta configuración no protegerá la aplicación de un error grave simultáneo de ambas regiones.  En el caso poco probable de que este error se produjese, podría recuperar sus bases de datos en una tercera región mediante una [operación de restauración geográfica](sql-database-disaster-recovery.md#recover-using-geo-restore).
>

Una vez que se mitiga interrupción hello, base de datos secundaria de hello volver a sincronizará automáticamente con hello principal. Durante la sincronización, rendimiento de hello principal podría verse afectada ligeramente según cantidad Hola de datos que necesita toobe sincronizado. Hello diagrama siguiente ilustra una interrupción en la región secundaria Hola.

![Base de datos secundaria sincronizada con la primaria. Recuperación ante desastres en la nube.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-3.png)

clave de Hello **ventajas** de este patrón de diseño son:

* Hola misma aplicación web es regiones tooboth implementado sin ninguna configuración específica de la región y sin conmutación por error de lógica adicional tooreact toohello. 
* rendimiento de la aplicación Hello no se ve afectado por la conmutación por error como aplicación web de Hola y base de datos de hello siempre se ubican conjuntamente.

Hola principal **contrapartida** es que aplicación de redundancia de hello instancia en la región secundaria Hola solo se utiliza para la recuperación ante desastres.

## <a name="design-pattern-2-active-active-deployment-for-application-load-balancing"></a>Patrón de diseño 2: implementación activa-activa para el equilibrio de carga de aplicación
Esta opción de recuperación ante desastres en la nube es ideal en las aplicaciones con hello siguientes características:

* Proporción alta de base de datos lee toowrites
* Base de datos de latencia de lectura es más importante para la experiencia del usuario final de Hola que la latencia de escritura Hola 
* La lógica de solo lectura se puede separar de la lógica de lectura y escritura mediante el uso de una cadena de conexión distinta.
* Lógica de solo lectura no dependen de datos completa que se sincronizan con las últimas actualizaciones de Hola  

Si las aplicaciones tienen estas características, puede mejorar sustancialmente el equilibrio de carga las conexiones de usuario final de hello entre varias instancias de aplicación en diferentes regiones Hola general experiencia del usuario final. Dos de las regiones de hello deben seleccionarse como Hola par de recuperación ante desastres y grupo de conmutación por error de hello debe incluir las bases de datos de hello en estas regiones. tooimplement equilibrio de carga, cada región debe tener una instancia activa de la aplicación hello con hello lectura y escritura (RW) lógica conectada toohello agente de escucha de lectura y escritura punto de conexión del grupo de conmutación por error de Hola. Se garantizará que Hola de conmutación por error se iniciará automáticamente si la base de datos principal de Hola se ve afectado por una interrupción del servicio. Hola de solo lectura lógica (RO) en la aplicación web de hello debe conectarse directamente toohello base de datos en dicha región. El Administrador de tráfico se debe configurar toouse [rendimiento enrutamiento](../traffic-manager/traffic-manager-configure-performance-routing-method.md) con [supervisión de extremo](../traffic-manager/traffic-manager-monitoring.md) habilitado para cada instancia de la aplicación.

Como en el patrón nº 1, debe considerar la posibilidad de implementar una aplicación de supervisión similar. Pero a diferencia de patrón #1, Hola supervisión de la aplicación no será responsable de activar la conmutación por error de hello extremo.

> [!NOTE]
> Aunque este patrón utiliza más de una base de datos secundaria, solo Hola secundaria en la región B se utilizarían para conmutación por error y debe formar parte del grupo de conmutación por error de Hola.
>

El Administrador de tráfico debe configurarse para la ubicación geográfica del rendimiento enrutamiento toodirect Hola usuario conexiones toohello instancia más cercano toohello de usuarios de aplicación. Hola siguiente diagrama ilustra esta configuración antes de una interrupción.

![Ninguna interrupción: aplicación de toonearest enrutamiento de rendimiento. Replicación geográfica.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-1.png)

Si se detecta una interrupción de la base de datos en una región de hello, grupo de conmutación por error de hello iniciará automáticamente conmutación por error de base de datos principal de hello en la región A toohello secundaria en la región de B. Se actualizará automáticamente también tooregion de punto de conexión de agente de escucha de lectura y escritura de hello B para que las conexiones de lectura y escritura en la aplicación web de hello no se verá afectadas. Administrador de tráfico de Hello, excluirá el extremo sin conexión Hola de tabla de enrutamiento de hello pero seguirá enrutamiento hello para el usuario final tráfico toohello restantes instancias en línea. Hello las cadenas de conexión de SQL de solo lectura no se verán afectadas como señalan siempre la base de datos de toohello Hola misma región. 

Hola siguiente diagrama muestra la configuración nuevo de hello después Hola conmutación por error.

![Configuración después de la conmutación por error. Recuperación ante desastres en la nube.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-2.png)

En caso de una interrupción en una de las regiones secundaria Hola, Administrador de tráfico de Hola quitará automáticamente extremo sin conexión de hello en dicha región de tabla de enrutamiento de Hola. se suspenderá Hola replicación canal toohello base de datos secundaria en dicha región. Porque regiones restantes Hola obtener tráfico de usuario adicionales en este escenario, se verá afectado el rendimiento de la aplicación hello durante la interrupción de Hola. Una vez que se mitiga interrupción hello, hello base de datos secundaria en la región afectada Hola inmediatamente sincronizarán con hello principal. Durante el saludo rendimiento de la sincronización de hello principal podría verse afectada ligeramente según cantidad Hola de datos que necesita toobe sincronizado. Hola siguiente diagrama ilustra una interrupción en la región de B.

![Interrupción en la región secundaria. Recuperación ante desastres en la nube: replicación geográfica.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-3.png)

clave de Hello **ventaja** de diseño de este patrón es que puede escalar la carga de trabajo de aplicación Hola a través de rendimiento de varios elementos secundarios tooachieve Hola óptimo para el usuario final. Hola **compensaciones** de esta opción son:

* Conexiones de lectura / escritura entre instancias de la aplicación hello y base de datos tienen distintos latencia y costo
* Rendimiento de la aplicación se ve afectado durante la interrupción de Hola

> [!NOTE]
> Puede usar un enfoque similar toooffload especializado las cargas de trabajo como los informes de trabajos, herramientas de inteligencia empresarial o las copias de seguridad. Normalmente, estas cargas de trabajo consumen recursos significativos de la base de datos, por tanto, se recomienda designar uno de Hola bases de datos secundarias para ellos con carga de trabajo prevista de hello rendimiento nivel toohello coincidente.
>

## <a name="design-pattern-3-active-passive-deployment-for-data-preservation"></a>Patrón de diseño 3: implementación activa-pasiva para la conservación de datos
Esta opción es ideal para las aplicaciones con hello siguientes características:

* Cualquier pérdida de datos supone un alto riesgo para la empresa. conmutación por error de base de datos de Hello solo puede usarse como último recurso si interrupción hello es grave.
* aplicación Hello admite los modos de solo lectura y lectura / escritura de operaciones y puede funcionar en "modo de solo lectura" durante un período de tiempo.

En este modelo, aplicación hello cambia el modo de sólo tooread cuando las conexiones de lectura / escritura de hello empiece a obtener errores de tiempo de espera. Hola aplicación Web está implementada tooboth regiones e incluyen un punto de conexión de agente de escucha de lectura y escritura de toohello de conexión y el punto de conexión de una conexión distinta toohello del agente de escucha de solo lectura. el Administrador de tráfico Hola se debe configurar toouse [enrutamiento de conmutación por error](../traffic-manager/traffic-manager-configure-failover-routing-method.md) con [supervisión de extremo](../traffic-manager/traffic-manager-monitoring.md) habilitada para el extremo de la aplicación hello en cada región.

Hola siguiente diagrama ilustra esta configuración antes de una interrupción.

![Implementación activa-pasiva antes de la conmutación por error. Recuperación ante desastres en la nube.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-1.png)

Cuando el Administrador de tráfico Hola detecta un tooregion de error de conectividad A, cambia automáticamente la instancia de aplicación de usuario tráfico toohello en la región de B. Con este modelo, es importante establecer período de gracia de hello con valor suficientemente alto de datos pérdida tooa, por ejemplo, 24 horas. Se asegurará de que se evita la pérdida de datos si se mitiga la interrupción de Hola durante este periodo. Cuando se activa hello las aplicaciones Web de región de hello B las operaciones de lectura y escritura de hello empiezan a generar errores. En ese momento, debe cambiar el modo de solo lectura de toohello. En este Hola modo solicitudes será toohello enrutado automáticamente la base de datos secundaria. En caso de hello del programa Hola a un error catastrófico interrupción no se pueden mitigar dentro del período de gracia de Hola y grupo de conmutación por error de hello desencadenará Hola conmutación por error. Después de ese Hola estará disponible el agente de escucha de lectura y escritura y Hola llamadas tooit se detendrá por error. Hola siguiente diagrama se ilustra.

![Interrupción: aplicación en modo de sólo lectura. Recuperación ante desastres en la nube.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-2.png)

Si se mitiga una interrupción de hello en la región principal de hello en período de gracia de hello, traffic manager detecta restauración Hola de conectividad en la región principal de Hola y activa la instancia de aplicación de usuario tráfico toohello atrás en la región A. Esa instancia de la aplicación se reanuda y funciona en modo de lectura y escritura en base de datos principal de hello región A.

En el caso de una interrupción en la región de hello B, Administrador de tráfico de hello detecta el error de hello del extremo de aplicación hello en la región B y el grupo de conmutación por error Hola conmutadores Hola del agente de escucha de solo lectura tooregion A. Esta interrupción no afecta a la experiencia del usuario final de hello pero se expondrá la base de datos principal de Hola durante la interrupción de Hola. Hola siguiente diagrama se ilustra.

![Interrupción: base de datos secundaria. Recuperación ante desastres en la nube.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-3.png)

Una vez que se mitiga interrupción hello, hello base de datos secundaria se sincronice inmediatamente con hello principal y agente de escucha de solo lectura de hello es conmutada toohello back-base de datos secundaria en la región de B. Durante la sincronización de rendimiento de hello principal podría verse afectada ligeramente según cantidad Hola de datos que necesita toobe sincronizado.

Este patrón de diseño tiene varias **ventajas**:

* Evita la pérdida de datos durante las interrupciones temporales de Hola.
* Tiempo de inactividad depende solo de la velocidad de traffic manager detecta errores de conectividad de hello, lo que es configurable.

Hola **contrapartida** es:

* Aplicación debe ser capaz de toooperate en modo de solo lectura.

> [!NOTE]
> En el caso de una interrupción del servicio permanente en la región de hello, manualmente activar la conmutación por error de base de datos y Aceptar Hola pérdida de datos. aplicación Hello será funcional en la región secundaria de hello con base de datos de toohello de acceso de lectura y escritura.
>

## <a name="business-continuity-planning-choose-an-application-design-for-cloud-disaster-recovery"></a>Planificación de continuidad del negocio: elección del diseño de una aplicación para la recuperación ante desastres en la nube
La estrategia de recuperación ante desastres de nube específica puede combinar o ampliar estos patrones de diseño necesidades de hello cumple toobest de la aplicación.  Como se mencionó anteriormente, estrategia de Hola que elija se basa en hello SLA desee a toooffer tooyour clientes y Hola topología de implementación de aplicación. toohelp guiar la decisión, hello en la tabla siguiente compara las opciones de hello basándose en datos estimada de hello pérdida o recuperación objetivos de punto (RPO) y el tiempo de recuperación estimado (ERT).

| Patrón | RPO | ERT |
|:--- |:--- |:--- |
| Implementación activa-pasiva para la recuperación ante desastres con acceso a base de datos colocalizada |Acceso de lectura y escritura < 5 s |Tiempo de detección de errores + TTL de DNS |
| Implementación activa-activa para el equilibrio de carga de aplicación |Acceso de lectura y escritura < 5 s |Tiempo de detección de errores + TTL de DNS |
| Implementación activa-pasiva para la conservación de datos |Acceso de solo lectura < 5 s | Acceso de solo lectura = 0 |
||Acceso de lectura y escritura = cero | Acceso de lectura y escritura = Tiempo de detección de errores + Período de gracia con pérdida de datos |
|||

## <a name="next-steps"></a>Pasos siguientes
* toolearn acerca de las copias de seguridad de base de datos de SQL de Azure automatizada, vea [copias de seguridad automáticas de base de datos SQL](sql-database-automated-backups.md)
* Para obtener una descripción general y los escenarios de la continuidad empresarial, consulte [Continuidad empresarial con Base de datos SQL de Azure](sql-database-business-continuity.md)
* toolearn sobre el uso de copias de seguridad automatizadas para la recuperación, vea [restaurar una base de datos de copias de seguridad de hello iniciadas por el servicio](sql-database-recovery-using-backups.md)
* toolearn acerca de las opciones de recuperación más rápidos, consulte [replicación geográfica activa](sql-database-geo-replication-overview.md)  
* toolearn sobre el uso de copias de seguridad automatizadas para el archivado, vea [copiar base de datos](sql-database-copy.md)
* Para saber cómo utilizar la replicación geográfica activa con los grupos elásticos, consulte [Estrategias de recuperación ante desastres para aplicaciones que usan el grupo elástico de Base de datos SQL](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
