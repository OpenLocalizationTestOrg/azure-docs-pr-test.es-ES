---
title: "formato de archivo de manifiesto de importación y exportación de aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca del formato de Hola Hola unidad del archivo de manifiesto que describe la asignación de hello entre archivos en una unidad en un trabajo de importación o exportación en el servicio de importación y exportación de Hola y de blobs en almacenamiento de blobs de Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f3119e1c-2c25-48ad-8752-a6ed4adadbb0
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: d7e5e1990482916f7ff5f891c97343b52e82b2f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-manifest-file-format"></a>Formato del archivo de manifiesto de servicio de Azure Import/Export
archivo de manifiesto de unidad de Hello describe la asignación de hello entre blobs en almacenamiento de blobs de Azure y los archivos en la unidad que componen un trabajo de importación o exportación. Para una operación de importación, archivo de manifiesto de Hola se crea como parte del proceso de preparación de unidad de Hola y se almacena en la unidad de hello antes de unidad de Hola se envía toohello centro de datos de Azure. Durante una operación de exportación, es crear el manifiesto de Hola y se almacena en la unidad de Hola Hola servicio de importación y exportación de Azure.  
  
Para importación ambos y se almacenan los trabajos de exportación, archivo de manifiesto de unidad de hello en hello importar o exportar unidad; no es transmitida toohello servicio a través de una operación de API.  
  
siguiente Hola describe Hola formato general de un archivo de manifiesto de unidad:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveManifest Version="2014-11-01">  
  <Drive>  
    <DriveId>drive-id</DriveId>  
    import-export-credential  
  
    <!-- First Blob List -->  
    <BlobList>  
      <!-- Global properties and metadata that applies tooall blobs -->  
      [<MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>]  
      [<PropertiesPath   
        Hash="md5-hash">global-properties-file-path</PropertiesPath>]  
  
      <!-- First Blob -->  
      <Blob>  
        <BlobPath>blob-path-relative-to-account</BlobPath>  
        <FilePath>file-path-relative-to-transfer-disk</FilePath>  
        [<ClientData>client-data</ClientData>]  
        [<Snapshot>snapshot</Snapshot>]  
        <Length>content-length</Length>  
        [<ImportDisposition>import-disposition</ImportDisposition>]  
        page-range-list-or-block-list          
        [<MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>]  
        [<PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>]  
      </Blob>  
  
      <!-- Second Blob -->  
      <Blob>  
      . . .  
      </Blob>  
    </BlobList>  
  
    <!-- Second Blob List -->  
    <BlobList>  
    . . .  
    </BlobList>  
  </Drive>  
</DriveManifest>  
  
import-export-credential ::=   
  <StorageAccountKey>storage-account-key</StorageAccountKey> | <ContainerSas>container-sas</ContainerSas>  
  
page-range-list-or-block-list ::=   
  page-range-list | block-list  
  
page-range-list ::=   
    <PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
    </PageRangeList>  
  
block-list ::=  
    <BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       Hash="md5-hash"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       Hash="md5-hash"/>]  
    </BlockList>  

```

## <a name="manifest-xml-elements-and-attributes"></a>Elementos y atributos XML del manifiesto

elementos de datos de Hola y los atributos de formato XML de manifiesto de unidad de Hola se especifican en hello en la tabla siguiente.  
  
|Elemento XML|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|`DriveManifest`|Elemento raíz|elemento raíz de Hola Hola del archivo de manifiesto. Todos los demás elementos en el archivo hello están por debajo de este elemento.|  
|`Version`|Attribute, String|versión de Hola Hola del archivo de manifiesto.|  
|`Drive`|Elemento XML anidado|Contiene el manifiesto de Hola para cada unidad.|  
|`DriveId`|String|Hola identificador único de la unidad de Hola. se encontró el identificador de unidad de Hello consultando unidad hello para el número de serie. número de serie de unidad de Hello normalmente se imprime en hello fuera de la unidad de hello así. Hola `DriveID` elemento debe aparecer antes de cualquier `BlobList` elemento en el archivo de manifiesto de Hola.|  
|`StorageAccountKey`|String|Se requiere para trabajos de importación si, y solo si, no se ha especificado `ContainerSas`. clave de cuenta de Hello para hello cuenta de almacenamiento de Azure asociadas trabajo Hola.<br /><br /> Este elemento se omite del manifiesto de Hola para una operación de exportación.|  
|`ContainerSas`|String|Se requiere para trabajos de importación si, y solo si, no se ha especificado `StorageAccountKey`. contenedor de Hello SAS para tener acceso a blobs Hola asociados Hola trabajo. Vea [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) para su formato. Este elemento se omite del manifiesto de Hola para una operación de exportación.|  
|`ClientCreator`|String|Especifica el cliente de Hola que ha creado el archivo XML de hello. Este valor no se interpreta por hello servicio de importación/exportación.|  
|`BlobList`|Elemento XML anidado|Contiene una lista de blobs que forman parte de la importación de Hola o el trabajo de exportación. Cada blob en una lista de blobs recursos compartidos de Hola mismos metadatos y propiedades.|  
|`BlobList/MetadataPath`|String|Opcional. Especifica la ruta de acceso relativa de Hola de un archivo en disco de Hola que contiene los metadatos predeterminados de Hola que se establecerá en blobs de lista de blobs de Hola para una operación de importación. Opcionalmente, estos metadatos se pueden reemplazar en función del blob.<br /><br /> Este elemento se omite del manifiesto de Hola para una operación de exportación.|  
|`BlobList/MetadataPath/@Hash`|Attribute, String|Especifica el valor de hash MD5 codificado en Base16 hello para el archivo de metadatos de hello.|  
|`BlobList/PropertiesPath`|String|Opcional. Especifica la ruta de acceso relativa de Hola de un archivo en disco de Hola que contiene propiedades predeterminadas de Hola que se establecerá en blobs de lista de blobs de Hola para una operación de importación. Opcionalmente, estas propiedades se pueden reemplazar en función del blob.<br /><br /> Este elemento se omite del manifiesto de Hola para una operación de exportación.|  
|`BlobList/PropertiesPath/@Hash`|Attribute, String|Especifica el valor de hash MD5 codificado en Base16 hello para el archivo de propiedades de hello.|  
|`Blob`|Elemento XML anidado|Contiene información sobre todos los blobs de todas las listas de blobs.|  
|`Blob/BlobPath`|String|Hola relativa URI toohello del blob, empezando por el nombre del contenedor de Hola. Si el blob de hello está en el contenedor raíz, debe comenzar con `$root`.|  
|`Blob/FilePath`|String|Especifica el archivo de toohello de ruta de acceso relativa de hello en unidad de Hola. Para los trabajos de exportación, se usará la ruta de acceso de blob de Hola para hello ruta de acceso si es posible; *p. ej.*, `pictures/bob/wild/desert.jpg` se exportarán demasiado`\pictures\bob\wild\desert.jpg`. Sin embargo, debido a limitaciones de toohello de los nombres NTFS, un blob puede ser archivo tooa exportado con una ruta de acceso que no son similares a la ruta de acceso de blob de Hola.|  
|`Blob/ClientData`|String|Opcional. Contiene comentarios del cliente de Hola. Este valor no se interpreta por hello servicio de importación/exportación.|  
|`Blob/Snapshot`|DateTime|Opcional para trabajos de exportación. Especifica el identificador de instantánea de Hola para una instantánea de blob exportada.|  
|`Blob/Length`|Entero|Especifica la longitud total de Hola de blob de hello en bytes. Hola valor puede ser too200 GB para un blob en bloques e instalación too1 TB para un blob en páginas. En el caso de un blob en páginas, este valor debe ser múltiplo de 512.|  
|`Blob/ImportDisposition`|string|Opcional en los trabajos de importación, se omite en los trabajos de exportación. Esto especifica forma Hola servicio de importación/exportación debe controlar el caso de hello para un trabajo de importación donde un blob con hello mismo nombre ya existe. Si este valor se omite en el manifiesto de importación de hello, es el valor predeterminado de hello `rename`.<br /><br /> valores de Hello para este elemento incluyen:<br /><br /> -   `no-overwrite`: Si un blob de destino ya está presente con hello mismo nombre, operación de importación de Hola se omitirá la importación del archivo.<br />-   `overwrite`: Hola de archivo recién importado sobrescribe completamente los blobs de destino existentes.<br />-   `rename`: nuevo blob en hello le cargado con un nombre modificado.<br /><br /> Hola, cambiar el nombre de regla es la siguiente:<br /><br /> -Si el nombre del blob de hello no contiene un punto, se genera un nuevo nombre anexando `(2)` toohello nombre original del blob; si este nuevo nombre también está en conflicto con un nombre de blob existente, a continuación, `(3)` se anexa en lugar de `(2)`; y así sucesivamente.<br />: Si el nombre del blob de hello contiene un punto, parte de hello siguiendo el último punto de Hola se considera el nombre de extensión de Hola. Toohello similar encima de procedimiento, `(2)` se inserta delante Hola último punto toogenerate un nuevo nombre; si el nuevo nombre de hello todavía está en conflicto con un nombre de blob existente, el servicio de hello intenta `(3)`, `(4)`, y así sucesivamente, hasta que no conflictivos se encontró el nombre.<br /><br /> Estos son algunos ejemplos:<br /><br /> blob de Hello `BlobNameWithoutDot` se cambiará para:<br /><br /> `BlobNameWithoutDot (2)  // if BlobNameWithoutDot exists`<br /><br /> `BlobNameWithoutDot (3)  // if both BlobNameWithoutDot and BlobNameWithoutDot (2) exist`<br /><br /> blob de Hello `Seattle.jpg` se cambiará para:<br /><br /> `Seattle (2).jpg  // if Seattle.jpg exists`<br /><br /> `Seattle (3).jpg  // if both Seattle.jpg and Seattle (2).jpg exist`|  
|`PageRangeList`|Elemento XML anidado|Se requiere para un blob en páginas.<br /><br /> Para que una importación operación, especifica una lista de intervalos de bytes de un toobe del archivo importado. Cada intervalo de páginas se describe mediante un desplazamiento y longitud en el archivo de código fuente de Hola que describe el intervalo de páginas de hello, junto con un hash MD5 de la región de Hola. Hola `Hash` atributo de un intervalo de páginas es necesario. servicio de Hello validará que hash Hola de datos de hello en el blob de hello coincide con hash MD5 de hello calculado del intervalo de páginas de Hola. Cualquier número de intervalos de páginas pueden ser utilizado toodescribe un archivo para una importación, con el tamaño total de hello hasta too1 TB. Todos los intervalos de página deben ordenarse por desplazamiento y no se permiten superposiciones.<br /><br /> Para una operación de exportación, especifica un conjunto de intervalos de bytes de un blob que se han exportado toohello unidad.<br /><br /> intervalos de páginas de Hello juntos pueden abarcar solo subintervalos de un archivo o blob.  se espera Hola la parte restante del archivo hello no cubierto por un intervalo de páginas y su contenido puede ser indefinido.|  
|`PageRange`|Elemento XML|Representa un intervalo de páginas.|  
|`PageRange/@Offset`|Attribute, Integer|Especifica el desplazamiento de hello en el archivo de transferencia de hello y blob Hola donde hello especifica el intervalo de páginas comienza. Este valor debe ser múltiplo de 512.|  
|`PageRange/@Length`|Attribute, Integer|Especifica la longitud de Hola de intervalo de páginas de Hola. Este valor debe ser múltiplo de 512 y no puede supera los 4 MB.|  
|`PageRange/@Hash`|Attribute, String|Especifica el valor de hash MD5 codificado en Base16 Hola Hola intervalo de páginas.|  
|`BlockList`|Elemento XML anidado|Se requiere para un blob en bloques con bloques con nombre.<br /><br /> Para una operación de importación, la lista de bloques de hello especifica un conjunto de bloques que se importarán en el almacenamiento de Azure. Para una operación de exportación, lista de bloques de hello especifica que cada bloque se almacena en el archivo hello en el disco de exportación de Hola. Cada bloque se describe por un desplazamiento en el archivo hello y una longitud de bloque; cada bloque se designa además mediante un atributo de Id. de bloque y contiene un hash MD5 para el bloque de Hola. Seguridad too50, 000 bloques pueden ser usado toodescribe un blob.  Todos los bloqueos se deben ordenar por el desplazamiento y juntos debe cubrir el intervalo completo de Hola de archivo hello, *, es decir,*, no debe haber ninguna diferencia entre los bloques. Si blob hello es no más de 64 MB, identificadores de bloque de Hola para cada bloque debe estar todos ausentes o todos presentes. Los identificadores de bloque son cadenas con codificación Base64 toobe necesarios. Para ver otros requisitos de los identificadores de bloque, consulte [Put Block](/rest/api/storageservices/put-block).|  
|`Block`|Elemento XML|Representa un bloque.|  
|`Block/@Offset`|Attribute, Integer|Especifica el desplazamiento Hola donde comienza el bloque especificado de Hola.|  
|`Block/@Length`|Attribute, Integer|Especifica el número de Hola de bytes en el bloque de hello; Este valor debe ser no más de 4MB.|  
|`Block/@Id`|Attribute, String|Especifica una cadena que representa el identificador de bloque de hello para el bloque de Hola.|  
|`Block/@Hash`|Attribute, String|Especifica Hola hash MD5 codificado en base16 del bloque de Hola.|  
|`Blob/MetadataPath`|String|Opcional. Especifica la ruta de acceso relativa de Hola de un archivo de metadatos. Durante la importación, los metadatos de Hola se establecen en blob de destino de Hola. Durante una operación de exportación, los metadatos del blob de Hola se almacenan en archivo de metadatos de hello en unidad de Hola.|  
|`Blob/MetadataPath/@Hash`|Attribute, String|Especifica Hola hash MD5 codificado en base16 del archivo de metadatos del blob de Hola.|  
|`Blob/PropertiesPath`|String|Opcional. Especifica la ruta de acceso relativa de Hola de un archivo de propiedades. Durante una importación, se establecen propiedades de Hola en blob de destino de Hola. Durante una operación de exportación, propiedades del blob Hola se almacenan en archivo de propiedades de hello en unidad de Hola.|  
|`Blob/PropertiesPath/@Hash`|Attribute, String|Especifica Hola hash MD5 codificado en base16 del archivo de propiedades del blob de Hola.|  
  
## <a name="next-steps"></a>Pasos siguientes
 
* [API de REST de Storage Import/Export](/rest/api/storageimportexport/)
