---
title: "recurso compartido de archivos de Azure de aaaMount a través de SMB con macOS | Documentos de Microsoft"
description: "Obtenga información acerca de cómo compartir toomount un archivo de Azure a través de SMB con macOS."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 71aaec8a77b770fe147b783c0ab9f86830176bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a>Montaje de un recurso compartido de archivos de Azure mediante SMB con macOS
[Almacenamiento de Azure archivo](../storage-dotnet-how-to-use-files.md) servicio de Microsoft que le permite toocreate y use red recursos compartidos de archivos en hello Azure usa estándar del sector Hola. Los recursos compartidos de archivos de Azure se pueden montar en macOS Sierra (10.12) y El Capitan (10.11). Este artículo muestra toomount de dos maneras diferentes un recurso compartido de archivos de Azure en macOS con hello buscador de interfaz de usuario y Hola Terminal.

> [!Note]  
> Antes de montar un recurso compartido de archivos de Azure con SMB, se recomienda deshabilitar la firma de paquetes SMB. De no hacerlo, puede producir un rendimiento deficiente al tener acceso a recurso compartido de archivos de Azure de Hola de macOS. Por lo que esto no afectan a la seguridad de saludo de la conexión, se cifrará la conexión de SMB. De Hola terminal hello siguientes comandos deshabilitará firma del paquete SMB, como se describe en este [artículo de soporte técnico de Apple acerca de cómo deshabilitar la firma de paquetes SMB](https://support.apple.com/HT205926):  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a>Requisitos previos para el montaje de un recurso compartido de archivos de Azure en macOS
* **Nombre de la cuenta de almacenamiento**: toomount compartir de un archivo de Azure, se necesita Hola nombre de cuenta de almacenamiento de Hola.

* **Clave de la cuenta de almacenamiento**: toomount compartir de un archivo de Azure, se necesita Hola clave de almacenamiento principal (o secundario). Actualmente no se admiten claves SAS para el montaje.

* **Asegúrese de que el puerto 445 está abierto**: SMB se comunica a través del puerto TCP 445. En el equipo cliente (Hola Mac), compruebe que el firewall no bloquea el puerto TCP 445 toomake.

## <a name="mount-an-azure-file-share-via-finder"></a>Montaje de un recurso compartido de archivos de Azure con Finder
1. **Abrir el selector**: buscador está abierto en macOS de forma predeterminada, pero puede asegurarse de sea Hola seleccionado actualmente aplicación haciendo clic en hello "macOS enfrentan a icono" en hello acoplar:  
    ![icono enfrentan a macOS Hola](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)

2. **Seleccionar "Conexión tooServer" del menú "Ir" hello**: mediante la ruta de acceso UNC de Hola de hello [requisitos previos](#preq), convertir Hola principio doble barra diagonal inversa (`\\`) demasiado`smb://` y todas las otras barras diagonales inversas (`\`) las barras diagonales tooforwards (`/`). El vínculo debe ser similar a Hola siguiente: ![cuadro de diálogo "Conectar tooServer" hello](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)

3. **Use Hola recurso compartido de almacenamiento y el nombre de clave de cuenta cuando se le solicite un nombre de usuario y una contraseña**: al hacer clic en "Conectar" del cuadro de diálogo "Conectar tooServer" Hola, se le pedirá el nombre de usuario de hello y una contraseña (se trata de autopopulated con su macOS nombre de usuario). Tiene la opción de Hola de colocar la clave de cuenta de nombre y el almacenamiento de recurso compartido de hello en la cadena de claves de macOS.

4. **Recurso compartido de archivos de Azure de Hola de uso según sea necesario**: después de sustituir Hola recurso compartido de almacenamiento y el nombre de clave de cuenta de hello nombre de usuario y una contraseña, se montará el recurso compartido de Hola. Se puede utilizar como lo haría normalmente un recurso compartido de archivo/carpeta local, incluidos arrastrar y colocar archivos en el recurso compartido de archivos de hello:

    ![Captura de pantalla de un recurso compartido de archivos de Azure montado](./media/storage-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a>Montaje de un recurso compartido de archivos de Azure con el Terminal
1. Reemplace `<storage-account-name>` con el nombre de saludo de la cuenta de almacenamiento. Proporcione la clave de cuenta de almacenamiento como contraseña cuando se le solicite. 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. **Recurso compartido de archivos de Azure de Hola de uso según sea necesario**: recurso compartido de archivos de Azure de Hola se montará en punto de montaje de hello especificado por el comando anterior Hola.  

    ![Una instantánea del recurso compartido de archivos de Azure de hello montado](./media/storage-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a>Pasos siguientes
Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.

* [Artículo de soporte técnico de Apple - cómo tooconnect con uso compartido de archivos en el equipo Mac](https://support.apple.com/HT204445)
* [Preguntas más frecuentes](../storage-files-faq.md)
* [Solución de problemas en Windows](storage-troubleshoot-windows-file-connection-problems.md)      
* [Solución de problemas en Linux](storage-troubleshoot-linux-file-connection-problems.md)    