---
title: "Personalización de la factoría conectada del Conjunto de aplicaciones de IoT de Azure | Microsoft Docs"
description: "Descripción de cómo personalizar el comportamiento de la solución preconfigurada de factoría conectada."
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
ms.openlocfilehash: 90a6172dbd887ecda5a9f5d9082a4e136092bc10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="customize-how-the-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="f3d47-103">Personalización de cómo muestra la solución de factoría conectada los datos de los servidores de OPC UA</span><span class="sxs-lookup"><span data-stu-id="f3d47-103">Customize how the connected factory solution displays data from your OPC UA servers</span></span>

## <a name="introduction"></a><span data-ttu-id="f3d47-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="f3d47-104">Introduction</span></span>

<span data-ttu-id="f3d47-105">La solución de factoría conectada agrega y muestra datos de los servidores de OPC UA conectados a la solución.</span><span class="sxs-lookup"><span data-stu-id="f3d47-105">The connected factory solution aggregates and displays data from the OPC UA servers connected to the solution.</span></span> <span data-ttu-id="f3d47-106">Puede examinar y enviar comandos a los servidores de OPC UA en la solución.</span><span class="sxs-lookup"><span data-stu-id="f3d47-106">You can browse and send commands to the OPC UA servers in your solution.</span></span> <span data-ttu-id="f3d47-107">Para más información acerca de OPC UA, consulte las [preguntas frecuentes sobre la fábrica conectada](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="f3d47-107">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

<span data-ttu-id="f3d47-108">Entre los ejemplos de datos agregados en la solución se pueden mencionar Overall Equipment Efficiency (OEE) (Eficacia general de equipos) y Key Performance Indicators (Indicadores clave de rendimiento) (KPI) que se pueden ver en el panel en los ámbitos de factoría, línea y estación.</span><span class="sxs-lookup"><span data-stu-id="f3d47-108">Examples of aggregated data in the solution include the Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in the dashboard at the factory, line, and station levels.</span></span> <span data-ttu-id="f3d47-109">En las capturas de pantalla siguientes se muestran los valores de OEE y KPI para la estación **Assembly**, en **Production line 1**, en la factoría **Munich**:</span><span class="sxs-lookup"><span data-stu-id="f3d47-109">The following screenshot shows the OEE and KPI values for the **Assembly** station, on **Production line 1**, in the **Munich** factory:</span></span>

![Ejemplo de valores de OEE y KPI en la solución][img-oee-kpi]

<span data-ttu-id="f3d47-111">La solución le permite ver información detallada de elementos de datos específicos de los servidores de OPC UA, llamados *estaciones*.</span><span class="sxs-lookup"><span data-stu-id="f3d47-111">The solution enables you to view detailed information from specific data items from the OPC UA servers, called *stations*.</span></span> <span data-ttu-id="f3d47-112">En la captura de pantalla siguiente se muestran los trazados del número de artículos fabricados desde una estación específica:</span><span class="sxs-lookup"><span data-stu-id="f3d47-112">The following screenshot shows plots of the number of manufactured items from a specific station:</span></span>

![Trazados del número de artículos fabricados][img-manufactured-items]

<span data-ttu-id="f3d47-114">Si hace clic en uno de los gráficos, puede explorar los datos aún más con Time Series Insights (TSI):</span><span class="sxs-lookup"><span data-stu-id="f3d47-114">If you click one of the graphs, you can explore the data further using Time Series Insights (TSI):</span></span>

![Exploración de datos con Time Series Insights][img-tsi]

<span data-ttu-id="f3d47-116">En este artículo se describe:</span><span class="sxs-lookup"><span data-stu-id="f3d47-116">This article describes:</span></span>

- <span data-ttu-id="f3d47-117">Cómo los datos se ponen a disposición de las distintas vistas de la solución.</span><span class="sxs-lookup"><span data-stu-id="f3d47-117">How the data is made available to the various views in the solution.</span></span>
- <span data-ttu-id="f3d47-118">Cómo puede personalizar la forma en que la solución muestra los datos.</span><span class="sxs-lookup"><span data-stu-id="f3d47-118">How you can customize the way the solution displays the data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="f3d47-119">Orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="f3d47-119">Data sources</span></span>

<span data-ttu-id="f3d47-120">La solución de factoría conectada muestra datos de los servidores de OPC UA conectados a la solución.</span><span class="sxs-lookup"><span data-stu-id="f3d47-120">The connected factory solution displays data from the OPC UA servers connected to the solution.</span></span> <span data-ttu-id="f3d47-121">La instalación predeterminada incluye varios servidores de OPC UA que ejecutan una simulación de factoría.</span><span class="sxs-lookup"><span data-stu-id="f3d47-121">The default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="f3d47-122">Puede agregar sus propios servidores OPC UA que se [conectan a través de una puerta de enlace][lnk-connect-cf] a la solución.</span><span class="sxs-lookup"><span data-stu-id="f3d47-122">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] to your solution.</span></span>

<span data-ttu-id="f3d47-123">Puede examinar los elementos de datos que un servidor de OPC UA conectado puede enviar a la solución en el panel:</span><span class="sxs-lookup"><span data-stu-id="f3d47-123">You can browse the data items that a connected OPC UA server can send to your solution in the dashboard:</span></span>

1. <span data-ttu-id="f3d47-124">Navegue hasta la vista **Select an OPC UA server** (Seleccionar un servidor de OPC UA):</span><span class="sxs-lookup"><span data-stu-id="f3d47-124">Navigate to the **Select an OPC UA server** view:</span></span>

    ![Navegación hasta la vista Select an OPC UA server (Seleccionar un servidor de OPC UA)][img-select-server]

1. <span data-ttu-id="f3d47-126">Seleccione un servidor y haga clic en **Connect** (Conectar).</span><span class="sxs-lookup"><span data-stu-id="f3d47-126">Select a server and click **Connect**.</span></span> <span data-ttu-id="f3d47-127">Haga clic en **Proceed** (Continuar) cuando aparezca la advertencia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f3d47-127">Click **Proceed** when the security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f3d47-128">Esta advertencia solo aparece una vez para cada servidor y establece una relación de confianza entre el panel de la solución y el servidor.</span><span class="sxs-lookup"><span data-stu-id="f3d47-128">This warning only appears once for each server and establishes a trust relationship between the solution dashboard and the server.</span></span>

1. <span data-ttu-id="f3d47-129">Ahora puede examinar los elementos de datos que el servidor puede enviar a la solución.</span><span class="sxs-lookup"><span data-stu-id="f3d47-129">You can now browse the data items that the server can send to the solution.</span></span> <span data-ttu-id="f3d47-130">Los elementos que se envían a la solución tienen una marca de verificación verde:</span><span class="sxs-lookup"><span data-stu-id="f3d47-130">Items that are being sent to the solution have a green check mark:</span></span>

    ![Elementos publicados][img-published]

1. <span data-ttu-id="f3d47-132">Si es un *administrador* de la solución, puede publicar un elemento de datos para que esté disponible en la solución de factoría conectada.</span><span class="sxs-lookup"><span data-stu-id="f3d47-132">If you are an *Administrator* in the solution, you can choose to publish a data item to make it available in the connected factory solution.</span></span> <span data-ttu-id="f3d47-133">Como administrador, también puede cambiar el valor de los elementos de datos y llamar a métodos en el servidor de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="f3d47-133">As an Administrator, you can also change the value of data items and call methods in the OPC UA server.</span></span>

## <a name="map-the-data"></a><span data-ttu-id="f3d47-134">Asignación de datos</span><span class="sxs-lookup"><span data-stu-id="f3d47-134">Map the data</span></span>

<span data-ttu-id="f3d47-135">La solución de factoría conectada asigna y agrega los elementos de datos publicados desde el servidor de OPC UA a las distintas vistas de la solución.</span><span class="sxs-lookup"><span data-stu-id="f3d47-135">The connected factory solution maps and aggregates the published data items from the OPC UA server to the various views in the solution.</span></span> <span data-ttu-id="f3d47-136">La solución de factoría conectada se implementa en su cuenta de Azure al aprovisionar la solución.</span><span class="sxs-lookup"><span data-stu-id="f3d47-136">The connected factory solution deploys to your Azure account when you provision the solution.</span></span> <span data-ttu-id="f3d47-137">Un archivo JSON de la solución de factoría conectada de Visual Studio almacena esta información de asignación.</span><span class="sxs-lookup"><span data-stu-id="f3d47-137">A JSON file in the Visual Studio connected factory solution stores this mapping information.</span></span> <span data-ttu-id="f3d47-138">Puede ver y modificar este archivo de configuración de JSON en la solución de Visual Studio de factoría conectada.</span><span class="sxs-lookup"><span data-stu-id="f3d47-138">You can view and modify this JSON configuration file in the connected factory Visual Studio solution.</span></span> <span data-ttu-id="f3d47-139">Puede volver a implementar la solución después de realizar un cambio.</span><span class="sxs-lookup"><span data-stu-id="f3d47-139">You can redeploy the solution after you make a change.</span></span>

<span data-ttu-id="f3d47-140">Puede usar el archivo de configuración para:</span><span class="sxs-lookup"><span data-stu-id="f3d47-140">You can use the configuration file to:</span></span>

- <span data-ttu-id="f3d47-141">Editar las líneas de producción, las estaciones y las factorías simuladas existentes.</span><span class="sxs-lookup"><span data-stu-id="f3d47-141">Edit the existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="f3d47-142">Asignar datos de los servidores de OPC UA reales que se conectan a la solución.</span><span class="sxs-lookup"><span data-stu-id="f3d47-142">Map data from real OPC UA servers that you connect to the solution.</span></span>

<span data-ttu-id="f3d47-143">Para clonar una copia de la solución de Visual Studio de factoría conectada, use el siguiente comando de git:</span><span class="sxs-lookup"><span data-stu-id="f3d47-143">To clone a copy of the connected factory Visual Studio solution, use the following git command:</span></span>

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

<span data-ttu-id="f3d47-144">El archivo **ContosoTopologyDescription.json** define la asignación entre los elementos de datos del servidor de OPC UA y las vistas del panel de la solución de factoría conectada.</span><span class="sxs-lookup"><span data-stu-id="f3d47-144">The file **ContosoTopologyDescription.json** defines the mapping from the OPC UA server data items to the views in the connected factory solution dashboard.</span></span> <span data-ttu-id="f3d47-145">Puede encontrar este archivo de configuración en la carpeta **Contoso\Topology** del proyecto **WebApp** de la solución de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f3d47-145">You can find this configuration file in the **Contoso\Topology** folder in the **WebApp** project in the Visual Studio solution.</span></span>

<span data-ttu-id="f3d47-146">El contenido del archivo JSON se organiza como una jerarquía de nodos de estación, línea de producción y factoría.</span><span class="sxs-lookup"><span data-stu-id="f3d47-146">The content of the JSON file is organized as a hierarchy of factory, production line, and station nodes.</span></span> <span data-ttu-id="f3d47-147">Esta jerarquía define la jerarquía de navegación en el panel de factoría conectada.</span><span class="sxs-lookup"><span data-stu-id="f3d47-147">This hierarchy defines the navigation hierarchy in the connected factory dashboard.</span></span> <span data-ttu-id="f3d47-148">Los valores de cada nodo de la jerarquía determinan la información mostrada en el panel.</span><span class="sxs-lookup"><span data-stu-id="f3d47-148">Values at each node of the hierarchy determine the information displayed in the dashboard.</span></span> <span data-ttu-id="f3d47-149">Por ejemplo, el archivo JSON contiene los siguientes valores para la factoría de Múnich:</span><span class="sxs-lookup"><span data-stu-id="f3d47-149">For example, the JSON file contains the following values for the Munich factory:</span></span>

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

<span data-ttu-id="f3d47-150">El nombre, la descripción y la ubicación aparecen en esta vista en el panel:</span><span class="sxs-lookup"><span data-stu-id="f3d47-150">The name, description, and location appear on this view in the dashboard:</span></span>

![Datos de Múnich en el panel][img-munich]

<span data-ttu-id="f3d47-152">Cada factoría, línea de producción y estación tiene una propiedad de imagen.</span><span class="sxs-lookup"><span data-stu-id="f3d47-152">Each factory, production line, and station have an image property.</span></span> <span data-ttu-id="f3d47-153">Puede encontrar estos archivos JPEG en la carpeta **Content\img** del proyecto **WebApp**.</span><span class="sxs-lookup"><span data-stu-id="f3d47-153">You can find these JPEG files in the **Content\img** folder in the **WebApp** project.</span></span> <span data-ttu-id="f3d47-154">Estos archivos de imagen se muestran en el panel de factoría conectada.</span><span class="sxs-lookup"><span data-stu-id="f3d47-154">These image files display in the connected factory dashboard.</span></span>

<span data-ttu-id="f3d47-155">Cada estación incluye varias propiedades detalladas que definen la asignación de los elementos de datos de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="f3d47-155">Each station includes several detailed properties that define the mapping from the OPC UA data items.</span></span> <span data-ttu-id="f3d47-156">Estas propiedades se describen en las secciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="f3d47-156">These properties are described in the following sections:</span></span>

### <a name="opcuri"></a><span data-ttu-id="f3d47-157">OpcUri</span><span class="sxs-lookup"><span data-stu-id="f3d47-157">OpcUri</span></span>

<span data-ttu-id="f3d47-158">El valor de **OpcUri** es el URI de la aplicación de OPC UA que identifica de forma única el servidor de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="f3d47-158">The **OpcUri** value is the OPC UA Application URI that uniquely identifies the OPC UA server.</span></span> <span data-ttu-id="f3d47-159">Por ejemplo, el valor **OpcUri** de la estación de ensamblado de la línea de producción 1 de Múnich tiene el siguiente aspecto: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span><span class="sxs-lookup"><span data-stu-id="f3d47-159">For example, the **OpcUri** value for the assembly station on production line 1 in Munich looks like the following: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span></span>

<span data-ttu-id="f3d47-160">Puede ver los URI de los servidores de OPC UA conectados en el panel de la solución:</span><span class="sxs-lookup"><span data-stu-id="f3d47-160">You can view the URIs of the connected OPC UA servers in the solution dashboard:</span></span>

![Vista de URI del servidor de OPC UA][img-server-uris]

### <a name="simulation"></a><span data-ttu-id="f3d47-162">Simulation</span><span class="sxs-lookup"><span data-stu-id="f3d47-162">Simulation</span></span>

<span data-ttu-id="f3d47-163">La información del nodo **Simulation** es específica de la simulación de OPC UA que se ejecuta en los servidores de OPC UA aprovisionados de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f3d47-163">The information in the **Simulation** node is specific to the OPC UA simulation that runs in the OPC UA servers that are provisioned by default.</span></span> <span data-ttu-id="f3d47-164">No se utiliza para un servidor de OPC UA real.</span><span class="sxs-lookup"><span data-stu-id="f3d47-164">It is not used for a real OPC UA server.</span></span>

### <a name="kpi1-and-kpi2"></a><span data-ttu-id="f3d47-165">Kpi1 y Kpi2</span><span class="sxs-lookup"><span data-stu-id="f3d47-165">Kpi1 and Kpi2</span></span>

<span data-ttu-id="f3d47-166">Estos nodos describen cómo los datos de la estación contribuyen a los dos valores de KPI en el panel.</span><span class="sxs-lookup"><span data-stu-id="f3d47-166">These nodes describe how data from the station contributes to the two KPI values in the dashboard.</span></span> <span data-ttu-id="f3d47-167">En una implementación predeterminada, estos valores de KPI son unidades por hora y kWh por hora.</span><span class="sxs-lookup"><span data-stu-id="f3d47-167">In a default deployment, these KPI values are units per hour and kWh per hour.</span></span> <span data-ttu-id="f3d47-168">La solución calcula los valores de KPI en el ámbito de una estación y los agrega a los ámbitos de línea de producción y de fábrica.</span><span class="sxs-lookup"><span data-stu-id="f3d47-168">The solution calculates KPI vales at the level of a station and aggregates them at the production line and factory levels.</span></span>

<span data-ttu-id="f3d47-169">Cada KPI tiene un valor mínimo, máximo y de destino.</span><span class="sxs-lookup"><span data-stu-id="f3d47-169">Each KPI has a minimum, maximum, and target value.</span></span> <span data-ttu-id="f3d47-170">Cada valor de KPI también puede definir acciones de alerta que se van a realizar para la solución de factoría conectada.</span><span class="sxs-lookup"><span data-stu-id="f3d47-170">Each KPI value can also define alert actions for the connected factory solution to perform.</span></span> <span data-ttu-id="f3d47-171">El fragmento de código siguiente muestra las definiciones de KPI para la estación de montaje de la línea de producción 1 de Múnich:</span><span class="sxs-lookup"><span data-stu-id="f3d47-171">The following snippet shows the KPI definitions for the assembly station on production line 1 in Munich:</span></span>

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

<span data-ttu-id="f3d47-172">En la siguiente captura de pantalla se muestran los datos de KPI en el panel.</span><span class="sxs-lookup"><span data-stu-id="f3d47-172">The following screenshot shows the KPI data in the dashboard.</span></span>

![Información de KPI en el panel][lnk-kpi]

### <a name="opcnodes"></a><span data-ttu-id="f3d47-174">OpcNodes</span><span class="sxs-lookup"><span data-stu-id="f3d47-174">OpcNodes</span></span>

<span data-ttu-id="f3d47-175">Los nodos **OpcNodes** identifican los elementos de datos publicados desde el servidor de OPC UA y especifican cómo procesar esos datos.</span><span class="sxs-lookup"><span data-stu-id="f3d47-175">The **OpcNodes** nodes identify the published data items from the OPC UA server and specify how to process that data.</span></span>

<span data-ttu-id="f3d47-176">El valor de **NodeId** identifica el identificador de nodo de OPC UA específico del servidor de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="f3d47-176">The **NodeId** value identifies the specific OPC UA NodeID from the OPC UA server.</span></span> <span data-ttu-id="f3d47-177">El primer nodo de la estación de montaje para la línea de producción 1 de Múnich tiene un valor de **ns=2;i=385**.</span><span class="sxs-lookup"><span data-stu-id="f3d47-177">The first node in the assembly station for production line 1 in Munich has a value **ns=2;i=385**.</span></span> <span data-ttu-id="f3d47-178">A valor de **NodeId** especifica el elemento de datos que se va a leer del servidor de OPC UA y **SymbolicName** proporciona un nombre descriptivo que se usará en el panel para esos datos.</span><span class="sxs-lookup"><span data-stu-id="f3d47-178">A **NodeId** value specifies the data item to read from the OPC UA server, and the **SymbolicName** provides a user-friendly name to use in the dashboard for that data.</span></span>

<span data-ttu-id="f3d47-179">En la tabla siguiente se resumen otros valores asociados a cada nodo:</span><span class="sxs-lookup"><span data-stu-id="f3d47-179">Other values associated with each node are summarized in the following table:</span></span>

| <span data-ttu-id="f3d47-180">Valor</span><span class="sxs-lookup"><span data-stu-id="f3d47-180">Value</span></span> | <span data-ttu-id="f3d47-181">Descripción</span><span class="sxs-lookup"><span data-stu-id="f3d47-181">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="f3d47-182">Relevancia</span><span class="sxs-lookup"><span data-stu-id="f3d47-182">Relevance</span></span>  | <span data-ttu-id="f3d47-183">Los valores de KPI y OEE con los que contribuyen estos datos.</span><span class="sxs-lookup"><span data-stu-id="f3d47-183">The KPI and OEE values this data contributes to.</span></span> |
| <span data-ttu-id="f3d47-184">OpCode</span><span class="sxs-lookup"><span data-stu-id="f3d47-184">OpCode</span></span>     | <span data-ttu-id="f3d47-185">Cómo se agregan los datos.</span><span class="sxs-lookup"><span data-stu-id="f3d47-185">How the data is aggregated.</span></span> |
| <span data-ttu-id="f3d47-186">Unidades</span><span class="sxs-lookup"><span data-stu-id="f3d47-186">Units</span></span>      | <span data-ttu-id="f3d47-187">Las unidades que se van a usar en el panel.</span><span class="sxs-lookup"><span data-stu-id="f3d47-187">The units to use in the dashboard.</span></span>  |
| <span data-ttu-id="f3d47-188">Visible</span><span class="sxs-lookup"><span data-stu-id="f3d47-188">Visible</span></span>    | <span data-ttu-id="f3d47-189">Si se muestra este valor o no en el panel.</span><span class="sxs-lookup"><span data-stu-id="f3d47-189">Whether to display this value in the dashboard.</span></span> <span data-ttu-id="f3d47-190">Algunos valores se utilizan en los cálculos pero no se muestran.</span><span class="sxs-lookup"><span data-stu-id="f3d47-190">Some values are used in calculations but not displayed.</span></span>  |
| <span data-ttu-id="f3d47-191">Máxima</span><span class="sxs-lookup"><span data-stu-id="f3d47-191">Maximum</span></span>    | <span data-ttu-id="f3d47-192">El valor máximo que se desencadena una alerta en el panel.</span><span class="sxs-lookup"><span data-stu-id="f3d47-192">The maximum value that triggers an alert in the dashboard.</span></span> |
| <span data-ttu-id="f3d47-193">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="f3d47-193">MaximumAlertActions</span></span> | <span data-ttu-id="f3d47-194">Una acción que se realizará en respuesta a una alerta.</span><span class="sxs-lookup"><span data-stu-id="f3d47-194">An action to take in response to an alert.</span></span> <span data-ttu-id="f3d47-195">Por ejemplo, enviar un comando a una estación.</span><span class="sxs-lookup"><span data-stu-id="f3d47-195">For example, send a command to a station.</span></span> |
| <span data-ttu-id="f3d47-196">ConstValue</span><span class="sxs-lookup"><span data-stu-id="f3d47-196">ConstValue</span></span> | <span data-ttu-id="f3d47-197">Un valor constante que se usa en un cálculo.</span><span class="sxs-lookup"><span data-stu-id="f3d47-197">A constant value used in a calculation.</span></span> |

## <a name="deploy-the-changes"></a><span data-ttu-id="f3d47-198">Implementación de los cambios</span><span class="sxs-lookup"><span data-stu-id="f3d47-198">Deploy the changes</span></span>

<span data-ttu-id="f3d47-199">Cuando haya terminado de realizar cambios en el archivo **ContosoTopologyDescription.json**, debe volver a implementar la solución de factoría conectada en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3d47-199">When you have finished making changes to the **ContosoTopologyDescription.json** file, you must redeploy the connected factory solution to your Azure account.</span></span>

<span data-ttu-id="f3d47-200">El repositorio **-azure-iot-connected-factory** incluye un script de PowerShell **build.ps1** que puede usar para volver a compilar e implementar la solución.</span><span class="sxs-lookup"><span data-stu-id="f3d47-200">The **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use to rebuild and deploy the solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3d47-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f3d47-201">Next Steps</span></span>

<span data-ttu-id="f3d47-202">Para obtener más información sobre la solución preconfigurada de factoría conectada, lea los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="f3d47-202">Learn more about the connected factory preconfigured solution by reading the following articles:</span></span>

* <span data-ttu-id="f3d47-203">[Tutorial de la solución preconfigurada de fábrica conectada][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="f3d47-203">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="f3d47-204">[Implementación de una puerta de enlace para una solución de fábrica conectada][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="f3d47-204">[Deploy a gateway for connected factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="f3d47-205">[Permisos en el sitio azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="f3d47-205">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="f3d47-206">Preguntas más frecuentes sobre fábrica conectada</span><span class="sxs-lookup"><span data-stu-id="f3d47-206">Connected factory FAQ</span></span>](iot-suite-faq-cf.md)
* <span data-ttu-id="f3d47-207">[Preguntas más frecuentes][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="f3d47-207">[FAQ][lnk-faq]</span></span>


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