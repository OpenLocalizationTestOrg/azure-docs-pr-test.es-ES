**Discos de máquina virtual no administrados Premium: por límites de cuenta**

| Recurso | Límite predeterminado |
| --- | --- |
| Capacidad total de disco por cuenta |35 TB |
| Capacidad total de instantáneas por cuenta |10 TB |
| Ancho de banda máximo por cuenta (entrada + salida<sup>1</sup>) |<=50 Gbps |

<sup>1</sup>*entrada* hace referencia a datos de tooall (solicitudes) enviados tooa cuenta de almacenamiento. *Salida* hace referencia a datos de tooall (respuestas) recibidos de una cuenta de almacenamiento.

**Discos de máquina virtual no administrados Premium: por límites de disco**

| Tipo de disco de Almacenamiento premium | P10 | P20 | P30 | P40 | P50 |
| --- | --- | --- | --- | --- | --- |
| Tamaño del disco |128 GB |512 GB |1024 GB (1 TB) |2048 GB (2 TB)|4095 GB (4 TB)|
| Máximo de IOPS por disco |500 |2300 |5000 |7500 |7500 |
| Rendimiento máximo por disco |100 MB/s | 150 MB/s |200 MB/s |250 MB/s |250 MB/s |
| Número máximo de discos por cuenta de almacenamiento |280 |70 |35 | 17 | 8 |

**Discos de máquina virtual no administrados Premium: por límites de máquina virtual**

| Recurso | Límite predeterminado |
| --- | --- |
| Máximo de IOPS por VM |80 000 IOPS con máquina virtual GS5<sup>1</sup> |
| Rendimiento máximo por VM |2000 MB/s con máquina virtual GS5<sup>1</sup> |

<sup>1</sup>consulte demasiado[tamaño de máquina virtual](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) límites de otros tamaños de máquina virtual. 
