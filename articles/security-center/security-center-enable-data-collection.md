---
title: "recopilación de datos de aaaEnable en el centro de seguridad de Azure | Documentos de Microsoft"
description: " Obtenga información acerca de cómo tooenable de recopilación de datos en el centro de seguridad de Azure. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 411d7bae-c9d4-4e83-be63-9f2f2312b075
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 78bbf9a3d852095e2a1387c1606ff4bbb778a0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-data-collection-in-azure-security-center"></a>Habilitación de la recolección de datos en Azure Security Center

> [!NOTE]
> A partir de los principios de junio de 2017, centro de seguridad usará Hola Microsoft Monitoring Agent toocollect y almacenar datos. más información, consulte toolearn [migración de la plataforma de Azure Security Center](security-center-platform-migration.md). información de Hello en este artículo representa la funcionalidad del centro de seguridad después de la transición toohello Microsoft Monitoring Agent.
>
>

Centro de seguridad recopila los datos desde su tooassess de máquinas virtuales (VM), su estado de seguridad, proporcionar recomendaciones de seguridad y alerta toothreats. Cuando acceda por primera vez el centro de seguridad, tendrá Hola opción tooenable recolección de datos todas las máquinas virtuales en su suscripción. Si no está habilitada la recopilación de datos, centro de seguridad en el que se recomienda activar la recopilación de datos en la directiva de seguridad de Hola para esa suscripción.

Cuando se habilita la recopilación de datos, centro de seguridad disposiciones Hola Microsoft Monitoring Agent en todas las existentes admite máquinas virtuales de Azure y los nuevos que se crean. Hola Microsoft Monitoring Agent busca varias configuraciones relacionadas con la seguridad. Además, sistema operativo de hello genera eventos de registro de eventos. Estos son algunos ejemplos de dichos datos: tipo y versión del sistema operativo, registros del sistema operativo (registros de eventos de Windows), procesos en ejecución, nombre de la máquina, direcciones IP, usuario conectado e identificador de inquilino. Hola Microsoft Monitoring Agent lee las configuraciones y las entradas de registro de eventos y copia hello tooyour área de trabajo para el análisis. Hola Microsoft Monitoring Agent también copia el área de trabajo tooyour archivos de volcado de memoria de bloqueo.

Si usas nivel gratuito de hello del centro de seguridad, puede deshabilitar la recopilación de datos de máquinas virtuales si se desactiva la recopilación de datos en la directiva de seguridad de Hola. Al deshabilitar la recopilación de datos, se limitarán las evaluaciones de seguridad de las máquinas virtuales. más información, consulte toolearn [deshabilitar la recopilación de datos](#disabling-data-collection). Las instantáneas de disco de máquina virtual y la recopilación de artefactos seguirán habilitadas, aunque la recopilación de datos se deshabilite. Recopilación de datos es necesaria para las suscripciones en el nivel estándar de hello del centro de seguridad.

> [!NOTE]
> Obtén más información sobre los [planes de tarifa](security-center-pricing.md) Gratis y Estándar de Security Center.
>
>

## <a name="implement-hello-recommendation"></a>Implementar la recomendación de Hola

> [!NOTE]
> Este documento presentan servicio hello mediante el uso de una implementación de ejemplo. Este documento no es una guía paso a paso.
>
>

1. Hola **recomendaciones** hoja, seleccione **habilitar la recopilación de datos de suscripciones**.  Se abrirá hello **activar la recopilación de datos** hoja.
   ![Hoja Recomendaciones][2]
2. En hello **activar la recopilación de datos** hoja, seleccione su suscripción. Hola **directiva de seguridad** abre la hoja de dicha suscripción.
3. En hello **directiva de seguridad** hoja, seleccione **en** en **la recopilación de datos** tooautomatically recopilar registros. Activar Hola de disposiciones de recopilación de datos extensión de supervisión en todos los actuales y nuevos admite máquinas virtuales en la suscripción de Hola.
4. Seleccione **Guardar**.
5. Seleccione **Aceptar**.

## <a name="disabling-data-collection"></a>Deshabilitación de la recopilación de datos
Si utilizas nivel gratuito de hello del centro de seguridad, puede deshabilitar la recopilación de datos de máquinas virtuales en cualquier momento si se desactiva la recopilación de datos en la directiva de seguridad de Hola. Recopilación de datos es necesaria para las suscripciones en el nivel estándar de hello del centro de seguridad.

1. Devolver toohello **centro de seguridad** hoja y seleccione hello **directiva** icono. Se abrirá hello **directiva por suscripción de definir directivas de seguridad** hoja.
   ![Seleccione el icono de la directiva de Hola][5]
2. En hello **directiva por suscripción de definir directivas de seguridad** hoja, suscripción seleccione Hola que desea toodisable la recopilación de datos.
3. Hola **directiva de seguridad** abre la hoja de dicha suscripción.  Seleccione **Desactivar** en recolección de datos.
4. Seleccione **guardar** en la cinta de opciones superior Hola.

## <a name="next-steps"></a>Pasos siguientes
En este artículo se ha explicado cómo tooimplement Hola centro de seguridad recomendación "Habilitar recopilación de datos." toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que le ayudan a proteger los recursos de Azure.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md): Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md): Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
- [Seguridad de datos de Azure Security Center](security-center-data-security.md): aprenda cómo se administran y protegen los datos en Security Center.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md)--buscar preguntas más frecuentes sobre el uso de servicio de Hola.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): obtener información y noticias de seguridad de Azure más recientes de Hola.

<!--Image references-->
[2]: ./media/security-center-enable-data-collection/recommendations.png
[3]: ./media/security-center-enable-data-collection/data-collection.png
[4]: ./media/security-center-enable-data-collection/storage-account.png
[5]: ./media/security-center-enable-data-collection/policy.png
[6]: ./media/security-center-enable-data-collection/disable-data-collection.png
