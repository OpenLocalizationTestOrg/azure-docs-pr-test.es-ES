---
title: "herramienta de migración de aaaDatabase para la base de datos de Azure Cosmos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola Abrir origen base de datos de Azure Cosmos datos migración herramientas tooimport datos tooAzure DB Cosmos desde diversos orígenes, incluidos los archivos de MongoDB, SQL Server, almacenamiento de tabla, DynamoDB de Amazon, CSV y JSON. Conversión de tooJSON CSV."
keywords: "CSV toojson, herramientas de migración de base de datos, convertir csv toojson"
services: cosmos-db
author: andrewhoh
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: d173581d-782a-445c-98d9-5e3c49b00e25
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 997648a31602d854db75bb6ce4e2ecff36fc1069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a>¿Cómo tooimport datos en la base de datos de Azure Cosmos para Hola API de documentos?

Este tutorial proporciona instrucciones sobre cómo utilizar Hola base de datos de Azure Cosmos: herramienta de migración de datos de API de documentos, que puede importar datos de varios orígenes, incluidos los archivos JSON, CSV, archivos, SQL, MongoDB, almacenamiento de tabla de Azure, DynamoDB de Amazon y documentos de base de datos de Azure Cosmos Colecciones de API en colecciones para usan con hello API de documentos y la base de datos de Azure Cosmos. herramienta de migración de datos de Hello también puede usarse cuando se migra de una colección de varias particiones de una única partición colección tooa para hello API de documentos.

herramienta de migración de datos de Hello solo funciona al importar datos en la base de datos de Azure Cosmos para usar con hello API de documentos. En este momento no se admite la importación de datos para su uso con Hola API de tabla o la API Graph. 

tooimport los datos para su uso con hello MongoDB API, consulte [base de datos de Azure Cosmos: cómo toomigrate datos de Hola MongoDB API?](mongodb-migrate.md).

Este tutorial trata Hola siguientes tareas:

> [!div class="checklist"]
> * Instalación de la herramienta de migración de datos de Hola
> * Importación de datos de orígenes de datos diferentes
> * Exportar desde la base de datos de Azure Cosmos tooJSON

## <a id="Prerequisites"></a>Requisitos previos
Antes de seguir las instrucciones de hello en este artículo, asegúrese de que tiene instalado el siguiente hello:

* [Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) o superior.

## <a id="Overviewl"></a>Información general sobre la herramienta de migración de datos de Hola
herramienta de migración de datos de Hello es una solución de código abierto que importa datos tooAzure DB Cosmos desde una variedad de orígenes, incluidas:

* Archivos JSON
* MongoDB
* SQL Server
* Archivos CSV
* Almacenamiento de tablas de Azure
* Amazon DynamoDB
* HBase
* Colecciones de Azure Cosmos DB

Mientras que la herramienta de importación Hola incluye una interfaz gráfica de usuario (dtui.exe), también se puede controlar desde la línea de comandos de hello (dt.exe). De hecho, hay un comando de opción toooutput Hola asociado después de configurar una importación a través de la interfaz de usuario de Hola. Se pueden transformar datos tabulares de origen (por ejemplo, archivos de SQL Server o CSV) de tal forma que se pueden crear relaciones jerárquicas (subdocumentos) durante la importación. Siga leyendo toolearn más información sobre opciones de fuente, tooimport de líneas de comandos de ejemplo de cada origen, importación opciones de destino y ver los resultados.

## <a id="Install"></a>Instalar la herramienta de migración de datos de Hola
código de fuente de herramienta de migración de Hello está disponible en GitHub en [este repositorio](https://github.com/azure/azure-documentdb-datamigrationtool) y está disponible en una versión compilada [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d). Puede compilar la solución de Hola o simplemente descargar y extraer el directorio de tooa Hola versión compilada de su elección. A continuación, ejecute:

* **Dtui.exe**: versión de interfaz gráfica de la herramienta de Hola
* **DT.exe**: versión de línea de comandos de herramienta de Hola

## <a name="import-data"></a>Importar datos

Una vez haya instalado la herramienta de hello, es hora tooimport los datos. ¿Qué tipo de datos ¿desea tooimport?

* [Archivos JSON](#JSON)
* [MongoDB](#MongoDB)
* [Archivos de exportación de MongoDB](#MongoDBExport)
* [SQL Server](#SQL)
* [Archivos CSV](#CSV)
* [Azure Table Storage](#AzureTableSource)
* [Amazon DynamoDB](#DynamoDBSource)
* [Blob](#BlobImport)
* [Colecciones de Azure Cosmos DB](#DocumentDBSource)
* [HBase](#HBaseSource)
* [Importación masiva de Azure Cosmos DB](#DocumentDBBulkImport)
* [Importación de registros secuenciales de Azure Cosmos DB](#DocumentDSeqTarget)


## <a id="JSON"></a>archivos JSON tooimport
opción de importador de origen de archivo JSON de Hello permite tooimport uno o más archivos JSON de único documento o archivos JSON que contienen una matriz de documentos JSON. Al agregar las carpetas que contienen JSON archivos tooimport, tendrá posibilidad de Hola de búsqueda de archivos en subcarpetas de forma recursiva.

![Captura de pantalla de opciones de origen de archivos JSON: herramientas de migración de base de datos](./media/import-data/jsonsource.png)

Estos son algunos archivos JSON de tooimport de ejemplos de línea de comandos:

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition hello data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <a id="MongoDB"></a>tooimport de MongoDB

> [!IMPORTANT]
> Si va a importar la cuenta de base de datos de Azure Cosmos tooan con soporte para MongoDB, siga estas [instrucciones](mongodb-migrate.md).
> 
> 

Hola opción de importador de código fuente de MongoDB permite tooimport de una colección de MongoDB individual y, opcionalmente, filtrar documentos mediante una consulta o modificar la estructura del documento hello mediante una proyección.  

![Captura de pantalla de las opciones de origen de MongoDB](./media/import-data/mongodbsource.png)

cadena de conexión de Hello está en formato de MongoDB estándar de hello:

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> Puede tener acceso a la utilice Hola Compruebe comando tooensure que Hola instancia MongoDB especificado en el campo de cadena de conexión de Hola.
> 
> 

Escriba el nombre de Hola de colección de Hola desde el que se importarán los datos. Si lo desea, puede especificar o proporcionar un archivo para una consulta (por ejemplo, {pop: {$gt: 5000}}) o proyección (p. ej. {loc:0}) tooboth filtro y la forma Hola datos toobe importado.

Estos son algunos tooimport de ejemplos de línea de comandos de MongoDB:

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <a id="MongoDBExport"></a>archivos de exportación de MongoDB tooimport

> [!IMPORTANT]
> Si va a importar la cuenta de base de datos de Azure Cosmos tooan con soporte para MongoDB, siga estas [instrucciones](mongodb-migrate.md).
> 
> 

Hola opción importador de origen de archivo JSON de MongoDB exportación permite tooimport uno o más archivos JSON procedentes de la utilidad de mongoexport Hola.  

![Captura de pantalla de las opciones de origen de exportación de MongoDB](./media/import-data/mongodbexportsource.png)

Al agregar las carpetas que contienen archivos de JSON de exportación de MongoDB para la importación, se tiene la opción de Hola de búsqueda de archivos en subcarpetas de forma recursiva.

Este es un tooimport de ejemplo de línea de comandos de la exportación de MongoDB archivos JSON:

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <a id="SQL"></a>tooimport de SQL Server
Hola opción de importador de código fuente SQL permite tooimport desde una base de datos de SQL Server individual y, opcionalmente, filtrar Hola registros toobe importar utilizando una consulta. Además, puede modificar la estructura del documento Hola especificando un separador de anidamiento (más en un momento).  

![Captura de pantalla de opciones de origen de SQL: herramientas de migración de base de datos](./media/import-data/sqlexportsource.png)

Hola formato de cadena de conexión de hello es Hola estándar SQL conexión cadena.

> [!NOTE]
> Puede tener acceso a la utilice Hola Compruebe comando tooensure que Hola la instancia de SQL Server especificada en el campo de cadena de conexión de Hola.
> 
> 

Hola anidar la propiedad separator es toocreate usa las relaciones jerárquicas (documentos secundarios) durante la importación. Considere la posibilidad de hello después de la consulta SQL:

*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as Address.AddressType, AddressLine1 as Address.AddressLine1, City as Address.Location.City, StateProvinceName as Address.Location.StateProvinceName, PostalCode as Address.PostalCode, CountryRegionName as Address.CountryRegionName from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*

Que devuelve Hola después de resultados (parciales):

![Screenshot of SQL query results](./media/import-data/sqlqueryresults.png)

Tenga en cuenta los alias de hello como Address.AddressType y Address.Location.StateProvinceName. Mediante la especificación de un separador de anidamiento de '.', la herramienta de importación Hola crea dirección e importación de subdocumentos Address.Location durante Hola. Este es un ejemplo de un documento resultante en Azure Cosmos DB:

*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*

Estos son algunos tooimport de ejemplos de línea de comandos de SQL Server:

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <a id="CSV"></a>archivos CSV de tooimport y convertir CSV tooJSON
Hola opción de importador de origen de archivo CSV permite tooimport uno o varios archivos CSV. Al agregar las carpetas que contienen archivos CSV para la importación, se tiene la opción de Hola de búsqueda de archivos en subcarpetas de forma recursiva.

![Opciones de origen de la captura de pantalla de CSV - CSV tooJSON](media/import-data/csvsource.png)

Origen SQL de toohello similar, Hola anidar la propiedad separator puede ser toocreate usa las relaciones jerárquicas (documentos secundarios) durante la importación. Considere la posibilidad de hello después de la fila de encabezado CSV y filas de datos:

![Registros de captura de pantalla de CSV de ejemplo - CSV tooJSON](./media/import-data/csvsample.png)

Tenga en cuenta los alias de hello como DomainInfo.Domain_Name y RedirectInfo.Redirecting. Mediante la especificación de un separador de anidamiento de '.', la herramienta de importación Hola creará DomainInfo e importación de subdocumentos RedirectInfo durante Hola. Este es un ejemplo de un documento resultante en Azure Cosmos DB:

*{"DomainInfo": {"Nombre_de_dominio": "ACUS.GOV", "Domain_Name_Address": "http://www. ACUS.GOV"},"Agencia Federal":"Conferencia administrativa de Estados Unidos de hello","RedirectInfo": {"Redirigir":"0","Redirect_Destination":" "},"id":"9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d"}*

herramienta de importación de Hello tratará de información de tipo de tooinfer de valores sin comillas en archivos CSV (valores entre comillas siempre se tratan como cadenas).  Los tipos se identifican en hello siguiendo el orden: número, fecha y hora, un valor booleano.  

Hay dos otro toonote cosas sobre la importación de CSV:

1. De forma predeterminada, los valores sin comillas se recortan siempre en tabuladores y espacios, mientras que los valores entre comillas se mantienen como son. Este comportamiento puede invalidarse con opción de línea de comandos de /s.TrimQuoted de casilla de verificación o hello valores entre comillas el recorte de hello.
2. De forma predeterminada, un valor null sin comillas se trata como un valor null. Este comportamiento puede invalidarse (es decir, tratar una opción null sin comillas como una cadena "null") con hello Treat sin comillas NULL como opción de línea de comandos de /s.NoUnquotedNulls de casilla de verificación o hello cadena.

Este es un ejemplo de línea de comandos para la importación CSV:

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <a id="AzureTableSource"></a>tooimport desde el almacenamiento de tabla de Azure
Hola opción de importador de origen de almacenamiento de tabla de Azure permite tooimport desde una tabla de almacenamiento de Azure tabla individual y, opcionalmente, filtrar Hola tabla entidades toobe importado. Tenga en cuenta que no puede usar datos de almacenamiento de tabla de Azure de tooimport herramienta de migración de datos de hello en la base de datos de Azure Cosmos para su uso con hello API de tabla. Se admite la importación sólo tooAzure DB Cosmos para su uso con hello API de documentos en este momento.

![Screenshot of Azure Table storage source options](./media/import-data/azuretablesource.png)

formato de Hola de hello cadena de conexión de almacenamiento de tabla de Azure es:

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> Puede tener acceso a la utilice Hola Compruebe comando tooensure que Hola instancia de almacenamiento de tabla de Azure especificada en el campo de cadena de conexión de Hola.
> 
> 

Escriba el nombre de Hola de hello Azure desde el que se importarán los datos de tabla. Opcionalmente, puede especificar un [filtro](https://msdn.microsoft.com/library/azure/ff683669.aspx).

Hola opción de importador de origen de almacenamiento de tabla de Azure consta de las siguientes opciones adicionales de hello:

1. Incluir campos internos
   1. All: incluir todos los campos internos (PartitionKey, RowKey y Timestamp)
   2. None: excluir todos los campos internos
   3. RowKey - sólo incluyen campos de hello RowKey
2. Seleccionar columnas
   1. Los filtros de almacenamiento de tablas de Azure no admiten proyecciones. Si desea tooonly importar propiedades de entidad de tabla de Azure específicas, agregarlos lista Seleccionar columnas de toohello. Se omitirán todas las demás propiedades de la entidad.

Este es un tooimport de ejemplo de línea de comandos desde el almacenamiento de tabla de Azure:

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <a id="DynamoDBSource"></a>tooimport de DynamoDB de Amazon
Hola opción de importador de código fuente de Amazon DynamoDB permite tooimport desde una tabla de Amazon DynamoDB individual y, opcionalmente, filtrar Hola entidades toobe importado. Se proporcionan varias plantillas para que configurar una importación resulte lo más fácil posible.

![Captura de pantalla de opciones de origen de Amazon DynamoD: herramientas de migración de base de datos](./media/import-data/dynamodbsource1.png)

![Captura de pantalla de opciones de origen de Amazon DynamoD: herramientas de migración de base de datos](./media/import-data/dynamodbsource2.png)

Hola formato de cadena de conexión de Amazon DynamoDB hello es:

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> Puede tener acceso a la utilice Hola Compruebe comando tooensure que Hola instancia Amazon DynamoDB especificado en el campo de cadena de conexión de Hola.
> 
> 

Este es un tooimport de ejemplo de línea de comandos de Amazon DynamoDB:

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <a id="BlobImport"></a>archivos de tooimport desde el almacenamiento de blobs de Azure
Hello archivo JSON, archivo de exportación de MongoDB y las opciones de importador de origen de archivo CSV le permiten tooimport uno o más archivos de almacenamiento de blobs de Azure. Después de especificar una dirección URL del contenedor de Blob y la clave de cuenta, basta con proporcionar un tooimport de los archivos de expresión regular tooselect Hola.

![Captura de pantalla de opciones de origen de archivos Blob](./media/import-data/blobsource.png)

Aquí es archivos JSON de tooimport de ejemplo de línea de comandos desde el almacenamiento de blobs de Azure:

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <a id="DocumentDBSource"></a>tooimport de una colección de API de documentos de base de datos de Azure Cosmos
Hola opción de importador de código fuente de base de datos de Azure Cosmos permite tooimport datos de una o varias recopilaciones de base de datos de Azure Cosmos y, opcionalmente, filtrar documentos mediante una consulta.  

![Captura de pantalla de opciones de origen de Azure Cosmos DB](./media/import-data/documentdbsource.png)

Hola formato de cadena de conexión de base de datos de Azure Cosmos hello es:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

cadena de conexión de cuenta de base de datos de Azure Cosmos Hola puede obtenerse de hoja de claves de Hola de hello portal de Azure, como se describe en [cómo toomanage una cuenta de base de datos de Azure Cosmos](manage-account.md); sin embargo, nombre de Hola de base de datos de hello debe toobe anexa toohello cadena de conexión en hello siguiendo el formato:

    Database=<CosmosDB Database>;

> [!NOTE]
> Puede tener acceso a la utilice Hola Compruebe comando tooensure que Hola instancia de base de datos de Azure Cosmos especificada en el campo de cadena de conexión de Hola.
> 
> 

tooimport desde una sola colección de base de datos de Azure Cosmos, escriba nombre de Hola de colección de Hola desde el que se importarán los datos. tooimport de varias colecciones de base de datos de Azure Cosmos, proporcionar una expresión regular toomatch uno o más nombres de colección (por ejemplo, collection01 | collection02 | collection03). Opcionalmente, se pueden especificar, o proporcionar un archivo para un filtro de consulta tooboth y Hola datos toobe importar de forma.

> [!NOTE]
> Puesto que el campo de la colección de hello acepta expresiones regulares, si va a importar desde una sola colección cuyo nombre contiene caracteres de expresión regular, los caracteres deben convertirse en consecuencia.
> 
> 

Hola opción de base de datos de Azure Cosmos origen importador tiene siguientes Hola opciones avanzadas:

1. Incluir campos internos: Especifica si se permite o no tooinclude las propiedades del sistema de documento de base de datos de Azure Cosmos Hola exportación (por ejemplo, _rid, _ts).
2. Número de reintentos en caso de error: especifica Hola número de veces tooretry Hola conexión tooAzure Cosmos DB en caso de errores transitorios (por ejemplo, interrupción de conectividad de red).
3. Intervalo de reintentos: Especifica cuánto tiempo toowait entre los reintentos de conexión tooAzure DB Cosmos de hello en caso de errores transitorios (por ejemplo, interrupción de conectividad de red).
4. Modo de conexión: Especifica toouse de modo de conexión de hello con base de datos de Azure Cosmos. las opciones disponibles de Hello son DirectTcp, DirectHttps y puerta de enlace. modos de conexión directa de Hello son más rápidos, mientras que el modo de puerta de enlace de hello es firewall más descriptivo como solo usa el puerto 443.

![Captura de pantalla de opciones avanzadas de origen de Azure Cosmos DB](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> modo de tooconnection de los valores predeterminados de herramienta DirectTcp de importación de Hola. Si experimenta problemas de firewall, cambie el modo de tooconnection puerta de enlace, ya que solo requiere el puerto 443.
> 
> 

Estos son algunos tooimport de ejemplos de línea de comandos de base de datos de Azure Cosmos:

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> Herramienta de importación de datos de Azure Cosmos DB Hello también admite la importación de datos de hello [emulador de base de datos de Azure Cosmos](local-emulator.md). Al importar datos desde un emulador local, establezca el punto de conexión de hello demasiado`https://localhost:<port>`. 
> 
> 

## <a id="HBaseSource"></a>tooimport de HBase
Hola opción de importador de código fuente de HBase permite tooimport datos de una tabla HBase y, opcionalmente, filtrar datos de Hola. Se proporcionan varias plantillas para que configurar una importación resulte lo más fácil posible.

![Captura de pantalla de opciones de origen de HBase](./media/import-data/hbasesource1.png)

![Captura de pantalla de opciones de origen de HBase](./media/import-data/hbasesource2.png)

Hola formato de cadena de conexión de HBase Stargate hello es:

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> Puede tener acceso a la utilice Hola Compruebe comando tooensure que Hola instancia HBase especificado en el campo de cadena de conexión de Hola.
> 
> 

Este es un tooimport de ejemplo de línea de comandos de HBase:

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API (importación masiva)
Importador de Hello Azure Cosmos DB masiva permite tooimport desde cualquiera de las opciones de origen disponible hello, utilizando un procedimiento de base de datos de Azure Cosmos almacenados para mejorar la eficacia. herramienta de Hello es compatible con la colección de base de datos de Azure Cosmos particiones único de importación tooone, así como importar particionada mediante el cual los datos se dividen en varias colecciones de base de datos de Azure Cosmos particiones único. Para más información sobre la creación de particiones de datos, consulte [Partición y escalado de datos en Azure Cosmos DB](partition-data.md). herramienta de Hello crear, ejecutar y, a continuación, elimine el procedimiento almacenado de Hola de las colecciones de destino de Hola.  

![Captura de pantalla de opciones de importación masiva de Azure Cosmos DB](./media/import-data/documentdbbulk.png)

Hola formato de cadena de conexión de base de datos de Azure Cosmos hello es:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

cadena de conexión de cuenta de base de datos de Azure Cosmos Hola puede obtenerse de hoja de claves de Hola de hello portal de Azure, como se describe en [cómo toomanage una cuenta de base de datos de Azure Cosmos](manage-account.md); sin embargo, nombre de Hola de base de datos de hello debe toobe anexa toohello cadena de conexión en hello siguiendo el formato:

    Database=<CosmosDB Database>;

> [!NOTE]
> Puede tener acceso a la utilice Hola Compruebe comando tooensure que Hola instancia de base de datos de Azure Cosmos especificada en el campo de cadena de conexión de Hola.
> 
> 

tooimport tooa única colección, escriba nombre de Hola de hello colección toowhich datos se va a importar y haga clic en el botón de agregar Hola. tooimport toomultiple colecciones, escriba los nombres de colección individualmente o bien Hola siguiendo la sintaxis toospecify varias colecciones: *collection_prefix*[inicio índice - índice final]. Al especificar varias colecciones a través de la sintaxis de hello mencionado anteriormente, tenga en cuenta los siguiente de hello:

1. Solo se admiten patrones de nombre de intervalo entero. Por ejemplo, especificar la colección [0-3] generará Hola después de colecciones: collection0, collection1, collection2, collection3.
2. Puede usar una sintaxis abreviada: colección[3] generará el mismo conjunto de colecciones que el paso 1.
3. Se pueden proporcionar varias sustituciones. Por ejemplo, colección[0-1] [0-9] 20 nombres de colección con ceros delante (colección01,... 02... 03).

Una vez hello nombres de colección se han especificado, elija rendimiento deseado de Hola de colecciones de hello (too10 de 400 RUs, 000 RUs). Para conseguir el mejor rendimiento en la importación, elija una mayor capacidad de proceso. Para más información sobre los niveles de rendimiento, consulte [Niveles de rendimiento en Azure Cosmos DB](performance-levels.md).

> [!NOTE]
> configuración de rendimiento de rendimiento de Hello solo aplica la creación de toocollection. Si Hola especifica la colección ya existe, su rendimiento no se modificarán.
> 
> 

Al importar toomultiple colecciones, herramienta de importación de hello admite el particionamiento de hash basado. En este escenario, especifique la propiedad de documento de hello desea toouse como Hola clave de partición (si la clave de partición se deja en blanco, documentos será particionados aleatoriamente en distintas colecciones de destino de hello).

También puede especificar qué campo de origen que se importarán Hola debe usarse como propiedad de identificador de documento de base de datos de Azure Cosmos Hola durante la importación de hello (tenga en cuenta que si los documentos no contienen esta propiedad, a continuación, herramienta de importación de hello generará un GUID como valor de propiedad de Id. de hello).

Hay una serie de opciones avanzadas disponibles durante la importación. En primer lugar, mientras que incluye la herramienta de hello una importación masiva de un valor predeterminado de procedimiento almacenado (BulkInsert.js), puede elegir toospecify su propio procedimiento almacenado de importación:

 ![Captura de pantalla de opciones de importación de insert sproc masiva de Azure Cosmos DB](./media/import-data/bulkinsertsp.png)

Además, al importar los tipos de fecha (por ejemplo, desde SQL Server o MongoDB), puede elegir entre tres opciones de importación:

 ![Captura de pantalla de opciones de importación de fecha y hora de Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* Cadena: conservar como un valor de cadena
* Tiempo: conservar como un valor de número de tiempo
* Ambos: conservar los valores de cadena y de número  Esta opción creará un subdocumento, por ejemplo "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }

Importador de Hello Azure Cosmos DB masiva dispone de opciones avanzadas adicionales siguientes de hello:

1. Tamaño de lote: Hola herramienta valores predeterminados tooa tamaño de lote de 50.  Si Hola documentos toobe importado es grande, considere la posibilidad de reducir el tamaño del lote de Hola. Por el contrario, si Hola documentos toobe importado es pequeño, considere la posibilidad de generar el tamaño de lote de Hola.
2. Tamaño máximo de la secuencia de comandos (bytes): herramienta de hello tiene como valor predeterminado el tamaño máximo de la secuencia de comandos de tooa de 512KB
3. Deshabilitar la generación automática de Id.: Si cada toobe documento importado contiene un campo id, a continuación, al seleccionar esta opción puede aumentar el rendimiento. No se importarán los documentos  que no contengan el campo de identificador exclusivo.
4. Documentos de actualización existente: Hola toonot de los valores predeterminados de herramienta reemplazando los documentos existentes con los conflictos de identificador. Si selecciona esta opción, permitirá que se sobrescriban los documentos existentes con identificadores que coinciden entre sí. Esta característica es útil para las migraciones de datos programadas que actualizan los documentos existentes.
5. Número de reintentos en caso de error: especifica Hola número de veces tooretry Hola conexión tooAzure Cosmos DB en caso de errores transitorios (por ejemplo, interrupción de conectividad de red).
6. Intervalo de reintentos: Especifica cuánto tiempo toowait entre los reintentos de conexión tooAzure DB Cosmos de hello en caso de errores transitorios (por ejemplo, interrupción de conectividad de red).
7. Modo de conexión: Especifica toouse de modo de conexión de hello con base de datos de Azure Cosmos. las opciones disponibles de Hello son DirectTcp, DirectHttps y puerta de enlace. modos de conexión directa de Hello son más rápidos, mientras que el modo de puerta de enlace de hello es firewall más descriptivo como solo usa el puerto 443.

![Captura de pantalla de opciones avanzadas de importación masiva de Azure Cosmos DB](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> modo de tooconnection de los valores predeterminados de herramienta DirectTcp de importación de Hola. Si experimenta problemas de firewall, cambie el modo de tooconnection puerta de enlace, ya que solo requiere el puerto 443.
> 
> 

## <a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API (secuencial en el registro de importación)
Importador de registro secuencial de base de datos de Azure Cosmos Hola permite tooimport desde cualquiera de las opciones de origen disponibles de hello en forma de registro por registro. Puede elegir esta opción si va a importar tooan colección existente que ha alcanzado su cuota de procedimientos almacenados. Hola herramienta admite la importación tooa única colección de base de datos de Azure Cosmos (única partición y varias particiones), así como importar particionada mediante el cual los datos se dividen en varias colecciones de base de datos de Azure Cosmos única partición o varias particiones. Para más información sobre la creación de particiones de datos, consulte [Partición y escalado de datos en Azure Cosmos DB](partition-data.md).

![Captura de pantalla de opciones de importación de registros secuenciales de Azure Cosmos DB](./media/import-data/documentdbsequential.png)

Hola formato de cadena de conexión de base de datos de Azure Cosmos hello es:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

cadena de conexión de cuenta de base de datos de Azure Cosmos Hola puede obtenerse de hoja de claves de Hola de hello portal de Azure, como se describe en [cómo toomanage una cuenta de base de datos de Azure Cosmos](manage-account.md); sin embargo, nombre de Hola de base de datos de hello debe toobe anexa toohello cadena de conexión en hello siguiendo el formato:

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> Puede tener acceso a la utilice Hola Compruebe comando tooensure que Hola instancia de base de datos de Azure Cosmos especificada en el campo de cadena de conexión de Hola.
> 
> 

tooimport tooa única colección, escriba nombre de Hola de hello colección toowhich datos se va a importar y haga clic en el botón de agregar Hola. tooimport toomultiple colecciones, escriba los nombres de colección individualmente o bien Hola siguiendo la sintaxis toospecify varias colecciones: *collection_prefix*[inicio índice - índice final]. Al especificar varias colecciones a través de la sintaxis de hello mencionado anteriormente, tenga en cuenta los siguiente de hello:

1. Solo se admiten patrones de nombre de intervalo entero. Por ejemplo, especificar la colección [0-3] generará Hola después de colecciones: collection0, collection1, collection2, collection3.
2. Puede usar una sintaxis abreviada: colección[3] generará el mismo conjunto de colecciones que el paso 1.
3. Se pueden proporcionar varias sustituciones. Por ejemplo, colección[0-1] [0-9] 20 nombres de colección con ceros delante (colección01,... 02... 03).

Una vez hello nombres de colección se han especificado, elija rendimiento deseado de Hola de colecciones de hello (too250 de 400 RUs, 000 RUs). Para conseguir el mejor rendimiento en la importación, elija una mayor capacidad de proceso. Para más información sobre los niveles de rendimiento, consulte [Niveles de rendimiento en Azure Cosmos DB](performance-levels.md). Toda importación toocollections con rendimiento > 10.000 RUs requerirá una clave de partición. Si elige más de 250.000 RUs toohave, deberá toofile una solicitud en toohave portal Hola aumenta su cuenta.

> [!NOTE]
> configuración de rendimiento de Hello solo aplica la creación de toocollection. Si Hola especifica la colección ya existe, su rendimiento no se modificarán.
> 
> 

Al importar toomultiple colecciones, herramienta de importación de hello admite el particionamiento de hash basado. En este escenario, especifique la propiedad de documento de hello desea toouse como Hola clave de partición (si la clave de partición se deja en blanco, documentos será particionados aleatoriamente en distintas colecciones de destino de hello).

También puede especificar qué campo de origen que se importarán Hola debe usarse como propiedad de identificador de documento de base de datos de Azure Cosmos Hola durante la importación de hello (tenga en cuenta que si los documentos no contienen esta propiedad, a continuación, herramienta de importación de hello generará un GUID como valor de propiedad de Id. de hello).

Hay una serie de opciones avanzadas disponibles durante la importación. En primer lugar, al importar los tipos de fecha (por ejemplo, desde SQL Server o MongoDB), puede elegir entre tres opciones de importación:

 ![Captura de pantalla de opciones de importación de fecha y hora de Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* Cadena: conservar como un valor de cadena
* Tiempo: conservar como un valor de número de tiempo
* Ambos: conservar los valores de cadena y de número  Esta opción creará un subdocumento, por ejemplo "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }

Hello Azure Cosmos DB - importador de registro secuencial dispone de opciones avanzadas adicionales siguientes de hello:

1. Número de solicitudes paralelas: herramienta de hello tiene como valor predeterminado de las solicitudes paralelas de too2. Si Hola documentos toobe importado es pequeño, considere la posibilidad de elevación Hola número de solicitudes paralelas. Tenga en cuenta que si este número se genera demasiado, Hola importación podría experimentar de limitación.
2. Deshabilitar la generación automática de Id.: Si cada toobe documento importado contiene un campo id, a continuación, al seleccionar esta opción puede aumentar el rendimiento. No se importarán los documentos  que no contengan el campo de identificador exclusivo.
3. Documentos de actualización existente: Hola toonot de los valores predeterminados de herramienta reemplazando los documentos existentes con los conflictos de identificador. Si selecciona esta opción, permitirá que se sobrescriban los documentos existentes con identificadores que coinciden entre sí. Esta característica es útil para las migraciones de datos programadas que actualizan los documentos existentes.
4. Número de reintentos en caso de error: especifica Hola número de veces tooretry Hola conexión tooAzure Cosmos DB en caso de errores transitorios (por ejemplo, interrupción de conectividad de red).
5. Intervalo de reintentos: Especifica cuánto tiempo toowait entre los reintentos de conexión tooAzure DB Cosmos de hello en caso de errores transitorios (por ejemplo, interrupción de conectividad de red).
6. Modo de conexión: Especifica toouse de modo de conexión de hello con base de datos de Azure Cosmos. las opciones disponibles de Hello son DirectTcp, DirectHttps y puerta de enlace. modos de conexión directa de Hello son más rápidos, mientras que el modo de puerta de enlace de hello es firewall más descriptivo como solo usa el puerto 443.

![Captura de pantalla de opciones avanzadas de importación de registros secuenciales de Azure Cosmos DB](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> modo de tooconnection de los valores predeterminados de herramienta DirectTcp de importación de Hola. Si experimenta problemas de firewall, cambie el modo de tooconnection puerta de enlace, ya que solo requiere el puerto 443.
> 
> 

## <a id="IndexingPolicy"></a>Especificar una directiva de indexación al crear colecciones de Azure Cosmos DB
Cuando se permite la migración de hello colecciones de toocreate herramienta durante la importación, puede especificar la directiva de indexación de Hola de colecciones de Hola. Hola avanzada de la sección de opciones de importación en bloque de base de datos de Azure Cosmos hello y secuencial de base de datos de Azure Cosmos opciones de registro, navegue toohello sección sobre la directiva de indización.

![Captura de pantalla de opciones avanzadas de política de indexación de Azure Cosmos DB](./media/import-data/indexingpolicy1.png)

Con hello opción de directiva de indización avanzada, puede seleccionar un archivo de directiva de indexación, manualmente especificar una directiva de indexación o seleccionar entre un conjunto de plantillas predeterminadas (haciendo clic en hello indización de cuadro de texto de directiva).

plantillas de directiva de Hola Hola herramienta proporciona son:

* Predeterminada. Esta directiva es mejor cuando se realizan consultas de igualdad en cadenas y se usan consultas ORDER BY, de rango y de igualdad para números. Esta directiva tiene una sobrecarga de almacenamiento de índices menor que la de intervalo.
* Intervalo. Esta directiva es mejor si está usando consultas de ORDER BY, intervalo e igualdad en números y cadenas. Esta directiva tiene una mayor sobrecarga de almacenamiento de índice que la Predeterminada o Hash.

![Captura de pantalla de opciones avanzadas de política de indexación de Azure Cosmos DB](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> Si no especifica una directiva de indexación, se aplicará la directiva predeterminada de Hola. Para más información sobre las directivas de indexación, consulte [Directivas de indexación de Azure Cosmos DB](indexing-policies.md).
> 
> 

## <a name="export-toojson-file"></a>Archivo de exportación tooJSON
exportador de JSON de base de datos de Azure Cosmos Hola permite tooexport cualquiera de hello origen disponibles opciones tooa archivo JSON que contiene una matriz de documentos JSON. herramienta Hola controlará la exportación de Hola para usted, o puede elegir el comando resultante de migración de tooview hello y ejecutar comando hello usted mismo. archivo JSON resultante de Hello puede almacenarse localmente o en el almacenamiento de blobs de Azure.

![Captura de pantalla de opción de exportación de archivo local JSON de Azure Cosmos DB](./media/import-data/jsontarget.png)

![Captura de pantalla de opción de exportación de Azure Blob Storage de JSON de Azure Cosmos DB](./media/import-data/jsontarget2.png)

También puede elegir hello tooprettify resultante JSON, lo que aumentará el tamaño de saludo del documento resultante de hello mientras lo Hola contenido más legibles.

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places toosee in Paris"}]}]

    Prettified JSON export
    [
     {
    "id": "Sample",
    "Title": "About Paris",
    "Language": {
      "Name": "English"
    },
    "Author": {
      "Name": "Don",
      "Location": {
        "City": "Paris",
        "Country": "France"
      }
    },
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places toosee in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a>Configuración avanzada
En la pantalla de configuración avanzada de bienvenida, especifique la ubicación de Hola de toowhich de archivo de registro de hello que desea que los errores que se escriben. Hola siguiendo las reglas aplica toothis página:

1. Si no se proporciona un nombre de archivo, se devolverán todos los errores en la página de resultados de Hola.
2. Si se proporciona un nombre de archivo sin un directorio, a continuación, archivo hello se crean (o sobrescribe) en el directorio actual de entorno de Hola.
3. Si selecciona una existente se sobrescribirán los archivos y, a continuación, archivo hello, no hay ninguna opción de anexar.

A continuación, elija si toolog todos los críticos, o ningún mensaje de error. Por último, decidir con qué frecuencia se actualizarán hello en el mensaje de transferencia de pantalla con su progreso.

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a>Confirmación de las opciones de importación y visualización de la línea de comandos
1. Después de especificar información de origen, la información de destino y la configuración avanzada, revise el resumen de la migración de Hola y, opcionalmente, ver o copiar Hola resultante comando migration (copia comando hello es útil tooautomate las operaciones de importación):
   
    ![Screenshot of summary screen](./media/import-data/summary.png)
   
    ![Screenshot of summary screen](./media/import-data/summarycommand.png)
2. Una vez que esté satisfecho con las opciones de origen y de destino, haga clic en **Importar**. tiempo transcurrido de Hello, recuento transferido e información del error (si no proporcionó un nombre de archivo de configuración avanzada de Hola) se actualizarán tal y como está en proceso de importación de Hola. Una vez completado, puede exportar resultados de hello (p. ej., toodeal con los errores de importación).
   
    ![Captura de pantalla de opción de exportación de JSON de Azure Cosmos DB](./media/import-data/viewresults.png)
3. También puede iniciar una nueva importación, conservando la configuración existente de hello (p. ej., elección de información de origen y de destino de la cadena de conexión, etc.) o restablecer todos los valores.
   
    ![Captura de pantalla de opción de exportación de JSON de Azure Cosmos DB](./media/import-data/newimport.png)

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha hecho siguiente de hello:

> [!div class="checklist"]
> * Instala la herramienta de migración de datos de Hola
> * Importación de datos de orígenes de datos diferentes
> * Exportar desde la base de datos de Azure Cosmos tooJSON

Ahora puede continuar el tutorial siguiente toohello y obtenga información acerca de cómo los datos de tooquery con la base de datos de Azure Cosmos. 

> [!div class="nextstepaction"]
>[¿Cómo tooquery datos?](../cosmos-db/tutorial-query-documentdb.md)
