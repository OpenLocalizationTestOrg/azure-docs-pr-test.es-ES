---
title: datos de aaaCopy hacia/desde el almacenamiento de blobs de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocopy blob datos en Data Factory de Azure. Utilice nuestro ejemplo: cómo toocopy tooand de datos de almacenamiento de blobs de Azure y base de datos de SQL Azure."
keywords: datos de blob, copia de blobs de azure
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a>Copiar datos tooor de almacenamiento de blobs de Azure mediante Data Factory de Azure
Este artículo explica cómo toouse Hola actividad de copia de Data Factory de Azure toocopy datos tooand desde el almacenamiento de blobs de Azure. Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.

## <a name="overview"></a>Información general
Puede copiar datos desde cualquier origen compatible almacenan tooAzure almacenamiento de blobs de datos o de datos de receptor de almacenamiento de blobs de Azure tooany admitida almacenan. Hello tabla siguiente proporciona una lista de almacenes de datos que se admiten como orígenes o receptores de actividad de copia de Hola. Por ejemplo, puede mover datos **de** una base de datos SQL Server o una base de datos Azure SQL **a** una instancia de Azure Blob Storage. Y, puede copiar datos **desde** Azure Blob Storage **hacia** una instancia de Azure SQL Data Warehouse o una colección de Azure Cosmos DB. 

## <a name="supported-scenarios"></a>Escenarios admitidos
Puede copiar datos **desde el almacenamiento de blobs de Azure** toohello siguientes almacenes de datos:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Puede copiar los datos de hello siguientes almacenes de datos **tooAzure almacenamiento de blobs**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> Actividad de copia es compatible con copia de datos de / tooboth cuentas de almacenamiento de Azure general y estrechamente/estupendo almacenamiento de blobs. admite la actividad Hello **leyendo de bloque, anexar o blobs en páginas**, pero es compatible con **escritura de blobs en bloques tooonly**. Azure Premium Storage no es compatible como receptor porque está respaldado por blobs en páginas.
> 
> Actividad de copia no elimina datos de origen de hello después Hola datos están correctamente copiados toohello destino. Si necesita datos de origen de toodelete después de una copia correcta, cree un [actividad personalizada](data-factory-use-custom-activities.md) toodelete Hola datos y usar actividad hello en canalización Hola. Para obtener un ejemplo, vea hello [ejemplo de Delete blob o una carpeta en GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity). 

## <a name="get-started"></a>Primeros pasos
Puede crear una canalización con actividad de copia que mueva los datos desde Azure Blob Storage o hacia él mediante el uso de diferentes herramientas o API.

toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Este artículo tiene un [tutorial](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) para crear una canalización de datos de toocopy de un tooanother de ubicación de almacenamiento de blobs de Azure ubicación de almacenamiento de blobs de Azure. Para obtener un tutorial sobre cómo crear un toocopy de datos de canalización desde una base de datos SQL de tooAzure de almacenamiento de blobs de Azure, consulte [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md).

También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:

1. Crear una **factoría de datos**. Una factoría de datos puede contener una o más canalizaciones. 
2. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink. Por ejemplo, si va a copiar datos desde una base de datos de SQL Azure del tooan de almacenamiento blob de Azure, cree dos toolink servicios vinculados su cuenta de almacenamiento de Azure y la factoría de datos de tooyour de base de datos de SQL Azure. Para las propiedades de servicio vinculado que son específico tooAzure almacenamiento de blobs, vea [vinculado propiedades del servicio](#linked-service-properties) sección. 
2. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. En el ejemplo de Hola mencionado en el último paso de hello, se crea un contenedor de blobs de hello toospecify de conjunto de datos y la carpeta que contiene los datos de entrada de Hola. Y crear tabla de otro conjunto de datos toospecify Hola SQL en la base de datos de SQL Azure de Hola que contiene los datos de hello copiados desde el almacenamiento de blobs de Hola. Para las propiedades del conjunto de datos que son específico tooAzure almacenamiento de blobs, vea [propiedades de conjunto de datos](#dataset-properties) sección.
3. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. En el ejemplo de Hola que se ha mencionado anteriormente, use BlobSource como un origen y SqlSink como un receptor para la actividad de copia de Hola. De forma similar, si va a copiar desde la base de datos de SQL Azure tooAzure almacenamiento de blobs, utilice SqlSource y BlobSink en la actividad de copia de Hola. Para copiar propiedades de actividad que son específico tooAzure almacenamiento de blobs, vea [copiar propiedades de la actividad](#copy-activity-properties) sección. Para obtener detalles sobre cómo toouse un almacén de datos como un origen o un receptor, haga clic en el vínculo de hello en la sección anterior de hello para el almacén de datos.  

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener ejemplos con definiciones de JSON para entidades de la factoría de datos que son utilizados toocopy datos hacia y desde un almacenamiento de blobs de Azure, vea [ejemplos JSON](#json-examples-for-copying-data-to-and-from-blob-storage  ) sección de este artículo.

Hello las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizados toodefine factoría de datos entidades específica tooAzure almacenamiento de blobs.

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Hay dos tipos de servicios vinculados que se puede usar toolink un generador de datos de Azure de tooan de almacenamiento de Azure. Se trata del servicio vinculado **AzureStorage** y el servicio vinculado **AzureStorageSas**. Hola servicio vinculado de almacenamiento de Azure proporciona factoría de datos de hello con acceso global toohello almacenamiento de Azure. Mientras que vinculado hello Azure almacenamiento SAS (firma de acceso compartido) servicio proporciona factoría de datos de hello con acceso restringido tiempo enlazadas toohello almacenamiento de Azure. No existen otras diferencias entre estos dos servicios vinculados. Elegir servicio de hello vinculado que se adapte a sus necesidades. Hello las secciones siguientes proporcionan más detalles sobre estos dos servicios vinculados.

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
toospecify un conjunto de datos toorepresent datos de entrada o salidas de un almacenamiento de blobs de Azure, Establece Hola de propiedad de tipo de conjunto de datos de Hola para: **AzureBlob**. Conjunto hello **linkedServiceName** servicio vinculado de propiedad del nombre de toohello de conjunto de datos de Hola de hello almacenamiento de Azure o SAS de almacenamiento de Azure.  propiedades de tipo Hello del conjunto de datos de hello especifican hello **contenedor de blobs** hello y **carpeta** Hola almacenamiento de blobs.

Para obtener una lista completa de secciones JSON y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).

Factoría de datos admite Hola después de valores de tipo conforme a CLS .NET según para proporcionar información de tipo en "estructura" para orígenes de datos de lectura de esquema como blobs de Azure: Int16, Int32, Int64, Single, Double, Decimal, Byte [], Bool, String, Guid, Datetime, DateTimeOffset, Timespan. Factoría de datos realiza automáticamente las conversiones de tipos al mover el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos.

Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y se proporciona información acerca de la ubicación de hello, etc., formato de datos de hello en el almacén de datos de Hola. sección typeProperties Hello para el conjunto de datos de tipo **AzureBlob** conjunto de datos tiene Hola propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| folderPath |Contenedor de toohello de ruta de acceso y la carpeta en el almacenamiento de blobs de Hola. Ejemplo: myblobcontainer\myblobfolder\ |Sí |
| fileName |Nombre del blob de Hola. La propiedad fileName es opcional y distingue entre mayúsculas y minúsculas.<br/><br/>Si especifica un nombre de archivo, funciona de la actividad (incluida la copia) de hello en Hola Blob en cuestión.<br/><br/>Cuando no se especifica el nombre de archivo, copia incluye todos los Blobs en folderPath hello para el conjunto de datos de entrada.<br/><br/>Cuando **fileName** no se especifica para un conjunto de datos de salida y **preserveHierarchy** no se especifica en el receptor de actividad, nombre de hello del archivo hello genera sería Hola siguiendo este formato: datos.<Guid>. txt (por ejemplo:: Data.0a405f8a 93ff 4c6f b3be f69616f1df7a.txt |No |
| partitionedBy |partitionedBy es una propiedad opcional. Se pueden usar toospecify un folderPath dinámica y nombre de archivo de datos de series temporales. Por ejemplo, se puede parametrizar folderPath por cada hora de datos. Vea hello [mediante partitionedBy propiedad sección](#using-partitionedBy-property) para obtener información detallada y ejemplos. |No |
| formato | se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Conjunto hello **tipo** propiedad en formato tooone de estos valores. Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida. |No |
| compresión | Especificar tipo de Hola y el nivel de compresión para datos de Hola. Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**. Los niveles admitidos son **Optimal** y **Fastest**. Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

### <a name="using-partitionedby-property"></a>Uso de la propiedad partitionedBy
Como se mencionó en la sección anterior de hello, puede especificar un folderPath dinámica y el nombre de archivo de datos de serie temporal con hello **partitionedBy** propiedad, [funciones de factoría de datos y las variables del sistema hello](data-factory-functions-variables.md).

Para más información sobre los conjuntos de datos de series temporales, la programación y los segmentos, consulte los artículos [Creación de conjuntos de datos](data-factory-create-datasets.md) y [Programación y ejecución](data-factory-scheduling-and-execution.md).

#### <a name="sample-1"></a>Ejemplo 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

En este ejemplo, {Slice} se reemplaza con el valor de Hola de variable del sistema SliceStart factoría de datos en formato de hello (AAAAMMDDHH) especificado. Hola SliceStart refiere a tiempo toostart de segmento de Hola. Hola folderPath es diferente para cada segmento. Por ejemplo: wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104

#### <a name="sample-2"></a>Ejemplo 2

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

En este ejemplo, year, month, day y time de SliceStart se extraen en variables independientes que se usan en las propiedades folderPath y fileName.

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, conjuntos de datos de entrada y salida, y directivas) están disponibles para todos los tipos de actividades. Mientras que propiedades disponibles en hello **typeProperties** sección de actividad hello varían con cada tipo de actividad. Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores. Si va a mover datos desde un almacenamiento de blobs de Azure, configure tipo de origen de hello en la actividad de copia de hello demasiado**BlobSource**. De forma similar, si va a mover datos tooan almacenamiento de blobs de Azure, Establece el tipo de receptor de hello en actividad de copia de hello demasiado**BlobSink**. Esta sección proporciona una lista de propiedades admitidas por BlobSource y BlobSink.

**BlobSource** admite Hola propiedades Hola siguientes **typeProperties** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| recursive |Indica si hello es leer los datos de forma recursiva de subcarpetas de Hola o solo de carpeta especificada de Hola. |True (valor predeterminado), False |No |

**BlobSink** admite Hola propiedades siguientes **typeProperties** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| copyBehavior |Define el comportamiento de la copia de hello al origen de hello es BlobSource o sistema de archivos. |<b>PreserveHierarchy</b>: conserva Hola jerarquía de archivos en la carpeta de destino de Hola. ruta de acceso relativa de Hola de carpeta de origen del archivo toosource es idéntico toohello ruta de acceso relativa de la carpeta de tootarget de archivo de destino.<br/><br/><b>FlattenHierarchy</b>: todos los archivos de la carpeta de origen Hola están en hello primero niveles de carpeta de destino. archivos de destino de Hello tienen nombre generado automáticamente. <br/><br/><b>MergeFiles</b>: combina todos los archivos del archivo de tooone de carpeta de origen de hello. Si se especifica Hola nombre de archivo o Blob, nombre de archivo combinado Hola sería Hola especificado de lo contrario, sería el nombre de archivo generado automáticamente. |No |

**BlobSource** también admite estas dos propiedades para ofrecer compatibilidad con versiones anteriores.

* **treatEmptyAsNull**: Especifica si una cadena nula o vacía tootreat como un valor nulo.
* **skipHeaderLineCount** : especifica cuántas líneas deben omitirse. Es aplicable únicamente cuando el conjunto de datos de entrada usa TextFormat.

De forma similar, **BlobSink** admite Hola después de propiedad para la compatibilidad con versiones anteriores.

* **blobWriterAddHeader**: Especifica si el conjunto de datos de salida de un encabezado de definiciones de columna al escribir tooan tooadd.

Hola de conjuntos de datos ahora compatibilidad con propiedades que implementan siguientes Hola misma funcionalidad: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.

Hello tabla siguiente proporciona orientación sobre el uso de propiedades de conjunto de datos nuevo hello en lugar de estas propiedades de origen/receptor de blob.

| Propiedad de la actividad de copia | Propiedad de conjunto de datos |
|:--- |:--- |
| skipHeaderLineCount en BlobSource |skipLineCount y firstRowAsHeader. Las líneas se omiten en primer lugar y, a continuación, se lee la primera fila de Hola como un encabezado. |
| treatEmptyAsNull en BlobSource |treatEmptyAsNull en el conjunto de datos de entrada |
| blobWriterAddHeader en BlobSink |firstRowAsHeader en el conjunto de datos de salida |

Consulte la sección [Especificación de TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) para obtener información detallada acerca de estas propiedades.    

### <a name="recursive-and-copybehavior-examples"></a>Ejemplos de recursive y copyBehavior
Esta sección describe el comportamiento resultante de Hola de operación de copia de Hola para diferentes combinaciones de valores recursiva y copyBehavior.

| recursive | copyBehavior | Comportamiento resultante |
| --- | --- | --- |
| true |preserveHierarchy |Para una carpeta de origen carpeta1 con hello siguiente estructura: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>se crea la carpeta de destino de Hello carpeta1 con hello misma estructura como origen de Hola<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5. |
| true |flattenHierarchy |Para una carpeta de origen carpeta1 con hello siguiente estructura: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>se crea el destino de Hola carpeta1 con hello siguiente estructura: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File5 |
| true |mergeFiles |Para una carpeta de origen carpeta1 con hello siguiente estructura: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>se crea el destino de Hola carpeta1 con hello siguiente estructura: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;El contenido de File1 + File2 + File3 + File4 + File 5 se combina en un archivo con un nombre de archivo generado automáticamente |
| false |preserveHierarchy |Para una carpeta de origen carpeta1 con hello siguiente estructura: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>se crea la carpeta de destino de Hello carpeta1 con hello siguiendo estructura<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/><br/><br/>No se selecciona la subcarpeta Subfolder1, que contiene los archivos File3, File4 y File5. |
| false |flattenHierarchy |Para una carpeta de origen carpeta1 con hello siguiente estructura:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>se crea la carpeta de destino de Hello carpeta1 con hello siguiendo estructura<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File2<br/><br/><br/>No se selecciona la subcarpeta Subfolder1, que contiene los archivos File3, File4 y File5. |
| false |mergeFiles |Para una carpeta de origen carpeta1 con hello siguiente estructura:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>se crea la carpeta de destino de Hello carpeta1 con hello siguiendo estructura<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;El contenido de File1 + File2 se combina en un archivo con un nombre de archivo generado automáticamente. Nombre de archivo generado automáticamente para File1<br/><br/>No se selecciona la subcarpeta Subfolder1, que contiene los archivos File3, File4 y File5. |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a>Tutorial: Datos de toocopy usar el Asistente para copia de almacenamiento de blobs
Echemos un vistazo a cómo el almacenamiento de blobs tooquickly copiar datos desde un Azure. En este tutorial, los almacenes de datos de origen y destino son de tipo: Azure Blob Storage. Hello canalización en este tutorial copia datos de una carpeta de tooanother en hello mismo contenedor de blob. Este tutorial es deliberadamente simple tooshow valores o propiedades cuando se usa el almacenamiento de blobs como origen o receptor. 

### <a name="prerequisites"></a>Requisitos previos
1. Si aún no tiene una, cree una **cuenta de Azure Storage** de uso general. Usar el almacenamiento de blobs de hello como **origen** y **destino** almacén de datos en este tutorial. Si no tiene una cuenta de almacenamiento de Azure, vea hello [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artículo para toocreate pasos uno.
2. Crear un contenedor de blobs denominado **adfblobconnector** en la cuenta de almacenamiento de Hola. 
4. Cree una carpeta denominada **entrada** en hello **adfblobconnector** contenedor.
5. Cree un archivo denominado **emp.txt** con hello después de contenido y cargarlo toohello **entrada** carpeta mediante herramientas como [Explorador de almacenamiento de Azure](https://azurestorageexplorer.codeplex.com/)
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a>Crear Hola factoría de datos
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **+ nuevo** desde la esquina superior izquierda de hello, haga clic en **Intelligence + análisis**y haga clic en **factoría de datos**.
3. Hola **factoría de datos** hoja:   
    1. Escriba **ADFBlobConnectorDF** para hello **nombre**. nombre de Hola Hola Azure factoría de datos debe ser único globalmente. Si recibe el error hello: `*Data factory name “ADFBlobConnectorDF” is not available`, cambiar nombre de Hola Hola factoría de datos (por ejemplo, yournameADFBlobConnectorDF) y pruebe a crear de nuevo. Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.
    2. Selección la **suscripción**de Azure.
    3. Para el grupo de recursos, seleccione **usar existente** tooselect una existente recursos grupo (o) seleccione **crear nuevo** tooenter un nombre para un grupo de recursos.
    4. Seleccione un **ubicación** de factoría de datos de Hola.
    5. Seleccione **toodashboard Pin** casilla situada en la parte inferior de Hola de hoja de Hola.
    6. Haga clic en **Crear**.
3. Una vez completada la creación de hello, vea hello **factoría de datos** hoja como se muestra en hello después de imagen: ![página principal de generador de datos](./media/data-factory-azure-blob-connector/data-factory-home-page.png)

### <a name="copy-wizard"></a>Asistente para copia
1. En la página de inicio de la factoría de datos de hello, haga clic en hello **copiar datos [vista previa]** icono toolaunch **Asistente para copia de datos** en una pestaña independiente.    
    
    > [!NOTE]
    >    Si ve ese explorador web de hello está atascado en "Autorizar …", deshabilite o desactive **bloquear las cookies de terceros y datos de sitio** configuración (o) manténgala habilitada y cree una excepción para **login.microsoftonline.com**y, a continuación, intente iniciar Asistente de Hola de nuevo.
2. Hola **propiedades** página:
    1. Escriba **CopyPipeline** en **Task name** (Nombre de tarea). nombre de la tarea de Hello es Hola de canalización de saludo de la factoría de datos.
    2. Escriba un **descripción** para la tarea de hello (opcional).
    3. Para **cadencia de tarea o la programación de tareas**, mantener hello **ejecute con regularidad en programación** opción. Si desea que toorun esta tarea solo una vez en lugar de ejecutar repetidamente según una programación, seleccione **ejecutar una vez ahora**. Si selecciona la opción **Run once now** (Ejecutar una vez ahora), se crea una [canalización única](data-factory-create-pipelines.md#onetime-pipeline). 
    4. Mantener valores de hello para **periódica patrón**. Esta tarea se ejecuta diariamente entre Hola empezar y terminar horas se especifique en el paso siguiente de Hola.
    5. Hola de cambio **fecha hora de inicio** demasiado**21/04/2017**. 
    6. Hola de cambio **fecha hora de finalización** demasiado**04/25/2017**. Puede que desee fecha de hello tootype en lugar de examinar calendario Hola.     
    8. Haga clic en **Siguiente**.
      ![Herramienta de copia: Página de propiedades](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png) 
3. En hello **almacén de datos de origen** página, haga clic en **almacenamiento de blobs de Azure** icono. Utilice este almacén de datos de origen de página toospecify hello para la tarea de copia de hello. Puede usar un servicio vinculado del almacén de datos existente, o bien especificar un almacén de datos nuevo. servicio vinculado de toouse existente, se debe seleccionar **de existente servicios vinculados** y seleccione Hola derecho servicio vinculado. 
    ![Herramienta de copia: Página de almacén de datos de origen](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)
4. En hello **especificar cuenta de almacenamiento de blobs de Azure de hello** página:
   1. Mantener el nombre generado automáticamente Hola para **nombre de la conexión**. nombre de la conexión de Hello es el nombre de hello del servicio de hello vinculado del tipo: el almacenamiento de Azure. 
   2. Confirme que la opción **De suscripciones de Azure** está seleccionada para **Método de selección de cuenta**.
   3. Seleccione la suscripción de Azure o mantenga **Seleccionar todo** para **Suscripción de Azure**.   
   4. Seleccione un **cuenta de almacenamiento de Azure** de hello cuentas disponible en la suscripción de hello seleccionado lista de almacenamiento de Azure. También puede elegir tooenter configuración de la cuenta de almacenamiento manualmente mediante la selección **escribir manualmente** opción para hello **método de selección de la cuenta**.
   5. Haga clic en **Siguiente**. 
      ![Herramienta Copiar: especificar la cuenta de almacenamiento de blobs de Azure Hola](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)
5. En **Elegir archivo de entrada de Hola o una carpeta** página:
   1. Haga doble clic en **adfblobcontainer**.
   2. Seleccione **entrada** y haga clic en **Elegir**. En este tutorial, se selecciona la carpeta de entrada de Hola. También podría seleccionar archivo de hello emp.txt en la carpeta de hello en su lugar. 
      ![Herramienta Copiar: elegir el archivo de entrada de Hola o una carpeta](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)
6. En hello **Elegir archivo de entrada de Hola o una carpeta** página:
    1. Confirme que hello **archivo o carpeta** se establece demasiado**adfblobconnector/entrada**. Si hay archivos de hello en subcarpetas, por ejemplo, de 2017/04/01, 2017/04/02 y así sucesivamente, escriba adfblobconnector/entrada / {year} / {month} / {day} para archivo o carpeta. Al presionar TAB fuera del cuadro de texto hello, verá tres formatos de tooselect listas desplegables para year (aaaa), month (MM) y día (dd). 
    2. No marque la casilla **Copy file recursively** (Copiar archivo de forma recursiva). Seleccione este recorrido de toorecursively opción a través de las carpetas de destino de archivos toobe toohello copiada. 
    3. Hola no **copia binaria** opción. Seleccione este tooperform opción una copia binaria del destino de toohello del archivo de origen. No seleccione para este tutorial para que puedan ver más opciones para páginas siguientes del saludo. 
    4. Confirme que hello **el tipo de compresión** se establece demasiado**ninguno**. Seleccione un valor para esta opción si los archivos de origen están comprimidos en uno de los formatos de hello compatible. 
    5. Haga clic en **Siguiente**.
    ![Herramienta Copiar: elegir el archivo de entrada de Hola o una carpeta](./media/data-factory-azure-blob-connector/chose-input-file-folder.png) 
7. En hello **configuración de formato de archivo** página, verá los delimitadores de Hola y Hola esquema detecta automáticamente por el Asistente de hello bien analizando el archivo hello. 
    1. Confirmar Hola siguientes opciones: una. Hola **formato de archivo** se establece demasiado**formato de texto**. Puede ver todos los formatos de hello compatibles en la lista desplegable de Hola. Por ejemplo: JSON, Avro, ORC, Parquet.
        b. Hola **delimitador de columna** se establece demasiado`Comma (,)`. Puede ver Hola otros delimitadores de columna admitidos por factoría de datos en la lista desplegable de Hola. También puede especificar un delimitador personalizado.
        c. Hola **delimitador de filas** se establece demasiado`Carriage Return + Line feed (\r\n)`. Puede ver Hola otros delimitadores de fila admitidos por factoría de datos en la lista desplegable de Hola. También puede especificar un delimitador personalizado.
        d. Hola **omitir recuento de líneas** se establece demasiado**0**. Si desea que unos toobe líneas omiten en la parte superior de hello del archivo hello, escriba aquí el número de Hola.
        e.  Hola **primera fila de datos contiene nombres de columna** no se ha establecido. Si los archivos de origen de hello contienen nombres de columna en la primera fila de hello, seleccione esta opción.
        f. Hola **tratar el valor de la columna vacía como null** opción está establecida.
    2. Expanda **configuración avanzada** toosee avanzada opción disponible.
    3. En parte inferior de Hola de página de hello, vea hello **vista previa** de datos de archivo de hello emp.txt.
    4. Haga clic en **esquema** pestaña en el esquema de hello inferior toosee Hola ese asistente para copiar de hello inferida examinando datos hello en el archivo de código fuente de Hola.
    5. Haga clic en **siguiente** después de revisar los delimitadores de Hola y obtener una vista previa de los datos.
    ![Herramienta de copia: Configuración de formato de archivo](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)  
8. En hello **página de almacén de datos de destino**, seleccione **almacenamiento de blobs de Azure**y haga clic en **siguiente**. Hola almacenamiento de blobs de Azure que usa como ambos almacenes de datos de origen y destino de hello en este tutorial.    
    ![Herramienta de copia: Selección del almacén de datos de destino](media/data-factory-azure-blob-connector/select-destination-data-store.png)
9. En **especificar cuenta de almacenamiento de blobs de Azure de hello** página:
   1. Escriba **AzureStorageLinkedService** para hello **nombre de la conexión** campo.
   2. Confirme que la opción **De suscripciones de Azure** está seleccionada para **Método de selección de cuenta**.
   3. Selección la **suscripción**de Azure.  
   4. Seleccione su cuenta de almacenamiento de Azure. 
   5. Haga clic en **Siguiente**.     
10. En hello **Hola Elegir archivo o carpeta de salida** página: 
    6. Especifique la **ruta de acceso de carpeta** como **adfblobconnector/output/{year}/{month}/{day}**. Escriba **TAB**.
    7. Para hello **año**, seleccione **aaaa**.
    8. Para hello **mes**, confirme que está establecido demasiado**MM**.
    9. Para hello **día**, confirme que está establecido demasiado**dd**.
    10. Confirme que hello **el tipo de compresión** se establece demasiado**ninguno**.
    11. Confirme que hello **Copiar comportamiento** se establece demasiado**combinar archivos**. Si el archivo con hello ya existe el mismo nombre de salida de hello, hello contenido nuevo es agregado toohello mismo archivo al final de Hola.
    12. Haga clic en **Siguiente**.
    ![Herramienta de copia: Selección del archivo o la carpeta de salida](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)
11. En hello **configuración de formato de archivo** página, revise la configuración de Hola y haga clic en **siguiente**. Una de estas opciones adicionales de hello es tooadd un archivo de salida de encabezado toohello. Si selecciona esta opción, se agrega una fila de encabezado con nombres de columnas de hello del esquema de Hola de origen Hola. Puede cambiar los nombres de columna predeterminados de hello al ver el esquema de hello para el origen de Hola. Por ejemplo, puede cambiar Hola primera columna tooFirst nombre y la segunda columna tooLast nombre. A continuación, archivo de salida de hello se genera con un encabezado con estos nombres como nombres de columna. 
    ![Herramienta de copia: Configuración del formato de archivo de destino](media/data-factory-azure-blob-connector/file-format-destination.png)
12. En hello **configuración de rendimiento** página, confirme que **unidades en la nube** y **copias en paralelo** se establecen demasiado**automática**y haga clic en siguiente. Para más información sobre esta configuración, consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md#parallel-copy).
    ![Herramienta de copia: Configuración de rendimiento](media/data-factory-azure-blob-connector/copy-performance-settings.png) 
14. En hello **resumen** página, revise todas las configuraciones (propiedades de la tarea, configuración de origen y de destino y Copiar configuración) y haga clic en **siguiente**.
    ![Herramienta de copia: Página de resumen](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)
15. Revise la información en hello **resumen** página y haga clic en **finalizar**. Asistente de Hello crea dos servicios vinculados, dos conjuntos de datos (entrada y salida) y una canalización de factoría de datos de hello (desde donde se haya iniciado Hola Asistente para copiar).
    ![Herramienta de copia: Página de implementación](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)

### <a name="monitor-hello-pipeline-copy-task"></a>Supervisar la canalización de hello (tarea de copia)

1. Haga clic en el vínculo de hello `Click here toomonitor copy pipeline` en hello **implementación** página. 
2. Debería ver Hola **supervisar y administrar aplicaciones** en una pestaña independiente.  ![Supervisar y administrar la aplicación](media/data-factory-azure-blob-connector/monitor-manage-app.png)
3. Hola de cambio **iniciar** de demasiado tiempo en la parte superior de hello`04/19/2017` y **final** demasiado tiempo`04/27/2017`y, a continuación, haga clic en **aplicar**. 
4. Debería ver cinco ventanas de la actividad en hello **WINDOWS actividad** lista. Hola **WindowStart** veces deben cubrir todos los días de horas de finalización de toopipeline de inicio de canalización. 
5. Haga clic en **actualizar** botón para hello **WINDOWS actividad** lista varias veces hasta que vea Estado Hola de todas las ventanas de la actividad de Hola se establece tooReady. 
6. Ahora, compruebe que se generan archivos de salida de hello en carpeta de salida de hello de contenedor adfblobconnector. Debería ver Hola siguiendo la estructura de carpetas en la carpeta de salida de hello: 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
Para más información sobre la supervisión y administración de factorías de datos, consulte el artículo [Supervisión y administración de canalizaciones de Data Factory](data-factory-monitor-manage-app.md). 
 
### <a name="data-factory-entities"></a>Entidades de Factoría de datos
Ahora, cambie toohello back-pestaña con la página principal de hello factoría de datos. Observe que ahora hay en su factoría de datos dos servicios vinculados, dos conjuntos de datos y una canalización. 

![Página principal de Data Factory con entidades](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

Haga clic en **autor e implementar** toolaunch Editor de generador de datos. 

![Editor de la Factoría de datos](media/data-factory-azure-blob-connector/data-factory-editor.png)

Debería ver Hola siguiendo las entidades de la factoría de datos de la factoría de datos: 

 - Dos servicios vinculados. Uno para el origen de Hola y Hola otro destino Hola. Ambos servicios Hola vinculado que hacen referencia toohello misma cuenta de almacenamiento de Azure en este tutorial. 
 - Dos conjuntos de datos. Un conjunto de datos de entrada y un conjunto de datos de salida. En este tutorial, ambos usan Hola mismo contenedor de blob, pero hacen referencia a las carpetas de toodifferent (entrada y salida).
 - Una canalización. canalización de Hello contiene una actividad de copia que utiliza un origen de blobs y una blob receptor toocopy de datos de un tooanother de ubicación de blob de Azure ubicación del blob de Azure. 

Hello las secciones siguientes proporcionan más información acerca de estas entidades. 

#### <a name="linked-services"></a>Servicios vinculados
Verá dos servicios vinculados. Uno para el origen de Hola y Hola otro destino Hola. En este tutorial, ambos buscar definiciones Hola mismo salvo para los nombres de Hola. Hola **tipo** de hello servicio vinculado se establece demasiado**AzureStorage**. Propiedad más importante de la definición del servicio vinculado de hello es hello **connectionString**, que se usa por factoría de datos tooconnect tooyour cuenta de almacenamiento de Azure en tiempo de ejecución. Caso omiso hello hubName propiedad en la definición de Hola. 

##### <a name="source-blob-storage-linked-service"></a>Servicio vinculado de almacenamiento de blobs de origen
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a>Servicio vinculado de almacenamiento de blobs de destino

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

Para más información sobre el servicio vinculado Azure Storage, consulte la sección [Propiedades del servicio vinculado](#linked-service-properties). 

#### <a name="datasets"></a>Conjuntos de datos
Hay dos conjuntos de datos: un conjunto de datos de entrada y un conjunto de datos de salida. tipo de Hello del conjunto de datos de Hola se establece demasiado**AzureBlob** para ambos. 

conjunto de datos de entrada de Hello señala toohello **entrada** carpeta de hello **adfblobconnector** contenedor de blobs. Hola **externo** propiedad se establece demasiado**true** para este conjunto de datos como Hola datos no se crea por canalización Hola con la actividad de copia de Hola que toma este conjunto de datos como entrada. 

Hola toohello de puntos del conjunto de datos de salida **salida** carpeta de hello mismo contenedor de blob. Hello conjunto de datos de salida también utiliza Hola año, mes y día de hello **SliceStart** toodynamically variable del sistema evaluar la ruta de acceso de hello para el archivo de salida de hello. Para ver la lista de funciones y variables del sistema que admite Data Factory, consulte [Azure Data Factory: funciones y variables del sistema](data-factory-functions-variables.md). Hola **externo** propiedad se establece demasiado**false** (valor predeterminado) porque este conjunto de datos generado por la canalización de Hola. 

Para más información sobre las propiedades admitidas por el conjunto de datos de blob de Azure, consulte la sección [Propiedades del conjunto de datos](#dataset-properties).

##### <a name="input-dataset"></a>Conjunto de datos de entrada

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a>Conjunto de datos de salida

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a>Canalización
canalización de Hello tiene solo una actividad. Hola **tipo** de hello actividad se establece demasiado**copia**.  En Propiedades de tipos de Hola de actividad hello, hay dos secciones, una para el origen y hello otro para el receptor. tipo de origen de Hola se establece demasiado**BlobSource** como actividad hello es copiar datos desde un almacenamiento de blobs. Hello el tipo de receptor se establece demasiado**BlobSink** como actividad hello copiando el almacenamiento de blobs de datos tooa. actividad de copia de Hello toma InputDataset z4y como entrada de Hola y OutputDataset z4y como salida de hello. 

Para más información sobre las propiedades admitidas por BlobSource y BlobSink, consulte la sección [Propiedades de la actividad de copia](#copy-activity-properties). 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a>Ejemplos JSON para copiar datos tooand del almacenamiento de blobs  
Hello en los ejemplos siguientes proporcionan las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Muestran cómo toocopy tooand de datos de almacenamiento de blobs de Azure y base de datos de SQL Azure. Sin embargo, se pueden copiar datos **directamente** desde cualquiera de tooany orígenes de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a>Ejemplo JSON: Copiar los datos de almacenamiento de blobs tooSQL base de datos
Hola el siguiente ejemplo se muestra:

1. Un servicio vinculado de tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
5. Una [canalización](data-factory-create-pipelines.md) con una actividad de copia que usa [BlobSource](#copy-activity-properties) y [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).

ejemplo de Hola copia datos de serie temporal de una tabla de SQL Azure tooan de blobs de Azure cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

**Servicio vinculado SQL de Azure:**

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Servicio vinculado de Almacenamiento de Azure:**

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
Azure Data Factory admite dos tipos de servicios vinculados de Azure Storage: **AzureStorage** y **AzureStorageSas**. Para Hola primero, especificar cadena de conexión de Hola que incluye la clave de la cuenta de hello y para hello uno posterior, especificar Hola Uri de firma de acceso compartido (SAS). Para más información, consulte la sección [Servicios vinculados](#linked-service-properties).  

**Conjunto de datos de entrada de blob de Azure:**

Los datos se seleccionan de un nuevo blob cada hora (frecuencia: hora, intervalo: 1). Hola ruta de acceso y nombre de la carpeta para el blob de Hola se evalúan dinámicamente en función del tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta de Hello utiliza year, month y parte del día de la hora de inicio de Hola y el nombre de archivo usa parte de hora de inicio de Hola Hola. "externo": "true" configuración indica factoría de datos de esa tabla hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
**Conjunto de datos de salida SQL de Azure:**

ejemplo de Hola copia la tabla de tooa de datos denominado "MyTable" en una base de datos de SQL Azure. Crear tabla de hello en la base de datos de SQL Azure con Hola mismo número de columnas, tal como se esperaba toocontain de archivo CSV de Blob de Hola. Se agregan nuevas filas toohello tabla cada hora.

```json
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Una actividad de copia en una canalización con el origen de blob y el receptor SQL:**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**BlobSource** y **receptor** tipo está establecido demasiado**SqlSink**.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a>Ejemplo JSON: Copiar los datos de SQL Azure tooAzure Blob
Hola el siguiente ejemplo se muestra:

1. Un servicio vinculado de tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](#dataset-properties).
5. Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) y [BlobSink](#copy-activity-properties).

ejemplo Hello copia datos de serie temporal de un tooan de tabla de SQL Azure blob de Azure cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

**Servicio vinculado SQL de Azure:**

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Servicio vinculado de Almacenamiento de Azure:**

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
Azure Data Factory admite dos tipos de servicios vinculados de Azure Storage: **AzureStorage** y **AzureStorageSas**. Para Hola primero, especificar cadena de conexión de Hola que incluye la clave de la cuenta de hello y para hello uno posterior, especificar Hola Uri de firma de acceso compartido (SAS). Para más información, consulte la sección [Servicios vinculados](#linked-service-properties).  

**Conjunto de datos de entrada SQL de Azure:**

ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en SQL Azure y contiene una columna denominada "timestampcolumn" para los datos de serie temporal.

Establecer "externo": "true" informa a servicio Data Factory esa tabla hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.

```json
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Conjunto de datos de salida de blob de Azure:**

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1). ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Actividad de copia en una canalización con el origen SQL y el receptor de blob:**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**SqlSource** y **receptor** tipo está establecido demasiado**BlobSink**. consulta SQL Hola especificada para hello **SqlReaderQuery** propiedad selecciona datos Hola Hola más allá de hora toocopy.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureSQLInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
         ]
    }
}
```

> [!NOTE]
> columnas de toomap de toocolumns de conjunto de datos de origen del conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Rendimiento y optimización
Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.
