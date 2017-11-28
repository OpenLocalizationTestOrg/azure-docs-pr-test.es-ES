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
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a><span data-ttu-id="15f98-105">¿Cómo tooimport datos en la base de datos de Azure Cosmos para Hola API de documentos?</span><span class="sxs-lookup"><span data-stu-id="15f98-105">How tooimport data into Azure Cosmos DB for hello DocumentDB API?</span></span>

<span data-ttu-id="15f98-106">Este tutorial proporciona instrucciones sobre cómo utilizar Hola base de datos de Azure Cosmos: herramienta de migración de datos de API de documentos, que puede importar datos de varios orígenes, incluidos los archivos JSON, CSV, archivos, SQL, MongoDB, almacenamiento de tabla de Azure, DynamoDB de Amazon y documentos de base de datos de Azure Cosmos Colecciones de API en colecciones para usan con hello API de documentos y la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="15f98-106">This tutorial provides instructions on using hello Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and hello DocumentDB API.</span></span> <span data-ttu-id="15f98-107">herramienta de migración de datos de Hello también puede usarse cuando se migra de una colección de varias particiones de una única partición colección tooa para hello API de documentos.</span><span class="sxs-lookup"><span data-stu-id="15f98-107">hello Data Migration tool can also be used when migrating from a single partition collection tooa multi-partition collection for hello DocumentDB API.</span></span>

<span data-ttu-id="15f98-108">herramienta de migración de datos de Hello solo funciona al importar datos en la base de datos de Azure Cosmos para usar con hello API de documentos.</span><span class="sxs-lookup"><span data-stu-id="15f98-108">hello Data Migration tool only works when importing data into Azure Cosmos DB for use with hello DocumentDB API.</span></span> <span data-ttu-id="15f98-109">En este momento no se admite la importación de datos para su uso con Hola API de tabla o la API Graph.</span><span class="sxs-lookup"><span data-stu-id="15f98-109">Importing data for use with hello Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="15f98-110">tooimport los datos para su uso con hello MongoDB API, consulte [base de datos de Azure Cosmos: cómo toomigrate datos de Hola MongoDB API?](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="15f98-110">tooimport data for use with hello MongoDB API, see [Azure Cosmos DB: How toomigrate data for hello MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="15f98-111">Este tutorial trata Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="15f98-111">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="15f98-112">Instalación de la herramienta de migración de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="15f98-112">Installing hello Data Migration tool</span></span>
> * <span data-ttu-id="15f98-113">Importación de datos de orígenes de datos diferentes</span><span class="sxs-lookup"><span data-stu-id="15f98-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="15f98-114">Exportar desde la base de datos de Azure Cosmos tooJSON</span><span class="sxs-lookup"><span data-stu-id="15f98-114">Exporting from Azure Cosmos DB tooJSON</span></span>

## <span data-ttu-id="15f98-115"><a id="Prerequisites"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="15f98-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="15f98-116">Antes de seguir las instrucciones de hello en este artículo, asegúrese de que tiene instalado el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="15f98-116">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="15f98-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) o superior.</span><span class="sxs-lookup"><span data-stu-id="15f98-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="15f98-118"><a id="Overviewl"></a>Información general sobre la herramienta de migración de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="15f98-118"><a id="Overviewl"></a>Overview of hello Data Migration tool</span></span>
<span data-ttu-id="15f98-119">herramienta de migración de datos de Hello es una solución de código abierto que importa datos tooAzure DB Cosmos desde una variedad de orígenes, incluidas:</span><span class="sxs-lookup"><span data-stu-id="15f98-119">hello Data Migration tool is an open source solution that imports data tooAzure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="15f98-120">Archivos JSON</span><span class="sxs-lookup"><span data-stu-id="15f98-120">JSON files</span></span>
* <span data-ttu-id="15f98-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="15f98-121">MongoDB</span></span>
* <span data-ttu-id="15f98-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="15f98-122">SQL Server</span></span>
* <span data-ttu-id="15f98-123">Archivos CSV</span><span class="sxs-lookup"><span data-stu-id="15f98-123">CSV files</span></span>
* <span data-ttu-id="15f98-124">Almacenamiento de tablas de Azure</span><span class="sxs-lookup"><span data-stu-id="15f98-124">Azure Table storage</span></span>
* <span data-ttu-id="15f98-125">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="15f98-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="15f98-126">HBase</span><span class="sxs-lookup"><span data-stu-id="15f98-126">HBase</span></span>
* <span data-ttu-id="15f98-127">Colecciones de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="15f98-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="15f98-128">Mientras que la herramienta de importación Hola incluye una interfaz gráfica de usuario (dtui.exe), también se puede controlar desde la línea de comandos de hello (dt.exe).</span><span class="sxs-lookup"><span data-stu-id="15f98-128">While hello import tool includes a graphical user interface (dtui.exe), it can also be driven from hello command line (dt.exe).</span></span> <span data-ttu-id="15f98-129">De hecho, hay un comando de opción toooutput Hola asociado después de configurar una importación a través de la interfaz de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-129">In fact, there is an option toooutput hello associated command after setting up an import through hello UI.</span></span> <span data-ttu-id="15f98-130">Se pueden transformar datos tabulares de origen (por ejemplo, archivos de SQL Server o CSV) de tal forma que se pueden crear relaciones jerárquicas (subdocumentos) durante la importación.</span><span class="sxs-lookup"><span data-stu-id="15f98-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="15f98-131">Siga leyendo toolearn más información sobre opciones de fuente, tooimport de líneas de comandos de ejemplo de cada origen, importación opciones de destino y ver los resultados.</span><span class="sxs-lookup"><span data-stu-id="15f98-131">Keep reading toolearn more about source options, sample command lines tooimport from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="15f98-132"><a id="Install"></a>Instalar la herramienta de migración de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="15f98-132"><a id="Install"></a>Install hello Data Migration tool</span></span>
<span data-ttu-id="15f98-133">código de fuente de herramienta de migración de Hello está disponible en GitHub en [este repositorio](https://github.com/azure/azure-documentdb-datamigrationtool) y está disponible en una versión compilada [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span><span class="sxs-lookup"><span data-stu-id="15f98-133">hello migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="15f98-134">Puede compilar la solución de Hola o simplemente descargar y extraer el directorio de tooa Hola versión compilada de su elección.</span><span class="sxs-lookup"><span data-stu-id="15f98-134">You may either compile hello solution or simply download and extract hello compiled version tooa directory of your choice.</span></span> <span data-ttu-id="15f98-135">A continuación, ejecute:</span><span class="sxs-lookup"><span data-stu-id="15f98-135">Then run either:</span></span>

* <span data-ttu-id="15f98-136">**Dtui.exe**: versión de interfaz gráfica de la herramienta de Hola</span><span class="sxs-lookup"><span data-stu-id="15f98-136">**Dtui.exe**: Graphical interface version of hello tool</span></span>
* <span data-ttu-id="15f98-137">**DT.exe**: versión de línea de comandos de herramienta de Hola</span><span class="sxs-lookup"><span data-stu-id="15f98-137">**Dt.exe**: Command-line version of hello tool</span></span>

## <a name="import-data"></a><span data-ttu-id="15f98-138">Importar datos</span><span class="sxs-lookup"><span data-stu-id="15f98-138">Import data</span></span>

<span data-ttu-id="15f98-139">Una vez haya instalado la herramienta de hello, es hora tooimport los datos.</span><span class="sxs-lookup"><span data-stu-id="15f98-139">Once you've installed hello tool, it's time tooimport your data.</span></span> <span data-ttu-id="15f98-140">¿Qué tipo de datos ¿desea tooimport?</span><span class="sxs-lookup"><span data-stu-id="15f98-140">What kind of data do you want tooimport?</span></span>

* [<span data-ttu-id="15f98-141">Archivos JSON</span><span class="sxs-lookup"><span data-stu-id="15f98-141">JSON files</span></span>](#JSON)
* [<span data-ttu-id="15f98-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="15f98-142">MongoDB</span></span>](#MongoDB)
* [<span data-ttu-id="15f98-143">Archivos de exportación de MongoDB</span><span class="sxs-lookup"><span data-stu-id="15f98-143">MongoDB Export files</span></span>](#MongoDBExport)
* [<span data-ttu-id="15f98-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="15f98-144">SQL Server</span></span>](#SQL)
* [<span data-ttu-id="15f98-145">Archivos CSV</span><span class="sxs-lookup"><span data-stu-id="15f98-145">CSV files</span></span>](#CSV)
* [<span data-ttu-id="15f98-146">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="15f98-146">Azure Table storage</span></span>](#AzureTableSource)
* [<span data-ttu-id="15f98-147">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="15f98-147">Amazon DynamoDB</span></span>](#DynamoDBSource)
* [<span data-ttu-id="15f98-148">Blob</span><span class="sxs-lookup"><span data-stu-id="15f98-148">Blob</span></span>](#BlobImport)
* [<span data-ttu-id="15f98-149">Colecciones de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="15f98-149">Azure Cosmos DB collections</span></span>](#DocumentDBSource)
* [<span data-ttu-id="15f98-150">HBase</span><span class="sxs-lookup"><span data-stu-id="15f98-150">HBase</span></span>](#HBaseSource)
* [<span data-ttu-id="15f98-151">Importación masiva de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="15f98-151">Azure Cosmos DB bulk import</span></span>](#DocumentDBBulkImport)
* [<span data-ttu-id="15f98-152">Importación de registros secuenciales de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="15f98-152">Azure Cosmos DB sequential record import</span></span>](#DocumentDSeqTarget)


## <span data-ttu-id="15f98-153"><a id="JSON"></a>archivos JSON tooimport</span><span class="sxs-lookup"><span data-stu-id="15f98-153"><a id="JSON"></a>tooimport JSON files</span></span>
<span data-ttu-id="15f98-154">opción de importador de origen de archivo JSON de Hello permite tooimport uno o más archivos JSON de único documento o archivos JSON que contienen una matriz de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="15f98-154">hello JSON file source importer option allows you tooimport one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="15f98-155">Al agregar las carpetas que contienen JSON archivos tooimport, tendrá posibilidad de Hola de búsqueda de archivos en subcarpetas de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="15f98-155">When adding folders that contain JSON files tooimport, you have hello option of recursively searching for files in subfolders.</span></span>

![Captura de pantalla de opciones de origen de archivos JSON: herramientas de migración de base de datos](./media/import-data/jsonsource.png)

<span data-ttu-id="15f98-157">Estos son algunos archivos JSON de tooimport de ejemplos de línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="15f98-157">Here are some command line samples tooimport JSON files:</span></span>

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

## <span data-ttu-id="15f98-158"><a id="MongoDB"></a>tooimport de MongoDB</span><span class="sxs-lookup"><span data-stu-id="15f98-158"><a id="MongoDB"></a>tooimport from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="15f98-159">Si va a importar la cuenta de base de datos de Azure Cosmos tooan con soporte para MongoDB, siga estas [instrucciones](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="15f98-159">If you are importing tooan Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="15f98-160">Hola opción de importador de código fuente de MongoDB permite tooimport de una colección de MongoDB individual y, opcionalmente, filtrar documentos mediante una consulta o modificar la estructura del documento hello mediante una proyección.</span><span class="sxs-lookup"><span data-stu-id="15f98-160">hello MongoDB source importer option allows you tooimport from an individual MongoDB collection and optionally filter documents using a query and/or modify hello document structure by using a projection.</span></span>  

![Captura de pantalla de las opciones de origen de MongoDB](./media/import-data/mongodbsource.png)

<span data-ttu-id="15f98-162">cadena de conexión de Hello está en formato de MongoDB estándar de hello:</span><span class="sxs-lookup"><span data-stu-id="15f98-162">hello connection string is in hello standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="15f98-163">Puede tener acceso a la utilice Hola Compruebe comando tooensure que Hola instancia MongoDB especificado en el campo de cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-163">Use hello Verify command tooensure that hello MongoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="15f98-164">Escriba el nombre de Hola de colección de Hola desde el que se importarán los datos.</span><span class="sxs-lookup"><span data-stu-id="15f98-164">Enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="15f98-165">Si lo desea, puede especificar o proporcionar un archivo para una consulta (por ejemplo, {pop: {$gt: 5000}}) o proyección (p. ej. {loc:0}) tooboth filtro y la forma Hola datos toobe importado.</span><span class="sxs-lookup"><span data-stu-id="15f98-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) tooboth filter and shape hello data toobe imported.</span></span>

<span data-ttu-id="15f98-166">Estos son algunos tooimport de ejemplos de línea de comandos de MongoDB:</span><span class="sxs-lookup"><span data-stu-id="15f98-166">Here are some command line samples tooimport from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="15f98-167"><a id="MongoDBExport"></a>archivos de exportación de MongoDB tooimport</span><span class="sxs-lookup"><span data-stu-id="15f98-167"><a id="MongoDBExport"></a>tooimport MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="15f98-168">Si va a importar la cuenta de base de datos de Azure Cosmos tooan con soporte para MongoDB, siga estas [instrucciones](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="15f98-168">If you are importing tooan Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="15f98-169">Hola opción importador de origen de archivo JSON de MongoDB exportación permite tooimport uno o más archivos JSON procedentes de la utilidad de mongoexport Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-169">hello MongoDB export JSON file source importer option allows you tooimport one or more JSON files produced from hello mongoexport utility.</span></span>  

![Captura de pantalla de las opciones de origen de exportación de MongoDB](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="15f98-171">Al agregar las carpetas que contienen archivos de JSON de exportación de MongoDB para la importación, se tiene la opción de Hola de búsqueda de archivos en subcarpetas de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="15f98-171">When adding folders that contain MongoDB export JSON files for import, you have hello option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="15f98-172">Este es un tooimport de ejemplo de línea de comandos de la exportación de MongoDB archivos JSON:</span><span class="sxs-lookup"><span data-stu-id="15f98-172">Here is a command line sample tooimport from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="15f98-173"><a id="SQL"></a>tooimport de SQL Server</span><span class="sxs-lookup"><span data-stu-id="15f98-173"><a id="SQL"></a>tooimport from SQL Server</span></span>
<span data-ttu-id="15f98-174">Hola opción de importador de código fuente SQL permite tooimport desde una base de datos de SQL Server individual y, opcionalmente, filtrar Hola registros toobe importar utilizando una consulta.</span><span class="sxs-lookup"><span data-stu-id="15f98-174">hello SQL source importer option allows you tooimport from an individual SQL Server database and optionally filter hello records toobe imported using a query.</span></span> <span data-ttu-id="15f98-175">Además, puede modificar la estructura del documento Hola especificando un separador de anidamiento (más en un momento).</span><span class="sxs-lookup"><span data-stu-id="15f98-175">In addition, you can modify hello document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![Captura de pantalla de opciones de origen de SQL: herramientas de migración de base de datos](./media/import-data/sqlexportsource.png)

<span data-ttu-id="15f98-177">Hola formato de cadena de conexión de hello es Hola estándar SQL conexión cadena.</span><span class="sxs-lookup"><span data-stu-id="15f98-177">hello format of hello connection string is hello standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="15f98-178">Puede tener acceso a la utilice Hola Compruebe comando tooensure que Hola la instancia de SQL Server especificada en el campo de cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-178">Use hello Verify command tooensure that hello SQL Server instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="15f98-179">Hola anidar la propiedad separator es toocreate usa las relaciones jerárquicas (documentos secundarios) durante la importación.</span><span class="sxs-lookup"><span data-stu-id="15f98-179">hello nesting separator property is used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="15f98-180">Considere la posibilidad de hello después de la consulta SQL:</span><span class="sxs-lookup"><span data-stu-id="15f98-180">Consider hello following SQL query:</span></span>

<span data-ttu-id="15f98-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as Address.AddressType, AddressLine1 as Address.AddressLine1, City as Address.Location.City, StateProvinceName as Address.Location.StateProvinceName, PostalCode as Address.PostalCode, CountryRegionName as Address.CountryRegionName from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span><span class="sxs-lookup"><span data-stu-id="15f98-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="15f98-182">Que devuelve Hola después de resultados (parciales):</span><span class="sxs-lookup"><span data-stu-id="15f98-182">Which returns hello following (partial) results:</span></span>

![Screenshot of SQL query results](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="15f98-184">Tenga en cuenta los alias de hello como Address.AddressType y Address.Location.StateProvinceName.</span><span class="sxs-lookup"><span data-stu-id="15f98-184">Note hello aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="15f98-185">Mediante la especificación de un separador de anidamiento de '.', la herramienta de importación Hola crea dirección e importación de subdocumentos Address.Location durante Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-185">By specifying a nesting separator of ‘.’, hello import tool creates Address and Address.Location subdocuments during hello import.</span></span> <span data-ttu-id="15f98-186">Este es un ejemplo de un documento resultante en Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="15f98-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="15f98-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span><span class="sxs-lookup"><span data-stu-id="15f98-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="15f98-188">Estos son algunos tooimport de ejemplos de línea de comandos de SQL Server:</span><span class="sxs-lookup"><span data-stu-id="15f98-188">Here are some command line samples tooimport from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="15f98-189"><a id="CSV"></a>archivos CSV de tooimport y convertir CSV tooJSON</span><span class="sxs-lookup"><span data-stu-id="15f98-189"><a id="CSV"></a>tooimport CSV files and convert CSV tooJSON</span></span>
<span data-ttu-id="15f98-190">Hola opción de importador de origen de archivo CSV permite tooimport uno o varios archivos CSV.</span><span class="sxs-lookup"><span data-stu-id="15f98-190">hello CSV file source importer option enables you tooimport one or more CSV files.</span></span> <span data-ttu-id="15f98-191">Al agregar las carpetas que contienen archivos CSV para la importación, se tiene la opción de Hola de búsqueda de archivos en subcarpetas de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="15f98-191">When adding folders that contain CSV files for import, you have hello option of recursively searching for files in subfolders.</span></span>

![Opciones de origen de la captura de pantalla de CSV - CSV tooJSON](media/import-data/csvsource.png)

<span data-ttu-id="15f98-193">Origen SQL de toohello similar, Hola anidar la propiedad separator puede ser toocreate usa las relaciones jerárquicas (documentos secundarios) durante la importación.</span><span class="sxs-lookup"><span data-stu-id="15f98-193">Similar toohello SQL source, hello nesting separator property may be used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="15f98-194">Considere la posibilidad de hello después de la fila de encabezado CSV y filas de datos:</span><span class="sxs-lookup"><span data-stu-id="15f98-194">Consider hello following CSV header row and data rows:</span></span>

![Registros de captura de pantalla de CSV de ejemplo - CSV tooJSON](./media/import-data/csvsample.png)

<span data-ttu-id="15f98-196">Tenga en cuenta los alias de hello como DomainInfo.Domain_Name y RedirectInfo.Redirecting.</span><span class="sxs-lookup"><span data-stu-id="15f98-196">Note hello aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="15f98-197">Mediante la especificación de un separador de anidamiento de '.', la herramienta de importación Hola creará DomainInfo e importación de subdocumentos RedirectInfo durante Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-197">By specifying a nesting separator of ‘.’, hello import tool will create DomainInfo and RedirectInfo subdocuments during hello import.</span></span> <span data-ttu-id="15f98-198">Este es un ejemplo de un documento resultante en Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="15f98-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="15f98-199">*{"DomainInfo": {"Nombre_de_dominio": "ACUS.GOV", "Domain_Name_Address": "http://www. ACUS.GOV"},"Agencia Federal":"Conferencia administrativa de Estados Unidos de hello","RedirectInfo": {"Redirigir":"0","Redirect_Destination":" "},"id":"9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d"}*</span><span class="sxs-lookup"><span data-stu-id="15f98-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of hello United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="15f98-200">herramienta de importación de Hello tratará de información de tipo de tooinfer de valores sin comillas en archivos CSV (valores entre comillas siempre se tratan como cadenas).</span><span class="sxs-lookup"><span data-stu-id="15f98-200">hello import tool will attempt tooinfer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="15f98-201">Los tipos se identifican en hello siguiendo el orden: número, fecha y hora, un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="15f98-201">Types are identified in hello following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="15f98-202">Hay dos otro toonote cosas sobre la importación de CSV:</span><span class="sxs-lookup"><span data-stu-id="15f98-202">There are two other things toonote about CSV import:</span></span>

1. <span data-ttu-id="15f98-203">De forma predeterminada, los valores sin comillas se recortan siempre en tabuladores y espacios, mientras que los valores entre comillas se mantienen como son.</span><span class="sxs-lookup"><span data-stu-id="15f98-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="15f98-204">Este comportamiento puede invalidarse con opción de línea de comandos de /s.TrimQuoted de casilla de verificación o hello valores entre comillas el recorte de hello.</span><span class="sxs-lookup"><span data-stu-id="15f98-204">This behavior can be overridden with hello Trim quoted values checkbox or hello /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="15f98-205">De forma predeterminada, un valor null sin comillas se trata como un valor null.</span><span class="sxs-lookup"><span data-stu-id="15f98-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="15f98-206">Este comportamiento puede invalidarse (es decir, tratar una opción null sin comillas como una cadena "null") con hello Treat sin comillas NULL como opción de línea de comandos de /s.NoUnquotedNulls de casilla de verificación o hello cadena.</span><span class="sxs-lookup"><span data-stu-id="15f98-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with hello Treat unquoted NULL as string checkbox or hello /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="15f98-207">Este es un ejemplo de línea de comandos para la importación CSV:</span><span class="sxs-lookup"><span data-stu-id="15f98-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="15f98-208"><a id="AzureTableSource"></a>tooimport desde el almacenamiento de tabla de Azure</span><span class="sxs-lookup"><span data-stu-id="15f98-208"><a id="AzureTableSource"></a>tooimport from Azure Table storage</span></span>
<span data-ttu-id="15f98-209">Hola opción de importador de origen de almacenamiento de tabla de Azure permite tooimport desde una tabla de almacenamiento de Azure tabla individual y, opcionalmente, filtrar Hola tabla entidades toobe importado.</span><span class="sxs-lookup"><span data-stu-id="15f98-209">hello Azure Table storage source importer option allows you tooimport from an individual Azure Table storage table and optionally filter hello table entities toobe imported.</span></span> <span data-ttu-id="15f98-210">Tenga en cuenta que no puede usar datos de almacenamiento de tabla de Azure de tooimport herramienta de migración de datos de hello en la base de datos de Azure Cosmos para su uso con hello API de tabla.</span><span class="sxs-lookup"><span data-stu-id="15f98-210">Note that you cannot use hello Data Migration tool tooimport Azure Table storage data into Azure Cosmos DB for use with hello Table API.</span></span> <span data-ttu-id="15f98-211">Se admite la importación sólo tooAzure DB Cosmos para su uso con hello API de documentos en este momento.</span><span class="sxs-lookup"><span data-stu-id="15f98-211">Only importing tooAzure Cosmos DB for use with hello DocumentDB API is supported at this time.</span></span>

![Screenshot of Azure Table storage source options](./media/import-data/azuretablesource.png)

<span data-ttu-id="15f98-213">formato de Hola de hello cadena de conexión de almacenamiento de tabla de Azure es:</span><span class="sxs-lookup"><span data-stu-id="15f98-213">hello format of hello Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="15f98-214">Puede tener acceso a la utilice Hola Compruebe comando tooensure que Hola instancia de almacenamiento de tabla de Azure especificada en el campo de cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-214">Use hello Verify command tooensure that hello Azure Table storage instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="15f98-215">Escriba el nombre de Hola de hello Azure desde el que se importarán los datos de tabla.</span><span class="sxs-lookup"><span data-stu-id="15f98-215">Enter hello name of hello Azure table from which data will be imported.</span></span> <span data-ttu-id="15f98-216">Opcionalmente, puede especificar un [filtro](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span><span class="sxs-lookup"><span data-stu-id="15f98-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="15f98-217">Hola opción de importador de origen de almacenamiento de tabla de Azure consta de las siguientes opciones adicionales de hello:</span><span class="sxs-lookup"><span data-stu-id="15f98-217">hello Azure Table storage source importer option has hello following additional options:</span></span>

1. <span data-ttu-id="15f98-218">Incluir campos internos</span><span class="sxs-lookup"><span data-stu-id="15f98-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="15f98-219">All: incluir todos los campos internos (PartitionKey, RowKey y Timestamp)</span><span class="sxs-lookup"><span data-stu-id="15f98-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="15f98-220">None: excluir todos los campos internos</span><span class="sxs-lookup"><span data-stu-id="15f98-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="15f98-221">RowKey - sólo incluyen campos de hello RowKey</span><span class="sxs-lookup"><span data-stu-id="15f98-221">RowKey - Only include hello RowKey field</span></span>
2. <span data-ttu-id="15f98-222">Seleccionar columnas</span><span class="sxs-lookup"><span data-stu-id="15f98-222">Select Columns</span></span>
   1. <span data-ttu-id="15f98-223">Los filtros de almacenamiento de tablas de Azure no admiten proyecciones.</span><span class="sxs-lookup"><span data-stu-id="15f98-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="15f98-224">Si desea tooonly importar propiedades de entidad de tabla de Azure específicas, agregarlos lista Seleccionar columnas de toohello.</span><span class="sxs-lookup"><span data-stu-id="15f98-224">If you want tooonly import specific Azure Table entity properties, add them toohello Select Columns list.</span></span> <span data-ttu-id="15f98-225">Se omitirán todas las demás propiedades de la entidad.</span><span class="sxs-lookup"><span data-stu-id="15f98-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="15f98-226">Este es un tooimport de ejemplo de línea de comandos desde el almacenamiento de tabla de Azure:</span><span class="sxs-lookup"><span data-stu-id="15f98-226">Here is a command line sample tooimport from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="15f98-227"><a id="DynamoDBSource"></a>tooimport de DynamoDB de Amazon</span><span class="sxs-lookup"><span data-stu-id="15f98-227"><a id="DynamoDBSource"></a>tooimport from Amazon DynamoDB</span></span>
<span data-ttu-id="15f98-228">Hola opción de importador de código fuente de Amazon DynamoDB permite tooimport desde una tabla de Amazon DynamoDB individual y, opcionalmente, filtrar Hola entidades toobe importado.</span><span class="sxs-lookup"><span data-stu-id="15f98-228">hello Amazon DynamoDB source importer option allows you tooimport from an individual Amazon DynamoDB table and optionally filter hello entities toobe imported.</span></span> <span data-ttu-id="15f98-229">Se proporcionan varias plantillas para que configurar una importación resulte lo más fácil posible.</span><span class="sxs-lookup"><span data-stu-id="15f98-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Captura de pantalla de opciones de origen de Amazon DynamoD: herramientas de migración de base de datos](./media/import-data/dynamodbsource1.png)

![Captura de pantalla de opciones de origen de Amazon DynamoD: herramientas de migración de base de datos](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="15f98-232">Hola formato de cadena de conexión de Amazon DynamoDB hello es:</span><span class="sxs-lookup"><span data-stu-id="15f98-232">hello format of hello Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="15f98-233">Puede tener acceso a la utilice Hola Compruebe comando tooensure que Hola instancia Amazon DynamoDB especificado en el campo de cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-233">Use hello Verify command tooensure that hello Amazon DynamoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="15f98-234">Este es un tooimport de ejemplo de línea de comandos de Amazon DynamoDB:</span><span class="sxs-lookup"><span data-stu-id="15f98-234">Here is a command line sample tooimport from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="15f98-235"><a id="BlobImport"></a>archivos de tooimport desde el almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="15f98-235"><a id="BlobImport"></a>tooimport files from Azure Blob storage</span></span>
<span data-ttu-id="15f98-236">Hello archivo JSON, archivo de exportación de MongoDB y las opciones de importador de origen de archivo CSV le permiten tooimport uno o más archivos de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="15f98-236">hello JSON file, MongoDB export file, and CSV file source importer options allow you tooimport one or more files from Azure Blob storage.</span></span> <span data-ttu-id="15f98-237">Después de especificar una dirección URL del contenedor de Blob y la clave de cuenta, basta con proporcionar un tooimport de los archivos de expresión regular tooselect Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-237">After specifying a Blob container URL and Account Key, simply provide a regular expression tooselect hello file(s) tooimport.</span></span>

![Captura de pantalla de opciones de origen de archivos Blob](./media/import-data/blobsource.png)

<span data-ttu-id="15f98-239">Aquí es archivos JSON de tooimport de ejemplo de línea de comandos desde el almacenamiento de blobs de Azure:</span><span class="sxs-lookup"><span data-stu-id="15f98-239">Here is command line sample tooimport JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="15f98-240"><a id="DocumentDBSource"></a>tooimport de una colección de API de documentos de base de datos de Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="15f98-240"><a id="DocumentDBSource"></a>tooimport from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="15f98-241">Hola opción de importador de código fuente de base de datos de Azure Cosmos permite tooimport datos de una o varias recopilaciones de base de datos de Azure Cosmos y, opcionalmente, filtrar documentos mediante una consulta.</span><span class="sxs-lookup"><span data-stu-id="15f98-241">hello Azure Cosmos DB source importer option allows you tooimport data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Captura de pantalla de opciones de origen de Azure Cosmos DB](./media/import-data/documentdbsource.png)

<span data-ttu-id="15f98-243">Hola formato de cadena de conexión de base de datos de Azure Cosmos hello es:</span><span class="sxs-lookup"><span data-stu-id="15f98-243">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="15f98-244">cadena de conexión de cuenta de base de datos de Azure Cosmos Hola puede obtenerse de hoja de claves de Hola de hello portal de Azure, como se describe en [cómo toomanage una cuenta de base de datos de Azure Cosmos](manage-account.md); sin embargo, nombre de Hola de base de datos de hello debe toobe anexa toohello cadena de conexión en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="15f98-244">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="15f98-245">Puede tener acceso a la utilice Hola Compruebe comando tooensure que Hola instancia de base de datos de Azure Cosmos especificada en el campo de cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-245">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="15f98-246">tooimport desde una sola colección de base de datos de Azure Cosmos, escriba nombre de Hola de colección de Hola desde el que se importarán los datos.</span><span class="sxs-lookup"><span data-stu-id="15f98-246">tooimport from a single Azure Cosmos DB collection, enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="15f98-247">tooimport de varias colecciones de base de datos de Azure Cosmos, proporcionar una expresión regular toomatch uno o más nombres de colección (por ejemplo, collection01 | collection02 | collection03).</span><span class="sxs-lookup"><span data-stu-id="15f98-247">tooimport from multiple Azure Cosmos DB collections, provide a regular expression toomatch one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="15f98-248">Opcionalmente, se pueden especificar, o proporcionar un archivo para un filtro de consulta tooboth y Hola datos toobe importar de forma.</span><span class="sxs-lookup"><span data-stu-id="15f98-248">You may optionally specify, or provide a file for, a query tooboth filter and shape hello data toobe imported.</span></span>

> [!NOTE]
> <span data-ttu-id="15f98-249">Puesto que el campo de la colección de hello acepta expresiones regulares, si va a importar desde una sola colección cuyo nombre contiene caracteres de expresión regular, los caracteres deben convertirse en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="15f98-249">Since hello collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="15f98-250">Hola opción de base de datos de Azure Cosmos origen importador tiene siguientes Hola opciones avanzadas:</span><span class="sxs-lookup"><span data-stu-id="15f98-250">hello Azure Cosmos DB source importer option has hello following advanced options:</span></span>

1. <span data-ttu-id="15f98-251">Incluir campos internos: Especifica si se permite o no tooinclude las propiedades del sistema de documento de base de datos de Azure Cosmos Hola exportación (por ejemplo, _rid, _ts).</span><span class="sxs-lookup"><span data-stu-id="15f98-251">Include Internal Fields: Specifies whether or not tooinclude Azure Cosmos DB document system properties in hello export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="15f98-252">Número de reintentos en caso de error: especifica Hola número de veces tooretry Hola conexión tooAzure Cosmos DB en caso de errores transitorios (por ejemplo, interrupción de conectividad de red).</span><span class="sxs-lookup"><span data-stu-id="15f98-252">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="15f98-253">Intervalo de reintentos: Especifica cuánto tiempo toowait entre los reintentos de conexión tooAzure DB Cosmos de hello en caso de errores transitorios (por ejemplo, interrupción de conectividad de red).</span><span class="sxs-lookup"><span data-stu-id="15f98-253">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="15f98-254">Modo de conexión: Especifica toouse de modo de conexión de hello con base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="15f98-254">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="15f98-255">las opciones disponibles de Hello son DirectTcp, DirectHttps y puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="15f98-255">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="15f98-256">modos de conexión directa de Hello son más rápidos, mientras que el modo de puerta de enlace de hello es firewall más descriptivo como solo usa el puerto 443.</span><span class="sxs-lookup"><span data-stu-id="15f98-256">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Captura de pantalla de opciones avanzadas de origen de Azure Cosmos DB](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="15f98-258">modo de tooconnection de los valores predeterminados de herramienta DirectTcp de importación de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-258">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="15f98-259">Si experimenta problemas de firewall, cambie el modo de tooconnection puerta de enlace, ya que solo requiere el puerto 443.</span><span class="sxs-lookup"><span data-stu-id="15f98-259">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="15f98-260">Estos son algunos tooimport de ejemplos de línea de comandos de base de datos de Azure Cosmos:</span><span class="sxs-lookup"><span data-stu-id="15f98-260">Here are some command line samples tooimport from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="15f98-261">Herramienta de importación de datos de Azure Cosmos DB Hello también admite la importación de datos de hello [emulador de base de datos de Azure Cosmos](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="15f98-261">hello Azure Cosmos DB Data Import Tool also supports import of data from hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="15f98-262">Al importar datos desde un emulador local, establezca el punto de conexión de hello demasiado`https://localhost:<port>`.</span><span class="sxs-lookup"><span data-stu-id="15f98-262">When importing data from a local emulator, set hello endpoint too`https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="15f98-263"><a id="HBaseSource"></a>tooimport de HBase</span><span class="sxs-lookup"><span data-stu-id="15f98-263"><a id="HBaseSource"></a>tooimport from HBase</span></span>
<span data-ttu-id="15f98-264">Hola opción de importador de código fuente de HBase permite tooimport datos de una tabla HBase y, opcionalmente, filtrar datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-264">hello HBase source importer option allows you tooimport data from an HBase table and optionally filter hello data.</span></span> <span data-ttu-id="15f98-265">Se proporcionan varias plantillas para que configurar una importación resulte lo más fácil posible.</span><span class="sxs-lookup"><span data-stu-id="15f98-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Captura de pantalla de opciones de origen de HBase](./media/import-data/hbasesource1.png)

![Captura de pantalla de opciones de origen de HBase](./media/import-data/hbasesource2.png)

<span data-ttu-id="15f98-268">Hola formato de cadena de conexión de HBase Stargate hello es:</span><span class="sxs-lookup"><span data-stu-id="15f98-268">hello format of hello HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="15f98-269">Puede tener acceso a la utilice Hola Compruebe comando tooensure que Hola instancia HBase especificado en el campo de cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-269">Use hello Verify command tooensure that hello HBase instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="15f98-270">Este es un tooimport de ejemplo de línea de comandos de HBase:</span><span class="sxs-lookup"><span data-stu-id="15f98-270">Here is a command line sample tooimport from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="15f98-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API (importación masiva)</span><span class="sxs-lookup"><span data-stu-id="15f98-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="15f98-272">Importador de Hello Azure Cosmos DB masiva permite tooimport desde cualquiera de las opciones de origen disponible hello, utilizando un procedimiento de base de datos de Azure Cosmos almacenados para mejorar la eficacia.</span><span class="sxs-lookup"><span data-stu-id="15f98-272">hello Azure Cosmos DB Bulk importer allows you tooimport from any of hello available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="15f98-273">herramienta de Hello es compatible con la colección de base de datos de Azure Cosmos particiones único de importación tooone, así como importar particionada mediante el cual los datos se dividen en varias colecciones de base de datos de Azure Cosmos particiones único.</span><span class="sxs-lookup"><span data-stu-id="15f98-273">hello tool supports import tooone single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="15f98-274">Para más información sobre la creación de particiones de datos, consulte [Partición y escalado de datos en Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="15f98-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="15f98-275">herramienta de Hello crear, ejecutar y, a continuación, elimine el procedimiento almacenado de Hola de las colecciones de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-275">hello tool will create, execute, and then delete hello stored procedure from hello target collection(s).</span></span>  

![Captura de pantalla de opciones de importación masiva de Azure Cosmos DB](./media/import-data/documentdbbulk.png)

<span data-ttu-id="15f98-277">Hola formato de cadena de conexión de base de datos de Azure Cosmos hello es:</span><span class="sxs-lookup"><span data-stu-id="15f98-277">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="15f98-278">cadena de conexión de cuenta de base de datos de Azure Cosmos Hola puede obtenerse de hoja de claves de Hola de hello portal de Azure, como se describe en [cómo toomanage una cuenta de base de datos de Azure Cosmos](manage-account.md); sin embargo, nombre de Hola de base de datos de hello debe toobe anexa toohello cadena de conexión en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="15f98-278">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="15f98-279">Puede tener acceso a la utilice Hola Compruebe comando tooensure que Hola instancia de base de datos de Azure Cosmos especificada en el campo de cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-279">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="15f98-280">tooimport tooa única colección, escriba nombre de Hola de hello colección toowhich datos se va a importar y haga clic en el botón de agregar Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-280">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="15f98-281">tooimport toomultiple colecciones, escriba los nombres de colección individualmente o bien Hola siguiendo la sintaxis toospecify varias colecciones: *collection_prefix*[inicio índice - índice final].</span><span class="sxs-lookup"><span data-stu-id="15f98-281">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="15f98-282">Al especificar varias colecciones a través de la sintaxis de hello mencionado anteriormente, tenga en cuenta los siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="15f98-282">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="15f98-283">Solo se admiten patrones de nombre de intervalo entero.</span><span class="sxs-lookup"><span data-stu-id="15f98-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="15f98-284">Por ejemplo, especificar la colección [0-3] generará Hola después de colecciones: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="15f98-284">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="15f98-285">Puede usar una sintaxis abreviada: colección[3] generará el mismo conjunto de colecciones que el paso 1.</span><span class="sxs-lookup"><span data-stu-id="15f98-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="15f98-286">Se pueden proporcionar varias sustituciones.</span><span class="sxs-lookup"><span data-stu-id="15f98-286">More than one substitution can be provided.</span></span> <span data-ttu-id="15f98-287">Por ejemplo, colección[0-1] [0-9] 20 nombres de colección con ceros delante (colección01,... 02... 03).</span><span class="sxs-lookup"><span data-stu-id="15f98-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="15f98-288">Una vez hello nombres de colección se han especificado, elija rendimiento deseado de Hola de colecciones de hello (too10 de 400 RUs, 000 RUs).</span><span class="sxs-lookup"><span data-stu-id="15f98-288">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too10,000 RUs).</span></span> <span data-ttu-id="15f98-289">Para conseguir el mejor rendimiento en la importación, elija una mayor capacidad de proceso.</span><span class="sxs-lookup"><span data-stu-id="15f98-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="15f98-290">Para más información sobre los niveles de rendimiento, consulte [Niveles de rendimiento en Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="15f98-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="15f98-291">configuración de rendimiento de rendimiento de Hello solo aplica la creación de toocollection.</span><span class="sxs-lookup"><span data-stu-id="15f98-291">hello performance throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="15f98-292">Si Hola especifica la colección ya existe, su rendimiento no se modificarán.</span><span class="sxs-lookup"><span data-stu-id="15f98-292">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="15f98-293">Al importar toomultiple colecciones, herramienta de importación de hello admite el particionamiento de hash basado.</span><span class="sxs-lookup"><span data-stu-id="15f98-293">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="15f98-294">En este escenario, especifique la propiedad de documento de hello desea toouse como Hola clave de partición (si la clave de partición se deja en blanco, documentos será particionados aleatoriamente en distintas colecciones de destino de hello).</span><span class="sxs-lookup"><span data-stu-id="15f98-294">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="15f98-295">También puede especificar qué campo de origen que se importarán Hola debe usarse como propiedad de identificador de documento de base de datos de Azure Cosmos Hola durante la importación de hello (tenga en cuenta que si los documentos no contienen esta propiedad, a continuación, herramienta de importación de hello generará un GUID como valor de propiedad de Id. de hello).</span><span class="sxs-lookup"><span data-stu-id="15f98-295">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="15f98-296">Hay una serie de opciones avanzadas disponibles durante la importación.</span><span class="sxs-lookup"><span data-stu-id="15f98-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="15f98-297">En primer lugar, mientras que incluye la herramienta de hello una importación masiva de un valor predeterminado de procedimiento almacenado (BulkInsert.js), puede elegir toospecify su propio procedimiento almacenado de importación:</span><span class="sxs-lookup"><span data-stu-id="15f98-297">First, while hello tool includes a default bulk import stored procedure (BulkInsert.js), you may choose toospecify your own import stored procedure:</span></span>

 ![Captura de pantalla de opciones de importación de insert sproc masiva de Azure Cosmos DB](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="15f98-299">Además, al importar los tipos de fecha (por ejemplo, desde SQL Server o MongoDB), puede elegir entre tres opciones de importación:</span><span class="sxs-lookup"><span data-stu-id="15f98-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Captura de pantalla de opciones de importación de fecha y hora de Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="15f98-301">Cadena: conservar como un valor de cadena</span><span class="sxs-lookup"><span data-stu-id="15f98-301">String: Persist as a string value</span></span>
* <span data-ttu-id="15f98-302">Tiempo: conservar como un valor de número de tiempo</span><span class="sxs-lookup"><span data-stu-id="15f98-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="15f98-303">Ambos: conservar los valores de cadena y de número </span><span class="sxs-lookup"><span data-stu-id="15f98-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="15f98-304">Esta opción creará un subdocumento, por ejemplo "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="15f98-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="15f98-305">Importador de Hello Azure Cosmos DB masiva dispone de opciones avanzadas adicionales siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="15f98-305">hello Azure Cosmos DB Bulk importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="15f98-306">Tamaño de lote: Hola herramienta valores predeterminados tooa tamaño de lote de 50.</span><span class="sxs-lookup"><span data-stu-id="15f98-306">Batch Size: hello tool defaults tooa batch size of 50.</span></span>  <span data-ttu-id="15f98-307">Si Hola documentos toobe importado es grande, considere la posibilidad de reducir el tamaño del lote de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-307">If hello documents toobe imported are large, consider lowering hello batch size.</span></span> <span data-ttu-id="15f98-308">Por el contrario, si Hola documentos toobe importado es pequeño, considere la posibilidad de generar el tamaño de lote de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-308">Conversely, if hello documents toobe imported are small, consider raising hello batch size.</span></span>
2. <span data-ttu-id="15f98-309">Tamaño máximo de la secuencia de comandos (bytes): herramienta de hello tiene como valor predeterminado el tamaño máximo de la secuencia de comandos de tooa de 512KB</span><span class="sxs-lookup"><span data-stu-id="15f98-309">Max Script Size (bytes): hello tool defaults tooa max script size of 512KB</span></span>
3. <span data-ttu-id="15f98-310">Deshabilitar la generación automática de Id.: Si cada toobe documento importado contiene un campo id, a continuación, al seleccionar esta opción puede aumentar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="15f98-310">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="15f98-311">No se importarán los documentos  que no contengan el campo de identificador exclusivo.</span><span class="sxs-lookup"><span data-stu-id="15f98-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="15f98-312">Documentos de actualización existente: Hola toonot de los valores predeterminados de herramienta reemplazando los documentos existentes con los conflictos de identificador.</span><span class="sxs-lookup"><span data-stu-id="15f98-312">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="15f98-313">Si selecciona esta opción, permitirá que se sobrescriban los documentos existentes con identificadores que coinciden entre sí.</span><span class="sxs-lookup"><span data-stu-id="15f98-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="15f98-314">Esta característica es útil para las migraciones de datos programadas que actualizan los documentos existentes.</span><span class="sxs-lookup"><span data-stu-id="15f98-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="15f98-315">Número de reintentos en caso de error: especifica Hola número de veces tooretry Hola conexión tooAzure Cosmos DB en caso de errores transitorios (por ejemplo, interrupción de conectividad de red).</span><span class="sxs-lookup"><span data-stu-id="15f98-315">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="15f98-316">Intervalo de reintentos: Especifica cuánto tiempo toowait entre los reintentos de conexión tooAzure DB Cosmos de hello en caso de errores transitorios (por ejemplo, interrupción de conectividad de red).</span><span class="sxs-lookup"><span data-stu-id="15f98-316">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="15f98-317">Modo de conexión: Especifica toouse de modo de conexión de hello con base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="15f98-317">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="15f98-318">las opciones disponibles de Hello son DirectTcp, DirectHttps y puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="15f98-318">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="15f98-319">modos de conexión directa de Hello son más rápidos, mientras que el modo de puerta de enlace de hello es firewall más descriptivo como solo usa el puerto 443.</span><span class="sxs-lookup"><span data-stu-id="15f98-319">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Captura de pantalla de opciones avanzadas de importación masiva de Azure Cosmos DB](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="15f98-321">modo de tooconnection de los valores predeterminados de herramienta DirectTcp de importación de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-321">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="15f98-322">Si experimenta problemas de firewall, cambie el modo de tooconnection puerta de enlace, ya que solo requiere el puerto 443.</span><span class="sxs-lookup"><span data-stu-id="15f98-322">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="15f98-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API (secuencial en el registro de importación)</span><span class="sxs-lookup"><span data-stu-id="15f98-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="15f98-324">Importador de registro secuencial de base de datos de Azure Cosmos Hola permite tooimport desde cualquiera de las opciones de origen disponibles de hello en forma de registro por registro.</span><span class="sxs-lookup"><span data-stu-id="15f98-324">hello Azure Cosmos DB sequential record importer allows you tooimport from any of hello available source options on a record by record basis.</span></span> <span data-ttu-id="15f98-325">Puede elegir esta opción si va a importar tooan colección existente que ha alcanzado su cuota de procedimientos almacenados.</span><span class="sxs-lookup"><span data-stu-id="15f98-325">You might choose this option if you’re importing tooan existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="15f98-326">Hola herramienta admite la importación tooa única colección de base de datos de Azure Cosmos (única partición y varias particiones), así como importar particionada mediante el cual los datos se dividen en varias colecciones de base de datos de Azure Cosmos única partición o varias particiones.</span><span class="sxs-lookup"><span data-stu-id="15f98-326">hello tool supports import tooa single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="15f98-327">Para más información sobre la creación de particiones de datos, consulte [Partición y escalado de datos en Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="15f98-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Captura de pantalla de opciones de importación de registros secuenciales de Azure Cosmos DB](./media/import-data/documentdbsequential.png)

<span data-ttu-id="15f98-329">Hola formato de cadena de conexión de base de datos de Azure Cosmos hello es:</span><span class="sxs-lookup"><span data-stu-id="15f98-329">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="15f98-330">cadena de conexión de cuenta de base de datos de Azure Cosmos Hola puede obtenerse de hoja de claves de Hola de hello portal de Azure, como se describe en [cómo toomanage una cuenta de base de datos de Azure Cosmos](manage-account.md); sin embargo, nombre de Hola de base de datos de hello debe toobe anexa toohello cadena de conexión en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="15f98-330">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="15f98-331">Puede tener acceso a la utilice Hola Compruebe comando tooensure que Hola instancia de base de datos de Azure Cosmos especificada en el campo de cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-331">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="15f98-332">tooimport tooa única colección, escriba nombre de Hola de hello colección toowhich datos se va a importar y haga clic en el botón de agregar Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-332">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="15f98-333">tooimport toomultiple colecciones, escriba los nombres de colección individualmente o bien Hola siguiendo la sintaxis toospecify varias colecciones: *collection_prefix*[inicio índice - índice final].</span><span class="sxs-lookup"><span data-stu-id="15f98-333">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="15f98-334">Al especificar varias colecciones a través de la sintaxis de hello mencionado anteriormente, tenga en cuenta los siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="15f98-334">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="15f98-335">Solo se admiten patrones de nombre de intervalo entero.</span><span class="sxs-lookup"><span data-stu-id="15f98-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="15f98-336">Por ejemplo, especificar la colección [0-3] generará Hola después de colecciones: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="15f98-336">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="15f98-337">Puede usar una sintaxis abreviada: colección[3] generará el mismo conjunto de colecciones que el paso 1.</span><span class="sxs-lookup"><span data-stu-id="15f98-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="15f98-338">Se pueden proporcionar varias sustituciones.</span><span class="sxs-lookup"><span data-stu-id="15f98-338">More than one substitution can be provided.</span></span> <span data-ttu-id="15f98-339">Por ejemplo, colección[0-1] [0-9] 20 nombres de colección con ceros delante (colección01,... 02... 03).</span><span class="sxs-lookup"><span data-stu-id="15f98-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="15f98-340">Una vez hello nombres de colección se han especificado, elija rendimiento deseado de Hola de colecciones de hello (too250 de 400 RUs, 000 RUs).</span><span class="sxs-lookup"><span data-stu-id="15f98-340">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too250,000 RUs).</span></span> <span data-ttu-id="15f98-341">Para conseguir el mejor rendimiento en la importación, elija una mayor capacidad de proceso.</span><span class="sxs-lookup"><span data-stu-id="15f98-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="15f98-342">Para más información sobre los niveles de rendimiento, consulte [Niveles de rendimiento en Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="15f98-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="15f98-343">Toda importación toocollections con rendimiento > 10.000 RUs requerirá una clave de partición.</span><span class="sxs-lookup"><span data-stu-id="15f98-343">Any import toocollections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="15f98-344">Si elige más de 250.000 RUs toohave, deberá toofile una solicitud en toohave portal Hola aumenta su cuenta.</span><span class="sxs-lookup"><span data-stu-id="15f98-344">If you choose toohave more than 250,000 RUs, you will need toofile a request in hello portal toohave your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="15f98-345">configuración de rendimiento de Hello solo aplica la creación de toocollection.</span><span class="sxs-lookup"><span data-stu-id="15f98-345">hello throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="15f98-346">Si Hola especifica la colección ya existe, su rendimiento no se modificarán.</span><span class="sxs-lookup"><span data-stu-id="15f98-346">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="15f98-347">Al importar toomultiple colecciones, herramienta de importación de hello admite el particionamiento de hash basado.</span><span class="sxs-lookup"><span data-stu-id="15f98-347">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="15f98-348">En este escenario, especifique la propiedad de documento de hello desea toouse como Hola clave de partición (si la clave de partición se deja en blanco, documentos será particionados aleatoriamente en distintas colecciones de destino de hello).</span><span class="sxs-lookup"><span data-stu-id="15f98-348">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="15f98-349">También puede especificar qué campo de origen que se importarán Hola debe usarse como propiedad de identificador de documento de base de datos de Azure Cosmos Hola durante la importación de hello (tenga en cuenta que si los documentos no contienen esta propiedad, a continuación, herramienta de importación de hello generará un GUID como valor de propiedad de Id. de hello).</span><span class="sxs-lookup"><span data-stu-id="15f98-349">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="15f98-350">Hay una serie de opciones avanzadas disponibles durante la importación.</span><span class="sxs-lookup"><span data-stu-id="15f98-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="15f98-351">En primer lugar, al importar los tipos de fecha (por ejemplo, desde SQL Server o MongoDB), puede elegir entre tres opciones de importación:</span><span class="sxs-lookup"><span data-stu-id="15f98-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Captura de pantalla de opciones de importación de fecha y hora de Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="15f98-353">Cadena: conservar como un valor de cadena</span><span class="sxs-lookup"><span data-stu-id="15f98-353">String: Persist as a string value</span></span>
* <span data-ttu-id="15f98-354">Tiempo: conservar como un valor de número de tiempo</span><span class="sxs-lookup"><span data-stu-id="15f98-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="15f98-355">Ambos: conservar los valores de cadena y de número </span><span class="sxs-lookup"><span data-stu-id="15f98-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="15f98-356">Esta opción creará un subdocumento, por ejemplo "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="15f98-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="15f98-357">Hello Azure Cosmos DB - importador de registro secuencial dispone de opciones avanzadas adicionales siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="15f98-357">hello Azure Cosmos DB - Sequential record importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="15f98-358">Número de solicitudes paralelas: herramienta de hello tiene como valor predeterminado de las solicitudes paralelas de too2.</span><span class="sxs-lookup"><span data-stu-id="15f98-358">Number of Parallel Requests: hello tool defaults too2 parallel requests.</span></span> <span data-ttu-id="15f98-359">Si Hola documentos toobe importado es pequeño, considere la posibilidad de elevación Hola número de solicitudes paralelas.</span><span class="sxs-lookup"><span data-stu-id="15f98-359">If hello documents toobe imported are small, consider raising hello number of parallel requests.</span></span> <span data-ttu-id="15f98-360">Tenga en cuenta que si este número se genera demasiado, Hola importación podría experimentar de limitación.</span><span class="sxs-lookup"><span data-stu-id="15f98-360">Note that if this number is raised too much, hello import may experience throttling.</span></span>
2. <span data-ttu-id="15f98-361">Deshabilitar la generación automática de Id.: Si cada toobe documento importado contiene un campo id, a continuación, al seleccionar esta opción puede aumentar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="15f98-361">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="15f98-362">No se importarán los documentos  que no contengan el campo de identificador exclusivo.</span><span class="sxs-lookup"><span data-stu-id="15f98-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="15f98-363">Documentos de actualización existente: Hola toonot de los valores predeterminados de herramienta reemplazando los documentos existentes con los conflictos de identificador.</span><span class="sxs-lookup"><span data-stu-id="15f98-363">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="15f98-364">Si selecciona esta opción, permitirá que se sobrescriban los documentos existentes con identificadores que coinciden entre sí.</span><span class="sxs-lookup"><span data-stu-id="15f98-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="15f98-365">Esta característica es útil para las migraciones de datos programadas que actualizan los documentos existentes.</span><span class="sxs-lookup"><span data-stu-id="15f98-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="15f98-366">Número de reintentos en caso de error: especifica Hola número de veces tooretry Hola conexión tooAzure Cosmos DB en caso de errores transitorios (por ejemplo, interrupción de conectividad de red).</span><span class="sxs-lookup"><span data-stu-id="15f98-366">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="15f98-367">Intervalo de reintentos: Especifica cuánto tiempo toowait entre los reintentos de conexión tooAzure DB Cosmos de hello en caso de errores transitorios (por ejemplo, interrupción de conectividad de red).</span><span class="sxs-lookup"><span data-stu-id="15f98-367">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="15f98-368">Modo de conexión: Especifica toouse de modo de conexión de hello con base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="15f98-368">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="15f98-369">las opciones disponibles de Hello son DirectTcp, DirectHttps y puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="15f98-369">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="15f98-370">modos de conexión directa de Hello son más rápidos, mientras que el modo de puerta de enlace de hello es firewall más descriptivo como solo usa el puerto 443.</span><span class="sxs-lookup"><span data-stu-id="15f98-370">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Captura de pantalla de opciones avanzadas de importación de registros secuenciales de Azure Cosmos DB](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="15f98-372">modo de tooconnection de los valores predeterminados de herramienta DirectTcp de importación de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-372">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="15f98-373">Si experimenta problemas de firewall, cambie el modo de tooconnection puerta de enlace, ya que solo requiere el puerto 443.</span><span class="sxs-lookup"><span data-stu-id="15f98-373">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="15f98-374"><a id="IndexingPolicy"></a>Especificar una directiva de indexación al crear colecciones de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="15f98-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="15f98-375">Cuando se permite la migración de hello colecciones de toocreate herramienta durante la importación, puede especificar la directiva de indexación de Hola de colecciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-375">When you allow hello migration tool toocreate collections during import, you can specify hello indexing policy of hello collections.</span></span> <span data-ttu-id="15f98-376">Hola avanzada de la sección de opciones de importación en bloque de base de datos de Azure Cosmos hello y secuencial de base de datos de Azure Cosmos opciones de registro, navegue toohello sección sobre la directiva de indización.</span><span class="sxs-lookup"><span data-stu-id="15f98-376">In hello advanced options section of hello Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate toohello Indexing Policy section.</span></span>

![Captura de pantalla de opciones avanzadas de política de indexación de Azure Cosmos DB](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="15f98-378">Con hello opción de directiva de indización avanzada, puede seleccionar un archivo de directiva de indexación, manualmente especificar una directiva de indexación o seleccionar entre un conjunto de plantillas predeterminadas (haciendo clic en hello indización de cuadro de texto de directiva).</span><span class="sxs-lookup"><span data-stu-id="15f98-378">Using hello Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in hello indexing policy textbox).</span></span>

<span data-ttu-id="15f98-379">plantillas de directiva de Hola Hola herramienta proporciona son:</span><span class="sxs-lookup"><span data-stu-id="15f98-379">hello policy templates hello tool provides are:</span></span>

* <span data-ttu-id="15f98-380">Predeterminada.</span><span class="sxs-lookup"><span data-stu-id="15f98-380">Default.</span></span> <span data-ttu-id="15f98-381">Esta directiva es mejor cuando se realizan consultas de igualdad en cadenas y se usan consultas ORDER BY, de rango y de igualdad para números.</span><span class="sxs-lookup"><span data-stu-id="15f98-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="15f98-382">Esta directiva tiene una sobrecarga de almacenamiento de índices menor que la de intervalo.</span><span class="sxs-lookup"><span data-stu-id="15f98-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="15f98-383">Intervalo.</span><span class="sxs-lookup"><span data-stu-id="15f98-383">Range.</span></span> <span data-ttu-id="15f98-384">Esta directiva es mejor si está usando consultas de ORDER BY, intervalo e igualdad en números y cadenas.</span><span class="sxs-lookup"><span data-stu-id="15f98-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="15f98-385">Esta directiva tiene una mayor sobrecarga de almacenamiento de índice que la Predeterminada o Hash.</span><span class="sxs-lookup"><span data-stu-id="15f98-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Captura de pantalla de opciones avanzadas de política de indexación de Azure Cosmos DB](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="15f98-387">Si no especifica una directiva de indexación, se aplicará la directiva predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-387">If you do not specify an indexing policy, then hello default policy will be applied.</span></span> <span data-ttu-id="15f98-388">Para más información sobre las directivas de indexación, consulte [Directivas de indexación de Azure Cosmos DB](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="15f98-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-toojson-file"></a><span data-ttu-id="15f98-389">Archivo de exportación tooJSON</span><span class="sxs-lookup"><span data-stu-id="15f98-389">Export tooJSON file</span></span>
<span data-ttu-id="15f98-390">exportador de JSON de base de datos de Azure Cosmos Hola permite tooexport cualquiera de hello origen disponibles opciones tooa archivo JSON que contiene una matriz de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="15f98-390">hello Azure Cosmos DB JSON exporter allows you tooexport any of hello available source options tooa JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="15f98-391">herramienta Hola controlará la exportación de Hola para usted, o puede elegir el comando resultante de migración de tooview hello y ejecutar comando hello usted mismo.</span><span class="sxs-lookup"><span data-stu-id="15f98-391">hello tool will handle hello export for you, or you can choose tooview hello resulting migration command and run hello command yourself.</span></span> <span data-ttu-id="15f98-392">archivo JSON resultante de Hello puede almacenarse localmente o en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="15f98-392">hello resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Captura de pantalla de opción de exportación de archivo local JSON de Azure Cosmos DB](./media/import-data/jsontarget.png)

![Captura de pantalla de opción de exportación de Azure Blob Storage de JSON de Azure Cosmos DB](./media/import-data/jsontarget2.png)

<span data-ttu-id="15f98-395">También puede elegir hello tooprettify resultante JSON, lo que aumentará el tamaño de saludo del documento resultante de hello mientras lo Hola contenido más legibles.</span><span class="sxs-lookup"><span data-stu-id="15f98-395">You may optionally choose tooprettify hello resulting JSON, which will increase hello size of hello resulting document while making hello contents more human readable.</span></span>

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

## <a name="advanced-configuration"></a><span data-ttu-id="15f98-396">Configuración avanzada</span><span class="sxs-lookup"><span data-stu-id="15f98-396">Advanced configuration</span></span>
<span data-ttu-id="15f98-397">En la pantalla de configuración avanzada de bienvenida, especifique la ubicación de Hola de toowhich de archivo de registro de hello que desea que los errores que se escriben.</span><span class="sxs-lookup"><span data-stu-id="15f98-397">In hello Advanced configuration screen, specify hello location of hello log file toowhich you would like any errors written.</span></span> <span data-ttu-id="15f98-398">Hola siguiendo las reglas aplica toothis página:</span><span class="sxs-lookup"><span data-stu-id="15f98-398">hello following rules apply toothis page:</span></span>

1. <span data-ttu-id="15f98-399">Si no se proporciona un nombre de archivo, se devolverán todos los errores en la página de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-399">If a file name is not provided, then all errors will be returned on hello Results page.</span></span>
2. <span data-ttu-id="15f98-400">Si se proporciona un nombre de archivo sin un directorio, a continuación, archivo hello se crean (o sobrescribe) en el directorio actual de entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-400">If a file name is provided without a directory, then hello file will be created (or overwritten) in hello current environment directory.</span></span>
3. <span data-ttu-id="15f98-401">Si selecciona una existente se sobrescribirán los archivos y, a continuación, archivo hello, no hay ninguna opción de anexar.</span><span class="sxs-lookup"><span data-stu-id="15f98-401">If you select an existing file, then hello file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="15f98-402">A continuación, elija si toolog todos los críticos, o ningún mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="15f98-402">Then, choose whether toolog all, critical, or no error messages.</span></span> <span data-ttu-id="15f98-403">Por último, decidir con qué frecuencia se actualizarán hello en el mensaje de transferencia de pantalla con su progreso.</span><span class="sxs-lookup"><span data-stu-id="15f98-403">Finally, decide how frequently hello on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="15f98-404">Confirmación de las opciones de importación y visualización de la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="15f98-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="15f98-405">Después de especificar información de origen, la información de destino y la configuración avanzada, revise el resumen de la migración de Hola y, opcionalmente, ver o copiar Hola resultante comando migration (copia comando hello es útil tooautomate las operaciones de importación):</span><span class="sxs-lookup"><span data-stu-id="15f98-405">After specifying source information, target information, and advanced configuration, review hello migration summary and, optionally, view/copy hello resulting migration command (copying hello command is useful tooautomate import operations):</span></span>
   
    ![Screenshot of summary screen](./media/import-data/summary.png)
   
    ![Screenshot of summary screen](./media/import-data/summarycommand.png)
2. <span data-ttu-id="15f98-408">Una vez que esté satisfecho con las opciones de origen y de destino, haga clic en **Importar**.</span><span class="sxs-lookup"><span data-stu-id="15f98-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="15f98-409">tiempo transcurrido de Hello, recuento transferido e información del error (si no proporcionó un nombre de archivo de configuración avanzada de Hola) se actualizarán tal y como está en proceso de importación de Hola.</span><span class="sxs-lookup"><span data-stu-id="15f98-409">hello elapsed time, transferred count, and failure information (if you didn't provide a file name in hello Advanced configuration) will update as hello import is in process.</span></span> <span data-ttu-id="15f98-410">Una vez completado, puede exportar resultados de hello (p. ej., toodeal con los errores de importación).</span><span class="sxs-lookup"><span data-stu-id="15f98-410">Once complete, you can export hello results (e.g. toodeal with any import failures).</span></span>
   
    ![Captura de pantalla de opción de exportación de JSON de Azure Cosmos DB](./media/import-data/viewresults.png)
3. <span data-ttu-id="15f98-412">También puede iniciar una nueva importación, conservando la configuración existente de hello (p. ej., elección de información de origen y de destino de la cadena de conexión, etc.) o restablecer todos los valores.</span><span class="sxs-lookup"><span data-stu-id="15f98-412">You may also start a new import, either keeping hello existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Captura de pantalla de opción de exportación de JSON de Azure Cosmos DB](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="15f98-414">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="15f98-414">Next steps</span></span>

<span data-ttu-id="15f98-415">En este tutorial, ha hecho siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="15f98-415">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="15f98-416">Instala la herramienta de migración de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="15f98-416">Installed hello Data Migration tool</span></span>
> * <span data-ttu-id="15f98-417">Importación de datos de orígenes de datos diferentes</span><span class="sxs-lookup"><span data-stu-id="15f98-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="15f98-418">Exportar desde la base de datos de Azure Cosmos tooJSON</span><span class="sxs-lookup"><span data-stu-id="15f98-418">Exported from Azure Cosmos DB tooJSON</span></span>

<span data-ttu-id="15f98-419">Ahora puede continuar el tutorial siguiente toohello y obtenga información acerca de cómo los datos de tooquery con la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="15f98-419">You can now proceed toohello next tutorial and learn how tooquery data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="15f98-420">¿Cómo tooquery datos?</span><span class="sxs-lookup"><span data-stu-id="15f98-420">How tooquery data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
