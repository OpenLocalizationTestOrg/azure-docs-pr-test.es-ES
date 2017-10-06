---
title: "aaaEnable agente de máquina virtual en el centro de seguridad de Azure | Documentos de Microsoft"
description: "Este documento muestra cómo tooimplement Hola recomendación de Azure Security Center ** agente ** de habilitar la máquina virtual."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a>Habilitación del Agente de máquina virtual en Azure Security Center
Hello agente de máquina virtual debe instalarse en máquinas virtuales (VM) en orden demasiado[habilitar la recopilación de datos](security-center-enable-data-collection.md).  Habilita el centro de seguridad de Azure se toosee que las máquinas virtuales requieren Hola a agente de máquina virtual y se recomienda que habilite Hola a agente de máquina virtual en esas máquinas virtuales.

Hola agente de máquina virtual está instalado de forma predeterminada para las máquinas virtuales que se implementan desde hello Azure Marketplace. artículo de Hello [agente de máquina virtual y extensiones: parte 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) proporciona información acerca de cómo tooinstall Hola agente de máquina virtual.

> [!NOTE]
> Este documento presentan servicio hello mediante el uso de una implementación de ejemplo. No se trata de una guía paso a paso.
>
>

## <a name="implement-hello-recommendation"></a>Implementar la recomendación de Hola
1. Hola **hoja de recomendaciones**, seleccione **habilitar agente de máquina virtual**.
   ![Habilitar el Agente de máquina virtual][1]
2. Esto abre una hoja de hello **VM agente falta o no responde**. Esta hoja enumera las máquinas virtuales de Hola que requieren Hola agente de máquina virtual. Siga las instrucciones de hello en el agente de máquina virtual de hello hoja tooinstall Hola.
   ![Agente de máquina virtual ausente][2]

## <a name="see-also"></a>Otras referencias
toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md): Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que lo ayudan a proteger los recursos de Azure.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md): Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md): Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md)--buscar preguntas más frecuentes sobre el uso de servicio de Hola.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): obtener información y noticias de seguridad de Azure más recientes de Hola.

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
