---
title: registros de aaaVisualizing flujo de grupo de seguridad de red de Azure con Power BI | Documentos de Microsoft
description: "Esta página describe el funcionamiento de flujo NSG toovisualize los registros con Power BI."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a><span data-ttu-id="bd0a2-103">Visualización de registros de flujo del grupo de seguridad de red con Power BI</span><span class="sxs-lookup"><span data-stu-id="bd0a2-103">Visualizing Network Security Group flow logs with Power BI</span></span>

<span data-ttu-id="bd0a2-104">Los registros de flujo de grupo de seguridad de red permiten tooview información sobre el tráfico IP de entrada y salida sobre los grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-104">Network Security Group flow logs allow you tooview information about ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="bd0a2-105">Mostrarán salidos estos registros de flujo y flujos de entrada en cada regla, Hola flujo de hello NIC se aplica a, 5-tupla información acerca del flujo de hello (origen/destino IP, puerto de origen/destino, protocolo), y si el tráfico de Hola se permitirá o denegará.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="bd0a2-106">Puede ser difícil toogain visiones flujo de registro de los datos mediante la búsqueda manualmente archivos de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-106">It can be difficult toogain insights into flow logging data by manually searching hello log files.</span></span> <span data-ttu-id="bd0a2-107">En este artículo se proporciona una solución toovisualize el flujo de más reciente registra y obtener información sobre el tráfico en la red.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-107">In this article, we provide a solution toovisualize your most recent flow logs and learn about traffic on your network.</span></span>

## <a name="scenario"></a><span data-ttu-id="bd0a2-108">Escenario</span><span class="sxs-lookup"><span data-stu-id="bd0a2-108">Scenario</span></span>

<span data-ttu-id="bd0a2-109">Hola siguiendo el escenario, nos conectamos cuenta de almacenamiento de Power BI desktop toohello que hemos configurado como receptor de Hola para nuestros datos del flujo de registro de NSG.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-109">In hello following scenario, we connect Power BI desktop toohello storage account we have configured as hello sink for our NSG Flow Logging data.</span></span> <span data-ttu-id="bd0a2-110">Una vez se conecta la cuenta de almacenamiento tooour, Power BI descarga y analiza Hola registros tooprovide una representación visual del tráfico de Hola que se registra por grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-110">After we connect tooour storage account, Power BI downloads and parses hello logs tooprovide a visual representation of hello traffic that is logged by Network Security groups.</span></span>

<span data-ttu-id="bd0a2-111">Uso de objetos visuales de hello proporcionados en la plantilla de hello que puede examinar:</span><span class="sxs-lookup"><span data-stu-id="bd0a2-111">Using hello visuals supplied in hello template you can examine:</span></span>

* <span data-ttu-id="bd0a2-112">Top Talkers</span><span class="sxs-lookup"><span data-stu-id="bd0a2-112">Top Talkers</span></span>
* <span data-ttu-id="bd0a2-113">Datos de flujo de serie temporal por decisión de regla y dirección</span><span class="sxs-lookup"><span data-stu-id="bd0a2-113">Time Series Flow Data by direction and rule decision</span></span>
* <span data-ttu-id="bd0a2-114">Flujos por dirección MAC de la interfaz de red</span><span class="sxs-lookup"><span data-stu-id="bd0a2-114">Flows by Network Interface MAC address</span></span>
* <span data-ttu-id="bd0a2-115">Flujos por NSG y regla</span><span class="sxs-lookup"><span data-stu-id="bd0a2-115">Flows by NSG and Rule</span></span>
* <span data-ttu-id="bd0a2-116">Flujos por puerto de destino</span><span class="sxs-lookup"><span data-stu-id="bd0a2-116">Flows by Destination Port</span></span>

<span data-ttu-id="bd0a2-117">plantilla de Hello proporcionada es editable para que pueda modificarlo tooadd nuevos datos, objetos visuales, o editar consultas toosuit sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-117">hello template provided is editable so you can modify it tooadd new data, visuals, or edit queries toosuit your needs.</span></span>

## <a name="setup"></a><span data-ttu-id="bd0a2-118">Configuración</span><span class="sxs-lookup"><span data-stu-id="bd0a2-118">Setup</span></span>

<span data-ttu-id="bd0a2-119">Antes de empezar, tiene que tener el registro de flujo de grupo de seguridad de red habilitado en uno o más grupos de seguridad de red de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="bd0a2-120">Para obtener instrucciones acerca de cómo habilitar la seguridad de red de flujo de registros, consulte el artículo siguiente de toohello: [registro tooflow de introducción para grupos de seguridad de red](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd0a2-120">For instructions on enabling Network Security flow logs, refer toohello following article: [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="bd0a2-121">También debe tener Hola Power BI Desktop instalado en su equipo y suficiente espacio libre en los máquina toodownload carga Hola datos del registro y que existe en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-121">You must also have hello Power BI Desktop client installed on your machine, and enough free space on your machine toodownload and load hello log data that exists in your storage account.</span></span>

![Diagrama de Visio][1]

### <a name="steps"></a><span data-ttu-id="bd0a2-123">Pasos</span><span class="sxs-lookup"><span data-stu-id="bd0a2-123">Steps</span></span>

1. <span data-ttu-id="bd0a2-124">Descarga y Hola abierto después de la plantilla de Power BI en Power BI Desktop aplicación Hola [plantilla de registros de flujo de PowerBI de Monitor de red](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span><span class="sxs-lookup"><span data-stu-id="bd0a2-124">Download and open hello following Power BI template in hello Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span></span>
1. <span data-ttu-id="bd0a2-125">Escriba los parámetros de consulta de hello necesario</span><span class="sxs-lookup"><span data-stu-id="bd0a2-125">Enter hello required Query parameters</span></span>
    1. <span data-ttu-id="bd0a2-126">**StorageAccountName** – toohello especifica el nombre de cuenta de almacenamiento de hello registros de flujo NSG Hola contenedor que desea tooload y visualizar.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-126">**StorageAccountName** – Specifies toohello name of hello storage account containing hello NSG flow logs that you would like tooload and visualize.</span></span>
    1. <span data-ttu-id="bd0a2-127">**NumberOfLogFiles** : especifica el número de Hola de archivos de registro que se desee toodownload y visualizar en Power BI.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-127">**NumberOfLogFiles** – Specifies hello number of log files that you would like toodownload and visualize in Power BI.</span></span> <span data-ttu-id="bd0a2-128">Por ejemplo, si se especifica 50, Hola 50 archivos de registro más recientes.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-128">For example, if 50 is specified, hello 50 latest log files.</span></span> <span data-ttu-id="bd0a2-129">FF tenemos 2 NSG habilitado y configurado toosend NSG flujo registros toothis cuenta y luego hello las últimas 25 horas de registros se pueden ver.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-129">Ff we have 2 NSGs enabled and configured toosend NSG flow logs toothis account, then hello past 25 hours of logs can be viewed.</span></span>

    ![Ventana principal de Power BI][2]

1. <span data-ttu-id="bd0a2-131">Escriba Hola clave de acceso para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-131">Enter hello Access Key for your storage account.</span></span> <span data-ttu-id="bd0a2-132">Puede encontrar las claves de acceso válido desplazándose tooyour cuenta de almacenamiento en hello Azure portal y seleccione **teclas de acceso** desde el menú de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-132">You can find valid access keys by navigating tooyour storage account in hello Azure portal and selecting **Access Keys** from hello Settings menu.</span></span> <span data-ttu-id="bd0a2-133">Haga clic en **Conectar** y aplique los cambios.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-133">Click **Connect** then apply changes.</span></span>

    ![Claves de acceso][3]

    ![Clave de acceso 2][4]

4.  <span data-ttu-id="bd0a2-136">Los registros están descargar y analizar y ahora pueden usar objetos visuales de hello creada previamente.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-136">Your logs are download and parsed and you can now utilize hello pre-created visuals.</span></span>

## <a name="understanding-hello-visuals"></a><span data-ttu-id="bd0a2-137">Descripción de los objetos visuales de Hola</span><span class="sxs-lookup"><span data-stu-id="bd0a2-137">Understanding hello visuals</span></span>

<span data-ttu-id="bd0a2-138">Proporcionado en hello plantilla son un conjunto de objetos visuales que le ayudan a tener sentido del programa Hola a los datos de registro de flujo de NSG.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-138">Provided in hello template are a set of visuals that help make sense of hello NSG Flow Log data.</span></span> <span data-ttu-id="bd0a2-139">Hello siguientes imágenes muestran un ejemplo de panel Hola aspecto cuando se rellena con datos.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-139">hello following images show a sample of what hello dashboard looks like when populated with data.</span></span> <span data-ttu-id="bd0a2-140">A continuación se examina con más detalle cada objeto visual</span><span class="sxs-lookup"><span data-stu-id="bd0a2-140">Below we examine each visual in greater detail</span></span> 

![Power BI][5]
 
<span data-ttu-id="bd0a2-142">Emisores de parte superior de Hello visual muestra Hola direcciones IP que se ha iniciado Hola mayoría de las conexiones a través de hello periodo especificado.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-142">hello Top Talkers visual shows hello IPs that have initiated hello most connections over hello period specified.</span></span> <span data-ttu-id="bd0a2-143">tamaño de Hola de cuadros de hello corresponde toohello relativa número de conexiones.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-143">hello size of hello boxes corresponds toohello relative number of connections.</span></span> 

![Toptalkers][6]

<span data-ttu-id="bd0a2-145">Hello gráficos de series de tiempo siguientes muestran el número de Hola de flujos en el período de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-145">hello following time series graphs show hello number of flows over hello period.</span></span> <span data-ttu-id="bd0a2-146">gráfico de Hello superior está segmentada por la dirección del flujo de Hola y Hola inferior se segmenta por decisión de hello realizada (permitir o denegar).</span><span class="sxs-lookup"><span data-stu-id="bd0a2-146">hello upper graph is segmented by hello flow direction, and hello lower is segmented by hello decision made (allow or deny).</span></span> <span data-ttu-id="bd0a2-147">Con este objeto visual, puede examinar las tendencias del tráfico a través del tiempo y detectar cualquier pico o disminución anómala la segmentación del tráfico.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span></span>

![flowsoverperiod][7]

<span data-ttu-id="bd0a2-149">Hello gráficos siguientes muestran Hola flujos interfaz de red, con hello superior segmentadas por la dirección del flujo y Hola inferior segmentadas por decisión realizada por.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-149">hello following graphs show hello flows per Network interface, with hello upper segmented by flow direction and hello lower segmented by decision made.</span></span> <span data-ttu-id="bd0a2-150">Con esta información, puede obtener información sobre cuáles de las máquinas virtuales que se comunicó Hola mayoría tooothers relativa, y si el tráfico tooa VM específica se está permitido o denegado.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-150">With this information, you can gain insights into which of your VMs communicated hello most relative tooothers, and if traffic tooa specific VM is being allowed or denied.</span></span>

![flowspernic][8]

<span data-ttu-id="bd0a2-152">Hola siguiendo el gráfico de anillos rueda muestra un desglose de los flujos por puerto de destino.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-152">hello following donut wheel chart shows a breakdown of Flows by Destination Port.</span></span> <span data-ttu-id="bd0a2-153">Con esta información, puede ver los puertos de destino de hello suelen usada utilizados en hello especificado período.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-153">With this information, you can view hello most commonly used destination ports used within hello specified period.</span></span>

![anillo][9]

<span data-ttu-id="bd0a2-155">Hello siguiente gráfico de barras muestra hello flujo NSG y reglas.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-155">hello following bar chart shows hello Flow by NSG and Rule.</span></span> <span data-ttu-id="bd0a2-156">Con esta información, puede ver hello NSG responsables de hello mayoría tráfico y desglose de Hola de tráfico en un NSG por regla.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-156">With this information, you can see hello NSGs responsible for hello most traffic, and hello breakdown of traffic on an NSG by rule.</span></span>

![gráfico de barras][10]
 
<span data-ttu-id="bd0a2-158">Hello siguientes gráficos informativos muestran información acerca de los NSG Hola presente en los registros de hello, Hola número de flujos capturados por período de Hola y fecha de Hola de registro más antiguo de hello capturado.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-158">hello following informational charts display information about hello NSGs present in hello logs, hello number of Flows captured over hello period, and hello date of hello earliest log captured.</span></span> <span data-ttu-id="bd0a2-159">Esta información ofrece una idea de qué NSG se registren y Hola intervalo de fechas de flujos.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-159">This information gives you an idea of what NSGs are being logged and hello date range of flows.</span></span>

![infochart1][11]

![infochart2][12]

<span data-ttu-id="bd0a2-162">Esta plantilla incluye Hola siguientes tooallow segmentaciones de datos solo datos de hello tooview está más interesado en.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-162">This template includes hello following slicers tooallow you tooview only hello data you are most interested in.</span></span> <span data-ttu-id="bd0a2-163">Puede filtrar por grupos de recursos, NSG y reglas.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-163">You can filter on your resource groups, NSGs, and rules.</span></span> <span data-ttu-id="bd0a2-164">También puede filtrar por información de la tupla de 5, la decisión y la hora de Hola Hola registro se escribe.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-164">You can also filter on 5-tuple information, decision, and hello time hello log was written.</span></span>

![segmentaciones][13]

## <a name="conclusion"></a><span data-ttu-id="bd0a2-166">Conclusión</span><span class="sxs-lookup"><span data-stu-id="bd0a2-166">Conclusion</span></span>

<span data-ttu-id="bd0a2-167">También hemos mostrado en este escenario que mediante el uso de registros de flujo de grupo de seguridad de red proporcionados por el Monitor de red y Power BI, estamos toovisualize capaz y comprender el tráfico Hola.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able toovisualize and understand hello traffic.</span></span> <span data-ttu-id="bd0a2-168">Mediante la plantilla de hello proporcionado, Power BI descarga registros de hello directamente desde el almacenamiento y las procesa localmente.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-168">Using hello provided template, Power BI downloads hello logs directly from storage and processes them locally.</span></span> <span data-ttu-id="bd0a2-169">Plantilla de tiempo que tarda tooload Hola varía en función número Hola de archivos solicitados y descarga de tamaño total de archivos.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-169">Time taken tooload hello template varies depending on hello number of files requested and total size of files downloaded.</span></span>

<span data-ttu-id="bd0a2-170">Sentirse toocustomize libre esta plantilla para sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-170">Feel free toocustomize this template for your needs.</span></span> <span data-ttu-id="bd0a2-171">Hay muchas formas en las que puede utilizar Power BI con los registros de flujo de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span></span> 

## <a name="notes"></a><span data-ttu-id="bd0a2-172">Notas</span><span class="sxs-lookup"><span data-stu-id="bd0a2-172">Notes</span></span>

* <span data-ttu-id="bd0a2-173">De forma predeterminada los registros se almacenan en `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span><span class="sxs-lookup"><span data-stu-id="bd0a2-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span></span>

    * <span data-ttu-id="bd0a2-174">Si hay otros datos en otro directorio Hola a toopull de las consultas y proceso Hola datos deben modificarse.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-174">If other data exists in another directory they hello queries toopull and process hello data must be modified.</span></span>

* <span data-ttu-id="bd0a2-175">plantilla de Hello proporcionada no se recomienda para su uso con más de 1 GB de registros.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-175">hello provided template is not recommended for use with more than 1 GB of logs.</span></span>

* <span data-ttu-id="bd0a2-176">Si tiene una gran cantidad de registros, recomendamos que investigue una solución utilizando otro almacén de datos como Data Lake o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bd0a2-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd0a2-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bd0a2-177">Next Steps</span></span>

<span data-ttu-id="bd0a2-178">Obtenga información acerca de cómo toovisualize su flujo NSG registra con hello Elastick pila visitando [visualizar tooand de patrones de tráfico de red de las máquinas virtuales mediante herramientas de código abierto](network-watcher-using-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="bd0a2-178">Learn how toovisualize your NSG flow logs with hello Elastick Stack by visiting [Visualize network traffic patterns tooand from your VMs using open source tools](network-watcher-using-open-source-tools.md)</span></span>

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
