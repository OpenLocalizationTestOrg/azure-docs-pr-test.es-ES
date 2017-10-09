---
title: "copia de seguridad de Azure de HANA aaaSAP basándose en instantáneas de almacenamiento | Documentos de Microsoft"
description: "Existen dos posibilidades de copia de seguridad principales para SAP HANA en Azure Virtual Machines. Este artículo trata sobre la copia de seguridad de SAP HANA basada en instantáneas de almacenamiento"
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
ms.openlocfilehash: 32bb80f5a928a2cf63699bfe4f4cf5bbad81e6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-backup-based-on-storage-snapshots"></a>Copia de seguridad de SAP HANA basada en instantáneas de almacenamiento

## <a name="introduction"></a>Introducción

Esto forma parte de una serie de tres partes de artículos relacionados sobre copia de seguridad de SAP HANA. [Guía de backup para SAP HANA en máquinas virtuales Azure](sap-hana-backup-guide.md) proporciona una introducción e información sobre los pasos iniciales, y [SAP HANA Azure copia de seguridad en el nivel de archivo](sap-hana-backup-file-level.md) portadas Hola opción de copia de seguridad basado en el archivo.

Cuando se usa una característica de copia de seguridad de máquina virtual para un sistema de demostración de all-in-one de instancia única, uno debe considere la posibilidad de realizar una copia de seguridad de la máquina virtual en lugar de administrar las copias de seguridad HANA en hello nivel del sistema operativo. Una alternativa es copias de toocreate de tootake blobs de Azure instantáneas de discos virtuales individuales, que son la máquina virtual de tooa adjunto y mantener los archivos de datos HANA Hola. Pero un punto crítico es coherencia de la aplicación al crear una instantánea de copia de seguridad o un disco de máquina virtual mientras Hola sistema está encendido y ejecuta. Vea _coherencia de datos de SAP HANA al tomar instantáneas de almacenamiento_ en el artículo relacionado de hello [Guía de copia de seguridad para SAP HANA en máquinas virtuales Azure](sap-hana-backup-guide.md). SAP HANA tiene una característica que admite estos tipos de instantáneas de almacenamiento.

## <a name="sap-hana-snapshots"></a>Instantáneas de SAP HANA

Existe una característica en SAP HANA que admite la toma de una instantánea de almacenamiento. Sin embargo, a partir de 2016 de diciembre, hay una restricción de sistemas de toosingle-container. Las configuraciones de contenedor de varios inquilinos no son compatibles con este tipo de instantánea de base de datos (vea [Creación de una instantánea de almacenamiento (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)).

Funciona como se indica a continuación:

- Preparar para una instantánea de almacenamiento mediante la realización de instantáneas de SAP HANA Hola
- Instantánea de ejecución Hola almacenamiento (blobs de Azure instantánea, por ejemplo)
- Confirmar la instantánea de SAP HANA Hola

![Esta captura de pantalla muestra que se puede crear una instantánea de datos SAP HANA a través de una instrucción SQL](media/sap-hana-backup-storage-snapshots/image011.png)

Esta captura de pantalla muestra que se puede crear una instantánea de datos SAP HANA a través de una instrucción SQL.

![Hola, a continuación, de instantáneas también aparece en el catálogo de copia de seguridad de hello en SAP HANA Studio](media/sap-hana-backup-storage-snapshots/image012.png)

Hola de instantáneas, a continuación, también aparece en el catálogo de copia de seguridad de hello en SAP HANA Studio.

![En el disco, instantánea Hola aparece en el directorio de datos de SAP HANA Hola](media/sap-hana-backup-storage-snapshots/image013.png)

En el disco, instantánea Hola aparece en el directorio de datos de SAP HANA Hola.

Uno tiene tooensure que también se garantiza la coherencia de sistema de archivos de hello antes de ejecutar la instantánea del almacenamiento de hello mientras SAP HANA está en modo de preparación de instantánea de Hola. Vea _coherencia de datos de SAP HANA al tomar instantáneas de almacenamiento_ en el artículo relacionado de hello [Guía de copia de seguridad para SAP HANA en máquinas virtuales Azure](sap-hana-backup-guide.md).

Una vez que se realiza la instantánea del almacenamiento de hello, es fundamental tooconfirm Hola SAP HANA instantánea. Hay un toorun de instrucción SQL correspondiente: instantánea de cierre de datos de copia de seguridad (consulte [copia de seguridad de datos de instantánea instrucción CLOSE (copia de seguridad y recuperación)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/9739966f7f4bd5818769ad4ce6a7f8/content.htm)).

> [!IMPORTANT]
> Confirme la instantánea HANA Hola. Vencimiento demasiado&quot;copia en escritura&quot; SAP HANA pueden requerir espacio en disco adicional en instantánea-modo de preparación y no es posible toostart nuevas copias de seguridad hasta que se confirma la instantánea de SAP HANA Hola.

## <a name="hana-vm-backup-via-azure-backup-service"></a>Copia de seguridad de VM de HANA a través del servicio Azure Backup

A partir de 2016 de diciembre, el agente de copia de seguridad de Hola de hello servicio copia de seguridad de Azure no está disponible para las máquinas virtuales de Linux. uso de toomake de copia de seguridad de Azure en el nivel de archivo o directorio de hello, uno copiar archivos de copia de seguridad de SAP HANA tooa máquina virtual de Windows y, a continuación, usar el agente de copia de seguridad de Hola. En caso contrario, solo una copia completa de VM de Linux es posible a través del servicio de copia de seguridad de Azure Hola. Vea [información general de hello las características de copia de seguridad de Azure](../../../backup/backup-introduction-to-azure-backup.md) toofind más.

Hola servicio de copia de seguridad de Azure ofrece una opción tooback y restaurar una máquina virtual. Para obtener más información acerca de este servicio y cómo funciona puede encontrarse en el artículo hello [planear la infraestructura de copia de seguridad de máquina virtual en Azure](../../../backup/backup-azure-vms-introduction.md).

Hay dos consideraciones importantes según toothat artículo:

_&quot;Para las máquinas virtuales de Linux, solo las copias de seguridad coherentes para el archivo son posibles, como Linux no tiene un tooVSS de plataforma equivalente.&quot;_

_&quot;Las aplicaciones necesitan tooimplement sus propios &quot;corrección&quot; mecanismo en hello datos restaurados.&quot;_

Por lo tanto, uno tiene toomake que SAP HANA esté en un estado coherente en el disco cuando se inicia la copia de seguridad de Hola. Vea _instantáneas de SAP HANA_ descrita anteriormente en el documento de Hola. Sin embargo, hay un posible problema cuando SAP HANA permanece en este modo de preparación de la instantánea. Vea [Creación de una instantánea de almacenamiento (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm) para obtener más información.

El artículo establece lo siguiente:

_&quot;Se recomienda encarecidamente tooconfirm o abandonar una instantánea de almacenamiento tan pronto como sea posible después de que se ha creado. Mientras instantánea del almacenamiento de saludo se está preparando o creado, Hola está inmovilizados datos relevantes para la instantánea. Mientras que los datos relevantes para la instantánea de hello permanecen inmovilizados, todavía pueden realizarse cambios en la base de datos de Hola. Tales cambios no provocarán Hola inmovilizada toobe relativas a la instantánea de datos cambia. En su lugar, se escriben cambios hello toopositions Hola área de datos que son independientes de la instantánea de almacenamiento de Hola. Los cambios también se escriben toohello registro. Sin embargo, hello más Hola relativas a la instantánea datos se mantienen inmovilizados, Hola Hola más puede aumentar el volumen de datos.&quot;_

Copia de seguridad de Azure se encarga de coherencia del sistema de archivos Hola a través de las extensiones de VM de Azure. Estas extensiones no están disponible de forma independiente y solo funcionan en combinación con el servicio Azure Backup. Sin embargo, sigue siendo un toomanage requisito una coherencia de aplicaciones de SAP HANA instantánea tooguarantee.

Azure Backup tiene dos fases principales:

- Tomar la instantánea
- Transferencia de datos toovault

Una vez completada la fase de servicio de copia de seguridad de Azure Hola de tomar una instantánea de esta manera, una pudo confirmar instantáneas de SAP HANA Hola. Es posible que tarde varios toosee minutos en hello portal de Azure.

![En esta ilustración se muestra parte de la lista de trabajos de copia de seguridad de Hola de un servicio de copia de seguridad de Azure](media/sap-hana-backup-storage-snapshots/image014.png)

Esta ilustración muestra parte de la lista de trabajos de copia de seguridad de Hola de un servicio de copia de seguridad de Azure, lo cual era tooback usa una máquina virtual de prueba HANA Hola.

![Detalles del trabajo de tooshow hello, haga clic en trabajo de copia de seguridad de Hola Hola portal de Azure](media/sap-hana-backup-storage-snapshots/image015.png)

Detalles del trabajo de tooshow hello, haga clic en trabajo de copia de seguridad de Hola Hola portal de Azure. En este caso, se puede ver que el Hola dos fases. Es posible que tarde unos minutos hasta que se muestra la fase de la instantánea de hello como completada. La mayoría de las veces de Hola se invierte en la fase de transferencia de datos de Hola.

## <a name="hana-vm-backup-automation-via-azure-backup-service"></a>Automatización de la copia de seguridad de VM de HANA a través del servicio Azure Backup

Instantánea de SAP HANA Hola uno podría confirmar manualmente una vez que se completa la fase de instantánea de copia de seguridad de Azure de hello, como se describió anteriormente, pero resulta útil tooconsider automatización porque un administrador no puede supervisar la lista de trabajos de copia de seguridad de Hola Hola portal de Azure.

Aquí aparece una explicación de cómo puede realizarse mediante cmdlets de Azure PowerShell.

![Un servicio de copia de seguridad de Azure se creó con nombre hello hana-copia de seguridad-almacén](media/sap-hana-backup-storage-snapshots/image016.png)

Un servicio de copia de seguridad de Azure se creó con el nombre de hello &quot;hana-copia de seguridad-almacén.&quot; Hola comando PS **AzureRmRecoveryServicesVault de Get-nombre de almacén de copia de seguridad de hana** recupera Hola objeto correspondiente. Este objeto es tooset usado Hola contexto de copia de seguridad, tal como se muestra en la figura siguiente Hola.

![Se pueden comprobar para el trabajo de copia de seguridad de hello actualmente en curso](media/sap-hana-backup-storage-snapshots/image017.png)

Después establece el contexto correcto hello, uno puede comprobar si el trabajo de copia de seguridad de hello actualmente en curso y, a continuación, busque los detalles del trabajo. lista de la subtarea de Hello muestra si ya se ha completado fase de la instantánea de Hola de hello trabajo de copia de seguridad de Azure:

```
$ars = Get-AzureRmRecoveryServicesVault -Name hana-backup-vault
Set-AzureRmRecoveryServicesVaultContext -Vault $ars
$jid = Get-AzureRmRecoveryServicesBackupJob -Status InProgress | select -ExpandProperty jobid
Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
```

![Valor de Hola de sondeo en un bucle hasta que se convierta tooCompleted](media/sap-hana-backup-storage-snapshots/image018.png)

Una vez que los detalles del trabajo Hola se almacenan en una variable, es simplemente PS sintaxis tooget toohello primera entrada de la matriz y recuperar el valor de estado de Hola. script de automatización de hello toocomplete, valor de Hola de sondeo en un bucle hasta que se activa demasiado&quot;completado.&quot;

```
$st = Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
$st[0] | select -ExpandProperty status
```

## <a name="hana-license-key-and-vm-restore-via-azure-backup-service"></a>Restauración de VM y de la clave de licencia de HANA a través del servicio Azure Backup

Hola servicio de copia de seguridad de Azure está diseñado toocreate una nueva máquina virtual durante la restauración. No hay ningún plan en este momento toodo una &quot;in situ&quot; restauración de una máquina virtual de Azure existente.

![Esta ilustración muestra la opción de restauración de Hola de hello servicio de Azure en hello portal de Azure](media/sap-hana-backup-storage-snapshots/image019.png)

Esta ilustración muestra la opción de restauración de Hola de hello servicio de Azure en hello portal de Azure. Se puede elegir entre crear una máquina virtual durante la restauración o restauración de discos de Hola. Después de restaurar discos hello, resulta toocreate siendo necesaria una nueva máquina virtual en la parte superior. Cada vez que se crea una nueva máquina virtual en los cambios de hello Azure únicos Id. de máquina virtual (vea [acceso y uso de Azure VM Id. único](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)).

![Esta ilustración muestra hello Id. único de máquina virtual de Azure antes y después de la restauración de Hola a través del servicio de copia de seguridad de Azure](media/sap-hana-backup-storage-snapshots/image020.png)

Esta ilustración muestra el identificador único de máquina virtual de Azure de Hola antes y después de la restauración de Hola a través del servicio de copia de seguridad de Azure. clave de hardware SAP de Hello, que se utiliza para SAP licencias, usa este identificador único de máquina virtual. En consecuencia, una nueva licencia SAP tiene toobe instalado después de una restauración de la máquina virtual.

Una nueva característica de copia de seguridad de Azure se presenta en modo de vista previa durante la creación de hello de esta guía de copia de seguridad. Permite que una restauración de nivel de archivo basada en la instantánea de la VM de hello tomada de hello VM copia de seguridad. Esto evita la necesidad de hello toodeploy una nueva máquina virtual y, por tanto, permanece Id. de máquina virtual única de Hola Hola mismo y no se requiere ninguna nueva clave de licencia de SAP HANA. Una vez está probado completamente, se proporcionará más documentación sobre esta característica.

Copia de seguridad de Azure finalmente permitirá copia de seguridad de los discos virtuales de Azure individuales, además de archivos y directorios desde dentro de Hola máquina virtual. Una ventaja fundamental de copia de seguridad de Azure es la administración de todas las copias de seguridad de hello, evita que los clientes de hello tenga toodo. Si necesita una restauración, copia de seguridad de Azure seleccionará hello toouse de copia de seguridad correcta.

## <a name="sap-hana-vm-backup-via-manual-disk-snapshot"></a>Copia de seguridad de VM de SAP HANA a través de una instantánea de disco manual

En lugar de usar el servicio de copia de seguridad de Azure de hello, uno podría configurar una solución de copia de seguridad individual mediante la creación de instantáneas de blob de discos duros virtuales de Azure manualmente a través de PowerShell. Vea [mediante instantáneas de blob con PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/) para obtener una descripción de los pasos de Hola.

Proporciona mayor flexibilidad, pero no se resuelven los problemas de hello descritos anteriormente en este documento:

- Puede que tenga que asegurarse de que SAP HANA tiene un estado coherente
- no se puede sobrescribir el disco del sistema operativo Hola aunque exista Hola que VM está desasignada debido a un error que indica que una concesión. Solo funciona después de eliminar Hola VM, Esto conduciría tooa nuevo único Id. de máquina virtual y Hola necesidad tooinstall una nueva licencia SAP.

![Es posible toorestore discos de datos de solo Hola de una VM de Azure](media/sap-hana-backup-storage-snapshots/image021.png)

Es posible toorestore solo discos de datos de Hola de una máquina virtual de Azure, evitar el problema de Hola de obtener un nuevo identificador único de máquina virtual y, por lo tanto, invalida la licencia SAP de hello:

- Para pruebas de hello, dos discos de datos de Azure se adjunta tooa VM y RAID de software se definieron encima de ellos 
- Se confirmó que SAP HANA se encontraba en un estado coherente mediante la característica de la instantánea de SAP HANA
- Inmovilizar de sistema de archivos (vea _coherencia de datos de SAP HANA al tomar instantáneas de almacenamiento_ en el artículo relacionado de hello [Guía de copia de seguridad para SAP HANA en máquinas virtuales Azure](sap-hana-backup-guide.md))
- Se toman instantáneas de blob desde ambos discos de datos
- Cancelación de la inmovilización del sistema de archivos
- Confirmación de la instantánea de SAP HANA
- discos de datos de toorestore hello, Hola VM se cerró y ambos discos desasociar
- Después de la separación discos hello, se sobrescribe con instantáneas de blob anterior de Hola
- A continuación, se adjunta Hola restaurar los discos virtuales nuevo toohello VM
- Después de hora de la instantánea inicial Hola VM, todo el contenido de software de hello RAID funcionaba bien y se vuelve a establecer toohello blob
- HANA se estableció instantánea HANA toohello

Si bien era posible tooshut hacia abajo de SAP HANA antes de las instantáneas de blob de Hola, procedimiento Hola sería menos compleja. En ese caso, uno podría omitir la instantánea HANA hello y, si nada más está ocurriendo en sistema de hello, también omitir inmovilización de sistema de archivos de Hola. Complejidad agregada entra en la imagen de hello cuando resulta necesario toodo instantáneas mientras todo lo que está en línea. Vea _coherencia de datos de SAP HANA al tomar instantáneas de almacenamiento_ en el artículo relacionado de hello [Guía de copia de seguridad para SAP HANA en máquinas virtuales Azure](sap-hana-backup-guide.md).

## <a name="next-steps"></a>Pasos siguientes
* [Guía de copia de seguridad de SAP HANA en Azure Virtual Machines](sap-hana-backup-guide.md) ofrece una introducción e información sobre los pasos iniciales.
* [Copia de seguridad de SAP HANA en función de nivel de archivo](sap-hana-backup-file-level.md) portadas Hola opción de copia de seguridad basado en el archivo.
* toolearn tooestablish alta disponibilidad y el plan de recuperación ante desastres de SAP HANA en Azure (instancias grandes), vea [SAP HANA (instancias de gran tamaño) alta disponibilidad y recuperación ante desastres en Azure](hana-overview-high-availability-disaster-recovery.md).
