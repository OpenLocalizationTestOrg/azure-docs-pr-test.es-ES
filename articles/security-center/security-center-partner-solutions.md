---
title: soluciones de socios de aaaManaging en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento le guía a través de cómo Azure Security Center permite a supervisar en un estado de mantenimiento de Hola de vista de las soluciones de socios comerciales integrado con su suscripción de Azure."
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
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a>Supervisión de las soluciones de asociados con Azure Security Center
Este documento le guía a través de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales en el centro de seguridad de Azure.

> [!NOTE]
> Este documento presentan servicio hello mediante el uso de una implementación de ejemplo. Este documento no es una guía paso a paso.
>
>

## <a name="monitoring-partner-solutions"></a>Supervisión de soluciones de asociados
Hola **soluciones de asociados** icono hello **centro de seguridad** permite hoja supervisar en un estado de mantenimiento de Hola de vista de las soluciones de socios comerciales que se integran con la suscripción de Azure.

![Icono Partner solutions (Soluciones de asociados)][1]

Hola **soluciones de asociados** mosaico muestra el número de Hola de soluciones de socios integrado con su suscripción. Si no hay ningún soluciones integradas, icono hello muestra hello número cero.

estado de hello tooview de las soluciones de socios comerciales:

1. Seleccione hello **soluciones de asociados** icono. Hola **soluciones de asociados** abre hoja muestra una lista de las soluciones de socios comerciales conectado tooSecurity Center.

   ![Soluciones de socios][3]

   estado de Hola de una solución de socio comercial puede ser:

   * Protegido (verde): no hay ningún problema de estado.
   * Incorrecto (rojo): hay un problema de estado que requiere atención inmediata.
   * Detenido informes (naranja) - solución Hola dejó de informar sobre su estado.
   * Estado de protección desconocido (naranja) - estado de Hola de solución de hello es desconocido en este momento debido proceso tooa no se pudo agregar una nueva solución existente de toohello de recursos.
   * No se notifica (gris) - solución hello no ha notificado nada todavía, el estado de la solución puede ser no notificado si recientemente ha conectado y todavía se está implementando.

2. Seleccione una solución de asociado. En este ejemplo, permite seleccionar hello **Qualys** solución.  Una hoja se abre con estado de Hola de solución de socios de Hola y de la solución de Hola los recursos asociados. Seleccione **consola de solución** la experiencia de administración de socios comerciales de hello tooopen de esta solución.

   ![Detalle de solución de asociado][4]
3. Volver atrás toohello **Qualys** hoja y seleccione **vínculo VM**. Hola **aplicaciones de vínculo** abre la hoja. Aquí puede conectarse solución de socios de recursos toohello.

   ![Solución de toopartner de recursos de vínculo][5]

## <a name="next-steps"></a>Pasos siguientes
En este documento, eran toohello se ha introducido **soluciones de socios** el icono Centro de seguridad. toolearn más información acerca del centro de seguridad, vea Hola siguientes artículos:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : más información cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que lo ayudan a proteger los recursos de Azure.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md) : más información cómo toomanage y que responden las alertas de toosecurity.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) : preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : obtener información y noticias de seguridad de Azure más recientes de Hola.

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
