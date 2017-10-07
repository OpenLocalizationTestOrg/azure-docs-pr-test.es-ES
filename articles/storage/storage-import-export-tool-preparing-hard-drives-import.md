---
title: "trabajo de importación de unidades de disco duro de aaaPreparing para una importación y exportación de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo las unidades de disco duro de tooprepare mediante Hola WAImportExport herramienta toocreate un trabajo de importación para hello servicio de importación y exportación de Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: muralikk
ms.openlocfilehash: 3f247a9efee29da2d18140353edc9dd7103a0761
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>Preparación de unidades de disco duro para un trabajo de importación

Hola herramienta WAImportExport es Hola unidad herramienta de preparación y reparación que puede usar con hello [servicio de importación y exportación de Microsoft Azure](storage-import-export-service.md). Puede usar esta herramienta toocopy datos toohello unidades de disco duro va tooship tooan centro de datos de Azure. Cuando haya finalizado un trabajo de importación, puede usar esta herramienta toorepair los blobs que estaban dañados que falten o que entran en conflicto con otros blobs. Después de recibir las unidades de Hola de un trabajo de exportación completado, puede usar esta herramienta toorepair los archivos que estaban dañados o que faltan en las unidades de Hola. En este artículo, vamos allá en lugar de utilizar esta herramienta Hola.

## <a name="prerequisites"></a>Requisitos previos

### <a name="requirements-for-waimportexportexe"></a>Requisitos para WAImportExport.exe

- **Configuración de la máquina**
  - Windows 7, Windows Server 2008 R2 o un sistema operativo de Windows más reciente
  - Se debe instalar .NET framework 4. Vea [preguntas más frecuentes sobre](#faq) acerca de cómo toocheck si .net Framework está instalado en el equipo de Hola.
- **Clave de la cuenta de almacenamiento** -necesita al menos una de las claves de cuenta de Hola Hola cuenta de almacenamiento.

### <a name="preparing-disk-for-import-job"></a>Preparación del disco para el trabajo de importación

- **BitLocker:** BitLocker debe estar habilitado en la herramienta de hello máquina ejecución hello WAImportExport. Vea hello [preguntas más frecuentes sobre](#faq) para saber cómo tooenable BitLocker.
- **Discos** accesibles desde la máquina en la que se ejecuta la herramienta WAImportExport. Consulte las [preguntas más frecuentes](#faq) sobre la especificación del disco.
- **Archivos de código fuente** -archivos Hola piensa tooimport deben ser accesibles desde el equipo de copia de hello, independientemente de si están en un recurso compartido de red o una unidad de disco duro local.

### <a name="repairing-a-partially-failed-import-job"></a>Reparación de un trabajo de importación con errores

- **Copie el archivo de registro** que se genera cuando el servicio Azure Import/Export copia los datos entre la cuenta de almacenamiento y el disco. Se encuentra en la cuenta de almacenamiento de destino.

### <a name="repairing-a-partially-failed-export-job"></a>Reparación de un trabajo de exportación con errores

- **Copie el archivo de registro** que se genera cuando el servicio Azure Import/Export copia los datos entre la cuenta de almacenamiento y el disco. Se encuentra en la cuenta de almacenamiento de origen.
- **Archivo de manifiesto**: [opcional] se encuentra en la unidad exportada que devolvió Microsoft.

## <a name="download-and-install-waimportexport"></a>Descarga e instalación de WAImportExport

Descargar hello [versión más reciente de WAImportExport.exe](https://www.microsoft.com/download/details.aspx?id=55280). Extraiga el directorio de tooa contenido comprimido de hello en el equipo.

La siguiente tarea es toocreate archivos CSV.

## <a name="prepare-hello-dataset-csv-file"></a>Preparar el archivo CSV de hello dataset

### <a name="what-is-dataset-csv"></a>¿Qué es un archivo CSV de conjunto de datos?

Archivo DataSet CSV es valor de Hola de marca de /conjunto de datos es un archivo CSV que contiene una lista de directorios o una lista de archivos copiado de toobe tootarget unidades. es toodetermine qué directorios Hello primer paso toocreating un trabajo de importación y archivos se van tooimport. Puede tratarse de una lista de directorios, una lista de archivos únicos o una combinación de ambos. Cuando se incluye un directorio, todos los archivos en el directorio de Hola y sus subdirectorios formarán parte del trabajo de importación de Hola.

Para cada directorio o archivo toobe importado, debe identificar un directorio virtual de destino o un blob en hello servicio Blob de Azure. Utilizará estos destinos como herramienta de entradas toohello WAImportExport. Los directorios deben delimitarse con caracteres de barra diagonal Hola "/".

Hello en la tabla siguiente muestra algunos ejemplos de destinos de blob:

| Archivo o directorio de origen | Blob de destino o directorio virtual |
| --- | --- |
| H:\Video | https://mystorageaccount.blob.core.windows.net/video |
| H:\Photo | https://mystorageaccount.blob.core.windows.net/photo |
| K:\Temp\FavoriteVideo.ISO | https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO |
| \\myshare\john\music | https://mystorageaccount.blob.core.windows.net/music |

### <a name="sample-datasetcsv"></a>Dataset.csv de ejemplo

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
"F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
"F:\50M_original\","containername/",BlockBlob,rename,"None",None
```

### <a name="dataset-csv-file-fields"></a>Campos del archivo CSV de conjunto de datos

| Campo | Descripción |
| --- | --- |
| BasePath | **[Obligatorio]**<br/>valor de Hola de este parámetro representa origen Hola donde se encuentra Hola datos toobe importado. herramienta de Hello va a copiar de forma recursiva todos los datos que se encuentran en esta ruta de acceso.<br><br/>**Valores permitidos**: Esto toobe no tiene una ruta de acceso válida en el equipo local o una ruta de acceso de recurso compartido válida y debe ser accesible para el usuario de Hola. ruta de acceso de directorio de Hello debe ser una ruta de acceso absoluta (no una ruta de acceso relativa). Si la ruta de acceso de hello termina con "\\", representa un directorio else finalice sin una ruta de acceso"\\" representa un archivo.<br/>No se permite ninguna expresión regular en este campo. Si la ruta de acceso de hello contiene espacios en blanco, colocarla en "".<br><br/>**Ejemplo**: "c:\Directory\c\Directory\File.txt"<br>"\\\\FBaseFilesharePath.domain.net\sharename\directory\"  |
| DstBlobPathOrPrefix | **[Obligatorio]**<br/> Hola ruta de acceso toohello directorio virtual de destino en la cuenta de almacenamiento de Windows Azure. directorio virtual de Hello puede o no existir. Si no existe, el servicio Import/Export creará uno.<br/><br/>Ser toouse seguro de los nombres de contenedor válido al especificar los directorios virtuales de destino o blobs. Tenga en cuenta que los nombres de contenedor deben estar en minúsculas. Para más información sobre las reglas de nomenclatura de contenedores, consulte [Asignación de nombres y referencias a contenedores, blobs y metadatos](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata). Si sólo se especifica la raíz, estructura de directorios de Hola de origen Hola se replica en el contenedor de blob de destino de Hola. Si se desea una estructura de directorios diferente que Hola de origen, varias filas de asignación en CSV<br/><br/>Puede especificar un contenedor o un prefijo de blob como music/70s/. directorio de destino Hello debe comenzar una con nombre de contenedor de hello, seguido por una barra diagonal "/" y puede incluir opcionalmente un directorio virtual de blob que termina por "/".<br/><br/>Cuando el contenedor de destino de hello es contenedor raíz de hello, debe especificar explícitamente contenedor raíz de hello, incluida Hola barra diagonal, como $root /. Puesto que no pueden incluir blobs bajo el contenedor raíz de Hola "/" en sus nombres, cualquier subdirectorio en el directorio de origen hello no se copiarán al directorio de destino de hello es el contenedor de raíz de Hola.<br/><br/>**Ejemplo**<br/>Si la ruta de acceso de blob de destino de hello es https://mystorageaccount.blob.core.windows.net/video, el valor de Hola de este campo puede ser vídeo /  |
| BlobType | **[Opcional]** block &amp;#124; page<br/>Actualmente el servicio Import/Export admite 2 tipos de blobs. Blobs en páginas y blobs en bloques. De forma predeterminada, todos los archivos se importarán como blobs en bloque. Y \*.vhd y \*.vhdx se importarán como Page BlobsThere constituye un límite en el blob en bloques de Hola y el tamaño permitido en el blob de página. Consulte [Objetivos de escalabilidad de Storage](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files) para más información.  |
| Disposition | **[Opcional]**  rename | no-overwrite | overwrite <br/> Este campo especifica el comportamiento de copia de Hola durante la importación sólo Cuando se están datos cargado toohello cuenta de almacenamiento del disco de Hola. Las opciones disponibles son: rename &#124; ¿desea sobrescribirla &#124; no sobrescribir. Los valores predeterminados demasiado "rename" Si no se especifica nada. <br/><br/>**Rename**: si hay un objeto con el mismo nombre, crea una copia en el destino.<br/>Sobrescribir: sobrescribe el archivo hello con archivo más reciente. archivo de Hello con wins de última modificación.<br/>**Sobrescribir no**: omite escribir Hola archivo si ya está presente.|
| MetadataFile | **[Opcional]** <br/>toothis campo de valor de Hello es el archivo de metadatos de Hola que puede concederse si Hola uno necesita toopreserve Hola metadatos de objetos de Hola o proporcionar metadatos personalizados. Archivo de metadatos de ruta de acceso toohello para blobs de destino de Hola. Para obtener más información, consulte [Formato de archivo de propiedades y metadatos del servicio Import/Export](storage-import-export-file-format-metadata-and-properties.md). |
| PropertiesFile | **[Opcional]** <br/>Archivo de propiedades de ruta de acceso toohello para blobs de destino de Hola. Para obtener más información, consulte [Formato de archivo de propiedades y metadatos del servicio Import/Export](storage-import-export-file-format-metadata-and-properties.md). |

## <a name="prepare-initialdriveset-or-additionaldriveset-csv-file"></a>Preparación del archivo CSV InitialDriveSet o AdditionalDriveSet

### <a name="what-is-driveset-csv"></a>¿Qué es el archivo CSV de conjunto de unidades?

Hello valor de marca de hello /InitialDriveSet o /AdditionalDriveSet es un archivo CSV que contiene la lista de Hola de discos toowhich hello las letras de unidad se asignan de manera que hello herramienta puede correctamente Hola una lista de selección toobe discos preparado. Si el tamaño de los datos hello es mayor que un tamaño de uno de los discos, herramienta de hello WAImportExport distribuirá datos hello en varios discos que se da de alta en este archivo CSV de forma optimizada.

No hay ningún límite del número de Hola de datos de saludo de discos se puede escribir tooin una sola sesión. herramienta de Hola encargará de distribuir datos basándose en el tamaño de disco y tamaño de la carpeta. Seleccionará el disco hello más optimizado para el tamaño del objeto de Hola. Hola datos cuando se cargan toohello cuenta de almacenamiento será la estructura de directorios de convergente toohello espera que se especificó en el archivo de conjunto de datos. En orden toocreate un driveset CSV, siga estos pasos Hola.

### <a name="create-basic-volume-and-assign-drive-letter"></a>Creación de volumen básico y asignación de letras de unidad

En Ordenar toocreate un volumen básico y asignar una letra de unidad, siga las instrucciones de Hola para "Creación de particiones más sencilla" de [Overview of Disk Management](https://technet.microsoft.com/library/cc754936.aspx).

### <a name="sample-initialdriveset-and-additionaldriveset-csv-file"></a>Archivos CSV InitialDriveSet o AdditionalDriveSet de ejemplo

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631
H,Format,SilentMode,Encrypt,
```

### <a name="driveset-csv-file-fields"></a>Campos del archivo CSV de conjunto de unidades

| Fields | Valor |
| --- | --- |
| DriveLetter | **[Obligatorio]**<br/> Cada unidad que se va a proporcionar toohello herramienta como destino de hello debe tener un volumen NTFS simple en él y una letra de unidad asignada tooit.<br/> <br/>**Ejemplo**: R o r |
| FormatOption | **[Obligatorio]**  Format | AlreadyFormatted<br/><br/> **Formato**: especificar esto dará formato a todos los datos de hello en el disco de Hola. <br/>**AlreadyFormatted**: herramienta de hello omitirá formato cuando se especifica este valor. |
| SilentOrPromptOnFormat | **[Obligatorio]**  SilentMode | PromptOnFormat<br/><br/>**SilentMode**: proporcionar este valor se habilitará la herramienta de hello toorun de usuario en modo silencioso. <br/>**PromptOnFormat**: herramienta de hello pedirá Hola usuario tooconfirm si realmente está pensado acción Hola a todos los formatos.<br/><br/>Si no se establece, el comando se anulará y mostrará el mensaje de error: "Incorrect value for SilentOrPromptOnFormat: none" (Valor incorrecto para SilentOrPromptOnFormat: ninguno) |
| Cifrado | **[Obligatorio]**  Encrypt | AlreadyEncrypted<br/> valor de Hola de este campo decide qué tooencrypt de disco y cuáles no. <br/><br/>**Cifrar**: herramienta formateará la unidad de Hola. Si el valor del campo "FormatOption" es "Format", a continuación, este valor es necesario toobe "Encrypt". Si se especifica "AlreadyEncrypted" en este caso, se producirá un error "When Format is specified, Encrypt must also be specified" (Si se especifica Format, también se debe especificar Encrypt).<br/>**AlreadyEncrypted**: herramienta descifrará unidad hello mediante hello BitLockerKey proporcionado en el campo "ExistingBitLockerKey". Si el valor del campo "FormatOption" es "AlreadyFormatted", este valor podrá ser "Encrypt" o "AlreadyEncrypted" |
| ExistingBitLockerKey | **[Obligatorio]**  Si el valor del campo "Encryption" es "AlreadyEncrypted"<br/> valor Hola de este campo es la clave de BitLocker de Hola que está asociado al disco concreto de Hola. <br/><br/>Este campo debe dejarse en blanco si el valor de Hola de campo de "Cifrado" es "Cifrar".  Si se especifica la clave de BitLocker en este caso, se producirá el error "Bitlocker Key should not be specified" (No se debe especificar la clave de Bitlocker).<br/>  **Ejemplo**: 060456-014509-132033-080300-252615-584177-672089-411631|

##  <a name="preparing-disk-for-import-job"></a>Preparación del disco para el trabajo de importación

unidades de tooprepare para un trabajo de importación, llame a la herramienta de WAImportExport de hello con hello **PrepImport** comando. Los parámetros que se debe incluir depende de si esto es Hola primera sesión de copia, o una sesión de copia posteriores.

### <a name="first-session"></a>Primera sesión

Primera sesión de copia tooCopy una herramienta de WAImportExport de disco (según lo especificado en el archivo CSV) de uno o varios Single/Multiple Directory tooa comando PrepImport para hello en primer lugar copie directorios de sesión toocopy o archivos con una nueva sesión de copia:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**Ejemplo:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:\*\*\*\*\*\*\*\*\*\*\*\*\* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

### <a name="add-data-in-subsequent-session"></a>Adición de datos en una sesión posterior

En sesiones de copia posteriores, no necesita parámetros iniciales de toospecify Hola. Necesita toouse Hola el mismo archivo de diario en orden para hello herramienta tooremember que dejan en hello sesión anterior. estado de Hola de sesión de copia de Hola se escribe el archivo de diario de toohello. Esta es Hola sintaxis para una copia posteriores directorios adicionales de sesión toocopy y o archivos:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<DifferentSessionId>  [DataSet:<differentdataset.csv>]
```

**Ejemplo:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

### <a name="add-drives-toolatest-session"></a>Agregar unidades toolatest sesión

Si los datos de hello no cabía en unidades especificadas en InitialDriveset, se pueden usar la sesión de copia de la toosame Hola herramienta tooadd unidades adicionales. 

>[!NOTE] 
>Id. de sesión de Hello debe coincidir con Id. de sesión anterior Hola. Archivo de diario debe coincidir con hello especificada en la sesión anterior.
>
```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AdditionalDriveSet:<newdriveset.csv>
```

**Ejemplo:**

```
WAImportExport.exe PrepImport /j:SameJournalTest.jrn /id:session#2  /AdditionalDriveSet:driveset-2.csv
```

### <a name="abort-hello-latest-session"></a>Anular Hola sesión más reciente:

Si se interrumpe una sesión de copia y no es posible tooresume (por ejemplo, si un directorio de origen resultó inaccesible), debe anular Hola sesión actual para que puedan implementarse nuevas sesiones de copia y se pueden iniciar:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AbortSession
```

**Ejemplo:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /AbortSession
```

Hola solo última sesión de copia si finalizó de forma anómala, puede anularse. Tenga en cuenta que no se puede anular Hola primera sesión de copia de una unidad. En su lugar, debe reiniciar la sesión de copia de hello con un nuevo archivo de diario.

### <a name="resume-a-latest-interrupted-session"></a>Reanudación de la última sesión interrumpida

Si se interrumpe una sesión de copia por alguna razón, puede reanudarla si ejecuta la herramienta de hello con solo archivo diario Hola especificado:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /ResumeSession
```

**Ejemplo:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /ResumeSession
```

> [!IMPORTANT] 
> Al reanudar una sesión de copia, no modifique los directorios y archivos de datos de origen de hello agregando o quitando los archivos.

## <a name="waimportexport-parameters"></a>Parámetros de WAImportExport

| Parámetros | Descripción |
| --- | --- |
|     /j:&lt;JournalFile&gt;  | **Obligatorio**<br/> Archivo de diario de toohello de ruta de acceso. Un archivo de journal realiza un seguimiento de un conjunto de unidades y registros Hola progreso en la preparación de estas unidades. archivo de diario de Hello siempre debe especificarse.  |
|     /logdir:&lt;LogDirectory&gt;  | **Opcional**. directorio de registro de Hello.<br/> Archivos de registro detallados, así como algunos archivos temporales se escribirán toothis directory. Si no se utilizará el directorio actual especificado como directorio de registro de hello. Hello directorio de registro se puede especificar una sola vez para hello mismo archivo diario.  |
|     /id:&lt;SessionId&gt;  | **Obligatorio**<br/> sesión de Hello que ID es tooidentify usa una sesión de copia. Es utilizado tooensure recuperación precisa de una sesión de copia interrumpida.  |
|     /ResumeSession  | Opcional. Si Hola última sesión de copia se terminó de forma anómala, este parámetro puede ser especificado tooresume Hola sesión.   |
|     /AbortSession  | Opcional. Si Hola última sesión de copia se terminó de forma anómala, este parámetro puede ser especificado tooabort Hola sesión.  |
|     /sn:&lt;StorageAccountName&gt;  | **Obligatorio**<br/> Solo es aplicable para RepairImport y RepairExport. nombre de Hola de cuenta de almacenamiento de Hola.  |
|     /sk:&lt;StorageAccountKey&gt;  | **Obligatorio**<br/> clave de Hola de cuenta de almacenamiento de Hola. |
|     /InitialDriveSet:&lt;driveset.csv&gt;  | **Necesario** cuando ejecuta Hola primera sesión de copia<br/> Un archivo CSV que contiene una lista de las unidades de tooprepare.  |
|     /AdditionalDriveSet:&lt;driveset.csv&gt; | **Obligatoria**. Al agregar la sesión de copia de toocurrent de unidades de disco. <br/> Un archivo CSV que contiene una lista de toobe unidades adicionales agregado.  |
|      /r:&lt;RepairFile&gt; | **Obligatorio** Solo es aplicable para RepairImport y RepairExport.<br/> Archivo toohello de ruta de acceso para el seguimiento del progreso de la reparación. Cada unidad debe tener un solo archivo de reparación.  |
|     /d:&lt;TargetDirectories&gt; | **Obligatoria**. Solo es aplicable para RepairImport y RepairExport. Para RepairImport, toorepair de uno o varios directorios separados por punto y coma; Para RepairExport, un directorio toorepair, p. ej. raíz del directorio de la unidad de Hola.  |
|     /CopyLogFile:&lt;DriveCopyLogFile&gt; | **Obligatorio** Solo es aplicable para RepairImport y RepairExport. Archivo de registro de copia de unidad de ruta de acceso toohello (detallado o error).  |
|     /ManifestFile:&lt;DriveManifestFile&gt; | **Obligatorio** Solo es aplicable para RepairExport.<br/> Archivo de manifiesto de ruta de acceso toohello unidad.  |
|     /PathMapFile:&lt;DrivePathMapFile&gt; | **Opcional**. Solo es aplicable para RepairImport.<br/> Ruta de acceso toohello archivo que contiene las asignaciones de archivo rutas de acceso relativas toohello unidad raíz toolocations de archivos reales (delimitado por tabulaciones). Cuando se especifica en primer lugar, se rellenará con las rutas de acceso de archivo con destinos vacíos, lo que significa que no se encuentran en TargetDirectories, se les ha denegado el acceso, tienen nombres no válidos o se encuentran en varios directorios. archivo de mapa de ruta de acceso de Hello puede tooinclude editada manualmente las rutas de acceso de destino correcta de Hola y especifica nuevo Hola herramienta tooresolve hello las rutas de acceso correctamente.  |
|     /ExportBlobListFile:&lt;ExportBlobListFile&gt; | **Obligatoria**. Solo se aplica para PreviewExport.<br/> Ruta de acceso toohello XML archivo que contiene una lista de rutas de acceso de blob o prefijos de ruta de acceso para hello blobs toobe exportado de blob. formato de archivo de Hello es Hola igual como formato de blob de lista de blob de Hola Hola operación Put Job de servicio de importación y exportación de hello API de REST.  |
|     /DriveSize:&lt;DriveSize&gt; | **Obligatoria**. Solo se aplica para PreviewExport.<br/>  Tamaño de toobe de unidades que se utiliza para la exportación. Por ejemplo, 500 GB; 1,5 TB. Nota: 1 GB = 1 000 000 000 bytes 1 TB = 1 000 000 000 000 bytes  |
|     /DataSet:&lt;dataset.csv&gt; | **Obligatorio**<br/> Un archivo CSV que contiene una lista de directorios o una lista de archivos toobe copia tootarget unidades.  |
|     /silentmode  | **Opcional**.<br/> Si no se especifica, le recordará Hola requisito de unidades y necesita su toocontinue de confirmación.  |

## <a name="tool-output"></a>Salida de la herramienta

### <a name="sample-drive-manifest-file"></a>Archivo de manifiesto de la unidad de ejemplo

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DriveManifest Version="2011-MM-DD">
   <Drive>
      <DriveId>drive-id</DriveId>
      <StorageAccountKey>storage-account-key</StorageAccountKey>
      <ClientCreator>client-creator</ClientCreator>
      <!-- First Blob List -->
      <BlobList Id="session#1-0">
         <!-- Global properties and metadata that applies tooall blobs -->
         <MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>
         <PropertiesPath Hash="md5-hash">global-properties-file-path</PropertiesPath>
         <!-- First Blob -->
         <Blob>
            <BlobPath>blob-path-relative-to-account</BlobPath>
            <FilePath>file-path-relative-to-transfer-disk</FilePath>
            <ClientData>client-data</ClientData>
            <Length>content-length</Length>
            <ImportDisposition>import-disposition</ImportDisposition>
            <!-- page-range-list-or-block-list -->
            <!-- page-range-list -->
            <PageRangeList>
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
            </PageRangeList>
            <!-- block-list -->
            <BlockList>
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
            </BlockList>
            <MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>
            <PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>
         </Blob>
      </BlobList>
   </Drive>
</DriveManifest>
```

### <a name="sample-journal-file-xml-for-each-drive"></a>Archivo de diario de ejemplo (XML) para cada unidad

```xml
[BeginUpdateRecord][2016/11/01 21:22:25.379][Type:ActivityRecord]
ActivityId: DriveInfo
DriveState: [BeginValue]
<?xml version="1.0" encoding="UTF-8"?>
<Drive>
   <DriveId>drive-id</DriveId>
   <BitLockerKey>*******</BitLockerKey>
   <ManifestFile>\DriveManifest.xml</ManifestFile>
   <ManifestHash>D863FE44F861AE0DA4DCEAEEFFCCCE68</ManifestHash> </Drive>
[EndValue]
SaveCommandOutput: Completed
[EndUpdateRecord]
```

### <a name="sample-journal-file-jrn-for-session-that-records-hello-trail-of-sessions"></a>Archivo de diario de ejemplo (JRN) para la sesión que registra el rastro de Hola de sesiones

```
[BeginUpdateRecord][2016/11/02 18:24:14.735][Type:NewJournalFile]
VocabularyVersion: 2013-02-01
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.749][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
LogDirectory: F:\logs
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.754][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
StorageAccountKey: *******
[EndUpdateRecord]
```

## <a name="faq"></a>P+F

### <a name="general"></a>General

#### <a name="what-is-waimportexport-tool"></a>¿Qué es la herramienta WAImportExport?

herramienta de WAImportExport Hello es Hola unidad herramienta de preparación y reparación que puede usar con hello servicio de importación y exportación de Microsoft Azure. Puede usar esta herramienta toocopy datos toohello unidades de disco duro va centro de datos de Azure de tooship tooan. Cuando haya finalizado un trabajo de importación, puede usar esta herramienta toorepair los blobs que estaban dañados que falten o que entran en conflicto con otros blobs. Después de recibir las unidades de Hola de un trabajo de exportación completado, puede usar esta herramienta toorepair los archivos que estaban dañados o que faltan en las unidades de Hola.

#### <a name="how-does-hello-waimportexport-tool-work-on-multiple-source-dir-and-disks"></a>¿Cómo hace Hola herramienta WAImportExport funciona en varios directorios de origen y los discos?

Si el tamaño de los datos hello es mayor que el tamaño del disco de hello, herramienta WAImportExport de Hola encargará de distribuir datos hello en varios discos de Hola de forma optimizada. Hola datos copiar toomultiple discos pueden realizarse en paralelo o secuencialmente. No hay ningún límite del número de Hola de datos de saludo de discos se puede escribir toosimultaneously. herramienta de Hola encargará de distribuir datos basándose en el tamaño de disco y tamaño de la carpeta. Seleccionará el disco hello más optimizado para el tamaño del objeto de Hola. Hola datos cuando se cargan se converger la cuenta de almacenamiento de toohello volver toohello especifica la estructura de directorios.

#### <a name="where-can-i-find-previous-version-of-waimportexport-tool"></a>¿Dónde puedo encontrar la versión anterior de la herramienta WAImportExport?

La herramienta WAImportExport tiene todas las funcionalidades que tenía la herramienta WAImportExport V1. Herramienta WAImportExport permite a los usuarios toospecify varios orígenes y las unidades de toomultiple de escritura. Además, uno puede administrar fácilmente varias ubicaciones de origen desde el que los datos de hello tienen toobe copiado en un único archivo CSV. Sin embargo, en caso necesario SAS admite o desea toocopy origen único toosingle disk, que puede [Descargar WAImportExport V1 herramienta] (http://go.Microsoft.com/fwlink/?) LinkID = 301900&amp;clcid = 0 x 409) y consulte demasiado[WAImportExport V1 referencia](storage-import-export-tool-how-to-v1.md) para obtener ayuda con el uso de WAImportExport V1.

#### <a name="what-is-a-session-id"></a>¿Qué es un identificador de sesión?

herramienta de Hello espera que la sesión de copia de hello (o Id.) parámetro toobe Hola igual si el intento de hello toospread Hola datos en varios discos. Mantener Hola mismo nombre de sesión de copia de hello permitirá toocopy datos de usuario de una o varias ubicaciones de origen en uno o varios discos/directorios de destino. Mantener el mismo Id. de sesión permite hello toopick de herramienta copia de seguridad Hola de archivos desde donde se quedó Hola última vez.

Sin embargo, la misma sesión de copia no puede ser cuentas de almacenamiento usado tooimport datos toodifferent.

Cuando el nombre de la sesión de copia es el mismo durante varias ejecuciones de la herramienta de hello, Hola archivo de registro (/ logdir) y la clave de cuenta de almacenamiento (/ sk) es también toobe esperado Hola igual.

SessionId puede estar formado por letras, números 0 a 9, guion bajo (\_), guion (-) o hash (#) y su longitud debe estar comprendida entre 3 y 30 caracteres.

Por ejemplo, session-1 o session#1 o session\_1

#### <a name="what-is-a-journal-file"></a>¿Qué es un archivo de diario?

Cada vez que ejecute hello WAImportExport herramienta toocopy archivos toohello unidad de disco duro, la herramienta de hello crea una sesión de copia. estado de Hola de sesión de copia de Hola se escribe el archivo de diario de toohello. Si se interrumpe una sesión de copia (por ejemplo, debido a pérdida de energía del sistema de tooa), se puede reanudar ejecutar herramienta Hola de nuevo y especificando el archivo de diario de hello en línea de comandos de Hola.

Para cada unidad de disco duro que prepare con hello herramienta de importación y exportación de Azure, Hola herramienta creará un solo archivo de diario con el nombre "&lt;IdUnidad&gt;.xml" donde Id. de unidad es el número de serie de hello asociado unidad toohello que Hola herramienta lee desde disco de Hola. Necesitará los archivos de diario de Hola de todo el trabajo de importación de las unidades toocreate Hola. archivo de diario de Hello también puede ser usado tooresume preparación de unidad si se interrumpe la herramienta de Hola.

#### <a name="what-is-a-log-directory"></a>¿Qué es un directorio de registro?

directorio de registro de Hello especifica que un directorio toobe utiliza toostore los registros detallados, así como los archivos de manifiesto temporales. Si no se especifica, se utilizará el directorio actual de hello como directorio de registro de hello. Hola registros son registros detallados.

### <a name="prerequisites"></a>Requisitos previos

#### <a name="what-are-hello-specifications-of-my-disk"></a>¿Cuáles son las especificaciones de Hola de mi disco?

Uno o más vacía SATAII 2,5 pulgadas o 3,5 pulgadas o III o SSD disco duro unidades equipo de copia de toohello conectado.

#### <a name="how-can-i-enable-bitlocker-on-my-machine"></a>¿Cómo se puede habilitar BitLocker en mi máquina?

Toocheck de manera sencilla es con el botón secundario en la unidad del sistema. Le mostrará la opciones de Bitlocker si está activada la capacidad de Hola. Si está desactivada, no las verá.

![Comprobación de BitLocker](./media/storage-import-export-tool-preparing-hard-drives-import/BitLocker.png)

Este es un artículo en [cómo tooenable BitLocker](https://technet.microsoft.com/library/cc766295.aspx)

Es posible que la máquina no tenga el chip TPM. Si no obtiene un resultado mediante tpm.msc, examine la siguiente pregunta Frecuente de Hola.

#### <a name="how-toodisable-trusted-platform-module-tpm-in-bitlocker"></a>¿Cómo toodisable el módulo de plataforma de confianza (TPM) de BitLocker?
> [!NOTE]
> Sólo si no hay ningún TPM en sus servidores, deberá toodisable directiva TPM. No es necesario toodisable TPM si hay un confianza TPM en el servidor del usuario. 
> 

En orden toodisable TPM de BitLocker, vaya a través de hello pasos:<br/>
1. Inicie el **Editor de directivas de grupo** escribiendo gpedit.msc en un símbolo del sistema. Si **Editor de directivas de grupo** aparece toobe disponible, para habilitar BitLocker en primer lugar. Consulte las preguntas más frecuentes descritas anteriormente.
2. Abra **Directiva de equipo Local &gt; Configuración del equipo &gt; Plantillas administrativas &gt; Componentes de Windows&gt; Cifrado de unidad BitLocker &gt; Unidades del sistema operativo**.
3. Edite la directiva **Requerir autenticación adicional al iniciar**.
4. Establecer una directiva de hello demasiado**habilitado** y asegúrese de que **Permitir BitLocker sin un TPM compatible** está activada.

####  <a name="how-toocheck-if-net-4-or-higher-version-is-installed-on-my-machine"></a>¿Cómo toocheck si .NET 4 o una versión posterior está instalada en mi equipo?

Todas las versiones de Microsoft .NET Framework se instalan en el directorio siguiente: %windir%\Microsoft.NET\Framework\

Navegue toohello anteriormente mencionado parte en el equipo de destino donde herramienta Hola necesita toorun. Busque un nombre de carpeta que empieza por "v4". La ausencia de un directorio de este tipo significa que .NET 4 no está instalado en la máquina. Puede descargar .Net 4 en la máquina con [Microsoft .NET Framework 4 (Instalador web)](https://www.microsoft.com/download/details.aspx?id=17851).

### <a name="limits"></a>límites

#### <a name="how-many-drives-can-i-preparesend-at-hello-same-time"></a>Cuántas unidades ¿preparar/envío en hello mismo tiempo?

No hay ningún límite en el número de Hola de discos que Hola herramienta puede preparar. Sin embargo, la herramienta de hello espera letras de unidad como entradas. Limita la preparación de disco simultáneos too25. Un solo trabajo puede controlar un máximo de 10 discos a la vez. Si se preparan los discos de más de 10 destinatarios Hola la misma cuenta de almacenamiento, los discos de Hola se pueden distribuir en varios trabajos.

#### <a name="can-i-target-more-than-one-storage-account"></a>¿Se puede usar como destino más de una cuenta de almacenamiento?

Solo se puede enviar una cuenta de almacenamiento por trabajo y en una sola sesión de copia.

### <a name="capabilities"></a>Capacidades

#### <a name="does-waimportexportexe-encrypt-my-data"></a>¿Cifra WAImportExport.exe mis datos?

Sí. El cifrado de BitLocker está habilitado y es obligatorio para este proceso.

#### <a name="what-will-be-hello-hierarchy-of-my-data-when-it-appears-in-hello-storage-account"></a>¿Cuál será la jerarquía Hola de Mis datos cuando aparece en la cuenta de almacenamiento de hello?

Aunque los datos se distribuyen en varios discos, Hola datos cuando cargan converger la cuenta de almacenamiento de toohello hacer copia de estructura de directorios de toohello especificado en el archivo CSV de hello dataset.

#### <a name="how-many-of-hello-input-disks-will-have-active-io-in-parallel-when-copy-is-in-progress"></a>¿Cuántos de Hola de entrada discos tendrá active E/S en paralelo, cuando se copia en curso?

herramienta de Hello distribuye los datos en discos de entrada de hello según su tamaño Hola Hola de archivos de entrada. Es decir, número de Hola de discos activos en paralelo delends completamente de naturaleza Hola Hola de datos de entrada. Según el tamaño de Hola de archivos individuales en el conjunto de datos de entrada de hello, uno o más discos pueden mostrar active E/S en paralelo. Consulte más detalles en la siguiente pregunta.

#### <a name="how-does-hello-tool-distribute-hello-files-across-hello-disks"></a>¿Cómo distribuir herramienta Hola archivos hello en varios discos de hello?

La herramienta WAImportExport lee y escribe archivos lote por lote, un lote contiene un número máximo de 100 000 archivos. Esto significa que se pueden escribir 100 000 archivos como máximo en paralelo. Se escriben varios discos toosimultaneously si estos 100000 archivos están distribuidas toomulti unidades. Sin embargo si Hola herramienta escribe toomultiple discos al mismo tiempo o un único disco depende del tamaño acumulado de Hola de lote de Hola. Por ejemplo, en el caso de archivos más pequeños, si todos los archivos 10.0000 son toofit pueda en una sola unidad, herramienta escribirá tooonly un disco durante el procesamiento de Hola de este lote.

### <a name="waimportexport-output"></a>Salida de WAImportExport

#### <a name="there-are-two-journal-files-which-one-should-i-upload-tooazure-portal"></a>¿Hay dos archivos de diario, cuál debería cargara tooAzure portal?

**.XML** -para cada unidad de disco duro que prepare con la herramienta WAImportExport de hello, Hola herramienta creará un archivo de diario única con nombre `<DriveID>.xml` donde IdUnidad es el número de serie de hello asociado unidad toohello que Hola herramienta lee desde el disco de Hola. Necesitará los archivos de diario de Hola de todo el trabajo de importación de las unidades toocreate Hola Hola portal de Azure. Este archivo de diario también puede ser usado tooresume preparación de unidad si se interrumpe la herramienta de Hola.

**.Jrn** -archivo de diario de hello con el sufijo `.jrn` contiene el estado de Hola para todas las sesiones de copia de una unidad de disco duro. También contiene información de Hola Hola toocreate necesita importar el trabajo. Siempre debe especificar un archivo de diario al identificador de herramienta de ejecución hello WAImportExport, así como una sesión de copia.

## <a name="next-steps"></a>Pasos siguientes

* [Setting Up Hola herramienta de importación y exportación de Azure](storage-import-export-tool-setup.md)
* [Proceso de importación de establecer las propiedades y metadatos durante Hola](storage-import-export-tool-setting-properties-metadata-import.md)
* [Unidades de disco duro de tooprepare de flujo de trabajo y ejemplo de un trabajo de importación](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
* [Referencia rápida de comandos usados con frecuencia para trabajos de importación](storage-import-export-tool-quick-reference.md) 
* [Revisión del estado del trabajo con archivos de registro de copia](storage-import-export-tool-reviewing-job-status-v1.md)
* [Reparación de un trabajo de importación](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Reparación de un trabajo de exportación](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Solución de problemas de hello herramienta de importación y exportación de Azure](storage-import-export-tool-troubleshooting-v1.md)
