---
title: "aaaTroubleshooting y supervisión de SAP HANA en Azure (instancias de gran tamaño) | Documentos de Microsoft"
description: "Solución de problemas y supervisión de SAP HANA en Azure (Instancias grandes)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a><span data-ttu-id="70598-103">¿Cómo tootroubleshoot y monitor de SAP HANA (instancias de gran tamaño) en Azure</span><span class="sxs-lookup"><span data-stu-id="70598-103">How tootroubleshoot and monitor SAP HANA (large instances) on Azure</span></span>


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="70598-104">Supervisión de SAP HANA en Azure (Instancias grandes)</span><span class="sxs-lookup"><span data-stu-id="70598-104">Monitoring in SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="70598-105">SAP HANA en Azure (instancias de gran tamaño) no es diferente de cualquier otra implementación de IaaS, es necesario toomonitor qué Hola OS y aplicación hello es hacerlo y cómo estos consumen Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="70598-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need toomonitor what hello OS and hello application is doing and how these consume hello following resources:</span></span>

- <span data-ttu-id="70598-106">CPU</span><span class="sxs-lookup"><span data-stu-id="70598-106">CPU</span></span>
- <span data-ttu-id="70598-107">Memoria</span><span class="sxs-lookup"><span data-stu-id="70598-107">Memory</span></span>
- <span data-ttu-id="70598-108">Ancho de banda de red</span><span class="sxs-lookup"><span data-stu-id="70598-108">Network bandwidth</span></span>
- <span data-ttu-id="70598-109">Espacio en disco</span><span class="sxs-lookup"><span data-stu-id="70598-109">Disk space</span></span>

<span data-ttu-id="70598-110">Como con las máquinas virtuales Azure necesite toofigure si son suficientes las clases de recursos de hello mencionadas anteriormente, o si éstos obtengan agota.</span><span class="sxs-lookup"><span data-stu-id="70598-110">As with Azure Virtual Machines you need toofigure out whether hello resource classes named above are sufficient, or whether these get depleted.</span></span> <span data-ttu-id="70598-111">Aquí es más detalle en cada una de las distintas clases de hello:</span><span class="sxs-lookup"><span data-stu-id="70598-111">Here is more detail on each of hello different classes:</span></span>

<span data-ttu-id="70598-112">**Consumo de recursos de CPU:** proporción de Hola que SAP definido para ciertas cargas de trabajo con HANA es obligatorio toomake seguro de que debe haber suficientes recursos de CPU disponible toowork a través de los datos de Hola que se almacenan en memoria.</span><span class="sxs-lookup"><span data-stu-id="70598-112">**CPU resource consumption:** hello ratio that SAP defined for certain workload against HANA is enforced toomake sure that there should be enough CPU resources available toowork through hello data that is stored in memory.</span></span> <span data-ttu-id="70598-113">No obstante, puede darse el caso donde HANA consume mucha CPU al ejecutar consultas de vencimiento toomissing índices o problemas similares.</span><span class="sxs-lookup"><span data-stu-id="70598-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due toomissing indexes or similar issues.</span></span> <span data-ttu-id="70598-114">Esto significa que debe supervisar el consumo de recursos de CPU de la unidad de hello HANA instancia grande, así como los recursos de CPU utilizados por servicios concretos de HANA de Hola.</span><span class="sxs-lookup"><span data-stu-id="70598-114">This means you should monitor CPU resource consumption of hello HANA large instance unit as well as CPU resources consumed by hello specific HANA services.</span></span>

<span data-ttu-id="70598-115">**Consumo de memoria:** es importante toomonitor desde dentro de HANA, así como fuera de HANA en la unidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="70598-115">**Memory consumption:** Is important toomonitor from within HANA, as well as outside of HANA on hello unit.</span></span> <span data-ttu-id="70598-116">Dentro de HANA, supervisar cómo consume datos de hello HANA asignado a la memoria en toostay de orden dentro de hello necesario ajustar el tamaño de las directrices de SAP.</span><span class="sxs-lookup"><span data-stu-id="70598-116">Within HANA, monitor how hello data is consuming HANA allocated memory in order toostay within hello required sizing guidelines of SAP.</span></span> <span data-ttu-id="70598-117">También puede toomonitor el consumo de memoria en hello instancia grande toomake nivel seguro que adicionales HANA-no instalado software no consumir demasiada memoria y, por tanto, entren en conflicto con HANA para la memoria.</span><span class="sxs-lookup"><span data-stu-id="70598-117">You also want toomonitor memory consumption on hello Large Instance level toomake sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span></span>

<span data-ttu-id="70598-118">**Ancho de banda de red:** puerta de enlace de red virtual de Azure Hola está limitado el ancho de banda de datos que se transfieren en hello red virtual de Azure, por lo que resulta útil toomonitor datos de saludo recibidos por todos los Hola máquinas virtuales de Azure dentro de un toofigure de red virtual información acerca de cómo cerrar son límites de toohello de hello Azure puerta de enlace de SKU que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="70598-118">**Network bandwidth:** hello Azure VNet gateway is limited in bandwidth of data moving into hello Azure VNet, so it is helpful toomonitor hello data received by all hello Azure VMs within a VNet toofigure out how close you are toohello limits of hello Azure gateway SKU you selected.</span></span> <span data-ttu-id="70598-119">En la unidad de instancia grande de HANA hello, que le sentido toomonitor entrantes y salientes tráfico de red así y realizar un seguimiento de tookeep de volúmenes de Hola que se administran con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="70598-119">On hello HANA Large Instance unit, it does make sense toomonitor incoming and outgoing network traffic as well, and tookeep track of hello volumes that are handled over time.</span></span>

<span data-ttu-id="70598-120">**Espacio en disco:** normalmente su uso aumenta a lo largo del tiempo.</span><span class="sxs-lookup"><span data-stu-id="70598-120">**Disk space:** Disk space consumption usually increases over time.</span></span> <span data-ttu-id="70598-121">Hay muchas razones para ello, pero las principales son: aumenta el volumen de datos, la ejecución de copias de seguridad de los registros de transacciones, el almacenamiento de los archivos de seguimiento y la realización de instantáneas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="70598-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span></span> <span data-ttu-id="70598-122">Por lo tanto, es importante toomonitor uso del espacio de disco y administrar espacio en disco Hola asociado con una unidad de instancia grande de HANA Hola.</span><span class="sxs-lookup"><span data-stu-id="70598-122">Therefore, it is important toomonitor disk space usage and manage hello disk space associated with hello HANA Large Instance unit.</span></span>

## <a name="monitoring-and-troubleshooting-from-hana-side"></a><span data-ttu-id="70598-123">Supervisión y solución de problemas en el lado HANA</span><span class="sxs-lookup"><span data-stu-id="70598-123">Monitoring and troubleshooting from HANA side</span></span>

<span data-ttu-id="70598-124">En orden tooeffectively analizar problemas relacionados tooSAP HANA en Azure (instancias grandes), resulta útil toonarrow hacia abajo de la causa raíz de Hola de un problema.</span><span class="sxs-lookup"><span data-stu-id="70598-124">In order tooeffectively analyze problems related tooSAP HANA on Azure (Large Instances), it is useful toonarrow down hello root cause of a problem.</span></span> <span data-ttu-id="70598-125">SAP ha publicado una gran cantidad de documentación toohelp.</span><span class="sxs-lookup"><span data-stu-id="70598-125">SAP has published a large amount of documentation toohelp you.</span></span>

<span data-ttu-id="70598-126">Aplicable preguntas más frecuentes relacionadas tooSAP HANA rendimiento puede encontrarse en hello siguiendo las notas de SAP:</span><span class="sxs-lookup"><span data-stu-id="70598-126">Applicable FAQs related tooSAP HANA performance can be found in hello following SAP Notes:</span></span>

- <span data-ttu-id="70598-127">[SAP Note #2222200 – FAQ: SAP HANA Network](https://launchpad.support.sap.com/#/notes/2222200) (Nota de SAP 2222200: preguntas más frecuentes sobre la red de SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="70598-127">[SAP Note #2222200 – FAQ: SAP HANA Network](https://launchpad.support.sap.com/#/notes/2222200)</span></span>
- <span data-ttu-id="70598-128">[SAP Note #2100040 – FAQ: SAP HANA CPU](https://launchpad.support.sap.com/#/notes/0002100040) (Nota de SAP 2100040: preguntas más frecuentes sobre la CPU de SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="70598-128">[SAP Note #2100040 – FAQ: SAP HANA CPU](https://launchpad.support.sap.com/#/notes/0002100040)</span></span>
- <span data-ttu-id="70598-129">[SAP Note #199997 – FAQ: SAP HANA Memory](https://launchpad.support.sap.com/#/notes/2177064) (Nota de SAP 199997: preguntas más frecuentes sobre la memoria de SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="70598-129">[SAP Note #199997 – FAQ: SAP HANA Memory](https://launchpad.support.sap.com/#/notes/2177064)</span></span>
- <span data-ttu-id="70598-130">[SAP Note #200000 – FAQ: SAP HANA Performance Optimization](https://launchpad.support.sap.com/#/notes/2000000) (Nota de SAP 199997: preguntas más frecuentes sobre la optimización del rendimiento de SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="70598-130">[SAP Note #200000 – FAQ: SAP HANA Performance Optimization](https://launchpad.support.sap.com/#/notes/2000000)</span></span>
- <span data-ttu-id="70598-131">[SAP Note #199930 – FAQ: SAP HANA I/O Analysis](https://launchpad.support.sap.com/#/notes/1999930) (Nota de SAP 199930: preguntas más frecuentes sobre el análisis de E/S de SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="70598-131">[SAP Note #199930 – FAQ: SAP HANA I/O Analysis](https://launchpad.support.sap.com/#/notes/1999930)</span></span>
- <span data-ttu-id="70598-132">[SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes](https://launchpad.support.sap.com/#/notes/2177064) (Nota de SAP #2177064: preguntas más frecuentes sobre el reinicio y la caída del servicio)</span><span class="sxs-lookup"><span data-stu-id="70598-132">[SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes](https://launchpad.support.sap.com/#/notes/2177064)</span></span>

<span data-ttu-id="70598-133">**Alertas de SAP HANA**</span><span class="sxs-lookup"><span data-stu-id="70598-133">**SAP HANA Alerts**</span></span>

<span data-ttu-id="70598-134">Como primer paso, compruebe los registros de alertas de SAP HANA actuales Hola.</span><span class="sxs-lookup"><span data-stu-id="70598-134">As a first step, check hello current SAP HANA alert logs.</span></span> <span data-ttu-id="70598-135">En SAP HANA Studio, vaya demasiado**consola de administración: alertas: mostrar: todas las alertas**.</span><span class="sxs-lookup"><span data-stu-id="70598-135">In SAP HANA Studio, go too**Administration Console: Alerts: Show: all alerts**.</span></span> <span data-ttu-id="70598-136">Esta ficha muestra todas las alertas de SAP HANA determinados valores (memoria física libre, el uso de CPU, etc.) que se encuentran fuera de hello establecer la duración mínima y máximos umbrales.</span><span class="sxs-lookup"><span data-stu-id="70598-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of hello set minimum and maximum thresholds.</span></span> <span data-ttu-id="70598-137">De forma predeterminada, las comprobaciones se actualizan automáticamente cada 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="70598-137">By default, checks are auto-refreshed every 15 minutes.</span></span>

![En SAP HANA Studio, vaya tooAdministration consola: alertas: mostrar: todas las alertas](./media/troubleshooting-monitoring/image1-show-alerts.png)

<span data-ttu-id="70598-139">**CPU**</span><span class="sxs-lookup"><span data-stu-id="70598-139">**CPU**</span></span>

<span data-ttu-id="70598-140">Para una alerta desencadenada debido tooimproper umbral configurado, una resolución es tooreset toohello valor o un valor de umbral más razonable.</span><span class="sxs-lookup"><span data-stu-id="70598-140">For an alert triggered due tooimproper threshold setting, a resolution is tooreset toohello default value or a more reasonable threshold value.</span></span>

![Restablecer el valor predeterminado de toohello o un valor de umbral más razonable](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

<span data-ttu-id="70598-142">Hola siguiendo las alertas puede indicar problemas de recursos de CPU:</span><span class="sxs-lookup"><span data-stu-id="70598-142">hello following alerts may indicate CPU resource problems:</span></span>

- <span data-ttu-id="70598-143">Uso de CPU del host (alerta 5)</span><span class="sxs-lookup"><span data-stu-id="70598-143">Host CPU Usage (Alert 5)</span></span>
- <span data-ttu-id="70598-144">Operación del punto de retorno más reciente (alerta 28)</span><span class="sxs-lookup"><span data-stu-id="70598-144">Most recent savepoint operation (Alert 28)</span></span>
- <span data-ttu-id="70598-145">Duración del punto de retorno (alerta 54)</span><span class="sxs-lookup"><span data-stu-id="70598-145">Savepoint duration (Alert 54)</span></span>

<span data-ttu-id="70598-146">Puede observar alto consumo de CPU en la base de datos de SAP HANA desde uno de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="70598-146">You may notice high CPU consumption on your SAP HANA database from one of hello following:</span></span>

- <span data-ttu-id="70598-147">La alerta 5 (Uso de CPU del host) se desencadena para el uso de CPU actual o antiguo</span><span class="sxs-lookup"><span data-stu-id="70598-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span></span>
- <span data-ttu-id="70598-148">Hello muestra el uso de CPU en pantalla de información general de bienvenida</span><span class="sxs-lookup"><span data-stu-id="70598-148">hello displayed CPU usage on hello overview screen</span></span>

![Muestra el uso de CPU en pantalla de información general de bienvenida](./media/troubleshooting-monitoring/image3-cpu-usage.png)

<span data-ttu-id="70598-150">gráfico de carga de Hello podría mostrar alto consumo de CPU o más consumo Hola anteriores:</span><span class="sxs-lookup"><span data-stu-id="70598-150">hello Load graph might show high CPU consumption, or high consumption in hello past:</span></span>

![gráfico de carga de Hello puede mostrar alto consumo de CPU o más consumo Hola anteriores](./media/troubleshooting-monitoring/image4-load-graph.png)

<span data-ttu-id="70598-152">Alerta desencadenada debido a la utilización de CPU toohigh pueden deberse a varias razones, entre ellas, pero sin limitarse a: ejecución de ciertas transacciones, carga de datos, que no responden de trabajos de larga ejecución instrucciones SQL y el rendimiento de consulta no válidos (por ejemplo, con BW en HANA cubos).</span><span class="sxs-lookup"><span data-stu-id="70598-152">An alert triggered due toohigh CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span></span>

<span data-ttu-id="70598-153">Consulte toohello [solución de problemas de SAP HANA: hace relacionados de CPU y soluciones](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) sitio pasos de solución de problemas detallada.</span><span class="sxs-lookup"><span data-stu-id="70598-153">Refer toohello [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="70598-154">**Sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="70598-154">**Operating System**</span></span>

<span data-ttu-id="70598-155">Uno de los más importantes de hello comprueba para SAP HANA en Linux es toomake seguro de que estén deshabilitadas transparente páginas muy grandes, consulte [SAP nota #2131662: transparente enorme páginas (THP) en servidores de SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).</span><span class="sxs-lookup"><span data-stu-id="70598-155">One of hello most important checks for SAP HANA on Linux is toomake sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span></span>

- <span data-ttu-id="70598-156">Puede comprobar si hay páginas enorme transparente habilitadas a través de hello siguiente comando de Linux: **cat /sys/kernel/mm/transparent\_hugepage/habilitado**</span><span class="sxs-lookup"><span data-stu-id="70598-156">You can check if Transparent Huge Pages are enabled through hello following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span></span>
- <span data-ttu-id="70598-157">Si _siempre_ se encierra entre corchetes como sigue, significa que están habilitadas Hola transparente enorme páginas: [siempre] madvise nunca; si _nunca_ se incluye entre corchetes como sigue, significa que Hola transparente Páginas enormes están deshabilitadas: siempre madvise [nunca]</span><span class="sxs-lookup"><span data-stu-id="70598-157">If _always_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are disabled: always madvise [never]</span></span>

<span data-ttu-id="70598-158">Hola siguiente comando de Linux debe devolver nada: **rpm - qa | grep ulimit.**</span><span class="sxs-lookup"><span data-stu-id="70598-158">hello following Linux command should return nothing: **rpm -qa | grep ulimit.**</span></span> <span data-ttu-id="70598-159">Si indica que _ulimit_ está instalado, desinstálelo inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="70598-159">If it appears _ulimit_ is installed, uninstall it immediately.</span></span>

<span data-ttu-id="70598-160">**Memoria**</span><span class="sxs-lookup"><span data-stu-id="70598-160">**Memory**</span></span>

<span data-ttu-id="70598-161">Puede observar esa cantidad de Hola de memoria asignada por hello SAP HANA, base de datos es mayor de lo esperado.</span><span class="sxs-lookup"><span data-stu-id="70598-161">You may observe that hello amount of memory allocated by hello SAP HANA database is higher than expected.</span></span> <span data-ttu-id="70598-162">Hola siguiendo las alertas indica problemas con mayor uso de memoria:</span><span class="sxs-lookup"><span data-stu-id="70598-162">hello following alerts indicate issues with high memory usage:</span></span>

- <span data-ttu-id="70598-163">Uso de memoria física del host (alerta 1)</span><span class="sxs-lookup"><span data-stu-id="70598-163">Host physical memory usage (Alert 1)</span></span>
- <span data-ttu-id="70598-164">Uso de memoria del servidor de nombres (alerta 12)</span><span class="sxs-lookup"><span data-stu-id="70598-164">Memory usage of name server (Alert 12)</span></span>
- <span data-ttu-id="70598-165">Uso total de la memoria de las tablas de almacenamiento de columnas (alerta 40)</span><span class="sxs-lookup"><span data-stu-id="70598-165">Total memory usage of Column Store tables (Alert 40)</span></span>
- <span data-ttu-id="70598-166">Uso de memoria de los servicios (alerta 43)</span><span class="sxs-lookup"><span data-stu-id="70598-166">Memory usage of services (Alert 43)</span></span>
- <span data-ttu-id="70598-167">Uso de memoria del almacenamiento principal de las tablas de almacenamiento de columnas (alerta 45)</span><span class="sxs-lookup"><span data-stu-id="70598-167">Memory usage of main storage of Column Store tables (Alert 45)</span></span>
- <span data-ttu-id="70598-168">Archivos de volcado de tiempo de ejecución (alerta 46)</span><span class="sxs-lookup"><span data-stu-id="70598-168">Runtime dump files (Alert 46)</span></span>

<span data-ttu-id="70598-169">Consulte toohello [solución de problemas de SAP HANA: problemas de memoria](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) sitio pasos de solución de problemas detallada.</span><span class="sxs-lookup"><span data-stu-id="70598-169">Refer toohello [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="70598-170">**Red**</span><span class="sxs-lookup"><span data-stu-id="70598-170">**Network**</span></span>

<span data-ttu-id="70598-171">Consulte demasiado[SAP nota #2081065: solución de problemas de red de SAP HANA](https://launchpad.support.sap.com/#/notes/2081065) y realice los pasos descritos en esta nota de SAP de solución de problemas de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="70598-171">Refer too[SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform hello network troubleshooting steps in this SAP Note.</span></span>

1. <span data-ttu-id="70598-172">Analice el tiempo de ida y vuelta entre el cliente y el servidor.</span><span class="sxs-lookup"><span data-stu-id="70598-172">Analyzing round-trip time between server and client.</span></span>
  <span data-ttu-id="70598-173">A.</span><span class="sxs-lookup"><span data-stu-id="70598-173">A.</span></span> <span data-ttu-id="70598-174">Ejecutar script SQL de hello [ _HANA\_red\_clientes_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="70598-174">Run hello SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>
  
2. <span data-ttu-id="70598-175">Analice la comunicación entre nodos.</span><span class="sxs-lookup"><span data-stu-id="70598-175">Analyze internode communication.</span></span>
  <span data-ttu-id="70598-176">A.</span><span class="sxs-lookup"><span data-stu-id="70598-176">A.</span></span> <span data-ttu-id="70598-177">Ejecute el script SQL [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="70598-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>

3. <span data-ttu-id="70598-178">Ejecute el comando de Linux **ifconfig** (salida de hello muestra si se producen las pérdidas de paquetes).</span><span class="sxs-lookup"><span data-stu-id="70598-178">Run Linux command **ifconfig** (hello output shows if any packet losses are occurring).</span></span>
4. <span data-ttu-id="70598-179">Ejecute el comando de Linux **tcpdump**.</span><span class="sxs-lookup"><span data-stu-id="70598-179">Run Linux command **tcpdump**.</span></span>

<span data-ttu-id="70598-180">Además, utilizar código abierto de hello [IPERF](https://iperf.fr/) herramienta (o similar) rendimiento de la red de toomeasure real de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="70598-180">Also, use hello open source [IPERF](https://iperf.fr/) tool (or similar) toomeasure real application network performance.</span></span>

<span data-ttu-id="70598-181">Consulte toohello [solución de problemas de SAP HANA: problemas de conectividad y de rendimiento de red](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) sitio pasos de solución de problemas detallada.</span><span class="sxs-lookup"><span data-stu-id="70598-181">Refer toohello [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="70598-182">**Almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="70598-182">**Storage**</span></span>

<span data-ttu-id="70598-183">Desde la perspectiva del usuario final, una aplicación (o sistema de Hola como un todo) se ejecuta con lentitud, deja de responder o incluso puede parecer toohang si hay problemas de rendimiento de E/S.</span><span class="sxs-lookup"><span data-stu-id="70598-183">From an end-user perspective, an application (or hello system as a whole) runs sluggishly, is unresponsive, or can even seem toohang if there are issues with I/O performance.</span></span> <span data-ttu-id="70598-184">Hola **volúmenes** ficha en SAP HANA Studio, puede ver Hola adjunta volúmenes y los volúmenes se utilizan por cada servicio.</span><span class="sxs-lookup"><span data-stu-id="70598-184">In hello **Volumes** tab in SAP HANA Studio, you can see hello attached volumes, and what volumes are used by each service.</span></span>

![En la ficha de volúmenes de hello en SAP HANA Studio, puede ver Hola adjunta volúmenes y los volúmenes se utilizan por cada servicio](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

<span data-ttu-id="70598-186">Los volúmenes conectados en la parte inferior de Hola de pantalla de bienvenida, de que puede ver detalles Hola volúmenes, como archivos y estadísticas de E/S.</span><span class="sxs-lookup"><span data-stu-id="70598-186">Attached volumes in hello lower part of hello screen you can see details of hello volumes, such as files and I/O statistics.</span></span>

![Los volúmenes conectados en la parte inferior de Hola de pantalla de bienvenida, de que puede ver detalles Hola volúmenes, como archivos y estadísticas de E/S](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

<span data-ttu-id="70598-188">Consulte toohello [solución de problemas de SAP HANA: E/S relacionados causas y soluciones](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) y [solución de problemas de SAP HANA: disco relacionados causas y soluciones](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) sitio pasos de solución de problemas detallada.</span><span class="sxs-lookup"><span data-stu-id="70598-188">Refer toohello [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="70598-189">**Herramientas de diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="70598-189">**Diagnostic Tools**</span></span>

<span data-ttu-id="70598-190">Realice una comprobación del estado de SAP HANA mediante HANA\_Configuration\_Minichecks.</span><span class="sxs-lookup"><span data-stu-id="70598-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span></span> <span data-ttu-id="70598-191">Esta herramienta devuelve problemas técnicos potencialmente críticos que ya deberían haber aparecido como alertas en SAP HANA Studio.</span><span class="sxs-lookup"><span data-stu-id="70598-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span></span>

<span data-ttu-id="70598-192">Consulte demasiado[SAP nota #1969700: colección de instrucciones SQL para SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) y descargar nota de hello SQL Statements.zip archivo toothat adjunto.</span><span class="sxs-lookup"><span data-stu-id="70598-192">Refer too[SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download hello SQL Statements.zip file attached toothat note.</span></span> <span data-ttu-id="70598-193">Almacene este archivo .zip en la unidad de disco duro local Hola.</span><span class="sxs-lookup"><span data-stu-id="70598-193">Store this .zip file on hello local hard drive.</span></span>

<span data-ttu-id="70598-194">En SAP HANA Studio, en hello **información del sistema** pestaña, haga clic en hello **nombre** columna y seleccione **instrucciones de importación SQL**.</span><span class="sxs-lookup"><span data-stu-id="70598-194">In SAP HANA Studio, on hello **System Information** tab, right-click in hello **Name** column and select **Import SQL Statements**.</span></span>

![En SAP HANA Studio, en la ficha de información del sistema de hello, haga clic en la columna de nombre de Hola y seleccione instrucciones SQL de importación](./media/troubleshooting-monitoring/image7-import-statements-a.png)

<span data-ttu-id="70598-196">Seleccione Hola SQL Statements.zip archivo almacena localmente y se importará una carpeta con instrucciones SQL correspondientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="70598-196">Select hello SQL Statements.zip file stored locally, and a folder with hello corresponding SQL statements will be imported.</span></span> <span data-ttu-id="70598-197">En este momento, hello que muchas comprobaciones de diagnóstico diferentes se pueden ejecutar con estas instrucciones SQL.</span><span class="sxs-lookup"><span data-stu-id="70598-197">At this point, hello many different diagnostic checks can be run with these SQL statements.</span></span>

<span data-ttu-id="70598-198">Por ejemplo, requisitos de ancho de banda de replicación del sistema de SAP HANA tootest, haga clic en hello **ancho de banda** instrucción en **replicación: ancho de banda** y seleccione **abiertos** en la consola de SQL.</span><span class="sxs-lookup"><span data-stu-id="70598-198">For example, tootest SAP HANA System Replication bandwidth requirements, right-click hello **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span></span>

<span data-ttu-id="70598-199">instrucción SQL completa de Hello abre toobe de parámetros de entrada (sección de modificación) lo que permite cambiar y, a continuación, se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="70598-199">hello complete SQL statement opens allowing input parameters (modification section) toobe changed and then executed.</span></span>

![instrucción SQL completa de Hello abre toobe de parámetros de entrada (sección de modificación) lo que permite cambiar y, a continuación, ejecutar](./media/troubleshooting-monitoring/image8-import-statements-b.png)

<span data-ttu-id="70598-201">Otro ejemplo es clic en las instrucciones de hello en **replicación: información general sobre**.</span><span class="sxs-lookup"><span data-stu-id="70598-201">Another example is right-clicking on hello statements under **Replication: Overview**.</span></span> <span data-ttu-id="70598-202">Seleccione **Execute** desde el menú contextual de hello:</span><span class="sxs-lookup"><span data-stu-id="70598-202">Select **Execute** from hello context menu:</span></span>

![Otro ejemplo es clic en las instrucciones de hello en la replicación: información general.](./media/troubleshooting-monitoring/image9-import-statements-c.png)

<span data-ttu-id="70598-205">Esto genera información que ayuda a solucionar el problema:</span><span class="sxs-lookup"><span data-stu-id="70598-205">This results in information that helps with troubleshooting:</span></span>

![Esto generará información que ayudará a solucionar el problema](./media/troubleshooting-monitoring/image10-import-statements-d.png)

<span data-ttu-id="70598-207">Hola igual de HANA\_configuración\_Minichecks y compruebe si hay alguna _X_ marcas en hello _C_ columna (crítico).</span><span class="sxs-lookup"><span data-stu-id="70598-207">Do hello same for HANA\_Configuration\_Minichecks and check for any _X_ marks in hello _C_ (Critical) column.</span></span>

<span data-ttu-id="70598-208">Ejemplo de salidas:</span><span class="sxs-lookup"><span data-stu-id="70598-208">Sample outputs:</span></span>

<span data-ttu-id="70598-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** para comprobaciones general de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="70598-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span></span>

![HANA\_Configuration\_MiniChecks\_Rev102.01+1 para comprobaciones general de SAP HANA](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

<span data-ttu-id="70598-211">**HANA\_Services\_Overview** para información general sobre los servicios de SAP HANA que se están ejecutando.</span><span class="sxs-lookup"><span data-stu-id="70598-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span></span>

![HANA\_Services\_Overview para información general sobre los servicios de SAP HANA que se están ejecutando](./media/troubleshooting-monitoring/image12-services-overview.png)

<span data-ttu-id="70598-213">**HANA\_Services\_Statistics**para información sobre los servicio de SAP HANA (CPU, memoria, etc.).</span><span class="sxs-lookup"><span data-stu-id="70598-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span></span>

![<span data-ttu-id="70598-214">HANA\_Services\_Statistics para información sobre los servicio de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="70598-214">HANA\_Services\_Statistics for SAP HANA service information</span></span> ](./media/troubleshooting-monitoring/image13-services-statistics.png)

<span data-ttu-id="70598-215">**HANA\_configuración\_Introducción\_Rev110 +** para obtener información general sobre la instancia de SAP HANA Hola.</span><span class="sxs-lookup"><span data-stu-id="70598-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on hello SAP HANA instance.</span></span>

![HANA\_configuración\_Introducción\_Rev110 + para obtener información general sobre la instancia de SAP HANA Hola](./media/troubleshooting-monitoring/image14-configuration-overview.png)

<span data-ttu-id="70598-217">**HANA\_configuración\_parámetros\_Rev70 +** toocheck parámetros de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="70598-217">**HANA\_Configuration\_Parameters\_Rev70+** toocheck SAP HANA parameters.</span></span>

![HANA\_configuración\_parámetros\_parámetros de SAP HANA de toocheck Rev70 +](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

