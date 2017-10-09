---
title: "tamaños de aaaLinux VM en Azure | Documentos de Microsoft"
description: "Muestra los tamaños diferentes de hello disponibles para máquinas virtuales de Linux en Azure."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: da681171-f045-4c80-a5a9-d8bd47964673
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 56cbe0a0d7d34def07636edba74c4c699e336012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a>Tamaños de las máquinas virtuales Linux en Azure
Este artículo describe los tamaños disponibles de Hola y opciones para hello máquinas virtuales de Azure puede usar toorun sus cargas de trabajo y aplicaciones de Linux. También proporciona toobe de consideraciones de implementación en cuenta cuando planee toouse estos recursos. Este artículo también está disponible para [máquinas virtuales Windows](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


| Tipo                     | Tamaños           |    Descripción       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Uso general](sizes-general.md)          | Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7,  | Uso equilibrado de la CPU en proporción de memoria. Ideal para pruebas y desarrollo, las bases de datos pequeñas toomedium y servidores web de tráfico de toomedium baja. |
| [Proceso optimizado](sizes-compute.md)        | Fs, F             | Uso elevado de la CPU en proporción de memoria. Bueno para servidores web de tráfico medio, aplicaciones de red, procesos por lotes y servidores de aplicaciones.        |
| [Memoria optimizada](sizes-memory.md)         | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Memoria alta en proporción de CPU. Excelente para servidores de base de datos relacional, las cachés de toolarge intermedio y análisis en memoria.                 |
| [Almacenamiento optimizado](sizes-storage.md)        | LS                | Alto rendimiento de disco y E/S. Perfecto para bases de datos SQL y NoSQL y macrodatos.                                                         |
| [GPU](sizes-gpu.md)            | NV, NC            | Máquinas virtuales especializadas específicas para la representación de gráficos pesados y la edición de vídeo. Están disponibles con uno o varios GPU.       |
| [Proceso de alto rendimiento](sizes-hpc.md) | H, A8-11          | Nuestras máquinas virtuales de CPU más rápidas y eficaces con interfaces de red de alto rendimiento opcionales (RDMA). 

<br>

- Para obtener información sobre los precios de saludo diversos tamaños, vea [precios de máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux). 
- Para ver la disponibilidad de los tamaños de máquina virtual en las regiones de Azure, consulte [Productos disponibles por región](https://azure.microsoft.com/regions/services/).
- límites generales de toosee en máquinas virtuales de Azure, consulte [suscripción de Azure y límites de servicio, cuotas y restricciones](../../azure-subscription-service-limits.md).
- Obtenga más información sobre cómo las [unidades de proceso de Azure (ACU)](../windows/acu.md) pueden ayudarlo a comparar el rendimiento en los distintos SKU de Azure.


## <a name="rest-api"></a>API de REST

Para obtener información sobre el uso de tooquery de API de REST de Hola para tamaños de máquinas virtuales, vea Hola siguiente:

- [Lista de tamaños de máquina virtual disponibles para cambio de tamaño](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [Lista de tamaños de máquina virtual disponibles para una suscripción](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [Lista de tamaños de máquina virtual disponibles en un conjunto de disponibilidad](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a>ACU

Obtenga más información sobre cómo las [unidades de proceso de Azure (ACU)](acu.md) pueden ayudarlo a comparar el rendimiento en los distintos SKU de Azure.

## <a name="next-steps"></a>Pasos siguientes

Más información acerca de los diferentes tamaños VM de Hola que están disponibles:
- [Uso general](sizes-general.md)
- [Proceso optimizado](sizes-compute.md)
- [Memoria optimizada](sizes-memory.md)
- [Almacenamiento optimizado](sizes-storage.md)
- [GPU](sizes-gpu.md)
- [Proceso de alto rendimiento](sizes-hpc.md)



