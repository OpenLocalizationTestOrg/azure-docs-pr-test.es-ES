---
title: "Tamaños de las máquinas virtuales Linux en Azure: GPU | Microsoft Docs"
description: "Enumera los tamaños diferentes optimizados para GPU disponibles para las máquinas virtuales Linux en Azure."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 5c9bf89feba519147b07f2810fe4da882664e89e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="gpu-linux-vm-sizes"></a><span data-ttu-id="9c7f6-103">Tamaño de máquinas virtuales optimizados para GPU Linux</span><span class="sxs-lookup"><span data-stu-id="9c7f6-103">GPU Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

<span data-ttu-id="9c7f6-104">Para los pasos de instalación y verificación de controladores, consulte [el programa de instalación del controlador de N-series para Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="9c7f6-104">For driver installation and verification steps, see [N-series driver setup for Linux](n-series-driver-setup.md).</span></span>

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* <span data-ttu-id="9c7f6-105">No se recomienda instalar X Server u otros sistemas que usan el controlador nouveau en máquinas virtuales Ubuntu NC.</span><span class="sxs-lookup"><span data-stu-id="9c7f6-105">We don't recommend installing X server or other systems that use the nouveau driver on Ubuntu NC VMs.</span></span> <span data-ttu-id="9c7f6-106">Antes de instalar controladores de GPU NVIDIA, debe deshabilitar al controlador nouveau.</span><span class="sxs-lookup"><span data-stu-id="9c7f6-106">Before installing NVIDIA GPU drivers, you need to disable the nouveau driver.</span></span>  

## <a name="other-sizes"></a><span data-ttu-id="9c7f6-107">Otros tamaños</span><span class="sxs-lookup"><span data-stu-id="9c7f6-107">Other sizes</span></span>
- [<span data-ttu-id="9c7f6-108">Uso general</span><span class="sxs-lookup"><span data-stu-id="9c7f6-108">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="9c7f6-109">Proceso optimizado</span><span class="sxs-lookup"><span data-stu-id="9c7f6-109">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="9c7f6-110">Memoria optimizada</span><span class="sxs-lookup"><span data-stu-id="9c7f6-110">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="9c7f6-111">Almacenamiento optimizado</span><span class="sxs-lookup"><span data-stu-id="9c7f6-111">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="9c7f6-112">Proceso de alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="9c7f6-112">High performance compute</span></span>](sizes-hpc.md)

## <a name="next-steps"></a><span data-ttu-id="9c7f6-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9c7f6-113">Next steps</span></span>
<span data-ttu-id="9c7f6-114">Obtenga más información sobre cómo las [unidades de proceso de Azure (ACU)](acu.md) pueden ayudarlo a comparar el rendimiento en los distintos SKU de Azure.</span><span class="sxs-lookup"><span data-stu-id="9c7f6-114">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>