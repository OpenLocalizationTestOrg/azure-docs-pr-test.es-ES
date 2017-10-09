
<!-- A-series, Av2-series, D-series, Dv2-series, DS-series*, DSv2-series* -->

- Hola serie y máquinas virtuales de serie Av2 pueden implementarse en una variedad de tipos de hardware y los procesadores. Limitar tamaño de Hello, basado en hardware de hello, rendimiento de procesador coherente toooffer para hello ejecutando la instancia, con independencia de hardware de Hola se implementa en. toodetermine Hola hardware físico en el que se implementa este tamaño, consulta Hola hardware virtual desde dentro de hello Máquina Virtual.

- Máquinas virtuales de la serie D son toorun diseñado aplicaciones que requieren mayor capacidad de proceso y rendimiento de disco temporal. Máquinas virtuales de serie D proporcionan procesadores más rápidos y una mayor proporción de memoria para vCPU, una unidad de estado sólida (SSD) para el disco temporal de Hola. Para obtener más información, consulte el anuncio de Hola en hello blog de Azure, [nuevos tamaños de máquina Virtual de serie D](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).

- Serie de Dv2, un toohello continuada serie D original, cuenta con una CPU más eficaz. Hola Dv2 serie CPU es aproximadamente un 35% más rápido que Hola serie D CPU. Se basa en hello última generación v3 de 2,4 GHz Intel Xeon® E5-2673 procesador (Haswell) y con hello aumento tecnología Intel Turbo 2.0, pueden crecer hasta too3.1 GHz. Hola Dv2 serie tiene Hola mismas configuraciones de memoria y disco como Hola serie D.

- los tamaños de nivel básico de Hello son principalmente para las cargas de trabajo de desarrollo y otras aplicaciones que no requieren equilibrio de carga, la escala automática, o que utilizan mucha memoria máquinas virtuales. Para más información sobre los tamaños de máquinas virtuales más adecuados para las aplicaciones de producción, consulte (Tamaños de las máquinas virtuales) [virtual-machines-size-specs.md] y para obtener información sobre sus precios, consulte [Precios de máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="dsv3-series"></a>Serie Dsv3

ACU: 160-190

Tamaños de Dsv3-series están basados en hello v4 de 2,3 GHz Intel XEON® E5-2673 procesador (Broadwell) y pueden conseguir 3.5GHz con tecnología de Intel Turbo Boost 2.0 y usar almacenamiento premium. tamaños de Dsv3 serie Hola ofrecen una combinación de vCPU, memoria y almacenamiento temporal para la mayoría de las cargas de trabajo de producción.


| Tamaño             | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Discos de datos máx. | Rendimiento de almacenamiento temporal en caché y máx.: E/S por segundo / MBps (tamaño de caché en GiB) | Rendimiento de disco no en caché máx.: E/S por segundo / Mbps | Nº máx. NIC / rendimiento de red esperado (Mbps) |
|------------------|--------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------------------------|
| Standard_D2s_v3  | 2      | 8           | 16             | 4              | 4 000 / 32 (50)                                                       | 3200 / 48                                | 2 / moderado                                   |
| Standard_D4s_v3  | 4      | 16          | 32             | 8              | 8 000 / 64 (100)                                                      | 6400 / 96                                | 2 / moderado                                   |
| Standard_D8s_v3  | 8      | 32          | 64             | 16             | 16 000 / 128 (200)                                                    | 12 800 / 192                              | 4 / alto                                       |
| Standard_D16s_v3 | 16     | 64          | 128            | 32             | 32 000 / 256 (400)                                                    | 25 600 / 384                              | 8 / alto                                       |


## <a name="dv3-series"></a>Serie Dv3

ACU: 160-190

Tamaños de Dv3-series están basados en hello v4 de 2,3 GHz Intel XEON® E5-2673 procesador (Broadwell) y que puede lograr 3.5GHz con tecnología de Intel Turbo Boost 2.0. tamaños de Dv3 serie Hola ofrecen una combinación de vCPU, memoria y almacenamiento temporal para la mayoría de las cargas de trabajo de producción.

El almacenamiento en disco de datos se factura de forma independiente a las máquinas virtuales. discos de almacenamiento de toouse premium, use tamaños de Dsv3 Hola. Hola precios y facturación medidores de tamaños de Dsv3 se Hola igual que Dv3-series. 


| Tamaño            | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Discos de datos máx. | Rendimiento máximo del almacenamiento temporal: E/S por segundo / MBps de lectura / MBps de escritura | Ancho de banda de red/NIC máx. |
|-----------------|-----------|-------------|----------------|----------------|----------------------------------------------------------|------------------------------|
| Standard_D2_v3  | 2         | 8           | 50             | 4              | 3000/46/23                                               | 2 / moderado                 |
| Standard_D4_v3  | 4         | 16          | 100            | 8              | 6000/93/46                                               | 2 / moderado                 |
| Standard_D8_v3  | 8         | 32          | 200            | 16             | 12000/187/93                                             | 4 / alto                     |
| Standard_D16_v3 | 16        | 64          | 400            | 32             | 24000/375/187                                            | 8 / alto                     |


## <a name="dsv2-series"></a>DSv2-series

ACU: 210-250

| Tamaño | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Discos de datos máx. | Rendimiento de almacenamiento temporal en caché y máx.: E/S por segundo / MBps (tamaño de caché en GiB) | Rendimiento de disco no en caché máx.: E/S por segundo / Mbps | Nº máx. NIC / rendimiento de red esperado (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS1_v2 |1 |3,5 |7 |2 |4000 / 32 (43) |3200 / 48 |2 / 750 |
| Standard_DS2_v2 |2 |7 |14 |4 |8000 / 64 (86) |6400 / 96 |2 / 1500 |
| Standard_DS3_v2 |4 |14 |28 |8 |16 000 / 128 (172) |12 800 / 192 |4 / 3000 |
| Standard_DS4_v2 |8 |28 |56 |16 |32 000 / 256 (344) |25 600 / 384 |8 / 6000 |
| Standard_DS5_v2 |16 |56 |112 |32 |64 000 / 512 (688) |51 200 / 768 |8 / 6000 - 12000 &#8224;|



## <a name="dv2-series"></a>Serie Dv2

ACU: 210-250

| Tamaño              | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Rendimiento máximo del almacenamiento temporal: E/S por segundo / MBps de lectura / MBps de escritura | Rendimiento máximo por discos de datos: E/S por segundo | Nº máx. NIC / rendimiento de red esperado (Mbps) |
|-------------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_D1_v2    | 1         | 3,5         | 50             | 3000 / 46 / 23                                           | 2 / 2x500                         | 2 / 750                 |
| Standard_D2_v2    | 2         | 7           | 100            | 6000 / 93 / 46                                           | 4 / 4x500                         | 2 / 1500                     |
| Standard_D3_v2    | 4         | 14          | 200            | 12000 / 187 / 93                                         | 8 / 8x500                         | 4 / 3000                     |
| Standard_D4_v2    | 8         | 28          | 400            | 24000 / 375 / 187                                        | 16 / 16x500                       | 8 / 6000                     |
| Standard_D5_v2    | 16        | 56          | 800            | 48000 / 750 / 375                                        | 32 / 32x500                       | 8 / 6000 - 12000 &#8224;          |


<br>

## <a name="ds-series"></a>Serie DS

ACU: 160

| Tamaño | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Discos de datos máx. | Rendimiento de almacenamiento temporal en caché y máx.: E/S por segundo / MBps (tamaño de caché en GiB) | Rendimiento de disco no en caché máx.: E/S por segundo / Mbps | Nº máx. NIC / rendimiento de red esperado (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS1 |1 |3,5 |7 |2 |4000 / 32 (43) |3200 / 32 |2 / 500 |
| Standard_DS2 |2 |7 |14 |4 |8000 / 64 (86) |6400 / 64 |2 / 1000 |
| Standard_DS3 |4 |14 |28 |8 |16 000 / 128 (172) |12 800 / 128 |4 / 2000 |
| Standard_DS4 |8 |28 |56 |16 |32 000 / 256 (344) |25 600 / 256 |8 / 4000 |

<br>

## <a name="d-series"></a>Serie D 

ACU: 160

| Tamaño         | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Rendimiento máximo del almacenamiento temporal: E/S por segundo / MBps de lectura / MBps de escritura | Rendimiento máximo por discos de datos: E/S por segundo | Nº máx. NIC / rendimiento de red esperado (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_D1  | 1         | 3,5         | 50             | 3000 / 46 / 23                                           | 2 / 2x500                         | 2 / 500                 |
| Standard_D2  | 2         | 7           | 100            | 6000 / 93 / 46                                           | 4 / 4x500                         | 2 / 1000                     |
| Standard_D3  | 4         | 14          | 200            | 12000 / 187 / 93                                         | 8 / 8x500                         | 4 / 2000                     |
| Standard_D4  | 8         | 28          | 400            | 24000 / 375 / 187                                        | 16 / 16x500                       | 8 / 4000                     |

<br>


## <a name="av2-series"></a>Serie Av2

ACU: 100

| Tamaño            | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Rendimiento máximo del almacenamiento temporal: E/S por segundo / MBps de lectura / MBps de escritura | Rendimiento máximo por discos de datos: E/S por segundo | Nº máx. NIC / rendimiento de red esperado (Mbps) | 
|-----------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_A1_v2  | 1         | 2           | 10             | 1000 / 20 / 10                                           | 2 / 2x500               | 2 / 250                 |
| Standard_A2_v2  | 2         | 4           | 20 |             | 2000 / 40 / 20                                           | 4 / 4x500               | 2 / 500                 |
| Standard_A4_v2  | 4         | 8           | 40             | 4000 / 80 / 40                                           | 8 / 8x500               | 4 / 1000                     |
| Standard_A8_v2  | 8         | 16          | 80             | 8000 / 160 / 80                                          | 16 / 16x500             | 8 / 2000                     |
| Standard_A2m_v2 | 2         | 16          | 20 |             | 2000 / 40 / 20                                           | 4 / 4x500               | 2 / 500                 |
| Standard_A4m_v2 | 4         | 32          | 40             | 4000 / 80 / 40                                           | 8 / 8x500               | 4 / 1000                     |
| Standard_A8m_v2 | 8         | 64          | 80             | 8000 / 160 / 80                                          | 16 / 16x500             | 8 / 2000                     |

<br>

## <a name="a-series"></a>Serie A

ACU: 50-100

| Tamaño | vCPU | Memoria: GiB | Almacenamiento temporal (HDD): GiB | Discos de datos máx. | Rendimiento de discos de datos máx.: E/S por segundo | Nº máx. NIC / rendimiento de red esperado (Mbps)  |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A0* |1 |0,768 |20 | |1 |1x500 |2 / 100 |
| Standard_A1 |1 |1,75 |70 |2 |2 x 500 |2 / 500  |
| Standard_A2 |2 |3,5 |135 |4 |4x500 |2 / 500 |
| Standard_A3 |4 |7 |285 |8 |8x500 |2 / 1000 |
| Standard_A4 |8 |14 |605 |16 |16x500 |4 / 2000 |
| Standard_A5 |2 |14 |135 |4 |4x500 |2 / 500 |
| Standard_A6 |4 |28 |285 |8 |8x500 |2 / 1000 |
| Standard_A7 |8 |56 |605 |16 |16x500 |4 / 2000 |
<br>

* Hola Tamaño A0 es excesiva suscrito en el hardware físico de Hola. Solo este tamaño específico, otras implementaciones de cliente pueden afectar al rendimiento de hello de la carga de trabajo de ejecución. a continuación se indica el rendimiento relativo de Hello como línea base Hola esperado, variabilidad aproximado de asunto tooan de 15 por ciento.

### <a name="standard-a0---a4-using-cli-and-powershell"></a>Standard_A0 - A4 con CLI y PowerShell
En el modelo de implementación clásica de hello, algunos nombres de tamaño de máquina virtual son ligeramente diferentes en CLI y PowerShell:

* Standard_A0 es ExtraSmall 
* Standard_A1 es Small
* Standard_A2 es Medium
* Standard_A3 es Large
* Standard_A4 es ExtraLarge

## <a name="basic-a"></a>A básico

|Tamaño – Tamaño\nombre | vCPU |Memoria|NICs (Máx)|Tamaño máximo del disco temporal |Máx. discos de datos (1023 GB cada uno)|Máx. E/S (300 por disco)|
|---|---|---|---|---|---|---|
|A0\Basic_A0|1|768 MB|2| 20 GB|1|1x300|
|A1\Basic_A1|1|1,75 GB|2| 40 GB |2|2x300|
|A2\Basic_A2|2|3,5 GB|2| 60 GB|4|4x300|
|A3\Basic_A3|4|7 GB|2| 120 GB |8|8x300|
|A4\Basic_A4|8|14 GB|2| 240 GB |16|16x300|
