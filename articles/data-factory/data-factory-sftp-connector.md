---
title: aaaMove datos del servidor SFTP con Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos desde una implementación local o un servidor SFTP de nubes mediante Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a>Movimiento de datos de un servidor FTP mediante Azure Data Factory
En este artículo se describe cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde un tooa de servidor SFTP en local y la nube admite el almacén de datos del receptor. En este artículo se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo que presenta una visión general de movimiento de datos con la lista de hello y actividad de copia de almacenes de datos que se admiten como orígenes y receptores.

Factoría de datos admite actualmente solo mover almacena los datos de un servidor de SFTP tooother datos, pero no para mover los datos de otros datos de los almacenes servidor SFTP de tooan. Admite servidores SFTP tanto locales como de nube.

> [!NOTE]
> Actividad de copia no elimina archivos de origen de Hola cuando este destino toohello copió correctamente. Si necesita toodelete archivo de código fuente de hello después de una copia correcta, cree un archivo de actividad personalizada toodelete hello y usar actividad hello en la canalización de Hola. 

## <a name="supported-scenarios-and-authentication-types"></a>Escenarios admitidos y tipos de autenticación
Puede usar estos datos SFTP conector toocopy de **ambos servidores SFTP y servidores SFTP local en la nube**. **Básico** y **SshPublicKey** se admiten los tipos de autenticación cuando se conecta el servidor de toohello SFTP.

Cuando se copian datos desde un servidor local de SFTP, necesita instalar una puerta de enlace de administración de datos en hello local entorno/VM de Azure. Vea [Data Management Gateway](data-factory-data-management-gateway.md) para obtener detalles sobre la puerta de enlace de Hola. Vea [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo para obtener instrucciones paso a paso sobre cómo configurar la puerta de enlace de Hola y usarlo.

## <a name="getting-started"></a>Introducción
Puede crear una canalización con una actividad de copia que mueva los datos desde un origen SFTP mediante diferentes herramientas o API.

- toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.

- También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia. Para JSON muestrea los datos de toocopy de tooAzure de servidor SFTP almacenamiento de blobs, vea [ejemplo de JSON: copiar los datos de blob SFTP server tooAzure](#json-example-copy-data-from-sftp-server-to-azure-blob) sección de este artículo.

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooFTP vinculado.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- | --- |
| type | se debe establecer propiedad de tipo Hello demasiado`Sftp`. |Sí |
| host | Nombre o dirección IP del servidor SFTP de Hola. |Sí |
| puerto |Puerto en qué Hola SFTP servidor está escuchando. es el valor predeterminado de Hello: 21 |No |
| authenticationType |Especifique el tipo de autenticación. Valores permitidos: **Básica**, **SshPublicKey**. <br><br> Consulte demasiado[mediante la autenticación básica](#using-basic-authentication) y [utilizando SSH autenticación de clave pública](#using-ssh-public-key-authentication) secciones en más propiedades y ejemplos JSON, respectivamente. |Sí |
| skipHostKeyValidation | Especificar si tooskip validación de clave de host. | No. Hola valor predeterminado: false |
| hostKeyFingerprint | Especifique la huella dactilar de Hola de clave de host de Hola. | Sí si hello `skipHostKeyValidation` se establece toofalse.  |
| gatewayName |Nombre de hello Data Management Gateway tooconnect tooan local servidor SFTP. | Sí, si va a copiar datos desde un servidor SFTP local. |
| encryptedCredential | Servidor de credenciales cifradas tooaccess Hola SFTP. Generado automáticamente cuando se especifica la autenticación básica (nombre de usuario y contraseña) o SshPublicKey (nombre de usuario + ruta de acceso de clave privada o contenido) en copia asistente o hello ClickOnce cuadro de diálogo emergente. | No. Se aplica solo cuando se copian datos desde un servidor SFTP local. |

### <a name="using-basic-authentication"></a>Uso de autenticación básica

establecer la autenticación básica toouse, `authenticationType` como `Basic`y especifique Hola propiedades siguientes, además de Hola conector SFTP genérico que introdujo en la última sección de hello:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- | --- |
| nombre de usuario | Usuario que tiene el servidor de acceso toohello SFTP. |Sí |
| Contraseña | Contraseña de usuario de hello (nombre de usuario). | Sí |

#### <a name="example-basic-authentication"></a>Ejemplo: Autenticación básica
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>Ejemplo: Autenticación básica con credenciales cifradas

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a>Uso de autenticación de clave pública SSH

establecer toouse SSH autenticación de clave pública, `authenticationType` como `SshPublicKey`y especifique Hola propiedades siguientes, además de Hola conector SFTP genérico que introdujo en la última sección de hello:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- | --- |
| nombre de usuario |Usuario que tiene el servidor de acceso toohello SFTP |Sí |
| privateKeyPath | Especifique la ruta de acceso absoluta toohello archivo de clave privada que puede tener acceso esa puerta de enlace. | Especifique cualquier hello `privateKeyPath` o `privateKeyContent`. <br><br> Se aplica solo cuando se copian datos desde un servidor SFTP local. |
| privateKeyContent | Una cadena serializada de contenido de clave privada de Hola. Hola Asistente para copiar puede leer el archivo de clave privada de Hola y extraer contenido de clave privada de hello automáticamente. Si está utilizando cualquier otra herramienta/SDK, use en su lugar la propiedad privateKeyPath de Hola. | Especifique cualquier hello `privateKeyPath` o `privateKeyContent`. |
| passPhrase | Especificar clave privada de hello paso contraseña/frase toodecrypt Hola si el archivo de clave de hello está protegido por una frase de contraseña. | Sí, si el archivo de clave privada de hello está protegido por una frase de contraseña. |

> [!NOTE]
> El conector de SFTP solo admite la clave OpenSSH. Asegúrese de que el archivo de clave es un formato correcto Hola. Puede usar la herramienta Putty tooconvert desde el formato de tooOpenSSH. ppk.

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a>Ejemplo: Autenticación de SshPublicKey mediante el valor de filePath de clave privada

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>Ejemplo: Autenticación de SshPublicKey mediante contenido de clave privada

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como estructura, disponibilidad y directiva de un JSON de conjunto de datos son similares para todos los tipos de conjunto de datos.

Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos. Proporciona información de tipo de conjunto de datos toohello específica. Hola typeProperties sección un conjunto de datos de tipo **FileShare** conjunto de datos tiene Hola propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| folderPath |Carpeta de toohello de ruta de acceso de Sub. Utilice el carácter de escape ' \ ' para los caracteres especiales en la cadena de Hola. Consulte los casos que se exponen en [Ejemplos de definiciones de servicio vinculado y conjunto de datos](#sample-linked-service-and-dataset-definitions) .<br/><br/>Puede combinar esta propiedad con **partitionBy** toohave de rutas de acceso de carpeta según fechas y horas de inicio y fin. |Sí |
| fileName |Especifique el nombre de hello del archivo hello en hello **folderPath** si desea Hola tabla toorefer tooa archivo específico en la carpeta de Hola. Si no especifica ningún valor para esta propiedad, tabla de hello señala tooall archivos en la carpeta de Hola.<br/><br/>Cuando no se especifica el nombre de archivo para un conjunto de datos de salida, nombre de hello del archivo hello genera sería Hola siguiendo este formato: <br/><br/>Data.<Guid>.txt (por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |No |
| fileFilter |Especifique un filtro toobe utiliza tooselect un subconjunto de archivos en folderPath hello en lugar de todos los archivos.<br/><br/>Valores permitidos son: `*` (varios caracteres) y `?` (un único individual).<br/><br/>Ejemplos 1: `"fileFilter": "*.log"`<br/>Ejemplo 2: `"fileFilter": 2014-1-?.txt"`<br/><br/> fileFilter es aplicable a un conjunto de datos FileShare de entrada. Esta propiedad no es compatible con HDFS. |No |
| partitionedBy |partitionedBy puede ser usado toospecify un folderPath dinámico, nombre de archivo de datos de series temporales. Por ejemplo, folderPath se parametriza por cada hora de datos. |No |
| formato | se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Conjunto hello **tipo** propiedad en formato tooone de estos valores. Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida. |No |
| compresión | Especificar tipo de Hola y el nivel de compresión para datos de Hola. Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**. Los niveles admitidos son **Optimal** y **Fastest**. Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |
| useBinaryTransfer |Especifica si se usará el modo de transferencia binario. Su valor es true para el modo binario y false para ASCII. Valor predeterminado: true. Esta propiedad solo puede usarse cuando el tipo de servicio vinculado asociado es: FtpServer. |No |

> [!NOTE]
> filename y fileFilter no pueden usarse simultáneamente.

### <a name="using-partionedby-property"></a>Uso de la propiedad partitionedBy
Como se mencionó en la sección anterior de hello, puede especificar un folderPath dinámico, nombre de archivo de datos de serie temporal con partitionedBy. Puede hacerlo con macros de la factoría de datos de Hola y variable del sistema SliceStart, SliceEnd que indican un período de tiempo lógico para un segmento de datos determinado Hola Hola.

toolearn acerca de los conjuntos de datos de series de tiempo, la programación y sectores, consulte [crear conjuntos de datos](data-factory-create-datasets.md), [ejecución y programación](data-factory-scheduling-and-execution.md), y [crear canalizaciones](data-factory-create-pipelines.md) artículos.

#### <a name="sample-1"></a>Muestra 1:

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
En este ejemplo {Slice} se reemplaza con el valor de Hola de variable del sistema SliceStart factoría de datos en formato de hello (AAAAMMDDHH) especificado. Hola SliceStart refiere a tiempo toostart de segmento de Hola. Hola folderPath es diferente para cada segmento. Ejemplo: wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Ejemplo 2:

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
Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

Mientras que hello las propiedades disponibles en la sección de typeProperties de Hola de actividad hello varían con cada tipo de actividad. Para la actividad de copia, propiedades de tipo de hello varían en función de tipos de Hola de orígenes y receptores.

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a>Formatos de archivo y de compresión admitidos
Consulte los detalles en [Formatos de compresión y de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a>Ejemplo JSON: Copiar los datos de blob de tooAzure servidor SFTP
Hello en el ejemplo siguiente se proporciona definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Muestra cómo tooAzure almacenamiento de blobs del origen de datos de toocopy de SFTP. Sin embargo, se pueden copiar datos **directamente** desde cualquiera de tooany orígenes de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.

> [!IMPORTANT]
> Este ejemplo proporciona fragmentos JSON. No incluye instrucciones paso a paso para la creación de factoría de datos de Hola. Las instrucciones paso a paso se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .

ejemplo de Hola tiene Hola después de entidades de la factoría de datos:

* Un servicio vinculado de tipo [sftp](#linked-service-properties).
* Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [FileShare](#dataset-properties).
* Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [FileSystemSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

ejemplo de Hola copia datos de una tooan del servidor SFTP blobs de Azure cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

**Servicio vinculado de SFTP**

En este ejemplo se utiliza la autenticación básica hello con nombre de usuario y una contraseña en texto sin formato. También puede utilizar uno de hello siguientes maneras:

* Autenticación básica con credenciales cifradas
* Autenticación de la clave pública SSH

Para los diferentes tipos de autenticación que se pueden usar, consulte la sección [Propiedades del servicio vinculado de FTP](#linked-service-properties).

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
**Servicio vinculado de Almacenamiento de Azure**

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
**Conjunto de datos de entrada de SFTP**

Este conjunto de datos hace referencia a carpeta SFTP toohello `mysharedfolder` y el archivo `test.csv`. Hola canalización copias hello toohello destino del archivo.

Establecer "externo": "true" informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Conjunto de datos de salida de blob de Azure**

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1). ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Canalización con actividad de copia**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**FileSystemSource** y **receptor** tipo está establecido demasiado**BlobSink**.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
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
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a>Rendimiento y optimización
Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.

## <a name="next-steps"></a>Pasos siguientes
Vea Hola siguientes artículos:

* [Tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso para la creación de una canalización con una actividad de copia.
