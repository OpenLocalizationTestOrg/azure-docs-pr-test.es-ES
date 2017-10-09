
## <a name="size-table-definitions"></a>Definiciones de tabla de tamaño

- La capacidad de almacenamiento se muestra en unidades de GiB o 1024^3 bytes. Al comparar discos medido en GB (1000 ^ 3 bytes) toodisks medido en GiB (1024 ^ 3) Recuerde que los números de capacidad en GiB pueden aparecer más pequeños. Por ejemplo, 1023 GiB = 1098.4 GB
- Se midió el rendimiento de disco en operaciones de entrada/salida por segundo (E/S por segundo) y Mbps, donde Mbps = 10^6 bytes/s.
- Los discos de datos pueden funcionar en modo en caché o en modo no en caché. Para la operación de disco de datos almacenados en caché, modo de caché de host de Hola se establece demasiado**ReadOnly** o **ReadWrite**.  Para la operación de disco de datos sin almacenar en caché, modo de caché de host de Hola se establece demasiado**ninguno**.
- **Se esperaba el rendimiento de la red** es Hola agregados ancho de banda máximo asignado por el tipo de máquina virtual en todos los NIC, para todos los destinos. Límites superiores no se garantiza que, pero son instrucciones tooprovide previsto para la selección de tipo VM correcto de hello para la aplicación hello prevista. El rendimiento de red real dependerá de diversos factores (como, por ejemplo, la congestión de la red, las cargas de la aplicación y la configuración de red). Para más información acerca de cómo optimizar el rendimiento de red, consulte [Optimización del rendimiento de red para Windows y Linux](../articles/virtual-network/virtual-network-optimize-network-bandwidth.md). Hola tooachieve espera el rendimiento de la red en Linux o Windows, podría estar tooselect necesaria una versión concreta u optimizar la máquina virtual. Para obtener más información, consulte [cómo probar tooreliably para el rendimiento de la máquina virtual](../articles/virtual-network/virtual-network-bandwidth-testing.md).

- &#8224; rendimiento de 16 vCPU constantemente alcanzará el límite superior de hello en una próxima versión.


