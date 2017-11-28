---
title: "el programa de instalación del controlador de aaaAzure N-series para Windows | Documentos de Microsoft"
description: "¿Cómo tooset los controladores de GPU NVIDIA para máquinas virtuales de N-series que ejecuta Windows en Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3950c34-9406-48ae-bcd9-c0418607b37d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/07/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2acce57d4f9eb1d02bf3bc0303bcb9690475698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a><span data-ttu-id="f7321-103">Instalación de controladores de GPU para máquinas virtuales de la serie N con Windows Server</span><span class="sxs-lookup"><span data-stu-id="f7321-103">Set up GPU drivers for N-series VMs running Windows Server</span></span>
<span data-ttu-id="f7321-104">tootake aprovechar las capacidades GPU de Hola de Azure N-series máquinas virtuales que ejecutan Windows Server 2016 o Windows Server 2012 R2, instalación de controladores de gráficos NVIDIA admitidos.</span><span class="sxs-lookup"><span data-stu-id="f7321-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="f7321-105">Este artículo proporciona pasos de instalación de controlador después de implementar una VM de la serie N.</span><span class="sxs-lookup"><span data-stu-id="f7321-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="f7321-106">También está disponible la información de instalación del controlador para las [máquinas virtuales Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7321-106">Driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="f7321-107">Para conocer las especificaciones básicas, las capacidades de almacenamiento y los detalles del disco, consulte [Tamaño de máquinas virtuales para GPU Windows](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7321-107">For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a><span data-ttu-id="f7321-108">Instalación del controlador</span><span class="sxs-lookup"><span data-stu-id="f7321-108">Driver installation</span></span>

1. <span data-ttu-id="f7321-109">Conectarse mediante Escritorio remoto tooeach VM N-series.</span><span class="sxs-lookup"><span data-stu-id="f7321-109">Connect by Remote Desktop tooeach N-series VM.</span></span>

2. <span data-ttu-id="f7321-110">Descargar, extraer e instalar a controladores de hello compatible para el sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="f7321-110">Download, extract, and install hello supported driver for your Windows operating system.</span></span>

<span data-ttu-id="f7321-111">En las máquinas virtuales de Azure NV, se requiere un reinicio después de la instalación del controlador.</span><span class="sxs-lookup"><span data-stu-id="f7321-111">On Azure NV VMs, a restart is required after driver installation.</span></span> <span data-ttu-id="f7321-112">En máquinas virtuales NC, no se requiere un reinicio.</span><span class="sxs-lookup"><span data-stu-id="f7321-112">On NC VMs, a restart is not required.</span></span>

## <a name="verify-driver-installation"></a><span data-ttu-id="f7321-113">Comprobación de la instalación del controlador</span><span class="sxs-lookup"><span data-stu-id="f7321-113">Verify driver installation</span></span>

<span data-ttu-id="f7321-114">Puede comprobar la instalación del controlador en el Administrador de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f7321-114">You can verify driver installation in Device Manager.</span></span> <span data-ttu-id="f7321-115">Hello en el ejemplo siguiente se muestra una configuración correcta de tarjeta de hello Tesla K80 en una máquina virtual NC de Azure.</span><span class="sxs-lookup"><span data-stu-id="f7321-115">hello following example shows successful configuration of hello Tesla K80 card on an Azure NC VM.</span></span>

![Propiedades del controlador de GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

<span data-ttu-id="f7321-117">Hola tooquery estado del dispositivo GPU, ejecute hello [smi nvidia](https://developer.nvidia.com/nvidia-system-management-interface) instalada con controlador Hola de utilidad de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="f7321-117">tooquery hello GPU device state, run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span>

1. <span data-ttu-id="f7321-118">Abra un símbolo del sistema y cambie toohello **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span><span class="sxs-lookup"><span data-stu-id="f7321-118">Open a command prompt and change toohello **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span></span>

2. <span data-ttu-id="f7321-119">Ejecute **nvidia-smi**.</span><span class="sxs-lookup"><span data-stu-id="f7321-119">Run **nvidia-smi**.</span></span> <span data-ttu-id="f7321-120">Si está instalado el controlador de hello verá toobelow similar de salida.</span><span class="sxs-lookup"><span data-stu-id="f7321-120">If hello driver is installed you will see output similar toobelow.</span></span> <span data-ttu-id="f7321-121">Tenga en cuenta que **GPU Util** muestra **0%** a menos que se está ejecutando actualmente una carga de trabajo GPU en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f7321-121">Note that **GPU-Util** shows **0%** unless you are currently running a GPU workload on hello VM.</span></span>

![Estado del dispositivo de NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a><span data-ttu-id="f7321-123">Red RDMA para máquinas virtuales NC24r</span><span class="sxs-lookup"><span data-stu-id="f7321-123">RDMA network for NC24r VMs</span></span>

<span data-ttu-id="f7321-124">Se puede habilitar la conectividad de red RDMA en máquinas virtuales de NC24r implementadas en hello mismo conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="f7321-124">RDMA network connectivity can be enabled on NC24r VMs deployed in hello same availability set.</span></span> <span data-ttu-id="f7321-125">Hola extensión HpcVmDrivers debe agregarse tooinstall controladores de dispositivos de red de Windows que habilitar la conectividad RDMA.</span><span class="sxs-lookup"><span data-stu-id="f7321-125">hello HpcVmDrivers extension must be added tooinstall Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="f7321-126">usar tooadd Hola VM extensión tooan NC24r VM, [Azure PowerShell](/powershell/azure/overview) cmdlets para el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f7321-126">tooadd hello VM extension tooan NC24r VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets for Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="f7321-127">Actualmente, solo en Windows Server 2012 R2 es compatible con red RDMA de hello en máquinas virtuales de NC24r.</span><span class="sxs-lookup"><span data-stu-id="f7321-127">Currently, only Windows Server 2012 R2 supports hello RDMA network on NC24r VMs.</span></span>
> 

<span data-ttu-id="f7321-128">extensión de HpcVMDrivers versión 1.1 más reciente de tooinstall de hello en una máquina virtual compatible con RDMA existente había denominada myVM en la región del oeste de Estados Unidos de hello:</span><span class="sxs-lookup"><span data-stu-id="f7321-128">tooinstall hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in hello West US region:</span></span>
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="f7321-129">Para obtener más información, consulte [Características y extensiones de las máquinas virtuales para Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7321-129">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="f7321-130">red de Hello RDMA admite el tráfico de interfaz de paso de mensajes (MPI) para aplicaciones que se ejecutan con [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) o Intel MPI 5.x.</span><span class="sxs-lookup"><span data-stu-id="f7321-130">hello RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="f7321-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f7321-131">Next steps</span></span>

* <span data-ttu-id="f7321-132">Para obtener más información sobre Hola GPU NVIDIA Hola N-series las máquinas virtuales, vea:</span><span class="sxs-lookup"><span data-stu-id="f7321-132">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="f7321-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (para máquinas virtuales de Azure NC)</span><span class="sxs-lookup"><span data-stu-id="f7321-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="f7321-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (para máquinas virtuales de Azure NV)</span><span class="sxs-lookup"><span data-stu-id="f7321-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="f7321-135">Los desarrolladores que crean aplicaciones y acelerados por GPU para hello NVIDIA Tesla GPU también pueden descargar e instalar hello 8 del Kit de herramientas de CUDA para [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) o [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span><span class="sxs-lookup"><span data-stu-id="f7321-135">Developers building GPU-accelerated applications for hello NVIDIA Tesla GPUs can also download and install hello CUDA Toolkit 8 for [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) or [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span></span> <span data-ttu-id="f7321-136">Para obtener más información, vea hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span><span class="sxs-lookup"><span data-stu-id="f7321-136">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span></span>


