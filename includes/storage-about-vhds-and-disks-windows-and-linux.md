
## <a name="about-vhds"></a>Acerca de los discos duros virtuales

Hola VHD que se usa en Azure son archivos .vhd almacenados como blobs de página en una cuenta de almacenamiento standard o premium de Azure. Para obtener información detallada sobre blobs en páginas, consulte [Introducción a los blobs en bloques y a los blobs en páginas](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs/). Para más información sobre Premium Storage, consulte [Premium Storage de alto rendimiento y máquinas virtuales de Azure](../articles/storage/common/storage-premium-storage.md).

Azure admite Hola formato de disco VHD fijo. establece de formato fijada de Hola Hola disco lógico out linealmente en archivo hello, por lo que ese desplazamiento X del disco se almacena en el desplazamiento de blob X. Un pequeño pie de página al final de hello del blob de Hola describe las propiedades de Hola de hello VHD. A menudo, formato fijo Hola desperdicia espacio porque la mayoría de los discos tiene intervalos grandes sin utilizar en ellos. Sin embargo, Azure almacena archivos .vhd en un formato disperso, para ofrecer beneficios Hola ambos Hola fijos y los discos dinámicos en hello mismo tiempo. Para obtener más información, consulte [Introducción a los discos duros virtuales](https://technet.microsoft.com/library/dd979539.aspx).

Todos los archivos .vhd en Azure que desea toouse como un disco de origen toocreate o imágenes son de solo lectura. Cuando se crea un disco o una imagen, Azure hace copias de hello archivos .vhd. Estas copias pueden ser de solo lectura o lectura y escritura, dependiendo de cómo utilice Hola VHD.

Cuando se crea una máquina virtual desde una imagen, Azure crea un disco de máquina virtual de Hola que es una copia del archivo .vhd de origen Hola. tooprotect la eliminación accidental, Azure coloca una concesión en cada archivo .vhd de origen que se usó toocreate una imagen, un disco del sistema operativo o un disco de datos.

Antes de poder eliminar un archivo .vhd, necesitará concesión de hello tooremove eliminando Hola disco o una imagen. toodelete un archivo .vhd que se está usando una máquina virtual como un disco del sistema operativo, puede eliminar máquina virtual de hello, el disco del sistema operativo de Hola y archivo .vhd de origen de Hola a la vez eliminando la máquina virtual de Hola y eliminando todos los discos asociados. Sin embargo, para eliminar un archivo .vhd que es el origen de un disco de datos es necesario realizar varios pasos en un orden determinado. Primero desasociar el disco de hello de la máquina virtual de hello, y luego eliminar Hola disco y, a continuación, elimine el archivo .vhd de hello.

> [!WARNING]
> Si elimina un archivo .vhd de origen del almacenamiento o elimina la cuenta de almacenamiento, Microsoft no puede recuperar esos datos por usted.
> 

## <a name="types-of-disks"></a>Tipos de discos 

Los discos de Azure están diseñados para ofrecer una disponibilidad del 99,999 %. Los discos de Azure ofrecen durabilidad de nivel empresarial, con una tasa de error anualizada del 0 %.

Hay dos niveles de rendimiento para el almacenamiento que puede elegir al crear los discos: almacenamiento estándar y Premium Storage. Además, hay dos tipos de discos, no administrados y administrados, y pueden residir en cualquier nivel de rendimiento.


### <a name="standard-storage"></a>Standard Storage 

El almacenamiento estándar está respaldado por unidades de disco duro y ofrece un almacenamiento rentable al mismo tiempo que tiene un rendimiento superior. El almacenamiento estándar se puede replicar de forma local en un centro de datos, o tener redundancia geográfica con centros de datos principales y secundarios. Para más información sobre la replicación almacenamiento, consulte [Replicación de Azure Storage](../articles/storage/common/storage-redundancy.md). 

Para más información sobre el uso del almacenamiento estándar con discos de máquina virtual, consulte el artículo sobre [Almacenamiento estándar y discos](../articles/storage/common/storage-standard-storage.md).

### <a name="premium-storage"></a>Premium Storage 

Premium Storage está respaldado por discos SSD y ofrece compatibilidad con discos de alto rendimiento y baja latencia para máquinas virtuales con cargas de trabajo intensivas de E/S. Puede usar Premium Storage con máquinas virtuales de Azure de las series DS, DSv2, GS, Ls o FS. Para más información, consulte [Premium Storage](../articles/storage/common/storage-premium-storage.md).

### <a name="unmanaged-disks"></a>Discos no administrados

Los discos no administrados son tipo tradicional de Hola de discos que se han usado en las máquinas virtuales. Con esto, cree su propia cuenta de almacenamiento y especificar esa cuenta de almacenamiento al crear el disco de Hola. Tendrá que asegurarse de no colocar demasiados discos toomake Hola la misma cuenta de almacenamiento, porque podría superar hello [objetivos de escalabilidad](../articles/storage/common/storage-scalability-targets.md) de cuenta de almacenamiento de hello (20.000 IOPS, por ejemplo), lo que resulta en Hola máquinas virtuales que se está limitadas. Con los discos no administrados, deberá toofigure cómo usar toomaximize Hola de uno o más cuentas tooget Hola mejor rendimiento de almacenamiento fuera de las máquinas virtuales.

### <a name="managed-disks"></a>Discos administrados 

Administrar controladores de discos almacenamiento Hola cuenta creación y administración en segundo plano de Hola y garantiza que no tengan tooworry acerca de los límites de escalabilidad de Hola de cuenta de almacenamiento de Hola. Simplemente especifique el tamaño del disco de Hola y nivel de rendimiento de hello (estándar o Premium) y Azure crea y administra el disco de hello en su nombre. Incluso a medida que agregue más discos o escala vertical y horizontalmente Hola VM, no tienes tooworry sobre el almacenamiento de Hola que se va a usar. 

También puede administrar sus imágenes personalizadas en una cuenta de almacenamiento por cada región de Azure y usarlos toocreate cientos de máquinas virtuales en hello misma suscripción. Para obtener más información acerca de los discos administrados, vea hello [información general de discos administradas](../articles/virtual-machines/windows/managed-disks-overview.md).

Se recomienda encarecidamente usar discos de Azure administrados para nuevas máquinas virtuales y convertir los discos de toomanaged anterior de discos no administrado, tootake aprovechar Hola muchas características disponibles en discos administrados.

### <a name="disk-comparison"></a>Comparación de discos

Hello en la tabla siguiente proporciona una comparación de vs Premium estándar para ambos administrado y no administrado toohelp discos decidir qué toouse.

|    | Disco Premium de Azure | Disco Estándar de Azure |
|--- | ------------------ | ------------------- |
| Tipo de disco | Unidades de estado sólido (SSD) | Unidades de disco duro (HDD)  |
| Información general  | Compatibilidad con discos de alto rendimiento y baja latencia basados en SSD para máquinas virtuales que ejecutan cargas de trabajo intensivas de E/S o que hospedan un entorno de producción crítico | Compatibilidad rentable con discos basados en HHD para escenarios de máquinas virtuales de desarrollo o pruebas |
| Escenario  | Cargas de trabajo confidenciales de producción y rendimiento | Desarrollo y pruebas, no crítico, <br>Acceso infrecuente |
| Tamaño del disco | P4: 32 GB (solo Managed Disks)<br>P6: 64 GB (solo Managed Disks)<br>P10: 128 GB<br>P20: 512 GB<br>P30: 1024 GB<br>P40: 2048 GB<br>P50: 4095 GB | Discos no administrados: de 1 GB a 4 TB (4095 GB) <br><br>Discos administrados:<br> S4: 32 GB <br>S6: 64 GB <br>S10: 128 GB <br>S20: 512 GB <br>S30: 1024 GB <br>S40: 2048 GB<br>S50: 4095 GB| 
| Rendimiento máximo por disco | 250 MB/s | 60 MB/s | 
| IOPS máximas por disco | 7500 IOPS | 500 IOPS | 

