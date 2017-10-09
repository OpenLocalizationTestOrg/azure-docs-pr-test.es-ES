---
title: "aaaSet VMM y Hyper-V para el sitio secundario de replicación tooa con Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo tooset los servidores de System Center VMM y hosts de Hyper-V para el sitio VMM secundario de replicación tooa."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d0389e3b-3737-496c-bda6-77152264dd98
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 677bf6d38328ccc425e3b0f056d03159a52da428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-vmm-and-hyper-v-for-hyper-v-vm-replication-tooa-secondary-site"></a>Paso 4: Configurar VMM y Hyper-V para el sitio secundario de tooa de replicación de máquina virtual de Hyper-V 

Una vez que ha preparado para redes, configurar los servidores de System Center Virtual Machine Manager (VMM) y hosts de Hyper-V para Hyper-V máquina virtual (VM) replicación tooa sitio secundario, con [Azure Site Recovery](site-recovery-overview.md) Hola portal de Azure. 

Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="prepare-vmm-servers"></a>Preparar los servidores VMM 

tooprepare para la implementación:


1. Asegúrese de que los servidores VMM obedecer hello [admiten requisitos](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), y [requisitos previos de implementación](vmm-to-vmm-walkthrough-prerequisites.md).
2. Asegúrese de que los servidores VMM están conectado toohello internet y tener las direcciones URL de acceso toothese.
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - Si tiene reglas de firewall basado en la dirección IP, asegúrate de que permiten tooAzure de comunicación.
    - Permitir hello [intervalos de IP del centro de datos de Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)y Hola puerto HTTPS (443).
    - Permitir que los intervalos de direcciones IP para hello región de Azure de su suscripción y oeste de Estados Unidos (utilizado para el Control de acceso y administración de identidades).
3. Asegúrese de que el servidor VMM de hello [preparado para la asignación de red](vmm-to-vmm-walkthrough-network.md#prepare-for-network-mapping)


## <a name="prepare-hyper-v-hostsclusters"></a>Preparar los hosts o clústeres de Hyper-V

1. Asegúrese de que los hosts y clústeres de Hyper-V a cumplirlos Hola [admiten requisitos](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), y [requisitos previos de implementación](vmm-to-vmm-walkthrough-prerequisites.md).
2. Comprobar los requisitos de Hola para [máquinas virtuales de Hyper-V](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)
3. Compruebe los requisitos de [red](site-recovery-support-matrix-to-sec-site.md#network-configuration) y [almacenamiento](site-recovery-support-matrix-to-sec-site.md#storage).
4. Asegúrese de que los hosts de Hyper-V son toohello conectado internet y tener las direcciones URL de acceso toothese.
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - Si tiene reglas de firewall basado en la dirección IP, asegúrate de que permiten tooAzure de comunicación.
    - Permitir hello [intervalos de IP del centro de datos de Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)y Hola puerto HTTPS (443).
    - Permitir que los intervalos de direcciones IP para hello región de Azure de su suscripción y oeste de Estados Unidos (utilizado para el Control de acceso y administración de identidades).

## <a name="prepare-for-single-server-deployment"></a>Preparación para la implementación de un solo servidor


Si solo tiene un único servidor VMM, puede replicar las máquinas virtuales en hosts de Hyper-V en la nube de VMM Hola demasiado[Azure](hyper-v-site-walkthrough-overview.md) o una nube VMM secundaria tooa, tal como se describe en este documento. Se recomienda la primera opción de hello porque replicar entre nubes no es perfecta.

Si desea tooreplicate entre nubes, puede replicar con un servidor VMM única e independiente o con un solo servidor VMM implementado en un clúster de Windows con Stretch

### <a name="replicate-with-a-standalone-vmm-server"></a>Replicar con un servidor VMM independiente

En este escenario, implementar Hola único servidor de VMM como una máquina virtual en el sitio primario de Hola y replicar este sitio secundario de tooa VM con Site Recovery y réplica de Hyper-V.

1. **Configurar VMM en una máquina virtual Hyper-V**. Se recomienda la colocación de instancia de SQL Server de hello utilizado por VMM en hello misma máquina virtual. Esto ahorra tiempo ya que solo una máquina virtual tiene toobe creado. Si desea toouse la instancia remota de SQL Server y se produce una interrupción, deberá toorecover esa instancia para poder recuperar VMM.
2. **Asegúrese de servidor VMM hello tiene al menos dos nubes configuradas**. Una nube contendrá hello las máquinas virtuales que desee tooreplicate y Hola otra nube servirá como ubicación secundaria Hola. Hola en la nube que contiene máquinas virtuales de hello desea deben cumplir tooprotect [requisitos previos](#prerequisites).
3. Configure Site Recovery tal como se describe en este artículo. Crear y registrar el servidor VMM de hello en un almacén, configurar una directiva de replicación y habilitar la replicación. los nombres VMM de origen y de destino de Hola se se Hola mismo. Especificar que la replicación inicial realiza a través de red de Hola.
4. Al configurar la asignación de red asignar red de VM de Hola Hola nube principal toohello red de VM de nube secundaria Hola.
5. En la consola de administrador de Hyper-V de hello, habilitar réplica de Hyper-V en el host de Hyper-V de Hola que contiene Hola VM de VMM y habilitar la replicación en hello máquina virtual. Asegúrese de que no agregue tooclouds de máquina virtual VMM de Hola que están protegidos por recuperación del sitio, tooensure que configuración de réplica de Hyper-V no se invalidan Site Recovery.
6. Si crea planes de recuperación para conmutación por error que usa Hola mismo servidor VMM de origen y de destino.
7. En una interrupción completa, se conmuta por error y se recupera de la siguiente forma:

   1. Ejecute una conmutación por error no planeada en la consola de administrador de Hyper-V de hello en el sitio secundario hello, toofail a través del sitio secundario del principal toohello VM de VMM de Hola.
   2. Compruebe que Hola que VM de VMM está activo y ejecutándose y en el almacén de hello, ejecutar una conmutación por error imprevista toofail a máquinas virtuales de Hola de nubes toosecondary principal. Confirmar conmutación por error de Hola y seleccione un punto de recuperación alternativo si es necesario.
   3. Una vez hello conmutación por error imprevista completada, todos los recursos son accesibles desde el sitio primario de hello nuevo.
   4. Cuando hay sitio primario de Hola de nuevo, en la consola de administrador de Hyper-V de hello en el sitio secundario de hello, habilitar la replicación inversa para hello VM de VMM. Esto inicia la replicación para hello VM desde tooprimary secundaria.
   5. Ejecute una conmutación por error planeada en la consola de administrador de Hyper-V de hello en el sitio secundario hello, toofail sobre Hola sitio primario de toohello de VM de VMM. Confirmar conmutación por error de Hola. A continuación, habilitar la replicación inversa, para que hello VM de VMM se vuelva a replicar desde toosecondary principal.
   6. En el almacén de servicios de recuperación de hello, habilitar la replicación inversa para cargas de trabajo de hello las máquinas virtuales, toostart replicándolos de tooprimary secundaria.
   7. En el almacén de servicios de recuperación hello, que se ejecute un conmutación por error planeada toofail Hola back-carga de trabajo VM toohello sitio primario. Confirmar toocomplete de conmutación por error de Hola. A continuación, habilite la replicación inversa toostart replicación Hola carga de trabajo máquinas virtuales de toosecondary principal.

### <a name="replicate-with-a-stretched-vmm-cluster"></a>Replicar con un clúster de VMM estirado

En lugar de implementar un servidor VMM independiente como una máquina virtual que se replica tooa de sitio secundario, puede hacer que VMM alta disponibilidad mediante la implementación como una máquina virtual en un clúster de conmutación por error de Windows. De esta forma, se garantiza la resistencia de las cargas de trabajo y la protección frente a los errores del hardware. toodeploy con hello de Site Recovery VM de VMM debe implementarse en un clúster de stretch en sitios dispersos geográficamente. toodo esto:

1. Instalar VMM en una máquina virtual en un clúster de conmutación por error de Windows y seleccione Hola opción toorun Hola servidor como de alta disponibilidad durante la instalación.
2. instancia de SQL Server de Hello usada por VMM se debe replicar con grupos de disponibilidad AlwaysOn de SQL Server, por lo que hay una réplica de base de datos de hello en el sitio secundario de Hola.
3. Siga las instrucciones de hello en este toocreate artículo un almacén, Registrar servidor hello y configure la protección. Necesita tooregister clúster de cada servidor VMM en hello en hello del almacén de servicios de recuperación. toodo, instalar Hola proveedor en un nodo activo y registrar el servidor VMM Hola. A continuación, instalar Hola proveedor en otros nodos.
4. Cuando se produce una interrupción, servidor VMM de Hola y su base de datos de SQL Server correspondiente se conmutarán por error y se tiene acceso desde el sitio secundario de Hola.



## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 5: configurar un almacén](vmm-to-vmm-walkthrough-create-vault.md).
