---
title: "máquinas virtuales de aaaMigrating tooAzure almacenamiento Premium | Documentos de Microsoft"
description: "Migre su tooAzure de máquinas virtuales existente almacenamiento Premium. El Almacenamiento premium le ofrece compatibilidad con discos de alto rendimiento y baja latencia para cargas de trabajo con un uso intensivo de E/S, que se ejecutan en máquinas virtuales de Azure."
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: cd812bdbe39f43fe053a998d96788045d5a43258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a>Migrar tooAzure almacenamiento Premium (discos no administrada)

> [!NOTE]
> Este artículo describe cómo toomigrate una máquina virtual que utiliza discos estándar no administrado tooa máquina virtual que usa no administrada de discos premium. Se recomienda utilizar discos de Azure administrados para nuevas máquinas virtuales y que convierta los discos de toomanaged anterior de discos no administrado. Administrar cuentas de almacenamiento subyacentes de discos identificador hello por lo que no es necesario. Para obtener más información, consulte [Managed Disks Overview](storage-managed-disks-overview.md) (Información general sobre Managed Disks).
>

El Almacenamiento premium de Azure le ofrece soporte de disco de alto rendimiento y latencia baja para máquinas virtuales con cargas de trabajo intensivas de E/S. Puede sacar partido de velocidad de Hola y el rendimiento de estos discos al migrar tooAzure discos de máquina virtual de su aplicación almacenamiento Premium.

Hola de esta guía sirve toohelp nuevos usuarios de almacenamiento de Azure Premium mejor preparación toomake una transición sin problemas desde su tooPremium de sistema almacenamiento actual. Guía de Hello direcciones tres componentes clave de hello en este proceso:

* [Planear la migración de hello tooPremium almacenamiento](#plan-the-migration-to-premium-storage)
* [Preparar y discos duros virtuales (VHD) de copia tooPremium almacenamiento](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [Creación de una máquina virtual de Azure mediante Premium Storage](#create-azure-virtual-machine-using-premium-storage)

Puede migrar las máquinas virtuales de otra tooAzure plataformas almacenamiento Premium o migrar máquinas virtuales de Azure existente de almacenamiento estándar tooPremium almacenamiento. En esta guía se describen los pasos para ambos escenarios. Siga los pasos de hello especificados en sección relevantes de hello según el escenario.

> [!NOTE]
> Encontrará una introducción a las características y los precios de Premium Storage en [Premium Storage: almacenamiento de alto rendimiento para cargas de trabajo de máquinas virtuales de Azure](storage-premium-storage.md). Se recomienda migrar cualquier disco de máquina virtual que requieren alta IOPS tooAzure almacenamiento Premium para mejorar el rendimiento de la aplicación hello. Si el disco no requiere un número elevado de operaciones de entrada/salida por segundo, puede limitar los costos mediante el mantenimiento del almacenamiento estándar, que almacena los datos de disco de máquina virtual en unidades de disco duro (HDD) en lugar de SSD.
>

Completar el proceso de migración de hello en su totalidad puede requerir alguna acción adicional antes y después de los pasos de hello proporcionados en esta guía. Algunos ejemplos son la configuración de redes virtuales o los puntos de conexión o de realizar cambios de código dentro de la aplicación hello propio y lo que puede requerir algún tiempo de inactividad en la aplicación. Estas acciones son tooeach único de la aplicación y se debe completar junto con los pasos de hello proporcionadas en este tooPremium de transición completa de hello guía toomake máxima uniformidad posible de almacenamiento.

## <a name="plan-the-migration-to-premium-storage"></a>Planear la migración de hello tooPremium almacenamiento
En esta sección se asegura de que está listo toofollow pasos de migración de hello en este artículo y le ayuda a mejor decisión de Hola de toomake en tipos de máquina virtual y disco.

### <a name="prerequisites"></a>Requisitos previos
* Necesitará una suscripción de Azure. Si no tiene ninguna, puede crear una suscripción de [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/) de un mes o visitar la página [Precios de Azure](https://azure.microsoft.com/pricing/) para conocer más opciones.
* tooexecute cmdlets de PowerShell, deberá módulo de Microsoft Azure PowerShell Hola. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para hello instalar punto e instrucciones de instalación.
* Cuando planee toouse Azure VM que se ejecutan en almacenamiento Premium, debe toouse Hola máquinas virtuales con capacidad de almacenamiento Premium. Puede usar discos de almacenamiento Estándar y Premium Storage con las máquinas virtuales compatibles con Premium Storage. Los discos de almacenamiento Premium estarán disponibles con más tipos VM en hello futuras. Para obtener más información sobre todos los tamaños y tipos de disco de máquina virtual de Azure disponibles, consulte [Tamaños de máquinas virtuales](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) y [Tamaños de Cloud Services](../cloud-services/cloud-services-sizes-specs.md).

### <a name="considerations"></a>Consideraciones
Una VM de Azure admite la asociación varios discos de almacenamiento Premium para que las aplicaciones pueden tener hasta too256 TB de almacenamiento por máquina virtual. Con el Almacenamiento premium, las aplicaciones pueden tener hasta 80.000 E/S por segundo (operaciones de entrada/salida por segundo) por máquina virtual, así como un rendimiento del disco de 2.000 MB por segundo por máquina virtual, con latencias extremadamente bajas para operaciones de lectura. Dispone de opciones en varias máquinas virtuales y discos. Esta sección es toohelp toofind una opción que mejor se adapte a la carga de trabajo.

#### <a name="vm-sizes"></a>Tamaños de VM
se enumeran las especificaciones de tamaño de máquina virtual de Azure de Hello en [tamaños de máquinas virtuales](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Revise las características de rendimiento de Hola de máquinas virtuales que funcionen con el almacenamiento Premium y elija el tamaño más adecuado de hello máquina virtual que mejor se adapte a la carga de trabajo. Asegúrese de que hay suficiente ancho de banda disponible en el tráfico de disco de máquina virtual toodrive Hola.

#### <a name="disk-sizes"></a>Tamaños de disco
Hay tres tipos de discos que se pueden usar con las máquinas virtuales y cada uno de ellos tiene sus límites específicos de rendimiento y E/S por segundo. Tenga en cuenta estos límites al elegir tipo de disco de hello para la máquina virtual en función de necesidades de saludo de la aplicación en cuanto a capacidad, rendimiento, escalabilidad, y la carga máxima.

| Tipo de discos Premium  | P10   | P20   | P30            | P40            | P50            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| Tamaño del disco           | 128 GB| 512 GB| 1.024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 
| IOPS por disco       | 500   | 2300  | 5000           | 7500           | 7500           | 
| Rendimiento de disco | 100 MB por segundo | 150 MB por segundo | 200 MB por segundo | 250 MB por segundo | 250 MB por segundo |

Dependiendo de la carga de trabajo, decida si son necesarios más discos de datos para la máquina virtual. Puede adjuntar varios datos persistentes discos tooyour máquina virtual. Si es necesario, puede crear bandas en capacidad de hello discos tooincrease Hola y el rendimiento de volumen de Hola. (Consulte qué es el seccionamiento de discos [aquí](storage-premium-storage-performance.md#disk-striping)). Si secciona discos de datos de Premium Storage mediante [Espacios de almacenamiento][4], tendrá que configurarlos con una columna por cada disco que use. En caso contrario, hello general rendimiento del volumen de hello particionado puede ser menor del esperado debido toouneven distribución del tráfico en varios discos de Hola. Para máquinas virtuales Linux pueden usar hello *mdadm* tooachieve utilidad Hola igual. Vea el artículo [Configuración del software RAID en Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para más información.

#### <a name="storage-account-scalability-targets"></a>Objetivos de escalabilidad de la cuenta de almacenamiento
Cuentas de almacenamiento Premium tienen Hola siguientes destinos de escalabilidad en suma toohello [objetivos de rendimiento y escalabilidad de almacenamiento de Azure](storage-scalability-targets.md). Si los requisitos de su aplicación superan los objetivos de escalabilidad de Hola de una única cuenta de almacenamiento, compilar su aplicación toouse varias cuentas de almacenamiento y dividir los datos en esas cuentas de almacenamiento.

| Capacidad total de la cuenta | Ancho de banda total de una cuenta de almacenamiento con redundancia local |
|:--- |:--- |
| Capacidad de disco: 35 TB<br />Capacidad de instantánea: 10 TB |Seguridad too50 gigabits por segundo entrante + saliente |

Hola a para obtener más información acerca de las especificaciones de almacenamiento Premium, visite [objetivos de escalabilidad y rendimiento al usar almacenamiento Premium](storage-premium-storage.md#scalability-and-performance-targets).

#### <a name="disk-caching-policy"></a>Directiva de almacenamiento en caché de disco
De forma predeterminada, es la directiva de caché de disco *de sólo lectura* de Hola a todos los discos de datos Premium, y *lectura y escritura* para el disco del sistema operativo Hola Premium asocia toohello máquina virtual. Esta opción de configuración se recomienda tooachieve Hola un rendimiento óptimo para IOs la aplicación. Para discos de datos de solo escritura o de gran cantidad de escritura (por ejemplo, archivos de registro de SQL Server), deshabilite el almacenamiento en caché de disco para lograr un mejor rendimiento de la aplicación. configuración de la caché de Hola para discos de datos existentes se puede actualizar con [Portal de Azure](https://portal.azure.com) o hello *- HostCaching* parámetro de hello *Set-AzureDataDisk* cmdlet.

#### <a name="location"></a>Ubicación
Elija una ubicación donde el Almacenamiento premium de Azure esté disponible. Consulte [Servicios de Azure por región](https://azure.microsoft.com/regions/#services) para obtener información actualizada sobre las ubicaciones disponibles. Máquinas virtuales ubicadas en hello misma región como lo Hola cuenta de almacenamiento que almacenes Hola discos para hello VM le proporcionará un rendimiento mucho mejor que si están en regiones independientes.

#### <a name="other-azure-vm-configuration-settings"></a>Otras opciones de configuración de máquina virtual de Azure
Al crear una máquina virtual de Azure, estará más frecuentes tooconfigure ciertas opciones de configuración de máquina virtual. Recuerde que algunos valores son fijos para duración de Hola de Hola de máquina virtual, mientras que puede modificar o agregar otros. Revise estos valores de configuración de máquina virtual de Azure y asegúrese de que se trata configurado adecuadamente toomatch sus requisitos de carga de trabajo.

### <a name="optimization"></a>Optimización
En [Azure Premium Storage: diseño de alto rendimiento](storage-premium-storage-performance.md) se proporcionan instrucciones para crear aplicaciones de alto rendimiento con Azure Premium Storage. Puede seguir directrices de hello combinadas con mejor tootechnologies de aplicable de prácticas rendimiento que usa la aplicación.

## <a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Preparar y copie tooPremium almacenamiento de discos duros virtuales (VHD)
Hola pasos de la sección proporciona instrucciones para preparar los discos duros virtuales de la máquina virtual y copiar discos duros virtuales tooAzure almacenamiento.

* [Escenario 1: "Estoy migrando tooAzure de máquinas virtuales de Azure existente almacenamiento Premium."](#scenario1)
* [Escenario 2: "Estoy migrar varias VM desde otro tooAzure plataformas almacenamiento Premium."](#scenario2)

### <a name="prerequisites"></a>Requisitos previos
Hola tooprepare discos duros virtuales para la migración, necesitará:

* Una suscripción de Azure, una cuenta de almacenamiento y un contenedor en el que el almacenamiento de la cuenta toowhich puede copiar el disco duro virtual. Tenga en cuenta que cuenta de almacenamiento de destino de hello puede ser una cuenta estándar o Premium almacenamiento según sus necesidades.
* Hola de toogeneralize de herramienta VHD si tiene previsto toocreate varias instancias VM del mismo. Por ejemplo, sysprep para Windows o virt sysprep para Ubuntu.
* Una herramienta tooupload Hola VHD archivo toohello cuenta de almacenamiento. Vea [transferir datos con la utilidad de línea de comandos de AzCopy hello](storage-use-azcopy.md) o usar un [el Explorador de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx). Esta guía describe copiar el disco duro virtual mediante la herramienta de AzCopy Hola.

> [!NOTE]
> Si elige la opción de copia sincrónica con AzCopy, para un rendimiento óptimo, copie el disco duro virtual mediante la ejecución de una de estas herramientas desde una máquina virtual de Azure que se encuentra en hello misma región que la cuenta de almacenamiento de destino de Hola. Si está copiando un VHD de una máquina virtual de Azure en una región distinta, el rendimiento puede ser más lento.
>
> Para copiar una gran cantidad de datos a través de ancho de banda limitado, considere la posibilidad de [con hello importación/exportación de Azure servicio tootransfer datos tooBlob almacenamiento](storage-import-export-service.md); Esto le permite tootransfer tooan Azure las unidades de los datos por disco duro de envío Centro de datos. Puede usar Hola importación/exportación de Azure servicio toocopy datos tooa cuenta de almacenamiento estándar solo. Una vez que los datos de hello están en su cuenta de almacenamiento estándar, puede usar cualquier hello [API de copia de Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) o cuenta de almacenamiento premium de AzCopy tootransfer Hola datos tooyour.
>
> Tenga en cuenta que Microsoft Azure solo admite archivos VHD de tamaño fijo. No se admiten archivos VHDX ni discos duros virtuales dinámicos. Si tiene un disco duro virtual dinámico, se puede convertir mediante Hola de tamaño de toofixed [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.
>
>

### <a name="scenario1"></a>Escenario 1: "Estoy migrando tooAzure de máquinas virtuales de Azure existente almacenamiento Premium."
Si va a migrar existente máquinas virtuales de Azure, Hola de detención de máquina virtual, preparar los discos duros virtuales por tipo de Hola de disco duro virtual que desee y, a continuación, copie Hola VHD con AzCopy o PowerShell.

Hola VM debe toobe completamente hacia abajo toomigrate un estado limpio. Habrá un tiempo de inactividad hasta que se complete la migración de Hola.

#### <a name="step-1-prepare-vhds-for-migration"></a>Paso 1. Preparar los VHD para la migración
Si va a migrar tooPremium de máquinas virtuales de Azure existente almacenamiento, puede ser el disco duro virtual:

* Una imagen del sistema operativo generalizado
* Un disco del sistema operativo exclusivo
* Un disco de datos

A continuación se describen estos tres escenarios para preparar un disco duro virtual.

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a>Usar un toocreate de disco duro virtual de sistema operativo generalizado varias instancias de máquina virtual
Si va a cargar un disco duro virtual que será usado toocreate varias instancias de máquina virtual de Azure genéricas, en primer lugar debe generalizar VHD con una utilidad de sysprep. Esto aplica tooa disco duro virtual que es local o en la nube de Hola. Sysprep quita cualquier información específica de la máquina de hello VHD.

> [!IMPORTANT]
> Realice una instantánea o copia de seguridad de la máquina virtual antes de generalizarla. Ejecutar sysprep se detenga y se cancela la asignación de instancia de la máquina virtual de Hola. Siga estos pasos toosysprep un VHD de sistema operativo de Windows. Tenga en cuenta que ejecuta el comando Sysprep de hello, deberá tooshut hacia abajo de la máquina virtual de Hola. Para obtener más información sobre Sysprep, consulte [Introducción a Sysprep](http://technet.microsoft.com/library/hh825209.aspx) o [Referencia técnica de Sysprep](http://technet.microsoft.com/library/cc766049.aspx).
>
>

1. Abra una ventana de símbolo del sistema como administrador.
2. Escriba Hola después tooopen comando Sysprep:

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. Hola herramienta de preparación del sistema, seleccione sistema Out-of-Box experiencia configuración rápida (OOBE), seleccione Hola generalizar casilla, seleccione **apagado**y, a continuación, haga clic en **Aceptar**, tal y como se muestra en la imagen de hello siguiente. Sysprep se generalizar el sistema operativo de Hola y apagar el sistema de Hola.

    ![][1]

Para una VM Ubuntu, use sysprep virt tooachieve Hola igual. Vea [sysprep virt](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) para más información. Vea también algunos de código abierto de hello [software de aprovisionamiento del servidor Linux](http://www.cyberciti.biz/tips/server-provisioning-software.html) para otros sistemas operativos Linux.

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a>Usar un único toocreate de sistema operativo VHD una única instancia de máquina virtual
Si tiene una aplicación que se ejecuta en hello VM que requiere datos específicos de la máquina de hello, no generalice Hola VHD. Un disco duro virtual generalizado no puede ser toocreate usa una única instancia de máquina virtual de Azure. Por ejemplo, si tiene el controlador de dominio en el disco duro virtual, ejecutar sysprep lo anulará como controlador de dominio. Revisar aplicaciones Hola que se ejecutan en la máquina virtual y Hola el impacto de ejecutar sysprep en ellos antes de generalizar Hola VHD.

##### <a name="register-data-disk-vhd"></a>Registro de VHD de disco de datos
Si tiene discos de datos en Azure toobe migrar, debe procurar seguro de máquinas virtuales de Hola que utilizan estos datos se apagan discos.

Siga los pasos de Hola se describe a continuación toocopy VHD tooAzure almacenamiento Premium y registrarlo como un disco de datos aprovisionado.

#### <a name="step-2-create-hello-destination-for-your-vhd"></a>Paso 2: Crear destino de hello para el disco duro virtual
Cree una cuenta de almacenamiento para mantener los discos duros virtuales. Considere la posibilidad de hello siguientes puntos cuando planee dónde toostore los discos duros virtuales:

* destino de Hello cuenta de almacenamiento Premium.
* ubicación Hello de la cuenta de almacenamiento debe ser igual que el almacenamiento Premium compatible con máquinas virtuales de Azure que creará en la fase final de Hola. Podría copiar tooa nueva cuenta de almacenamiento u Hola de toouse plan misma cuenta de almacenamiento según sus necesidades.
* Copie y guarde la clave de cuenta de almacenamiento de Hola de cuenta de almacenamiento de destino de hello para la fase siguiente de Hola.

En los discos de datos, puede elegir tookeep algunos discos de datos en una cuenta de almacenamiento estándar (por ejemplo, los discos que tienen almacenamiento mejor refrigeración), pero se recomienda encarecidamente que mover todos los datos de almacenamiento de información premium toouse de carga de trabajo de producción.

#### <a name="copy-vhd-with-azcopy-or-powershell"></a>Paso 3. Copiar un VHD con AzCopy o PowerShell
Necesitará toofind la ruta de acceso del contenedor y la cuenta tooprocess clave cualquiera de estas dos opciones de almacenamiento. Tanto una como otra pueden encontrarse en **Azure Portal** > **Storage**. dirección URL del contenedor Hola será como "https://myaccount.blob.core.windows.net/mycontainer/".

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a>Opción 1: Copiar un VHD con AzCopy (copia asincrónica)
AzCopy puede cargar fácilmente Hola VHD a través de Internet de Hola. Función tamaño Hola de hello discos duros virtuales, esto puede tardar tiempo. Recuerde límites de entrada/salida de la cuenta de almacenamiento de toocheck hello cuando utilice esta opción. Vea [Objetivos de escalabilidad y rendimiento del almacenamiento en Azure](storage-scalability-targets.md) para obtener detalles.

1. Descargue e instale AzCopy desde aquí: [versión más reciente de AzCopy](http://aka.ms/downloadazcopy)
2. Abra PowerShell de Azure y carpeta toohello vaya donde está instalado AzCopy.
3. Archivo de disco duro virtual de hello toocopy de "Origen" de comando siguiente de Hola de uso demasiado "Destino".

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    Ejemplo:

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    Estas son las descripciones de parámetros de hello utilizados en hello AzCopy comando:

   * **El código fuente:  *&lt;origen&gt;:***  ubicación de carpeta de Hola o dirección URL del contenedor de almacenamiento que contiene Hola VHD.
   * **/ SourceKey:  *&lt;clave de la cuenta de origen&gt;:***  clave de cuenta de almacenamiento de la cuenta de almacenamiento de origen de Hola.
   * **/ Dest:  *&lt;destino&gt;:***  toocopy de dirección URL del contenedor de almacenamiento Hola disco duro virtual.
   * **/ DestKey:  *&lt;clave de cuenta dest&gt;:***  clave de cuenta de almacenamiento de la cuenta de almacenamiento de destino de Hola.
   * **/ Patrón:  *&lt;nombre de archivo&gt;:***  especificar el nombre de archivo de Hola de hello toocopy de disco duro virtual.

Para obtener más información sobre el uso de AzCopy herramienta, consulte [transferir datos con la utilidad de línea de comandos de AzCopy hello](storage-use-azcopy.md).

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a>Opción 2: Copiar un VHD con PowerShell (copia sincronizada)
También puede copiar el archivo VHD de hello mediante el cmdlet de PowerShell de hello AzureStorageBlobCopy de inicio. Usar hello siguiente comando de PowerShell de Azure toocopy disco duro virtual. Reemplazar valores de hello en <> con los valores correspondientes de la cuenta de almacenamiento de origen y de destino. toouse este comando, debe tener un contenedor denominado discos duros virtuales en la cuenta de almacenamiento de destino. Si no existe el contenedor de hello, crear uno antes de ejecutar el comando de Hola.

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

Ejemplo:

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <a name="scenario2"></a>Escenario 2: "Estoy migrar varias VM desde otro tooAzure plataformas almacenamiento Premium."
Si va a migrar el disco duro virtual de almacenamiento en nube que no Azure tooAzure, primero debe exportar el directorio local de hello VHD tooa. Tiene la ruta de acceso de origen completa de hello del directorio local Hola donde se almacena los VHD práctica y, a continuación, utilizando tooupload AzCopy se tooAzure almacenamiento.

#### <a name="step-1-export-vhd-tooa-local-directory"></a>Paso 1. Exportar el directorio local de disco duro virtual tooa
##### <a name="copy-a-vhd-from-aws"></a>Copia de un VHD desde AWS
1. Si usas AWS, exportar Hola EC2 instancia tooa disco duro virtual en un depósito de S3 de Amazon. Siga los pasos de hello descritos en la documentación de Amazon de herramienta de interfaz de línea de comandos (CLI) de exportación de Amazon EC2 instancias tooinstall Hola Amazon EC2 hello y ejecutar archivo VHD de hello comando Crear-instancia-export-tarea tooexport Hola EC2 instancia tooa. Ser seguro toouse **VHD** para hello disco &#95; imagen &#95; Variable de formato cuando se ejecuta hello **crear instancia-export-tareas** comando. Hello VHD archivo exportado se guarda en el cubo de hello Amazon S3 que designar durante ese proceso.

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. Descargar archivo de disco duro virtual de hello de depósito de S3 Hola. Archivo VHD Hola seleccione, a continuación, **acciones** > **descargar**.

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a>Copia un VHD de una nube que no es de Azure
Si va a migrar el disco duro virtual de almacenamiento en nube que no Azure tooAzure, primero debe exportar el directorio local de hello VHD tooa. Copiar ruta de acceso de origen completa de hello del directorio local Hola donde se almacena los VHD.

##### <a name="copy-a-vhd-from-on-premises"></a>Copia de un VHD desde un entorno local
Si está migrando VHD desde un entorno local, necesitará la ruta de acceso de origen completa de Hola donde se almacena los VHD. ruta de acceso de origen de Hello podría ser un recurso compartido de archivo o ubicación de servidor.

#### <a name="step-2-create-hello-destination-for-your-vhd"></a>Paso 2: Crear destino de hello para el disco duro virtual
Cree una cuenta de almacenamiento para mantener los discos duros virtuales. Considere la posibilidad de hello siguientes puntos cuando planee dónde toostore los discos duros virtuales:

* cuenta de almacenamiento de destino de Hello podría ser almacenamiento standard o premium según sus necesidades de aplicación.
* región Hello de la cuenta de almacenamiento debe ser igual que el almacenamiento Premium compatible con máquinas virtuales de Azure que creará en la fase final de Hola. Podría copiar tooa nueva cuenta de almacenamiento u Hola de toouse plan misma cuenta de almacenamiento según sus necesidades.
* Copie y guarde la clave de cuenta de almacenamiento de Hola de cuenta de almacenamiento de destino de hello para la fase siguiente de Hola.

Se recomienda encarecidamente que mover todos los datos de almacenamiento de información premium toouse de carga de trabajo de producción.

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a>Paso 3: Cargar Hola VHD tooAzure almacenamiento
Ahora que tiene el disco duro virtual en el directorio local de hello, puede utilizar AzCopy o AzurePowerShell tooupload Hola .vhd archivo tooAzure almacenamiento. A continuación se explican ambas opciones:

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a>Opción 1: Usar el archivo .vhd de Azure PowerShell Add-AzureVhd tooupload Hola

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

Un ejemplo <Uri> podría ser ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***. Un ejemplo <FileInfo> podría ser ***"C:\path\to\upload.vhd"***.

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a>Opción 2: Usar el archivo .vhd de AzCopy tooupload Hola
AzCopy puede cargar fácilmente Hola VHD a través de Internet de Hola. Función tamaño Hola de hello discos duros virtuales, esto puede tardar tiempo. Recuerde límites de entrada/salida de la cuenta de almacenamiento de toocheck hello cuando utilice esta opción. Vea [Objetivos de escalabilidad y rendimiento del almacenamiento en Azure](storage-scalability-targets.md) para obtener detalles.

1. Descargue e instale AzCopy desde aquí: [versión más reciente de AzCopy](http://aka.ms/downloadazcopy)
2. Abra PowerShell de Azure y carpeta toohello vaya donde está instalado AzCopy.
3. Archivo de disco duro virtual de hello toocopy de "Origen" de comando siguiente de Hola de uso demasiado "Destino".

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    Ejemplo:

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    Estas son las descripciones de parámetros de hello utilizados en hello AzCopy comando:

   * **El código fuente:  *&lt;origen&gt;:***  ubicación de carpeta de Hola o dirección URL del contenedor de almacenamiento que contiene Hola VHD.
   * **/ SourceKey:  *&lt;clave de la cuenta de origen&gt;:***  clave de cuenta de almacenamiento de la cuenta de almacenamiento de origen de Hola.
   * **/ Dest:  *&lt;destino&gt;:***  toocopy de dirección URL del contenedor de almacenamiento Hola disco duro virtual.
   * **/ DestKey:  *&lt;clave de cuenta dest&gt;:***  clave de cuenta de almacenamiento de la cuenta de almacenamiento de destino de Hola.
   * **/ BlobType: página:** especifica ese destino hello es un blob en páginas.
   * **/ Patrón:  *&lt;nombre de archivo&gt;:***  especificar el nombre de archivo de Hola de hello toocopy de disco duro virtual.

Para obtener más información sobre el uso de AzCopy herramienta, consulte [transferir datos con la utilidad de línea de comandos de AzCopy hello](storage-use-azcopy.md).

##### <a name="other-options-for-uploading-a-vhd"></a>Otras opciones para cargar un disco duro virtual
También puede cargar una cuenta de almacenamiento de disco duro virtual tooyour utilizando uno de hello siguiente significa:

* [API de tipo Copy Blob de Almacenamiento Azure](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [Blobs de carga de Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)
* [Referencia de la API de REST de servicios de importación y exportación de almacenamiento](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> Se recomienda utilizar el servicio Import/Export si se calcula que el tiempo de carga va a ser superior a siete días. Puede usar [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate tiempo de Hola de unidad de tamaño y la transferencia de datos.
>
> Importación/exportación puede ser usar cuenta de almacenamiento estándar tooa toocopy. Necesitará toocopy de cuenta de almacenamiento de almacenamiento estándar toopremium mediante una herramienta como AzCopy.
>
>

## <a name="create-azure-virtual-machine-using-premium-storage"></a>Creación de máquinas virtuales de Azure mediante Premium Storage
Una vez Hola VHD cargado o copiado toohello deseado cuenta de almacenamiento, siga las instrucciones de hello en este Hola de tooregister sección VHD como una imagen del sistema operativo o disco del sistema operativo según el escenario y, a continuación, crear una instancia de la máquina virtual del mismo. disco de datos de Hello VHD puede ser toohello adjunto VM una vez que se crea.
Final de Hola de esta sección se incluye un script de migración de ejemplo. Dicho script no se ajusta a todos los escenarios. Puede que tenga tooupdate Hola script toomatch con su escenario concreto. Consulte más adelante, toosee si esta secuencia de comandos aplica el escenario de tooyour, [un Script de migración de ejemplo](#a-sample-migration-script).

### <a name="checklist"></a>Lista de comprobación
1. Espere a que todos los discos VHD de hello copia está completa.
2. Asegúrese de que el almacenamiento Premium está disponible en la región de Hola que se va a migrar a.
3. Decidir la serie de hello nuevas máquinas virtuales que va a usar. Debe ser un sistema de almacenamiento Premium capaz y Hola debe ser dependiendo de la disponibilidad de hello en la región de Hola y en función de sus necesidades.
4. Decida el tamaño VM exacto de Hola que va a usar. Tamaño de máquina virtual debe toobe número de hello toosupport lo suficientemente grande como de los discos de datos que tiene. Por ejemplo, Si tiene 4 discos de datos, Hola VM debe tener 2 o más núcleos. Considere también las necesidades de potencia de procesamiento, memoria y ancho de banda de red.
5. Crear una cuenta de almacenamiento Premium en la región de destino de Hola. Se trata de cuenta de hello que se empleará para hello nueva máquina virtual.
6. Tener detalles VM actuales de hello útiles, incluidas las listas de Hola de discos y los blobs de disco duro virtual correspondientes.

Prepare la aplicación para el tiempo de inactividad. toodo una migración limpia, que toostop todo el procesamiento de hello en hello actual sistema. Solo entonces puede obtenerlo tooconsistent estado en el que puede migrar toohello nueva plataforma. Duración del tiempo de inactividad dependerá de la cantidad de Hola de datos en hello discos toomigrate.

> [!NOTE]
> Si va a crear una VM de administrador de recursos de Azure desde un disco especializado de disco duro virtual, consulte demasiado[esta plantilla](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) para la implementación de administrador de recursos de VM con disco existente.
>
>

### <a name="register-your-vhd"></a>Registrar el disco duro virtual
toocreate una máquina virtual desde el disco duro virtual del sistema operativo o tooattach un tooa de disco de datos nueva máquina virtual, primero debe registrarse ellos. Siga los pasos especificados a continuación en función del escenario de su VHD.

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a>Generalizado toocreate de sistema operativo VHD varias instancias de máquina virtual de Azure
Después de imagen del sistema operativo generalizado es el disco duro virtual cargado toohello cuenta de almacenamiento, regístrelo como un **imagen de máquina virtual de Azure** para que pueda crear una o varias instancias VM del mismo. Usar un VHD de hello después tooregister de cmdlets de PowerShell como una imagen de sistema operativo de máquina virtual de Azure. Proporcione la dirección URL de contenedor completa de Hola donde se ha copiado el disco duro virtual a.

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

Copie y guarde el nombre de Hola de esta nueva imagen de máquina virtual de Azure. En el ejemplo de Hola anterior, es *NombreImagenSO*.

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a>Único sistema operativo VHD toocreate una sola instancia de máquina virtual de Azure
Después de hello único VHD de SO es almacenamiento toohello cargado account, registrarlo como un **el disco del sistema operativo de Azure** para que pueda crear una instancia de la máquina virtual del mismo. Usar estas tooregister de cmdlets de PowerShell en un VHD como un disco de sistema operativo de Azure. Proporcione la dirección URL de contenedor completa de Hola donde se ha copiado el disco duro virtual a.

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

Copie y guarde el nombre de Hola de este nuevo disco de SO de Azure. En el ejemplo de Hola anterior, es *OSDisk*.

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a>Toobe de disco duro virtual del disco de datos adjunta toonew instancias de máquina virtual de Azure
Después de hello VHD es el disco de datos cargado toostorage cuenta, registrarlo como un disco de datos de Azure para que pueda tooyour adjunto nueva serie DS, DSv2 serie o instancia de máquina virtual de la serie GS Azure.

Use estos tooregister de cmdlets de PowerShell en el disco duro virtual como un disco de datos de Azure. Proporcione la dirección URL de contenedor completa de Hola donde se ha copiado el disco duro virtual a.

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

Copie y guarde el nombre de Hola de este nuevo disco de datos de Azure. En el ejemplo de Hola anterior, es *DataDisk*.

### <a name="create-a-premium-storage-capable-vm"></a>Creación de una máquina virtual compatible con Premium Storage
Una vez Hola imagen del sistema operativo o disco del sistema operativo se registran, cree un nuevo DS-series, DSv2-series o GS-series VM. Va a utilizar imagen de sistema operativo de Hola o nombre de disco de sistema operativo que haya registrado. Seleccione el tipo de máquina virtual de Hola de capa de almacenamiento Premium de Hola. En el ejemplo siguiente, estamos utilizando hello *Standard_DS2* tamaño de máquina virtual.

> [!NOTE]
> Actualizar hello toomake de tamaño de disco que se corresponde con la capacidad y los requisitos de rendimiento y tamaños de disco de Azure disponibles de Hola.
>
>

Cmdlets de PowerShell de seguimiento Hola paso a paso por debajo de toocreate Hola nueva máquina virtual. En primer lugar, establezca los parámetros comunes de hello:

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

En primer lugar, cree un servicio en la nube en el que hospedar las máquinas virtuales nuevas.

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

A continuación, según el escenario, crear instancia de máquina virtual de Azure de Hola de hello imagen del sistema operativo o disco del sistema operativo que haya registrado.

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a>Generalizado toocreate de sistema operativo VHD varias instancias de máquina virtual de Azure
Crear Hola uno o más instancias de máquina virtual de la serie DS Azure nuevo mediante hello **imagen del sistema operativo Azure** que haya registrado. Especifique este nombre de imagen del sistema operativo en configuración de máquina virtual de hello al crear la nueva máquina virtual tal y como se muestra a continuación.

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a>Único sistema operativo VHD toocreate una sola instancia de máquina virtual de Azure
Crear una nueva instancia de máquina virtual de Azure de serie de DS utilizando hello **disco del sistema operativo Azure** que haya registrado. Especifique este nombre de disco del sistema operativo en configuración de máquina virtual de hello al crear Hola nueva máquina virtual tal y como se muestra a continuación.

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

Especifique más datos sobre la máquina virtual de Azure, como un servicio en la nube, la región, la cuenta de almacenamiento, el conjunto de disponibilidad y la directiva de almacenamiento en caché. Observe que la instancia de la máquina virtual de hello debe compartir ubicación con el sistema operativo asociado o discos de datos, por lo que la cuenta de almacenamiento, la región y el servicio de nube Hola seleccionado debe estar en Hola la misma ubicación que Hola subyacente discos duros virtuales de esos discos.

### <a name="attach-data-disk"></a>Acoplar disco de datos
Por último, si se ha registrado datos disco discos duros virtuales, deberá asociarlas toohello nueva VM de Azure con capacidad de almacenamiento Premium.

Usar los siguientes datos disco toohello de PowerShell cmdlet tooattach nueva máquina virtual y especifique Hola directiva de caché. En el ejemplo siguiente Hola directiva de caché se establece demasiado*ReadOnly*.

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> Puede haber pasos adicionales necesarios toosupport la aplicación que no es estarán sujetos a esta guía.
>
>

### <a name="checking-and-plan-backup"></a>Comprobación y planeamiento de la copia de seguridad
Una vez Hola nueva máquina virtual está activo y en ejecución, acceso mediante Hola mismo identificador de inicio de sesión y la contraseña es que la VM original de Hola y comprobar que todo funciona según lo previsto. Todas las configuraciones de hello, incluidos volúmenes de hello particionado, estará presentes en Hola nueva máquina virtual.

Hola último paso es tooplan programación de copia de seguridad y mantenimiento de hello que nueva máquina virtual en función de las necesidades de la aplicación hello.

### <a name="a-sample-migration-script"></a>Un script de migración de ejemplo
Si tiene varios toomigrate de máquinas virtuales, automatización mediante scripts de PowerShell le resultarán útil. Aquí te mostramos una secuencia de comandos de ejemplo que automatiza la migración de Hola de una máquina virtual. Tenga en cuenta que el siguiente script es sólo un ejemplo y no hay algunos supuestos sobre discos de máquina virtual actuales de Hola. Puede que tenga tooupdate Hola script toomatch con su escenario concreto.

suposiciones de Hello son:

* Va a crear máquinas virtuales de Azure clásico.
* Los discos de SO de origen y los discos de datos de origen están en la misma cuenta de almacenamiento y en el mismo contenedor. Si los discos de sistema operativo y los discos de datos no están en Hola mismo colocar, puede utilizar AzCopy o Azure PowerShell toocopy discos duros virtuales a través de las cuentas de almacenamiento y los contenedores. Consulte el paso anterior toohello: [VHD de copia con AzCopy o PowerShell](#copy-vhd-with-azcopy-or-powershell). Editar esta secuencia de comandos toomeet el escenario que es otra opción, pero se recomienda utilizar AzCopy o PowerShell, ya que es más rápido y sencillo.

a continuación se proporciona el script de automatización de Hola. Reemplace el texto por la información y actualizar Hola script toomatch con su escenario concreto.

> [!NOTE]
> Utilizando un script existente hello no conserva la configuración de red de hello del máquina virtual de origen. Se necesita una configuración de red hello toore-config en las máquinas virtuales migradas.
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check hello Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <a name="optimization"></a>Optimización
La configuración actual de la máquina virtual se puede personalizar específicamente toowork bien con los discos estándar. Por ejemplo, tooincrease Hola rendimiento mediante el uso de muchos discos en un volumen seccionado. Por ejemplo, en lugar de utilizar discos de 4 por separado en almacenamiento Premium, es posible que costo de hello toooptimize puede tener un único disco. Las optimizaciones como este toobe necesidad maneja un caso por caso y requieren pasos personalizados después de la migración de Hola. Además, tenga en cuenta que este proceso no puede funcionar bien para bases de datos y las aplicaciones que dependen de diseño del disco Hola definido en el programa de instalación de Hola.

##### <a name="preparation"></a>Preparación
1. Hola completa migración Simple, como se describe en hello en la sección anterior. Las optimizaciones se realizará en hello nueva máquina virtual después de la migración de Hola.
2. Definir nuevos tamaños de disco Hola necesarios para la configuración de hello optimizado.
3. Determinar la asignación de hello actual discos o volúmenes toohello nuevo disco especificaciones.

##### <a name="execution-steps"></a>Pasos de ejecución
1. Crear nuevos discos de hello con los tamaños adecuados de hello en hello VM de almacenamiento Premium.
2. Inicio de sesión toohello VM y copia Hola datos de hello volumen toohello nuevo disco actual que asigna toothat volumen. Haga esto para todos los volúmenes actual Hola que necesitan toomap tooa nuevo disco.
3. A continuación, cambiar discos nuevos de hello aplicación configuración tooswitch toohello y separar los anteriores volúmenes Hola.

Para ajustar la aplicación hello para mejorar el rendimiento de disco, consulte demasiado[optimizar el rendimiento de la aplicación](storage-premium-storage-performance.md#optimizing-application-performance).

### <a name="application-migrations"></a>Migraciones de aplicaciones
Las bases de datos y otras aplicaciones complejas pueden requerir pasos especiales definidos por el proveedor de la aplicación hello para la migración de Hola. Consulte la documentación de la aplicación toorespective. Por ejemplo, las bases de datos normalmente se pueden migrar mediante copia de seguridad y restauración.

## <a name="next-steps"></a>Pasos siguientes
Vea Hola recursos para escenarios específicos para migrar máquinas virtuales siguientes:

* [Migrar máquinas virtuales de Azure entre cuentas de almacenamiento](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [Crear y cargar un VHD de Windows Server tooAzure.](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Crear y cargar un disco duro Virtual que contiene Hola sistema operativo Linux](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Migración de máquinas virtuales de Amazon AWS tooMicrosoft Azure](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

Además, vea Hola después recursos toolearn más información sobre el almacenamiento de Azure y máquinas virtuales de Azure:

* [Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Máquinas virtuales de Azure](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Almacenamiento premium: Almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
