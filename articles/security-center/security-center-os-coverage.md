---
title: plataformas de aaaSupported en el centro de seguridad de Azure | Documentos de Microsoft
description: En este documento se proporciona una lista de sistemas operativos Windows y Linux compatibles con Azure Security Center.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: f73e04970749271fc9d75836f4f468b0a4953f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="supported-platforms-in-azure-security-center"></a>Plataformas compatibles con Azure Security Center
Supervisión de estado de seguridad y recomendaciones están disponibles para las máquinas virtuales (VM) creadas mediante Hola clásico y modelos de implementación del Administrador de recursos.

> [!NOTE]
> Obtener más información sobre hello [clásico y modelos de implementación del Administrador de recursos](../azure-classic-rm.md) para recursos de Azure.
>
>

## <a name="supported-platforms-for-windows-vms"></a>Plataformas compatibles con máquinas virtuales Windows
Sistemas operativos Windows compatibles:

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

> [!NOTE]
>
* Las evaluaciones de vulnerabilidad del sistema operativo todavía no están disponibles para Windows Server 2016.
* Las detecciones de análisis de bloqueos solo son compatibles con Windows Server 2012 y Windows Server 2012 R2.
>
>

## <a name="supported-platforms-for-linux-vms"></a>Plataformas compatibles con máquinas virtuales Linux
Sistemas operativos Linux compatibles:

* Versiones de Ubuntu 12.04, 14.04 y 16.04 y 16.10
* Versiones de Debian 7, 8
* Versiones de CentOS 6.\*, 7.*
* Versiones de Red Hat Enterprise Linux (RHEL) 6.\*, 7.*
* Versiones de SUSE Linux Enterprise Server (SLES) 11 SP4+, 12.*
* Versiones de Oracle Linux 6.\*, 7.*

> [!NOTE]
> El análisis de comportamiento de máquinas virtuales todavía no está disponible para los sistemas operativos Linux.
>
>

## <a name="vms-and-cloud-services"></a>Servicios en la nube y máquinas virtuales
También se admiten máquinas virtuales que se ejecuten en un servicio en la nube. Se supervisan los roles de web y de trabajo de servicios en la nube que se ejecutan en espacios de producción. toolearn más información acerca del servicio en la nube, consulte [Introducción a los servicios de nube](../cloud-services/cloud-services-choose-me.md).

## <a name="next-steps"></a>Pasos siguientes

- [Guía de operaciones de planificación de Azure Security Center e](security-center-planning-and-operations-guide.md) : más información cómo tooplan y entender las consideraciones de diseño de hello tooadopt Azure Security Center
- [Alertas de seguridad por tipo de Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-alerts-type.md#virtual-machine-behavioral-analysis): obtenga más información sobre el análisis de comportamiento de máquinas virtuales y el análisis de la memoria de volcado en Security Center.
- [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) : preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda
- [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): encuentre entradas de blog sobre cumplimiento y seguridad de Azure.
