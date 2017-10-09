---
title: "aaaCopy tooand de datos de almacén de Azure Data Lake | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocopy tooand de datos de almacén de Data Lake mediante el uso de Data Factory de Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a>Copiar datos tooand de almacén de Data Lake con factoría de datos
Este artículo se explica cómo toouse actividad de copia de Data Factory de Azure toomove datos tooand de almacén de Azure Data Lake. Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, información general sobre el movimiento de datos con la actividad de copia.

## <a name="supported-scenarios"></a>Escenarios admitidos
Puede copiar datos **de almacén de Azure Data Lake** toohello siguientes almacenes de datos:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Puede copiar los datos de hello siguientes almacenes de datos **tooAzure almacén de Data Lake**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Cree una cuenta de Data Lake Store antes de crear una canalización con la actividad de copia. Para más información, consulte [Introducción a Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).

## <a name="supported-authentication-types"></a>Tipos de autenticación que se admiten
Conector de almacén de Data Lake Hello es compatible con estos tipos de autenticación:
* Autenticación de entidad de servicio
* Autenticación de credenciales de usuario (OAuth) 

Se recomienda que use la autenticación de la entidad de servicio, en especial para una copia de datos programada. Con la autenticación se credenciales de usuario puede darse la situación de que expiren los tokens. Para obtener detalles de configuración, vea hello [vinculado propiedades del servicio](#linked-service-properties) sección.

## <a name="get-started"></a>Primeros pasos
Puede crear una canalización con actividad de copia que mueva los datos hacia Azure Data Lake Store y desde este servicio mediante el uso de diferentes herramientas o API.

toocreate de manera más fácil de Hello datos toocopy canalización es hello de toouse **Asistente para copiar**. Para obtener un tutorial sobre cómo crear una canalización mediante Hola Asistente para copiar, consulte [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md).

También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:

1. Crear una **factoría de datos**. Una factoría de datos puede contener una o más canalizaciones. 
2. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink. Por ejemplo, si va a copiar datos desde un tooan de almacenamiento de blobs de Azure almacén de Data Lake de Azure, cree dos toolink servicios vinculados su cuenta de almacenamiento de Azure y la factoría de datos de Azure Data Lake almacén tooyour. Para las propiedades de servicio vinculado que son específico tooAzure almacén de Data Lake, consulte [vinculado propiedades del servicio](#linked-service-properties) sección. 
2. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. En el ejemplo de Hola mencionado en el último paso de hello, se crea un contenedor de blobs de hello toospecify de conjunto de datos y la carpeta que contiene los datos de entrada de Hola. Y crear otra conjunto de datos toospecify Hola carpeta y la ruta en el almacén de Data Lake de Hola que contiene datos de hello copiados desde el almacenamiento de blobs de Hola. Para las propiedades del conjunto de datos que son específico tooAzure almacén de Data Lake, consulte [propiedades de conjunto de datos](#dataset-properties) sección.
3. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. En el ejemplo de Hola que se ha mencionado anteriormente, use BlobSource como un origen y AzureDataLakeStoreSink como un receptor para la actividad de copia de Hola. De forma similar, si va a copiar desde el almacén de Azure Data Lake tooAzure almacenamiento de blobs, usar AzureDataLakeStoreSource y BlobSink de actividad de copia de Hola. Para copiar propiedades de actividad que son específico tooAzure almacén de Data Lake, consulte [copiar propiedades de la actividad](#copy-activity-properties) sección. Para obtener detalles sobre cómo toouse un almacén de datos como un origen o un receptor, haga clic en el vínculo de hello en la sección anterior de hello para el almacén de datos.  

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener ejemplos con definiciones de JSON para entidades de factoría de datos que son utilizados toocopy datos hacia y desde un almacén de Data Lake de Azure, vea [ejemplos JSON](#json-examples-for-copying-data-to-and-from-data-lake-store) sección de este artículo.

Hello las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizado toodefine factoría de datos de entidades específico tooData Lake almacén.

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Un servicio vinculado vincula una factoría de datos de tooa de almacén de datos. Crear un servicio vinculado de tipo **AzureDataLakeStore** toolink su factoría de datos de almacén de Data Lake datos tooyour. Hello en la tabla siguiente describe los servicios de tooData Lake almacén vinculado específicos de elementos JSON. Puede elegir entre la autenticación de la entidad de servicio y la autenticación de credenciales de usuario.

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| **type** | se debe establecer propiedad de tipo Hello demasiado**AzureDataLakeStore**. | Sí |
| **dataLakeStoreUri** | Información acerca de la cuenta de almacén de Azure Data Lake Hola. Esta información toma una de hello siguientes formatos: `https://[accountname].azuredatalakestore.net/webhdfs/v1` o `adl://[accountname].azuredatalakestore.net/`. | Sí |
| **subscriptionId** | Hola de toowhich de Id. de suscripción de Azure cuenta de almacén de Data Lake pertenece. | Necesario para el receptor |
| **resourceGroupName** | Hola de toowhich de nombre de grupo de recursos de Azure cuenta de almacén de Data Lake pertenece. | Necesario para el receptor |

### <a name="service-principal-authentication-recommended"></a>Autenticación de la entidad de servicio (recomendada)
toouse autenticación principal del servicio, registrar una entidad de la aplicación en Azure Active Directory (Azure AD) y conceda a Hola acceso tooData Lake almacén. Consulte [Autenticación entre servicios](../data-lake-store/data-lake-store-authenticate-using-active-directory.md) para ver los pasos detallados. Tome nota de hello después de valores, que se utiliza toodefine Hola servicio vinculado:
* Identificador de aplicación
* Clave de la aplicación 
* Id. de inquilino

> [!IMPORTANT]
> Si usas las canalizaciones de datos de hello Asistente para copiar tooauthor, asegúrese de que concedan entidad de servicio de hello al menos un **lector** rol en el control de acceso (administración de identidades y acceso) para la cuenta de almacén de Data Lake Hola. Además, al menos a conceder entidad de servicio de Hola **lectura + Execute** raíz de almacén de Data Lake tooyour de permiso ("/") y sus elementos secundarios. En caso contrario, puede aparecer el mensaje de Hola "hello las credenciales proporcionaron no son válidos".<br/><br/>
Después de crear o actualizar a una entidad de servicio en Azure AD, puede tardar unos minutos para hello cambios tootake efecto. Compruebe la entidad de servicio de Hola y configuraciones de lista (ACL) de control de acceso de almacén de Data Lake. Si todavía aparece el mensaje de saludo "¡hello las credenciales proporcionaron no son válidos", espere unos instantes e inténtelo de nuevo.

Utilizar autenticación de entidad de seguridad de servicio mediante la especificación de hello propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| **servicePrincipalId** | Especifique el identificador de cliente de. la aplicación hello | Sí |
| **servicePrincipalKey** | Especifique la clave de la aplicación hello. | Sí |
| **tenant** | Especifique la información de inquilino de hello (inquilino o el nombre de identificador de dominio) en que se encuentra la aplicación. Puede recuperarlo mediante el desplazamiento del mouse de hello en la esquina superior derecha de Hola de hello portal de Azure. | Sí |

**Ejemplo: autenticación de la entidad de servicio**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Autenticación de credenciales de usuario
Como alternativa, puede usar toocopy de autenticación de credenciales de usuario de o tooData Lake almacén mediante la especificación de hello propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| **authorization** | Haga clic en hello **Authorize** botón Hola Editor de generador de datos y escriba sus credenciales que asigna la propiedad de hello autogenerado autorización URL toothis. | Sí |
| **sessionId** | Identificador de sesión de OAuth de sesión de autorización de OAuth de Hola. Cada id. de sesión es único y solo se puede usar una vez. Esta configuración se genera automáticamente cuando se usa Hola Editor de generador de datos. | Sí |

**Ejemplo: autenticación de credenciales de usuario**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a>Expiración del token
Hola código de autorización que genera mediante el uso de hello **Authorize** botón expira transcurrido un período de tiempo. Hola sigue mensaje significa que ese token de autenticación Hola expiró:

Error de operación de credencial: invalid_grant - AADSTS70002: error al validar las credenciales. AADSTS70008: Hola proporciona concesión de acceso expiró o se revocó. Id. de seguimiento: d18629e8-af88-43c5-88e3-d8419eb1fca1 Id. de correlación: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Marca de tiempo: 2015-12-15 21:09:31Z.

Hello tabla siguiente muestran los tiempos de expiración de Hola de diferentes tipos de cuentas de usuario:


| Tipo de usuario | Expira después de |
|:--- |:--- |
| Cuentas de usuario *no* administradas por Azure Active Directory (por ejemplo, @hotmail.com o @live.com) |12 horas |
| Cuentas de usuario administradas por Azure Active Directory |ejecutar 14 días después de último segmento de Hola <br/><br/>90 días, si un segmento basado en un servicio vinculado basado en OAuth se ejecuta al menos una vez cada 14 días. |

Si cambia la contraseña anterior a la hora de expiración del token de hello, símbolo (token) de hello caduca inmediatamente. Verá mensajes de bienvenida se ha mencionado anteriormente en esta sección.

Puede autorizar la cuenta de hello mediante el uso de hello **Authorize** botón cuando caduca de token de Hola Hola tooredeploy servicio vinculado. También pueden generar valores de hello **sessionId** y **autorización** Hola propiedades mediante programación mediante el uso de código siguiente:


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
Para obtener más información acerca de las clases de factoría de datos de hello usarse en el código de hello, vea hello [azuredatalakestorelinkedservice clase](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService clase](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), y [ Clase AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) temas. Agregar una referencia tooversion `2.9.10826.1824` de `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` para hello `WindowsFormsWebAuthenticationDialog` clase usada en el código de hello.

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
un conjunto de datos toorepresent datos de entrada en un almacén de Data Lake toospecify, Establece hello **tipo** propiedad del conjunto de datos de hello demasiado**AzureDataLakeStore**. Conjunto hello **linkedServiceName** propiedad del nombre de toohello Hola conjunto de datos de almacén de Data Lake hello servicio vinculado. Para obtener una lista completa de las secciones JSON y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones de un conjunto de datos de JSON, como **structure**, **availability** y **policy**, son similares para todos los tipos de datos (base de datos SQL de Azure, blob de Azure y tabla de Azure, por ejemplo). Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información como la ubicación y el formato de datos de hello en el almacén de datos de Hola. 

Hola **typeProperties** sección para un conjunto de datos de tipo **AzureDataLakeStore** contiene Hola propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| **folderPath** |Contenedor de toohello de ruta de acceso y la carpeta en el almacén de Data Lake. |Sí |
| **fileName** |Nombre del archivo de hello en el almacén de Azure Data Lake. Hola **fileName** propiedad es opcional y distingue mayúsculas de minúsculas. <br/><br/>Si especifica **fileName**, actividad de hello (incluida la copia) funciona en archivos específicos de Hola.<br/><br/>Cuando **fileName** no se especifica, copia incluye todos los archivos en **folderPath** en el conjunto de datos de entrada de Hola.<br/><br/>Cuando **fileName** no se especifica para un conjunto de datos de salida y **preserveHierarchy** no se especifica en el receptor de actividad, nombre de Hola de archivo hello generado está en formato de hello datos. _GUID_.txt'. Por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt. |No |
| **partitionedBy** |Hola **partitionedBy** propiedad es opcional. Puede usarlo toospecify una ruta de acceso dinámico y el nombre de archivo de datos de serie temporal. Por ejemplo, se puede parametrizar **folderPath** por cada hora de datos. Para obtener más información y ejemplos, vea [Hola propiedad partitionedBy](#using-partitionedby-property). |No |
| **format** | se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, y  **ParquetFormat**. Conjunto hello **tipo** propiedad bajo **formato** tooone de estos valores. Para obtener más información, vea hello [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [el formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato ORC](data-factory-supported-file-and-compression-formats.md#orc-format), y [Parquet formato ](data-factory-supported-file-and-compression-formats.md#parquet-format) secciones de hello [compresión de archivos y formatos admitidos por factoría de datos de Azure](data-factory-supported-file-and-compression-formats.md) artículo. <br><br> Si desea que los archivos de toocopy "como-es" entre los almacenes basados en archivos (copia binaria), omitir hello `format` sección en ambas definiciones de conjunto de datos de entrada y salida. |No |
| **compression** | Especificar tipo de Hola y el nivel de compresión para datos de Hola. Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**. Niveles admitidos son **Optimal** y **Fastest**. Para más información, consulte el artículo sobre [Formatos de compresión de archivos admitidos por Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

### <a name="hello-partitionedby-property"></a>propiedad de Hello partitionedBy
Puede especificar dinámica **folderPath** y **fileName** propiedades para los datos de serie temporal con hello **partitionedBy** propiedad, funciones de factoría de datos y sistema variables. Para obtener más información, vea hello [factoría de datos de Azure: funciones y variables del sistema](data-factory-functions-variables.md) artículo.


En el siguiente ejemplo, el Hola `{Slice}` se reemplaza con el valor de Hola de variable del sistema Hola factoría de datos `SliceStart` en formato de hello especificado (`yyyyMMddHH`). nombre de Hello `SliceStart` hace referencia toohello hora de inicio del segmento de Hola. Hola `folderPath` propiedad es diferente para cada segmento, como en `wikidatagateway/wikisampledataout/2014100103` o `wikidatagateway/wikisampledataout/2014100104`.

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

Hola siguiente ejemplo, año hello, mes, día y hora de `SliceStart` se extraen en variables independientes que usan hello `folderPath` y `fileName` propiedades:
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
Para obtener más detalles sobre los conjuntos de datos de series temporales, programación y segmentos, vea hello [conjuntos de datos de Data Factory de Azure](data-factory-create-datasets.md) y [programación de la factoría de datos y la ejecución](data-factory-scheduling-and-execution.md) artículos. 


## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de las secciones y las propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

Hola propiedades disponibles en hello **typeProperties** sección de una actividad varían con cada tipo de actividad. Para una actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.

**AzureDataLakeStoreSource** admite Hola después propiedad Hola **typeProperties** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| **recursive** |Indica si los datos de Hola es de lectura de forma recursiva de las subcarpetas de Hola o solo de la carpeta especificada de Hola. |True (valor predeterminado), False |No |


**AzureDataLakeStoreSink** admite Hola propiedades Hola siguientes **typeProperties** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| **copyBehavior** |Especifica el comportamiento de la copia de Hola. |<b>PreserveHierarchy</b>: conserva la jerarquía de archivos de hello en la carpeta de destino de Hola. ruta de acceso relativa de Hola de carpeta de origen del archivo toosource es idéntico toohello ruta de acceso relativa de la carpeta de tootarget de archivo de destino.<br/><br/><b>FlattenHierarchy</b>: todos los archivos de la carpeta de origen Hola se crean en el primer nivel de carpeta de destino de Hola de Hola. archivos de destino de Hola se crean con nombres generados automáticamente.<br/><br/><b>MergeFiles</b>: combina todos los archivos del archivo de tooone de carpeta de origen de hello. Si hello nombre de archivo o blob no se especifica, nombre de archivo combinado de hello es nombre especificado de Hola. En caso contrario, el nombre del archivo de hello es generado automáticamente. |No |

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

## <a name="supported-file-and-compression-formats"></a>Formatos de archivo y de compresión admitidos
Para obtener más información, vea hello [compresión de archivos y formatos de factoría de datos de Azure](data-factory-supported-file-and-compression-formats.md) artículo.

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a>Ejemplos JSON para copiar datos tooand de almacén de Data Lake
Hello en los ejemplos siguientes proporciona definiciones de JSON de ejemplo. Puede usar estos toocreate de definiciones de ejemplo una canalización mediante hello [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Hola ejemplos se muestra cómo toocopy tooand de datos desde el almacenamiento de blobs de Azure y de almacén de Data Lake. Sin embargo, se pueden copiar datos _directamente_ desde cualquiera de hello orígenes tooany de receptores de hello compatible. Para obtener más información, consulte sección de Hola "almacenes de datos admitidos y formatos" Hola [mover datos mediante la actividad de copia](data-factory-data-movement-activities.md) artículo.  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a>Ejemplo: Copiar los datos de almacenamiento de blobs de Azure tooAzure almacén de Data Lake
Muestra el código de ejemplo de Hola en esta sección:

* Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Un servicio vinculado de tipo [AzureDataLakeStore](#linked-service-properties).
* Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureDataLakeStore](#dataset-properties).
* Una [canalización](data-factory-create-pipelines.md) con una actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) y [AzureDataLakeStoreSink](#copy-activity-properties).

Hello ejemplos muestran cómo series temporales datos desde almacenamiento de blobs de Azure están copiar tooData Lake almacén cada hora. 

**Servicio vinculado de Almacenamiento de Azure**

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

**Servicio vinculado de Azure Data Lake Store**

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> Para obtener detalles de configuración, vea hello [vinculado propiedades del servicio](#linked-service-properties) sección.
>

**Conjunto de datos de entrada de blob de Azure:**

En el siguiente ejemplo de Hola, datos recoge de un blob nuevo cada hora (`"frequency": "Hour", "interval": 1`). Hola ruta de acceso y nombre de la carpeta para el blob de Hola se evalúan dinámicamente en función del tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta de Hello usa Hola año, mes y parte de día de la hora de inicio de Hola. nombre de archivo de Hello usa hora Hola parte del programa Hola a la hora de inicio. Hola `"external": true` configuración indica el servicio de factoría de datos de hello esa tabla hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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

**Conjunto de datos de salida de Azure Data Lake Store**

Hola siguiente ejemplo copia datos tooData Lake almacén. Se copian los datos nuevos tooData Lake almacén cada hora.

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


**Actividad de copia en una canalización con un origen de blob y el receptor de Azure Data Lake Store**

En el siguiente ejemplo de Hola, canalización de hello contiene una actividad de copia que se configura toouse Hola conjuntos de datos de entrada y salida. actividad de copia de Hello es toorun programada cada hora. En la definición de JSON de canalización de hello, Hola `source` tipo está establecido demasiado`BlobSource`, hello y `sink` tipo está establecido demasiado`AzureDataLakeStoreSink`.

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
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

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a>Ejemplo: Copiar los datos de almacén de Azure Data Lake tooan blobs de Azure
Muestra el código de ejemplo de Hola en esta sección:

* Un servicio vinculado de tipo [AzureDataLakeStore](#linked-service-properties).
* Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureDataLakeStore](#dataset-properties).
* Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Una [canalización](data-factory-create-pipelines.md) con una actividad de copia que usa [AzureDataLakeStoreSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

código de Hello copia datos de serie temporal de almacén de Data Lake tooan blobs de Azure cada hora. 

**Servicio vinculado de Azure Data Lake Store**

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> Para obtener detalles de configuración, vea hello [vinculado propiedades del servicio](#linked-service-properties) sección.
>

**Servicio vinculado de Almacenamiento de Azure**

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
**Conjunto de datos de entrada de Azure Data Lake**

En este ejemplo, si se establece `"external"` demasiado`true` informa a servicio de factoría de datos de hello esa tabla hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
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
**Conjunto de datos de salida de blob de Azure**

En el siguiente ejemplo de Hola, se escriben datos tooa nuevo blob cada hora (`"frequency": "Hour", "interval": 1`). ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta de Hello usa Hola año, mes, día y parte de horas de la hora de inicio de Hola.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Una actividad de copia en una canalización con un origen de Azure Data Lake Store y un receptor de blob**

En el siguiente ejemplo de Hola, canalización de hello contiene una actividad de copia que se configura toouse Hola conjuntos de datos de entrada y salida. actividad de copia de Hello es toorun programada cada hora. En la definición de JSON de canalización de hello, Hola `source` tipo está establecido demasiado`AzureDataLakeStoreSource`, hello y `sink` tipo está establecido demasiado`BlobSink`.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
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

En la definición de la actividad de copia de hello, también puede asignar columnas de hello toocolumns de conjunto de datos de origen en el conjunto de datos de hello receptor. Para obtener más información, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Rendimiento y optimización
toolearn acerca de los factores de Hola que afectan al rendimiento de la actividad de copia y cómo toooptimize, vea hello [actividad de copia Guía de rendimiento y optimización](data-factory-copy-activity-performance.md) artículo.
