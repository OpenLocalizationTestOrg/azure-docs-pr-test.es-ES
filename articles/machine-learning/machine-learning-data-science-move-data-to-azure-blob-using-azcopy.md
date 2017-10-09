---
title: aaaMove tooand de datos del almacenamiento de Blob de Azure con AzCopy | Documentos de Microsoft
description: Mover datos tooand de almacenamiento de blobs de Azure con AzCopy
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c309ceb2-0e83-4a07-b16d-c997dcd62d5c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: b381ba004ac16879b6c633950d03d13ad82d5b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a>Mover datos tooand de almacenamiento de blobs de Azure con AzCopy
AzCopy es una utilidad de línea de comandos diseñada para cargar, descargar y copia tooand de datos de blob de Microsoft Azure, archivos y almacenamiento de tabla.

Para obtener instrucciones acerca de cómo instalar AzCopy e información adicional sobre el uso con hello plataforma Windows Azure, consulte [Introducción a la utilidad de línea de comandos de AzCopy hello](../storage/common/storage-use-azcopy.md).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Si está usando la máquina virtual que se configuró con secuencias de comandos de hello proporcionadas por [máquinas virtuales de ciencia de datos en Azure](machine-learning-data-science-virtual-machines.md), a continuación, AzCopy ya está instalado en hello máquina virtual.
> 
> [!NOTE]
> Para un almacenamiento de blobs de tooAzure introducción completa, consulte demasiado[conceptos básicos de Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) y demasiado[servicio Blob de Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Requisitos previos
Este documento se supone que tiene una suscripción de Azure, una cuenta de almacenamiento y Hola correspondiente clave de almacenamiento para esa cuenta. Antes de cargar o descargar datos, debe conocer su nombre de cuenta de almacenamiento de Azure y la clave de cuenta.

* tooset una suscripción de Azure, consulte [un mes evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Para obtener instrucciones sobre la creación de una cuenta de almacenamiento y para obtener información de cuentas y claves, vea [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).

## <a name="run-azcopy-commands"></a>Ejecución de comandos de AzCopy
comandos de AzCopy toorun, abra una ventana de comandos y navegar por el directorio de instalación de AzCopy toohello en el equipo, donde se encuentra la aplicación ejecutable de hello AzCopy.exe. 

sintaxis básica de Hola para comandos de AzCopy es:

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> Puede agregar hello AzCopy tooyour sistema ruta de instalación y, a continuación, ejecute comandos de Hola desde cualquier directorio. De forma predeterminada, AzCopy se instala demasiado*% ProgramFiles (x86) %\Microsoft SDKs\Azure\AzCopy* o *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.
> 
> 

## <a name="upload-files-tooan-azure-blob"></a>Cargar archivos tooan blobs de Azure
tooupload un archivo, use Hola siguiente comando:

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a>Descarga de archivos de un blob de Azure
toodownload un archivo de un blob de Azure, Hola de uso siguiente comando:

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a>Transferir blobs de un contenedor de Azure a otro
blobs de tootransfer entre contenedores de Azure, use Hola siguiente comando:

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a>Sugerencias de uso de AzCopy
> [!TIP]
> 1. Al **cargar** archivos, */S* lo hace de forma recursiva. Sin este parámetro, no se cargan los archivos de los subdirectorios.  
> 2. Cuando **descargar** archivo */S* búsquedas Hola contenedor de forma recursiva hasta que todos los archivos en el directorio especificado hello y sus subdirectorios u Hola a todos los archivos que coinciden con un patrón especificado en hello dado directorio y sus subdirectorios, se descargan.  
> 3. No se puede especificar un **archivos blob en cuestión** toodownload con hello */Source* parámetro. toodownload un archivo específico, especifique toodownload de nombre de archivo hello blob mediante hello */patrón* parámetro. **/S** parámetro puede ser usado toohave AzCopy, busque un patrón de nombre de archivo recursivamente. Sin el parámetro de patrón de hello, AzCopy descarga todos los archivos de ese directorio.
> 
> 

