---
title: "prácticas recomendadas de Site Recovery aaaAzure | Documentos de Microsoft"
description: "En este artículo se describe los procedimientos recomendados para la implementación de Azure Site Recovery"
services: site-recovery
documentationCenter: 
author: rayne-wiselman"
manager: cfreeman
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-support-matrix-to-azure
ms.openlocfilehash: 288df858a0e1c1f5ad96dbe8b9dd0dc69d8f56ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-ready-toodeploy-azure-site-recovery"></a>Obtener lista toodeploy Azure Site Recovery

Este artículo se describe cómo tooprepare para la implementación de Azure Site Recovery.

## <a name="protecting-hyper-v-virtual-machines"></a>Protección de las máquinas virtuales de Hyper-V

Dispone de un par opciones para implementar la protección de las máquinas virtuales de Hyper-V. Puede replicar tooAzure de máquinas virtuales de Hyper en local o tooa centro de datos secundario. Cada implementación presenta diferentes requisitos.

**Requisito** | **Replicar tooAzure (con VMM)** | **Replicar máquinas virtuales de Hyper-V tooAzure (no hay VMM)** | **Replicar máquinas virtuales de Hyper-V toosecondary sitio (con VMM)** | **Detalles**
---|---|---|---|---
**VMM** | VMM ejecutándose en System Center 2012 R2 <br/><br/>Al menos una nube VMM que contenga uno o más grupos de hosts de VMM. | N/D | Servidores VMM en sitios primarios y secundarios de hello ejecutando al menos en System Center 2012 SP1 con las últimas actualizaciones. <br/><br/> Al menos una nube en cada servidor VMM. Nubes deben tener el perfil de capacidad de Hyper-V de hello establecidos.<br/><br/> nube de origen Hola debe tener al menos un grupo de host VMM. | Opcional. No es necesario toohave que System Center VMM implementado en tooAzure de máquinas virtuales de Hyper-V de orden tooreplicate pero si lo hace, necesitará toomake seguro de servidor VMM Hola está configurado correctamente. Que consiste en asegurarse de que está ejecutando la versión de VMM correcta de Hola y que las nubes estén configuradas.
**Hyper-V** | Al menos un servidor de host de Hyper-V en el sitio local de hello ejecuta Windows Server 2012 R2 o posterior | Al menos un servidor de Hyper-V en los sitios de origen y destino de hello, ejecute como mínimo Windows Server 2012 con las últimas actualizaciones de hello instalado y conectado toohello internet.<br/><br/> servidores de Hyper-V de Hello deben estar en un grupo host en una nube de VMM. | Al menos un servidor de Hyper-V en los sitios de origen y destino de hello, ejecute como mínimo Windows Server 2012 con las últimas actualizaciones de hello instalado y conectado toohello internet.<br/><br/> servidores de Hyper-V de Hello deben encontrarse en un grupo host en una nube de VMM. |
**Máquinas virtuales** | Al menos una máquina virtual en el servidor de host de Hyper-V de origen Hola | Al menos una máquina virtual en el servidor de host de hello Hyper-V en el origen de hello nube de VMM | Al menos una máquina virtual en el servidor de host de hello Hyper-V en el origen de hello nube de VMM. |  Máquinas virtuales replicar tooAzure deben cumplir con requisitos previos de la máquina virtual de Azure
**Cuenta de Azure** | Necesitará una cuenta de Azure y un servicio de Site Recovery toohello de suscripción. | Necesitará una cuenta de Azure y un servicio de Site Recovery toohello de suscripción. | N/D | Si no tiene cuenta, comience con una evaluación gratuita.
**Almacenamiento de Azure** | Necesitará una suscripción para una cuenta de Azure Storage que tenga habilitada la replicación geográfica. | Necesitará una suscripción para una cuenta de Azure Storage que tenga habilitada la replicación geográfica. | N/D | cuenta de Hello debe tener Hola misma región que el almacén de Azure Site Recovery de Hola y estar asociado a Hola misma suscripción.
**Redes** | Configurar tooensure de asignación de red que todas las máquinas que conmutan por error en Hola la misma red de Azure puede conectarse tooeach otro, independientemente del plan de recuperación que se encuentran en. Por otra parte si una puerta de enlace de red está configurada en el destino de hello red de Azure, máquinas virtuales pueden conectarse máquinas virtuales de tooother local. Si no configura la red asignación solo las máquinas que conmutan por error en hello puede conectarse el mismo plan de recuperación. | N/D |  <br/><br/>Configurar tooensure de asignación de red que las máquinas virtuales son redes conectadas tooappropriate después de la conmutación por error y que las máquinas virtuales de réplica se colocan de forma óptima en los servidores de host de Hyper-V. Si no configura la red asignar máquinas replicadas no estará conectada tooany red de VM después de la conmutación por error. |  tooset la asignación de red con VMM, deberá toomake seguro de que VMM lógica y redes de VM están configuradas correctamente.
**Proveedores y agentes** | Durante la implementación instalará hello Azure Site Recovery Provider en servidores VMM. En servidores de Hyper-V en nubes de VMM instalará el agente de servicios de recuperación de Azure de Hola. | Durante la implementación se instalará Hola proveedor de Azure Site Recovery y el agente de servicios de recuperación de Azure de hello en clúster o servidor de host de Hyper-V de Hola| Durante la implementación instalará hello Azure Site Recovery Provider en servidores VMM. En servidores de Hyper-V en nubes de VMM instalará el agente de servicios de recuperación de Azure de Hola. | Proveedores y tooSite recuperación sobre Hola se conectan mediante una conexión cifrada de HTTPS de internet. No necesita las excepciones del firewall tooadd o crear a un proxy específico para la conexión del proveedor Hola.
**Conectividad de Internet** | Sólo los servidores VMM de hello necesitan una conexión a internet | Servidores de host de Hyper-V a solo Hola tienen una conexión a internet | Solo los servidores VMM necesitan una conexión a Internet | Máquinas virtuales no se necesita nada instalado en ellos y no se conecta directamente toohello internet.



## <a name="protect-vmware-virtual-machines-or-physical-servers"></a>Protección de máquinas virtuales de VMware o servidores físicos

Dispone de un par de opciones para implementar la protección de máquinas virtuales de VMware o de servidores físicos Windows o Linux. Puede replicarlos tooAzure o tooa centro de datos secundario. Cada implementación presenta diferentes requisitos.

**Requisito** | **TooAzure de servidores de VMware replicar las máquinas virtuales o físicas)** | * **Replicar el sitio de toosecondary de servidores físicos o máquinas virtuales de VMware**  
---|---|---
**Sitio principal** | **Servidor de procesos**: un servidor de Windows dedicado (físico o virtual) | **Servidor de procesos**: un servidor de Windows dedicado (físico o una máquina virtual de VMware)<br/><br/>  
**Sitio local secundario** | N/D | **Servidor de configuración**: un servidor de Windows dedicado (físico o virtual) <br/><br/> **Servidor de destino maestro**: un servidor dedicado (físico o virtual). Configurar con máquinas con Windows tooprotect Windows o Linux tooprotect Linux.
**Las tablas de Azure** | **Suscripción**: necesitará una suscripción para hello servicio Site Recovery. <br/><br/> **Cuenta de almacenamiento**: necesitará una cuenta de almacenamiento con la replicación geográfica habilitada. cuenta de Hello debe tener Hola misma región que el almacén de Site Recovery de Hola y estar asociado a Hola misma suscripción. <br/><br/> **Servidor de configuración**: necesitará tooset de servidor de configuración de hello como una máquina virtual de Azure <br/><br/> **Servidor de destino maestro**: necesitará tooset de servidor de destino maestro hello como una máquina virtual de Azure <br/><br/> Configurar con máquinas con Windows tooprotect Windows o Linux tooprotect Linux.<br/><br/> **Red virtual de Azure**: necesitará una red virtual de Azure en qué Hola se implementará el servidor de configuración y el servidor de destino maestro. Debería ser Hola misma suscripción y región como almacén de Azure Site Recovery Hola | N/D  
**Máquinas virtuales/Servidores físicos** | Al menos una máquina virtual de VMware o un servidor físico de Windows o Linux.<br/><br/>Durante la implementación se instalará Hola servicio de movilidad en cada máquina| Al menos una máquina virtual de VMware o un servidor físico de Windows o Linux.<br/><br/> Durante la implementación del agente de unificado de hello está instalado en cada equipo.




## <a name="azure-virtual-machine-requirements"></a>Requisitos para las máquinas virtuales de Azure

Puede implementar máquinas virtuales de Site Recovery tooreplicate y servidores físicos que ejecutan cualquier sistema operativo compatible con Azure. Incluye la mayoría de las versiones de Windows y Linux. Necesitará toomake seguro que las máquinas virtuales que desea tooprotect cumplir con los requisitos de Azure a local.


## <a name="optimizing-your-deployment"></a>Optimización de la implementación

Usar hello siguiendo las sugerencias toohelp optimizar y escalar la implementación.

- **Tamaño del volumen de sistema operativo**: al replicar una hello tooAzure de máquina virtual funciona el volumen del sistema debe ser inferior a 1 TB. Si tiene varios volúmenes que esto se puede moverlas manualmente tooa otro disco antes de empezar la implementación.
- **Tamaño de disco de datos**: Si replica tooAzure puede tener hasta too32 discos de datos en una máquina virtual, cada uno con un máximo de 1 TB. Puede replicar y conmutar por error de manera eficaz una máquina virtual de ~32 TB.
- **Límites del plan de recuperación**: recuperación del sitio puede escalar toothousands de máquinas virtuales. Planes de recuperación están diseñados como un modelo para las aplicaciones que deben conmutar entre sí por lo que se limite el número de Hola de máquinas en un too50 del plan de recuperación.
- **Límites de servicio de Azure**: cada suscripción de Azure incluye un conjunto de límites predeterminados sobre núcleos, servicios en la nube, etc. Le recomendamos que ejecute una conmutación por error prueba toovalidate la disponibilidad de Hola de recursos en su suscripción. Puede modificar estos límites a través de soporte técnico de Azure.
- **Planeamiento de capacidad**: planee la escalabilidad y el rendimiento.
- **Ancho de banda de replicación**: si tiene poco ancho de banda de replicación, tenga en cuenta lo siguiente:
    - **ExpressRoute**: Site Recovery funciona con los optimizadores de ExpressRoute de Azure y WAN, como Riverbed.
    - **Tráfico de replicación**: recuperación del sitio utiliza realiza una replicación inicial inteligente usando sólo los bloques de datos y no Hola discos duros virtuales completos. Solo se replican los cambios durante la replicación continua.
    - **El tráfico de red**: puede controlar el tráfico de red usado para la replicación mediante la configuración de QoS de Windows con una directiva basada en la dirección IP de destino de Hola y el puerto.  Además, si se está replicando tooAzure Site Recovery con hello Azure Backup agent. Puede configurar la limitación para ese agente.
- **RTO**: si desea que toomeasure Hola tiempo objetivo de recuperación (RTO) que se pueden esperar con Site Recovery se recomienda ejecutar una prueba de conmutación por error y vista tooanalyze de trabajos de recuperación del sitio de hello cuánto tiempo tarda toocomplete operaciones Hola. Si no pueden realizar a través de tooAzure, para hello mejor RTO, se recomienda que automatice todas las acciones manuales mediante la integración con la recuperación y automatización de Azure planes.
- **RPO**: recuperación del sitio es compatible con un objetivo de punto de recuperación casi sincrónica (RPO) cuando se replica tooAzure. Esto supone suficiente ancho de banda entre el centro de datos y Azure.
