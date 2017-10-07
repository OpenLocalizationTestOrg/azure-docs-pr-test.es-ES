---
title: Hola aaaUsing 2.0 de CLI de Azure con el almacenamiento de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola interfaz de línea de comandos de Azure (CLI de Azure) 2.0 con toocreate de almacenamiento de Azure y administrar cuentas de almacenamiento y trabajar con blobs de Azure y archivos. Hola CLI de Azure 2.0 es una herramienta de multiplataforma escrita en Python."
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 14e6eb0c913676380c90a72563276245e7f08aa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a>Uso de hello Azure CLI 2.0 con el almacenamiento de Azure

Hola código abierto, multiplataforma Azure CLI 2.0 proporciona un conjunto de comandos para trabajar con hello plataforma Windows Azure. Proporciona gran parte de la misma funcionalidad que se encuentra en Hola de Hola [portal de Azure](https://portal.azure.com), incluido el acceso de datos enriquecidos.

En esta guía, le mostramos cómo hello toouse [CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform varias tareas trabajar con recursos de la cuenta de almacenamiento de Azure. Se recomienda descargar e instalar o actualizar toohello la versión más reciente de hello CLI 2.0 antes de utilizar a esta guía.

ejemplos de Hello de guía de hello suponen el uso de Hola de hello shell de Bash en Ubuntu, pero otras plataformas deben realizar de forma similar. 

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a>Requisitos previos
Esta guía se da por supuesto que comprende los conceptos básicos de hello del almacenamiento de Azure. También se da por supuesto que es capaz de toosatisfy Hola creación requisitos de las cuentas que se especifican a continuación para Azure y Hola servicio de almacenamiento.

### <a name="accounts"></a>Cuentas
* **Cuenta de Azure**: si aún no tiene ninguna suscripción a Azure, [cree una cuenta gratuita de Azure](https://azure.microsoft.com/free/).
* **Cuenta de almacenamiento**: consulte la sección [Crear una cuenta de almacenamiento](storage-create-storage-account.md#create-a-storage-account) del artículo [Acerca de las cuentas de almacenamiento de Azure](storage-create-storage-account.md).

### <a name="install-hello-azure-cli-20"></a>Instalar Hola 2.0 de CLI de Azure

Descargue e instale Hola 2.0 de CLI de Azure siguiendo las instrucciones de Hola que se describen en [instalar Azure CLI 2.0](/cli/azure/install-az-cli2).

> [!TIP]
> Si tiene problemas con la instalación de hello, desproteger hello [solución de problemas de instalación](/cli/azure/install-az-cli2#installation-troubleshooting) sección del artículo de Hola y Hola [solución de problemas de instalación](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guía en GitHub.
>

## <a name="working-with-hello-cli"></a>Trabajar con hello CLI

Una vez haya instalado Hola CLI, puede usar hello `az` comando en los comandos de CLI de Azure de interfaz de línea de comandos (intensiva de errores, Terminal, símbolo del sistema) tooaccess Hola. Hola de tipo `az` comando toosee una lista completa de comandos de base de hello (se ha truncado la siguiente salida de ejemplo de Hola):

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

En la interfaz de línea de comandos, ejecute el comando de hello `az storage --help` hello toolist `storage` comando subgrupos. las descripciones de Hola de subgrupos de hello proporcionan una visión general de Hola Hola de funcionalidad que CLI de Azure proporciona para trabajar con los recursos de almacenamiento.

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a>Conectar Hola CLI tooyour suscripción de Azure

toowork con recursos de hello en su suscripción de Azure, primero debe iniciar sesión en tooyour cuenta de Azure con `az login`. Hay varias formas de iniciar sesión:

* **Inicio de sesión interactivo**: `az login`
* **Inicio de sesión con nombre de usuario y contraseña**: `az login -u johndoe@contoso.com -p VerySecret`
  * Esta opción no es compatible con cuentas de Microsoft o cuentas que usan autenticación multifactor.
* **Inicio de sesión con una entidad de servicio**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`

## <a name="azure-cli-20-sample-script"></a>Script de ejemplo de CLI de Azure 2.0

A continuación, vamos a trabajar con una secuencia de comandos de shell pequeño que emite unos toointeract de comandos de CLI de Azure 2.0 básica con los recursos de almacenamiento de Azure. script de Hola primero crea un nuevo contenedor en la cuenta de almacenamiento, a continuación, carga un contenedor de toothat de archivo (como un blob) existente. A continuación, enumera todos los blobs Hola contenedor y por último, descarga tooa destino de archivo de hello en el equipo local que especifique.

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

**Configurar y ejecutar el script de Hola**

1. Abra el editor de texto, a continuación, copie y pegue Hola anteponer la secuencia de comandos en el editor de Hola.

2. A continuación, actualizar tooreflect de variables del script de Hola las opciones de configuración. Reemplace Hola siguientes valores tal como se especifica:

   * **\<storage_account_name\>**  nombre hello de la cuenta de almacenamiento.
   * **\<storage_account_key\>**  clave de acceso principal o secundaria de hello para la cuenta de almacenamiento.
   * **\<container_name\>**  nuevas toocreate de contenedor, por ejemplo, "azure-cli-ejemplo-container" Hola a un nombre.
   * **\<blob_name\>**  un nombre para el blob de destino de hello en el contenedor de Hola.
   * **\<file_to_upload\>**  Hola archivo toosmall de ruta de acceso en el equipo local, como "~ / images/HelloWorld.png".
   * **\<destination_file\>**  Hola ruta de acceso de archivo de destino, como "~ / downloadedImage.png".

3. Después de actualizar las variables necesarias de hello, Guardar script de Hola y salir del editor. Hola siguiente da por sentado ha denominado el script **my_storage_sample.sh**.

4. Marcar el script de Hola como archivo ejecutable, si es necesario:`chmod +x my_storage_sample.sh`

5. Ejecutar script de Hola. Por ejemplo, en Bash: `./my_storage_sample.sh`

Debe ver salida similares toohello siguiente y Hola  **\<destination_file\>**  especificado en hello script debe aparecer en el equipo local.

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> Hello salida anterior está en **tabla** formato. Puede especificar qué salida toouse formato especificando hello `--output` argumento en los comandos de CLI, o establecer globalmente mediante `az configure`.
>

## <a name="manage-storage-accounts"></a>Administrar cuentas de almacenamiento

### <a name="create-a-new-storage-account"></a>Creación de una cuenta de almacenamiento nueva
toouse almacenamiento de Azure, necesita una cuenta de almacenamiento. Puede crear una nueva cuenta de almacenamiento de Azure después de haber configurado el equipo demasiado[conectar tooyour suscripción](#connect-to-your-azure-subscription).

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* `--location` [Requerido]: Ubicación. Por ejemplo, "Oeste de EE. UU.".
* `--name`[Required]: nombre de cuenta de almacenamiento de Hola. nombre de Hello debe tener 3 caracteres too24 y use solo caracteres alfanuméricos en minúsculas.
* `--resource-group`[Required]: Nombre del grupo de recursos.
* `--sku`[Required]: Hola SKU de cuenta de almacenamiento. Valores permitidos:
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a>Establecimiento variables de entorno para una cuenta de almacenamiento de Azure predeterminada
Puede tener varias cuentas de almacenamiento en su suscripción a Azure. tooselect uno de ellos toouse para todo el almacenamiento de posterior comandos, puede establecer estas variables de entorno:

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

Otra manera tooset una cuenta de almacenamiento predeterminada consiste en usar una cadena de conexión. En primer lugar, obtener la cadena de conexión de hello con hello `show-connection-string` comando:

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

A continuación, Hola copia cadena de conexión de salida y establecer hello `AZURE_STORAGE_CONNECTION_STRING` variable de entorno (tal vez tenga la cadena de conexión de hello tooenclose entre comillas):

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> Todos los ejemplos de hello siguientes secciones de este artículo se supone que ha establecido hello `AZURE_STORAGE_ACCOUNT` y `AZURE_STORAGE_ACCESS_KEY` las variables de entorno.
>

## <a name="create-and-manage-blobs"></a>Creación y administración de blobs
Almacenamiento de blobs de Azure es un servicio para almacenar grandes cantidades de datos no estructurados, como texto o binario, que puede tener acceso desde cualquier lugar Hola mundo a través de HTTP o HTTPS. En esta sección se supone que ya está familiarizado con los conceptos del almacenamiento de Azure Blob Storage. Para más información, consulte [Introducción a Azure Blob Storage mediante .NET](../blobs/storage-dotnet-how-to-use-blobs.md) y [Conceptos de Blob service](/rest/api/storageservices/blob-service-concepts).

### <a name="create-a-container"></a>Crear un contenedor
Todos los blobs del almacenamiento de Azure han de estar en un contenedor. Puede crear un contenedor mediante hello `az storage container create` comando:

```azurecli
az storage container create --name <container_name>
```

Puede establecer uno de tres niveles de acceso de lectura para un nuevo contenedor mediante la especificación de hello opcional `--public-access` argumento:

* `off`(valor predeterminado): datos del contenedor están el propietario de la cuenta de toohello privada.
* `blob`: acceso de lectura público solo para blobs.
* `container`: Leer y mostrar acceso toohello todo contenedor público.

Para obtener más información, consulte [administrar toocontainers de acceso de lectura anónimo y los blobs](../blobs/storage-manage-access-to-resources.md).

### <a name="upload-a-blob-tooa-container"></a>Cargar un contenedor de blob tooa
Azure Blob Storage admite blobs de bloque, anexados y en páginas. Cargar blobs tooa contenedor mediante el uso de hello `blob upload` comando:

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 De forma predeterminada, Hola `blob upload` comando carga los blobs de *.vhd archivos toopage o blobs en bloques en caso contrario. toospecify otro cuando escriba cargar un blob, puede usar hello `--type` argumento--valores permitido son `append`, `block`, y `page`.

 Para obtener más información sobre tipos de blob distinto de hello, consulte [descripción Blobs en bloques, anexar Blobs y Blobs en páginas](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).


### <a name="download-a-blob-from-a-container"></a>Descarga de un blob de un contenedor
Este ejemplo se muestra cómo toodownload un blob de un contenedor:

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a>Lista de blobs de hello en un contenedor

Lista de blobs de hello en un contenedor con hello [lista de blobs de almacenamiento az](/cli/azure/storage/blob#list) comando.

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a>Copia de blobs
Los blobs se pueden copiar dentro de las cuentas de almacenamiento y regiones, o entre ellas, de forma asincrónica.

Hello en el ejemplo siguiente se muestra cómo toocopy blobs desde el almacenamiento de una cuenta tooanother. Primero creamos un contenedor en la cuenta de almacenamiento de origen de hello, especifica el acceso de lectura público para sus blobs. A continuación, se carga un contenedor de toohello de archivo y, finalmente, copia de blob de Hola desde ese contenedor en un contenedor en la cuenta de almacenamiento de destino de Hola.

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

Hola ejemplo anterior, contenedor de destino de hello ya debe existir en la cuenta de almacenamiento de destino de Hola para toosucceed de operación de copia de Hola. Además, Hola blob de origen especificada en hello `--source-uri` argumento debe incluir un token de firma (SAS) de acceso compartido, o ser accesibles públicamente, como en este ejemplo.

### <a name="delete-a-blob"></a>Eliminar un blob
toodelete un blob, use hello `blob delete` comando:

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a>Creación y administración de recursos compartidos de archivos
Almacenamiento de archivos de Azure ofrece almacenamiento compartido para las aplicaciones que usan el protocolo de bloque de mensajes del servidor (SMB) Hola. Los servicios en la nube y las máquinas virtuales de Microsoft Azure, así como las aplicaciones locales, pueden compartir datos de archivos a través de recursos compartidos montados. Puede administrar recursos compartidos de archivos y datos de archivos a través de hello CLI de Azure. Para obtener más información sobre el almacenamiento de archivos de Azure, consulte [Introducción al almacenamiento de archivos de Azure en Windows](../storage-dotnet-how-to-use-files.md) o [cómo toouse almacenamiento de archivos de Azure con Linux](../storage-how-to-use-files-linux.md).

### <a name="create-a-file-share"></a>Creación de un recurso compartido de archivos
Un recurso compartido de archivos de Azure es un recurso compartido de archivos de SMB en Azure. Todos los directorios y archivos se deben crear en un recurso compartido de archivos. Una cuenta puede contener un número ilimitado de recursos compartidos y un recurso compartido puede almacenar un número ilimitado de archivos, los límites de capacidad de toohello de cuenta de almacenamiento de Hola. Hello en el ejemplo siguiente se crea un recurso compartido de archivos denominado **MiRecursoCompartido**.

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a>Creación de directorios
Un directorio proporciona una estructura jerárquica para los recursos compartidos de archivos de Azure. Hello en el ejemplo siguiente se crea un directorio denominado **myDir** en el recurso compartido de archivos de Hola.

```azurecli
az storage directory create --name myDir --share-name myshare
```

La ruta de acceso al directorio puede incluir varios niveles, por ejemplo, **dir1/dir2**. Pero debe asegurarse de que existen todos los directorios principales antes de crear un subdirectorio. Por ejemplo, para la ruta de acceso **dir1/dir2**, primero se debe crear el directorio **dir1** y luego el directorio **dir2**.

### <a name="upload-a-local-file-tooa-share"></a>Cargar un recurso compartido tooa de archivos local
Hello en el ejemplo siguiente se carga un archivo de **~/temp/samplefile.txt** tooroot de hello **MiRecursoCompartido** recurso compartido de archivos. Hola `--source` tooupload de archivo local existente de Hola que especifica el argumento.

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

Al igual que con la creación del directorio, puede especificar una ruta de acceso de directorio dentro de hello tooupload Hola archivo tooan existente directorio compartido en el recurso compartido de hello:

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

Puede ser un archivo en el recurso compartido de hello hasta too1 TB de tamaño.

### <a name="list-hello-files-in-a-share"></a>Enumerar archivos de hello en un recurso compartido
Puede enumerar archivos y directorios en un recurso compartido mediante hello `az storage file list` comando:

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a>Copiar archivos      
Puede copiar un archivo de tooanother, un blob de tooa de archivo o un archivo de tooa de blob. Por ejemplo, toocopy un archivo tooa directorio en otro recurso compartido:        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a>Pasos siguientes
Aquí tiene algunos recursos adicionales para aprender más acerca de cómo trabajar con hello 2.0 de CLI de Azure.

* [Introducción a la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Referencia de comandos de la CLI de Azure 2.0](/cli/azure)
* [CLI de Azure 2.0 en GitHub](https://github.com/Azure/azure-cli)
