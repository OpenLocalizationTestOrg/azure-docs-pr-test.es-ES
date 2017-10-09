---
title: aaaMove datos desde un servidor FTP mediante el uso de Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos desde un servidor FTP mediante Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a>Movimiento de datos de un servidor FTP mediante Azure Data Factory
Este artículo explica cómo toouse Hola actividad de copia de datos de Data Factory de Azure toomove desde un servidor FTP. Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.

Puede copiar datos desde un almacén de datos de receptor FTP server tooany compatible. Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla. Solo almacena la migración de datos de un datos tooother de servidor FTP, pero no mover los datos de otros datos almacena tooan FTP server admite actualmente factoría de datos. Admite servidores FTP tanto locales como en la nube.

> [!NOTE]
> actividad de copia de Hello no eliminar el archivo de origen de hello cuando este destino toohello copió correctamente. Si necesita toodelete archivo de código fuente de Hola después de una copia correcta, cree un archivo de hello toodelete de actividad personalizada y usa la actividad hello en canalización de Hola. 

## <a name="enable-connectivity"></a>Habilitación de la conectividad
Si va a mover datos desde un **locales** el almacén de datos en la nube de servidor tooa FTP (por ejemplo, tooAzure almacenamiento de blobs), instalar y usar Data Management Gateway. Hola Data Management Gateway es un agente de cliente que está instalado en el equipo local, y permite recurso local tooan tooconnect de servicios de nube. Para más información, vea [Data Management Gateway](data-factory-data-management-gateway.md). Para obtener instrucciones paso a paso sobre cómo configurar la puerta de enlace de Hola y utilizarlo, vea [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md). Usar servidor de hello puerta de enlace tooconnect tooan FTP, aunque Hola servidor en una infraestructura de Azure como una máquina virtual (VM) de servicio (IaaS).

Es puerta de enlace de posibles tooinstall Hola Hola igual en local machine o IaaS VM como Hola servidor FTP. Sin embargo, se recomienda instalar la puerta de enlace de hello en un equipo independiente o contención de recursos de IaaS VM tooavoid y para mejorar el rendimiento. Cuando se instala la puerta de enlace de hello en un equipo independiente, máquina Hola debe ser servidor FTP puede tooaccess Hola.

## <a name="get-started"></a>Primeros pasos
Puede crear una canalización con una actividad de copia que mueva datos desde un origen FTP mediante diferentes herramientas o API.

toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar de factoría de datos**. Para ver un tutorial rápido, consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md).

También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.

Si usa herramientas de Hola o las API, lleve a cabo Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:

1. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.
2. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.
3. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas o las API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola. Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos FTP, vea hello [ejemplo de JSON: copiar los datos de blob FTP server tooAzure](#json-example-copy-data-from-ftp-server-to-azure-blob) sección de este artículo.

> [!NOTE]
> Para obtener más información sobre toouse de formatos de compresión de archivos y compatible, consulte [compresión de archivos y formatos de factoría de datos de Azure](data-factory-supported-file-and-compression-formats.md).

Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son entidades de factoría de datos usado toodefine tooFTP específico.

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Hello en la tabla siguiente describe el servicio FTP vinculada de tooan específico de elementos JSON.

| Propiedad | Descripción | Obligatorio | Valor predeterminado |
| --- | --- | --- | --- |
| type |Establecer este tooFtpServer. |Sí |&nbsp; |
| host |Especificar nombre de Hola o dirección IP del servidor FTP de Hola. |Sí |&nbsp; |
| authenticationType |Especifique el tipo de autenticación de Hola. |Sí |Basic, Anonymous |
| nombre de usuario |Especifique el usuario de Hola que tiene el servidor de acceso toohello FTP. |No |&nbsp; |
| Contraseña |Especifique la contraseña de hello para el usuario hello (usuario). |No |&nbsp; |
| encryptedCredential |Especificar servidor de hello cifrado credencial tooaccess Hola FTP. |No |&nbsp; |
| gatewayName |Especifique el nombre de Hola de puerta de enlace de hello en el servidor FTP local de Data Management Gateway tooconnect tooan. |No |&nbsp; |
| puerto |Especificar puerto hello en qué Hola FTP está escuchando el servidor. |No |21 |
| enableSsl |Especifique si toouse FTP sobre un canal SSL/TLS. |No |true |
| enableServerCertificateValidation |Especifique si, cuando se utiliza FTP a través de canal SSL/TLS, se validación de certificado de servidor tooenable SSL. |No |true |

### <a name="use-anonymous-authentication"></a>Uso de la autenticación anónima

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a>Uso del nombre de usuario y la contraseña en texto sin formato para la autenticación básica

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a>Uso de puerto, enableSsl, enableServerCertificateValidation

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a>Uso de encryptedCredential para la autenticación y la puerta de enlace

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para ver una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, consulte [Creación de conjuntos de datos](data-factory-create-datasets.md). Las secciones como estructura, disponibilidad y directiva de un JSON de conjunto de datos son similares para todos los tipos de conjunto de datos.

Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos. Proporciona información de tipo de conjunto de datos toohello específica. Hola **typeProperties** sección para un conjunto de datos de tipo **FileShare** tiene Hola propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| folderPath |Carpeta de toohello subruta de acceso. Utilice el carácter de escape ' \ ' para los caracteres especiales en la cadena de Hola. Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .<br/><br/>Puede combinar esta propiedad con **partitionBy** según las rutas de carpeta toohave empezar y terminar fechas y horas. |Sí |
| fileName |Especifique el nombre de hello del archivo hello en hello **folderPath** si desea Hola tabla toorefer tooa archivo específico en la carpeta de Hola. Si no especifica ningún valor para esta propiedad, tabla de hello señala tooall archivos en la carpeta de Hola.<br/><br/>Cuando **fileName** no se especifica para un conjunto de datos de salida, nombre de hello del archivo hello generado está en hello siguiendo el formato: <br/><br/>Data.<Guid>.txt (por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |No |
| fileFilter |Especificar un tooselect de toobe utiliza un subconjunto de archivos de filtro en hello **folderPath**, en lugar de todos los archivos.<br/><br/>Valores permitidos son: `*` (varios caracteres) y `?` (un único individual).<br/><br/>Ejemplo 1: `"fileFilter": "*.log"`<br/>Ejemplo 2: `"fileFilter": 2014-1-?.txt"`<br/><br/> **fileFilter** es aplicable a un conjunto de datos FileShare de entrada. Esta propiedad no es compatible con el sistema de archivos distribuido de Hadoop (HDFS). |No |
| partitionedBy |Usar toospecify dinámico **folderPath** y **fileName** para datos de serie temporal. Por ejemplo, puede especificar una propiedad **folderPath** que tenga parámetros para cada hora de datos. |No |
| formato | se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Conjunto hello **tipo** propiedad en formato tooone de estos valores. Para obtener más información, vea hello [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [el formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), y [Parquet formato ](data-factory-supported-file-and-compression-formats.md#parquet-format) secciones. <br><br> Si desea toocopy archivos tal como están entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida. |No |
| compresión | Especificar tipo de Hola y el nivel de compresión para datos de Hola. Los tipos admitidos son: **GZip**, **Deflate**, **BZip2** y **ZipDeflate**, y los niveles que se admiten son: **Optimal** (Óptimo) y **Fastest** (Más rápido). Para obtener más información, consulte el artículo sobre [formatos de archivo y compresión en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |
| useBinaryTransfer |Especifique si el modo de transferencia de archivo binario de hello toouse. Hola valores son true para el modo binario (Esto es el valor predeterminado de hello) y false para ASCII. Esta propiedad solo puede usarse cuando hello asociado servicio vinculado de tipo es de tipo: FtpServer. |No |

> [!NOTE]
> **fileName** y **fileFilter** no pueden usarse simultáneamente.

### <a name="use-hello-partionedby-property"></a>Utilice hello partionedBy propiedad
Como se mencionó en la sección anterior de hello, puede especificar un dinámico **folderPath** y **fileName** para datos de serie temporal con hello **partitionedBy** propiedad.

toolearn acerca de los conjuntos de datos de series de tiempo, la programación y sectores, consulte [crear conjuntos de datos](data-factory-create-datasets.md), [ejecución y programación](data-factory-scheduling-and-execution.md), y [crear canalizaciones](data-factory-create-pipelines.md).

#### <a name="sample-1"></a>Ejemplo 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
En este ejemplo, {Slice} se reemplaza con el valor de Hola de variable del sistema SliceStart de factoría de datos, en hello formato (AAAAMMDDHH) especificado. Hola SliceStart refiere a tiempo toostart de segmento de Hola. ruta de acceso de carpeta de Hello es diferente para cada segmento. (Por ejemplo, wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104).

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
En este ejemplo, se extraen en variables independientes que usan Hola Hola año, mes, día y hora de SliceStart **folderPath** y **fileName** propiedades.

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte [Creación de canalizaciones](data-factory-create-pipelines.md). Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

Propiedades disponibles en hello **typeProperties** sección de Hola actividad en hello en otra parte, varían con cada tipo de actividad. Para la actividad de copia de hello, propiedades de tipo de hello varían en función de tipos de Hola de orígenes y receptores.

En la actividad de copia, cuando el origen de hello es de tipo **FileSystemSource**, Hola después de la propiedad está disponible en **typeProperties** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| recursive |Indica si los datos de hello es de lectura de forma recursiva de las subcarpetas de hello, o solo de la carpeta especificada de Hola. |True, False (predeterminada) |No |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a>Ejemplo de JSON: copiar los datos de servidor FTP tooAzure Blob
Este ejemplo se muestra cómo toocopy datos desde un tooAzure de servidor FTP almacenamiento de blobs. Sin embargo, los datos pueden copiarse directamente Hola indicado en los receptores de tooany de hello [admite almacenes de datos y formatos](data-factory-data-movement-activities.md#supported-data-stores-and-formats), mediante el uso de actividad de copia de hello de factoría de datos.  

Hello en los ejemplos siguientes proporcionan las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):

* Un servicio vinculado de tipo [FtpServer](#linked-service-properties).
* Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [FileShare](#dataset-properties).
* Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [FileSystemSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

ejemplo de Hola copia datos de un tooan de servidor FTP blobs de Azure cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

### <a name="ftp-linked-service"></a>Servicio vinculado FTP

En este ejemplo se utiliza la autenticación básica, con el nombre de usuario de hello y una contraseña en texto sin formato. También puede utilizar uno de hello siguientes maneras:

* Autenticación anónima
* Autenticación básica con credenciales cifradas
* FTP sobre SSL/TLS (FTPS)

Vea hello [servicio vinculado de FTP](#linked-service-properties) sección para diferentes tipos de autenticación que se puede usar.

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a>Servicio vinculado de Azure Storage

```JSON
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
### <a name="ftp-input-dataset"></a>Conjunto de datos de entrada FTP

Este conjunto de datos hace referencia la carpeta FTP toohello `mysharedfolder` y el archivo `test.csv`. Hola canalización copias hello toohello destino del archivo.

Establecer **externo** demasiado**true** informa a servicio de factoría de datos de Hola ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a>Conjunto de datos de salida de blob de Azure

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1). ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de Hola Hola hora de inicio.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a>Actividad de copia en una canalización con el origen del sistema de archivos y el receptor de blob

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida, y es toorun programada cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**FileSystemSource**, hello y **receptor** tipo está establecido demasiado**BlobSink**.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> columnas de toomap de toocolumns de conjunto de datos de origen del conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).

## <a name="next-steps"></a>Pasos siguientes
Vea Hola siguientes artículos:

* toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos y toooptimize de diversas formas, vea hello [copiar actividad Guía de rendimiento y optimización](data-factory-copy-activity-performance.md).

* Para obtener instrucciones paso a paso para crear una canalización con una actividad de copia, consulte hello [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
