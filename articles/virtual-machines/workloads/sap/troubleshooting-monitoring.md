---
title: "Solución de problemas y supervisión de SAP HANA en Azure (Instancias grandes) | Microsoft Docs"
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
ms.openlocfilehash: ee5be707b443cbe42bf4a492d79390e534d4b91f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-troubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a><span data-ttu-id="c2ba2-103">Procedimiento para solucionar problemas y supervisar SAP HANA en Azure (instancias grandes)</span><span class="sxs-lookup"><span data-stu-id="c2ba2-103">How to troubleshoot and monitor SAP HANA (large instances) on Azure</span></span>


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="c2ba2-104">Supervisión de SAP HANA en Azure (Instancias grandes)</span><span class="sxs-lookup"><span data-stu-id="c2ba2-104">Monitoring in SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="c2ba2-105">SAP HANA en Azure (Instancias grandes) no se diferencia de cualquier otra implementación de IaaS: necesita supervisar lo que están haciendo el sistema operativo y la aplicación y cómo consumen los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="c2ba2-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need to monitor what the OS and the application is doing and how these consume the following resources:</span></span>

- <span data-ttu-id="c2ba2-106">CPU</span><span class="sxs-lookup"><span data-stu-id="c2ba2-106">CPU</span></span>
- <span data-ttu-id="c2ba2-107">Memoria</span><span class="sxs-lookup"><span data-stu-id="c2ba2-107">Memory</span></span>
- <span data-ttu-id="c2ba2-108">Ancho de banda de red</span><span class="sxs-lookup"><span data-stu-id="c2ba2-108">Network bandwidth</span></span>
- <span data-ttu-id="c2ba2-109">Espacio en disco</span><span class="sxs-lookup"><span data-stu-id="c2ba2-109">Disk space</span></span>

<span data-ttu-id="c2ba2-110">Al igual que con Azure Virtual Machines, debe averiguar si las clases de recursos indicadas anteriormente serán suficientes, o si se agotarán.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-110">As with Azure Virtual Machines you need to figure out whether the resource classes named above are sufficient, or whether these get depleted.</span></span> <span data-ttu-id="c2ba2-111">A continuación se proporcionan más detalles sobre cada una de las clases:</span><span class="sxs-lookup"><span data-stu-id="c2ba2-111">Here is more detail on each of the different classes:</span></span>

<span data-ttu-id="c2ba2-112">**Consumo de recursos de CPU:** se fuerza la relación definida por SAP para una determinada carga de trabajo con HANA con el fin de asegurarse de que haya suficientes recursos de CPU disponibles para trabajar con los datos almacenados en la memoria.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-112">**CPU resource consumption:** The ratio that SAP defined for certain workload against HANA is enforced to make sure that there should be enough CPU resources available to work through the data that is stored in memory.</span></span> <span data-ttu-id="c2ba2-113">No obstante, puede haber casos en los que HANA consuma una gran cantidad de CPU al ejecutar consultas debido a que falten índices o problemas similares.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due to missing indexes or similar issues.</span></span> <span data-ttu-id="c2ba2-114">Esto significa que debe supervisar el consumo de los recursos de CPU por parte de la unidad de Instancias grandes de HANA, así como los recursos de CPU utilizados por servicios específicos de HANA.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-114">This means you should monitor CPU resource consumption of the HANA large instance unit as well as CPU resources consumed by the specific HANA services.</span></span>

<span data-ttu-id="c2ba2-115">**Consumo de memoria:** es importante supervisarlo desde dentro y desde fuera de HANA (en la unidad).</span><span class="sxs-lookup"><span data-stu-id="c2ba2-115">**Memory consumption:** Is important to monitor from within HANA, as well as outside of HANA on the unit.</span></span> <span data-ttu-id="c2ba2-116">Dentro de HANA, supervise cómo los datos utilizan la memoria asignada a HANA con el fin de que se mantengan dentro de las directrices de tamaño obligatorias de SAP.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-116">Within HANA, monitor how the data is consuming HANA allocated memory in order to stay within the required sizing guidelines of SAP.</span></span> <span data-ttu-id="c2ba2-117">También puede supervisar el consumo de memoria en el nivel de Instancias grandes para asegurarse de que el software instalado no perteneciente a HANA no utiliza demasiada memoria y compite por la memoria con HANA.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-117">You also want to monitor memory consumption on the Large Instance level to make sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span></span>

<span data-ttu-id="c2ba2-118">**Ancho de banda de red:** la puerta de enlace de red virtual de Azure tiene una limitación en el ancho de banda de los datos que se transfieren a la red virtual de Azure, por lo que es útil supervisar los datos recibidos por todas las máquinas virtuales de Azure dentro de una red virtual para averiguar si está cerca de los límites de la SKU de puerta de enlace de Azure que seleccionó.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-118">**Network bandwidth:** The Azure VNet gateway is limited in bandwidth of data moving into the Azure VNet, so it is helpful to monitor the data received by all the Azure VMs within a VNet to figure out how close you are to the limits of the Azure gateway SKU you selected.</span></span> <span data-ttu-id="c2ba2-119">En la unidad de Instancias grandes de HANA, tiene sentido supervisar también el tráfico de red de entrada y de salida, así como realizar un seguimiento de los volúmenes que se administran a lo largo del tiempo.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-119">On the HANA Large Instance unit, it does make sense to monitor incoming and outgoing network traffic as well, and to keep track of the volumes that are handled over time.</span></span>

<span data-ttu-id="c2ba2-120">**Espacio en disco:** normalmente su uso aumenta a lo largo del tiempo.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-120">**Disk space:** Disk space consumption usually increases over time.</span></span> <span data-ttu-id="c2ba2-121">Hay muchas razones para ello, pero las principales son: aumenta el volumen de datos, la ejecución de copias de seguridad de los registros de transacciones, el almacenamiento de los archivos de seguimiento y la realización de instantáneas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span></span> <span data-ttu-id="c2ba2-122">Por lo tanto, es importante supervisarlo y administrar el espacio en disco asociado a la unidad de Instancias grandes de HANA.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-122">Therefore, it is important to monitor disk space usage and manage the disk space associated with the HANA Large Instance unit.</span></span>

## <a name="monitoring-and-troubleshooting-from-hana-side"></a><span data-ttu-id="c2ba2-123">Supervisión y solución de problemas en el lado HANA</span><span class="sxs-lookup"><span data-stu-id="c2ba2-123">Monitoring and troubleshooting from HANA side</span></span>

<span data-ttu-id="c2ba2-124">Con el fin de analizar de forma eficaz los problemas relacionados con SAP HANA en Azure (Instancias grandes), es conveniente averiguar la causa raíz de un problema.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-124">In order to effectively analyze problems related to SAP HANA on Azure (Large Instances), it is useful to narrow down the root cause of a problem.</span></span> <span data-ttu-id="c2ba2-125">SAP ha publicado una gran cantidad de documentación para ayudarle.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-125">SAP has published a large amount of documentation to help you.</span></span>

<span data-ttu-id="c2ba2-126">Las preguntas más frecuentes relacionadas con el rendimiento de SAP HANA pueden encontrarse en las siguientes notas de SAP:</span><span class="sxs-lookup"><span data-stu-id="c2ba2-126">Applicable FAQs related to SAP HANA performance can be found in the following SAP Notes:</span></span>

- <span data-ttu-id="c2ba2-127">[SAP Note #2222200 – FAQ: SAP HANA Network](https://launchpad.support.sap.com/#/notes/2222200) (Nota de SAP 2222200: preguntas más frecuentes sobre la red de SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="c2ba2-127">[SAP Note #2222200 – FAQ: SAP HANA Network](https://launchpad.support.sap.com/#/notes/2222200)</span></span>
- <span data-ttu-id="c2ba2-128">[SAP Note #2100040 – FAQ: SAP HANA CPU](https://launchpad.support.sap.com/#/notes/0002100040) (Nota de SAP 2100040: preguntas más frecuentes sobre la CPU de SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="c2ba2-128">[SAP Note #2100040 – FAQ: SAP HANA CPU](https://launchpad.support.sap.com/#/notes/0002100040)</span></span>
- <span data-ttu-id="c2ba2-129">[SAP Note #199997 – FAQ: SAP HANA Memory](https://launchpad.support.sap.com/#/notes/2177064) (Nota de SAP 199997: preguntas más frecuentes sobre la memoria de SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="c2ba2-129">[SAP Note #199997 – FAQ: SAP HANA Memory](https://launchpad.support.sap.com/#/notes/2177064)</span></span>
- <span data-ttu-id="c2ba2-130">[SAP Note #200000 – FAQ: SAP HANA Performance Optimization](https://launchpad.support.sap.com/#/notes/2000000) (Nota de SAP 199997: preguntas más frecuentes sobre la optimización del rendimiento de SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="c2ba2-130">[SAP Note #200000 – FAQ: SAP HANA Performance Optimization](https://launchpad.support.sap.com/#/notes/2000000)</span></span>
- <span data-ttu-id="c2ba2-131">[SAP Note #199930 – FAQ: SAP HANA I/O Analysis](https://launchpad.support.sap.com/#/notes/1999930) (Nota de SAP 199930: preguntas más frecuentes sobre el análisis de E/S de SAP HANA)</span><span class="sxs-lookup"><span data-stu-id="c2ba2-131">[SAP Note #199930 – FAQ: SAP HANA I/O Analysis](https://launchpad.support.sap.com/#/notes/1999930)</span></span>
- <span data-ttu-id="c2ba2-132">[SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes](https://launchpad.support.sap.com/#/notes/2177064) (Nota de SAP #2177064: preguntas más frecuentes sobre el reinicio y la caída del servicio)</span><span class="sxs-lookup"><span data-stu-id="c2ba2-132">[SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes](https://launchpad.support.sap.com/#/notes/2177064)</span></span>

<span data-ttu-id="c2ba2-133">**Alertas de SAP HANA**</span><span class="sxs-lookup"><span data-stu-id="c2ba2-133">**SAP HANA Alerts**</span></span>

<span data-ttu-id="c2ba2-134">Como primer paso, compruebe los registros de alerta de SAP HANA actuales.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-134">As a first step, check the current SAP HANA alert logs.</span></span> <span data-ttu-id="c2ba2-135">En SAP HANA Studio, vaya a **Consola de administración: Alertas: Mostrar: Todas las alertas**.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-135">In SAP HANA Studio, go to **Administration Console: Alerts: Show: all alerts**.</span></span> <span data-ttu-id="c2ba2-136">En esta pestaña se muestran todas las alertas de SAP HANA para determinados valores (memoria física libre, uso de CPU, etc.) que se encuentran fuera de los umbrales mínimo y máximo establecidos.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of the set minimum and maximum thresholds.</span></span> <span data-ttu-id="c2ba2-137">De forma predeterminada, las comprobaciones se actualizan automáticamente cada 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-137">By default, checks are auto-refreshed every 15 minutes.</span></span>

![En SAP HANA Studio, vaya a Consola de administración: Alertas: Mostrar: Todas las alertas.](./media/troubleshooting-monitoring/image1-show-alerts.png)

<span data-ttu-id="c2ba2-139">**CPU**</span><span class="sxs-lookup"><span data-stu-id="c2ba2-139">**CPU**</span></span>

<span data-ttu-id="c2ba2-140">En el caso de una alerta activada debido a una configuración incorrecta del umbral, una solución es restablecerlo al valor predeterminado o a un valor más razonable.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-140">For an alert triggered due to improper threshold setting, a resolution is to reset to the default value or a more reasonable threshold value.</span></span>

![Restablecer el umbral al valor predeterminado o a un valor más razonable](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

<span data-ttu-id="c2ba2-142">Las siguientes alertas pueden indicar problemas de recursos de CPU:</span><span class="sxs-lookup"><span data-stu-id="c2ba2-142">The following alerts may indicate CPU resource problems:</span></span>

- <span data-ttu-id="c2ba2-143">Uso de CPU del host (alerta 5)</span><span class="sxs-lookup"><span data-stu-id="c2ba2-143">Host CPU Usage (Alert 5)</span></span>
- <span data-ttu-id="c2ba2-144">Operación del punto de retorno más reciente (alerta 28)</span><span class="sxs-lookup"><span data-stu-id="c2ba2-144">Most recent savepoint operation (Alert 28)</span></span>
- <span data-ttu-id="c2ba2-145">Duración del punto de retorno (alerta 54)</span><span class="sxs-lookup"><span data-stu-id="c2ba2-145">Savepoint duration (Alert 54)</span></span>

<span data-ttu-id="c2ba2-146">Puede observar el uso de CPU elevado en la base de datos de SAP HANA de las siguientes formas:</span><span class="sxs-lookup"><span data-stu-id="c2ba2-146">You may notice high CPU consumption on your SAP HANA database from one of the following:</span></span>

- <span data-ttu-id="c2ba2-147">La alerta 5 (Uso de CPU del host) se desencadena para el uso de CPU actual o antiguo</span><span class="sxs-lookup"><span data-stu-id="c2ba2-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span></span>
- <span data-ttu-id="c2ba2-148">El uso de CPU mostrado en la pantalla de información general</span><span class="sxs-lookup"><span data-stu-id="c2ba2-148">The displayed CPU usage on the overview screen</span></span>

![Uso de CPU mostrado en la pantalla de información general](./media/troubleshooting-monitoring/image3-cpu-usage.png)

<span data-ttu-id="c2ba2-150">El gráfico Carga podría mostrar un uso de CPU elevado o un uso de elevado en el pasado:</span><span class="sxs-lookup"><span data-stu-id="c2ba2-150">The Load graph might show high CPU consumption, or high consumption in the past:</span></span>

![El gráfico Carga podría mostrar un uso de CPU elevado o un uso de elevado en el pasado](./media/troubleshooting-monitoring/image4-load-graph.png)

<span data-ttu-id="c2ba2-152">Una alerta desencadenada debido al uso elevado de CPU puede tener varias causas; entre ellas, la ejecución de ciertas transacciones, la carga de datos, trabajos que no responden, instrucciones SQL de larga ejecución y un rendimiento de consulta incorrecto (por ejemplo, con BW en cubos HANA).</span><span class="sxs-lookup"><span data-stu-id="c2ba2-152">An alert triggered due to high CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span></span>

<span data-ttu-id="c2ba2-153">Consulte el sitio sobre la [solución de problemas de SAP HANA: causas relacionadas con la CPU y soluciones](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) para ver los pasos detallados para la solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-153">Refer to the [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="c2ba2-154">**Sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="c2ba2-154">**Operating System**</span></span>

<span data-ttu-id="c2ba2-155">Una de las comprobaciones más importantes para SAP HANA en Linux es asegurarse de que las páginas gigantes transparentes están deshabilitadas; consulte la [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662) (Nota de SAP #2131662: páginas gigantes transparentes (THP) en servidores de SAP HANA).</span><span class="sxs-lookup"><span data-stu-id="c2ba2-155">One of the most important checks for SAP HANA on Linux is to make sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span></span>

- <span data-ttu-id="c2ba2-156">Puede comprobar si las páginas gigantes transparentes están habilitadas con el siguiente comando de Linux: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span><span class="sxs-lookup"><span data-stu-id="c2ba2-156">You can check if Transparent Huge Pages are enabled through the following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span></span>
- <span data-ttu-id="c2ba2-157">Si _always_ está encerrado entre corchetes como a continuación, significa que las páginas gigantes transparentes están habilitadas: [always] madvise never; si _never_ está encerrado entre corchetes como a continuación, significa que las páginas gigantes transparentes están deshabilitadas: always madvise [never]</span><span class="sxs-lookup"><span data-stu-id="c2ba2-157">If _always_ is enclosed in brackets as below, it means that the Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that the Transparent Huge Pages are disabled: always madvise [never]</span></span>

<span data-ttu-id="c2ba2-158">El siguiente comando de Linux no debe devolver nada: **rpm -qa | grep ulimit.**</span><span class="sxs-lookup"><span data-stu-id="c2ba2-158">The following Linux command should return nothing: **rpm -qa | grep ulimit.**</span></span> <span data-ttu-id="c2ba2-159">Si indica que _ulimit_ está instalado, desinstálelo inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-159">If it appears _ulimit_ is installed, uninstall it immediately.</span></span>

<span data-ttu-id="c2ba2-160">**Memoria**</span><span class="sxs-lookup"><span data-stu-id="c2ba2-160">**Memory**</span></span>

<span data-ttu-id="c2ba2-161">Puede observar que la cantidad de memoria asignada por la base de datos de SAP HANA es mayor de lo esperado.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-161">You may observe that the amount of memory allocated by the SAP HANA database is higher than expected.</span></span> <span data-ttu-id="c2ba2-162">Las siguientes alertas indican problemas con un uso de memoria elevado:</span><span class="sxs-lookup"><span data-stu-id="c2ba2-162">The following alerts indicate issues with high memory usage:</span></span>

- <span data-ttu-id="c2ba2-163">Uso de memoria física del host (alerta 1)</span><span class="sxs-lookup"><span data-stu-id="c2ba2-163">Host physical memory usage (Alert 1)</span></span>
- <span data-ttu-id="c2ba2-164">Uso de memoria del servidor de nombres (alerta 12)</span><span class="sxs-lookup"><span data-stu-id="c2ba2-164">Memory usage of name server (Alert 12)</span></span>
- <span data-ttu-id="c2ba2-165">Uso total de la memoria de las tablas de almacenamiento de columnas (alerta 40)</span><span class="sxs-lookup"><span data-stu-id="c2ba2-165">Total memory usage of Column Store tables (Alert 40)</span></span>
- <span data-ttu-id="c2ba2-166">Uso de memoria de los servicios (alerta 43)</span><span class="sxs-lookup"><span data-stu-id="c2ba2-166">Memory usage of services (Alert 43)</span></span>
- <span data-ttu-id="c2ba2-167">Uso de memoria del almacenamiento principal de las tablas de almacenamiento de columnas (alerta 45)</span><span class="sxs-lookup"><span data-stu-id="c2ba2-167">Memory usage of main storage of Column Store tables (Alert 45)</span></span>
- <span data-ttu-id="c2ba2-168">Archivos de volcado de tiempo de ejecución (alerta 46)</span><span class="sxs-lookup"><span data-stu-id="c2ba2-168">Runtime dump files (Alert 46)</span></span>

<span data-ttu-id="c2ba2-169">Consulte el sitio sobre la [solución de problemas de SAP HANA: problemas de memoria](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) para ver los pasos detallados para la solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-169">Refer to the [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="c2ba2-170">**Red**</span><span class="sxs-lookup"><span data-stu-id="c2ba2-170">**Network**</span></span>

<span data-ttu-id="c2ba2-171">Consulte [SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) (Nota de SAP #2081065: solución de problemas de la red de SAP HANA) y realice los pasos para solucionar los problemas de red indicados en ella.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-171">Refer to [SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform the network troubleshooting steps in this SAP Note.</span></span>

1. <span data-ttu-id="c2ba2-172">Analice el tiempo de ida y vuelta entre el cliente y el servidor.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-172">Analyzing round-trip time between server and client.</span></span>
  <span data-ttu-id="c2ba2-173">A.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-173">A.</span></span> <span data-ttu-id="c2ba2-174">Ejecute el script SQL [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="c2ba2-174">Run the SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>
  
2. <span data-ttu-id="c2ba2-175">Analice la comunicación entre nodos.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-175">Analyze internode communication.</span></span>
  <span data-ttu-id="c2ba2-176">A.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-176">A.</span></span> <span data-ttu-id="c2ba2-177">Ejecute el script SQL [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="c2ba2-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>

3. <span data-ttu-id="c2ba2-178">Ejecute el comando de Linux **ifconfig** (la salida muestra si se producen las pérdidas de paquetes).</span><span class="sxs-lookup"><span data-stu-id="c2ba2-178">Run Linux command **ifconfig** (the output shows if any packet losses are occurring).</span></span>
4. <span data-ttu-id="c2ba2-179">Ejecute el comando de Linux **tcpdump**.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-179">Run Linux command **tcpdump**.</span></span>

<span data-ttu-id="c2ba2-180">Además, utilice la herramienta de código abierto [IPERF](https://iperf.fr/) (u otra similar) para medir el rendimiento de red real de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-180">Also, use the open source [IPERF](https://iperf.fr/) tool (or similar) to measure real application network performance.</span></span>

<span data-ttu-id="c2ba2-181">Consulte el sitio sobre la [solución de problemas de SAP HANA: problemas de conectividad y de rendimiento de red](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) para ver los pasos detallados para la solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-181">Refer to the [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="c2ba2-182">**Storage**</span><span class="sxs-lookup"><span data-stu-id="c2ba2-182">**Storage**</span></span>

<span data-ttu-id="c2ba2-183">Desde la perspectiva del usuario final, una aplicación (o el sistema en su conjunto) se ejecuta lentamente, deja de responder o incluso puede parecer que se cuelga si hay problemas de rendimiento de E/S.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-183">From an end-user perspective, an application (or the system as a whole) runs sluggishly, is unresponsive, or can even seem to hang if there are issues with I/O performance.</span></span> <span data-ttu-id="c2ba2-184">En la pestaña **Volúmenes** de SAP HANA Studio, puede ver los volúmenes conectados y los utilizados por cada servicio.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-184">In the **Volumes** tab in SAP HANA Studio, you can see the attached volumes, and what volumes are used by each service.</span></span>

![En la pestaña Volúmenes de SAP HANA Studio, puede ver los volúmenes conectados y los utilizados por cada servicio](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

<span data-ttu-id="c2ba2-186">Para los volúmenes conectados, en la parte inferior de la pantalla puede ver los detalles de los volúmenes, como los archivos y las estadísticas de E/S.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-186">Attached volumes in the lower part of the screen you can see details of the volumes, such as files and I/O statistics.</span></span>

![Para los volúmenes conectados, en la parte inferior de la pantalla puede ver los detalles de los volúmenes, como los archivos y las estadísticas de E/S](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

<span data-ttu-id="c2ba2-188">Consulte el sitio sobre la [solución de problemas de SAP HANA: causas raíz relacionadas con E/S y soluciones](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) y la [solución de problemas de SAP HANA: causas raíz relacionadas con el disco](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) para ver los pasos detallados para la solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-188">Refer to the [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="c2ba2-189">**Herramientas de diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="c2ba2-189">**Diagnostic Tools**</span></span>

<span data-ttu-id="c2ba2-190">Realice una comprobación del estado de SAP HANA mediante HANA\_Configuration\_Minichecks.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span></span> <span data-ttu-id="c2ba2-191">Esta herramienta devuelve problemas técnicos potencialmente críticos que ya deberían haber aparecido como alertas en SAP HANA Studio.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span></span>

<span data-ttu-id="c2ba2-192">Consulte [SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) (Nota de SAP #1969700: recopilación de instrucciones SQL para SAP HANA) y descargue el archivo SQL Statements.zip adjunto a esa nota.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-192">Refer to [SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download the SQL Statements.zip file attached to that note.</span></span> <span data-ttu-id="c2ba2-193">Almacene este archivo .zip en el disco duro local.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-193">Store this .zip file on the local hard drive.</span></span>

<span data-ttu-id="c2ba2-194">En SAP HANA Studio, en la pestaña **System Information** (Información del sistema), haga clic en la columna **Name** (Nombre) y seleccione **Import SQL Statements** (Instrucciones SQL de importación).</span><span class="sxs-lookup"><span data-stu-id="c2ba2-194">In SAP HANA Studio, on the **System Information** tab, right-click in the **Name** column and select **Import SQL Statements**.</span></span>

![En SAP HANA Studio, en la pestaña System Information (Información del sistema), haga clic en la columna Name (Nombre) y seleccione Import SQL Statements (Instrucciones SQL de importación)](./media/troubleshooting-monitoring/image7-import-statements-a.png)

<span data-ttu-id="c2ba2-196">Seleccione el archivo SQL Statements.zip que está almacenado localmente y se importará una carpeta con las instrucciones SQL correspondientes.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-196">Select the SQL Statements.zip file stored locally, and a folder with the corresponding SQL statements will be imported.</span></span> <span data-ttu-id="c2ba2-197">En este punto, se pueden ejecutar las numerosas comprobaciones de diagnóstico con estas instrucciones SQL.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-197">At this point, the many different diagnostic checks can be run with these SQL statements.</span></span>

<span data-ttu-id="c2ba2-198">Por ejemplo, para probar los requisitos de ancho de banda de la replicación del sistema de SAP HANA, haga clic en la instrucción **Bandwidth** (Bancho de banda) en **Replication: Bandwidth** (Replicación: ancho de banda) y seleccione **Open** (Abrir) en la consola de SQL.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-198">For example, to test SAP HANA System Replication bandwidth requirements, right-click the **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span></span>

<span data-ttu-id="c2ba2-199">La instrucción SQL completa se abre, lo que permite cambiar y, después, ejecutar los parámetros de entrada (sección de modificación).</span><span class="sxs-lookup"><span data-stu-id="c2ba2-199">The complete SQL statement opens allowing input parameters (modification section) to be changed and then executed.</span></span>

![La instrucción SQL completa se abre, lo que permite cambiar y, después, ejecutar los parámetros de entrada (sección de modificación)](./media/troubleshooting-monitoring/image8-import-statements-b.png)

<span data-ttu-id="c2ba2-201">Otro ejemplo es hacer clic en las instrucciones en **Replication: Overview** (Replicación: Información general).</span><span class="sxs-lookup"><span data-stu-id="c2ba2-201">Another example is right-clicking on the statements under **Replication: Overview**.</span></span> <span data-ttu-id="c2ba2-202">Seleccione **Execute** (Ejecutar) en el menú contextual:</span><span class="sxs-lookup"><span data-stu-id="c2ba2-202">Select **Execute** from the context menu:</span></span>

![Otro ejemplo es hacer clic en las instrucciones en Replication: Overview (Replicación: Información general).](./media/troubleshooting-monitoring/image9-import-statements-c.png)

<span data-ttu-id="c2ba2-205">Esto genera información que ayuda a solucionar el problema:</span><span class="sxs-lookup"><span data-stu-id="c2ba2-205">This results in information that helps with troubleshooting:</span></span>

![Esto generará información que ayudará a solucionar el problema](./media/troubleshooting-monitoring/image10-import-statements-d.png)

<span data-ttu-id="c2ba2-207">Haga lo mismo para HANA\_Configuration\_Minichecks y compruebe si hay alguna marca _X_ en la columna _C_ (Crítico).</span><span class="sxs-lookup"><span data-stu-id="c2ba2-207">Do the same for HANA\_Configuration\_Minichecks and check for any _X_ marks in the _C_ (Critical) column.</span></span>

<span data-ttu-id="c2ba2-208">Ejemplo de salidas:</span><span class="sxs-lookup"><span data-stu-id="c2ba2-208">Sample outputs:</span></span>

<span data-ttu-id="c2ba2-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** para comprobaciones general de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span></span>

![HANA\_Configuration\_MiniChecks\_Rev102.01+1 para comprobaciones general de SAP HANA](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

<span data-ttu-id="c2ba2-211">**HANA\_Services\_Overview** para información general sobre los servicios de SAP HANA que se están ejecutando.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span></span>

![HANA\_Services\_Overview para información general sobre los servicios de SAP HANA que se están ejecutando](./media/troubleshooting-monitoring/image12-services-overview.png)

<span data-ttu-id="c2ba2-213">**HANA\_Services\_Statistics**para información sobre los servicio de SAP HANA (CPU, memoria, etc.).</span><span class="sxs-lookup"><span data-stu-id="c2ba2-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span></span>

![<span data-ttu-id="c2ba2-214">HANA\_Services\_Statistics para información sobre los servicio de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="c2ba2-214">HANA\_Services\_Statistics for SAP HANA service information</span></span> ](./media/troubleshooting-monitoring/image13-services-statistics.png)

<span data-ttu-id="c2ba2-215">**HANA\_Configuration\_Overview\_Rev110+** para información general sobre la instancia de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on the SAP HANA instance.</span></span>

![HANA\_Configuration\_Overview\_Rev110+ para información general sobre la instancia de SAP HANA](./media/troubleshooting-monitoring/image14-configuration-overview.png)

<span data-ttu-id="c2ba2-217">**HANA\_Configuration\_Parameters\_Rev70+** para comprobar los parámetros de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="c2ba2-217">**HANA\_Configuration\_Parameters\_Rev70+** to check SAP HANA parameters.</span></span>

![HANA\_Configuration\_Parameters\_Rev70+ para comprobar los parámetros de SAP HANA](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

