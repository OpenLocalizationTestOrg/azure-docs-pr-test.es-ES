
Hola serie Ls está optimizado para cargas de trabajo que requieren almacenamiento temporal de latencia baja, como las bases de datos NoSQL, incluidos Casandra, MongoDB, Cloudera y Redis. Hola Ls-series ofrece seguridad too32 vCPU, con hello [procesador Intel® Xeon® E5 v3 familia](http://www.intel.com/content/www/us/en/processors/xeon/xeon-e5-solutions.html). Hola serie Ls obtiene Hola el mismo rendimiento de la CPU como Hola G/GS-Series e incluye 8 GiB de memoria por vCPU.  

## <a name="ls-series"></a>Serie Ls

ACU: 180-240
 
| Tamaño          | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Discos de datos máx. | Rendimiento de almacenamiento temporal en caché y máx.: E/S por segundo / MBps (tamaño de caché en GiB) | Rendimiento de disco no en caché máx.: E/S por segundo / Mbps | Nº máx. NIC / rendimiento de red esperado (Mbps) | 
|---------------|-----------|-------------|--------------------------|----------------|-------------------------------------------------------------|-------------------------------------------|------------------------------| 
| Standard_L4s  | 4    | 32   | 678   | 8              | ND / ND (0)          | 5000 / 125                               | 2 / 4000       | 
| Standard_L8s  | 8    | 64   | 1,388 | 16             | ND / ND (0)          | 10 000 / 250                              | 4 / 8000  | 
| Standard_L16s | 16   | 128  | 2,807 | 32             | ND / ND (0)          | 20 000 / 500                              | 8 / 6000 - 16000 &#8224; | 
| Standard_L32s* | 32 | 256  | 5,630 | 64             | ND / ND (0)          | 40 000 / 1000                            | 8 / 20000 | 
 

rendimiento de disco máximo Hola posible con máquinas virtuales de serie Ls puede ser limitado por el número de hello, el tamaño y la creación de bandas de cualquier disco conectado. Para obtener más información, consulte [Premium Storage: almacenamiento de alto rendimiento para cargas de trabajo de máquinas virtuales de Azure](../articles/storage/common/storage-premium-storage.md). 

* Instancia está aislado toohardware tooa dedicado solo cliente.

