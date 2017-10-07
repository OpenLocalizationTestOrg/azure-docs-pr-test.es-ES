---
title: aaaCopy o mover datos tooAzure almacenamiento con AzCopy en Linux | Documentos de Microsoft
description: "Usar hello AzCopy en la utilidad de Linux a toomove o copia de la tooor de datos con el del contenido de blob y archivo. Copiar datos tooAzure almacenamiento de archivos locales, o copiar datos dentro de o entre cuentas de almacenamiento. Migrar fácilmente el almacenamiento de datos tooAzure."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: aa155738-7c69-4a83-94f8-b97af4461274
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: seguler
ms.openlocfilehash: ee39c311d996a046999b7fd4a4eb873f25b4eb86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a>Transferencia de datos con AzCopy en Linux
AzCopy en Linux es una utilidad de línea de comandos diseñada para copiar datos tooand de almacenamiento de blobs de Microsoft Azure y el archivo mediante comandos sencillos con un rendimiento óptimo. Puede copiar datos de una tooanother de objeto dentro de la cuenta de almacenamiento, o entre cuentas de almacenamiento.

Hay dos versiones de AzCopy que puede descargar. AzCopy en Linux se compila con .NET Core Framework, que tiene como destino plataformas Linux que ofrecen opciones de línea de comandos con estilo POSIX. [AzCopy en Windows](../storage-use-azcopy.md) se compila con .NET Framework y ofrece opciones de línea de comandos con estilo Windows. En este artículo se describe AzCopy en Linux.

## <a name="download-and-install-azcopy"></a>Descarga e instalación de AzCopy
### <a name="installation-on-linux"></a>Instalación en Linux

AzCopy en Linux requiere el marco de trabajo de .NET Core en la plataforma de Hola. Consulte las instrucciones de instalación de hello en hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) página.

Como ejemplo, instalemos .NET Core en Ubuntu 16.10. Para la Guía de instalación más reciente de hello, visite [.NET Core en Linux](https://www.microsoft.com/net/core#linuxubuntu) página de instalación.


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

Una vez que instale .NET Core, descargue e instale AzCopy.

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

Puede quitar archivos de hello extraída una vez instalado AzCopy en Linux. O bien si no tiene privilegios de superusuario, también puede ejecutar AzCopy mediante script de shell de hello 'azcopy' en la carpeta extraída de Hola. 

### <a name="alternative-installation-on-ubuntu"></a>Instalación alternativa en Ubuntu

**Ubuntu 14.04**

Agregue apt source para .NET Core:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Agregue apt source para el repositorio de productos de Linux para Microsoft e instale AzCopy:

```bash
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.04**

Agregue apt source para .NET Core:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Agregue apt source para el repositorio de productos de Linux para Microsoft e instale AzCopy:

```bash
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.10**

Agregue apt source para .NET Core:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Agregue apt source para el repositorio de productos de Linux para Microsoft e instale AzCopy:

```bash
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

## <a name="writing-your-first-azcopy-command"></a>Escritura del primer comando de AzCopy
sintaxis básica de Hola para comandos de AzCopy es:

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

Hello en los ejemplos siguientes muestra varios escenarios para copiar datos tooand de Blobs de Microsoft Azure y los archivos. Consulte toohello `azcopy --help` menú para obtener una explicación detallada de los parámetros de hello utilizadas en cada ejemplo.

## <a name="blob-download"></a>Blob: descarga
### <a name="download-single-blob"></a>Descarga de un solo blob

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Si carpeta hello `/mnt/myfiles` no existe, AzCopy lo crea y descarga `abc.txt ` en la nueva carpeta de Hola.

### <a name="download-single-blob-from-secondary-region"></a>Descarga de un solo blob desde la región secundaria

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Tenga en cuenta que debe tener almacenamiento con redundancia geográfica con acceso de lectura habilitado.

### <a name="download-all-blobs"></a>Descarga de todos los blobs

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Suponga la siguiente Hola blobs residen en el contenedor especificado de hello:  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

Después de la operación de descarga de Hola Hola directory `/mnt/myfiles` incluye Hola siguientes archivos:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

Si no especifica la opción `--recursive`, no se descargará ningún blob.

### <a name="download-blobs-with-specified-prefix"></a>Descarga de blobs con el prefijo especificado

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

Suponga la siguiente Hola blobs residen en el contenedor especificado de Hola. Todos los blobs que comienzan con el prefijo de hello `a` se descargan.

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

Después de la operación de descarga de Hola Hola carpeta `/mnt/myfiles` incluye Hola siguientes archivos:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

prefijo de Hello aplica toohello directorio virtual, que forma Hola primera parte del nombre de blob de Hola. Ejemplo de Hola mostrado anteriormente, directorio virtual hello no coincide con el prefijo especificado de hello, por lo que no se descarga ningún blob. Además, si hello opción `--recursive` no se especifica, AzCopy descargar los blobs.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>Establecer la hora de última modificación de Hola de los archivos exportados toobe igual que Hola blobs de origen

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

También puede excluir blobs de operación de descarga de hello según su hora de última modificación. Por ejemplo, si desea que los blobs tooexclude cuya hora de última modificación es hello igual o más reciente que el archivo de destino de hello, agregar hello `--exclude-newer` opción:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

O si desea que los blobs tooexclude cuya hora de última modificación es hello igual o anterior a archivo de destino de hello, agregue hello `--exclude-older` opción:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a>Blob: carga
### <a name="upload-single-file"></a>Carga de un solo archivo

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Si no existe el contenedor de destino especificado de hello, AzCopy lo crea y cargas Hola archivos en él.

### <a name="upload-single-file-toovirtual-directory"></a>Cargar archivo único directorio toovirtual

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Si Hola especifica el directorio virtual no existe, se AzCopy carga Hola archivo tooinclude Hola directorio virtual en el nombre del blob de hello (*p. ej.*, `vd/abc.txt` en el ejemplo de Hola anterior).

### <a name="upload-all-files"></a>Carga de todos los archivos

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

Especificar la opción `--recursive` cargas Hola contenido de hello especificado directorios tooBlob almacenamiento de manera recursiva, lo que significa que todas las subcarpetas y sus archivos se cargan también. Por ejemplo, suponga el siguiente Hola archivos residen en la carpeta `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Después de la operación de carga de hello, contenedor Hola incluye Hola siguientes archivos:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Hola cuando la opción `--recursive` no se especifica, solo hello siguientes tres archivos se cargan:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a>Carga de archivos que coincidan con el patrón especificado

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

Suponga la siguiente Hola archivos residen en la carpeta `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Después de la operación de carga de hello, contenedor Hola incluye Hola siguientes archivos:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Hola cuando la opción `--recursive` no se especifica, AzCopy omite los archivos que están en subdirectorios:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>Especifique el tipo de contenido MIME de Hola de un blob de destino
De forma predeterminada, AzCopy establece tipo de contenido de Hola de un blob de destino demasiado`application/octet-stream`. Sin embargo, puede especificar explícitamente los tipo de contenido de Hola a través de la opción de hello `--set-content-type [content-type]`. Esta sintaxis establece el tipo de contenido de Hola para todos los blobs en una operación de carga.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

Si hello opción `--set-content-type` se especifica sin un valor, AzCopy establece cada blob o el archivo del tipo de contenido según tooits extensión de archivo.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a>Blob: copia
### <a name="copy-single-blob-within-storage-account"></a>Copia de un solo blob dentro de una cuenta de almacenamiento

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

Cuando copia un blob sin la opción --syn-copy, se realiza una operación de [copia de lado servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-single-blob-across-storage-accounts"></a>Copia de un solo blob entre cuentas de almacenamiento

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

Cuando copia un blob sin la opción --syn-copy, se realiza una operación de [copia de lado servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>Copiar blob único de una región secundaria tooprimary otra

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

Tenga en cuenta que debe tener almacenamiento con redundancia geográfica con acceso de lectura habilitado.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Copia de un solo blob y de sus instantáneas entre cuentas de almacenamiento

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

Después de la operación de copia de hello, contenedor de destino de hello incluye blob hello y sus instantáneas. Hello contenedor incluye siguiente Hola blob y sus instantáneas:

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Copia sincrónica de blobs entre cuentas de almacenamiento.
De forma predeterminada, AzCopy copia datos entre dos extremos de almacenamiento asincrónicamente. Por lo tanto, se copia la copia de hello operación se ejecuta en segundo plano de hello utilizando la capacidad de reserva de ancho de banda que no tenga ningún SLA en cuanto a la rapidez con que un blob. 

Hola `--sync-copy` opción garantiza que la operación de copia de Hola obtiene velocidad coherente. AzCopy realiza copia sincrónica hello mediante la descarga de blobs de hello toocopy de hello especificado memoria toolocal de origen y, a continuación, cargarlos toohello destino de almacenamiento de blobs.

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

`--sync-copy`puede generar una salida adicional en comparación con el costo tooasynchronous copia. Hola enfoque recomendado es toouse esta opción en una máquina virtual de Azure, que se encuentra en hello misma región que el costo de salida origen tooavoid de cuenta de almacenamiento.

## <a name="file-download"></a>Archivo: descarga
### <a name="download-single-file"></a>Descarga de un solo archivo

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Si no especifica Hola origen es un recurso compartido de archivos de Azure, o bien debe especificar el nombre exacto del archivo de hello, (*p. ej.* `abc.txt`) toodownload un solo archivo, o especificar la opción `--recursive` toodownload todos los archivos en el recurso compartido de Hola de forma recursiva. Intentar toospecify un patrón de archivo y la opción `--recursive` junto produce un error.

### <a name="download-all-files"></a>Descarga de todos los archivos

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Tenga en cuenta que no se descarga ninguna carpeta vacía.

## <a name="file-upload"></a>Archivo: carga
### <a name="upload-single-file"></a>Carga de un solo archivo

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a>Carga de todos los archivos

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

Tenga en cuenta que no se carga ninguna carpeta vacía.

### <a name="upload-files-matching-specified-pattern"></a>Carga de archivos que coincidan con el patrón especificado

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a>Archivo: copia
### <a name="copy-across-file-shares"></a>Copia a través de recursos compartidos de archivos

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Al copiar un archivo en distintos recursos compartidos de archivos, se realiza una operación de [copia del lado del servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-from-file-share-tooblob"></a>Copiar desde tooblob del recurso compartido de archivo

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Al copiar un archivo de tooblob de recurso compartido de archivo, un [copia del lado servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) se realiza la operación.

### <a name="copy-from-blob-toofile-share"></a>Copiar desde el recurso compartido de blob toofile

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Al copiar un archivo de recurso compartido de blob toofile, un [copia del lado servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) se realiza la operación.

### <a name="synchronously-copy-files"></a>Copia sincrónica de archivos
Puede especificar hello `--sync-copy` opción toocopy datos de almacenamiento de archivos tooFile almacenamiento, de almacenamiento de archivos tooBlob almacenamiento y de almacenamiento de blobs tooFile almacenamiento de forma sincrónica. AzCopy ejecuta esta operación, se descargan de memoria de toolocal de datos de origen de hello y, a continuación, cargarlo toodestination. En este caso, se aplica el costo de salida estándar.

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

Cuando se copia desde el almacenamiento de archivos tooBlob almacenamiento, tipo de blob de hello predeterminado es blob en bloques, usuario puede especificar la opción `/BlobType:page` tipo de blob de destino de toochange Hola.

Tenga en cuenta que `--sync-copy` podría generar salida adicional costo comparar copia tooasynchronous. Hola enfoque recomendado es toouse esta opción en una máquina virtual de Azure, que se encuentra en hello misma región que el costo de salida origen tooavoid de cuenta de almacenamiento.

## <a name="other-azcopy-features"></a>Otras características de AzCopy
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Sólo copia los datos que no existen en el destino de Hola
Hola `--exclude-older` y `--exclude-newer` parámetros permiten tooexclude recursos de origen anterior o posterior que copien, respectivamente. Si solo desea toocopy recursos de origen que no existen en el destino de hello, puede especificar los dos parámetros en hello AzCopy comando:

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a>Usar un parámetros de línea de comandos de toospecify de archivo de configuración

```azcopy
azcopy --config-file "azcopy-config.ini"
```

Puede incluir cualquier parámetro de la línea de comandos de AzCopy en un archivo de configuración. Procesos de AzCopy Hola parámetros en el archivo hello como si hubieran especificado en la línea de comandos de hello, realizar una sustitución directa con contenido de Hola de archivo hello.

Se supone un archivo de configuración denominado `copyoperation`, que contiene Hola siguiendo las líneas. Cada parámetro de AzCopy se puede especificar en una sola línea.

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

o bien, en líneas independientes:

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

AzCopy se produce un error si parámetro hello se divide en dos líneas, como se muestra aquí para hello `--source-key` parámetro:

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a>Especificación de una firma de acceso compartido (SAS)

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

También puede especificar una SAS en el contenedor de hello URI:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

Tenga en cuenta que AzCopy actualmente sólo admite hello [cuenta SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).

### <a name="journal-file-folder"></a>Carpeta de archivo de diario
Cada vez que se emite un tooAzCopy de comando, comprueba si existe un archivo de diario en la carpeta predeterminada de hello, o si se encuentra en una carpeta que especifica mediante esta opción. Si no existe el archivo de diario de Hola en cualquier lugar, AzCopy trata operación hello como nueva y genera un nuevo archivo de diario.

Si existe el archivo de diario de hello, AzCopy comprueba si línea de comandos de hello especificado coincide con hello de línea de comandos en el archivo de diario de Hola. Si coincide con dos líneas de comandos hello, AzCopy reanuda la operación incompleta de Hola. Si no coinciden, AzCopy solicita diario archivo toostart una nueva operación de usuario tooeither sobrescribir Hola o toocancel operación en curso Hola.

Si desea que toouse Hola esta ubicación para el archivo de diario de hello:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

Si se omite la opción `--resume`, o especificar la opción `--resume` sin ruta de acceso de carpeta de hello, como se muestra arriba, AzCopy crea archivo diario de hello en la ubicación predeterminada de hello, que es `~\Microsoft\Azure\AzCopy`. Si ya existe un archivo de diario de hello, a continuación, AzCopy reanuda la operación de hello basado en archivo de diario de Hola.

Si desea que una ubicación personalizada para el archivo de diario de Hola toospecify:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

Este ejemplo crea el archivo de diario de hello si aún no existe. Si existe, a continuación, AzCopy reanuda la operación de hello basado en archivo de diario de Hola.

Si desea que una operación de AzCopy tooresume, repita Hola mismo comando. AzCopy en Linux le pedirá confirmación:

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a>Registros detallados de salida

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Especificar número de Hola de operaciones simultáneas toostart
Opción `--parallel-level` especifica Hola número de operaciones de copia simultáneas. De forma predeterminada, AzCopy inicia un número determinado de rendimiento de transferencia de datos de las operaciones simultáneas tooincrease Hola. Hola número de operaciones simultáneas es igual ocho veces Hola número de procesadores de que disponga. Si está ejecutando AzCopy a través de una red de ancho de banda bajo, puede especificar un número menor para: error de tooavoid de nivel de paralelo causado por la competencia de recursos.

[!TIP]
>lista completa de hello tooview de parámetros de AzCopy, desproteger 'azcopy--ayuda' menú.

## <a name="known-issues-and-best-practices"></a>Problemas conocidos y procedimientos recomendados
### <a name="error-net-core-is-not-found-in-hello-system"></a>Error: No se encuentra .NET Core en sistema Hola.
Si se produce un error que indica que no está instalado .NET Core en sistema de hello, Hola binario de .NET Core de ruta de acceso toohello `dotnet` posible que falte.

En Ordenar tooaddress este problema, busque binario de .NET Core hello en el sistema de hello:
```bash
sudo find / -name dotnet
```

Esto devuelve Hola ruta de acceso toohello dotnet binario. 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

Ahora agregue esta variable de ruta de acceso de toohello de ruta de acceso. Para sudo, edite secure_path toocontain Hola ruta de acceso toohello dotnet binario:
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

En este ejemplo, la variable secure_path se lee de la siguiente manera:

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

Para el usuario actual de hello, editar.bash_profile/.profile tooinclude Hola ruta de acceso toohello dotnet binario en la variable de ruta de acceso 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

Compruebe que .NET Core ahora esté en PATH:
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a>Error al instalar AzCopy
Si encuentra problemas con la instalación de AzCopy, puede intentar toorun AzCopy mediante scripts de bash Hola Hola extraído `azcopy` carpeta.

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a>Limitación de escrituras concurrentes mientras se copian datos
Cuando copia blobs o archivos con AzCopy, tenga en cuenta que otra aplicación puede modificar datos de hello mientras que va a copiar. Si es posible, asegúrese de que los datos de hello que va a copiar no se está modificando durante la operación de copia de Hola. Por ejemplo, al copiar un disco duro virtual asociado a una máquina virtual de Azure, asegúrese de que ninguna otra aplicación actualmente está escribiendo toohello disco duro virtual. Una buena manera toodo es mediante la concesión de hello recursos toobe copiado. Como alternativa, puede crear una instantánea de disco duro virtual de hello en primer lugar y, a continuación, copiar instantáneas Hola.

Si no se puede impedir que otras aplicaciones escribir tooblobs o archivos mientras se se copian y tenga en cuenta que al trabajo Hola Hola finaliza, hello recursos copiados pueden ya no tiene paridad completa con recursos de origen de Hola.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Ejecutar una instancia de AzCopy en un solo equipo.
AzCopy es toomaximize diseñada Hola utilización de la transferencia de datos de máquina recursos tooaccelerate hello, le recomendamos que ejecute solo una instancia de AzCopy en un equipo y especifica la opción de hello `--parallel-level` si necesita las operaciones más simultáneas. Para obtener más información, escriba `AzCopy --help parallel-level` en línea de comandos de Hola.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre el almacenamiento de Azure y AzCopy, vea Hola recursos siguientes:

### <a name="azure-storage-documentation"></a>Documentación de Almacenamiento de Azure:
* [Introducción tooAzure almacenamiento](../storage-introduction.md)
* [crear una cuenta de almacenamiento](../storage-create-storage-account.md)
* [Administración de blobs con el Explorador de Storage](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [Uso de hello Azure CLI 2.0 con el almacenamiento de Azure](../storage-azure-cli.md)
* [¿Cómo toouse almacenamiento de blobs de C++](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [¿Cómo toouse almacenamiento de blobs desde Java](../blobs/storage-java-how-to-use-blob-storage.md)
* [¿Cómo toouse almacenamiento de blobs de Node.js](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [¿Cómo toouse almacenamiento de blobs de Python](../blobs/storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a>Publicaciones en blobs de Almacenamiento de Azure
* [Anuncio de AzCopy en Linux (versión preliminar)](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [Introducción a la versión de vista previa de la biblioteca de movimiento de datos de Almacenamiento de Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: Introducción a la copia sincrónica y el tipo de contenido personalizado](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: Presentación de la disponibilidad general de AzCopy 3.0 y de la versión de vista previa de AzCopy 4.0 compatible con tablas y archivos](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: Optimizada para escenarios de copia a gran escala](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: Compatibilidad para almacenamiento con redundancia geográfica de acceso de lectura](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy: Transferencia de datos con modo reiniciable y token SAS](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [AzCopy: Uso de copia de blobs entre cuentas](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: Carga y descarga de archivos para blobs de Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

