---
title: "Visualización de registros de flujo del grupo de seguridad de red de Azure con Power BI | Microsoft Docs"
description: "En esta página se describe cómo utilizar Power BI para visualizar los registros de flujo del grupo de seguridad de red (NSG)."
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
ms.openlocfilehash: d8c61ca2a3bd5affe02e8f9500655db6699a245f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a><span data-ttu-id="52c19-103">Visualización de registros de flujo del grupo de seguridad de red con Power BI</span><span class="sxs-lookup"><span data-stu-id="52c19-103">Visualizing Network Security Group flow logs with Power BI</span></span>

<span data-ttu-id="52c19-104">Los registros de flujo del grupo de seguridad de red le permiten visualizar información sobre el tráfico IP de entrada y salida en los grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="52c19-104">Network Security Group flow logs allow you to view information about ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="52c19-105">Estos registros de flujo muestran los flujos de entrada y salida en función de cada regla, la NIC a la que se aplica el flujo, información de 5-tupla sobre el flujo (IP de origen y de destino, puerto de origen y de destino, protocolo), y si se permitió o denegó el tráfico.</span><span class="sxs-lookup"><span data-stu-id="52c19-105">These flow logs show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="52c19-106">Puede ser difícil obtener información sobre los datos de registro de flujo mediante la búsqueda manual de los archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="52c19-106">It can be difficult to gain insights into flow logging data by manually searching the log files.</span></span> <span data-ttu-id="52c19-107">En este artículo se proporcionan una solución para visualizar los registros de flujo más recientes y obtener información sobre el tráfico en la red.</span><span class="sxs-lookup"><span data-stu-id="52c19-107">In this article, we provide a solution to visualize your most recent flow logs and learn about traffic on your network.</span></span>

## <a name="scenario"></a><span data-ttu-id="52c19-108">Escenario</span><span class="sxs-lookup"><span data-stu-id="52c19-108">Scenario</span></span>

<span data-ttu-id="52c19-109">En el siguiente escenario, conectamos Power BI Desktop a la cuenta de almacenamiento que hemos configurado como el receptor de los datos del registro de flujo de NSG.</span><span class="sxs-lookup"><span data-stu-id="52c19-109">In the following scenario, we connect Power BI desktop to the storage account we have configured as the sink for our NSG Flow Logging data.</span></span> <span data-ttu-id="52c19-110">Una vez que se conecta a la cuenta de almacenamiento, Power BI descarga y analiza los registros para proporcionar una representación visual del tráfico que registran los grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="52c19-110">After we connect to our storage account, Power BI downloads and parses the logs to provide a visual representation of the traffic that is logged by Network Security groups.</span></span>

<span data-ttu-id="52c19-111">Utilizando los objetos visuales proporcionados en la plantilla puede examinar:</span><span class="sxs-lookup"><span data-stu-id="52c19-111">Using the visuals supplied in the template you can examine:</span></span>

* <span data-ttu-id="52c19-112">Top Talkers</span><span class="sxs-lookup"><span data-stu-id="52c19-112">Top Talkers</span></span>
* <span data-ttu-id="52c19-113">Datos de flujo de serie temporal por decisión de regla y dirección</span><span class="sxs-lookup"><span data-stu-id="52c19-113">Time Series Flow Data by direction and rule decision</span></span>
* <span data-ttu-id="52c19-114">Flujos por dirección MAC de la interfaz de red</span><span class="sxs-lookup"><span data-stu-id="52c19-114">Flows by Network Interface MAC address</span></span>
* <span data-ttu-id="52c19-115">Flujos por NSG y regla</span><span class="sxs-lookup"><span data-stu-id="52c19-115">Flows by NSG and Rule</span></span>
* <span data-ttu-id="52c19-116">Flujos por puerto de destino</span><span class="sxs-lookup"><span data-stu-id="52c19-116">Flows by Destination Port</span></span>

<span data-ttu-id="52c19-117">La plantilla que se proporciona es editable, por lo que puede modificarla agregando nuevos datos u objetos visuales, o modificando consultas para adaptarla a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="52c19-117">The template provided is editable so you can modify it to add new data, visuals, or edit queries to suit your needs.</span></span>

## <a name="setup"></a><span data-ttu-id="52c19-118">Configuración</span><span class="sxs-lookup"><span data-stu-id="52c19-118">Setup</span></span>

<span data-ttu-id="52c19-119">Antes de empezar, tiene que tener el registro de flujo de grupo de seguridad de red habilitado en uno o más grupos de seguridad de red de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="52c19-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="52c19-120">Para ver instrucciones para habilitar los registros de flujo de grupo de seguridad de red, consulte el artículo siguiente: [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md) (Introducción al registro de flujo para grupos de seguridad de red).</span><span class="sxs-lookup"><span data-stu-id="52c19-120">For instructions on enabling Network Security flow logs, refer to the following article: [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="52c19-121">También tiene que tener el cliente de Power BI Desktop instalado en su equipo y suficiente espacio disponible en el mismo para descargar y cargar los datos del registro que existen en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="52c19-121">You must also have the Power BI Desktop client installed on your machine, and enough free space on your machine to download and load the log data that exists in your storage account.</span></span>

![Diagrama de Visio][1]

### <a name="steps"></a><span data-ttu-id="52c19-123">Pasos</span><span class="sxs-lookup"><span data-stu-id="52c19-123">Steps</span></span>

1. <span data-ttu-id="52c19-124">Descargue y abra la siguiente plantilla de Power BI en la aplicación de Power BI Desktop [plantilla de registros de flujo de Power BI de Network Watcher](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span><span class="sxs-lookup"><span data-stu-id="52c19-124">Download and open the following Power BI template in the Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span></span>
1. <span data-ttu-id="52c19-125">Escriba los parámetros de consulta necesarios</span><span class="sxs-lookup"><span data-stu-id="52c19-125">Enter the required Query parameters</span></span>
    1. <span data-ttu-id="52c19-126">**StorageAccountName**: especifica el nombre de la cuenta de almacenamiento que contiene los registros de flujo de NSG que desea cargar y visualizar.</span><span class="sxs-lookup"><span data-stu-id="52c19-126">**StorageAccountName** – Specifies to the name of the storage account containing the NSG flow logs that you would like to load and visualize.</span></span>
    1. <span data-ttu-id="52c19-127">**NumberOfLogFiles**: especifica el número de archivos de registro que desear descargar y visualizar en Power BI.</span><span class="sxs-lookup"><span data-stu-id="52c19-127">**NumberOfLogFiles** – Specifies the number of log files that you would like to download and visualize in Power BI.</span></span> <span data-ttu-id="52c19-128">Por ejemplo, si se especifica 50, los 50 archivos de registro más recientes.</span><span class="sxs-lookup"><span data-stu-id="52c19-128">For example, if 50 is specified, the 50 latest log files.</span></span> <span data-ttu-id="52c19-129">Si tenemos 2 NSG habilitados y configurados para enviar registros de flujo de NSG a esta cuenta, se podrán ver las últimas 25 horas de registros.</span><span class="sxs-lookup"><span data-stu-id="52c19-129">Ff we have 2 NSGs enabled and configured to send NSG flow logs to this account, then the past 25 hours of logs can be viewed.</span></span>

    ![Ventana principal de Power BI][2]

1. <span data-ttu-id="52c19-131">Escriba la clave de acceso para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="52c19-131">Enter the Access Key for your storage account.</span></span> <span data-ttu-id="52c19-132">Puede encontrar claves de acceso válidas navegando a la cuenta de almacenamiento en Azure Portal y seleccionando **Claves de acceso** en el menú de configuración.</span><span class="sxs-lookup"><span data-stu-id="52c19-132">You can find valid access keys by navigating to your storage account in the Azure portal and selecting **Access Keys** from the Settings menu.</span></span> <span data-ttu-id="52c19-133">Haga clic en **Conectar** y aplique los cambios.</span><span class="sxs-lookup"><span data-stu-id="52c19-133">Click **Connect** then apply changes.</span></span>

    ![Claves de acceso][3]

    ![Clave de acceso 2][4]

4.  <span data-ttu-id="52c19-136">Los registros se descargan y analizan, y ahora ya puede usar los objetos visuales creados previamente.</span><span class="sxs-lookup"><span data-stu-id="52c19-136">Your logs are download and parsed and you can now utilize the pre-created visuals.</span></span>

## <a name="understanding-the-visuals"></a><span data-ttu-id="52c19-137">Descripción de los objetos visuales</span><span class="sxs-lookup"><span data-stu-id="52c19-137">Understanding the visuals</span></span>

<span data-ttu-id="52c19-138">En la plantilla se proporcionan un conjunto de objetos visuales que lo ayudan a comprender los datos del registro de flujo de NSG.</span><span class="sxs-lookup"><span data-stu-id="52c19-138">Provided in the template are a set of visuals that help make sense of the NSG Flow Log data.</span></span> <span data-ttu-id="52c19-139">Las siguientes imágenes muestran un ejemplo del aspecto del panel cuando se rellena con datos.</span><span class="sxs-lookup"><span data-stu-id="52c19-139">The following images show a sample of what the dashboard looks like when populated with data.</span></span> <span data-ttu-id="52c19-140">A continuación se examina con más detalle cada objeto visual</span><span class="sxs-lookup"><span data-stu-id="52c19-140">Below we examine each visual in greater detail</span></span> 

![Power BI][5]
 
<span data-ttu-id="52c19-142">El objeto visual Top Talkers muestra las direcciones IP que han iniciado la mayoría de las conexiones durante el período especificado.</span><span class="sxs-lookup"><span data-stu-id="52c19-142">The Top Talkers visual shows the IPs that have initiated the most connections over the period specified.</span></span> <span data-ttu-id="52c19-143">El tamaño de los cuadros corresponde al número relativo de conexiones.</span><span class="sxs-lookup"><span data-stu-id="52c19-143">The size of the boxes corresponds to the relative number of connections.</span></span> 

![Toptalkers][6]

<span data-ttu-id="52c19-145">Los siguientes gráficos de series temporales muestran el número de flujos en el período.</span><span class="sxs-lookup"><span data-stu-id="52c19-145">The following time series graphs show the number of flows over the period.</span></span> <span data-ttu-id="52c19-146">El gráfico superior está segmentado por la dirección del flujo y el inferior está segmentado por la decisión MADD (permitir o denegar).</span><span class="sxs-lookup"><span data-stu-id="52c19-146">The upper graph is segmented by the flow direction, and the lower is segmented by the decision made (allow or deny).</span></span> <span data-ttu-id="52c19-147">Con este objeto visual, puede examinar las tendencias del tráfico a través del tiempo y detectar cualquier pico o disminución anómala la segmentación del tráfico.</span><span class="sxs-lookup"><span data-stu-id="52c19-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span></span>

![flowsoverperiod][7]

<span data-ttu-id="52c19-149">Los gráficos siguientes muestran los flujos por interfaz de red, con el superior segmentado por dirección del flujo y el inferior segmentado por decisión realizada.</span><span class="sxs-lookup"><span data-stu-id="52c19-149">The following graphs show the flows per Network interface, with the upper segmented by flow direction and the lower segmented by decision made.</span></span> <span data-ttu-id="52c19-150">Con esta información, puede obtener detalles sobre cuáles máquinas virtuales se comunican más en relación con otras, y si el tráfico a una máquina virtual se está permitiendo o denegando.</span><span class="sxs-lookup"><span data-stu-id="52c19-150">With this information, you can gain insights into which of your VMs communicated the most relative to others, and if traffic to a specific VM is being allowed or denied.</span></span>

![flowspernic][8]

<span data-ttu-id="52c19-152">El siguiente gráfico de anillo muestra un desglose de los flujos por puerto de destino.</span><span class="sxs-lookup"><span data-stu-id="52c19-152">The following donut wheel chart shows a breakdown of Flows by Destination Port.</span></span> <span data-ttu-id="52c19-153">Con esta información, puede ver los puertos de destino más utilizados dentro del período especificado.</span><span class="sxs-lookup"><span data-stu-id="52c19-153">With this information, you can view the most commonly used destination ports used within the specified period.</span></span>

![anillo][9]

<span data-ttu-id="52c19-155">El siguiente gráfico de barras muestra el flujo por NSG y regla.</span><span class="sxs-lookup"><span data-stu-id="52c19-155">The following bar chart shows the Flow by NSG and Rule.</span></span> <span data-ttu-id="52c19-156">Con esta información, puede ver los NSG responsables de la mayor parte del tráfico y el desglose del tráfico en un NSG por regla.</span><span class="sxs-lookup"><span data-stu-id="52c19-156">With this information, you can see the NSGs responsible for the most traffic, and the breakdown of traffic on an NSG by rule.</span></span>

![gráfico de barras][10]
 
<span data-ttu-id="52c19-158">Los siguientes gráficos informativos muestran información sobre los NSG presentes en los registros, el número de flujos capturados durante el período y la fecha del registro más antiguo capturado.</span><span class="sxs-lookup"><span data-stu-id="52c19-158">The following informational charts display information about the NSGs present in the logs, the number of Flows captured over the period, and the date of the earliest log captured.</span></span> <span data-ttu-id="52c19-159">Esta información le ofrece una idea de cuáles NSG se están registrando y el intervalo de fechas de los flujos.</span><span class="sxs-lookup"><span data-stu-id="52c19-159">This information gives you an idea of what NSGs are being logged and the date range of flows.</span></span>

![infochart1][11]

![infochart2][12]

<span data-ttu-id="52c19-162">Esta plantilla incluye las segmentaciones siguientes para que pueda ver solo los datos en los que está más interesado.</span><span class="sxs-lookup"><span data-stu-id="52c19-162">This template includes the following slicers to allow you to view only the data you are most interested in.</span></span> <span data-ttu-id="52c19-163">Puede filtrar por grupos de recursos, NSG y reglas.</span><span class="sxs-lookup"><span data-stu-id="52c19-163">You can filter on your resource groups, NSGs, and rules.</span></span> <span data-ttu-id="52c19-164">También puede filtrar por información de 5-tupla, decisión y la hora cuando se escribió el registro.</span><span class="sxs-lookup"><span data-stu-id="52c19-164">You can also filter on 5-tuple information, decision, and the time the log was written.</span></span>

![segmentaciones][13]

## <a name="conclusion"></a><span data-ttu-id="52c19-166">Conclusión</span><span class="sxs-lookup"><span data-stu-id="52c19-166">Conclusion</span></span>

<span data-ttu-id="52c19-167">Hemos mostrado en este escenario que utilizando los registros de flujo de grupo de seguridad de red proporcionados por Network Watcher y Power BI, se puede visualizar y comprender el tráfico.</span><span class="sxs-lookup"><span data-stu-id="52c19-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able to visualize and understand the traffic.</span></span> <span data-ttu-id="52c19-168">Utilizando la plantilla proporcionada, Power BI descarga los registros directamente desde el almacenamiento y los procesa localmente.</span><span class="sxs-lookup"><span data-stu-id="52c19-168">Using the provided template, Power BI downloads the logs directly from storage and processes them locally.</span></span> <span data-ttu-id="52c19-169">El tiempo necesario para cargar la plantilla varía dependiendo del número de archivos solicitados y del tamaño total de los archivos descargados.</span><span class="sxs-lookup"><span data-stu-id="52c19-169">Time taken to load the template varies depending on the number of files requested and total size of files downloaded.</span></span>

<span data-ttu-id="52c19-170">Puede personalizar esta plantilla para que se adapte a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="52c19-170">Feel free to customize this template for your needs.</span></span> <span data-ttu-id="52c19-171">Hay muchas formas en las que puede utilizar Power BI con los registros de flujo de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="52c19-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span></span> 

## <a name="notes"></a><span data-ttu-id="52c19-172">Notas</span><span class="sxs-lookup"><span data-stu-id="52c19-172">Notes</span></span>

* <span data-ttu-id="52c19-173">De forma predeterminada los registros se almacenan en `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span><span class="sxs-lookup"><span data-stu-id="52c19-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span></span>

    * <span data-ttu-id="52c19-174">Si hay otros datos en otro directorio, las consultas para la extracción y procesamiento de los datos tienen que modificarse.</span><span class="sxs-lookup"><span data-stu-id="52c19-174">If other data exists in another directory they the queries to pull and process the data must be modified.</span></span>

* <span data-ttu-id="52c19-175">La plantilla proporcionada no se recomienda para su uso con más de 1 GB de registros.</span><span class="sxs-lookup"><span data-stu-id="52c19-175">The provided template is not recommended for use with more than 1 GB of logs.</span></span>

* <span data-ttu-id="52c19-176">Si tiene una gran cantidad de registros, recomendamos que investigue una solución utilizando otro almacén de datos como Data Lake o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="52c19-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52c19-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="52c19-177">Next Steps</span></span>

<span data-ttu-id="52c19-178">Aprenda a visualizar los registros de flujo de NSG con la pila Elastick visitando [Visualización de los patrones de tráfico de red de entrada y salida de las máquinas virtuales utilizando herramientas de código abierto](network-watcher-using-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="52c19-178">Learn how to visualize your NSG flow logs with the Elastick Stack by visiting [Visualize network traffic patterns to and from your VMs using open source tools](network-watcher-using-open-source-tools.md)</span></span>

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
