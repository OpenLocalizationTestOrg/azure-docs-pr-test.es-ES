---
title: actualizaciones del sistema aaaApply en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento muestra cómo tooimplement Hola recomendaciones de Azure Security Center ** aplicar las actualizaciones de sistema ** y ** reiniciar después de las actualizaciones de sistema **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a>Aplicar actualizaciones del sistema en Azure Security Center
Azure Security Center supervisa diariamente las máquinas virtuales Windows y Linux por si faltan actualizaciones de sistema operativo. Security Center recupera una lista de actualizaciones críticas y de seguridad disponibles desde Windows Update o Windows Server Update Services (WSUS), dependiendo de qué servicio está configurado en una máquina virtual Windows.  Centro de seguridad también comprueba las actualizaciones más recientes de hello en sistemas Linux. Si falta una actualización del sistema en la máquina virtual, Security Center le recomendará que aplique las actualizaciones del sistema

> [!NOTE]
> Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.  No se trata de una guía paso a paso.
>
>

## <a name="implement-hello-recommendation"></a>Implementar la recomendación de Hola
1. Hola **recomendaciones** hoja, seleccione **aplicar actualizaciones del sistema**.

   ![Aplicar actualizaciones del sistema][1]
2. Hola **aplicar actualizaciones del sistema** hoja abrirá mostrando una lista de las máquinas virtuales que les faltan actualizaciones de sistema. Seleccione una máquina virtual.

   ![Seleccionar una máquina virtual][2]
3. Se abre una hoja que muestra una lista de las actualizaciones que faltan en esa máquina virtual. Seleccione una actualización del sistema. En este ejemplo, vamos a seleccionar KB3156016.

   ![Actualizaciones de seguridad que faltan][3]

4. Siga los pasos de Hola Hola **de actualizaciones de seguridad** tooapply hoja Hola actualización que falta.

   ![Actualización de seguridad][4]

## <a name="reboot-after-system-updates"></a>Reiniciar tras actualizar el sistema
1. Devolver toohello **recomendaciones** hoja. Se genera una nueva entrada después de aplicar las actualizaciones del sistema, denominada **Reiniciar tras actualizar el sistema**. Esta entrada le permite saber que necesita proceso tooreboot Hola VM toocomplete Hola de aplicar las actualizaciones del sistema.

   ![Reiniciar tras actualizar el sistema][5]
2. Seleccione **Reiniciar tras actualizar el sistema**. Se abrirá **es reiniciar el equipo las actualizaciones del sistema pendiente toocomplete** hoja muestra una lista de las máquinas virtuales que necesite toorestart toocomplete Hola aplica proceso actualizaciones del sistema.

   ![Reinicio pendiente][6]

Reinicie Hola VM desde el proceso de Azure toocomplete Hola.

## <a name="see-also"></a>Otras referencias
toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que le ayudan a proteger los recursos de Azure.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre publicaciones de blog sobre el cumplimiento y la seguridad de Azure.

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
