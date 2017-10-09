# <a name="back-up-azure-unmanaged-vm-disks-with-incremental-snapshots"></a>Copias de seguridad de discos de máquinas virtuales de Azure no administrados con instantáneas incrementales
## <a name="overview"></a>Información general
Almacenamiento de Azure proporciona funcionalidad de hello tootake instantáneas de blobs. Las instantáneas capturan el estado de blob de hello en ese momento en el tiempo. En este artículo, se describe un escenario para mantener copias de seguridad de discos de máquinas virtuales por medio de instantáneas. Puede usar esta metodología cuando se elige no toouse deseos toocreate una estrategia de copia de seguridad personalizada para los discos de máquina virtual y servicio de recuperación y copia de seguridad de Azure.

Los discos de las máquinas virtuales de Azure se almacenan como blobs en páginas en Almacenamiento de Azure. Puesto que describimos una estrategia de copia de seguridad para los discos de máquina virtual en este artículo, nos referiremos toosnapshots en contexto de Hola de blobs en páginas. toolearn más información acerca de las instantáneas, consulte demasiado[crear una instantánea de un Blob](https://docs.microsoft.com/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob).

## <a name="what-is-a-snapshot"></a>¿Qué es una instantánea?
Una instantánea de blob es una versión de solo lectura de un blob que se ha capturado en un momento dado. Una vez se crea la instantánea, puede leerla, copiarla o eliminarla, pero no modificarla. Las instantáneas proporcionan una tooback forma de un blob tal y como aparece en un momento determinado. Hasta REST versión 2015-04-05, tenía las instantáneas de hello capacidad toocopy completa. Con hello REST versión 08-07-2015 y versiones posteriores, también puede copiar instantáneas incrementales.

## <a name="full-snapshot-copy"></a>Copia de instantáneas completas
Las instantáneas se pueden copiar tooanother cuenta de almacenamiento como una copias de seguridad de blob tookeep del blob base Hola. También puede copiar una instantánea sobre su blob base, que se asemeja a restaurar Hola blob tooan versión anterior. Cuando se copia una instantánea de un tooanother de cuenta de almacenamiento, ocupa Hola mismo espacio como blob en páginas base Hola. Por lo tanto, copiar instantáneas toda desde un tooanother de cuenta de almacenamiento es lento y consume la cantidad de espacio en la cuenta de almacenamiento de destino de Hola.

> [!NOTE]
> Si copia el destino de hello blob base tooanother, instantáneas de Hola de blob de hello no se copian junto con ella. De forma similar, si un blob base se sobrescribe con una copia, instantáneas asociadas al blob base hello no se ven afectadas y bajo nombre de blob de base de Hola.
> 
> 

### <a name="back-up-disks-using-snapshots"></a>Copia de seguridad de discos mediante instantáneas
Como una estrategia de copia de seguridad para los discos de máquina virtual, puede tomar instantáneas periódicas del blob de disco o una página de Hola y cópielos tooanother cuenta de almacenamiento con herramientas como [Copy Blob](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob) operación o [AzCopy](../articles/storage/common/storage-use-azcopy.md). Puede copiar un blob de página de destino de instantánea tooa con un nombre diferente. blob de página de destino resultante Hello es un blob en páginas puede escribir y no es una instantánea. Más adelante en este artículo, describimos las copias de seguridad tootake pasos del uso de instantáneas de discos de máquina virtual.

### <a name="restore-disks-using-snapshots"></a>Restauración de discos mediante instantáneas
Cuando resulte toorestore tiempo su tooa disco estables de versión que se ha capturado previamente en una de las instantáneas de copia de seguridad de hello, puede copiar una instantánea a través de blob en páginas base Hola. Una vez Hola instantánea blob en páginas base toohello promocionadas, Hola instantánea se conserva, pero el origen se sobrescribe con una copia que puede leer y escribir. Más adelante en este artículo se describe los pasos toorestore una versión anterior del disco de la instantánea.

### <a name="implementing-full-snapshot-copy"></a>Implementación de una copia una instantánea completa
Puede implementar una copia instantánea completa haciendo Hola siguiente,

* En primer lugar, cree una instantánea de blob de base de hello mediante hello [Blob de instantánea](https://docs.microsoft.com/rest/api/storageservices/Snapshot-Blob) operación.
* A continuación, copia Hola instantánea tooa destino cuenta de almacenamiento mediante [Copy Blob](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob).
* Repita este proceso toomaintain copias de seguridad de su blob base.

## <a name="incremental-snapshot-copy"></a>Copia de instantáneas incrementales
nueva característica de Hola Hola [GetPageRanges](https://docs.microsoft.com/rest/api/storageservices/Get-Page-Ranges) API proporciona un tooback de manera mucho mejor seguridad de instantáneas de Hola de blobs en páginas o los discos. Hola API devuelve lista Hola de cambios entre blob base Hola e instantáneas de hello, lo que reduce la cantidad de Hola de espacio de almacenamiento utilizado en la cuenta de copia de seguridad de Hola. Hola API es compatible con blobs en páginas en almacenamiento Premium, así como almacenamiento estándar. Gracias a esta API, puede crear soluciones de copia de seguridad más rápidas y eficaces para las máquinas virtuales de Azure. Esta API estará disponible con la versión REST de hello 08-07-2015 y versiones posteriores.

La copia de instantánea incremental permite toocopy desde un almacenamiento cuenta tooanother Hola diferenciar,

* Un blob de base y su instantánea, o bien
* Las dos instantáneas de blob de base de Hola

Siempre que se cumplan Hola condiciones siguientes,

* blob de Hola se creó a partir del 1 de enero de 2016.
* no se sobrescribe el blob de Hello con [PutPage](https://docs.microsoft.com/rest/api/storageservices/Put-Page) o [Copy Blob](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob) entre dos instantáneas.

**Nota**: Esta característica está disponible para los blobs en páginas de Azure premium y estándar.

Cuando tenga una estrategia de copia de seguridad personalizada con instantáneas, copiar instantáneas Hola desde una tooanother de cuenta de almacenamiento puede ser lenta y puede consumir mucho espacio de almacenamiento. En lugar de copiar la cuenta de almacenamiento de copia de seguridad de tooa de hello instantánea completa, puede escribir diferenciar hello en blob de página de copia de seguridad de instantáneas consecutivas tooa. De esta manera, se reduce significativamente Hola tiempo hello y toocopy espacio toostore copias de seguridad.

### <a name="implementing-incremental-snapshot-copy"></a>Implementación de la copia de instantáneas incrementales
Puede implementar la copia de instantánea incremental haciendo Hola siguiente,

* Tomar una instantánea del uso de blob de base de hello [Blob de instantánea](https://docs.microsoft.com/rest/api/storageservices/Snapshot-Blob).
* Copia Hola instantánea toohello destino copia de seguridad cuenta de almacenamiento mediante [Copy Blob](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob). Se trata de un blob en páginas de copia de seguridad Hola. Tomar una instantánea del blob de página de copia de seguridad de Hola y almacenarlo en la cuenta de copia de seguridad de Hola.
* Tome otra instantánea del blob base Hola con Blob de instantánea.
* Obtener la diferencia de hello entre las instantáneas primeros y segunda Hola de hello blob base mediante [GetPageRanges](https://docs.microsoft.com/rest/api/storageservices/Get-Page-Ranges). Usar Hola nuevo parámetro **prevsnapshot**, toospecify Hola valor de fecha y hora de instantánea de Hola que quieres diferencia de hello tooget con. Cuando este parámetro está presente, Hola respuesta REST incluye sólo páginas de Hola que se han cambiado entre la instantánea de destino y anterior incluso borrar páginas.
* Use [PutPage](https://docs.microsoft.com/rest/api/storageservices/Put-Page) tooapply estos blob en páginas de copia de seguridad toohello cambios.
* Por último, tomar una instantánea del blob de página de copia de seguridad de Hola y almacenarlo en la cuenta de almacenamiento de copia de seguridad de Hola.

En la siguiente sección hello, vamos a describir con más detalle cómo puede mantener copias de seguridad de discos mediante la copia de instantánea Incremental

## <a name="scenario"></a>Escenario
En esta sección se describe un escenario en el que se utiliza una estrategia de copia de seguridad personalizada para discos de máquinas virtuales mediante instantáneas.

Considere la posibilidad de usar una VM de Azure de serie DS con un disco P30 de almacenamiento premium conectado. disco de Hello P30 denominado *mypremiumdisk* se almacena en una cuenta de almacenamiento premium denominada *mypremiumaccount*. Llama a una cuenta de almacenamiento estándar *mybackupstdaccount* se usa para almacenar la copia de seguridad de Hola de *mypremiumdisk*. Nos gustaría tookeep una instantánea de *mypremiumdisk* cada 12 horas.

toolearn acerca de cómo crear la cuenta de almacenamiento y los discos, consulte demasiado[cuentas de almacenamiento de Azure sobre](../articles/storage/storage-create-storage-account.md).

toolearn acerca de la copia de seguridad de máquinas virtuales de Azure, consulte demasiado[copias de seguridad de máquina virtual de Azure de Plan](../articles/backup/backup-azure-vms-introduction.md).

## <a name="steps-toomaintain-backups-of-a-disk-using-incremental-snapshots"></a>Copias de seguridad de toomaintain de pasos de un disco con instantáneas incrementales
Hello pasos siguientes se describe cómo las instantáneas de tootake de *mypremiumdisk* y mantener las copias de seguridad de hello en *mybackupstdaccount*. copia de seguridad Hello es un blob en páginas estándar denominado *mybackupstdpageblob*. Hello blob en páginas de copia de seguridad siempre refleja Hola mismo estados como última instantánea de Hola de *mypremiumdisk*.

1. Crear Hola blob en páginas de copia de seguridad para el disco de almacenamiento premium, tomando una instantánea de *mypremiumdisk* llama *mypremiumdisk_ss1*.
2. Copiar este toomybackupstdaccount instantánea como un blob en páginas llama *mybackupstdpageblob*.
3. Realice una instantánea de *mybackupstdpageblob* denominada *mybackupstdpageblob_ss1* con [Instantánea de blob](https://docs.microsoft.com/rest/api/storageservices/Snapshot-Blob) y almacénela en *mybackupstdaccount*.
4. Durante la ventana de copia de seguridad de hello, cree otra instantánea de *mypremiumdisk*, digamos *mypremiumdisk_ss2*y almacenarla en *mypremiumaccount*.
5. Para obtener los cambios incrementales de hello entre las instantáneas de hello dos, *mypremiumdisk_ss2* y *mypremiumdisk_ss1*con [GetPageRanges](https://docs.microsoft.com/rest/api/storageservices/Get-Page-Ranges) en  *mypremiumdisk_ss2* con hello **prevsnapshot** parámetro establece la marca de tiempo de toohello de *mypremiumdisk_ss1*. Escribir estos blob de página de copia de seguridad de los cambios incrementales toohello *mybackupstdpageblob* en *mybackupstdaccount*. Si hay intervalos eliminados en los cambios incrementales de hello, debe borrar de blob de página de copia de seguridad de Hola. Use [PutPage](https://docs.microsoft.com/rest/api/storageservices/Put-Page) blob de página de copia de seguridad de toohello de toowrite cambios incrementales.
6. Tomar una instantánea del blob en páginas de copia de seguridad hello *mybackupstdpageblob*, llamado *mybackupstdpageblob_ss2*. Eliminar la instantánea anterior hello *mypremiumdisk_ss1* de cuenta de almacenamiento premium.
7. Repita los pasos del 4 al 6 en cada ventana de copia de seguridad. De esta forma, puede mantener copias de seguridad de *mypremiumdisk* en una cuenta de almacenamiento estándar.

![Realización de copias de seguridad de discos usando instantáneas incrementales](../articles/virtual-machines/windows/media/incremental-snapshots/storage-incremental-snapshots-1.png)

## <a name="steps-toorestore-a-disk-from-snapshots"></a>Pasos toorestore un disco de instantáneas
Hola lo siguiente, se describen cómo toorestore Hola disco premium, *mypremiumdisk* tooan anteriormente instantánea de la cuenta de almacenamiento de copia de seguridad de hello *mybackupstdaccount*.

1. Identificar el punto de hello en el tiempo que desee toorestore Hola premium disco. Supongamos que es snapshot *mybackupstdpageblob_ss2*, que está almacenado en la cuenta de almacenamiento de copia de seguridad de hello *mybackupstdaccount*.
2. En mybackupstdaccount, promocionará instantánea hello *mybackupstdpageblob_ss2* como blob en páginas de base de copia de seguridad nueva hello *mybackupstdpageblobrestored*.
3. Realice una instantánea de este blob en páginas de copia de seguridad restaurado denominada *mybackupstdpageblobrestored_ss1*.
4. Blob en páginas Hola restaurar copia *mybackupstdpageblobrestored* de *mybackupstdaccount* demasiado*mypremiumaccount* como disco de premium nuevo hello  *mypremiumdiskrestored*.
5. Realice una instantánea de *mypremiumdiskrestored* denominada *mypremiumdiskrestored_ss1* para realizar futuras copias de seguridad incrementales.
6. Punto de serie DS hello toohello restaurar el disco de VM *mypremiumdiskrestored* y separar Hola anterior *mypremiumdisk* de hello máquina virtual.
7. Iniciar proceso de copia de seguridad de hello descrito en la sección anterior para el disco de hello restaurar *mypremiumdiskrestored*, con hello *mybackupstdpageblobrestored* como blob en páginas de copia de seguridad Hola.

![Restauración de discos usando instantáneas](../articles/virtual-machines/windows/media/incremental-snapshots/storage-incremental-snapshots-2.png)

## <a name="next-steps"></a>Pasos siguientes
Siguiente Hola de uso vincula toolearn más información sobre la creación de instantáneas de un blob y planear la infraestructura de copia de seguridad de la máquina virtual.

* [Crear una instantánea de un blob](https://docs.microsoft.com/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob)
* [Planeación de la infraestructura de copia de seguridad de máquinas virtuales](../articles/backup/backup-azure-vms-introduction.md)

