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
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="4d823-103">Personalizar cómo Hola conectado generador solución muestra los datos de los servidores de OPC UA</span><span class="sxs-lookup"><span data-stu-id="4d823-103">Customize how hello connected factory solution displays data from your OPC UA servers</span></span>

## <a name="introduction"></a><span data-ttu-id="4d823-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="4d823-104">Introduction</span></span>

<span data-ttu-id="4d823-105">Hello generador conectado solución agrega y muestra los datos de hello OPC UA servidores conectados toohello solución.</span><span class="sxs-lookup"><span data-stu-id="4d823-105">hello connected factory solution aggregates and displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="4d823-106">Puede examinar y enviar comandos toohello OPC UA servidores de la solución.</span><span class="sxs-lookup"><span data-stu-id="4d823-106">You can browse and send commands toohello OPC UA servers in your solution.</span></span> <span data-ttu-id="4d823-107">Para obtener más información sobre OPC UA, vea hello [conectado generador preguntas más frecuentes sobre](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="4d823-107">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

<span data-ttu-id="4d823-108">Indicadores clave de rendimiento (KPI) que puede ver en el panel de hello en los niveles de estación, línea y generador de Hola y de saludo eficacia general de equipos (OEE) son ejemplos de datos agregados en la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d823-108">Examples of aggregated data in hello solution include hello Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in hello dashboard at hello factory, line, and station levels.</span></span> <span data-ttu-id="4d823-109">Hello captura de pantalla siguiente muestra los valores OEE y KPI de Hola para hello **ensamblado** estación en **producción línea 1**, Hola **Munich** fábrica:</span><span class="sxs-lookup"><span data-stu-id="4d823-109">hello following screenshot shows hello OEE and KPI values for hello **Assembly** station, on **Production line 1**, in hello **Munich** factory:</span></span>

![Ejemplo de valores de OEE y KPI de solución de Hola][img-oee-kpi]

<span data-ttu-id="4d823-111">habilita la solución Hola se tooview obtener información de elementos de datos específicos de Hola servidores OPC UA, denominados *estaciones*.</span><span class="sxs-lookup"><span data-stu-id="4d823-111">hello solution enables you tooview detailed information from specific data items from hello OPC UA servers, called *stations*.</span></span> <span data-ttu-id="4d823-112">Hello captura de pantalla siguiente muestra gráficos del número de Hola de artículos fabricados desde una estación específica:</span><span class="sxs-lookup"><span data-stu-id="4d823-112">hello following screenshot shows plots of hello number of manufactured items from a specific station:</span></span>

![Trazados del número de artículos fabricados][img-manufactured-items]

<span data-ttu-id="4d823-114">Si hace clic en uno de los gráficos de hello, puede explorar los datos de hello mediante visión de Series de tiempo (ETI):</span><span class="sxs-lookup"><span data-stu-id="4d823-114">If you click one of hello graphs, you can explore hello data further using Time Series Insights (TSI):</span></span>

![Exploración de datos con Time Series Insights][img-tsi]

<span data-ttu-id="4d823-116">En este artículo se describe:</span><span class="sxs-lookup"><span data-stu-id="4d823-116">This article describes:</span></span>

- <span data-ttu-id="4d823-117">Cómo datos Hola estará disponible toohello distintas vistas de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d823-117">How hello data is made available toohello various views in hello solution.</span></span>
- <span data-ttu-id="4d823-118">Cómo personalizar soluciones de Hola de manera hello muestra los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d823-118">How you can customize hello way hello solution displays hello data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="4d823-119">Orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="4d823-119">Data sources</span></span>

<span data-ttu-id="4d823-120">Hola generador conectado solución muestra datos de hello OPC UA servidores conectados toohello solución.</span><span class="sxs-lookup"><span data-stu-id="4d823-120">hello connected factory solution displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="4d823-121">instalación predeterminada de Hello incluye varios servidores de OPC UA ejecuta una simulación de fábrica.</span><span class="sxs-lookup"><span data-stu-id="4d823-121">hello default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="4d823-122">Puede agregar sus propios servidores OPC UA que [conectarse a través de una puerta de enlace] [ lnk-connect-cf] tooyour solución.</span><span class="sxs-lookup"><span data-stu-id="4d823-122">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] tooyour solution.</span></span>

<span data-ttu-id="4d823-123">Puede examinar los elementos de datos de Hola que un servidor de OPC UA conectado puede enviar tooyour solución en el panel de hello:</span><span class="sxs-lookup"><span data-stu-id="4d823-123">You can browse hello data items that a connected OPC UA server can send tooyour solution in hello dashboard:</span></span>

1. <span data-ttu-id="4d823-124">Navegue toohello **seleccionar un servidor de OPC UA** vista:</span><span class="sxs-lookup"><span data-stu-id="4d823-124">Navigate toohello **Select an OPC UA server** view:</span></span>

    ![Navegue toohello seleccione una vista de servidor de OPC UA][img-select-server]

1. <span data-ttu-id="4d823-126">Seleccione un servidor y haga clic en **Connect** (Conectar).</span><span class="sxs-lookup"><span data-stu-id="4d823-126">Select a server and click **Connect**.</span></span> <span data-ttu-id="4d823-127">Haga clic en **continuar** cuando aparezca la advertencia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d823-127">Click **Proceed** when hello security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4d823-128">Esta advertencia sólo aparece una vez para cada servidor y establece una relación de confianza entre el panel de la solución de Hola y el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d823-128">This warning only appears once for each server and establishes a trust relationship between hello solution dashboard and hello server.</span></span>

1. <span data-ttu-id="4d823-129">Ahora puede examinar de elementos de datos Hola Hola server pueden enviar toohello solución.</span><span class="sxs-lookup"><span data-stu-id="4d823-129">You can now browse hello data items that hello server can send toohello solution.</span></span> <span data-ttu-id="4d823-130">Elementos que se envían toohello solución tienen una marca de verificación verde:</span><span class="sxs-lookup"><span data-stu-id="4d823-130">Items that are being sent toohello solution have a green check mark:</span></span>

    ![Elementos publicados][img-published]

1. <span data-ttu-id="4d823-132">Si eres un *administrador* en soluciones de hello, puede elegir toopublish un toomake de elemento de datos estén disponibles en hello conectado solución de fábrica.</span><span class="sxs-lookup"><span data-stu-id="4d823-132">If you are an *Administrator* in hello solution, you can choose toopublish a data item toomake it available in hello connected factory solution.</span></span> <span data-ttu-id="4d823-133">Como administrador, también puede cambiar el valor de Hola de elementos de datos y llamar a métodos en hello servidor OPC UA.</span><span class="sxs-lookup"><span data-stu-id="4d823-133">As an Administrator, you can also change hello value of data items and call methods in hello OPC UA server.</span></span>

## <a name="map-hello-data"></a><span data-ttu-id="4d823-134">Asignar datos de Hola</span><span class="sxs-lookup"><span data-stu-id="4d823-134">Map hello data</span></span>

<span data-ttu-id="4d823-135">Hola conectado mapas de solución de fábrica y Hola de agrega elementos de datos publicados de hello OPC UA server toohello distintas vistas en soluciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d823-135">hello connected factory solution maps and aggregates hello published data items from hello OPC UA server toohello various views in hello solution.</span></span> <span data-ttu-id="4d823-136">Hello generador conectado solución implementa tooyour cuenta de Azure al aprovisionar solución Hola.</span><span class="sxs-lookup"><span data-stu-id="4d823-136">hello connected factory solution deploys tooyour Azure account when you provision hello solution.</span></span> <span data-ttu-id="4d823-137">Un archivo JSON en hello soluciones de Visual Studio conectado generador almacena esta información de asignación.</span><span class="sxs-lookup"><span data-stu-id="4d823-137">A JSON file in hello Visual Studio connected factory solution stores this mapping information.</span></span> <span data-ttu-id="4d823-138">Puede ver y modificar este archivo de configuración de JSON en fábrica conectado de hello solución de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d823-138">You can view and modify this JSON configuration file in hello connected factory Visual Studio solution.</span></span> <span data-ttu-id="4d823-139">Puede volver a implementar soluciones de hello después de realizar un cambio.</span><span class="sxs-lookup"><span data-stu-id="4d823-139">You can redeploy hello solution after you make a change.</span></span>

<span data-ttu-id="4d823-140">Puede usar el archivo de configuración de Hola para:</span><span class="sxs-lookup"><span data-stu-id="4d823-140">You can use hello configuration file to:</span></span>

- <span data-ttu-id="4d823-141">Editar generadores simulada existente de hello, líneas de producción y las estaciones.</span><span class="sxs-lookup"><span data-stu-id="4d823-141">Edit hello existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="4d823-142">Asignar datos de servidores de OPC UA reales que se conecta toohello solución.</span><span class="sxs-lookup"><span data-stu-id="4d823-142">Map data from real OPC UA servers that you connect toohello solution.</span></span>

<span data-ttu-id="4d823-143">tooclone una copia del programa Hola conectado solución de Visual Studio de fábrica, Hola de uso siguiente comando de git:</span><span class="sxs-lookup"><span data-stu-id="4d823-143">tooclone a copy of hello connected factory Visual Studio solution, use hello following git command:</span></span>

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

<span data-ttu-id="4d823-144">archivo hello **ContosoTopologyDescription.json** define Hola elementos toohello vistas en panel de solución de fábrica conectado Hola de asignación de datos del servidor de OPC UA Hola.</span><span class="sxs-lookup"><span data-stu-id="4d823-144">hello file **ContosoTopologyDescription.json** defines hello mapping from hello OPC UA server data items toohello views in hello connected factory solution dashboard.</span></span> <span data-ttu-id="4d823-145">Puede encontrar este archivo de configuración en hello **Contoso\Topology** carpeta Hola **WebApp** proyecto Hola solución de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d823-145">You can find this configuration file in hello **Contoso\Topology** folder in hello **WebApp** project in hello Visual Studio solution.</span></span>

<span data-ttu-id="4d823-146">contenido de Hola de archivo JSON de hello se organiza como una jerarquía de nodos de estación, línea de producción y generador.</span><span class="sxs-lookup"><span data-stu-id="4d823-146">hello content of hello JSON file is organized as a hierarchy of factory, production line, and station nodes.</span></span> <span data-ttu-id="4d823-147">Esta jerarquía define la jerarquía de navegación de hello en panel de fábrica conectado Hola.</span><span class="sxs-lookup"><span data-stu-id="4d823-147">This hierarchy defines hello navigation hierarchy in hello connected factory dashboard.</span></span> <span data-ttu-id="4d823-148">Los valores en cada nodo de jerarquía de hello determinarán información de hello aparecen en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d823-148">Values at each node of hello hierarchy determine hello information displayed in hello dashboard.</span></span> <span data-ttu-id="4d823-149">Por ejemplo, archivo JSON de hello contiene Hola siguiendo los valores de fábrica Munich hello:</span><span class="sxs-lookup"><span data-stu-id="4d823-149">For example, hello JSON file contains hello following values for hello Munich factory:</span></span>

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

<span data-ttu-id="4d823-150">nombre de hello, descripción y ubicación aparecen en esta vista en el panel de hello:</span><span class="sxs-lookup"><span data-stu-id="4d823-150">hello name, description, and location appear on this view in hello dashboard:</span></span>

![Datos de Munich en panel de Hola][img-munich]

<span data-ttu-id="4d823-152">Cada factoría, línea de producción y estación tiene una propiedad de imagen.</span><span class="sxs-lookup"><span data-stu-id="4d823-152">Each factory, production line, and station have an image property.</span></span> <span data-ttu-id="4d823-153">Puede encontrar estos archivos JPEG en hello **Content\img** carpeta Hola **WebApp** proyecto.</span><span class="sxs-lookup"><span data-stu-id="4d823-153">You can find these JPEG files in hello **Content\img** folder in hello **WebApp** project.</span></span> <span data-ttu-id="4d823-154">Estos archivos de imagen se muestran en el panel Generador conectado de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d823-154">These image files display in hello connected factory dashboard.</span></span>

<span data-ttu-id="4d823-155">Cada estación incluye varias propiedades detalladas que definen Hola de hello OPC UA al asignar elementos de datos.</span><span class="sxs-lookup"><span data-stu-id="4d823-155">Each station includes several detailed properties that define hello mapping from hello OPC UA data items.</span></span> <span data-ttu-id="4d823-156">Estas propiedades se describen en las secciones siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="4d823-156">These properties are described in hello following sections:</span></span>

### <a name="opcuri"></a><span data-ttu-id="4d823-157">OpcUri</span><span class="sxs-lookup"><span data-stu-id="4d823-157">OpcUri</span></span>

<span data-ttu-id="4d823-158">Hola **OpcUri** valor es hello OPC UA URI de la aplicación que identifica de forma única Hola servidor OPC UA.</span><span class="sxs-lookup"><span data-stu-id="4d823-158">hello **OpcUri** value is hello OPC UA Application URI that uniquely identifies hello OPC UA server.</span></span> <span data-ttu-id="4d823-159">Por ejemplo, hello **OpcUri** valor de la estación de ensamblado de hello en la línea de producción 1 de Munich aspecto Hola siguientes: **urn: scada2194:ua:munich:productionline0:assemblystation**.</span><span class="sxs-lookup"><span data-stu-id="4d823-159">For example, hello **OpcUri** value for hello assembly station on production line 1 in Munich looks like hello following: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span></span>

<span data-ttu-id="4d823-160">Puede ver Hola URI de servidores de agente de usuario de OPC Hola conectado en el panel de la solución de hello:</span><span class="sxs-lookup"><span data-stu-id="4d823-160">You can view hello URIs of hello connected OPC UA servers in hello solution dashboard:</span></span>

![Vista de URI del servidor de OPC UA][img-server-uris]

### <a name="simulation"></a><span data-ttu-id="4d823-162">Simulation</span><span class="sxs-lookup"><span data-stu-id="4d823-162">Simulation</span></span>

<span data-ttu-id="4d823-163">Hola información de hello **simulación** nodo es toohello específico simulación de OPC UA que se ejecuta en hello servidores OPC UA aprovisionados de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4d823-163">hello information in hello **Simulation** node is specific toohello OPC UA simulation that runs in hello OPC UA servers that are provisioned by default.</span></span> <span data-ttu-id="4d823-164">No se utiliza para un servidor de OPC UA real.</span><span class="sxs-lookup"><span data-stu-id="4d823-164">It is not used for a real OPC UA server.</span></span>

### <a name="kpi1-and-kpi2"></a><span data-ttu-id="4d823-165">Kpi1 y Kpi2</span><span class="sxs-lookup"><span data-stu-id="4d823-165">Kpi1 and Kpi2</span></span>

<span data-ttu-id="4d823-166">Estos nodos describen cómo los datos de la estación de hello contribuyen toohello dos valores KPI en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d823-166">These nodes describe how data from hello station contributes toohello two KPI values in hello dashboard.</span></span> <span data-ttu-id="4d823-167">En una implementación predeterminada, estos valores de KPI son unidades por hora y kWh por hora.</span><span class="sxs-lookup"><span data-stu-id="4d823-167">In a default deployment, these KPI values are units per hour and kWh per hour.</span></span> <span data-ttu-id="4d823-168">solución de Hello calcula los valores KPI en el nivel de Hola de una estación y los agrega a la línea de producción de hello y niveles de fábrica.</span><span class="sxs-lookup"><span data-stu-id="4d823-168">hello solution calculates KPI vales at hello level of a station and aggregates them at hello production line and factory levels.</span></span>

<span data-ttu-id="4d823-169">Cada KPI tiene un valor mínimo, máximo y de destino.</span><span class="sxs-lookup"><span data-stu-id="4d823-169">Each KPI has a minimum, maximum, and target value.</span></span> <span data-ttu-id="4d823-170">Cada valor KPI también puede definir acciones de alerta para tooperform de solución de fábrica de hello conectado.</span><span class="sxs-lookup"><span data-stu-id="4d823-170">Each KPI value can also define alert actions for hello connected factory solution tooperform.</span></span> <span data-ttu-id="4d823-171">Hello fragmento de código siguiente muestra las definiciones de KPI de Hola para estación de ensamblado de hello en la línea de producción 1 de Munich:</span><span class="sxs-lookup"><span data-stu-id="4d823-171">hello following snippet shows hello KPI definitions for hello assembly station on production line 1 in Munich:</span></span>

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

<span data-ttu-id="4d823-172">Hello siguiente captura de pantalla muestra datos KPI de hello en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d823-172">hello following screenshot shows hello KPI data in hello dashboard.</span></span>

![Información de KPI en el panel de Hola][lnk-kpi]

### <a name="opcnodes"></a><span data-ttu-id="4d823-174">OpcNodes</span><span class="sxs-lookup"><span data-stu-id="4d823-174">OpcNodes</span></span>

<span data-ttu-id="4d823-175">Hola **OpcNodes** identifican nodos Hola elementos de datos publicados de hello servidor OPC UA y especificar cómo tooprocess esos datos.</span><span class="sxs-lookup"><span data-stu-id="4d823-175">hello **OpcNodes** nodes identify hello published data items from hello OPC UA server and specify how tooprocess that data.</span></span>

<span data-ttu-id="4d823-176">Hola **NodeId** valor identifica Hola específicas OPC UA NodeID de hello servidor OPC UA.</span><span class="sxs-lookup"><span data-stu-id="4d823-176">hello **NodeId** value identifies hello specific OPC UA NodeID from hello OPC UA server.</span></span> <span data-ttu-id="4d823-177">primer nodo de Hello en estaciones de ensamblado de hello para la línea de producción 1 en Munich tiene un valor **ns = 2; = 385**.</span><span class="sxs-lookup"><span data-stu-id="4d823-177">hello first node in hello assembly station for production line 1 in Munich has a value **ns=2;i=385**.</span></span> <span data-ttu-id="4d823-178">A **NodeId** valor especifica hello tooread de elemento de datos de hello y Hola servidor OPC UA **nombre** proporciona un nombre descriptivo toouse en el panel de Hola para esos datos.</span><span class="sxs-lookup"><span data-stu-id="4d823-178">A **NodeId** value specifies hello data item tooread from hello OPC UA server, and hello **SymbolicName** provides a user-friendly name toouse in hello dashboard for that data.</span></span>

<span data-ttu-id="4d823-179">Otros valores asociados a cada nodo se resumen en hello en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="4d823-179">Other values associated with each node are summarized in hello following table:</span></span>

| <span data-ttu-id="4d823-180">Valor</span><span class="sxs-lookup"><span data-stu-id="4d823-180">Value</span></span> | <span data-ttu-id="4d823-181">Descripción</span><span class="sxs-lookup"><span data-stu-id="4d823-181">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="4d823-182">Relevancia</span><span class="sxs-lookup"><span data-stu-id="4d823-182">Relevance</span></span>  | <span data-ttu-id="4d823-183">valores KPI y OEE Hola estos datos contribuyen a.</span><span class="sxs-lookup"><span data-stu-id="4d823-183">hello KPI and OEE values this data contributes to.</span></span> |
| <span data-ttu-id="4d823-184">OpCode</span><span class="sxs-lookup"><span data-stu-id="4d823-184">OpCode</span></span>     | <span data-ttu-id="4d823-185">¿Cómo se agregan datos Hola.</span><span class="sxs-lookup"><span data-stu-id="4d823-185">How hello data is aggregated.</span></span> |
| <span data-ttu-id="4d823-186">Unidades</span><span class="sxs-lookup"><span data-stu-id="4d823-186">Units</span></span>      | <span data-ttu-id="4d823-187">Hola toouse de unidades en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d823-187">hello units toouse in hello dashboard.</span></span>  |
| <span data-ttu-id="4d823-188">Visible</span><span class="sxs-lookup"><span data-stu-id="4d823-188">Visible</span></span>    | <span data-ttu-id="4d823-189">Si toodisplay este valor en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d823-189">Whether toodisplay this value in hello dashboard.</span></span> <span data-ttu-id="4d823-190">Algunos valores se utilizan en los cálculos pero no se muestran.</span><span class="sxs-lookup"><span data-stu-id="4d823-190">Some values are used in calculations but not displayed.</span></span>  |
| <span data-ttu-id="4d823-191">Máxima</span><span class="sxs-lookup"><span data-stu-id="4d823-191">Maximum</span></span>    | <span data-ttu-id="4d823-192">valor máximo de Hola que genera una alerta en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d823-192">hello maximum value that triggers an alert in hello dashboard.</span></span> |
| <span data-ttu-id="4d823-193">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="4d823-193">MaximumAlertActions</span></span> | <span data-ttu-id="4d823-194">Tootake de una acción de alerta de tooan de respuesta.</span><span class="sxs-lookup"><span data-stu-id="4d823-194">An action tootake in response tooan alert.</span></span> <span data-ttu-id="4d823-195">Por ejemplo, enviar una estación de tooa de comando.</span><span class="sxs-lookup"><span data-stu-id="4d823-195">For example, send a command tooa station.</span></span> |
| <span data-ttu-id="4d823-196">ConstValue</span><span class="sxs-lookup"><span data-stu-id="4d823-196">ConstValue</span></span> | <span data-ttu-id="4d823-197">Un valor constante que se usa en un cálculo.</span><span class="sxs-lookup"><span data-stu-id="4d823-197">A constant value used in a calculation.</span></span> |

## <a name="deploy-hello-changes"></a><span data-ttu-id="4d823-198">Implementar los cambios de Hola</span><span class="sxs-lookup"><span data-stu-id="4d823-198">Deploy hello changes</span></span>

<span data-ttu-id="4d823-199">Cuando haya terminado de realizar cambios toohello **ContosoTopologyDescription.json** archivo, debe volver a implementar Hola conectado generador solución tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="4d823-199">When you have finished making changes toohello **ContosoTopologyDescription.json** file, you must redeploy hello connected factory solution tooyour Azure account.</span></span>

<span data-ttu-id="4d823-200">Hola **-iot-conectado-factory de azure** repositorio incluye un **build.ps1** secuencia de comandos de PowerShell que puede usar toorebuild e implementar soluciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d823-200">hello **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use toorebuild and deploy hello solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d823-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4d823-201">Next Steps</span></span>

<span data-ttu-id="4d823-202">Obtener más información sobre solución de fábrica preconfigurado Hola conectado por leer Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="4d823-202">Learn more about hello connected factory preconfigured solution by reading hello following articles:</span></span>

* <span data-ttu-id="4d823-203">[Tutorial de la solución preconfigurada de fábrica conectada][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="4d823-203">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="4d823-204">[Implementación de una puerta de enlace para una solución de fábrica conectada][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="4d823-204">[Deploy a gateway for connected factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="4d823-205">[Permisos en el sitio de hello azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="4d823-205">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="4d823-206">Preguntas más frecuentes sobre fábrica conectada</span><span class="sxs-lookup"><span data-stu-id="4d823-206">Connected factory FAQ</span></span>](iot-suite-faq-cf.md)
* <span data-ttu-id="4d823-207">[Preguntas más frecuentes][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="4d823-207">[FAQ][lnk-faq]</span></span>


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