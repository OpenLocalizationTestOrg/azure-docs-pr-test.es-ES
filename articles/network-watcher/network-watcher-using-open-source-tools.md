---
title: "aaaVisualize patrones de tráfico de red con Monitor de red de Azure y herramientas de código abierto | Documentos de Microsoft"
description: "Esta página describe el modo de captura de paquetes de Monitor de red de toouse con patrones de tráfico de Capanalysis toovisualize tooand de las máquinas virtuales."
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
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a><span data-ttu-id="f659a-103">Visualizar tooand de patrones de tráfico de red de las máquinas virtuales mediante herramientas de código abierto</span><span class="sxs-lookup"><span data-stu-id="f659a-103">Visualize network traffic patterns tooand from your VMs using open source tools</span></span>

<span data-ttu-id="f659a-104">Capturas de paquetes contienen datos de red que le permiten tooperform forenses de red y la inspección profunda de paquetes.</span><span class="sxs-lookup"><span data-stu-id="f659a-104">Packet captures contain network data that allow you tooperform network forensics and deep packet inspection.</span></span> <span data-ttu-id="f659a-105">Hay muchas abre herramientas de origen que puede usar tooanalyze paquete capturas toogain información acerca de la red.</span><span class="sxs-lookup"><span data-stu-id="f659a-105">There are many opens source tools you can use tooanalyze packet captures toogain insights about your network.</span></span> <span data-ttu-id="f659a-106">Una de estas herramientas es CapAnalysis, una herramienta de código abierto para la visualización de captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="f659a-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="f659a-107">Visualización de los datos de captura de paquetes es una forma muy eficaz tooquickly derivar nuevas perspectivas sobre patrones y las anomalías de la red.</span><span class="sxs-lookup"><span data-stu-id="f659a-107">Visualizing packet capture data is a valuable way tooquickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="f659a-108">Las visualizaciones también proporcionan un medio para compartir dicha información de una manera fácil de consumir.</span><span class="sxs-lookup"><span data-stu-id="f659a-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="f659a-109">Monitor de red de Azure proporciona que Hola toocapture capacidad captura estos valiosos datos permitiéndole tooperform paquetes en la red.</span><span class="sxs-lookup"><span data-stu-id="f659a-109">Azure’s Network Watcher provides you hello ability toocapture this valuable data by allowing you tooperform packet captures on your network.</span></span> <span data-ttu-id="f659a-110">En este artículo, se proporciona un tutorial sobre cómo visión toovisualize y mejora del paquete de captura usando CapAnalysis con Monitor de red.</span><span class="sxs-lookup"><span data-stu-id="f659a-110">In this article, we provide a walkthrough of how toovisualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="f659a-111">Escenario</span><span class="sxs-lookup"><span data-stu-id="f659a-111">Scenario</span></span>

<span data-ttu-id="f659a-112">Tiene una aplicación web simple que se implementa en una máquina virtual en Azure desea toouse de código abierto herramientas toovisualize su tooquickly de tráfico de red identificar patrones de flujo y las posibles anomalías.</span><span class="sxs-lookup"><span data-stu-id="f659a-112">You have a simple web application deployed on a VM in Azure want toouse open source tools toovisualize its network traffic tooquickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="f659a-113">Con Network Watcher, puede obtener una captura de paquetes de su entorno de red y almacenarla directamente en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f659a-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="f659a-114">CapAnalysis, a continuación, puede introducir captura directamente de hello paquetes desde blob de almacenamiento de Hola y ver su contenido.</span><span class="sxs-lookup"><span data-stu-id="f659a-114">CapAnalysis can then ingest hello packet capture directly from hello storage blob and visualize its contents.</span></span>

![escenario][1]

## <a name="steps"></a><span data-ttu-id="f659a-116">Pasos</span><span class="sxs-lookup"><span data-stu-id="f659a-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="f659a-117">Instalar CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="f659a-117">Install CapAnalysis</span></span>

<span data-ttu-id="f659a-118">tooinstall CapAnalysis en una máquina virtual, puede hacer referencia instrucciones oficial toohello https://www.capanalysis.net/ca/how-to-install-capanalysis aquí.</span><span class="sxs-lookup"><span data-stu-id="f659a-118">tooinstall CapAnalysis on a virtual machine, you can refer toohello official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="f659a-119">En el orden de acceso remoto CapAnalysis, necesitamos tooopen puerto 9877 en su máquina virtual mediante la adición de una nueva regla de seguridad de entrada.</span><span class="sxs-lookup"><span data-stu-id="f659a-119">In order access CapAnalysis remotely, we need tooopen port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="f659a-120">Para obtener más información sobre cómo crear reglas en grupos de seguridad de red, consulte demasiado[crear reglas en un NSG existente](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span><span class="sxs-lookup"><span data-stu-id="f659a-120">For more about creating rules in Network Security Groups, refer too[Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="f659a-121">Una vez que se ha agregado correctamente la regla de hello, debe ser capaz de tooaccess CapAnalysis de`http://<PublicIP>:9877`</span><span class="sxs-lookup"><span data-stu-id="f659a-121">Once hello rule has been successfully added, you should be able tooaccess CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a><span data-ttu-id="f659a-122">Usar toostart de Monitor de red de Azure un paquete de capturar sesión</span><span class="sxs-lookup"><span data-stu-id="f659a-122">Use Azure Network Watcher toostart a packet capture session</span></span>

<span data-ttu-id="f659a-123">Monitor de red permite el tráfico de tootrack de paquetes de toocapture dentro y fuera de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f659a-123">Network Watcher allows you toocapture packets tootrack traffic in and out of a virtual machine.</span></span> <span data-ttu-id="f659a-124">Puede hacer referencia a las instrucciones de toohello en [captura de paquetes de administrar con Monitor de red](network-watcher-packet-capture-manage-portal.md) toostart una sesión de captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="f659a-124">You can refer toohello instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) toostart a packet capture session.</span></span> <span data-ttu-id="f659a-125">Esta captura de paquetes se puede almacenar en un toobe de blob de almacenamiento acceso CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="f659a-125">This packet capture can be stored in a storage blob toobe accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-toocapanalysis"></a><span data-ttu-id="f659a-126">Cargar un tooCapAnalysis de captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="f659a-126">Upload a packet capture tooCapAnalysis</span></span>
<span data-ttu-id="f659a-127">Puede cargar directamente una captura de paquetes realizada por el Monitor de red utilizando la pestaña de "Import from URL" hello y proporcionando un blob de almacenamiento de vínculo toohello donde se almacena la captura de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="f659a-127">You can directly upload a packet capture taken by network watcher using hello “Import from URL” tab and providing a link toohello storage blob where hello packet capture is stored.</span></span>

<span data-ttu-id="f659a-128">Cuando se proporciona un vínculo tooCapAnalysis, asegúrese de tooappend seguro de una dirección URL de SAS toohello token almacenamiento blob.</span><span class="sxs-lookup"><span data-stu-id="f659a-128">When providing a link tooCapAnalysis, make sure tooappend a SAS token toohello storage blob URL.</span></span>  <span data-ttu-id="f659a-129">toodo, vaya tooShared firma de acceso de cuenta de almacenamiento de hello, designar Hola permisos permitido y presione Hola generar SAS botón toocreate un token.</span><span class="sxs-lookup"><span data-stu-id="f659a-129">toodo this, navigate tooShared access signature from hello storage account, designate hello allowed permissions, and press hello Generate SAS button toocreate a token.</span></span> <span data-ttu-id="f659a-130">A continuación, puede anexar esta dirección URL de SAS toohello token paquete captura almacenamiento blob.</span><span class="sxs-lookup"><span data-stu-id="f659a-130">You can then append this SAS token toohello packet capture storage blob URL.</span></span>

<span data-ttu-id="f659a-131">Hello URL resultante tendrá un aspecto similar al siguiente: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="f659a-131">hello resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="f659a-132">Análisis de captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="f659a-132">Analyzing packet captures</span></span>

<span data-ttu-id="f659a-133">CapAnalysis ofrece varios toovisualize de opciones de la captura de paquete, cada análisis proporcionando desde una perspectiva distinta.</span><span class="sxs-lookup"><span data-stu-id="f659a-133">CapAnalysis offers various options toovisualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="f659a-134">Con estos resúmenes visuales, podrá entender las tendencias del tráfico de la red y detectar rápidamente cualquier actividad inusual.</span><span class="sxs-lookup"><span data-stu-id="f659a-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="f659a-135">Hola lista siguiente muestra algunas de estas características:</span><span class="sxs-lookup"><span data-stu-id="f659a-135">A few of these features are shown in hello following list:</span></span>

1. <span data-ttu-id="f659a-136">Tablas de flujo</span><span class="sxs-lookup"><span data-stu-id="f659a-136">Flow Tables</span></span>

    <span data-ttu-id="f659a-137">Esto deja de tabla Hola lista de flujos de datos de paquetes de saludo, Hola marca de tiempo asociada a los flujos de Hola y Hola diversos protocolos asociados con el flujo de hello, así como IP de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="f659a-137">This table gives you hello list of flows in hello packet data, hello time stamp associated with hello flows and hello various protocols associated with hello flow, as well as source and destination IP.</span></span>

    ![Página de flujo de Capanalysis][5]

1. <span data-ttu-id="f659a-139">Información general sobre protocolos</span><span class="sxs-lookup"><span data-stu-id="f659a-139">Protocol Overview</span></span>

    <span data-ttu-id="f659a-140">Este panel le permite tooquickly ver la distribución de Hola de tráfico de red a lo largo Hola distintos protocolos y regiones geográficas.</span><span class="sxs-lookup"><span data-stu-id="f659a-140">This pane allows you tooquickly see hello distribution of network traffic over hello various protocols and geographies.</span></span>

    ![Información general sobre protocolos de Capanalysis][6]

1. <span data-ttu-id="f659a-142">Estadísticas</span><span class="sxs-lookup"><span data-stu-id="f659a-142">Statistics</span></span>

    <span data-ttu-id="f659a-143">Este panel permite que las estadísticas de tráfico de red tooview: bytes enviados y recibidos de origen y destino IP, flujos para cada origen de Hola y de destino de direcciones IP, protocolo usado para varios flujos y la duración de Hola de flujos.</span><span class="sxs-lookup"><span data-stu-id="f659a-143">This pane allows you tooview network traffic statistics – bytes sent and received from source and destination IPs, flows for each of hello source and destination IPs, protocol used for various flows, and hello duration of flows.</span></span>

    ![Estadísticas de Capanalysis][7]

1. <span data-ttu-id="f659a-145">Geomap</span><span class="sxs-lookup"><span data-stu-id="f659a-145">Geomap</span></span>

    <span data-ttu-id="f659a-146">Este panel proporciona una vista del mapa del tráfico de red con toohello volumen de tráfico de cada país de ajuste de escala de colores.</span><span class="sxs-lookup"><span data-stu-id="f659a-146">This pane provides you with a map view of your network traffic, with colors scaling toohello volume of traffic from each country.</span></span> <span data-ttu-id="f659a-147">Puede seleccionar las estadísticas de países resaltados tooview flujo adicionales como la proporción de Hola de datos enviados y recibidos desde direcciones IP en ese país.</span><span class="sxs-lookup"><span data-stu-id="f659a-147">You can select highlighted countries tooview additional flow statistics such as hello proportion of data sent and received from IPs in that country.</span></span>

    ![Geomap][8]

1. <span data-ttu-id="f659a-149">Filtros</span><span class="sxs-lookup"><span data-stu-id="f659a-149">Filters</span></span>

    <span data-ttu-id="f659a-150">CapAnalysis proporciona un conjunto de filtros para el análisis rápido de paquetes específicos.</span><span class="sxs-lookup"><span data-stu-id="f659a-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="f659a-151">Por ejemplo, puede elegir datos de hello toofilter por información específica de protocolo toogain en ese subconjunto de tráfico.</span><span class="sxs-lookup"><span data-stu-id="f659a-151">For example, you can choose toofilter hello data by protocol toogain specific insights on that subset of traffic.</span></span>

    ![filters][11]

    <span data-ttu-id="f659a-153">Visite [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn más información acerca de las capacidades de todos los CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="f659a-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="f659a-154">Conclusión</span><span class="sxs-lookup"><span data-stu-id="f659a-154">Conclusion</span></span>

<span data-ttu-id="f659a-155">Característica de captura de paquetes del Monitor de red permite análisis forense de red de toocapture Hola datos tooperform necesarios y comprender mejor el tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="f659a-155">Network Watcher’s packet capture feature allows you toocapture hello data necessary tooperform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="f659a-156">En este escenario, hemos mostrado cómo las capturas de paquetes de Network Watcher se pueden integrar fácilmente con herramientas de visualización de código abierto.</span><span class="sxs-lookup"><span data-stu-id="f659a-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="f659a-157">Mediante herramientas de código abierto como captura CapAnalysis toovisualize paquetes, puede realizar una inspección profunda de paquetes e identificar rápidamente las tendencias en el tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="f659a-157">By using open source tools such as CapAnalysis toovisualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f659a-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f659a-158">Next steps</span></span>

<span data-ttu-id="f659a-159">toolearn más información acerca de los registros de flujo NSG, visite [registros de flujo de NSG](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f659a-159">toolearn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="f659a-160">Obtenga información acerca de cómo toovisualize su flujo NSG registra con Power BI visitando [flujos de NSG visualizar registros con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="f659a-160">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
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
