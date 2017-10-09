<!-- F-series, Fs-series* -->

F-series se basa en hello v3 de 2,4 GHz Intel Xeon® E5-2673 procesador (Haswell), que puede alcanzar velocidades de reloj tan alto como 3,1 GHz con hello aumento tecnología Intel Turbo 2.0. Esto es Hola mismo rendimiento de la CPU como Hola Dv2-series de máquinas virtuales.  A un precio de lista por hora inferior, Hola F-series es mejor valor de hello en el rendimiento de precio en hello Azure cartera en función de hello unidad de proceso de Azure (ACU) por vCPU. 

Las máquinas virtuales de la serie F son una opción excelente para cargas de trabajo que exigen CPU más rápidas, pero que no necesitan tanta memoria o almacenamiento temporal por vCPU.  Las cargas de trabajo, como el análisis, servidores de juegos, servidores web y el procesamiento por lotes se beneficiarán del valor de Hola de hello F-series.

Hola Fs-series proporciona todas las ventajas de Hola de hello F-series, en el almacenamiento de tooPremium de adición.

## <a name="fs-series"></a>Serie Fs*

ACU: 210 - 250

| Tamaño | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Discos de datos máx. | Rendimiento de almacenamiento temporal en caché y máx.: E/S por segundo / MBps (tamaño de caché en GiB) | Rendimiento de disco no en caché máx.: E/S por segundo / Mbps | Nº máx. NIC / rendimiento de red esperado (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_F1s |1 |2 |4 |2 |4000 / 32 (12) |3200 / 48 |2 / 750 |
| Standard_F2s |2 |4 |8 |4 |8000 / 64 (24) |6400 / 96 |2 / 1500 |
| Standard_F4s |4 |8 |16 |8 |16 000 / 128 (48) |12 800 / 192 |4 / 3000 |
| Standard_F8s |8 |16 |32 |16 |32 000 / 256 (96) |25 600 / 384 |8 / 6000 |
| Standard_F16s |16 |32 |64 |32 |64 000 / 512 (192) |51 200 / 768 |8 / 6000-12000 &#8224; |

MBps = 10^6 bytes por segundo y GiB = 1024^3 bytes.

* Hola máximo el rendimiento del disco (IOPS o MBps) posible con una serie de Fs VM puede verse limitado por número de hello, tamaño y la creación de bandas de hello adjuntan discos.  Para obtener más información, consulte [Premium Storage: almacenamiento de alto rendimiento para cargas de trabajo de máquinas virtuales de Azure](../articles/storage/common/storage-premium-storage.md).


<br>

## <a name="f-series"></a>Serie F

ACU: 210 - 250

| Tamaño         | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Rendimiento máximo del almacenamiento temporal: E/S por segundo / MBps de lectura / MBps de escritura | Rendimiento máximo por discos de datos: E/S por segundo | Nº máx. NIC / rendimiento de red esperado (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_F1  | 1         | 2           | 16             | 3000 / 46 / 23                                           | 2 / 2x500                         | 2 / 750                 |
| Standard_F2  | 2         | 4           | 32             | 6000 / 93 / 46                                           | 4 / 4x500                         | 2 / 1500                     |
| Standard_F4  | 4         | 8           | 64             | 12000 / 187 / 93                                         | 8 / 8x500                         | 4 / 3000                     |
| Standard_F8  | 8         | 16          | 128            | 24000 / 375 / 187                                        | 16 / 16x500                       | 8 / 6000                     |
| Standard_F16 | 16        | 32          | 256            | 48000 / 750 / 375                                        | 32 / 32x500                       | 8 / 6000 - 12000 &#8224;           |


<br>


