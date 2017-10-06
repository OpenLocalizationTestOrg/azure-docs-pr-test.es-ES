---
title: aaaIntroduction tooAzure centro de seguridad | Documentos de Microsoft
description: "Obtenga información sobre el Centro de seguridad de Azure, sus capacidades clave y cómo funciona."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 45b9756b-6449-49ec-950b-5ed1e7c56daa
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 287dbaaa7e2004c522f103595bc316261daf05b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security-center"></a>Introducción tooAzure centro de seguridad
Obtenga información sobre el Centro de seguridad de Azure, sus capacidades clave y cómo funciona.

> [!NOTE]
> A partir de los principios de junio de 2017, centro de seguridad usará Hola Microsoft Monitoring Agent toocollect y almacenar datos. Vea [migración de la plataforma de Azure Security Center](security-center-platform-migration.md) toolearn más. información de Hello en este artículo representa la funcionalidad del centro de seguridad después de la transición toohello Microsoft Monitoring Agent.
>
>

## <a name="what-is-azure-security-center"></a>¿Qué es el Centro de seguridad de Azure?
 Centro de seguridad le ayuda a evitar, detectar y responder toothreats con una mayor visibilidad y control sobre la seguridad de Hola de los recursos de Azure. Proporciona administración de directivas y supervisión de la seguridad integrada en las suscripciones de Azure, ayuda a detectar las amenazas que podrían pasar desapercibidas y funciona con un amplio ecosistema de soluciones de seguridad.

## <a name="key-capabilities"></a>Principales capacidades
 Centro de seguridad ofrece amenaza fácil de usar y eficaces capacidades de prevención, detección y respuesta que están integradas en tooAzure. Principales capacidades:

| Fase | Capacidad |
| --- | --- |
| Prevención |Hola de monitores de estado de seguridad de los recursos de Azure |
| Prevención | Define directivas para las suscripciones de Azure en función de los requisitos de seguridad de su empresa, tipos de Hola de aplicaciones que usan y Hola confidencialidad de los datos |
| Prevención | Usa controlado por directivas seguridad recomendaciones tooguide los propietarios de servicio a través del proceso Hola de implementación necesarios controles |
| Prevención | Implementa rápidamente servicios y dispositivos de seguridad de Microsoft y asociados |
| Detección |Recopila y analiza los datos de seguridad de los recursos de Azure, red de Hola y soluciones de socios comerciales, como programas antimalware y firewalls automáticamente |
| Detección | Usa global de amenazas inteligencia de hello productos y servicios, Hola Microsoft Digital crímenes unidad (DCU), Microsoft Security Response Center (MSRC) de Microsoft y fuentes externas |
| Detección | Aplica análisis avanzados, incluido el aprendizaje automático y el análisis de comportamientos |
| Respuesta |Proporciona seguridad prioritaria ante incidentes y alertas |
| Respuesta | Proporciona información sobre el origen de Hola de ataque de Hola y de recursos afectados |
| Respuesta | Sugiere formas toostop Hola ataque actual y ayudar a evitar ataques futuros |

## <a name="introductory-walkthrough"></a>Tutorial de introducción

> [!NOTE]
> Este documento presentan servicio hello mediante el uso de una implementación de ejemplo. Este documento no es una guía paso a paso.
>
>

 Acceder a centro de seguridad de hello [portal de Azure](https://azure.microsoft.com/features/azure-portal/). [Inicie sesión en el portal de toohello](https://portal.azure.com). En el menú de portal principal de hello, desplácese toohello **centro de seguridad** opción o seleccione hello **centro de seguridad** icono que fijado anteriormente toohello panel del portal.

![Icono Seguridad en el Portal de Azure][1]

En el Centro de seguridad, puede establecer directivas de seguridad, supervisar configuraciones de seguridad y ver alertas de seguridad.

### <a name="security-policies"></a>Directivas de seguridad
Puede definir directivas para las suscripciones de Azure según los requisitos de seguridad de la compañía tooyour. También puede adaptarlas toohello tipos de aplicaciones que está usando o importancia de toohello de datos de hello en cada suscripción. Por ejemplo, es posible que los recursos usados para el desarrollo o las pruebas tengan requisitos de seguridad distintos a los empleados para las aplicaciones de producción. Del mismo modo, es posible que las aplicaciones con datos regulados como PII requieran un mayor nivel de seguridad.

> [!NOTE]
> toomodify una directiva de seguridad, debe ser propietario de una suscripción de administrador de seguridad u Hola o de colaborador. toolearn más información acerca de los roles y las acciones permitidas en el centro de seguridad, consulte [permisos en el centro de seguridad de Azure](security-center-permissions.md).
>
>

En hello **centro de seguridad** hoja, seleccione hello **directiva** icono para obtener una lista de las suscripciones y los grupos de recursos.   

![Hoja de centro de seguridad][2]

En hello **directiva de seguridad** hoja, seleccione un detalles de la directiva de la suscripción tooview Hola.

**Recopilación de datos** habilita la recopilación de datos en una directiva de seguridad. Con la habilitación se consigue lo siguiente:

* Examen diario de todas las máquinas virtuales (VM) admitidas para las recomendaciones y la supervisión de seguridad.
* Colección de eventos de seguridad para el análisis y la detección de amenazas.

> [!NOTE]
> Recopilación de datos se configura en el nivel de suscripción de Hola.
>
>

Seleccione **directivas de prevención** tooopen hello **directivas de prevención** hoja. **Mostrar recomendaciones para** le permite elegir los controles de seguridad de Hola que desee hello y toomonitor recomendaciones que desea toosee según las necesidades de seguridad de Hola de recursos de hello en la suscripción de Hola.

### <a name="security-recommendations"></a>Recomendaciones de seguridad
 Centro de seguridad analiza el estado de seguridad de Hola de las recursos de Azure tooidentify vulnerabilidades de seguridad. Una lista de recomendaciones le guía a través del proceso de Hola de configuración de controles necesarios. Algunos ejemplos son:

* Aprovisionamiento antimalware toohelp identificar y quitar software malintencionado
* Configuración de red seguridad reglas y grupos toocontrol tráfico tooVMs
* Aprovisionamiento de los firewalls de aplicación web toohelp defenderse contra los ataques que tienen como destino las aplicaciones web
* Implementación de actualizaciones del sistema que faltan.
* Direccionamiento de las configuraciones de sistema operativo que no coincide con hello recomienda líneas de base

Haga clic en hello **recomendaciones** icono para obtener una lista de recomendaciones. Haga clic en cada recomendación tooview obtener información adicional o un problema de tootake acción tooresolve Hola.

![Recomendaciones de seguridad en el Centro de seguridad de Azure][5]

### <a name="security-state-of-azure-resources"></a>Estado de seguridad de recursos de Azure
Hola **prevención** sección del panel de hello muestra Hola postura de seguridad general del entorno de Hola por tipo de recurso, incluidas las máquinas virtuales, las aplicaciones web y otros recursos.   

Seleccione un tipo de recurso en **prevención** tooview para obtener más información, incluida una lista de las vulnerabilidades de seguridad que se han identificado. (**Proceso** está seleccionado en el siguiente ejemplo de Hola.)

![Icono Estado de los recursos][6]

### <a name="security-alerts"></a>Alertas de seguridad
 Centro de seguridad automáticamente recopila, analiza y se integra datos de registro de recursos de Azure, redes de Hola y soluciones de socios comerciales, como programas antimalware y firewalls. Cuando se detecten amenazas, se creará una alerta de seguridad. Como ejemplos se incluye la detección de:

* VM en peligro que se comunican con direcciones IP malintencionadas conocidas
* Malware avanzado detectado mediante la generación de informes de errores de Windows.
* Ataques de fuerza bruta contra VM
* Alertas de seguridad de programas antimalware y firewalls integrados

Si hace clic en hello **alertas de seguridad** icono muestra una lista de alertas con prioridad.

![Alertas de seguridad][7]

Seleccionar una alerta muestra más información acerca de los ataques de Hola y sugerencias sobre cómo tooremediate lo.

![Detalles de alertas de seguridad][8]

### <a name="partner-solutions"></a>Soluciones de socios
Hola **soluciones de asociados** permite icono supervisar en un estado de seguridad de Hola de vista de las soluciones de socios comerciales se integra con su suscripción de Azure. Centro de seguridad muestra alertas procedentes de soluciones de Hola.

Seleccione hello **soluciones de asociados** icono. Se muestra una hoja con una lista de todas las soluciones de asociados conectadas.

![Soluciones de socios][9]

## <a name="get-started"></a>Primeros pasos
tooget a trabajar con el centro de seguridad, es necesario un tooMicrosoft de suscripción a Azure. El Centro de seguridad se habilita con su suscripción de Azure. Si no tiene una suscripción, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).

 Acceder a centro de seguridad de hello [portal de Azure](https://azure.microsoft.com/features/azure-portal/). Vea hello [documentación portal](https://azure.microsoft.com/documentation/services/azure-portal/) toolearn más.

[Introducción a Azure Security Center](security-center-get-started.md) rápidamente le guía a través de centro de seguridad de los componentes de supervisión de seguridad y administración de directivas de Hola.

## <a name="next-steps"></a>Pasos siguientes
En este documento, eran introducidas Center tooSecurity, sus capacidades claves y cómo se inicia tooget. toolearn más información, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : más información cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que lo ayudan a proteger los recursos de Azure.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md) : más información cómo toomanage y que responden las alertas de toosecurity.
* [Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
- [Seguridad de datos de Azure Security Center](security-center-data-security.md): aprenda cómo se administran y protegen los datos en Security Center.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) : preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : obtener información y noticias de seguridad de Azure más recientes de Hola.

<!--Image references-->
[1]: ./media/security-center-intro/security-tile.png
[2]: ./media/security-center-intro/security-center.png
[3]: ./media/security-center-intro/security-policy.png
[4]: ./media/security-center-intro/security-policy-blade.png
[5]: ./media/security-center-intro/recommendations.png
[6]: ./media/security-center-intro/resources-health.png
[7]: ./media/security-center-intro/security-alert.png
[8]: ./media/security-center-intro/security-alert-detail.png
[9]: ./media/security-center-intro/partner-solutions.png
