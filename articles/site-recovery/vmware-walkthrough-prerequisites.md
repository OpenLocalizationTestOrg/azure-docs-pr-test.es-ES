---
title: "aaaPrerequisites para la replicación de tooAzure de VMware con Azure Site Recovery | Documentos de Microsoft"
description: "Resume los requisitos previos de hello para la replicación de las cargas de trabajo que se ejecutan en máquinas virtuales VMware tooAzure, mediante el servicio de Azure Site Recovery Hola."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 318156ba-793b-48d0-98d4-cc5436bf28a3
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 14f8e9713b42a1d8da71223fbbb7a6b7c4303adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-vmware-tooazure-replication"></a>Paso 2: Revise los requisitos previos de hello para la replicación de tooAzure de VMware

Lea los requisitos previos de hello resumidos en hello en la tabla siguiente.

**Requisito previo** | **Detalles**
--- | ---
**Las tablas de Azure** | Aprenda acerca de los [requisitos de Azure](site-recovery-prereq.md#azure-requirements)
**Servidor de configuración local** | Necesita una máquina virtual de VMware con Windows Server 2012 R2 o posterior. Configure este servidor durante la implementación de Site Recovery.<br/><br/> Proceso predeterminado de hello server y servidor de destino maestro también se instalan en esta máquina virtual. Al escalar verticalmente, tendrá que un servidor de procesos independiente y tendrá Hola mismos requisitos que el servidor de configuración de Hola.<br/><br/> Aprenda más sobre estos componentes [aquí](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).
**Servidores de VMware locales** | Uno o más servidores de VMware vSphere, con 6.5, 6.0, 5.5 o 5.1 con las últimas actualizaciones. Servidores deben ubicarse en hello misma red que el servidor de configuración de hello (o servidor de procesos independiente).<br/><br/> Se recomienda a un servidor vCenter toomanage hosts, que se ejecutan 6.5, 6.0 ó 5.5 con las actualizaciones más recientes de Hola.
**Máquinas virtuales locales** | Las máquinas virtuales que desee tooreplicate debe estar en ejecución una [sistema operativo compatible](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)y cumplir con [requisitos previos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). Las máquinas virtuales deberían ejecutar las herramientas de VMware.
**URLs** | servidor de configuración de Hello necesita tener acceso a direcciones URL toothese:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Si tiene reglas de firewall basado en la dirección IP, asegúrate de que permiten tooAzure de comunicación.<br/></br> Permitir hello [intervalos de IP del centro de datos de Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)y Hola puerto HTTPS (443).<br/></br> Permitir que los intervalos de direcciones IP para hello región de Azure de su suscripción y oeste de Estados Unidos (utilizado para el Control de acceso y administración de identidades).<br/><br/> Permitir que esta dirección URL de descarga de MySQL de hello: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Servicio de movilidad** | Instalado en cada máquina virtual replicada.




## <a name="limitations"></a>Limitaciones

Asegúrese de que comprende las limitaciones de hello resumidas en la tabla de hello antes de implementar.

**Limitación** | **Detalles**
--- | ---
**Las tablas de Azure** | Cuentas de almacenamiento y de red deben estar en hello misma región que el almacén de Hola<br/><br/> Si usa una cuenta de almacenamiento premium, también necesita un estándar almacenar registros de replicación de toostore de cuenta<br/><br/> No se puede replicar toopremium cuentas en el centro y sur de India.
**Servidor de configuración local** | El tipo de adaptador de máquina virtual de VMware debe ser VMXNET3. Si no lo es, [instale esta actualización](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).<br/><br/> Se debe instalar vSphere PowerCLI 6.0.<br/><br> máquina de Hello no debe ser un controlador de dominio. máquina de Hello debe tener una dirección IP estática.<br/><br/> nombre de host de Hello debe ser de 15 caracteres o menos, y el sistema operativo debe estar en inglés.
**VMware** | Site Recovery no admite las nuevas características de vCenter y vSphere 6.5 y 6.0, como Cross vCenter vMotion, volúmenes virtuales y DRS de almacenamiento.
**VM** | Compruebe las [limitaciones de máquinas virtuales de Azure](site-recovery-prereq.md#azure-requirements).<br/><br/> No se pueden replicar máquinas virtuales con discos cifrados ni tampoco con arranque UEFI/EFI.<br/><br> No se admiten los clústeres de disco compartido. Si una VM de origen hello tiene la formación de equipos, se convierte tooa único NIC después de la conmutación por error.<br/><br/> Si las máquinas virtuales tengan un disco iSCSI, Site Recovery lo convierte archivos de disco duro virtual tooa después de la conmutación por error. Si el destino de iSCSI de hello pueda tener acceso mediante Hola VM de Azure, se conecta tooit y ve y Hola VHD. Si esto ocurre, desconecte el destino de iSCSI de Hola.<br/><br/> Si desea que la coherencia de varias máquinas de tooenable, lo que permite a máquinas virtuales que ejecutan Hola mismo toobe de carga de trabajo recuperado datos coherentes tooa juntos punto, abrir el puerto 20004 en hello VM.<br/><br/> Windows debe instalarse en la unidad C de Hola. debe ser el disco del sistema operativo de Hello básicos y no dinámicos. disco de datos de Hello puede ser dinámico.<br/><br/> Los archivos / etc/hosts de Linux en máquinas virtuales deben contener entradas que asignan nombre de host local de hello tooIP direcciones asociado con todos los adaptadores de red. Hola, nombre de host, los puntos de montaje, nombre de dispositivo, las rutas de acceso del sistema y los nombres de archivo (/ etcetera; / usr) debe estar en inglés solamente.<br/><br/> Se admiten tipos específicos de [almacenamiento Linux](site-recovery-support-matrix-to-azure.md#support-for-storage).<br/><br/>Crear o establecer **disk.enableUUID=true** en la configuración de máquina virtual de Hola. Esto proporciona un toohello UUID coherente VMDK, por lo que se monta correctamente y garantiza que los cambios diferenciales solo se transfieren local tooon back-durante la conmutación por recuperación, sin replicación completa.


## <a name="next-steps"></a>Pasos siguientes

- Si está realizando una implementación completa, vaya demasiado[paso 3: planear la capacidad](vmware-walkthrough-capacity.md)
- Si está realizando una implementación de prueba simple, vaya demasiado[paso 4: planear las redes](vmware-walkthrough-network.md).
