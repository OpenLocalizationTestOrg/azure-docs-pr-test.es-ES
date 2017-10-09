---
title: datos de aaaMove de HDFS local | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos desde local HDFS mediante Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a>Movimiento de datos desde HDFS local mediante Azure Data Factory
Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde un HDFS local. Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.

Puede copiar datos de almacén de datos de receptor HDFS tooany compatible. Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla. Factoría de datos admite actualmente solo mover datos desde un almacenes de datos de tooother HDFS local, pero no para mover los datos de otros datos tooan almacenes locales HDFS.

> [!NOTE]
> Actividad de copia no elimina archivos de origen de Hola cuando este destino toohello copió correctamente. Si necesita toodelete archivo de código fuente de hello después de una copia correcta, cree un archivo de actividad personalizada toodelete hello y usar actividad hello en la canalización de Hola. 

## <a name="enabling-connectivity"></a>Habilitación de la conectividad
Servicio de factoría de datos admite la conexión HDFS local tooon con hello Data Management Gateway. Vea [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) toolearn artículo acerca de la puerta de enlace de datos de administración y las instrucciones paso a paso sobre cómo configurar la puerta de enlace de Hola. Utilice Hola puerta de enlace tooconnect tooHDFS incluso si está hospedado en una máquina virtual de IaaS de Azure.

> [!NOTE]
> Asegúrese de Hola que puede tener acceso Data Management Gateway demasiado**todos los** Hola [servidor de nombres de nodo]: [nombre de puerto de nodo] y [servidores de nodos de datos]: [puerto de nodo de datos] de clúster de Hadoop de Hola. El [puerto de nodo de nombres] predeterminado es 50070 y el [puerto de nodo de datos] es 50075.

Durante la instalación de puerta de enlace en hello mismo locales máquina o hello Azure VM Hola HDFS, se recomienda que instale la puerta de enlace de hello en un equipo independiente/Azure VM de IaaS. Al tener la puerta de enlace en un equipo independiente, se reduce la contención de recursos y se mejora el rendimiento. Cuando se instala la puerta de enlace de hello en un equipo independiente, máquina Hola debe ser capaz de tooaccess máquina de hello con hello HDFS.

## <a name="getting-started"></a>Introducción
Puede crear una canalización con actividad de copia que mueva los datos desde un origen de HDFS mediante el uso de diferentes herramientas o API.

toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.

También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:

1. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.
2. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.
3. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos HDFS, consulte [ejemplo de JSON: copiar los datos de tooAzure HDFS local Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) sección de este artículo.

Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son entidades de factoría de datos usado toodefine tooHDFS específico:

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Un servicio vinculado vincula una factoría de datos de tooa de almacén de datos. Crear un servicio vinculado de tipo **Hdfs** toolink una factoría de datos de tooyour HDFS local. Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooHDFS vinculado.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |propiedad de tipo Hello debe establecerse en: **Hdfs** |Sí |
| URL |Dirección URL toohello HDFS |Sí |
| authenticationType |Anónima o Windows. <br><br> toouse **la autenticación Kerberos** para conector HDFS, consulte demasiado[en esta sección](#use-kerberos-authentication-for-hdfs-connector) tooset del entorno local en consecuencia. |Sí |
| userName |Nombre de usuario para la autenticación de Windows |Sí (para la autenticación de Windows) |
| contraseña |Contraseña para la autenticación de Windows |Sí (para la autenticación de Windows) |
| gatewayName |Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar tooconnect toohello HDFS. |Sí |
| encryptedCredential |[Nueva AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) salida de credenciales de acceso de Hola. |No |

### <a name="using-anonymous-authentication"></a>Uso de autenticación anónima

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a>Uso de autenticación de Windows

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).

Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. sección typeProperties Hello para el conjunto de datos de tipo **FileShare** (que incluye el conjunto de datos HDFS) tiene Hola propiedades siguientes

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| folderPath |Carpeta de toohello de ruta de acceso. Ejemplo: `myfolder`<br/><br/>Utilice el carácter de escape ' \ ' para los caracteres especiales en la cadena de Hola. Por ejemplo: para folder\subfolder, especifique la carpeta\\\\subcarpeta y para d:\samplefolder, especifique d:\\\\samplefolder.<br/><br/>Puede combinar esta propiedad con **partitionBy** toohave de rutas de acceso de carpeta según fechas y horas de inicio y fin. |Sí |
| fileName |Especifique el nombre de hello del archivo hello en hello **folderPath** si desea Hola tabla toorefer tooa archivo específico en la carpeta de Hola. Si no especifica ningún valor para esta propiedad, tabla de hello señala tooall archivos en la carpeta de Hola.<br/><br/>Cuando no se especifica el nombre de archivo para un conjunto de datos de salida, nombre de hello del archivo hello genera sería Hola siguiendo este formato: <br/><br/>Data<Guid>.txt (por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |No |
| partitionedBy |partitionedBy puede ser usado toospecify un folderPath dinámico, nombre de archivo de datos de series temporales. Por ejemplo, folderPath se parametriza para cada hora de datos. |No |
| formato | se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Conjunto hello **tipo** propiedad en formato tooone de estos valores. Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida. |No |
| compresión | Especificar tipo de Hola y el nivel de compresión para datos de Hola. Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**. Los niveles admitidos son **Optimal** y **Fastest**. Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

> [!NOTE]
> filename y fileFilter no pueden usarse simultáneamente.

### <a name="using-partionedby-property"></a>Uso de la propiedad partitionedBy
Como se mencionó en la sección anterior de hello, puede especificar un folderPath dinámica y el nombre de archivo de datos de serie temporal con hello **partitionedBy** propiedad, [funciones de factoría de datos y las variables del sistema hello](data-factory-functions-variables.md).

toolearn más información acerca de los conjuntos de datos de series de tiempo, la programación y sectores, consulte [crear conjuntos de datos](data-factory-create-datasets.md), [ejecución y programación](data-factory-scheduling-and-execution.md), y [crear canalizaciones](data-factory-create-pipelines.md) artículos.

#### <a name="sample-1"></a>Muestra 1:

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
En este ejemplo {Slice} se reemplaza con el valor de Hola de variable del sistema SliceStart factoría de datos en formato de hello (AAAAMMDDHH) especificado. Hola SliceStart refiere a tiempo toostart de segmento de Hola. Hola folderPath es diferente para cada segmento. Por ejemplo: wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104.

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
En este ejemplo, year, month, day y time de SliceStart se extraen en variables independientes que se usan en las propiedades folderPath y fileName.

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

Mientras que las propiedades disponibles en la sección de typeProperties de Hola de actividad hello varían con cada tipo de actividad. Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.

Para la actividad de copia, cuando el origen es de tipo **FileSystemSource** Hola propiedades siguientes está disponible en la sección typeProperties:

**FileSystemSource** admite Hola propiedades siguientes:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| recursive |Indica si hello es leer los datos de forma recursiva de subcarpetas de Hola o solo de carpeta especificada de Hola. |True, False (predeterminada) |No |

## <a name="supported-file-and-compression-formats"></a>Formatos de archivo y de compresión admitidos
Consulte los detalles en [Formatos de compresión y de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a>Ejemplo de JSON: copiar los datos de tooAzure HDFS local Blob
Este ejemplo se muestra cómo toocopy datos desde un tooAzure HDFS local almacenamiento de blobs. Sin embargo, se pueden copiar datos **directamente** tooany de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.  

ejemplo de Hola proporciona definiciones de JSON para hello siguiendo las entidades de la factoría de datos. Puede usar estos toocreate definiciones una toocopy de datos de canalización de HDFS tooAzure almacenamiento de blobs mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).

1. Un servicio vinculado del tipo [OnPremisesHdfs](#linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [FileShare](#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [FileSystemSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

ejemplo de Hola copia datos de un tooan HDFS local blobs de Azure cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

Como primer paso, configurar la puerta de enlace de administración de datos de Hola. Hola instrucciones de hello [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.

**Servicio vinculado de HDFS:** en este ejemplo usa Hola autenticación de Windows. Consulte la sección [Propiedades del servicio vinculado de HDFS](#linked-service-properties) para conocer los diferentes tipos de autenticación que se pueden usar.

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

**Servicio vinculado de Almacenamiento de Azure:**

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

**Conjunto de datos de entrada de HDFS:** este conjunto de datos hace referencia a carpeta HDFS toohello DataTransfer/UnitTest /. canalización de Hello copia todos los archivos de hello en este destino de carpeta toohello.

Establecer "externo": "true" informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

**Conjunto de datos de salida de blob de Azure:**

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1). ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Actividad de copia en una canalización con origen del sistema de archivos y receptor blob:**

canalización de Hello contiene una actividad de copia que esté configurado toouse estos conjuntos de datos de entrada y salidas o toorun programada cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**FileSystemSource** y **receptor** tipo está establecido demasiado**BlobSink**. consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos Hola Hola más allá de hora toocopy.

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a>Uso de autenticación Kerberos para el conector HDFS
Hay dos tooset de opciones de entorno local de hello así como toouse la autenticación Kerberos en el conector de HDFS. Puede elegir Hola uno se adapta mejor a su caso.
* Opción 1: [Unirse a la máquina de puerta de enlace en el dominio Kerberos](#kerberos-join-realm)
* Opción 2: [Habilitar la confianza mutua entre el dominio de Windows y el dominio Kerberos](#kerberos-mutual-trust)

### <a name="kerberos-join-realm"></a>Opción 1: Unirse a la máquina de puerta de enlace en el dominio Kerberos

#### <a name="requirement"></a>Requisito:

* máquina de puerta de enlace de Hello necesita dominio Kerberos de toojoin hello y no puede unir a ningún dominio de Windows.

#### <a name="how-tooconfigure"></a>¿Cómo tooconfigure:

**En la máquina de puerta de enlace:**

1.  Ejecute hello **Ksetup** utilidad tooconfigure Hola servidor KDC de Kerberos o el dominio Kerberos.

    máquina de Hello debe configurarse como un miembro de un grupo de trabajo desde un dominio Kerberos que es diferente de un dominio de Windows. Esto puede lograrse estableciendo el dominio Kerberos de Hola y agregar un servidor KDC como sigue. Sustituya *REALM.COM* por su dominio respectivo, según sea necesario.

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    **Reinicie** máquina Hola después de ejecutar estos 2 comandos.

2.  Comprobar la configuración de hello con **Ksetup** comando. salida de Hello será similar:

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

**En Azure Data Factory:**

* Configure el conector HDFS de hello mediante **autenticación de Windows** junto con Kerberos principal nombre y la contraseña tooconnect toohello HDFS origen de datos. Compruebe la sección [HDFS Linked Service properties](#linked-service-properties) (Propiedades de servicio vinculado de HDFS) en los detalles de configuración.

### <a name="kerberos-mutual-trust"></a>Opción 2: Habilitar la confianza mutua entre el dominio de Windows y el dominio Kerberos

#### <a name="requirement"></a>Requisito:
*   máquina de puerta de enlace de Hello debe unirse a un dominio de Windows.
*   Necesita una configuración del controlador de dominio de permiso tooupdate Hola.

#### <a name="how-tooconfigure"></a>¿Cómo tooconfigure:

> [!NOTE]
> Reemplazar dominio.com y AD.COM en hello sigue el tutorial con su propio controlador de dominio Kerberos y el dominio respectivo según sea necesario.

**En el servidor KDC:**

1.  Editar configuración de KDC de hello en **krb5.conf** toolet archivo KDC confiar en que hace referencia toohello después de la plantilla de configuración de dominio de Windows. De forma predeterminada, se encuentra en configuración de hello **/etc/krb5.conf**.

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  **Reinicie** Hola servicio KDC después de la configuración.

2.  Preparar una entidad de seguridad denominado  **krbtgt/REALM.COM@AD.COM**  en el servidor KDC con hello siguiente comando:

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  En el archivo de configuración de servicio de HDFS **hadoop.security.auth_to_local**, agregue `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.

**En el controlador de dominio:**

1.  Ejecute hello siguiente **Ksetup** comandos tooadd una entrada de dominio:

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  Establecer la confianza de dominio Kerberos del dominio de Windows tooKerberos. [contraseña] es la contraseña de Hola de entidad de seguridad de hello  **krbtgt/REALM.COM@AD.COM** .

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  Seleccione el algoritmo de cifrado usado en Kerberos.

    1. Vaya tooServer Manager > Administración de directivas de grupo > dominio > objetos de directiva de grupo > predeterminado o la directiva de dominio de Active y la edición.

    2. Hola **Editor de administración de directivas de grupo** ventana emergente, vaya tooComputer configuración > directivas > configuración de Windows > configuración de seguridad > directivas locales > Opciones de seguridad y configurar **red seguridad: configurar los tipos de cifrado permitidos para que Kerberos**.

    3. Algoritmo de cifrado de hello seleccione desea toouse cuando conecta tooKDC. Normalmente, puede seleccionar simplemente todas las opciones de Hola.

        ![Configuración de tipos de cifrado para Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. Use **Ksetup** toobe comando toospecify Hola cifrado algoritmo usado en hello territorio específico.

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  Crear asignación de hello entre Hola cuenta y de dominio Kerberos principal, en orden toouse principal de Kerberos en el dominio de Windows.

    1. Iniciar herramientas administrativas de hello > **equipos y usuarios de Active Directory**.

    2. Configure características avanzadas; para ello, haga clic en **Ver** > **Características avanzadas**.

    3. Busque Hola cuenta toowhich desee toocreate asignaciones y haga clic en tooview **las asignaciones de nombres** > haga clic en **nombres Kerberos** ficha.

    4. Agregar una entidad de seguridad de dominio Kerberos de Hola.

        ![Asignación de la identidad de seguridad](media/data-factory-hdfs-connector/map-security-identity.png)

**En la máquina de puerta de enlace:**

* Ejecute hello siguiente **Ksetup** comandos tooadd una entrada de dominio Kerberos.

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

**En Azure Data Factory:**

* Configure el conector HDFS de hello mediante **autenticación de Windows** junto con su cuenta de dominio o el origen de datos de entidad de seguridad de Kerberos tooconnect toohello HDFS. Compruebe la sección [HDFS Linked Service properties](#linked-service-properties) (Propiedades de servicio vinculado de HDFS) en los detalles de configuración.

> [!NOTE]
> columnas de toomap de toocolumns de conjunto de datos de origen del conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).


## <a name="performance-and-tuning"></a>Rendimiento y optimización
Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.
