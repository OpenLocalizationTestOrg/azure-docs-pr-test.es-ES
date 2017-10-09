
* Hola M-Series ofrece mayor número de vCPU hello (arriba too128 vCPU) y mayor memoria (arriba too2.0 TiB) de todas las máquinas virtuales en la nube de Hola.  Es ideal para bases de datos extremadamente grandes u otras aplicaciones que se benefician de un elevado número de vCPU y grandes cantidades de memoria.

* Serie Dv2, serie D, G-series, y homólogos de DS/GS Hola son ideales para aplicaciones que exigen más rápido vCPU, mejorar el rendimiento de almacenamiento temporal, o que tienen mayor demanda de memoria.  Ofrecen una combinación eficaz para muchas aplicaciones de clase empresarial.

* Máquinas virtuales de la serie D son toorun diseñado aplicaciones que requieren mayor capacidad de proceso y rendimiento de disco temporal. Las máquinas virtuales de la serie D proporcionan procesadores más rápidos, una mayor proporción de memoria a vCPU y una unidad de estado sólido (SSD) para el almacenamiento temporal. Para obtener más información, consulte el anuncio de Hola en hello blog de Azure, [nuevos tamaños de máquina Virtual de serie D](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).

* Serie de Dv2, un toohello continuada serie D original, cuenta con una CPU más eficaz. Hola Dv2 serie CPU es aproximadamente un 35% más rápido que Hola serie D CPU. Se basa en hello última generación v3 de 2,4 GHz Intel Xeon® E5-2673 procesador (Haswell) y con hello aumento tecnología Intel Turbo 2.0, pueden crecer hasta too3.1 GHz. Hola Dv2 serie tiene Hola mismas configuraciones de memoria y disco como Hola serie D.


## <a name="esv3-series"></a>Serie ESv3

ACU: 160-190

Instancias de ESv3 serie se basan en hello v4 de 2,3 GHz Intel XEON® E5-2673 procesador (Broadwell) y pueden conseguir 3.5GHz con tecnología de Intel Turbo Boost 2.0 y usar almacenamiento premium. Las instancias de la serie Ev3 son ideales para aplicaciones empresariales de uso intensivo de memoria.


| Tamaño             | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Discos de datos máx. | Rendimiento de almacenamiento temporal en caché y máx.: E/S por segundo / MBps (tamaño de caché en GiB) | Rendimiento de disco no en caché máx.: E/S por segundo / Mbps | Nº máx. NIC / rendimiento de red esperado (Mbps) |
|------------------|--------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------------------------|
| Standard_E2s_v3  | 2      | 16          | 32             | 4              | 4 000 / 32 (50)                                                       | 3200 / 48                                | 2 / moderado                                   |
| Standard_E4s_v3  | 4      | 32          | 64             | 8              | 8 000 / 64 (100)                                                      | 6400 / 96                                | 2 / moderado                                   |
| Standard_E8s_v3  | 8      | 64          | 128            | 16             | 16 000 / 128 (200)                                                    | 12 800 / 192                              | 4 / alto                                       |
| Standard_E16s_v3 | 16     | 128         | 256            | 32             | 32 000 / 256 (400)                                                    | 25 600 / 384                              | 8 / alto                                       |
| Standard_E32s_v3 | 32     | 256         | 512            | 32             | 64 000 / 512 (800)                                                    | 51 200 / 768                              | 8 / extremadamente alto                             |
| Standard_E64s_v3 | 64     | 432         | 864            | 32             | 128 000/1024 (1600)                                                   | 80 000 / 1200                             | 8 / extremadamente alto                             |



## <a name="ev3-series"></a>Serie Ev3

ACU: 160 - 190 

Instancias de Ev3 serie se basan en hello v4 de 2,3 GHz Intel XEON® E5-2673 procesador (Broadwell) y que puede lograr 3.5GHz con tecnología de Intel Turbo Boost 2.0. Las instancias de la serie Ev3 son ideales para aplicaciones empresariales de uso intensivo de memoria.

El almacenamiento en disco de datos se factura de forma independiente a las máquinas virtuales. discos de almacenamiento de toouse premium, use tamaños de ESv3 Hola. Hola precios y facturación medidores de tamaños de ESv3 se Hola igual que Ev3-series. 


| Tamaño            | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Discos de datos máx. | Rendimiento máximo del almacenamiento temporal: E/S por segundo / MBps de lectura / MBps de escritura | Ancho de banda de red/NIC máx. |
|-----------------|-----------|-------------|----------------|----------------|----------------------------------------------------------|------------------------------|
| Standard_E2_v3  | 2         | 16          | 50             | 4              | 3000/46/23                                               | 2 / moderado                 |
| Standard_E4_v3  | 4         | 32          | 100            | 8              | 6000/93/46                                               | 2 / moderado                 |
| Standard_E8_v3  | 8         | 64          | 200            | 16             | 12000/187/93                                             | 4 / alto                     |
| Standard_E16_v3 | 16        | 128         | 400            | 32             | 24000/375/187                                            | 8 / alto                     |
| Standard_E32_v3 | 32        | 256         | 800            | 32             | 48000/750/375                                            | 8 / extremadamente alto           |
| Standard_E64_v3 | 64        | 432         | 1600           | 32             | 96000/1000/500                                           | 8 / extremadamente alto           |


## <a name="m-series"></a>Serie M*

ACU: 160-180

| Tamaño            | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Discos de datos máx. | Rendimiento de almacenamiento temporal en caché y máx.: E/S por segundo / MBps (tamaño de caché en GiB) | Rendimiento de disco no en caché máx.: E/S por segundo / Mbps | Nº máx. NIC / rendimiento de red esperado (Mbps) |
|-----------------|------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------|
| Standard_M64ms  | 64   | 1792        | 2048           | 32             | 80,000 / 800 (6348)       | 40 000 / 1000                            | 8 / 16000          |
| Standard_M128s** | 128  | 2048        | 4096           | 64             | 160,000 / 1,600 (12,696) | 80 000 / 2000                            | 8 / 25000          |



*Las máquinas virtuales de la serie M cuentan con la tecnología Hyper-Threading de Intel®

**Más de 64 vCPU requieren uno de estos SO invitados compatibles: Windows Server 2016, Ubuntu 16.04 LTS, SLES 12 SP2 y Red Hat Enterprise Linux o CentOS 7.3 con LIS 4.2.1 

<br>

## <a name="gs-series"></a>Serie GS*

ACU: 180 - 240

| Tamaño | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Discos de datos máx. | Rendimiento de almacenamiento temporal en caché y máx.: E/S por segundo / MBps (tamaño de caché en GiB) | Rendimiento de disco no en caché máx.: E/S por segundo / Mbps | Nº máx. NIC / rendimiento de red esperado (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_GS1 |2 |28 |56 |4 |10 000 / 100 (264) |5000 / 125 |2 / 2000 |
| Standard_GS2 |4 |56 |112 |8 |20 000 / 200 (528) |10 000 / 250 |2 / 4000 |
| Standard_GS3 |8 |112 |224 |16 |40 000 / 400 (1056) |20 000 / 500 |4 / 8000 |
| Standard_GS4 |16 |224 |448 |32 |80 000 / 800 (2112) |40 000 / 1000 |8 / 6000 - 16000 &#8224; |
| Standard_GS5** |32 |448 |896 |64 |160 000 / 1600 (4224) |80 000 / 2000 |8 / 20000 |

* Hola máximo el rendimiento del disco (IOPS o MBps) posible con una serie de GS VM puede verse limitado por número de hello, tamaño y la creación de bandas de hello adjuntan discos. Para obtener más información, consulte [Premium Storage: almacenamiento de alto rendimiento para cargas de trabajo de máquinas virtuales de Azure](../articles/storage/common/storage-premium-storage.md). 

** Instancia está aislado toohardware tooa dedicado solo cliente.


<br>

## <a name="g-series"></a>Serie G

ACU: 180 - 240

| Tamaño         | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Rendimiento máximo del almacenamiento temporal: E/S por segundo / MBps de lectura / MBps de escritura | Rendimiento máximo por discos de datos: E/S por segundo | Nº máx. NIC / rendimiento de red esperado (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_G1  | 2         | 28          | 384            | 6000 / 93 / 46                                           | 4 / 4 x 500                       | 2 / 2000                     |
| Standard_G2  | 4         | 56          | 768            | 12000 / 187 / 93                                         | 8 / 8 x 500                       | 2 / 4000                     |
| Standard_G3  | 8         | 112         | 1536          | 24000 / 375 / 187                                        | 16 / 16 x 500                     | 4 / 8000                |
| Standard_G4  | 16        | 224         | 3072          | 48000 / 750 / 375                                        | 32 / 32 x 500                     | 8 / 6000 - 16000 &#8224;          |
| Standard_G5* | 32        | 448         | 6144          | 96000 / 1500 / 750                                       | 64 / 64 x 500                     | 8 / 20000           |

* Instancia está aislado toohardware tooa dedicado solo cliente.
<br>


## <a name="dsv2-series"></a>Serie DSv2*

ACU: 210 - 250

| Tamaño | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Discos de datos máx. | Rendimiento de almacenamiento temporal en caché y máx.: E/S por segundo / MBps (tamaño de caché en GiB) | Rendimiento de disco no en caché máx.: E/S por segundo / Mbps | Nº máx. NIC / rendimiento de red esperado (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS11_v2 |2 |14 |28 |4 |8000 / 64 (72) |6400 / 96 |2 / 1500 |
| Standard_DS12_v2 |4 |28 |56 |8 |16 000 / 128 (144) |12 800 / 192 |4 / 3000 |
| Standard_DS13_v2 |8 |56 |112 |16 |32 000 / 256 (288) |25 600 / 384 |8 / 6000 |
| Standard_DS14_v2 |16 |112 |224 |32 |64 000 / 512 (576) |51 200 / 768 |8 / 6000 - 12000 &#8224; |
| Standard_DS15_v2** |20 | |140 |280 |40 |80 000 / 640 (720) |64 000 / 960 |8 / 20000***

* Hola máximo el rendimiento del disco (IOPS o MBps) posible con una serie de DSv2 VM puede verse limitado por número de hello, tamaño y la creación de bandas de hello adjuntan discos.  Para obtener más información, consulte [Premium Storage: almacenamiento de alto rendimiento para cargas de trabajo de máquinas virtuales de Azure](../articles/storage/common/storage-premium-storage.md).

** Instancia es un nodo aislado que garantiza que la máquina virtual está Hola solo VM en el nodo Haswell de Intel.

*** 25000 Mbps con redes aceleradas.

<br>

## <a name="dv2-series"></a>Serie Dv2

ACU: 210 - 250

| Tamaño              | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Rendimiento máximo del almacenamiento temporal: E/S por segundo / MBps de lectura / MBps de escritura | Rendimiento máximo por discos de datos: E/S por segundo | Nº máx. NIC / rendimiento de red esperado (Mbps) |
|-------------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_D11_v2   | 2         | 14          | 100            | 6000 / 93 / 46                                           | 4 / 4x500                         | 2 / 1500                     |
| Standard_D12_v2   | 4         | 28          | 200            | 12000 / 187 / 93                                         | 8 / 8x500                         | 4 / 3000                     |
| Standard_D13_v2   | 8         | 56          | 400            | 24000 / 375 / 187                                        | 16 / 16x500                       | 8 / 6000                     |
| Standard_D14_v2   | 16        | 112         | 800            | 48000 / 750 / 375                                        | 32 / 32x500                       | 8 / 6000 - 12000 &#8224;          |
| Standard_D15_v2* | 20 |        | 140         | 1000          | 60000 / 937 / 468                                        | 40 / 40x500                       | 8 / 20000** |

* Instancia es un nodo aislado que garantiza que la máquina virtual está Hola solo VM en el nodo Haswell de Intel.

** 25000 Mbps con redes aceleradas.

<br>

## <a name="ds-series"></a>Serie DS*

ACU: 160

| Tamaño | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Discos de datos máx. | Rendimiento de almacenamiento temporal en caché y máx.: E/S por segundo / MBps (tamaño de caché en GiB) | Rendimiento de disco no en caché máx.: E/S por segundo / Mbps | Nº máx. NIC / rendimiento de red esperado (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS11 |2 |14 |28 |4 |8000 / 64 (72) |6400 / 64 |2 / 1000 |
| Standard_DS12 |4 |28 |56 |8 |16 000 / 128 (144) |12 800 / 128 |4 / 2000 |
| Standard_DS13 |8 |56 |112 |16 |32 000 / 256 (288) |25 600 / 256 |8 / 4000 |
| Standard_DS14 |16 |112 |224 |32 |64 000 / 512 (576) |51 200 / 512 |8 / 6000 - 8000 &#8224; |

* Hola máximo el rendimiento del disco (IOPS o MBps) posible con una serie DS VM puede verse limitado por número de hello, tamaño y la creación de bandas de hello adjuntan discos.  Para obtener más información, consulte [Premium Storage: almacenamiento de alto rendimiento para cargas de trabajo de máquinas virtuales de Azure](../articles/storage/common/storage-premium-storage.md).


## <a name="d-series"></a>Serie D

ACU: 160

| Tamaño         | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Rendimiento máximo del almacenamiento temporal: E/S por segundo / MBps de lectura / MBps de escritura | Rendimiento máximo por discos de datos: E/S por segundo | Nº máx. NIC / rendimiento de red esperado (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_D11 | 2         | 14          | 100            | 6000 / 93 / 46                                           | 4 / 4x500                         | 2 / 1000                     |
| Standard_D12 | 4         | 28          | 200            | 12000 / 187 / 93                                         | 8 / 8x500                         | 4 / 2000                     |
| Standard_D13 | 8         | 56          | 400            | 24000 / 375 / 187                                        | 16 / 16x500                       | 8 / 4000                     |
| Standard_D14 | 16        | 112         | 800            | 48000 / 750 / 375                                        | 32 / 32x500                       | 8 / 6000 - 8000 &#8224;                |

<br>

