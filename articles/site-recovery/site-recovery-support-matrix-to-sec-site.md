---
title: "matriz de aaaSupport para el sitio secundario de replicación tooa con Azure Site Recovery | Documentos de Microsoft"
description: Se recogen Hola admitida los sistemas operativos y los componentes de Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: raynew
ms.openlocfilehash: 0b2bbc86aff52308d5a90a56d7a3ff4286877740
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="support-matrix-for-replication-tooa-secondary-site-with-azure-site-recovery"></a>Matriz de compatibilidad para el sitio secundario de replicación tooa con Azure Site Recovery

Este artículo resume lo que se admite cuando se utiliza el sitio de Azure Site Recovery tooreplicate tooa local secundario.

## <a name="deployment-options"></a>Opciones de implementación

**Implementación** | **Servidores físicos o de VMware** | **Hyper-V (con o sin SCVMM)**
--- | --- | --- | ---
**Portal de Azure** | Máquinas virtuales de VMware toosecondary VMware sitio local.<br/><br/> Descargar hello [Guía de usuario de InMage Scout](http://download.microsoft.com/download/E/0/8/E08B3BCE-3631-4CED-8E65-E3E7D252D06D/InMage_Scout_Standard_User_Guide_8.0.1.pdf) (no disponible en hello portal de Azure). | Máquinas virtuales de Hyper-V en la nube VMM secundaria de tooa de nubes VMM local.<br></br> No se admite sin VMM  <br/><br/> Solo replicación de Hyper-V estándar. SAN no es compatible.
**Portal clásico** | Solo en el modo mantenimiento. No se pueden crear almacenes nuevos. | Solo en modo de mantenimiento<br></br> No se admite sin SCVMM.
**PowerShell** | No compatible | Compatible<br></br> No se admite sin SCVMM.

## <a name="on-premises-servers"></a>Servidores locales

### <a name="virtualization-servers"></a>Servidores de virtualización

**Implementación** | **Soporte técnico**
--- | ---
**Servidor de máquina virtual de VMware o físico** | vSphere 6.0, 5.5 o 5.1 con la última actualización
**Hyper-V (con VMM)** | VMM 2016 y VMM 2012 R2

  >[!Note]
  > Actualmente, no se admiten las nubes VMM 2016 que combinan hosts de Windows Server 2016 y 2012 R2.

### <a name="host-servers"></a>Servidores host

**Implementación** | **Soporte técnico**
--- | ---
**Servidor de máquina virtual de VMware o físico** | vCenter 5.5 o 6.0 (compatible solo con características de 5.5) 
**Hyper-V (sin VMM)** | No es una configuración admitida para la replicación de sitio secundario tooa
**Hyper-V con VMM** | Windows Server 2016 y Windows Server 2012 R2 con las últimas actualizaciones de Hola.<br/><br/> Los hosts de Windows Server 2016 deben administrarse mediante VMM 2016.

## <a name="support-for-replicated-machine-os-versions"></a>Compatibilidad con las versiones de SO de las máquinas replicadas
Hello en la tabla siguiente resume la compatibilidad de sistema operativo en varios escenarios de implementación encontrado durante el uso de Azure Site Recovery. Esta compatibilidad es aplicable para cualquier carga de trabajo que se ejecutan en hello menciona el sistema operativo.

**Servidores físicos o de VMware** | **Hyper-V (con VMM)**
--- | --- | ---
Windows Server 2012 R2 de 64 bits, Windows Server 2012, Windows Server 2008 R2 con al menos SP1<br/><br/> Red Hat Enterprise Linux 6.7, 7.1 y 7.2 <br/><br/> CentOS 6.5, 6.6, 6.7, 7.0, 7.1 y 7.2 <br/><br/> Oracle Enterprise Linux 6.4 o 6.5 ejecuta kernel compatible de Red Hat de Hola o separable Enterprise Kernel versión 3 (UEK3) <br/><br/> SUSE Linux Enterprise Server 11 SP3 | Cualquier sistema operativo invitado [compatible con Hyper-V](https://technet.microsoft.com/library/mt126277.aspx)

>[!Note]
>Se pueden replicar sola máquinas de Linux con hello después de almacenamiento: filesystem (EXT3, ETX4, ReiserFS, XFS); Asignador de múltiples rutas de acceso de dispositivo de software; Administrador de volúmenes (LVM2).
>No se admiten servidores físicos con almacenamiento de controlador HP CCISS.
>sistema de archivos de Hello ReiserFS solo se admite en SUSE Linux Enterprise Server 11 SP3.

## <a name="network-configuration"></a>Network configuration (Configuración de red)

### <a name="hosts"></a>Hosts

**Configuración** | **Servidores físicos o de VMware** | **Hyper-V (con VMM)**
--- | --- | ---
Formación de equipos NIC | Sí | Sí
VLAN | Sí | Sí
IPv4 | Sí | Sí
IPv6 | No | No

### <a name="guest-vms"></a>VM invitadas

**Configuración** | **Servidores físicos o de VMware** | **Hyper-V (con VMM)**
--- | --- | ---
Formación de equipos NIC | No | No
IPv4 | Sí | Sí
IPv6 | No | No
Dirección IP estática (Windows) | Sí | Sí
Dirección IP estática (Linux) | Sí | Sí
Varias NIC | Sí | Sí


## <a name="storage"></a>Almacenamiento

### <a name="host-storage"></a>Almacenamiento de host

**Almacenamiento (host)** | **Servidores físicos o de VMware** | **Hyper-V (con VMM)**
--- | --- | ---
NFS | Sí | N/D
SMB 3.0 | N/D | Sí
SAN (ISCSI) | Sí | Sí
Varias rutas (MPIO) | Sí | Sí

### <a name="guest-or-physical-server-storage"></a>Almacenamiento de servidor físico o invitado

**Configuración** | **Servidores físicos o de VMware** | **Hyper-V (con VMM)**
--- | --- | ---
VMDK | Sí | N/D
VHD/VHDX | N/D | Sí (los discos de too16)
VM de 2 generación | N/D | Sí
Disco en clúster compartido | Sí  | No
Disco cifrado | No | No
UEFI| No | N/D
NFS | No | No
SMB 3.0 | No | No
RDM | Sí | N/D
Disco > 1 TB | No | Sí
Volumen con disco en bandas > 1 TB<br/><br/> LVM | Sí | Sí
Espacios de almacenamiento | No | Sí
Agregar/quitar disco en caliente | No | No
Excluir el disco | No | Sí
Varias rutas (MPIO) | N/D | Sí

## <a name="vaults"></a>Almacenes

**Acción** | **Servidores físicos o de VMware** | **Hyper-V (con VMM)**
--- | --- | ---
Migrar los almacenes entre los grupos de recursos (dentro de las suscripciones o entre ellas) | No | No
Migrar el almacenamiento, la red y las VM de Azure entre los grupos de recursos (dentro de las suscripciones o entre ellas) | No | No

## <a name="provider-and-agent"></a>Proveedor y agente

**Name** | **Descripción** | **La versión más reciente** | **Detalles**
--- | --- | --- | --- | ---
**Proveedor de Azure Site Recovery** | Coordina las comunicaciones entre los servidores locales y Azure <br/><br/> Se instala en servidores VMM locales o en servidores de Hyper-V si no hay ningún servidor VMM | 5.1.19 ([disponible en el portal](http://aka.ms/downloaddra)) | [Características y correcciones más recientes](https://support.microsoft.com/kb/3155002)
**Servicio de movilidad** | Coordina la replicación entre servidores de VMware locales o servidores físicos y sitio secundario de Hola<br/><br/> Instalar en VM de VMware o en servidores físicos que desea tooreplicate  | N/D (disponible en el portal) | N/D


## <a name="next-steps"></a>Pasos siguientes

- [Replicar máquinas virtuales de Hyper-V en el sitio secundario de tooa de nubes VMM](site-recovery-vmm-to-vmm.md)
- [Replicar máquinas virtuales de VMware y el sitio secundario de tooa de servidores físicos](site-recovery-vmware-to-vmware.md)
