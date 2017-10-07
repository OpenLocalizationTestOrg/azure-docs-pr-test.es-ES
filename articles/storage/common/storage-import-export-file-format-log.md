---
title: "formato de archivo de registro de importación y exportación de aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca del formato de Hola Hola de archivos de registro creado cuando se ejecutan los pasos de un trabajo de servicio de importación y exportación."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a>Formato del archivo de registro del servicio Azure Import/Export
Cuando Hola servicio de importación y exportación de Microsoft Azure realiza una acción en una unidad como parte de un trabajo de importación o un trabajo de exportación, los registros se escriben tooblock blobs en la cuenta de almacenamiento de hello asociada con ese trabajo.  
  
Hay dos registros que se pueden escribir Hola servicio de importación y exportación:  
  
-   siempre se genera el registro de errores de Hello en caso de hello de un error.  
  
-   Hello registro detallado no está habilitado de forma predeterminada, pero puede habilitarla mediante configuración hello `EnableVerboseLog` propiedad en un [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) o [actualizar propiedades del trabajo](/rest/api/storageimportexport/jobs#Jobs_Update) operación.  
  
## <a name="log-file-location"></a>Ubicación del archivo de registro  
Hola se escriben los registros tooblock blobs en el contenedor de Hola o el directorio virtual especificado por hello `ImportExportStatesPath` configuración, que puede establecer en un `Put Job` operación. Hola ubicación toowhich Hola registros se escriben depende de cómo se especifica la autenticación para el trabajo de hello, junto con el valor de hello especificado para `ImportExportStatesPath`. Se puede especificar la autenticación para el trabajo de Hola a través de una clave de cuenta de almacenamiento o un contenedor SAS (firma de acceso compartido).  
  
nombre Hola de hello contenedor o directorio virtual puede ser el nombre predeterminado de Hola de `waimportexport`, o en otro contenedor o nombre del directorio virtual que especifique.  
  
Hola tabla siguiente muestran opciones posibles de hello:  
  
|Método de autenticación|Valor de `ImportExportStatesPath`Element|Ubicación de blobs del registro|  
|---------------------------|----------------------------------------------|---------------------------|  
|Clave de cuenta de almacenamiento|Valor predeterminado|Un contenedor denominado `waimportexport`, que es el contenedor predeterminado de Hola. Por ejemplo:<br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|Clave de cuenta de almacenamiento|Valor especificado por el usuario|Un contenedor denominado por el usuario de Hola. Por ejemplo:<br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|SAS de contenedor|Valor predeterminado|Un directorio virtual denominado `waimportexport`, que es nombre predeterminado de hello, debajo de contenedor de hello especificado en hello SAS.<br /><br /> Por ejemplo, si especifica Hola SAS para trabajo de hello es `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, ubicación de registro de hello sería`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`|  
|SAS de contenedor|Valor especificado por el usuario|Un directorio virtual denominado por el usuario de hello, debajo de contenedor de hello especificado en hello SAS.<br /><br /> Por ejemplo, si especifica Hola SAS para trabajo de hello es `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, y Hola especifica el directorio virtual se denomina `mylogblobs`, ubicación de registro de hello sería `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.|  
  
Puede recuperar la dirección URL de Hola para error de Hola y el registro detallado por llamada hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operación. registros de Hello están disponibles una vez completado el procesamiento de unidad de Hola.  
  
## <a name="log-file-format"></a>Formato de archivo de registro  
Hello formato para los registros se Hola mismo: un blob que contiene las descripciones XML de eventos de Hola que se produjeron mientras se copiaban blobs entre la unidad de disco duro de Hola y la cuenta del cliente de Hola.  
  
registro detallado de Hello contiene información completa sobre el estado de Hola de operación de copia de Hola para cada blob (para un trabajo de importación) o el archivo (para un trabajo de exportación), mientras que el registro de errores de hello contiene únicamente la información de Hola de blobs o archivos que encontraron errores durante Hola importar o exportar un trabajo.  
  
a continuación se muestra el formato de registro detallado de Hola. registro de errores de Hello tiene Hola equivalente a la estructura, pero filtra las operaciones correctas.  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

Hello tabla siguiente describe los elementos de Hola Hola del archivo de registro.  
  
|Elemento XML|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|`DriveLog`|Elemento XML|Representa un registro de la unidad.|  
|`Version`|Attribute, String|versión de Hola del formato de registro de hello.|  
|`DriveId`|String|Hola número de serie del hardware de la unidad de disco.|  
|`Status`|String|Estado de procesamiento de la unidad de Hola. Vea hello `Drive Status Codes` tabla de abajo para obtener más información.|  
|`Blob`|Elemento XML anidado|Representa un blob.|  
|`Blob/BlobPath`|String|URI de blob de Hola Hola.|  
|`Blob/FilePath`|String|archivo de toohello de la ruta de acceso relativa de Hello en unidad de Hola.|  
|`Blob/Snapshot`|DateTime|versión de instantánea de Hola de blob de hello, para un trabajo de exportación únicamente.|  
|`Blob/Length`|Entero|longitud total de Hola de blob de hello en bytes.|  
|`Blob/LastModified`|DateTime|fecha y hora de Hello blob Hola se modificó por última vez, para un trabajo de exportación únicamente.|  
|`Blob/ImportDisposition`|String|Hola importar disposition del blob de hello, para un trabajo de importación únicamente.|  
|`Blob/ImportDisposition/@Status`|Attribute, String|estado de saludo del programa Hola a disposición de importación.|  
|`PageRangeList`|Elemento XML anidado|Representa una lista de los intervalos de páginas de un blob en páginas.|  
|`PageRange`|Elemento XML|Representa un intervalo de páginas.|  
|`PageRange/@Offset`|Attribute, Integer|Desplazamiento inicial del intervalo de páginas de hello en blob de Hola.|  
|`PageRange/@Length`|Attribute, Integer|Longitud en bytes del intervalo de páginas de Hola.|  
|`PageRange/@Hash`|Attribute, String|Hash de MD5 codificado en Base16 del intervalo de páginas de Hola.|  
|`PageRange/@Status`|Attribute, String|Estado de procesamiento de intervalo de páginas de Hola.|  
|`BlockList`|Elemento XML anidado|Representa una lista de bloques de un blob en bloques.|  
|`Block`|Elemento XML|Representa un bloque.|  
|`Block/@Offset`|Attribute, Integer|Desplazamiento inicial del bloque de hello en blob de Hola.|  
|`Block/@Length`|Attribute, Integer|Longitud en bytes del bloque de Hola.|  
|`Block/@Id`|Attribute, String|identificador de bloque de Hola.|  
|`Block/@Hash`|Attribute, String|Hash de MD5 codificado en Base16 del bloque de Hola.|  
|`Block/@Status`|Attribute, String|Estado de procesamiento bloque Hola.|  
|`Metadata`|Elemento XML anidado|Representa los metadatos del blob de Hola.|  
|`Metadata/@Status`|Attribute, String|Estado de procesamiento de metadatos del blob Hola.|  
|`Metadata/GlobalPath`|String|Archivo de metadatos globales toohello de ruta de acceso relativa.|  
|`Metadata/GlobalPath/@Hash`|Attribute, String|Hash de MD5 codificado en Base16 del archivo de metadatos globales Hola.|  
|`Metadata/Path`|String|Archivo de metadatos de toohello de ruta de acceso relativa.|  
|`Metadata/Path/@Hash`|Attribute, String|Hash de MD5 codificado en Base16 del archivo de metadatos de Hola.|  
|`Properties`|Elemento XML anidado|Representa las propiedades de blob de Hola.|  
|`Properties/@Status`|Attribute, String|Estado de procesamiento de propiedades del blob hello, por ejemplo, archivo no encontrado, finalizado.|  
|`Properties/GlobalPath`|String|Archivo de propiedades globales de toohello de ruta de acceso relativa.|  
|`Properties/GlobalPath/@Hash`|Attribute, String|Hash de MD5 codificado en Base16 del archivo de propiedades globales de Hola.|  
|`Properties/Path`|String|Archivo de propiedades de toohello de ruta de acceso relativa.|  
|`Properties/Path/@Hash`|Attribute, String|Hash de MD5 codificado en Base16 del archivo de propiedades de Hola.|  
|`Blob/Status`|String|Estado de procesamiento Hola blob.|  
  
# <a name="drive-status-codes"></a>Códigos de estado de unidad  
Hello tabla siguiente enumeran los códigos de estado de hello para el procesamiento de una unidad.  
  
|Código de estado|Descripción|  
|-----------------|-----------------|  
|`Completed`|unidad de Hello ha finalizado el procesamiento sin errores.|  
|`CompletedWithWarnings`|unidad de Hello ha finalizado el procesamiento con advertencias en uno o más blobs según las disposiciones de importación de hello especificadas para los blobs de Hola.|  
|`CompletedWithErrors`|Hola unidad ha finalizado con errores en uno o más blobs o fragmentos.|  
|`DiskNotFound`|Se encontró ningún disco en la unidad de Hola.|  
|`VolumeNotNtfs`|primer volumen de datos Hello en el disco de hello no está en formato NTFS.|  
|`DiskOperationFailed`|Se produjo un error desconocido al realizar operaciones en la unidad de Hola.|  
|`BitLockerVolumeNotFound`|No se encuentra ningún volumen cifrable de BitLocker.|  
|`BitLockerNotActivated`|BitLocker no está habilitado en el volumen de Hola.|  
|`BitLockerProtectorNotFound`|protector de clave de contraseña numérica de Hello no existe en el volumen de Hola.|  
|`BitLockerKeyInvalid`|contraseña numérica de Hello especificada no puede desbloquear el volumen de Hola.|  
|`BitLockerUnlockVolumeFailed`|Ha ocurrido error desconocido al tratar de volumen de hello toounlock.|  
|`BitLockerFailed`|Se produjo un error desconocido al realizar operaciones de BitLocker.|  
|`ManifestNameInvalid`|nombre de archivo de manifiesto de Hello no es válido.|  
|`ManifestNameTooLong`|nombre de archivo de manifiesto de Hello es demasiado largo.|  
|`ManifestNotFound`|no se encuentra el archivo de manifiesto de Hola.|  
|`ManifestAccessDenied`|Archivo de manifiesto de toohello de acceso denegado.|  
|`ManifestCorrupted`|Hello archivo de manifiesto está dañado (contenido de hello no coincide con su hash).|  
|`ManifestFormatInvalid`|contenido del manifiesto Hello no cumple el formato requerido de toohello.|  
|`ManifestDriveIdMismatch`|unidad de Hello no coincide con el Id. de archivo de manifiesto de Hola Hola se lee en la unidad de Hola.|  
|`ReadManifestFailed`|Se ha producido un error de E/S de disco al leer desde el manifiesto de Hola.|  
|`BlobListFormatInvalid`|lista de blobs exportación de Hello no cumple el formato requerido de toohello.|  
|`BlobRequestForbidden`|Se prohíbe blobs de toohello de acceso de cuenta de almacenamiento de Hola. Esto podría ser debido a la clave de cuenta de almacenamiento de tooinvalid o un contenedor SAS.|  
|`InternalError`|Y se produjo un error interno al procesar la unidad de Hola.|  
  
## <a name="blob-status-codes"></a>Códigos de estado de blob  
Hello tabla siguiente enumeran los códigos de estado de hello para el procesamiento de un blob.  
  
|Código de estado|Descripción|  
|-----------------|-----------------|  
|`Completed`|blob de Hello ha finalizado el procesamiento sin errores.|  
|`CompletedWithErrors`|blob de Hello ha finalizado el procesamiento con errores en uno o más intervalos de páginas o bloques, metadatos o propiedades.|  
|`FileNameInvalid`|nombre de archivo de Hello no es válido.|  
|`FileNameTooLong`|nombre de archivo de Hello es demasiado largo.|  
|`FileNotFound`|no se encuentra el archivo hello.|  
|`FileAccessDenied`|Archivo de toohello de acceso denegado.|  
|`BlobRequestFailed`|Error de solicitud de servicio de Blob de Hello tooaccess Hola blob.|  
|`BlobRequestForbidden`|se prohíbe la solicitud del servicio Blob Hello tooaccess Hola blob. Esto podría ser debido a la clave de cuenta de almacenamiento de tooinvalid o un contenedor SAS.|  
|`RenameFailed`|No se pudo blob de hello toorename (para un trabajo de importación) o archivo de hello (para un trabajo de exportación).|  
|`BlobUnexpectedChange`|Se ha producido un cambio inesperado con blob hello (para un trabajo de exportación).|  
|`LeasePresent`|Hay una concesión en el blob de Hola.|  
|`IOFailed`|Un disco o un error de E/S de red se ha producido durante el procesamiento de blob de Hola.|  
|`Failed`|Se ha producido un error desconocido al procesar Hola blob.|  
  
## <a name="import-disposition-status-codes"></a>Códigos de estado de disposición de importación  
Hello tabla siguiente enumeran los códigos de estado de Hola para resolver una disposición de importación.  
  
|Código de estado|Descripción|  
|-----------------|-----------------|  
|`Created`|se ha creado el blob de Hola.|  
|`Renamed`|se ha cambiado el blob de Hola por disposición de importación de cambio de nombre. Hola `Blob/BlobPath` elemento contiene Hola URI de blob de hello cambia el nombre.|  
|`Skipped`|se ha omitido el blob de Hola por `no-overwrite` disposición de importación.|  
|`Overwritten`|blob de Hello ha sobrescrito un blob existente según `overwrite` disposición de importación.|  
|`Cancelled`|Un error anterior ha detenido el procesamiento posterior de disposición de importación de Hola.|  
  
## <a name="page-rangeblock-status-codes"></a>Códigos de estado de intervalo de páginas o bloque  
Hello tabla siguiente enumeran los códigos de estado de hello para el procesamiento de un intervalo de páginas o un bloque.  
  
|Código de estado|Descripción|  
|-----------------|-----------------|  
|`Completed`|intervalo de páginas de Hola o bloque ha finalizado el procesamiento sin errores.|  
|`Committed`|Hola bloque se ha confirmado, pero no en hello lista de bloques completa porque otros bloques dispone de error o colocar la propia lista de bloques completa ha.|  
|`Uncommitted`|bloque de Hello es cargado pero no confirmado.|  
|`Corrupted`|intervalo de páginas de Hola o bloque está dañado (contenido de hello no coincide con su hash).|  
|`FileUnexpectedEnd`|Se ha encontrado un final de archivo inesperado.|  
|`BlobUnexpectedEnd`|Se ha encontrado un final de blob inesperado.|  
|`BlobRequestFailed`|Hola solicitud del servicio Blob tooaccess Hola intervalo de páginas o bloque ha fallado.|  
|`IOFailed`|Un disco o un error de E/S de red se produjo al procesar el intervalo de páginas de Hola o bloque.|  
|`Failed`|Se ha producido un error desconocido al procesar el intervalo de páginas de Hola o bloque.|  
|`Cancelled`|Un error anterior ha detenido el procesamiento posterior de intervalo de páginas de Hola o un bloque.|  
  
## <a name="metadata-status-codes"></a>Códigos de estado de metadatos  
Hello tabla siguiente enumeran los códigos de estado de Hola para procesar los metadatos de blob.  
  
|Código de estado|Descripción|  
|-----------------|-----------------|  
|`Completed`|metadatos de Hello han finalizado el procesamiento sin errores.|  
|`FileNameInvalid`|nombre de archivo de metadatos de Hello no es válido.|  
|`FileNameTooLong`|nombre de archivo de metadatos de Hello es demasiado largo.|  
|`FileNotFound`|no se encuentra el archivo de metadatos de Hello.|  
|`FileAccessDenied`|Archivo de metadatos de toohello de acceso denegado.|  
|`Corrupted`|archivo de metadatos de Hello está dañado (contenido de hello no coincide con su hash).|  
|`XmlReadFailed`|contenido de metadatos de Hello no cumple el formato requerido de toohello.|  
|`XmlWriteFailed`|Escribir metadatos Hola que XML ha fallado.|  
|`BlobRequestFailed`|Error de solicitud de servicio de Blob de Hello tooaccess Hola metadatos.|  
|`IOFailed`|Se ha producido un error de E/S de disco o de red al procesar metadatos Hola.|  
|`Failed`|Se ha producido un error desconocido al procesar metadatos Hola.|  
|`Cancelled`|Un error anterior ha detenido el procesamiento posterior de los metadatos de Hola.|  
  
## <a name="properties-status-codes"></a>Códigos de estado de las propiedades  
Hello tabla siguiente enumeran los códigos de estado de hello para el procesamiento de propiedades del blob.  
  
|Código de estado|Descripción|  
|-----------------|-----------------|  
|`Completed`|propiedades de Hello han finalizado el procesamiento sin errores.|  
|`FileNameInvalid`|nombre de archivo de propiedades de Hello no es válido.|  
|`FileNameTooLong`|nombre de archivo de propiedades de Hello es demasiado largo.|  
|`FileNotFound`|no se encuentra el archivo de propiedades de Hello.|  
|`FileAccessDenied`|Archivo de propiedades de toohello de acceso denegado.|  
|`Corrupted`|archivo de propiedades de Hello está dañado (contenido de hello no coincide con su hash).|  
|`XmlReadFailed`|contenido de las propiedades Hello no cumplen el formato requerido de toohello.|  
|`XmlWriteFailed`|Escribir propiedades de hello que XML ha fallado.|  
|`BlobRequestFailed`|Error de solicitud de servicio de Blob de Hello tooaccess Hola propiedades.|  
|`IOFailed`|Se ha producido un error de E/S de disco o de red durante el procesamiento de propiedades de Hola.|  
|`Failed`|Se produjo un error desconocido durante el procesamiento de propiedades de Hola.|  
|`Cancelled`|Un error anterior ha detenido el procesamiento posterior de las propiedades de Hola.|  
  
## <a name="sample-logs"></a>Registros de ejemplo  
Hola aquí te mostramos un ejemplo de registro detallado.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
registro de errores de Hello correspondiente se muestra a continuación.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 registro de errores de seguimiento de Hola para un trabajo de importación contiene un error sobre un archivo que no se encuentra en la unidad de importación de Hola. Tenga en cuenta que el estado de saludo de los componentes siguientes es `Cancelled`.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

Hello siguiente registro de errores para un trabajo de exportación indica que el contenido de blob Hola se ha escrito correctamente toohello unidad, pero que se produjo un error al exportar las propiedades del blob de Hola.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a>Pasos siguientes
 
* [API de REST de Storage Import/Export](/rest/api/storageimportexport/)
