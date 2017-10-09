---
title: "tamaños de VM de Linux aaaAzure - GPU | Documentos de Microsoft"
description: "Muestra los tamaños GPU con optimización para diferentes de hello disponibles para máquinas virtuales de Linux en Azure."
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
ms.openlocfilehash: e98f720499be37df4048aeb513aa4f6b187b7335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="gpu-linux-vm-sizes"></a><span data-ttu-id="78eb4-103">Tamaño de máquinas virtuales optimizados para GPU Linux</span><span class="sxs-lookup"><span data-stu-id="78eb4-103">GPU Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

<span data-ttu-id="78eb4-104">Para los pasos de instalación y verificación de controladores, consulte [el programa de instalación del controlador de N-series para Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="78eb4-104">For driver installation and verification steps, see [N-series driver setup for Linux](n-series-driver-setup.md).</span></span>

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* <span data-ttu-id="78eb4-105">No se recomienda instalar X server u otros sistemas que usan el controlador de estilo nouveau de hello en máquinas virtuales de NC Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="78eb4-105">We don't recommend installing X server or other systems that use hello nouveau driver on Ubuntu NC VMs.</span></span> <span data-ttu-id="78eb4-106">Antes de instalar controladores de GPU NVIDIA, necesita controladores de estilo nouveau hello toodisable.</span><span class="sxs-lookup"><span data-stu-id="78eb4-106">Before installing NVIDIA GPU drivers, you need toodisable hello nouveau driver.</span></span>  

## <a name="other-sizes"></a><span data-ttu-id="78eb4-107">Otros tamaños</span><span class="sxs-lookup"><span data-stu-id="78eb4-107">Other sizes</span></span>
- [<span data-ttu-id="78eb4-108">Uso general</span><span class="sxs-lookup"><span data-stu-id="78eb4-108">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="78eb4-109">Proceso optimizado</span><span class="sxs-lookup"><span data-stu-id="78eb4-109">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="78eb4-110">Memoria optimizada</span><span class="sxs-lookup"><span data-stu-id="78eb4-110">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="78eb4-111">Almacenamiento optimizado</span><span class="sxs-lookup"><span data-stu-id="78eb4-111">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="78eb4-112">Proceso de alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="78eb4-112">High performance compute</span></span>](sizes-hpc.md)

## <a name="next-steps"></a><span data-ttu-id="78eb4-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="78eb4-113">Next steps</span></span>
<span data-ttu-id="78eb4-114">Obtenga más información sobre cómo las [unidades de proceso de Azure (ACU)](acu.md) pueden ayudarlo a comparar el rendimiento en los distintos SKU de Azure.</span><span class="sxs-lookup"><span data-stu-id="78eb4-114">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>