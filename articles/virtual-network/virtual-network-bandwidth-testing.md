---
title: "rendimiento de red de máquina virtual de Azure aaaTesting | Documentos de Microsoft"
description: "Obtenga información acerca de cómo el rendimiento de la red de tootest máquina virtual de Azure."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/21/2017
ms.author: steveesp
ms.openlocfilehash: 2da85c27bc8d16a443b215891f4cd0460f41926f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a><span data-ttu-id="23465-103">Pruebas de ancho de banda y rendimiento (NTTTCP)</span><span class="sxs-lookup"><span data-stu-id="23465-103">Bandwidth/Throughput testing (NTTTCP)</span></span>

<span data-ttu-id="23465-104">Al probar el rendimiento de la red en Azure, es mejor toouse una herramienta que tenga como destino de red de Hola para pruebas y minimiza el uso de Hola de otros recursos que puede afectar al rendimiento.</span><span class="sxs-lookup"><span data-stu-id="23465-104">When testing network throughput performance in Azure, it's best toouse a tool that targets hello network for testing and minimizes hello use of other resources that could impact performance.</span></span> <span data-ttu-id="23465-105">Se recomienda NTTTCP.</span><span class="sxs-lookup"><span data-stu-id="23465-105">NTTTCP is recommended.</span></span>

<span data-ttu-id="23465-106">Copiar Hola herramienta tootwo máquinas virtuales de Azure de hello mismo tamaño.</span><span class="sxs-lookup"><span data-stu-id="23465-106">Copy hello tool tootwo Azure VMs of hello same size.</span></span> <span data-ttu-id="23465-107">Una máquina virtual funciona como hello otro como receptor y remitente.</span><span class="sxs-lookup"><span data-stu-id="23465-107">One VM functions as SENDER and hello other as RECEIVER.</span></span>

#### <a name="deploying-vms-for-testing"></a><span data-ttu-id="23465-108">Implementación de máquinas virtuales para pruebas</span><span class="sxs-lookup"><span data-stu-id="23465-108">Deploying VMs for testing</span></span>
<span data-ttu-id="23465-109">Para fines de Hola de esta prueba, Hola dos máquinas virtuales deben estar en Hola mismo servicio en la nube u Hola el mismo conjunto de disponibilidad para que podamos usar su direcciones IP internas y excluir Hola equilibradores de carga de la prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="23465-109">For hello purposes of this test, hello two VMs should be in either hello same Cloud Service or hello same Availability Set so that we can use their internal IPs and exclude hello Load Balancers from hello test.</span></span> <span data-ttu-id="23465-110">Es posible tootest con hello VIP, pero este tipo de pruebas está fuera de ámbito de Hola de este documento.</span><span class="sxs-lookup"><span data-stu-id="23465-110">It is possible tootest with hello VIP but this kind of testing is outside hello scope of this document.</span></span>
 
<span data-ttu-id="23465-111">Tome nota de la dirección IP del destinatario Hola.</span><span class="sxs-lookup"><span data-stu-id="23465-111">Make a note of hello RECEIVER's IP address.</span></span> <span data-ttu-id="23465-112">Vamos a llamar a esa dirección IP "a.b.c.r".</span><span class="sxs-lookup"><span data-stu-id="23465-112">Let's call that IP "a.b.c.r"</span></span>

<span data-ttu-id="23465-113">Tome nota del número de Hola de núcleos en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="23465-113">Make a note of hello number of cores on hello VM.</span></span> <span data-ttu-id="23465-114">Llamémoslo "\#num\_cores".</span><span class="sxs-lookup"><span data-stu-id="23465-114">Let's call this "\#num\_cores"</span></span>
 
<span data-ttu-id="23465-115">Ejecute hello NTTTCP comprobar 300 segundos (o 5 minutos) en hello remitente VM y el receptor máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="23465-115">Run hello NTTTCP test for 300 seconds (or 5 minutes) on hello sender VM and receiver VM.</span></span>

<span data-ttu-id="23465-116">Sugerencia: Al configurar esta prueba para hello primera vez, puede intentar antes una menor comentarios tooget período de prueba.</span><span class="sxs-lookup"><span data-stu-id="23465-116">Tip: When setting up this test for hello first time, you might try a shorter test period tooget feedback sooner.</span></span> <span data-ttu-id="23465-117">Una vez que la herramienta de hello funciona según lo esperado, extender a segundos de too300 período de prueba de Hola para obtener resultados más precisos Hola.</span><span class="sxs-lookup"><span data-stu-id="23465-117">Once hello tool is working as expected, extend hello test period too300 seconds for hello most accurate results.</span></span>

> [!NOTE]
> <span data-ttu-id="23465-118">remitente de Hello **y** receptor debe especificar **Hola mismo** parámetro de duración de la prueba (-t).</span><span class="sxs-lookup"><span data-stu-id="23465-118">hello sender **and** receiver must specify **hello same** test duration parameter (-t).</span></span>

<span data-ttu-id="23465-119">tootest un único flujo TCP durante 10 segundos:</span><span class="sxs-lookup"><span data-stu-id="23465-119">tootest a single TCP stream for 10 seconds:</span></span>

<span data-ttu-id="23465-120">Parámetros de receptor: ntttcp -r -t 10 -P 1</span><span class="sxs-lookup"><span data-stu-id="23465-120">Receiver parameters: ntttcp -r -t 10 -P 1</span></span>

<span data-ttu-id="23465-121">Parámetros de remitente: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span><span class="sxs-lookup"><span data-stu-id="23465-121">Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span></span>

> [!NOTE]
> <span data-ttu-id="23465-122">Hola anterior ejemplo solo deben tooconfirm usa la configuración.</span><span class="sxs-lookup"><span data-stu-id="23465-122">hello preceding sample should only be used tooconfirm your configuration.</span></span> <span data-ttu-id="23465-123">Más adelante en este documento se ofrecen ejemplos válidos de pruebas.</span><span class="sxs-lookup"><span data-stu-id="23465-123">Valid examples of testing are covered later in this document.</span></span>

## <a name="testing-vms-running-windows"></a><span data-ttu-id="23465-124">Pruebas de máquinas virtuales que ejecutan WINDOWS:</span><span class="sxs-lookup"><span data-stu-id="23465-124">Testing VMs running WINDOWS:</span></span>

#### <a name="get-ntttcp-onto-hello-vms"></a><span data-ttu-id="23465-125">Obtener NTTTCP en hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="23465-125">Get NTTTCP onto hello VMs.</span></span>

<span data-ttu-id="23465-126">Descargar la versión más reciente de hello: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span><span class="sxs-lookup"><span data-stu-id="23465-126">Download hello latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span></span>

<span data-ttu-id="23465-127">Si no se encuentra en esa página, realice esta búsqueda <https://www.bing.com/search?q=ntttcp+download>\< (debe ser el primer resultado).</span><span class="sxs-lookup"><span data-stu-id="23465-127">Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit</span></span>

<span data-ttu-id="23465-128">Considere la colocar NTTTCP en una carpeta independiente, como c:\\tools.</span><span class="sxs-lookup"><span data-stu-id="23465-128">Consider putting NTTTCP in separate folder, like c:\\tools</span></span>

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a><span data-ttu-id="23465-129">Permitir NTTTCP a través de firewall de Windows hello</span><span class="sxs-lookup"><span data-stu-id="23465-129">Allow NTTTCP through hello Windows firewall</span></span>
<span data-ttu-id="23465-130">En hello receptor, cree una regla de permiso en tooallow de Firewall de Windows hello el tooarrive de tráfico NTTTCP.</span><span class="sxs-lookup"><span data-stu-id="23465-130">On hello RECEIVER, create an Allow rule on hello Windows Firewall tooallow the NTTTCP traffic tooarrive.</span></span> <span data-ttu-id="23465-131">Resulta más fácil tooallow Hola todo NTTTCP programa por su nombre en lugar de puertos TCP específicos de tooallow de entrada.</span><span class="sxs-lookup"><span data-stu-id="23465-131">It's easiest tooallow hello entire NTTTCP program by name rather than tooallow specific TCP ports inbound.</span></span>

<span data-ttu-id="23465-132">Permitir ntttcp a través de hello Firewall de Windows como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="23465-132">Allow ntttcp through hello Windows Firewall like this:</span></span>

<span data-ttu-id="23465-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="23465-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

<span data-ttu-id="23465-134">Por ejemplo, si ha copiado ntttcp.exe toohello "c:\\herramientas" carpeta, esto sería el comando hello:</span><span class="sxs-lookup"><span data-stu-id="23465-134">For example, if you copied ntttcp.exe toohello "c:\\tools" folder, this would be hello command:</span></span> 

<span data-ttu-id="23465-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="23465-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

#### <a name="running-ntttcp-tests"></a><span data-ttu-id="23465-136">Ejecución de pruebas de NTTTCP</span><span class="sxs-lookup"><span data-stu-id="23465-136">Running NTTTCP tests</span></span>

<span data-ttu-id="23465-137">Iniciar NTTTCP en hello receptor (**ejecutar desde CMD**, no de PowerShell):</span><span class="sxs-lookup"><span data-stu-id="23465-137">Start NTTTCP on hello RECEIVER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="23465-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span><span class="sxs-lookup"><span data-stu-id="23465-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span></span>

<span data-ttu-id="23465-139">Si Hola VM tiene cuatro núcleos y una dirección IP de 10.0.0.4, sería similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="23465-139">If hello VM has four cores and an IP address of 10.0.0.4, it would look like this:</span></span>

<span data-ttu-id="23465-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="23465-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span></span>


<span data-ttu-id="23465-141">Iniciar NTTTCP en hello remitente (**ejecutar desde CMD**, no de PowerShell):</span><span class="sxs-lookup"><span data-stu-id="23465-141">Start NTTTCP on hello SENDER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="23465-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="23465-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span></span> 

<span data-ttu-id="23465-143">Esperar los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="23465-143">Wait for hello results.</span></span>


## <a name="testing-vms-running-linux"></a><span data-ttu-id="23465-144">Pruebas de máquinas virtuales que ejecutan LINUX:</span><span class="sxs-lookup"><span data-stu-id="23465-144">Testing VMs running LINUX:</span></span>

<span data-ttu-id="23465-145">Use nttcp-for-linux.</span><span class="sxs-lookup"><span data-stu-id="23465-145">Use nttcp-for-linux.</span></span> <span data-ttu-id="23465-146">Está disponible en <https://github.com/Microsoft/ntttcp-for-linux>.</span><span class="sxs-lookup"><span data-stu-id="23465-146">It is available from <https://github.com/Microsoft/ntttcp-for-linux></span></span>

<span data-ttu-id="23465-147">En hello máquinas virtuales de Linux (remitente y receptor), ejecute estos comandos para preparar ntttcp para linux en las máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="23465-147">On hello Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:</span></span>

<span data-ttu-id="23465-148">CentOS: instalación de Git:</span><span class="sxs-lookup"><span data-stu-id="23465-148">CentOS - Install Git:</span></span>
``` bash
  yum install gcc -y  
  yum install git -y
```
<span data-ttu-id="23465-149">Ubuntu: instalación de Git:</span><span class="sxs-lookup"><span data-stu-id="23465-149">Ubuntu - Install Git:</span></span>
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
<span data-ttu-id="23465-150">Cree e instale en ambas:</span><span class="sxs-lookup"><span data-stu-id="23465-150">Make and Install on both:</span></span>
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

<span data-ttu-id="23465-151">Como en el ejemplo de Windows hello, suponemos que IP del receptor de hello Linux es 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="23465-151">As in hello Windows example, we assume hello Linux RECEIVER's IP is 10.0.0.4</span></span>

<span data-ttu-id="23465-152">Iniciar NTTTCP para Linux en hello receptor:</span><span class="sxs-lookup"><span data-stu-id="23465-152">Start NTTTCP-for-Linux on hello RECEIVER:</span></span>

``` bash
ntttcp -r -t 300
```

<span data-ttu-id="23465-153">Y en hello remitente, ejecute:</span><span class="sxs-lookup"><span data-stu-id="23465-153">And on hello SENDER, run:</span></span>

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
<span data-ttu-id="23465-154">Se proporciona too60 segundos si ningún parámetro de tiempo de prueba longitud valores predeterminados</span><span class="sxs-lookup"><span data-stu-id="23465-154">Test length defaults too60 seconds if no time parameter is given</span></span>

## <a name="testing-between-vms-running-windows-and-linux"></a><span data-ttu-id="23465-155">Pruebas entre máquinas virtuales que ejecutan Windows y Linux:</span><span class="sxs-lookup"><span data-stu-id="23465-155">Testing between VMs running Windows and LINUX:</span></span>

<span data-ttu-id="23465-156">En escenarios de esta se deberíamos habilite el modo de sincronización no Hola por lo que puede ejecutar la prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="23465-156">On this scenarios we should enable hello no-sync mode so hello test can run.</span></span> <span data-ttu-id="23465-157">Esto se realiza mediante hello **-N marca** para Linux, y **marca -ns** para Windows.</span><span class="sxs-lookup"><span data-stu-id="23465-157">This is done by using hello **-N flag** for Linux, and **-ns flag** for Windows.</span></span>

#### <a name="from-linux-toowindows"></a><span data-ttu-id="23465-158">Desde tooWindows de Linux:</span><span class="sxs-lookup"><span data-stu-id="23465-158">From Linux tooWindows:</span></span>

<span data-ttu-id="23465-159">Receptor<Windows>:</span><span class="sxs-lookup"><span data-stu-id="23465-159">Receiver <Windows>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

<span data-ttu-id="23465-160">Remitente<Linux> :</span><span class="sxs-lookup"><span data-stu-id="23465-160">Sender <Linux> :</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a><span data-ttu-id="23465-161">Desde Windows tooLinux:</span><span class="sxs-lookup"><span data-stu-id="23465-161">From Windows tooLinux:</span></span>

<span data-ttu-id="23465-162">Receptor<Linux>:</span><span class="sxs-lookup"><span data-stu-id="23465-162">Receiver <Linux>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

<span data-ttu-id="23465-163">Remitente<Windows>:</span><span class="sxs-lookup"><span data-stu-id="23465-163">Sender <Windows>:</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a><span data-ttu-id="23465-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="23465-164">Next steps</span></span>
* <span data-ttu-id="23465-165">Dependiendo de los resultados, puede haber espacio demasiado[optimizar máquinas de rendimiento de red](virtual-network-optimize-network-bandwidth.md) para su escenario.</span><span class="sxs-lookup"><span data-stu-id="23465-165">Depending on results, there may be room too[Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.</span></span>
* <span data-ttu-id="23465-166">Más información sobre [Preguntas más frecuentes (P+F) acerca de Azure Virtual Network](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="23465-166">Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
