---
title: "aaaAzure IoT Suite conectado información general sobre generador | Documentos de Microsoft"
description: "Una descripción de hello Azure IoT Suite conectado solución preconfigurada de fábrica."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a>Empezar a trabajar con soluciones de fábrica preconfigurado Hola conectado

Conjunto de Azure IoT [soluciones preconfiguradas] [ lnk-preconfigured-solutions] combinar varias IoT de Azure servicios toodeliver-to-end soluciones que implementan escenarios empresariales IoT. Hola *generador conectado* solución preconfigurada conecta tooand supervisa los dispositivos industriales. Puede usar Hola solución tooanalyze Hola flujo de datos de los dispositivos y la productividad operativa toodrive y la rentabilidad.

Este tutorial muestra cómo tooprovision Hola conectado fábrica preconfigurado solución. También le guía a través de características básicas de Hola de solución de hello preconfigurado. Puede tener acceso a muchas de estas características de solución de hello *panel* que implementa como parte de la solución de hello preconfigurado:

![panel de la solución preconfigurada de fábrica conectada][img-cf-home]

toocomplete este tutorial, necesita una suscripción activa de Azure.

> [!NOTE]
> En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para más información, consulte la [evaluación gratuita de Azure][lnk_free_trial].
> 
> 

## <a name="provision-hello-solution"></a>Solución de Hola de aprovisionamiento

1. Inicie sesión con sus credenciales de cuenta de Azure de tooazureiotsuite.com y haga clic en "**+**" toocreate una solución.
2. Haga clic en **seleccione** en hello **generador conectado** icono.
3. Escriba un valor en **Nombre de la solución** para la solución preconfigurada de fábrica conectada.
4. Seleccione hello **suscripción** y **región** desea toouse tooprovision Hola solución.
5. Haga clic en **crear solución** hello toobegin proceso de aprovisionamiento. Este proceso suele tarda varios toorun minutos.

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a>Mientras esperan hello toocomplete del proceso de aprovisionamiento

1. Haga clic en el icono de hello para la solución con **Provisioning** estado.
2. Hola aviso **aprovisionamiento estados** tal y como se implementan los servicios de Azure en su suscripción de Azure.
3. Una vez que finalice el aprovisionamiento, Hola cambios de estado demasiado**listo**.
4. Haga clic en detalles del hello toosee Hola icono de la solución en el panel derecho de Hola.

> [!NOTE]
> Si encuentra problemas al implementar soluciones de hello preconfigurado, consulte [permisos en el sitio de hello azureiotsuite.com] [ lnk-permissions] hello y [conectado generador preguntas más frecuentes sobre](iot-suite-faq-cf.md). Si continúan los problemas de hello, crear un vale de servicio en hello [portal][lnk-portal].

¿Hay detalles que se esperaría toosee que no aparezcan para su solución? Puede sugerirnos nuevas características en [User Voice](https://feedback.azure.com/forums/321918-azure-iot)(La voz del usuario).

## <a name="scenario-overview"></a>Información general de escenario

Al implementar Hola conectado fábrica preconfigurado solución, se rellena previamente con recursos que le permiten toostep a través de un escenario industrial común. En este escenario, varias fábricas conectan informes de solución de toohello toocompute requiere valores de los datos de Hola la eficacia general de equipos (OEE) y los indicadores clave de rendimiento (KPI). Hello las secciones siguientes muestran cómo para:

* Supervisar los valores de la fábrica, las líneas de producción, el valor de OEE de las estaciones y los valores de KPI
* Analizar los datos de telemetría de hello generados a partir de estos dispositivos con visión de serie de tiempo de Azure
* Actuar sobre los problemas de toofix de alertas

Una característica clave de este escenario es que puede realizar todas estas acciones de forma remota desde el panel de la solución de Hola. No es necesario dispositivos toohello de acceso físico.

## <a name="view-hello-solution-dashboard"></a>Panel de vista Hola solución

panel de la solución de Hello permite toomanage solución de hello implementado. Es una representación jerárquica de una configuración de fábrica global. Por ejemplo, puede ver los valores de OEE y KPI, publicar nuevos nodos para telemetría y actuar sobre las alertas.

1. Cuando el aprovisionamiento de hello está completado e indica el icono de Hola para su solución preconfigurada **listo**, elija **iniciar** tooopen el portal de solución de fábrica conectados en una nueva pestaña.

    ![Iniciar solución de hello preconfigurado][img-launch-solution]

1. De forma predeterminada, el portal de solución de hello muestra hello *panel*. toonavigate tooother áreas del portal de hello, use menú de hello en el lado izquierdo de Hola de página de Hola.

    ![Panel de la solución preconfigurada de fábrica conectada][cf-img-menu]

panel de Hello muestra hello siguiente información:

* A **lista generador** panel que muestra el estado de hello, la ubicación y la configuración de producción actual de solución de Hola. Cuando ejecuta por primera vez solución hello, hay un número de dispositivos simulados. simulación de la línea de producción de Hello se compone de tres real OPC UA servidores por línea de producción que realicen tareas simuladas y compartan datos. Para obtener más información sobre OPC UA, vea hello [conectado generador preguntas más frecuentes sobre](iot-suite-faq-cf.md).
* A **mapa** que muestra hello ubicación de cada dispositivo conectado toohello solución. solución de Hello puede utilizar información de tooplot de API de Bing Maps de hello en el mapa de Hola. Si la suscripción está habilitada para la API de Bing Maps Enterprise, esta característica se usa automáticamente. Si no es así, consulte hello [preguntas más frecuentes sobre] [ lnk-faq] toolearn cómo toomake Hola dinámicos de mapa.
* Un panel de **Alertas**, que muestra las alertas generadas cuando un valor de OEE, KPI o telemetría supera un umbral específico.
* Un **la eficacia general de equipos** panel que muestra valores de hello OEE para toda la empresa Hola o generador de Hola o de producción de línea/estación está viendo. Este valor se agrega desde el nivel de empresa de hello estación vista toohello. ilustración de Hello OEE y sus elementos constituyentes se pueden analizar aún más.
* **Indicadores clave de rendimiento** panel que muestra hello número de unidades producidas y energía usada por toda la empresa Hola o línea de fábrica o de producción de hello/estación está viendo. Estos valores se agregan desde un nivel de empresa de estación vista toohello.

## <a name="view-factories"></a>Visualización de fábricas

Hola *generadores* Hola ubicación geográfica de todos los generadores de hello en soluciones de hello, su estado y la configuración de producción actual se muestra en el panel. Desde la lista de ubicaciones de hello, puede navegar toohello otros niveles de jerarquía de la solución de Hola. Hola lista Hola son hipervínculos que se vinculan los detalles de las líneas de producción de hello en esa ubicación. A continuación, es posible toodrill en los detalles de la línea de producción de hello y hacia abajo de la vista de nivel de estación de toohello. También puede aplicar una lista de toohello de filtros.

![Fábricas de la solución preconfigurada de fábrica conectada][cf-img-factories] 

1. Hola **panel Generador** muestra Hola lista de fábrica para esta solución.

2. lista de fábrica de Hello inicialmente muestra seis generadores creados por el proceso de aprovisionamiento de Hola. Puede agregar más dispositivos simulados y físicos toohello solución.

3. detalles de hello tooview de un generador, haga clic en la fila de hello en la lista de fábrica de Hola.

4. detalles de hello tooview de una línea de producción, haga clic en la fila de hello en lista de Hola.

5. tooview Hola publica nodos OPC UA de una estación en la línea de producción de hello, haga clic en lista de Hola de fila de Hola.

6. detalles de tooview en un nodo específico en la estación de hello, haga clic en la fila de hello en lista de Hola. Esta acción inicia el panel de contexto Hola con visualizaciones de visión de la serie de tiempo. Haga clic en estos gráficos toodo un análisis más profundo en entorno de explorador de hello visión de la serie de tiempo.

## <a name="view-map"></a>Visualización de mapas

Si su suscripción tiene acceso toohello API de Bing Maps, Hola *generadores* mapa muestra ubicación geográfica de Hola y el estado de todos los generadores de hello en soluciones de Hola. toodrill en los detalles de la ubicación de hello, haga clic en ubicaciones de Hola que se muestra en el mapa de Hola.

![Mapa de la solución preconfigurada de fábrica conectada][cf-img-map]

## <a name="view-alerts"></a>Visualización de alertas

Hola **alerta** panel muestra las alertas generadas debido tooa notifica el valor o un valor calculado de OEE o KPI que supera el umbral configurado. Este panel muestra las alertas en cada nivel de jerarquía de hello, desde Hola estación nivel toohello global ver. alertas de Hello contienen una descripción de alerta de hello, fecha, hora, ubicación y número de repeticiones. Puede obtener información en datos toohello que provocó la alerta hello mediante Hola información de la serie de tiempo. Hola tiempo serie visión datos se visualizarán en Hola alertas si procede. Si es administrador, puede realizar acciones predeterminadas en las alertas de hello como:

* Alerta de cierre Hola.
* Confirmar la alerta de Hola.

Si lo desea, puede realizar acciones más complejas. Por ejemplo, para hello nodo de agente de usuario de OPC presión de hello ensamblado se puede realizar:

* Mostrar información de soporte técnico en una página web de una nueva ventana del explorador.
* Mitigue la causa de Hola de alerta de hello mediante una llamada a un método de OPC UA en dispositivo Hola.
* Suprimir disponibilidad Hola de acciones predeterminadas de Hola.

    ![Alertas de la solución preconfigurada de fábrica conectada][cf-img-alerts]

> [!NOTE]
> Estas alertas se generan las reglas que se especifican en un archivo de configuración de solución de hello preconfigurado. Estas reglas pueden generar alertas cuando Hola OEE o cifras KPI o valores de los nodos de agente de usuario de OPC supera el umbral configurado.

1. Hola **panel alertas** muestra Hola alertas generadas en esta solución.

2. detalles de hello tooview de una alerta, haga clic en la alerta de hello en el panel de alertas de Hola.

3. toofurther analizar datos de alertas de hello, haga clic en gráfico de hello en entorno de explorador de hello panel alerta tooopen Hola visión de la serie de tiempo.

4. tooaddress Hola alerta, varias acciones están disponibles en el panel alertas Hola. Elija Hola la opción adecuada para usted y haga clic en hello ejecutar botón de comando de acción.

## <a name="view-overall-equipment-efficiency"></a>Ver la eficiencia general de equipos

Las tasas OEE Hola eficacia del proceso de fabricación de hello mediante una clave parámetros operativos relacionadas con la producción. OEE es una medida estándar se calcula multiplicando la velocidad de disponibilidad de hello, la velocidad de rendimiento y velocidad de calidad de la industria: OEE = disponibilidad x calidad del rendimiento x.

![OEE de la solución preconfigurada de fábrica conectada][cf-img-oee]

1. tooview OEE en cualquier nivel de jerarquía de hello, navegue toohello vista específica que necesite. Hola OEE para esa vista muestra en el panel de hello junto con cada uno de los elementos de Hola que componen el porcentaje OEE Hola.

2. toofurther analizar hello OEE para cualquier nivel de datos de la jerarquía de hello, haga clic en hello OEE, disponibilidad, rendimiento o porcentaje de calidad. Aparece un panel de contexto con información de la serie de tiempo alimentados visualizaciones que muestran datos de hello última hora, últimas 24 horas y últimos 7 días.

    ![Visualización TSI de la solución preconfigurada de fábrica conectada][cf-img-tsi-visualization]

3. toofurther analizar datos de alertas de hello, haga clic en gráfico de hello en el panel alertas Hola. Esta acción abre el entorno de explorador de hello visión de la serie de tiempo.

    ![Explorador de TSI de la solución preconfigurada de fábrica conectada][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a>Visualización de los indicadores clave de rendimiento

solución de Hello proporciona dos indicadores clave de rendimiento, *unidades por hora* y *energía utilizada en kWh*.

![KPI de la solución preconfigurada de fábrica conectada][cf-img-kpi]

1. unidades de tooview por hora o de energía utilizada en cualquier nivel de jerarquía de hello, navegue toohello vista específica que necesite. las unidades de Hola por hora y energía usan mostrar en el panel de Hola.

2. unidades de tooanalyze por hora o de energía utilizada en cualquier nivel de jerarquía de hello aún más, haga clic en medidor Hola Hola **indicadores clave de rendimiento** panel. Aparece un panel de contexto con visualizaciones de visión de la serie de tiempo con la tecnología de lo que los datos de tooview de hello última hora, Hola últimas 24 horas y los últimos 7 días.

## <a name="scenario-review"></a>Revisión del escenario

En este escenario, está supervisando los valores OEE y KPI de generadores, en el panel de Hola. A continuación, usó tooprovide visión de la serie de tiempo más información toohelp profundizar aún más los datos de telemetría de Hola para toohelp OEE y KPI con detección de anomalías. También usa tooview problemas de hello panel alerta con los generadores y usa alerta de hello acciones disponibles tooyou tooresolve Hola.

## <a name="other-features"></a>Otras características

Hola siguientes secciones describe algunas características adicionales de solución de fábrica de hello conectado que no se describen en el escenario anterior Hola.

## <a name="apply-filters"></a>Aplicación de filtros

1. Haga clic en hello **comillas angulares** toodisplay una lista de filtros disponibles en el panel de ubicaciones de fábrica de Hola o panel de alertas de Hola.

2. se muestra el panel de filtros de Hola para usted. 

    ![Filtros de la solución preconfigurada de fábrica conectada][cf-img-alert-filter]

3. Seleccione el filtro de Hola que necesite. También es posible tootype texto libre en los campos de filtro de Hola.

4. a continuación, se aplica el filtro de Hola para usted. También se muestra el estado del filtro Hello en panel de Hola a través de un embudo que muestra de generadores de Hola y tablas de alertas.

    ![Filtros de la solución preconfigurada de fábrica conectada][cf-img-alert-filter-funnel]

    > [!NOTE]
    > Un filtro activo no afecta a hello muestra valores OEE y KPI, solo filtra mostrar el contenido de Hola.

5. tooclear un filtro, haga clic en el embudo de Hola y haga clic en filtro en el panel de contexto de filtro de Hola. Hola texto **todos los** se muestra en los generadores de Hola y tablas de alertas.

## <a name="browse-an-opc-ua-server"></a>Examinar un servidor de OPC UA

Al implementar soluciones de hello preconfigurado, aprovisionar automáticamente los servidores de OPC UA simulados que se pueden examinar mediante el Explorador de soluciones de Hola. Estos servidores son *servidores de OPC UA simulados*. Servidores simulados facilitan automáticamente tooexperiment con la solución de hello preconfigurado sin Hola necesidad toodeploy real, físico los servidores. Si desea tooconnect una solución de toohello de servidor de OPC UA real, vea hello [conectarse a la solución de fábrica preconfigurado de OPC UA dispositivo toohello conectado] [ lnk-connect-cf] tutorial.

1. Haga clic en hello **icono generador** en la barra de navegación del panel de Hola.

    ![Explorador de servidores de la solución preconfigurada de fábrica conectada][cf-img-server-browser]

2. Elija uno de los servidores de Hola de lista preconfigurada Hola. Esta lista muestra los servidores de Hola que se implementan en soluciones de hello preconfigurado.

    ![Selección del servidor de la solución preconfigurada de fábrica conectada][cf-img-server-choice]

3. Haga clic en **Conectar**; aparece un cuadro de diálogo de seguridad. Simulación de hello, resulta seguro tooclick **continuar**

4. tooexpand cualquiera de los nodos de hello en el árbol de servidores de hello, haga clic en él. Los nodos que publican telemetría tienen una marca de verificación junto a ellos.

    ![Árbol de servidores de la solución preconfigurada de fábrica conectada][cf-img-server-tree]

5. Haga clic en un elemento tooread, escribir, publicar o llame a ese nodo. tooyou de Hello las acciones disponibles dependen de los permisos y atributos de hello del nodo de Hola. Hola lee opción toodisplays un panel de contexto Mostrar valor de Hola de nodo específico Hola. Hola escribir opción muestra un panel de contexto donde puede escribir un nuevo valor. opción de llamada de Hello muestra un nodo donde puede especificar parámetros de Hola para llamada Hola.

## <a name="publish-a-node"></a>Publicación de un nodo

Cuando se examina un *servidor simulado de OPC UA*, también puede elegir toopublish nuevos nodos. Puede analizar la telemetría de Hola de estos nodos de solución de Hola. Estos *simulados servidores OPC UA* que sea fácil tooexperiment con soluciones de hello preconfigurado sin implementar dispositivos físicos reales.

1. Buscar nodo tooa en el árbol del explorador de servidores de OPC UA que desea toopublish Hola.

2. Haga clic en el nodo de Hola.

3. Elija **Publicar**.

    ![Nodo de publicación de fábrica conectada][cf-img-publish-node]

4. Un panel de contexto aparece lo que indica que Hola de publicación se ha realizado correctamente. nodo de Hello aparece en la vista de nivel de estación de hello con una marca de verificación junto a él.

    ![Publicación correcta en la solución preconfigurada de fábrica conectada][cf-img-publish-success]

## <a name="command-and-control"></a>Comando y control

Hola conectado generador permite comandos y controlar los dispositivos de la industria directamente desde la nube de Hola. Puede usar este tooalerts de toorespond característica generados por dispositivo de Hola. Por ejemplo, podría enviar un dispositivo de toohello de comando de nube de Hola. Puede encontrar Hola comandos disponibles en hello **StationCommands** nodo de árbol del explorador de servidores de OPC UA Hola. En este escenario, se abrirá una válvula de versión en la estación de ensamblado hello de una línea de producción de Munich. funcionalidad de comando y control de hello toouse, debe estar en hello **administrador** rol para hello preconfigurado implementación de la solución.

1. Examinar toohello **StationCommands** nodo de árbol del explorador de servidores de OPC UA Hola.

2. Elija el comando de Hola que desea usar.

3. Haga clic en el nodo de Hola.

4. Elija **Llamada**.

    ![Comando de llamada de la solución preconfigurada de fábrica conectada][cf-img-call-command]

5. Aparece de un panel de contexto que le informa de qué método va toocall y los detalles de los parámetros es aplicable.

6. Elija **Llamada**.

    ![Contexto de llamada de la solución preconfigurada de fábrica conectada][cf-img-call-context]

7. panel de contexto de Hello es tooinform actualizado que Hola llamada al método se realizó correctamente. Puede comprobar llamada Hola leyendo Hola valor del nodo de presión de Hola que actualizado como resultado de llamada de Hola se realizó correctamente.

    ![Llamada correcta de la solución preconfigurada de fábrica conectada][cf-img-call-success]


## <a name="behind-hello-scenes"></a>Entre bastidores de Hola

Al implementar una solución preconfigurada, el proceso de implementación de hello crea varios recursos en hello Azure suscripción que ha seleccionado. Puede ver estos recursos en hello Azure [portal][lnk-portal]. proceso de implementación de Hello crea un **grupo de recursos** con un nombre basado en el nombre de Hola que elija para su solución preconfigurada:

![Solución preconfigurada en hello portal de Azure][img-cf-portal]

Puede ver configuración de Hola de cada recurso mediante su selección en la lista de Hola de recursos de grupo de recursos de Hola.

También puede ver el código fuente de hello para la solución de hello preconfigurado. Hello conectado fábrica preconfigurado solución código fuente está en hello [-iot-conectado-factory de azure] [ lnk-cfgithub] repositorio de GitHub:

Cuando haya terminado, puede eliminar solución Hola preconfigurado de su suscripción de Azure en hello [azureiotsuite.com] [ lnk-azureiotsuite] sitio. Este sitio le permite eliminar tooeasily que todos Hola recursos que estaban aprovisionados al crear soluciones de hello preconfigurado.

> [!NOTE]
> tooensure eliminar todos los elementos relacionados con la solución toohello preconfigurado, eliminarlo de hello [azureiotsuite.com] [ lnk-azureiotsuite] sitio. No se elimine el grupo de recursos de hello en el portal de Hola.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha implementado una solución de trabajo configurado preconfigurada, puede seguir introducción con Suite IoT leyendo Hola siguientes artículos:

* [Tutorial de la solución preconfigurada de fábrica conectada][lnk-rm-walkthrough]
* [Conectarse a la solución de fábrica conectado preconfigurado toohello de dispositivo][lnk-connect-cf]
* [Permisos en el sitio de hello azureiotsuite.com][lnk-permissions]

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md