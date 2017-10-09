---
title: aaaMove tooand de datos de almacenamiento de blobs de Azure con Python | Documentos de Microsoft
description: Mover datos tooand de almacenamiento de blobs de Azure usa Python
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 24276252-b3dd-4edf-9e5d-f6803f8ccccc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: c2be9600e0d6cb05bcf4109a8d554db522704ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a>Mover datos tooand de almacenamiento de blobs de Azure usa Python
Este tema describe cómo toolist, cargar y descargar blobs mediante Hola API de Python. Con hello API de Python proporcionado en Azure SDK, puede:

* Crear un contenedor
* Cargar un blob en un contenedor
* Descargar blobs
* Lista de blobs de hello en un contenedor
* Eliminar un blob

Para obtener más información acerca del uso de hello Python API, consulte [cómo tooUse Hola servicio de almacenamiento de blobs de Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Si está usando la máquina virtual que se configuró con secuencias de comandos de hello proporcionadas por [máquinas virtuales de ciencia de datos en Azure](machine-learning-data-science-virtual-machines.md), a continuación, AzCopy ya está instalado en hello máquina virtual.
> 
> [!NOTE]
> Para un almacenamiento de blobs de tooAzure introducción completa, consulte demasiado[conceptos básicos de Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) y demasiado[servicio Blob de Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Requisitos previos
Este documento se da por supuesto que tiene una suscripción de Azure, una cuenta de almacenamiento y la clave de almacenamiento correspondiente de Hola para esa cuenta. Antes de cargar o descargar datos, debe conocer su nombre de cuenta de almacenamiento de Azure y la clave de cuenta.

* tooset una suscripción de Azure, consulte [un mes evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Para obtener instrucciones sobre la creación de una cuenta de almacenamiento y para obtener información de cuentas y claves, vea [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).

## <a name="upload-data-tooblob"></a>Cargar datos tooBlob
Agregue Hola siguiente fragmento de código cerca de la parte superior de Hola de cualquier código de Python en las que quiera tooprogrammatically acceso a almacenamiento de Azure:

    from azure.storage.blob import BlobService

Hola **BlobService** objeto le permite trabajar con contenedores y blobs. Hola siguiente código crea un objeto de BlobService con clave de cuenta y el nombre de la cuenta del almacenamiento Hola. Reemplace el nombre de la cuenta y la clave de cuenta por la cuenta real y la clave.

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

Usar hello después de blob de métodos tooupload datos tooa:

1. colocar\_bloque\_blob\_de\_(carga el contenido de Hola de un archivo de ruta de acceso especificada de hello) de la ruta de acceso
2. colocar\_block_blob\_de\_archivo (carga contenido Hola desde un archivo ya abierto/stream)
3. put\_block\_blob\_from\_bytes (carga una matriz de bytes)
4. colocar\_bloque\_blob\_de\_texto (carga Hola especificada valor de texto mediante Hola una codificación especificada)

Hola siguiente código de ejemplo carga un contenedor de tooa de archivo local:

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

Hello código de ejemplo siguiente carga todos los archivos de hello (excluyendo los directorios) en un almacenamiento de tooblob de directorio local:

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in hello LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading hello data %s"%blob_name


## <a name="download-data-from-blob"></a>Descargar datos del blob
Usar hello siguientes datos toodownload de métodos de un blob:

1. get\_blob\_to\_path
2. get\_blob\_to\_file
3. get\_blob\_to\_bytes
4. get\_blob\_to\_text

Estos métodos que realizan Hola de fragmentación es necesario cuando el tamaño de Hola de datos de hello supera los 64 MB.

Hello código de ejemplo siguiente descarga contenido de Hola de un blob en un archivo local de tooa de contenedor:

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

Hello código de ejemplo siguiente descarga todos los blobs de un contenedor. Utiliza lista\_blobs tooget lista de Hola de blobs disponibles en el contenedor de Hola y descargarlos tooa de directorio local.

    from azure.storage.blob import BlobService
    from os.path import join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)

    # List all blobs and download them one by one
    blobs = blob_service.list_blobs(CONTAINER_NAME)
    for blob in blobs:
        local_file = join(LOCAL_DIRECT, blob.name)
        try:
            blob_service.get_blob_to_path(CONTAINER_NAME, blob.name, local_file)
        except:
            print "something wrong happened when downloading hello data %s"%blob.name
