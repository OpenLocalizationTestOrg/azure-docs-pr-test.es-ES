---
title: "archivos de aaaPersist en el Shell de nube de Azure (versión preliminar) | Documentos de Microsoft"
description: "Tutorial de cómo Azure Cloud Shell persiste archivos."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a>Persistencia de archivos en Azure Cloud Shell
Shell de nube aprovecha las ventajas de los archivos de toopersist de almacenamiento de archivos de Azure entre las sesiones.

## <a name="set-up-a-clouddrive-file-share"></a>Configuración de un recurso compartido de archivos `clouddrive`
Primer inicio, el Shell de nube le pedirá que tooassociate un archivo nuevo o existente compartir archivos toopersist entre sesiones.

### <a name="create-new-storage"></a>creación de nuevo almacenamiento

Al usar la configuración básica y seleccionar solo una suscripción, el Shell de nube crea tres recursos en su nombre de región de hello compatible que está más cerca de tooyou:
* Grupos de recursos: `cloud-shell-storage-<region>`
* Cuenta de almacenamiento: `cs<uniqueGuid>`
* Recurso compartido de archivos: `cs-<user>-<domain>-com-<uniqueGuid>`

![configuración de la suscripción de Hola](media/basic-storage.png)

recurso compartido de archivos de Hello monta como `clouddrive` en su `$Home` directory. Hello recurso compartido de archivos también es toostore usa una imagen de 5 GB que se crea automáticamente para usted y que se actualiza y se continúa la `$Home` directory. Se trata de una acción única y recurso compartido de archivos de hello monta automáticamente en las siguientes sesiones.

### <a name="use-existing-resources"></a>Uso de recursos existentes

Mediante el uso de hello opción avanzada, es posible asociar recursos existentes. Cuando aparezca el símbolo del sistema de hello almacenamiento el programa de instalación, seleccione **Mostrar configuración avanzada** tooview las opciones adicionales. Recursos compartidos de archivos existente reciban un toopersist de imagen de usuario de 5 GB su `$Home` directory. los menús desplegables de Hola se filtran para su región de Shell en la nube y las cuentas de almacenamiento con redundancia geográfica & local redundantes.

![configuración de grupo de recursos de Hola](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a>Restringir la creación de recursos con una directiva de recursos de Azure
Las cuentas de almacenamiento creadas en Cloud Shell se etiquetan con `ms-resource-usage:azure-cloud-shell`. Si desea que los usuarios de toodisallow desde la creación de cuentas de almacenamiento en nube Shell, cree un [directiva de recursos de Azure para etiquetas](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) que desencadena esta etiqueta específica.

## <a name="how-cloud-shell-works"></a>Cómo funciona Cloud Shell
En la nube Shell continúa archivos a través de hello siguientes métodos:
* Crear una imagen de disco de su `$Home` directory toopersist todos los contenido en el directorio de Hola. imagen de disco de Hola se guarda en el recurso compartido de archivo especificado como `acc_<User>.img` en `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, y sincroniza automáticamente los cambios.

* Montaje del recurso compartido de archivos especificado como `clouddrive` en el directorio `$Home` para la interacción directa del recurso compartido de archivos. `/Home/<User>/clouddrive`se ha asignado demasiado`fileshare.storage.windows.net/fileshare`.
 
> [!NOTE]
> Todos los archivos en el directorio `$Home`, como las claves de SSH, se conservan en la imagen de disco de usuario almacenada en el recurso compartido de archivos montado. Ponga en práctica los procedimientos recomendados correspondientes para conservar la información en el directorio `$Home` y en el recurso compartido de archivos montado.

## <a name="use-hello-clouddrive-command"></a>Hola de uso `clouddrive` comando
Con el Shell de nube, puede ejecutar un comando denominado `clouddrive`, que permite toomanually actualización Hola recurso compartido de archivos que tooCloud montada Shell.
![Ejecutar el comando "clouddrive" hello](media/clouddrive-h.png)

## <a name="mount-a-new-clouddrive"></a>Montaje de un nuevo `clouddrive`

### <a name="prerequisites-for-manual-mounting"></a>Requisitos previos para el montaje manual
Puede actualizar el recurso compartido de archivos de Hola que esté asociada con el Shell de nube mediante el uso de hello `clouddrive mount` comando.

Si montar un recurso compartido de archivos existente, deben ser cuentas de almacenamiento de hello:
* Almacenamiento con redundancia local o recursos compartidos de archivos de almacenamiento con redundancia geográfica toosupport.
* Deben ubicarse en su región asignada. Cuando haya incorporación, región de Hola se asignan toois aparece en el nombre del grupo de recursos de hello `cloud-shell-storage-<region>`.

### <a name="supported-storage-regions"></a>Regiones de almacenamiento admitidas
Hello Azure archivos deben residir en hello misma región como máquina de Shell en la nube de Hola que esté montando puedan. Clústeres de Shell en la nube existen actualmente en hello siguientes regiones:
|Ámbito|Region|
|---|---|
|América|Este de EE. UU., centro-sur de EE. UU. y oeste de EE. UU.|
|Europa|Norte de Europa y Oeste de Europa|
|Asia Pacífico|India central, Sudeste Asiático|

### <a name="hello-clouddrive-mount-command"></a>Hola `clouddrive mount` comando

> [!NOTE]
> Si va a montar un nuevo recurso compartido de archivos, se crea una nueva imagen de usuario para su `$Home` directorio, porque su anterior `$Home` imagen se mantiene en el recurso compartido de archivos anterior Hola.

Ejecute hello `clouddrive mount` comando con hello parámetros siguientes:

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

tooview obtener más detalles, ejecute `clouddrive mount -h`, tal y como se muestra aquí:

![Ejecución hello ' clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a>Desmontar `clouddrive`
Puede desmontar un recurso compartido de archivos de Shell que tooCloud montado en cualquier momento. Una vez que el recurso compartido de archivos se desmonta, estará solicitada toomount un tooyour anterior del recurso compartido de archivo nueva sesión siguiente.

tooremove un archivo de recurso compartido de Shell en la nube:
1. Ejecute `clouddrive unmount`.
2. Confirmar y confirme los mensajes de Hola.

El recurso compartido de archivos continuará tooexist a menos que se elimine manualmente. Cloud Shell dejará de buscar este recurso compartido de archivos en sesiones posteriores.

tooview obtener más detalles, ejecute `clouddrive unmount -h`, tal y como se muestra aquí:

![Ejecución hello ' clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> Ejecutar este comando no eliminará ningún recurso. Eliminación manual de un grupo de recursos, la cuenta de almacenamiento o el recurso compartido de archivos que está asignado tooCloud Shell, se eliminará permanentemente su `$Home` imagen de directorio y cualquier otro archivo en el recurso compartido de archivos. Esta operación no se puede deshacer.

## <a name="list-clouddrive-file-shares"></a>Listado de Recursos compartidos de archivos de `clouddrive`
toodiscover qué recurso compartido de archivos se monta como `clouddrive`, ejecute hello siguiente `df` comando. 

tooclouddrive de ruta de acceso del archivo de Hello muestra que su nombre de la cuenta de almacenamiento y el archivo compartan en la dirección URL de Hola. Por ejemplo: `//storageaccountname.file.core.windows.net/filesharename`

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-toocloud-shell"></a>Transferencia de archivos locales tooCloud Shell
Hola `clouddrive` sincronizaciones de directorio con la hoja de hello almacenamiento de portal de Azure. Utilice este tooor de hoja tootransfer archivos locales desde el recurso compartido de archivos. Actualizar archivos desde el Shell de nube se refleja en el almacenamiento de archivos de hello GUI al actualizar la hoja de Hola.

### <a name="download-files"></a>Descarga de archivos

![Lista de archivos locales](media/download.png)
1. En hello portal de Azure, vaya el recurso compartido de archivos montados de toohello.
2. Seleccione el archivo de destino de hello.
3. Seleccione hello **descargar** botón.

### <a name="upload-files"></a>Carga de archivos

![Toobe de archivos locales cargado](media/upload.png)
1. Vaya tooyour monta el recurso compartido de archivos.
2. Seleccione hello **cargar** botón.
3. Seleccione el archivo hello o archivos que desee tooupload.
4. Confirmar carga Hola.

Ahora debería ver los archivos de Hola que son accesibles en su `clouddrive` directorio en el Shell de nube.

## <a name="next-steps"></a>Pasos siguientes
[Inicio rápido de Cloud Shell](quickstart.md) <br>
[Información sobre Azure File Storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage) <br>
[Información sobre las etiquetas de Storage](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) <br>
