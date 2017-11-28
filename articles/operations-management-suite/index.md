---
title: "Documentación de Operations Management Suite (OMS) - tutoriales aaaAzure | Documentos de Microsoft"
description: "Microsoft Operations Management Suite (OMS) es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura local y en la nube. En este artículo se identifican Hola servicios diferentes incluidos en OMS y se proporcionan vínculos tootheir detallada contenido."
services: operations-management-suite
author: carolz
manager: carolz
layout: LandingPage
ms.assetid: 
ms.service: operations-management-suite
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: landing-page
ms.date: 01/23/2017
ms.author: carolz
ms.openlocfilehash: 11a8f5ecb3d84aed90554510fc1bb43320fdebb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>¿Qué es Operations Management Suite (OMS)?
Microsoft Operations Management Suite (OMS) es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura local y en la nube.  Puesto que OMS se implementa como un servicio basado en la nube, puede hacer que funcione rápidamente con una inversión mínima en servicios de infraestructura.  Las características nuevas se entregan automáticamente, lo que le ahorra el mantenimiento continuo y los costos de actualización.

Además tooproviding servicios valiosos en su propio, OMS pueden integrarse con componentes de System Center como System Center Operations Manager tooextend sus inversiones de administración existente en la nube de Hola.  System Center y OMS pueden trabajar juntos tooprovide experiencia de una administración híbrida completa.

Hola las secciones siguientes proporciona una descripción de alto nivel de hello diferentes áreas de valor de los servicios OMS y Hola que las implementan.  Puede hacer referencia tooOMS arquitectura para obtener información general de los distintos componentes de OMS Hola antes de revisar Hola documentación detallada de cada uno de ellos.

## <a name="insight-and-analyticsmediaoperations-management-suite-overviewicon-insight-analyticspng-insight-and-analytics"></a>![Insight and Analytics](media/operations-management-suite-overview/icon-insight-analytics.png) Insight and Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) ayuda a recopilar, correlacionar, buscar y actuar en los datos de rendimiento y registro generados por sistemas operativos y aplicaciones. Le ofrece visión operativa en tiempo real mediante búsqueda integrada y paneles personalizados tooreadily analizar millones de registros en todas sus cargas de trabajo y servidores, independientemente de su ubicación física.

Puede agregar fácilmente soluciones tooLog análisis que definen toobe datos recopilado y Hola lógica para su análisis.  Las soluciones pueden incluir funcionalidad adicional que se entrega automáticamente tooagents con mínima o ninguna configuración.  Además herramientas de análisis de toousing proporcionados por las soluciones individuales, puede realizar búsquedas personalizadas en un conjunto de datos completo de hello en los datos de toocorrelate de orden entre sistemas y aplicaciones.  

## <a name="automation--controlmediaoperations-management-suite-overviewicon-automation-controlpng-automation--control"></a>![Automation & Control](media/operations-management-suite-overview/icon-automation-control.png) Automation & Control
Automatización de Azure automatiza los procesos administrativos con [runbooks](../automation/automation-runbook-types.md) que se basan en PowerShell y ejecutar en hello nube de Azure.  Los runbooks pueden obtener acceso a cualquier producto o servicio que se puede administrar con PowerShell, incluidos los recursos de otras nubes como Amazon Web Services (AWS).  Runbooks también se pueden ejecutar en un servidor en los recursos de local de toomanage de centros de datos locales.

Azure Automation proporciona administración de configuración con [DSC de PowerShell](../automation/automation-dsc-overview.md).  Puede crear y administrar recursos de DSC hospedados en Azure y aplicarlos toodefine sistemas toocloud y local y aplicar automáticamente su configuración.

## <a name="protection-and-recoverymediaoperations-management-suite-overviewicon-protection-recoverypng-protection-and-disaster-recovery"></a>![Protección y recuperación](media/operations-management-suite-overview/icon-protection-recovery.png) Protección y recuperación ante desastres
[Azure Site Backup](http://azure.microsoft.com/documentation/services/backup) protege los datos de las aplicaciones y los conserva durante años sin necesidad de realizar ninguna inversión y afrontando unos costes operativos mínimos.  Hacer una copia de datos desde servidores Windows físicos y virtuales en las cargas de trabajo tooapplication de suma, como SQL Server y SharePoint.  También puede utilizarse por tooAzure de datos de System Center Data Protection Manager (DPM) tooreplicate protegido para ofrecer redundancia y almacenamiento a largo plazo.

[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) contribuye tooyour la continuidad del negocio y una estrategia de recuperación (BCDR) mediante la coordinación de la replicación, la conmutación por error y la recuperación de máquinas virtuales de Hyper-V de locales, máquinas virtuales de VMware y Windows físico / Servidores de Linux. Puede replicar el centro de datos secundario tooa máquinas o ampliar su centro de datos mediante replicación tooAzure. Site Recovery también proporciona conmutación por error simple y recuperación para cargas de trabajo. Se integra con mecanismos de recuperación ante desastres, como SQL Server AlwaysOn y proporciona planes de recuperación para una conmutación por error sencilla de cargas de trabajo que están organizados en niveles entre varias máquinas.

## <a name="oms-security-and-compliancemediaoperations-management-suite-overviewicon-security-compliancepng-security-and-compliance"></a>![Seguridad y cumplimiento normativo de OMS](media/operations-management-suite-overview/icon-security-compliance.png) Seguridad y cumplimiento normativo
Seguridad y cumplimiento de normas le ayuda a identificar, evaluar y mitigar los riesgos de seguridad tooyour infraestructura.  Estas características de OMS se implementan a través de varias soluciones de análisis de registros que se analizan los datos de registro y la configuración de agente sistemas tooassist en garantizar Hola seguridad continua de su entorno.

* Hola [solución seguridad y auditoría](oms-security-getting-started.md) recopila y analiza los eventos de seguridad en cualquier actividad sospechosa tooidentify sistemas administrados.
* Hola [solución Antimalware](../log-analytics/log-analytics-malware.md) informa sobre el estado de Hola de protección antimalware en sistemas administrados.  
* Hola solución actualizaciones del sistema realiza un análisis de las actualizaciones de seguridad de Hola y otras actualizaciones en sus sistemas administrados para que se puedan identificar fácilmente sistemas que requieren la aplicación de revisiones.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información sobre [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics).
* Obtenga información sobre [Azure Automation](../automation/automation-intro.md).
* Obtenga información sobre [Azure Backup](http://azure.microsoft.com/documentation/services/backup).
* Obtenga información sobre [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).

