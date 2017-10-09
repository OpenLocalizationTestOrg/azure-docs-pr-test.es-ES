---
title: aaaRespond toosecurity incidentes con el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento explica cómo toouse Azure Security Center para un escenario de respuesta a incidentes."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 8af12f1c-4dce-4212-8ac4-170d4313492d
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: aaf50c0c7e774d03d517c3fd11686dbae48dd29b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-security-center-for-an-incident-response"></a>Uso de Azure Security Center para dar respuesta a incidentes
Obtenga información acerca de muchas organizaciones cómo toorespond toosecurity incidentes únicamente después de sufrir un ataque. tooreduce costos y los daños, es importante toohave una respuesta a incidentes previsto en su lugar antes de que realiza un ataque. Azure Security Center puede usarse en distintas fases de una respuesta a incidentes.

## <a name="incident-response-planning"></a>Planeamiento de respuesta a incidentes
Un plan eficaz depende de tres funciones principales: ser capaz de tooprotect, detectar y responder toothreats. Protección es acerca de cómo evitar incidentes, detección se acerca de cómo identificar amenazas al principio y respuesta implica expulsar atacante hello e impactos de hello toomitigate de sistemas de una infracción de la restauración.

Este artículo utiliza fases de respuesta a incidentes de seguridad de Hola de hello [respuestas de seguridad de Microsoft Azure en hello en la nube](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678) artículo, como se muestra en hello siguiente diagrama:

![Ciclo de vida de respuesta a incidentes](./media/security-center-incident-response/security-center-incident-response-fig1.png)

Puede usar el centro de seguridad durante las fases de detectar, evaluar y diagnosticar de Hola. Estos son ejemplos de cómo el centro de seguridad pueden ser útil durante tres fases de respuesta a incidentes inicial hello:

* **Detectar**: Revise el primer indicio de Hola de una investigación de eventos.
  * Ejemplo: revisión Hola inicial comprobación que se generó una alerta de seguridad de alta prioridad en el panel del centro de seguridad de Hola.
* **Evaluar**: realizar Hola evaluación inicial tooobtain obtener más información sobre la actividad sospechosa Hola.
  * Ejemplo: obtener más información acerca de la alerta de seguridad de Hola.
* **Diagnosticar**: realizar una investigación técnica e identificar las estrategias de contención, mitigación y solución.
  * Ejemplo: siga los pasos de corrección de hello descritos por el centro de seguridad en esa alerta de seguridad determinada.

escenario de Hola que se indica a continuación se muestra cómo tooleverage centro de seguridad durante Hola detectar, evaluar y diagnosticar/responden fases de un incidente de seguridad. En Security Center, un [incidente de seguridad](security-center-incident.md) es la suma de todas las alertas de un recurso que se alinean con patrones de [cadenas de eliminación](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/). Incidentes aparecen en hello [alertas de seguridad](security-center-managing-and-responding-alerts.md) mosaico y hoja. Un incidente revela lista Hola de alertas relacionadas, lo que permite tooobtain obtener más información sobre cada repetición. Centro de seguridad también presenta independiente alertas de seguridad que también pueden ser utilizado tootrack hacia abajo una actividad sospechosa.

## <a name="scenario"></a>Escenario
Contoso había migrado recientemente algunos de su tooAzure de recursos locales, incluidas algunas cargas de trabajo de línea de negocio basadas en máquinas virtuales y bases de datos SQL. Actualmente el equipo de respuesta a incidentes de seguridad informática central de Contoso (CSIRT) tiene un problema para investigar asuntos de seguridad, debido a la falta de inteligencia de seguridad integrada en sus herramientas actuales de respuesta a incidentes. Esta falta de integración presenta un problema durante el saludo detectar fase (demasiados falsos positivos), así como durante la evaluación de Hola y fases de diagnosticar. Como parte de esta migración, decidió tooopt en para el centro de seguridad toohelp a resolver este problema.

Hola primera fase de esta migración terminada después de que esté incorporado todos los recursos a cabo todas las recomendaciones de seguridad de hello del centro de seguridad. Contoso CSIRT es Hola focal para tratar los incidentes de seguridad del equipo. equipo de Hello consta de un grupo de personas encargadas de tratar con los incidentes de seguridad. los miembros del equipo de Hello tener claramente definidos tooensure de tareas que no se deja área de respuesta detectado.

A fin de Hola de este escenario, vamos toofocus en roles de Hola de hello siguiendo los roles que forman parte de Contoso CSIRT:

![Ciclo de vida de respuesta a incidentes](./media/security-center-incident-response/security-center-incident-response-fig2.png)

Judy se encarga de las operaciones de seguridad. Entre sus responsabilidades están:

* Supervisar y responder toosecurity amenazas alrededor de reloj de Hola.
* Concentrar propietario de carga de trabajo de toohello en la nube o el analista de seguridad según sea necesario.

Sam es un analista de seguridad y sus responsabilidades incluyen:

* Investigar los ataques.
* Solucionar las alertas.
* Trabajar con toodetermine de propietarios de cargas de trabajo y las mitigaciones se aplican.

Como puede ver, Cristina y Sam también tienen responsabilidades diferentes, y deben trabajar conjuntamente tooshare información de centro de seguridad.

## <a name="recommended-solution"></a>Solución recomendada
Puesto que Cristina y Sam tienen distintos roles, usará áreas diferentes de información relevante de centro de seguridad tooobtain para sus actividades diarias. Judy usará las **alertas de seguridad** como parte de su supervisión diaria.

![Alertas de seguridad](./media/security-center-incident-response/security-center-incident-response-fig3.png)

Cristina utiliza alertas de seguridad durante su Hola detectar y las fases de evaluación. Al finalizar Cristina evaluación inicial de hello, puede escalar Hola problema tooSam si se requiere una investigación adicional. En este momento, Sam usará información de hello proporcionado por el centro de seguridad, en ocasiones, junto con otros orígenes de datos, toomove toohello diagnosticar fase.

## <a name="how-tooimplement-this-solution"></a>¿Cómo tooimplement esta solución
toosee Cómo usaría el centro de seguridad de Azure en un escenario de respuesta a incidentes, se le siga los pasos de Cristina en fases de detectar y evaluación de hello y, a continuación, consulte ¿Qué Sam problema de hello toodiagnose.

### <a name="detect-and-assess-incident-response-stages"></a>Etapas de detección y evaluación de respuesta a incidentes
Cristina firmado en toohello portal de Azure y se trabaja en la consola de centro de seguridad de Hola. Como parte de su actividades de supervisión de diario, iniciado revisión de seguridad de alta prioridad Hola de alertas mediante la realización de pasos:

1. Haga clic en hello **alertas de seguridad** Hola mosaico y acceso **alertas de seguridad** hoja.
    ![Hoja Alertas de seguridad](./media/security-center-incident-response/security-center-incident-response-fig4.png)

   > [!NOTE]
   > A fin de Hola de este escenario, Cristina es continuo tooperform una valoración de alerta de actividad de hello SQL malintencionado, tal como se muestra en hello anterior figura.
   >
   >
2. Haga clic en hello **actividad SQL malintencionado** de alerta y revise los recursos de un ataque de Hola Hola **actividad SQL malintencionado** hoja: ![detalles de incidentes](./media/security-center-incident-response/security-center-incident-response-fig5.png)

    En esta hoja, Cristina puede tomar notas con respecto a los recursos de un ataque de hello, cómo muchas veces este ataque se produjo y, cuando se ha detectado.
3. Haga clic en hello **atacadas recursos** tooobtain obtener más información acerca de este ataque.

Después de leer la descripción de hello, Cristina está convencida de que esto no es un falso positivo que ella debe y remitirlo a este tooSam mayúscula.

### <a name="diagnose-incident-response-stage"></a>Fases de diagnóstico de la respuesta a incidentes
SAM recibe el caso de hello de Cristina y revisar los pasos de corrección de Hola que sugiere el centro de seguridad inicia.

![Ciclo de vida de respuesta a incidentes](./media/security-center-incident-response/security-center-incident-response-fig6.png)

### <a name="additional-resources"></a>Recursos adicionales
equipo de respuesta a incidentes de Hello también puede sacar partido de hello [seguridad Centro de Power BI](security-center-powerbi.md) toosee distintos tipos de funcionalidad de informes. Estos informes pueden ayudarles a durante más toovisualize de investigación, analizar y filtrar las alertas de seguridad y recomendaciones. Para las empresas que usan su información de seguridad y la solución de administración (SIEM) de eventos durante el proceso de investigación de hello, también pueden [integrar centro de seguridad con la solución](security-center-integrating-alerts-with-log-integration.md). También se puede integrar los registros de auditoría de Azure y eventos de seguridad de máquina virtual (VM) mediante el uso de hello [herramienta de integración de Azure registros](https://blogs.msdn.microsoft.com/azuresecurity/2016/07/21/microsoft-azure-log-integration-preview/). tooinvestigate un ataque, puede usar esta información junto con información de Hola que proporciona el centro de seguridad.

## <a name="conclusion"></a>Conclusión
Reunir un equipo antes de que se produzca un incidente es muy importante tooyour organización e influirá positivamente cómo se administran los incidentes. Hola herramientas adecuadas toomonitor recursos pueden ayudar a este tooremediate de pasos precisos de tootake un incidente de seguridad de equipo. Centro de seguridad [las capacidades de detección](security-center-detection-capabilities.md) puede ayudar a incidentes de TI tooquickly responden toosecurity y corregir los problemas de seguridad.
