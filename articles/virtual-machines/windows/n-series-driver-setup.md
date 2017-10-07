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
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a>Instalación de controladores de GPU para máquinas virtuales de la serie N con Windows Server
tootake aprovechar las capacidades GPU de Hola de Azure N-series máquinas virtuales que ejecutan Windows Server 2016 o Windows Server 2012 R2, instalación de controladores de gráficos NVIDIA admitidos. Este artículo proporciona pasos de instalación de controlador después de implementar una VM de la serie N. También está disponible la información de instalación del controlador para las [máquinas virtuales Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Para conocer las especificaciones básicas, las capacidades de almacenamiento y los detalles del disco, consulte [Tamaño de máquinas virtuales para GPU Windows](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a>Instalación del controlador

1. Conectarse mediante Escritorio remoto tooeach VM N-series.

2. Descargar, extraer e instalar a controladores de hello compatible para el sistema operativo Windows.

En las máquinas virtuales de Azure NV, se requiere un reinicio después de la instalación del controlador. En máquinas virtuales NC, no se requiere un reinicio.

## <a name="verify-driver-installation"></a>Comprobación de la instalación del controlador

Puede comprobar la instalación del controlador en el Administrador de dispositivos. Hello en el ejemplo siguiente se muestra una configuración correcta de tarjeta de hello Tesla K80 en una máquina virtual NC de Azure.

![Propiedades del controlador de GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

Hola tooquery estado del dispositivo GPU, ejecute hello [smi nvidia](https://developer.nvidia.com/nvidia-system-management-interface) instalada con controlador Hola de utilidad de línea de comandos.

1. Abra un símbolo del sistema y cambie toohello **C:\Program Files\NVIDIA Corporation\NVSMI** directory.

2. Ejecute **nvidia-smi**. Si está instalado el controlador de hello verá toobelow similar de salida. Tenga en cuenta que **GPU Util** muestra **0%** a menos que se está ejecutando actualmente una carga de trabajo GPU en hello máquina virtual.

![Estado del dispositivo de NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a>Red RDMA para máquinas virtuales NC24r

Se puede habilitar la conectividad de red RDMA en máquinas virtuales de NC24r implementadas en hello mismo conjunto de disponibilidad. Hola extensión HpcVmDrivers debe agregarse tooinstall controladores de dispositivos de red de Windows que habilitar la conectividad RDMA. usar tooadd Hola VM extensión tooan NC24r VM, [Azure PowerShell](/powershell/azure/overview) cmdlets para el Administrador de recursos de Azure.

> [!NOTE]
> Actualmente, solo en Windows Server 2012 R2 es compatible con red RDMA de hello en máquinas virtuales de NC24r.
> 

extensión de HpcVMDrivers versión 1.1 más reciente de tooinstall de hello en una máquina virtual compatible con RDMA existente había denominada myVM en la región del oeste de Estados Unidos de hello:
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  Para obtener más información, consulte [Características y extensiones de las máquinas virtuales para Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

red de Hello RDMA admite el tráfico de interfaz de paso de mensajes (MPI) para aplicaciones que se ejecutan con [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) o Intel MPI 5.x. 


## <a name="next-steps"></a>Pasos siguientes

* Para obtener más información sobre Hola GPU NVIDIA Hola N-series las máquinas virtuales, vea:
    * [NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (para máquinas virtuales de Azure NC)
    * [NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (para máquinas virtuales de Azure NV)

* Los desarrolladores que crean aplicaciones y acelerados por GPU para hello NVIDIA Tesla GPU también pueden descargar e instalar hello 8 del Kit de herramientas de CUDA para [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) o [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe). Para obtener más información, vea hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).


