---
title: "aaaPrerequisites para tooAzure de replicación mediante el uso de Azure Site Recovery | Documentos de Microsoft"
description: "Obtenga información sobre los requisitos previos de Hola para replicar las máquinas virtuales y máquinas físicas tooAzure mediante servicio de Azure Site Recovery Hola."
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: rajanaki
ms.openlocfilehash: 0e32ab7cd7c65a3f67ffa2f2c15af189c15b6f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replication-from-on-premises-tooazure-by-using-site-recovery"></a>Requisitos previos para la replicación desde tooAzure local mediante el uso de Site Recovery

> [!div class="op_single_selector"]
> * [Replicar desde Azure tooAzure](site-recovery-azure-to-azure-prereq.md)
> * [Replicar desde tooAzure local](site-recovery-prereq.md)

Azure Site Recovery puede ayudar a admitir la estrategia de recuperación (BCDR) de desastres y la continuidad de negocio mediante la coordinación de la replicación de una región de Azure tooanother de máquina virtual de Azure (VM). Recuperación de sitio también replica servidores físicos locales y máquinas virtuales en la nube toohello (Azure) o tooa centro de datos secundario. Si se produce una interrupción en la ubicación principal, puede conmutar tooa ubicación secundaria tookeep aplicaciones y cargas de trabajo disponibles. Puede producir un error de ubicación principal tooyour atrás cuando ubicación principal Hola devuelve toonormal operaciones. Para obtener más información sobre Site Recovery, consulte [¿Qué es Site Recovery?](site-recovery-overview.md)

En este artículo, se resumen los requisitos previos de Hola para comenzar la replicación de Site Recovery desde un tooAzure de la máquina local.

Puede publicar cualquier comentario final Hola de artículo Hola. También puede hacer preguntas técnicas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="azure-requirements"></a>Requisitos de Azure

**Requisito** | **Detalles**
--- | ---
**Cuenta de Azure** | Una [cuenta de Microsoft Azure](http://azure.microsoft.com/). Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
**Servicio Site Recovery** | Para obtener más información sobre los precios Hola servicio Azure Site Recovery, consulte [precios de Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/). |
**Azure Storage** | Necesita un toostore replicado de datos de la cuenta de almacenamiento de Azure. cuenta de almacenamiento de Hello debe estar en hello misma región que hello del almacén de servicios de recuperación de Azure. Las máquinas virtuales de Azure se crean cuando se realiza la conmutación por error.<br/><br/> Según el modelo de recursos de hello desea toouse para conmutación por error de máquina virtual de Azure, puede configurar una cuenta mediante el uso de hello [modelo de implementación de Azure Resource Manager](../storage/common/storage-create-storage-account.md) o hello [modelo de implementación clásica](../storage/common/storage-create-storage-account.md).<br/><br/>Puede usar [almacenamiento con redundancia geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) o almacenamiento con redundancia local. Se recomienda el almacenamiento con redundancia geográfica. Con el almacenamiento con redundancia geográfica, datos son resistente a errores si se produce una interrupción regional, o si no se puede recuperar la región principal de Hola.<br/><br/> Puede usar una cuenta de Azure Storage estándar o Azure Premium Storage. Normalmente, [Premium Storage](https://docs.microsoft.com/azure/storage/storage-premium-storage) se usa para las máquinas virtuales que necesitan un alto volumen constante de E/S y una latencia baja. Con este servicio, una máquina virtual puede hospedar cargas de trabajo intensivas de E/S. Si utiliza Premium Storage para los datos replicados, también necesitará una cuenta de almacenamiento estándar Una cuenta de almacenamiento estándar almacena los registros de replicación que capturen datos tooon local de los cambios en curso.<br/><br/>
**Limitaciones de almacenamiento** | No se puede mover cuentas de almacenamiento que se utilizan en el grupo de recursos distinto de Site Recovery tooa o mover el uso de tooor con otra suscripción.<br/><br/> Actualmente, replicar las cuentas de almacenamiento de toopremium en India Central y sur de India no está disponible.
**Red de Azure** | Es necesario una red de Azure, máquinas virtuales de Azure toowhich conectarse después de la conmutación por error. red de Azure Hello debe ser una en hello misma región que hello del almacén de servicios de recuperación.<br/><br/> Hola portal de Azure, puede crear una red de Azure mediante hello [modelo de implementación del Administrador de recursos](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) o hello [modelo de implementación clásica](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).<br/><br/> Si se replican desde tooAzure de System Center Virtual Machine Manager (VMM), debe establecer la asignación de red entre redes de VM de VMM y redes de Azure. Esto garantiza que las máquinas virtuales de Azure conectar redes tooappropriate después de la conmutación por error.
**Limitaciones de la red** | No se puede mover cuentas de red que se utilizan en el grupo de recursos distinto de Site Recovery tooa o mover el uso de tooor con otra suscripción.
**Asignación de red** | Si se replican máquinas virtuales Microsoft Hyper-V en nubes VMM, hay que configurar la asignación de red. Esto garantiza que las máquinas virtuales de Azure conectar redes tooappropriate cuando se crean después de la conmutación por error.

> [!NOTE]
> Hello siguientes secciones describen los requisitos previos de Hola para diversos componentes del entorno de cliente de Hola. Para obtener más información sobre la compatibilidad para configuraciones específicas, consulte hello [matriz de compatibilidad](site-recovery-support-matrix.md).
>

## <a name="disaster-recovery-of-vmware-vms-or-physical-windows-or-linux-servers-tooazure"></a>Recuperación ante desastres de máquinas virtuales de VMware o tooAzure de servidores físico de Windows o Linux
Hola de los componentes siguientes es necesario para la recuperación ante desastres de máquinas virtuales VMware o en servidores físicos de Windows o Linux. Se trata de además toohello los que se describen en [requisitos de Azure](#azure-requirements).


### <a name="configuration-server-or-additional-process-server"></a>Servidor de configuración o de proceso adicional

Configurar una máquina local como Hola configuración server tooorchestrate la comunicación entre el sitio local de Hola y Azure. máquina local de Hello también administra la replicación de datos. <br/></br>

*   **Requisitos previos de hosts de VMware vCenter o VMware vSphere**

    | **Componente** | **Requisitos** |
    | --- | --- |
    | **vSphere** | Se requieren uno o varios hipervisores de VMware vSphere.<br/><br/>Hipervisores deben estar ejecutando vSphere versión 6.0, 5.5 o 5.1, con hello actualizaciones más recientes.<br/><br/>Se recomienda que vSphere hosts y servidores vCenter ser Hola igual de red como servidor de procesos de Hola. A menos que haya configurado un servidor de proceso dedicado, esto es donde se encuentra el servidor de configuración de Hola de red de Hola. |
    | **vCenter** | Se recomienda implementar un toomanage de servidor VMware vCenter los hosts de vSphere. Se debe ejecutar vCenter versión 6.0 o 5.5, con las últimas actualizaciones de Hola.<br/><br/>**Limitación**: Site Recovery no admite la replicación entre instancias de vMotion de vCenter. Storage DRS y Storage vMotion tampoco se admiten en máquinas virtuales de destino maestras después de una operación de reprotección.||

* **Requisitos previos de máquinas replicadas**

    | **Componente** | **Requisitos** |
    | --- | --- |
    | **Máquinas locales** (máquinas virtuales VMware) | Las máquinas virtuales replicadas deben tener las herramientas de VMware instaladas y en ejecución.<br/><br/> Las máquinas virtuales deben cumplir los [requisitos previos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) para poder crear una máquina virtual de Azure.<br/><br/>La capacidad de disco de cada máquina protegida no puede ser superior a 1023 GB. <br/><br/>Un mínimo 2 GB de espacio disponible en la unidad de instalación de Hola es necesario para la instalación de componentes.<br/><br/>Si desea que la coherencia de varias máquinas de tooenable, puerto 20004 debe abrirse en firewall de hello VM local.<br/><br/>Los nombres de las máquinas deben tener entre 1 y 63 caracteres (se pueden usar letras, números y guiones). nombre de Hello debe empezar con una letra o un número y terminar por una letra o un número. <br/><br/>Después de habilitar la replicación de una máquina, puede modificar Hola nombres de Azure.<br/><br/> |
    | **Máquinas Windows** (físicas o de VMware) | Hello máquina debe ejecutar uno de los siguientes Hola admitidos sistemas operativos de 64 bits: <br/>- Windows Server 2012 R2<br/>- Windows Server 2012<br/>- Windows Server 2008 R2 con SP1 o una versión posterior<br/><br/> Hello sistema operativo debe estar instalado en el disco de la unidad C. Hola SO debe ser un disco básico de Windows y no dinámicos. disco de datos de Hello puede ser dinámico.<br/><br/>|
    | **Equipos con Linux** (físicos o VMware) | Hello máquina debe ejecutar uno de los siguientes Hola admitidos sistemas operativos de 64 bits: <br/>- Red Hat Enterprise Linux 7.2, 7.1, 6.8 o 6.7.<br/>- Centos 7.2, 7.1, 7.0, 6.8, 6.7, 6.6 o 6.5.<br/>- Servidor Ubuntu 14.04 LTS (para ver una lista de versiones de kernel compatibles con Ubuntu, consulte los [sistemas operativos que se admiten](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)).<br/>-Núcleo de oracle compatible con Enterprise Linux 6.5 ó 6.4, que se ejecuta cualquier Hola rojo Hat o separable Enterprise Kernel versión 3 (UEK3)<br/>- SUSE Linux Enterprise Server 11 SP4 o SUSE Linux Enterprise Server 11 SP3.<br/><br/>Los archivos / etc/hosts en equipos protegidos deben tener entradas que asignan nombre de host local de hello tooIP direcciones asociado con todos los adaptadores de red.<br/><br/>Después de la conmutación por error, si desea tooconnect tooan VM de Azure que ejecuta Linux mediante el uso de un cliente de Shell seguro (SSH), asegúrese de que Hola SSH del servicio en la máquina de hello protegido está establecido toostart automáticamente al iniciar el sistema. Asegúrese también de que las reglas de firewall permiten que una máquina de toohello protegido de conexión de SSH.<br/><br/>nombre de host de Hello, puntos de montaje, nombres de dispositivo y las rutas de acceso de sistema de Linux y nombres de archivo (por ejemplo, / etc / y/usr) deben estar en inglés solamente.<br/><br/>Hola siguientes directorios (si configurado como particiones independientes o sistemas de archivos) deben estar todas en hello mismo disco (disco Hola OS) en el servidor de origen de hello:<br/>- / (raíz)<br/>- /boot<br/>- /usr<br/>- /usr/local<br/>- /var<br/>- /etc<br/><br/>En estos momentos, las características de la versión 5 de XFS, como la suma de comprobación de metadatos, no son compatibles con Site Recovery en sistemas de archivos XFS. Asegúrese de que los sistemas de archivos XFS no usan ninguna característica de la versión 5. Puede usar superbloque de hello xfs_info utilidad toocheck Hola XFS para partición Hola. Si **ftype** se establece demasiado**1**, se usan características XFS v5.<br/><br/>En los servidores de Red Hat Enterprise Linux 7 y CentOS 7, utilidad de hello lsof debe estar instalado y disponible.<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-tooazure-no-vmm"></a>Recuperación ante desastres de máquinas virtuales de Hyper-V tooAzure (no hay VMM)

Hola de los componentes siguientes es necesario para la recuperación ante desastres de máquinas virtuales de Hyper-V en nubes de VMM. Se trata de además toohello los que se describen en [requisitos de Azure](#azure-requirements).

| **Requisito previo** | **Detalles** |
| --- | --- |
| **Host de Hyper-V** |Uno o más servidores locales deben ejecutar Windows Server 2012 R2 con las actualizaciones más recientes de Hola y habilitado el rol de Hyper-V de Hola o Microsoft Hyper-V Server 2012 R2.<br/><br/>Los servidores Hyper-V deben tener una o varias máquinas virtuales.<br/><br/>Servidores de Hyper-V deben ser toohello conectado Internet, ya sea directamente o a través de un servidor proxy.<br/><br/>Servidores de Hyper-V deben tener correcciones Hola se describe en el artículo de Knowledge Base hello [2961977](https://support.microsoft.com/kb/2961977) instalado.
|**Proveedor y agente**| Durante la implementación de Site Recovery, instale al proveedor de Azure Site Recovery Hola. instalación del proveedor de Hello también instala el agente de servicios de recuperación de Azure de hello en cada servidor de Hyper-V que ejecuta máquinas virtuales que desea tooprotect. <br/><br/>Mismas versiones de proveedor de Hola y el agente de Hola Hola a todos los servidores de Hyper-V en una recuperación del sitio debe tener el almacén.<br/><br/>proveedor de Hello debe tooconnect tooSite recuperación sobre Hola Internet. El tráfico puede enviarse directamente o a través de un proxy. No se admite el proxy basado en HTTPS. servidor de proxy de Hello debe permitir toohello de acceso a las siguientes direcciones URL:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/>Si tiene reglas de firewall basado en la dirección IP en el servidor de hello, asegúrese de que las reglas de hello permiten tooAzure de comunicación.<br/><br/> Permitir hello [intervalos IP del centro de datos Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)y HTTPS (puerto 443).<br/><br/> Permitir que los intervalos de direcciones IP para hello región de Azure de su suscripción y para hello US occidentales (utilizado para la administración de identidades y de control de acceso).


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooazure"></a>Recuperación ante desastres de máquinas virtuales de Hyper-V en tooAzure de nubes VMM

Hola de los componentes siguientes es necesario para la recuperación ante desastres de máquinas virtuales de Hyper-V en nubes de VMM. Se trata de además toohello los que se describen en [requisitos de Azure](#azure-requirements).

| **Requisito previo** | **Detalles** |
| --- | --- |
| **Virtual Machine Manager** |Debe tener uno o varios servidores VMM que ejecuten System Center 2012 R2 o una versión posterior. Cada uno de ellos debe tener una o varias nubes configuradas. <br/><br/>Una nube debe tener lo siguiente:<br/>- Uno o más grupos de hosts de VMM.<br/>- Uno o más servidores host de Hyper-V o clústeres en cada grupo de hosts.<br/><br/>Para obtener más información acerca de cómo configurar las nubes de VMM, consulte [cómo toocreate una nube en Virtual Machine Manager 2012](http://social.technet.microsoft.com/wiki/contents/articles/2729.how-to-create-a-cloud-in-vmm-2012.aspx). |
| **Hyper-V** |Servidores de host de Hyper-V deben ejecutar al menos Windows Server 2012 R2 con habilitado el rol de Hyper-V de Hola o Microsoft Hyper-V Server 2012 R2. las actualizaciones más recientes de Hello deben instalarse.<br/><br/> Un servidor Hyper-V debe tener una o varias máquinas virtuales.<br/><br/> Un servidor de host de Hyper-V o un clúster que incluya las máquinas virtuales que desea tooreplicate debe administrarse en una nube VMM.<br/><br/>Servidores de Hyper-V deben ser toohello conectado Internet, ya sea directamente o a través de un servidor proxy.<br/><br/>Servidores de Hyper-V deben tener correcciones Hola se describe en el artículo de Knowledge Base hello [2961977](https://support.microsoft.com/kb/2961977) instalado.<br/><br/>Servidores de host de Hyper-V tienen acceso a Internet para tooAzure de replicación de datos. |
| **Proveedor y agente** |Durante la implementación de Azure Site Recovery, instale el proveedor de Azure Site Recovery en el servidor VMM Hola. Instale el agente de Recovery Services en servidores host de Hyper-V. agente y el proveedor de hello necesitan tooconnect tooAzure directamente a través de Internet de Hola o a través de un servidor proxy. No se admite un proxy basado en HTTPS. servidor de proxy de Hello en el servidor VMM de Hola y hosts de Hyper-V debe permitir el acceso a: <br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>Si tiene reglas de firewall basado en la dirección IP en el servidor VMM hello, asegúrese de que las reglas de hello permiten tooAzure de comunicación.<br/><br/> Permitir hello [intervalos IP del centro de datos Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) y HTTPS (puerto 443).<br/><br/>Permitir que los intervalos de direcciones IP para hello región de Azure para su suscripción y para hello US occidentales (utilizado para la administración de identidades y de control de acceso).<br/><br/> |

### <a name="replicated-machine-prerequisites"></a>Requisitos previos de máquinas replicadas

| **Componente** | **Detalles** |
| --- | --- |
| **Máquinas virtuales protegidas** | Site Recovery es compatible con todos los sistemas operativos admitidos por [Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx).<br/><br/>Las máquinas virtuales deben cumplir hello [requisitos previos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) para crear una máquina virtual de Azure. Los nombres de las máquinas deben tener entre 1 y 63 caracteres (se pueden usar letras, números y guiones). nombre de Hello debe empezar con una letra o un número y terminar por una letra o un número. <br/><br/>Puede modificar nombre de la máquina virtual de hello después de habilitar la replicación para hello máquina virtual. <br/><br/> La capacidad de disco de cada máquina protegida no puede ser superior a 1023 GB. Una máquina virtual puede tener los discos de too16 (arriba too16 TB).<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooa-customer-owned-site"></a>Recuperación ante desastres de máquinas virtuales de Hyper-V en el sitio de propiedad del cliente de tooa de nubes VMM

Hola de los componentes siguientes es necesario para la recuperación ante desastres de máquinas virtuales de Hyper-V en el sitio de propiedad del cliente de tooa de nubes VMM. Se trata de además toohello los que se describen en [requisitos de Azure](#azure-requirements).

| **Componente** | **Detalles** |
| --- | --- |
| **Virtual Machine Manager** |  Se recomienda que implemente un servidor VMM en el sitio primario de Hola y el sitio secundario de Hola.<br/><br/> Puede [replicar máquinas virtuales entre nubes en un único servidor VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment). tooreplicate entre nubes en un único servidor VMM, necesita al menos dos nubes configuradas en el servidor VMM Hola.<br/><br/> Servidores VMM se deben ejecutar al menos System Center 2012 SP1, con las últimas actualizaciones de Hola.<br/><br/> Todos los servidores VMM deben tener una o varias nubes. Todas las nubes deben tener el conjunto de perfiles de capacidad de Hyper-V de Hola. <br/><br/>Las nubes deben incluir uno o varios grupos de hosts de VMM. Para obtener más información sobre cómo configurar nubes VMM, consulte [Preparación de la implementación de Azure Site Recovery](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric). |
| **Hyper-V** | Servidores de Hyper-V deben ejecutar al menos Windows Server 2012 con el rol de Hyper-V de hello habilitado y ha hello las últimas actualizaciones instaladas.<br/><br/> Un servidor Hyper-V debe tener una o varias máquinas virtuales.<br/><br/>  Servidores de host de Hyper-V deben encontrarse en los grupos host en nubes VMM principales y secundarias de Hola.<br/><br/> Si ejecuta Hyper-V en un clúster en Windows Server 2012 R2, se recomienda que instale la actualización de hello descrita en el artículo de Knowledge Base [2961977](https://support.microsoft.com/kb/2961977).<br/><br/> Si ejecuta Hyper-V en un clúster de Windows Server 2012 y tiene un clúster basado en una dirección IP estática, el agente de clúster no se creará automáticamente; Debe configurar manualmente un agente de clúster Hola. Para obtener más información sobre el agente de clúster de hello, consulte [configurar rol de agente de réplica de hello para la replicación de clúster al clúster](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx). |
| **Proveedor** | Durante la implementación de Site Recovery, instale al proveedor de Azure Site Recovery hello en servidores VMM. proveedor de Hola se comunica con Site Recovery a través de la replicación de tooorchestrate HTTPS (puerto 443). Se produce la replicación de datos entre Hola servidores principales y secundarios Hyper-V en hello LAN o a través de una conexión VPN.<br/><br/> proveedor de Hola que se ejecuta en el servidor VMM Hola necesita tener acceso a toohello las siguientes direcciones URL:<br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>el proveedor de Site Recovery Hola debe permitir la comunicación de firewall de hello VMM servidores toohello [intervalos IP del centro de datos Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)y permitir que el protocolo de hello HTTPS (puerto 443). |


## <a name="url-access"></a>Acceso a direcciones URL
Estas direcciones URL deben estar disponibles desde los servidores host de Hyper-V, VMM y VMware:

|**URL** | **TooVMM VMM** | **TooAzure VMM** | **TooAzure de Hyper-V** | **TooAzure de VMware** |
|--- | --- | --- | --- | --- |
|``*.accesscontrol.windows.net`` | PERMITIR | Permitir | Permitir | Permitir |
|``*.backup.windowsazure.com`` | No se requiere | Permitir | Permitir | Permitir |
|``*.hypervrecoverymanager.windowsazure.com`` | Permitir | Permitir | Permitir | Permitir |
|``*.store.core.windows.net`` | Permitir | Permitir | Permitir | Permitir |
|``*.blob.core.windows.net`` | No se requiere | Permitir | Permitir | Permitir |
|``https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi`` | No se requiere | No se requiere | No se requiere | Permitir la descarga SQL |
|``time.windows.com`` | PERMITIR | Permitir | Permitir | Permitir|
|``time.nist.gov`` | Permitir | Permitir | Permitir | PERMITIR |
