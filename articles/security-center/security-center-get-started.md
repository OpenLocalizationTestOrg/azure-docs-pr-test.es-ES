---
title: "Guía de inicio de aaaAzure rápida de centro de seguridad | Documentos de Microsoft"
description: "En este artículo le ayuda a empezar a trabajar rápidamente con el centro de seguridad de Azure, le guía a través de los componentes de administración de supervisión y la directiva de seguridad de Hola y vinculación toonext pasos."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 61e95a87-39c5-48f5-aee6-6f90ddcd336e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 23b2444ba1ba30d0a1bd1a1afbc4fd0abfd0827c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-quick-start-guide"></a>Guía de inicio rápido de Azure Security Center
En este artículo le ayuda a comenzar rápidamente a trabajar con el centro de seguridad de Azure le guía a través de hello supervisión y la directiva de administración componentes de seguridad del centro de seguridad.

> [!NOTE]
> A partir de los principios de junio de 2017, centro de seguridad usará Hola Microsoft Monitoring Agent toocollect y almacenar datos. Vea [migración de la plataforma de Azure Security Center](security-center-platform-migration.md) toolearn más. información de Hello en este artículo representa la funcionalidad del centro de seguridad después de la transición toohello Microsoft Monitoring Agent.
>
>

## <a name="prerequisites"></a>Requisitos previos
tooget a trabajar con el centro de seguridad, debe tener un tooMicrosoft de suscripción a Azure. Si no tiene una suscripción, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).

nivel gratis de Hello del centro de seguridad se habilita automáticamente con su suscripción y proporciona visibilidad en estado de seguridad de Hola de los recursos de Azure. Ofrece administración básica de directivas de seguridad, recomendaciones de seguridad e integración con servicios y productos de seguridad de Azure de asociados.

Acceder a centro de seguridad de hello [portal de Azure](https://azure.microsoft.com/features/azure-portal/). toolearn más información acerca de hello portal de Azure, vea hello [documentación portal](https://azure.microsoft.com/documentation/services/azure-portal/).

## <a name="permissions"></a>Permisos
En el centro de seguridad, sólo verá información relacionada con tooan recursos de Azure cuando se le asigna Hola rol de propietario, Colaborador o lector de hello suscripción o grupo de recursos que pertenece el recurso. Vea [permisos en el centro de seguridad de Azure](security-center-permissions.md) toolearn más información acerca de los roles y las acciones permitidas en el centro de seguridad.

## <a name="data-collection"></a>Colección de datos
Centro de seguridad recopila los datos desde su tooassess de máquinas virtuales (VM), su estado de seguridad, proporcionar recomendaciones de seguridad y alerta toothreats. La primera vez que se accede a Security Center, la recopilación de datos está habilitada en todas las máquinas virtuales de la suscripción. Centro de seguridad disposiciones Hola Microsoft Monitoring Agent en todas las existentes admite máquinas virtuales de Azure y los nuevos que se crean. Vea [habilitar la recopilación de datos](security-center-enable-data-collection.md) toolearn más información acerca de cómo funciona la recolección de datos.

Se recomienda habilitar la recopilación de datos. Si usas nivel gratuito de hello del centro de seguridad, puede deshabilitar la recopilación de datos desde máquinas virtuales si se desactiva la recopilación de datos en la directiva de seguridad de Hola. Recopilación de datos es necesaria para las suscripciones en el nivel estándar de hello del centro de seguridad. Vea [precios del centro de seguridad](security-center-pricing.md) toolearn más información sobre Hola Free y niveles de precios estándar.

Hola pasos describe cómo tooaccess y uso Hola componentes del centro de seguridad. En estos pasos, le mostramos cómo tooturn desactivar la recopilación de datos si elige tooopt out.

> [!NOTE]
> Este artículo detallan servicio hello mediante el uso de una implementación de ejemplo. No es una guía paso a paso.
>
>

## <a name="access-security-center"></a>Acceso al Centro de seguridad
En el portal de hello, siga estas tooaccess pasos centro de seguridad:

1. En hello **Microsoft Azure** menú, seleccione **centro de seguridad**.

   ![Menú de Azure][1]
2. Si tiene acceso el centro de seguridad para hello primera vez, Hola **bienvenida** abre la hoja. Seleccione **centro de seguridad de inicio** tooopen hello **centro de seguridad** hoja y tooenable la recopilación de datos.
   ![Pantalla principal][10]
3. Después de iniciar el centro de seguridad de hoja bienvenida de Hola o seleccione el centro de seguridad desde el menú de Microsoft Azure hello, Hola **centro de seguridad** abre la hoja. Para facilitar el acceso toohello **centro de seguridad** hoja Hola Hola futuras, seleccione **Pin hoja toodashboard** opción (esquina superior derecha).
   ![Opción de PIN hoja toodashboard][2]

## <a name="use-security-center"></a>Uso del Centro de seguridad
Puede configurar directivas de seguridad para los grupos de recursos y las suscripciones de Azure. Vamos a configurar una directiva de seguridad para su suscripción:

1. En hello **centro de seguridad** hoja, seleccione hello **directiva** icono.
2. En hello **directiva de seguridad: definir directivas por suscripción** hoja, seleccione una suscripción.
3. En hello **directiva de seguridad** hoja, **la recopilación de datos** es tooautomatically habilitado recopilar registros. Hola extensión de supervisión se aprovisiona en todas las máquinas virtuales actuales y la nuevas en la suscripción de Hola. (En el nivel gratuito de hello del centro de seguridad, puede rechazar la recopilación de datos estableciendo **la recopilación de datos** demasiado**desactivar**. Establecer **la recopilación de datos** demasiado**desactivar** impide que el centro de seguridad ofrecerle recomendaciones y alertas de seguridad.)
4. En hello **directiva de seguridad** hoja, seleccione **directivas de prevención**. Se abrirá hello **directivas de prevención** hoja.
5. En hello **directivas de prevención** hoja, activar recomendaciones de Hola que desea toosee como parte de la directiva de seguridad. Ejemplos:

   * Establecer **actualizaciones del sistema** demasiado**en** todos los exámenes admiten máquinas virtuales para que les faltan actualizaciones de sistema operativo.
   * Establecer **vulnerabilidades de sistema operativo** demasiado**en** exámenes todos admiten tooidentify de máquinas virtuales de las configuraciones de SO que podrían hacer Hola VM tooattack más vulnerable.

### <a name="view-recommendations"></a>Ver recomendaciones
1. Devolver toohello **centro de seguridad** hoja y seleccione hello **recomendaciones** icono. Centro de seguridad periódicamente analiza el estado de seguridad de Hola de los recursos de Azure. Cuando el centro de seguridad identifica posibles vulnerabilidades de seguridad, muestra las recomendaciones en hello **recomendaciones** hoja.
   ![Recomendaciones en Azure Security Center][5]
2. Seleccione una recomendación en hello **recomendaciones** tooview hoja más hello de tooresolve acción información u tootake emitir.

### <a name="view-hello-security-state-of-your-resources"></a>Ver estado de seguridad de Hola de los recursos
1. Devolver toohello **centro de seguridad** hoja. Hola **prevención** sección del panel de hello contiene indicadores de estado de seguridad de Hola para máquinas virtuales, redes, aplicaciones y datos.
2. Seleccione **proceso** tooview obtener más información. Hola **proceso** hoja abre mostrando tres pestañas:

  - **Información general**: contiene recomendaciones de supervisión y de máquinas virtuales.
  - **Máquinas virtuales**: enumera todas las máquinas virtuales y sus estados de seguridad actuales.
  - **Cloud Services**: lista de todos los roles web y de trabajo que supervisa Security Center.

    ![icono de estado de recursos de Hello en el centro de seguridad de Azure][6]

3. En hello **Introducción** ficha, seleccione una recomendación en **recomendaciones de máquinas virtuales** tooview más información y/o realizar acción tooconfigure controles necesarios.
4. En hello **máquinas virtuales** ficha, seleccione una máquina virtual tooview obtener más detalles.

### <a name="view-security-alerts"></a>Ver alertas de seguridad
1. Devolver toohello **centro de seguridad** hoja y seleccione hello **alertas de seguridad** icono. Hola **alertas de seguridad** hoja se abre y muestra una lista de alertas. Hola análisis de centro de seguridad de los registros de seguridad y la actividad de red genera estas alertas. También se incluyen alertas de soluciones de asociados integradas.
   ![Alertas de seguridad en el Centro de seguridad de Azure][7]

   > [!NOTE]
   > Alertas de seguridad solo están disponibles si se habilita el nivel estándar de hello del centro de seguridad. Una prueba gratuita de 60 días de nivel de hello estándar está disponible. Vea [pasos siguientes](#next-steps) para obtener información sobre cómo tooget Hola estándar de nivel.
   >
   >
2. Seleccione una alerta tooview obtener información adicional. En este ejemplo, vamos a seleccionar **Modified system binary discovered** (Detectado binario del sistema modificado). Se abrirá hojas que proporcionan detalles adicionales sobre la alerta de Hola.
   ![Detalles de alertas de seguridad en Azure Security Center][8]

### <a name="view-hello-health-of-your-partner-solutions"></a>Ver el estado de Hola de las soluciones de socios comerciales
1. Devolver toohello **centro de seguridad** hoja. Hola **soluciones de asociados** permite icono supervisar, de una ojeada, Hola estado de mantenimiento de las soluciones de socios comerciales integrado con su suscripción de Azure.
2. Seleccione hello **soluciones de asociados** icono. Se abre una hoja y muestra una lista de las soluciones de socios comerciales conectado tooSecurity Center.
   ![Soluciones de asociados][9]
3. Seleccione una solución de asociado. En este ejemplo, vamos a seleccionar hello **QualysVa1** solución.  Una hoja se abre y muestra el estado de Hola de solución de socios de Hola y de la solución de Hola los recursos asociados. Seleccione **consola de solución** la experiencia de administración de socios comerciales de hello tooopen de esta solución.

## <a name="next-steps"></a>Pasos siguientes
En este artículo se introdujo toohello supervisión y la directiva de administración componentes de seguridad del centro de seguridad. Ahora que está familiarizado con el centro de seguridad, intente Hola pasos:

* Configure una directiva de seguridad para su suscripción de Azure. más información, consulte toolearn [establecer directivas de seguridad en Azure Security Center](security-center-policies.md).
* Uso de las recomendaciones de hello en el centro de seguridad toohelp proteger los recursos de Azure. más información, consulte toolearn [administrar recomendaciones de seguridad de Azure Security Center](security-center-recommendations.md).
* Revise y administre las alertas de seguridad actuales. más información, consulte toolearn [toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md).
- [Seguridad de datos de Azure Security Center](security-center-data-security.md): aprenda cómo se administran y protegen los datos en Security Center.
* Obtener más información sobre hello [las características de detección avanzadas amenazas](security-center-detection-capabilities.md) que se suministran con hello [nivel estándar](security-center-pricing.md) del centro de seguridad. nivel estándar de Hello ofrece gratuitamente para hello primeros 60 días.
* Si tiene alguna pregunta sobre el uso de centro de seguridad, vea hello [preguntas más frecuentes de Azure Security Center](security-center-faq.md).

<!--Image references-->
[1]: ./media/security-center-get-started/azure-menu.png
[2]: ./media/security-center-get-started/security-center-pin.png
[3]: ./media/security-center-get-started/security-policy.png
[4]: ./media/security-center-get-started/prevention-policy.png
[5]: ./media/security-center-get-started/recommendations.png
[6]: ./media/security-center-get-started/resources-health.png
[7]: ./media/security-center-get-started/security-alert.png
[8]: ./media/security-center-get-started/security-alert-detail.png
[9]: ./media/security-center-get-started/partner-solutions.png
[10]: ./media/security-center-get-started/welcome.png
