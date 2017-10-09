---
title: aaaHow toocreate un recurso compartido de archivos de Azure | Documentos de Microsoft
description: "Cómo toocreate compartir un archivo de Azure en almacenamiento de archivos de Azure con hello portal de Azure, PowerShell y Hola CLI de Azure."
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
ms.openlocfilehash: c4c59966b82d743fb4ecf79f48c0c8e61295d03d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a>Creación de un recurso compartido de archivos en Azure File Storage
Puede crear recursos compartidos de archivos de Azure mediante [portal de Azure](https://portal.azure.com/)Hola cmdlets de PowerShell de almacenamiento de Azure, Hola bibliotecas de cliente de almacenamiento de Azure u Hola API de REST de almacenamiento de Azure. En este tutorial, obtendrá información sobre:
* [¿Cómo toocreate un archivo de Azure compartir el uso de hello portal de Azure](#Create file share through hello Portal)
* [¿Cómo toocreate un archivo de Azure compartir con Powershell](#Create file share using PowerShell)
* [¿Cómo toocreate un archivo de Azure compartir con CLI](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a>Requisitos previos
toocreate un recurso compartido de archivos de Azure, puede usar una cuenta de almacenamiento que ya existe, o [crear una nueva cuenta de almacenamiento de Azure](storage-create-storage-account.md). toocreate un recurso compartido de archivos de Azure con PowerShell, necesitará la clave de cuenta de hello y nombre de la cuenta de almacenamiento... Necesitará la clave de la cuenta de almacenamiento si tiene previsto toouse Powershell o CLI.

## <a name="create-file-share-through-hello-portal"></a>Crear recurso compartido de archivos a través de hello Portal
1. **Vaya tooStorage hoja de cuenta en el Portal de Azure**:    
    ![Hoja de la cuenta de almacenamiento](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)

2. **Haga clic en el botón Agregar recurso compartido de archivos**:    
    ![Haga clic en hello Agregar botón de recurso compartido de archivos](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)

3. **Proporcione el nombre y la cuota. Actualmente, la cuota puede llegar a un máximo de 5 TB**:    
    ![Proporcione un nombre y una cuota deseada Hola nuevo recurso compartido de archivos](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)

4. **Ver el nuevo recurso compartido de archivos**: ![ver el nuevo recurso compartido de archivos](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)

5. **Cargar un archivo**: ![Cargar un archivo](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)

6. **Explorar el recurso compartido de archivos y administrar los directorios y archivos**: ![Explorar el recurso compartido de archivos](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)


## <a name="create-file-share-through-powershell"></a>Creación de un recurso compartido de archivos mediante PowerShell
tooprepare toouse PowerShell, descargar e instalar los cmdlets de PowerShell de Azure de Hola. Vea [cómo tooinstall y configurar Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) para hello instalar punto e instrucciones de instalación.

> [!Note]  
> Se recomienda descargar e instalar o actualizar toohello última versión del módulo Azure PowerShell.

1. **Crear un contexto para la cuenta de almacenamiento y clave** contexto Hola encapsula clave de cuenta y el nombre de la cuenta del almacenamiento Hola. Para obtener instrucciones acerca de cómo copiar la clave de una cuenta desde [Azure Portal](https://portal.azure.com/), consulte [Visualización y copia de las claves de acceso de almacenamiento](storage-create-storage-account.md#view-and-copy-storage-access-keys).

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. **Creación de un nuevo recurso compartido de archivos**:    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> nombre de Hello el recurso compartido de archivos debe ser en minúsculas. Para obtener detalles completos sobre cómo asignar un nombre a recursos compartidos y archivos, consulte [Asignación de nombres y referencia a recursos compartidos, directorios, archivos y metadatos](https://msdn.microsoft.com/library/azure/dn167011.aspx).

## <a name="create-file-share-through-command-line-interface-cli"></a>Creación de un recurso compartido de archivos mediante la interfaz de línea de comandos (CLI)
1. **tooprepare toouse una interfaz de línea de comandos (CLI), descargue e instale Hola CLI de Azure.**  
    Consulte [Instalación de la CLI de Azure 2.0](/cli/azure/install-az-cli2.md) e [Introducción a la CLI de Azure 2.0](/cli/azure/get-started-with-azure-cli.md).

2. **Crear una cuenta de almacenamiento toohello de cadena de conexión en la que desea compartir de hello toocreate.**  
    Reemplace ```<storage-account>``` y ```<resource_group>``` con su grupo de recursos y el nombre de la cuenta de almacenamiento en el siguiente ejemplo de Hola.

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. **Creación de un recurso compartido de archivos**
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a>Pasos siguientes
* [Conectar y montar un recurso compartido de archivos - Windows](storage-file-how-to-use-files-windows.md)
* [Conectar y montar un recurso compartido de archivos - Linux](storage-how-to-use-files-linux.md)
* [Conectar y montar un recurso compartido de archivos - macOS](storage-file-how-to-use-files-mac.md)

Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.

* [Preguntas más frecuentes](storage-files-faq.md)
* [Solución de problemas](storage-troubleshoot-file-connection-problems.md)