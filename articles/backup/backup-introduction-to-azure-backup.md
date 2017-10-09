---
title: "¿aaaWhat es la copia de seguridad de Azure? | Microsoft Docs"
description: "Utilice tooback de copia de seguridad de Azure y restaurar los datos y las cargas de trabajo de servidores de Windows, las estaciones de trabajo de Windows, servidores de System Center DPM y máquinas virtuales de Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "copia de seguridad y restauración; servicios de recuperación; soluciones de copia de seguridad"
ms.assetid: 0d2a7f08-8ade-443a-93af-440cbf7c36c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/11/2017
ms.author: markgal;trinadhk;anuragm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 953a19600f67a6b7451f71b1e3234d913816d18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-features-in-azure-backup"></a>Información general de las características de hello en copia de seguridad de Azure
Copia de seguridad de Azure es servicio de basado en Azure de hello puede consumir tooback (o proteger) y restaurar los datos en la nube de Microsoft Hola. Reemplaza su solución de copia de seguridad local o remota existente por una solución confiable, segura y rentable basada en la nube. Copia de seguridad de Azure ofrece varios componentes que descargar e implementar en el equipo adecuado que hello, server, o en la nube de Hola. componente de Hello, o el agente, que se implementa depende de qué desea tooprotect. Todos los componentes de copia de seguridad de Azure (con independencia de si va a proteger datos de forma local o en la nube de hello) pueden ser usado tooback el almacén de servicios de recuperación de datos tooa en Azure. Vea hello [tabla de componentes de copia de seguridad de Azure](backup-introduction-to-azure-backup.md#which-azure-backup-components-should-i-use) (más adelante en este artículo) para obtener información acerca de qué datos específicos del componente toouse tooprotect, aplicaciones o cargas de trabajo.

[Ver un vídeo de información general de Azure Backup](https://azure.microsoft.com/documentation/videos/what-is-azure-backup/)

## <a name="why-use-azure-backup"></a>¿Por qué usar Azure Backup?
Las soluciones tradicionales de copia de seguridad han evolucionado en la nube tootreat Hola como un punto de conexión, o un destino de almacenamiento estática, similar toodisks o una cinta. Si bien este enfoque es sencillo, es limitado y no aprovechar al máximo de una plataforma de nube subyacente, lo que se traduce tooan costosos y poco eficaces soluciones. Otras soluciones son caras porque terminará pagar por un tipo de almacenamiento o almacenamiento que no es necesario Hola incorrecto. Otras soluciones a menudo son ineficaces porque no ofrecen, tipo de Hola o la cantidad de almacenamiento que necesita, o tareas administrativas requieren demasiado tiempo. En cambio, Azure Backup proporciona las siguientes ventajas principales:

**Administración de almacenamiento automático** : a menudo, los entornos híbridos requieren almacenamiento heterogéneo: algunos locales y otras en hello en la nube. Con Azure Backup, no hay ningún costo por el uso de dispositivos de almacenamiento local. Azure Backup asigna y administra automáticamente almacenamiento de copia de seguridad y emplea un modelo de pago por uso. Pague como-usar significa que solo se paga por almacenamiento de Hola que utilizará. Para obtener más información, vea hello [Azure precios artículo](https://azure.microsoft.com/pricing/details/backup).

**Ajuste de escala en ilimitado** : copia de seguridad de Azure utiliza Hola subyacente power y escala ilimitada de hello Azure toodeliver alta disponibilidad - con ningún mantenimiento o carga de supervisión en la nube. Puede configurar la información de tooprovide alertas sobre los eventos, pero no es necesario tooworry sobre alta disponibilidad para los datos en la nube de Hola.

**Varias opciones de almacenamiento**: un aspecto de alta disponibilidad es la replicación del almacenamiento. Azure Backup ofrece dos tipos de replicación: [almacenamiento con redundancia local](../storage/common/storage-redundancy.md#locally-redundant-storage) y [almacenamiento con redundancia geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage). Elija la opción de almacenamiento de copia de seguridad de hello según las necesidades del:

* Almacenamiento con redundancia local (LRS) replica los datos tres veces (crea tres copias de los datos) en un centro de datos emparejado Hola misma región. LRS es una opción de bajo costo para proteger los datos contra errores de hardware local.

* Almacenamiento con redundancia geográfica (GRS) replica la región secundaria de tooa de datos (cientos de miles fuera de la ubicación principal de Hola Hola de datos de origen). GRS cuesta más que LRS, pero proporciona un mayor nivel de durabilidad de los datos, incluso si hay una interrupción regional.

**Transferencia de datos ilimitado** : copia de seguridad de Azure no limita la cantidad de Hola de entrada o salidas transferencia de datos de. También copia de seguridad de Azure no cobra por los datos de Hola que se transfieren. Sin embargo, si usas Hola importación/exportación de Azure servicio tooimport grandes cantidades de datos, hay un costo asociado a los datos de entrada. Para más información sobre este costo, consulte [Flujo de trabajo de copia de seguridad sin conexión en Azure Backup](backup-azure-backup-import-export.md). Datos de salida refieren toodata transferido desde un almacén de servicios de recuperación durante una operación de restauración.

**Cifrado de datos** -cifrado de datos permite la transmisión segura y almacenamiento de los datos en la nube pública de Hola. Almacenar Hola frase de contraseña localmente, y nunca se transmiten o almacenado en Azure. Si es necesario toorestore cualquier de los datos de hello, sólo dispone de frase de contraseña o clave.

**Copia de seguridad coherentes con la aplicación** -si copia de seguridad de un servidor de archivos, la máquina virtual o la base de datos SQL, necesita tooknow que un punto de recuperación tiene todas requiere la copia de seguridad de datos toorestore Hola. Copia de seguridad de Azure proporciona copias de seguridad coherentes con la aplicación, que garantiza correcciones adicionales no son necesarios toorestore Hola datos. Restaurar datos coherentes de aplicación reduce el tiempo de restauración de hello, permitiéndole tooquickly tooa devuelto estado de ejecución.

**Retención a largo plazo** -en lugar de cambiar las copias de seguridad de disco tootape y móvil Hola cinta tooan fuera de las instalaciones, puede usar Azure para la retención a corto plazo y a largo plazo. Azure no limita Hola tiempo los datos permanecen en un almacén de copia de seguridad o los servicios de recuperación. Los datos se pueden conservar en un almacén tanto tiempo como se desee. Azure Backup tiene un límite de 9999 puntos de recuperación por instancia protegida. Vea hello [copias de seguridad y retención](backup-introduction-to-azure-backup.md#backup-and-retention) sección de este artículo para obtener una explicación de cómo este límite puede afectar a sus necesidades de copia de seguridad.  

## <a name="which-azure-backup-components-should-i-use"></a>¿Qué componentes de Azure Backup debo usar?
Si no está seguro de qué componente de copia de seguridad de Azure funciona para sus necesidades, vea Hola para obtener información sobre lo que se puede proteger con cada componente en la tabla siguiente. Hola portal de Azure proporciona a un asistente, que está integrado en el portal de hello, tooguide a través de la elección de Hola toodownload componente e implementación. Asistente de Hello, que forma parte de la creación del almacén de servicios de recuperación de hello, muestran los pasos de Hola para seleccionar un objetivo de copia de seguridad y luego tooprotect de datos o una aplicación Hola a.

| Componente | Ventajas | límites | ¿Qué se protege? | ¿Dónde se almacenan las copias de seguridad? |
| --- | --- | --- | --- | --- |
| Agente de Azure Backup (MARS) |<li>Copia de seguridad de archivos y carpetas en el sistema operativo Windows físico o virtual (las máquinas virtuales pueden estar en el entorno local o en Azure)<li>No se necesita ningún servidor de copia de seguridad independiente. |<li>Copia de seguridad tres veces al día <li>No es compatible con la aplicación; restauración solo a nivel de archivo, carpeta y volumen. <li>  No se admite Linux. |<li>Archivos <li>Carpetas |Almacén de Recovery Services |
| System Center DPM |<li>Instantáneas compatibles con aplicación (VSS)<li>Total flexibilidad para decidir cuándo las copias de seguridad de tootake<li>Granularidad en la recuperación (todo)<li>Puede usar un almacén de Recovery Services<li>Linux Support en máquinas virtuales de Hyper-V y VMware <li>Copia de seguridad y restauración de máquinas virtuales de VMware mediante DPM 2012 R2 |No puede realizar la copia de seguridad de una carga de trabajo de Oracle.|<li>Archivos <li>Carpetas<li> Volúmenes <li>Máquinas virtuales<li> Aplicaciones<li> Cargas de trabajo |<li>Almacén de Recovery Services,<li> Disco conectado localmente<li>  Cinta (solo local) |
| Azure Backup Server |<li>Instantáneas compatibles con la aplicación (VSS)<li>Total flexibilidad para decidir cuándo las copias de seguridad de tootake<li>Granularidad en la recuperación (todo)<li>Puede usar un almacén de Recovery Services<li>Linux Support en máquinas virtuales de Hyper-V y VMware<li>Creación de copias de seguridad y restauración de máquinas virtuales de VMware <li>No requiere licencia de System Center |<li>No puede realizar la copia de seguridad de una carga de trabajo de Oracle.<li>Siempre requiere una suscripción de Azure activa<li>No se admite la copia de seguridad en cinta |<li>Archivos <li>Carpetas<li> Volúmenes <li>Máquinas virtuales<li> Aplicaciones<li> Cargas de trabajo |<li>Almacén de Recovery Services,<li> Disco conectado localmente |
| Copia de seguridad de máquina virtual de IaaS de Azure |<li>Copias de seguridad nativas de Windows/Linux<li>No se requiere la instalación de ningún agente específico<li>Copia de seguridad de nivel de tejido sin necesidad de ninguna infraestructura de copia de seguridad |<li>Copia de seguridad de máquinas virtuales una vez al día <li>Restauración de máquinas virtuales solo en el nivel de disco<li>No puede realizar copias de seguridad locales |<li>Máquinas virtuales <li>Todos los discos (con PowerShell) |<p>Almacén de Recovery Services</p> |

## <a name="what-are-hello-deployment-scenarios-for-each-component"></a>¿Cuáles son los escenarios de implementación de Hola para cada componente?
| Componente | ¿Se puede implementar en Azure? | ¿Se puede implementar de forma local? | Almacenamiento de destino admitido |
| --- | --- | --- | --- |
| Agente de Azure Backup (MARS) |<p>**Sí**</p> <p>agente de copia de seguridad de Azure Hola se puede implementar en las VM de Windows Server que se ejecuta en Azure.</p> |<p>**Sí**</p> <p>agente de copia de seguridad de Hola se puede implementar en cualquier máquina física o VM de Windows Server.</p> |<p>Almacén de Recovery Services</p> |
| System Center DPM |<p>**Sí**</p><p>Obtenga más información sobre [cómo tooprotect cargas de trabajo en Azure mediante el uso de System Center DPM](backup-azure-dpm-introduction.md).</p> |<p>**Sí**</p> <p>Obtenga más información sobre [cómo tooprotect las cargas de trabajo y las máquinas virtuales en su centro de datos](https://technet.microsoft.com/system-center-docs/dpm/data-protection-manager).</p> |<p>Disco conectado localmente</p> <p>Almacén de Recovery Services,</p> <p>Cinta (solo local)</p> |
| Azure Backup Server |<p>**Sí**</p><p>Obtenga más información sobre [cómo tooprotect cargas de trabajo en Azure mediante el uso de servidor de copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md).</p> |<p>**Sí**</p> <p>Obtenga más información sobre [cómo tooprotect cargas de trabajo en Azure mediante el uso de servidor de copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md).</p> |<p>Disco conectado localmente</p> <p>Almacén de Recovery Services</p> |
| Copia de seguridad de máquina virtual de IaaS de Azure |<p>**Sí**</p><p>Parte del tejido de Azure</p><p>Especializado para [copia de seguridad de máquinas virtuales de infraestructura como servicio (IaaS) de Azure](backup-azure-vms-introduction.md).</p> |<p>**No**</p> <p>Use System Center DPM tooback las máquinas virtuales de su centro de datos.</p> |<p>Almacén de Recovery Services</p> |

## <a name="which-applications-and-workloads-can-be-backed-up"></a>¿De qué aplicaciones y cargas de trabajo puedo hacer copias de seguridad?
Hello en la tabla siguiente proporciona una matriz de datos de Hola y cargas de trabajo que se pueden proteger mediante copia de seguridad de Azure. columna de solución de copia de seguridad de Azure de Hello tiene documentación de implementación de vínculos toohello para esa solución. Cada componente de Azure Backup puede implementarse en un entorno de modelo de implementación clásico (implementación mediante Service Manager) o de Resource Manager.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

| Datos o carga de trabajo | Entorno de origen | Solución de Azure Backup |
| --- | --- | --- |
| Archivos y carpetas |Windows Server |<p>[Agente de Azure Backup](backup-configure-vault.md),</p> <p>[System Center DPM](backup-azure-dpm-introduction.md) (+ agente de copia de seguridad de Azure de hello)</p> <p>[Servidor de copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md) (incluye el agente de copia de seguridad de Azure de hello)</p> |
| Archivos y carpetas |Equipo de Windows |<p>[Agente de Azure Backup](backup-configure-vault.md),</p> <p>[System Center DPM](backup-azure-dpm-introduction.md) (+ agente de copia de seguridad de Azure de hello)</p> <p>[Servidor de copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md) (incluye el agente de copia de seguridad de Azure de hello)</p> |
| Máquina virtual de Hyper-V (Windows) |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ agente de copia de seguridad de Azure de hello)</p> <p>[Servidor de copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md) (incluye el agente de copia de seguridad de Azure de hello)</p> |
| Máquina virtual de Hyper-V (Linux) |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ agente de copia de seguridad de Azure de hello)</p> <p>[Servidor de copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md) (incluye el agente de copia de seguridad de Azure de hello)</p> |
| Microsoft SQL Server |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ agente de copia de seguridad de Azure de hello)</p> <p>[Servidor de copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md) (incluye el agente de copia de seguridad de Azure de hello)</p> |
| Microsoft SharePoint |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ agente de copia de seguridad de Azure de hello)</p> <p>[Servidor de copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md) (incluye el agente de copia de seguridad de Azure de hello)</p> |
| Microsoft Exchange |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ agente de copia de seguridad de Azure de hello)</p> <p>[Servidor de copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md) (incluye el agente de copia de seguridad de Azure de hello)</p> |
| Máquinas virtuales de Azure IaaS (Windows) |Ejecución en Azure |[Copia de seguridad de Azure (extensión de máquina virtual)](backup-azure-vms-introduction.md) |
| Máquinas virtuales de IaaS de Azure (Linux) |Ejecución en Azure |[Copia de seguridad de Azure (extensión de máquina virtual)](backup-azure-vms-introduction.md) |

## <a name="linux-support"></a>Linux Support
Hello tabla siguiente muestran los componentes de copia de seguridad de Azure de Hola que tienen compatibilidad con Linux.  

| Componente | Linux Support (reconocido por Azure) |
| --- | --- |
| Agente de Azure Backup (MARS) |No (solo agente basado en Windows) |
| System Center DPM |<li> Copia de seguridad coherente con archivo de máquinas virtuales invitadas de Linux en Hyper-V y VMWare<br/> <li> Restauración de máquinas virtuales invitadas de Linux en Hyper-V y VMWare </br> </br>  *Copia de seguridad coherente con archivo no disponible para la máquina virtual de Azure* <br/> |
| Azure Backup Server |<li>Copia de seguridad coherente con archivo de máquinas virtuales invitadas de Linux en Hyper-V y VMWare<br/> <li> Restauración de máquinas virtuales invitadas de Linux en Hyper-V y VMWare </br></br> *Copia de seguridad coherente con archivo no disponible para la máquina virtual de Azure*  |
| Copia de seguridad de máquina virtual de IaaS de Azure |Copia de seguridad coherente con la aplicación mediante un [marco de scripts previos y posteriores](backup-azure-linux-app-consistent.md)<br/> [Recuperación de archivos pormenorizada](backup-azure-restore-files-from-vm.md)<br/> [Restauración de todos los discos de máquina virtual](backup-azure-arm-restore-vms.md#restore-backed-up-disks)<br/> [Restauración de máquina virtual](backup-azure-arm-restore-vms.md#create-a-new-vm-from-restore-point) |

## <a name="using-premium-storage-vms-with-azure-backup"></a>Uso de máquinas virtuales de Premium Storage con Azure Backup
Azure Backup protege las máquinas virtuales de Premium Storage. Almacenamiento Premium de Azure es la unidad de estado sólido (SSD)-según las cargas de trabajo intensivas de entrada de almacenamiento de información diseñado toosupport. Premium Storage es adecuado para cargas de trabajo de máquina virtual (VM). Para obtener más información sobre el almacenamiento Premium, vea el artículo de hello [almacenamiento Premium: almacenamiento de alto rendimiento para cargas de trabajo de máquina Virtual de Azure](../storage/common/storage-premium-storage.md).

### <a name="back-up-premium-storage-vms"></a>Copia de seguridad de máquinas virtuales de Premium Storage
Mientras la copia de seguridad de máquinas virtuales de almacenamiento de Premium, servicio de copia de seguridad de hello crea una ubicación de almacenamiento provisional temporal, había denominado "AzureBackup-", en la cuenta de almacenamiento Premium de Hola. tamaño de Hola de hello ubicación de almacenamiento provisional es tamaño toohello igual de instantánea de punto de recuperación de Hola. Asegúrese de hello cuenta de almacenamiento Premium tiene la ubicación de almacenamiento provisional de temporal de espacio libre suficiente tooaccommodate Hola. Para obtener más información, vea el artículo de hello [limitaciones de almacenamiento premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets). Una vez que finalice el trabajo de copia de seguridad de hello, Hola ubicación de almacenamiento provisional se elimina. Hello precio de almacenamiento utilizado para la ubicación de almacenamiento provisional de hello es coherente con todas las [precios del almacenamiento Premium](../storage/common/storage-premium-storage.md#pricing-and-billing).

> [!NOTE]
> No modifique ni editar Hola ubicación de almacenamiento provisional.
>
>

### <a name="restore-premium-storage-vms"></a>Restauración de máquinas virtuales de Premium Storage
Máquinas virtuales de almacenamiento Premium puede ser almacenamiento de almacenamiento Premium o toonormal tooeither restaurada. Restaurar un tooPremium atrás de máquina virtual de almacenamiento Premium recuperación punto de almacenamiento es el proceso típico de Hola de restauración. Sin embargo, puede ser más rentable toorestore un almacenamiento de toostandard de punto de recuperación de máquina virtual de almacenamiento Premium. Este tipo de restauración puede usarse si necesita un subconjunto de archivos de hello máquina virtual.

## <a name="using-managed-disk-vms-with-azure-backup"></a>Uso de máquinas virtuales de disco administrado con Azure Backup
Azure Backup protege las máquinas virtuales de disco administrado. Los discos administrados le liberan de la administración de cuentas de almacenamiento de máquinas virtuales simplifican en gran medida el aprovisionamiento de las máquinas virtuales.

### <a name="back-up-managed-disk-vms"></a>Copia de seguridad de máquinas virtuales de disco administrado
Realizar copias de seguridad de máquinas virtuales en discos administrados no es tan diferente a realizar copias de seguridad de máquinas virtuales de Resource Manager. Hola portal de Azure, puede configurar el trabajo de copia de seguridad de hello directamente desde Hola vista de máquina Virtual o de servicios de recuperación de hello del almacén de vista. Puede realizar la copia de seguridad de máquinas virtuales en discos administrados mediante colecciones de RestorePoint basadas en discos administrados. Azure Backup también admite la realización de copias de seguridad de máquinas virtuales de discos administrados cifradas mediante Azure Disk Encryption (ADE).

### <a name="restore-managed-disk-vms"></a>Restauración de máquinas virtuales de disco administrado
Copia de seguridad de Azure permite toorestore una máquina virtual completa con discos administrados o restauración administra la cuenta de almacenamiento de discos tooa. Azure administra discos Hola administrado durante el proceso de restauración de Hola. Usted (cliente hello) administra cuenta de almacenamiento de hello creado como parte del proceso de restauración de Hola. Al restaurar administrado cifrados de las máquinas virtuales, hello claves y secretos de la máquina virtual deben existir en operación de restauración de hello almacén de claves anterior toostarting Hola.

## <a name="what-are-hello-features-of-each-backup-component"></a>¿Cuáles son las características de Hola de cada componente de copia de seguridad?
Hola las secciones siguientes proporciona tablas que se resumen la disponibilidad de Hola o soporte técnico de diversas características de cada componente de copia de seguridad de Azure. Consulte la información de hello cada para soporte técnico adicional o los detalles de la tabla siguiente.

### <a name="storage"></a>Storage
| Característica | Agente de Azure Backup | System Center DPM | Azure Backup Server | Copia de seguridad de máquina virtual de IaaS de Azure |
| --- | --- | --- | --- | --- |
| Almacén de Recovery Services |![Sí][green] |![Sí][green] |![Sí][green] |![Sí][green] |
| Almacenamiento en disco | |![Sí][green] |![Sí][green] | |
| Almacenamiento en cinta | |![Sí][green] | | |
| Compresión <br/>(en el almacén de Recovery Services) |![Sí][green] |![Sí][green] |![Sí][green] | |
| Copia de seguridad incremental |![Sí][green] |![Sí][green] |![Sí][green] |![Sí][green] |
| Desduplicación de disco | |![Parcialmente][yellow] |![Parcialmente][yellow] | | |

![clave de tabla](./media/backup-introduction-to-azure-backup/table-key.png)

almacén de servicios de recuperación de Hello es destino de almacenamiento que prefiera hello en todos los componentes. System Center DPM y el servidor de copia de seguridad de Azure también proporcionan Hola opción toohave una copia de disco local. Sin embargo, solo System Center DPM proporciona Hola opción toowrite tooa cinta dispositivo de almacenamiento.

#### <a name="compression"></a>Compresión
Las copias de seguridad se comprimen tooreduce Hola requiere espacio de almacenamiento. Hola único componente que no utilice la compresión es extensión de máquina virtual de Hola. copias de extensión VM de Hello todos los datos de su toohello de cuenta de almacenamiento servicios de recuperación de copia de seguridad del almacén de Hola misma región. Al transferir datos de hello, se usa ninguna compresión. Transferir datos de hello sin compresión ligeramente aumenta el almacenamiento de hello utilizado. Sin embargo, almacenar datos de hello sin compresión permite la restauración más rápida, si necesita ese punto de recuperación.


#### <a name="disk-deduplication"></a>Desduplicación de disco
Puede aprovechar las ventajas de la desduplicación al implementar System Center DPM o Azure Backup Server [en una máquina virtual de Hyper-V](http://blogs.technet.com/b/dpm/archive/2015/01/06/deduplication-of-dpm-storage-reduce-dpm-storage-consumption.aspx). Windows Server realiza la desduplicación de datos (en el nivel de host de Hola) en discos duros virtuales (VHD) que son la máquina virtual de toohello adjunto como almacenamiento de copia de seguridad.

> [!NOTE]
> La desduplicación no está disponible en Azure para ninguno de los componentes de Backup. Cuando System Center DPM y el servidor de copia de seguridad se implementan en Azure, discos de almacenamiento de hello adjuntan toohello que VM no puede ser desduplicada.
>
>

### <a name="incremental-backup-explained"></a>Explicación de una copia de seguridad incremental
Cada componente de copia de seguridad de Azure es compatible con copia de seguridad incremental con independencia de almacenamiento de destino de hello (disco, cinta, el almacén de servicios de recuperación). Copia de seguridad incremental garantiza que las copias de seguridad están almacenados y eficaz, tiempo transfiriendo únicamente los cambios realizados desde la última copia de seguridad de Hola.

#### <a name="comparing-full-differential-and-incremental-backup"></a>Comparación entre copia de seguridad completa, diferencial o incremental

El consumo de almacenamiento, el objetivo de tiempo de recuperación (RTO) y el consumo de red varían según el tipo de método de copia de seguridad. tookeep Hola copia de seguridad costo total de propiedad (TCO) hacia abajo, deberá toounderstand la solución de copia de seguridad recomendada toochoose Hola. Hola después de imagen compara la copia de seguridad completa, copia de seguridad diferencial y copia de seguridad Incremental. En la imagen de hello, origen de datos A se compone de almacenamiento 10 bloquea A1-A10, que se copia de seguridad mensual. Bloques A2, A3, A4 y A9 cambiar Hola primer mes y bloquear los cambios de A5 Hola mes siguiente.

![imagen que muestra las comparaciones de métodos de copia de seguridad](./media/backup-introduction-to-azure-backup/backup-method-comparison.png)

Con **copia de seguridad completa**, cada copia de seguridad contiene el origen de datos completo de Hola. La copia de seguridad completa consume una gran cantidad de ancho de banda de red y almacenamiento, cada vez que se transfiere una copia de seguridad.

**Copia de seguridad diferencial** almacena solo Hola bloquea que cambiaron desde Hola inicial copia de seguridad completa, que da lugar a una menor cantidad de consumo de red y almacenamiento. Las copias de seguridad diferenciales no conservan copias redundantes de los datos sin modificar. Sin embargo, dado que los bloques de datos de Hola que no cambian entre copias de seguridad posteriores se transfieren y almacenan, copias de seguridad diferenciales son ineficaces. Hola segundo mes, los bloques modificados A2, A3, A4 y A9 se copian. Hola tercer mes, estos mismos bloques se copian de nuevo, junto con los bloques cambiados A5. Hola los bloques modificado continuar toobe realizará una copia de seguridad copia de seguridad completa Hola siguiente ocurre.

**Copia de seguridad incremental** logra alta eficacia de almacenamiento y red almacenando únicamente los bloques de datos que ha cambiado desde la copia de seguridad anterior de Hola Hola. Con copia de seguridad incremental, no hay copias de seguridad completas tootake regular. En el ejemplo de Hola, después de hello copia de seguridad completa se realiza para hello primer mes, A2, A3, A4 y A9 se marcan como bloques que han cambiado cambiado y transfieren para hello segundo mes. Hola tercer mes, cambiar solo bloque A5 se marca y se transfieren. Mover menos datos ahorra recursos de almacenamiento y red, lo que reduce el TCO.   

### <a name="security"></a>Seguridad
| Característica | Agente de Azure Backup | System Center DPM | Azure Backup Server | Copia de seguridad de máquina virtual de IaaS de Azure |
| --- | --- | --- | --- | --- |
| Seguridad de las redes<br/> (tooAzure) |![Sí][green] |![Sí][green] |![Sí][green] |![Parcialmente][yellow] |
| Seguridad de los datos<br/> (en Azure) |![Sí][green] |![Sí][green] |![Sí][green] |![Parcialmente][yellow] |

![clave de tabla](./media/backup-introduction-to-azure-backup/table-key.png)

#### <a name="network-security"></a>Seguridad de las redes
Todo el tráfico de copia de seguridad de su toohello de servidores que del almacén de servicios de recuperación se cifra mediante avanzada 256 estándar de cifrado. datos de copia de seguridad de Hola se envían a través de una conexión HTTPS segura. datos de copia de seguridad de Hello también se almacenan en el almacén de servicios de recuperación de hello en formato cifrado. Solo, hello al cliente de Azure, tiene Hola frase de contraseña toounlock estos datos. Microsoft no puede descifrar los datos de copia de seguridad de Hola en cualquier momento.

> [!WARNING]
> Una vez que haya establecido el almacén de servicios de recuperación de hello, solo tiene clave de cifrado de toohello de acceso. Microsoft nunca mantiene una copia de la clave de cifrado y no tiene acceso toohello clave. Si está mal colocado clave hello, Microsoft no puede recuperar datos de copia de seguridad de saludo.
>
>

#### <a name="data-security"></a>Seguridad de los datos
Copia de seguridad de máquinas virtuales de Azure requiere la configuración de cifrado *en* máquina virtual de Hola. Use BitLocker en máquinas virtuales Windows y **dm-crypt** en máquinas virtuales Linux. Azure Backup no cifra automáticamente los datos de copia de seguridad que circulan a través de esta ruta.

### <a name="network"></a>Red
| Característica | Agente de Azure Backup | System Center DPM | Azure Backup Server | Copia de seguridad de máquina virtual de IaaS de Azure |
| --- | --- | --- | --- | --- |
| Compresión de red <br/>(demasiado**servidor de copia de seguridad**) | |![Sí][green] |![yes][green] | |
| Compresión de red <br/>(demasiado**del almacén de servicios de recuperación**) |![Sí][green] |![Sí][green] |![Sí][green] | |
| Protocolo de red <br/>(demasiado**servidor de copia de seguridad**) | |TCP |TCP | |
| Protocolo de red <br/>(demasiado**del almacén de servicios de recuperación**) |HTTPS |HTTPS |HTTPS |HTTPS |

![clave de tabla](./media/backup-introduction-to-azure-backup/table-key-2.png)

Hola extensión de máquina virtual (en Hola IaaS VM) lee Hola datos directamente de hello cuenta de almacenamiento de Azure a través de la red de almacenamiento de hello, por lo que no es necesario toocompress este tráfico.

Si usa un servidor de System Center DPM o el servidor de copia de seguridad de Azure como un servidor de copia de seguridad secundario, comprimir los datos de Hola desde el servidor de reserva toohello Hola servidor principal. Comprimir los datos antes de realizar una copia de seguridad tooDPM o servidor de copia de seguridad de Azure, ahorra ancho de banda.

#### <a name="network-throttling"></a>Limitación de la red
agente de copia de seguridad de Azure de Hello ofrece el límite de red, lo que le permite toocontrol uso de ancho de banda de red durante la transferencia de datos. La limitación puede resultar útil si necesita tooback los datos durante las horas laborables, pero no desea hello toointerfere de proceso de copia de seguridad con otro tráfico de internet. La limitación para datos transferencia tooback se aplique la configuración y restaurar las actividades.

## <a name="backup-and-retention"></a>Copia de seguridad y retención

Azure Backup tiene un límite de 9999 puntos de recuperación, también conocidos como copias de seguridad o instantáneas, por cada *instancia protegida*. Una instancia protegida es un equipo, servidor (físico o virtual) o carga de trabajo configurado tooback seguridad tooAzure de datos. Para obtener más información, vea la sección de hello, [¿qué es una instancia protegida](backup-introduction-to-azure-backup.md#what-is-a-protected-instance). Una instancia está protegida una vez que se ha guardado una copia de seguridad de los datos. Hola copia de seguridad de datos es la protección de Hola. Si los datos de origen de Hola se ha perdido o está dañados, copia de seguridad de hello pudo restaurar datos de origen de saludo. Hello siguiente tabla muestra frecuencia de copia de seguridad máximo de Hola para cada componente. La configuración de directiva de copia de seguridad determina la rapidez consumir puntos de recuperación de Hola. Por ejemplo, si crea un punto de recuperación cada día, puede conservarlos durante 27 años antes de que se agoten. Si tiene un punto de recuperación mensuales, puede conservar los puntos de recuperación 833 años antes de que se agote. Hola servicio de copia de seguridad no establece un límite de tiempo de expiración en un punto de recuperación.

|  | Agente de Azure Backup | System Center DPM | Azure Backup Server | Copia de seguridad de máquina virtual de IaaS de Azure |
| --- | --- | --- | --- | --- |
| Frecuencia de copia de seguridad<br/> (almacén de servicios de tooRecovery) |Tres copias de seguridad por día |Dos copias de seguridad por día |Dos copias de seguridad por día |Una copia de seguridad por día |
| Frecuencia de copia de seguridad<br/> (toodisk) |No aplicable |<li>Cada 15 minutos para SQL Server <li>Cada hora para otras cargas de trabajo |<li>Cada 15 minutos para SQL Server <li>Cada hora para otras cargas de trabajo</p> |No aplicable |
| Opciones de retención |Diariamente, semanalmente, mensualmente y anualmente |Diariamente, semanalmente, mensualmente y anualmente |Diariamente, semanalmente, mensualmente y anualmente |Diariamente, semanalmente, mensualmente y anualmente |
| Número máximo de puntos de recuperación por instancia protegida |9.999|9.999|9.999|9.999|
| Período de retención máximo |Depende de la frecuencia de la copia de seguridad |Depende de la frecuencia de la copia de seguridad |Depende de la frecuencia de la copia de seguridad |Depende de la frecuencia de la copia de seguridad |
| Puntos de recuperación en disco local |No aplicable |<li>64 en el caso de servidores de archivos,<li>448 en el caso de servidores de aplicaciones |<li>64 en el caso de servidores de archivos,<li>448 en el caso de servidores de aplicaciones |No aplicable |
| Puntos de recuperación en cinta |No aplicable |Sin límite |No aplicable |No aplicable |

## <a name="what-is-a-protected-instance"></a>Descripción de una instancia protegida
Una instancia protegida es un equipo de referencia genérica tooa Windows, un servidor (físico o virtual) o la base de datos SQL que se ha configurado tooback seguridad tooAzure. Una instancia está protegida después de configurar una directiva de copia de seguridad para el equipo de hello, servidor o base de datos y crear una copia de seguridad de datos de Hola. Posteriores copias de datos de copia de seguridad de Hola para esa instancia protegida (que se denominan puntos de recuperación), aumente la cantidad de Hola de almacenamiento usado. Puede crear hasta too9999 puntos de recuperación para una instancia protegido. Si elimina un punto de recuperación de almacenamiento, no cuenta con el total de punto de recuperación 9999 Hola.
Algunos ejemplos comunes de instancias protegidas son máquinas virtuales, servidores de aplicaciones, bases de datos y equipos que ejecutan el sistema operativo de Windows hello. Por ejemplo:

* Una máquina virtual que ejecuta el tejido de hipervisor de Hyper-V o IaaS de Azure Hola. Hola sistemas operativos para la máquina virtual de hello puede ser Windows Server o Linux.
* Un servidor de aplicaciones: servidor de aplicaciones de hello puede ser una máquina física o virtual con Windows Server y las cargas de trabajo con datos que es necesario toobe copia de seguridad. Cargas de trabajo comunes son el rol de servidor de archivos de hello en Windows Server, Microsoft Exchange server, Microsoft SharePoint server y Microsoft SQL Server. tooback seguridad estas cargas de trabajo necesita System Center Data Protection Manager (DPM) o el servidor de copia de seguridad de Azure.
* Un PC, una estación de trabajo o un PC portátil que ejecuta el sistema operativo de Windows hello.


## <a name="what-is-a-recovery-services-vault"></a>¿Qué es un almacén de Recovery Services?
Un almacén de servicios de recuperación es que una entidad de almacenamiento en línea en Azure usa datos toohold como copias de seguridad y los puntos de recuperación, las directivas de copia de seguridad. Puede usar datos de copia de seguridad de toohold de almacenes de servicios de recuperación para estaciones de trabajo y servidores de servicios locales y en Azure. Almacenes de servicios de recuperación que sea fácil tooorganize los datos de copia de seguridad, y reduce su sobrecarga de administración. Puede crear tantos almacenes de Recovery Services como desee, dentro de una suscripción.

Almacenes de copia de seguridad, que se basan en el administrador del servicio de Azure, eran la primera versión de Hola de almacén de Hola. Almacenes de servicios de recuperación, que permiten agregar características del modelo de hello Azure Resource Manager, son la segunda versión del almacén de Hola de Hola. Vea hello [artículo de información general de almacén de servicios de recuperación](backup-azure-recovery-services-vault-overview.md) para obtener una descripción completa de las diferencias de características de Hola. Use Hola portal toocreate ya no se puede crear almacenes de copia de seguridad, pero todavía se admiten los almacenes de copia de seguridad.

> [!IMPORTANT]
> Ahora puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad. Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.<br/> **15 de octubre de 2017**, ya no estará almacenes de copia de seguridad de toocreate de toouse capaz de PowerShell. <br/> **El 1 de noviembre de 2017**:
>- Los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.
>- No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola. En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.
>

## <a name="how-does-azure-backup-differ-from-azure-site-recovery"></a>¿Qué diferencias hay entre Azure Backup y Azure Site Recovery?
Azure Backup y Azure Site Recovery tienen en común que ambos servicios realizan una copia de seguridad de los datos y pueden restaurar dichos datos. Sin embargo, estos servicios atienden a finalidades distintas para proporcionar recuperación ante desastres y continuidad empresarial en su organización. Utilice tooprotect de copia de seguridad de Azure y restaurar los datos en un nivel más específico. Por ejemplo, si una presentación en un equipo portátil resultó dañada, usaría presentación de hello toorestore de copia de seguridad de Azure. Si desea que los datos en una máquina virtual y configuración de hello tooreplicate en otro centro de datos, utilice Azure Site Recovery.

Copia de seguridad de Azure protege los datos de forma local y en la nube de Hola. Azure Site Recovery coordina la replicación de la máquina virtual y el servidor físico, la conmutación por error y la conmutación por recuperación. Ambos servicios son importantes porque su solución de recuperación ante desastres debe tookeep los datos recuperables y seguros (Backup) *y* mantener las cargas de trabajo disponibles (Site Recovery) cuando se producen interrupciones.

Hola después conceptos puede ayudarle a tomar decisiones importantes alrededor de copia de seguridad y recuperación ante desastres.

| Concepto | Detalles | Copia de seguridad | Recuperación ante desastres (DR) |
| --- | --- | --- | --- |
| Objetivo de punto de recuperación (RPO) |cantidad de Hello aceptable de pérdida de datos si toobe realiza las necesidades de una recuperación. |Las soluciones de copia de seguridad tienen una gran variabilidad en su RPO aceptable. Las copias de seguridad de máquina virtual normalmente tienen un RPO de un día, mientras que las copias de seguridad de base de datos tienen RPO bajos, de hasta 15 minutos. |Las soluciones de recuperación ante desastres tienen RPO bajos. Hola copia de recuperación ante desastres puede estará por detrás en unos segundos o varios minutos. |
| Objetivo de tiempo de recuperación (RTO) |cantidad de Hola de tiempo que tarda toocomplete una restauración o recuperación. |Debido a Hola RPO mayor, cantidad de Hola de datos que una solución de copia de seguridad necesita tooprocess es normalmente mucho mayor, lo que provoca toolonger RTO. Por ejemplo, puede tardar días toorestore datos de cintas, dependiendo de Hola que tarda cinta de hello tootransport desde una ubicación externa. |Soluciones de recuperación ante desastres tienen menor RTO porque son más sincronizados con el origen de Hola. Menor número de cambios debe toobe procesado. |
| Retención |¿Durante cuánto tiempo necesita datos toobe almacenado |En escenarios que requieren recuperación de operaciones (daños en los datos, eliminación involuntaria de archivos o errores del SO), los datos de copia de seguridad normalmente se conservan durante 30 días o menos.<br>Desde la perspectiva del cumplimiento de normas, los datos que tenga toobe almacenado para meses o incluso años. Los datos de copia de seguridad son perfectos para el archivado en tales casos. |Solo datos de recuperación de las operaciones, que suele tardar unas pocas horas o día de tooa las necesidades de recuperación de desastres. Debido a la captura de datos con precisión de hello usada en soluciones de recuperación ante desastres, no se recomienda el uso de datos de recuperación ante desastres para la retención a largo plazo. |

## <a name="next-steps"></a>Pasos siguientes
Utilice uno de los siguientes tutoriales para obtener instrucciones paso a paso, para proteger los datos en Windows Server, o al proteger una máquina virtual (VM) de Hola en Azure:

* [Realizar copias de seguridad de archivos y carpetas](backup-try-azure-backup-in-10-mins.md)
* [Copia de seguridad de máquinas virtuales de Azure](backup-azure-vms-first-look-arm.md)

Para más información sobre cómo proteger otras cargas de trabajo, pruebe uno de estos artículos:

* [Copia de seguridad de Windows Server](backup-configure-vault.md)
* [Copia de seguridad de cargas de trabajo de aplicaciones](backup-azure-microsoft-azure-backup.md)
* [Copia de seguridad de máquinas virtuales de IaaS de Azure](backup-azure-vms-prepare.md)

[green]: ./media/backup-introduction-to-azure-backup/green.png
[yellow]: ./media/backup-introduction-to-azure-backup/yellow.png
[red]: ./media/backup-introduction-to-azure-backup/red.png
