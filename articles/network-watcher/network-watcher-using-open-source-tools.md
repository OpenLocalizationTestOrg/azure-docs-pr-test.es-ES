---
title: "Visualización de los patrones de tráfico de red con Azure Network Watcher y herramientas de código abierto | Microsoft Docs"
description: "Esta página describe cómo utilizar la captura de paquetes de Network Watcher con Capanalysis para visualizar los patrones de tráfico de entrada y salida de las máquinas virtuales."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: e27bb694d0cbcf1ff7c9d8ca4682a79c8b5c5cb1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-network-traffic-patterns-to-and-from-your-vms-using-open-source-tools"></a><span data-ttu-id="e4945-103">Visualización de los patrones de tráfico de red de entrada y salida de las máquinas virtuales utilizando herramientas de código abierto</span><span class="sxs-lookup"><span data-stu-id="e4945-103">Visualize network traffic patterns to and from your VMs using open source tools</span></span>

<span data-ttu-id="e4945-104">Las capturas de paquetes contienen datos de red que permiten realizar análisis forense de la red e inspección profunda de paquetes.</span><span class="sxs-lookup"><span data-stu-id="e4945-104">Packet captures contain network data that allow you to perform network forensics and deep packet inspection.</span></span> <span data-ttu-id="e4945-105">Hay muchas herramientas de código abierto que puede usar para analizar las capturas de paquetes y obtener información sobre la red.</span><span class="sxs-lookup"><span data-stu-id="e4945-105">There are many opens source tools you can use to analyze packet captures to gain insights about your network.</span></span> <span data-ttu-id="e4945-106">Una de estas herramientas es CapAnalysis, una herramienta de código abierto para la visualización de captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="e4945-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="e4945-107">La visualización de los datos de captura de paquetes es una forma muy eficaz de derivar rápidamente información sobre patrones y anomalías dentro de la red.</span><span class="sxs-lookup"><span data-stu-id="e4945-107">Visualizing packet capture data is a valuable way to quickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="e4945-108">Las visualizaciones también proporcionan un medio para compartir dicha información de una manera fácil de consumir.</span><span class="sxs-lookup"><span data-stu-id="e4945-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="e4945-109">Azure Network Watcher proporciona la capacidad para capturar estos valiosos datos permitiéndole realizar capturas de paquetes en su red.</span><span class="sxs-lookup"><span data-stu-id="e4945-109">Azure’s Network Watcher provides you the ability to capture this valuable data by allowing you to perform packet captures on your network.</span></span> <span data-ttu-id="e4945-110">En este artículo, proporcionamos un tutorial en el que se explica cómo visualizar y obtener información de las capturas de paquetes usando CapAnalysis con Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="e4945-110">In this article, we provide a walkthrough of how to visualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="e4945-111">Escenario</span><span class="sxs-lookup"><span data-stu-id="e4945-111">Scenario</span></span>

<span data-ttu-id="e4945-112">Tiene una aplicación web simple implementada en una máquina virtual en Azure y desea usar herramientas de código abierto para visualizar su tráfico de red para identificar rápidamente los patrones de flujo y las posibles anomalías.</span><span class="sxs-lookup"><span data-stu-id="e4945-112">You have a simple web application deployed on a VM in Azure want to use open source tools to visualize its network traffic to quickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="e4945-113">Con Network Watcher, puede obtener una captura de paquetes de su entorno de red y almacenarla directamente en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e4945-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="e4945-114">CapAnalysis puede a continuación ingerir la captura de paquetes directamente desde el blob de almacenamiento y visualizar su contenido.</span><span class="sxs-lookup"><span data-stu-id="e4945-114">CapAnalysis can then ingest the packet capture directly from the storage blob and visualize its contents.</span></span>

![escenario][1]

## <a name="steps"></a><span data-ttu-id="e4945-116">Pasos</span><span class="sxs-lookup"><span data-stu-id="e4945-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="e4945-117">Instalar CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="e4945-117">Install CapAnalysis</span></span>

<span data-ttu-id="e4945-118">Para instalar CapAnalysis en una máquina virtual, puede acudir a las instrucciones oficiales en esta página https://www.capanalysis.net/ca/how-to-install-capanalysis.</span><span class="sxs-lookup"><span data-stu-id="e4945-118">To install CapAnalysis on a virtual machine, you can refer to the official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="e4945-119">Para poder acceder de forma remota a CapAnalysis, es necesario abrir el puerto 9877 en la máquina virtual mediante la adición de una nueva regla de seguridad de entrada.</span><span class="sxs-lookup"><span data-stu-id="e4945-119">In order access CapAnalysis remotely, we need to open port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="e4945-120">Para más información sobre cómo crear reglas en los grupos de seguridad de red, consulte [Creación de reglas en un grupo de seguridad de red existente](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span><span class="sxs-lookup"><span data-stu-id="e4945-120">For more about creating rules in Network Security Groups, refer to [Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="e4945-121">Una vez que la regla se ha agregado correctamente, debe poder tener acceso a CapAnalysis desde `http://<PublicIP>:9877`</span><span class="sxs-lookup"><span data-stu-id="e4945-121">Once the rule has been successfully added, you should be able to access CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-to-start-a-packet-capture-session"></a><span data-ttu-id="e4945-122">Utilice Azure Network Watcher para iniciar una sesión de captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="e4945-122">Use Azure Network Watcher to start a packet capture session</span></span>

<span data-ttu-id="e4945-123">Network Watcher le permite capturar paquetes para realizar el seguimiento del tráfico dentro y fuera de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e4945-123">Network Watcher allows you to capture packets to track traffic in and out of a virtual machine.</span></span> <span data-ttu-id="e4945-124">Puede acudir a las instrucciones en [Administración de capturas de paquetes con Network Watcher](network-watcher-packet-capture-manage-portal.md) para iniciar una sesión de captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="e4945-124">You can refer to the instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) to start a packet capture session.</span></span> <span data-ttu-id="e4945-125">Esta captura de paquetes se puede almacenar en un blob de almacenamiento para que CapAnalysis pueda acceder a ella.</span><span class="sxs-lookup"><span data-stu-id="e4945-125">This packet capture can be stored in a storage blob to be accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-to-capanalysis"></a><span data-ttu-id="e4945-126">Carga de una captura de paquetes en CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="e4945-126">Upload a packet capture to CapAnalysis</span></span>
<span data-ttu-id="e4945-127">Puede cargar directamente una captura de paquetes realizada por Network Watcher usando la pestaña "Importar desde dirección URL" y proporcionando un vínculo al blob de almacenamiento donde está almacenada la captura de paquete.</span><span class="sxs-lookup"><span data-stu-id="e4945-127">You can directly upload a packet capture taken by network watcher using the “Import from URL” tab and providing a link to the storage blob where the packet capture is stored.</span></span>

<span data-ttu-id="e4945-128">Cuando proporciona un vínculo a CapAnalysis, asegúrese de anexar un token de SAS a la dirección URL del blob de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e4945-128">When providing a link to CapAnalysis, make sure to append a SAS token to the storage blob URL.</span></span>  <span data-ttu-id="e4945-129">Para ello, vaya a la firma de acceso compartido de la cuenta de almacenamiento, designe los permisos concedidos y presione el botón Generar SAS para crear un token.</span><span class="sxs-lookup"><span data-stu-id="e4945-129">To do this, navigate to Shared access signature from the storage account, designate the allowed permissions, and press the Generate SAS button to create a token.</span></span> <span data-ttu-id="e4945-130">A continuación, puede anexar este token de SAS a la URL del blob de almacenamiento de captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="e4945-130">You can then append this SAS token to the packet capture storage blob URL.</span></span>

<span data-ttu-id="e4945-131">La dirección URL resultante tendrá un aspecto similar al siguiente: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="e4945-131">The resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="e4945-132">Análisis de captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="e4945-132">Analyzing packet captures</span></span>

<span data-ttu-id="e4945-133">CapAnalysis ofrece varias opciones para visualizar la captura de paquetes, cada una proporciona un análisis desde una perspectiva distinta.</span><span class="sxs-lookup"><span data-stu-id="e4945-133">CapAnalysis offers various options to visualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="e4945-134">Con estos resúmenes visuales, podrá entender las tendencias del tráfico de la red y detectar rápidamente cualquier actividad inusual.</span><span class="sxs-lookup"><span data-stu-id="e4945-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="e4945-135">Algunas de estas características se muestran en la lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="e4945-135">A few of these features are shown in the following list:</span></span>

1. <span data-ttu-id="e4945-136">Tablas de flujo</span><span class="sxs-lookup"><span data-stu-id="e4945-136">Flow Tables</span></span>

    <span data-ttu-id="e4945-137">Esta tabla proporciona la lista de flujos en los datos del paquete, la marca de tiempo asociada a los flujos y los diversos protocolos asociados con el flujo, así como la IP de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="e4945-137">This table gives you the list of flows in the packet data, the time stamp associated with the flows and the various protocols associated with the flow, as well as source and destination IP.</span></span>

    ![Página de flujo de Capanalysis][5]

1. <span data-ttu-id="e4945-139">Información general sobre protocolos</span><span class="sxs-lookup"><span data-stu-id="e4945-139">Protocol Overview</span></span>

    <span data-ttu-id="e4945-140">Este panel le permite ver rápidamente la distribución del tráfico de red a través de los distintos protocolos y regiones geográficas.</span><span class="sxs-lookup"><span data-stu-id="e4945-140">This pane allows you to quickly see the distribution of network traffic over the various protocols and geographies.</span></span>

    ![Información general sobre protocolos de Capanalysis][6]

1. <span data-ttu-id="e4945-142">Estadísticas</span><span class="sxs-lookup"><span data-stu-id="e4945-142">Statistics</span></span>

    <span data-ttu-id="e4945-143">Este panel permite ver las estadísticas de tráfico de red: bytes enviados y recibidos desde las IP de origen y destino, flujos de cada una de las IP de origen y destino, protocolo usado para distintos flujos y duración de los flujos.</span><span class="sxs-lookup"><span data-stu-id="e4945-143">This pane allows you to view network traffic statistics – bytes sent and received from source and destination IPs, flows for each of the source and destination IPs, protocol used for various flows, and the duration of flows.</span></span>

    ![Estadísticas de Capanalysis][7]

1. <span data-ttu-id="e4945-145">Geomap</span><span class="sxs-lookup"><span data-stu-id="e4945-145">Geomap</span></span>

    <span data-ttu-id="e4945-146">Este panel proporciona una vista del mapa del tráfico de red, con colores de ajuste de escala para el volumen de tráfico de cada país.</span><span class="sxs-lookup"><span data-stu-id="e4945-146">This pane provides you with a map view of your network traffic, with colors scaling to the volume of traffic from each country.</span></span> <span data-ttu-id="e4945-147">Puede seleccionar países resaltados para ver las estadísticas de flujo adicionales, como la proporción de datos enviados y recibidos desde direcciones IP en ese país.</span><span class="sxs-lookup"><span data-stu-id="e4945-147">You can select highlighted countries to view additional flow statistics such as the proportion of data sent and received from IPs in that country.</span></span>

    ![Geomap][8]

1. <span data-ttu-id="e4945-149">Filtros</span><span class="sxs-lookup"><span data-stu-id="e4945-149">Filters</span></span>

    <span data-ttu-id="e4945-150">CapAnalysis proporciona un conjunto de filtros para el análisis rápido de paquetes específicos.</span><span class="sxs-lookup"><span data-stu-id="e4945-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="e4945-151">Por ejemplo, puede filtrar los datos por protocolo para obtener información específica en ese subconjunto de tráfico.</span><span class="sxs-lookup"><span data-stu-id="e4945-151">For example, you can choose to filter the data by protocol to gain specific insights on that subset of traffic.</span></span>

    ![filters][11]

    <span data-ttu-id="e4945-153">Visite [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) para más información sobre todas las funcionalidades de CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="e4945-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) to learn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="e4945-154">Conclusión</span><span class="sxs-lookup"><span data-stu-id="e4945-154">Conclusion</span></span>

<span data-ttu-id="e4945-155">La característica de captura de paquetes de Network Watcher permite capturar los datos necesarios para realizar un análisis forense de red y comprender mejor el tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="e4945-155">Network Watcher’s packet capture feature allows you to capture the data necessary to perform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="e4945-156">En este escenario, hemos mostrado cómo las capturas de paquetes de Network Watcher se pueden integrar fácilmente con herramientas de visualización de código abierto.</span><span class="sxs-lookup"><span data-stu-id="e4945-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="e4945-157">Mediante el uso de herramientas de código abierto como CapAnalysis para visualizar las capturas de paquetes, puede realizar una inspección profunda de los paquetes e identificar rápidamente las tendencias en el tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="e4945-157">By using open source tools such as CapAnalysis to visualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4945-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e4945-158">Next steps</span></span>

<span data-ttu-id="e4945-159">Para más información acerca de los registros de flujo de NSG, visite el artículo sobre [Registros de flujo de NSG](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e4945-159">To learn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="e4945-160">Aprenda a visualizar los registros de flujo de grupos de seguridad de red con Power BI en el artículo [Visualización de registros de flujo del grupo de seguridad de red de Azure con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="e4945-160">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
