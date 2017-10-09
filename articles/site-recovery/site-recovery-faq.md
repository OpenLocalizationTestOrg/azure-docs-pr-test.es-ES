---
title: "Azure Site Recovery: Preguntas más frecuentes (P+F) | Microsoft Docs"
description: "En este artículo se analizan las preguntas más frecuentes acerca de Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5cdc4bcd-b4fe-48c7-8be1-1db39bd9c078
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/22/2017
ms.author: raynew
ms.openlocfilehash: 6d0bd2475466e5745e1f084bd2267d954d624ebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-frequently-asked-questions-faq"></a>Azure Site Recovery: preguntas más frecuentes (P+F)
En este artículo se incluyen las preguntas más frecuentes sobre Azure Site Recovery. Si tiene alguna pregunta después de leer este artículo, expóngalos en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).

## <a name="general"></a>General
### <a name="what-does-site-recovery-do"></a>¿Qué hace Site Recovery?
Site Recovery contribuye tooyour la continuidad del negocio y estrategia de recuperación (BCDR), mediante la orquestación y automatización de la replicación de máquinas virtuales de Azure entre regiones, máquinas virtuales en locales y servidores físicos tooAzure y tooa máquinas locales Centro de datos secundario. [Más información](site-recovery-overview.md).

### <a name="what-can-site-recovery-protect"></a>¿Qué se puede proteger con Site Recovery?
* **Máquinas virtuales de Azure**: Site Recovery puede replicar cualquier carga de trabajo que se ejecute en una máquina virtual de Azure compatible.
* **Máquinas virtuales de Hyper-V**: Site Recovery puede proteger cualquier carga de trabajo que se ejecute en una máquina virtual de Hyper-V.
* **Servidores físicos**: Site Recovery puede proteger servidores físicos con Windows o Linux.
* **Máquinas virtuales de VMware**: Site Recovery puede proteger cualquier carga de trabajo que se ejecute en una máquina virtual de VMware.

### <a name="does-site-recovery-support-hello-azure-resource-manager-model"></a>¿Admite recuperación del sitio modelo de hello Azure Resource Manager?
Recuperación de sitio está disponible en hello portal de Azure con compatibilidad para el Administrador de recursos. Recuperación de sitio admite implementaciones heredadas en hello portal de Azure clásico. No se puede crear almacenes nuevos en el portal clásico de hello y no se admiten nuevas características.

### <a name="can-i-replicate-azure-vms"></a>¿Puedo replicar máquinas virtuales de Azure?
Sí, puede replicar máquinas virtuales de Azure compatibles entre regiones de Azure. [Más información](site-recovery-azure-to-azure.md).

### <a name="what-do-i-need-in-hyper-v-tooorchestrate-replication-with-site-recovery"></a>¿Qué es necesario en la replicación de Hyper-V tooorchestrate con Site Recovery?
Para el servidor de host de Hyper-V de hello lo que necesita depende de escenario de implementación de Hola. Desproteger Hola de requisitos previos de Hyper-V en:

* [Replicación de máquinas virtuales de Hyper-V (sin WMM) tooAzure](site-recovery-hyper-v-site-to-azure.md)
* [Replicación de máquinas virtuales de Hyper-V (con VMM) tooAzure](site-recovery-vmm-to-azure.md)
* [Replicación de centro de datos de máquinas virtuales de Hyper-V tooa secundario](site-recovery-vmm-to-vmm.md)
* Si replica secundaria tooa centro de datos que conozca [admite los sistemas operativos invitados para máquinas virtuales de Hyper-V](https://technet.microsoft.com/library/mt126277.aspx).
* Si replica tooAzure, Site Recovery es compatible con todos los sistemas de operativos de invitado de Hola que son [compatible con Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx).

### <a name="can-i-protect-vms-when-hyper-v-is-running-on-a-client-operating-system"></a>¿Se pueden proteger las máquinas virtuales cuando se ejecuta Hyper-V en un sistema operativo cliente?
No, las máquinas virtuales deben estar ubicadas en un servidor host de Hyper-V en el que se esté ejecutando una máquina de servidor de Windows compatible. Si necesita tooprotect un equipo cliente podría replicarla como una máquina física demasiado[Azure](site-recovery-vmware-to-azure.md) o un [centro de datos secundario](site-recovery-vmware-to-vmware.md).

### <a name="what-workloads-can-i-protect-with-site-recovery"></a>¿Qué cargas de trabajo se pueden proteger con Site Recovery?
Puede utilizar Site Recovery tooprotect mayoría cargas de trabajo ejecutándose en un servidor físico o máquina virtual compatible. Recuperación de sitio proporciona compatibilidad para la replicación consciente de las aplicaciones, ya que las aplicaciones se pueden recuperar tooan inteligente estado. Se integra con aplicaciones de Microsoft como SharePoint, Exchange, Dynamics, SQL Server y Active Directory; además, colabora estrechamente con los principales proveedores, como Oracle, SAP, IBM y Red Hat. [Obtenga más información](site-recovery-workload.md) acerca de la protección de la carga de trabajo.

### <a name="do-hyper-v-hosts-need-toobe-in-vmm-clouds"></a>¿Es necesario hosts de Hyper-V toobe en nubes de VMM?
Si desea centro de datos secundario de tooreplicate tooa, a continuación, las máquinas virtuales de Hyper-V deben estar en Hyper-V aloja servidores ubicados en una nube de VMM. Si desea tooreplicate tooAzure, puede replicar las máquinas virtuales en los servidores de host de Hyper-V con o sin nubes de VMM. [Más información](site-recovery-hyper-v-site-to-azure.md).

### <a name="can-i-deploy-site-recovery-with-vmm-if-i-only-have-one-vmm-server"></a>¿Se puede implementar Site Recovery con VMM si solo se tiene un servidor de VMM?

Sí. O bien puede replicar las máquinas virtuales de servidores de Hyper-V en tooAzure de nube VMM hello, o puede replicar entre nubes VMM en hello mismo servidor. En la replicación de tooon local en local, se recomienda tener un servidor VMM en ambos sitios primarios y secundarios de Hola.  

### <a name="what-physical-servers-can-i-protect"></a>¿Qué servidores físicos se pueden proteger?
Puede replicar servidores físicos que ejecutan Windows y Linux tooAzure o tooa sitio secundario. [Obtenga información](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) acerca de los requisitos del sistema operativo.  Hola aplican los mismos requisitos si está replicando tooAzure servidores físicos, o un sitio secundario de tooa.


Tenga en cuenta que los servidores físicos se ejecutarán como máquinas virtuales en Azure si se desactiva el servidor local. Conmutación por recuperación tooan local de servidor físico no se admite actualmente. Para un equipo protegido como física, puedes solo conmutación por recuperación tooa máquina virtual de VMware.

### <a name="what-vmware-vms-can-i-protect"></a>¿Qué máquinas virtuales de VMware se pueden proteger?

máquinas virtuales de VMware tooprotect necesitará un hipervisor de vSphere y máquinas virtuales que ejecutan las herramientas de VMware. También se recomienda que tengan un hipervisores de VMware vCenter server toomanage Hola. [Obtener más información](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) sobre requisitos concretos para la replicación de servidores de VMware y tooAzure de las máquinas virtuales o tooa de sitio secundario.


### <a name="can-i-manage-disaster-recovery-for-my-branch-offices-with-site-recovery"></a>¿Es posible administrar la recuperación ante desastres para las sucursales con Site Recovery?
Sí. Cuando se usa replicación de Site Recovery tooorchestrate y conmutación por error en sus sucursales, obtendrá una orquestación unificada y una vista de todas las cargas de trabajo de oficina sucursal en una ubicación central. Fácilmente puede ejecutar conmutaciones por error y administrar la recuperación ante desastres de todas las ramas de la oficina principal, sin necesidad de visitar bifurcaciones Hola.

## <a name="pricing"></a>Precios

### <a name="what-charges-do-i-incur-while-using-azure-site-recovery"></a>¿En qué cargos se incurre al utilizar Azure Site Recovery?
Cuando se utiliza la recuperación del sitio, se incurre en cargos de licencia de Site Recovery hello, almacenamiento de Azure, las transacciones de almacenamiento y transferencia de datos de salida. [Más información](https://azure.microsoft.com/pricing/details/site-recovery).

licencia de Site Recovery Hello es por instancia protegido, donde una instancia es una máquina virtual o un servidor físico.

- Si un disco de máquina virtual replica tooa cuenta de almacenamiento estándar, Hola cargo de almacenamiento de Azure está destinado al consumo de almacenamiento de Hola. Por ejemplo, si el tamaño del disco de origen de hello es 1 TB y 400 GB se utiliza, Site Recovery crea un disco duro virtual de 1 TB en Azure, pero almacenamiento Hola cobrado es 400 GB (más cantidad de Hola de espacio de almacenamiento que se utiliza para los registros de replicación).
- Si un disco de máquina virtual replica tooa cuenta de almacenamiento premium, Hola cargo de almacenamiento de Azure es para el tamaño de almacenamiento de hello aprovisionado, redondeado para hello más cercano de la opción de disco de almacenamiento premium. Por ejemplo, si el tamaño del disco de origen de hello es de 50 GB, Site Recovery crea un disco de 50 GB en Azure y Azure asigna este toohello más cercano de disco de almacenamiento premium (P10).  Los costos se calculan en P10 y no en el tamaño del disco de 50 GB de Hola.  [Más información](https://aka.ms/premium-storage-pricing).  Si usa almacenamiento premium, también se requiere una cuenta de almacenamiento estándar para el registro de replicación y también se factura la cantidad de hello del espacio de almacenamiento estándar usan estos registros.
- No se crean discos hasta que se produce una conmutación por error de prueba o una conmutación por error. En el estado de replicación de hello, almacenamiento cargos por categoría Hola "blob en páginas como disco" según hello [Calculadora de precios de almacenamiento](https://azure.microsoft.com/en-in/pricing/calculator/) se incurre en ellos. Estos cargos se basan en el tipo de almacenamiento de hello hello y premium y standard de redundancia de datos escriba - LRS, GRS, RA-GRS etcetera.
- Si Hola opción toouse discos administrados en una conmutación por error está activada, [cargos para discos administrados](https://azure.microsoft.com/en-in/pricing/details/managed-disks/) aplicar después de una conmutación por error de conmutación por error y pruebas. No se aplican los cargos por discos administrados durante la replicación.
- Si no se selecciona Hola opción toouse administrar discos en una conmutación por error, almacenamiento cargos por categoría de Hola "blob en páginas como disco" según hello [Calculadora de precios de almacenamiento](https://azure.microsoft.com/en-in/pricing/calculator/) se generan después de la conmutación por error. Estos cargos se basan en el tipo de almacenamiento de hello hello y premium y standard de redundancia de datos escriba - LRS, GRS, RA-GRS etcetera.
- Las transacciones de almacenamiento se cargan durante la replicación en estado estable y por las operaciones normales de máquina virtual después de una conmutación por error o conmutación por error de prueba. Pero estos cargos son insignificantes.

También se incurre en costos durante la conmutación por error de prueba, donde se aplicarán los costos de las transacciones de VM, almacenamiento, almacenamiento y salida de hello.



## <a name="security"></a>Seguridad
### <a name="is-replication-data-sent-toohello-site-recovery-service"></a>¿Se envían datos de replicación de servicio de Site Recovery toohello?
No, Site Recovery no intercepta los datos replicados ni tiene información sobre lo que se ejecuta en sus máquinas virtuales o servidores físicos.
Los datos de replicación se intercambian entre hosts locales de Hyper-V, hipervisores de VMware o servidores físicos y el Almacenamiento de Azure en el sitio secundario. Site Recovery no tiene ninguna capacidad toointercept esos datos. Solo los metadatos de hello necesarios tooorchestrate replicación y conmutación por error se envía el servicio de Site Recovery toohello.  

Recuperación de sitio es ISO 27001: 2013, 27018, HIPAA, DPA certificadas y está en proceso de Hola de evaluaciones de SOC2 y FedRAMP JAB.

### <a name="for-compliance-reasons-even-our-on-premises-metadata-must-remain-within-hello-same-geographic-region-can-site-recovery-help-us"></a>Por motivos de cumplimiento, incluso los metadatos locales deben permanecer dentro de hello misma región geográfica. ¿Site Recovery puede ayudarnos?
Sí. Cuando se crea un almacén de Site Recovery en una región, es asegurarse de que todos los metadatos que se necesita tooenable y coordinar la replicación y conmutación por error sigue siendo de esa región 's geográfica límite.

### <a name="does-site-recovery-encrypt-replication"></a>¿Site Recovery cifra la replicación?
Al replicar máquinas virtuales y servidores físicos entre sitios locales, se admite el cifrado en tránsito. Para máquinas virtuales y servidores físicos que se replican tooAzure, cifrado en tránsito y [cifrado en reposo (en Azure)](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) son compatibles.

## <a name="replication"></a>Replicación

### <a name="can-i-replicate-over-a-site-to-site-vpn-tooazure"></a>¿Replicar a través de un tooAzure VPN de sitio a sitio?
Azure Site Recovery replica datos tooan cuenta de almacenamiento Azure, a través de un punto de conexión público. La replicación no se realiza a través de una VPN de sitio a sitio. Puede crear una VPN de sitio a sitio con una instancia de Azure Virtual Network. Esto no interfiere con la replicación de Site Recovery.

### <a name="can-i-use-expressroute-tooreplicate-virtual-machines-tooazure"></a>¿Puedo usar ExpressRoute tooreplicate máquinas virtuales tooAzure?
Sí, ExpressRoute puede ser usado tooreplicate tooAzure de máquinas virtuales. Azure Site Recovery replica datos tooan cuenta de almacenamiento de Azure a través de un punto de conexión público. Necesita tooset [emparejamiento público](../expressroute/expressroute-circuit-peerings.md#public-peering) toouse ExpressRoute para la replicación de Site Recovery. Después de hello las máquinas virtuales se han conmutado tooan red virtual de Azure puede tener acceso a ellos mediante hello [emparejamiento privado](../expressroute/expressroute-circuit-peerings.md#private-peering) el programa de instalación con hello red virtual de Azure.

### <a name="are-there-any-prerequisites-for-replicating-virtual-machines-tooazure"></a>¿Existen todos los requisitos previos para la replicación de máquinas virtuales tooAzure?
Deben cumplir las máquinas virtuales que desee tooreplicate tooAzure [requisitos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

Su cuenta de usuario de Azure necesita toohave determinados [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la replicación de una nueva tooAzure de máquina virtual.

### <a name="can-i-replicate-hyper-v-generation-2-virtual-machines-tooazure"></a>¿Puedo replicar tooAzure de 2 máquinas virtuales de generación de Hyper-V?
Sí. Recuperación de sitio se convierte de generación 2 toogeneration 1 durante la conmutación por error. En la conmutación por recuperación máquina hello es convertido toogeneration back-2. [Más información](http://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/).

### <a name="if-i-replicate-tooazure-how-do-i-pay-for-azure-vms"></a>¿Si se replica tooAzure cómo paga para máquinas virtuales de Azure?
Durante la replicación normal, datos están el almacenamiento de Azure toogeo redundantes replicado y no es necesario toopay cualquier cargo de máquina virtual de IaaS de Azure, que proporciona una ventaja considerable. Al ejecutar una conmutación por error tooAzure, Site Recovery automáticamente crea máquinas virtuales de IaaS de Azure y, después de que facturarán para recursos de proceso de Hola que utilizas en Azure.

### <a name="can-i-automate-site-recovery-scenarios-with-an-sdk"></a>¿Se pueden automatizar escenarios de Site Recovery con un SDK?
Sí. Puede automatizar flujos de trabajo de recuperación del sitio mediante API de Rest de hello, PowerShell o hello Azure SDK. Escenarios admitidos actualmente para la implementación de Site Recovery con PowerShell:

* [Replicar máquinas virtuales de Hyper-V en nubes de VMM tooAzure Administrador de recursos de PowerShell](site-recovery-vmm-to-azure-powershell-resource-manager.md)
* [Replicar máquinas virtuales de Hyper-V sin tooAzure Administrador de recursos de PowerShell VMM](site-recovery-deploy-with-powershell-resource-manager.md)

### <a name="if-i-replicate-tooazure-what-kind-of-storage-account-do-i-need"></a>¿Si se replican tooAzure qué tipo de cuenta de almacenamiento necesito?
* **Portal de Azure clásico**: si va a implementar recuperación del sitio de portal de Azure clásico de Hola, necesitará un [cuenta de almacenamiento con redundancia geográfica estándar](../storage/common/storage-redundancy.md#geo-redundant-storage). El Almacenamiento premium no se admite actualmente. cuenta de Hello debe estar en hello misma región que el almacén de Site Recovery Hola.
* **Portal de Azure**: si va a implementar recuperación del sitio de hello portal de Azure, necesitará una cuenta de almacenamiento LRS o GRS. Se recomienda GRS, para que son resistentes datos si se produce una interrupción regional, o si no se puede recuperar la región principal de Hola. cuenta de Hello debe estar en hello misma región que hello del almacén de servicios de recuperación. Almacenamiento Premium ahora se admite para VM de VMware, la máquina virtual de Hyper-V y la replicación de servidor físico, al implementar en hello portal de Azure Site Recovery.

### <a name="how-often-can-i-replicate-data"></a>¿Con qué frecuencia se pueden replicar los datos?
* **Hyper-V:** las máquinas virtuales de Hyper-V se pueden replicar cada 30 segundos (excepto en el caso de Premium Storage), 5 minutos o 15 minutos. Si ha configurado la replicación de SAN, la replicación es sincrónica.
* **VMware y servidores físicos:** en este caso no es relevante la frecuencia de replicación. La replicación es continua.

### <a name="can-i-extend-replication-from-existing-recovery-site-tooanother-tertiary-site"></a>¿Puedo extender la replicación de sitio tooanother terciaria sitio de recuperación existente?
No se admite la replicación extendida o encadenada. Solicite esta característica en el [foro de comentarios](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6097959-support-for-exisiting-extended-replication).

### <a name="can-i-do-an-offline-replication-hello-first-time-i-replicate-tooazure"></a>¿Puedo hacer una Hola de replicación sin conexión primera vez que se replican tooAzure?
No es una opción admitida. Solicitar esta característica en hello [foro de comentarios](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6227386-support-for-offline-replication-data-transfer-from).

### <a name="can-i-exclude-specific-disks-from-replication"></a>¿Se pueden excluir discos específicos de la replicación?
Esto se admite cuando esté [replicar máquinas virtuales de VMware y las máquinas virtuales de Hyper-V](site-recovery-exclude-disk.md) tooAzure, con hello portal de Azure.

### <a name="can-i-replicate-virtual-machines-with-dynamic-disks"></a>¿Se pueden replicar máquinas virtuales con discos dinámicos?
Los discos dinámicos se admiten al replicar máquinas virtuales de Hyper-V. También se admiten al replicar las máquinas virtuales de VMware y tooAzure máquinas físicas. disco del sistema operativo Hola debe ser un disco básico.

### <a name="can-i-add-a-new-machine-tooan-existing-replication-group"></a>¿Puedo agregar un nueva máquina tooan grupo de replicación existente?
Se admite la adición de nuevos grupos de replicación de máquinas tooexisting. por lo tanto, toodo Seleccionar grupo de replicación de hello (de 'Elementos replicadas' hoja) y menú contextual de o seleccionar haga clic en el grupo de replicación de Hola y seleccione opción apropiada de Hola.

![Agregar grupo de tooreplication](./media/site-recovery-faq/add-server-replication-group.png)

### <a name="can-i-throttle-bandwidth-allotted-for-hyper-v-replication-traffic"></a>¿Puedo limitar el ancho de banda asignado para el tráfico de replicación de Hyper-V?
Sí. Puede leer más acerca de la limitación de ancho de banda en los artículos de implementación de hello:

* [Capacity planning for replicating VMware VMs and physical servers](site-recovery-plan-capacity-vmware.md)
* [Capacity planning for replicating Hyper-V VMs in VMM clouds](site-recovery-vmm-to-azure.md#capacity-planning)
* [Capacity planning for replicating Hyper-V VMs without VMM](site-recovery-hyper-v-site-to-azure.md)

## <a name="failover"></a>Conmutación por error
### <a name="if-im-failing-over-tooazure-how-do-i-access-hello-azure-virtual-machines-after-failover"></a>Si me conmuta por error tooAzure, ¿cómo obtengo acceso hello Azure máquinas virtuales después de la conmutación por error?
Puede tener acceso a Hola máquinas virtuales de Azure a través de una conexión a Internet segura, a través de una VPN de sitio a sitio o a través de ExpressRoute de Azure. Necesitará tooprepare varias cosas en orden tooconnect. [Más información](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)


### <a name="if-i-fail-over-tooazure-how-does-azure-make-sure-my-data-is-resilient"></a>¿Si conmutar por error tooAzure cómo Azure Asegúrese de que están resistentes Mis datos?
Azure está diseñado para la resistencia. Recuperación de sitio ya se ha diseñado para conmutación por error tooa Azure centro de datos secundario, con arreglo a Hola surge de SLA de Azure si necesita Hola. Si esto sucede, nos aseguramos de sus metadatos y almacenes permanecen dentro de hello misma región geográfica que eligió para el almacén.  

### <a name="if-im-replicating-between-two-datacenters-what-happens-if-my-primary-datacenter-experiences-an-unexpected-outage"></a>Si se replica entre dos centros de datos, ¿qué ocurre si el centro de datos principal experimenta una interrupción inesperada?
Puede desencadenar una conmutación por error no planeada desde el sitio secundario de Hola. Recuperación de sitio no tiene conectividad de hello sitio primario tooperform Hola conmutación por error.

### <a name="is-failover-automatic"></a>¿La conmutación por error es automática?
La conmutación por error no es automática. Iniciar las conmutaciones por error con solo un clic en el portal de hello, o puede usar [PowerShell de recuperación de sitio](/powershell/module/azurerm.siterecovery) tootrigger una conmutación por error. Errores nuevo es una acción simple hello portal de Site Recovery.

tooautomate que puede usar Orchestrator u Operations Manager toodetect un error de la máquina virtual local, y luego desencadenador Hola conmutación por error utilizando Hola SDK.

* [Obtenga más información](site-recovery-create-recovery-plans.md) sobre los planes de recuperación.
* [Más información](site-recovery-failover.md) acerca de la conmutación por error.
* [Más información](site-recovery-failback-azure-to-vmware.md) acerca de la conmutación por recuperación de servidores físicos y máquinas virtuales de VMware

### <a name="if-my-on-premises-host-is-not-responding-or-crashed-can-i-failover-back-tooa-different-host"></a>¿Si mi host local no responde o se ha bloqueado, se puede conmutar por error tooa espera otro host?
Sí, puede usar Hola ubicación alternativa toofailback tooa otro host de recuperación de Azure. Leer más acerca de las opciones de Hola Hola vínculos de abajo para las máquinas virtuales de Hyper-v y VMware.

* [Para máquinas virtuales de VMware](site-recovery-how-to-failback-azure-to-vmware.md#fail-back-to-the-original-or-alternate-location)
* [Para máquinas virtuales de Hyper-v](site-recovery-failback-from-azure-to-hyper-v.md#failback-to-an-alternate-location)

## <a name="service-providers"></a>Proveedores de servicios
### <a name="im-a-service-provider-does-site-recovery-work-for-dedicated-and-shared-infrastructure-models"></a>Soy un proveedor de servicios. ¿Site Recovery funciona para los modelos de infraestructura compartida o específica?
Sí, Site Recovery admite ambos modelos de infraestructura, dedicados y compartidos.

### <a name="for-a-service-provider-is-hello-identity-of-my-tenant-shared-with-hello-site-recovery-service"></a>¿Para un proveedor de servicios, es la identidad de Hola de mi inquilino compartido con el servicio de Site Recovery Hola?
No. La identidad del inquilino permanece anónima. Los inquilinos no necesitan el portal de Site Recovery toohello de acceso. Solo el Administrador de proveedor del servicio de hello interactúa con el portal de Hola.

### <a name="will-tenant-application-data-ever-go-tooazure"></a>¿Datos de la aplicación de inquilino alguna vez irá tooAzure?
Cuando se replican entre sitios de propiedad de proveedor de servicios, datos de la aplicación nunca llegan tooAzure. Se cifran datos en tránsito y se replican directamente entre sitios del proveedor de servicios de Hola.

Si se está replicando tooAzure, se envían datos de la aplicación tooAzure almacenamiento pero no toohello servicio Site Recovery. Los datos se cifran en tránsito y permanecen cifrados en Azure.

### <a name="will-my-tenants-receive-a-bill-for-any-azure-services"></a>¿Recibirán mis inquilinos una factura por los servicios de Azure?
No. Relación de facturación de Azure es directamente con el proveedor de servicios de Hola. Los proveedores de servicios son responsables de generar facturas específicas para sus inquilinos.

### <a name="if-im-replicating-tooazure-do-we-need-toorun-virtual-machines-in-azure-at-all-times"></a>¿Si va a estoy replicar tooAzure, tenemos toorun las máquinas virtuales en Azure en todo momento?
No, datos están replicada tooan cuenta de almacenamiento de Azure en su suscripción. Al realizar una conmutación por error de prueba (obtención de detalles de recuperación ante desastres) o una conmutación por error real, Site Recovery crea automáticamente las máquinas virtuales en su suscripción.

### <a name="do-you-ensure-tenant-level-isolation-when-i-replicate-tooazure"></a>¿¿Garantizar el aislamiento del nivel del inquilino cuando se replican tooAzure?
Sí.

### <a name="what-platforms-do-you-currently-support"></a>¿Qué plataformas se admiten actualmente?
Se admite Azure Pack, el sistema de plataforma en la nube e implementaciones basadas en System Center (2012 y superiores). [Más información](https://technet.microsoft.com/library/dn850370.aspx) acerca de la integración de Azure Pack y Site Recovery.

### <a name="do-you-support-single-azure-pack-and-single-vmm-server-deployments"></a>¿Se admite un paquete Azure Pack sencillo e implementaciones de servidor VMM individuales?
Sí, puede replicar tooAzure de máquinas virtuales de Hyper-V, o entre sitios del proveedor de servicios.  Tenga en cuenta que si se replica entre sitios del proveedor de servicios, la integración de runbooks de Azure no estará disponible.

## <a name="next-steps"></a>Pasos siguientes
* Hola de lectura [información general de Site Recovery](site-recovery-overview.md)
* Obtenga información acerca de la [Arquitectura de Site Recovery](site-recovery-components.md)  
