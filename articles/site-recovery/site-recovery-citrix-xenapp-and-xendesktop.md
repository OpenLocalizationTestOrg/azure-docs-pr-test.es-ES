---
title: "una implementación de Citrix XenDesktop y XenApp de varios nivel con Azure Site Recovery aaaReplicate | Documentos de Microsoft"
description: "Este artículo se describe cómo tooprotect y recuperar Citrix XenDesktop XenApp las implementaciones y con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a>Replicar una implementación de XenApp y XenDesktop de Citrix de niveles múltiples mediante Azure Site Recovery

## <a name="overview"></a>Información general

Citrix XenDesktop es una solución de virtualización de escritorio que ofrece aplicaciones y escritorios como ondemand servicio tooany usuario, en cualquier lugar. Con la tecnología de entrega FlexCast, XenDesktop puede rápida y segura entregar aplicaciones y escritorios toousers.
Actualmente, XenApp de Citrix no proporciona funciones de recuperación ante desastres.

Una solución de recuperación ante desastres conveniente, debe permitir que el modelo de planes de recuperación alrededor de Hola por encima de arquitecturas de aplicación compleja y también tienen Hola capacidad tooadd personalizar pasos toohandle aplicación asignaciones entre los distintos niveles, por lo que proporciona un con un solo clic que captura la solución en caso de hello de un desastre iniciales tooa reducir el RTO.

Este documento proporciona instrucciones detalladas para crear una solución de recuperación ante desastres para las implementaciones locales de XenApp de Citrix en plataformas vSphere de Hyper-V y VMware. Este documento también se describe cómo tooperform una conmutación por error de prueba (detalles de recuperación ante desastres) y tooAzure de conmutación por error imprevista con planes de recuperación, los requisitos previos y configuraciones de hello compatible.


## <a name="prerequisites"></a>Requisitos previos

Antes de empezar, asegúrese de que comprende siguiente hello:

1. [Replicar una máquina virtual tooAzure](site-recovery-vmware-to-azure.md)
1. Cómo demasiado[el diseño de una red de recuperación](site-recovery-network-design.md)
1. [Realizar una tooAzure de conmutación por error de prueba](site-recovery-test-failover-to-azure.md)
1. [Realizar una conmutación por error tooAzure](site-recovery-failover.md)
1. Cómo demasiado[replicar un controlador de dominio](site-recovery-active-directory.md)
1. Cómo demasiado[replicar SQL Server](site-recovery-sql.md)

## <a name="deployment-patterns"></a>Modelos de implementación

Normalmente, una granja de servidores Citrix XenApp y XenDesktop tiene Hola seguir el patrón de implementación:

**Patrón de implementación**

Implementación de XenApp y XenDesktop de Citrix con servidor DNS de AD, servidor de SQL Database, controlador de entrega de Citrix, servidor de StoreFront, XenApp Master (VDA) y servidor de licencias de XenApp de Citrix

![Modelo de implementación 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a>Compatibilidad de Site Recovery

A fin de Hola de este artículo, administra las implementaciones de Citrix en máquinas virtuales de VMware vSphere 6.0 o System Center VMM 2012 R2 han estado usado toosetup recuperación ante desastres.

### <a name="source-and-target"></a>Origen y destino

**Escenario** | **sitio secundario tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Fuera del ámbito | Sí
**VMware** | Fuera del ámbito | Sí
**Servidor físico** | Fuera del ámbito | Sí

### <a name="versions"></a>Versiones
Los clientes pueden implementar componentes de XenApp como máquinas virtuales que se ejecutan en Hyper-V o VMware o como servidores físicos. Azure Site Recovery puede proteger tanto tooAzure las implementaciones físicas y virtuales.
Como XenApp 7.7 o una versión posterior se admite en Azure, solo las implementaciones con estas versiones pueden conmutar por error tooAzure para la migración o recuperación ante desastres.

### <a name="things-tookeep-in-mind"></a>Tookeep de cosas en cuenta

1. Protección y recuperación de local se admite implementaciones con sistema operativo Server máquinas toodeliver XenApp las aplicaciones publicadas y XenApp publicado escritorios.

2. Protección y recuperación de las implementaciones locales mediante Escritorio toodeliver de máquinas de sistema operativo de escritorio VDI para escritorios virtuales del cliente, incluida Windows 10, no se admite. Esto es porque ASR no admite la recuperación de Hola de equipos con escritorio OS'es.  Además, todavía no se admiten algunos tipos de escritorio virtual de cliente (por ejemplo, Windows 7) para la concesión de licencias en Azure. Aquí encontrará [más información](https://azure.microsoft.com/pricing/licensing-faq/) acerca de la concesión de licencias a escritorios de cliente/servidor de Azure.

3.  Azure Site Recovery no puede replicar y proteger clones locales de MCS o PVS existentes.
Debe toorecreate estos clones usar Azure RM el aprovisionamiento de controlador de entrega.

4. No se puede proteger NetScaler con Azure Site Recovery, ya que NetScaler se basa en FreeBSD y Azure Site Recovery no admite la protección del sistema operativo de FreeBSD. ¿Necesita toodeploy y configurar un nuevo dispositivo NetScaler de mercado de Azure después de la conmutación por error tooAzure.


## <a name="replicating-virtual-machines"></a>Replicación de máquinas virtuales

Hola de hello Citrix XenApp implementación de los componentes siguientes necesita toobe protegido tooenable replicación y la recuperación.

* Protección del servidor DNS de AD
* Protección del servidor de SQL Database
* Protección del controlador de entrega de Citrix
* Protección del servidor de StoreFront
* Protección de XenApp Master (VDA)
* Protección del servidor de licencias de XenApp de Citrix


**Replicación del servidor DNS de AD**

Consulte demasiado[proteger Active Directory y DNS con Azure Site Recovery](site-recovery-active-directory.md) de guía para replicar y configurar un controlador de dominio en Azure.

**Replicación del servidor de SQL Database**

Consulte demasiado[proteger SQL Server con la recuperación ante desastres de SQL Server y Azure Site Recovery](site-recovery-sql.md) para orientación técnica detallada sobre Hola opciones recomendadas para proteger los servidores SQL.

Siga [esta guía](site-recovery-vmware-to-azure.md) toostart replicar Hola otro tooAzure de máquinas virtuales de componente.

![Protección de componentes de XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

**Configuración de proceso y red**

Después de hello equipos están protegidos (estado se muestra como "Protegido" en elementos de replicar), Hola proceso y configuración de red necesita toobe configurado.
En proceso y red > calcular propiedades, puede especificar el tamaño de nombre y de destino de la máquina virtual de Azure de Hola.
Modificar Hola nombre toocomply requisitos de Azure si necesita. También puede ver y agregar información acerca de la red de destino de hello, subred y dirección IP que se va a asignar toohello máquina virtual de Azure.

Tenga en cuenta los siguiente hello:

* Puede establecer la dirección IP de destino de Hola. Si no proporciona una dirección, Hola conmutado por error equipo usará DHCP. Si establece una dirección que no está disponible en la conmutación por error, conmutación por error de hello no funcionará. Hola la misma dirección IP de destino puede usarse para la conmutación por error si está disponible en la red de conmutación por error de prueba de Hola Hola dirección.

* Para el servidor de AD/DNS hello, conservando Hola local dirección le permite que especificar Hola igual de direcciones como servidor DNS de hello para la red Virtual de Azure de Hola.

número de Hola de adaptadores de red es dictados por tamaño de Hola que especifique para la máquina virtual de destino de hello, del siguiente modo:

*   Si el número de Hola de adaptadores de red en la máquina de origen de hello es menor o igual toohello de adaptadores permitidas para el tamaño de máquina de destino de hello, a continuación, tendrá destino Hola Hola el mismo número de adaptadores como origen de Hola.
*   Si número Hola de adaptadores para la máquina virtual de origen de hello supera número Hola permitido para el tamaño de destino de hello después máximo de tamaño de destino de Hola se usará.
* Por ejemplo, si una máquina de origen tiene dos adaptadores de red y tamaño de máquina de destino de hello es compatible con cuatro, el equipo de destino Hola tendrá dos adaptadores. Si la máquina de origen hello tiene dos adaptadores de pero hello tamaño de destino admitida solo admite un equipo de destino de Hola tendrá solo un adaptador.
*   Si la máquina virtual de hello tiene varios adaptadores de red se conectarán todos toohello misma red.
*   Si la máquina virtual de hello tiene varios adaptadores de red, a continuación, hello primera se muestra en la lista de Hola se convierte en adaptador de red predeterminada de Hola Hola máquina virtual de Azure.


## <a name="creating-a-recovery-plan"></a>Creación de un plan de recuperación

Después de habilita la replicación para máquinas virtuales de componente de XenApp hello, Hola siguiente paso es toocreate un plan de recuperación.
Un plan de recuperación agrupa las máquinas virtuales con requisitos similares para la conmutación por error y la recuperación.  

**Pasos toocreate un plan de recuperación**

1. Agregar máquinas virtuales de hello XenApp componente Hola Plan de recuperación.
2. Haga clic en Planes de recuperación > + Plan de recuperación. Proporcionar un nombre para el plan de recuperación de hello intuitiva.
3. Para las máquinas virtuales de VMware, seleccione como origen un servidor de procesos de VMware, como destino Microsoft Azure y como modelo de implementación el Administrador de recursos. Después, haga clic en Seleccionar elementos.
4. Para las máquinas virtuales de Hyper-V: Seleccionar origen como servidor de VMM, como Microsoft Azure y el modelo de implementación como el Administrador de recursos de destino y haga clic en la selección de elementos y, a continuación, seleccione VM de la implementación de XenApp Hola.

### <a name="adding-virtual-machines-toofailover-groups"></a>Agregar grupos de toofailover de máquinas virtuales

Planes de recuperación pueden ser grupos de conmutación por error de tooadd personalizados para las acciones de orden, las secuencias de comandos o manual de inicio específico. los grupos siguientes de Hola necesita plan de recuperación de toobe toohello agregada.

1. Grupo de conmutación por error 1: DNS de AD
2. Grupo de conmutación por error 2: máquinas virtuales con SQL Server
2. Grupo de conmutación por error 3: máquina virtual de imagen maestra de VDA
3. Grupo de conmutación por error 4: máquinas virtuales del controlador de entrega y del servidor de StoreFront


### <a name="adding-scripts-toohello-recovery-plan"></a>Agregar plan de recuperación de toohello de secuencias de comandos

Puede ejecutar los scripts antes o después de un grupo específico en un plan de recuperación. También puede incluir y realizar acciones manuales durante la conmutación por error.

plan de recuperación personalizada Hello es similar a Hola siguiente:

1. Grupo de conmutación por error 1: DNS de AD
2. Grupo de conmutación por error 2: máquinas virtuales con SQL Server
3. Grupo de conmutación por error 3: máquina virtual de imagen maestra de VDA

   >[!NOTE]     
   >Los pasos 4, 6 y 7 que contiene acciones manuales o de scripts son aplicable tooonly un XenApp local > entorno con catálogos MCS/PVS.

4. Acción de script o Manual del grupo 3: Hola de VDA VM maestra apagado Master VDA VM si ha conmutado tooAzure estará en estado de ejecución. toocreate con Azure ARM de hospedaje nuevos catálogos MCS, maestro de hello VDA VM es necesario toobe en detenido (Alemania asignado) estado. Hola apagar VM desde el Portal de Azure.

5. Grupo de conmutación por error 4: máquinas virtuales del controlador de entrega y del servidor de StoreFront
6. Acción manual o de script 1 del grupo 3:

    ***Agregar conexión de host de Azure RM***

    Crear conexión a host ARM de Azure en el controlador de entrega máquina tooprovision nuevos catálogos MCS en Azure. Siga los pasos de hello tal como se describe en este [artículo](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).

7. Acción manual o de script 2 del grupo 3:

    ***Volver a crear catálogos MCS en Azure***

    Hola existente MCS o PVS clones en sitio primario de hello no estará tooAzure replicada. Necesita toorecreate estos clones con hello replicaron VDA maestro y ARM de Azure de aprovisionamiento de controlador de entrega. Siga los pasos de hello tal como se describe en este [artículo](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS catálogos en Azure.

![Plan de recuperación para componentes de XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   >Puede utilizar secuencias de comandos en [ubicación](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate Hola DNS con hello conmutarán por error nuevas direcciones IP de hello > máquinas virtuales o tooattach un equilibrador de carga en hello conmutado por error la máquina virtual, si es necesario.


## <a name="doing-a-test-failover"></a>Realización de una conmutación por error de prueba

Siga [esta guía](site-recovery-test-failover-to-azure.md) toodo una conmutación por error de prueba.

![Plan de recuperación](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a>Realización de una conmutación por error

Siga [estas directrices](site-recovery-failover.md) cuando realice una conmutación por error.

## <a name="next-steps"></a>Pasos siguientes

Puede obtener [más información](https://aka.ms/citrix-xenapp-xendesktop-with-asr) sobre la replicación de implementaciones de XenApp y XenDesktop de Citrix en estas notas del producto. Mire instrucciones Hola demasiado[replicar otras aplicaciones](site-recovery-workload.md) con Site Recovery.
