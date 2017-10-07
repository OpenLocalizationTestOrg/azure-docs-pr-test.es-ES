---
title: Hola aaaUsing 1.0 de CLI de Azure con el almacenamiento de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola interfaz de línea de comandos de Azure (CLI de Azure) 1.0 con toocreate de almacenamiento de Azure y administrar cuentas de almacenamiento y trabajar con blobs de Azure y archivos. Hola CLI de Azure es una herramienta multiplataforma"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: 786f2be64875f5094f09fd6e4a47532889c3a82f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a>Uso de hello Azure CLI 1.0 con el almacenamiento de Azure

## <a name="overview"></a>Información general

Hola CLI de Azure proporciona un conjunto de código abierto, multiplataforma comandos para trabajar con hello plataforma de Azure. Proporciona gran parte de la misma funcionalidad que se encuentra en Hola de Hola [portal de Azure](https://portal.azure.com) datos enriquecidos, así como tener acceso a funcionalidad.

En esta guía, exploraremos cómo toouse [interfaz de línea de comandos de Azure (Azure CLI)](../cli-install-nodejs.md) tooperform una serie de tareas de desarrollo y la administración con el almacenamiento de Azure. Se recomienda descargar e instalar o actualizar toohello CLI de Azure más recientes antes de utilizar esta guía.

Esta guía se da por supuesto que comprende los conceptos básicos de hello del almacenamiento de Azure. Guía de Hello proporciona a una serie de secuencias de comandos toodemonstrate uso de Hola de hello CLI de Azure con el almacenamiento de Azure. Ser tooupdate seguro de las variables de script de Hola según la configuración antes de ejecutar cada script.

> [!NOTE]
> Guía de Hello proporciona ejemplos de comandos y secuencias de comandos de CLI de Azure de Hola para cuentas de almacenamiento clásicas. Vea [Using Hola CLI de Azure para Mac, Linux y Windows con administración de recursos de Azure](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) para comandos de CLI de Azure para las cuentas de almacenamiento de administrador de recursos.
>
>

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a>Introducción a almacenamiento de Azure y Azure CLI hello en 5 minutos
En esta guía se usa Ubuntu para los ejemplos, pero el funcionamiento debe ser similar en otros sistemas operativos.

**Nueva tooAzure:** obtener una suscripción de Microsoft Azure y una cuenta de Microsoft asociadas a esa suscripción. Para más información sobre las opciones de compra de Azure, consulte [Evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/), [Opciones de compra](https://azure.microsoft.com/pricing/purchase-options/) y [Ofertas para miembros](https://azure.microsoft.com/pricing/member-offers/) (para miembros de MSDN, Microsoft Partner Network, BizSpark y otros programas de Microsoft).

Para obtener más información sobre las suscripciones a Azure, consulte [Asignación de roles de administrador en Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) .

**Después de crear una suscripción y una cuenta de Microsoft Azure:**

1. Descargue e instale Hola CLI de Azure siguiendo las instrucciones de Hola que se describen en [Install hello Azure CLI](../cli-install-nodejs.md).
2. Una vez hello CLI de Azure se ha instalado, podrá toouse capaz de hello azure comando desde los comandos de CLI de Azure de interfaz de línea de comandos (intensiva de errores, Terminal, símbolo del sistema) tooaccess Hola. Hola de tipo _azure_ command y debería ver Hola después de salida.

    ![Resultado del comando de Azure][Image1]
3. En la interfaz de línea de comandos de hello, escriba `azure storage` toolist todas Hola comandos de almacenamiento de azure y obtener una primera impresión de Hola Hola de funcionalidades CLI de Azure proporciona. Puede escribir el nombre de comando con **-h** parámetro (por ejemplo, `azure storage share create -h`) toosee detalles de la sintaxis del comando.
4. Ahora, le ofreceremos una secuencia de comandos simple que muestra tooaccess de comandos de CLI de Azure básico almacenamiento de Azure. script de Hola le primero preguntará si tooset dos variables para la cuenta de almacenamiento y la clave. A continuación, Hola script creará un nuevo contenedor en esta nueva cuenta de almacenamiento y cargar un contenedor de toothat de archivo (blob) de imagen existente. Después de que el script de Hola enumera todos los blobs en ese contenedor, descargará Hola imagen archivo toohello directorio de destino que se encuentra en el equipo local de Hola.

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. En el equipo local, abra el editor de texto que desee (por ejemplo, vim). Escriba Hola por encima de la secuencia de comandos en el editor de texto.
6. Ahora, necesita las variables de script de Hola tooupdate basadas en las opciones de configuración.

   * **< Storage_account_name >** usar hello según el nombre de script de Hola o escriba un nombre nuevo para la cuenta de almacenamiento. **Importante:** Hola nombre de cuenta de almacenamiento de hello debe ser único en Azure. También debe estar en minúscula.
   * **< storage_account_key >** clave de acceso de saludo de la cuenta de almacenamiento.
   * **< Container_name >** usar hello según el nombre de script de Hola o escriba un nombre nuevo para el contenedor.
   * **< Image_to_upload >** escriba una imagen de tooa de ruta de acceso en el equipo local, como por ejemplo: "~ / images/HelloWorld.png".
   * **< Destination_folder >** ENTRAR archivos toostore en el directorio local de tooa de una ruta de acceso se descargan desde el almacenamiento de Azure, como: "~/downloadImages".
7. Después de actualizar las variables necesarias de hello en vim, presionar combinaciones de teclas `ESC`, `:`, `wq!` script de Hola toosave.
8. toorun esta secuencia de comandos, simplemente tipo hello script nombre de archivo en la consola de hello intensiva de errores. Después de ejecutar este script, debe tener una carpeta de destino local que incluye el archivo de imagen de hello descargado. Hola siguiente captura de pantalla muestra una salida de ejemplo:

Después de ejecutar el script de Hola, debe tener una carpeta de destino local que incluye el archivo de imagen de hello descargado.

## <a name="manage-storage-accounts-with-hello-azure-cli"></a>Administrar cuentas de almacenamiento con hello CLI de Azure
### <a name="connect-tooyour-azure-subscription"></a>Conectar tooyour suscripción de Azure
Mientras que la mayoría de los comandos de almacenamiento de hello funcionará sin una suscripción de Azure, le recomendamos que tooconnect tooyour suscripción de hello CLI de Azure. tooconfigure hello Azure CLI toowork con su suscripción, siga los pasos de hello en [conectarse tooan suscripción de Azure desde hello Azure CLI](../xplat-cli-connect.md).

### <a name="create-a-new-storage-account"></a>Creación de una cuenta de almacenamiento nueva
toouse almacenamiento de Azure, necesitará una cuenta de almacenamiento. Puede crear una nueva cuenta de almacenamiento de Azure después de haber configurado la suscripción de tooyour tooconnect de equipo.

```azurecli
azure storage account create <account_name>
```

nombre de Hello de la cuenta de almacenamiento debe tener entre 3 y 24 caracteres de longitud y usar números y letras en minúsculas solo.

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a>Establecimiento de una cuenta predeterminada de Almacenamiento de Azure en las variables de entorno
Puede tener varias cuentas de almacenamiento en su suscripción. Puede elegir uno de ellos y establecerla en hello las variables de entorno de comandos de todo el almacenamiento de Hola Hola misma sesión. Esto le permite toorun almacenamiento de Azure CLI Hola comandos sin especificar almacenamiento de hello cuenta y clave de forma explícita.

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

Otra manera tooset una cuenta de almacenamiento predeterminada está usando la cadena de conexión. En primer lugar obtener cadena de conexión de hello, comando:

```azurecli
azure storage account connectionstring show <account_name>
```

A continuación, copie la cadena de conexión de salida de hello y establézcalo tooenvironment variable:

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a>Creación y administración de blobs
Almacenamiento de blobs de Azure es un servicio para almacenar grandes cantidades de datos no estructurados, como texto o binario, que puede tener acceso desde cualquier lugar Hola mundo a través de HTTP o HTTPS. En esta sección se da por supuesto que ya está familiarizado con conceptos de almacenamiento de blobs de Azure Hola. Para más información, consulte [Introducción a Azure Blob Storage mediante .NET](storage-dotnet-how-to-use-blobs.md) y [Conceptos de Blob service](http://msdn.microsoft.com/library/azure/dd179376.aspx).

### <a name="create-a-container"></a>Crear un contenedor
Todos los blobs del almacenamiento de Azure han de estar en un contenedor. Puede crear un contenedor privado con hello `azure storage container create` comando:

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> Existen tres niveles de acceso de lectura anónimo: **Desactivado**, **Blob** y **Contenedor**. tooprevent anónimo tener acceso a tooblobs, parámetro del conjunto de permisos Hola demasiado**desactivar**. De forma predeterminada, el nuevo contenedor de hello es privado y son accesibles solo por el propietario de la cuenta de hello. público anónimo tooallow lee tooblob acceder a los recursos, pero no toocontainer metadatos o toohello lista de blobs en el contenedor de hello, establezca el parámetro de permiso de hello demasiado**Blob**. tooallow completa público de lectura tooblob acceder a los recursos, metadatos del contenedor y lista de Hola de blobs en el contenedor de Hola, establezca el parámetro de permiso de hello demasiado**contenedor**. Para obtener más información, consulte [administrar toocontainers de acceso de lectura anónimo y los blobs](storage-manage-access-to-resources.md).
>
>

### <a name="upload-a-blob-into-a-container"></a>Cargar un blob en un contenedor
El almacenamiento de blobs de Azure admite blobs en bloques y en páginas. Para más información, consulte [Descripción de los blobs en bloques, en anexos y en páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).

blobs tooupload tooa contenedor, puede usar hello `azure storage blob upload`. De forma predeterminada, este comando carga blob en bloques tooa Hola archivos locales. tipo de hello toospecify para blob hello, puede usar hello `--blobtype` parámetro.

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a>Descarga  de blobs de un contenedor
Hola siguiente ejemplo muestra cómo toodownload blobs de un contenedor.

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a>Copia de blobs
Los blobs se pueden copiar dentro de las cuentas de almacenamiento y regiones, o entre ellas, de forma asincrónica.

Hello en el ejemplo siguiente se muestra cómo toocopy blobs desde el almacenamiento de una cuenta tooanother. En este ejemplo crearemos un contenedor donde al que es posible acceder de forma pública y anónima a los blobs.

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

En este ejemplo se realiza una copia asincrónica. Puede supervisar el estado Hola de cada operación de copia ejecutando Hola `azure storage blob copy show` operación.

Tenga en cuenta que Hola dirección URL de origen proporcionado para la operación de copia de hello debe ser accesibles públicamente, o incluir un token SAS (firma de acceso compartido).

### <a name="delete-a-blob"></a>Eliminar un blob
toodelete un blob, use Hola comando siguiente:

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a>Creación y administración de recursos compartidos de archivos
Almacenamiento de archivos de Azure ofrece almacenamiento compartido para las aplicaciones que usan el protocolo SMB estándar de Hola. Los servicios en la nube y las máquinas virtuales de Microsoft Azure, así como las aplicaciones locales, pueden compartir datos de archivos a través de recursos compartidos montados. Puede administrar recursos compartidos de archivos y datos de archivos a través de hello CLI de Azure. Para obtener más información sobre el almacenamiento de archivos de Azure, consulte [Introducción al almacenamiento de archivos de Azure en Windows](storage-dotnet-how-to-use-files.md) o [cómo toouse almacenamiento de archivos de Azure con Linux](storage-how-to-use-files-linux.md).

### <a name="create-a-file-share"></a>Creación de un recurso compartido de archivos
Un recurso compartido de archivos de Azure es un recurso compartido de archivos de SMB en Azure. Todos los directorios y archivos se deben crear en un recurso compartido de archivos. Una cuenta puede contener un número ilimitado de recursos compartidos y un recurso compartido puede almacenar un número ilimitado de archivos, los límites de capacidad de toohello de cuenta de almacenamiento de Hola. Hello en el ejemplo siguiente se crea un recurso compartido de archivos denominado **MiRecursoCompartido**.

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a>Creación de directorios
Un directorio proporciona una estructura jerárquica opcional para los recursos compartidos de archivos de Azure. Hello en el ejemplo siguiente se crea un directorio denominado **myDir** en el recurso compartido de archivos de Hola.

```azurecli
azure storage directory create myshare myDir
```

Tenga en cuenta que la ruta de acceso al directorio puede incluir varios niveles, *p. ej.*, **a/b**. Pero debe asegurarse de que existen todos los directorios principales. Por ejemplo, para la ruta de acceso **a/b**, primero se debe crear el directorio **a** y luego el directorio **b**.

### <a name="upload-a-local-file-toodirectory"></a>Cargar un archivo local toodirectory
Hello en el ejemplo siguiente se carga un archivo de **~/temp/samplefile.txt** toohello **myDir** directory. Edite la ruta de acceso de archivo de Hola para que apunte tooa archivo válido en el equipo local:

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

Tenga en cuenta que puede ser un archivo en el recurso compartido de hello hasta too1 TB de tamaño.

### <a name="list-hello-files-in-hello-share-root-or-directory"></a>Enumerar archivos de hello en la raíz del recurso compartido de Hola o directorio
Puede enumerar Hola archivos y subdirectorios en una raíz de recurso compartido o un directorio mediante Hola siguiente comando:

```azurecli
azure storage file list myshare myDir
```

Tenga en cuenta que nombre del directorio hello es opcional para la operación de lista de Hola. Si se omite, comando hello muestra contenido de hello del directorio raíz de Hola de recurso compartido de Hola.

### <a name="copy-files"></a>Copiar archivos
A partir de la versión 0.9.8 de CLI de Azure, puede copiar un archivo de tooanother, un blob de tooa de archivo o un archivo de tooa de blob. A continuación se muestran cómo tooperform estas copian operaciones mediante comandos de CLI. toocopy un archivo toohello directorio:

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

toocopy un directorio de archivos de blob tooa:

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a>Pasos siguientes

Aquí puede encontrar la referencia a los comandos de la CLI de Azure 1.0 para trabajar con recursos de Storage:

* [Comandos de la CLI de Azure en el modo de Resource Manager](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [Comandos de la CLI de Azure en modo de Azure Service Management (asm)](../cli-install-nodejs.md)

También les gusta hello tootry [CLI de Azure 2.0](storage-azure-cli.md), nuestro CLI de próxima generación escrito en Python, para su uso con el modelo de implementación del Administrador de recursos de Hola.

[Image1]: ./media/storage-azure-cli/azure_command.png
