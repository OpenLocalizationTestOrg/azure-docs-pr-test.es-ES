---
title: "aaaBackup y recuperación ante desastres para los discos de Azure IaaS | Documentos de Microsoft"
description: "En este artículo, explicaremos cómo tooplan copia de seguridad y recuperación ante desastres (DR) de las máquinas virtuales de IaaS (VM) y discos de Azure. En este documento se tratan los discos administrados y no administrados."
services: storage
cloud: Azure
documentationcenter: na
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: luywang
ms.openlocfilehash: 17c697bc411fb47c4b7483b59829af1c40732ac1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-disaster-recovery-for-azure-iaas-disks"></a>Copia de seguridad y recuperación ante desastres para discos IaaS de Azure

En este artículo, explicaremos cómo tooplan copia de seguridad y recuperación ante desastres (DR) de las máquinas virtuales de IaaS (VM) y discos de Azure. En este documento se tratan los discos administrados y los no administrados.

En primer lugar hablaremos sobre Hola errores integrada capacidades de tolerancia en hello plataforma Windows Azure que ayudan a protegerse contra errores locales. A continuación, trataremos los escenarios de desastres de hello completamente cubiertos por las capacidades integradas de hello, que es el tema principal de hello mencionado en este documento. También se muestran varios ejemplos de escenarios de carga de trabajo a los que se pueden aplicar distintas consideraciones sobre copia de seguridad y recuperación ante desastres. Luego se revisan las posibles soluciones para la recuperación ante desastres de discos IaaS. 

## <a name="introduction"></a>Introducción

Hola plataforma Windows Azure usa distintos métodos para obtener redundancia y toohelp de tolerancia a errores proteger a clientes frente a errores de hardware localizados que se pueden producir. Errores locales pueden incluir problemas con un equipo de servidor de almacenamiento de Azure que almacena los errores de un SSD o HDD o parte de los datos de hello para el disco virtual en ese servidor. Tales errores del componente de hardware aislados pueden producirse durante las operaciones normales y plataforma de hello es toobe diseñada toothese resistente errores. Los desastres de gran envergadura pueden producir errores o inaccesibilidad de un gran número de servidores de almacenamiento o de un centro de datos completo. Mientras las máquinas virtuales y discos normalmente están protegidos de errores localizados, pasos adicionales son necesario tooprotect la carga de trabajo de errores catastróficos toda la región (por ejemplo, un desastre importante) que pueden afectar a la máquina virtual y los discos.

Además toohello posibilidad de errores de plataforma, pueden producirse problemas con la aplicación de cliente de Hola o sus datos. Por ejemplo, una nueva versión de la aplicación puede accidentalmente cambiar una separación de datos toohello. En ese caso, puede que desee toorevert aplicación de Hola y Hola datos tooa versión anterior que lo contiene Hola último estado bueno conocido. Para ello, es necesario haber realizado copias de seguridad periódicas.

Recuperación ante desastres regionales, deben realizar backup su región diferente de IaaS VM discos tooa. 

Antes de examinar las opciones de copia de seguridad y recuperación ante desastres, repasemos algunos métodos disponibles para controlar errores localizados.

### <a name="azure-iaas-resiliency"></a>Resistencia de IaaS de Azure

*Resistencia* hace referencia toohello tolerancia a errores normales que se producen en los componentes de hardware. Resistencia es Hola capacidad toorecover de errores y continuar toofunction. No es acerca de cómo evitar los errores, pero responde toofailures de forma que se evita perder el tiempo de inactividad o datos. objetivo de Hola de resistencia es tooreturn hello tooa totalmente operativa estado de la aplicación después de un error. Máquinas virtuales y discos de Azure están diseñadas toobe toocommon resistente los errores de hardware. Echemos un vistazo a la plataforma de IaaS de Azure de hello proporciona esta resistencia.

Una máquina virtual está compuesta principalmente de dos partes: (1) un proceso servidor y discos persistentes (2) Hola. Ambos afectan a la tolerancia a errores Hola de una máquina virtual.

Si el servidor de host de proceso de Azure de Hola que aloja la máquina virtual experimenta un error de hardware (que es poco frecuente), Azure es tooautomatically diseñada restauración Hola VM en otro servidor. Si esto ocurre, experimentarán un reinicio y Hola VM será una copia de seguridad más tarde. Azure detecta automáticamente estos errores de hardware y los ejecuta recuperaciones toohelp garantizan cliente hello VM estará disponible tan pronto como sea posible.

Relacionada con los discos de IaaS, la durabilidad de los datos es fundamental para la plataforma de almacenamiento persistente de Hola. Los clientes de Azure tienen aplicaciones empresariales importantes que se ejecutan en IaaS y dependen de la persistencia de Hola de los datos de Hola. Azure diseña la protección de estos discos IaaS con tres copias redundantes de datos almacenados localmente, lo que ofrece gran durabilidad contra errores locales. Si se produce un error en uno de los componentes de hardware de Hola que contiene el disco, la máquina virtual no se ve afectada porque hay dos copias adicionales toosupport disco solicitudes. Funciona bien incluso si hay errores de dos componentes de hardware diferente que admiten un disco en hello mismo tiempo (lo que sería muy poco frecuente). Asegúrese de toohelp siempre se mantienen tres réplicas, servicio de almacenamiento de Azure Hola genera automáticamente una nueva copia de datos en segundo plano de hello si uno de tres copias de hello deja de estar disponible. Por lo tanto, no debe ser necesario toouse RAID con discos de Azure para tolerancia a errores. RAID 0 simple configuración debería ser suficiente para la creación de bandas discos Hola si es necesario toocreate mayores volúmenes.

Gracias a esta arquitectura, **Azure ha ofrecido de manera constante durabilidad de nivel empresarial para discos IaaS, con una [tasa de error anualizada del 0 %](https://en.wikipedia.org/wiki/Annualized_failure_rate)**.

Errores de hardware localizados en Hola de proceso de host o en almacenamiento de hello plataforma a veces puede producir en indisponibilidad temporal para la máquina virtual que está cubierto por Hola Hola [SLA de Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) para la disponibilidad de la máquina virtual. Azure ofrece también un Acuerdo de Nivel de Servicio líder del sector para instancias únicas de máquina virtual que usan discos de Premium Storage.

cargas de trabajo de aplicación de toosafeguard de tiempo de inactividad debido toohello indisponibilidad temporal de un disco o una máquina virtual, los clientes pueden aprovechar [conjuntos de disponibilidad](../virtual-machines/windows/manage-availability.md). Dos o más máquinas virtuales en un conjunto de disponibilidad proporciona redundancia de la aplicación hello. Azure luego crea estas máquinas virtuales y discos en dominios de error independientes con distintos componentes de alimentación, red y servidor. Por lo tanto, los errores de hardware localizados normalmente no afectan a varias máquinas virtuales en hello establecido en hello mismo tiempo, proporcionar alta disponibilidad de la aplicación. Se considera que una disponibilidad de toouse recomendable establece cuando se necesita una alta disponibilidad. Para obtener más información, consulte aspectos de recuperación ante desastres de hello descritos a continuación.

### <a name="backup-and-disaster-recovery"></a>Copia de seguridad y recuperación ante desastres

Recuperación ante desastres (DR) es Hola capacidad toorecover de incidentes importantes pero poco frecuentes: errores no transitorios y de gran escala, como la interrupción del servicio que afecta a toda una región. La recuperación ante desastres incluye la copia de seguridad y el archivado de datos, y puede incluir la intervención manual, como la restauración manual de una base de datos a partir de la copia de seguridad.

Hello protección integrada de la plataforma de Azure frente a errores localizadas puede no proteger completamente Hola máquinas virtuales/discos en caso de hello de casos de desastres importantes que pueden provocar interrupciones a gran escala. Esto incluye eventos catastróficos tales como que un centro de datos se vea afectado por un huracán, terremoto, incendio o errores de unidades de hardware a gran escala. Además, se pueden producir errores debido a problemas de tooapplication o de datos.

toohelp proteger las cargas de trabajo de IaaS de interrupciones, debe planear para la recuperación de tooenable de redundancia y copias de seguridad. Recuperación ante desastres, debe planear la redundancia y la copia de seguridad en una ubicación geográfica distinta fuera de sitio primario de Hola. Esto ayuda a garantizar la copia de seguridad no se ve afectada por hello mismo evento que originalmente afectados Hola máquinas virtuales o discos. Para más información, vea [Disaster Recovery for Applications built on Azure](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications) (Recuperación ante desastres para aplicaciones generadas en Azure).

Las consideraciones de recuperación ante desastres pueden incluir Hola siguientes aspectos:

1. Alta disponibilidad (HA) es la capacidad de Hola de hello aplicación toocontinue ejecutando en un estado correcto, sin tiempo de inactividad considerable. Por "estado correcto," se entiende la aplicación hello tiene capacidad de respuesta, y los usuarios pueden conectar toohello aplicación e interactuar con él. Ciertas aplicaciones de misión crítica y las bases de datos pueden ser necesario toobe disponible siempre, incluso si existen errores en la plataforma de Hola. Estas cargas de trabajo, puede que necesite tooplan redundancia para la aplicación hello, así como datos de Hola.

2. Durabilidad de los datos: En algunos casos, consideración principal hello es garantizar que se conservan los datos de hello en caso de hello de un desastre. Por consiguiente, puede que tenga que realizar una copia de seguridad de los datos en otro sitio. Estas cargas de trabajo, no es necesario una redundancia completa para la aplicación hello, pero una copia de seguridad periódica de los discos de Hola.

## <a name="backup-and-dr-scenarios"></a>Escenarios de copia de seguridad y recuperación ante desastres

Veamos algunos ejemplos típicos de los escenarios de carga de trabajo de aplicaciones y consideraciones de Hola para planear la recuperación ante desastres.

### <a name="scenario-1-major-database-solutions"></a>Escenario 1: Soluciones de bases de datos principales

Considere la posibilidad de usar un servidor de base de datos de producción, como SQL Server u Oracle, que pueda admitir alta disponibilidad. Los usuarios y las aplicaciones de producción críticas dependen de esta base de datos. plan de recuperación ante desastres de Hola para este sistema necesite hello toosupport según los requisitos:

1. Los datos deben estar protegidos y ser recuperables.
2.  El servidor debe estar disponible para su uso.

Esto puede requerir el mantenimiento de una réplica de base de datos de hello en una región distinta como una copia de seguridad. Dependiendo de los requisitos de Hola para disponibilidad del servidor y la recuperación de datos, solución de hello puede abarcar desde un activo / activo o activo / pasivo réplica sitio tooperiodic sin conexión las copias de seguridad de datos de Hola. Las bases de datos relacionales, como SQL Server y Oracle, ofrecen varias opciones de replicación. Con SQL Server, se pueden usar [grupos de disponibilidad Always On de SQL Server](https://msdn.microsoft.com/library/hh510230.aspx) para alta disponibilidad.

Las bases de datos NoSQL, como MongoDB, también admiten [réplicas](https://docs.mongodb.com/manual/replication/) para conseguir redundancia. se pueden utilizar réplicas de Hola para lograr alta disponibilidad.

### <a name="scenario-2-a-cluster-of-redundant-vms"></a>Escenario 2: Un clúster de máquinas virtuales redundantes

Considere la posibilidad de una carga de trabajo controlada por un clúster de máquinas virtuales que proporcionan redundancia y equilibrio de carga. Un ejemplo sería un clúster Cassandra implementado en una región. Este tipo de arquitectura ya proporciona un alto nivel de redundancia en esa región. Sin embargo, carga de trabajo de hello tooprotect tras un error de nivel regional, debería considerar propagándose clúster hello en dos regiones o realizar región tooanother de copias de seguridad periódicas.

### <a name="scenario-3-iaas-application-workload"></a>Escenario 3: Carga de trabajo de la aplicación IaaS

Podría tratarse de una carga de trabajo de producción típica que se ejecuta en una máquina virtual de Azure. Por ejemplo, podría ser un servidor web o servidor de archivos que contiene el contenido de Hola y otros recursos de un sitio. También podría ser una aplicación de negocio personalizadas ejecutando en una máquina virtual que almacena sus datos, los recursos y estado de la aplicación en discos de máquina virtual de Hola. En este caso, es importante toomake seguro que realizar copias de seguridad de forma regular. Frecuencia de copia de seguridad debe basarse en la naturaleza de Hola de carga de trabajo de máquina virtual de Hola. Por ejemplo, si la aplicación hello ejecuta cada día y modifica los datos, a continuación, Hola realizó copia de seguridad debe ser cada hora.

Otro ejemplo es un servidor de informes que extrae datos de otros orígenes y genera informes agregados. Pérdida de esta máquina virtual o discos dará lugar a pérdida de toohello de informes de Hola. Sin embargo, es posible hello toorerun posible informar de proceso y la salida de hello regenerar. En ese caso, realmente no tiene una pérdida de datos, incluso si el servidor de informes de Hola se visita con un desastre, por lo que podría tener un nivel más alto de tolerancia de pérdida de parte de los datos de hello en hello servidor de informes. En ese caso, las copias de seguridad menos frecuentes es un costo de opción tooreduce Hola.

### <a name="scenario-4-iaas-application-data-issues"></a>Escenario 4: Problemas de datos de la aplicación IaaS

Tiene una aplicación que calcula, mantiene y sirve de datos comerciales críticos, como información sobre los precios. Una nueva versión de la aplicación tenía un error de software que incorrectamente calcula el precio de Hola y Hola existente comercio datos atendidos por plataforma de hello erróneos. En este caso, sería Hola hacer a continuación a toorevert toohello versión anterior de la aplicación hello y datos de hello primero. tooenable, realice copias de seguridad periódicas del sistema.

## <a name="disaster-recovery-solution-azure-backup-service"></a>Solución de recuperación ante desastres: servicio Azure Backup

El [servicio Azure Backup](https://azure.microsoft.com/services/backup/) puede usarse para copia de seguridad y recuperación ante desastres y funciona tanto con [Managed Disks](storage-managed-disks-overview.md) como con [discos no administrados](storage-about-disks-and-vhds-windows.md#unmanaged-disks). Puede crear un trabajo de copia de seguridad con copias de seguridad basadas en tiempo, fácil restauración de la máquina virtual y directivas de retención de copia de seguridad. 

Si usa [discos de almacenamiento Premium](storage-premium-storage.md), [discos administrados](storage-managed-disks-overview.md), u otros tipos de disco con hello [almacenamiento localmente redundante (LRS)](storage-redundancy.md#locally-redundant-storage) opción, es especialmente importante tooleverage copias de seguridad periódicas de recuperación ante desastres. Copia de seguridad de Azure almacena los datos de hello en el almacén de servicios de recuperación para la retención a largo plazo. Elija hello [almacenamiento con redundancia geográfica (GRS)](storage-redundancy.md#geo-redundant-storage) opción de almacén de servicios de recuperación de copia de seguridad de Hola. Eso garantizará que las copias de seguridad son replicados tooa una región distinta de Azure para proteger contra desastres regionales.

Para [discos no administrado](storage-about-disks-and-vhds-windows.md#unmanaged-disks), puede usar tipo de almacenamiento LRS Hola para discos de IaaS, pero asegúrese de que está habilitada la copia de seguridad de Azure con hello opción GRS de hello almacén de servicios de recuperación.

**Si usas hello [GRS](storage-redundancy.md#geo-redundant-storage)/[RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage) opción para los discos no administrado, sigue siendo necesario instantáneas coherentes con la copia de seguridad y recuperación ante desastres.** Se debe usar el [servicio Azure Backup ](https://azure.microsoft.com/services/backup/) o [instantáneas coherentes](#alternative-solution-consistent-snapshots).

Hola aquí te mostramos un resumen de las soluciones de recuperación ante desastres.

| Escenario | Replicación automática | Solución de recuperación ante desastres |
| --- | --- | --- |
| *Discos de Premium Storage* | Local ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Copia de seguridad de Azure](https://azure.microsoft.com/services/backup/) |
| *Managed Disks* | Local ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Copia de seguridad de Azure](https://azure.microsoft.com/services/backup/) |
| *Discos LRS no administrados* | Local ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Copia de seguridad de Azure](https://azure.microsoft.com/services/backup/) |
| *Discos GRS no administrados* | Entre regiones ([GRS](storage-redundancy.md#geo-redundant-storage)) | [Copia de seguridad de Azure](https://azure.microsoft.com/services/backup/)<br/>[Instantáneas coherentes](#alternative-solution-consistent-snapshots) |
| *Discos RA-GRS no administrados* | Entre regiones ([RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage)) | [Copia de seguridad de Azure](https://azure.microsoft.com/services/backup/)<br/>[Instantáneas coherentes](#alternative-solution-consistent-snapshots) |

Alta disponibilidad por puede satisfacen mejor mediante el uso de Hola de discos administrado en un conjunto de disponibilidad junto con la copia de seguridad de Azure. Si usa discos no administrados, todavía puede usar Azure Backup con recuperación ante desastres. Si es que no se puede toouse copia de seguridad de Azure, a continuación, tomar [las instantáneas coherentes con](#alternative-solution-consistent-snapshots) tal y como se describe en una sección posterior es una solución alternativa para la copia de seguridad y recuperación ante desastres.

Las opciones de alta disponibilidad, copia de seguridad y recuperación ante desastres en los niveles de aplicación o de infraestructura se pueden representar como sigue:

| *Level* | Alta disponibilidad   | Copia de seguridad y recuperación ante desastres |
| --- | --- | --- |
| *Aplicación* | Always On de SQL | Copia de seguridad de Azure |
| *Infraestructura*  | Conjunto de disponibilidad  | GRS con instantáneas coherentes |

### <a name="using-hello-azure-backup-service"></a>Uso de hello servicio de copia de seguridad de Azure

[Copia de seguridad de Azure](../backup/backup-azure-vms-introduction.md) hacer una copia de las máquinas virtuales que ejecutan Windows o Linux toohello almacén de servicios de recuperación de Azure. Copias de seguridad y restaurar los datos críticos para la empresa se ve complicado por hecho de Hola que deben hacer copia los datos empresariales críticos mientras las aplicaciones de Hola que generan Hola ejecutan datos. tooaddress, copia de seguridad de Azure proporciona copias de seguridad coherentes con la aplicación para las cargas de trabajo de Microsoft mediante hello tooensure de servicio de instantáneas de volumen (VSS) que se escriben correctamente datos toostorage. Para máquinas virtuales de Linux, solo las copias de seguridad coherentes para el archivo son posibles, como Linux no tiene funcionalidad equivalente tooVSS.

![][1]

Si copia de seguridad de Azure inicia un trabajo de copia de seguridad en tiempo de hello programado, desencadena extensión de copia de seguridad de hello instalada en hello VM tootake una instantánea en un momento. Se toma una instantánea en coordinación con VSS tooget una instantánea coherente de los discos de hello en la máquina virtual de hello sin necesidad de tooshut lo hacia abajo. extensión de copia de seguridad de Hola Hola VM vacía todas las escrituras antes de realizar instantáneas coherentes de Hola de todos los discos de Hola. Después de tomar instantáneas de hello, datos de Hola se transfieren por el almacén de copia de seguridad de toohello de copia de seguridad de Azure. toomake Hola copia de seguridad proceso más eficaz, servicio de hello identifica y transfiere únicamente los bloques de datos que han cambiado desde la última copia de seguridad de Hola Hola.


toorestore, puede ver copias de seguridad disponibles de Hola a través de la copia de seguridad de Azure y, a continuación, iniciar una restauración. Puede crear y restaurar copias de seguridad de Azure a través de hello [portal de Azure](https://portal.azure.com/), [con PowerShell](../backup/backup-azure-vms-automation.md ), o mediante hello [CLI de Azure](https://docs.microsoft.com/azure/xplat-cli-install). Para más información, vea Azure Backup.

### <a name="steps-tooenable-backup"></a>Pasos tooEnable copia de seguridad

Hello es seguir estos pasos tooenable normalmente se usan las copias de seguridad de las máquinas virtuales con hello [Portal de Azure](https://portal.azure.com/). Habrá algunas variaciones según el escenario exacto. Consulte toohello [copia de seguridad de Azure](../backup/backup-azure-vms-introduction.md) documentación para obtener detalles completos. Azure Backup también [admite máquinas virtuales con Managed Disks](https://azure.microsoft.com/blog/azure-managed-disk-backup/).

1.  Crear un almacén de servicios de recuperación para una máquina virtual mediante Hola pasos:

    a.  Con hello [portal de Azure](https://portal.azure.com/), examinar todos los recursos y busque "Almacenes de servicios de recuperación".

    b.  En hello servicios de recuperación de almacenes de credenciales de menú, haga clic en Agregar y siga los pasos de hello toocreate un nuevo almacén en hello misma región que Hola máquina virtual. Por ejemplo, si la máquina virtual está en la región del oeste de Estados Unidos, seleccionar West US para el almacén de Hola.

2.  Comprobar la replicación de almacenamiento de Hola para hello recién creado el almacén. toodo este, almacén de Hola de acceso de hello servicios de recuperación almacenes hoja y vaya toohello configuración de copia de seguridad o configuración. Asegúrese de hello opción GRS está activada de forma predeterminada. Esto garantizará que el almacén es automáticamente replicada tooa centro de datos secundario. Por ejemplo, el almacén de la zona horaria del Pacífico occidental será automáticamente replicada tooEast Estados Unidos.

3.  Configurar la directiva de copia de seguridad de Hola y seleccione Hola VM de hello misma interfaz de usuario.

4.  Asegúrese de hello seguro que Backup Agent está instalado en hello máquina virtual. Si la máquina virtual se creó mediante una imagen de la Galería de Azure, agente de copia de seguridad de hello ya está instalado. En caso contrario (es decir, si está utilizando una imagen personalizada), use instrucciones demasiado[Hola instalar agente de máquina virtual en la máquina virtual de hello](../backup/backup-azure-arm-vms-prepare.md#install-the-vm-agent-on-the-virtual-machine).

5.  Asegúrese de que ese Hola VM permite conectividad de red para hello toofunction de servicio de copia de seguridad. Siga estas instrucciones para la [conectividad de red](../backup/backup-azure-arm-vms-prepare.md#network-connectivity).

6.  Cuando haya realizado Hola por encima de los pasos, copia de seguridad de Hola se ejecutará a intervalos regulares según se especifica en la directiva de copia de seguridad de Hola. Si es necesario, puede desencadenar la primera copia de seguridad Hola manualmente desde el panel de almacén de hello en hello portal de Azure.

Para la automatización de Azure Backup mediante secuencias de comandos, consulte demasiado[cmdlets de PowerShell para copia de seguridad de máquina virtual](../backup/backup-azure-vms-automation.md).

### <a name="steps-for-recovery"></a>Pasos para la recuperación

Si necesita toorepair o volver a generar una máquina virtual, puede restaurar Hola VM desde cualquiera de los puntos de recuperación de copia de seguridad de hello en el almacén de Hola. Hay un par de opciones diferentes para realizar la recuperación de hello:

1.  Puede crear otra máquina virtual como una representación de un momento dado de la máquina virtual de copia de seguridad.

2.  Puede restaurar Hola discos y, a continuación, usar plantilla Hola para toocustomize VM de Hola y Hola de regeneración restaura máquinas virtuales. 

Consulte las instrucciones demasiado[máquinas virtuales de Azure de uso toorestore portal](../backup/backup-azure-arm-restore-vms.md#restoring-a-vm-during-azure-datacenter-disaster). documento de Hello también explica pasos específicos de Hola para restaurar una copia de seguridad las máquinas virtuales toohello emparejados data center usando el almacén de copia de seguridad con redundancia geográfica en caso de hello de un desastre en el centro de datos principal de Hola. En ese caso, copia de seguridad de Azure usa el servicio de proceso de saludo de la máquina virtual de hello región secundaria toocreate Hola restaurado.

También puede usar PowerShell para [restaurar una máquina virtual](../backup/backup-azure-vms-automation.md#restore-an-azure-vm) o para [crear una máquina virtual a partir de discos restaurados](../backup/backup-azure-vms-automation.md#create-a-vm-from-restored-disks).

## <a name="alternative-solution-consistent-snapshots"></a>Solución alternativa: Instantáneas coherentes con la

Si es que no se puede toouse Hola servicio de copia de seguridad de Azure, puede implementar su propio mecanismo de copia de seguridad con las instantáneas. Es complicado toocreate las instantáneas coherentes para todos los discos usados por una máquina virtual y, a continuación, replicar esos región tooanother de instantáneas. Por esta razón, Azure considera Hola aprovecha el servicio de copia de seguridad de una opción mejor que la compilación de una solución personalizada. Si utiliza almacenamiento de RA, GRS y RA-GRS para los discos, las instantáneas son automáticamente replicada tooa centro de datos secundario. Si utiliza almacenamiento LRS para los discos, se necesita datos de hello tooreplicate. Para más información, vea [Copias de seguridad de discos de máquinas virtuales de Azure no administrados con instantáneas incrementales](storage-incremental-snapshots.md).

Una instantánea es una representación de un objeto en un momento dado. Le cobrará una instantánea de facturación para el tamaño de incremental de Hola de hello datos contiene. Para más información, vea [Creación de una instantánea de un blob](storage-blob-snapshots.md).

### <a name="creating-snapshots-while-hello-vm-is-running"></a>La creación de instantáneas al Hola VM está ejecutando

Mientras que puede tomar una instantánea en cualquier momento, si hello máquina virtual se está ejecutando, todavía hay datos que se transmite toohello discos y las instantáneas de hello pueden contener operaciones parciales que estaban en tránsito. Además, si hay varios discos, las instantáneas de Hola de discos diferentes pueden haberse producido en momentos diferentes, lo que significa que no pueden ser coordinadas estas instantáneas. Esto es especialmente problemático para los volúmenes seccionados cuyos archivos pueden resultar dañados si se realizan cambios durante la copia de seguridad.

tooavoid esta situación, el proceso de copia de seguridad de hello debe implementar Hola siguiendo los pasos:

1.  Inmovilizar todos los discos de Hola

2.  Vaciar Hola todas las escrituras pendientes

3.  A continuación, [crear una instantánea de blob](storage-blob-snapshots.md) para todos los discos de Hola

Algunas aplicaciones de Windows como SQL Server proporcionan un mecanismo de copia de seguridad coordinado a través de copias de seguridad VSS toocreate coherentes con la aplicación. En Linux, puede usar una herramienta como fsfreeze para coordinar los discos de hello, que le proporcionará las copias de seguridad coherentes para el archivo, pero las instantáneas no coherentes con la aplicación. Este proceso es complicado, por lo que debe plantarse el uso de [Azure Backup](../backup/backup-azure-vms-introduction.md) o una solución de copia de seguridad de terceros que ya lo implementan.

Hola anteriormente proceso dará como resultado de una colección de instantáneas coordinadas de todos los discos de máquina virtual de hello, que representa una vista en un momento específica de hello VM. Se trata de un punto de restauración de copia de seguridad Hola máquina virtual. Puede repetir el proceso de hello en copias de seguridad periódicas de los intervalos programados toocreate. Vea a continuación para conocer los pasos hello[región de tooanother de las copias de seguridad de copia hello](#copy-the-snapshots-to-another-region) para recuperación ante desastres.

### <a name="creating-snapshots-while-hello-vm-is-offline"></a>La creación de instantáneas al Hola VM está sin conexión

Otra opción toocreate copias de seguridad coherentes se está cerrando hello VM y blob de tomar instantáneas de cada disco. Esto resulta más sencillo que coordinar instantáneas de una máquina virtual en ejecución, pero requiere algunos minutos de inactividad. Para este proceso, siga estos pasos:

1. Apagar VM Hola.

2. Cree una instantánea de cada blob de VHD, que solo tarda unos segundos.

    toocreate una instantánea, puede usar [PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blob-snapshots), hello [API de Rest de almacenamiento de Azure](https://msdn.microsoft.com/library/azure/ee691971.aspx), [CLI de Azure](https://docs.microsoft.com/azure/xplat-cli-install), o una de las bibliotecas de cliente de almacenamiento de Azure de hello como [ biblioteca de cliente de almacenamiento de Hola para .NET](https://msdn.microsoft.com/library/azure/hh488361.aspx).

3. Iniciar máquina virtual, que finaliza el tiempo de inactividad de Hola Hola. Por lo general todo proceso de Hola se completa dentro de unos minutos.

Este proceso produce una colección de las instantáneas coherentes para todos los discos de hello, que proporciona un punto de restauración de copia de seguridad para hello VM. Vea a continuación para región de hello pasos toocopy Hola instantáneas tooanother para recuperación ante desastres.

### <a name="copy-hello-snapshots-tooanother-region"></a>Copia Hola instantáneas tooanother región

Creación de instantáneas de Hola por sí sola puede no ser suficiente para la recuperación ante desastres. También debe replicar la región de tooanother de las copias de seguridad de instantánea de Hola.

Si usas GRS o RA-GRS para los discos, las instantáneas de hello son región secundaria toohello replicada automáticamente. Puede haber unos minutos de retardo antes de la réplica de hello y, si el centro de datos principal de hello deja de funcionar antes de concluir la replicación de instantáneas de hello, no será capaz de tooaccess instantáneas de Hola desde el centro de datos secundaria de Hola. probabilidad de Hola de esto es pequeña.

> [!Note] 
> Solo tiene discos de hello en una cuenta GRS o RA-GRS no protege Hola VM de desastres. También debe crear instantáneas coordinadas o usar Azure Backup. Se trata de toorecover requiere un estado coherente de tooa de máquina virtual.

Si usas LRS, debe copiar la cuenta de almacenamiento distinta de hello instantáneas tooa inmediatamente después de crear una instantánea de Hola. destino de la copia de Hello podría ser una cuenta de almacenamiento LRS en una región distinta, lo que copia Hola está en una región remota. También puede copiar la cuenta de almacenamiento de hello instantánea tooan RA-GRS Hola misma región. En este caso, instantánea Hola será región secundaria de forma diferida replicada toohello remoto. La copia de seguridad está protegido ante desastres en el sitio primario de hello una vez completada copiar hello y la replicación.

toocopy sus instantáneas incrementales para recuperación ante desastres de manera eficaz, revisión las instrucciones de Hola de [copia de seguridad Azure discos de máquina virtual no administrados con instantáneas incrementales](storage-incremental-snapshots.md).

![][2]

### <a name="recovery-from-snapshots"></a>Recuperación de instantáneas

tooretrieve una instantánea, cópielo toomake un nuevo blob. Si va a copiar instantáneas Hola de cuenta principal de hello, puede copiar Hola instantánea sobre toohello base blob de instantánea de hello, por lo tanto reversión Hola disco toohello instantánea; Esto se conoce como promoción de instantánea de Hola. Si va a copiar la copia de seguridad de instantánea de Hola desde una cuenta secundaria (en caso de hello de RA-GRS), debe copiar tooa de cuenta principal. Puede copiar una instantánea [con PowerShell](storage-powershell-guide-full.md#how-to-copy-a-snapshot-of-a-blob) o mediante la utilidad de AzCopy Hola. Para obtener más información, consulte [transferir datos con la utilidad de línea de comandos de AzCopy hello](storage-use-azcopy.md).

En caso de hello de máquinas virtuales con varios discos, debe copiar todas las instantáneas de Hola que forman parte de hello coordinado por el mismo punto de restauración. Cuando copia blobs de disco duro virtual de hello instantáneas toowritable, puede usar Hola blobs toorecreate la máquina virtual con la plantilla de Hola para hello máquina virtual.

## <a name="other-options"></a>Otras opciones

### <a name="sql-server"></a>SQL Server

SQL Server en una máquina virtual tiene su propio toobackup capacidades integradas su tooAzure de base de datos de SQL Server almacenamiento de blobs o un recurso compartido de archivos. Si la cuenta de almacenamiento de hello es GRS o RA-GRS, puede tener acceso a las copias de seguridad en el centro de datos secundario de la cuenta de almacenamiento de hello en caso de hello de un desastre, con hello las mismas restricciones según lo descrito anteriormente. Para más información, consulte [Copias de seguridad y restauración para SQL Server en máquinas virtuales de Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-backup-recovery.md). Toobackup de adición y la restauración, [SQL Server grupos de disponibilidad AlwaysOn](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md) pueden mantener las réplicas secundarias de las bases de datos toogreatly reducen el tiempo de recuperación ante desastres de Hola.

## <a name="other-considerations"></a>Otras consideraciones

Este artículo ha explicado cómo toobackup o tome instantáneas de las máquinas virtuales y su recuperación ante desastres de toosupport de discos y cómo toouse esos toorecover. Con el modelo de Azure Resource Manager hello, muchas personas usan plantillas toocreate sus máquinas virtuales y otras infraestructuras en Azure. Puede usar un toocreate plantilla una máquina virtual que tiene Hola misma configuración cada vez. Si utiliza imágenes personalizadas para crear las máquinas virtuales, también debe asegurarse las imágenes están protegidas mediante un toostore de cuenta de RA-GRS ellos.

Por lo tanto, el proceso de copia de seguridad puede ser una combinación de estas dos acciones:

1. Datos de copia de seguridad hello (discos)
2. Configuración de copia de seguridad hello (plantillas, imágenes personalizadas)

Dependiendo de la opción de copia de seguridad de Hola que elija, puede tener copias de seguridad de toohandle Hola de datos de Hola y la configuración de Hola o servicio de copia de seguridad de hello puede controlan todo esto por usted.

## <a name="appendix---understanding-hello-impact-of-lrs-grs-and-ra-grs"></a>Apéndice: comprender el impacto de Hola de LRS, GRS y RA-GRS

En el caso de las cuentas de almacenamiento de Azure, hay tres tipos de redundancia de datos que se debe considerar con respecto a la recuperación ante desastres: localmente redundante (LRS), con redundancia geográfica (GRS) o con redundancia geográfica y acceso de lectura (RA-GRS). 

Localmente almacenamiento redundante (LRS) mantiene tres copias de datos de Hola Hola mismo centro de datos. Al escribir datos de hello, se actualizan todas las copias de tres antes de que se realizará correctamente toohello autor de la llamada, por lo que son idénticos. El disco está protegido contra errores locales, ya que es muy poco probable que se vean afectadas todas las copias de tres en hello mismo tiempo. En caso de hello de LRS, no hay ninguna redundancia geográfica, por lo que el disco de hello no está protegida contra errores catastróficos que pueden afectar a una unidad de almacenamiento o centro de datos completo.

Con GRS y RA-GRS, tres copias de los datos se conservan en la región principal de hello (seleccionada por el usuario) y, más de tres copias de los datos se conservan en una región secundaria correspondiente (establecida de Azure). Por ejemplo, si almacena datos de zona horaria del Pacífico occidental, datos de hello será replicada tooEast Estados Unidos. Esto se hace de forma asincrónica y no hay un pequeño retraso entre actualizaciones toohello principal y secundaria. Réplicas de discos de hello en el sitio secundario de hello son coherentes en una base por disco (con un retardo de hello), pero las réplicas de varios discos activas pueden no estar sincronizadas **entre sí**. se necesitan toohave réplicas coherente en varios discos, las instantáneas coherentes.

Hola principal diferencia entre GRS y RA-GRS es que con RA-GRS, puede leer copia secundaria de Hola en cualquier momento. Si hay un problema que representa los datos de hello en la región principal de hello inaccesible, Hola, equipo de Azure hará que cada acceso toorestore de esfuerzo. Mientras Hola principal está inactivo, si tienen RA-GRS habilitada, puede tener acceso a datos de hello en el centro de datos secundaria de Hola. Por lo tanto, si tiene previsto tooread de réplica de hello mientras Hola principal es inaccesible, deben considerarse RA-GRS.

Si resulta toobe una interrupción importante, Hola, equipo de Azure puede desencadenar una conmutación geográfica y cambiar Hola principal DNS entradas toopoint toosecondary almacenamiento. En este momento, si tiene cualquier GRS o RA-GRS habilitada, puede tener acceso a datos de hello en región de Hola que usa toobe Hola secundaria. En otras palabras, si la cuenta de almacenamiento es GRS y hay un problema, puede tener acceso a almacenamiento secundario Hola solo si se produce una conmutación geográfica.

Para obtener más información, consulte [qué toodo si se produce una interrupción de almacenamiento de Azure](storage-disaster-recovery-guidance.md). 

Tenga en cuenta que Microsoft controla si se produce una conmutación por error. La conmutación por error no se controla por cuenta de almacenamiento, por lo tanto no son los clientes individuales quienes deciden su uso. tooimplement recuperación ante desastres para las cuentas de almacenamiento específico o discos de máquina virtual, debe usar técnicas de Hola que se ha descrito anteriormente en este artículo.



[1]: ./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-1.png
[2]: ./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-2.png