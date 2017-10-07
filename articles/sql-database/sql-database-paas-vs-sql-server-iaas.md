---
title: "aaaSQL (PaaS) frente a base de datos. SQL Server en la nube de hello en máquinas virtuales (IaaS) | Documentos de Microsoft"
description: "Obtenga información acerca de qué opción de SQL Server en la nube se adapte a su aplicación: base de datos SQL de Azure (PaaS) o SQL Server en la nube de hello en máquinas virtuales de Azure."
services: sql-database, virtual-machines
keywords: Nube de SQL Server, SQL Server en la nube de hello, base de datos de PaaS, SQL Server, DBaaS en la nube
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: cjgronlund
ms.assetid: 7467f422-b77d-4b60-9cb5-0f1ec17ec565
ms.service: sql-database
ms.custom: DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: carlrab
ms.openlocfilehash: 1b462a9a822d04dc5deb8422ed505a5d09279253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="choose-a-cloud-sql-server-option-azure-sql-paas-database-or-sql-server-on-azure-vms-iaas"></a>Selección de una opción de SQL Server en la nube: Base de datos (PaaS) SQL de Azure o SQL Server en máquinas virtuales de Azure (IaaS)
Azure proporciona dos opciones para el hospedaje de las cargas de trabajo de SQL Server en Microsoft Azure:

* [La base de datos de SQL Azure](https://azure.microsoft.com/services/sql-database/): SQL de una base de datos toohello nativo en la nube, también conocido como una plataforma como una base de datos de servicio (PaaS) o una base de datos como un servicio (DBaaS) que está optimizado para el desarrollo de aplicaciones de software como servicio (SaaS). Ofrece compatibilidad con la mayoría de las características de SQL Server. Para más información acerca de PaaS, consulte [¿Qué es PaaS?](https://azure.microsoft.com/overview/what-is-paas/).
* [SQL Server en máquinas virtuales Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/): SQL Server instalado y hospedada en nube de hello máquinas virtuales en Windows Server (VM) que ejecuta en Azure, también conocido como una infraestructura como servicio (IaaS).
  SQL Server en máquinas virtuales de Azure está optimizado para migrar aplicaciones existentes de SQL Server. Hola a todas las versiones y ediciones de SQL Server están disponibles. Ofrece compatibilidad del 100% con SQL Server, lo cual permite un toohost tantas bases de datos necesarias y se ejecutan transacciones entre bases de datos. Ofrece un control total sobre SQL Server y Windows.

Obtenga información acerca de cómo cada opción se adapta a la plataforma de datos de Microsoft de Hola y obtener ayuda coincidente Hola opción derecho tooyour los requisitos empresariales. Si se da prioridad a ahorros de costo o muy poca administración por delante de todo lo demás, en este artículo puede ayudarle a decidir qué método se entrega con los requisitos de negocios de Hola que considere más relevante.

## <a name="microsofts-data-platform"></a>Plataforma de datos de Microsoft
Uno de hello primera cosas toounderstand en cualquier descripción de Azure frente a bases de datos de SQL Server local es que puede usar todo. La plataforma de datos de Microsoft aprovecha la tecnología de SQL Server y la pone a disposición de los usuarios en máquinas físicas locales, entornos en nubes privadas, entornos en nubes privadas hospedados por terceros y la nube pública. SQL Server en máquinas virtuales de Azure permite toomeet las necesidades del negocio únicos y distintos a través de una combinación de local y las implementaciones hospedados en la nube, mientras utilizando Hola el mismo conjunto de productos de servidor, herramientas de desarrollo y experiencia a través de estas entornos.

   ![Opciones de SQL Server en la nube: base de datos de SQL server en IaaS o SaaS SQL en la nube de Hola.](./media/sql-database-paas-vs-sql-server-iaas/SQLIAAS_SQL_Server_Cloud_Continuum.png)

Tal como se muestra en el diagrama de hello, cada oferta se puede clasificar por nivel de Hola de administración que tienen sobre infraestructura de hello (en el eje de hello X) y por el grado de Hola de eficacia de costos que se logra mediante la consolidación de nivel de base de datos y automatización (en el eje de Hola Y).

Al diseñar una aplicación, están disponibles para hospedar la parte de SQL Server de Hola de aplicación hello cuatro opciones básicas:

* SQL Server en máquinas físicas no virtualizadas
* SQL Server en máquinas locales virtualizadas (nube privada)
* SQL Server en máquinas virtuales de Azure (nube pública de Microsoft)
* Base de datos SQL de Azure (nube pública de Microsoft)

Hola siguientes secciones, aprenderá acerca de SQL Server en hello nube pública de Microsoft: base de datos de SQL Azure y SQL Server en máquinas virtuales de Azure. Además, explorará factores de motivación comunes del negocio para determinar la opción que mejor funciona para su aplicación.

## <a name="a-closer-look-at-azure-sql-database-and-sql-server-on-azure-vms"></a>Base de datos SQL de Azure y SQL Server en Máquinas virtuales de Azure en detalle
**La base de datos de SQL Azure** es un relacional base de datos-como-servicio (DBaaS) hospedado en hello Azure en la nube que se divide en categorías de sector de Hola de *Software como-servicio (SaaS)* y *plataforma como servicio (PaaS)* . [Base de datos SQL](sql-database-technical-overview.md) se compila en hardware y software estandarizados que Microsoft posee, hospeda y mantiene. Con la base de datos de SQL, puede desarrollar directamente en servicio de hello utilizando características integradas y funciones. Cuando se usa la base de datos de SQL, que pago por uso con opciones tooscale vertical u horizontalmente para mayor potencia de se produzca ninguna interrupción.

**SQL Server en máquinas virtuales de Azure (VM)** entra en la categoría del sector hello *infraestructura como-servicio (IaaS)* y le permite toorun SQL Server en una máquina virtual en la nube de Hola. Base de datos de tooSQL similar, se basa en hardware estandarizado que posee, hospedado y mantenido por Microsoft. Cuando se usa SQL Server en una máquina virtual, puede usar la licencia de pago por uso de SQL Server ya incluida en una imagen de SQL Server o usar fácilmente una licencia existente. También puede hacer fácilmente Hola escala-arriba/abajo y pausar y reanudar máquinas virtuales según sea necesario.

Por lo general, estas dos opciones SQL se optimizan con diferentes fines:

* **La base de datos de SQL Azure** es tooreduce optimizado los costes generales toohello mínimo para aprovisionar y administrar muchas bases de datos. Reduce los costos de administración en curso porque no tiene toomanage las máquinas virtuales, el sistema operativo o el software de base de datos. No tiene actualizaciones toomanage, alta disponibilidad, o [copias de seguridad](sql-database-automated-backups.md). En general, base de datos de SQL Azure pueden aumentar drásticamente el número de Hola de bases de datos administradas por un único TI o recursos de desarrollo.
* **SQL Server que se ejecutan en máquinas virtuales de Azure** está optimizado para migrar existente tooAzure de aplicaciones o extender local existente en la nube aplicaciones toohello en las implementaciones híbridas. Además, puede usar SQL Server en una máquina virtual toodevelop y probar las aplicaciones tradicionales de SQL Server. Con SQL Server en máquinas virtuales de Azure, tendrá derechos administrativos completos de Hola a través de una instancia dedicada de SQL Server y una máquina virtual basada en la nube. Es una opción perfecta cuando una organización ya tiene máquinas virtuales de TI recursos disponibles toomaintain Hola. Estas capacidades permiten toobuild un tooaddress sistema altamente personalizados específicos de rendimiento y requisitos de disponibilidad de la aplicación.

Hello en la tabla siguiente resume las principales características de Hola de base de datos SQL y SQL Server en máquinas virtuales de Azure:

| **Más adecuado para:** | **Azure SQL Database** | **SQL Server en una máquina virtual de Azure** |
| --- | --- | --- |
|  |Nuevas aplicaciones diseñadas para la nube que tienen restricciones de tiempo en desarrollo y marketing. |Aplicaciones existentes que requieren la nube de toohello de migración rápida con cambios mínimos. Desarrollar y probar escenarios de rápido si no desea hardware de SQL Server de toobuy local no sea de producción. |
|  | Equipos que necesitan alta disponibilidad integrada, recuperación ante desastres y actualización de base de datos de Hola. |Equipos que puedan configurar y administrar alta disponibilidad, recuperación ante desastres y aplicación de revisiones para SQL Server. Algunas funciones automatizadas ya incorporadas simplifican considerablemente estos aspectos. | |
|  | Equipos que no desea que sistema de operativo toomanage Hola subyacente y la configuración. |Necesita un entorno personalizado con derechos administrativos completos. | |
|  | Bases de datos de hasta too4 TB o bases de datos mayores que pueden ser [horizontal o verticalmente particiones](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling) utilizando un modelo de escalabilidad horizontal. |Instancias de SQL Server con hasta too64 TB de almacenamiento. instancia de Hello puede admitir todas las bases de datos según sea necesario. | |
|  | [Compilación de aplicaciones de software como servicio (SaaS)](sql-database-design-patterns-multi-tenancy-saas-applications.md). |Migración y creación de aplicaciones empresariales e híbridas. | |
|  | | |
| **Recursos:** |No desea tooemploy TI recursos para la configuración y administración de hello subyacente de infraestructura, pero desea toofocus de capa de aplicación Hola. |Tiene algunos recursos de TI para la configuración y administración. Algunas funciones automatizadas ya incorporadas simplifican considerablemente estos aspectos. |
| **Costo total de propiedad:** |Elimina los costos de hardware y reduce los costos administrativos. |Elimina costes de hardware. |
| **Continuidad del negocio:** |Capacidades de infraestructura de tolerancia de error toobuilt en suma, base de datos de SQL Azure proporciona características, como [copias de seguridad automáticas](sql-database-automated-backups.md), [punto-In-Time restauración](sql-database-recovery-using-backups.md#point-in-time-restore), [larestauracióngeográfica](sql-database-recovery-using-backups.md#geo-restore), y [replicación geográfica activa](sql-database-geo-replication-overview.md) tooincrease la continuidad del negocio. Para más información, consulte [Información general: continuidad del negocio en la nube y recuperación ante desastres con la Base de datos SQL](sql-database-business-continuity.md). |SQL Server en máquinas virtuales de Azure permite configurar una solución de recuperación ante desastres y alta disponibilidad para las necesidades específicas de su base de datos. Por consiguiente, podrá tener un sistema altamente optimizado para la aplicación. Podrá probar y ejecutar conmutaciones por error cuando sea necesario. Para más información, consulte [Alta disponibilidad y recuperación ante desastres para SQL Server en máquinas virtuales de Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md). |
| **Nube híbrida:** |La aplicación local puede obtener acceso a datos de Base de datos de SQL de Azure. |Con SQL Server en máquinas virtuales de Azure, pueden tener las aplicaciones que se ejecutan en parte en nube de Hola y en parte en local. Por ejemplo, puede ampliar su red local y la nube de toohello de dominio de Active Directory a través de [red Virtual de Azure](../virtual-network/virtual-networks-overview.md). Además, se pueden almacenar archivos de datos locales en Almacenamiento de Azure con [Archivos de datos de SQL Server en Azure](http://msdn.microsoft.com/library/dn385720.aspx). Para obtener más información, consulte [tooSQL Introducción nube híbrida de 2014 de servidor](http://msdn.microsoft.com/library/dn606154.aspx). |
|  | Admite [replicación transaccional de SQL Server](https://msdn.microsoft.com/library/mt589530.aspx) como tooreplicate de datos de suscriptor. |Es totalmente compatible con [replicación transaccional de SQL Server](https://msdn.microsoft.com/library/mt589530.aspx), [grupos de disponibilidad AlwaysOn](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md), Integration Services y el trasvase de registros de datos de tooreplicate. Además, las copias de seguridad de SQL Server tradicionales son totalmente compatibles. | |
|  | | |

## <a name="business-motivations-for-choosing-azure-sql-database-or-sql-server-on-azure-vms"></a>Motivaciones empresariales al elegir Base de datos SQL de Azure o SQL Server en Máquinas virtuales de Azure
### <a name="cost"></a>Coste
Si es un inicio que sujetó para efectivo o un equipo de una compañía establecida que opera en estrecha las restricciones de presupuesto, limitadas financiación suele ser controlador principal de hello al decidir cómo toohost las bases de datos. En esta sección, aprenderá sobre la facturación de Hola y licencias de conceptos básicos de Azure con lo que respecta a dos opciones de base de datos relacional toothese: base de datos SQL y SQL Server en máquinas virtuales de Azure. También aprenderá acerca de cómo calcular el costo de la aplicación total de Hola.

#### <a name="billing-and-licensing-basics"></a>Conceptos básicos sobre facturación y licencias
**Base de datos de SQL** se vende toocustomers como un servicio, no con una licencia.  [SQL Server en máquinas virtuales de Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md) se vende con una licencia incluida que se paga por minutos. Si ya tiene una licencia, puede usarla también.  

Actualmente, **base de datos SQL** está disponible en varios niveles de servicio, todos ellos se facturan por horas en una tarifa fija basada en hello servicio nivel y rendimiento que elija. Además, se le facturará el tráfico saliente de Internet en las [tasas de transferencia de datos](https://azure.microsoft.com/pricing/details/data-transfers/)habituales. Hola Basic, Standard y Premium y servicio Premium RS niveles están diseñados toodeliver un rendimiento predecible con varios toomatch de niveles de rendimiento requisitos de máxima de la aplicación. Puede cambiar entre niveles de servicio y toomatch de niveles de rendimiento que necesidades de rendimiento de diversos de su aplicación. Si la base de datos tiene muchos usuarios simultáneos de alta toosupport transaccional de volumen y las necesidades, se recomienda el nivel de servicio Premium de Hola. Para información más reciente de hello en los niveles de servicio de hello actual admite, consulte [niveles de servicio de base de datos de SQL Azure](sql-database-service-tiers.md). También puede crear [grupos elásticos](sql-database-elastic-pool.md) tooshare recursos de rendimiento entre las instancias de base de datos.

Con **base de datos SQL**, software de base de datos de hello automáticamente está configurado, revisar y actualiza Microsoft, lo que reduce los costos de administración. Además, sus capacidades de [copia de seguridad integrada](sql-database-automated-backups.md) ayudan a obtener un ahorro significativo, sobre todo, cuando se tiene gran cantidad de base de datos.

Con **SQL Server en máquinas virtuales de Azure**, puede usar cualquiera de hello proporcionada por la plataforma imágenes de SQL Server (que incluye una licencia) o poner su licencia de SQL Server. Hola todos admite versiones de SQL Server (2008 R2, 2012, 2014, 2016) y están disponibles las ediciones (Developer, Express, Web, Standard, Enterprise). Además, están disponibles versiones de Bring Your-posee-licencia (BYOL) de imágenes de Hola. Cuando se usa hello que Azure proporciona imágenes, costo operativo Hola depende de tamaño de VM de Hola y edición de Hola de SQL Server que elija. Independientemente del tamaño de máquina virtual o la edición de SQL Server, se paga por minuto costo de las licencias de SQL Server y Windows Server, junto con el costo de almacenamiento de Azure para discos de máquina virtual de Hola Hola. opción de facturación por minuto de Hello permite toouse SQL Server mientras según sea necesario sin necesidad de adquirir licencias de SQL Server de adición. Si vuelve a poner su propio tooAzure de licencia de SQL Server, se le cobra por Windows Server y los costos de almacenamiento. Para obtener más información sobre la incorporación de licencias propias, consulte [Movilidad de Licencias a través de Software Assurance en Azure](https://azure.microsoft.com/pricing/license-mobility/).

#### <a name="calculating-hello-total-application-cost"></a>Calcular el costo total de aplicación Hola
Cuando empiece a usar una plataforma de nube, costo de hello de la aplicación en ejecución incluye los costos de administración y desarrollo hello, además de costes de servicio de plataforma de nube pública de Hola.

Aquí es Hola de cálculo del coste detallada de la aplicación se ejecuta en la base de datos SQL y SQL Server en máquinas virtuales de Azure:

**Cuándo se usa Base de datos SQL de Azure:**

*Costo total de la aplicación = costos de administración muy minimizados + costos de desarrollo de software + costos de servicio de Base de datos SQL*

**Cuándo se usa SQL Server en Máquinas virtuales de Azure:**

*Coste total de la aplicación = costos muy minimizados de desarrollo de software + costos de administración + costos de licencias de SQL Server y Windows Server + costos de Azure Storage*

Para obtener más información sobre los precios, vea Hola recursos siguientes:

* [Precios de base de datos SQL](https://azure.microsoft.com/pricing/details/sql-database/)
* [Precios de máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/) para [SQL](https://azure.microsoft.com/pricing/details/virtual-machines/#sql) y [Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#windows)
* [Calculadora de precios de Azure](https://azure.microsoft.com/pricing/calculator/)

> [!NOTE]
> Hay unas pocas características de SQL Server que no se pueden aplicar o no están disponibles en Base de datos SQL. Consulte [SQL Database Features](sql-database-features.md) (Características de Azure SQL Database) e [información sobre Transact-SQL de SQL Database](sql-database-transact-sql-information.md) para más información. Si va a mover una nube de toohello de solución existente de SQL Server, vea [migrar un tooAzure de base de datos base de datos SQL de SQL Server](sql-database-cloud-migrate.md). Cuando se migra un tooSQL de aplicación de SQL Server base de datos local existente, considere la posibilidad de actualizar Hola aplicación tootake aprovechar las capacidades de Hola que oferta de servicios en la nube. Por ejemplo, podría considerar el uso [servicio de aplicaciones Web de Azure](https://azure.microsoft.com/services/app-service/web/) o [servicios en la nube](https://azure.microsoft.com/services/cloud-services/) toohost ventajas de costo de su tooincrease de capa de aplicación.
> 
> 

### <a name="administration"></a>Administración
Para muchas empresas, servicio de nube de hello decisión tootransition tooa es como mucho sobre la descarga de complejidad de administración tal y como costo. Con **base de datos SQL**, Microsoft administra Hola subyacente de hardware. Microsoft automáticamente replica la alta disponibilidad de todos los datos tooprovide, configura y actualiza el software de base de datos de hello, administra el equilibrio de carga y no realiza conmutación por error transparente si hay un error de servidor. Puede continuar tooadminister la base de datos, pero ya no necesita el motor de base de datos de toomanage hello, sistema operativo o hardware.  Ejemplos de elementos que puede seguir tooadminister incluyen bases de datos y los inicios de sesión, índice y consulta para la optimización y auditoría y seguridad.

Con **SQL Server en máquinas virtuales de Azure**, tiene control total sobre el sistema operativo de Hola y configuración de la instancia de SQL Server. Con una máquina virtual, es una tooyou toodecide cuando tooupdate/actualización Hola software de base de datos y sistema operativo y tooinstall ningún software adicional, como un antivirus. Algunas características automatizadas están siempre toodramatically simplificar la aplicación de revisiones, copia de seguridad y de alta disponibilidad. Además, puede controlar el tamaño de Hola de hello VM, número de Hola de discos y sus configuraciones de almacenamiento. Azure permite toochange tamaño de Hola de una máquina virtual según sea necesario. Para obtener más información, consulte [Tamaños de máquinas virtuales](../virtual-machines/windows/sizes.md). 

### <a name="service-level-agreement-sla"></a>Contrato de nivel de servicio (SLA)
Para algunos departamentos de TI, cumplir las obligaciones de tiempo de actividad de un contrato de nivel de servicio (SLA) es una prioridad máxima. En esta sección, veremos qué aplica los SLA de base de datos de tooeach opción de hospedaje.

Para los niveles de servicio Básico, Estándar, Premium y Premium RS de **SQL Database**, Microsoft proporciona un Acuerdo de Nivel de Servicio de disponibilidad del 99,99 %. Para obtener información más reciente de hello, consulte [contrato de nivel de servicio](https://azure.microsoft.com/support/legal/sla/sql-database/). Para información más reciente de hello en los niveles de servicio de base de datos SQL y planes de continuidad del negocio de hello compatibles, consulte [niveles de servicio](sql-database-service-tiers.md).

Para **SQL Server que se ejecutan en máquinas virtuales de Azure**, Microsoft proporciona un SLA de disponibilidad durante el 99,95% que cubre simplemente Hola Máquina Virtual. Este SLA no cubre los procesos de hello (por ejemplo, SQL Server) con hello VM y requiere que se hospedan de al menos dos instancias de máquina virtual en un conjunto de disponibilidad. Para obtener información más reciente de hello, vea hello [VM SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/). Para la base de datos alta disponibilidad (HA) dentro de las máquinas virtuales, debe configurar uno de hello admitida opciones de alta disponibilidad en SQL Server, como [grupos de disponibilidad AlwaysOn](http://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx). Mediante una opción de alta disponibilidad compatibles no proporcionamos un SLA adicional, pero permite tooachieve > disponibilidad de base de datos del 99,99%.

### <a name="market"></a>Toomarket de tiempo
**Base de datos SQL** es la solución adecuada de hello aplicaciones diseñadas en la nube cuando la productividad del desarrollador y tiempo de comercialización rápido son fundamentales. Con una funcionalidad similar a DBA mediante programación, es perfecto para la nube arquitectos y desarrolladores como, reduce la necesidad de Hola para administrar el sistema operativo subyacente de Hola y de base de datos. Por ejemplo, puede usar hello [API de REST](http://msdn.microsoft.com/library/azure/dn505719.aspx) y [Cmdlets de PowerShell](http://msdn.microsoft.com/library/mt740629.aspx) tooautomate y administrar las operaciones administrativas para miles de bases de datos. Características como [grupos elásticos](sql-database-elastic-pool.md) le permiten toofocus de capa de aplicación hello y proporcionar su mercado toohello de solución con mayor rapidez.

**SQL Server que se ejecutan en máquinas virtuales de Azure** es perfecto si sus aplicaciones nuevas o existentes requieren grandes bases de datos, bases de datos interrelacionadas, o tener acceso a características de tooall en SQL Server o Windows. También es una buena opción si desea toomigrate existente tooAzure de aplicaciones y bases de datos como local-es. Puesto que no necesita toochange Hola presentación, aplicación y datos, ahorra tiempo y presupuesto en la solución de cambio de la arquitectura. En su lugar, puede centrarse en la migración de su tooAzure de soluciones y haciendo algunas optimizaciones de rendimiento que pueden ser necesarias en hello plataforma Windows Azure. Para obtener más información, consulte [Procedimientos recomendadas para mejorar el rendimiento para SQL Server en máquinas virtuales de Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md).

## <a name="summary"></a>Resumen
Este artículo explora Base de datos SQL y SQL Server en Máquinas virtuales de Azure y describe los factores de motivación empresariales comunes que pueden afectar a su decisión. Hola te mostramos un resumen de sugerencias para tooconsider:

Elija **Base de datos SQL de Azure** , si:

* Son generar nuevo basado en la nube aplicaciones proporcionar tootake aprovechar Hola costo ahorro y optimización del rendimiento que servicios en la nube. Este enfoque proporciona hello las ventajas de un servicio de nube completamente administrado, ayuda a inferior inicial tiempo de comercialización y puede ofrecer una optimización de costo a largo plazo.
* Desea toohave Microsoft realizar operaciones de administración comunes en las bases de datos y requieren una mayor disponibilidad SLA para las bases de datos.

Elija **SQL Server en Máquinas virtuales de Azure** si:

* Tiene aplicaciones locales existentes que se desea toomigrate o ampliar toohello en la nube, o si desea que las aplicaciones empresariales toobuild mayores de 4 TB. Este enfoque proporciona la ventaja de Hola de compatibilidad SQL del 100%, capacidad de la base de datos grande, un control total sobre SQL Server y Windows y segura entornos tooon túneles. Este enfoque minimiza los costos de desarrollo y modificaciones de las aplicaciones existentes.
* Ya dispone de recursos de TI existentes, y podría contar con aplicación de revisiones, copias de seguridad y alta disponibilidad de la base de datos. Tenga en cuenta que algunas características automatizadas simplifican considerablemente estas operaciones. 

## <a name="next-steps"></a>Pasos siguientes
* Vea [la primera base de datos de SQL Azure](sql-database-get-started-portal.md) tooget a trabajar con la base de datos SQL.
* Consulte [Precio de Base de datos SQL](https://azure.microsoft.com/pricing/details/sql-database/).
* Vea [aprovisionar una máquina virtual de SQL Server en Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md) tooget a trabajar con SQL Server en máquinas virtuales de Azure.

