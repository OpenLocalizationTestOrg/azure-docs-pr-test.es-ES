---
title: aaaMove datos de un origen HTTP - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo usar Data Factory de Azure del origen de datos de toomove desde una implementación local o una nube de HTTP."
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
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a>Movimiento de datos desde un origen HTTP mediante Azure Data Factory
En este artículo se describe cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde un tooa de punto de conexión HTTP en local y la nube admite el almacén de datos del receptor. En este artículo se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo que presenta una visión general de movimiento de datos con la lista de hello y actividad de copia de almacenes de datos que se admiten como orígenes y receptores.

Factoría de datos actualmente admite sólo mover datos de un elemento HTTP origen tooother almacenes de datos, pero no mover los datos de otros datos almacena destino tooan HTTP.

## <a name="supported-scenarios-and-authentication-types"></a>Escenarios admitidos y tipos de autenticación
Puede usar estos datos de tooretrieve de conector HTTP de **extremo HTTP/s en la nube y locales** mediante HTTP **obtener** o **POST** método. se admite los siguientes tipos de autenticación de Hello: **Anonymous**, **básica**, **implícita**, **Windows**, y  **ClientCertificate**. Observe Hola diferencia que existe entre este conector y hello [conector de tabla Web](data-factory-web-table-connector.md) es: hello este último es usado tooextract tabla contenida de la página web HTML.

Cuando se copian datos desde un punto de conexión HTTP en local, necesita instalar una puerta de enlace de administración de datos en hello local entorno/VM de Azure. Vea [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) toolearn artículo acerca de la puerta de enlace de datos de administración y las instrucciones paso a paso sobre cómo configurar la puerta de enlace de Hola.

## <a name="getting-started"></a>Introducción
Puede crear una canalización con una actividad de copia que mueva datos desde un origen HTTP mediante diferentes herramientas o API.

- toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.

- También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia. Para JSON muestrea los datos de toocopy de HTTP origen tooAzure almacenamiento de blobs, vea [ejemplos JSON](#json-examples) sección de este artículo.

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooHTTP vinculado.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type | propiedad de tipo Hello debe establecerse en: `Http`. | Sí |
| url | Basar la dirección URL toohello servidor Web | Sí |
| authenticationType | Especifica el tipo de autenticación de Hola. Los valores permitidos son: **Anonymous**, **Basic**, **Digest**, **Windows** y **ClientCertificate**. <br><br> Consulte toosections por debajo de esta tabla en más propiedades y ejemplos JSON para esos tipos de autenticación, respectivamente. | Sí |
| enableServerCertificateValidation | Especifique si el servidor de tooenable SSL la validación de certificados si el origen es el servidor de Web HTTPS | No, el valor predeterminado es True. |
| gatewayName | Nombre de hello Data Management Gateway tooconnect tooan local de origen HTTP. | Sí si va a copiar datos desde un origen HTTP local. |
| encryptedCredential | Credenciales cifradas tooaccess Hola extremo HTTP. Generado automáticamente al configurar la información de autenticación de hello en copia asistente o hello ClickOnce cuadro de diálogo emergente. | No. Se aplica solo cuando se copian datos desde un servidor HTTP local. |

Vea [mover datos entre orígenes locales y en la nube Hola con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) para obtener más información acerca de cómo establecer las credenciales de origen de datos del conector local HTTP.

### <a name="using-basic-digest-or-windows-authentication"></a>Uso de la autenticación Basic, Digest o Windows

Establecer `authenticationType` como `Basic`, `Digest`, o `Windows`y especifique Hola propiedades siguientes, además de Hola el genérico de conector HTTP los descritos anteriormente:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| nombre de usuario | Nombre de usuario tooaccess Hola extremo HTTP. | Sí |
| Contraseña | Contraseña de usuario de hello (nombre de usuario). | Sí |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>Ejemplo: Uso de la autenticación Basic, Digest o Windows

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a>Uso de la autenticación ClientCertificate

establecer la autenticación básica toouse, `authenticationType` como `ClientCertificate`y especifique Hola propiedades siguientes, además de Hola el genérico de conector HTTP los descritos anteriormente:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| embeddedCertData | contenido codificado en Base64 Hola de datos binarios del archivo de intercambio de información Personal (PFX) Hola. | Especifique cualquier hello `embeddedCertData` o `certThumbprint`. |
| certThumbprint | Hola huella digital del certificado de Hola que se instaló en el almacén de certificados de la máquina de la puerta de enlace. Se aplica solo cuando se copian datos desde un origen HTTP local. | Especifique cualquier hello `embeddedCertData` o `certThumbprint`. |
| Contraseña | Contraseña asociada con el certificado de Hola. | No |

Si usa `certThumbprint` para hello y autenticación de certificado está instalado en el almacén personal de hello del equipo local de hello, necesita que el servicio de puerta de enlace de toohello de toogrant Hola permiso de lectura:

1. Inicie Microsoft Management Console (MMC). Agregar hello **certificados** complemento ese Hola destinos **equipo Local**.
2. Expanda **Certificados**, **Personal** y haga clic en **Certificados**.
3. Haga clic en certificado Hola almacén personal de Hola y seleccione **todas las tareas**->**administrar claves privadas...**
3. En hello **seguridad** ficha, agregue la cuenta de usuario de hello en que se ejecuta el servicio de Host de Data Management Gateway con certificado de toohello de acceso de lectura de Hola.  

#### <a name="example-using-client-certificate"></a>Ejemplo: Uso del certificado de cliente
Esto vincula vínculos de servicio el servidor de web HTTP de datos generador tooan local. Utiliza un certificado de cliente que se instala en la máquina de hello con Data Management Gateway instalado.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>Ejemplo: Uso del certificado de cliente en un archivo
Esto vincula vínculos de servicio el servidor de web HTTP de datos generador tooan local. Utiliza un archivo de certificado de cliente en la máquina de hello con Data Management Gateway instalado.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).

Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. sección typeProperties Hello para el conjunto de datos de tipo **Http** tiene Hola propiedades siguientes

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| type | Tipo de hello del conjunto de datos de hello especificado. debe establecerse demasiado`Http`. | Sí |
| relativeUrl | Un recurso de toohello de dirección URL relativo al que contiene los datos de Hola. Cuando no se especifica la ruta de acceso, se usa solo dirección URL de hello especificada en definición de servicio vinculado de Hola. <br><br> dirección URL dinámica tooconstruct, puede usar [funciones de factoría de datos y las variables del sistema](data-factory-functions-variables.md), por ejemplo, "relativeUrl": "$$Text.Format ('/ my/informe? mes = {0:yyyy}-{0:MM} & fmt = csv', SliceStart)". | No |
| requestMethod | Método HTTP. Los valores permitidos son **GET** o **POST**. | No. El valor predeterminado es `GET`. |
| additionalHeaders | Encabezados de solicitud HTTP adicionales. | No |
| requestBody | Cuerpo de la solicitud HTTP. | No |
| formato | Si desea que toosimply **recuperar datos de Hola de extremo HTTP como-es** sin analizarlo, omita esta configuración de formato. <br><br> Si desea tooparse Hola HTTP respuesta contenido durante la copia, se admite los siguientes tipos de formato de Hola: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). |No |
| compresión | Especificar tipo de Hola y el nivel de compresión para datos de Hola. Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**. Los niveles admitidos son **Optimal** y **Fastest**. Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

### <a name="example-using-hello-get-default-method"></a>Ejemplo: usar el método de hello GET (valor predeterminado)

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-hello-post-method"></a>Ejemplo: utilizar el método POST de Hola

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

Propiedades disponibles en hello **typeProperties** sección de actividad de hello en hello varían con cada tipo de actividad en otra parte. Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.

Actualmente, al origen de hello en la actividad de copia es de tipo **HttpSource**, Hola propiedades siguientes se admite.

| Propiedad | Descripción | Obligatorio |
| -------- | ----------- | -------- |
| httpRequestTimeout | Hola (TimeSpan) de tiempo de espera de solicitud tooget una respuesta de hello HTTP. Es tooget Hola de tiempo de espera una respuesta, datos de respuesta no Hola el tooread del tiempo de espera. | No. Valor predeterminado: 00:01:40 |

## <a name="supported-file-and-compression-formats"></a>Formatos de archivo y de compresión admitidos
Consulte los detalles en [Formatos de compresión y de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

## <a name="json-examples"></a>Ejemplos de JSON
Hola de ejemplo siguiente proporciona definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Muestra cómo tooAzure almacenamiento de blobs del origen de datos de toocopy de HTTP. Sin embargo, se pueden copiar datos **directamente** desde cualquiera de tooany orígenes de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a>Ejemplo: Copiar los datos de origen HTTP tooAzure almacenamiento de blobs
solución de factoría de datos de este ejemplo de Hola contiene Hola siguiendo las entidades de la factoría de datos:

1. Un servicio vinculado de tipo [HTTP](#linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [Http](#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [canalización](data-factory-create-pipelines.md) con actividad de copia que usa [HttpSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

ejemplo de Hola copia datos de un tooan de origen HTTP blobs de Azure cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

### <a name="http-linked-service"></a>Servicio vinculado HTTP
Este ejemplo usa Hola HTTP vinculado servicio con la autenticación anónima. Para los diferentes tipos de autenticación que se pueden usar, consulte la sección [Propiedades del servicio vinculado](#linked-service-properties).

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Servicio vinculado de Almacenamiento de Azure

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

### <a name="http-input-dataset"></a>Conjunto de datos de entrada HTTP
Establecer **externo** demasiado**true** informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a>Conjunto de datos de salida de blob de Azure

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a>Canalización con actividad de copia

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**HttpSource** y **receptor** tipo está establecido demasiado**BlobSink**.

Vea [HttpSource](#copy-activity-properties) para lista de Hola de propiedades admitidas por hello HttpSource.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
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
