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
# <a name="gpu-linux-vm-sizes"></a>Tamaño de máquinas virtuales optimizados para GPU Linux

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

Para los pasos de instalación y verificación de controladores, consulte [el programa de instalación del controlador de N-series para Linux](n-series-driver-setup.md).

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* No se recomienda instalar X server u otros sistemas que usan el controlador de estilo nouveau de hello en máquinas virtuales de NC Ubuntu. Antes de instalar controladores de GPU NVIDIA, necesita controladores de estilo nouveau hello toodisable.  

## <a name="other-sizes"></a>Otros tamaños
- [Uso general](sizes-general.md)
- [Proceso optimizado](sizes-compute.md)
- [Memoria optimizada](sizes-memory.md)
- [Almacenamiento optimizado](sizes-storage.md)
- [Proceso de alto rendimiento](sizes-hpc.md)

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre cómo las [unidades de proceso de Azure (ACU)](acu.md) pueden ayudarlo a comparar el rendimiento en los distintos SKU de Azure.