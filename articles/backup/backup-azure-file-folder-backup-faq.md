---
title: "agente de copia de seguridad de aaaAzure preguntas más frecuentes | Documentos de Microsoft"
description: "Responde a las preguntas de toocommon sobre: cómo Hola límites de works, copia de seguridad y retención de agente de copia de seguridad de Azure."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "copia de seguridad y recuperación ante desastres; servicio de copia de seguridad"
ms.assetid: 778c6ccf-3e57-4103-a022-367cc60c411a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: bdefb4efb39301f38cdf692bdc93c841a2bbb441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-agent"></a>Preguntas acerca del agente de copia de seguridad de Azure Hola
Este artículo tiene respuestas toocommon preguntas toohelp rápidamente comprender componentes del agente de copia de seguridad de Azure Hola. En algunas de las respuestas de hello, hay artículos de toohello vínculos que tienen información completa. También puede publicar preguntas sobre Hola servicio de copia de seguridad de Azure en hello [foro de discusión](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="configure-backup"></a>Configuración de la copia de seguridad
### <a name="where-can-i-download-hello-latest-azure-backup-agent-br"></a>¿Dónde puedo descargar agente de copia de seguridad de Azure más reciente de hello? <br/>
Puede descargar el agente más reciente de Hola para realizar la copia de seguridad de Windows Server, System Center DPM o el cliente de Windows, de [aquí](http://aka.ms/azurebackup_agent). Si desea tooback una máquina virtual, utilice Hola agente de máquina virtual (que se instala automáticamente la extensión correspondiente hello). Hola agente de máquina virtual ya está presente en las máquinas virtuales creadas desde Hola Galería de Azure.

### <a name="when-configuring-hello-azure-backup-agent-i-am-prompted-tooenter-hello-vault-credentials-do-vault-credentials-expire"></a>Cuando se configura el agente de copia de seguridad de Azure de Hola, soy las credenciales de almacén de hello tooenter solicitadas. ¿Expiran las credenciales de almacén?
Sí, las credenciales de almacén de hello expiran después de 48 horas. Si se agota el archivo hello, archivos de registro en toohello Azure portal y descarga Hola almacén credenciales desde el almacén.

### <a name="what-types-of-drives-can-i-back-up-files-and-folders-from-br"></a>¿Desde qué tipos de unidades puedo realizar copias de seguridad de archivos y carpetas? <br/>
No se puede respaldar Hola siguiendo las unidades o volúmenes:

* Medios extraíbles: todos los orígenes de elementos de copia de seguridad deben notificarse como corregidos.
* Volúmenes de solo lectura: Hola volumen debe ser grabable para hello volumen shadow copy service (VSS) toofunction.
* Volúmenes sin conexión: volumen Hola debe estar en línea para toofunction VSS.
* Recurso compartido de red: volumen Hola debe ser local toohello server toobe copiado de seguridad mediante copia de seguridad en línea.
* Volúmenes protegidos por BitLocker: Hola debe desbloquearse para copia de seguridad de hello pueda suceder.
* Identificación del sistema de archivos: NTFS es Hola solo filesystem admitida.

### <a name="what-file-and-folder-types-can-i-back-up-from-my-serverbr"></a>¿De qué tipos de archivos y carpetas puedo hacer copias de seguridad desde mi servidor?<br/>
se admite Hola siguientes tipos:

* Cifrados
* Comprimidos
* Dispersos
* Comprimidos + dispersos
* Vínculos físicos: no compatibles, se omiten
* Puntos de repetición: no compatibles, se omiten
* Cifrados + dispersos: no compatibles, se omiten
* Secuencias comprimidas: no compatibles, se omiten
* Secuencias dispersas: no compatibles, se omiten

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-already-backed-by-hello-azure-backup-service-using-hello-vm-extension-br"></a>¿Puedo instalar el agente de copia de seguridad de Azure de hello en una máquina virtual de Azure ya respaldadas por el servicio de copia de seguridad de Azure de hello mediante Hola extensión de máquina virtual? <br/>
Totalmente. Copia de seguridad de Azure proporciona copia de seguridad de nivel de máquina virtual para máquinas virtuales de Azure con la extensión de máquina virtual de Hola. tooprotect archivos y carpetas en invitado Hola sistema operativo de Windows, instale el agente de copia de seguridad de Azure de hello en invitado Hola del sistema operativo Windows.

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-tooback-up-files-and-folders-present-on-temporary-storage-provided-by-hello-azure-vm-br"></a>¿Puedo instalar a hello Azure Backup agent en un tooback de máquina virtual de Azure seguridad de archivos y carpetas que aparece en el almacenamiento temporal proporcionada por hello VM de Azure? <br/>
Sí. Instalar a agente de copia de seguridad de Azure de hello en invitado Hola del sistema operativo Windows y copia de seguridad de almacenamiento de tootemporary de archivos y carpetas. Las copias de seguridad de los trabajos dejarán de funcionar cuando se borren los datos del almacenamiento temporal. Además, si se han eliminado los datos de almacenamiento temporal de hello, sólo puede restaurar el almacenamiento volátil toonon.

### <a name="whats-hello-minimum-size-requirement-for-hello-cache-folder-br"></a>¿Cuál es el requisito de tamaño mínimo de hello para la carpeta de caché de hello? <br/>
tamaño de Hola de carpeta de caché de hello determina la cantidad de Hola de datos de copia de seguridad. La carpeta de caché debe ser 5% de espacio de hello necesario para el almacenamiento de datos.

### <a name="how-do-i-register-my-server-tooanother-datacenterbr"></a>¿Cómo puedo registrar mi centro de datos de servidor tooanother?<br/>
Datos de copia de seguridad se envían toohello datacenter de hello almacén toowhich que está registrado. Centro de datos de Hello más fácil manera toochange hello toouninstall Hola agente y volver a instalar al agente de Hola y registra tooa nuevo almacén que pertenece el centro de datos de toodesired.

### <a name="does-hello-azure-backup-agent-work-on-a-server-that-uses-windows-server-2012-deduplication-br"></a>¿Es hello Azure Backup agent funcionará en un servidor que utiliza la desduplicación de Windows Server 2012? <br/>
Sí. el servicio del agente de Hello convierte Hola desduplicado datos toonormal datos cuando prepara la operación de copia de seguridad de Hola. A continuación, optimiza Hola datos de copia de seguridad, cifra los datos de hello y, a continuación, envía el servicio de copia de seguridad en línea toohello Hola cifrado datos.

## <a name="backup"></a>Backup
### <a name="how-do-i-change-hello-cache-location-specified-for-hello-azure-backup-agentbr"></a>¿Cómo se cambia la ubicación de la caché de hello especificado para el agente de copia de seguridad de Azure Hola?<br/>
Usar hello después de la ubicación de la caché de lista toochange Hola.

1. Detenga el motor de copia de seguridad de hello ejecutando el siguiente comando en un símbolo del sistema con privilegios elevados de hello:

    ```PS C:\> Net stop obengine``` 
  
2. No mueva los archivos de saludo. En su lugar, copie Hola caché espacio carpeta tooa otra unidad con espacio suficiente. espacio de memoria caché original de Hola puede quitarse después de confirmar hello las copias de seguridad están trabajando con el nuevo espacio de memoria caché Hola.
3. Hola de actualización después de las entradas del registro con la carpeta de espacio de hello ruta de acceso toohello nueva memoria caché.<br/>

    | Ruta de acceso del Registro | Clave del Registro | Valor |
    | --- | --- | --- |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config` |ScratchLocation |*Nueva ubicación de la carpeta de la memoria caché* |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider` |ScratchLocation |*Nueva ubicación de la carpeta de la memoria caché* |

4. Reiniciar el motor de copia de seguridad de hello ejecutando Hola siguiente comando en un símbolo del sistema con privilegios elevados:

    ```PS C:\> Net start obengine```

Una vez que la creación de copias de seguridad de Hola se ha completado correctamente en la nueva ubicación de la caché de hello, puede quitar la carpeta de caché original de Hola.


### <a name="where-can-i-put-hello-cache-folder-for-hello-azure-backup-agent-toowork-as-expectedbr"></a>¿Dónde puedo incluir carpeta de caché de Hola de hello Azure Backup Agent toowork según lo previsto?<br/>
Hello siguientes ubicaciones de carpeta de caché de hello no se recomiendan:

* Un medio extraíble o recurso compartido de red: carpeta de caché de hello debe ser servidor toohello local que es necesario realizar copias de seguridad mediante copia de seguridad en línea. No se admiten ubicaciones de red ni medios extraíbles como unidades USB.
* Volúmenes sin conexión: carpeta de caché de hello debe estar en línea para copia de seguridad previsto con el agente de copia de seguridad de Azure.

### <a name="are-there-any-attributes-of-hello-cache-folder-that-are-not-supportedbr"></a>¿Existen todos los atributos de carpeta de caché de Hola que no son compatibles?<br/>
Hello siguientes atributos o sus combinaciones no se admiten para la carpeta de caché de hello:

* Cifrados
* Desduplicados
* Comprimidos
* Dispersos
* Punto de reanálisis

carpeta de caché de Hola y Hola metadatos VHD no tiene atributos necesarios de hello para el agente de copia de seguridad de Azure Hola.

### <a name="is-there-a-way-tooadjust-hello-amount-of-bandwidth-used-by-hello-backup-servicebr"></a>¿Hay una cantidad de Hola de manera tooadjust de ancho de banda utilizado por el servicio de copia de seguridad de hello?<br/>
  Sí, usar hello **cambiar las propiedades de** opción ancho de banda de tooadjust del agente de copia de seguridad de Hola. También puede ajustar la cantidad de Hola de veces hello y ancho de banda cuando se usa ese ancho de banda. Para obtener instrucciones detalladas, consulte  **[Habilitación de la limitación de la red](backup-configure-vault.md#enable-network-throttling)**.

## <a name="manage-backups"></a>Administración de copias de seguridad
### <a name="what-happens-if-i-rename-a-windows-server-that-is-backing-up-data-tooazurebr"></a>¿Qué ocurre si cambia el nombre de un servidor de Windows que realiza copias de seguridad tooAzure de datos?<br/>
Al cambiar el nombre de un servidor, se detienen todas las copias de seguridad configuradas actualmente.
Registrar nuevo nombre del servidor de Hola de hello con almacén de copia de seguridad de Hola. Al registrar el nuevo nombre de Hola con el almacén de hello, Hola primera operación de copia de seguridad es un *completa* copia de seguridad. Si necesita datos toorecover copia de seguridad toohello almacén con el nombre antiguo del servidor hello, usar hello [ **otro servidor** ](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) opción Hola **recuperar datos** asistente.

### <a name="what-is-hello-maximum-file-path-length-that-can-be-specified-in-backup-policy-using-azure-backup-agent-br"></a>¿Cuál es la longitud de ruta de acceso de archivo máximo de Hola que se pueden especificar en la directiva de copia de seguridad con el agente de copia de seguridad de Azure? <br/>
El agente de Copia de seguridad de Azure usa NTFS. Hola [especificación de longitud de ruta del archivo está limitado por la API de Windows hello](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths). Si los archivos de Hola que desee tooprotect tienen una longitud de ruta de acceso de archivo más de las permitidas por hello API de Windows, copia de seguridad de carpeta primaria de Hola o unidad de disco de Hola.  

### <a name="what-characters-are-allowed-in-file-path-of-azure-backup-policy-using-azure-backup-agent-br"></a>¿Qué caracteres se permiten en la ruta de acceso de archivo de la directiva de Copia de seguridad de Azure cuando se usa el agente de Copia de seguridad de Azure? <br>
 El agente de Copia de seguridad de Azure usa NTFS. Permite [caracteres compatibles con NTFS](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) como parte de la especificación de los archivos. 
 
### <a name="i-receive-hello-warning-azure-backups-have-not-been-configured-for-this-server-even-though-i-configured-a-backup-policy-br"></a>Recibo Hola advertencia, "Copias de seguridad de Azure no se ha configurado para este servidor" Aunque he configurado una directiva de copia de seguridad <br/>
Esta advertencia se produce una vez configuración de la programación de copia de seguridad de hello almacenados en el servidor local de hello no Hola igual Hola valores almacenados en el almacén de copia de seguridad Hola. Cuando el servidor de Hola o configuración de Hola se han recuperado tooa estado bueno conocido, programaciones de copia de seguridad de hello pueden perder la sincronización. Si aparece esta advertencia, [volver a configurar la directiva de copia de seguridad de hello](backup-azure-manage-windows-server.md) y, a continuación, **ejecutar Back Up Now** servidor local de hello tooresynchronize con Azure.
