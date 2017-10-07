---
title: aaaOperations arquitectura Management Suite (OMS) | Documentos de Microsoft
description: "Microsoft Operations Management Suite (OMS) es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura local y en la nube.  En este artículo se identifican Hola servicios diferentes incluidos en OMS y se proporcionan vínculos tootheir detallada contenido."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 40e41686-7e35-4d85-bbe8-edbcb295a534
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: fa3227aa9c19219009ebe363b7fd2d6565cec59c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="oms-architecture"></a>Arquitectura de OMS
[Operations Management Suite (OMS)](https://azure.microsoft.com/documentation/services/operations-management-suite/) es una colección de servicios basados en la nube para la administración de sus entornos locales y en la nube.  Este artículo describe Hola diferentes local y componentes de la nube de OMS y su arquitectura de informática en nube de alto nivel.  Puede hacer referencia a documentación de toohello para cada servicio para obtener más detalles.

## <a name="log-analytics"></a>Log Analytics
Los datos recopilados por [análisis de registros](https://azure.microsoft.com/documentation/services/log-analytics/) se almacena en el repositorio OMS de Hola que se hospeda en Azure.  Orígenes conectados generan datos recopilados en el repositorio de OMS Hola.  Actualmente hay tres tipos de orígenes conectados compatibles.

* Un agente instalado en un [Windows](../log-analytics/log-analytics-windows-agents.md) o [Linux](../log-analytics/log-analytics-linux-agents.md) equipo directamente conectado tooOMS.
* Un grupo de administración de System Center Operations Manager (SCOM) [conectado tooLog análisis](../log-analytics/log-analytics-om-agents.md) .  Los agentes SCOM seguirán toocommunicate con servidores de administración que reenvían los eventos y datos de rendimiento tooLog análisis.
* Una [cuenta de almacenamiento de Azure](../log-analytics/log-analytics-azure-storage.md) que recopila datos de [Diagnósticos de Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) de un rol de trabajo, rol web o máquina virtual de Azure.

Orígenes de datos definen los datos de Hola que recopila de análisis de registros de orígenes conectados, incluidos los registros de eventos y contadores de rendimiento.  Soluciones de agregar funcionalidad tooOMS y pueden agregarse fácilmente el área de trabajo de tooyour de hello [Galería de soluciones de OMS](../log-analytics/log-analytics-add-solutions.md).  Algunas soluciones pueden requerir una conexión directa de tooLog análisis de agentes de SCOM, mientras que otros pueden requerir un toobe agente adicional instalado.

Análisis de registro tiene un portal basado en web que puede usar recursos de OMS toomanage, agregar y configurar soluciones de OMS y ver y analizar datos en el repositorio OMS Hola.

![Arquitectura de alto nivel de Log Analytics](media/operations-management-suite-architecture/log-analytics.png)

## <a name="azure-automation"></a>Azure Automation
[Runbooks de automatización de Azure](http://azure.microsoft.com/documentation/services/automation) se ejecutan en la nube de Azure de Hola y puede tener acceso a recursos que están en Azure, en otros servicios en la nube o accesibles desde Hola Internet pública.  También puede designar máquinas locales en su centro de datos local con [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md) para que los Runbooks puedan acceder a recursos locales.

[Las configuraciones de DSC](../automation/automation-dsc-overview.md) almacena en automatización de Azure puede ser tooAzure aplicada directamente las máquinas virtuales.  Otras máquinas físicas y virtuales pueden solicitar configuraciones de servidor de extracción de DSC de automatización de Azure Hola.

Automatización de Azure tiene una solución de OMS que muestra las estadísticas y vínculos toolaunch Hola portal de Azure para cualquier operación.

![Arquitectura de alto nivel de Automatización de Azure](media/operations-management-suite-architecture/automation.png)

## <a name="azure-backup"></a>Copia de seguridad de Azure
Los datos protegidos en [Copia de seguridad de Azure](http://azure.microsoft.com/documentation/services/backup) se almacenan en un almacén de copia de seguridad ubicado en una región geográfica determinada.  Hola datos se replican en Hola la misma región y, según tipo hello de almacén, también pueden ser replicadas tooanother región para una mayor redundancia.

Azure Backup tiene tres escenarios fundamentales.

* Máquina de Windows con agente de copia de seguridad de Azure.  Esto le permite toobackup archivos y carpetas desde cualquier cliente o servidor Windows directamente tooyour almacén de copia de seguridad de Azure.  
* System Center Data Protection Manager (DPM) o servidor de Copia de seguridad de Microsoft Azure. Esto permite tooleverage DPM o el servidor de copia de seguridad de Microsoft Azure toobackup archivos y carpetas además las cargas de trabajo de tooapplication como almacenamiento toolocal SQL y SharePoint y, a continuación, replicar tooyour almacén de copia de seguridad de Azure.
* Extensiones de la máquina virtual de Azure.  Esto le permite toobackup máquinas virtuales de Azure tooyour almacén de copia de seguridad de Azure.

Copia de seguridad de Azure tiene una solución OMS que muestra las estadísticas y vínculos toolaunch Hola portal de Azure para cualquier operación.

![Arquitectura de alto nivel de Copia de seguridad de Azure](media/operations-management-suite-architecture/backup.png)

## <a name="azure-site-recovery"></a>Azure Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) organiza la replicación, la conmutación por error y la conmutación por recuperación de máquinas virtuales y servidores físicos. Los datos de replicación se intercambian entre los hosts de Hyper-V, los hipervisores de VMware y servidores físicos en los centros de datos principal y secundaria, o entre centros de datos de Hola y el almacenamiento de Azure.  Site Recovery almacena metadatos en almacenes ubicados en una región geográfica de Azure determinada. Ningún dato replicado se almacena por hello servicio Site Recovery.

Azure Site Recovery tiene tres escenarios fundamentales de replicación.

**Replicación de máquinas virtuales de Hyper-V**

* Si las máquinas virtuales de Hyper-V se administran en nubes VMM, puede replicar tooa almacenamiento de centro o tooAzure de datos secundaria.  Replicación tooAzure es a través de una conexión a internet segura.  Centro de datos de replicación tooa secundario está por encima de hello LAN.
* Si las máquinas virtuales de Hyper-V no están administradas por VMM, puede replicar tooAzure almacenamiento solo.  Replicación tooAzure es a través de una conexión a internet segura.

**Replicación de máquinas virtuales de VMWare**

* Puede replicar VMware máquinas virtuales tooa centro de datos secundario ejecuta almacenamiento VMware o tooAzure.  Replicación tooAzure puede producirse a través de una VPN de sitio a sitio o ExpressRoute de Azure o a través de una conexión a Internet segura. Centro de datos de replicación tooa secundario se produce a través de canal de datos de InMage Scout Hola.

**Replicación de servidores físicos de Windows o Linux** 

* Puede replicar servidores físicos tooa centro de datos o tooAzure almacenamiento secundario. Replicación tooAzure puede producirse a través de una VPN de sitio a sitio o ExpressRoute de Azure o a través de una conexión a Internet segura. Centro de datos de replicación tooa secundario se produce a través de canal de datos de InMage Scout Hola.  Azure Site Recovery tiene una solución de OMS que muestra algunas estadísticas, pero debe usar Hola portal de Azure para cualquier operación.

![Arquitectura de alto nivel de Azure Site Recovery](media/operations-management-suite-architecture/site-recovery.png)

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información sobre [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics).
* Obtenga información sobre [Azure Automation](https://azure.microsoft.com/documentation/services/automation).
* Obtenga información sobre [Azure Backup](http://azure.microsoft.com/documentation/services/backup).
* Obtenga información sobre [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).

