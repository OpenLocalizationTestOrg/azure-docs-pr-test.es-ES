---
title: "Azure Backup: Copias de seguridad coherentes con la aplicación de las máquinas virtuales Linux | Microsoft Docs"
description: "Usar secuencias de comandos tooguarantee copias de seguridad coherentes con la aplicación tooAzure, para las máquinas virtuales de Linux. los scripts de Hola aplican solo tooLinux las máquinas virtuales en una implementación de administrador de recursos; las secuencias de comandos de Hello no aplican tooWindows máquinas virtuales o las implementaciones de administrador de servicios. En este artículo le guiará por los pasos de Hola para configurar scripts de hello, incluida la solución de problemas."
services: backup
documentationcenter: dev-center-name
author: anuragmehrotra
manager: shivamg
keywords: "copias de seguridad coherentes con la aplicación; copias de seguridad coherentes con la aplicación de máquinas virtuales de Azure; copia de seguridad de máquinas virtuales Linux; Azure Backup"
ms.assetid: bbb99cf2-d8c7-4b3d-8b29-eadc0fed3bef
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/12/2017
ms.author: anuragm;markgal
ms.openlocfilehash: d557dd973364d79bb4d8ce954f648de835dd345f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-consistent-backup-of-azure-linux-vms-preview"></a>Copias de seguridad coherentes con la aplicación de las máquinas virtuales Linux de Azure (versión preliminar)

En este artículo se habla Hola script previo de Linux y framework posterior a la secuencia de comandos y cómo puede resultarle tootake usa copias de seguridad coherentes con la aplicación de máquinas virtuales de Linux de Azure.

> [!Note]
> marco de script previo y posterior a la secuencia de comandos de Hello solo se admite para máquinas virtuales Linux implementadas por el Administrador de recursos de Azure. No se admiten scripts para coherencia con la aplicación de máquinas virtuales implementadas por el administrador de servicios o máquinas virtuales Windows.
>

## <a name="how-hello-framework-works"></a>Cómo funciona el marco de trabajo de Hola

marco de Hello proporciona una opción toorun scripts previos personalizados y secuencias de comandos posteriores al mientras viaja con instantáneas de máquina virtual. Se ejecutan scripts previos justo antes de tomar instantánea de máquina virtual de Hola y scripts posteriores a la que se ejecutan inmediatamente después de tomar instantáneas de máquina virtual de Hola. Esto deja Hola flexibilidad toocontrol su aplicación y entorno mientras viaja con instantáneas de máquina virtual.

En este escenario, es importante tooensure backup de VM coherentes con la aplicación. secuencia de comandos previa Hola puede invocar nativo de la aplicación API tooquiesce Hola IOs y vaciar disco toohello contenido en memoria. Esto garantiza que esa instantánea hello es coherente con la aplicación (es decir, esa aplicación Hola aparece cuando Hola arranca la máquina virtual posteriores a la restauración). Posterior a la secuencia de comandos puede ser usado toothaw Hola IOs. Esto lo hace mediante el uso de las API nativas de la aplicación para que la aplicación hello puede reanudar la instantánea de la VM de post de las operaciones normales.

## <a name="steps-tooconfigure-pre-script-and-post-script"></a>Pasos tooconfigure script previo y posterior a la secuencia de comandos

1. Inicie sesión en como Hola toohello de usuario raíz VM de Linux que desea tooback.

2. Descargar **VMSnapshotScriptPluginConfig.json** de [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig)y, a continuación, cópielo toohello **/etcetera/azure** carpeta en todas las máquinas virtuales de Hola que se vayan tooback seguridad. Crear hello **/etcetera/azure** directorio si no existe ya.

3. Copie Hola script previo y posterior a la secuencia de comandos para la aplicación en hello todas las máquinas virtuales que piensa tooback seguridad. Puede copiar ubicación Hola scripts tooany Hola máquina virtual. Puede tooupdate seguro Hola ruta de acceso completa Hola archivos de script de Hola **VMSnapshotScriptPluginConfig.json** archivo.

4. Asegúrese de hello los siguientes permisos para estos archivos:

   - **VMSnapshotScriptPluginConfig.json**: permiso "600". Por ejemplo, solo el usuario de "root" debe tener el archivo de toothis de permisos de "lectura" y "escritura" y ningún usuario debe tener permisos de "ejecución".

   - **Archivo de script anterior**: permiso "700".  Por ejemplo, debe tener solo "usuario"root "lectura", "escritura" y "ejecutar" archivo de toothis de permisos.
  
   - **Script posterior**: permiso "700". Por ejemplo, debe tener solo "usuario"root "lectura", "escritura" y "ejecutar" archivo de toothis de permisos.

   > [!Important]
   > marco de trabajo de Hello proporciona a los usuarios de gran ayuda. Es importante que es seguro y que el usuario "root" solo tiene toocritical acceder a los archivos JSON y secuencias de comandos.
   > Si no se cumplen los requisitos anteriores hello, no se ejecuta el script de Hola. Esto resultará en la realización de copias de seguridad coherentes con el sistema de archivos y coherentes frente a bloqueos.
   >

5. Configure **VMSnapshotPluginConfig.json** como se describe a continuación:
    - **pluginName**: deje este campo como está ya que, de lo contrario, los scripts podrían no funcionar según lo previsto.

    - **preScriptLocation**: proporcionar ruta de acceso completa de Hola de secuencia de comandos previa hello en hello VM copia de seguridad que toobe continuo.

    - **postScriptLocation**: proporcione la ruta de acceso completa de hello del script posterior a la de hello en hello VM copia de seguridad que toobe continuo.

    - **preScriptParams**: proporcionar parámetros opcionales de Hola que necesitan toobe pasa toohello pre-script. Todos los parámetros deben estar entre comillas y deben estar separados por comas si hay varios parámetros.

    - **postScriptParams**: proporcionar parámetros opcionales de Hola que necesitan toobe pasa toohello posteriores a la secuencia de comandos. Todos los parámetros deben estar entre comillas y deben estar separados por comas si hay varios parámetros.

    - **preScriptNoOfRetries**: Hola número de veces que se debe reintentar la secuencia de comandos previa Hola si hay algún error antes de terminar de conjunto. Cero significa que hay solo un intento y ningún reintento en caso de error.

    - **postScriptNoOfRetries**: Hola número de veces que se debe reintentar la secuencia de comandos posterior a la de Hola si hay algún error antes de terminar de conjunto. Cero significa que hay solo un intento y ningún reintento en caso de error.
    
    - **tiempoDeEsperaEnSegundos**: especificar los tiempos de espera individuales de script posterior a la de Hola y de escritura previa de Hola.

    - **continueBackupOnFailure**: establezca este valor demasiado**true** si desea copia de seguridad de Azure toofall tooa atrás archivo sistema coherente de bloqueo/copia de seguridad coherente si el script anterior o posterior a la secuencia de comandos se produce un error. Si se establece demasiado**false** Hola copia de seguridad en caso de error de secuencia de comandos (excepto cuando tenga VM solo disco que corresponden a las fechas volver toocrash-copia de seguridad coherente independientemente de esta configuración) se produce un error.

    - **fsFreezeEnabled**: especifique si debe llamarse fsfreeze Linux mientras viaja con coherencia del sistema de archivos de hello VM instantánea tooensure. Se recomienda mantener esta configuración establece demasiado**true** a menos que la aplicación tiene una dependencia acerca de cómo deshabilitar fsfreeze.

6. marco de trabajo de script de Hola ya está configurada. Si ya está configurada la copia de seguridad de máquina virtual de hello, siguiente copia de seguridad de hello invoca scripts de Hola y desencadena la copia de seguridad coherentes con la aplicación. Si no está configurada la copia de seguridad de máquina virtual de hello, puede configurarlo mediante el uso de [almacenes de servicios de máquinas virtuales de Azure tooRecovery de copia de seguridad.](https://docs.microsoft.com/azure/backup/backup-azure-vms-first-look-arm)

## <a name="troubleshooting"></a>Solución de problemas

Asegúrese de agregar un registro adecuado al escribir el script previo y posterior a la secuencia de comandos y revisar su toofix de registros de script cualquier problema de secuencia de comandos. Si sigue teniendo problemas al ejecutar las secuencias de comandos, consulte toohello para obtener más información en la tabla siguiente.

| Error | Mensaje de error | Acción recomendada |
| ------------------------ | -------------- | ------------------ |
| Pre-ScriptExecutionFailed |secuencia de comandos previa Hola devolvió un error, por lo que la copia de seguridad podría no ser coherentes con la aplicación. | Buscar registros de error de Hola para su problema de hello toofix de secuencia de comandos.|  
|   Post-ScriptExecutionFailed |    script posterior a la de Hello devolvió un error que podría afectar al estado de la aplicación. |  Buscar registros de error de Hola para su problema de hello toofix de secuencia de comandos y compruebe el estado de la aplicación hello. |
| Pre-ScriptNotFound |  Hello previa de la secuencia de comandos no se encontró en la ubicación de Hola que se especifica en hello **VMSnapshotScriptPluginConfig.json** el archivo de configuración. | Asegúrese de seguro es preliminar script está presente en la ruta de acceso de Hola que se especifica en hello config tooensure coherentes con la aplicación copia de seguridad.|
| Post-ScriptNotFound | script posterior a la Hello no se encontró una en la ubicación de Hola que se especifica en hello **VMSnapshotScriptPluginConfig.json** el archivo de configuración. | Asegúrese de que es posterior a la secuencia de comandos está presente en la ruta de acceso de Hola que se especifica en hello config tooensure coherentes con la aplicación copia de seguridad.|
| IncorrectPluginhostFile | Hola **Pluginhost** archivo, que se incluye con hello VmSnapshotLinux extensión, está dañado, por lo que no se pueden ejecutar el script previo y posterior a la secuencia de comandos y copia de seguridad de hello no es coherentes con la aplicación.   | Desinstalar hello **VmSnapshotLinux** y automáticamente se reinstalará problema de hello siguiente copia de seguridad toofix Hola. |
| IncorrectJSONConfigFile | Hola **VMSnapshotScriptPluginConfig.json** archivo es incorrecta, por lo que el script de anterior y no se puede ejecutar el script posterior a la copia de seguridad de hello no es coherentes con la aplicación. | Descargar copia Hola de [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig) y volver a configurar. |
| InsufficientPermissionforPre-Script | Para ejecutar scripts, usuario "raíz" debe ser propietario de Hola de archivo hello y archivo hello debe tener permisos "700" (es decir, debe tener solo "propietario" de "lectura", "escritura" y "ejecutar" permisos). | Asegúrese de que es de usuario "raíz" hello "propietario" del archivo de script de Hola y que solo el "propietario" con "permisos de lectura", "escritura" y "ejecutar". |
| InsufficientPermissionforPost-Script | Para ejecutar scripts, usuario raíz debe ser propietario de Hola de archivo hello y archivo hello debe tener permisos "700" (es decir, debe tener solo "propietario" de "lectura", "escritura" y "ejecutar" permisos). | Asegúrese de que es de usuario "raíz" hello "propietario" del archivo de script de Hola y que solo el "propietario" con "permisos de lectura", "escritura" y "ejecutar". |
| Pre-ScriptTimeout | Hello ejecución del script anterior copia de seguridad coherentes con la aplicación hello-agotó el tiempo. | Compruebe el script de Hola y aumentar el tiempo de espera de hello en hello **VMSnapshotScriptPluginConfig.json** archivo que se encuentra en **/etcetera/azure**. |
| Post-ScriptTimeout | ejecución de Hello del script posterior a la copia de seguridad coherentes con la aplicación hello agotó el tiempo de espera. | Compruebe el script de Hola y aumentar el tiempo de espera de hello en hello **VMSnapshotScriptPluginConfig.json** archivo que se encuentra en **/etcetera/azure**. |

## <a name="next-steps"></a>Pasos siguientes
[Configurar el almacén de servicios de recuperación de tooa de copia de seguridad de máquina virtual](https://docs.microsoft.com/azure/backup/backup-azure-arm-vms)
