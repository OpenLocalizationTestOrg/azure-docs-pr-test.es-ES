<!-- A-series - compute-intensive instances, H-series -->

Hello tamaños A8 A11 y H-series son también se denomina *instancias de proceso intensivo*. hardware de Hola que ejecuta estos tamaños está diseñado y optimizado para el proceso intensivo y aplicaciones, modelado y simulaciones de clúster de aplicaciones de red intensiva, incluido informática de alto rendimiento (HPC). Hola A8 A11 serie utiliza Intel Xeon E5-2670 a 2,6 GHZ y Hola H-series utiliza Intel Xeon E5-2667 v3 @ 3,2 GHz. 

Máquinas virtuales de Azure H-series son Hola siguiente generación informática de alto rendimiento que las máquinas virtuales dirigidas a las necesidades de cálculo de high-end, como modelado molecular y dinámica de fluidos computacional. Estas 8 y 16 vCPU máquinas virtuales se compilan en la tecnología de procesador de hello Intel 2667 Haswell E5 V3 que incluye DDR4 memoria y almacenamiento temporal basada en SSD. 

Además toohello gran potencia de la CPU, Hola H-series ofrece diversas opciones para las redes de RDMA de latencia baja mediante FDR InfiniBand y varias configuraciones toosupport memoria intensivas cálculo requisitos de memoria.



## <a name="h-series"></a>Serie H

ACU: 290-300

| Tamaño | vCPU | Memoria: GiB | GiB de almacenamiento temporal (SSD) | Discos de datos máx. | Rendimiento de discos máx.: E/S por segundo | Nº máx. NIC |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_H8 |8 |56 |1000 |16 |16 x 500 |2  |
| Standard_H16 |16 |112 |2000 |32 |32 x 500 |4 |
| Standard_H8m |8 |112 |1000 |16 |16 x 500 |2  |
| Standard_H16m |16 |224 |2000 |32 |32 x 500 |4  |
| Standard_H16r* |16 |112 |2000 |32 |32 x 500 |4  |
| Standard_H16mr* |16 |224 |2000 |32 |32 x 500 |4 |

* Para las aplicaciones MPI, la red de back-end RDMA dedicada está habilitada por la red InfiniBand FDR, que ofrece una latencia sumamente baja y un alto ancho de banda.

<br>



## <a name="a-series---compute-intensive-instances"></a>Serie A: instancias de proceso intensivo

ACU: 225

| Tamaño | vCPU | Memoria: GiB | Almacenamiento temporal (HDD): GiB | Discos de datos máx. | Rendimiento de discos de datos máx.: E/S por segundo | Nº máx. NIC|
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A8* |8 |56 |382 |16 |16x500 |2 |
| Standard_A9* |16 |112 |382 |16 |16x500 |4 |
| Standard_A10 |8 |56 |382 |16 |16x500 |2  |
| Standard_A11 |16 |112 |382 |16 |16x500 |4 |

* Para las aplicaciones MPI, la red de back-end RDMA dedicada está habilitada por la red InfiniBand FDR, que ofrece una latencia sumamente baja y un alto ancho de banda.

<br>



