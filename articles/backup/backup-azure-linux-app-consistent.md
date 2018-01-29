---
title: "Azure Backup: Copias de seguridad coherentes con la aplicación de las máquinas virtuales Linux | Microsoft Docs"
description: "Cree copias de seguridad coherentes con la aplicación de sus máquinas virtuales Linux en Azure. En este artículo se explica la configuración del marco de trabajo del script para la copia de seguridad de máquinas virtuales de Linux implementadas en Azure. Este artículo también incluye información sobre la solución de problemas."
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
ms.date: 1/12/2018
ms.author: anuragm;markgal
ms.openlocfilehash: c2437b4cd90deda3e7239d87837a47a072f52835
ms.sourcegitcommit: e19f6a1709b0fe0f898386118fbef858d430e19d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/13/2018
---
# <a name="application-consistent-backup-of-azure-linux-vms"></a>Copias de seguridad coherentes con la aplicación de las máquinas virtuales Linux de Azure

Al tomar instantáneas de copia de seguridad de las máquinas virtuales, la coherencia con la aplicación hace referencia al inicio de las aplicaciones cuando se inician las máquinas virtuales después de su restauración. Como puede imaginar, la coherencia con la aplicación es extremadamente importante. Para asegurarse de que las máquinas virtuales de Linux son coherentes con la aplicación, que puede usar el marco de trabajo del script anterior y el script posterior de Linux para realizar copias de seguridad coherentes con la aplicación. El marco de trabajo del script anterior y el script posterior es compatible con las máquinas virtuales Linux implementadas por Azure Resource Manager. Los scripts de coherencia con la aplicación no son compatibles con máquinas virtuales implementadas por Service Manager ni máquinas virtuales Windows.

## <a name="how-the-framework-works"></a>Funcionamiento del marco de trabajo

El marco de trabajo proporciona una opción para ejecutar scripts anteriores y posteriores personalizados mientras toma una instantánea de las máquinas virtuales. Los scripts anteriores se ejecutan justo antes de tomar la instantánea de la máquina virtual y los scripts posteriores, inmediatamente después. Los scripts anteriores y posteriores proporcionan la flexibilidad necesaria para controlar la aplicación y el entorno mientras toma instantáneas de las máquinas virtuales.

Los scripts anteriores invocan las API nativas de la aplicación, que ponen en modo inactivo las E/S, y vacían el contenido en memoria en el disco. Estas acciones garantizan que la instantánea sea coherente con la aplicación. Los scripts posteriores usan las API nativas de la aplicación para reanudar las E/S, lo que permite que la aplicación reanude las operaciones normales después de tomar la instantánea de las máquinas virtuales.

## <a name="steps-to-configure-pre-script-and-post-script"></a>Pasos para configurar el script anterior y posterior

1. Inicie sesión como usuario raíz en la máquina virtual Linux de la que desea realizar la copia de seguridad.

2. Desde [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig), descargue el archivo **VMSnapshotScriptPluginConfig.json** y cópielo en la carpeta **/etc/azure** de todas las máquinas virtuales de las que quiera realizar copias de seguridad. Si la carpeta **/etc/azure** no existe, créela.

3. Copie el script anterior y el posterior de la aplicación en todas las máquinas virtuales de las que quiera realizar copias de seguridad. Puede copiar los scripts en cualquier ubicación de la máquina virtual. Asegúrese de actualizar la ruta de acceso completa de los archivos de script en el archivo **VMSnapshotScriptPluginConfig.json**.

4. Asegúrese de proporcionar los siguientes permisos para estos archivos:

   - **VMSnapshotScriptPluginConfig.json**: permiso "600". Por ejemplo, solo el usuario "raíz" debe tener permisos de "lectura" y "escritura" para este archivo, ningún usuario debe tener permisos de "ejecución".

   - **Archivo de script anterior**: permiso "700".  Por ejemplo, solo el usuario "raíz" debe tener permisos de "lectura", "escritura" y "ejecución" para este archivo.
  
   - **Script posterior**: permiso "700". Por ejemplo, solo el usuario "raíz" debe tener permisos de "lectura", "escritura" y "ejecución" para este archivo.

   > [!Important]
   > El marco de trabajo proporciona a los usuarios una gran ayuda. Proteja el marco y asegúrese de que solo el usuario "raíz" tenga acceso a los archivos JSON y de script importantes.
   > Si no se cumplen los requisitos, el script no se ejecuta, lo que da lugar a un bloqueo del sistema de archivos y a una copia de seguridad incoherente.
   >

5. Configure **VMSnapshotPluginConfig.json** como se describe a continuación:
    - **pluginName**: deje este campo como está ya que, de lo contrario, los scripts podrían no funcionar según lo previsto.

    - **preScriptLocation**: proporcione la ruta de acceso completa del script anterior en la máquina virtual de la que se va a realizar la copia de seguridad.

    - **postScriptLocation**: proporcione la ruta de acceso completa del script posterior en la máquina virtual de la que se va a realizar la copia de seguridad.

    - **preScriptParams**: proporcione los parámetros opcionales que se deban pasar al script anterior. Todos los parámetros deben estar entre comillas. Si usa varios parámetros, separe los parámetros con una coma.

    - **postScriptParams**: proporcione los parámetros opcionales que se deban pasar al script posterior. Todos los parámetros deben estar entre comillas. Si usa varios parámetros, separe los parámetros con una coma.

    - **preScriptNoOfRetries**: establezca el número de veces que el script anterior se debe volver a intentar si se produce cualquier error antes de finalizar. Cero significa que hay solo un intento y ningún reintento en caso de error.

    - **postScriptNoOfRetries**: establezca el número de veces que el script posterior se debe volver a intentar si se produce cualquier error antes de finalizar. Cero significa que hay solo un intento y ningún reintento en caso de error.
    
    - **timeoutInSeconds**: especifique los tiempos de espera individuales para el script anterior y el posterior.

    - **continueBackupOnFailure**: establezca este valor en **true** si desea que Azure Backup revierta a una copia de seguridad coherente con el sistema de archivos o coherente frente a bloqueos en caso de que el script anterior o posterior sufran un error. Si se establece en **false**, se producirá un error de la copia de seguridad en caso de error del script (excepto en el caso de una máquina virtual de un solo disco, en el que se revertirá a una copia de seguridad coherente frente a bloqueos independientemente de este valor).

    - **fsFreezeEnabled**: especifique si se debe llamar a fsfreeze de Linux al realizar la instantánea de la máquina virtual para garantizar la coherencia del sistema de archivos. Es recomendable mantener este valor en **true** a menos que la aplicación tenga una dependencia al deshabilitar fsfreeze.

6. Ahora ya está configurado el marco de trabajo del script. Si ya está configurada la copia de seguridad de la máquina virtual, la copia de seguridad siguiente invoca los scripts y desencadena la copia de seguridad coherente con la aplicación. Si la copia de seguridad de la máquina virtual no está configurada, hágalo siguiendo las instrucciones descritas en [Copia de seguridad de máquinas virtuales de Azure en almacenes de Recovery Services.](https://docs.microsoft.com/azure/backup/backup-azure-vms-first-look-arm)

## <a name="troubleshooting"></a>solución de problemas

Asegúrese de que agrega el registro adecuado al escribir el script anterior y el posterior y revise los registros de script para corregir cualquier problema. Si sigue teniendo problemas para ejecutar los scripts, consulte la tabla siguiente para más información.

| Error | Mensaje de error | Acción recomendada |
| ------------------------ | -------------- | ------------------ |
| Pre-ScriptExecutionFailed |El script anterior devolvió un error por lo que puede que la copia de seguridad no sea coherente con la aplicación.   | Examine los registros de error del script para corregir el problema.|  
|   Post-ScriptExecutionFailed |    El script posterior devolvió un error que podría afectar al estado de la aplicación. |    Examine los registros de error del script para corregir el problema y compruebe el estado de la aplicación. |
| Pre-ScriptNotFound |  No se encontró el script anterior en la ubicación especificada en el archivo de configuración **VMSnapshotScriptPluginConfig.json**. |   Asegúrese de que el script anterior está en la ruta de acceso especificada en el archivo de configuración para garantizar la realización de copias de seguridad coherentes con la aplicación.|
| Post-ScriptNotFound | No se encontró el script posterior en la ubicación especificada en el archivo de configuración **VMSnapshotScriptPluginConfig.json**. |   Asegúrese de que el script posterior está en la ruta de acceso especificada en el archivo de configuración para garantizar la realización de copias de seguridad coherentes con la aplicación.|
| IncorrectPluginhostFile | El archivo de **Pluginhost** que se incluye con la extensión VmSnapshotLinux está dañado por lo que no se puede ejecutar el script anterior ni el posterior y la copia de seguridad no será coherente con la aplicación. | Desinstale la extensión **VmSnapshotLinux**. Esta se volverá a instalar automáticamente con la siguiente copia de seguridad para solucionar el problema. |
| IncorrectJSONConfigFile | El archivo **VMSnapshotScriptPluginConfig.json** es incorrecto por lo que no se puede ejecutar el script anterior ni el posterior y la copia de seguridad no será coherente con la aplicación. | Descargue la copia de [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig) y configúrela de nuevo. |
| InsufficientPermissionforPre-Script | Para ejecutar scripts, el usuario "raíz" debe ser el propietario del archivo y este debe tener permisos "700", es decir, solo el propietario tiene permisos de "lectura", "escritura" y "ejecución". | Asegúrese de que el usuario "raíz" es el "propietario" del archivo de script y que solo el "propietario" tiene permisos de "lectura", "escritura" y "ejecución". |
| InsufficientPermissionforPost-Script | Para ejecutar scripts, el usuario "raíz" debe ser el propietario del archivo y este debe tener permisos "700", es decir, solo el "propietario" tiene permisos de "lectura", "escritura" y "ejecución". | Asegúrese de que el usuario "raíz" es el "propietario" del archivo de script y que solo el "propietario" tiene permisos de "lectura", "escritura" y "ejecución". |
| Pre-ScriptTimeout | La ejecución del script anterior de la copia de seguridad coherente con la aplicación ha superado el tiempo de espera. | Compruebe el script y aumente el tiempo de espera en el archivo **VMSnapshotScriptPluginConfig.json** situado en **/etc/azure**. |
| Post-ScriptTimeout | La ejecución del script posterior de la copia de seguridad coherente con la aplicación ha superado el tiempo de espera. | Compruebe el script y aumente el tiempo de espera en el archivo **VMSnapshotScriptPluginConfig.json** situado en **/etc/azure**. |

## <a name="next-steps"></a>pasos siguientes
[Configuración de la copia de seguridad en un almacén de Recovery Services](https://docs.microsoft.com/azure/backup/backup-azure-arm-vms)
