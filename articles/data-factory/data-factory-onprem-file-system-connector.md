---
title: datos de aaaCopy hacia/desde un sistema de archivos con Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocopy tooand de datos desde un sistema de archivos local mediante el uso de Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a>Copiar datos tooand desde un sistema de archivos local mediante Data Factory de Azure
Este artículo explica cómo toouse Hola actividad de copia de datos de Data Factory de Azure toocopy a/desde un sistema de archivos local. Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.

## <a name="supported-scenarios"></a>Escenarios admitidos
Puede copiar datos **desde un sistema de archivos local** toohello siguientes almacenes de datos:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Puede copiar los datos de hello siguientes almacenes de datos **tooan sistema de archivos local**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Actividad de copia no elimina archivos de origen de Hola cuando este destino toohello copió correctamente. Si necesita toodelete archivo de código fuente de hello después de una copia correcta, cree un archivo de actividad personalizada toodelete hello y usar actividad hello en la canalización de Hola. 

## <a name="enabling-connectivity"></a>Habilitación de la conectividad
Factoría de datos admite la conexión tooand desde un sistema de archivos local a través de **Data Management Gateway**. Debe instalar Hola Data Management Gateway en su entorno local para hello factoría de datos servicio tooconnect tooany local compatible almacén de datos incluyendo el sistema de archivos. toolearn acerca de Data Management Gateway y para obtener instrucciones paso a paso sobre cómo configurar la puerta de enlace de hello, consulte [mover datos entre orígenes locales y en la nube con Data Management Gateway hello](data-factory-move-data-between-onprem-and-cloud.md). Aparte de Data Management Gateway, no hay otros archivos binarios deben toobe instalado toocommunicate tooand desde un sistema de archivos local. Debe instalar y usar Hola Data Management Gateway incluso si es de sistema de archivos de hello en VM de IaaS de Azure. Para obtener información detallada acerca de la puerta de enlace de hello, consulte [Data Management Gateway](data-factory-data-management-gateway.md).

instalar un recurso compartido de archivos de Linux, toouse [Samba](https://www.samba.org/) en el servidor Linux e instalar Data Management Gateway en un servidor de Windows. No se admite la instalación de la puerta de enlace de administración de datos en un servidor Linux.

## <a name="getting-started"></a>Introducción
Puede crear una canalización con actividad de copia que mueva los datos desde un sistema de archivos o hacia él mediante el uso de distintas herramientas o API.

toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.

También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:

1. Crear una **factoría de datos**. Una factoría de datos puede contener una o más canalizaciones. 
2. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink. Por ejemplo, si va a copiar datos desde un sistema de archivos de blob de Azure almacenamiento tooan local, cree dos toolink servicios vinculados su sistema de archivos local y la factoría de datos de almacenamiento de Azure cuenta tooyour. Para las propiedades de servicio vinculado que el sistema de archivos local tooan específicos, consulte [vinculado propiedades del servicio](#linked-service-properties) sección.
3. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. En el ejemplo de Hola mencionado en el último paso de hello, se crea un contenedor de blobs de hello toospecify de conjunto de datos y la carpeta que contiene los datos de entrada de Hola. Y crear otro conjunto de datos toospecify Hola carpeta y nombre de archivo (opcional) en el sistema de archivos. Para el sistema de archivos de propiedades de conjunto de datos que son locales tooon específicos, consulte [propiedades de conjunto de datos](#dataset-properties) sección.
4. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. En el ejemplo de Hola que se ha mencionado anteriormente, use BlobSource como un origen y FileSystemSink como un receptor para la actividad de copia de Hola. De forma similar, si va a copiar de tooAzure de sistema de archivos local almacenamiento de blobs, utilice FileSystemSource y BlobSink en la actividad de copia de Hola. Para las propiedades de la actividad de copia local tooon específico de sistema de archivos, consulte [copiar propiedades de la actividad](#copy-activity-properties) sección. Para obtener detalles sobre cómo toouse un almacén de datos como un origen o un receptor, haga clic en el vínculo de hello en la sección anterior de hello para el almacén de datos.

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener ejemplos con definiciones de JSON para entidades de la factoría de datos que son utilizados toocopy datos hacia y desde un sistema de archivos, vea [ejemplos JSON](#json-examples-for-copying-data-to-and-from-file-system) sección de este artículo.

Hello las secciones siguientes proporciona detalles acerca de las propiedades JSON que están toodefine usado factoría de datos entidades específicas toofile sistema:

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Puede vincular un generador de datos de Azure local tooan de sistema de archivo con hello **servidor de archivos local** servicio vinculado. Hello en la tabla siguiente proporciona descripciones para los elementos JSON que sean específico toohello servicio servidor de archivos local vinculado.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |Asegúrese de que la propiedad de tipo hello está establecido demasiado**OnPremisesFileServer**. |Sí |
| host |Especifica la ruta de acceso de raíz de Hola de carpeta de Hola que desea toocopy. Utilice el carácter de escape de hello ' \ ' para los caracteres especiales en la cadena de Hola. Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) . |Sí |
| userid |Especifique el identificador de Hola Hola del usuario de que tiene acceso toohello servidor. |No (si elige encryptedCredential) |
| Contraseña |Especifique la contraseña de hello para el usuario de hello (userid). |No (si elige encryptedCredential) |
| encryptedCredential |Especifique las credenciales de hello cifrada que pueden obtener ejecutando el cmdlet New-AzureRmDataFactoryEncryptValue Hola. |No (si elige toospecify identificador de usuario y una contraseña en texto sin formato) |
| gatewayName |Especifica el nombre de Hola de puerta de enlace de Hola que factoría de datos debe usar el servidor de archivos de tooconnect toohello local. |Sí |


### <a name="sample-linked-service-and-dataset-definitions"></a>Ejemplos de definiciones de servicio vinculado y conjunto de datos
| Escenario | Host en definición de servicio vinculado | folderPath en definición de conjunto de datos |
| --- | --- | --- |
| Carpeta local en la máquina de Data Management Gateway::  <br/><br/>Ejemplos: D:\\\* o D:\folder\subfolder\\* |D:\\\\ (para Data Management Gateway 2.0 y versiones posteriores) <br/><br/> localhost (para versiones anteriores a Data Management Gateway 2.0) |\\\\ o la carpeta\\\\subcarpeta (Data Management Gateway 2.0 y versiones posteriores) <br/><br/>D:\\\\ o D:\\\\carpeta\\\\subcarpeta (para versiones de la puerta de enlace interiores a 2.0) |
| Carpeta compartida remota:  <br/><br/>Ejemplos: \\\\myserver\\share\\\* o \\\\myserver\\share\\folder\\subfolder\\* |\\\\\\\\myserver\\\\ |.\\\\ o carpeta\\\\subcarpeta |


### <a name="example-using-username-and-password-in-plain-text"></a>Ejemplo: uso de nombre de usuario y contraseña en texto sin formato

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a>Ejemplo: uso de encryptedcredential

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para ver una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, consulte [Creación de conjuntos de datos](data-factory-create-datasets.md). Las secciones como estructura, disponibilidad y directiva de un JSON de conjunto de datos son similares para todos los tipos de conjunto de datos.

sección de typeProperties Hello es diferente para cada tipo de conjunto de datos. Proporciona información como ubicación de Hola y el formato de datos de hello en el almacén de datos de Hola. Hola typeProperties sección Hola conjunto de datos de tipo **FileShare** tiene Hola propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| folderPath |Especifica la carpeta de hello subruta toohello. Utilice el carácter de escape de hello ' \' para los caracteres especiales en la cadena de Hola. Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .<br/><br/>Puede combinar esta propiedad con **partitionBy** toohave de rutas de acceso de carpeta según fechas y horas de inicio y fin. |Sí |
| fileName |Especifique el nombre de hello del archivo hello en hello **folderPath** si desea Hola tabla toorefer tooa archivo específico en la carpeta de Hola. Si no especifica ningún valor para esta propiedad, tabla de hello señala tooall archivos en la carpeta de Hola.<br/><br/>Cuando **fileName** no se especifica para un conjunto de datos de salida y **preserveHierarchy** no se especifica en el receptor de actividad, nombre de hello del archivo hello generado está en hello siguiendo el formato: <br/><br/>`Data.<Guid>.txt` (Ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |No |
| fileFilter |Especifique un filtro toobe utiliza tooselect un subconjunto de archivos en folderPath hello en lugar de todos los archivos. <br/><br/>Valores permitidos son: `*` (varios caracteres) y `?` (un único individual).<br/><br/>Ejemplo 1: "fileFilter": "*.log"<br/>Ejemplo 2: "fileFilter": 2014-1-?.txt"<br/><br/>Tenga en cuenta que fileFilter es aplicable a un conjunto de datos de FileShare de entrada. |No |
| partitionedBy |Puede usar partitionedBy toospecify dinámica folderPath/nombre de archivo para los datos de serie temporal. Por ejemplo, folderPath se parametriza por cada hora de datos. |No |
| formato | se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Conjunto hello **tipo** propiedad en formato tooone de estos valores. Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida. |No |
| compresión | Especificar tipo de Hola y el nivel de compresión para datos de Hola. Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**. Los niveles admitidos son **Optimal** y **Fastest**. consulte [Formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

> [!NOTE]
> No se puede usar fileName y fileFilter a la vez.

### <a name="using-partitionedby-property"></a>Uso de la propiedad partitionedBy
Como se mencionó en la sección anterior de hello, puede especificar un folderPath dinámica y el nombre de archivo de datos de serie temporal con hello **partitionedBy** propiedad, [funciones de factoría de datos y las variables del sistema hello](data-factory-functions-variables.md).

toounderstand más detalles sobre los conjuntos de datos de series temporales, programación y sectores, consulte [crear conjuntos de datos](data-factory-create-datasets.md), [ejecución y programación](data-factory-scheduling-and-execution.md), y [crear canalizaciones](data-factory-create-pipelines.md).

#### <a name="sample-1"></a>Muestra 1:

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

En este ejemplo, {Slice} se reemplaza con el valor de Hola de variable del sistema Hola factoría de datos SliceStart en formato de hello (AAAAMMDDHH). SliceStart refiere a tiempo toostart de segmento de Hola. Hola folderPath es diferente para cada segmento. Por ejemplo: wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Ejemplo 2:

```JSON
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

En este ejemplo, año, mes, día y hora de SliceStart se extraen en variables independientes que usan propiedades folderPath y fileName de Hola.

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, conjuntos de datos de entrada y salida, y directivas) están disponibles para todos los tipos de actividades. Mientras que propiedades disponibles en hello **typeProperties** sección de actividad hello varían con cada tipo de actividad.

Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores. Si va a mover datos desde un sistema de archivos local, establecer tipo de origen de hello en la actividad de copia de hello demasiado**FileSystemSource**. De forma similar, si va a mover datos tooan sistema de archivos local, establezca el tipo de receptor de hello en la actividad de copia de hello demasiado**FileSystemSink**. Esta sección proporciona una lista de las propiedades compatibles con FileSystemSource y FileSystemSink.

**FileSystemSource** admite Hola propiedades siguientes:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| recursive |Indica si los datos de Hola es de lectura de forma recursiva de las subcarpetas de Hola o solo de la carpeta especificada de Hola. |True, False (predeterminada) |No |

**FileSystemSink** admite Hola propiedades siguientes:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| copyBehavior |Define el comportamiento de la copia de hello al origen de hello es BlobSource o sistema de archivos. |**PreserveHierarchy:** conserva la jerarquía de archivos de hello en la carpeta de destino de Hola. Es decir, ruta de acceso relativa de Hola de carpeta de origen de toohello de archivo de origen de hello es Hola igual a la ruta de acceso relativa de Hola de carpeta de destino de toohello de archivo de destino de Hola.<br/><br/>**FlattenHierarchy:** todos los archivos de la carpeta de origen Hola se crean en el primer nivel de Hola de carpeta de destino. archivos de destino de Hola se crean con un nombre generado automáticamente.<br/><br/>**MergeFiles:** combina todos los archivos del archivo de tooone de carpeta de origen de hello. Si se especifica el nombre de blob/nombre de archivo de hello, nombre de archivo combinado de hello es nombre especificado de Hola. De lo contrario, es un nombre de archivo generado automáticamente. |No |

### <a name="recursive-and-copybehavior-examples"></a>Ejemplos de recursive y copyBehavior
Esta sección describe el comportamiento resultante de Hola de operación de copia de Hola para diferentes combinaciones de valores para propiedades de recursiva y copyBehavior de Hola.

| valor recursive | valor copyBehavior | Comportamiento resultante |
| --- | --- | --- |
| true |preserveHierarchy |Para una carpeta de origen carpeta1 con hello siguiendo estructura,<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>se crea la carpeta de destino de Hola carpeta1 con hello misma estructura como origen de Hola:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5 |
| true |flattenHierarchy |Para una carpeta de origen carpeta1 con hello siguiendo estructura,<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>se crea el destino de Hola carpeta1 con hello siguiente estructura: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File5 |
| true |mergeFiles |Para una carpeta de origen carpeta1 con hello siguiendo estructura,<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>se crea el destino de Hola carpeta1 con hello siguiente estructura: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;El contenido de File1 + File2 + File3 + File4 + File 5 se combina en un archivo con un nombre de archivo generado automáticamente. |
| false |preserveHierarchy |Para una carpeta de origen carpeta1 con hello siguiendo estructura,<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>carpeta de destino de Hello carpeta1 se crea con hello siguiente estructura:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/><br/>No se selecciona la subcarpeta Subfolder1, con File3, File4 y File5. |
| false |flattenHierarchy |Para una carpeta de origen carpeta1 con hello siguiendo estructura,<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>carpeta de destino de Hello carpeta1 se crea con hello siguiente estructura:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nombre de archivo generado automáticamente para File2<br/><br/>No se selecciona la subcarpeta Subfolder1, con File3, File4 y File5. |
| false |mergeFiles |Para una carpeta de origen carpeta1 con hello siguiendo estructura,<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5<br/><br/>carpeta de destino de Hello carpeta1 se crea con hello siguiente estructura:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;El contenido de File1 + File2 se combina en un archivo con un nombre de archivo generado automáticamente.<br/>&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1<br/><br/>No se selecciona la subcarpeta Subfolder1, con File3, File4 y File5. |

## <a name="supported-file-and-compression-formats"></a>Formatos de archivo y de compresión admitidos
Consulte los detalles en [Formatos de compresión y de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a>Ejemplos JSON para copiar datos tooand de sistema de archivos
Hello en los ejemplos siguientes proporcionan las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante hello [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Muestran cómo toocopy tooand de datos desde un sistema de archivos local y el almacenamiento de blobs de Azure. Sin embargo, puede copiar datos *directamente* desde cualquiera de hello orígenes tooany de receptores de hello enumerados en [admite orígenes y receptores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando la actividad de copia de Data Factory de Azure.

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a>Ejemplo: Copiar datos desde un sistema de archivos local tooAzure almacenamiento de blobs
Este ejemplo se muestra cómo toocopy datos desde un sistema de archivos local tooAzure almacenamiento de blobs. ejemplo de Hola tiene Hola siguiendo las entidades de la factoría de datos:

* Un servicio vinculado de tipo [OnPremisesFileServer](#linked-service-properties).
* Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [FileShare](#dataset-properties).
* Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [FileSystemSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Hola según muestra copia datos de serie temporal de un sistema de archivos local tooAzure almacenamiento de blobs cada hora. propiedades JSON de Hola que se usan en estos ejemplos se describen en secciones de hello después de los ejemplos de hello.

Como primer paso, configurar la puerta de enlace de datos de administración según las instrucciones de hello en [mover datos entre orígenes locales y en la nube con Data Management Gateway hello](data-factory-move-data-between-onprem-and-cloud.md).

**Servicio vinculado del servidor de archivos local:**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

Se recomienda usar hello **encryptedCredential** propiedad en su lugar Hola **userid** y **contraseña** propiedades. Consulte [Servicio vinculado del sistema de archivos](#linked-service-properties) para más información sobre este servicio vinculado.

**Servicio vinculado de Almacenamiento de Azure:**

```JSON
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

**Conjunto de datos de entrada del sistema de archivos local:**

Los datos se seleccionan de un archivo nuevo cada hora. Hola folderPath y propiedades de nombre de archivo se determinan en función del tiempo de inicio de Hola de segmento de Hola.  

Establecer `"external": "true"` informa factoría de datos de ese conjunto de datos de hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ]
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

**Conjunto de datos de salida de Azure Blob Storage:**

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1). ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y hora de Hola Hola hora de inicio.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
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

**Actividad de copia en una canalización con origen del sistema de archivos y receptor blob:**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida, y es toorun programada cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**FileSystemSource**, y **receptor** tipo está establecido demasiado**BlobSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "FileSystemSource"
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

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a>Ejemplo: Copiar los datos de sistema de archivos de base de datos de SQL Azure tooan local
Hola el siguiente ejemplo se muestra:

* Un servicio vinculado de tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
* Un servicio vinculado de tipo [OnPremisesFileServer](#linked-service-properties).
* Un conjunto de datos de entrada de tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
* Un conjunto de datos de salida de tipo [FileShare](#dataset-properties).
* Una canalización con una actividad de copia que usa [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) y [FileSystemSink](#copy-activity-properties).

ejemplo Hello copia datos de serie temporal de un sistema de archivos local de SQL Azure tabla tooan cada hora. propiedades JSON de Hola que se usan en estos ejemplos se describen en secciones después de los ejemplos de hello.

**Servicio vinculado a Azure SQL Database:**

```JSON
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

**Servicio vinculado del servidor de archivos local:**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

Se recomienda usar hello **encryptedCredential** propiedad en lugar de usar hello **userid** y **contraseña** propiedades. Consulte [Servicio vinculado del sistema de archivos](#linked-service-properties) para más información sobre este servicio vinculado.

**Conjunto de datos de entrada SQL de Azure:**

ejemplo de Hola se supone que ha creado una tabla "MyTable" en SQL Azure, y contiene una columna denominada "timestampcolumn" para los datos de serie temporal.

Establecer ``“external”: ”true”`` informa factoría de datos de ese conjunto de datos de hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.

```JSON
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

**Conjunto de datos de salida del sistema de archivos local:**

Datos son tooa copiado nuevo archivo cada hora. folderPath Hola y el nombre de blob de Hola se determinan en función del tiempo de inicio de Hola de segmento de Hola.

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ]
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

**Actividad de copia en una canalización con el origen de SQL y el receptor de sistema de archivos:**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida, y es toorun programada cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**SqlSource**, hello y **receptor** tipo está establecido demasiado**FileSystemSink**. consulta SQL de Hola que se especifica para hello **SqlReaderQuery** propiedad selecciona datos Hola Hola más allá de hora toocopy.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


También puede asignar columnas de toocolumns de conjunto de datos de origen del conjunto de datos de receptor en la definición de actividad de copia de Hola. Para obtener más información, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Rendimiento y optimización
 toolearn acerca de la clave de factores que afectan al rendimiento Hola de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas formas, vea hello [actividad de copia Guía de rendimiento y optimización](data-factory-copy-activity-performance.md).
