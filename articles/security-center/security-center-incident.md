---
title: aaaHandling las alertas de seguridad en el centro de seguridad de Azure | Documentos de Microsoft
description: Este documento le ayuda a incidentes de seguridad de toohandle capacidades de toouse centro de seguridad de Azure.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: edb911c298a2ce93cd0ea5b22ce002005040090f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a>Control de incidentes de seguridad en Azure Security Center
Clasificación e investigación de alertas de seguridad pueden llevar mucho tiempo para los analistas de seguridad más cualificados incluso hello y para muchos es tooeven difícil saber dónde toobegin. Mediante el uso de [análisis](security-center-detection-capabilities.md) tooconnect información de hello entre distintos [alertas de seguridad](security-center-managing-and-responding-alerts.md), centro de seguridad puede proporcionar una vista única de una campaña de ataque y todas las de hello relacionadas alertas: también puede comprender rápidamente qué atacante de hello acciones tardó y qué recursos se vieron afectados.

Este documento describe cómo toouse seguridad avisarle capacidad en el centro de seguridad tooassist control de incidentes de seguridad.

## <a name="what-is-a-security-incident"></a>¿Qué es un incidente de seguridad?
En Security Center, un incidente de seguridad es la suma de todas las alertas de un recurso que se alinean con patrones de [cadenas de eliminación](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) . Incidentes aparecen en hello [alertas de seguridad](security-center-managing-and-responding-alerts.md) mosaico y hoja. Un incidente revelará lista Hola de alertas relacionadas, lo que permite tooobtain obtener más información sobre cada repetición.

## <a name="managing-security-incidents"></a>Administración de incidentes de seguridad
Puede revisar los incidentes de seguridad actual examinando el icono de alertas de seguridad de Hola. Acceso Hola Portal de Azure y siga estos pasos hello toosee más detalles sobre cada incidente de seguridad:

1. En el panel del centro de seguridad de hello, verá hello **alertas de seguridad** icono.

    ![Icono Alertas de seguridad en Security Center](./media/security-center-incident/security-center-incident-fig1.png)

2. Haga clic en este icono tooexpand, y si se detecta un incidente de seguridad, aparecerá en el gráfico de alertas de seguridad de hello tal y como se muestra a continuación:

    ![Incidente de seguridad](./media/security-center-incident/security-center-incident-fig2.png)

3. Observe que la descripción de incidentes de seguridad de hello tiene un icono diferente en comparación con las alertas de tooother. Haga clic en ella tooview más detalles sobre este incidente.

    ![Incidente de seguridad](./media/security-center-incident/security-center-incident-fig3.png)

4. En hello **incidente** hoja verá más detalles sobre este incidente de seguridad, que incluye su descripción completa, su gravedad (que en este caso es alta), su estado actual (en este caso sigue siendo *activo*, lo cual implica usuario hello no ha tomado un tooit de acción: puede hacerlo haciendo clic en incidente Hola Hola **alertas de seguridad** hoja), Hola atacadas recursos (en este caso *VM1*) Hola pasos de corrección de incidente de hello y, en el panel inferior de hello tiene alertas de Hola que se incluyeron en este incidente. Si desea obtener más información sobre cada alerta tooobtain, simplemente haga clic en él y otra hoja se abrirá, tal y como se muestra a continuación:

    ![Incidente de seguridad](./media/security-center-incident/security-center-incident-fig4.png)

información de Hello en esta hoja variará alerta de toohello correspondiente. Lectura [toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md) para obtener más información acerca de cómo toomanage estas alertas. Algunas consideraciones importantes con respecto a esta funcionalidad son las siguientes:

* Un nuevo filtro le permite toocustomize que su tooIncident vista únicamente, las alertas sólo, o ambos.
* Hola misma alerta puede existir como parte de un incidente (si procede), así como toobe visible como una alerta independiente.

## <a name="see-also"></a>Otras referencias
En este documento, aprendió cómo toouse Hola capacidad de incidentes de seguridad en el centro de seguridad. toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Administrar y responder a alertas de toosecurity en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md)
* [Funcionalidades de detección de Azure Security Center](security-center-detection-capabilities.md)
* [Guía de planeamiento y operaciones de Azure Security Center](security-center-planning-and-operations-guide.md)
* [Administrar y responder a alertas de toosecurity en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md)
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md)--buscar preguntas más frecuentes sobre el uso de servicio de Hola.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): encuentre entradas de blog sobre el cumplimiento y la seguridad en Azure.
