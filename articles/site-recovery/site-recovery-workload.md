---
title: "¿las cargas de trabajo de aaaWhat pueden proteger con Azure Site Recovery?"
description: "Azure Site Recovery protege las cargas de trabajo y las aplicaciones, se coordina la replicación hello, conmutación por error y recuperación de máquinas virtuales en locales y servidores físicos tooAzure o tooa secundario al sitio local"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: 4953948f-26c0-4699-8fe7-59d3bfc1d3da
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/08/2017
ms.author: raynew
ms.openlocfilehash: cab2e1ce3c2b7b2c5f899d957219f5c12eb5965c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-workloads-can-you-protect-with-azure-site-recovery"></a>¿Qué cargas de trabajo se pueden proteger con Azure Site Recovery?
Este artículo describen las cargas de trabajo y las aplicaciones que se puede replicar con hello servicio Azure Site Recovery.

Enviar comentarios o preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="overview"></a>Información general
Las organizaciones necesitan una continuidad del negocio y cargas de trabajo de tookeep de estrategia de desastres (BCDR) de recuperación de datos segura y está disponible durante el tiempo de inactividad planeado y no planeado y recuperación las condiciones de trabajo de tooregular tan pronto como sea posible.

Recuperación de sitio es un servicio de Azure que contribuye estrategia BCDR tooyour. Recuperación de sitio puede implementar en la nube toohello replicación consciente de las aplicaciones, o un sitio secundario de tooa. Si las aplicaciones son ventanas o basados en Linux, la ejecución en servidores físicos, VMware o Hyper-V, puede utilizar la replicación de Site Recovery tooorchestrate, realizar pruebas de recuperación ante desastres y ejecutar conmutaciones por error y conmutación por recuperación.

Site Recovery se integra con aplicaciones de Microsoft, incluidas SharePoint, Exchange, Dynamics, SQL Server y Active Directory. Microsoft también trabaja en estrecha colaboración con proveedores líderes como Oracle, SAP, IBM y Red Hat. Puede personalizar las soluciones de replicación en función de cada aplicación.

## <a name="why-use-site-recovery-for-application-replication"></a>¿Por qué es aconsejable usar Site Recovery para la replicación de aplicaciones?
Site Recovery contribuye tooapplication nivel de protección y recuperación como sigue:

* Independiente de las aplicaciones; proporciona replicación para las cargas de trabajo que se ejecutan en un equipo compatible.
* Replicación casi sincrónica con RPO tan bajo como necesidades de hello toomeet de 30 segundos de las aplicaciones empresariales más importantes.
* Instantáneas coherentes con las aplicaciones para aplicaciones de uno o varios niveles.
* Integración con SQL Server AlwaysOn y asociación con otras tecnologías de replicación de nivel de aplicación, incluida la replicación de AD, SQL AlwaysOn, Grupos de disponibilidad de base de datos (DAG) de Exchange y Oracle Data Guard.
* Planes de recuperación flexible, que permiten toorecover toda una aplicación de la pila con un solo clic y se incluyen scripts externos tooinclude acciones manuales en el plan de Hola.
* Administración de red en Site Recovery y Azure toosimplify avanzada de requisitos de red de aplicaciones, incluidas las direcciones IP de hello capacidad tooreserve, configurar Equilibrio de carga y la integración con Azure Traffic Manager, para switchovers de red de baja RTO.
* Una biblioteca de automatización enriquecida que proporciona scripts específicos de la aplicación y preparados para la producción que pueden descargarse e integrarse con los planes de recuperación.

## <a name="workload-summary"></a>Resumen de cargas de trabajo
Site Recovery puede replicar cualquier aplicación que se ejecute en una máquina compatible. Además, nos hemos asociado con toocarry de los equipos de producto cabo pruebas adicionales de específico de la aplicación.

| **Carga de trabajo** | **Sitio secundario de replicar las máquinas virtuales de Hyper-V tooa** | **Replicar máquinas virtuales de Hyper-V tooAzure** | **Replicar el sitio secundario de máquinas virtuales VMware tooa** | **Replicar máquinas virtuales VMware tooAzure** |
| --- | --- | --- | --- | --- |
| Active Directory, DNS |Y |Y |Y |Y |
| Aplicaciones web (IIS, SQL) |Y |Y |Y |Y |
| System Center Operations Manager |Y |Y |Y |Y |
| SharePoint |Y |Y |Y |Y |
| SAP<br/><br/>Replicar tooAzure de sitio SAP para no clúster |S (probado por Microsoft) |S (probado por Microsoft) |S (probado por Microsoft) |S (probado por Microsoft) |
| Exchange (no DAG) |Y |Y |Y |Y |
| Escritorio remoto/VDI |Y |Y |Y |N/D |
| Linux (sistema operativo y aplicaciones) |S (probado por Microsoft) |S (probado por Microsoft) |S (probado por Microsoft) |S (probado por Microsoft) |
| Dynamics AX |Y |Y |Y |Y |
| Dynamics CRM |Y |Próximamente |Y |Próximamente |
| Oracle |S (probado por Microsoft) |S (probado por Microsoft) |S (probado por Microsoft) |S (probado por Microsoft) |
| Servidor de archivos de Windows |Y |Y |Y |Y |
| Citrix XenApp y XenDesktop |N/D |Y |N/D |Y |

## <a name="replicate-active-directory-and-dns"></a>Replicación de Active Directory y DNS
Una infraestructura de Active Directory y DNS son aplicaciones de empresa de toomost esenciales. Durante la recuperación ante desastres, podrá necesita tooprotect y recuperar estos componentes de la infraestructura antes de recuperar las aplicaciones y cargas de trabajo.

Puede usar toocreate un plan de recuperación ante desastres automatizada completa de recuperación del sitio de Active Directory y DNS. Por ejemplo, si desea toofail sobre SharePoint y SAP desde un sitio secundario tooa principal, puede configurar un plan de recuperación que conmuta por Active Directory primero y, a continuación, una recuperación específica de aplicación adicionales planear toofail sobre Hola otras aplicaciones que se basan en activo Directorio.

[Más información](site-recovery-active-directory.md) sobre la protección de Active Directory y DNS.

## <a name="protect-sql-server"></a>Protección de SQL Server
SQL Server proporciona una base de servicios de datos para los servicios de datos de muchas aplicaciones empresariales de un centro de datos local.  Recuperación de sitio puede utilizarse junto con las tecnologías de SQL Server HA/DR, aplicaciones de varios niveles empresariales de tooprotect que utilizan SQL Server. Site Recovery proporciona:

* Una solución de recuperación ante desastres simple y rentable para SQL Server. Replicar varias versiones y ediciones de servidores independientes de SQL Server y clústeres, tooAzure o tooa sitio secundario.  
* Integración con grupos de disponibilidad AlwaysOn de SQL, toomanage conmutación por error y conmutación por recuperación con planes de recuperación de Azure Site Recovery.
* Planes de recuperación to-end de hello en todos los niveles de una aplicación, incluidas bases de datos de SQL Server de Hola.
* Escalado de SQL Server para cargas máximas con Site Recovery "protegiéndolos" en tamaños de máquina virtual de IaaS más grandes en Azure.
* Pruebas fáciles de recuperación ante desastres de SQL Server. Puede ejecutar conmutaciones por error de prueba tooanalyze datos y ejecutar comprobaciones de cumplimiento, sin afectar a su entorno de producción.

[Más información](site-recovery-sql.md) sobre cómo proteger SQL Server.

## <a name="protect-sharepoint"></a>Protección de SharePoint
Azure Site Recovery ayuda a proteger las implementaciones de SharePoint como se indica a continuación:

* Elimina la necesidad de Hola y los costos de infraestructura asociado para una granja de modo de espera para la recuperación ante desastres. Use Site Recovery tooreplicate un sitio secundario (niveles de Web, aplicación y base de datos) del conjunto de servidores completo tooAzure o tooa.
* Simplifica la administración e implementación de las aplicaciones. Sitio de actualizaciones implementadas toohello primario se replican automáticamente y, por tanto, están disponible después de la conmutación por error y recuperación de una granja de servidores en un sitio secundario. También reduce los costos asociados con la actualización de una granja de modo de espera actualizada y complejidad de la administración de Hola.
* Simplifica el desarrollo y las pruebas de aplicaciones de SharePoint mediante la creación de un entorno de réplica de copia de producción a petición para realizar pruebas y depuraciones.
* Simplifica la nube de transición toohello mediante tooAzure de las implementaciones de SharePoint de Site Recovery toomigrate.

[Más información](site-recovery-sharepoint.md) sobre cómo proteger SharePoint.

## <a name="protect-dynamics-ax"></a>Protección de Dynamics AX
Azure Site Recovery le ayuda a proteger soluciones ERP de Dynamics AX mediante:

* Coordinación de la replicación de todo el entorno de Dynamics AX (niveles de Web y AOS, niveles de base de datos de SharePoint) tooAzure, o un sitio secundario de tooa.
* Simplificar la migración de Dynamics AX implementaciones toohello en la nube (Azure).
* La simplificación del desarrollo y de las pruebas de aplicaciones de Dynamics AX mediante la creación de una copia de producción a petición para realizar pruebas y depuraciones.

[Más información](site-recovery-dynamicsax.md) sobre cómo proteger Dynamic AX.

## <a name="protect-rds"></a>Protección de RDS
Servicios de escritorio remoto (RDS) permite la infraestructura de escritorio virtual (VDI), escritorios basados en sesión y las aplicaciones, lo que permite a los usuarios toowork en cualquier lugar. Con Azure Site Recovery, puede:

* Replicar sitio secundario de tooa de escritorios virtuales agrupados administrados o no administrados y las aplicaciones y las sesiones tooa secundaria sitio remoto o Azure.
* Esto es lo que se puede replicar:

| **RDS** | **Sitio secundario de replicar las máquinas virtuales de Hyper-V tooa** | **Replicar máquinas virtuales de Hyper-V tooAzure** | **Replicar el sitio secundario de máquinas virtuales VMware tooa** | **Replicar máquinas virtuales VMware tooAzure** | **Sitio secundario de replicar servidores físicos tooa** | **Replicar servidores físicos tooAzure** |
| --- | --- | --- | --- | --- | --- | --- |
| **Escritorio virtual agrupado (no administrado)** |Sí |No |Sí |No |Sí |No |
| **Escritorio virtual agrupado (administrado y sin UPD)** |Sí |No |Sí |No |Sí |No |
| **Aplicaciones remotas y sesiones de escritorio (sin UPD)** |Sí |Sí |Sí |Sí |Sí |Sí |

[Más información](https://gallery.technet.microsoft.com/Remote-Desktop-DR-Solution-bdf6ddcb) sobre cómo proteger RDS.

## <a name="protect-exchange"></a>Protección de Exchange
Site Recovery ayuda a proteger Exchange como se indica a continuación:

* Para implementaciones pequeñas de Exchange, como los servidores de un único o independiente, Site Recovery puede replicar y conmutar por error tooAzure o tooa sitio secundario.
* En implementaciones mayores Site Recovery se integra con los DAG de Exchange.
* Dag de Exchange son Hola recomendada solución para la recuperación ante desastres de Exchange en una empresa.  Planes de recuperación de recuperación de sitio pueden incluir dag, tooorchestrate DAG conmutación por error en todos los sitios.

[Más información](https://gallery.technet.microsoft.com/Exchange-DR-Solution-using-11a7dcb6) sobre cómo proteger Exchange.

## <a name="protect-sap"></a>Protección de SAP
Use Site Recovery tooprotect la implementación de SAP, como sigue:

* Habilitar la protección de aplicaciones de SAP NetWeaver y no es de producción NetWeaver que se ejecutan de forma local, replicando tooAzure de componentes.
* Habilitar la protección de aplicaciones de SAP NetWeaver y no es de producción NetWeaver ejecuta Azure, mediante la replicación de componentes tooanother centro de datos de Azure.
* Simplificar la migración a la nube, mediante el uso de Site Recovery toomigrate su tooAzure de implementación de SAP.
* Simplificar las actualizaciones de los proyectos SAP, las pruebas y la creación de prototipos, mediante la creación de una clon en producción a petición para probar las aplicaciones SAP.

[Más información](site-recovery-sap.md) sobre cómo proteger SAP.

## <a name="protect-iis"></a>Protección de IIS
Use Site Recovery tooprotect la implementación de IIS, como sigue:

Azure Site Recovery proporciona recuperación ante desastres mediante la replicación de componentes críticos de hello en entorno tooa frío sitio remoto o una nube pública, como Microsoft Azure. Puesto que la máquina virtual de hello con servidor web de Hola y de base de datos de Hola se están replicados toohello sitio de recuperación, no hay ningún archivo de configuración de toobackup de requisito o certificados por separado. Hola asignaciones para la aplicación y se puede actualizar enlaces depende de variables de entorno que oficina de correos modificada de conmutación por error a través de scripts que se integra en planes de recuperación ante desastres de Hola. Máquinas virtuales se muestren en el sitio de recuperación de hello solo en caso de hello de una conmutación por error. Esto no solo, Azure Site Recovery también le ayuda a orquestar la conmutación por error de hello final tooend proporcionando que Hola siguiendo las capacidades:

-   Apagado de Hola de secuenciación y el inicio de máquinas virtuales de Hola distintos niveles.
-   Agregar la actualización de tooallow de secuencias de comandos de las dependencias de aplicación y enlaces en máquinas virtuales de hello después de iniciar. las secuencias de comandos de Hello también pueden ser sitio de recuperación del servidor toopoint toohello de tooupdate usado Hola DNS.
-   Asignar IP direcciones toovirtual máquinas pre-conmutación por error mediante la asignación de redes principales y de recuperación de hello y, por tanto, las secuencias de comandos de uso que no es necesario toobe actualizan posterior conmutación por error.
-   Capacidad de una conmutación por error de un solo clic para varias aplicaciones web en servidores web de hello, lo que elimina ámbito Hola confusiones en caso de hello de un desastre.
-   Planes de recuperación de capacidad tootest hello en un entorno aislado para recuperación ante desastres aumenta.

[Más información](https://aka.ms/asr-iis) acerca de cómo una granja de servidores web de IIS.

## <a name="protect-citrix-xenapp-and-xendesktop"></a>Protección de Citrix XenApp y XenDesktop
Use Site Recovery tooprotect las implementaciones de Citrix XenApp o XenDesktop, como sigue:

* Habilitar la protección de hello implementación Citrix XenApp y XenDesktop, mediante la replicación de implementación diferentes capas incluidos (servidor de DNS de AD, SQL bases de datos servidor, controlador de entrega de Citrix, StoreFront server, XenApp Master (VDA), servidor de licencias de Citrix XenApp) tooAzure.
* Simplificar la migración a la nube, mediante el uso de Site Recovery toomigrate su tooAzure de implementación de Citrix XenApp y XenDesktop.
* Simplifique las pruebas de Citrix XenApp o XenDesktop mediante la creación de una copia de producción a petición para la realización de pruebas y depuraciones.
* Esta solución solo se puede aplicar a escritorios virtuales del sistema operativo de Windows Server, no a escritorios virtuales cliente, ya que estos aún no se admiten para la concesión de licencias en Azure.
Aquí encontrará [más información](https://azure.microsoft.com/pricing/licensing-faq/) acerca de la concesión de licencias a escritorios de cliente/servidor de Azure.

[Más información](site-recovery-citrix-xenapp-and-xendesktop.md) acerca de la protección de las implementaciones de Citrix XenApp y XenDesktop. Como alternativa, puede hacer referencia hello [notas del producto de Citrix](https://aka.ms/citrix-xenapp-xendesktop-with-asr) que detalla Hola igual.

## <a name="next-steps"></a>Pasos siguientes
[Comprobación de los requisitos previos](site-recovery-prereq.md)
