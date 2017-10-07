---
title: "trabajo - v1 de importación de unidades de disco duro de aaaPreparing para una importación y exportación de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo las unidades de disco duro de tooprepare mediante Hola WAImportExport v1 herramienta toocreate un trabajo de importación para el servicio de importación y exportación de Azure de Hola."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 3d818245-8b1b-4435-a41f-8e5ec1f194b2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 8803ac01b7c7a2ec2e3199231d7b4c04ceafd5a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>Preparación de unidades de disco duro para un trabajo de importación
tooprepare uno o más unidades de disco duro para un trabajo de importación, siga estos pasos:

-   Identificar Hola datos tooimport en hello servicio Blob

-   Identificar los directorios virtuales de destino y los blobs en hello servicio Blob

-   Determine cuántas unidades necesita

-   Copiar hello tooeach de datos de los discos duros

 Para un flujo de trabajo de ejemplo, vea [tooPrepare de flujo de trabajo de ejemplo unidades de disco duro para un trabajo de importación](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md).

## <a name="identify-hello-data-toobe-imported"></a>Identificar hello toobe de datos importado
 es toodetermine qué directorios Hello primer paso toocreating un trabajo de importación y archivos se van tooimport. Puede tratarse de una lista de directorios, una lista de archivos únicos o una combinación de ambos. Cuando se incluye un directorio, todos los archivos en el directorio de Hola y sus subdirectorios formarán parte del trabajo de importación de Hola.

> [!NOTE]
>  Puesto que subdirectorios son incluyen de forma recurrente, cuando se incluye un directorio primario, especifique sólo directorio principal de Hola. No especifique ninguno de los subdirectorios.
>
>  Actualmente, Hola herramienta de importación y exportación de Microsoft Azure tiene Hola siguiente limitación: si un directorio contiene más datos de un disco duro puede contener, directorio de hello necesita toobe divide en directorios más pequeños. Por ejemplo, si un directorio contiene 2,5 TB de datos y Hola capacidad del disco duro es de solo 2TB, deberá toobreak directorio de 2,5 TB de hello en directorios más pequeños. Esta limitación se solucionará en una versión posterior de la herramienta de Hola.

## <a name="identify-hello-destination-locations-in-hello-blob-service"></a>Identificar las ubicaciones de destino de hello en el servicio de blob de Hola
 Para cada directorio o archivo que se va a importar, debe tooidentify un directorio virtual de destino o un blob en hello servicio Blob de Azure. Utilizará estos destinos como entradas toohello herramienta de importación y exportación de Azure. Tenga en cuenta que los directorios deben delimitarse con caracteres de barra diagonal Hola "/".

 Hello en la tabla siguiente muestra algunos ejemplos de destinos de blob:

|Archivo o directorio de origen|Blob de destino o directorio virtual|
|------------------------------|-------------------------------------------|
|H:\Video|https://mystorageaccount.blob.core.windows.net/video|
|H:\Photo|https://mystorageaccount.blob.core.windows.net/photo|
|K:\Temp\FavoriteVideo.ISO|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO|
|\\\myshare\john\music|https://mystorageaccount.blob.core.windows.net/music|

## <a name="determine-how-many-drives-are-needed"></a>Determinación de cuántas unidades necesita
 A continuación, necesita toodetermine:

-   número de Hola de unidades de disco duro necesita datos de hello toostore.

-   directorios de Hello y/o archivos independientes que serán tooeach copiada de la unidad de disco duro.

 Asegúrese de que tiene número de Hola de unidades de disco duro que debe toostore datos de Hola para transferir.

## <a name="copy-data-tooyour-hard-drive"></a>Copiar la unidad de disco duro de tooyour de datos
 Esta sección describe cómo toocall Hola herramienta de importación y exportación de Azure toocopy su tooone de datos o más unidades de disco duro. Cada vez que se llama a Hola herramienta de importación y exportación de Azure, se crea un nuevo *copiar sesión*. Crear al menos una sesión de copia para cada unidad toowhich copiar datos; en algunos casos, puede que necesite más de una copia sesión toocopy todos de la unidad de toosingle de datos. Estas son algunas de las razones por las que puede que necesite varias sesiones de copia:

-   Debe crear una sesión de copia independiente para cada unidad en la que vaya a realizar una copia.

-   Una sesión de copia puede copiar un único directorio o una unidad de toohello único blob. Si va a copiar varios directorios, varios blobs o una combinación de ambos, deberá toocreate varias sesiones de copia.

-   Puede especificar propiedades y metadatos que se establecerá en blobs de hello importados como parte de un trabajo de importación. propiedades de Hola o metadatos que se especifican para una sesión de copia se aplicarán blobs tooall especificados por esa sesión de copia. Si desea toospecify diferentes propiedades o metadatos para algunos blobs, deberá toocreate un independiente que copie la sesión. Vea [establecer las propiedades y metadatos durante el proceso de importación de hello](storage-import-export-tool-setting-properties-metadata-import-v1.md)para obtener más información.

> [!NOTE]
>  Si tiene varios equipos que cumplan los requisitos de hello descritos en [Setting Up Hola herramienta de importación y exportación de Azure](storage-import-export-tool-setup-v1.md), puede copiar las unidades de disco duro de toomultiple de datos en paralelo mediante la ejecución de una instancia de esta herramienta en cada equipo.

 Para cada unidad de disco duro que prepare con hello herramienta de importación y exportación de Azure, herramienta de hello creará un solo archivo de diario. Necesitará los archivos de diario de Hola de todo el trabajo de importación de las unidades toocreate Hola. archivo de diario de Hello también puede ser usado tooresume preparación de unidad si se interrumpe la herramienta de Hola.

### <a name="azure-importexport-tool-syntax-for-an-import-job"></a>Sintaxis de la herramienta Azure Import/Export para un trabajo de importación
 unidades de tooprepare para un trabajo de importación, llame a Hola herramienta de importación y exportación de Azure con hello **PrepImport** comando. Los parámetros que se debe incluir depende de si esto es Hola primera sesión de copia, o una sesión de copia posteriores.

 primera sesión de copia de una unidad de Hello requiere alguna clave de cuenta de almacenamiento de parámetros adicionales toospecify Hola; letra de unidad de destino de Hello; Si Hola debe estar formateado; Si se debe cifrar la unidad de Hola y si es así, Hola clave de BitLocker; y el directorio de registro de hello. Aquí se muestra sintaxis Hola un toocopy de sesión de la copia inicial un directorio o un único archivo:

 **En primer lugar copie toocopy un único directorio de sesión**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **En primer lugar copie toocopy un único archivo de sesión**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 En sesiones de copia posteriores, no necesita parámetros iniciales de toospecify Hola. Aquí se muestra sintaxis Hola un toocopy de sesión de copia posteriores un directorio o un único archivo:

 **Las sesiones de copia posteriores toocopy un único directorio**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **Las sesiones de copia posteriores toocopy un único archivo**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

### <a name="parameters-for-hello-first-copy-session-for-a-hard-drive"></a>Parámetros de hello en primer lugar copie sesión para una unidad de disco duro
 Cada vez que ejecute archivos de toocopy de herramienta de importación y exportación de Azure de hello toohello unidad de disco duro, la herramienta de hello crea una sesión de copia. Cada sesión copia un único directorio o una unidad de disco duro de tooa de archivo único. estado de Hola de sesión de copia de Hola se escribe el archivo de diario de toohello. Si se interrumpe una sesión de copia (por ejemplo, debido a pérdida de energía del sistema de tooa), se puede reanudar ejecutar herramienta Hola de nuevo y especificando el archivo de diario de hello en línea de comandos de Hola.

> [!WARNING]
>  Si especifica hello **/formatea** parámetro hello primera sesión de copia, se formateará la unidad de Hola y se borrarán todos los datos en la unidad de Hola. Se recomienda que use solo unidades vacías para la sesión de copia.

 comando de Hola que se usa para hello primera sesión de copia para cada unidad de disco requiere parámetros diferentes que los comandos de Hola para sesiones de copia posteriores. Hello siguiente tabla enumera Hola parámetros adicionales que están disponibles para hello primera sesión de copia:

|Parámetro de línea de comandos|Descripción|
|-----------------------------|-----------------|
|**/sk:**&lt;ClaveCuentaAlmacenamiento\>|`Optional.`clave de cuenta de almacenamiento de Hola de hello almacenamiento cuenta toowhich Hola datos se hayan importado. Se debe incluir **/sk:**< StorageAccountKey\> o **/csas:**< ContainerSas\> en comando Hola.|
|**/csas:**&lt;SasContenedor\>|`Optional`. contenedor de Hello cuenta de almacenamiento SAS toouse tooimport datos toohello. Se debe incluir **/sk:**< StorageAccountKey\> o **/csas:**< ContainerSas\> en comando Hola.<br /><br /> valor de Hola para este parámetro debe comenzar con el nombre del contenedor de hello, seguido por un signo de interrogación (?) y el token SAS de Hola. Por ejemplo:<br /><br /> `mycontainer?sv=2014-02-14&sr=c&si=abcde&sig=LiqEmV%2Fs1LF4loC%2FJs9ZM91%2FkqfqHKhnz0JM6bqIqN0%3D&se=2014-11-20T23%3A54%3A14Z&sp=rwdl`<br /><br /> permisos de Hello, si se especifica en la dirección URL de Hola o en una directiva de acceso almacenada, deben incluir lectura, escritura y eliminación para trabajos de importación y lectura, escritura y lista de trabajos de exportación.<br /><br /> Cuando se especifica este parámetro, todos los toobe de blobs importar o exportar debe estar dentro de contenedor Hola especificado en la firma de acceso compartido de Hola.|
|**/t:**&lt;LetraUnidadDestino\>|`Required.`letra de unidad de Hola de unidad de disco duro de destino de Hola para sesión de copia actual hello, sin Hola finales dos puntos.|
|**/format**|`Optional.`Especifique este parámetro cuando la unidad de hello necesita toobe formato; en caso contrario, omitirlo. Antes de hello herramienta dé formato a la unidad de hello, se le solicitará confirmación de la consola. toosuppress Hola confirmación, especifique el parámetro/silentmode de Hola.|
|**/silentmode**|`Optional.`Especifique esta confirmación de hello toosuppress de parámetro para el formato de la unidad de destino de Hola.|
|**/encrypt**|`Optional.`Este parámetro se especifica cuando la unidad de hello aún no se ha cifrado con BitLocker y necesita toobe cifrada mediante la herramienta de Hola. Si la unidad de hello ya se ha cifrado con BitLocker, a continuación, omite este parámetro y especificar hello `/bk` parámetro, proporcionar la clave de BitLocker de hello existente.<br /><br /> Si especifica hello `/format` parámetro, a continuación, se debe especificar también hello `/encrypt` parámetro.|
|**/bk:**&lt;ClaveBitLocker\>|`Optional.`Si se ha especificado `/encrypt`, se omite este parámetro. Si `/encrypt` es se omite, se necesita toohave ya cifrada unidad Hola con BitLocker. Use esta clave de BitLocker de parámetro toospecify Hola. El cifrado de BitLocker es necesario en todos los discos duros para poder realizar trabajos de importación.|
|**/logdir:**&lt;DirectorioRegistro\>|`Optional.`directorio de registro de Hello especifica que un directorio toobe utiliza toostore los registros detallados, así como los archivos de manifiesto temporales. Si no se especifica, se utilizará el directorio actual de hello como directorio de registro de hello.|

### <a name="parameters-required-for-all-copy-sessions"></a>Parámetros requeridos para todas las sesiones de copia
 archivo de diario de Hello contiene el estado de Hola para todas las sesiones de copia de una unidad de disco duro. También contiene información de Hola Hola toocreate necesita importar el trabajo. Siempre debe especificar un archivo de diario al ejecutar Hola herramienta de importación y exportación de Azure, así como un identificador de sesión de copia:

|||
|-|-|
|Parámetro de línea de comandos|Descripción|
|**/j:**&lt;ArchivoDiario\>|`Required.`archivo de diario de toohello de ruta de acceso de Hola. Cada unidad debe tener exactamente un archivo de diario. Tenga en cuenta que ese archivo de diario de hello no debe residir en la unidad de destino de Hola. extensión de archivo de diario de Hello es `.jrn`.|
|**/id:**&lt;IdSesión\>|`Required.`Id. de sesión de Hello identifica una sesión de copia. Es utilizado tooensure recuperación precisa de una sesión de copia interrumpida. Archivos que se copian en una sesión de copia se almacenan en un directorio denominado Id. de sesión de hello en la unidad de destino de Hola.|

### <a name="parameters-for-copying-a-single-directory"></a>Parámetros para copiar un único directorio
 Al copiar un único directorio, se aplican siguientes Hola requeridos y parámetros opcionales:

|Parámetro de línea de comandos|Descripción|
|----------------------------|-----------------|
|**/srcdir:**&lt;DirectorioOrigen\>|`Required.`directorio de origen de Hola que contiene archivos toobe copia toohello unidad de destino. ruta de acceso de directorio de Hello debe ser una ruta de acceso absoluta (no una ruta de acceso relativa).|
|**/dstdir:**&lt;DirectorioVirtualBlobDestino\>|`Required.`Hola ruta de acceso toohello directorio virtual de destino en la cuenta de almacenamiento de Windows Azure. directorio virtual de Hello puede o no existir.<br /><br /> Puede especificar un contenedor o un prefijo de blob como `music/70s/`. directorio de destino Hello debe comenzar una con nombre de contenedor de hello, seguido por una barra diagonal "/" y puede incluir opcionalmente un directorio virtual de blob que termina por "/".<br /><br /> Cuando el contenedor de destino de hello es contenedor raíz de hello, debe especificar explícitamente contenedor raíz de hello, incluida Hola barra diagonal, como `$root/`. Puesto que no pueden incluir blobs bajo el contenedor raíz de Hola "/" en sus nombres, cualquier subdirectorio en el directorio de origen hello no se copiarán al directorio de destino de hello es el contenedor de raíz de Hola.<br /><br /> Ser toouse seguro de los nombres de contenedor válido al especificar los directorios virtuales de destino o blobs. Tenga en cuenta que los nombres de contenedor deben estar en minúsculas. Para más información sobre las reglas de nomenclatura de contenedores, consulte [Asignación de nombres y referencias a contenedores, blobs y metadatos](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).|
|**/Disposition:**&lt;rename&amp;#124;no-overwrite&amp;#124;overwrite&gt;|`Optional.`Especifica el comportamiento de hello cuando un blob con hello especifica la dirección ya existe. Los valores válidos para este parámetro son: `rename`, `no-overwrite` y `overwrite`. Tenga en cuenta que estos valores distinguen mayúsculas de minúsculas. Si se especifica ningún valor, valor predeterminado de hello es `rename`.<br /><br /> Hola valor especificado para este parámetro afecta a todos los archivos de hello en directorio de hello especificado por hello `/srcdir` parámetro.|
|**/BlobType:**&lt;BlockBlob&amp;#124;PageBlob&gt;|`Optional.`Especifica el tipo de blob de Hola para blobs de destino de Hola. Los valores válidos son: `BlockBlob` y `PageBlob`. Tenga en cuenta que estos valores distinguen mayúsculas de minúsculas. Si se especifica ningún valor, valor predeterminado de hello es `BlockBlob`.<br /><br /> En la mayoría de los casos, se recomienda `BlockBlob`. Si especifica `PageBlob`, longitud de Hola de cada archivo en el directorio de hello debe ser un múltiplo del tamaño de 512, Hola de una página para blobs en páginas.|
|**/PropertyFile:**&lt;PropertyFile\>|`Optional.`Archivo de propiedades de ruta de acceso toohello para blobs de destino de Hola. Para obtener más información, consulte [Formato de archivo de propiedades y metadatos del servicio Import/Export](storage-import-export-file-format-metadata-and-properties.md).|
|**/MetadataFile:**&lt;MetadataFile\>|`Optional.`Archivo de metadatos de ruta de acceso toohello para blobs de destino de Hola. Para obtener más información, consulte [Formato de archivo de propiedades y metadatos del servicio Import/Export](storage-import-export-file-format-metadata-and-properties.md).|

### <a name="parameters-for-copying-a-single-file"></a>Parámetros para copiar un único archivo
 Al copiar un único archivo, hello parámetros obligatorios y opcionales siguientes se aplican:

|Parámetro de línea de comandos|Descripción|
|----------------------------|-----------------|
|**/srcfile:**&lt;SourceFile\>|`Required.`Hola ruta de acceso completa toohello archivo toobe copiado. ruta de acceso de directorio de Hello debe ser una ruta de acceso absoluta (no una ruta de acceso relativa).|
|**/dstblob:**&lt;DestinationBlobPath\>|`Required.`blob de destino de Hello ruta de acceso toohello en la cuenta de almacenamiento de Windows Azure. blob de Hello puede o no existir.<br /><br /> Especificar nombre de blob empezando de hello con el nombre del contenedor de Hola. nombre de blob de Hello no puede comenzar con "/" o el nombre de cuenta de almacenamiento de Hola. Para más información sobre las reglas de nomenclatura de blobs, consulte [Asignación de nombres y referencias a contenedores, blobs y metadatos](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).<br /><br /> Cuando el contenedor de destino de hello es contenedor raíz de hello, debe especificar explícitamente `$root` como Hola contenedor, como `$root/sample.txt`. Tenga en cuenta que los blobs en el contenedor raíz de hello no puede incluir "/" en sus nombres.|
|**/Disposition:**&lt;rename&amp;#124;no-overwrite&amp;#124;overwrite&gt;|`Optional.`Especifica el comportamiento de hello cuando un blob con hello especifica la dirección ya existe. Los valores válidos para este parámetro son: `rename`, `no-overwrite` y `overwrite`. Tenga en cuenta que estos valores distinguen mayúsculas de minúsculas. Si se especifica ningún valor, valor predeterminado de hello es `rename`.|
|**/BlobType:**&lt;BlockBlob&amp;#124;PageBlob&gt;|`Optional.`Especifica el tipo de blob de Hola para blobs de destino de Hola. Los valores válidos son: `BlockBlob` y `PageBlob`. Tenga en cuenta que estos valores distinguen mayúsculas de minúsculas. Si se especifica ningún valor, valor predeterminado de hello es `BlockBlob`.<br /><br /> En la mayoría de los casos, se recomienda `BlockBlob`. Si especifica `PageBlob`, longitud de Hola de cada archivo en el directorio de hello debe ser un múltiplo del tamaño de 512, Hola de una página para blobs en páginas.|
|**/PropertyFile:**&lt;PropertyFile\>|`Optional.`Archivo de propiedades de ruta de acceso toohello para blobs de destino de Hola. Para obtener más información, consulte [Formato de archivo de propiedades y metadatos del servicio Import/Export](storage-import-export-file-format-metadata-and-properties.md).|
|**/MetadataFile:**&lt;MetadataFile\>|`Optional.`Archivo de metadatos de ruta de acceso toohello para blobs de destino de Hola. Para obtener más información, consulte [Formato de archivo de propiedades y metadatos del servicio Import/Export](storage-import-export-file-format-metadata-and-properties.md).|

### <a name="resuming-an-interrupted-copy-session"></a>Reanudación de una sesión de copia interrumpida
 Si se interrumpe una sesión de copia por alguna razón, puede reanudarla si ejecuta la herramienta de hello con solo archivo diario Hola especificado:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /ResumeSession
```

 Sesión de copia más reciente de solo hello, si finalizó de forma anómala, se puede reanudar.

> [!IMPORTANT]
>  Al reanudar una sesión de copia, no modifique los directorios y archivos de datos de origen de hello agregando o quitando los archivos.

### <a name="aborting-an-interrupted-copy-session"></a>Anulación de una sesión de copia interrumpida
 Si se interrumpe una sesión de copia y no es posible tooresume (por ejemplo, si un directorio de origen resultó inaccesible), debe anular Hola sesión actual para que puedan implementarse nuevas sesiones de copia y se pueden iniciar:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AbortSession
```

 Hola solo última sesión de copia si finalizó de forma anómala, puede anularse. Tenga en cuenta que no se puede anular Hola primera sesión de copia de una unidad. En su lugar, debe reiniciar la sesión de copia de hello con un nuevo archivo de diario.

## <a name="next-steps"></a>Pasos siguientes

* [Setting Up Hola herramienta de importación y exportación de Azure](storage-import-export-tool-setup-v1.md)
* [Proceso de importación de establecer las propiedades y metadatos durante Hola](storage-import-export-tool-setting-properties-metadata-import-v1.md)
* [Unidades de disco duro de tooprepare de flujo de trabajo y ejemplo de un trabajo de importación](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
* [Quick reference for frequently used commands for import jobs](storage-import-export-tool-quick-reference-v1.md) (Referencia rápida para comandos usados con frecuencia) 
* [Revisión del estado del trabajo con archivos de registro de copia](storage-import-export-tool-reviewing-job-status-v1.md)
* [Reparación de un trabajo de importación](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Reparación de un trabajo de exportación](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Solución de problemas de hello herramienta de importación y exportación de Azure](storage-import-export-tool-troubleshooting-v1.md)
