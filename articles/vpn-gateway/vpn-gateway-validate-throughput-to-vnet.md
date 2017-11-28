---
title: Validar VPN rendimiento tooa red Virtual de Microsoft Azure | Documentos de Microsoft
description: "propósito de este documento Hello es toohelp un usuario validar el rendimiento de la red de Hola desde su tooan de recursos locales máquina virtual de Azure."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: 9cf0b67145645a3c2a9556b0cc910066cc62a9ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a><span data-ttu-id="91025-103">La red virtual de toovalidate VPN rendimiento tooa</span><span class="sxs-lookup"><span data-stu-id="91025-103">How toovalidate VPN throughput tooa virtual network</span></span>

<span data-ttu-id="91025-104">Una conexión VPN de puerta de enlace le permite tooestablish la conectividad entre entornos seguros, entre la red Virtual dentro de Azure y sus instalaciones de infraestructura de TI.</span><span class="sxs-lookup"><span data-stu-id="91025-104">A VPN gateway connection enables you tooestablish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span></span>

<span data-ttu-id="91025-105">Este artículo muestra cómo toovalidate rendimiento de la red de hello local recursos tooan máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="91025-105">This article shows how toovalidate network throughput from hello on-premises resources tooan Azure virtual machine.</span></span> <span data-ttu-id="91025-106">También proporciona orientación para la solución de errores.</span><span class="sxs-lookup"><span data-stu-id="91025-106">It also provides troubleshooting guidance.</span></span>

>[!NOTE]
><span data-ttu-id="91025-107">Este artículo está destinado toohelp diagnosticar y corregir problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="91025-107">This article is intended toohelp diagnose and fix common issues.</span></span> <span data-ttu-id="91025-108">Si le problema de hello toosolve no se puede mediante el uso de hello después de obtener información, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="91025-108">If you're unable toosolve hello issue by using hello following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="91025-109">Información general</span><span class="sxs-lookup"><span data-stu-id="91025-109">Overview</span></span>

<span data-ttu-id="91025-110">Hola conexión de puerta de enlace VPN implica Hola de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="91025-110">hello VPN gateway connection involves hello following components:</span></span>

- <span data-ttu-id="91025-111">Dispositivo VPN local (vea una lista de [dispositivos VPN validados)](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="91025-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span></span>
- <span data-ttu-id="91025-112">Internet público</span><span class="sxs-lookup"><span data-stu-id="91025-112">Public Internet</span></span>
- <span data-ttu-id="91025-113">Azure VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="91025-113">Azure VPN gateway</span></span>
- <span data-ttu-id="91025-114">Máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="91025-114">Azure virtual machine</span></span>

<span data-ttu-id="91025-115">Hola siguiente diagrama muestra hello lógica a la conectividad de un tooan de red local red virtual de Azure a través de VPN.</span><span class="sxs-lookup"><span data-stu-id="91025-115">hello following diagram shows hello logical connectivity of an on-premises network tooan Azure virtual network through VPN.</span></span>

![Lógica tooMSFT de conectividad de red de cliente de red con VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a><span data-ttu-id="91025-117">Calcular Hola máximo esperado entrada/salida</span><span class="sxs-lookup"><span data-stu-id="91025-117">Calculate hello maximum expected ingress/egress</span></span>

1.  <span data-ttu-id="91025-118">Determine los requisitos de rendimiento de la línea de base de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="91025-118">Determine your application's baseline throughput requirements.</span></span>
2.  <span data-ttu-id="91025-119">Establezca los límites de rendimiento de la puerta de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="91025-119">Determine your Azure VPN gateway throughput limits.</span></span> <span data-ttu-id="91025-120">Para obtener ayuda, consulte sección Hola "rendimiento agregado por tipo SKU y VPN" de [planificación y diseño para la puerta de enlace VPN](vpn-gateway-plan-design.md).</span><span class="sxs-lookup"><span data-stu-id="91025-120">For help, see hello "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span></span>
3.  <span data-ttu-id="91025-121">Determinar hello [Guía de rendimiento de máquina virtual de Azure](../virtual-machines/virtual-machines-windows-sizes.md) para el tamaño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="91025-121">Determine hello [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span></span>
4.  <span data-ttu-id="91025-122">Establezca el ancho de banda del proveedor de servicios de Internet (ISP).</span><span class="sxs-lookup"><span data-stu-id="91025-122">Determine your Internet Service Provider (ISP) bandwidth.</span></span>
5.  <span data-ttu-id="91025-123">Calcule el rendimiento esperado: menor ancho de banda de (VM, puerta de enlace e ISP) * 0,8.</span><span class="sxs-lookup"><span data-stu-id="91025-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) * 0.8.</span></span>

<span data-ttu-id="91025-124">Si el rendimiento calculado no cumple los requisitos de rendimiento de línea de base de la aplicación, necesita ancho de banda de tooincrease Hola de recursos de Hola que ha identificado como cuello de botella de Hola.</span><span class="sxs-lookup"><span data-stu-id="91025-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need tooincrease hello bandwidth of hello resource that you identified as hello bottleneck.</span></span> <span data-ttu-id="91025-125">tooresize una puerta de enlace de VPN de Azure, consulte [cambiar una SKU de puerta de enlace](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="91025-125">tooresize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="91025-126">tooresize una máquina virtual, consulte [cambiar el tamaño de una máquina virtual](../virtual-machines/virtual-machines-windows-resize-vm.md).</span><span class="sxs-lookup"><span data-stu-id="91025-126">tooresize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span></span> <span data-ttu-id="91025-127">Si no tiene previsto ancho de banda de Internet, también puede toocontact su ISP.</span><span class="sxs-lookup"><span data-stu-id="91025-127">If you are not experiencing expected Internet bandwidth, you may also want toocontact your ISP.</span></span>

## <a name="validate-network-throughput-by-using-performance-tools"></a><span data-ttu-id="91025-128">Validación del rendimiento de red mediante el uso de herramientas de rendimiento</span><span class="sxs-lookup"><span data-stu-id="91025-128">Validate network throughput by using performance tools</span></span>

<span data-ttu-id="91025-129">Esta validación debe realizarse durante las horas de poca actividad, ya que la saturación de rendimiento del túnel VPN durante las pruebas provoca que no se produzcan resultados precisos.</span><span class="sxs-lookup"><span data-stu-id="91025-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span></span>

<span data-ttu-id="91025-130">herramienta de Hola que se usa para esta prueba es iPerf, que funciona en Windows y Linux y tiene los modos de cliente y servidor.</span><span class="sxs-lookup"><span data-stu-id="91025-130">hello tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span></span> <span data-ttu-id="91025-131">Es limitado too3 GB/s para máquinas virtuales de Windows.</span><span class="sxs-lookup"><span data-stu-id="91025-131">It is limited too3 Gbps for Windows VMs.</span></span>

<span data-ttu-id="91025-132">Esta herramienta no lleva a cabo cualquier toodisk de operaciones de lectura/escritura.</span><span class="sxs-lookup"><span data-stu-id="91025-132">This tool does not perform any read/write operations toodisk.</span></span> <span data-ttu-id="91025-133">Solamente se produce el tráfico TCP generado automáticamente desde un toohello de final otros.</span><span class="sxs-lookup"><span data-stu-id="91025-133">It solely produces self-generated TCP traffic from one end toohello other.</span></span> <span data-ttu-id="91025-134">Generan estadísticas basadas en experimentación que mide Hola de ancho de banda disponible entre los nodos de cliente y servidor.</span><span class="sxs-lookup"><span data-stu-id="91025-134">It generated statistics based on experimentation that measures hello bandwidth available between client and server nodes.</span></span> <span data-ttu-id="91025-135">Cuando se prueba entre dos nodos, uno actúa como servidor de Hola y Hola otro como un cliente.</span><span class="sxs-lookup"><span data-stu-id="91025-135">When testing between two nodes, one acts as hello server and hello other as a client.</span></span> <span data-ttu-id="91025-136">Una vez completada esta prueba, se recomienda que invertir Hola roles tootest ambos cargar y descargar el rendimiento en ambos nodos.</span><span class="sxs-lookup"><span data-stu-id="91025-136">Once this test is completed, we recommend that you reverse hello roles tootest both upload and download throughput on both nodes.</span></span>

### <a name="download-iperf"></a><span data-ttu-id="91025-137">Descarga de iPerf</span><span class="sxs-lookup"><span data-stu-id="91025-137">Download iPerf</span></span>
<span data-ttu-id="91025-138">Descargue [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span><span class="sxs-lookup"><span data-stu-id="91025-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span></span> <span data-ttu-id="91025-139">Para más información, vea la [documentación de Ambari](https://iperf.fr/iperf-doc.php).</span><span class="sxs-lookup"><span data-stu-id="91025-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span></span>

 >[!NOTE]
 ><span data-ttu-id="91025-140">productos de terceros de Hola que se explica en este artículo están fabricados por compañías independientes de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="91025-140">hello third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span></span> <span data-ttu-id="91025-141">Microsoft no otorga ninguna garantía, implícita o de otro tipo, sobre el rendimiento de Hola o la confiabilidad de estos productos.</span><span class="sxs-lookup"><span data-stu-id="91025-141">Microsoft makes no warranty, implied or otherwise, about hello performance or reliability of these products.</span></span>
 >
 >

### <a name="run-iperf-iperf3exe"></a><span data-ttu-id="91025-142">Ejecución de iPerf (iperf3.exe)</span><span class="sxs-lookup"><span data-stu-id="91025-142">Run iPerf (iperf3.exe)</span></span>
1. <span data-ttu-id="91025-143">Habilitar una regla ACL de GSN/permitiendo el tráfico de hello (para la dirección IP pública pruebas en la máquina virtual de Azure).</span><span class="sxs-lookup"><span data-stu-id="91025-143">Enable an NSG/ACL rule allowing hello traffic (for public IP address testing on Azure VM).</span></span>

2. <span data-ttu-id="91025-144">En ambos nodos, habilite una excepción de firewall para el puerto 5001.</span><span class="sxs-lookup"><span data-stu-id="91025-144">On both nodes, enable a firewall exception for port 5001.</span></span>

    <span data-ttu-id="91025-145">**Windows:** siguiente Hola de ejecución de comandos como administrador:</span><span class="sxs-lookup"><span data-stu-id="91025-145">**Windows:** Run hello following command as an administrator:</span></span>

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    <span data-ttu-id="91025-146">regla de hello tooremove cuando se prueba está completa, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="91025-146">tooremove hello rule when testing is complete, run this command:</span></span>

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    <span data-ttu-id="91025-147">**Azure Linux**: las imágenes de Azure Linux tienen firewalls permisivos.</span><span class="sxs-lookup"><span data-stu-id="91025-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span></span> <span data-ttu-id="91025-148">Si hay una aplicación escuchando en un puerto, se permite el tráfico de Hola a través.</span><span class="sxs-lookup"><span data-stu-id="91025-148">If there is an application listening on a port, hello traffic is allowed through.</span></span> <span data-ttu-id="91025-149">Las imágenes personalizadas que se protegen pueden necesitar puertos abiertos de forma explícita.</span><span class="sxs-lookup"><span data-stu-id="91025-149">Custom images that are secured may need ports opened explicitly.</span></span> <span data-ttu-id="91025-150">Los firewalls de nivel de sistema operativo Linux comunes incluyen `iptables`, `ufw`, o `firewalld`.</span><span class="sxs-lookup"><span data-stu-id="91025-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span></span>

3. <span data-ttu-id="91025-151">En el nodo del servidor hello, cambie el directorio de toohello donde se extrae iperf3.exe.</span><span class="sxs-lookup"><span data-stu-id="91025-151">On hello server node, change toohello directory where iperf3.exe is extracted.</span></span> <span data-ttu-id="91025-152">A continuación, ejecutar iPerf en modo de servidor y ha configurado toolisten en el puerto 5001 como Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="91025-152">Then run iPerf in server mode and set it toolisten on port 5001 as hello following commands:</span></span>

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. <span data-ttu-id="91025-153">En el nodo de cliente hello, cambie el directorio de toohello donde se extrae y a continuación, ejecute el siguiente comando de hello iperf herramienta:</span><span class="sxs-lookup"><span data-stu-id="91025-153">On hello client node, change toohello directory where iperf tool is extracted and then run hello following command:</span></span>

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    <span data-ttu-id="91025-154">cliente de Hello es inducción de tráfico en el servidor de puertos 5001 toohello durante 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="91025-154">hello client is inducing traffic on port 5001 toohello server for 30 seconds.</span></span> <span data-ttu-id="91025-155">Hola marca '-P ' que indica que estamos usando 32 nodos de servidor toohello de conexiones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="91025-155">hello flag '-P ' that indicates we are using 32 simultaneous connections toohello server node.</span></span>

    <span data-ttu-id="91025-156">Hello pantalla siguiente muestra la salida de hello de este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="91025-156">hello following screen shows hello output from this example:</span></span>

    ![Salida](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. <span data-ttu-id="91025-158">(Opcional) toopreserve Hola pruebas resultados, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="91025-158">(OPTIONAL) toopreserve hello testing results, run this command:</span></span>

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. <span data-ttu-id="91025-159">Después de completar los pasos anteriores de hello, ejecutar Hola invierten mismos pasos con roles de hello, por lo que hello nodo servidor ahora será cliente hello y viceversa.</span><span class="sxs-lookup"><span data-stu-id="91025-159">After completing hello previous steps, execute hello same steps with hello roles reversed, so that hello server node will now be hello client and vice-versa.</span></span>

## <a name="address-slow-file-copy-issues"></a><span data-ttu-id="91025-160">Solución de problemas de copia de archivos lenta</span><span class="sxs-lookup"><span data-stu-id="91025-160">Address slow file copy issues</span></span>
<span data-ttu-id="91025-161">Puede experimentar una copia de archivos lenta cuando use el Explorador de Windows o arrastre suelte en una sesión RDP.</span><span class="sxs-lookup"><span data-stu-id="91025-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span></span> <span data-ttu-id="91025-162">Este problema suele ser debido a tooone o ambos de hello siguientes factores:</span><span class="sxs-lookup"><span data-stu-id="91025-162">This problem is normally due tooone or both of hello following factors:</span></span>

- <span data-ttu-id="91025-163">Las aplicaciones de copia de archivos, como el Explorador de Windows y RDP, no utilizan varios subprocesos al copiar archivos.</span><span class="sxs-lookup"><span data-stu-id="91025-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span></span> <span data-ttu-id="91025-164">Para mejorar el rendimiento, use una aplicación de copia de archivo multiproceso como [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy archivos mediante el uso de 16 o 32 subprocesos.</span><span class="sxs-lookup"><span data-stu-id="91025-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy files by using 16 or 32 threads.</span></span> <span data-ttu-id="91025-165">número de subprocesos de hello toochange de copia de archivo en Richcopy, haga clic en **acción** > **copiar opciones** > **copiar el archivo**.</span><span class="sxs-lookup"><span data-stu-id="91025-165">toochange hello thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span></span><br><br><span data-ttu-id="91025-166">
![Problemas de copia de archivos lenta](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span><span class="sxs-lookup"><span data-stu-id="91025-166">
![Slow file copy issues](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span></span><br>
- <span data-ttu-id="91025-167">Velocidad de lectura/escritura del disco de VM insuficiente.</span><span class="sxs-lookup"><span data-stu-id="91025-167">Insufficient VM disk read/write speed.</span></span> <span data-ttu-id="91025-168">Para más información, vea [Solución de problemas de Azure Storage](../storage/common/storage-e2e-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="91025-168">For more information, see [Azure Storage Troubleshooting](../storage/common/storage-e2e-troubleshooting.md).</span></span>

## <a name="on-premises-device-external-facing-interface"></a><span data-ttu-id="91025-169">Interfaz con orientación externa del dispositivo local</span><span class="sxs-lookup"><span data-stu-id="91025-169">On-premises device external facing interface</span></span>
<span data-ttu-id="91025-170">Si el dispositivo VPN dirección IP a través de Internet se incluye en hello en local de hello [red local](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definición en Azure, es posible que experimente incapacidad toobring Hola se desconecta de la VPN, esporádico o problemas de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="91025-170">If hello on-premises VPN device Internet-facing IP address is included in hello [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability toobring up hello VPN, sporadic disconnects, or performance issues.</span></span>

## <a name="checking-latency"></a><span data-ttu-id="91025-171">Comprobación de la latencia</span><span class="sxs-lookup"><span data-stu-id="91025-171">Checking latency</span></span>
<span data-ttu-id="91025-172">Usar tracert tootrace tooMicrosoft Azure borde dispositivo toodetermine si hay retrasos superior a 100 ms. entre saltos.</span><span class="sxs-lookup"><span data-stu-id="91025-172">Use tracert tootrace tooMicrosoft Azure Edge device toodetermine if there are any delays exceeding 100 ms between hops.</span></span>

<span data-ttu-id="91025-173">Desde la red local de hello, ejecute *tracert* toohello VIP de hello puerta de enlace de Azure o la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="91025-173">From hello on-premises network, run *tracert* toohello VIP of hello Azure Gateway or VM.</span></span> <span data-ttu-id="91025-174">Una vez que vea sólo * devuelve, sabrá que ha alcanzado hello borde de Azure.</span><span class="sxs-lookup"><span data-stu-id="91025-174">Once you see only * returned, you know you have reached hello Azure edge.</span></span> <span data-ttu-id="91025-175">Cuando vea los nombres DNS que incluyan "MSN" devuelto, sabrá que ha alcanzado la red troncal de Microsoft de Hola.</span><span class="sxs-lookup"><span data-stu-id="91025-175">When you see DNS names that include "MSN" returned, you know you have reached hello Microsoft backbone.</span></span><br><br><span data-ttu-id="91025-176">
![Comprobación de la latencia](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span><span class="sxs-lookup"><span data-stu-id="91025-176">
![Checking Latency](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="91025-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="91025-177">Next steps</span></span>
<span data-ttu-id="91025-178">Para obtener más información o ayuda, visite Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="91025-178">For more information or help, check out hello following links:</span></span>

- [<span data-ttu-id="91025-179">Optimización del rendimiento de red en las máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="91025-179">Optimize network throughput for Azure virtual machines</span></span>](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [<span data-ttu-id="91025-180">Ayuda y soporte técnico de Microsoft</span><span class="sxs-lookup"><span data-stu-id="91025-180">Microsoft Support</span></span>](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
