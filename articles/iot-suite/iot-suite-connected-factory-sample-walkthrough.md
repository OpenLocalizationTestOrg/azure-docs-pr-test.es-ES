---
title: "Tutorial de la solución de aaaConnected generador Suite de IoT de Azure | Documentos de Microsoft"
description: "Una descripción de solución de IoT de Azure preconfigurado hello conectados generador y su arquitectura."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 7fd55c51351659401349cfde91a20fce1045b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a><span data-ttu-id="3c208-103">Tutorial de la solución de fábrica preconfigurada conectada</span><span class="sxs-lookup"><span data-stu-id="3c208-103">Connected factory preconfigured solution walkthrough</span></span>

<span data-ttu-id="3c208-104">Hola IoT Suite conectado generador [preconfigurado solución] [ lnk-preconfigured-solutions] es una implementación de una solución industrial-to-end que:</span><span class="sxs-lookup"><span data-stu-id="3c208-104">hello IoT Suite connected factory [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end industrial solution that:</span></span>

* <span data-ttu-id="3c208-105">Se conecta tooboth simulada dispositivos industrial ejecutan servidores de OPC UA en líneas de producción de fábrica simulada y dispositivos de servidor de OPC UA reales.</span><span class="sxs-lookup"><span data-stu-id="3c208-105">Connects tooboth simulated industrial devices running OPC UA servers in simulated factory production lines, and real OPC UA server devices.</span></span> <span data-ttu-id="3c208-106">Para obtener más información sobre OPC UA, vea hello [conectado generador preguntas más frecuentes sobre](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="3c208-106">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="3c208-107">Muestra las claves KPI operativas y el OEE de esos servicios y líneas de producción.</span><span class="sxs-lookup"><span data-stu-id="3c208-107">Shows operational KPIs and OEE of those devices and production lines.</span></span>
* <span data-ttu-id="3c208-108">Muestra cómo una aplicación basada en la nube podría ser toointeract usado con sistemas de servidor de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3c208-108">Demonstrates how a cloud-based application could be used toointeract with OPC UA server systems.</span></span>
* <span data-ttu-id="3c208-109">Permite tooconnect sus propios dispositivos de servidor de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3c208-109">Enables you tooconnect your own OPC UA server devices.</span></span>
* <span data-ttu-id="3c208-110">Le permite toobrowse y modificar datos del servidor de OPC UA Hola.</span><span class="sxs-lookup"><span data-stu-id="3c208-110">Enables you toobrowse and modify hello OPC UA server data.</span></span>
* <span data-ttu-id="3c208-111">Se integra con hello tooprovide de servicio de información de serie de tiempo de Azure (ETI) vistas personalizadas de datos de saludo de los servidores de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3c208-111">Integrates with hello Azure Time Series Insights (TSI) service tooprovide customized views of hello data from your OPC UA servers.</span></span>

<span data-ttu-id="3c208-112">Puede usar soluciones de hello como punto de partida para su propia implementación y [personalizar] [ lnk-customize] toomeet sus propios requisitos empresariales específicos.</span><span class="sxs-lookup"><span data-stu-id="3c208-112">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="3c208-113">Este artículo le guiará a través de algunos de los elementos clave de Hola de hello conectado generador solución tooenable toounderstand su funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="3c208-113">This article walks you through some of hello key elements of hello connected factory solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="3c208-114">Esta información le ayuda a:</span><span class="sxs-lookup"><span data-stu-id="3c208-114">This knowledge helps you to:</span></span>

* <span data-ttu-id="3c208-115">Solucionar problemas de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c208-115">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="3c208-116">Planear cómo toocustomize toohello solución toomeet sus propios requisitos específicos.</span><span class="sxs-lookup"><span data-stu-id="3c208-116">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span>
* <span data-ttu-id="3c208-117">Diseñar una solución de IoT propia que utilice servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c208-117">Design your own IoT solution that uses Azure services.</span></span>

<span data-ttu-id="3c208-118">Para obtener más información, vea hello [conectado generador preguntas más frecuentes sobre](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="3c208-118">For more information, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="3c208-119">Arquitectura lógica</span><span class="sxs-lookup"><span data-stu-id="3c208-119">Logical architecture</span></span>

<span data-ttu-id="3c208-120">Hola siguiente diagrama describe los componentes lógicos de Hola de solución de hello preconfigurado:</span><span class="sxs-lookup"><span data-stu-id="3c208-120">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![Arquitectura lógica de fábrica conectada][connected-factory-logical]

## <a name="communication-patterns"></a><span data-ttu-id="3c208-122">Patrones de comunicación</span><span class="sxs-lookup"><span data-stu-id="3c208-122">Communication patterns</span></span>

<span data-ttu-id="3c208-123">solución de Hello usa hello [especificación de OPC UA Pub/Sub](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend tooIoT de datos de telemetría OPC UA concentrador en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="3c208-123">hello solution uses hello [OPC UA Pub/Sub specification](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA telemetry data tooIoT Hub in JSON format.</span></span> <span data-ttu-id="3c208-124">solución de Hello usa hello [OPC publicador](https://github.com/Azure/iot-edge-opc-publisher) módulo IoT Edge para este propósito.</span><span class="sxs-lookup"><span data-stu-id="3c208-124">hello solution uses hello [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge module for this purpose.</span></span>

<span data-ttu-id="3c208-125">solución de Hello también tiene un cliente de OPC UA integrado en una aplicación web que puede establecer conexiones con servidores de agente de usuario de OPC locales.</span><span class="sxs-lookup"><span data-stu-id="3c208-125">hello solution also has an OPC UA client integrated into a web application that can establish connections with on-premises OPC UA servers.</span></span> <span data-ttu-id="3c208-126">Hola cliente utiliza un [proxy inverso](https://wikipedia.org/wiki/Reverse_proxy) y recibe ayuda de conexión de centro de IoT toomake Hola sin necesidad de abrir los puertos en firewall de hello en local.</span><span class="sxs-lookup"><span data-stu-id="3c208-126">hello client uses a [reverse-proxy](https://wikipedia.org/wiki/Reverse_proxy) and receives help from IoT Hub toomake hello connection without requiring open ports in hello on-premises firewall.</span></span> <span data-ttu-id="3c208-127">Este patrón de comunicación se denomina [comunicación asistida por el servicio](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span><span class="sxs-lookup"><span data-stu-id="3c208-127">This communication pattern is called [service-assisted communication](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span></span> <span data-ttu-id="3c208-128">solución de Hello usa hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) módulo IoT Edge para este propósito.</span><span class="sxs-lookup"><span data-stu-id="3c208-128">hello solution uses hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge module for this purpose.</span></span>


## <a name="simulation"></a><span data-ttu-id="3c208-129">Simulation</span><span class="sxs-lookup"><span data-stu-id="3c208-129">Simulation</span></span>

<span data-ttu-id="3c208-130">Hola simula las estaciones y la ejecución de fabricación de hello simulado sistemas (MES) constituyen una línea de producción de fábrica.</span><span class="sxs-lookup"><span data-stu-id="3c208-130">hello simulated stations and hello simulated manufacturing execution systems (MES) make up a factory production line.</span></span> <span data-ttu-id="3c208-131">Hello hello OPC publicador módulo y dispositivos simulados se basan en hello [OPC UA .NET estándar] [ lnk-OPC-UA-NET-Standard] publicados por hello Foundation de OPC.</span><span class="sxs-lookup"><span data-stu-id="3c208-131">hello simulated devices and hello OPC Publisher Module are based on hello [OPC UA .NET Standard][lnk-OPC-UA-NET-Standard] published by hello OPC Foundation.</span></span>

<span data-ttu-id="3c208-132">Hello OPC Proxy y el publicador de OPC se implementan como módulos basados en [Azure IoT borde][lnk-Azure-IoT-Gateway].</span><span class="sxs-lookup"><span data-stu-id="3c208-132">hello OPC Proxy and OPC Publisher are implemented as modules based on [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span></span> <span data-ttu-id="3c208-133">Cada línea de producción simulada tiene asociada una puerta de enlace designada.</span><span class="sxs-lookup"><span data-stu-id="3c208-133">Each simulated production line has a designated gateway attached.</span></span>

<span data-ttu-id="3c208-134">Todos los componentes de simulación se ejecutan en contenedores de Docker hospedados en una máquina virtual Linux de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c208-134">All simulation components run in Docker containers  hosted in an Azure Linux VM.</span></span> <span data-ttu-id="3c208-135">simulación de Hello es ocho líneas de producción configurado toorun simulada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3c208-135">hello simulation is configured toorun eight simulated production lines by default.</span></span>

## <a name="simulated-production-line"></a><span data-ttu-id="3c208-136">Línea de producción simulada</span><span class="sxs-lookup"><span data-stu-id="3c208-136">Simulated production line</span></span>

<span data-ttu-id="3c208-137">Una línea de producción fabrica piezas.</span><span class="sxs-lookup"><span data-stu-id="3c208-137">A production line manufactures parts.</span></span> <span data-ttu-id="3c208-138">La forman distintas estaciones: una estación de ensamblado, una estación de prueba y una estación de empaquetado.</span><span class="sxs-lookup"><span data-stu-id="3c208-138">It is composed of different stations: an assembly station, a test station, and a packaging station.</span></span>

<span data-ttu-id="3c208-139">simulación de Hola se ejecuta y actualiza los datos de Hola que se exponen a través de nodos de agente de usuario de OPC Hola.</span><span class="sxs-lookup"><span data-stu-id="3c208-139">hello simulation runs and updates hello data that is exposed through hello OPC UA nodes.</span></span> <span data-ttu-id="3c208-140">Hola MES a través de OPC UA se organizan todas las estaciones de la línea de producción simulada.</span><span class="sxs-lookup"><span data-stu-id="3c208-140">All simulated production line stations are orchestrated by hello MES through OPC UA.</span></span>

## <a name="simulated-manufacturing-execution-system"></a><span data-ttu-id="3c208-141">Sistema de ejecución de fabricación simulado</span><span class="sxs-lookup"><span data-stu-id="3c208-141">Simulated manufacturing execution system</span></span>

<span data-ttu-id="3c208-142">Hola MES supervisa cada estación en la línea de producción de hello con cambios de estado de OPC UA toodetect estación.</span><span class="sxs-lookup"><span data-stu-id="3c208-142">hello MES monitors each station in hello production line through OPC UA toodetect station status changes.</span></span> <span data-ttu-id="3c208-143">Llama a OPC UA estaciones de métodos toocontrol hello y pasa a continuación un producto de una estación toohello hasta que se complete.</span><span class="sxs-lookup"><span data-stu-id="3c208-143">It calls OPC UA methods toocontrol hello stations and passes a product from one station toohello next until it is complete.</span></span>

## <a name="gateway-opc-publisher-module"></a><span data-ttu-id="3c208-144">Módulo publicador de OPC de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="3c208-144">Gateway OPC publisher module</span></span>

<span data-ttu-id="3c208-145">Módulo de publicador de OPC se conecta a servidores de agente de usuario de OPC estación toohello y se suscribe toohello OPC nodos toobe publicado.</span><span class="sxs-lookup"><span data-stu-id="3c208-145">OPC Publisher Module connects toohello station OPC UA servers and subscribes toohello OPC nodes toobe published.</span></span> <span data-ttu-id="3c208-146">módulo de Hello convierte los datos del nodo hello en formato JSON, lo cifra y envía tooIoT concentrador como mensajes de agente de usuario de OPC Pub/Sub.</span><span class="sxs-lookup"><span data-stu-id="3c208-146">hello module converts hello node data into JSON format, encrypts it, and sends it tooIoT Hub as OPC UA Pub/Sub messages.</span></span>

<span data-ttu-id="3c208-147">módulo de OPC publicador Hola solo requiere un puerto de salida https (443) y puede trabajar con la infraestructura empresarial existente.</span><span class="sxs-lookup"><span data-stu-id="3c208-147">hello OPC Publisher module only requires an outbound https port (443) and can work with existing enterprise infrastructure.</span></span>

## <a name="gateway-opc-proxy-module"></a><span data-ttu-id="3c208-148">Módulo proxy de OPC de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="3c208-148">Gateway OPC proxy module</span></span>

<span data-ttu-id="3c208-149">Hola módulo de Proxy de agente de usuario de puerta de enlace de OPC túneles mensajes de comando y control de OPC UA binarios y solo requiere un puerto de salida https (443).</span><span class="sxs-lookup"><span data-stu-id="3c208-149">hello Gateway OPC UA Proxy Module tunnels binary OPC UA command and control messages and only requires an outbound https port (443).</span></span> <span data-ttu-id="3c208-150">Puede funcionar con la infraestructura empresarial existente, incluidos los proxies web.</span><span class="sxs-lookup"><span data-stu-id="3c208-150">It can work with existing enterprise infrastructure, including Web Proxies.</span></span>

<span data-ttu-id="3c208-151">Usa datos de dispositivos del centro de IoT métodos tootransfer qué TCP/IP en el nivel de aplicación Hola y, por tanto, se asegura de confianza de punto de conexión, el cifrado de datos y la integridad mediante el uso de SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="3c208-151">It uses IoT Hub Device methods tootransfer packetized TCP/IP data at hello application layer and thus ensures endpoint trust, data encryption, and integrity using SSL/TLS.</span></span>

<span data-ttu-id="3c208-152">Hola protocolo binario de OPC UA retransmitida a través de proxy de hello propio usa cifrado y la autenticación de agente de usuario.</span><span class="sxs-lookup"><span data-stu-id="3c208-152">hello OPC UA binary protocol relayed through hello proxy itself uses UA authentication and encryption.</span></span>

## <a name="azure-time-series-insights"></a><span data-ttu-id="3c208-153">Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="3c208-153">Azure Time Series Insights</span></span>

<span data-ttu-id="3c208-154">Hola módulo de publicador de puerta de enlace de OPC suscribe cambios tooOPC UA server nodos toodetect hello en valores de datos.</span><span class="sxs-lookup"><span data-stu-id="3c208-154">hello Gateway OPC Publisher Module subscribes tooOPC UA server nodes toodetect change in hello data values.</span></span> <span data-ttu-id="3c208-155">Si se detecta un cambio de datos en uno de los nodos de hello, este módulo, a continuación, envía mensajes tooAzure centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="3c208-155">If a data change is detected in one of hello nodes, this module then sends messages tooAzure IoT Hub.</span></span>

<span data-ttu-id="3c208-156">Centro de IoT proporciona un tooAzure de origen de evento ETI.</span><span class="sxs-lookup"><span data-stu-id="3c208-156">IoT Hub provides an event source tooAzure TSI.</span></span> <span data-ttu-id="3c208-157">Los datos de almacenes de ETI durante 30 días en función de las marcas de tiempo adjuntar toohello mensajes.</span><span class="sxs-lookup"><span data-stu-id="3c208-157">TSI stores data for 30 days based on timestamps attached toohello messages.</span></span> <span data-ttu-id="3c208-158">Estos datos incluyen:</span><span class="sxs-lookup"><span data-stu-id="3c208-158">This data includes:</span></span>

* <span data-ttu-id="3c208-159">OPC UA ApplicationUri</span><span class="sxs-lookup"><span data-stu-id="3c208-159">OPC UA ApplicationUri</span></span>
* <span data-ttu-id="3c208-160">OPC UA NodeId</span><span class="sxs-lookup"><span data-stu-id="3c208-160">OPC UA NodeId</span></span>
* <span data-ttu-id="3c208-161">Valor del nodo de Hola</span><span class="sxs-lookup"><span data-stu-id="3c208-161">Value of hello node</span></span>
* <span data-ttu-id="3c208-162">Marca de tiempo de origen</span><span class="sxs-lookup"><span data-stu-id="3c208-162">Source timestamp</span></span>
* <span data-ttu-id="3c208-163">OPC UA DisplayName</span><span class="sxs-lookup"><span data-stu-id="3c208-163">OPC UA DisplayName</span></span>

<span data-ttu-id="3c208-164">Actualmente, ETI no permite que los clientes toocustomize cuánto hubieran querido tookeep datos de Hola para.</span><span class="sxs-lookup"><span data-stu-id="3c208-164">Currently, TSI does not allow customers toocustomize how long they wish tookeep hello data for.</span></span>

<span data-ttu-id="3c208-165">TSI realiza consultas en los datos del nodo mediante SearchSpan (Time.From, Time.To) y los agrega mediante OPC UA ApplicationUri, OPC UA NodeId u OPC UA DisplayName.</span><span class="sxs-lookup"><span data-stu-id="3c208-165">TSI queries against node data using a SearchSpan (Time.From, Time.To) and aggregates by OPC UA ApplicationUri or OPC UA NodeId or OPC UA DisplayName.</span></span>

<span data-ttu-id="3c208-166">datos de Hola de tooretrieve para medidores OEE y KPI de Hola y líneas de serie del tiempo de hello, los datos se agregan por recuento de eventos, Sum, Avg, Min y Max.</span><span class="sxs-lookup"><span data-stu-id="3c208-166">tooretrieve hello data for hello OEE and KPI gauges, and hello time series charts, data is aggregated by count of events, Sum, Avg, Min, and Max.</span></span>

<span data-ttu-id="3c208-167">serie temporal de Hola se compila con un proceso diferente.</span><span class="sxs-lookup"><span data-stu-id="3c208-167">hello time series are built using a different process.</span></span> <span data-ttu-id="3c208-168">OEE y KPI se calcula a partir de datos de base de estación y propaga hacia arriba para la topología de hello (líneas de producción, generadores, enterprise) en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="3c208-168">OEE and KPIs are calculated from station base data and bubbled up for hello topology (production lines, factories, enterprise) in hello application.</span></span>

<span data-ttu-id="3c208-169">Además, serie temporal para la topología OEE y un KPI se calcula en la aplicación hello, cada vez que un objeto timespan mostrado esté listo.</span><span class="sxs-lookup"><span data-stu-id="3c208-169">Additionally, time series for OEE and KPI topology is calculated in hello app, whenever a displayed timespan is ready.</span></span> <span data-ttu-id="3c208-170">Por ejemplo, vista de día de Hola se actualiza cada hora completa.</span><span class="sxs-lookup"><span data-stu-id="3c208-170">For example, hello day view is updated every full hour.</span></span>

<span data-ttu-id="3c208-171">vista en Hello tiempo series de datos del nodo proviene directamente de ETI utilizando una agregación de intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="3c208-171">hello time series view of node data comes directly from TSI using an aggregation for timespan.</span></span>

## <a name="iot-hub"></a><span data-ttu-id="3c208-172">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="3c208-172">IoT Hub</span></span>
<span data-ttu-id="3c208-173">Hola [centro de IoT] [ lnk-IoT Hub] recibe los datos enviados desde Hola OPC publicador módulo en la nube de Hola y facilita el servicio de Azure ETI toohello disponible.</span><span class="sxs-lookup"><span data-stu-id="3c208-173">hello [IoT hub][lnk-IoT Hub] receives data sent from hello OPC Publisher Module into hello cloud and makes it available toohello Azure TSI service.</span></span> 

<span data-ttu-id="3c208-174">Hola centro de IoT de solución de hello también:</span><span class="sxs-lookup"><span data-stu-id="3c208-174">hello IoT Hub in hello solution also:</span></span>
- <span data-ttu-id="3c208-175">Mantiene un registro de la identidad que almacena los identificadores de Hola para todos los OPC publicador módulo y todos los módulos de Proxy de OPC.</span><span class="sxs-lookup"><span data-stu-id="3c208-175">Maintains an identity registry that stores hello IDs for all OPC Publisher Module and all OPC Proxy Modules.</span></span>
- <span data-ttu-id="3c208-176">Se utiliza como canal de transporte para la comunicación bidireccional de hello módulo de Proxy de OPC.</span><span class="sxs-lookup"><span data-stu-id="3c208-176">Is used as transport channel for bidirectional communication of hello OPC Proxy Module.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="3c208-177">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3c208-177">Azure Storage</span></span>
<span data-ttu-id="3c208-178">solución de Hello utiliza almacenamiento de blobs de Azure como almacenamiento en disco para datos de implementación de VM y toostore Hola.</span><span class="sxs-lookup"><span data-stu-id="3c208-178">hello solution uses Azure blob storage as disk storage for hello VM and toostore deployment data.</span></span>

## <a name="web-app"></a><span data-ttu-id="3c208-179">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="3c208-179">Web app</span></span>
<span data-ttu-id="3c208-180">aplicación web de Hello implementada como parte de la solución de hello preconfigurado está formado por un cliente de OPC UA integrado, el procesamiento de alertas y la visualización de telemetría.</span><span class="sxs-lookup"><span data-stu-id="3c208-180">hello web app deployed as part of hello preconfigured solution comprises of an integrated OPC UA client, alerts processing and telemetry visualization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c208-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3c208-181">Next steps</span></span>

<span data-ttu-id="3c208-182">Puede seguir introducción con Suite IoT leyendo Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="3c208-182">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="3c208-183">[Permisos en el sitio de hello azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="3c208-183">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="3c208-184">Implementar una puerta de enlace de Windows o Linux para la solución de fábrica preconfigurado Hola conectado</span><span class="sxs-lookup"><span data-stu-id="3c208-184">Deploy a gateway on Windows or Linux for hello connected factory preconfigured solution</span></span>](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
