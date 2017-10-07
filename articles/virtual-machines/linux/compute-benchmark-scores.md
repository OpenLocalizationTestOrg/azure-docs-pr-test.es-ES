---
title: "puntuaciones de la prueba comparativa de aaaCompute para máquinas virtuales de Linux | Documentos de Microsoft"
description: "Comparación de puntuaciones de pruebas comparativas de proceso de CoreMark para máquinas virtuales de Azure con Linux"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 93e812c1-79dd-40c5-b97b-aa79f5cd7d76
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: cynthn
ms.openlocfilehash: b2c1ca5fbd80cea030ac2cc22156c4e9444c6726
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="compute-benchmark-scores-for-linux-vms"></a>Puntuaciones de pruebas comparativas de proceso para máquinas virtuales Linux
Hola después de mostrar las puntuaciones de CoreMark prueba comparativa de proceso rendimiento de línea VM de alto rendimiento de Azure ejecutando Ubuntu. Las puntuaciones de pruebas comparativas de proceso también están disponibles para las [máquinas virtuales de Windows](../windows/compute-benchmark-scores.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="a-series---compute-intensive"></a>Serie A: de proceso intensivo
| Tamaño | vCPU | Nodos NUMA | CPU | Ejecuciones | Iteraciones/seg. | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A8 |8 |1 |Intel Xeon CPU E5-2670 0 a 2,6 GHz |179 |110 294 |554 |
| Standard_A9 |16 |2 |Intel Xeon CPU E5-2670 0 a 2,6 GHz |189 |210 816 |2126 |
| Standard_A10 |8 |1 |Intel Xeon CPU E5-2670 0 a 2,6 GHz |188 |110 025 |1045 |
| Standard_A11 |16 |2 |Intel Xeon CPU E5-2670 0 a 2,6 GHz |188 |210 727 |2073 |

## <a name="dv2-series"></a>Serie Dv2
| Tamaño | vCPU | Nodos NUMA | CPU | Ejecuciones | Iteraciones/seg. | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_D1_v2 |1 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |140 |14 852 |780 |
| Standard_D2_v2 |2 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |133 |29 467 |1863 |
| Standard_D3_v2 |4 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |139 |56 205 |1167 |
| Standard_D4_v2 |8 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |126 |108 543 |3446 |
| Standard_D5_v2 |16 |2 |Intel Xeon E5-2673 v3 a 2,4 GHz |126 |205 332 |9998 |
| Standard_D11_v2 |2 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |125 |28 598 |1510 |
| Standard_D12_v2 |4 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |131 |55 673 |1418 |
| Standard_D13_v2 |8 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |140 |107 986 |3089 |
| Standard_D14_v2 |16 |2 |Intel Xeon E5-2673 v3 a 2,4 GHz |140 |208 186 |8839 |
| Standard_D15_v2 |20 | |2 |Intel Xeon E5-2673 v3 a 2,4 GHz |28 |268 560 |4667 |

## <a name="f-series"></a>Serie F
| Tamaño | vCPU | Nodos NUMA | CPU | Ejecuciones | Iteraciones/seg. | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_F1 |1 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |154 |15 602 |787 |
| Standard_F2 |2 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |126 |29 519 |1233 |
| Standard_F4 |4 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |147 |58 709 |1227 |
| Standard_F8 |8 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |224 |112 772 |3006 |
| Standard_F16 |16 |2 |Intel Xeon E5-2673 v3 a 2,4 GHz |42 |218 571 |5113 |

## <a name="g-series"></a>Serie G
| Tamaño | vCPU | Nodos NUMA | CPU | Ejecuciones | Iteraciones/seg. | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_G1 |2 |1 |Intel Xeon E5-2698B v3 a 2 GHz |83 |31 310 |2891 |
| Standard_G2 |4 |1 |Intel Xeon E5-2698B v3 a 2 GHz |84 |60 112 |3537 |
| Standard_G3 |8 |1 |Intel Xeon E5-2698B v3 a 2 GHz |84 |107 522 |4537 |
| Standard_G4 |16 |1 |Intel Xeon E5-2698B v3 a 2 GHz |83 |195 116 |5024 |
| Standard_G5 |32 |2 |Intel Xeon E5-2698B v3 a 2 GHz |84 |360 329 |14 212 |

## <a name="gs-series"></a>Serie GS
| Tamaño | vCPU | Nodos NUMA | CPU | Ejecuciones | Iteraciones/seg. | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_GS1 |2 |1 |Intel Xeon E5-2698B v3 a 2 GHz |84 |28 613 |1884 |
| Standard_GS2 |4 |1 |Intel Xeon E5-2698B v3 a 2 GHz |83 |54 348 |3474 |
| Standard_GS3 |8 |1 |Intel Xeon E5-2698B v3 a 2 GHz |83 |104 564 |1834 |
| Standard_GS4 |16 |1 |Intel Xeon E5-2698B v3 a 2 GHz |84 |194 111 |4735 |
| Standard_GS5 |32 |2 |Intel Xeon E5-2698B v3 a 2 GHz |84 |357 396 |16 228 |

## <a name="h-series"></a>Serie H
| Tamaño | vCPU | Nodos NUMA | CPU | Ejecuciones | Iteraciones/seg. | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_H8 |8 |1 |Intel Xeon E5-2667 v3 a 3,2 GHz |28 |140 782 |2512 |
| Standard_H16 |16 |2 |Intel Xeon E5-2667 v3 a 3,2 GHz |35 |275 289 |7110 |
| Standard_H18m |8 |1 |Intel Xeon E5-2667 v3 a 3,2 GHz |28 |139 071 |3988 |
| Standard_H16m |16 |2 |Intel Xeon E5-2667 v3 a 3,2 GHz |28 |275 988 |6963 |
| Standard_H16r |16 |2 |Intel Xeon E5-2667 v3 a 3,2 GHz |28 |273 982 |6069 |
| Standard_H16mr |16 |2 |Intel Xeon E5-2667 v3 a 3,2 GHz |28 |274 523 |5698 |

## <a name="about-coremark"></a>Acerca de CoreMark
Los números de Linux se procesaron ejecutando [CoreMark](http://www.eembc.org/coremark/faq.php) en Ubuntu. CoreMark se configuró con hello número de subprocesos conjunto toohello de CPU virtuales y simultaneidad establece tooPThreads. número de destino de Hola de iteraciones se ajusta basándose en el rendimiento esperado tooprovide un tiempo de ejecución de al menos 20 segundos (suele ser mucho mayor). puntuación final Hola representa número de Hola de iteraciones completado dividido por el número de segundos que llevó toorun Hola Hola. Cada prueba se ejecutó al menos siete veces en cada máquina virtual. Pruebas (excepto para series_ H se ejecutaron en octubre de 2015 en varias máquinas virtuales en cada Hola región pública de Azure VM se admite en fecha hello de la ejecución.

## <a name="next-steps"></a>Pasos siguientes
* Para más información sobre las capacidades de almacenamiento, los detalles del disco y consideraciones adicionales para seleccionar tamaños de máquinas virtuales, consulte [Tamaños de máquinas virtuales](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* secuencias de comandos de toorun hello CoreMark en máquinas virtuales de Linux, descargar hello [CoreMark módulo de script](http://download.microsoft.com/download/3/0/5/305A3707-4D3A-4599-9670-AAEB423B4663/AzureCoreMarkScriptPack.zip).

