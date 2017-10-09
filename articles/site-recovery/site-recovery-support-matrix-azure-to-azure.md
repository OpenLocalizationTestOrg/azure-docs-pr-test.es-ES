---
title: matriz de compatibilidad de Site Recovery aaaAzure para replicar desde Azure tooAzure | Documentos de Microsoft
description: "Resume Hola admitida los sistemas operativos y configuraciones de replicación de Azure Site Recovery de máquinas virtuales de Azure (VM) de una región tooanother para necesidades de disaster recovery (recuperación ante desastres)."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: 75b2451b4c2069ca4b11deb0efe1329d43879eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-support-matrix-for-replicating-from-azure-tooazure"></a>Matriz de compatibilidad de Azure Site Recovery para replicar desde Azure tooAzure


>[!NOTE]
>
> La replicación de Site Recovery en máquinas virtuales de Azure se encuentra actualmente en versión preliminar.

Este artículo resumen los componentes y las configuraciones admitidas para Azure Site Recovery al replicar y recuperación de máquinas virtuales de Azure desde una región tooanother otra.

## <a name="user-interface-options"></a>Opciones de la interfaz de usuario

**Interfaz de usuario** |  **Se admite/no se admite**
--- | ---
**Portal de Azure** | Compatible
**Portal clásico** | No compatible
**PowerShell** | No se admite actualmente.
**API de REST** | No se admite actualmente.
**CLI** | No se admite actualmente.


## <a name="resource-move-support"></a>Compatibilidad con el movimiento de recursos.

**Tipo de movimiento de recursos** | **Se admite/no se admite** | **Comentarios**  
--- | --- | ---
**Mover el almacén entre grupos de recursos** | No compatible |No se puede mover el almacén de servicios de recuperación de hello en grupos de recursos.
**Mover los servicios Compute, Storage y Network entre grupos de recursos** | No compatible |Si mueve una máquina virtual (o sus componentes asociados, como almacenamiento y red) después de habilitar la replicación, es necesario toodisable replicación y habilitar la replicación de máquina virtual de Hola de nuevo.


## <a name="support-for-deployment-models"></a>Compatibilidad con modelos de implementación

**Modelo de implementación** | **Se admite/no se admite** | **Comentarios**  
--- | --- | ---
**Clásico** | Compatible | Solo puede replicar una máquina virtual clásica y recuperarla como máquina virtual clásica. No puede recuperarla como una máquina virtual de Resource Manager. Si implementa una máquina virtual clásica sin una red virtual y directamente tooan región de Azure, no se admite.
**Resource Manager** | Compatible |

## <a name="support-for-replicated-machine-os-versions"></a>Compatibilidad con las versiones de SO de las máquinas replicadas

Hola por debajo del soporte es aplicable para cualquier carga de trabajo que se ejecutan en hello menciona el sistema operativo.

#### <a name="windows"></a>Windows

- Windows Server 2016 (Server Core y Server con Experiencia de escritorio)*
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 con al menos SP1

>[!NOTE]
>
> \* No se admite Windows Server 2016 Nano Server.

#### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 6.7, 6.8, 7.0, 7.1, 7.2 y 7.3
- CentOS 6.5, 6.6, 6.7, 6.8, 7.0, 7.1, 7.2, 7.3
- Servidor Ubuntu 14.04 LTS[ (versiones de kernel admitidas)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Servidor Ubuntu 16.04 LTS[ (versiones de kernel admitidas)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Oracle Enterprise Linux 6.4, 6.5 ejecuta kernel compatible de Red Hat de Hola o separable Enterprise Kernel versión 3 (UEK3)
- SUSE Linux Enterprise Server 11 SP3

>[!NOTE]
>
> Servidores Ubuntu mediante una contraseña autenticación e inicio de sesión, y con las máquinas virtuales de nube de tooconfigure de paquete de hello init de la nube, puede haber contraseña deshabilitada tras una conmutación por error (en función de configuración de cloudinit Hola.) de inicio de sesión Inicio de sesión basada en contraseña puede habilitarse de nuevo en la máquina virtual de hello mediante el restablecimiento de contraseña de Hola desde el menú de configuración de hello (bajo Hola compatibilidad + sección Solución de problemas) de hello conmutado por máquina virtual en hello portal de Azure.

### <a name="supported-ubuntu-kernel-versions-for-azure-virtual-machines"></a>Versiones de kernel de Ubuntu admitidas para máquinas virtuales de Azure

**Versión** | **Versión de Mobility service** | **Versión de kernel** |
--- | --- | --- |
14.04 LTS | 9.9 | 3.13.0-24-Generic too3.13.0-117-genérico,<br/>3.16.0-25-Generic too3.16.0-77-genérico,<br/>3.19.0-18-Generic too3.19.0-80-genérico,<br/>4.2.0-18-Generic too4.2.0-42-genérico,<br/>4.4.0-21-Generic too4.4.0 75 genérica |
14.04 LTS | 9.10 | 3.13.0-24-Generic too3.13.0 121-genérica,<br/>3.16.0-25-Generic too3.16.0-77-genérico,<br/>3.19.0-18-Generic too3.19.0-80-genérico,<br/>4.2.0-18-Generic too4.2.0-42-genérico,<br/>4.4.0-21-Generic too4.4.0 81 genérica |
16.04 LTS | 9.10 | 4.4.0-21-Generic too4.4.0-81-genérico,<br/>4.8.0-34-Generic too4.8.0 56-genérica,<br/>4.10.0-14-Generic too4.10.0-24-genérico |

## <a name="supported-file-systems-and-guest-storage-configurations-on-azure-virtual-machines-running-linux-os"></a>Sistemas de archivos y configuraciones de almacenamiento de invitado admitidos en máquinas virtuales de Azure que ejecutan el sistema operativo Linux

* Sistemas de archivos: ext3, ext4, ReiserFS (solo Suse Linux Enterprise Server), XFS
* Administrador de volúmenes: LVM2
* Software de múltiples rutas: asignador de dispositivos

## <a name="region-support"></a>Regiones admitidas

Puede replicar y recuperar las máquinas virtuales entre los dos regiones dentro de hello mismo clúster geográfico.

**Clúster geográfico** | **Regiones de Azure**
-- | --
América | Centro de Canadá y este de Canadá, centro-sur de EE. UU., centro-oeste de EE. UU., este de EE. UU., este de EE. UU. 2, oeste de EE. UU., oeste de EE. UU. 2 centro de EE. UU., centro-norte de EE. UU.
Europa | Oeste de Reino Unido, Sur de Reino Unido, Europa del Norte, Europa Occidental
Asia | India del Sur, centro de la India, Sudeste Asiático, Asia Oriental, Japón Oriental, Japón Occidental, Corea Central, Corea del Sur
Australia   | Este de Australia, Sudeste de Australia

>[!NOTE]
>
> Para la región sur de Brasil, sólo se puede replicar y realizar copias de tooone de conmutación por error de Ee.uu. Central sur, oeste Ee.uu. Central, este de EE., UU 2, oeste de EE., oeste de Estados Unidos 2 y Ee.uu. Central Norte regiones y producirá un error.


## <a name="support-for-compute-configuration"></a>Compatibilidad con la configuración de Compute

**Configuración** | **No admite/no se admite** | **Comentarios**
--- | --- | ---
Tamaño | Cualquier tamaño de máquina virtual de Azure con 2 núcleos de CPU y 1 GB de RAM | Consulte demasiado[tamaños de máquina virtual de Azure](../virtual-machines/windows/sizes.md)
Conjuntos de disponibilidad | Compatible | Si usas opción predeterminada de Hola durante el paso habilitar la replicación en el portal, conjunto de disponibilidad de hello es auto creado de acuerdo con la configuración de región de origen. Puede cambiar la disponibilidad de destino de hello establecido ' replicadas elemento > Configuración > proceso y red > conjunto de disponibilidad ' cualquier momento.
Máquinas virtuales con ventaja de uso híbrido (HUB) | Compatible | Si una VM de origen hello tiene licencia de concentrador habilitado, conmutación por error de prueba de Hola o Failover VM también utiliza licencias de base de datos central de Hola.
Conjuntos de escalado de máquinas virtuales | No compatible |
Imágenes de la galería de Azure (publicadas por Microsoft) | Compatible | Admite como Hola VM se ejecuta en un sistema operativo compatible con Site Recovery
Imágenes de la Galería de Azure (publicadas por terceros) | Compatible | Admite como Hola VM se ejecuta en un sistema operativo compatible con Site Recovery.
Imágenes personalizadas (publicados de terceros) | Compatible | Admite como Hola VM se ejecuta en un sistema operativo compatible con Site Recovery.
Máquinas virtuales migradas con Site Recovery | Compatible | Si es una máquina físicos/VMware migrado tooAzure con Site Recovery, necesita la versión anterior de hello toouninstall del servicio de movilidad y reiniciar la máquina de hello antes de replicar tooanother región de Azure.

## <a name="support-for-storage-configuration"></a>Compatibilidad con la configuración de Storage

**Configuración** | **No admite/no se admite** | **Comentarios**
--- | --- | ---
Tamaño de disco máximo del sistema operativo | 1023 GB | Consulte demasiado[discos que se utilizan en las máquinas virtuales.](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)
Tamaño máximo del disco de datos | 1023 GB | Consulte demasiado[discos que se utilizan en las máquinas virtuales.](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)
Número de discos de datos | Hasta 64, que es el admitido por un tamaño de máquina virtual específico de Azure. | Consulte demasiado[tamaños de máquina virtual de Azure](../virtual-machines/windows/sizes.md)
Disco temporal | Siempre se excluyen de la replicación | El disco temporal se excluye de la replicación siempre. Como recomienda Azure, no se deben colocar los datos persistentes en los discos temporales. Consulte demasiado[disco temporal en máquinas virtuales de Azure](../virtual-machines/windows/about-disks-and-vhds.md#temporary-disk) para obtener más detalles.
Velocidad en el disco de Hola de cambio de datos | Máximo de 6 Mbps por disco | Si la tasa de cambio de datos medio de hello en disco Hola está más allá de 6 MBps continuamente, la replicación no se ponga al día. Sin embargo, si es una ráfaga de datos ocasionales y tasa de cambio de datos de hello es superior a 6 MBps durante algún tiempo e incluye hacia abajo, la replicación se ponerse al día. En este caso, podría ver puntos de recuperación ligeramente retrasados.
Discos en cuentas de almacenamiento estándar | Compatible |
Discos en cuentas de almacenamiento premium | Compatible | Si una máquina virtual tiene discos repartidas entre cuentas de almacenamiento estándar y premium, puede seleccionar una cuenta de almacenamiento de destino diferente para cada disco tooensure tiene Hola la misma configuración de almacenamiento en la región de destino
Discos administrados estándar | No compatible |  
Discos administrados premium | No compatible |
Espacios de almacenamiento | Compatible |         
Cifrado en reposo (SSE) | Compatible | Para las cuentas de almacenamiento de destino y de almacenamiento en caché, puede seleccionar una cuenta de almacenamiento habilitada para SSE.     
Azure Disk Encryption (ADE) | No compatible |
Agregar/quitar disco en caliente | No compatible | Si agrega o quita el disco de datos en VM de hello, es necesario toodisable replicación y habilitar la replicación nuevo Hola máquina virtual.
Excluir el disco | No compatible|   El disco temporal se excluye de forma predeterminada.
LRS | Compatible |
GRS | Compatible |
RA-GRS | Compatible |
ZRS | No compatible |  
Almacenamiento en frío y en caliente | No compatible | Los discos de máquina virtual no admiten el almacenamiento temporal y permanente.

>[!IMPORTANT]
> Asegúrese de seguir hello [instrucciones sobre el almacenamiento](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) para el origen de virtual de Azure máquinas tooavoid cualquier problema de rendimiento. Si sigue la configuración predeterminada de hello, Site Recovery creará cuentas de almacenamiento de hello necesaria en función de la configuración del origen de Hola. Si ha personalizado y seleccione su propia configuración, asegúrese de seguir hello (.. / storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) como origen de las máquinas virtuales.

## <a name="support-for-network-configuration"></a>Compatibilidad con la configuración de red
**Configuración** | **No admite/no se admite** | **Comentarios**
--- | --- | ---
Tarjeta de interfaz de red (NIC) | Hasta el número máximo de NIC admitidas por un tamaño específico de máquina virtual de Azure. | NIC se crean cuando Hola máquina virtual se crea como parte de la operación de conmutación por error o conmutación por error de prueba. número de Hola de NIC en la máquina virtual depende de número de Hola de origen de hello NIC que VM tenga en el momento de Hola de habilitar la replicación de conmutación por error de Hola. Si se agrega o quitar NIC después de habilitar la replicación, no afecta el recuento NIC de conmutación por error de hello VM.
Equilibrador de carga de Internet | Compatible | Necesita tooassociate Hola configurado previamente el equilibrador de carga mediante un script de automatización de azure en un plan de recuperación.
Equilibrador de carga interno | Compatible | Necesita tooassociate Hola configurado previamente el equilibrador de carga mediante un script de automatización de azure en un plan de recuperación.
Dirección IP pública| Compatible | Necesita tooassociate un toohello IP pública NIC ya existente o cree uno y asociar toohello NIC mediante un script de automatización de azure en un plan de recuperación.
NSG en NIC (Resource Manager)| Compatible | Necesita tooassociate hello NSG toohello NIC mediante un script de automatización de azure en un plan de recuperación.  
NSG en una subred (Resource Manager y modelo clásico)| Compatible | Necesita tooassociate hello NSG toohello NIC mediante un script de automatización de azure en un plan de recuperación.
NSG en una máquina virtual (modelo clásico)| Compatible | Necesita tooassociate hello NSG toohello NIC mediante un script de automatización de azure en un plan de recuperación.
IP reservada (IP estática)/retener la IP de origen | Compatible | Si Hola NIC en una VM de origen hello tiene configuración de IP estática y la subred de destino de hello ha Hola misma IP disponible, se le asigna toohello conmutación por error de máquina virtual. Si subred de destino de hello no tiene Hola mismo IP está disponible, uno de Hola direcciones IP disponible en subred Hola se reserva para esta máquina virtual. Puede especificar una IP fija de su elección en "Elemento replicado > Configuración > Compute and Network (Proceso y red) > Interfaces de red". Puede seleccionar Hola NIC y especifique una subred de Hola y dirección IP de su elección.
IP dinámica| Compatible | Si Hola NIC en una VM de origen hello tiene la configuración de IP dinámica, hello NIC de conmutación por error de hello VM también es dinámica de forma predeterminada. Puede especificar una IP fija de su elección en "Elemento replicado > Configuración > Compute and Network (Proceso y red) > Interfaces de red". Puede seleccionar Hola NIC y especifique una subred de Hola y dirección IP de su elección.
Integración de Traffic Manager | Compatible | Puede configurar previamente el Administrador de tráfico de manera que el tráfico de hello es toohello enrutado extremo en la región de origen en un extremo de base y toohello normal en la región de destino en caso de conmutación por error.
DNS administrado por Azure | Compatible |
DNS personalizado  | Compatible |    
Proxy no autenticado | Compatible | Consulte demasiado[documento de guía de red.](site-recovery-azure-to-azure-networking-guidance.md)    
Proxy autenticado | No compatible | Si Hola VM está usando a un proxy autenticado para la conectividad saliente, no se pueden replicar mediante Azure Site Recovery.  
Sitio tooSite VPN local (con o sin ExpressRoute)| Compatible | Asegúrese de que hello UDRs y NSG están configurados de manera que el tráfico de recuperación del sitio de hello no es local tooon enrutado. Consulte demasiado[documento de guía de red.](site-recovery-azure-to-azure-networking-guidance.md)  
Conexión de red virtual tooVNET | Compatible | Consulte demasiado[documento de guía de red.](site-recovery-azure-to-azure-networking-guidance.md)  


## <a name="next-steps"></a>Pasos siguientes
- Aprenda más en las [instrucciones sobre redes para replicar máquinas virtuales de Azure](site-recovery-azure-to-azure-networking-guidance.md).
- Comience a proteger las cargas de trabajo mediante la [replicación de máquinas virtuales de Azure](site-recovery-azure-to-azure.md).
