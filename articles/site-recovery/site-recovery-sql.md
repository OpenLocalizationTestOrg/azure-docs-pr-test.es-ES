---
title: las aplicaciones de aaaReplicate con SQL Server y Azure Site Recovery | Documentos de Microsoft
description: "Este artículo se describe cómo tooreplicate con Azure Site Recovery para las capacidades de desastres de SQL Server de SQL Server."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 99755f2cd2f7e924071f1e230ac4a0bda88f0a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protect-sql-server-using-sql-server-disaster-recovery-and-azure-site-recovery"></a>Proteger SQL Server con la recuperación ante desastres de SQL Server y Azure Site Recovery

Este artículo describe cómo tooprotect Hola SQL Server back-end de una aplicación con una combinación de continuidad del negocio de SQL Server y tecnologías de (BCDR) de recuperación ante desastres, y [Azure Site Recovery](site-recovery-overview.md).

Antes de empezar, asegúrese de que comprende las funcionalidades de recuperación ante desastres de SQL Server, incluidos los clústeres de conmutación por error, los grupos de disponibilidad AlwaysOn, la creación de reflejo de la base de datos y el trasvase de registros.


## <a name="sql-server-deployments"></a>Implementaciones de SQL Server

Muchas cargas de trabajo usar SQL Server como base, y se puede integrar con aplicaciones, como SharePoint y Dynamics, SAP, servicios de datos de tooimplement.  SQL Server se puede implementar de varias maneras:

* **Servidor SQL independiente**: SQL Server y todas las bases de datos se hospedan en una sola máquina (física o virtual). Cuando se virtualiza, la agrupación en clústeres de host se utiliza para conseguir una elevada disponibilidad local. No se implementa alta disponibilidad de nivel de invitado.
* **Instancias de agrupación en clústeres de conmutación por error de SQL Server**: dos o más nodos que ejecutan instancias de SQL Server con discos compartidos se configuran en un clúster de conmutación por error de Windows. Si un nodo está inactivo, el clúster de Hola puede conmutar por error SQL Server instancia tooanother. Este programa de instalación es tooimplement usados normalmente alta disponibilidad en un sitio primario. Esta implementación no protege frente a errores o una interrupción en la capa de almacenamiento compartido Hola. Un disco compartido se puede implementar con iSCSI, canal de fibra o VHDx compartido.
* **Grupos de disponibilidad AlwaysOn de SQL**: se configuran dos o más nodos en un clúster no compartido, con bases de datos SQL Server configuradas en un grupo de disponibilidad, con replicación sincrónica y conmutación por error automática.

 En este artículo aprovecha Hola después de tecnologías de recuperación de desastres SQL nativo para la recuperación de sitio remoto tooa de bases de datos:

* SQL grupos de disponibilidad AlwaysOn, tooprovide para recuperación ante desastres para SQL Server 2012 o 2014 Enterprise Edition.
* Reflejo de base de datos SQL en modo de alta seguridad para SQL Server Standard Edition (cualquier versión) o SQL Server 2008 R2.

## <a name="site-recovery-support"></a>Compatibilidad de Site Recovery

### <a name="supported-scenarios"></a>Escenarios admitidos
Recuperación de sitio puede proteger SQL Server como se resume en la tabla de Hola.

**Escenario** | **sitio secundario tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Sí | Sí
**VMware** | Sí | Sí
**Servidor físico** | Sí | Sí

### <a name="supported-sql-server-versions"></a>Versiones admitidas de SQL Server
Se admiten estas versiones de SQL Server, para escenarios de hello admitida:

* SQL Server 2016 Enterprise y Standard
* SQL Server 2014 Enterprise y Standard
* SQL Server 2012 Enterprise y Standard
* SQL Server 2008 R2 Enterprise y Standard

### <a name="supported-sql-server-integration"></a>Integración de SQL Server admitida

Recuperación del sitio puede integrarse con las tecnologías nativas de SQL Server BCDR resumidas en la tabla de hello, tooprovide una solución de recuperación ante desastres.

**Característica** | **Detalles** | **SQL Server** |
--- | --- | ---
**Grupos de disponibilidad AlwaysOn** | Se ejecutan varias instancias independientes de SQL Server, cada una en un clúster de conmutación por error que tiene varios nodos.<br/><br/>Las bases de datos se pueden agrupar en grupos de conmutación por error que se puede copiar (reflejar) en instancias de SQL Server para que no se necesite ningún almacenamiento compartido.<br/><br/>Proporciona recuperación ante desastres entre un sitio principal y uno o más sitios secundarios. Dos nodos pueden configurarse en un clúster no compartido con Bases de datos de SQL Server configurado en un grupo de disponibilidad con replicación sincrónica y conmutación por error automática. | SQL Server 2014 y 2012 Enterprise Edition
**Clústeres de conmutación por error (FCI AlwaysOn)** | SQL Server aprovecha la agrupación en clústeres de conmutación por error de Windows para conseguir alta disponibilidad de las cargas de trabajo locales de SQL Server.<br/><br/>Los nodos que ejecutan instancias de SQL Server con discos compartidos se configuran en un clúster de conmutación por error. Si una instancia está inactiva Hola clúster conmuta por error toodifferent uno.<br/><br/>clúster de Hello no protege frente a errores o interrupciones en el almacenamiento compartido. disco compartido Hola puedan implementarse con iSCSI, canal de fibra, o compartido de Vhdx. | SQL Server Enterprise Edition<br/><br/>SQL Server Standard edition (solo nodos tootwo limitado)
**Creación de un reflejo de la base de datos (modo de alta seguridad)** | Protege una única secundaria copia tooa de única base de datos. Disponible en modos de replicación de seguridad alta (sincrónica) y de alto rendimiento (asincrónica). No requiere un clúster de conmutación por error. | SQL Server 2008 R2<br/><br/>Todas las ediciones de SQL Server Enterprise
**SQL Server independiente** | Hola SQL Server y base de datos se hospedan en un único servidor (físico o virtual). Clústeres de host se utiliza para lograr alta disponibilidad si servidor hello es virtual. Sin alta disponibilidad de nivel de invitado. | Edición Enterprise o Standard

## <a name="deployment-recommendations"></a>Recomendaciones de implementación

En la siguiente tabla se resumen nuestras recomendaciones para integrar las tecnologías de SQL Server BCDR con Site Recovery.

| **Versión** | **Edición** | **Implementación** | **Local tooon-local** | **TooAzure local** |
| --- | --- | --- | --- | --- |
| SQL Server 2014 o 2012 |Enterprise |Instancia de clúster de conmutación por error |Grupos de disponibilidad AlwaysOn |Grupos de disponibilidad AlwaysOn |
|| Enterprise |Grupos de disponibilidad AlwaysOn para alta disponibilidad |Grupos de disponibilidad AlwaysOn |Grupos de disponibilidad AlwaysOn | |
|| Standard |Instancia de clúster de conmutación por error (FCI) |Replicación de Site Recovery con un reflejo local |Replicación de Site Recovery con un reflejo local | |
|| Enterprise o Standard |Independiente |Replicación de Site Recovery |Replicación de Site Recovery | |
| SQL Server 2008 R2 o 2008 |Enterprise o Standard |Instancia de clúster de conmutación por error (FCI) |Replicación de Site Recovery con un reflejo local |Replicación de Site Recovery con un reflejo local |
|| Enterprise o Standard |Independiente |Replicación de Site Recovery |Replicación de Site Recovery | |
| SQL Server (cualquier versión) |Enterprise o Standard |Instancia de clúster de conmutación por error: aplicación de DTC |Replicación de Site Recovery |No compatible |

## <a name="deployment-prerequisites"></a>Requisitos previos de implementación

* La implementación local de SQL Server ejecuta una versión compatible de SQL Server. Normalmente, también necesitará Active Directory para SQL Server.
* requisitos de Hola para Hola escenario que desee toodeploy. Obtener más información sobre los requisitos de compatibilidad para [replicación tooAzure](site-recovery-support-matrix-to-azure.md) y [local](site-recovery-support-matrix.md), y [requisitos previos de implementación](site-recovery-prereq.md).
* tooset la recuperación en Azure, ejecución hello [evaluación de preparación de máquina Virtual de Azure](http://www.microsoft.com/download/details.aspx?id=40898) herramienta en sus máquinas virtuales de SQL Server, toomake seguro de que sean compatibles con Azure y Site Recovery.

## <a name="set-up-active-directory"></a>Configuración de Active Directory

Establecer seguridad de Active Directory, en el sitio de recuperación secundaria hello, para SQL Server toorun correctamente.

* **Pequeña empresa**, con un número pequeño de aplicaciones y el controlador de dominio único para el sitio local de hello, si desea toofail sobre todo sitio hello, se recomienda usar el controlador de dominio de Site Recovery replicación tooreplicate Hola Centro de datos secundario toohello o tooAzure.
* **Enterprise toolarge Media**: si tiene un gran número de aplicaciones, un bosque de Active Directory, y desea toofail por aplicaciones o cargas de trabajo, se recomienda configurar un controlador de dominio adicional en el centro de datos secundario de hello, o en Azure. Si usa AlwaysOn disponibilidad grupos toorecover tooa sitio remoto, se recomienda que configurar otro controlador de dominio adicional en el sitio secundario de Hola o en Azure, toouse de instancia de SQL Server de hello recuperado.

instrucciones de Hello en este artículo suponen que un controlador de dominio está disponible en la ubicación secundaria Hola. [Más información](site-recovery-active-directory.md) sobre la protección de Active Directory con Site Recovery.


## <a name="integrate-with-sql-server-always-on-for-replication-tooazure"></a>Integrar con SQL Server Always On para tooAzure de replicación

Esto es lo necesita toodo:

1. Importe scripts en su cuenta de Azure Automation. Contiene scripts de hello toofailover grupo de disponibilidad de SQL en un [máquina virtual del Administrador de recursos](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAG.ps1) y un [máquina virtual de clásico](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAGClassic.ps1).

    [![Implementar tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)


1. Agregar FailoverAG de SQL de ASR como una acción antes del primer grupo de Hola Hola del plan de recuperación.

1. Siga las instrucciones de hello disponibles en hello script toocreate un nombre de automatización de la variable tooprovide Hola Hola de grupos de disponibilidad.

### <a name="steps-toodo-a-test-failover"></a>Pasos toodo una conmutación por error de prueba

SQL AlwaysOn no admite de forma nativa la conmutación por error de prueba. Por lo tanto, se recomienda siguiente hello:

1. Configurar [copia de seguridad de Azure](../backup/backup-azure-vms.md) en la máquina virtual de Hola que hospeda la réplica del grupo de disponibilidad de hello en Azure.

1. Antes de activar la conmutación por error de prueba del plan de recuperación de hello, recuperar máquina virtual de Hola de copia de seguridad de hello realizada en el paso anterior de Hola.

    ![Restauración de datos de Azure Backup ](./media/site-recovery-sql/restore-from-backup.png)

1. [Forzar un quórum](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum#PowerShellProcedure) en la máquina virtual de hello restaurado desde copia de seguridad.

1. Actualizar la dirección IP de hello escucha tooan IP disponible en la red de conmutación por error de prueba de Hola.

    ![Actualización de la dirección IP del agente de escucha](./media/site-recovery-sql/update-listener-ip.png)

1. Conecte el agente de escucha.

    ![Conexión del agente de escucha](./media/site-recovery-sql/bring-listener-online.png)

1. Cree un equilibrador de carga con una IP creado en el servidor front-end IP grupo correspondiente tooeach agente de escucha y máquina virtual Hola SQL que agregó en el grupo de back-end de Hola.

     ![Creación del equilibrador de carga: grupo de direcciones IP de front-end ](./media/site-recovery-sql/create-load-balancer1.png)

    ![Creación del equilibrador de carga: grupo de direcciones IP de back-end ](./media/site-recovery-sql/create-load-balancer2.png)

1. Realice una conmutación por error de prueba del plan de recuperación de Hola.

### <a name="steps-toodo-a-failover"></a>Pasos toodo una conmutación por error

Cuando haya agregado el script de Hola Hola plan de recuperación y plan de recuperación de hello validado, realice una conmutación por error de prueba, puede hacer Hola del plan de recuperación de conmutación por error.


## <a name="integrate-with-sql-server-always-on-for-replication-tooa-secondary-on-premises-site"></a>Integrar con SQL Server Always On para el sitio de replicación tooa local secundario

Si Hola SQL Server está usando grupos de disponibilidad para alta disponibilidad (o una FCI), se recomienda usar grupos de disponibilidad en el sitio de recuperación de hello también. Tenga en cuenta que esto se aplica tooapps que no utilicen transacciones distribuidas.

1. [Configure bases de datos](https://msdn.microsoft.com/library/hh213078.aspx) en grupos de disponibilidad.
1. Crear una red virtual en el sitio secundario de Hola.
1. Configurar una conexión de VPN de sitio a sitio entre la red virtual de hello y el sitio primario de Hola.
1. Crear una máquina virtual en el sitio de recuperación de hello e instalar a SQL Server en ella.
1. Extender Hola existente siempre en disponibilidad grupos toohello nueva VM de SQL Server. Configure esta instancia de SQL Server como una copia de réplica asincrónica.
1. Crear un agente de escucha del grupo de disponibilidad o actualizar: máquina virtual de réplica asincrónica de hello existente del agente de escucha tooinclude Hola.
1. Asegúrese de que esa granja de servidores de aplicación Hola se define mediante el agente de escucha de Hola. Si es el programa de instalación utilizando el nombre del servidor de base de datos de hello, actualizarlo y agente de escucha de toouse hello, que no es necesario tooreconfigure después Hola conmutación por error.

Para las aplicaciones que usan transacciones distribuidas, le recomendamos implementar Site Recovery con la [replicación entre sitios de VMware o servidores físicos](site-recovery-vmware-to-vmware.md).

### <a name="recovery-plan-considerations"></a>Consideraciones del plan de recuperación
1. Agregar esta biblioteca VMM toohello de secuencia de comandos de ejemplo, en sitios primarios y secundarios de Hola.

        Param(
        [string]$SQLAvailabilityGroupPath
        )
        import-module sqlps
        Switch-SqlAvailabilityGroup -Path $SQLAvailabilityGroupPath -AllowDataLoss -force

1. Cuando se crea un plan de recuperación para la aplicación hello, agregue un pre acción tooGroup-1 con scripts paso, que invoca Hola script toofail sobre grupos de disponibilidad.

## <a name="protect-a-standalone-sql-server"></a>Protección de un servidor SQL Server independiente

En este escenario, se recomienda que realice máquina de SQL Server de Site Recovery replicación tooprotect Hola. los pasos exactos Hola dependerán de si SQL Server es una máquina virtual o un servidor físico y si desea tooreplicate tooAzure o un elemento secundario de sitio local. Más información acerca de [escenarios de Site Recovery](site-recovery-overview.md).

## <a name="protect-a-sql-server-cluster-standard-editionwindows-server-2008-r2"></a>Protección de un clúster de SQL Server (Standard Edition o Windows Server 2008 R2)

Para un clúster que ejecuta SQL Server Standard edition o SQL Server 2008 R2, se recomienda que utilizar la replicación de Site Recovery tooprotect SQL Server.

### <a name="on-premises-tooon-premises"></a>Local tooon-local

* Si la aplicación hello utiliza transacciones distribuidas se recomienda implementar [Site Recovery con replicación de SAN](site-recovery-vmm-san.md) en un entorno de Hyper-V, o [físicos/VMware server tooVMware](site-recovery-vmware-to-vmware.md) para un entorno de VMware.
* Para aplicaciones de DTC no, use Hola por encima de clúster de enfoque toorecover Hola como un servidor independiente, mediante el aprovechamiento de una base de datos reflejada de seguridad alta local.

### <a name="on-premises-tooazure"></a>TooAzure locales

Recuperación de sitio no proporciona invitado compatibilidad con clústeres al replicar tooAzure. SQL Server tampoco proporciona una solución de recuperación ante desastres de bajo costo para la edición Standard. En este escenario, se recomienda proteger SQL Server de hello local SQL Server cluster tooa independiente y recuperarlos en Azure.

1. Configurar una instancia de SQL Server independientes adicionales en el sitio local de Hola.
1. Configurar Hola instancia tooserve como un espejo de hello las bases de datos desea tooprotect. Configure el reflejo en modo de alta seguridad.
1. Configurar la recuperación del sitio en el sitio local de hello, para ([Hyper-V](site-recovery-hyper-v-site-to-azure.md) o [servidores físicos o máquinas virtuales de VMware)](site-recovery-vmware-to-azure-classic.md).
1. Utilice tooAzure de instancia de Site Recovery replicación tooreplicate Hola nuevo SQL Server. Puesto que es una copia de seguridad alta reflejada, se sincronizarán con clúster principal hello, pero será tooAzure replicado mediante replicación de Site Recovery.


![Clúster estándar](./media/site-recovery-sql/standalone-cluster-local.png)

### <a name="failback-considerations"></a>Consideraciones de la conmutación por recuperación

Para los clústeres de SQL Server Standard, conmutación por recuperación después de una conmutación por error no planeada requiere una copia de seguridad SQL server y restaurar, desde Hola reflejado instancia toohello clúster original, con restablecimiento del reflejo de Hola.

## <a name="next-steps"></a>Pasos siguientes
[Obtenga información](site-recovery-components.md) acerca de la arquitectura de Site Recovery.
