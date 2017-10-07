---
title: matriz de compatibilidad de Site Recovery aaaAzure para replicar tooAzure | Documentos de Microsoft
description: Se recogen Hola admitida los sistemas operativos y los componentes de Azure Site Recovery
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: rajanaki
ms.openlocfilehash: eae1db2ff1392d272f6b2eb0e3410da19d09da7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-support-matrix-for-replicating-from-on-premises-tooazure"></a>Matriz de compatibilidad de Azure Site Recovery para replicar desde tooAzure local


Este artículo resumen los componentes y las configuraciones admitidas para Azure Site Recovery al replicar y recuperar tooAzure. Para obtener más información acerca de los requisitos de Azure Site Recovery, vea hello [requisitos previos](site-recovery-prereq.md).


## <a name="support-for-deployment-options"></a>Compatibilidad con opciones de implementación

**Implementación** | **Servidores físicos o de VMware** | **Hyper-V (con o sin Virtual Machine Manager)** |
--- | --- | ---
**Portal de Azure** | Almacenamiento de tooAzure de máquinas virtuales VMware, con el Administrador de recursos de Azure o almacenamiento clásico y redes locales.<br/><br/> Conmutación por error tooResource clásicas o basado en el Administrador de máquinas virtuales. | Almacenamiento de tooAzure de máquinas virtuales de Hyper-V, con el Administrador de recursos o almacenamiento clásico y redes locales.<br/><br/> Conmutación por error tooResource clásicas o basado en el Administrador de máquinas virtuales.
**Portal clásico** | Solo en el modo mantenimiento. No se pueden crear almacenes nuevos. | Solo en el modo mantenimiento.
**PowerShell** | No se admite actualmente. | Compatible


## <a name="support-for-datacenter-management-servers"></a>Compatibilidad con servidores de administración de centro de datos

### <a name="virtualization-management-entities"></a>Entidades de administración de virtualización

**Implementación** | **Soporte técnico**
--- | ---
**Servidor de máquina virtual de VMware o físico** | vCenter 6.5, 6.0 o 5.5
**Hyper-V (con Virtual Machine Manager)** | System Center Virtual Machine Manager 2016 y System Center Virtual Machine Manager 2012 R2

  >[!Note]
  > No se admite actualmente una nube de System Center Virtual Machine Manager 2016 que combine hosts de Windows Server 2016 y 2012 R2.

### <a name="host-servers"></a>Servidores host

**Implementación** | **Soporte técnico**
--- | ---
**Servidor de máquina virtual de VMware o físico** | vSphere 6.5, 6.0 y 5.5
**Hyper-V (con o sin Virtual Machine Manager)** | Windows Server 2016 y Windows Server 2012 R2 con las actualizaciones más recientes.<br></br>Si se usa SCVMM, los hosts de Windows Server 2016 debe administrarlos SCVMM 2016.


  >[!Note]
  >No se admite actualmente un sitio de Hyper-V que combine hosts que ejecutan Windows Server 2016 y 2012 R2. Recuperación tooan ubicación alternativa para las máquinas virtuales en un host de Windows Server 2016 no se admite actualmente.

## <a name="support-for-replicated-machine-os-versions"></a>Compatibilidad con las versiones de SO de las máquinas replicadas

Debe cumplir las máquinas virtuales que están protegidas [requisitos de Azure](#failed-over-azure-vm-requirements) al replicar tooAzure.
Hello en la tabla siguiente resume la compatibilidad de sistema operativo replicadas en distintos escenarios de implementación durante el uso de Azure Site Recovery. Esta compatibilidad es aplicable para cualquier carga de trabajo que se ejecutan en hello menciona el sistema operativo.

 **Servidores físicos o de VMware** | **Hyper-V (con o sin VMM)** |
--- | --- |
Windows Server 2012 R2 de 64 bits, Windows Server 2012, Windows Server 2008 R2 con al menos SP1<br/>*Windows Server 2016*: no se admite actualmente en servidores físicos y máquinas virtuales de VMware. <br/><br/> Red Hat Enterprise Linux: too5.11 5.2, 6.1 too6.8, too7.3 7.0 <br/><br/>Ciento OS: too5.11 5.2, 6.1 too6.8, too7.3 7.0 <br/><br/>Servidor Ubuntu 14.04 LTS[ (versiones de kernel admitidas)](#supported-ubuntu-kernel-versions-for-vmwarephysical-servers)<br/><br/>Servidor Ubuntu 16.04 LTS[ (versiones de kernel admitidas)](#supported-ubuntu-kernel-versions-for-vmwarephysical-servers)<br/><br/>Oracle Enterprise Linux 6.4, 6.5 ejecuta kernel compatible de Red Hat de Hola o separable Enterprise Kernel versión 3 (UEK3) <br/><br/> SUSE Linux Enterprise Server 11 SP3 <br/><br/> SUSE Linux Enterprise Server 11 SP4 <br/>(No se admite la actualización de replicación de máquinas de SLES 11 SP3 tooSLES 11 SP4. Si se ha actualizado un equipo replicado desde SLES 11SP3 tooSLES 11 SP4, podrá necesitan replicación toodisable y proteger la máquina de hello nuevo post actualización Hola.) | Cualquier sistema operativo invitado [compatible con Azure](https://technet.microsoft.com/library/cc794868.aspx)


>[!IMPORTANT]
>(Aplicable tooVMware/física servidores que se replican tooAzure)
>
> En Red Hat Enterprise Linux Server 7 + y servidores de CentOS 7 +, 3.10.0-514 de la versión de kernel se admite a partir de la versión 9.8 de hello servicio de movilidad de recuperación del sitio de Azure.<br/><br/>
> Los clientes en el núcleo de hello 3.10.0-514 con una versión de servicio de movilidad anterior a la versión 9.8 Hola están toodisable requiere la replicación, versión de Hola de actualización de tooversion de servicio de movilidad de hello 9.8 y, a continuación, vuelva a habilitar la replicación.


### <a name="supported-ubuntu-kernel-versions-for-vmwarephysical-servers"></a>Versiones de kernel de Ubuntu admitidas para servidores VMware y Physical

**Versión** | **Versión de Mobility service** | **Versión de kernel** |
--- | --- | --- |
14.04 LTS | 9.9 | 3.13.0-24-Generic too3.13.0-117-genérico,<br/>3.16.0-25-Generic too3.16.0-77-genérico,<br/>3.19.0-18-Generic too3.19.0-80-genérico,<br/>4.2.0-18-Generic too4.2.0-42-genérico,<br/>4.4.0-21-Generic too4.4.0 75 genérica |
14.04 LTS | 9.10 | 3.13.0-24-Generic too3.13.0 121-genérica,<br/>3.16.0-25-Generic too3.16.0-77-genérico,<br/>3.19.0-18-Generic too3.19.0-80-genérico,<br/>4.2.0-18-Generic too4.2.0-42-genérico,<br/>4.4.0-21-Generic too4.4.0 81 genérica |
16.04 LTS | 9.10 | 4.4.0-21-Generic too4.4.0-81-genérico,<br/>4.8.0-34-Generic too4.8.0 56-genérica,<br/>4.10.0-14-Generic too4.10.0-24-genérico |


## <a name="supported-file-systems-and-guest-storage-configurations-on-linux-vmwarephysical-servers"></a>Sistemas de archivos compatibles y configuraciones de almacenamiento de invitado en Linux (servidores físicos/VMware)

siguiente Hola sistemas de archivos y almacenamiento del software de configuración se admite en servidores Linux que se ejecutan en servidores de VMware o físico:
* Sistemas de archivos: ext3, ext4, ReiserFS (solo Suse Linux Enterprise Server), XFS
* Administrador de volúmenes: LVM2
* Software de múltiples rutas: asignador de dispositivos

No se admiten dispositivos de almacenamiento de paravirtualizados (dispositivos exportados por controladores paravirtualizados).<br/>
No se admiten dispositivos de E/S de bloque multicola.<br/>
No se admiten servidores físicos con la controladora de almacenamiento HP CCISS Hola.<br/>

>[!Note]
> En Hola de servidores Linux después de directorios (si configurado como particiones/archivo-sistemas independientes) deben estar todas en hello mismo disco (disco Hola OS) en el servidor de origen de hello: / (raíz), / Boot, / usr, / usr/local, / var, / etc<br/><br/>
> Se admiten características de XFSv5 en XFS filesystems como la suma de comprobación de metadatos a partir de la versión 9.10 de hello servicio de movilidad. Si está usando características de XFSv5, asegúrese de que está ejecutando la versión 9.10 de Mobility Service o una versión posterior. Puede usar superbloque de hello xfs_info utilidad toocheck Hola XFS para partición Hola. Si ftype se establece too1, XFSv5 características se están usando.
>


## <a name="support-for-network-configuration"></a>Compatibilidad con la configuración de red
Hola las tablas siguientes resume la compatibilidad con la configuración de red en distintos escenarios de implementación que utilizan Azure Site Recovery tooreplicate tooAzure.

### <a name="host-network-configuration"></a>Configuración de red del servidor host

**Configuración** | **Servidores físicos o de VMware** | **Hyper-V (con o sin Virtual Machine Manager)**
--- | --- | ---
Formación de equipos NIC | Sí<br/><br/>No se admite cuando se replican las máquinas virtuales| Sí
VLAN | Sí | Sí
IPv4 | Sí | Sí
IPv6 | No | No

### <a name="guest-vm-network-configuration"></a>Configuración de red de la máquina virtual invitada

**Configuración** | **Servidores físicos o de VMware** | **Hyper-V (con o sin Virtual Machine Manager)**
--- | --- | ---
Formación de equipos NIC | No | No
IPv4 | Sí | Sí
IPv6 | No | No
Dirección IP estática (Windows) | Sí | Sí
Dirección IP estática (Linux) | Sí <br/><br/>Máquinas virtuales es toouse configurado DHCP en la conmutación por recuperación  | No
Varias NIC | Sí | Sí

### <a name="failed-over-azure-vm-network-configuration"></a>Configuración de red de la máquina virtual de Azure a la que se conmuta por error

**Redes de Azure** | **Servidores físicos o de VMware** | **Hyper-V (con o sin Virtual Machine Manager)**
--- | --- | ---
ExpressRoute | Sí | Sí
ILB | Sí | Sí
ELB | Sí | Sí
Traffic Manager | Sí | Sí
Varias NIC | Sí | Sí
IP reservada | Sí | Sí
IPv4 | Sí | Sí
Conservar dirección IP de origen | Sí | Sí


## <a name="support-for-storage"></a>Compatibilidad con el almacenamiento
Hola las tablas siguientes resume la compatibilidad con la configuración de almacenamiento en distintos escenarios de implementación que utilizan Azure Site Recovery tooreplicate tooAzure.

### <a name="host-storage-configuration"></a>Configuración de almacenamiento del servidor host

**Configuración** | **Servidores físicos o de VMware** | **Hyper-V (con o sin Virtual Machine Manager)**
--- | --- | --- | ---
NFS | Sí para VMware<br/><br/> No para servidores físicos | N/D
SMB 3.0 | N/D | Sí
SAN (ISCSI) | Sí | Sí
Varias rutas (MPIO)<br></br>Probado con: Microsoft DSM, EMC PowerPath 5.7 SP4, EMC PowerPath DSM para CLARiiON | Sí | Sí

### <a name="guest-or-physical-server-storage-configuration"></a>Configuración de almacenamiento del servidor físico o invitado

**Configuración** | **Servidores físicos o de VMware** | **Hyper-V (con o sin Virtual Machine Manager)**
--- | --- | ---
VMDK | Sí | N/D
VHD/VHDX | N/D | Sí
VM de 2 generación | N/D | Sí
EFI/UEFI| No | Sí
Disco en clúster compartido | No | No
Disco cifrado | No | No
NFS | No | N/D
SMB 3.0 | No | No
RDM | Sí<br/><br/> N/D para servidores físicos | N/D
Disco > 1 TB | Sí<br/><br/>Hasta 4095 GB | Sí<br/><br/>Hasta 4095 GB
Disco con tamaño de sector de 4K | Sí | Sí, compatible con máquinas virtuales de Generación 1<br/><br/>No compatible con máquinas virtuales de Generación 2
Volumen con disco en bandas > 1 TB<br/><br/> Administración de volúmenes lógicos (LVM) | Sí | Sí
Espacios de almacenamiento | No | Sí
Agregar/quitar disco en caliente | No | No
Excluir el disco | Sí | Sí
Varias rutas (MPIO) | N/D | Sí

**Almacenamiento de Azure** | **Servidores físicos o de VMware** | **Hyper-V (con o sin Virtual Machine Manager)**
--- | --- | ---
LRS | Sí | Sí
GRS | Sí | Sí
RA-GRS | Sí | Sí
Almacenamiento de acceso esporádico | No | No
Almacenamiento de acceso frecuente| No | No
Cifrado en reposo (SSE)| Sí | Sí
Premium Storage | Sí | Sí
Servicio Import/Export | No | No


## <a name="support-for-azure-compute-configuration"></a>Compatibilidad con la configuración del proceso de Azure

**Característica de proceso** | **Servidores físicos o de VMware** | **Hyper-V (con o sin Virtual Machine Manager)**
--- | --- | --- 
Conjuntos de disponibilidad | Sí | Sí
CONCENTRADOR | Sí | Sí  
Discos administrados | Sí | Sí<br/><br/>Conmutación por recuperación tooon local de la máquina virtual de Azure con discos administrados no se admite actualmente.

## <a name="failed-over-azure-vm-requirements"></a>Requisitos de la máquina virtual de Azure a la que se conmuta por error

Puede implementar máquinas virtuales de Site Recovery tooreplicate y servidores físicos que ejecutan cualquier sistema operativo compatible con Azure. Incluye la mayoría de las versiones de Windows y Linux. Máquinas virtuales que quieres tooreplicate deben cumplir con hello según los requisitos de Azure mientras se replicaba tooAzure local.

**Entidad** | **Requisitos** | **Detalles**
--- | --- | ---
**Sistema operativo invitado** | Replicación de Hyper-V tooAzure: recuperación del sitio es compatible con todos los sistemas operativos que son [compatible con Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx). <br/><br/> Para la replicación de servidor físico y VMware: comprobar Hola Windows y Linux [requisitos previos](site-recovery-vmware-to-azure-classic.md) | Se producirá un error en la comprobación de los requisitos previos si no es compatible.
**Arquitectura del sistema operativo invitado** | 64 bits | Se producirá un error en la comprobación de los requisitos previos si no es compatible.
**Tamaño del disco del sistema operativo** | Una copia de seguridad too2048 GB si se están replicando **máquinas virtuales de VMware o servidores físicos tooAzure**.<br/><br/>Hasta 2048 GB para VM de **la generación 1 de Hyper-V**.<br/><br/>Hasta 300 GB para VM de **la generación 2 de Hyper-V**.  | Se producirá un error en la comprobación de los requisitos previos si no es compatible.
**Número de discos del sistema operativo** | 1 | Se producirá un error en la comprobación de los requisitos previos si no es compatible.
**Número de discos de datos** | 64 o menos si desea replicar **tooAzure de máquinas virtuales VMware**; 16 o menos si va a replicar **tooAzure de máquinas virtuales de Hyper-V** | Se producirá un error en la comprobación de los requisitos previos si no es compatible.
**Tamaño de VHD del disco de datos** | Backup too4095 GB | Se producirá un error en la comprobación de los requisitos previos si no es compatible.
**Adaptadores de red** | Se admiten varios adaptadores |
**VHD compartido** | No compatible | Se producirá un error en la comprobación de los requisitos previos si no es compatible.
**Disco FC** | No compatible | Se producirá un error en la comprobación de los requisitos previos si no es compatible.
**Formato de disco duro** | VHD  <br/><br/> VHDX | Aunque VHDX no se admite actualmente en Azure, Site Recovery convierte automáticamente VHDX tooVHD cuando se conmuta por error tooAzure. Cuando haya un error nuevo máquinas virtuales de tooon local Hola continuar con el formato VHDX toouse Hola.
**BitLocker** | No compatible | Se debe deshabilitar BitLocker antes de proteger una máquina virtual.
**Nombre de la máquina virtual** | Entre 1 y 63 caracteres. Tooletters restringidos, números y guiones. nombre de la máquina virtual de Hello debe empezar y terminar por una letra o un número. | Actualice el valor de hello en Propiedades de la máquina virtual de hello en Site Recovery.
**Tipo de máquina virtual** | Generación 1<br/><br/> Generación 2 - Windows | Las VM de generación 2 con un tipo de disco de SO básico, que incluye uno o dos volúmenes de datos con el formato VHDX y menos de 300 GB de espacio en disco, son compatibles.<br></br>No se admiten las VM Linux de generación 2. [Más información](https://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/)|

## <a name="support-for-recovery-services-vault-actions"></a>Compatibilidad con acciones de almacén de Recovery Services

**Acción** | **Servidores físicos o de VMware** | **Hyper-V (sin Virtual Machine Manager)** | **Hyper-V (con Virtual Machine Manager)**
--- | --- | --- | ---
Mover el almacén entre grupos de recursos<br/><br/> Entre las suscripciones | No | No | No
Mover el almacenamiento, la red y las máquinas virtuales de Azure entre grupos de recursos<br/><br/> Entre las suscripciones | No | No | No


## <a name="support-for-provider-and-agent"></a>Compatibilidad con proveedores y agentes

**Name** | **Descripción** | **La versión más reciente** | **Detalles**
--- | --- | --- | --- | ---
**Proveedor de Azure Site Recovery** | Coordina las comunicaciones entre los servidores locales y Azure <br/><br/> Se instala en servidores de Virtual Machine Manager locales o en servidores de Hyper-V si no hay ningún servidor de Virtual Machine Manager | 5.1.19 ([disponible en el portal](http://aka.ms/downloaddra)) | [Características y correcciones más recientes](https://support.microsoft.com/kb/3155002)
**Configuración Azure Site Recovery unificado (tooAzure de VMware)** | Coordina las comunicaciones entre servidores de VMware locales y Azure  <br/><br/> Se instala en servidores de VMware locales | 9.3.4246.1 (disponible en el portal) | [Características y correcciones más recientes](https://support.microsoft.com/kb/3155002)
**Servicio de movilidad** | Coordina la replicación entre servidores de VMware locales o servidores físicos y el sitio secundario o Azure<br/><br/> Instalar en VM de VMware o en servidores físicos que desee tooreplicate  | N/D (disponible en el portal) | N/D
**Agente de Microsoft Azure Recovery Services (MARS)** | Coordina la replicación entre máquinas virtuales de Hyper-V y Azure<br/><br/> Se instala en servidores de Hyper-V locales (con o sin un servidor VMM) | Agente más reciente ([disponible en el portal](http://aka.ms/latestmarsagent)) |






## <a name="next-steps"></a>Pasos siguientes
[Comprobación de los requisitos previos](site-recovery-prereq.md)
