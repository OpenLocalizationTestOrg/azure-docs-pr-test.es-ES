---
title: aaaMount un recurso compartido de archivos de Azure y Hola de acceso que se comparten en Windows | Documentos de Microsoft
description: Montar un recurso compartido de archivos de Azure y el recurso compartido de Hola de acceso en Windows.
services: storage
documentationcenter: na
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
ms.openlocfilehash: 15ac468d9d7b8e0a195b024926ed4dd9790360d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a>Montar un recurso compartido de archivos de Azure y el recurso compartido de Hola de acceso en Windows
[Almacenamiento de Azure archivo](storage-dotnet-how-to-use-files.md) es sistema de archivos de nube de Microsoft toouse fácil. Los recursos compartidos de archivos de Azure se pueden montar en Windows y Windows Server. Este artículo muestra un recurso compartido de archivos de Azure de tres toomount de distintas maneras en Windows: con hello IU del explorador de archivos, a través de PowerShell y Hola símbolo del sistema. 

En orden toomount de un archivo de Azure compartir fuera de hello región de Azure se hospeda en, por ejemplo, local o en una región distinta de Azure, Hola sistema operativo debe admitir SMB 3.0. 

Un recurso compartido de archivos de Azure se puede montar en un equipo Windows tanto en local como en una máquina virtual de Azure en función de la versión del sistema operativo. Tabla a continuación muestra hello 

| Versión de Windows        | Versión de SMB |Se puede montar en una máquina virtual de Azure|Se puede montar en un entorno local|
|------------------------|-------------|---------------------|---------------------|
| Windows 7              | SMB 2.1     | Sí                 | No                  |
| Windows Server 2008 R2 | SMB 2.1     | Sí                 | No                  |
| Windows 8              | SMB 3.0     | Sí                 | Sí                 |
| Windows Server 2012    | SMB 3.0     | Sí                 | Sí                 |
| Windows Server 2012 R2 | SMB 3.0     | Sí                 | Sí                 |
| Windows 10             | SMB 3.0     | Sí                 | Sí                 |

> [!Note]  
> Siempre se recomienda tomar Hola KB más reciente para su versión de Windows.

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a></a>Requisitos previos para el montaje de un recurso compartido de archivos de Azure en Windows 
* **Nombre de la cuenta de almacenamiento**: toomount compartir de un archivo de Azure, se necesita Hola nombre de cuenta de almacenamiento de Hola.

* **Clave de la cuenta de almacenamiento**: toomount compartir de un archivo de Azure, se necesita Hola clave de almacenamiento principal (o secundario). Actualmente no se admiten claves SAS para el montaje.

* **Asegúrese de que el puerto 445 está abierto**: Azure File Storage usa el protocolo SMB. SMB se comunica a través del puerto TCP 445 - Compruebe toosee si el firewall no bloquea los puertos TCP 445 en el equipo cliente.

## <a name="mount-hello-azure-file-share-with-file-explorer"></a>Montar el recurso compartido de archivos de Azure de hello con el Explorador de archivos
> [!Note]  
> Tenga en cuenta que Hola siguiendo las instrucciones se muestran en Windows 10 y puede variar ligeramente en las versiones anteriores. 

1. **Abra el Explorador de archivos**: Esto puede hacerse mediante la apertura de hello menú Inicio, o bien presionando contextual Win + E.

2. **Navegue toohello el elemento de "Este PC" en el lado izquierdo de Hola de ventana hello. Esta operación cambiará menús Hola disponibles en la cinta de opciones de Hola. En el menú de equipo de hello, seleccione "Conectar a unidad de red"**.
    
    ![Menú desplegable de una captura de pantalla de hello "Conectar a unidad de red"](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. **Copiar ruta de acceso UNC de hello en panel de "Conectar" Hola Hola portal de Azure**: una descripción detallada de cómo toofind esta información puede encontrarse [aquí](storage-file-how-to-use-files-portal.md#connect-to-file-share).

    ![ruta de acceso UNC de Hola desde el panel de conexión de almacenamiento de archivo de Azure de Hola](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. **Seleccione la letra de unidad de Hola y escriba la ruta de acceso UNC Hola.** 
    
    ![Una captura de pantalla del cuadro de diálogo "Conectar a unidad de red" hello](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. **Hola de uso con el nombre de cuenta de almacenamiento `Azure\` como nombre de usuario de hello y una clave de cuenta de almacenamiento como contraseña de Hola.**
    
    ![Una captura de pantalla del cuadro de diálogo de credenciales de red de Hola](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. **Uso del recurso compartido de archivos de Azure**.
    
    ![El recurso compartido de archivos de Azure ahora está montado](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. **Cuando se toodismount listo (o desconectarse) recurso compartido de archivos de Azure de hello, puede hacerlo haciendo clic en la entrada de hello para el recurso compartido de hello en hello "ubicaciones de red" en el Explorador de archivos y seleccionando "Desconectar"**.

## <a name="mount-hello-azure-file-share-with-powershell"></a>Montar el recurso compartido de archivos de Azure de hello con PowerShell
1. **Recurso compartido de archivos de Azure de Hola de toomount de comandos siguiente Hola de uso**: Recuerde tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` con la información adecuada Hola.

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. **Recurso compartido de archivos de Azure de Hola de uso según sea necesario**.

3. **Cuando haya terminado, desmonte el recurso compartido de archivos de Azure de hello mediante el siguiente comando de hello**.

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> Puede usar hello `-Persist` parámetro en `New-PSDrive` toomake Hola rest de toohello visible de recurso compartido de archivos de Azure de hello SO mientras montado.

## <a name="mount-hello-azure-file-share-with-command-prompt"></a>Montar el recurso compartido de archivos de Azure de hello con símbolo del sistema
1. **Recurso compartido de archivos de Azure de Hola de toomount de comandos siguiente Hola de uso**: Recuerde tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` con la información adecuada Hola.

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. **Recurso compartido de archivos de Azure de Hola de uso según sea necesario**.

3. **Cuando haya terminado, desmonte el recurso compartido de archivos de Azure de hello mediante el siguiente comando de hello**.

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> Puede configurar Hola reconexión tooautomatically del recurso compartido de archivo de Azure al reiniciar por conservar las credenciales de hello en Windows. Hola siguiente comando conservará las credenciales de hello:
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a>Pasos siguientes
Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.

* [Preguntas más frecuentes](storage-files-faq.md)
* [Solución de problemas](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a>Artículos y vídeos conceptuales
* [Azure File Storage: un sistema de archivos SMB en la nube sin dificultades para Windows y Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [¿Cómo toouse almacenamiento de archivos de Azure con Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a>Compatibilidad de herramientas con Azure File Storage
* [Usar Azure PowerShell con Almacenamiento de Azure](storage-powershell-guide-full.md)
* [Cómo toouse AzCopy con almacenamiento de Microsoft Azure](storage-use-azcopy.md)
* [Uso de hello CLI de Azure con el almacenamiento de Azure](storage-azure-cli.md#create-and-manage-file-shares)
* [Solución de problemas de Azure File Storage](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a>Publicaciones de blog
* [El almacenamiento de archivos de Azure ya está disponible de manera general](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [En el interior de Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Introducing Microsoft Azure File Service (Introducción al servicio de archivos de Microsoft Azure)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Migración de datos tooAzure archivo](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Referencia
* [Referencia de la biblioteca de clientes de almacenamiento para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Referencia de la API REST del servicio de archivos](http://msdn.microsoft.com/library/azure/dn167006.aspx)
