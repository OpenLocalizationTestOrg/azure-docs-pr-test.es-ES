---
title: "almacenamiento de información de rendimiento de aaaHigh Premium y Azure discos administran para máquinas virtuales | Documentos de Microsoft"
description: "Obtenga información sobre Azure Managed Disks y Premium Storage de alto rendimiento para Azure Virtual Machines. Las máquinas virtuales de Azure de la serie DS, DSv2, GS y Fs admiten Premium Storage."
services: storage
documentationcenter: 
author: ramankumarlive
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: ramankum
ms.openlocfilehash: 2474fa75116fe394672fde48520441fa80cf434f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-premium-storage-and-managed-disks-for-vms"></a>Discos administrados y Premium Storage de alto rendimiento para VM
Azure Premium Storage le ofrece soporte de disco de alto rendimiento y latencia baja para máquinas virtuales (VM) con cargas de trabajo intensivas de entrada/salida (E/S). Los discos de VM que usan Premium Storage almacenan los datos en unidades de estado sólido (SSD). tootake ventaja de velocidad de Hola y el rendimiento de discos de almacenamiento premium, puede migrar tooPremium de discos de máquina virtual existente almacenamiento.

En Azure, puede adjuntar varios tooa de discos de almacenamiento premium máquina virtual. Uso de varios discos ofrece las aplicaciones hasta too256 TB de almacenamiento por máquina virtual. Con el almacenamiento Premium, las aplicaciones pueden lograr 80.000 operaciones de E/S por segundo (IOPS) por máquina virtual y un rendimiento de disco de seguridad too2, 000 megabytes por segundo (MB/s) por máquina virtual. Las operaciones de lectura proporcionan latencias muy bajas.

Con el almacenamiento Premium, Azure ofrece la capacidad de hello tootruly elevación y MAYÚS aplicaciones empresariales como nube de toohello de granjas de servidores de Dynamics AX, Dynamics CRM, Exchange Server, SAP Business Suite y SharePoint. Puede ejecutar cargas de trabajo de bases de datos de rendimiento intensivo como SQL Server, Oracle, MongoDB, MySQL y Redis, que requieren una baja latencia y un alto rendimiento de forma coherente.

> [!NOTE]
> Hola recomendados para el rendimiento de la aplicación, se recomienda que migre cualquier disco de máquina virtual que requiere alta IOPS tooPremium almacenamiento. Si el disco no requiere E/S por segundo elevadas, puede limitar los costos conservando Azure Storage estándar. En Standard Storage, los datos de disco de VM se almacenan en unidades de disco duro (HDD) en lugar de en SSD.
> 

Azure ofrece dos formas de discos de almacenamiento de toocreate premium para las máquinas virtuales:

* **Discos no administrados**

    método original de Hello es discos toouse no administrado. En un disco no administrado, administrar cuentas de almacenamiento de Hola que se usan archivos de disco duro virtual (VHD) de hello toostore correspondientes tooyour discos de máquina virtual. Los archivos VHD se almacenan como blobs de páginas en las cuentas de Azure Storage. 

* **Discos administrados**

    Cuando eliges [discos de Azure administrados](storage-managed-disks-overview.md), Azure administra las cuentas de almacenamiento de Hola que usas para los discos de máquina virtual. Especifique el tipo de disco de hello (Premium o estándar) y el tamaño de hello del disco de Hola que necesita. Azure crea y administra el disco de hello en su nombre. No es necesario tooworry acerca de cómo colocar discos hello en varios tooensure de cuentas de almacenamiento que permanezca dentro de los límites de escalabilidad para las cuentas de almacenamiento. Azure se encarga de ello.

Se recomienda que elija discos administrados, tootake aprovechar muchas de sus características.

tooget a trabajar con almacenamiento Premium, [crear su cuenta de Azure gratuita](https://azure.microsoft.com/pricing/free-trial/). 

Para obtener información acerca de cómo migrar su tooPremium de máquinas virtuales de almacenamiento existente, vea [convertir una máquina virtual de Windows de discos de los discos no administrado toomanaged](../virtual-machines/virtual-machines-windows-convert-unmanaged-to-managed-disks.md) o [convertir una VM Linux de discos de los discos no administrado toomanaged](../virtual-machines/linux/convert-unmanaged-to-managed-disks.md).

> [!NOTE]
> Premium Storage está disponible en la mayoría de las regiones. Para obtener lista de regiones disponibles, hello en [servicios de Azure por región](https://azure.microsoft.com/regions/#services), vistazo a las regiones de hello en el que admite máquinas virtuales de la serie de tamaño de la compatibilidad con Premium (DS-series, DSV2-series, GS-series y máquinas virtuales de serie Fs) se admiten.
> 

## <a name="features"></a>Características

Estas son algunas de las características de Hola de almacenamiento Premium:

* **Discos de Premium Storage**

    Premium almacenamiento es compatible con discos de máquina virtual pueden ser adjunta toospecific tamaño-series máquinas virtuales. Premium Storage es compatible con máquinas virtuales de las series DS, DSv2, GS, Ls y Fs. Tiene la opción de siete tamaños de disco: P4 (32 GB), P6 (64 GB), P10 (128 GB), P20 (512 GB), P30 (1024 GB), P40 (2048 GB), P50 (4095 GB). Los tamaños de disco P4 y P6 siguen admitiéndose solo para Managed Disks. Cada tamaño de disco tiene sus propias especificaciones de rendimiento. Dependiendo de los requisitos de la aplicación, puede asociar uno o más discos tooyour máquina virtual. Se describen con más detalle en las especificaciones de hello [destinos de escalabilidad y rendimiento de almacenamiento Premium](#scalability-and-performance-targets).

* **Blobs en páginas Premium**

    Premium Storage admite blobs en páginas. Usar página blobs toostore persistente y no administrado discos para máquinas virtuales en almacenamiento Premium. A diferencia de Azure Storage estándar, Premium Storage no admite blobs en bloques, blobs en anexos, archivos, tablas o colas. Blobs en páginas Premium admite seis tamaños de P10 tooP50 y P60 (8191GiB). Blob en páginas P60 Premium no es compatible toobe conectado como discos de máquina virtual. 

    Cualquier objeto que se coloque en una cuenta de Premium Storage será un blob en páginas. blob en páginas Hola ajusta tooone de hello admite tamaños de aprovisionamiento. Se trata de por qué una cuenta de almacenamiento premium no está pensada toobe utiliza toostore minúsculo blobs.

* **Cuenta de Premium Storage**

    toostart con almacenamiento Premium, cree una cuenta de almacenamiento premium para los discos no administrados. Hola [portal de Azure](https://portal.azure.com), toocreate una cuenta de almacenamiento premium, elija hello **Premium** nivel de rendimiento. Seleccione hello **almacenamiento localmente redundante (LRS)** opción de replicación. También puede crear una cuenta de almacenamiento premium estableciendo tipo hello demasiado**Premium_LRS** en uno de hello ubicaciones siguientes:
    * [API de REST de almacenamiento](https://docs.microsoft.com/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference) (versión 2014-02-14 o una versión posterior)
    * [API de REST de administración de servicios](http://msdn.microsoft.com/library/azure/ee460799.aspx) (versión 2014-10-01 o una versión posterior, para las implementaciones de Azure clásicas)
    * [API de REST del proveedor de recursos de Azure Storage](https://docs.microsoft.com/rest/api/storagerp) (para implementaciones de Azure Resource Manager)
    * [Azure PowerShell](../powershell-install-configure.md) (versión 0.8.10 o una versión posterior)

    toolearn acerca de los límites de cuenta de almacenamiento premium, consulte [destinos de escalabilidad y rendimiento de almacenamiento Premium](#premium-storage-scalability-and-performance-targets).

* **Premium Storage con redundancia local**

    Una cuenta de almacenamiento premium admite almacenamiento con redundancia solo local como opción de replicación de Hola. Almacenamiento con redundancia local mantiene tres copias de datos de hello en una única región. Para la recuperación ante desastres regionales, debe realizar una copia de los discos de máquina virtual en una región distinta con [Azure Backup](../backup/backup-introduction-to-azure-backup.md). También debe usar una cuenta de almacenamiento con redundancia geográfica (GRS) como almacén de copia de seguridad de Hola. 

    Azure usa la cuenta de almacenamiento como contenedor para discos no administrados. Cuando crea una máquina virtual de Azure de las series DS, DSv2, GS o Fs con discos no administrados y selecciona una cuenta de Premium Storage, tanto el disco del sistema operativo como el de datos se almacenan en dicha cuenta de almacenamiento.

## <a name="supported-vms"></a>VM admitidas
Premium Storage es compatible con máquinas virtuales de las series DS, DSv2, GS, Ls y Fs. Con estos tipos de VM puede usar discos de Premium Storage y Standard Storage. No puede utilizar discos de Premium Storage con series de VM que no sean compatibles con Premium Storage.

Para más información sobre los tamaños y tipos de VM en Azure para Windows, vea [Tamaños de VM para Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Para más información sobre los tamaños y tipos de VM en Azure para Linux, vea [Tamaños de VM para Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Estas son algunas de las características de Hola de hello DS-series, DSv2-series, GS-series, Ls-series y máquinas virtuales de serie Fs:

* **Servicio en la nube**

    Puede agregar máquinas virtuales de serie DS tooa servicio en la nube que tienen solo máquinas virtuales de la serie DS. No agregue máquinas virtuales de serie DS tooan servicio en la nube existente que tenga cualquier tipo distinto a las máquinas virtuales de la serie DS. Puede migrar existente discos duros virtuales tooa nuevo servicio en la nube que se ejecuta solo máquinas virtuales de la serie DS. Si desea toouse Hola la misma dirección IP virtual para hello nuevo servicio en la nube que hospeda las máquinas virtuales de la serie DS, use [direcciones IP reservadas](../virtual-network/virtual-networks-instance-level-public-ip.md). Se pueden agregar máquinas virtuales de GS-series tooan servicio en nube existente que tiene solo GS-series las máquinas virtuales.

* **Disco del sistema operativo**

    Puede configurar la máquina virtual de almacenamiento Premium toouse una prima o un disco de sistema operativo estándar. Para la mejor experiencia de hello, se recomienda utilizar un disco de sistema operativo basado en almacenamiento Premium.

* **Discos de datos**

    Puede usar premium y los discos estándar en Hola misma máquina virtual de almacenamiento Premium. Con el almacenamiento Premium, puede aprovisionar una máquina virtual y adjuntar toohello de discos de datos persistentes varias máquinas virtuales. Si es necesario, la capacidad de hello tooincrease y rendimiento del volumen de hello, puede crear bandas en los discos.

    > [!NOTE]
    > Si fragmenta discos de datos de Premium Storage mediante [Espacios de almacenamiento](http://technet.microsoft.com/library/hh831739.aspx), tendrá que configurarlos con una columna por cada disco que use. En caso contrario, general rendimiento del volumen de hello particionado podría ser inferior al esperado debido a una distribución desigual de tráfico en varios discos de Hola. De forma predeterminada, en el administrador del servidor, puede configurar las columnas para los discos de too8. Si tiene más de 8 discos, utilice volúmenes de hello toocreate de PowerShell. Especificar manualmente el número de Hola de columnas. En caso contrario, Hola UI del Administrador de servidor continúa toouse 8 columnas, incluso si tiene varios discos. Por ejemplo, si tiene 32 discos en un conjunto de bandas único, especifique 32 columnas. número de hello toospecify de columnas Hola usos de disco virtual, en hello [New-VirtualDisk](http://technet.microsoft.com/library/hh848643.aspx) cmdlet de PowerShell, use hello *NumberOfColumns* parámetro. Para más información, consulte [Introducción a los espacios de almacenamiento](http://technet.microsoft.com/library/hh831739.aspx) y [Preguntas más frecuentes sobre los espacios de almacenamiento](http://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx).
    >
    > 

* **Memoria caché**

    Máquinas virtuales de serie de tamaño de Hola que admite el almacenamiento Premium tienen una capacidad de almacenamiento en caché exclusiva de altos niveles de rendimiento y la latencia. Hola capacidad de caché supera el rendimiento de disco de almacenamiento premium subyacente. Puede establecer demasiado de la directiva en los discos de almacenamiento premium de caché de disco de hello**ReadOnly**, **ReadWrite**, o **ninguno**. Hola predeterminado disco directiva de caché es **ReadOnly** para todos los discos de datos premium, y **ReadWrite** discos del sistema operativo. Para obtener un rendimiento óptimo para la aplicación, use Hola corregir la configuración de caché. Por ejemplo, en los discos de datos de uso intensivo de lectura o de solo lectura, como archivos de datos de SQL Server, establezca demasiado de la directiva de caché de disco de Hola**ReadOnly**. En los discos de datos de uso intensivo de la escritura o de solo escritura, como archivos de registro de SQL Server, establezca demasiado de la directiva de caché de disco de Hola**ninguno**. toolearn más acerca de cómo optimizar el diseño de almacenamiento Premium, consulte [diseño de rendimiento con el almacenamiento Premium](storage-premium-storage-performance.md).

* **Analytics**

    rendimiento de la máquina virtual de tooanalyze mediante el uso de discos de almacenamiento Premium, activar diagnósticos de máquina virtual en hello [portal de Azure](https://portal.azure.com). Para más información, consulte [Supervisión de una máquina virtual de Azure con Extensión de Diagnósticos de Azure](https://azure.microsoft.com/blog/2014/09/02/windows-azure-virtual-machine-monitoring-with-wad-extension/). 

    rendimiento de disco toosee, herramientas basada en el sistema operativo como [Monitor de rendimiento de Windows](https://technet.microsoft.com/library/cc749249.aspx) para hello y máquinas virtuales de Windows [iostat](http://linux.die.net/man/1/iostat) comando para máquinas virtuales de Linux.

* **Rendimiento y límites de escala de VM**

    Cada tamaño VM admite almacenamiento Premium tiene límites de escala y especificaciones de rendimiento de e/s por segundo, ancho de banda y número de Hola de discos que se pueden adjuntar por máquina virtual. Al usar discos de almacenamiento premium con máquinas virtuales, asegúrese de que hay suficientes IOPS y ancho de banda en el tráfico de disco de máquina virtual toodrive.

    Por ejemplo, una VM STANDARD_DS1 tiene un ancho de banda dedicado de 32 MB/s para el tráfico de disco de Premium Storage. Un disco de Premium Storage P10 puede proporcionar un ancho de banda de 100 MB/s. Si un disco de almacenamiento premium P10 está adjunto toothis VM, sólo puede subir too32 MB/s. No puede utilizar Hola que puede proporcionar el máximo 100 MB/s disco P10 Hola.

    Actualmente, hello máquina virtual más grande en hello DS-series es hello Standard_DS15_v2. Hola Standard_DS15_v2 puede proporcionar seguridad too960 MB/s a través de todos los discos. Hello máquina virtual más grande en hello GS-series es hello Standard_GS5. Hola Standard_GS5 puede proporcionar seguridad too2, 000 MB/s a través de todos los discos.

    Tenga en cuenta que estos límites son solo para el tráfico de disco. Estos límites no incluyen los aciertos de la caché y el tráfico de red. Hay disponible un ancho de banda independiente para el tráfico de red de VM. Ancho de banda para el tráfico de red es diferente de ancho de banda de hello dedicado utilizado por los discos de almacenamiento premium.

    Para hello información más actualizada acerca de máximo de IOPS y rendimiento (ancho de banda) para máquinas virtuales admiten almacenamiento Premium, consulte [tamaños de máquina virtual de Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [tamaños de VM de Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

    Para obtener más información acerca de los discos de almacenamiento premium y sus límites IOPS y el rendimiento, vea la tabla de hello en la sección siguiente Hola.

## <a name="scalability-and-performance-targets"></a>Objetivos de escalabilidad y rendimiento
En esta sección, describimos tooconsider de destinos de escalabilidad y rendimiento de hello cuando se usa almacenamiento Premium.

Cuentas de almacenamiento Premium tienen Hola siguientes destinos de escalabilidad:

| Capacidad total de la cuenta | Ancho de banda total de una cuenta de almacenamiento con redundancia local |
| --- | --- | 
| Capacidad de disco: 35 TB <br>Capacidad de instantánea: 10 TB | Seguridad too50 gigabits por segundo de entrada<sup>1</sup> + saliente<sup>2</sup> |

<sup>1</sup> todos los datos (solicitudes) que se envían tooa cuenta de almacenamiento

<sup>1</sup> Todos los datos (respuestas) que se reciben desde una cuenta de almacenamiento

Para más información, consulte [Objetivos de escalabilidad y rendimiento de Azure Storage](storage-scalability-targets.md).

Si usas cuentas de almacenamiento premium para los discos no administrados y la aplicación supera los objetivos de escalabilidad de Hola de una única cuenta de almacenamiento, conviene toomigrate toomanaged discos. Si no desea toomigrate toomanaged discos, compile la aplicación toouse varias cuentas de almacenamiento. A continuación, divida los datos en esas cuentas de almacenamiento. Por ejemplo, si desea que los discos de 51 TB tooattach entre varias máquinas virtuales, distribuirlos entre dos cuentas de almacenamiento. 35 TB es el límite de Hola para una cuenta de almacenamiento premium solo. Asegúrese de que una sola cuenta de Premium Storage nunca tenga más de 35 TB de discos aprovisionados.

### <a name="premium-storage-disk-limits"></a>Límites de discos de Premium Storage
Cuando se determina de aprovisionar un disco de almacenamiento premium, tamaño de hello del disco de Hola Hola máximo IOPS y el rendimiento (ancho de banda). Azure ofrece siete tipos de discos de Premium Storage: P4 (solo Managed Disks), P6 (solo Managed Disks), P10, P20, P30, P40 y P50. Cada tipo de disco de Premium Storage tiene límites específicos de E/S por segundo y rendimiento. En hello en la tabla siguiente se describen los límites de los tipos de disco de hello:

| Tipo de discos Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Tamaño del disco           | 32 GB| 64 GB| 128 GB| 512 GB            | 1.024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOPS por disco       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Rendimiento de disco | 25 MB por segundo  | 50 MB por segundo  | 100 MB por segundo | 150 MB por segundo | 200 MB por segundo | 250 MB por segundo | 250 MB por segundo | 

> [!NOTE]
> Asegúrese de que el ancho de banda suficiente está disponible en el tráfico de disco de máquina virtual toodrive, como se describe en [admitidos por el almacenamiento Premium, las máquinas virtuales](#premium-storage-supported-vms). En caso contrario, el rendimiento del disco y e/s por segundo es tener valores toolower restringida. Rendimiento máximo y las IOPS se basan en los límites VM de hello, no en límites de disco Hola descritos en la tabla anterior de Hola.  
> 
> 

Estos son algunos tooknow aspectos importantes sobre los destinos de escalabilidad y rendimiento de almacenamiento Premium:

* **Rendimiento y capacidad aprovisionados**

    Cuando se aprovisiona un disco de almacenamiento premium, a diferencia de almacenamiento estándar, se garantiza que capacidad hello, IOPS y el rendimiento de dicho disco. Por ejemplo, si crea un disco P50, Azure aprovisiona una capacidad de almacenamiento de 4095 GB, 7500 E/S por segundo y un rendimiento de 250 MB/s para él. La aplicación puede usar todo o parte de la capacidad de Hola y rendimiento.

* **Tamaño del disco**

    Mapas de Azure Hola toohello (redondeado al alza) de tamaño de disco más cercano de la opción de disco de almacenamiento premium, como se especifica en la tabla de Hola Hola sección anterior. Por ejemplo, un tamaño de disco de 100 GB se clasifica como una opción P10. Puede realizar too500 IOPS, con seguridad de rendimiento de MB/s too100. De forma similar, un disco con un tamaño de 400 GB se clasifica como P20. Puede realizar una too2, 300 e/s por segundo, con un rendimiento de 150 MB/s.
    
    > [!NOTE]
    > Puede aumentar fácilmente el tamaño de Hola de discos existentes. Por ejemplo, podría desea que tooincrease Hola tamaño de un disco de 30 GB too128 GB o incluso too1 TB. O bien, podría tooconvert el disco de tooa P30 P20 disco porque se necesita más capacidad o más IOPS y rendimiento. 
    > 
 
* **Tamaño de E/S**

    tamaño de Hola de una E/S es de 256 KB. Si se transfieren datos de hello están inferior a 256 KB, se considera 1 unidad de E/S. Los tamaños de E/S más grandes se cuentan como varias operaciones de E/S con un tamaño de 256 KB. Por ejemplo, una E/S de 1,100 KB se cuenta como cinco unidades de E/S.

* **Rendimiento**

    límite de rendimiento de Hello incluye escrituras toohello disco e incluye las operaciones de lectura de disco que no están disponibles desde caché de Hola. Por ejemplo, un disco P10 tiene un rendimiento de 100 MB/s por disco. Se muestran algunos ejemplos de rendimiento válido para un disco P10 en hello en la tabla siguiente:

    | Rendimiento máximo por disco P10 | Lecturas no en la memoria caché desde el disco | No estaba en caché escribe toodisk |
    | --- | --- | --- |
    | 100 MB/s | 100 MB/s | 0 |
    | 100 MB/s | 0 | 100 MB/s |
    | 100 MB/s | 60 MB/s | 40 MB/s |

* **Aciertos de caché**

    Aciertos de caché no están limitados por hello asignada IOPS o rendimiento de disco de Hola. Por ejemplo, cuando usa un disco de datos con un **ReadOnly** configuración de caché en una máquina virtual que es compatible con almacenamiento Premium, lecturas que se atienden desde la memoria caché de hello no es toohello asunto IOPS y límites de rendimiento de disco de Hola. Si la carga de trabajo de Hola de un disco es fundamentalmente lee, es posible que obtenga un rendimiento muy alto. caché de Hello es asunto tooseparate IOPS y límites de rendimiento en hello nivel de máquina virtual, en función de hello tamaño de máquina virtual. Las VM de la serie DS tienen aproximadamente 4000 E/S por segundo y un rendimiento de 33 MB/s por núcleo de caché y E/S de SSD locales. Las VM de la serie DS tienen aproximadamente un límite de 5000 E/S por segundo y un rendimiento de 50 MB/s por núcleo de caché y E/S de SSD locales. 

## <a name="throttling"></a>Limitaciones
La limitación puede ocurrir si la aplicación IOPS o rendimiento supera el límite de hello asignado de un disco de almacenamiento premium. Limitación también se podría producir si el tráfico total en disco en todos los discos en hello VM supera el límite de ancho de banda de hello disco disponible para hello VM. la limitación tooavoid, se recomienda que limite el número Hola de pendiente de las solicitudes de E/S de disco de Hola. Utilice un límite basado en objetivos de escalabilidad y rendimiento de disco de hello que ha aprovisionado y en hello disco ancho de banda disponible toohello máquina virtual.  

La aplicación puede lograr la latencia más baja de hello cuando está diseñado tooavoid limitación. Sin embargo, si hello número de pendientes las solicitudes de E/S de disco de hello es demasiado pequeño, la aplicación no puede sacar provecho de hello niveles máximos de IOPS y el rendimiento que están disponibles toohello disco.

Hello en los ejemplos siguientes muestra cómo los niveles de limitación de toocalculate. Todos los cálculos se basan en un tamaño de unidad de E/S de 256 KB.

### <a name="example-1"></a>Ejemplo 1
La aplicación procesó 495 unidades de E/S de 16 KB de tamaño en un segundo en un disco P10. unidades de E/S de Hola se cuentan como 495 e/s por segundo. Si trata de una E/S de 2 MB en Hola igual en segundo lugar, total de Hola de unidades de E/S es igual too495 + 8 e/s por segundo. Esto es porque E/S de 2 MB = unidades de 2.048 KB / 256 KB = 8 i/OS, al tamaño de la unidad de E/S de hello es de 256 KB. Porque suma Hola de 495 + 8 supera el límite de IOPS 500 hello para el disco de hello, se produce una limitación.

### <a name="example-2"></a>Ejemplo 2
La aplicación procesó 400 unidades de E/S de 256 KB de tamaño en un disco P10. Hola ancho de banda total utilizado es (400 &#215; 256) / 1.024 KB = 100 MB/s. El rendimiento de un disco P10 es de 100 MB/s. Si la aplicación intenta tooperform más operaciones de E/S en ese segundo, está limitado porque supera el límite de hello asignada.

### <a name="example-3"></a>Ejemplo 3
Tiene una máquina virtual DS4 con dos discos P30 conectados. Cada disco P30 es capaz de tener un rendimiento de 200 MB/s. Sin embargo, una VM DS4 tiene una capacidad de ancho de banda de disco total de 256 MB/s. No puede controlar el rendimiento máximo de ambos toohello de discos conectados en esta máquina virtual de DS4 en hello mismo tiempo. tooresolve esto, puede admitir el tráfico de 200 MB/s en un disco y 56 MB/s en Hola otro disco. Si suma Hola del tráfico disco supera 256 MB/s, está limitado el tráfico del disco.

> [!NOTE]
> Si el tráfico de disco principalmente consta de los tamaños de E/S pequeños, la aplicación probablemente alcanzarán límite de IOPS de hello antes de límite de rendimiento de Hola. Sin embargo, si el tráfico de disco Hola principalmente consta de los tamaños de E/S grandes, la aplicación probablemente alcanzarán límite de rendimiento de hello en primer lugar, en lugar de límite de IOPS de Hola. Puede maximizar la E/S por segundo y el rendimiento de su aplicación mediante el uso de tamaños de E/S óptimos. Además, puede limitar número de Hola de solicitudes de E/S para un disco pendientes.
> 

toolearn más sobre el diseño de alto rendimiento mediante el uso de almacenamiento Premium, consulte [diseño de rendimiento con el almacenamiento Premium](storage-premium-storage-performance.md).

## <a name="snapshots-and-copy-blob"></a>Instantáneas y Copy Blob

servicio de almacenamiento de archivo de disco duro virtual de hello toohello es un blob en páginas. Puede tomar instantáneas de blobs de página y cópielos tooanother ubicación, como la cuenta de almacenamiento distinta de tooa.

### <a name="unmanaged-disks"></a>Discos no administrados

Crear [instantáneas incrementales](storage-incremental-snapshots.md) para discos premium no administrado Hola mismo forma de usar instantáneas con almacenamiento estándar. Almacenamiento Premium admite almacenamiento con redundancia solo local como opción de replicación de Hola. Se recomienda que crear instantáneas y, a continuación, copie la cuenta de almacenamiento estándar con redundancia geográfica de hello instantáneas tooa. Para obtener más información, vea [Opciones de redundancia de Azure Storage](storage-redundancy.md).

Si un disco está conectado tooa VM, no se permiten algunas operaciones de API en el disco de Hola. Por ejemplo, no se puede realizar un [Copy Blob](/rest/api/storageservices/Copy-Blob) operación en ese blob si Hola disco está vinculada tooa máquina virtual. En su lugar, cree primero una instantánea del blob utilizando hello [Blob de instantánea](/rest/api/storageservices/Snapshot-Blob) API de REST. A continuación, realizar hello [Copy Blob](/rest/api/storageservices/Copy-Blob) de Hola Hola de toocopy de instantánea se adjuntó el disco. Como alternativa, puede desconectar el disco de hello y, a continuación, realizar las operaciones necesarias.

Hola siguiendo los límites aplica instantáneas de blob de almacenamiento de toopremium:

| Límite de Premium Storage | Valor |
| --- | --- |
| Número máximo de instantáneas por blob | 100 |
| Capacidad de la cuenta de almacenamiento de instantáneas<br>(Incluye solo datos en las instantáneas. No incluye datos en blob base). | 10 TB |
| Tiempo mínimo entre instantáneas consecutivas | 10 minutos |

toomaintain copias con redundancia geográfica de las instantáneas, puede copiar las instantáneas de una cuenta de almacenamiento estándar con redundancia geográfica premium tooa de cuenta de almacenamiento mediante AzCopy o copia de Blob. Para obtener más información, consulte [transferir datos a la utilidad de línea de comandos de AzCopy de hello](storage-use-azcopy.md) y [Copy Blob](/rest/api/storageservices/Copy-Blob).

Para más información acerca de cómo realizar operaciones de REST en blobs en páginas en cuentas de Premium Storage, consulte [Uso de operaciones de Blob service con Azure Premium Storage](http://go.microsoft.com/fwlink/?LinkId=521969).

### <a name="managed-disks"></a>Discos administrados

Una instantánea de un disco administrado es una copia de solo lectura de disco administrado Hola. Hola instantánea se almacena como un disco administrado estándar. Actualmente, las [instantáneas incrementales](storage-incremental-snapshots.md) no son compatibles con discos administrados. toolearn tootake una instantánea de un disco administrado, vea [crear una copia de un VHD almacenado como un Azure administrado disco mediante el uso de instantáneas administradas en Windows](../virtual-machines/virtual-machines-windows-snapshot-copy-managed-disk.md) o [crear una copia de un VHD almacenado como un Azure administrado disco utilizando administrados las instantáneas en Linux](../virtual-machines/linux/snapshot-copy-managed-disk.md).

Si un disco administrado está conectado tooa VM, no se permiten algunas operaciones de API en el disco de Hola. Por ejemplo, no se puede generar un tooperform de firma (SAS) de acceso compartido a una operación de copia mientras disco Hola está adjunto tooa máquina virtual. En su lugar, cree primero una instantánea del disco de hello y, a continuación, realizar copia de Hola de instantánea de Hola. Como alternativa, puede desconectar el disco de hello y, a continuación, generar una operación de copia SAS tooperform Hola.


## <a name="premium-storage-for-linux-vms"></a>Premium Storage para VM Linux
Puede usar Hola después de configurar las máquinas virtuales de Linux en el almacenamiento Premium de toohelp de información:

está dirigida a tooachieve escalabilidad de almacenamiento Premium, para todos los discos de almacenamiento premium con caché conjunto demasiado**ReadOnly** o **ninguno**, debe deshabilitar "barreras" al montar el sistema de archivos de Hola. Las barreras que existen en este escenario no es necesario porque Hola escribe discos de almacenamiento de toopremium sean duraderos para esta configuración de caché. Cuando se finalice correctamente la solicitud de escritura de hello, datos se han escrito toohello un almacén persistente. toodisable "barreras", utilice uno de los siguientes métodos de Hola. Elija hello para el sistema de archivos:
  
* Para **reiserFS**, toodisable barreras, usar hello `barrier=none` opción de montaje. (las barreras tooenable, utilice `barrier=flush`.)
* Para **ext3/ext4**, toodisable barreras, usar hello `barrier=0` opción de montaje. (las barreras tooenable, utilice `barrier=1`.)
* Para **XFS**, toodisable barreras, usar hello `nobarrier` opción de montaje. (las barreras tooenable, utilice `barrier`.)
* Para los discos de almacenamiento premium con memoria caché establecida demasiado**ReadWrite**, habilitar las barreras para que la durabilidad de escritura.
* Toopersist de las etiquetas de volumen después de reiniciar Hola de máquina virtual, debe actualizar/etc/fstab con referencias toohello discos de hello identificador único universal (UUID). Para obtener más información, consulte [agregar una VM de Linux de disco administrado tooa](../virtual-machines/linux/add-disk.md).

Hola siguiendo las distribuciones de Linux se ha validado para el almacenamiento de Azure Premium. Para obtener un mejor rendimiento y estabilidad con almacenamiento Premium, se recomienda que actualice su tooone de máquinas virtuales de estas versiones, como mínimo (o tooa una versión posterior). Servicios de integración para última Linux (LIS), v4.0, algunos de hello requieren versiones Hola de Azure. toodownload e instalar una distribución, siga el vínculo del Hola enumerado en hello en la tabla siguiente. Agregamos la lista de imágenes toohello cuando se complete la validación. Tenga en cuenta que nuestras validaciones muestran que el rendimiento en cada imagen. El rendimiento depende en las características de carga de trabajo y la configuración de la imagen. Se ajustan diferentes imágenes a los distintos tipos de cargas de trabajo.

| Distribución | Versión | Kernel compatible | Detalles |
| --- | --- | --- | --- |
| Ubuntu | 12.04 | 3.2.0-75.110+ | Ubuntu-12_04_5-LTS-amd64-server-20150119-en-us-30GB |
| Ubuntu | 14.04 | 3.13.0-44.73+ | Ubuntu-14_04_1-LTS-amd64-server-20150123-en-us-30GB |
| Debian | 7.x, 8.x | 3.16.7-ckt4-1+ | &nbsp; |
| SUSE | SLES 12| 3.12.36-38.1+| suse-sles-12-priority-v20150213 <br> suse-sles-12-v20150213 |
| SUSE | SLES 11 SP4 | 3.0.101-0.63.1+ | &nbsp; |
| CoreOS | 584.0.0+| 3.18.4+ | CoreOS 584.0.0 |
| CentOS | 6.5, 6.6, 6.7, 7.0 | &nbsp; | [LIS4 requerido](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *Vea la nota en la sección siguiente Hola* |
| CentOS | 7.1+ | 3.10.0-229.1.2.el7+ | [LIS4 recomendado](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *Vea la nota en la sección siguiente Hola* |
| Red Hat Enterprise Linux (RHEL) | 6.8+, 7.2+ | &nbsp; | &nbsp; |
| Oracle | 6.0+ y 7.2+ | &nbsp; | UEK4 o RHCK |
| Oracle | 7.0-7.1 | &nbsp; | UEK4 o RHCK con[LIS 4.1+](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |
| Oracle | 6.4-6.7 | &nbsp; | UEK4 o RHCK con[LIS 4.1+](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |


### <a name="lis-drivers-for-openlogic-centos"></a>Controladores de LIS para CentOS Openlogic

Si se ejecutan las máquinas virtuales de OpenLogic CentOS, ejecute hello siguiendo los controladores más recientes de comando tooinstall hello:

```
sudo rpm -e hypervkvpd  ## (Might return an error if not installed. That's OK.)
sudo yum install microsoft-hyper-v
```

Hola tooactivate nuevos controladores, reiniciar equipo Hola.

## <a name="pricing-and-billing"></a>Precios y facturación

Al usar almacenamiento Premium, se aplica Hola después de facturación consideraciones:

* **Tamaño de disco y blob de Premium Storage**

    La facturación de un disco de almacenamiento premium o blob depende de tamaño de hello aprovisionado de disco de Hola o blob. Mapas de Azure Hola toohello tamaño aprovisionado (redondeado al alza) más cercano de la opción de disco de almacenamiento premium. Para obtener más información, vea la tabla hello en [destinos de escalabilidad y rendimiento de almacenamiento Premium](#premium-storage-scalability-and-performance-targets). Cada tooa de asignaciones de disco admitida aprovisionado el tamaño del disco y se factura según corresponda. La facturación de cualquier disco aprovisionado se prorratea cada hora mediante el uso de precio mensual de hello para la oferta de almacenamiento Premium de Hola. Por ejemplo, si se aprovisiona un disco P10 y eliminar después de 20 horas, se le facturará para hello P10 horas prorrateados too20 la oferta. Esto es así independientemente de la cantidad de Hola de datos que se escriben toohello disco u Hola IOPS y el rendimiento que se utiliza.

* **Instantáneas de Unmanaged Disks premium**

    Instantáneas de discos premium no administrado se facturan por capacidad adicional de hello utilizada por las instantáneas de Hola. Para más información sobre las instantáneas, consulte [Creación de una instantánea de un blob](/rest/api/storageservices/Snapshot-Blob).

* **Instantáneas de Managed Disks premium**

    Una instantánea de un disco administrado es una copia de solo lectura de disco de Hola. disco de Hola se almacena como un disco administrado estándar. Los costos de una instantánea Hola mismo como un estándar administrado disco. Por ejemplo, si toma una instantánea de un disco administrado premium de 128 GB, costo de Hola de instantánea de hello es disco administrado estándar tooa equivalente de 128 GB.  

* **Transferencias de datos de salida**

    [Transferencias de datos de salida](https://azure.microsoft.com/pricing/details/data-transfers/) (datos que salen de los centros de datos de Azure) incurren en la facturación por el uso de ancho de banda.

Para información detallada sobre los precios de Premium Storage, de las máquinas virtuales compatibles con Premium Storage y de Managed Disks, consulte los estos artículos:

* [Precios de Azure Storage](https://azure.microsoft.com/pricing/details/storage/)
* [Precios de máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Precios de Managed Disks](https://azure.microsoft.com/pricing/details/managed-disks/)

## <a name="azure-backup-support"></a>Soporte técnico de Azure Backup 

Para recuperación ante desastres regionales, debe realizar una copia de los discos de máquina virtual en una región distinta con [Azure Backup](../backup/backup-introduction-to-azure-backup.md) y una cuenta de almacenamiento GRS como almacén de Backup.

toocreate un trabajo de copia de seguridad con copias de seguridad basadas en el tiempo y facilitar la restauración de máquinas virtuales, las directivas de retención de copia de seguridad, utilice copia de seguridad de Azure. Puede utilizar Backup con discos administrados y no administrados. Para más información, vea [Azure Backup para VM con Unmanaged Disks ](../backup/backup-azure-vms-first-look-arm.md) y [Azure Backup para VM con Managed Disks](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup). 

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre el almacenamiento Premium, vea Hola siguientes artículos.

### <a name="design-and-implement-with-premium-storage"></a>Diseño e implementación con Premium Storage
* [Diseño para rendimiento con Premium Storage](storage-premium-storage-performance.md)
* [Operaciones de almacenamiento de blobs con Premium Storage](http://go.microsoft.com/fwlink/?LinkId=521969)

### <a name="operational-guidance"></a>Guía de operaciones
* [Migrar tooAzure almacenamiento Premium](storage-migration-to-premium-storage.md)

### <a name="blog-posts"></a>Publicaciones de blog
* [Disponibilidad general de Azure Premium Storage](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/)
* [Anuncio de Hola GS-series: agregar toohello de soporte técnico de almacenamiento Premium mayor Hola máquinas virtuales en nube pública](https://azure.microsoft.com/blog/azure-has-the-most-powerful-vms-in-the-public-cloud/)
