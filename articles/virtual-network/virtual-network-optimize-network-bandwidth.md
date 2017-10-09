---
title: rendimiento de red VM aaaOptimize | Documentos de Microsoft
description: "Obtenga información acerca de cómo el rendimiento de la red de toooptimize máquina virtual de Azure."
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
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: a5cff2d0ab6e3553c3f90d99629521a431477de0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a><span data-ttu-id="a79db-103">Optimización del rendimiento de red en las máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="a79db-103">Optimize network throughput for Azure virtual machines</span></span>

<span data-ttu-id="a79db-104">Las máquinas virtuales de Azure (VM) tienen una configuración de red predeterminada que se puede optimizar para mejorar aún más el rendimiento de la red.</span><span class="sxs-lookup"><span data-stu-id="a79db-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span></span> <span data-ttu-id="a79db-105">Este artículo describe cómo toooptimize red de rendimiento para Windows de Microsoft Azure y máquinas virtuales de Linux, incluidas las distribuciones principales como Ubuntu, CentOS y Red Hat.</span><span class="sxs-lookup"><span data-stu-id="a79db-105">This article describes how toooptimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS and Red Hat.</span></span>

## <a name="windows-vm"></a><span data-ttu-id="a79db-106">Máquina virtual de Windows</span><span class="sxs-lookup"><span data-stu-id="a79db-106">Windows VM</span></span>

<span data-ttu-id="a79db-107">Si la máquina virtual de Windows es compatible con [Accelerated redes](virtual-network-create-vm-accelerated-networking.md), habilitar esta característica sería la configuración óptima de hello para el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="a79db-107">If your Windows VM is supported with [Accelerated Networking](virtual-network-create-vm-accelerated-networking.md), enabling that feature would be hello optimal configuration for throughput.</span></span> <span data-ttu-id="a79db-108">En el caso de otras máquinas virtuales Windows, el uso de escalado en el lado de la recepción (RSS) pueden logar un rendimiento máximo mayor que las que no lo usan.</span><span class="sxs-lookup"><span data-stu-id="a79db-108">For all other Windows VMs, using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span></span> <span data-ttu-id="a79db-109">En las máquinas virtuales Windows, RSS se puede deshabilitar de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a79db-109">RSS may be disabled by default in a Windows VM.</span></span> <span data-ttu-id="a79db-110">Completar hello siguiendo los pasos toodetermine si RSS está habilitado y tooenable si está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="a79db-110">Complete hello following steps toodetermine whether RSS is enabled and tooenable it if it's disabled.</span></span>

1. <span data-ttu-id="a79db-111">Escriba hello `Get-NetAdapterRss` toosee de comandos de PowerShell si RSS está habilitado para un adaptador de red.</span><span class="sxs-lookup"><span data-stu-id="a79db-111">Enter hello `Get-NetAdapterRss` PowerShell command toosee if RSS is enabled for a network adapter.</span></span> <span data-ttu-id="a79db-112">Hola siguiendo la salida de ejemplo devuelto de hello `Get-NetAdapterRss`, RSS no está habilitado.</span><span class="sxs-lookup"><span data-stu-id="a79db-112">In hello following example output returned from hello `Get-NetAdapterRss`, RSS is not enabled.</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. <span data-ttu-id="a79db-113">Escriba Hola después tooenable comando RSS:</span><span class="sxs-lookup"><span data-stu-id="a79db-113">Enter hello following command tooenable RSS:</span></span>

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    <span data-ttu-id="a79db-114">comando de Hello anterior no tiene una salida.</span><span class="sxs-lookup"><span data-stu-id="a79db-114">hello previous command does not have an output.</span></span> <span data-ttu-id="a79db-115">comando Hello cambia configuración de NIC, provocar la pérdida de conectividad temporal de aproximadamente un minuto.</span><span class="sxs-lookup"><span data-stu-id="a79db-115">hello command changed NIC settings, causing temporary connectivity loss for about one minute.</span></span> <span data-ttu-id="a79db-116">Aparece un cuadro de diálogo volviendo a conectarse durante la pérdida de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="a79db-116">A Reconnecting dialog box appears during hello connectivity loss.</span></span> <span data-ttu-id="a79db-117">Normalmente se restaure la conectividad después tercer intento de Hola.</span><span class="sxs-lookup"><span data-stu-id="a79db-117">Connectivity is typically restored after hello third attempt.</span></span>
3. <span data-ttu-id="a79db-118">Confirme que RSS está habilitado en hello VM escribiendo hello `Get-NetAdapterRss` comando nuevo.</span><span class="sxs-lookup"><span data-stu-id="a79db-118">Confirm that RSS is enabled in hello VM by entering hello `Get-NetAdapterRss` command again.</span></span> <span data-ttu-id="a79db-119">Si se realiza correctamente, se devuelve la siguiente salida de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="a79db-119">If successful, hello following example output is returned:</span></span>

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a><span data-ttu-id="a79db-120">Máquina virtual de Linux</span><span class="sxs-lookup"><span data-stu-id="a79db-120">Linux VM</span></span>

<span data-ttu-id="a79db-121">De manera predeterminada, en las máquinas virtuales Linux de Azure RSS está siempre habilitado.</span><span class="sxs-lookup"><span data-stu-id="a79db-121">RSS is always enabled by default in an Azure Linux VM.</span></span> <span data-ttu-id="a79db-122">Núcleos Linux publicados a partir de enero de 2017 incluyen nuevas opciones de optimización de red que permiten un rendimiento de red de VM de Linux tooachieve superior.</span><span class="sxs-lookup"><span data-stu-id="a79db-122">Linux kernels released since January, 2017 include new network optimization options that enable a Linux VM tooachieve higher network throughput.</span></span>

### <a name="ubuntu"></a><span data-ttu-id="a79db-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a79db-123">Ubuntu</span></span>

<span data-ttu-id="a79db-124">Optimización de la orden tooget hello, actualice primero toohello admitido la última versión, a partir de junio de 2017, que es:</span><span class="sxs-lookup"><span data-stu-id="a79db-124">In order tooget hello optimization, first update toohello latest supported version, as of June 2017, which is:</span></span>
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
<span data-ttu-id="a79db-125">Una vez completada la actualización de hello, escriba Hola después del núcleo de comandos tooget hello más reciente:</span><span class="sxs-lookup"><span data-stu-id="a79db-125">After hello update is complete, enter hello following commands tooget hello latest kernel:</span></span>

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

<span data-ttu-id="a79db-126">Comando opcional:</span><span class="sxs-lookup"><span data-stu-id="a79db-126">Optional command:</span></span>

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a><span data-ttu-id="a79db-127">Kernel de versión preliminar de Azure de Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a79db-127">Ubuntu Azure Preview kernel</span></span>
> [!WARNING]
> <span data-ttu-id="a79db-128">Esta vista previa de Linux de Azure no puede tener el kernel Hola de mismo nivel de disponibilidad y confiabilidad como imágenes de Marketplace y núcleos que por lo general son versión de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="a79db-128">This Azure Linux Preview kernel may not have hello same level of availability and reliability as Marketplace images and kernels that are in general availability release.</span></span> <span data-ttu-id="a79db-129">características de Hello no se admiten, pueden haber limitado las capacidades y no pueden ser tan confiable como núcleo de hello predeterminado.</span><span class="sxs-lookup"><span data-stu-id="a79db-129">hello feature is not supported, may have constrained capabilities, and may not be as reliable as hello default kernel.</span></span> <span data-ttu-id="a79db-130">No utilice este kernel para cargas de trabajo de producción.</span><span class="sxs-lookup"><span data-stu-id="a79db-130">Do not use this kernel for production workloads.</span></span>

<span data-ttu-id="a79db-131">Significativa al rendimiento se puede lograr mediante la instalación de hello propuesto kernel de Linux de Azure.</span><span class="sxs-lookup"><span data-stu-id="a79db-131">Significant throughput performance can be achieved by installing hello proposed Azure Linux kernel.</span></span> <span data-ttu-id="a79db-132">tootry este kernel, agregue esta línea too/etc/apt/sources.list</span><span class="sxs-lookup"><span data-stu-id="a79db-132">tootry this kernel, add this line too/etc/apt/sources.list</span></span>

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

<span data-ttu-id="a79db-133">Luego, ejecute estos comandos como raíz.</span><span class="sxs-lookup"><span data-stu-id="a79db-133">Then run these commands as root.</span></span>
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a><span data-ttu-id="a79db-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="a79db-134">CentOS</span></span>

<span data-ttu-id="a79db-135">Optimización de la orden tooget hello, actualice primero toohello admitido la última versión, a partir de julio de 2017, que es:</span><span class="sxs-lookup"><span data-stu-id="a79db-135">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
<span data-ttu-id="a79db-136">Una vez completada la actualización de hello, instalación Hola servicios de integración de Linux (LIS) más reciente.</span><span class="sxs-lookup"><span data-stu-id="a79db-136">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="a79db-137">optimización del rendimiento de Hello es en LIS, desde 4.2.2-2.</span><span class="sxs-lookup"><span data-stu-id="a79db-137">hello throughput optimization is in LIS, starting from 4.2.2-2.</span></span> <span data-ttu-id="a79db-138">Escriba Hola después comandos tooinstall LIS:</span><span class="sxs-lookup"><span data-stu-id="a79db-138">Enter hello following commands tooinstall LIS:</span></span>

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a><span data-ttu-id="a79db-139">Red Hat</span><span class="sxs-lookup"><span data-stu-id="a79db-139">Red Hat</span></span>

<span data-ttu-id="a79db-140">Optimización de la orden tooget hello, actualice primero toohello admitido la última versión, a partir de julio de 2017, que es:</span><span class="sxs-lookup"><span data-stu-id="a79db-140">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
<span data-ttu-id="a79db-141">Una vez completada la actualización de hello, instalación Hola servicios de integración de Linux (LIS) más reciente.</span><span class="sxs-lookup"><span data-stu-id="a79db-141">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="a79db-142">optimización del rendimiento de Hello es en LIS, desde 4.2.</span><span class="sxs-lookup"><span data-stu-id="a79db-142">hello throughput optimization is in LIS, starting from 4.2.</span></span> <span data-ttu-id="a79db-143">Escriba Hola después toodownload de comandos e instalar LIS:</span><span class="sxs-lookup"><span data-stu-id="a79db-143">Enter hello following commands toodownload and install LIS:</span></span>

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

<span data-ttu-id="a79db-144">Obtener más información sobre Linux Integration Services versión 4.2 para Hyper-V mediante la visualización hello [página de descarga de](https://www.microsoft.com/download/details.aspx?id=55106).</span><span class="sxs-lookup"><span data-stu-id="a79db-144">Learn more about Linux Integration Services Version 4.2 for Hyper-V by viewing hello [download page](https://www.microsoft.com/download/details.aspx?id=55106).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a79db-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a79db-145">Next steps</span></span>
* <span data-ttu-id="a79db-146">Ahora que hello VM está optimizada, vea el resultado de hello con [pruebas VM de Azure de ancho de banda/rendimiento](virtual-network-bandwidth-testing.md) para su escenario.</span><span class="sxs-lookup"><span data-stu-id="a79db-146">Now that hello VM is optimized, see hello result with [Bandwidth/Throughput testing Azure VM](virtual-network-bandwidth-testing.md) for your scenario.</span></span>
* <span data-ttu-id="a79db-147">Obtenga más información con las [Preguntas más frecuentes (P+F) acerca de Azure Virtual Network](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="a79db-147">Learn more with [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
