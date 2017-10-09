---
title: "mantenimiento aaaPredictive preconfigurado solución | Documentos de Microsoft"
description: "Una descripción de un mantenimiento predictivo hello Azure IoT conjunto preconfigurado de solución."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a>Información general de la solución preconfigurada de mantenimiento predictivo

Hola *mantenimiento predictivo* [preconfigurado solución] [ lnk_preconfigured_solutions] es uno de hello [Microsoft Azure IoT Suite] [ lnk_iot_suite] soluciones preconfiguradas. Esta solución integra la colección de telemetría del dispositivo en tiempo real con un modelo predictivo creado mediante [Azure Machine Learning][lnk-machine-learning].

Con el conjunto de IoT de Azure, puede rápidamente y fácilmente conectarse tooand activos de monitor y analizar la telemetría en tiempo real en los paneles y las visualizaciones. En la solución de un mantenimiento predictivo hello, visualizaciones y los paneles de hello proporcionan nueva inteligencia que puede impulsar las eficiencias y mejorar los flujos de ingresos.

## <a name="hello-scenario"></a>Hola escenario

Fabrikam es una compañía de líneas aéreas regional que se centra en la fantástica experiencia del cliente en los precios competitivos. Una causa de los retrasos en los vuelos son los problemas de mantenimiento y el mantenimiento de los motores de los aviones supone especialmente un desafío. Fabrikam debe evitar el error del motor durante el vuelo a toda costa, así que inspecciona sus motores con regularidad y programa según tooa plan de mantenimiento. Sin embargo, siempre no usan motores de avión Hola igual. En los motores se realizan algunas tareas de mantenimiento innecesarias. Lo que es aún más importante, surgen problemas que pueden hacer que un avión quede inmovilizado hasta que se realice el mantenimiento. Si un avión está en una ubicación donde Hola derecho técnicos o piezas de recambio no están disponibles, estos problemas pueden ser especialmente costosos.

motores de Hola de avión de Fabrikam se instrumentan con sensores que supervisan las condiciones del motor durante el tránsito. Fabrikam utiliza Hola mantenimiento predictivo solución toocollect Hola sensor datos recopilados durante la caja de Hola. Después de acumular años de funcionamiento del motor y datos de error, científicos de datos de Fabrikam modelan un hello toopredict de manera vida útil restante (RUL) de un motor de avión. modelo de Hello usa una correlación entre los datos de cuatro de sensores de motor de Hola y desgaste motor que provoca el error tooeventual. Mientras Fabrikam continúa tooensure seguridad de tooperform inspecciones periódicas, ahora puede usar Hola modelos toocompute Hola RUL para cada motor después de cada vuelo. modelo de Hello usa telemetría Hola recopilada de los motores de Hola durante el vuelo de Hola. Fabrikam puede predecir ahora de antemano los puntos futuros de error y el plan de mantenimiento y reparación.

> [!NOTE]
> modelo de solución de Hello usa datos de uso reales del motor.

Al predecir punto hello cuando se requiere mantenimiento, Fabrikam puede optimizar el costo que implica operaciones tooreduce.

Los coordinadores de mantenimiento trabajan con programadores para:

- Plan de mantenimiento toocoincide con un avión detener en una ubicación concreta.
- Asegúrese de que el tiempo suficiente está disponible para hello avión toobe fuera de servicio sin causar interrupciones de programación.
- tooschedule tooensure de técnicos que avión se atiende de forma eficaz sin tiempo de espera.

Los administradores del control de inventario reciben planes de mantenimiento para poder optimizar su proceso de realización de pedidos y el inventario de las piezas de repuesto.

Estas actividades habilitar hora de tierra de Fabrikam toominimize avión y reducen los costos operativos al garantizar la seguridad de Hola de pasajeros y personal.

toounderstand cómo [Azure IoT Suite] [ lnk_iot_suite] proporciona capacidades de hello los clientes necesitan potencial de hello toorealize del mantenimiento predictivo, revise esta [infografía] [lnk_infographic].

## <a name="how-hello-predictive-maintenance-solution-is-built"></a>Cómo se crea la solución de un mantenimiento predictivo Hola

solución de Hello utiliza un modelo de aprendizaje automático de Azure existente disponible como una plantilla tooshow estas capacidades trabajar de telemetría de dispositivo que se recopilan a través de servicios IoT Suite. Microsoft ha creado un [modelo de regresión] [ lnk_regression_model] de un motor de avión basándose en los datos disponibles públicamente<sup>\[1\]</sup>y paso a paso instrucciones sobre cómo toouse Hola modelo.

Hola solución de un mantenimiento predictivo IoT de Azure usa el modelo de regresión de hello creado desde esta plantilla. modelo de Hello es implementado en su suscripción de Azure y se expone a través de una API generada automáticamente. solución de Hello incluye un subconjunto de datos que representa 4 (del total de 100) de prueba de hello motores y secuencias de datos del sensor de hello 4 (de 21 total). Estos datos son suficiente tooprovide un resultado exacto del modelo entrenado Hola.

*\[1\] A. Saxena and K. Goebel (2008). "Conjunto de datos de simulación de degradación del motor de turbofán", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*

## <a name="get-started-with-predictive-maintenance"></a>Introducción al mantenimiento predictivo

Este tutorial muestra cómo tooprovision Hola solución mantenimiento predictivo. También le guía a través de características básicas de Hola de solución de un mantenimiento predictivo Hola. Puede tener acceso a muchas de estas características a través del panel de la solución de Hola que implementa junto con la solución de hello preconfigurado.

toocomplete este tutorial, necesita una suscripción activa de Azure.

> [!NOTE]
> En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para más información, consulte la [evaluación gratuita de Azure][lnk_free_trial].

1. Inicie sesión demasiado[azureiotsuite.com] [ lnk-azureiotsuite] con Azure credenciales de cuenta y haga clic en  **+**  toocreate una solución.
1. Haga clic en **seleccione** hello **mantenimiento predictivo** icono.
1. Escriba un **nombre** para la solución preconfigurada de mantenimiento predictivo.
1. Seleccione hello **región** y **suscripción** desea toouse tooprovision Hola solución.
1. Haga clic en **crear solución** hello toobegin proceso de aprovisionamiento. Este proceso suele tarda varios toorun minutos.

### <a name="wait-for-hello-provisioning-process-toocomplete"></a>Espere hello toocomplete del proceso de aprovisionamiento

1. Haga clic en el icono de hello para la solución con **Provisioning** estado.
1. Hola aviso **aprovisionamiento estados** tal y como se implementan los servicios de Azure en su suscripción de Azure.
1. Una vez que finalice el aprovisionamiento, Hola cambios de estado demasiado**listo**.
1. Haga clic en detalles del hello toosee Hola icono de la solución en el panel derecho de Hola. En este panel, puede iniciar Hola solución panel y acceso Hola aprendizaje automático área de trabajo.

> [!NOTE]
> Si encuentra problemas al implementar soluciones de hello preconfigurado, consulte [permisos en el sitio de hello azureiotsuite.com] [ lnk-permissions] hello y [preguntas más frecuentes sobre] [ lnk-faq]. Si continúan los problemas de hello, crear un vale de servicio en hello [portal][lnk-portal].

¿Hay detalles que se esperaría toosee que no aparezcan para su solución? Puede sugerirnos nuevas características en [User Voice](https://feedback.azure.com/forums/321918-azure-iot)(La voz del usuario).

## <a name="view-hello-solution"></a>Solución de hello de vista

Esta sección le guía a través de la solución de hello interfaz de usuario.

### <a name="predictive-maintenance-dashboard"></a>Panel de mantenimiento predictivo 

Esta página de aplicación web de hello usa controles de PowerBI JavaScript (vea hello [repositorio de PowerBI-visuals][lnk-powerbi]) toovisualize:

* datos de salida de Hello de trabajos de análisis de transmisiones de hello en almacenamiento de blobs.
* Hola RUL y ciclo de recuento por el motor de avión.

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a>Observar el comportamiento de Hola de solución de nube de Hola

En la consulta Hola portal de Azure, navegue toohello grupo de recursos con nombre de la solución de hello eligió tooview los recursos aprovisionados.

![][img-resource-group]

Al aprovisionar solución Hola preconfigurado, recibirá un correo electrónico con un área de trabajo de aprendizaje automático de toohello de vínculo. También puede navegar el área de trabajo de aprendizaje automático de toohello de hello [azureiotsuite.com] [ lnk-azureiotsuite] página para su solución de aprovisionamiento. Un icono está disponible en esta página cuando la solución de Hola Hola **listo** estado.

![][img-machine-learning]

En el portal de solución de hello, puede ver que ese ejemplo Hola está proporcionado de avión de dos dispositivos simulados cuatro toorepresent con dos motores por avión, cada uno con cuatro sensores. Cuando desplace portal de solución de toohello por primera vez, se ha detenido simulación de Hola.

![][img-simulation-stopped]

Haga clic en **iniciar simulación** simulación de hello toobegin. Hola historial de sensor, RUL, ciclos y RUL historial rellenar panel Hola.

![][img-simulation-running]

Cuando RUL es inferior a 160 (un umbral arbitrario elegido para fines de demostración), portal de solución de hello muestra un toohello siguiente de símbolo de advertencia RUL mostrar. portal de solución de Hello también resalta el motor de avión de hello en amarillo. Observe cómo los valores de hello RUL tienen una tendencia hacia abajo general general, pero suelen toobounce arriba y abajo. Este comportamiento da como resultado de diversas longitudes de ciclo de Hola y precisión del modelo Hola.

![][img-simulation-warning]

simulación completa de Hello tarda aproximadamente 35 toocomplete minutos 148 ciclos. umbral de Hello 160 RUL se cumple para hello primera vez en unos 5 minutos y dos motores ha alcanzado el umbral de hello en aproximadamente 8 minutos.

simulación de Hola se ejecuta a través del conjunto de datos completo de Hola para 148 ciclos y abona en valores finales RUL y ciclo.

Puede detener la simulación de Hola en cualquier punto, pero al hacer clic en **iniciar simulación** las reproducciones Hola simulación desde el principio de hello del conjunto de datos de Hola.

## <a name="next-steps"></a>Pasos siguientes

más información acerca de cómo IoT de Azure permite escenarios de un mantenimiento predictivo, leer toolearn [capturar el valor de Internet de las cosas hello][lnk_capture_value].

Tomar una [tutorial] [ lnk-predictive-walkthrough] de solución de un mantenimiento predictivo Hola.

También puede explorar algunas de hello otras características y capacidades de hello IoT preconfigurado soluciones:

* [Preguntas más frecuentes sobre el Conjunto de aplicaciones de IoT][lnk-faq]
* [Seguridad de IoT de hello masa][lnk-security-groundup]

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/