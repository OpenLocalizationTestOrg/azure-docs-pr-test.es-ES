---
title: aaaCustomize Suite de IoT de Azure conectado generador | Documentos de Microsoft
description: "Una descripción de cómo toocustomize comportamiento de Hola de hello había conectado fábrica preconfigurado solución."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: c#
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 53f2fef7a76b5d8e6ad023945a7812dc7fabd12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a>Personalizar cómo Hola conectado generador solución muestra los datos de los servidores de OPC UA

## <a name="introduction"></a>Introducción

Hello generador conectado solución agrega y muestra los datos de hello OPC UA servidores conectados toohello solución. Puede examinar y enviar comandos toohello OPC UA servidores de la solución. Para obtener más información sobre OPC UA, vea hello [conectado generador preguntas más frecuentes sobre](iot-suite-faq-cf.md).

Indicadores clave de rendimiento (KPI) que puede ver en el panel de hello en los niveles de estación, línea y generador de Hola y de saludo eficacia general de equipos (OEE) son ejemplos de datos agregados en la solución de Hola. Hello captura de pantalla siguiente muestra los valores OEE y KPI de Hola para hello **ensamblado** estación en **producción línea 1**, Hola **Munich** fábrica:

![Ejemplo de valores de OEE y KPI de solución de Hola][img-oee-kpi]

habilita la solución Hola se tooview obtener información de elementos de datos específicos de Hola servidores OPC UA, denominados *estaciones*. Hello captura de pantalla siguiente muestra gráficos del número de Hola de artículos fabricados desde una estación específica:

![Trazados del número de artículos fabricados][img-manufactured-items]

Si hace clic en uno de los gráficos de hello, puede explorar los datos de hello mediante visión de Series de tiempo (ETI):

![Exploración de datos con Time Series Insights][img-tsi]

En este artículo se describe:

- Cómo datos Hola estará disponible toohello distintas vistas de solución de Hola.
- Cómo personalizar soluciones de Hola de manera hello muestra los datos de Hola.

## <a name="data-sources"></a>Orígenes de datos

Hola generador conectado solución muestra datos de hello OPC UA servidores conectados toohello solución. instalación predeterminada de Hello incluye varios servidores de OPC UA ejecuta una simulación de fábrica. Puede agregar sus propios servidores OPC UA que [conectarse a través de una puerta de enlace] [ lnk-connect-cf] tooyour solución.

Puede examinar los elementos de datos de Hola que un servidor de OPC UA conectado puede enviar tooyour solución en el panel de hello:

1. Navegue toohello **seleccionar un servidor de OPC UA** vista:

    ![Navegue toohello seleccione una vista de servidor de OPC UA][img-select-server]

1. Seleccione un servidor y haga clic en **Connect** (Conectar). Haga clic en **continuar** cuando aparezca la advertencia de seguridad de Hola.

    > [!NOTE]
    > Esta advertencia sólo aparece una vez para cada servidor y establece una relación de confianza entre el panel de la solución de Hola y el servidor de Hola.

1. Ahora puede examinar de elementos de datos Hola Hola server pueden enviar toohello solución. Elementos que se envían toohello solución tienen una marca de verificación verde:

    ![Elementos publicados][img-published]

1. Si eres un *administrador* en soluciones de hello, puede elegir toopublish un toomake de elemento de datos estén disponibles en hello conectado solución de fábrica. Como administrador, también puede cambiar el valor de Hola de elementos de datos y llamar a métodos en hello servidor OPC UA.

## <a name="map-hello-data"></a>Asignar datos de Hola

Hola conectado mapas de solución de fábrica y Hola de agrega elementos de datos publicados de hello OPC UA server toohello distintas vistas en soluciones de Hola. Hello generador conectado solución implementa tooyour cuenta de Azure al aprovisionar solución Hola. Un archivo JSON en hello soluciones de Visual Studio conectado generador almacena esta información de asignación. Puede ver y modificar este archivo de configuración de JSON en fábrica conectado de hello solución de Visual Studio. Puede volver a implementar soluciones de hello después de realizar un cambio.

Puede usar el archivo de configuración de Hola para:

- Editar generadores simulada existente de hello, líneas de producción y las estaciones.
- Asignar datos de servidores de OPC UA reales que se conecta toohello solución.

tooclone una copia del programa Hola conectado solución de Visual Studio de fábrica, Hola de uso siguiente comando de git:

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

archivo hello **ContosoTopologyDescription.json** define Hola elementos toohello vistas en panel de solución de fábrica conectado Hola de asignación de datos del servidor de OPC UA Hola. Puede encontrar este archivo de configuración en hello **Contoso\Topology** carpeta Hola **WebApp** proyecto Hola solución de Visual Studio.

contenido de Hola de archivo JSON de hello se organiza como una jerarquía de nodos de estación, línea de producción y generador. Esta jerarquía define la jerarquía de navegación de hello en panel de fábrica conectado Hola. Los valores en cada nodo de jerarquía de hello determinarán información de hello aparecen en el panel de Hola. Por ejemplo, archivo JSON de hello contiene Hola siguiendo los valores de fábrica Munich hello:

```json
"Guid": "73B534AE-7C7E-4877-B826-F1C0EA339F65",
"Name": "Munich",
"Description": "Braking system",
"Location": {
    "City": "Munich",
    "Country": "Germany",
    "Latitude": 48.13641,
    "Longitude": 11.57754
},
"Image": "munich.jpg"
```

nombre de hello, descripción y ubicación aparecen en esta vista en el panel de hello:

![Datos de Munich en panel de Hola][img-munich]

Cada factoría, línea de producción y estación tiene una propiedad de imagen. Puede encontrar estos archivos JPEG en hello **Content\img** carpeta Hola **WebApp** proyecto. Estos archivos de imagen se muestran en el panel Generador conectado de Hola.

Cada estación incluye varias propiedades detalladas que definen Hola de hello OPC UA al asignar elementos de datos. Estas propiedades se describen en las secciones siguientes de hello:

### <a name="opcuri"></a>OpcUri

Hola **OpcUri** valor es hello OPC UA URI de la aplicación que identifica de forma única Hola servidor OPC UA. Por ejemplo, hello **OpcUri** valor de la estación de ensamblado de hello en la línea de producción 1 de Munich aspecto Hola siguientes: **urn: scada2194:ua:munich:productionline0:assemblystation**.

Puede ver Hola URI de servidores de agente de usuario de OPC Hola conectado en el panel de la solución de hello:

![Vista de URI del servidor de OPC UA][img-server-uris]

### <a name="simulation"></a>Simulation

Hola información de hello **simulación** nodo es toohello específico simulación de OPC UA que se ejecuta en hello servidores OPC UA aprovisionados de forma predeterminada. No se utiliza para un servidor de OPC UA real.

### <a name="kpi1-and-kpi2"></a>Kpi1 y Kpi2

Estos nodos describen cómo los datos de la estación de hello contribuyen toohello dos valores KPI en el panel de Hola. En una implementación predeterminada, estos valores de KPI son unidades por hora y kWh por hora. solución de Hello calcula los valores KPI en el nivel de Hola de una estación y los agrega a la línea de producción de hello y niveles de fábrica.

Cada KPI tiene un valor mínimo, máximo y de destino. Cada valor KPI también puede definir acciones de alerta para tooperform de solución de fábrica de hello conectado. Hello fragmento de código siguiente muestra las definiciones de KPI de Hola para estación de ensamblado de hello en la línea de producción 1 de Munich:

```json
"Kpi1": {
  "Minimum": 150,
  "Target": 300,
  "Maximum": 600
},
"Kpi2": {
  "Minimum": 50,
  "Target": 100,
  "Maximum": 200,
  "MinimumAlertActions": [
    {
      "Type": "None"
    }
  ]
}
```

Hello siguiente captura de pantalla muestra datos KPI de hello en el panel de Hola.

![Información de KPI en el panel de Hola][lnk-kpi]

### <a name="opcnodes"></a>OpcNodes

Hola **OpcNodes** identifican nodos Hola elementos de datos publicados de hello servidor OPC UA y especificar cómo tooprocess esos datos.

Hola **NodeId** valor identifica Hola específicas OPC UA NodeID de hello servidor OPC UA. primer nodo de Hello en estaciones de ensamblado de hello para la línea de producción 1 en Munich tiene un valor **ns = 2; = 385**. A **NodeId** valor especifica hello tooread de elemento de datos de hello y Hola servidor OPC UA **nombre** proporciona un nombre descriptivo toouse en el panel de Hola para esos datos.

Otros valores asociados a cada nodo se resumen en hello en la tabla siguiente:

| Valor | Descripción |
| ----- | ----------- |
| Relevancia  | valores KPI y OEE Hola estos datos contribuyen a. |
| OpCode     | ¿Cómo se agregan datos Hola. |
| Unidades      | Hola toouse de unidades en el panel de Hola.  |
| Visible    | Si toodisplay este valor en el panel de Hola. Algunos valores se utilizan en los cálculos pero no se muestran.  |
| Máxima    | valor máximo de Hola que genera una alerta en el panel de Hola. |
| MaximumAlertActions | Tootake de una acción de alerta de tooan de respuesta. Por ejemplo, enviar una estación de tooa de comando. |
| ConstValue | Un valor constante que se usa en un cálculo. |

## <a name="deploy-hello-changes"></a>Implementar los cambios de Hola

Cuando haya terminado de realizar cambios toohello **ContosoTopologyDescription.json** archivo, debe volver a implementar Hola conectado generador solución tooyour cuenta de Azure.

Hola **-iot-conectado-factory de azure** repositorio incluye un **build.ps1** secuencia de comandos de PowerShell que puede usar toorebuild e implementar soluciones de Hola.

## <a name="next-steps"></a>Pasos siguientes

Obtener más información sobre solución de fábrica preconfigurado Hola conectado por leer Hola siguientes artículos:

* [Tutorial de la solución preconfigurada de fábrica conectada][lnk-rm-walkthrough]
* [Implementación de una puerta de enlace para una solución de fábrica conectada][lnk-connect-cf]
* [Permisos en el sitio de hello azureiotsuite.com][lnk-permissions]
* [Preguntas más frecuentes sobre fábrica conectada](iot-suite-faq-cf.md)
* [Preguntas más frecuentes][lnk-faq]


[img-oee-kpi]: ./media/iot-suite-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-suite-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-suite-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-suite-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-suite-connected-factory-customize/published.png
[img-munich]: ./media/iot-suite-connected-factory-customize/munich.png
[img-server-uris]: ./media/iot-suite-connected-factory-customize/serveruris.png
[lnk-kpi]: ./media/iot-suite-connected-factory-customize/kpidisplay.png

[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md