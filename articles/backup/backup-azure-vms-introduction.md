---
title: "aaaPlanning su infraestructura de copia de seguridad de máquina virtual en Azure | Documentos de Microsoft"
description: "Consideraciones importantes al planear tooback las máquinas virtuales en Azure"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "copias de seguridad de máquinas virtuales, realizar copias de seguridad de máquinas virtuales"
ms.assetid: 19d2cf82-1f60-43e1-b089-9238042887a9
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: d11982431610000293038ee6aa7df8e7bc2d8b70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="plan-your-vm-backup-infrastructure-in-azure"></a>Planeación de la infraestructura de copia de seguridad de máquinas virtuales en Azure
Este artículo proporciona rendimiento y recursos sugerencias toohelp planear la infraestructura de copia de seguridad de la máquina virtual. También define los aspectos clave del servicio de copia de seguridad de hello; estos aspectos pueden resultar fundamental para determinar la arquitectura, planificación de capacidad y la programación. Si ha [preparado el entorno](backup-azure-vms-prepare.md), planificación es el paso siguiente Hola antes de empezar [tooback las máquinas virtuales](backup-azure-vms.md). Si necesita obtener más información acerca de máquinas virtuales de Azure, vea hello [documentación de máquinas virtuales](https://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="how-does-azure-back-up-virtual-machines"></a>¿Cómo realiza Azure la copia de seguridad de las máquinas virtuales?
Cuando Hola servicio copia de seguridad de Azure inicia un trabajo de copia de seguridad en tiempo de hello programado, desencadena Hola extensión de reserva tootake una instantánea en un momento. Hola servicio de copia de seguridad de Azure usa hello _VMSnapshot_ extensión en Windows y hello _VMSnapshotLinux_ extensión en Linux. Hola extensión se instala durante la copia de seguridad de hello primera máquina virtual. extensión de hello tooinstall, Hola VM debe estar ejecutándose. Si hello no se está ejecutando, Hola servicio de copia de seguridad toma una instantánea de hello almacenamiento subyacente (debido a que ninguna aplicación de escritura aparecen al Hola que VM está en estado detenido).

Cuando se toma una instantánea de máquinas virtuales de Windows, servicio de copia de seguridad de Hola coordina con tooget de servicio de instantáneas de volumen (VSS) de hello una instantánea coherente de los discos de la máquina virtual Hola. Si hace copia de seguridad de máquinas virtuales de Linux, puede escribir su propia coherencia de tooensure scripts personalizados al tomar una instantánea de máquina virtual. Más adelante en este artículo se proporcionan más detalles sobre cómo invocar estas secuencias de comandos.

Una vez Hola servicio de copia de seguridad de Azure toma instantáneas de hello, datos de hello están el almacén de toohello transferidos. toomaximize eficacia, servicio de hello identifica y transfiere únicamente los bloques de datos que han cambiado desde la copia de seguridad anterior de Hola Hola.

![Arquitectura de copia de seguridad de máquinas virtuales de Azure](./media/backup-azure-vms-introduction/vmbackup-architecture.png)

Una vez completada la transferencia de datos hello, instantánea Hola se quita y se crea un punto de recuperación.

> [!NOTE]
> 1. Durante el proceso de copia de seguridad de hello, copia de seguridad de Azure no incluye Hola temporal disco conectado toohello virtual machine. Para obtener más información, consulte el blog de hello en [almacenamiento temporal](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/).
> 2. Puesto que la copia de seguridad de Azure toma una instantánea de nivel de almacenamiento y las transferencias que toovault de instantáneas, no cambie claves de cuenta de almacenamiento de hello hasta que finalice el trabajo de copia de seguridad de Hola.
> 3. Para las máquinas virtuales de premium, copiaremos toostorage cuenta de hello instantánea. Se trata de toomake seguro de que el servicio de copia de seguridad de Azure obtiene suficientes IOPS para transferir datos toovault. Esta copia adicional de almacenamiento se cobra según Hola VM tamaño asignado. 
>

### <a name="data-consistency"></a>Coherencia de datos
Copia de seguridad y restaurar los datos críticos del negocio resulta complicada por el hecho de Hola que deben hacer copia los datos críticos del negocio mientras las aplicaciones de Hola que generan Hola ejecutan datos. tooaddress, copias de seguridad coherentes con la aplicación de copia de seguridad de Azure admite para máquinas virtuales de Linux y Windows
#### <a name="windows-vm"></a>Máquina virtual de Windows
Copia de seguridad de Azure realiza copias de seguridad completas de VSS en máquinas virtuales de Windows (más información sobre [copia de seguridad completa de VSS](http://blogs.technet.com/b/filecab/archive/2008/05/21/what-is-the-difference-between-vss-full-backup-and-vss-copy-backup-in-windows-server-2008.aspx)). tooenable VSS copia copias de seguridad, Hola siguiente conjunto de toobe necesidades clave del registro de hello máquina virtual.

```
[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT]
"USEVSSCOPYBACKUP"="TRUE"
```

#### <a name="linux-vms"></a>Máquinas virtuales con Linux
Azure Backup proporciona un marco de trabajo para las secuencias de comandos. coherencia con las aplicaciones tooensure al realizar copias de seguridad de máquinas virtuales de Linux, crear scripts previos personalizados y secuencias de comandos posteriores a la que controlan el flujo de trabajo de copia de seguridad de Hola y entorno. Copia de seguridad de Azure hello secuencia de comandos anterior, invoca antes de realizar la instantánea de la VM de Hola y script posterior a la de hello, invoca una vez completado el trabajo de instantáneas de máquina virtual de Hola. Para obtener más información, consulte sobre [copias de seguridad de máquinas virtuales coherentes con la aplicación mediante las secuencias de comandos anteriores y posteriores](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).
> [!NOTE]
> Copia de seguridad de Azure, solo invoca Hola escrito por el cliente anterior scripts y posteriores. Si el script previo de Hola y scripts posteriores a la se ejecutan correctamente, copia de seguridad de Azure marca punto de recuperación de hello como aplicación coherente. Sin embargo, al cliente de hello es el responsable último de coherencia de la aplicación hello cuando se utilizan scripts personalizados.
>


Esta tabla explica los tipos de Hola de hello y coherencia condiciones que se producen en durante la copia de seguridad de máquina virtual de Azure y procedimientos de restauración.

| Coherencia | Con base en VSS | Explicación y detalles |
| --- | --- | --- |
| Coherencia de las aplicaciones |Sí para Windows|Se trata del tipo de coherencia ideal para las cargas de trabajo, ya que garantiza que:<ol><li> Hola VM *arranca*. <li>No hay *daños*. <li>No hay *pérdida de datos*.<li> datos de Hello están aplicación de toohello coherente que utiliza datos de hello, por implicadas en la aplicación hello en tiempo de Hola de copia de seguridad--mediante script VSS o anterior o posterior.</ol> <li>*Máquinas virtuales de Windows*-las cargas de trabajo de Microsoft más tengan escritores VSS que realizan acciones específicas de la carga de trabajo relacionados toodata coherencia. Por ejemplo, Microsoft SQL Server tiene un escritor VSS que garantiza que se realizan correctamente el archivo de registro de transacciones de hello escrituras toohello y base de datos de Hola. Copias de seguridad de la máquina virtual de Windows Azure, toocreate un punto de recuperación coherentes con la aplicación, extensión de copia de seguridad de hello debe invocar el flujo de trabajo de hello VSS y completar antes de realizar la instantánea de la VM de Hola. Para hello Azure VM instantánea toobe preciso, los escritores VSS de Hola de todas las aplicaciones de Azure VM deben completar también. (Obtenga información acerca de hello [conceptos básicos de VSS](http://blogs.technet.com/b/josebda/archive/2007/10/10/the-basics-of-the-volume-shadow-copy-service-vss.aspx) y profundice en los detalles de Hola de [su funcionamiento](https://technet.microsoft.com/library/cc785914%28v=ws.10%29.aspx)). </li> <li> *Máquinas virtuales de Linux*-los clientes pueden ejecutar [tooensure personalizado de script previo y posterior a la coherencia de la aplicación](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent). </li> |
| Coherencia del sistema de archivos |Sí, para equipos basados en Windows |Hay dos escenarios donde puede ser el punto de recuperación de hello *coherente de sistema de archivos*:<ul><li>Copias de seguridad de máquinas virtuales con Linux en Azure, sin los script anterior y posterior, o en caso de que estos generen errores. <li>Error de VSS durante la copia de seguridad de máquinas virtuales Windows en Azure.</li></ul> En ambos casos estos, Hola recomendado que se puede hacer es tooensure que: <ol><li> Hola VM *arranca*. <li>No hay *daños*.<li>No hay *pérdida de datos*.</ol> Las aplicaciones necesitan mecanismo tooimplement su propios "revisión de seguridad" en los datos de hello restaurado. |
| Coherencia de bloqueos |No |Esta situación es la máquina virtual de tooa equivalente experimentan un "bloqueo" (a través de un restablecimiento parcial o disco duro). Coherencia de bloqueo suele sucede cuando se cierra Hola máquina virtual de Azure en tiempo de Hola de copia de seguridad. Un punto de recuperación coherente para bloqueos no proporciona ninguna garantía alrededor de coherencia de Hola de los datos de hello en medio de almacenamiento de hello, ya sea desde la perspectiva de Hola de sistema operativo de Hola o aplicación hello. Los únicos datos de Hola que ya existe en el disco de hello en tiempo de Hola de copia de seguridad se capturan y copia de seguridad. <br/> <br/> Aunque no hay ninguna garantía, normalmente, Hola arranque del sistema operativo, seguido de comprobación de disco procedimiento, como chkdsk, toofix los errores por daños. Los datos en memoria o escribe que no se han transferido toohello disco se pierden. aplicación Hello sigue normalmente con su propio mecanismo de comprobación en caso de que la desinstalación de datos necesita toobe realiza. <br><br>Por ejemplo, si el registro de transacciones de hello tiene entradas que no están presentes en la base de datos de hello, a continuación, software de base de datos de hello hace una reversión hasta que Hola datos son coherentes. Cuando los datos se distribuyen en varios discos virtuales (por ejemplo, los volúmenes distribuidos), un punto de recuperación coherente para bloqueos no proporciona ninguna garantía de exactitud de Hola de datos de Hola. |

## <a name="performance-and-resource-utilization"></a>Rendimiento y uso de recursos
Al igual que el software de copia de seguridad que se implementa de forma local, debe planear las necesidades de capacidad y utilización de recursos al realizar la copia de seguridad de máquinas virtuales en Azure. Hola [limita el almacenamiento de Azure](../azure-subscription-service-limits.md#storage-limits) definir cómo afecta a las cargas de trabajo de toorunning toostructure VM implementaciones tooget rendimiento máximo con como mínimo.

Pagar toohello atención que siguiente almacenamiento de Azure limita al planear el rendimiento de copia de seguridad:

* Salida máxima por cuenta de almacenamiento
* Tasa de solicitud total por cuenta de almacenamiento

### <a name="storage-account-limits"></a>Límites de la cuenta de almacenamiento
Datos de copia de seguridad copiado desde una cuenta de almacenamiento, se agrega toohello operaciones de entrada/salida por segundo (IOPS) y las métricas de salida (o rendimiento) de cuenta de almacenamiento de Hola. Hola al mismo tiempo máquinas virtuales también están consumiendo IOPS y el rendimiento. el objetivo de Hello es tooensure copia de seguridad y tráfico de máquinas virtuales no superan los límites de su cuenta de almacenamiento.

### <a name="number-of-disks"></a>Número de discos
proceso de copia de seguridad de Hello intenta toocomplete un trabajo de copia de seguridad tan pronto como sea posible. Con ello, se consume tantos recursos como es posible. Sin embargo, todas las operaciones de E/S están limitadas por hello *rendimiento total único Blob*, que tiene un límite de 60 MB por segundo. En un intento de toomaximize su velocidad, proceso de copia de seguridad de hello intenta tooback cada uno de los discos de la máquina virtual de hello *en paralelo*. Si una máquina virtual tiene cuatro discos, servicio de hello intenta tooback los todos los cuatro discos en paralelo. Hola **número de discos** copia de seguridad, es el factor más importante de Hola para determinar el tráfico de copia de seguridad de cuenta de almacenamiento.

### <a name="backup-schedule"></a>Programación de copia de seguridad
Otro factor que afecta al rendimiento es hello **programar copia de seguridad**. Si configura las directivas de Hola para todas las máquinas virtuales se copian en hello mismo tiempo, se ha programado un atasco de tráfico. proceso de copia de seguridad de Hello intenta tooback los todos los discos en paralelo. tráfico de copia de seguridad de Hola de tooreduce desde una cuenta de almacenamiento, copia de seguridad diferentes máquinas virtuales en otro momento del día de hello, sin superposición.

## <a name="capacity-planning"></a>Planificación de capacidad
Que reúnan los factores anteriores hello, necesitará tooplan para necesidades de uso de cuenta de almacenamiento de Hola. Descargar hello [hoja de cálculo de Excel de planeación de la capacidad de copia de seguridad virtual](https://gallery.technet.microsoft.com/Azure-Backup-Storage-a46d7e33) impacto de hello toosee de su disco y las opciones de programación de copia de seguridad.

### <a name="backup-throughput"></a>Rendimiento de la copia de seguridad
Para cada disco haciendo copias de seguridad, copia de seguridad de Azure lee bloques de hello en el disco de Hola y almacenes de Hola solo datos modificados (copia de seguridad incremental). Hello tabla siguiente muestran valores de rendimiento de copia de seguridad promedio de hello servicio. Hola después de datos puede calcular cantidad Hola de tiempo que sea necesario tooback configurar un disco de un tamaño determinado.

| Operación de copia de seguridad | Mejor rendimiento |
| --- | --- |
| Copia de seguridad inicial |160 Mbps |
| Copia de seguridad incremental (DR) |640 Mbps  <br><br> Quita de rendimiento considerablemente si Hola cambia datos (que es necesario toobe copia de seguridad) es dispersa en disco Hola.|

## <a name="total-vm-backup-time"></a>Tiempo total de copia de seguridad de máquinas virtuales
Aunque la mayor parte de hora de copia de seguridad de Hola se dedica a leer y copiar los datos, otras operaciones contribuyen toohello tiempo total necesario tooback seguridad de una máquina virtual:

* Necesita demasiado tiempo[instalar o actualizar la extensión de copia de seguridad de hello](backup-azure-vms.md).
* Hora de la instantánea, que es hello tootrigger de tiempo que tarda una instantánea. Las instantáneas son de tiempo de copia de seguridad de desencadenadas toohello cierre programado.
* Tiempo de espera en la cola. Puesto que el servicio de copia de seguridad de Hola procesa con copias de seguridad desde varios clientes, copiar datos de copia de seguridad de servicios de recuperación o copia de seguridad de instantánea toohello almacén podría no iniciarse inmediatamente. En los momentos de picos de carga, puede ajustar Hola espera tooeight horas debido toohello número de copias de seguridad que se va a procesar. Sin embargo, el tiempo de copia de seguridad de VM total hello es inferior a 24 horas para las directivas de copia de seguridad diarias.
* Tiempo de transferencia de datos, tiempo necesario para la copia de seguridad toocompute Hola los cambios incrementales desde la copia de seguridad anterior del servicio y transferir esos almacenamiento toovault de cambios.

### <a name="why-am-i-observing-longer12-hours-backup-time"></a>¿Por qué veo un tiempo de copia de seguridad más largo (>12 horas)?
Copia de seguridad consta de dos fases: tomar instantáneas y la transferencia de Hola instantáneas toohello almacén. Hola servicio de copia de seguridad se optimiza para el almacenamiento. Al transferir datos tooa almacén de hello instantánea, servicio de hello transfiere solo los cambios incrementales desde la instantánea anterior Hola.  toodetermine cambios incrementales de hello, servicio de hello calcula suma de comprobación de Hola de bloques de Hola. Si se cambia un bloque, bloque de Hola se identifica como un toobe de bloque enviado toohello almacén. A continuación, aumenta el servicio Hola aún más en cada una de Hola habían identificado bloques, buscando oportunidades toominimize Hola datos tootransfer. Después de evaluar todos los bloques cambiados, servicio de hello fusiona cambios hello y los envía toohello almacén. En algunas aplicaciones heredadas, las escrituras pequeñas y fragmentadas no son óptimas para el almacenamiento. Si instantánea hello contiene muchas escrituras pequeñas, fragmentados, servicio Hola emplea más tiempo de procesamiento de datos de hello escritos aplicaciones de Hola. Hola recomendada bloque de escritura de aplicaciones de Azure, para aplicaciones que se ejecutan dentro de Hola de máquina virtual, es un mínimo de 8 KB. Si la aplicación utiliza un bloque de menos de 8 KB, se realiza el rendimiento de copia de seguridad. Para obtener ayuda con el rendimiento de copia de seguridad de tooimprove de aplicación para la optimización, vea [aplicaciones para un rendimiento óptimo con el almacenamiento de Azure para la optimización](../storage/common/storage-premium-storage-performance.md). Aunque el artículo de hello en el rendimiento de copia de seguridad utilizan ejemplos de almacenamiento Premium, instrucciones de hello es aplicable para discos de almacenamiento estándar.

## <a name="total-restore-time"></a>Tiempo total de restauración
Una operación de restauración consta de dos tareas de sub main: copiar datos desde la cuenta de almacenamiento del cliente de hello almacén toohello elegido y la creación de la máquina virtual de Hola. Copiar datos desde el almacén de hello depende de dónde se almacenan internamente las copias de seguridad de hello en Azure y donde se almacena la cuenta de almacenamiento del cliente de Hola. Tiempo que tarda toocopy datos depende de:
* -Tiempo de espera en cola desde procesos de servicio de hello trabajos de restauración desde varios clientes en hello mismo tiempo, las solicitudes de restauración son ponen en cola.
* Tiempo - de copia de datos se copian datos de cuenta de almacenamiento de hello almacén toohello cliente. Restaurar tiempo depende de IOPS y obtiene rendimiento servicio de copia de seguridad de Azure en la cuenta de almacenamiento del cliente de hello seleccionado. tooreduce Hola Copiar hora durante el proceso de restauración de hello, seleccione una cuenta de almacenamiento no se cargó con otras lecturas y escrituras de aplicación.

## <a name="best-practices"></a>Prácticas recomendadas
Se recomienda seguir estos procedimientos recomendados al configurar copias de seguridad para máquinas virtuales:

* No programar más de 10 VM clásicas de hello mismo nube servicio tooback en hello mismo tiempo. Si desea tooback de varias máquinas virtuales del mismo servicio en la nube, escalonar las horas de inicio de copia de seguridad de hello en una hora.
* No programe más de 40 tooback de máquinas virtuales de seguridad en hello mismo tiempo.
* Programe las copias de seguridad de máquinas virtuales durante horas de poca actividad. Este servicio de copia de seguridad de Hola de forma usa e/s por segundo para transferir datos desde el depósito de toohello de hello del cliente de cuenta.
* Asegúrese de que una directiva se aplique en máquinas virtuales entre distintas cuentas de almacenamiento. Se recomienda no más de 20 total discos desde una única cuenta de almacenamiento estará protegida por hello misma programación de copia de seguridad. Si tiene mayor que 20 discos en una cuenta de almacenamiento, se propagan esas máquinas virtuales a través de varias de las directivas de tooget Hola IOPS necesarias durante la fase de transferencia de hello del proceso de copia de seguridad de Hola.
* No restaure una máquina virtual que se ejecuta en la cuenta de almacenamiento de toosame de almacenamiento Premium. Si el proceso de operación de restauración de hello coincide con la operación de copia de seguridad de hello, reduce Hola IOPS disponible para copia de seguridad.
* Para una copia de seguridad de la máquina virtual Premium, asegúrese de que la cuenta de almacenamiento que hospeda los discos Premium tenga al menos 50 % de espacio libre para que la instantánea de almacenamiento provisional realice una copia de seguridad correcta. 
* Asegúrese de que la versión de python en máquinas virtuales Linux habilitadas para la copia de seguridad sea 2.7

## <a name="data-encryption"></a>Cifrado de datos
Copia de seguridad de Azure no cifra los datos como parte del proceso de copia de seguridad de Hola. Sin embargo, puede cifrar los datos dentro de hello VM y copia de seguridad Hola datos protegidos sin problemas (Obtenga más información sobre [copia de seguridad de los datos cifrados](backup-azure-vms-encryption.md)).

## <a name="calculating-hello-cost-of-protected-instances"></a>Calcular el costo de Hola de instancias protegidas
Máquinas virtuales de Azure que se copian mediante copia de seguridad de Azure están sujetas demasiado[precios de copia de seguridad de Azure](https://azure.microsoft.com/pricing/details/backup/). Hola cálculo de instancias protegidas se basa en hello *real* tamaño de máquina virtual de hello, que es la suma de Hola de todos los datos de hello en la máquina virtual de hello--excepto Hola "disco de recursos".

Precios de copia de seguridad de máquinas virtuales es *no* según tamaño Hola máximo compatible para cada máquina virtual de datos disco toohello adjunto. Precio se basa en datos reales de hello almacenados en disco de datos de Hola. Del mismo modo, facturación de almacenamiento de copia de seguridad de Hola se basa en la cantidad de Hola de datos que se almacenan en la copia de seguridad de Azure, que es la suma de Hola de datos reales de hello en cada punto de recuperación.

Por ejemplo, veamos una máquina virtual de tamaño estándar A2 con dos discos de datos adicionales con un tamaño máximo de 1 TB cada uno. Hello siguiente tabla ofrece Hola datos almacenados en cada uno de estos discos:

| Tipo de disco | Tamaño máximo | Datos reales presentes |
| --- | --- | --- |
| Disco del sistema operativo |1023 GB |17 GB |
| Disco local o disco de recursos |135 GB |5 GB (no incluidos en la copia de seguridad) |
| Disco de datos 1 |1023 GB |30 GB |
| Disco de datos 2 |1023 GB |0 GB |

Hola *real* en este caso es el tamaño de máquina virtual de Hola de 17 GB + 30 GB + 0 GB = 47 GB. Este tamaño de instancias protegidas (47 GB) se convierte en la base de Hola para factura mensual de Hola. Como Hola cantidad de datos en una máquina virtual de hello crece, tamaño de instancias protegidas Hola usado para los cambios de facturación en consecuencia.

Facturación no se inicia hasta que se complete la copia de seguridad correcta Hola primero. En este momento, comienza la facturación hello para el almacenamiento e instancias protegidas. Facturación permanecerá así siempre que hay *cualquier copia de seguridad de datos almacenados en un almacén* para la máquina virtual de Hola. Si detiene la protección en la máquina virtual de hello, pero hay datos de copia de seguridad de máquinas virtuales en un almacén, continúa la facturación.

Facturación de una máquina virtual especificada se detiene solo si se detiene la protección de Hola *y* se eliminan todos los datos de copia de seguridad. Cuando se detiene la protección y no hay ningún trabajo de copia de seguridad activa, tamaño Hola de hello última VM copia de seguridad correcta se convierte en el tamaño de instancias protegidas de hello utilizado para la factura mensual de Hola.

## <a name="questions"></a>¿Tiene preguntas?
Si tiene alguna pregunta, o si hay cualquier característica que le gustaría toosee incluido, [nos envíe sus comentarios](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Pasos siguientes
* [Copia de seguridad de máquinas virtuales](backup-azure-vms.md)
* [Administrar copia de seguridad de máquina virtual](backup-azure-manage-vms.md)
* [Restauración de máquinas virtuales](backup-azure-restore-vms.md)
* [Solución de problemas de copia de seguridad de máquinas virtuales](backup-azure-vms-troubleshoot.md)
