---
title: aaaSAP HANA la copia de seguridad de Azure en el nivel de archivo | Documentos de Microsoft
description: "Existen dos posibilidades de copia de seguridad principales para SAP HANA en Azure Virtual Machines. Este artículo trata sobre Azure Backup de SAP HANA en el nivel de archivo"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: d5a55de5634ac7724e7fd0fa3760c6c408c3db74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-azure-backup-on-file-level"></a>Azure Backup de SAP HANA en el nivel de archivo

## <a name="introduction"></a>Introducción

Esto forma parte de una serie de tres partes de artículos relacionados sobre copia de seguridad de SAP HANA. [Guía de backup para SAP HANA en máquinas virtuales Azure](./sap-hana-backup-guide.md) proporciona una introducción e información sobre los pasos iniciales, y [copia de seguridad de SAP HANA basándose en instantáneas de almacenamiento](./sap-hana-backup-storage-snapshots.md) portadas Hola opción de copia de seguridad basados en instantáneas de almacenamiento.

Examinando los tamaños de máquina virtual de Azure de hello, uno puede ver que una GS5 permite 64 discos de datos adjuntos. Para los sistemas de SAP HANA de gran tamaño, puede haberse tomado ya un número significativo de discos para archivos de registro y datos, posiblemente junto con el RAID del software para ofrecer un rendimiento óptimo de E/S del disco. ¿a continuación, la pregunta de Hello es donde toostore SAP HANA copia de seguridad de archivos, que podrían llenarse datos Hola adjunta discos con el tiempo? Vea [tamaños de máquinas virtuales de Linux en Azure](../../linux/sizes.md) para las tablas de tamaño de máquina virtual de Azure Hola.

En este momento no hay ninguna integración de copia de seguridad de SAP HANA disponible con el servicio Azure Backup. manera estándar de Hello toomanage copia de seguridad/restauración en el nivel de archivo hello es con una copia de seguridad basada en archivos a través de SAP HANA Studio o instrucciones SQL de SAP HANA. Vea [SAP HANA SQL y referencia de vistas del sistema](https://help.sap.com/hana/SAP_HANA_SQL_and_System_Views_Reference_en.pdf) para obtener más información.

![Esta ilustración muestra el cuadro de diálogo de Hola Hola copia de seguridad del elemento de menú en SAP HANA Studio](media/sap-hana-backup-file-level/image022.png)

Esta ilustración muestra el cuadro de diálogo de Hola Hola copia de seguridad del elemento de menú en SAP HANA Studio. Al elegir el tipo &quot;archivo&quot; uno tiene toospecify una ruta de acceso del sistema de archivos de Hola donde SAP HANA escribe archivos de copia de seguridad de Hola. Restauración funciona Hola igual.

Aunque esta opción suena simple y sencilla, existen algunas consideraciones. Como se mencionó antes, una máquina virtual de Azure tiene una limitación del número de discos de datos que se pueden asociar. No puede haber archivos de copia de seguridad de SAP HANA de toostore y capacidad en sistemas de archivos de Hola Hola de máquina virtual, según el tamaño de Hola de hello base de datos y disco requisitos de rendimiento, que podría causar el software RAID mediante la creación de bandas a través de los datos de varios discos. Se proporcionan más opciones para mover estos archivos de copia de seguridad y administrar las restricciones de tamaño de archivo y el rendimiento cuando se administran terabytes de datos más adelante en este artículo.

Otra opción, que ofrece más libertad con respecto a la capacidad total, es Azure Blob Storage. Mientras un único blob también está restringido too1 TB, la capacidad total de Hola de un único contenedor blobs está actualmente 500 TB. Además, ofrece a los clientes Hola choice tooselect denominada &quot;frío&quot; almacenamiento de blobs, que tiene una ventaja de costo. Vea [Azure Blob Storage: capas de almacenamiento de acceso frecuente y esporádico](../../../storage/blobs/storage-blob-storage-tiers.md) para obtener más información sobre el almacenamiento de blobs en frío.

Por motivos de seguridad adicional, utilice un almacenamiento de replicación geográfica cuenta toostore Hola SAP HANA las copias de seguridad. Vea [Replicación de Azure Storage](../../../storage/common/storage-redundancy.md) para obtener más información sobre la replicación de la cuenta de almacenamiento.

Puede colocar VHD dedicados para copias de seguridad de SAP HANA en una cuenta de almacenamiento de copia de seguridad dedicada con replicación geográfica. O bien uno podría copiar discos duros virtuales de Hola que mantienen copias de seguridad de SAP HANA Hola cuenta de almacenamiento georreplicadas tooa o tooa cuenta de almacenamiento que se encuentra en una región diferente.

## <a name="azure-backup-agent"></a>Azure Backup Agent

Ofertas de copia de seguridad de Azure Hola opción toonot solo realizar una copia completa de máquinas virtuales, pero también archivos y directorios a través de agente de copia de seguridad de hello, que tiene instalado en el sistema operativo invitado de Hola de toobe. Pero a partir de 2016 de diciembre, este agente sólo se admite en Windows (vea [copia de seguridad una tooAzure de Windows Server o cliente utilizando el modelo de implementación del Administrador de recursos de hello](../../../backup/backup-configure-vault.md)).

Una solución alternativa es copia de toofirst tooa de archivos de copia de seguridad de SAP HANA VM de Windows en Azure (por ejemplo, a través de recursos compartidos SAMBA) y, a continuación, usar hello agente de copia de seguridad de Azure desde allí. Aunque es técnicamente posible, podría agregar complejidad y ralentizar la copia de seguridad de Hola o proceso un poco debido toohello copia entre hello VM de Windows y Linux de Hola de restauración. No es recomendable toofollow este enfoque.

## <a name="azure-blobxfer-utility-details"></a>Detalles de la utilidad bloxfer de Azure

toostore directorios y archivos en almacenamiento de Azure, podría usar una CLI o PowerShell, o desarrolle una herramienta mediante uno de hello [Azure SDK](https://azure.microsoft.com/downloads/). También hay una utilidad listos para usar, AzCopy, para la copia de almacenamiento de datos tooAzure, pero se trata solo de Windows (consulte [transferir datos con hello utilidad de línea de comandos de AzCopy](../../../storage/common/storage-use-azcopy.md)).

Por lo tanto, se usó blobxfer para copiar los archivos de copia de seguridad de SAP HANA. Se trata de código abierto, que usan muchos clientes en entornos de producción, y que está disponible en [GitHub](https://github.com/Azure/blobxfer). Esta herramienta permite que los datos de una toocopy directamente tooeither Azure blob storage o recurso compartido de archivos de Azure. También ofrece una gama de características útiles, como hash md5 o paralelismo automático al copiar un directorio con varios archivos.

## <a name="sap-hana-backup-performance"></a>Rendimiento de copia de seguridad de SAP HANA

![Esta captura de pantalla es de la consola de copia de seguridad de SAP HANA hello en SAP HANA Studio](media/sap-hana-backup-file-level/image023.png)

Esta captura de pantalla es de la consola de copia de seguridad de SAP HANA hello en SAP HANA Studio. Copia de seguridad de aproximadamente 42 minutos toodo Hola. se tardó de hello 230 GB en un disco de almacenamiento de Azure único estándar adjunta toohello HANA VM mediante el sistema de archivos XFS.

![Esta captura de pantalla es de YaST en la máquina virtual de la prueba de SAP HANA Hola](media/sap-hana-backup-file-level/image024.png)

Esta captura de pantalla es de YaST en la máquina virtual de la prueba de SAP HANA Hola. Como se mencionó antes, se puede ver solo disco de 1 TB de Hola para copia de seguridad de SAP HANA. Se tardó aproximadamente 42 minutos toobackup 230 GB. Además, se asocian cinco discos de 200 GB y software RAID md0 creado, con la fragmentación en la parte superior de estaos cinco discos de datos de Azure.

![Repetir Hola igual de copia de seguridad en RAID de software con creación de bandas en cinco discos de datos de almacenamiento estándar Azure conectados](media/sap-hana-backup-file-level/image025.png)

Hola repetición igual de copia de seguridad en RAID de software con creación de bandas en cinco conectado hora de copia de seguridad de Azure almacenamiento estándar datos discos poner Hola de 42 minutos hacia abajo too10 minutos. se han adjuntado discos Hola sin almacenamiento en caché toohello máquina virtual. Por lo que resulta evidente la importancia rendimiento de escritura en disco es para tiempo de copia de seguridad de Hola. Uno podría conmutador tooAzure premium almacenamiento toofurther acelerar el proceso de Hola para un rendimiento óptimo. En general, debe usarse Azure Premium Storage para los sistemas de producción.

## <a name="copy-sap-hana-backup-files-tooazure-blob-storage"></a>Copie el almacenamiento de blobs de tooAzure de archivos de copia de seguridad de SAP HANA

Como de 2016 de diciembre, Hola mejor opción tooquickly almacén SAP HANA copias de seguridad es el almacenamiento de blobs de Azure. Un contenedor de blob único tiene un límite de 500 TB, suficiente para la mayoría de los sistemas de SAP HANA, ejecute en una máquina virtual GS5 en Azure, tookeep suficientes SAP HANA las copias de seguridad. Los clientes tienen la opción de hello entre &quot;activa&quot; y &quot;frío&quot; almacenamiento de blobs (vea [almacenamiento de blobs de Azure: caliente y estupendo capas de almacenamiento](../../../storage/blobs/storage-blob-storage-tiers.md)).

Con la herramienta de blobxfer Hola, son archivos de copia de seguridad de fácil toocopy Hola SAP HANA directamente tooAzure almacenamiento de blobs.

![Aquí se pueden ver archivos de Hola de una copia de seguridad completa del archivo de SAP HANA](media/sap-hana-backup-file-level/image026.png)

Aquí se pueden ver archivos de Hola de una copia de seguridad completa del archivo de SAP HANA. Hay cuatro archivos y una mayor hello tiene aproximadamente 230 GB.

![Se tardó aproximadamente 3.000 segundos contenedor de blob de la cuenta del almacenamiento estándar Azure tooan toocopy Hola de 230 GB](media/sap-hana-backup-file-level/image027.png)

No usar hash md5 en prueba inicial de hello, que tardó aproximadamente 3.000 segundos contenedor de blob de la cuenta del almacenamiento estándar Azure tooan toocopy Hola de 230 GB.

![En esta captura de pantalla, uno puede ver su aspecto en hello portal de Azure](media/sap-hana-backup-file-level/image028.png)

En esta captura de pantalla, uno puede ver su aspecto en hello portal de Azure. Un contenedor de blobs denominado &quot;backups de sap hana&quot; creó e incluye blobs Hola cuatro, que representan los archivos de copia de seguridad de SAP HANA Hola. Uno de ellos tiene un tamaño de aproximadamente 230 GB.

consola de copia de seguridad de Hello HANA Studio permite un tamaño máximo de archivo de hello toorestrict de archivos de copia de seguridad de HANA. En el entorno de ejemplo de Hola, lo mayor rendimiento posible toohave archivos de varias copias de seguridad más pequeños, en lugar de un archivo grande de 230 GB para convertirla.

![Establecer límite de tamaño de archivo de copia de seguridad de hello en hello HANA lado &#39; t mejorar el tiempo de copia de seguridad de Hola](media/sap-hana-backup-file-level/image029.png)

Establecer límite de tamaño de archivo de copia de seguridad de hello en hello HANA lado &#39; t mejoran el tiempo de copia de seguridad de hello, dado que los archivos de saludo se escriben secuencialmente, tal como se muestra en esta ilustración. límite de tamaño de archivo de Hola se estableció too60 GB, por lo que copia de seguridad de hello crea cuatro archivos de datos de gran tamaño en lugar de hello 230 GB único archivo.

![paralelismo de tootest de herramienta de hello blobxfer, tamaño máximo de archivo de Hola para copias de seguridad HANA, a continuación, se estableció too15 GB](media/sap-hana-backup-file-level/image030.png)

paralelismo de tootest de herramienta de hello blobxfer, tamaño máximo de archivo de Hola para copias de seguridad HANA, a continuación, se estableció too15 GB, lo que provocó 19 archivos de copia de seguridad. Esta configuración, vuelva a tiempo hello para el almacenamiento de blobs de blobxfer toocopy Hola de 230 GB tooAzure de 3.000 segundos hacia abajo too875 segundos.

El resultado es pagar toohello límite de 60 MB/s para escribir un blob de Azure. Paralelismo a través de varios blobs resuelve el cuello de botella de hello, pero tiene un inconveniente: aumento del rendimiento de hello blobxfer herramienta toocopy estos tooAzure de copia de seguridad de archivos HANA almacenamiento de blobs supone una carga en hello HANA VM y red de Hola. Afecta al funcionamiento del sistema de HANA.

## <a name="blob-copy-of-dedicated-azure-data-disks-in-backup-software-raid"></a>Copia de blob de discos de datos de Azure dedicados en el software RAID de copia de seguridad

A diferencia de hello VM datos disco copia de seguridad manual, en este enfoque uno no realizar copias de seguridad todos los discos de datos de hello en una máquina virtual toosave Hola SAP instalación completa, incluidos los datos HANA HANA registra los archivos y archivos de configuración. En su lugar, Hola idea es RAID de software toohave dedicado con creación de bandas en varios discos duros virtuales de datos de Azure para almacenar una copia de seguridad completa del archivo de SAP HANA. Una copia de solo estos discos, que tienen copia de seguridad de hello SAP HANA. Se podía mantenerse fácilmente en una cuenta de almacenamiento de copia de seguridad de HANA dedicada o adjunta tooa dedicado &quot;administración de máquinas virtuales de copia de seguridad&quot; para su posterior procesamiento.

![Se han copiado todos los discos duros virtuales implicadas con Hola ** iniciar-azurestorageblobcopy ** comandos de PowerShell](media/sap-hana-backup-file-level/image031.png)

Después de que se completó hello toohello copia de seguridad local de software RAID, todos los discos duros virtuales implicadas se copiaron con hello **inicio azurestorageblobcopy** comando de PowerShell (vea [AzureStorageBlobCopy inicio](/powershell/module/azure.storage/start-azurestorageblobcopy)). Como solo afecta al sistema de archivos de hello dedicado para conservar los archivos de copia de seguridad de hello, no hay preocupaciones acerca de la coherencia de los archivos de datos o de registro de SAP HANA en disco Hola. Una ventaja de este comando es que funciona mientras Hola VM permanece en línea. toobe determinado que no hay ningún proceso escribe un conjunto de copia de seguridad bandas toohello, ser seguro toounmount con anterioridad Hola copia de blob y montar de nuevo posteriormente. O se podría usar un adecuado demasiado&quot;inmovilizar&quot; Hola de sistema de archivos. Por ejemplo, a través de xfs\_inmovilizar Hola XFS sistema de archivos.

![Esta captura de pantalla muestra la lista de Hola de blobs en contenedor de discos duros virtuales Hola Hola portal de Azure](media/sap-hana-backup-file-level/image032.png)

Esta captura de pantalla muestra la lista de Hola de blobs en hello &quot;discos duros virtuales&quot; contenedor en hello portal de Azure. captura de pantalla de Hello muestra hello cinco discos duros virtuales, que estuviera conectada toohello SAP HANA servidor VM tooserve como archivos de copia de seguridad de hello software RAID tookeep SAP HANA. También muestra hello cinco copias, que se han realizado a través del comando de copia de blob de Hola.

![Para realizar pruebas, copias de Hola de los discos RAID de software de copia de seguridad de SAP HANA Hola estaban máquina virtual del servidor de aplicación toohello adjunto](media/sap-hana-backup-file-level/image033.png)

Para realizar pruebas, copias de Hola de los discos RAID de software de copia de seguridad de SAP HANA Hola eran máquina virtual del servidor de aplicación toohello adjunto.

![máquina virtual del servidor de aplicación Hola se cerró tooattach Hola disco copias](media/sap-hana-backup-file-level/image034.png)

máquina virtual del servidor de aplicación Hola se cerró tooattach Hola disco copias. Después de iniciar Hola VM, se detectaron correctamente hello RAID y discos de hello (montado a través de UUID). Solo el punto de montaje Hola faltaba, que se creó mediante particionador de YaST Hola. Después copias de archivos de copia de seguridad de SAP HANA de hello pasara a ser visibles en el nivel del sistema operativo.

## <a name="copy-sap-hana-backup-files-toonfs-share"></a>Copiar archivos de copia de seguridad de SAP HANA tooNFS compartir

toolessen Hola posible impacto en el sistema de SAP HANA desde una perspectiva de espacio de disco o rendimiento hello, uno puede almacenar los archivos de copia de seguridad de SAP HANA hello en un recurso compartido NFS. Técnicamente funciona, pero significa utilizando una segunda máquina virtual de Azure como host de Hola de hello que recursos compartidos de NFS. No debe ser un tamaño de máquina virtual pequeño, debido a ancho de banda de red VM de toohello. Sería sentido, a continuación, tooshut hacia abajo esto &quot;VM de copia de seguridad&quot; y solo se ponga a ejecutar copia de seguridad de hello SAP HANA. Escribir en un NFS recurso compartido supone una carga de red de Hola e impactos Hola sistema SAP HANA, pero simplemente administrar Hola archivos de copia de seguridad después de hello &quot;VM de copia de seguridad&quot; no pueda influir en sistema de SAP HANA hello en absoluto.

![Un recurso compartido NFS desde otra máquina virtual de Azure era la máquina virtual del servidor de SAP HANA toohello montado](media/sap-hana-backup-file-level/image035.png)

caso de uso de hello tooverify NFS, un recurso compartido NFS desde otra máquina virtual de Azure fue la máquina virtual del servidor de SAP HANA toohello montada. No se ha aplicado ningún ajuste de NFS especial.

![Tardó copia de seguridad de 1 hora y 46 minutos toodo Hola directamente](media/sap-hana-backup-file-level/image036.png)

recurso compartido NFS de Hello era un conjunto de bandas rápida, como Hola uno en el servidor de SAP HANA Hola. No obstante, se tardaron 1 hora y Hola de 46 minutos toodo copia de seguridad directamente en el recurso compartido NFS de hello en lugar de 10 minutos, cuando se escribe un conjunto de bandas local tooa.

![alternativa de Hello no estaba mucho más rápido en 1 hora y 43 minutos](media/sap-hana-backup-file-level/image037.png)

alternativa de Hola de realizar un conjunto de bandas local de copia de seguridad tooa y copiar toohello recursos compartidos de NFS en el nivel del sistema operativo (un sencillo **cp - avr** comandos) no estaba mucho más rápido. Se tardó 1 hora y 43 minutos.

Por lo que funciona, pero el rendimiento no era válido durante la prueba de copia de seguridad de 230 GB Hola. Podría ser incluso peor para varios terabytes.

## <a name="copy-sap-hana-backup-files-tooazure-file-service"></a>Copie el servicio de archivos de tooAzure de archivos de copia de seguridad de SAP HANA

Es posible toomount compartir un archivo de Azure dentro de una máquina virtual Linux de Azure. artículo de Hello [cómo toouse almacenamiento de archivos de Azure con Linux](../../../storage/files/storage-how-to-use-files-linux.md) proporciona detalles acerca de cómo toodo lo. Tenga en cuenta que actualmente hay un límite de cuota de 5 TB de un recurso compartido de archivos de Azure y un límite de tamaño de archivo de 1 TB por cada archivo. Vea [Objetivos de escalabilidad y rendimiento de Azure Storage](../../../storage/common/storage-scalability-targets.md) para obtener más información sobre los límites de almacenamiento.

Sin embargo, las pruebas demuestran que la copia de seguridad de SAP HANA no funciona hoy en día directamente con este tipo de montaje CIFS. También se estableció en la [nota 1820529 de SAP](https://launchpad.support.sap.com/#/notes/1820529) que no se recomienda CIFS.

![Esta ilustración muestra un error en el cuadro de diálogo copia de seguridad de Hola de SAP HANA Studio](media/sap-hana-backup-file-level/image038.png)

En esta ilustración se muestra un error en el cuadro de diálogo copia de seguridad de Hola de SAP HANA Studio, al tratar de tooback directamente recurso compartido de archivos de Azure montados en CIFS tooa. Por lo que uno tiene toodo una copia de seguridad estándar de SAP HANA en un sistema de archivos de máquina virtual en primer lugar y, a continuación, archivos de copia de seguridad de Hola desde ahí tooAzure servicio de archivos.

![Esta ilustración muestra que tardó aproximadamente 929 segundos toocopy 19 SAP HANA copias de seguridad](media/sap-hana-backup-file-level/image039.png)

Esta ilustración muestra que tardaron aproximadamente 929 segundos toocopy 19 archivos de copia de seguridad de SAP HANA con un tamaño total aproximadamente 230 GB toohello Azure recurso compartido de archivos.

![estructura de directorios de origen de Hello en hello VM de SAP HANA era el recurso compartido de archivos de Azure toohello copiados](media/sap-hana-backup-file-level/image040.png)

En esta captura de pantalla, se puede ver que estructura de directorios de origen de hello en hello VM de SAP HANA fue recurso compartido de archivos de Azure toohello copiada: un directorio (hana\_copia de seguridad\_fsl\_15 gb) y 19 archivos de copia de seguridad individuales.

Almacenar los archivos de copia de seguridad de SAP HANA en archivos de Azure podría ser una opción interesante en hello futuro, cuando las copias de seguridad del archivo de SAP HANA admitan directamente. O bien, cuando es posible que toomount archivos de Azure a través de NFS y límite de cuota máximo hello es considerablemente mayor que 5 TB.

## <a name="next-steps"></a>Pasos siguientes
* [Guía de copia de seguridad de SAP HANA en Azure Virtual Machines](sap-hana-backup-guide.md) ofrece una introducción e información sobre los pasos iniciales.
* [Copia de seguridad de SAP HANA basándose en instantáneas de almacenamiento](sap-hana-backup-storage-snapshots.md) describe Hola almacenamiento basados en instantáneas copia de seguridad de las opciones.
* toolearn tooestablish alta disponibilidad y el plan de recuperación ante desastres de SAP HANA en Azure (instancias grandes), vea [SAP HANA (instancias de gran tamaño) alta disponibilidad y recuperación ante desastres en Azure](hana-overview-high-availability-disaster-recovery.md).
