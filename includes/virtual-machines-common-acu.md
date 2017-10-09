



Hemos creado concepto de Hola de hello unidad de proceso de Azure (ACU) tooprovide una manera de comparar el rendimiento de proceso (CPU) a través de SKU de Azure. Esto le permitirá identificar fácilmente qué SKU es toosatisfy probablemente sus necesidades de rendimiento.  Actualmente, una ACU está estandarizada en una máquina virtual pequeña (Standard_A1) como 100 y todas las demás SKU representan, aproximadamente, qué tanto más rápido esa SKU puede ejecutar una prueba comparativa estándar. 

> [!IMPORTANT]
> Hola ACU es solo una directriz.  resultados de Hello para la carga de trabajo pueden variar. 
> 
> 

<br>

| Familia de SKU | ACU \ vCPU |
| --- | --- |
| [A0](../articles/virtual-machines/windows/sizes-general.md) |50 |
| [A1-A4](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A5-A7](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A1_v2-A8_v2](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A2m_v2-A8m_v2](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A8-A11](../articles/virtual-machines/windows/sizes-hpc.md) |225* |
| [D1-D14](../articles/virtual-machines/windows/sizes-general.md) |160 |
| [D1_v2-D15_v2](../articles/virtual-machines/windows/sizes-general.md) |210 - 250* |
| [DS1-DS14](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |160 |
| [DS1_v2-DS15_v2](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |210-250* |
| [D_v3](../articles/virtual-machines/virtual-machines-windows-sizes-general.md) |160-190* ** |
| [Ds_v3](../articles/virtual-machines/virtual-machines-windows-sizes-general.md) |160-190* ** |
| [E_v3](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |160-190* ** |
| [Es_v3](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |160-190* ** |
| [F1-F16](../articles/virtual-machines/windows/sizes-compute.md) |210-250* |
| [F1s F16s](../articles/virtual-machines/windows/sizes-compute.md) |210-250* |
| [G1-G5](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |180 - 240* |
| [GS1-GS5](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |180 - 240* |
| [H](../articles/virtual-machines/windows/sizes-hpc.md) |290 - 300* |
| [L4s-L32s](../articles/virtual-machines/windows/sizes-storage.md) |180 - 240* |
| [M](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) | 160-180** |

ACUs marcados con un * usan una frecuencia tooincrease CPU de Intel® Turbo tecnología y proporcionar un aumento del rendimiento.  Hello cantidad de aumento de hello puede variar en función de tamaño de máquina virtual de hello, carga de trabajo y otras cargas de trabajo que se ejecutan en hello mismo host.

**Hyper-threaded. 
