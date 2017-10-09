---
title: aaaCopy o mover datos tooAzure almacenamiento con AzCopy en Windows | Documentos de Microsoft
description: "Usar hello AzCopy en la utilidad de Windows a toomove o copia de la tooor de datos con el de blobs, tablas y contenido del archivo. Copiar datos tooAzure almacenamiento de archivos locales, o copiar datos dentro de o entre cuentas de almacenamiento. Migrar fácilmente el almacenamiento de datos tooAzure."
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
ms.date: 05/14/2017
ms.author: seguler
ms.openlocfilehash: a063a0380b7b8e6b212d0cec276f7d0f421936ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-azcopy-on-windows"></a>Transferencia de datos con hello AzCopy en Windows
AzCopy es una utilidad de línea de comandos diseñada para copiar datos tooand de almacenamiento de blobs de Microsoft Azure, el archivo y la tabla mediante comandos sencillos con un rendimiento óptimo. Puede copiar datos de una tooanother de objeto dentro de la cuenta de almacenamiento, o entre cuentas de almacenamiento.

Hay dos versiones de AzCopy que puede descargar. AzCopy en Windows está integrado en .NET Framework y ofrece opciones de línea de comandos de estilo Windows. [AzCopy en Linux](storage-use-azcopy-linux.md) está integrado en .NET Core Framework que tiene como destino plataformas Linux y ofrece opciones de línea de comandos de estilo POSIX. Este artículo trata sobre AzCopy en Windows.

## <a name="download-and-install-azcopy"></a>Descarga e instalación de AzCopy
### <a name="azcopy-on-windows"></a>AzCopy en Windows
Descargar hello [versión más reciente de AzCopy en Windows](http://aka.ms/downloadazcopy).

#### <a name="installation-on-windows"></a>Instalación en Windows
Después de instalar AzCopy en Windows con el instalador de hello, abra una ventana de comandos y desplácese toohello AzCopy directorio de instalación en el equipo, donde hello `AzCopy.exe` ejecutable se encuentra. Si lo desea, puede agregar hello AzCopy tooyour sistema ruta de instalación. De forma predeterminada, AzCopy se instala demasiado`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` o `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.

## <a name="writing-your-first-azcopy-command"></a>Escritura del primer comando de AzCopy
sintaxis básica de Hola para comandos de AzCopy es:

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

Hello en los ejemplos siguientes muestra una variedad de escenarios para copiar datos tooand de Blobs de Microsoft Azure, archivos y tablas. Consulte toohello [AzCopy parámetros](#azcopy-parameters) sección para obtener una explicación detallada de los parámetros de hello utilizadas en cada ejemplo.

## <a name="blob-download"></a>Blob: descarga
### <a name="download-single-blob"></a>Descarga de un solo blob

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

Tenga en cuenta que si carpeta hello `C:\myfolder` no existe, AzCopy crea y descarga `abc.txt ` en la nueva carpeta de Hola.

### <a name="download-single-blob-from-secondary-region"></a>Descarga de un solo blob desde la región secundaria

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Tenga en cuenta que debe tener almacenamiento con redundancia geográfica con acceso de lectura habilitado.

### <a name="download-all-blobs"></a>Descarga de todos los blobs

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

Suponga la siguiente Hola blobs residen en el contenedor especificado de hello:  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

Después de la operación de descarga de Hola Hola directory `C:\myfolder` incluye Hola siguientes archivos:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

Si no especifica la opción `/S`, no se descarga ningún blob.

### <a name="download-blobs-with-specified-prefix"></a>Descarga de blobs con el prefijo especificado

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

Suponga la siguiente Hola blobs residen en el contenedor especificado de Hola. Todos los blobs que comienzan con el prefijo de hello `a` se descargan:

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

Después de la operación de descarga de Hola Hola carpeta `C:\myfolder` incluye Hola siguientes archivos:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

prefijo de Hello aplica toohello directorio virtual, que forma Hola primera parte del nombre de blob de Hola. Ejemplo de Hola mostrado anteriormente, directorio virtual hello no coincide con el prefijo especificado de hello, por lo que no se descarga. Además, si hello opción `\S` no se especifica, AzCopy descargar los blobs.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>Establecer la hora de última modificación de Hola de los archivos exportados toobe igual que Hola blobs de origen

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

También puede excluir blobs de operación de descarga de hello según su hora de última modificación. Por ejemplo, si desea que los blobs tooexclude cuya hora de última modificación es hello igual o más reciente que el archivo de destino de hello, agregar hello `/XN` opción:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

O si desea que los blobs tooexclude cuya hora de última modificación es hello igual o anterior a archivo de destino de hello, agregue hello `/XO` opción:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a>Blob: carga
### <a name="upload-single-file"></a>Carga de un solo archivo

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

Si no existe el contenedor de destino especificado de hello, AzCopy lo crea y cargas Hola archivos en él.

### <a name="upload-single-file-toovirtual-directory"></a>Cargar archivo único directorio toovirtual

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

Si Hola especifica el directorio virtual no existe, se AzCopy carga Hola archivo tooinclude Hola directorio virtual en su nombre (*p. ej.*, `vd/abc.txt` en el ejemplo de Hola anterior).

### <a name="upload-all-files"></a>Carga de todos los archivos

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

Especificar la opción `/S` cargas Hola contenido de hello especificado directorios tooBlob almacenamiento de manera recursiva, lo que significa que todas las subcarpetas y sus archivos se cargan también. Por ejemplo, suponga el siguiente Hola archivos residen en la carpeta `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Después de la operación de carga de hello, contenedor Hola incluye Hola siguientes archivos:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Si no especifica la opción `/S`, AzCopy no realiza la carga de forma recursiva. Después de la operación de carga de hello, contenedor Hola incluye Hola siguientes archivos:

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a>Carga de archivos que coincidan con el patrón especificado

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

Suponga la siguiente Hola archivos residen en la carpeta `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Después de la operación de carga de hello, contenedor Hola incluye Hola siguientes archivos:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Si no especifica la opción `/S`, AzCopy solo carga los blobs que no residan en un directorio virtual:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>Especifique el tipo de contenido MIME de Hola de un blob de destino
De forma predeterminada, AzCopy establece tipo de contenido de Hola de un blob de destino demasiado`application/octet-stream`. A partir de la versión 3.1.0, puede especificar explícitamente Hola de tipo de contenido a través de la opción de hello `/SetContentType:[content-type]`. Esta sintaxis establece el tipo de contenido de Hola para todos los blobs en una operación de carga.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

Si especifica `/SetContentType` sin un valor, AzCopy establece cada blob o tipo de contenido del archivo según tooits extensión de archivo.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a>Blob: copia
### <a name="copy-single-blob-within-storage-account"></a>Copia de un solo blob dentro de una cuenta de almacenamiento

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

Cuando copia un blob dentro de una cuenta de almacenamiento, se realiza una operación de [copia del lado del servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) .

### <a name="copy-single-blob-across-storage-accounts"></a>Copia de un solo blob entre cuentas de almacenamiento

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

Cuando copia un blob entre cuentas de almacenamiento, se realiza una operación de [copia del lado del servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) .

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>Copiar blob único de una región secundaria tooprimary otra

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

Tenga en cuenta que debe tener almacenamiento con redundancia geográfica con acceso de lectura habilitado.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Copia de un solo blob y de sus instantáneas entre cuentas de almacenamiento

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

Después de la operación de copia de hello, contenedor de destino de hello incluye blob hello y sus instantáneas. Suponiendo que el blob de hello en el ejemplo de Hola anterior tiene dos instantáneas, el contenedor de hello incluye siguiente Hola blobs e instantáneas:

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Copia sincrónica de blobs entre cuentas de almacenamiento.
De forma predeterminada, AzCopy copia datos entre dos extremos de almacenamiento asincrónicamente. Por lo tanto, se copia la copia de hello operación se ejecuta en segundo plano de hello utilizando la capacidad de reserva de ancho de banda que no tenga ningún SLA en cuanto a la rapidez con que un blob y AzCopy comprueba periódicamente el estado de la copia de hello hasta que se copia Hola completado o no se pudo.

Hola `/SyncCopy` opción garantiza que la operación de copia de Hola obtiene velocidad coherente. AzCopy realiza copia sincrónica hello mediante la descarga de blobs de hello toocopy de hello especificado memoria toolocal de origen y, a continuación, cargarlos toohello destino de almacenamiento de blobs.

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

`/SyncCopy`puede generar salida adicional costo tooasynchronous comparados copia, hello enfoque recomendado es toouse esta opción en una máquina virtual de Azure que se encuentra en hello misma región que el costo de salida origen tooavoid de cuenta de almacenamiento.

## <a name="file-download"></a>Archivo: descarga
### <a name="download-single-file"></a>Descarga de un solo archivo

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Si no especifica Hola origen es un recurso compartido de archivos de Azure, o bien debe especificar el nombre exacto del archivo de hello, (*p. ej.* `abc.txt`) toodownload un solo archivo, o especificar la opción `/S` toodownload todos los archivos en el recurso compartido de Hola de forma recursiva. Intentar toospecify un patrón de archivo y la opción `/S` junto produce un error.

### <a name="download-all-files"></a>Descarga de todos los archivos

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

Tenga en cuenta que no se descarga ninguna carpeta vacía.

## <a name="file-upload"></a>Archivo: carga
### <a name="upload-single-file"></a>Carga de un solo archivo

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a>Carga de todos los archivos

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

Tenga en cuenta que no se carga ninguna carpeta vacía.

### <a name="upload-files-matching-specified-pattern"></a>Carga de archivos que coincidan con el patrón especificado

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a>Archivo: copia
### <a name="copy-across-file-shares"></a>Copia a través de recursos compartidos de archivos

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
Al copiar un archivo en distintos recursos compartidos de archivos, se realiza una operación de [copia del lado del servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-from-file-share-tooblob"></a>Copiar desde tooblob del recurso compartido de archivo

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
Al copiar un archivo de tooblob de recurso compartido de archivo, un [copia del lado servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) se realiza la operación.


### <a name="copy-from-blob-toofile-share"></a>Copiar desde el recurso compartido de blob toofile

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
Al copiar un archivo de recurso compartido de blob toofile, un [copia del lado servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) se realiza la operación.

### <a name="synchronously-copy-files"></a>Copia sincrónica de archivos
Puede especificar hello `/SyncCopy` opción toocopy datos de almacenamiento, del almacenamiento de archivos tooFile de almacenamiento de archivos tooBlob almacenamiento y de almacenamiento de blobs tooFile almacenamiento sincrónicamente, AzCopy hace esto mediante la descarga de memoria de toolocal de datos de origen de Hola y cargarlo nuevo toodestination. Se aplica el costo de salida estándar.

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

Cuando se copia desde el almacenamiento de archivos tooBlob almacenamiento, tipo de blob de hello predeterminado es blob en bloques, usuario puede especificar la opción `/BlobType:page` tipo de blob de destino de toochange Hola.

Tenga en cuenta que `/SyncCopy` podría generar salida adicional costo comparar copia tooasynchronous, hello enfoque recomendado es toouse esta opción en Hola VM de Azure que se encuentra en hello misma región que el costo de salida origen tooavoid de cuenta de almacenamiento.

## <a name="table-export"></a>Tabla: exportación
### <a name="export-table"></a>Tabla de exportación

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

AzCopy escribe una carpeta de destino especificado de toohello de archivo de manifiesto. archivo de manifiesto de Hola se utiliza en los archivos de datos necesarios de hello importación proceso toolocate hello y realizar la validación de datos. archivo de manifiesto de Hello usa Hola sigue la convención de nomenclatura de forma predeterminada:

    <account name>_<table name>_<timestamp>.manifest

Usuario también puede especificar la opción de hello `/Manifest:<manifest file name>` nombre de archivo de manifiesto de tooset Hola.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a>Exportación dividida en varios archivos

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

AzCopy utiliza un *índice de volumen* Hola dividir los datos de nombres de los archivos toodistinguish varios archivos. índice de volumen de Hello consta de dos partes, un *índice de intervalo de claves de partición* y un *división archivo índice*. Ambos índices se basan en 0.

índice de intervalo de claves de partición de Hello es 0 si el usuario de hello no especifica la opción `/PKRS`.

Por ejemplo, suponga que AzCopy genera dos archivos de datos después de que el usuario de hello especifica la opción de `/SplitSize`. Hola resultante nombres de archivo de datos podría ser:

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

Tenga en cuenta que Hola valor mínimo posible para la opción `/SplitSize` es 32 MB. Si Hola especifica el destino es el almacenamiento de blobs, AzCopy divide el archivo de datos de hello cuando su tamaño alcanza el límite de tamaño de blob de hello (200GB), con independencia de si la opción `/SplitSize` se ha especificado por el usuario de Hola.

### <a name="export-table-toojson-or-csv-data-file-format"></a>Formato de archivo de datos CSV o tooJSON de la tabla de exportación
AzCopy predeterminada exporta los archivos de datos de tablas tooJSON. También puede especificar la opción de hello `/PayloadFormat:JSON|CSV` tablas de hello tooexport como JSON o CSV.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

Al especificar el formato de carga de hello CSV, AzCopy también genera un archivo de esquema con la extensión `.schema.csv` para cada archivo de datos.

### <a name="export-table-entities-concurrently"></a>Exportación de entidades de tabla simultáneamente

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

AzCopy inicia las entidades de las operaciones simultáneas tooexport al usuario Hola especifica la opción `/PKRS`. Cada operación exporta un rango de claves de partición.

Tenga en cuenta que el número de Hola de operaciones simultáneas también se controla mediante la opción `/NC`. AzCopy utiliza el número de Hola de procesadores de núcleo como valor predeterminado de Hola de `/NC` cuando se copian las entidades de tabla, incluso si `/NC` no se especificó. Cuando el usuario de hello especifica la opción `/PKRS`, AzCopy usa Hola menor del número de Hola de hello dos valores - intervalos clave de partición frente a las operaciones simultáneas especificados de forma implícita o explícita - toodetermine de toostart de operaciones simultáneas. Para obtener más información, escriba `AzCopy /?:NC` en línea de comandos de Hola.

### <a name="export-table-tooblob"></a>Tooblob de la tabla de exportación

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

AzCopy genera un archivo de datos JSON en el contenedor de blobs de hello con las siguientes convención de nomenclatura:

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

archivo de datos JSON de Hello generado sigue el formato de carga de hello para la cantidad mínima de metadatos. Para obtener más información sobre el formato de carga, consulte [Formato de carga para las operaciones del servicio Tabla](http://msdn.microsoft.com/library/azure/dn535600.aspx).

Tenga en cuenta que cuando se exportan tablas tooblobs, AzCopy descargas de archivos de datos temporales de toolocal de las entidades de tabla de hello y, a continuación, carga los blob de toohello de entidades. Estos archivos de datos temporales se colocan en la carpeta de archivos de diario de hello con ruta de acceso de hello predeterminada "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", puede especificar la opción/Z: [carpeta de archivo diario] toochange Hola ubicación de carpeta del archivo de diario y, por tanto, cambiar la ubicación de archivos de datos temporales de Hola. Hello temporales tamaño del archivo se decide por tamaño y el tamaño de hello especificado con hello opción /SplitSize, las entidades de la tabla, aunque el archivo de datos temporales de hello en el disco local se elimina de forma instantánea una vez que ha sido cargado datos blob toohello, asegúrese de que tiene suficiente local disco toostore de espacio en estos archivos de datos temporal antes de que se eliminen.

## <a name="table-import"></a>Tabla: importación
### <a name="import-table"></a>Importación de la tabla

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

Hola opción `/EntityOperation` indica cómo tooinsert entidades en Hola tabla. Los valores posibles son:

* `InsertOrSkip`: Omite una entidad existente o inserta una nueva entidad si no existe en la tabla de Hola.
* `InsertOrMerge`: Combina una entidad existente o inserta una nueva entidad si no existe en la tabla de Hola.
* `InsertOrReplace`: Reemplaza una entidad existente o inserta una nueva entidad si no existe en la tabla de Hola.

Tenga en cuenta que no se puede especificar la opción `/PKRS` en escenario de importación de Hola. A diferencia del escenario de exportación de hello, en el que se debe especificar la opción `/PKRS` toostart operaciones simultáneas, AzCopy inicia las operaciones simultáneas de forma predeterminada cuando se importa una tabla. número predeterminado de Hola de operaciones simultáneas iniciado es toohello igual número de procesadores de núcleo; Sin embargo, puede especificar un número diferente de simultáneas con la opción `/NC`. Para obtener más información, escriba `AzCopy /?:NC` en línea de comandos de Hola.

Tenga en cuenta que AzCopy solo admite la importación de archivos con el formato JSON, no CSV. AzCopy no permite importar tablas de archivos de manifiesto y archivos JSON creados por los usuarios. Estos archivos deben proceder de una exportación de tablas de AzCopy. errores de tooavoid, no modifique Hola exporta JSON o archivo de manifiesto.

### <a name="import-entities-tootable-using-blobs"></a>Importar entidades tootable mediante blobs
Suponga que un contenedor de Blob contiene siguiente hello: archivo A JSON que representa una tabla de Azure y su archivo de manifiesto que lo acompaña.

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

Puede ejecutar Hola siguiendo las entidades de tooimport de comando en una tabla usando el archivo de manifiesto de hello en ese contenedor de blobs:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a>Otras características de AzCopy
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Sólo copia los datos que no existen en el destino de Hola
Hola `/XO` y `/XN` parámetros permiten tooexclude recursos de origen anterior o posterior que copien, respectivamente. Si solo desea toocopy recursos de origen que no existen en el destino de hello, puede especificar los dos parámetros en hello AzCopy comando:

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

Tenga en cuenta que esto no se admite cuando el origen de Hola o de destino es una tabla.

### <a name="use-a-response-file-toospecify-command-line-parameters"></a>Usar un parámetros de línea de comandos de toospecify de archivo de respuesta

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

Puede incluir cualquier parámetro de la línea de comandos de AzCopy en un archivo de respuesta. Procesos de AzCopy Hola parámetros en el archivo hello como si hubieran especificado en la línea de comandos de hello, realizar una sustitución directa con contenido de Hola de archivo hello.

Se supone un archivo de respuesta denominado `copyoperation.txt`, que contiene Hola siguiendo las líneas. Cada parámetro de AzCopy se puede especificar en una sola línea

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

o bien, en líneas independientes:

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

AzCopy se produce un error si parámetro hello se divide en dos líneas, como se muestra aquí para hello `/sourcekey` parámetro:

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a>Utilizar varios parámetros de línea de comandos de respuesta archivos toospecify
Imaginemos un archivo de respuesta llamado `source.txt` que especifica un contenedor de origen:

    /Source:http://myaccount.blob.core.windows.net/mycontainer

Y un archivo de respuesta denominado `dest.txt` que especifica una carpeta de destino en el sistema de archivos de hello:

    /Dest:C:\myfolder

Y un archivo de respuesta llamado `options.txt` que especifica opciones para AzCopy:

    /S /Y

toocall AzCopy con estos archivos de respuesta, que residen en un directorio `C:\responsefiles`, use este comando:

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

AzCopy procesa este comando tal como lo haría si incluye todos los parámetros individuales en la línea de comandos de Hola Hola:

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a>Especificación de una firma de acceso compartido (SAS)

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

También puede especificar una SAS en el contenedor de hello URI:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a>Carpeta de archivo de diario
Cada vez que se emite un tooAzCopy de comando, comprueba si existe un archivo de diario en la carpeta predeterminada de hello, o si se encuentra en una carpeta que especifica mediante esta opción. Si no existe el archivo de diario de Hola en cualquier lugar, AzCopy trata operación hello como nueva y genera un nuevo archivo de diario.

Si existe el archivo de diario de hello, AzCopy comprueba si línea de comandos de hello especificado coincide con hello de línea de comandos en el archivo de diario de Hola. Si coincide con dos líneas de comandos hello, AzCopy reanuda la operación incompleta de Hola. Si no coinciden, son tooeither solicitadas sobrescribir Hola diario archivo toostart una operación de nuevo o toocancel Hola operación actual.

Si desea que toouse Hola esta ubicación para el archivo de diario de hello:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

Si se omite la opción `/Z`, o especificar la opción `/Z` sin ruta de acceso de carpeta de hello, como se muestra arriba, AzCopy crea archivo diario de hello en la ubicación predeterminada de hello, que es `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`. Si ya existe un archivo de diario de hello, a continuación, AzCopy reanuda la operación de hello basado en archivo de diario de Hola.

Si desea que una ubicación personalizada para el archivo de diario de Hola toospecify:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

Este ejemplo crea el archivo de diario de hello si aún no existe. Si existe, a continuación, AzCopy reanuda la operación de hello basado en archivo de diario de Hola.

Si desea que una operación de AzCopy tooresume:

```azcopy
AzCopy /Z:C:\journalfolder\
```

Este ejemplo reanuda la operación última hello, que podría no haber toocomplete.

### <a name="generate-a-log-file"></a>Generación de un archivo de registro

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

Si se especifica opción `/V` sin proporcionar un registro detallado de archivo ruta de acceso toohello, a continuación, AzCopy crea archivos de registro de hello en la ubicación predeterminada de hello, que es `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.

De lo contrario, puede crear un archivo de registro en una ubicación personalizada:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

Tenga en cuenta que si especifica una ruta de acceso relativa siguiente opción `/V`, como `/V:test/azcopy1.log`, a continuación, se crea el registro detallado de hello en el directorio de trabajo actual de hello en una subcarpeta denominada `test`.

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Especificar número de Hola de operaciones simultáneas toostart
Opción `/NC` especifica Hola número de operaciones de copia simultáneas. De forma predeterminada, AzCopy inicia un número determinado de rendimiento de transferencia de datos de las operaciones simultáneas tooincrease Hola. Para las operaciones de tabla, el número de Hola de operaciones simultáneas es toohello igual número de procesadores de que disponga. Para operaciones de Blob y archivo, número de Hola de operaciones simultáneas es es igual 8 veces Hola número de procesadores de que disponga. Si está ejecutando AzCopy a través de una red de ancho de banda bajo, puede especificar un número menor para el parámetro/NC tooavoid error por competencia de recursos.

### <a name="run-azcopy-against-azure-storage-emulator"></a>Ejecución de AzCopy en el emulador de Almacenamiento de Azure
Puede ejecutar AzCopy contra Hola [emulador de almacenamiento de Azure](storage-use-emulator.md) para Blobs:

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

y tablas:

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a>Parámetros de AzCopy
A continuación se describen los parámetros para AzCopy. También puede escribir uno de los siguientes comandos de línea de comandos de Hola para Ayuda sobre el uso de AzCopy de hello:

* Para obtener ayuda detallada sobre la línea de comandos de AzCopy: `AzCopy /?`
* Para obtener ayuda detallada con algún parámetro de AzCopy: `AzCopy /?:SourceKey`
* Para obtener ejemplos de línea de comandos: `AzCopy /?:Samples`

### <a name="sourcesource"></a>/Source:"source"
Especifica los datos de origen de Hola de qué toocopy. Hola origen puede ser un directorio del sistema de archivos, un contenedor de blobs, un directorio virtual de blob, un recurso compartido de archivos de almacenamiento, un directorio de archivos de almacenamiento o una tabla de Azure.

**Aplicable a:** blobs, archivos, tablas

### <a name="destdestination"></a>/Dest:"destination"
Especifica Hola destino toocopy a. Hola destino puede ser un directorio del sistema de archivos, un contenedor de blobs, un directorio virtual de blob, un recurso compartido de archivos de almacenamiento, un directorio de archivos de almacenamiento o una tabla de Azure.

**Aplicable a:** blobs, archivos, tablas

### <a name="patternfile-pattern"></a>/Pattern:"file-pattern"
Especifica un patrón de archivo que indica qué toocopy de archivos. comportamiento de Hola de parámetro de hello /Pattern viene determinado por la ubicación Hola Hola de datos de origen y la presencia de Hola de opción de modo recursivo Hola. El modo recursivo viene especificado por la opción /S.

Si Hola especificado es un directorio en el sistema de archivos de hello, caracteres comodín estándar está en vigor, y proporcionar el patrón del archivo Hola se compara con los archivos contenidos en el directorio de Hola. Si está opción que se especifica/s., AzCopy, a continuación, también coincide con patrón especificado de hello en todos los archivos de las subcarpetas por debajo del directorio de Hola.

Si el origen especificado de hello es un contenedor de blob o directorio virtual, no se aplica caracteres comodín. Si la opción que se especifica/s., AzCopy, a continuación, interpreta el patrón de archivo especificado de Hola como un prefijo de blob. Si está opción que no se especifica/s., AzCopy, a continuación, coincide con patrón de archivo de hello con nombres de blob exacto.

Si no especifica Hola origen es un recurso compartido de archivos de Azure, debe especificar nombre de archivo exacto de hello, (p. ej. abc.txt) toocopy un solo archivo, o especificar opción /S toocopy todos los archivos de forma recursiva del recurso compartido de Hola. Se intentó una toospecify tanto un archivo patrón y la opción /S conjuntamente da como resultado un error.

AzCopy usa la coincidencia distingue mayúsculas de minúsculas al Hola/Source es un contenedor de blob o el directorio virtual de blob, y entre mayúsculas y minúsculas para búsqueda de coincidencias en todos los usos Hola otros casos.

Hola patrón de archivo predeterminado que usa cuando no se especifica ningún patrón de archivo es *.* para una ubicación del sistema de archivos, o un prefijo vacío para una ubicación de Almacenamiento de Azure. No se admite la especificación de varios patrones de archivos.

**Aplicable a:** blobs, archivos

### <a name="destkeystorage-key"></a>/DestKey:"storage-key"
Especifica la clave de cuenta de almacenamiento de hello para el recurso de destino de Hola.

**Aplicable a:** blobs, archivos, tablas

### <a name="destsassas-token"></a>/DestSAS:"sas-token"
Especifica una firma de acceso compartido (SAS) con permisos de lectura y escritura para el destino de hello (si procede). Rodear Hola SAS con comillas dobles, ya que puede contiene caracteres especiales de línea de comandos.

Si el recurso de destino de hello es un contenedor de blobs, el recurso compartido de archivos o la tabla, puede especificar esta opción seguida por el token de SAS de Hola o puede especificar Hola SAS como parte del contenedor de blob de destino de hello, el recurso compartido de archivos o el URI de la tabla, sin esta opción.

Si Hola origen y destino son ambos blobs, entonces blob de destino de hello debe residir dentro de hello misma cuenta de almacenamiento como blob de origen Hola.

**Aplicable a:** blobs, archivos, tablas

### <a name="sourcekeystorage-key"></a>/SourceKey:"storage-key"
Especifica la clave de cuenta de almacenamiento de hello para el recurso de código fuente de Hola.

**Aplicable a:** blobs, archivos, tablas

### <a name="sourcesassas-token"></a>/SourceSAS:"sas-token"
Especifica una firma de acceso compartido con permisos de lectura y lista para el origen de hello (si procede). Rodear Hola SAS con comillas dobles, ya que puede contiene caracteres especiales de línea de comandos.

Si el recurso de código fuente de hello es un contenedor de blob y se proporciona una clave ni una SAS, contenedor de blobs de Hola se lee mediante acceso anónimo.

Si el origen de hello es un recurso compartido de archivos o una tabla, se debe proporcionar una clave o una SAS.

**Aplicable a:** blobs, archivos, tablas

### <a name="s"></a>/S
Especifica el modo recursivo para operaciones de copia. En el modo recursivo, AzCopy copia todos los blobs o archivos que coinciden con el patrón de archivo especificado de hello, las de las subcarpetas incluidas.

**Aplicable a:** blobs, archivos

### <a name="blobtypeblock--page--append"></a>/BlobType:"block" | "page" | "append"
Especifica si el blob de destino de hello es un blob en bloques, un blob de página o un blob en anexos. Esta opción solo es aplicable cuando se carga un blob. De lo contrario, se producirá un error. Si el destino de hello es un blob y no se especifica esta opción, de forma predeterminada, AzCopy crea un blob en bloques.

**Aplicable a:** blobs

### <a name="checkmd5"></a>/CheckMD5
Calcula un hash MD5 para datos descargados y comprueba que el hash de MD5 de hello almacenados en el blob de Hola o la propiedad Content-MD5 del archivo coincide con hello calculado hash. comprobación de Hello MD5 está desactivada de forma predeterminada, por lo que debe especificar esta comprobación de opción tooperform Hola MD5 al descargar los datos.

Tenga en cuenta que el almacenamiento de Azure no garantiza que Hola hash MD5 almacenado para el blob de Hola o archivo está actualizado. Hola tooupdate de responsabilidad del cliente MD5 es cada vez que se modifica el blob de Hola o archivo.

AzCopy siempre establece propiedad Content-MD5 de Hola para un blob de Azure o un archivo después de cargarlo toohello servicio.  

**Aplicable a:** blobs, archivos

### <a name="snapshot"></a>/Snapshot
Indica si las instantáneas tootransfer. Esta opción solo es válida si el origen de hello es un blob.

Hello las instantáneas de blob transferidos se cambia el nombre en este formato: .extension de nombre de blob (hora de la instantánea)

De forma predeterminada, las instantáneas no se copian.

**Aplicable a:** blobs

### <a name="vverbose-log-file"></a>/V:[verbose-log-file]
Envía mensajes con el estado detallado a un archivo de registro.

De forma predeterminada, el archivo de registro detallado de Hola se denomina AzCopyVerbose.log en `%LocalAppData%\Microsoft\Azure\AzCopy`. Si especifica una ubicación de archivo existente para esta opción, registro detallado de hello es archivo toothat anexado.  

**Aplicable a:** blobs, archivos, tablas

### <a name="zjournal-file-folder"></a>/Z:[carpeta de archivos de diario]
Especifica una carpeta de archivos de diario para reanudar una operación.

AzCopy siempre admite la reanudación si una operación se ha interrumpido.

Si no se especifica esta opción, o se especifica sin una ruta de acceso de carpeta, AzCopy crea el archivo de diario de hello en la ubicación predeterminada de hello, que es % LocalAppData%\Microsoft\Azure\AzCopy.

Cada vez que se emite un tooAzCopy de comando, comprueba si existe un archivo de diario en la carpeta predeterminada de hello, o si se encuentra en una carpeta que especifica mediante esta opción. Si no existe el archivo de diario de Hola en cualquier lugar, AzCopy trata operación hello como nueva y genera un nuevo archivo de diario.

Si existe el archivo de diario de hello, AzCopy comprueba si línea de comandos de hello especificado coincide con hello de línea de comandos en el archivo de diario de Hola. Si coincide con dos líneas de comandos hello, AzCopy reanuda la operación incompleta de Hola. Si no coinciden, son tooeither solicitadas sobrescribir Hola diario archivo toostart una operación de nuevo o toocancel Hola operación actual.

archivo de diario de Hola se elimina tras la finalización correcta de operación de Hola.

Tenga en cuenta que la reanudación de una operación a partir de un archivo de diario creado por una versión anterior de AzCopy no se admite.

**Aplicable a:** blobs, archivos, tablas

### <a name="parameter-file"></a>/@:"parameter-file"
Especifica un archivo que contiene parámetros. Procesos de AzCopy Hola parámetros en el archivo hello como si se hubieran especificado en la línea de comandos de Hola.

En un archivo de respuesta, puede especificar varios parámetros en una sola línea o especificar cada parámetro en su propia línea. Tenga en cuenta que un parámetro individual no puede ocupar varias líneas.

Archivos de respuesta pueden incluir líneas de comentarios que comienzan por el símbolo # de Hola.

Puede especificar varios archivos de respuesta. Sin embargo, tenga en cuenta que AzCopy no admite archivos de respuesta anidados.

**Aplicable a:** blobs, archivos, tablas

### <a name="y"></a>/Y
Suprime todos los mensajes de confirmación de AzCopy.

**Aplicable a:** blobs, archivos, tablas

### <a name="l"></a>/L
Especifica solamente una operación de descripción; no se copian datos.

AzCopy interpreta Hola uso de esta opción como una simulación de línea de comandos de ejecución Hola sin esta opción /L y recuentos de cuántos objetos se copian, puede especificar opción /V al mismo tiempo toocheck qué objetos se copian en el registro detallado de Hola de Hola.

comportamiento de Hola de esta opción también viene determinado por la ubicación de Hola Hola de datos de origen y la presencia de Hola de hello recursiva modo /S y archivo patrón opción /Pattern.

AzCopy requiere el permiso LISTA y LECTURA de esta ubicación de origen cuando se usa esta opción.

**Aplicable a:** blobs, archivos

### <a name="mt"></a>/MT
Establece toobe Hola igual como blob de origen de Hola o del archivo de la hora de la última modificación del archivo descargado Hola.

**Aplicable a:** blobs, archivos

### <a name="xn"></a>/XN
Excluye un recurso origen más nuevo. Hello recursos no si se copian hora de última modificación del origen de Hola de hello es hello igual o más reciente que el destino.

**Aplicable a:** blobs, archivos

### <a name="xo"></a>/XO
Excluye un recurso de origen más antiguo. Hello recursos no si se copian hora de última modificación del origen de Hola de hello es hello igual o anterior a destino.

**Aplicable a:** blobs, archivos

### <a name="a"></a>/A
Carga sólo los archivos que tienen el atributo Archive de hello establecido.

**Aplicable a:** blobs, archivos

### <a name="iarashcnetoi"></a>/IA:[RASHCNETOI]
Solo los archivos de carga que contenga cualquiera de Hola especifican el conjunto de atributos.

Los atributos disponibles son los siguientes:

* R = Archivos de solo lectura
* A = Archivos listos para archivarse
* S = Archivos del sistema
* H = Archivos ocultos
* C = Archivos comprimidos
* N = Archivos normales
* E = Archivos cifrados
* T = Archivos temporales
* O = Archivos fuera de línea
* I = Archivos no indexados

**Aplicable a:** blobs, archivos

### <a name="xarashcnetoi"></a>/XA:[RASHCNETOI]
Excluye los archivos que contengan cualquiera de hello especificado establecido algún atributo.

Los atributos disponibles son los siguientes:

* R = Archivos de solo lectura
* A = Archivos listos para archivarse
* S = Archivos del sistema
* H = Archivos ocultos
* C = Archivos comprimidos
* N = Archivos normales
* E = Archivos cifrados
* T = Archivos temporales
* O = Archivos fuera de línea
* I = Archivos no indexados

**Aplicable a:** blobs, archivos

### <a name="delimiterdelimiter"></a>/Delimiter:"delimiter"
Indica el carácter de delimitador de hello usa toodelimit los directorios virtuales en un nombre de blob.

De forma predeterminada, AzCopy utiliza / como carácter de delimitador de Hola. Sin embargo, AzCopy admite el uso de cualquier carácter convencional (como @, # o %) como delimitador. Si necesita tooinclude uno de estos caracteres especiales en la línea de comandos de hello, ponga el nombre de archivo de hello entre comillas dobles.

Esta opción solamente se aplica para descarga de blobs.

**Aplicable a:** blobs

### <a name="ncnumber-of-concurrent-operations"></a>/NC:"number-of-concurrent-operations"
Especifica el número de Hola de operaciones simultáneas.

AzCopy forma predeterminada, inicia un número determinado de rendimiento de transferencia de datos de las operaciones simultáneas tooincrease Hola. Tenga en cuenta que gran número de operaciones simultáneas en un entorno de ancho de banda bajo puede saturar la conexión de red de Hola y evitar las operaciones de hello complete totalmente. Reduzca el número de operaciones simultáneas basándose en el ancho de banda de red disponible real.

límite superior de Hola para las operaciones simultáneas es 512.

**Aplicable a:** blobs, archivos, tablas

### <a name="sourcetypeblob--table"></a>/SourceType:"Blob" | "Table"
Especifica que hello `source` recurso es un blob disponible en el entorno de desarrollo local hello, ejecute en un emulador de almacenamiento de Hola.

**Aplicable a:** blobs, tablas

### <a name="desttypeblob--table"></a>/DestType:"Blob" | "Table"
Especifica que hello `destination` recurso es un blob disponible en el entorno de desarrollo local hello, ejecute en un emulador de almacenamiento de Hola.

**Aplicable a:** blobs, tablas

### <a name="pkrskey1key2key3"></a>/PKRS:"key1#key2#key3#..."
Divisiones Hola tooenable de intervalo de claves de partición exportar datos de la tabla en paralelo, lo que aumenta la velocidad de Hola de operación de exportación de Hola.

Si no se especifica esta opción, AzCopy utiliza un entidades de tabla de tooexport de subproceso único. Por ejemplo, si hello usuario especifica /PKRS: "aa #bb" y, a continuación, AzCopy inicia tres operaciones simultáneas.

Cada operación exporta uno de los tres rangos de claves de partición, como se muestra a continuación:

  [first-partition-key, aa)

  [aa, bb)

  [bb, last-partition-key]

**Aplicable a:** tablas

### <a name="splitsizefile-size"></a>/SplitSize:"file-size"
Especifica Hola archivo exportado dividir tamaño en MB, Hola valor mínimo permitido es de 32.

Si no se especifica esta opción, AzCopy exporta tooa de datos de tabla de archivos únicos.

Si datos de la tabla de hello están blob tooa exportado y tamaño del archivo exportado hello alcanza límite de 200 GB de hello para el tamaño del blob, AzCopy divide Hola archivo exportado, incluso si no se especifica esta opción.

**Aplicable a:** tablas

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a>/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"
Especifica el comportamiento de importación de datos de tabla de Hola.

* InsertOrSkip - omite una entidad existente o inserta una nueva entidad si no existe en la tabla de Hola.
* InsertOrMerge - combina una entidad existente o inserta una nueva entidad si no existe en la tabla de Hola.
* InsertOrReplace - reemplaza una entidad existente o inserta una nueva entidad si no existe en la tabla de Hola.

**Aplicable a:** tablas

### <a name="manifestmanifest-file"></a>/Manifest:"manifest-file"
Especifica el archivo de manifiesto de Hola para tabla Hola exportación e importación de operación.

Esta opción es opcional durante la operación de exportación de hello, AzCopy genera un archivo de manifiesto con nombre predefinido, si no se especifica esta opción.

Esta opción es necesaria durante la operación de importación de Hola para buscar archivos de datos de Hola.

**Aplicable a:** tablas

### <a name="synccopy"></a>/SyncCopy
Indica si toosynchronously copiar blobs o archivos entre dos extremos de almacenamiento de Azure.

De forma predeterminada, AzCopy usa la copia asincrónica del servidor. Especifique este tooperform opción sincrónica copy, que descarga de blobs o archivos toolocal memoria y, a continuación, carga tooAzure almacenamiento.

Puede usar esta opción cuando se copian archivos dentro del almacenamiento de blobs, almacenamiento de archivos, o desde Blob almacenamiento tooFile almacenamiento o viceversa.

**Aplicable a:** blobs, archivos

### <a name="setcontenttypecontent-type"></a>/SetContentType:"content-type"
Especifica el tipo de contenido MIME de Hola de blobs de destino o los archivos.

Conjuntos de AzCopy Hola de tipo de contenido para un blob o tooapplication/octet-stream de archivos de forma predeterminada. Puede establecer el tipo de contenido de Hola para todos los blobs o archivos especificando explícitamente un valor para esta opción.

Si se especifica esta opción sin ningún valor, AzCopy establece cada blob o tipo de contenido del archivo según tooits extensión de archivo.

**Aplicable a:** blobs, archivos

### <a name="payloadformatjson--csv"></a>/PayloadFormat:"JSON" | "CSV"
Especifica el formato de Hola Hola datos exportados del archivo de tabla.

Si no se especifica esta opción, de forma predeterminada, AzCopy exporta el archivo de datos de tabla en formato JSON.

**Aplicable a:** tablas

## <a name="known-issues-and-best-practices"></a>Problemas conocidos y prácticas recomendadas
### <a name="limit-concurrent-writes-while-copying-data"></a>Limitación de escrituras concurrentes mientras se copian datos
Cuando copia blobs o archivos con AzCopy, tenga en cuenta que otra aplicación puede modificar datos de hello mientras que va a copiar. Si es posible, asegúrese de que los datos de hello que va a copiar no se está modificando durante la operación de copia de Hola. Por ejemplo, al copiar un disco duro virtual asociado a una máquina virtual de Azure, asegúrese de que ninguna otra aplicación actualmente está escribiendo toohello disco duro virtual. Una buena manera toodo es mediante la concesión de hello recursos toobe copiado. Como alternativa, puede crear una instantánea de disco duro virtual de hello en primer lugar y, a continuación, copiar instantáneas Hola.

Si no se puede impedir que otras aplicaciones escribir tooblobs o archivos mientras se se copian y tenga en cuenta que al trabajo Hola Hola finaliza, hello recursos copiados pueden ya no tiene paridad completa con recursos de origen de Hola.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Ejecutar una instancia de AzCopy en un solo equipo.
AzCopy es toomaximize diseñada Hola utilización de la transferencia de datos de máquina recursos tooaccelerate hello, le recomendamos que ejecute solo una instancia de AzCopy en un equipo y especifica la opción de hello `/NC` si necesita las operaciones más simultáneas. Para obtener más información, escriba `AzCopy /?:NC` en línea de comandos de Hola.

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a>Habilitar algoritmos MD5 que cumplan con FIPS para AzCopy cuando "Use algoritmos que cumplen con FIPS para el cifrado, firma y operaciones hash".
AzCopy predeterminada usa hello toocalculate de implementación .NET MD5 MD5 al copiar los objetos, pero hay algunos requisitos de seguridad que necesitan AzCopy tooenable FIPS MD5 comprobar si es compatible.

Puede crear un archivo app.config `AzCopy.exe.config` con la propiedad `AzureStorageUseV1MD5` y separarlo con AzCopy.exe.

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

Para la propiedad "AzureStorageUseV1MD5" • True: valor predeterminado es hello AzCopy utiliza implementación MD5. NET.
• False: AzCopy utiliza el algoritmo MD5 compatible con FIPS.

Tenga en cuenta que los algoritmos compatibles con FIPS están deshabilitados de forma predeterminada en el equipo de Windows, puede escribir secpol.msc en la ventana de ejecución y comprobar este modificador en Configuración de seguridad -> Directivas locales -> Opciones de seguridad -> Criptografía de sistema: Usar algoritmos compatibles con FIPS para cifrado, firma y operaciones hash.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre el almacenamiento de Azure y AzCopy, vea Hola recursos siguientes:

### <a name="azure-storage-documentation"></a>Documentación de Almacenamiento de Azure:
* [Introducción tooAzure almacenamiento](../storage-introduction.md)
* [¿Cómo toouse almacenamiento de blobs en .NET](../blobs/storage-dotnet-how-to-use-blobs.md)
* [¿Cómo toouse almacenamiento de archivos de .NET](../storage-dotnet-how-to-use-files.md)
* [¿Cómo toouse almacenamiento de tablas de .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Cómo administrar toocreate, o eliminar una cuenta de almacenamiento](../storage-create-storage-account.md)
* [Transferencia de datos con AzCopy en Linux](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a>Publicaciones en blobs de Almacenamiento de Azure
* [Introducción a la versión de vista previa de la biblioteca de movimiento de datos de Almacenamiento de Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: Introducción a la copia sincrónica y el tipo de contenido personalizado](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: Presentación de la disponibilidad general de AzCopy 3.0 y de la versión de vista previa de AzCopy 4.0 compatible con tablas y archivos](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: Optimizada para escenarios de copia a gran escala](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: Compatibilidad para almacenamiento con redundancia geográfica de acceso de lectura](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy: Transferencia de datos con modo reiniciable y token SAS](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [AzCopy: Uso de copia de blobs entre cuentas](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: Carga y descarga de archivos para blobs de Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

