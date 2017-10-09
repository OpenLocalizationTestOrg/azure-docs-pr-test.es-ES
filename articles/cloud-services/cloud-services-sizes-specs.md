---
title: "tamaños de máquina de aaaVirtual de servicios en la nube de Azure | Documentos de Microsoft"
description: "Enumera los tamaños de máquina virtual diferente de hello (e identificadores) para los roles de web y de trabajo de servicio de nube de Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1127c23e-106a-47c1-a2e9-40e6dda640f6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 93d91a67afc352f3d18c31e0dd5cf976bf46350c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-cloud-services"></a>Tamaños de los servicios en la nube
En este tema se describe los tamaños disponibles de Hola y las opciones para instancias de rol de servicio en la nube (roles web y roles de trabajo). También proporciona toobe de consideraciones de implementación tenga en cuenta al planear toouse estos recursos. Cada tamaño tiene un identificador que pondrá en su [archivo de definición de servicio](cloud-services-model-and-package.md#csdef). Los precios para cada tamaño de están disponibles en hello [precios de servicios de nube](https://azure.microsoft.com/pricing/details/cloud-services/) página.

> [!NOTE]
> toosee relacionadas con el límite de Azure, consulte [suscripción de Azure y límites de servicio, cuotas y restricciones](../azure-subscription-service-limits.md)
>
>

## <a name="sizes-for-web-and-worker-role-instances"></a>Tamaños de instancias de roles web y de trabajo
Hay varias toochoose tamaños estándar de en Azure. Entre las consideraciones para algunos de estos tamaños, se incluyen:

* Máquinas virtuales de la serie D son toorun diseñado aplicaciones que requieren mayor capacidad de proceso y rendimiento de disco temporal. Máquinas virtuales de serie D proporcionan procesadores más rápidos, una mayor proporción de memoria a núcleo y una unidad de estado sólida (SSD) para el disco temporal de Hola. Para obtener más información, consulte el anuncio de Hola en hello blog de Azure, [nuevos tamaños de máquina Virtual de serie D](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).
* Serie de Dv2, un toohello continuada serie D original, cuenta con una CPU más eficaz. Hola Dv2 serie CPU es aproximadamente un 35% más rápido que Hola serie D CPU. Se basa en hello última generación v3 de 2,4 GHz Intel Xeon® E5-2673 procesador (Haswell) y con hello aumento tecnología Intel Turbo 2.0, pueden crecer hasta too3.1 GHz. Hola Dv2 serie tiene Hola mismas configuraciones de memoria y disco como Hola serie D.
* Máquinas virtuales de serie G ofrecen hello más memoria y ejecutan en hosts que tienen procesadores de la familia Intel Xeon E5 V3.
* Hola serie a las máquinas virtuales se puede implementar en varios tipos de hardware y procesadores. Limitar tamaño de Hello, basados en hardware de hello, rendimiento de procesador coherente toooffer para hello ejecutando la instancia, con independencia de hardware de Hola se implementa en. toodetermine Hola hardware físico en el que se implementa este tamaño, consulta Hola hardware virtual desde dentro de hello Máquina Virtual.
* Hola Tamaño A0 es excesiva suscrito en el hardware físico de Hola. Solo este tamaño específico, otras implementaciones de cliente pueden afectar al rendimiento de hello de la carga de trabajo de ejecución. a continuación se indica el rendimiento relativo de Hello como línea base Hola esperado, variabilidad aproximado de asunto tooan de 15 por ciento.

tamaño de Hola de máquina virtual de hello afecta a precios de Hola. tamaño de Hello también afecta a la capacidad de procesamiento, memoria y almacenamiento de Hola de máquina virtual de Hola. Los costos de almacenamiento se calculan por separado según las páginas usadas en la cuenta de almacenamiento de Hola. Para más información, consulte [Detalles de precios de Cloud Services](https://azure.microsoft.com/pricing/details/cloud-services/) y [Precios de Azure Storage](https://azure.microsoft.com/pricing/details/storage/).

Hola después consideraciones podría ayudarle a decidirse por un tamaño:

* Hello tamaños A8 A11 y H-series son también se denomina *instancias de proceso intensivo*. hardware de Hola que ejecuta estos tamaños está diseñado y optimizado para el proceso intensivo y aplicaciones, modelado y simulaciones de clúster de aplicaciones de red intensiva, incluido informática de alto rendimiento (HPC). Hola A8 A11 serie utiliza Intel Xeon E5-2670 a 2,6 GHZ y Hola H-series utiliza Intel Xeon E5-2667 v3 @ 3,2 GHz. Para más información y consideraciones sobre el uso de estos tamaños, consulte [Tamaños de máquina virtual de informática de alto rendimiento](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Las series Dv2, D y G son ideales para las aplicaciones que requieren CPU más rápidas, mejor rendimiento de disco local, o tienen mayor demanda de memoria. Ofrecen una combinación eficaz para muchas aplicaciones de clase empresarial.
* Puede que algunos de los hosts físicos de hello en los centros de datos de Azure no admitan tamaños mayores de máquina virtual, como A5-A11. Como resultado, verá el mensaje de error de hello **máquina virtual de tooconfigure error {nombre de la máquina}** o **máquina virtual de toocreate error {nombre de la máquina}** al cambiar el tamaño de una existente tooa de máquina virtual nueva tamaño; crear una nueva máquina virtual en una red virtual creada antes del 16 de abril de 2013; o bien, agregar un nueva máquina virtual tooan existente servicio en la nube. Vea [Error: "Error tooconfigure virtual machine"](https://social.msdn.microsoft.com/Forums/9693f56c-fcd3-4d42-850e-5e3b56c7d6be/error-failed-to-configure-virtual-machine-with-a5-a6-or-a7-vm-size?forum=WAVirtualMachinesforWindows) en el foro de soporte técnico de Hola para las soluciones alternativas para cada escenario de implementación.
* La suscripción también puede limitar el número de Hola de núcleos que se puede implementar en ciertas familias de tamaño. tooincrease una cuota, póngase en contacto con soporte técnico de Azure.

## <a name="performance-considerations"></a>Consideraciones sobre rendimiento
Hemos creado concepto de Hola de hello unidad de proceso de Azure (ACU) tooprovide una manera de comparar el rendimiento de proceso (CPU) a través de SKU de Azure y tooidentify que SKU es probablemente toosatisfy el rendimiento necesario.  Actualmente, una ACU está estandarizada en una máquina virtual pequeña (Standard_A1) como 100 y todas las demás SKU representan, aproximadamente, qué tanto más rápido esa SKU puede ejecutar una prueba comparativa estándar.

> [!IMPORTANT]
> Hola ACU es solo una directriz. resultados de Hello para la carga de trabajo pueden variar.
>
>

<br>

| Familia de SKU | ACU/núcleo |
| --- | --- |
| [ExtraSmall](#a-series) |50 |
| [Small-ExtraLarge](#a-series) |100 |
| [A5-7](#a-series) |100 |
| [Standard_A1-8v2](#av2-series) |100 |
| [Standard_A2m-8mv2](#av2-series) |100 |
| [A8-A11](#a-series) |225* |
| [D1-14](#d-series) |160 |
| [D1 15v2](#dv2-series) |210 - 250* |
| [G1 5](#g-series) |180 - 240* |
| [H](#h-series) |290 - 300* |

ACUs marcados con un * usan una frecuencia tooincrease CPU de Intel® Turbo tecnología y proporcionar un aumento del rendimiento. Hello cantidad de aumento de hello puede variar en función de tamaño de máquina virtual de hello, carga de trabajo y otras cargas de trabajo que se ejecutan en hello mismo host.

## <a name="size-tables"></a>Tablas de tamaño
Hello en las tablas siguientes muestran tamaños de Hola y capacidades de hello proporcionan.

* La capacidad de almacenamiento se muestra en unidades de GiB o 1024^3 bytes. Al comparar discos medido en GB (1000 ^ 3 bytes) toodisks medido en GiB (1024 ^ 3) Recuerde que los números de capacidad en GiB pueden aparecer más pequeños. Por ejemplo, 1023 GiB = 1098.4 GB
* Se midió el rendimiento de disco en operaciones de entrada/salida por segundo (E/S por segundo) y Mbps, donde Mbps = 10^6 bytes/s.
* Los discos de datos pueden funcionar en modo en caché o en modo no en caché. Para la operación de disco de datos almacenados en caché, modo de caché de host de Hola se establece demasiado**ReadOnly** o **ReadWrite**. Para la operación de disco de datos sin almacenar en caché, modo de caché de host de Hola se establece demasiado**ninguno**.
* Ancho de banda de red máximo es Hola agregados ancho de banda máximo asignado y asignado por el tipo de máquina virtual. ancho de banda máximo de Hello proporciona orientación para la selección de hello derecho VM tipo tooensure suficiente capacidad de la red está disponible. Al mover entre baja, moderada, alta y muy alta, el rendimiento de hello aumenta en consecuencia. El rendimiento de red real dependerá de muchos factores (como, por ejemplo, las cargas de la red y de la aplicación y la configuración de red de la aplicación).

## <a name="a-series"></a>Serie A
| Tamaño            | Núcleos de CPU | Memoria: GiB  | HDD local: GiB       | Ancho de banda de red/NIC máx. |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| ExtraSmall      | 1         | 0,768        | 20 |                   | 1 / bajo |
| Pequeña           | 1         | 1,75         | 225                  | 1 / moderado |
| Mediano          | 2         | 3,5 GB       | 490                  | 1 / moderado |
| Grande           | 4         | 7            | 1000                 | 2 / alto |
| ExtraLarge      | 8         | 14           | 2040                 | 4 / alto |
| A5              | 2         | 14           | 490                  | 1 / moderado |
| A6              | 4         | 28           | 1000                 | 2 / alto |
| A7              | 8         | 56           | 2040                 | 4 / alto |

## <a name="a-series---compute-intensive-instances"></a>Serie A: instancias de proceso intensivo
Para más información y consideraciones sobre el uso de estos tamaños, consulte [Tamaños de máquina virtual de informática de alto rendimiento](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

| Tamaño            | Núcleos de CPU | Memoria: GiB  | HDD local: GiB       | Ancho de banda de red/NIC máx. |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| A8*             |8          | 56           | 1817                 | 2 / alto |
| A9*             |16         | 112          | 1817                 | 4 / muy alto |
| A10             |8          | 56           | 1817                 | 2 / alto |
| A11             |16         | 112          | 1817                 | 4 / muy alto |

\*Compatible con RDMA

## <a name="av2-series"></a>Serie Av2

| Tamaño            | Núcleos de CPU | Memoria: GiB  | SSD local: GiB       | Ancho de banda de red/NIC máx. |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_A1_v2  | 1         | 2            | 10                   | 1 / moderado                 |
| Standard_A2_v2  | 2         | 4            | 20 |                   | 2 / moderado                 |
| Standard_A4_v2  | 4         | 8            | 40                   | 4 / alto                     |
| Standard_A8_v2  | 8         | 16           | 80                   | 8 / alto                     |
| Standard_A2m_v2 | 2         | 16           | 20 |                   | 2 / moderado                 |
| Standard_A4m_v2 | 4         | 32           | 40                   | 4 / alto                     |
| Standard_A8m_v2 | 8         | 64           | 80                   | 8 / alto                     |


## <a name="d-series"></a>Serie D
| Tamaño            | Núcleos de CPU | Memoria: GiB  | SSD local: GiB       | Ancho de banda de red/NIC máx. |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_D1     | 1         | 3,5          | 50                   | 1 / moderado |
| Standard_D2     | 2         | 7            | 100                  | 2 / alto |
| Standard_D3     | 4         | 14           | 200                  | 4 / alto |
| Standard_D4     | 8         | 28           | 400                  | 8 / alto |
| Standard_D11    | 2         | 14           | 100                  | 2 / alto |
| Standard_D12    | 4         | 28           | 200                  | 4 / alto |
| Standard_D13    | 8         | 56           | 400                  | 8 / alto |
| Standard_D14    | 16        | 112          | 800                  | 8 / muy alto |

## <a name="dv2-series"></a>Serie Dv2
| Tamaño            | Núcleos de CPU | Memoria: GiB  | SSD local: GiB       | Ancho de banda de red/NIC máx. |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_D1_v2  | 1         | 3,5          | 50                   | 1 / moderado |
| Standard_D2_v2  | 2         | 7            | 100                  | 2 / alto |
| Standard_D3_v2  | 4         | 14           | 200                  | 4 / alto |
| Standard_D4_v2  | 8         | 28           | 400                  | 8 / alto |
| Standard_D5_v2  | 16        | 56           | 800                  | 8 / extremadamente alto |
| Standard_D11_v2 | 2         | 14           | 100                  | 2 / alto |
| Standard_D12_v2 | 4         | 28           | 200                  | 4 / alto |
| Standard_D13_v2 | 8         | 56           | 400                  | 8 / alto |
| Standard_D14_v2 | 16        | 112          | 800                  | 8 / extremadamente alto |
| Standard_D15_v2 | 20 |        | 140          | 1000                | 8 / extremadamente alto |

## <a name="g-series"></a>Serie G
| Tamaño            | Núcleos de CPU | Memoria: GiB  | SSD local: GiB       | Ancho de banda de red/NIC máx. |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_G1     | 2         | 28           | 384                  |1 / alto |
| Standard_G2     | 4         | 56           | 768                  |2 / alto |
| Standard_G3     | 8         | 112          | 1536                |4 / muy alto |
| Standard_G4     | 16        | 224          | 3072                |8 / extremadamente alto |
| Standard_G5     | 32        | 448          | 6144                |8 / extremadamente alto |

## <a name="h-series"></a>Serie H
Máquinas virtuales de Azure H-series son Hola siguiente generación informática de alto rendimiento que las máquinas virtuales dirigidas a las necesidades de cálculo de high-end, como modelado molecular y dinámica de fluidos computacional. Estas 8 y 16 núcleos las máquinas virtuales se crean en la tecnología de procesador de hello Intel 2667 Haswell E5 V3 que incluye DDR4 memoria y almacenamiento basada en SSD local.

Además toohello gran potencia de la CPU, Hola H-series ofrece diversas opciones para las redes de RDMA de latencia baja mediante FDR InfiniBand y varias configuraciones toosupport memoria intensivas cálculo requisitos de memoria.

| Tamaño            | Núcleos de CPU | Memoria: GiB  | SSD local: GiB       | Ancho de banda de red/NIC máx. |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_H8     | 8         | 56           | 1000                 | 8 / alto |
| Standard_H16    | 16        | 112          | 2000                 | 8 / muy alto |
| Standard_H8m    | 8         | 112          | 1000                 | 8 / alto |
| Standard_H16m   | 16        | 224          | 2000                 | 8 / muy alto |
| Standard_H16r*  | 16        | 112          | 2000                 | 8 / muy alto |
| Standard_H16mr* | 16        | 224          | 2000                 | 8 / muy alto |

\*Compatible con RDMA

## <a name="configure-sizes-for-cloud-services"></a>Configuración de tamaños para los Servicios en la nube
Puede especificar el tamaño de una instancia de rol de máquina Virtual de hello como parte del modelo de servicio de hello descrito por hello [archivo de definición de servicio](cloud-services-model-and-package.md#csdef). tamaño de Hola de rol Hola determina número Hola de núcleos de CPU, capacidad de memoria de Hola y tamaño del sistema de archivos local Hola que se asigna tooa ejecuta la instancia. Elegir tamaño de rol de hello en función de los requisitos de recursos de la aplicación.

Este es un ejemplo para establecer toobe de tamaño de rol de hello [Standard_D2](#general-purpose-d) para una instancia de rol Web:

```xml
<WorkerRole name="Worker1" vmsize="Standard_D2">
...
</WorkerRole>
```

## <a name="changing-hello-size-of-an-existing-role"></a>Cambiar el tamaño de Hola de un rol existente

Como la naturaleza de Hola de los cambios de carga de trabajo o los nuevos tamaños de máquina virtual esté disponibles, puede que desee toochange tamaño de Hola de su rol. toodo por lo tanto, también debe cambiar el tamaño VM de hello en el archivo de definición de servicio (tal y como se muestra arriba), volver a empaquetar el servicio en la nube e implementarlo. No es posible toochange tamaños de máquina virtual directamente desde el portal de Hola o PowerShell.

>[!TIP]
> Puede que desee toouse distintos tamaños de máquina virtual para el rol en diferentes entornos (p. ej. prueba frente a producción). Toodo una manera de esto es toocreate varios archivos de definición (.csdef) de servicio en el proyecto y después crear paquetes de servicio por cada entorno de nube diferente durante la compilación automatizada con la herramienta CSPack de Hola. ¿paquete de servicios de toolearn más información acerca de los elementos de una nube hello y cómo toocreate, consulte [Novedades en la nube hello de servicios de modelo y cómo empaquetarla?](cloud-services-model-and-package.md)
>
>

## <a name="get-a-list-of-sizes"></a>Obtención de una lista de tamaños
También puede usar PowerShell o hello tooget una lista de tamaños de API de REST. Hello API de REST se documenta [aquí](https://msdn.microsoft.com/library/azure/dn469422.aspx). Hello código siguiente es un comando de PowerShell que mostrará una lista de todos los tamaños de hello disponibles actualmente para el servicio de nube.

```powershell
Get-AzureRoleSize | where SupportedByWebWorkerRoles -eq $true | select InstanceSize
```

## <a name="next-steps"></a>Pasos siguientes
* Conozca los [límites, cuotas y restricciones de suscripción y servicios de Azure](../azure-subscription-service-limits.md).
* Más información [sobre los tamaños de máquinas virtuales de procesos de alto rendimiento](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para cargas de trabajo HPC.
