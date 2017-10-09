---
title: "inspección del aaaPacket con Monitor de red de Azure | Documentos de Microsoft"
description: "Este artículo describe cómo se recopila toouse inspección profunda de paquetes de tooperform de Monitor de red de una máquina virtual"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4aeddcd482edc4df3d63e87b5c4b0788c540850b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a><span data-ttu-id="adf61-103">Inspección de paquetes con Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="adf61-103">Packet inspection with Azure Network Watcher</span></span>

<span data-ttu-id="adf61-104">Con la característica de captura de paquetes de Hola de Monitor de red, puede iniciar y administrar sesiones de captura en las máquinas virtuales de Azure desde el portal de hello, PowerShell CLI y mediante programación a través de hello SDK y API de REST.</span><span class="sxs-lookup"><span data-stu-id="adf61-104">Using hello packet capture feature of Network Watcher, you can initiate and manage captures sessions on your Azure VMs from hello portal, PowerShell, CLI, and programmatically through hello SDK and REST API.</span></span> <span data-ttu-id="adf61-105">Captura de paquetes permite tooaddress escenarios que requieren datos de nivel de paquete ofreciendo información de hello en un formato utilizable con facilidad.</span><span class="sxs-lookup"><span data-stu-id="adf61-105">Packet capture allows you tooaddress scenarios that require packet level data by providing hello information in a readily usable format.</span></span> <span data-ttu-id="adf61-106">Aprovechamiento de datos de Hola de tooinspect muchas herramientas gratuitas disponibles, puede examinar las comunicaciones enviadas tooand de las máquinas virtuales y obtener información sobre el tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="adf61-106">Leveraging freely available tools tooinspect hello data, you can examine communications sent tooand from your VMs and gain insights into your network traffic.</span></span> <span data-ttu-id="adf61-107">Algunos ejemplos de uso de datos de captura de paquetes son: investigación de los problemas de la red o de las aplicaciones, detección del uso incorrecto de la red y de los intentos de intrusión o mantenimiento del cumplimiento normativo.</span><span class="sxs-lookup"><span data-stu-id="adf61-107">Some example uses of packet capture data include: investigating network or application issues, detecting network misuse and intrusion attempts, or maintaining regulatory compliance.</span></span> <span data-ttu-id="adf61-108">En este artículo, le mostramos cómo tooopen un archivo de captura de paquete proporcionado por el Monitor de red mediante una herramienta de código abierto populares.</span><span class="sxs-lookup"><span data-stu-id="adf61-108">In this article, we show how tooopen a packet capture file provided by Network Watcher using a popular open source tool.</span></span> <span data-ttu-id="adf61-109">También proporcionamos ejemplos que muestran cómo identificar el tráfico anómalo toocalculate una latencia de conexión y examinar las estadísticas de red.</span><span class="sxs-lookup"><span data-stu-id="adf61-109">We will also provide examples showing how toocalculate a connection latency, identify abnormal traffic, and examine networking statistics.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="adf61-110">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="adf61-110">Before you begin</span></span>

<span data-ttu-id="adf61-111">En este artículo se recorren algunos escenarios preconfigurados en una captura de paquetes que se ha ejecutado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="adf61-111">This article goes through some pre-configured scenarios on a packet capture that was run previously.</span></span> <span data-ttu-id="adf61-112">Estos escenarios ilustran funcionalidades a las que se puede acceder mediante la revisión de una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="adf61-112">These scenarios illustrate capabilities that can be accessed by reviewing a packet capture.</span></span> <span data-ttu-id="adf61-113">Este escenario se usa [WireShark](https://www.wireshark.org/) tooinspect captura de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="adf61-113">This scenario uses [WireShark](https://www.wireshark.org/) tooinspect hello packet capture.</span></span>

<span data-ttu-id="adf61-114">Se asume también que ya se ejecutó una captura de paquetes en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="adf61-114">This scenario assumes you already ran a packet capture on a virtual machine.</span></span> <span data-ttu-id="adf61-115">toolearn cómo visite toocreate una captura de paquetes [captura de paquetes de administrar con el portal de hello](network-watcher-packet-capture-manage-portal.md) o con REST visitando [captura de paquetes de administración con la API de REST](network-watcher-packet-capture-manage-rest.md).</span><span class="sxs-lookup"><span data-stu-id="adf61-115">toolearn how toocreate a packet capture visit [Manage packet captures with hello portal](network-watcher-packet-capture-manage-portal.md) or with REST by visiting [Managing Packet Captures with REST API](network-watcher-packet-capture-manage-rest.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="adf61-116">Escenario</span><span class="sxs-lookup"><span data-stu-id="adf61-116">Scenario</span></span>

<span data-ttu-id="adf61-117">En este escenario, podrá:</span><span class="sxs-lookup"><span data-stu-id="adf61-117">In this scenario, you:</span></span>

* <span data-ttu-id="adf61-118">Revisar una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="adf61-118">Review a packet capture</span></span>

## <a name="calculate-network-latency"></a><span data-ttu-id="adf61-119">Calcular la latencia de red</span><span class="sxs-lookup"><span data-stu-id="adf61-119">Calculate network latency</span></span>

<span data-ttu-id="adf61-120">En este escenario, se muestra cómo tooview Hola inicial de ida y vuelta (RTT Time) de una conversación de protocolo de Control de transmisión (TCP) que se producen entre dos extremos.</span><span class="sxs-lookup"><span data-stu-id="adf61-120">In this scenario, we show how tooview hello initial Round Trip Time (RTT) of a Transmission Control Protocol (TCP) conversation occurring between two endpoints.</span></span>

<span data-ttu-id="adf61-121">Cuando se establece una conexión TCP, hello en primer lugar tres paquetes enviados en la conexión de hello siguen un protocolo de enlace de tres vías de patrón conocida tooas Hola.</span><span class="sxs-lookup"><span data-stu-id="adf61-121">When a TCP connection is established, hello first three packets sent in hello connection follow a pattern commonly referred tooas hello three-way handshake.</span></span> <span data-ttu-id="adf61-122">Mediante el examen primero dos paquetes enviados en este protocolo de enlace, una solicitud inicial del cliente de hello y una respuesta del servidor de hello, podemos calcular latencia hello cuando se establece esta conexión.</span><span class="sxs-lookup"><span data-stu-id="adf61-122">By examining hello first two packets sent in this handshake, an initial request from hello client and a response from hello server, we can calculate hello latency when this connection was established.</span></span> <span data-ttu-id="adf61-123">Esta latencia es que se hace referencia tooas Hola tiempo de ida y vuelta (RTT).</span><span class="sxs-lookup"><span data-stu-id="adf61-123">This latency is referred tooas hello Round Trip Time (RTT).</span></span> <span data-ttu-id="adf61-124">Para obtener más información sobre el protocolo TCP de Hola y el protocolo de enlace de hello triple consulte toohello después de recursos.</span><span class="sxs-lookup"><span data-stu-id="adf61-124">For more information on hello TCP protocol and hello three-way handshake refer toohello following resource.</span></span> <span data-ttu-id="adf61-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span><span class="sxs-lookup"><span data-stu-id="adf61-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span></span>

### <a name="step-1"></a><span data-ttu-id="adf61-126">Paso 1</span><span class="sxs-lookup"><span data-stu-id="adf61-126">Step 1</span></span>

<span data-ttu-id="adf61-127">Inicie WireShark.</span><span class="sxs-lookup"><span data-stu-id="adf61-127">Launch WireShark</span></span>

### <a name="step-2"></a><span data-ttu-id="adf61-128">Paso 2</span><span class="sxs-lookup"><span data-stu-id="adf61-128">Step 2</span></span>

<span data-ttu-id="adf61-129">Hola carga **CAP.** archivo desde la captura de paquete.</span><span class="sxs-lookup"><span data-stu-id="adf61-129">Load hello **.cap** file from your packet capture.</span></span> <span data-ttu-id="adf61-130">Este archivo puede encontrarse en el blob de Hola se ha guardado en nuestro localmente en máquina virtual de hello, dependiendo de cómo la haya configurado.</span><span class="sxs-lookup"><span data-stu-id="adf61-130">This file can be found in hello blob it was saved in our locally on hello virtual machine, depending on how you configured it.</span></span>

### <a name="step-3"></a><span data-ttu-id="adf61-131">Paso 3</span><span class="sxs-lookup"><span data-stu-id="adf61-131">Step 3</span></span>

<span data-ttu-id="adf61-132">tooview Hola inicial de ida y vuelta (RTT Time) en las conversaciones de TCP, solo nos encargaremos en paquetes de saludo de dos primeras implicados en el protocolo de enlace de hello TCP.</span><span class="sxs-lookup"><span data-stu-id="adf61-132">tooview hello initial Round Trip Time (RTT) in TCP conversations, we will only be looking at hello first two packets involved in hello TCP handshake.</span></span> <span data-ttu-id="adf61-133">Vamos a usar en primer lugar dos paquetes de saludo de protocolo de enlace de tres vías de hello, que son Hola [SYN], [SYN, ACK] paquetes.</span><span class="sxs-lookup"><span data-stu-id="adf61-133">We will be using hello first two packets in hello three-way handshake, which are hello [SYN], [SYN, ACK] packets.</span></span> <span data-ttu-id="adf61-134">Se denominan marcadores establecidos en el encabezado TCP de Hola.</span><span class="sxs-lookup"><span data-stu-id="adf61-134">They are named for flags set in hello TCP header.</span></span> <span data-ttu-id="adf61-135">no se utilizará el último paquete de Hello en el protocolo de enlace de hello, paquete de saludo [confirmación], en este escenario.</span><span class="sxs-lookup"><span data-stu-id="adf61-135">hello last packet in hello handshake, hello [ACK] packet, will not be used in this scenario.</span></span> <span data-ttu-id="adf61-136">Hola cliente envía paquetes de saludo [s].</span><span class="sxs-lookup"><span data-stu-id="adf61-136">hello [SYN] packet is sent by hello client.</span></span> <span data-ttu-id="adf61-137">Una vez que se recibe servidor de hello envía paquetes de saludo [confirmación] como una confirmación de recepción Hola SYN de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="adf61-137">Once it is received hello server sends hello [ACK] packet as an acknowledgement of receiving hello SYN from hello client.</span></span> <span data-ttu-id="adf61-138">Aprovechar el hecho de Hola que respuesta del servidor de hello requiere muy poca sobrecarga, calculamos Hola Hola cliente envió RTT restando la hora de hello paquete de saludo [SYN, ACK] se ha recibido por el cliente de Hola por paquete de tiempo [s] de saludo.</span><span class="sxs-lookup"><span data-stu-id="adf61-138">Leveraging hello fact that hello server’s response requires very little overhead, we calculate hello RTT by subtracting hello time hello [SYN, ACK] packet was received by hello client by hello time [SYN] packet was sent by hello client.</span></span>

<span data-ttu-id="adf61-139">Con WireShark este valor se calcula automáticamente.</span><span class="sxs-lookup"><span data-stu-id="adf61-139">Using WireShark this value is calculated for us.</span></span>

<span data-ttu-id="adf61-140">toomore ver fácilmente los dos primeros paquetes en hello TCP tridireccional, vamos a utilizar Hola filtrado capacidad proporcionada por WireShark.</span><span class="sxs-lookup"><span data-stu-id="adf61-140">toomore easily view hello first two packets in hello TCP three-way handshake, we will utilize hello filtering capability provided by WireShark.</span></span>

<span data-ttu-id="adf61-141">filtro de Hola de tooapply en WireShark, expanda Hola "Protocolo de Control de transmisión" segmento de un paquete [SYN] en la captura y examine las marcas de hello establecidos en el encabezado TCP de Hola.</span><span class="sxs-lookup"><span data-stu-id="adf61-141">tooapply hello filter in WireShark, expand hello “Transmission Control Protocol” Segment of a [SYN] packet in your capture and examine hello flags set in hello TCP header.</span></span>

<span data-ttu-id="adf61-142">Puesto que estamos buscando toofilter en todos los [SYN] y [SYN, ACK] paquetes en marcas de cofirm que bit Syn de Hola se establece too1, a continuación, haga clic en el bit de hello Syn -> aplicar como filtro -> seleccionados.</span><span class="sxs-lookup"><span data-stu-id="adf61-142">Since we are looking toofilter on all [SYN] and [SYN, ACK] packets, under flags cofirm that hello Syn bit is set too1, then right click on hello Syn bit -> Apply as Filter -> Selected.</span></span>

![figura 7][7]

### <a name="step-4"></a><span data-ttu-id="adf61-144">Paso 4</span><span class="sxs-lookup"><span data-stu-id="adf61-144">Step 4</span></span>

<span data-ttu-id="adf61-145">Ahora que ha filtrado los paquetes de saludo ventana tooonly vea con hello [SYN] bit establecido, puede seleccionar fácilmente las conversaciones que le interesen tooview Hola RTT inicial.</span><span class="sxs-lookup"><span data-stu-id="adf61-145">Now that you have filtered hello window tooonly see packets with hello [SYN] bit set, you can easily select conversations you are interested in tooview hello initial RTT.</span></span> <span data-ttu-id="adf61-146">Un hello tooview de manera sencilla RTT en WireShark simplemente haga clic en lista desplegable de hello marcado "SEQ/confirmación" análisis.</span><span class="sxs-lookup"><span data-stu-id="adf61-146">A simple way tooview hello RTT in WireShark simply click hello dropdown marked “SEQ/ACK” analysis.</span></span> <span data-ttu-id="adf61-147">A continuación, verá Hola que RTT muestra.</span><span class="sxs-lookup"><span data-stu-id="adf61-147">You will then see hello RTT displayed.</span></span> <span data-ttu-id="adf61-148">En este caso, Hola RTT era 0.0022114 segundos o ms 2.211.</span><span class="sxs-lookup"><span data-stu-id="adf61-148">In this case, hello RTT was 0.0022114 seconds, or 2.211 ms.</span></span>

![figura 8][8]

## <a name="unwanted-protocols"></a><span data-ttu-id="adf61-150">Protocolos no deseados</span><span class="sxs-lookup"><span data-stu-id="adf61-150">Unwanted protocols</span></span>

<span data-ttu-id="adf61-151">Puede tener muchas aplicaciones ejecutándose en una instancia de máquina virtual que haya implementado en Azure.</span><span class="sxs-lookup"><span data-stu-id="adf61-151">You can have many applications running on a virtual machine instance you have deployed in Azure.</span></span> <span data-ttu-id="adf61-152">Muchas de estas aplicaciones se comunican a través de la red de hello, quizás sin su permiso explícito.</span><span class="sxs-lookup"><span data-stu-id="adf61-152">Many of these applications communicate over hello network, perhaps without your explicit permission.</span></span> <span data-ttu-id="adf61-153">Con la comunicación de red de toostore de captura de paquetes, podemos analizaremos cómo aplicación hablar en red de Hola y busque los problemas.</span><span class="sxs-lookup"><span data-stu-id="adf61-153">Using packet capture toostore network communication, we can investigate how application are talking on hello network and look for any issues.</span></span>

<span data-ttu-id="adf61-154">En este ejemplo, revisamos una captura de paquetes ejecutada anteriormente para ver si existen protocolos indeseados que podrían indicar la comunicación no autorizada desde una aplicación que se ejecuta en su máquina.</span><span class="sxs-lookup"><span data-stu-id="adf61-154">In this example, we review a previous ran packet capture for unwanted protocols that may indicate unauthorized communication from an application running on your machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="adf61-155">Paso 1</span><span class="sxs-lookup"><span data-stu-id="adf61-155">Step 1</span></span>

<span data-ttu-id="adf61-156">Usar Hola misma captura en haga clic en anterior escenario de Hola **estadísticas** > **jerarquía de protocolo**</span><span class="sxs-lookup"><span data-stu-id="adf61-156">Using hello same capture in hello previous scenario click **Statistics** > **Protocol Hierarchy**</span></span>

![menú de jerarquía de protocolos][2]

<span data-ttu-id="adf61-158">aparece la ventana de jerarquía de protocolo de Hola.</span><span class="sxs-lookup"><span data-stu-id="adf61-158">hello protocol hierarchy window appears.</span></span> <span data-ttu-id="adf61-159">Esta vista proporciona una lista de todos los protocolos de Hola que estaban en uso durante la sesión de captura de Hola y el número de Hola de paquetes transmitidos y recibidos mediante protocolos de Hola.</span><span class="sxs-lookup"><span data-stu-id="adf61-159">This view provides a list of all hello protocols that were in use during hello capture session and hello number of packets transmitted and received using hello protocols.</span></span> <span data-ttu-id="adf61-160">Puede ser útil para buscar el tráfico de red no deseado en las máquinas virtuales o la red.</span><span class="sxs-lookup"><span data-stu-id="adf61-160">This view can be useful for finding unwanted network traffic on your virtual machines or network.</span></span>

![jerarquía de protocolo abierto][3]

<span data-ttu-id="adf61-162">Como puede ver en la siguiente captura de pantalla de hello, hubo tráfico mediante el protocolo de BitTorrent hello, que se utiliza para compartir archivos de toopeer de mismo nivel.</span><span class="sxs-lookup"><span data-stu-id="adf61-162">As you can see in hello following screen capture, there was traffic using hello BitTorrent protocol, which is used for peer toopeer file sharing.</span></span> <span data-ttu-id="adf61-163">Como administrador que no espera toosee BitTorrent tráfico en este determinado las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="adf61-163">As an administrator you do not expect toosee BitTorrent traffic on this particular virtual machines.</span></span> <span data-ttu-id="adf61-164">Ahora, tenga en cuenta este tráfico, puede quitar Hola del mismo nivel toopeer software que instalado en esta máquina virtual u Hola bloque tráfico mediante grupos de seguridad de red o un Firewall.</span><span class="sxs-lookup"><span data-stu-id="adf61-164">Now you aware of this traffic, you can remove hello peer toopeer software that installed on this virtual machine, or block hello traffic using Network Security Groups or a Firewall.</span></span> <span data-ttu-id="adf61-165">Además, es posible que decida toorun capturas de paquetes en una programación, para poder revisar uso del protocolo de hello en sus máquinas virtuales con regularidad.</span><span class="sxs-lookup"><span data-stu-id="adf61-165">Additionally, you may elect toorun packet captures on a schedule, so you can review hello protocol use on your virtual machines regularly.</span></span> <span data-ttu-id="adf61-166">Para obtener un ejemplo de cómo tooautomate red tareas de la visita de azure [supervisar los recursos de red con automatización de azure](network-watcher-monitor-with-azure-automation.md)</span><span class="sxs-lookup"><span data-stu-id="adf61-166">For an example on how tooautomate network tasks in azure visit [Monitor network resources with azure automation](network-watcher-monitor-with-azure-automation.md)</span></span>

## <a name="finding-top-destinations-and-ports"></a><span data-ttu-id="adf61-167">Búsqueda de puertos y destinos más frecuentes</span><span class="sxs-lookup"><span data-stu-id="adf61-167">Finding top destinations and ports</span></span>

<span data-ttu-id="adf61-168">Descripción de los tipos de Hola de tráfico, Hola extremos y puertos de hello comunicados por medio de es un importante al supervisar o solucionar problemas de aplicaciones y recursos de la red.</span><span class="sxs-lookup"><span data-stu-id="adf61-168">Understanding hello types of traffic, hello endpoints, and hello ports communicated over is an important when monitoring or troubleshooting applications and resources on your network.</span></span> <span data-ttu-id="adf61-169">Gracias a un archivo de captura de paquetes desde arriba, podemos aprender rápidamente destinos principales de hello nuestro VM está comunicando y Hola puertos que se utilizan.</span><span class="sxs-lookup"><span data-stu-id="adf61-169">Utilizing a packet capture file from above, we can quickly learn hello top destinations our VM is communicating with and hello ports being utilized.</span></span>

### <a name="step-1"></a><span data-ttu-id="adf61-170">Paso 1</span><span class="sxs-lookup"><span data-stu-id="adf61-170">Step 1</span></span>

<span data-ttu-id="adf61-171">Usar Hola misma captura en haga clic en anterior escenario de Hola **estadísticas** > **las estadísticas de IPv4** > **destinos y puertos**</span><span class="sxs-lookup"><span data-stu-id="adf61-171">Using hello same capture in hello previous scenario click **Statistics** > **IPv4 Statistics** > **Destinations and Ports**</span></span>

![ventana de captura de paquetes][4]

### <a name="step-2"></a><span data-ttu-id="adf61-173">Paso 2</span><span class="sxs-lookup"><span data-stu-id="adf61-173">Step 2</span></span>

<span data-ttu-id="adf61-174">Cuando consideramos a través de los resultados de hello destaque una línea, hay varias conexiones en el puerto 111.</span><span class="sxs-lookup"><span data-stu-id="adf61-174">As we look through hello results a line stands out, there were multiple connections on port 111.</span></span> <span data-ttu-id="adf61-175">puerto de Hello usado más estaba 3389, que es el escritorio remoto y Hola restantes son puertos dinámicos de RPC.</span><span class="sxs-lookup"><span data-stu-id="adf61-175">hello most used port was 3389, which is remote desktop, and hello remaining are RPC dynamic ports.</span></span>

<span data-ttu-id="adf61-176">Aunque este tráfico puede significar nada, es un puerto que se usó para muchas conexiones y es administrador toohello desconocido.</span><span class="sxs-lookup"><span data-stu-id="adf61-176">While this traffic may mean nothing, it is a port that was used for many connections and is unknown toohello administrator.</span></span>

![figura 5][5]

### <a name="step-3"></a><span data-ttu-id="adf61-178">Paso 3</span><span class="sxs-lookup"><span data-stu-id="adf61-178">Step 3</span></span>

<span data-ttu-id="adf61-179">Ahora que hemos determinado un fuera de lugar puerto podemos filtrar la captura basado en puerto de Hola.</span><span class="sxs-lookup"><span data-stu-id="adf61-179">Now that we have determined an out of place port we can filter our capture based on hello port.</span></span>

<span data-ttu-id="adf61-180">filtro de Hello en este escenario sería:</span><span class="sxs-lookup"><span data-stu-id="adf61-180">hello filter in this scenario would be:</span></span>

```
tcp.port == 111
```

<span data-ttu-id="adf61-181">Se escriba el texto de filtro de Hola desde arriba en el cuadro de texto de filtro de hello y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="adf61-181">We enter hello filter text from above in hello filter textbox and hit enter.</span></span>

![figura 6][6]

<span data-ttu-id="adf61-183">Desde los resultados de hello, podemos ver todo el tráfico de hello procede de una máquina virtual local en hello misma subred.</span><span class="sxs-lookup"><span data-stu-id="adf61-183">From hello results, we can see all hello traffic is coming from a local virtual machine on hello same subnet.</span></span> <span data-ttu-id="adf61-184">Si todavía no comprender por qué se está produciendo este tráfico, podemos inspeccionar Hola paquetes toodetermine ¿por qué está realizando estas llamadas en el puerto 111 aún más.</span><span class="sxs-lookup"><span data-stu-id="adf61-184">If we still don’t understand why this traffic is occurring, we can further inspect hello packets toodetermine why it is making these calls on port 111.</span></span> <span data-ttu-id="adf61-185">Con esta información podemos realizar las acciones apropiadas Hola.</span><span class="sxs-lookup"><span data-stu-id="adf61-185">With this information we can take hello appropriate action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="adf61-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="adf61-186">Next steps</span></span>

<span data-ttu-id="adf61-187">Obtenga información acerca de aproximadamente Hola otras características de diagnóstico del Monitor de red visitando [información general de supervisión de red de Azure](network-watcher-monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="adf61-187">Learn about hello other diagnostic features of Network Watcher by visiting [Azure network monitoring overview](network-watcher-monitoring-overview.md)</span></span>

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













