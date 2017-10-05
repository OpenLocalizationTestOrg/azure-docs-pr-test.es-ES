---
title: "Prueba del rendimiento de la red de una máquina virtual de Azure | Microsoft Docs"
description: "Aprenda a probar el rendimiento de la red de una máquina virtual de Azure."
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
ms.openlocfilehash: ccebc722386a19014674d7a59757a3685bd50793
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a><span data-ttu-id="48159-103">Pruebas de ancho de banda y rendimiento (NTTTCP)</span><span class="sxs-lookup"><span data-stu-id="48159-103">Bandwidth/Throughput testing (NTTTCP)</span></span>

<span data-ttu-id="48159-104">Al probar el rendimiento de la red de Azure, se recomienda usar una herramienta que tenga como destino de la red para realizar pruebas y minimizar el uso de otros recursos que podrían afectar al rendimiento.</span><span class="sxs-lookup"><span data-stu-id="48159-104">When testing network throughput performance in Azure, it's best to use a tool that targets the network for testing and minimizes the use of other resources that could impact performance.</span></span> <span data-ttu-id="48159-105">Se recomienda NTTTCP.</span><span class="sxs-lookup"><span data-stu-id="48159-105">NTTTCP is recommended.</span></span>

<span data-ttu-id="48159-106">Copie la herramienta en dos máquinas virtuales de Azure del mismo tamaño.</span><span class="sxs-lookup"><span data-stu-id="48159-106">Copy the tool to two Azure VMs of the same size.</span></span> <span data-ttu-id="48159-107">Una máquina virtual funciona como remitente y la otra como receptora.</span><span class="sxs-lookup"><span data-stu-id="48159-107">One VM functions as SENDER and the other as RECEIVER.</span></span>

#### <a name="deploying-vms-for-testing"></a><span data-ttu-id="48159-108">Implementación de máquinas virtuales para pruebas</span><span class="sxs-lookup"><span data-stu-id="48159-108">Deploying VMs for testing</span></span>
<span data-ttu-id="48159-109">Para los fines de esta prueba, las dos máquinas virtuales deben tener el mismo servicio en la nube o el mismo conjunto de disponibilidad para que podamos usar sus direcciones IP internas y excluir los equilibradores de carga de la prueba.</span><span class="sxs-lookup"><span data-stu-id="48159-109">For the purposes of this test, the two VMs should be in either the same Cloud Service or the same Availability Set so that we can use their internal IPs and exclude the Load Balancers from the test.</span></span> <span data-ttu-id="48159-110">Es posible realizar pruebas con la dirección VIP, pero este tipo de pruebas está fuera del ámbito de este documento.</span><span class="sxs-lookup"><span data-stu-id="48159-110">It is possible to test with the VIP but this kind of testing is outside the scope of this document.</span></span>
 
<span data-ttu-id="48159-111">Tome nota de la dirección IP del DESTINATARIO.</span><span class="sxs-lookup"><span data-stu-id="48159-111">Make a note of the RECEIVER's IP address.</span></span> <span data-ttu-id="48159-112">Vamos a llamar a esa dirección IP "a.b.c.r".</span><span class="sxs-lookup"><span data-stu-id="48159-112">Let's call that IP "a.b.c.r"</span></span>

<span data-ttu-id="48159-113">Tome nota del número de núcleos de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="48159-113">Make a note of the number of cores on the VM.</span></span> <span data-ttu-id="48159-114">Llamémoslo "\#num\_cores".</span><span class="sxs-lookup"><span data-stu-id="48159-114">Let's call this "\#num\_cores"</span></span>
 
<span data-ttu-id="48159-115">Ejecute la prueba NTTTCP durante 300 segundos (o 5 minutos) en la máquina virtual del remitente y en la del receptor.</span><span class="sxs-lookup"><span data-stu-id="48159-115">Run the NTTTCP test for 300 seconds (or 5 minutes) on the sender VM and receiver VM.</span></span>

<span data-ttu-id="48159-116">Sugerencia: Al configurar esta prueba por primera vez, puede probar un período de prueba más corto para obtener antes comentarios.</span><span class="sxs-lookup"><span data-stu-id="48159-116">Tip: When setting up this test for the first time, you might try a shorter test period to get feedback sooner.</span></span> <span data-ttu-id="48159-117">Una vez que la herramienta funciona según lo esperado, amplíe el período de prueba en 300 segundos para obtener resultados más precisos.</span><span class="sxs-lookup"><span data-stu-id="48159-117">Once the tool is working as expected, extend the test period to 300 seconds for the most accurate results.</span></span>

> [!NOTE]
> <span data-ttu-id="48159-118">El remitente **y** el receptor deben especificar **el mismo** parámetro de duración de prueba (-t).</span><span class="sxs-lookup"><span data-stu-id="48159-118">The sender **and** receiver must specify **the same** test duration parameter (-t).</span></span>

<span data-ttu-id="48159-119">Para probar un único flujo TCP durante 10 segundos:</span><span class="sxs-lookup"><span data-stu-id="48159-119">To test a single TCP stream for 10 seconds:</span></span>

<span data-ttu-id="48159-120">Parámetros de receptor: ntttcp -r -t 10 -P 1</span><span class="sxs-lookup"><span data-stu-id="48159-120">Receiver parameters: ntttcp -r -t 10 -P 1</span></span>

<span data-ttu-id="48159-121">Parámetros de remitente: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span><span class="sxs-lookup"><span data-stu-id="48159-121">Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span></span>

> [!NOTE]
> <span data-ttu-id="48159-122">El ejemplo anterior solo debe emplearse para confirmar la configuración.</span><span class="sxs-lookup"><span data-stu-id="48159-122">The preceding sample should only be used to confirm your configuration.</span></span> <span data-ttu-id="48159-123">Más adelante en este documento se ofrecen ejemplos válidos de pruebas.</span><span class="sxs-lookup"><span data-stu-id="48159-123">Valid examples of testing are covered later in this document.</span></span>

## <a name="testing-vms-running-windows"></a><span data-ttu-id="48159-124">Pruebas de máquinas virtuales que ejecutan WINDOWS:</span><span class="sxs-lookup"><span data-stu-id="48159-124">Testing VMs running WINDOWS:</span></span>

#### <a name="get-ntttcp-onto-the-vms"></a><span data-ttu-id="48159-125">Obtenga NTTTCP en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="48159-125">Get NTTTCP onto the VMs.</span></span>

<span data-ttu-id="48159-126">Descargue la versión más reciente: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span><span class="sxs-lookup"><span data-stu-id="48159-126">Download the latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span></span>

<span data-ttu-id="48159-127">Si no se encuentra en esa página, realice esta búsqueda <https://www.bing.com/search?q=ntttcp+download>\< (debe ser el primer resultado).</span><span class="sxs-lookup"><span data-stu-id="48159-127">Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit</span></span>

<span data-ttu-id="48159-128">Considere la colocar NTTTCP en una carpeta independiente, como c:\\tools.</span><span class="sxs-lookup"><span data-stu-id="48159-128">Consider putting NTTTCP in separate folder, like c:\\tools</span></span>

#### <a name="allow-ntttcp-through-the-windows-firewall"></a><span data-ttu-id="48159-129">Procedimiento para permitir NTTTCP a través del Firewall de Windows</span><span class="sxs-lookup"><span data-stu-id="48159-129">Allow NTTTCP through the Windows firewall</span></span>
<span data-ttu-id="48159-130">En el RECEPTOR, cree una regla Permitir en el Firewall de Windows para permitir la recepción de tráfico NTTTCP.</span><span class="sxs-lookup"><span data-stu-id="48159-130">On the RECEIVER, create an Allow rule on the Windows Firewall to allow the NTTTCP traffic to arrive.</span></span> <span data-ttu-id="48159-131">Es más fácil permitir todo el programa NTTTCP por su nombre en lugar de determinados puertos TCP de entrada.</span><span class="sxs-lookup"><span data-stu-id="48159-131">It's easiest to allow the entire NTTTCP program by name rather than to allow specific TCP ports inbound.</span></span>

<span data-ttu-id="48159-132">Permita NTTTCP a través del Firewall de Windows de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="48159-132">Allow ntttcp through the Windows Firewall like this:</span></span>

<span data-ttu-id="48159-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="48159-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

<span data-ttu-id="48159-134">Por ejemplo, si ha copiado ntttcp.exe a la carpeta "c:\\tools", este sería el comando:</span><span class="sxs-lookup"><span data-stu-id="48159-134">For example, if you copied ntttcp.exe to the "c:\\tools" folder, this would be the command:</span></span> 

<span data-ttu-id="48159-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="48159-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

#### <a name="running-ntttcp-tests"></a><span data-ttu-id="48159-136">Ejecución de pruebas de NTTTCP</span><span class="sxs-lookup"><span data-stu-id="48159-136">Running NTTTCP tests</span></span>

<span data-ttu-id="48159-137">Inicie NTTTCP en el RECEPTOR (**se ejecuta desde CMD**, no desde PowerShell):</span><span class="sxs-lookup"><span data-stu-id="48159-137">Start NTTTCP on the RECEIVER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="48159-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span><span class="sxs-lookup"><span data-stu-id="48159-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span></span>

<span data-ttu-id="48159-139">Si la máquina virtual tiene cuatro núcleos y una dirección IP 10.0.0.4, sería similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="48159-139">If the VM has four cores and an IP address of 10.0.0.4, it would look like this:</span></span>

<span data-ttu-id="48159-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="48159-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span></span>


<span data-ttu-id="48159-141">Inicie NTTTCP en el REMITENTE (**se ejecuta desde CMD**, no desde PowerShell)::</span><span class="sxs-lookup"><span data-stu-id="48159-141">Start NTTTCP on the SENDER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="48159-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="48159-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span></span> 

<span data-ttu-id="48159-143">Espere a que se muestren los resultados.</span><span class="sxs-lookup"><span data-stu-id="48159-143">Wait for the results.</span></span>


## <a name="testing-vms-running-linux"></a><span data-ttu-id="48159-144">Pruebas de máquinas virtuales que ejecutan LINUX:</span><span class="sxs-lookup"><span data-stu-id="48159-144">Testing VMs running LINUX:</span></span>

<span data-ttu-id="48159-145">Use nttcp-for-linux.</span><span class="sxs-lookup"><span data-stu-id="48159-145">Use nttcp-for-linux.</span></span> <span data-ttu-id="48159-146">Está disponible en <https://github.com/Microsoft/ntttcp-for-linux>.</span><span class="sxs-lookup"><span data-stu-id="48159-146">It is available from <https://github.com/Microsoft/ntttcp-for-linux></span></span>

<span data-ttu-id="48159-147">En las máquinas virtuales Linux (REMITENTE y RECEPTOR), ejecute estos comandos para preparar ntttcp-for-linux en las máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="48159-147">On the Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:</span></span>

<span data-ttu-id="48159-148">CentOS: instalación de Git:</span><span class="sxs-lookup"><span data-stu-id="48159-148">CentOS - Install Git:</span></span>
``` bash
  yum install gcc -y  
  yum install git -y
```
<span data-ttu-id="48159-149">Ubuntu: instalación de Git:</span><span class="sxs-lookup"><span data-stu-id="48159-149">Ubuntu - Install Git:</span></span>
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
<span data-ttu-id="48159-150">Cree e instale en ambas:</span><span class="sxs-lookup"><span data-stu-id="48159-150">Make and Install on both:</span></span>
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

<span data-ttu-id="48159-151">Como en el ejemplo de Windows, supongamos que la IP del RECEPTOR Linux es 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="48159-151">As in the Windows example, we assume the Linux RECEIVER's IP is 10.0.0.4</span></span>

<span data-ttu-id="48159-152">Inicie ntttcp-for-linux en el RECEPTOR:</span><span class="sxs-lookup"><span data-stu-id="48159-152">Start NTTTCP-for-Linux on the RECEIVER:</span></span>

``` bash
ntttcp -r -t 300
```

<span data-ttu-id="48159-153">Y en el REMITENTE, ejecute:</span><span class="sxs-lookup"><span data-stu-id="48159-153">And on the SENDER, run:</span></span>

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
<span data-ttu-id="48159-154">Los valores predeterminados de duración de prueba están establecidos en 60 segundos si no hay ningún parámetro de tiempo.</span><span class="sxs-lookup"><span data-stu-id="48159-154">Test length defaults to 60 seconds if no time parameter is given</span></span>

## <a name="testing-between-vms-running-windows-and-linux"></a><span data-ttu-id="48159-155">Pruebas entre máquinas virtuales que ejecutan Windows y Linux:</span><span class="sxs-lookup"><span data-stu-id="48159-155">Testing between VMs running Windows and LINUX:</span></span>

<span data-ttu-id="48159-156">En estos escenarios, se debería habilitar el modo sin sincronización para que la prueba pueda ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="48159-156">On this scenarios we should enable the no-sync mode so the test can run.</span></span> <span data-ttu-id="48159-157">Para ello, use **-N flag** para Linux y **-ns flag** para Windows.</span><span class="sxs-lookup"><span data-stu-id="48159-157">This is done by using the **-N flag** for Linux, and **-ns flag** for Windows.</span></span>

#### <a name="from-linux-to-windows"></a><span data-ttu-id="48159-158">De Linux a Windows:</span><span class="sxs-lookup"><span data-stu-id="48159-158">From Linux to Windows:</span></span>

<span data-ttu-id="48159-159">Receptor<Windows>:</span><span class="sxs-lookup"><span data-stu-id="48159-159">Receiver <Windows>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

<span data-ttu-id="48159-160">Remitente<Linux> :</span><span class="sxs-lookup"><span data-stu-id="48159-160">Sender <Linux> :</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-to-linux"></a><span data-ttu-id="48159-161">De Windows a Linux:</span><span class="sxs-lookup"><span data-stu-id="48159-161">From Windows to Linux:</span></span>

<span data-ttu-id="48159-162">Receptor<Linux>:</span><span class="sxs-lookup"><span data-stu-id="48159-162">Receiver <Linux>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

<span data-ttu-id="48159-163">Remitente<Windows>:</span><span class="sxs-lookup"><span data-stu-id="48159-163">Sender <Windows>:</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a><span data-ttu-id="48159-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="48159-164">Next steps</span></span>
* <span data-ttu-id="48159-165">Dependiendo de los resultados, puede que haya espacio para [optimizar máquinas de rendimiento de red](virtual-network-optimize-network-bandwidth.md) para su escenario.</span><span class="sxs-lookup"><span data-stu-id="48159-165">Depending on results, there may be room to [Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.</span></span>
* <span data-ttu-id="48159-166">Más información sobre [Preguntas más frecuentes (P+F) acerca de Azure Virtual Network](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="48159-166">Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
