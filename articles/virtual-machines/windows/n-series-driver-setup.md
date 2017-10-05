---
title: "Instalación del controlador de la serie N de Azure para Windows | Microsoft Docs"
description: "Instalación de controladores de GPU de NVIDIA para máquinas virtuales de la serie N que se ejecutan en Windows en Azure"
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
ms.openlocfilehash: b480d10df777a2757c073ff77e1845d33d63163a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a><span data-ttu-id="9fed1-103">Instalación de controladores de GPU para máquinas virtuales de la serie N con Windows Server</span><span class="sxs-lookup"><span data-stu-id="9fed1-103">Set up GPU drivers for N-series VMs running Windows Server</span></span>
<span data-ttu-id="9fed1-104">Para aprovechar las funcionalidades de GPU de las máquinas virtuales de la serie N de Azure que ejecutan Windows Server 2016 o Windows Server 2012 R2, instale los controladores de gráficos de NVIDIA compatibles.</span><span class="sxs-lookup"><span data-stu-id="9fed1-104">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="9fed1-105">Este artículo proporciona pasos de instalación de controlador después de implementar una VM de la serie N.</span><span class="sxs-lookup"><span data-stu-id="9fed1-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="9fed1-106">También está disponible la información de instalación del controlador para las [máquinas virtuales Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9fed1-106">Driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="9fed1-107">Para conocer las especificaciones básicas, las capacidades de almacenamiento y los detalles del disco, consulte [Tamaño de máquinas virtuales para GPU Windows](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9fed1-107">For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a><span data-ttu-id="9fed1-108">Instalación del controlador</span><span class="sxs-lookup"><span data-stu-id="9fed1-108">Driver installation</span></span>

1. <span data-ttu-id="9fed1-109">Conéctese mediante Escritorio remoto a cada máquina virtual de la serie N.</span><span class="sxs-lookup"><span data-stu-id="9fed1-109">Connect by Remote Desktop to each N-series VM.</span></span>

2. <span data-ttu-id="9fed1-110">Descargue, extraiga e instale el controlador compatible con su sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="9fed1-110">Download, extract, and install the supported driver for your Windows operating system.</span></span>

<span data-ttu-id="9fed1-111">En las máquinas virtuales de Azure NV, se requiere un reinicio después de la instalación del controlador.</span><span class="sxs-lookup"><span data-stu-id="9fed1-111">On Azure NV VMs, a restart is required after driver installation.</span></span> <span data-ttu-id="9fed1-112">En máquinas virtuales NC, no se requiere un reinicio.</span><span class="sxs-lookup"><span data-stu-id="9fed1-112">On NC VMs, a restart is not required.</span></span>

## <a name="verify-driver-installation"></a><span data-ttu-id="9fed1-113">Comprobación de la instalación del controlador</span><span class="sxs-lookup"><span data-stu-id="9fed1-113">Verify driver installation</span></span>

<span data-ttu-id="9fed1-114">Puede comprobar la instalación del controlador en el Administrador de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="9fed1-114">You can verify driver installation in Device Manager.</span></span> <span data-ttu-id="9fed1-115">En el ejemplo siguiente se muestra una configuración correcta de la tarjeta Tesla K80 en una máquina virtual de Azure NC.</span><span class="sxs-lookup"><span data-stu-id="9fed1-115">The following example shows successful configuration of the Tesla K80 card on an Azure NC VM.</span></span>

![Propiedades del controlador de GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

<span data-ttu-id="9fed1-117">Para consultar el estado del dispositivo de GPU, ejecute la utilidad de línea de comandos [smi nvidia](https://developer.nvidia.com/nvidia-system-management-interface) que se instala con el controlador.</span><span class="sxs-lookup"><span data-stu-id="9fed1-117">To query the GPU device state, run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span>

1. <span data-ttu-id="9fed1-118">Abra un símbolo del sistema y cambie al directorio **C:\Program Files\NVIDIA Corporation\NVSMI**.</span><span class="sxs-lookup"><span data-stu-id="9fed1-118">Open a command prompt and change to the **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span></span>

2. <span data-ttu-id="9fed1-119">Ejecute **nvidia-smi**.</span><span class="sxs-lookup"><span data-stu-id="9fed1-119">Run **nvidia-smi**.</span></span> <span data-ttu-id="9fed1-120">Si el controlador está instalado, obtendrá un resultado parecido al siguiente.</span><span class="sxs-lookup"><span data-stu-id="9fed1-120">If the driver is installed you will see output similar to below.</span></span> <span data-ttu-id="9fed1-121">Tenga en cuenta que **GPU-Util** muestra **0 %** a no ser que esté ejecutando actualmente una carga de trabajo de la GPU en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9fed1-121">Note that **GPU-Util** shows **0%** unless you are currently running a GPU workload on the VM.</span></span>

![Estado del dispositivo de NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a><span data-ttu-id="9fed1-123">Red RDMA para máquinas virtuales NC24r</span><span class="sxs-lookup"><span data-stu-id="9fed1-123">RDMA network for NC24r VMs</span></span>

<span data-ttu-id="9fed1-124">La conectividad de red RDMA puede habilitarse en máquinas virtuales NC24r implementadas en el mismo conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="9fed1-124">RDMA network connectivity can be enabled on NC24r VMs deployed in the same availability set.</span></span> <span data-ttu-id="9fed1-125">En las máquinas virtuales compatibles con RDMA, es necesario agregar la extensión HpcVmDrivers a las máquinas virtuales para instalar los controladores de dispositivos de red de Windows necesarios para la conectividad RDMA.</span><span class="sxs-lookup"><span data-stu-id="9fed1-125">The HpcVmDrivers extension must be added to install Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="9fed1-126">Para agregar la extensión de máquina virtual a una máquina virtual NC24r, puede usar los cmdlets de [Azure PowerShell](/powershell/azure/overview) para Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9fed1-126">To add the VM extension to an NC24r VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets for Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="9fed1-127">Actualmente, solo Windows Server 2012 R2 es compatible con la red RDMA en máquinas virtuales NC24r.</span><span class="sxs-lookup"><span data-stu-id="9fed1-127">Currently, only Windows Server 2012 R2 supports the RDMA network on NC24r VMs.</span></span>
> 

<span data-ttu-id="9fed1-128">Para instalar la versión más reciente de la extensión HpcVMDrivers 1.1 en una máquina virtual compatible con RDMA existente denominada "myVM" en la región de oeste de EE. UU.:</span><span class="sxs-lookup"><span data-stu-id="9fed1-128">To install the latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in the West US region:</span></span>
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="9fed1-129">Para obtener más información, consulte [Características y extensiones de las máquinas virtuales para Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9fed1-129">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="9fed1-130">Ahora, la red RDMA admite el tráfico de interfaz de paso de mensajes (MPI) para aplicaciones que se ejecutan con [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) o Intel MPI 5.x.</span><span class="sxs-lookup"><span data-stu-id="9fed1-130">The RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="9fed1-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9fed1-131">Next steps</span></span>

* <span data-ttu-id="9fed1-132">Para obtener más información sobre las GPU de NVIDIA en las máquinas virtuales de la serie N, consulte:</span><span class="sxs-lookup"><span data-stu-id="9fed1-132">For more information about the NVIDIA GPUs on the N-series VMs, see:</span></span>
    * <span data-ttu-id="9fed1-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (para máquinas virtuales de Azure NC)</span><span class="sxs-lookup"><span data-stu-id="9fed1-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="9fed1-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (para máquinas virtuales de Azure NV)</span><span class="sxs-lookup"><span data-stu-id="9fed1-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="9fed1-135">Los desarrolladores que creen aplicaciones con aceleración por GPU para las GPU Tesla de NVIDIA también pueden descargar e instalar la CUDA Toolkit 8 para [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) o [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span><span class="sxs-lookup"><span data-stu-id="9fed1-135">Developers building GPU-accelerated applications for the NVIDIA Tesla GPUs can also download and install the CUDA Toolkit 8 for [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) or [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span></span> <span data-ttu-id="9fed1-136">Para obtener más información, consulte la [guía de instalación de CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span><span class="sxs-lookup"><span data-stu-id="9fed1-136">For more information, see the [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span></span>


