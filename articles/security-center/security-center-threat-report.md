---
title: informe de inteligencia de amenazas de centro de seguridad aaaAzure | Documentos de Microsoft
description: "Este documento le ayuda a informes inteligente amenaza del centro de seguridad de toouse Azure durante una investigación toofind obtener más información sobre una alerta de seguridad."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5662e312-e8c2-4736-974e-576eeb333484
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: c888cfac1dd8b057616a6b8e6c6f6b67b552f2e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-threat-intelligence-report"></a>Informe de inteligencia frente a amenazas de Azure Security Center
En este documento se explica cómo los informes de inteligencia frente a amenazas de Azure Security Center pueden ayudarle a aprender más sobre una amenaza que ha generado una alerta de seguridad.

## <a name="what-is-a-threat-intelligence-report"></a>¿Qué es un informe de inteligencia frente a amenazas?
Detección de amenazas de centro de seguridad funciona mediante la supervisión de la información de seguridad de los recursos de Azure, red de Hola y soluciones de socios conectados. Analiza esta información, a menudo correlacionar información procedente de varios orígenes, tooidentify amenazas. Este proceso es parte del centro de seguridad de hello [las capacidades de detección](security-center-detection-capabilities.md).

Cuando Security Center identifica una amenaza, desencadena una [alerta de seguridad](security-center-managing-and-responding-alerts.md), que contiene información detallada sobre un evento determinado, junto con sugerencias para remediarlo. los equipos de respuesta a incidentes de tooassist investigación y corregir las amenazas, centro de seguridad incluye un informe de inteligencia de amenazas que contiene información sobre la amenaza de Hola que se ha detectado, incluida información como el:

* Identidad o asociaciones del atacante (si esta información está disponible)
* Objetivos de los atacantes
* Campañas de ataques históricas y actuales (si esta información está disponible)
* Tácticas, herramientas y procedimientos de los atacantes
* Indicadores asociados de peligro (IoC), como direcciones URL y hash de archivo
* Victimology, que es tooassist prevalencia geográfica y del sector de hello en determinar si los recursos de Azure están en riesgo
* Información de corrección y mitigación

> [!NOTE]
> cantidad de Hola de información en cualquier informe determinado variarán; nivel de Hola de detalle se basa en la actividad y la prevalencia de hello malware.
>
>

Centro de seguridad tiene tres tipos de informes de amenazas, que pueden variar de ataque de toohello correspondiente. informes de Hello disponibles son:

* **Informe de grupo de actividad**: proporciona información detallada sobre los atacantes, sus objetivos y las tácticas que empelan.
* **Informe de campaña**: se centra en los detalles de campañas de ataque específicas.
* **Informe de resumen de amenazas**: cubre todos los elementos de hello en los informes de dos anterior Hola.

Este tipo de información es muy útil durante hello [respuesta a incidentes](security-center-incident-response.md) procesos, donde hay un origen de hello toounderstand de investigación en curso de ataque de hello, motivaciones del atacante hello y qué toodo toomitigate esto problema en el futuro.

## <a name="how-tooaccess-hello-threat-intelligence-report"></a>¿Cómo tooaccess Hola informes de inteligencia de amenazas?
Puede revisar las alertas actuales examinando hello **alertas de seguridad** icono. Abra Hola Portal de Azure y siga estos pasos hello toosee más detalles sobre cada alerta:

1. En el panel del centro de seguridad de hello, verá hello **alertas de seguridad** icono.
2. Haga clic en Hola mosaico tooopen Hola **alertas de seguridad** hoja que contiene información más detallada acerca de las alertas de Hola y haga clic en la alerta de seguridad de Hola que desea tooobtain obtener más información acerca de.

    ![Alertas de seguridad](./media/security-center-threat-report/security-center-threat-report-fig1.png)
3. En este caso Hola **sospechosa proceso ejecutado** hoja muestra los detalles de Hola de alerta de hello tal y como se muestra en la siguiente ilustración de hello:

    ![Detalles de alerta de seguridad](./media/security-center-threat-report/security-center-threat-report-fig2.png)
4. cantidad de Hola de información disponible para cada alerta de seguridad variará correspondiente de toohello de tipo de alerta. Hola **informes** campo que tiene un informe de inteligencia de amenazas de vínculo toohello. Haga clic en él. Aparecerá otra ventana del explorador con el archivo PDF.

   ![Selección de almacenamiento](./media/security-center-threat-report/security-center-threat-report-fig3.png)

Desde aquí puede descargar Hola PDF para este informe y para leer que más acerca de la seguridad de hello emiten que se detectó y realizar acciones basadas en información de hello proporcionada.

## <a name="see-also"></a>Otras referencias
En este documento, ha aprendido cómo los informes de inteligencia frente a amenazas de Azure Security Center pueden ayudar durante una investigación sobre alertas de seguridad. toolearn más información acerca del centro de seguridad de Azure, vea Hola recursos siguientes:

* [Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md). Busque las preguntas más frecuentes sobre el uso de servicio de Hola.
* [Cómo aprovechar Azure Security Center para dar respuesta a incidentes](security-center-incident-response.md)
* [Funcionalidades de detección de Azure Security Center](security-center-detection-capabilities.md)
* [Guía de planeamiento y operaciones de Azure Security Center](security-center-planning-and-operations-guide.md). Obtenga información acerca de cómo tooplan y entender las consideraciones de diseño de hello tooadopt Azure Security Center.
* [Toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md). Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Control de incidentes de seguridad en Azure Security Center](security-center-incident.md)
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/). Encuentre artículos de blog sobre el cumplimiento y la seguridad de Azure.
