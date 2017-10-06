---
title: aaaHow toouse PowerShell toomanage almacenamiento de archivos de Azure | Documentos de Microsoft
description: "Obtenga información acerca de almacenamiento de archivos de Azure de toouse PowerShell toomanage."
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
ms.openlocfilehash: 0e30e8796cf8bbf5f9249b26179d5e0f9077c8fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a>¿Cómo toouse PowerShell toomanage almacenamiento de archivos de Azure
Puede usar toocreate de PowerShell de Azure y administrar recursos compartidos de archivos.

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a>Instalar los cmdlets de PowerShell de hello para el almacenamiento de Azure
tooprepare toouse PowerShell, descargar e instalar los cmdlets de PowerShell de Azure de Hola. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) para hello instalar punto e instrucciones de instalación.

> [!NOTE]
> Se recomienda descargar e instalar o actualizar toohello última versión del módulo Azure PowerShell.
> 
> 

Abra una ventana de Azure PowerShell haciendo clic en **Inicio** y escribiendo **Windows PowerShell**. ventana de PowerShell de Hello carga el módulo de Powershell de Azure de Hola para usted.

## <a name="create-a-context-for-your-storage-account-and-key"></a>Creación de un contexto para la cuenta y clave de almacenamiento
Crear el contexto de cuenta de almacenamiento de Hola. contexto de Hello encapsula clave de cuenta y el nombre de la cuenta del almacenamiento Hola. Para obtener instrucciones acerca de cómo copiar la clave de cuenta de hello [portal de Azure](https://portal.azure.com), consulte [visualizar y copiar claves de acceso de almacenamiento](storage-create-storage-account.md#view-and-copy-storage-access-keys).

Reemplace `storage-account-name` y `storage-account-key` con el nombre de la cuenta de almacenamiento y la clave en el siguiente ejemplo de Hola.

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a>Creación de un nuevo recurso compartido de archivos
Crear recurso compartido nuevo hello, denominado `logs`.

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

Ahora tiene un recurso compartido de archivos en Almacenamiento de archivos. A continuación, agregaremos un directorio y un archivo.

> [!IMPORTANT]
> nombre de Hello el recurso compartido de archivos debe ser en minúsculas. Para obtener detalles completos sobre cómo asignar un nombre a recursos compartidos y archivos, consulte [Asignación de nombres y referencia a recursos compartidos, directorios, archivos y metadatos](https://msdn.microsoft.com/library/azure/dn167011.aspx).
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a>Cree un directorio en el recurso compartido de archivos de Hola
Cree un directorio en el recurso compartido de Hola. En el siguiente ejemplo de Hola, directorio de Hola se denomina `CustomLogs`.

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a>Cargar un directorio de archivos local toohello
Ahora cargue un directorio de toohello de archivos local. Hello en el ejemplo siguiente se carga un archivo de `C:\temp\Log1.txt`. Edite la ruta de acceso de archivo de Hola para que apunte tooa archivo válido en el equipo local.

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a>Enumerar archivos de hello en el directorio de Hola
toosee Hola archivo hello directorio, puede enumerar todos los archivos del directorio de Hola. Este comando devuelve subdirectorios y archivos de hello (si hay alguno) hello CustomLogs directorio.

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

Get-AzureStorageFile devuelve una lista de archivos y directorios para cualquier objeto de directorio que se pase. "Get-AzureStorageFile-compartir $s" devuelve una lista de archivos y directorios en el directorio raíz de Hola. tooget una lista de archivos en un subdirectorio, deberá toopass Hola subdirectorio tooGet-AzureStorageFile. Es lo que hace esto: Hola primera parte del comando hello la canalización de toohello devuelve una instancia del directorio del subdirectorio de hello CustomLogs. A continuación, que se pasó a Get-AzureStorageFile, que devuelve Hola archivos y directorios en CustomLogs.

## <a name="copy-files"></a>Copiar archivos
A partir de la versión 0.9.7 de PowerShell de Azure, puede copiar un archivo de tooanother, un blob de tooa de archivo o un archivo de tooa de blob. A continuación se muestran cómo tooperform estas copian operaciones mediante cmdlets de PowerShell.

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a>Pasos siguientes
Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.

* [Preguntas más frecuentes](storage-files-faq.md)
* [Solución de problemas](storage-troubleshoot-file-connection-problems.md)