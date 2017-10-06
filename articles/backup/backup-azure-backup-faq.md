---
title: "Preguntas más frecuentes de copia de seguridad aaaAzure | Documentos de Microsoft"
description: "Responde a las preguntas de toocommon sobre: incluidos los servicios de recuperación almacenes, lo que puede realizar una copia, cómo funciona, cifrado y límites de características de copia de seguridad de Azure. "
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "copia de seguridad y recuperación ante desastres; servicio de copia de seguridad"
ms.assetid: 1011bdd6-7a64-434f-abd7-2783436668d7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/21/2017
ms.author: markgal;arunak;trinadhk;
ms.openlocfilehash: 3338f7620bcc6ebf53c9c161191f2d8bca1a29da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-service"></a>Preguntas sobre Hola servicio de copia de seguridad de Azure
Este artículo tiene respuestas toocommon preguntas toohelp rápidamente entender los componentes de copia de seguridad de Azure Hola. En algunas de las respuestas de hello, hay artículos de toohello vínculos que tienen información completa. Puede hacer preguntas sobre copias de seguridad de Azure, haga clic en **comentarios** (toohello derecha). Los comentarios aparecen en la parte inferior de Hola de este artículo. Una cuenta de Livefyre es toocomment necesario. También puede publicar preguntas sobre Hola servicio de copia de seguridad de Azure en hello [foro de discusión](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

secciones de hello tooquickly examen en este artículo, use derecha de toohello de vínculos de hello, en **en este artículo**.


## <a name="recovery-services-vault"></a>Almacén de Recovery Services

### <a name="is-there-any-limit-on-hello-number-of-vaults-that-can-be-created-in-each-azure-subscription-br"></a>¿Hay ningún límite del número de Hola de almacenes de credenciales que se pueden crear en cada suscripción de Azure? <br/>
Sí. A partir de septiembre de 2016, puede crear 25 almacenes de Recovery Services o de copia de seguridad por suscripción. Puede crear los servicios de recuperación de too25 almacenes, por región compatible de copia de seguridad de Azure por suscripción. Si necesita más almacenes, cree otra suscripción.

### <a name="are-there-limits-on-hello-number-of-serversmachines-that-can-be-registered-against-each-vault-br"></a>¿Hay límites en el número de Hola de servidores o equipos que se pueden registrar en cada almacén? <br/>
Sí, puede registrar las máquinas de too50 por almacén. Para las máquinas virtuales de IaaS de Azure, límite de hello es de 200 máquinas virtuales por almacén. Si necesita tooregister más máquinas, cree otro almacén.

### <a name="if-my-organization-has-one-vault-how-can-i-isolate-one-servers-data-from-another-server-when-restoring-databr"></a>Si la organización tiene un almacén, ¿cómo se pueden aislar los datos de un servidor desde otro servidor al restaurar los datos?<br/>
Hola a todos los servidores que están registrado toohello puede recuperar el mismo almacén de datos respaldados por otros servidores *que utilizan Hola misma frase de contraseña*. Si tiene servidores cuyos datos de copia de seguridad que desee tooisolate desde otros servidores de su organización, use una frase de contraseña designado para esos servidores. Por ejemplo, los servidores de recursos humanos podrían usar una frase de contraseña de cifrado, los servidores de contabilidad, otra y los servidores de almacenamiento, otra distinta.

### <a name="can-i-migrate-my-backup-data-or-vault-between-subscriptions-br"></a>¿Puedo "migrar" mi almacén o datos de copia de seguridad de una suscripción a otra? <br/>
No. almacén de Hola se crea en un nivel de suscripción y no puede ser tooanother reasignarse suscripción una vez que se crea.

### <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Los almacenes de Recovery Services se basan en Resource Manager. ¿Se admiten aún los almacenes de Backup (modo clásico)? <br/>
Todos los almacenes de copia de seguridad existentes en hello [portal clásico](https://manage.windowsazure.com) continuar toobe compatible. Sin embargo, no podrá usar almacenes de copia de seguridad nueva de hello toodeploy portal clásico. Microsoft recomienda el uso de almacenes de servicios de recuperación para todas las implementaciones porque futuras mejoras tooRecovery los almacenes de servicios, solo aplican. Si intentas toocreate un almacén de copia de seguridad en el portal clásico de hello, será redirigido toohello [portal de Azure](https://portal.azure.com).

### <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>¿Puedo migrar un almacén de servicios de recuperación de tooa de almacén de copia de seguridad? <br/>
Lamentablemente no, no se pueden migrar contenido de Hola de un tooa de almacén de copia de seguridad que del almacén de servicios de recuperación. Estamos trabajando para agregar esta funcionalidad, pero no está disponible actualmente.

### <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>He realizado copias de seguridad de mis máquinas virtuales clásicas en un almacén de Backup. ¿Puedo migrar Mis máquinas virtuales de modo de administrador de tooResource de modo clásico y protegerlos en un almacén de servicios de recuperación?
Clásicos puntos de recuperación de máquina virtual en un almacén de copia de seguridad no migran automáticamente tooa el almacén de servicios de recuperación cuando se mueve Hola VM de clásico tooResource modo de administrador. Siga estos pasos tootransfer las copias de seguridad de máquina virtual:

1. En el almacén de copia de seguridad de hello, vaya toohello **elementos protegidos** pestaña y seleccione Hola máquina virtual. Haga clic en [Detener protección](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Deje la opción *Eliminar los datos de copia de seguridad asociados***desactivada**.
2. Eliminar la extensión de copia de seguridad o instantánea de Hola de hello máquina virtual.
3. Migrar máquina virtual de Hola de modo de administrador de tooResource de modo clásico. Asegúrese de migrar la información de red y almacenamiento de hello, máquina virtual de toohello correspondiente también es tooResource el modo de administrador.
4. Crear un almacén de servicios de recuperación y configurar copia de seguridad en hello migrar máquina virtual usando **copia de seguridad** acción sobre el panel almacén. Para obtener información detallada sobre la copia de seguridad de los servicios de recuperación de tooa de una máquina virtual del almacén, consulte el artículo de hello, [proteger máquinas virtuales de Azure con un almacén de servicios de recuperación](backup-azure-vms-first-look-arm.md).

## <a name="azure-backup-agent"></a>Agente de Azure Backup
Se puede encontrar una lista detallada de preguntas en las [P+F sobre la copia de seguridad de archivos y carpetas de Azure](backup-azure-file-folder-backup-faq.md).

## <a name="azure-vm-backup"></a>Copia de seguridad de máquina virtual de Azure
Se puede encontrar una lista detallada de preguntas en las [P+F sobre la copia de seguridad de máquinas virtuales de Azure](backup-azure-vm-backup-faq.md).

## <a name="back-up-vmware-servers"></a>Copias de seguridad de servidores VMware

### <a name="can-i-back-up-vmware-vcenter-servers-tooazure"></a>¿Puedo hacer copias de seguridad tooAzure de servidores de VMware vCenter?

Sí. Puede usar el servidor de copia de seguridad de Azure tooback VMware vCenter y ESXi tooAzure. Para obtener información sobre la versión de Hola admite VMware, consulte el artículo de hello, [matriz de protección del servidor de copia de seguridad de Azure](backup-mabs-protection-matrix.md). Para obtener instrucciones detalladas, consulte [tooback de servidor de copia de seguridad de Azure de uso de un servidor de VMware](backup-azure-backup-server-vmware.md).


## <a name="azure-backup-server-and-system-center-data-protection-manager"></a>Azure Backup Server y System Center Data Protection Manager
### <a name="can-i-use-azure-backup-server-toocreate-a-bare-metal-recovery-bmr-backup-for-a-physical-server-br"></a>¿Puedo usar servidor de copia de seguridad de Azure toocreate una copia de seguridad de reconstrucción completa (BMR) para un servidor físico? <br/>
Sí.

### <a name="can-i-register-my-dpm-server-toomultiple-vaults-br"></a>¿Puedo registrar mi almacenes de toomultiple de servidor DPM? <br/>
No. Un servidor DPM o MABS puede ser tooonly registrado un almacén.

### <a name="which-version-of-system-center-data-protection-manager-is-supported-br"></a>¿Qué versión de System Center Data Protection Manager se admite? <br/>
Se recomienda que instale hello [más reciente](http://aka.ms/azurebackup_agent) agente de copia de seguridad de Azure en hello último paquete acumulativo (UR) para System Center Data Protection Manager (DPM). A partir de agosto de 2016, actualizar 11 del paquete acumulativo de actualizaciones es Hola última actualización.

### <a name="i-have-installed-azure-backup-agent-tooprotect-my-files-and-folders-can-i-now-install-system-center-dpm-toowork-with-azure-backup-agent-tooprotect-on-premises-applicationvm-workloads-tooazure-br"></a>Instalé tooprotect de agente de copia de seguridad de Azure Mis archivos y carpetas. ¿Puedo instalar ahora toowork de System Center DPM con copia de seguridad de Azure agente tooprotect local las cargas de trabajo de aplicación/VM tooAzure? <br/>
toouse copia de seguridad de Azure con System Center Data Protection Manager (DPM), instale DPM en primer lugar y, a continuación, instalar el agente de copia de seguridad de Azure. Instalación de componentes de copia de seguridad de Azure de hello en este orden garantiza el agente de copia de seguridad de Azure Hola funciona con DPM. No se recomienda o se admite instalar agente de copia de seguridad de Azure de hello antes de instalar DPM.


## <a name="how-azure-backup-works"></a>Cómo funciona Azure Backup
### <a name="if-i-cancel-a-backup-job-once-it-has-started-is-hello-transferred-backup-data-deleted-br"></a>¿Si cancela un trabajo de copia de seguridad una vez que se ha iniciado, se hello transfieren datos de copia de seguridad elimina? <br/>
No. Todos los datos transferidos en el almacén de hello, antes de que se ha cancelado el trabajo de copia de seguridad de hello, permanece en el almacén de Hola. Hola a Azure usa copia de seguridad una toooccasionally del mecanismo de punto de control agregar datos de copia de seguridad de toohello de puntos de comprobación durante la copia de seguridad. Porque hay puntos de comprobación en datos de copia de seguridad de hello, proceso de copia de seguridad siguiente Hola puede validar la integridad de Hola de archivos de Hola. trabajo de copia de seguridad siguiente Hola tendrán toohello incremental previamente una copia. Copias de seguridad incrementales solo transfieren los datos nuevos o modificados, lo que equivale a toobetter uso de ancho de banda.

Si cancela un trabajo de copia de seguridad para una máquina virtual de Azure, se omiten los datos transferidos. siguiente trabajo de copia de seguridad de Hello transfiere los datos incrementales de trabajo de copia de seguridad correcta última Hola.

### <a name="are-there-limits-on-when-or-how-many-times-a-backup-job-can-be-scheduledbr"></a>¿Existen límites sobre cuándo y cuántas veces se puede programar un trabajo de copia de seguridad?<br/>
Sí. Puede ejecutar trabajos de copia de seguridad en Windows Server o estaciones de trabajo de Windows una toothree veces por día. Puede ejecutar trabajos de copia de seguridad en System Center DPM tootwice un día. Por último, en las máquinas virtuales de IaaS solo se puede ejecutar un trabajo de copia de seguridad al día. Puede usar Hola directiva de programación para Windows Server o toospecify de estación de trabajo de Windows programaciones diarias o semanales. Mediante System Center DPM, puede especificar programaciones diarias, semanales, mensuales y anuales.

### <a name="why-is-hello-size-of-hello-data-transferred-toohello-recovery-services-vault-smaller-than-hello-data-i-backed-upbr"></a>¿Por qué es tamaño Hola de hello datos transferidos toohello que más pequeño que hice copia de seguridad de datos de saludo del almacén de servicios de recuperación?<br/>
 Todos los datos de Hola que se copian desde el agente de copia de seguridad de Azure o SCDPM o servidor de copia de seguridad de Azure, se comprimen y se cifran antes de que se transfieren. Una vez que se aplica el cifrado y compresión de hello, datos de hello en el almacén de copia de seguridad hello están 30-40% más pequeño.

## <a name="what-can-i-back-up"></a>¿De qué puedo hacer copia de seguridad?
### <a name="which-operating-systems-do-azure-backup-support-br"></a>¿Qué sistemas operativos admite Azure Backup? <br/>
Copia de seguridad de Azure admite Hola después de la lista de sistemas operativos para realizar copias de seguridad: archivos y carpetas y las aplicaciones de la carga de trabajo protegidas con servidor de copia de seguridad de Azure y System Center Data Protection Manager (DPM).

| Sistema operativo | Plataforma | SKU |
|:--- | --- |:--- |
| Windows 8 y SP más recientes |64 bits |Enterprise, Pro |
| Windows 7 y SP más recientes |64 bits |Ultimate, Enterprise, Professional, Home Premium, Home Basic, Starter |
| Windows 8.1 y SP más recientes |64 bits |Enterprise, Pro |
| Windows 10 |64 bits |Enterprise, Pro, Home |
| Windows Server 2016 |64 bits |Standard, Datacenter, Essentials |
| Windows Server 2012 R2 y SP más recientes |64 bits |Standard, Datacenter, Foundation |
| Windows Server 2012 y SP más recientes |64 bits |Datacenter, Foundation, Standard |
| Windows Storage Server 2016 y SP más recientes |64 bits |Standard, Workgroup | 
| Windows Storage Server 2012 R2 y SP más recientes |64 bits |Standard, Workgroup |
| Windows Storage Server 2012 y SP más recientes |64 bits |Standard, Workgroup |
| Windows Server 2012 R2 y SP más recientes |64 bits |Essential |
| Windows Server 2008 R2 SP1 |64 bits |Standard, Enterprise, Datacenter, Foundation |
| Windows Server 2008 SP2 |64 bits |Standard, Enterprise, Datacenter, Foundation |

**Para la copia de seguridad de máquinas virtuales de Azure:**

* **Linux**: Copia de seguridad de Azure admite [una lista de distribuciones aprobadas por Azure](../virtual-machines/linux/endorsed-distros.md) , con la excepción de CoreOS Linux.  Otras Bring-Your-posee-las distribuciones de Linux también pueden trabajar como agente de máquina virtual de hello está disponible en la máquina virtual de Hola y la compatibilidad con Python existe.
* **Windows Server**: no se admiten las versiones anteriores a Windows Server 2008 R2.


### <a name="is-there-a-limit-on-hello-size-of-each-data-source-being-backed-up-br"></a>¿Hay un límite de tamaño de Hola de cada origen de datos haciendo copias de seguridad? <br/>
No hay ningún límite en la cantidad de Hola de hacer copias de seguridad tooa el almacén de datos. Copia de seguridad de Azure limita el tamaño máximo de Hola Hola origen de datos, sin embargo, estos límites son grandes. A partir de agosto de 2015, tamaño máximo de Hola para un origen de datos para los sistemas operativos de hello admitida es:

| S.No | Sistema operativo | Tamaño máximo del origen de datos |
|:---:|:--- |:--- |
| 1 |Windows Server 2012 o superior |54 400 GB |
| 2 |Windows 8 o posterior |54 400 GB |
| 3 |Windows Server 2008, Windows Server 2008 R2 |1700 GB |
| 4 |Windows 7 |1700 GB |

Hello en la tabla siguiente explica cómo se determina el tamaño de cada origen de datos.

| Origen de datos | Detalles |
|:---:|:--- |
| Volumen |cantidad de Hola de datos haciendo copias de seguridad del volumen único de un equipo servidor o cliente |
| Máquina virtual de Hyper-V |Suma de los datos de todos los VHD de Hola de máquina virtual de hello haciendo copias de seguridad |
| Base de datos de Microsoft SQL Server |Tamaño de una sola base de datos SQL de la que se hace copia de seguridad |
| Microsoft SharePoint |Suma de bases de datos de hello contenido y la configuración de una granja de servidores de SharePoint que se haya realizado previamente |
| Microsoft Exchange |Suma de todas las bases de datos de un servidor de Exchange de las que se hace copia de seguridad |
| Estado del sistema y BMR |Cada copia individual de BMR o estado del sistema del equipo de hello haciendo copias de seguridad |

Para copia de seguridad de la máquina virtual de Azure, cada máquina virtual puede tener los discos de datos too16 con cada disco de datos que se están de tamaño 1023GB o menos. 

## <a name="retention-policy-and-recovery-points"></a>Puntos de recuperación y directiva de retención
### <a name="is-there-a-difference-between-hello-retention-policy-for-dpm-and-windows-serverclient-that-is-on-windows-server-without-dpmbr"></a>¿Hay una diferencia entre la directiva de retención de Hola para DPM y cliente de Windows Server (es decir, en Windows Server sin DPM)?<br/>
No, tanto DPM como Windows Server o el cliente Windows tienen directivas de retención diarias, semanales, mensuales y anuales.

### <a name="can-i-configure-my-retention-policies-selectively--ie-configure-weekly-and-daily-but-not-yearly-and-monthlybr"></a>¿Puedo configurar de forma selectiva mis directivas de retención (es decir, configurar semanal y diariamente, pero no anual y mensualmente)?<br/>
Sí, Hola estructura de retención de copia de seguridad de Azure permite toohave total flexibilidad en la definición de directiva de retención de hello según sus requisitos.

### <a name="can-i-schedule-a-backup-at-6pm-and-specify-retention-policies-at-a-different-timebr"></a>¿Puedo programar una copia de seguridad a las 6 p.m. y establecer las directivas de retención a una hora diferente?<br/>
No. Las directivas de retención solo pueden aplicarse a puntos de copia de seguridad. Hola después de la imagen, directiva de retención de Hola se especifica para copias de seguridad realizadas en 12 a.m. y las 6 p.m.. <br/>

![Programación de copia de seguridad y retención](./media/backup-azure-backup-faq/Schedule.png)
<br/>

### <a name="if-a-backup-is-retained-for-a-long-duration-does-it-take-more-time-toorecover-an-older-data-point-br"></a>¿Si una copia de seguridad se conserva durante un período prolongado, tarda más de tiempo toorecover un punto de datos anterior? <br/>
No – hora de hello toorecover Hola más antiguo u Hola punto más reciente es Hola mismo. Cada punto de recuperación se comporta como un punto completo.

### <a name="if-each-recovery-point-is-like-a-full-point-does-it-impact-hello-total-billable-backup-storagebr"></a>¿Si cada punto de recuperación es como un punto completo, afecte Hola total facturable copia de seguridad de almacenamiento?<br/>
Los productos con un punto de retención a largo plazo típicos almacenan los datos de copia de seguridad como puntos completos. puntos completa Hola son almacenamiento *ineficaz* pero resulta más fácil y más rápido toorestore. Las copias incrementales son almacenamiento *eficaz* pero requiere que toorestore una cadena de datos, lo que afecta a su tiempo de recuperación. Azure copia de seguridad almacenamiento arquitectura proporciona Hola mejor de ambos mundos óptimamente almacenando datos para restores más rápidos y incurrir en costos de almacenamiento baja. Este enfoque del almacenamiento de datos garantiza que el ancho de banda de entrada y salida se utiliza de manera eficiente. Tanto la cantidad de Hola de tiempo de hello y almacenamiento de datos necesita toorecover Hola datos, se mantiene tooa mínimo. Aprenda más sobre la eficacia de las [copias de seguridad incrementales](https://azure.microsoft.com/blog/microsoft-azure-backup-save-on-long-term-storage/).

### <a name="is-there-a-limit-on-hello-number-of-recovery-points-that-can-be-createdbr"></a>¿Hay un límite del número de Hola de puntos de recuperación que se pueden crear?<br/>
Puede crear puntos de recuperación de too9999 por instancia protegido. Una instancia protegida es un equipo, servidor (físico o virtual) o carga de trabajo configurado tooback seguridad tooAzure de datos. Para obtener más información, vea las explicaciones de Hola de [copias de seguridad y retención](./backup-introduction-to-azure-backup.md#backup-and-retention), y [¿qué es una instancia protegida](./backup-introduction-to-azure-backup.md#what-is-a-protected-instance)?

### <a name="how-many-recoveries-can-i-perform-on-hello-data-that-is-backed-up-tooazurebr"></a>¿El número de recuperaciones se pueden realizar en los datos de Hola que se copian de seguridad tooAzure?<br/>
No hay ningún límite en el número de Hola de recuperaciones de copia de seguridad de Azure.

### <a name="when-restoring-data-do-i-pay-for-hello-egress-traffic-from-azure-br"></a>Al restaurar los datos, ¿tengo que pagar por el tráfico de salida de hello de Azure? <br/>
No. Sus recuperaciones son gratuitos y no se le cobrará por tráfico de salida de hello.

## <a name="azure-backup-encryption"></a>Cifrado de Azure Backup
### <a name="is-hello-data-sent-tooazure-encrypted-br"></a>¿Se envían datos de hello tooAzure cifrado? <br/>
Sí. Los datos se cifran en la máquina de cliente/servidor/SCDPM local hello mediante AES256 y datos Hola se envían a través de una conexión HTTPS segura.

### <a name="is-hello-backup-data-on-azure-encrypted-as-wellbr"></a>¿Son los datos de copia de seguridad de hello en Azure cifrado también?<br/>
Sí. enviar datos de Hello tooAzure permanece cifrado (en reposo). Microsoft descifrar los datos de copia de seguridad de Hola en cualquier momento. Cuando copia de seguridad de una máquina virtual de Azure, copia de seguridad de Azure se basa en el cifrado de la máquina virtual de Hola. Por ejemplo, si la máquina virtual se cifra con el cifrado del disco de Azure, o alguna otra tecnología de cifrado, copia de seguridad de Azure utiliza ese toosecure cifrado los datos.

### <a name="what-is-hello-minimum-length-of-encryption-key-used-tooencrypt-backup-data-br"></a>¿Cuál es la longitud mínima de Hola de clave de cifrado utilizan datos de copia de seguridad de tooencrypt? <br/>
clave de cifrado de Hello debe tener al menos 16 caracteres cuando se utiliza el agente de copia de seguridad de Azure. Para las máquinas virtuales de Azure, no hay ningún toolength límite de las claves usadas por KeyVault de Azure. 

### <a name="what-happens-if-i-misplace-hello-encryption-key-can-i-recover-hello-data-or-can-microsoft-recover-hello-data-br"></a>¿Qué ocurre si pierde la clave de cifrado de hello? ¿Puedo recuperar datos de hello (o) Microsoft puede recuperar los datos de hello? <br/>
datos de copia de seguridad de Hello tooencrypt usado clave Hola están presentes únicamente en instalaciones de cliente de Hola. Microsoft no mantiene una copia en Azure y no tiene ninguna clave de acceso toohello. Si el cliente de hello coloca incorrectamente clave hello, Microsoft no puede recuperar datos de copia de seguridad de saludo.
