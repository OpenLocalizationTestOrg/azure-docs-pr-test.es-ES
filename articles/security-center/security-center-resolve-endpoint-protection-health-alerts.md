---
title: aaaResolve de alertas de estado de endpoint protection en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento muestra cómo tooimplement Hola recomendación de Azure Security Center ** alertas de estado de resolver Endpoint Protection **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a>Resolución de alertas de estado de Endpoint Protection en Azure Security Center
Azure Security Center recomendará resolver las alertas de estado detectadas de Endpoint Protection.  Centro de seguridad le permite toosee qué máquinas virtuales (VM) tiene errores de protección de extremo y de cuántos.

> [!NOTE]
> Este documento presentan servicio hello mediante el uso de una implementación de ejemplo. No se trata de una guía paso a paso.
> 
> 

## <a name="implement-hello-recommendation"></a>Implementar la recomendación de Hola
1. Hola **hoja de recomendaciones**, seleccione **las alertas de estado de Endpoint Protection de resolver**.
   ![Resolver alertas de estado de Endpoint Protection][1]
2. Esto abre una hoja de hello **error de Endpoint Protection** que enumera las máquinas virtuales con errores y el número de Hola de errores para cada máquina virtual. Seleccione una máquina virtual de hello lista.
   ![Endpoint protection failure][2]
3. A **lista de errores de** hoja se abre para saludo seleccionado VM, mostrando una lista de errores. Seleccione un error de hello lista toolearn más. Se abrirá una hoja con información sobre el error de hello seleccionado.
   ![Lista de errores][3]
   ![Evento de error][4]

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
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
