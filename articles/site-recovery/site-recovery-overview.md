---
title: "¿aaaWhat es Azure Site Recovery? | Microsoft Docs"
description: "Proporciona una introducción de hello servicio Azure Site Recovery y se resumen los escenarios de implementación."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: e9b97b00-0c92-4970-ae92-5166a4d43b68
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: da6755654b8036a03314ec836f014b64428d5518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-site-recovery"></a>¿Qué es Site Recovery?

¡Página principal del servicio de Azure Site Recovery toohello! Este artículo proporciona una introducción rápida de servicio de Hola.

## <a name="business-continuity-and-disaster-recovery-bcdr-with-azure-recovery-services"></a>Continuidad empresarial y recuperación ante desastres (BCDR) con Azure Recovery Services

Como una organización necesita toofigure out cómo va tookeep los datos seguros y aplicaciones o cargas de trabajo ejecutándose cuando se planean e interrupciones imprevistas se producen.

Servicios de recuperación de Azure contribuyen estrategia BCDR tooyour:

- **Servicio Site Recovery**: Site Recovery ayuda a garantizar la continuidad empresarial, ya que mantiene las aplicaciones en funcionamiento tanto en las máquinas virtuales como en los servidores físicos disponibles si un sitio deja de funcionar. Recuperación del sitio replica las cargas de trabajo que se ejecutan en máquinas virtuales y servidores físicos para que sigan estando disponibles en una ubicación secundaria si no está disponible el sitio primario de Hola. Recupera el sitio primario de las cargas de trabajo toohello cuando está en funcionamiento y vuelva a ejecutar.
- **Servicio de copia de seguridad**: Hola Además, [copia de seguridad de Azure](https://docs.microsoft.com/azure/backup/) servicio mantiene los datos recuperables y seguras al hacer una copia de seguridad tooAzure.

Site Recovery puede administrar la replicación de:

- Máquinas virtuales de Azure que se replican entre regiones de Azure.
- Local de máquinas virtuales y servidores físicos que se replican tooAzure, o un sitio secundario de tooa.


## <a name="what-does-site-recovery-provide"></a>¿Qué ofrece Site Recovery?

**Característica** | **Detalles**
--- | ---
**Implementación de una solución de BCDR simple** | Site Recovery puede configurar y administrar la replicación, la conmutación por error y conmutación por recuperación desde una sola ubicación en hello portal de Azure.
**Replicación de máquinas virtuales de Azure** | La estrategia BCDR se puede configurar para que las máquinas virtuales de Azure se repliquen entre distintas regiones de Azure.
**Replicación de máquinas locales fuera del sitio** | Puede replicar máquinas virtuales locales y servidores físicos tooAzure o ubicación de tooa local secundario. Replicación tooAzure elimina Hola costo y la complejidad de mantener un centro de datos secundaria.
**Replicación de cualquier carga de trabajo** | La replicación de cualquier carga de trabajo que se ejecuta en máquinas virtuales de Azure compatibles, máquinas virtuales de Hyper-V locales, máquinas virtuales VMware y servidores físicos Windows o Linux.
**Mantener los datos resistentes y seguros** | Site Recovery coordina la replicación sin interceptar los datos de las aplicaciones. Los datos replicados se almacenan en el almacenamiento de Azure, con resistencia de Hola que proporciona. Cuando se produce conmutación por error, máquinas virtuales de Azure se crean en función de saludo replican datos.
**Cumplimiento de RTO y RPO** | Mantenga los objetivos de tiempo de recuperación (RTO) y los objetivos de punto de recuperación (RPO) dentro de los límites de la organización. Site Recovery proporciona una replicación continua tanto a las máquinas virtuales de Azure como a las máquinas virtuales VMware con una frecuencia de tan solo 30 segundos para Hyper-V. Para reducir aún más los objetivos de tiempo de recuperación (RTO), realice la integración con [Azure Traffic Manager](https://azure.microsoft.com/blog/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/).
**Mantener la coherencia de aplicaciones a través de la conmutación por error** | Los puntos de recuperación se pueden configurar con instantáneas coherentes con la aplicación. Las instantáneas coherentes con la aplicación capturan los datos del disco, todos los datos en que hay en la memoria y todas las transacciones en curso.
**Prueba sin interrupciones** | Puede ejecutar fácilmente las conmutaciones por error de prueba toosupport de recuperación ante desastres, sin afectar a la replicación en curso.
**Ejecución de conmutaciones por error flexibles** | Puede ejecutar conmutaciones por error planeadas para interrupciones planeadas sin pérdida de datos o conmutaciones por error no planeadas con una pérdida de datos mínima (según la frecuencia de replicación) ante desastres inesperados. Fácilmente puede producir un error de sitio primario espera tooyour cuando lo esté disponible de nuevo.
**Creación de planes de recuperación** | Puede personalizar y secuenciar la conmutación por error y la recuperación de aplicaciones de niveles múltiples en varias máquinas virtuales con planes de recuperación. Agrupe las máquinas en planes y agregue scripts y acciones manuales. Los planes de recuperación se pueden integrar con runbooks de Azure Automation.
**Integración con las tecnologías de BCDR existentes** | Site Recovery se integra con otras tecnologías de BCDR. Por ejemplo, puede utilizar Site Recovery tooprotect Hola SQL Server back-end de cargas de trabajo corporativos, incluida la compatibilidad nativa para SQL Server AlwaysOn, conmutación por error de toomanage Hola de grupos de disponibilidad.
**Integrar con la biblioteca de automatización de Hola** | Una ingente biblioteca de Azure Automation proporciona scripts específicos de la aplicación y preparados para la producción que se pueden descargar e integrarse con Site Recovery.
**Administración de la configuración de la red** | Site Recovery se integra con Azure para simplificar la administración de la red de una aplicación, lo que incluye la reserva de direcciones IP, la configuración de equilibradores de carga o la integración de Azure Traffic Manager, con el fin de que los cambios de red sean eficientes.


## <a name="what-can-i-replicate"></a>¿Qué puedo replicar?

**Compatible** | **Detalles**
--- | ---
**¿Qué puedo replicar?** | Máquinas virtuales de Azure entre regiones de Azure (en versión preliminar)<br/><br/>  Máquinas virtuales de VMware, las máquinas virtuales de Hyper-V, servidores físicos (Windows y Linux) tooAzure local < br /<br/> Máquinas virtuales de VMware, las máquinas virtuales de Hyper-V, sitio secundario de servidores físicos tooa local. Para las máquinas virtuales de Hyper-V, sitio secundario de replicación tooa solo se admite si los hosts de Hyper-V administrados por System Center VMM.
**¿Qué regiones se admiten para Site Recovery?** | [Regiones admitidas](https://azure.microsoft.com/regions/services/) |
**¿Qué sistemas operativos necesitan las máquinas replicadas?** | [Requisitos de máquinas virtuales de Azure](site-recovery-support-matrix-azure-to-azure.md#support-for-replicated-machine-os-versions)<br></br>[Requisitos de máquinas virtuales VMWare](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)<br/><br/> En el caso de las máquinas virtuales de Hyper-V, se admite cualquier [SO invitado](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows) compatible con Hyper-V y Azure.<br/><br/> [Requisitos del servidor físico](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)
**¿Qué hosts o servidores VMware necesito?** | Las máquinas virtuales de VMware se pueden ubicar en [hosts de vSphere/servidores de vCenter compatibles](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)
**¿Qué cargas de trabajo puedo replicar?** | Puede replicar cualquier carga de trabajo que se ejecute en una máquina de replicación admitida. Además, equipo de Site Recovery Hola ha realizado pruebas específicas de la aplicación para una [número de aplicaciones](site-recovery-workload.md#workload-summary).


## <a name="azure-portal-considerations"></a>Consideraciones de Azure Portal

* Recuperación de sitio se puede implementar en hello [portal de Azure](https://portal.azure.com).
* Hola portal de Azure clásico, puede administrar Site Recovery con el modelo de administración de servicios clásico de Hola.
- portal clásico de Hello solo debe tener implementaciones existentes de Site Recovery de toomaintain usado. No se puede crear almacenes nuevos en el portal clásico de Hola.

## <a name="next-steps"></a>Pasos siguientes
* Más información sobre [compatibilidad con cargas de trabajo](site-recovery-workload.md).
* Empezar a trabajar con [replicación de máquina virtual de Azure entre regiones](site-recovery-azure-to-azure.md), [tooAzure de replicación de VMware](vmware-walkthrough-overview.md), o [tooAzure de replicación de Hyper-V](hyper-v-site-walkthrough-overview.md).
