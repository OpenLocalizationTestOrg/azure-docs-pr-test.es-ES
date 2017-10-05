---
title: "Herramienta de migración de base de datos para Azure Cosmos DB | Microsoft Docs"
description: "Obtenga información sobre cómo usar las herramientas de migración de datos de código abierto de Azure Cosmos DB para importar datos a Azure Cosmos DB desde varios orígenes, incluidos archivos MongoDB, SQL Server, Table Storage, Amazon DynamoDB, CSV y JSON. Conversión de CSV a JSON."
keywords: "csv a json, herramientas de migración de base de datos, convertir csv a json"
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
ms.openlocfilehash: 23a4a82dbdb611f4da90562af936fca28da9b24d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-data-into-azure-cosmos-db-for-the-documentdb-api"></a><span data-ttu-id="10ef7-105">Importación de datos en Azure Cosmos DB para la API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="10ef7-105">How to import data into Azure Cosmos DB for the DocumentDB API?</span></span>

<span data-ttu-id="10ef7-106">En este tutorial se muestra cómo utilizar la herramienta DocumentDB API Data Migration de Azure Cosmos DB, que puede importar datos desde diversos orígenes, incluidos archivos JSON, archivos CSV, SQL, MongoDB, Azure Table Storage, Amazon DynamoDB y colecciones de la API de DocumentDB de Azure Cosmos DB en colecciones para utilizarlos con Azure Cosmos DB y la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="10ef7-106">This tutorial provides instructions on using the Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and the DocumentDB API.</span></span> <span data-ttu-id="10ef7-107">También se puede utilizar la herramienta de migración de datos al migrar de una colección de una recolección de una sola partición a una colección de varias particiones de la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="10ef7-107">The Data Migration tool can also be used when migrating from a single partition collection to a multi-partition collection for the DocumentDB API.</span></span>

<span data-ttu-id="10ef7-108">La herramienta de migración de datos solo funciona al importar datos a Azure Cosmos DB para usar con la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="10ef7-108">The Data Migration tool only works when importing data into Azure Cosmos DB for use with the DocumentDB API.</span></span> <span data-ttu-id="10ef7-109">En este momento, no se admite la importación de datos para su uso con la API de Table o la API Graph.</span><span class="sxs-lookup"><span data-stu-id="10ef7-109">Importing data for use with the Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="10ef7-110">Para importar datos para su uso con la API de MongoDB, vea [Azure Cosmos DB: migración de datos para la API de MongoDB](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="10ef7-110">To import data for use with the MongoDB API, see [Azure Cosmos DB: How to migrate data for the MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="10ef7-111">En este tutorial se describen las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="10ef7-111">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="10ef7-112">Instalación de la herramienta de migración de datos</span><span class="sxs-lookup"><span data-stu-id="10ef7-112">Installing the Data Migration tool</span></span>
> * <span data-ttu-id="10ef7-113">Importación de datos de orígenes de datos diferentes</span><span class="sxs-lookup"><span data-stu-id="10ef7-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="10ef7-114">Exportación desde Azure Cosmos DB a JSON</span><span class="sxs-lookup"><span data-stu-id="10ef7-114">Exporting from Azure Cosmos DB to JSON</span></span>

## <span data-ttu-id="10ef7-115"><a id="Prerequisites"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="10ef7-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="10ef7-116">Antes de seguir las instrucciones del presente artículo, asegúrese de tener instalados los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="10ef7-116">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="10ef7-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) o superior.</span><span class="sxs-lookup"><span data-stu-id="10ef7-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="10ef7-118"><a id="Overviewl"></a>Información general sobre la herramienta de migración de datos</span><span class="sxs-lookup"><span data-stu-id="10ef7-118"><a id="Overviewl"></a>Overview of the Data Migration tool</span></span>
<span data-ttu-id="10ef7-119">La herramienta de migración de datos es una solución de código abierto que importa los datos a Azure Cosmos DB desde una variedad de orígenes, como:</span><span class="sxs-lookup"><span data-stu-id="10ef7-119">The Data Migration tool is an open source solution that imports data to Azure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="10ef7-120">Archivos JSON</span><span class="sxs-lookup"><span data-stu-id="10ef7-120">JSON files</span></span>
* <span data-ttu-id="10ef7-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="10ef7-121">MongoDB</span></span>
* <span data-ttu-id="10ef7-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="10ef7-122">SQL Server</span></span>
* <span data-ttu-id="10ef7-123">Archivos CSV</span><span class="sxs-lookup"><span data-stu-id="10ef7-123">CSV files</span></span>
* <span data-ttu-id="10ef7-124">Almacenamiento de tablas de Azure</span><span class="sxs-lookup"><span data-stu-id="10ef7-124">Azure Table storage</span></span>
* <span data-ttu-id="10ef7-125">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="10ef7-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="10ef7-126">HBase</span><span class="sxs-lookup"><span data-stu-id="10ef7-126">HBase</span></span>
* <span data-ttu-id="10ef7-127">Colecciones de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="10ef7-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="10ef7-128">Aunque la herramienta de importación incluye una interfaz gráfica de usuario (dtui.exe), también se pueden controlar desde la línea de comandos (dt.exe).</span><span class="sxs-lookup"><span data-stu-id="10ef7-128">While the import tool includes a graphical user interface (dtui.exe), it can also be driven from the command line (dt.exe).</span></span> <span data-ttu-id="10ef7-129">De hecho, hay una opción para mostrar el comando asociado después de configurar una importación a través de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="10ef7-129">In fact, there is an option to output the associated command after setting up an import through the UI.</span></span> <span data-ttu-id="10ef7-130">Se pueden transformar datos tabulares de origen (por ejemplo, archivos de SQL Server o CSV) de tal forma que se pueden crear relaciones jerárquicas (subdocumentos) durante la importación.</span><span class="sxs-lookup"><span data-stu-id="10ef7-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="10ef7-131">Siga leyendo para obtener más información acerca de las opciones de origen, las líneas de comandos de muestra para importar desde cada origen, las opciones de destino y la visualización de los resultados de importación.</span><span class="sxs-lookup"><span data-stu-id="10ef7-131">Keep reading to learn more about source options, sample command lines to import from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="10ef7-132"><a id="Install"></a>Instalación de la herramienta de migración de datos</span><span class="sxs-lookup"><span data-stu-id="10ef7-132"><a id="Install"></a>Install the Data Migration tool</span></span>
<span data-ttu-id="10ef7-133">El código fuente de la herramienta de migración está disponible en GitHub en [este repositorio](https://github.com/azure/azure-documentdb-datamigrationtool) y una versión compilada se encuentra disponible en el [Centro de descarga de Microsoft](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span><span class="sxs-lookup"><span data-stu-id="10ef7-133">The migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="10ef7-134">Puede compilar la solución o simplemente descargar y extraer la versión compilada en un directorio de su elección.</span><span class="sxs-lookup"><span data-stu-id="10ef7-134">You may either compile the solution or simply download and extract the compiled version to a directory of your choice.</span></span> <span data-ttu-id="10ef7-135">A continuación, ejecute:</span><span class="sxs-lookup"><span data-stu-id="10ef7-135">Then run either:</span></span>

* <span data-ttu-id="10ef7-136">**Dtui.exe**: versión de interfaz gráfica de la herramienta</span><span class="sxs-lookup"><span data-stu-id="10ef7-136">**Dtui.exe**: Graphical interface version of the tool</span></span>
* <span data-ttu-id="10ef7-137">**Dt.exe**: versión de línea de comandos de la herramienta</span><span class="sxs-lookup"><span data-stu-id="10ef7-137">**Dt.exe**: Command-line version of the tool</span></span>

## <a name="import-data"></a><span data-ttu-id="10ef7-138">Importar datos</span><span class="sxs-lookup"><span data-stu-id="10ef7-138">Import data</span></span>

<span data-ttu-id="10ef7-139">Una vez que haya instalado la herramienta, es el momento de importar los datos.</span><span class="sxs-lookup"><span data-stu-id="10ef7-139">Once you've installed the tool, it's time to import your data.</span></span> <span data-ttu-id="10ef7-140">¿Qué tipo de datos desea importar?</span><span class="sxs-lookup"><span data-stu-id="10ef7-140">What kind of data do you want to import?</span></span>

* [<span data-ttu-id="10ef7-141">Archivos JSON</span><span class="sxs-lookup"><span data-stu-id="10ef7-141">JSON files</span></span>](#JSON)
* [<span data-ttu-id="10ef7-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="10ef7-142">MongoDB</span></span>](#MongoDB)
* [<span data-ttu-id="10ef7-143">Archivos de exportación de MongoDB</span><span class="sxs-lookup"><span data-stu-id="10ef7-143">MongoDB Export files</span></span>](#MongoDBExport)
* [<span data-ttu-id="10ef7-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="10ef7-144">SQL Server</span></span>](#SQL)
* [<span data-ttu-id="10ef7-145">Archivos CSV</span><span class="sxs-lookup"><span data-stu-id="10ef7-145">CSV files</span></span>](#CSV)
* [<span data-ttu-id="10ef7-146">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="10ef7-146">Azure Table storage</span></span>](#AzureTableSource)
* [<span data-ttu-id="10ef7-147">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="10ef7-147">Amazon DynamoDB</span></span>](#DynamoDBSource)
* [<span data-ttu-id="10ef7-148">Blob</span><span class="sxs-lookup"><span data-stu-id="10ef7-148">Blob</span></span>](#BlobImport)
* [<span data-ttu-id="10ef7-149">Colecciones de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="10ef7-149">Azure Cosmos DB collections</span></span>](#DocumentDBSource)
* [<span data-ttu-id="10ef7-150">HBase</span><span class="sxs-lookup"><span data-stu-id="10ef7-150">HBase</span></span>](#HBaseSource)
* [<span data-ttu-id="10ef7-151">Importación masiva de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="10ef7-151">Azure Cosmos DB bulk import</span></span>](#DocumentDBBulkImport)
* [<span data-ttu-id="10ef7-152">Importación de registros secuenciales de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="10ef7-152">Azure Cosmos DB sequential record import</span></span>](#DocumentDSeqTarget)


## <span data-ttu-id="10ef7-153"><a id="JSON"></a>Para importar archivos JSON</span><span class="sxs-lookup"><span data-stu-id="10ef7-153"><a id="JSON"></a>To import JSON files</span></span>
<span data-ttu-id="10ef7-154">La opción del importador de origen de archivos JSON permite importar uno o varios archivos JSON de un único documento o archivos JSON que contengan cada uno una matriz de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="10ef7-154">The JSON file source importer option allows you to import one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="10ef7-155">Cuando se agregan carpetas que contienen archivos JSON que se van a importar, existe la opción de buscar archivos en subcarpetas de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="10ef7-155">When adding folders that contain JSON files to import, you have the option of recursively searching for files in subfolders.</span></span>

![Captura de pantalla de opciones de origen de archivos JSON: herramientas de migración de base de datos](./media/import-data/jsonsource.png)

<span data-ttu-id="10ef7-157">Estos son algunos ejemplos de línea de comandos para importar archivos JSON:</span><span class="sxs-lookup"><span data-stu-id="10ef7-157">Here are some command line samples to import JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition the data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <span data-ttu-id="10ef7-158"><a id="MongoDB"></a>Para importar desde MongoDB</span><span class="sxs-lookup"><span data-stu-id="10ef7-158"><a id="MongoDB"></a>To import from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10ef7-159">Si va a importar a una cuenta de Azure Cosmos DB compatible con MongoDB, siga estas [instrucciones](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="10ef7-159">If you are importing to an Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="10ef7-160">La opción del importador de origen de MongoDB permite importar desde una colección de MongoDB individual y, opcionalmente, filtrar documentos mediante una consulta o modificar la estructura del documento con una proyección.</span><span class="sxs-lookup"><span data-stu-id="10ef7-160">The MongoDB source importer option allows you to import from an individual MongoDB collection and optionally filter documents using a query and/or modify the document structure by using a projection.</span></span>  

![Captura de pantalla de las opciones de origen de MongoDB](./media/import-data/mongodbsource.png)

<span data-ttu-id="10ef7-162">La cadena de conexión tiene el formato estándar de MongoDB:</span><span class="sxs-lookup"><span data-stu-id="10ef7-162">The connection string is in the standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="10ef7-163">Utilice el comando Verify para asegurarse de que se puede tener acceso a la instancia de MongoDB especificada en el campo de la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="10ef7-163">Use the Verify command to ensure that the MongoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="10ef7-164">Escriba el nombre de la colección desde la que se importarán los datos.</span><span class="sxs-lookup"><span data-stu-id="10ef7-164">Enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="10ef7-165">Opcionalmente, puede especificar o facilitar un archivo para una consulta (por ejemplo, {pop: {$gt:5000}}) o proyección (por ejemplo, {loc:0}) para filtrar los datos que se van a importar y darles forma.</span><span class="sxs-lookup"><span data-stu-id="10ef7-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) to both filter and shape the data to be imported.</span></span>

<span data-ttu-id="10ef7-166">Estos son algunos ejemplos de línea de comandos para importar desde MongoDB:</span><span class="sxs-lookup"><span data-stu-id="10ef7-166">Here are some command line samples to import from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match the query and exclude the loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="10ef7-167"><a id="MongoDBExport"></a>Para importar archivos de exportación de MongoDB</span><span class="sxs-lookup"><span data-stu-id="10ef7-167"><a id="MongoDBExport"></a>To import MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10ef7-168">Si va a importar a una cuenta de Azure Cosmos DB compatible con MongoDB, siga estas [instrucciones](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="10ef7-168">If you are importing to an Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="10ef7-169">La opción del importador de origen de archivos JSON de exportación de MongoDB permite importar uno o más archivos JSON generados a partir de la utilidad mongoexport.</span><span class="sxs-lookup"><span data-stu-id="10ef7-169">The MongoDB export JSON file source importer option allows you to import one or more JSON files produced from the mongoexport utility.</span></span>  

![Captura de pantalla de las opciones de origen de exportación de MongoDB](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="10ef7-171">Cuando se agregan carpetas que contienen archivos JSON de exportación de MongoDB para importarlos, tiene la opción de buscar archivos en subcarpetas de forma recursiva:</span><span class="sxs-lookup"><span data-stu-id="10ef7-171">When adding folders that contain MongoDB export JSON files for import, you have the option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="10ef7-172">A continuación se muestra un ejemplo de línea de comandos para importar desde archivos JSON de exportación de MongoDB:</span><span class="sxs-lookup"><span data-stu-id="10ef7-172">Here is a command line sample to import from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="10ef7-173"><a id="SQL"></a>Para importar desde SQL Server</span><span class="sxs-lookup"><span data-stu-id="10ef7-173"><a id="SQL"></a>To import from SQL Server</span></span>
<span data-ttu-id="10ef7-174">La opción del importador de origen SQL permite importar desde una base de datos SQL Server individual y, opcionalmente, filtrar los registros que se pueden importar utilizando una consulta.</span><span class="sxs-lookup"><span data-stu-id="10ef7-174">The SQL source importer option allows you to import from an individual SQL Server database and optionally filter the records to be imported using a query.</span></span> <span data-ttu-id="10ef7-175">Además, puede modificar la estructura del documento especificando un separador de anidamiento (más en un momento determinado).</span><span class="sxs-lookup"><span data-stu-id="10ef7-175">In addition, you can modify the document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![Captura de pantalla de opciones de origen de SQL: herramientas de migración de base de datos](./media/import-data/sqlexportsource.png)

<span data-ttu-id="10ef7-177">El formato de la cadena de conexión es el formato de la cadena de conexión SQL estándar.</span><span class="sxs-lookup"><span data-stu-id="10ef7-177">The format of the connection string is the standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="10ef7-178">Utilice el comando Verify para asegurarse de que se puede tener acceso a la instancia de SQL Server especificada en el campo de la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="10ef7-178">Use the Verify command to ensure that the SQL Server instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="10ef7-179">La propiedad de separador de anidamiento se utiliza para crear relaciones jerárquicas (documentos secundarios) durante la importación.</span><span class="sxs-lookup"><span data-stu-id="10ef7-179">The nesting separator property is used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="10ef7-180">Considere la siguiente consulta SQL:</span><span class="sxs-lookup"><span data-stu-id="10ef7-180">Consider the following SQL query:</span></span>

<span data-ttu-id="10ef7-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as Address.AddressType, AddressLine1 as Address.AddressLine1, City as Address.Location.City, StateProvinceName as Address.Location.StateProvinceName, PostalCode as Address.PostalCode, CountryRegionName as Address.CountryRegionName from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span><span class="sxs-lookup"><span data-stu-id="10ef7-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="10ef7-182">Que devuelve los resultados siguientes (parciales):</span><span class="sxs-lookup"><span data-stu-id="10ef7-182">Which returns the following (partial) results:</span></span>

![Screenshot of SQL query results](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="10ef7-184">Tenga en cuenta los alias como Address.AddressType y Address.Location.StateProvinceName.</span><span class="sxs-lookup"><span data-stu-id="10ef7-184">Note the aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="10ef7-185">Al especificar un separador de anidamiento de “.”, la herramienta de importación crea subdocumentos Address y Address.Location durante la importación.</span><span class="sxs-lookup"><span data-stu-id="10ef7-185">By specifying a nesting separator of ‘.’, the import tool creates Address and Address.Location subdocuments during the import.</span></span> <span data-ttu-id="10ef7-186">Este es un ejemplo de un documento resultante en Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="10ef7-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="10ef7-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span><span class="sxs-lookup"><span data-stu-id="10ef7-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="10ef7-188">Estos son algunos ejemplos de línea de comandos para importar desde SQL Server:</span><span class="sxs-lookup"><span data-stu-id="10ef7-188">Here are some command line samples to import from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="10ef7-189"><a id="CSV"></a>Para importar archivos CSV y convertirlos a JSON</span><span class="sxs-lookup"><span data-stu-id="10ef7-189"><a id="CSV"></a>To import CSV files and convert CSV to JSON</span></span>
<span data-ttu-id="10ef7-190">La opción del importador de origen de archivos CSV le permite importar uno o varios archivos CSV.</span><span class="sxs-lookup"><span data-stu-id="10ef7-190">The CSV file source importer option enables you to import one or more CSV files.</span></span> <span data-ttu-id="10ef7-191">Cuando se agregan carpetas que contienen archivos CSV que se van a importar, existe la opción de buscar archivos en subcarpetas de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="10ef7-191">When adding folders that contain CSV files for import, you have the option of recursively searching for files in subfolders.</span></span>

![Captura de pantalla de opciones de origen de CSV](media/import-data/csvsource.png)

<span data-ttu-id="10ef7-193">De forma similar a lo que sucede con el origen SQL, la propiedad de separador de anidamiento se utiliza para crear relaciones jerárquicas (documentos secundarios) durante la importación.</span><span class="sxs-lookup"><span data-stu-id="10ef7-193">Similar to the SQL source, the nesting separator property may be used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="10ef7-194">Tenga en cuenta las siguientes filas de datos y la fila de encabezado CSV:</span><span class="sxs-lookup"><span data-stu-id="10ef7-194">Consider the following CSV header row and data rows:</span></span>

![Captura de pantalla de registros de ejemplo de CSV: CSV a JSON](./media/import-data/csvsample.png)

<span data-ttu-id="10ef7-196">Tenga en cuenta los alias como DomainInfo.Domain_Name y RedirectInfo.Redirecting.</span><span class="sxs-lookup"><span data-stu-id="10ef7-196">Note the aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="10ef7-197">Al especificar un separador de anidamiento de “.”, la herramienta de importación crea subdocumentos DomainInfo y RedirectInfo durante la importación.</span><span class="sxs-lookup"><span data-stu-id="10ef7-197">By specifying a nesting separator of ‘.’, the import tool will create DomainInfo and RedirectInfo subdocuments during the import.</span></span> <span data-ttu-id="10ef7-198">Este es un ejemplo de un documento resultante en Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="10ef7-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="10ef7-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span><span class="sxs-lookup"><span data-stu-id="10ef7-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="10ef7-200">La herramienta de importación intentará inferir la información de tipo de los valores sin comillas de los archivos CSV (los valores entre comillas se tratan siempre como cadenas).</span><span class="sxs-lookup"><span data-stu-id="10ef7-200">The import tool will attempt to infer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="10ef7-201">Los tipos se identifican en el siguiente orden: número, fecha y hora, booleano.</span><span class="sxs-lookup"><span data-stu-id="10ef7-201">Types are identified in the following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="10ef7-202">Hay otras dos cosas que debe saber sobre la importación de archivos CSV:</span><span class="sxs-lookup"><span data-stu-id="10ef7-202">There are two other things to note about CSV import:</span></span>

1. <span data-ttu-id="10ef7-203">De forma predeterminada, los valores sin comillas se recortan siempre en tabuladores y espacios, mientras que los valores entre comillas se mantienen como son.</span><span class="sxs-lookup"><span data-stu-id="10ef7-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="10ef7-204">Este comportamiento se puede invalidar con la casilla Recortar valores entre comillas o la opción de línea de comandos /s.TrimQuoted.</span><span class="sxs-lookup"><span data-stu-id="10ef7-204">This behavior can be overridden with the Trim quoted values checkbox or the /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="10ef7-205">De forma predeterminada, un valor null sin comillas se trata como un valor null.</span><span class="sxs-lookup"><span data-stu-id="10ef7-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="10ef7-206">Este comportamiento se puede invalidar (es decir, tratar a los valores null sin comillas como si fueran cadenas "null") con la casilla Tratar NULL sin comillas como cadena o la opción de línea de comandos /s.NoUnquotedNulls.</span><span class="sxs-lookup"><span data-stu-id="10ef7-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with the Treat unquoted NULL as string checkbox or the /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="10ef7-207">Este es un ejemplo de línea de comandos para la importación CSV:</span><span class="sxs-lookup"><span data-stu-id="10ef7-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="10ef7-208"><a id="AzureTableSource"></a>Para importar desde Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="10ef7-208"><a id="AzureTableSource"></a>To import from Azure Table storage</span></span>
<span data-ttu-id="10ef7-209">La opción del importador de código fuente de almacenamiento de tabla de Azure permite importar desde una tabla de almacenamiento de Azure individual y, opcionalmente, filtrar las entidades de tabla que se van a importar.</span><span class="sxs-lookup"><span data-stu-id="10ef7-209">The Azure Table storage source importer option allows you to import from an individual Azure Table storage table and optionally filter the table entities to be imported.</span></span> <span data-ttu-id="10ef7-210">Tenga en cuenta que no puede usar la herramienta de migración de datos para importar datos de Azure Table Storage a Azure Cosmos DB para su uso con la API de Table.</span><span class="sxs-lookup"><span data-stu-id="10ef7-210">Note that you cannot use the Data Migration tool to import Azure Table storage data into Azure Cosmos DB for use with the Table API.</span></span> <span data-ttu-id="10ef7-211">En este momento, se admite solo la importación de Azure Cosmos DB para su uso con la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="10ef7-211">Only importing to Azure Cosmos DB for use with the DocumentDB API is supported at this time.</span></span>

![Screenshot of Azure Table storage source options](./media/import-data/azuretablesource.png)

<span data-ttu-id="10ef7-213">El formato de la cadena de conexión de almacenamiento de tablas de Azure es:</span><span class="sxs-lookup"><span data-stu-id="10ef7-213">The format of the Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="10ef7-214">Utilice el comando Verify para asegurarse de que se puede tener acceso a la instancia de almacenamiento de tablas de Azure especificada en el campo de la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="10ef7-214">Use the Verify command to ensure that the Azure Table storage instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="10ef7-215">Escriba el nombre de la tabla de Azure desde la que se importarán los datos.</span><span class="sxs-lookup"><span data-stu-id="10ef7-215">Enter the name of the Azure table from which data will be imported.</span></span> <span data-ttu-id="10ef7-216">Opcionalmente, puede especificar un [filtro](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span><span class="sxs-lookup"><span data-stu-id="10ef7-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="10ef7-217">La opción del importador de origen de almacenamiento de tablas de Azure tiene las siguientes opciones adicionales:</span><span class="sxs-lookup"><span data-stu-id="10ef7-217">The Azure Table storage source importer option has the following additional options:</span></span>

1. <span data-ttu-id="10ef7-218">Incluir campos internos</span><span class="sxs-lookup"><span data-stu-id="10ef7-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="10ef7-219">All: incluir todos los campos internos (PartitionKey, RowKey y Timestamp)</span><span class="sxs-lookup"><span data-stu-id="10ef7-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="10ef7-220">None: excluir todos los campos internos</span><span class="sxs-lookup"><span data-stu-id="10ef7-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="10ef7-221">RowKey: incluir sólo el campo RowKey</span><span class="sxs-lookup"><span data-stu-id="10ef7-221">RowKey - Only include the RowKey field</span></span>
2. <span data-ttu-id="10ef7-222">Seleccionar columnas</span><span class="sxs-lookup"><span data-stu-id="10ef7-222">Select Columns</span></span>
   1. <span data-ttu-id="10ef7-223">Los filtros de almacenamiento de tablas de Azure no admiten proyecciones.</span><span class="sxs-lookup"><span data-stu-id="10ef7-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="10ef7-224">Si desea importar sólo las propiedades específicas de la entidad de tablas de Azure, agréguelas a la lista Seleccionar columnas.</span><span class="sxs-lookup"><span data-stu-id="10ef7-224">If you want to only import specific Azure Table entity properties, add them to the Select Columns list.</span></span> <span data-ttu-id="10ef7-225">Se omitirán todas las demás propiedades de la entidad.</span><span class="sxs-lookup"><span data-stu-id="10ef7-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="10ef7-226">A continuación se muestra un ejemplo de línea de comandos para importar desde el almacenamiento de tablas de Azure:</span><span class="sxs-lookup"><span data-stu-id="10ef7-226">Here is a command line sample to import from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="10ef7-227"><a id="DynamoDBSource"></a>Para importar desde Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="10ef7-227"><a id="DynamoDBSource"></a>To import from Amazon DynamoDB</span></span>
<span data-ttu-id="10ef7-228">La opción de importador de origen Amazon DynamoDB permite importar de una tabla individual de Amazon DynamoDB individual y, opcionalmente, filtrar las entidades que desea importar.</span><span class="sxs-lookup"><span data-stu-id="10ef7-228">The Amazon DynamoDB source importer option allows you to import from an individual Amazon DynamoDB table and optionally filter the entities to be imported.</span></span> <span data-ttu-id="10ef7-229">Se proporcionan varias plantillas para que configurar una importación resulte lo más fácil posible.</span><span class="sxs-lookup"><span data-stu-id="10ef7-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Captura de pantalla de opciones de origen de Amazon DynamoD: herramientas de migración de base de datos](./media/import-data/dynamodbsource1.png)

![Captura de pantalla de opciones de origen de Amazon DynamoD: herramientas de migración de base de datos](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="10ef7-232">El formato de la cadena de conexión de Amazon DynamoDB es:</span><span class="sxs-lookup"><span data-stu-id="10ef7-232">The format of the Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="10ef7-233">Use el comando Verify para asegurarse de que se puede tener acceso a la instancia de Amazon DynamoDB especificada en el campo de la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="10ef7-233">Use the Verify command to ensure that the Amazon DynamoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="10ef7-234">A continuación se muestra un ejemplo de línea de comandos para importar desde Amazon DynamoDB:</span><span class="sxs-lookup"><span data-stu-id="10ef7-234">Here is a command line sample to import from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="10ef7-235"><a id="BlobImport"></a>Para importar archivos desde Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="10ef7-235"><a id="BlobImport"></a>To import files from Azure Blob storage</span></span>
<span data-ttu-id="10ef7-236">El archivo JSON, archivo de exportación de MongoDB y opciones de importador de origen de archivo CSV permiten importar uno o más archivos del almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="10ef7-236">The JSON file, MongoDB export file, and CSV file source importer options allow you to import one or more files from Azure Blob storage.</span></span> <span data-ttu-id="10ef7-237">Después de especificar una dirección URL de contenedor de blobs y una clave de cuenta, basta con proporcionar una expresión regular para seleccionar los archivos para importar.</span><span class="sxs-lookup"><span data-stu-id="10ef7-237">After specifying a Blob container URL and Account Key, simply provide a regular expression to select the file(s) to import.</span></span>

![Captura de pantalla de opciones de origen de archivos Blob](./media/import-data/blobsource.png)

<span data-ttu-id="10ef7-239">Este es el ejemplo de línea de comandos para importar archivos JSON del almacenamiento de blobs de Azure:</span><span class="sxs-lookup"><span data-stu-id="10ef7-239">Here is command line sample to import JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="10ef7-240"><a id="DocumentDBSource"></a>Para importar desde una colección de la API de DocumentDB de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="10ef7-240"><a id="DocumentDBSource"></a>To import from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="10ef7-241">La opción del importador de origen de Azure Cosmos DB permite importar datos de una o varias colecciones de Azure Cosmos DB y, opcionalmente, filtrar los documentos mediante una consulta.</span><span class="sxs-lookup"><span data-stu-id="10ef7-241">The Azure Cosmos DB source importer option allows you to import data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Captura de pantalla de opciones de origen de Azure Cosmos DB](./media/import-data/documentdbsource.png)

<span data-ttu-id="10ef7-243">El formato de la cadena de conexión de Azure Cosmos DB es:</span><span class="sxs-lookup"><span data-stu-id="10ef7-243">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="10ef7-244">La cadena de conexión de la cuenta de Azure Cosmos DB se puede obtener en la hoja Claves de Azure Portal, como se describe en [Administración de una cuenta de Azure Cosmos DB](manage-account.md); sin embargo, el nombre de la base de datos se debe anexar a la cadena de conexión con el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="10ef7-244">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="10ef7-245">Use el comando Verify para asegurarse de que se puede tener acceso a la instancia de Azure Cosmos DB especificada en el campo de la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="10ef7-245">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="10ef7-246">Para realizar la importación desde una sola colección de Azure Cosmos DB, escriba el nombre de la colección de la que se van a importar los datos.</span><span class="sxs-lookup"><span data-stu-id="10ef7-246">To import from a single Azure Cosmos DB collection, enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="10ef7-247">Para realizar la importación desde varias colecciones de Azure Cosmos DB, especifique una expresión regular que coincida con uno o varios nombres de colección (por ejemplo, collección01 | collección02 | collección03).</span><span class="sxs-lookup"><span data-stu-id="10ef7-247">To import from multiple Azure Cosmos DB collections, provide a regular expression to match one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="10ef7-248">Opcionalmente, puede especificar o facilitar un archivo para una consulta para filtrar los datos que se van a importar y darles forma.</span><span class="sxs-lookup"><span data-stu-id="10ef7-248">You may optionally specify, or provide a file for, a query to both filter and shape the data to be imported.</span></span>

> [!NOTE]
> <span data-ttu-id="10ef7-249">Dado que el campo de colecciones acepta expresiones regulares, si la importación se va a realizar de una sola colección cuyo nombre contenga caracteres de expresión regular, dichos caracteres deben incluir una secuencia de escape.</span><span class="sxs-lookup"><span data-stu-id="10ef7-249">Since the collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="10ef7-250">La opción del importador de origen de Azure Cosmos DB tiene las siguientes opciones avanzadas:</span><span class="sxs-lookup"><span data-stu-id="10ef7-250">The Azure Cosmos DB source importer option has the following advanced options:</span></span>

1. <span data-ttu-id="10ef7-251">Incluir campos internos: especifica si se debe o no incluir propiedades del sistema de documentos de Azure Cosmos DB en la exportación (por ejemplo, _rid, _ts).</span><span class="sxs-lookup"><span data-stu-id="10ef7-251">Include Internal Fields: Specifies whether or not to include Azure Cosmos DB document system properties in the export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="10ef7-252">Número de reintentos en caso de error: especifica el número de veces que se intentará la conexión a Azure Cosmos DB en caso de errores transitorios (por ejemplo, interrupciones de conectividad de red).</span><span class="sxs-lookup"><span data-stu-id="10ef7-252">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="10ef7-253">Intervalo de reintento: especifica el tiempo de espera entre los reintentos de restablecimiento de conexión a Azure Cosmos DB en caso de errores transitorios (por ejemplo, interrupción de la conectividad de red).</span><span class="sxs-lookup"><span data-stu-id="10ef7-253">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="10ef7-254">Modo de conexión: especifica el modo de conexión para utilizar con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="10ef7-254">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="10ef7-255">Las opciones disponibles son DirectTcp, DirectHttps y puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="10ef7-255">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="10ef7-256">Los modos de conexión directa son más rápidos, mientras que el modo de puerta de enlace es compatible con el firewall, ya que sólo usa el puerto 443.</span><span class="sxs-lookup"><span data-stu-id="10ef7-256">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Captura de pantalla de opciones avanzadas de origen de Azure Cosmos DB](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="10ef7-258">El modo de conexión predeterminado de la herramienta de importación es DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="10ef7-258">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="10ef7-259">Si experimenta problemas de firewall, cambie al modo de conexión puerta de enlace, ya que sólo requiere el puerto 443.</span><span class="sxs-lookup"><span data-stu-id="10ef7-259">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="10ef7-260">Estos son algunos ejemplos de línea de comandos para importar desde Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="10ef7-260">Here are some command line samples to import from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection to another Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections to a single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection to a JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="10ef7-261">La herramienta de importación de datos de Azure Cosmos DB también admite la importación de datos desde el [Emulador de Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="10ef7-261">The Azure Cosmos DB Data Import Tool also supports import of data from the [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="10ef7-262">Al importar datos desde un emulador local, establezca el punto de conexión en `https://localhost:<port>`.</span><span class="sxs-lookup"><span data-stu-id="10ef7-262">When importing data from a local emulator, set the endpoint to `https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="10ef7-263"><a id="HBaseSource"></a>Para importar desde HBase</span><span class="sxs-lookup"><span data-stu-id="10ef7-263"><a id="HBaseSource"></a>To import from HBase</span></span>
<span data-ttu-id="10ef7-264">La opción del importador de origen de HBase le permite importar datos de una tabla HBase y, opcionalmente, filtrar los datos.</span><span class="sxs-lookup"><span data-stu-id="10ef7-264">The HBase source importer option allows you to import data from an HBase table and optionally filter the data.</span></span> <span data-ttu-id="10ef7-265">Se proporcionan varias plantillas para que configurar una importación resulte lo más fácil posible.</span><span class="sxs-lookup"><span data-stu-id="10ef7-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Captura de pantalla de opciones de origen de HBase](./media/import-data/hbasesource1.png)

![Captura de pantalla de opciones de origen de HBase](./media/import-data/hbasesource2.png)

<span data-ttu-id="10ef7-268">El formato de la cadena de conexión de HBase Stargate es:</span><span class="sxs-lookup"><span data-stu-id="10ef7-268">The format of the HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="10ef7-269">Use el comando Verify para asegurarse de que se puede tener acceso a la instancia de HBase especificada en el campo de la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="10ef7-269">Use the Verify command to ensure that the HBase instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="10ef7-270">A continuación se muestra un ejemplo de línea de comandos para importar desde HBase:</span><span class="sxs-lookup"><span data-stu-id="10ef7-270">Here is a command line sample to import from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="10ef7-271"><a id="DocumentDBBulkTarget"></a>Para importar a la API de DocumentDB (importación masiva)</span><span class="sxs-lookup"><span data-stu-id="10ef7-271"><a id="DocumentDBBulkTarget"></a>To import to the DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="10ef7-272">El importador masivo de Azure Cosmos DB permite importar desde cualquier opción de origen disponible con un procedimiento almacenado de Azure Cosmos DB para que resulte más eficaz.</span><span class="sxs-lookup"><span data-stu-id="10ef7-272">The Azure Cosmos DB Bulk importer allows you to import from any of the available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="10ef7-273">La herramienta admite la importación en una sola colección de Azure Cosmos DB con particiones, así como la importación con particiones por la cual los datos se dividen entre varias colecciones de Azure Cosmos DB con una única partición.</span><span class="sxs-lookup"><span data-stu-id="10ef7-273">The tool supports import to one single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="10ef7-274">Para más información sobre la creación de particiones de datos, consulte [Partición y escalado de datos en Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="10ef7-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="10ef7-275">La herramienta creará, ejecutará y eliminará el procedimiento almacenado de las colecciones de destino.</span><span class="sxs-lookup"><span data-stu-id="10ef7-275">The tool will create, execute, and then delete the stored procedure from the target collection(s).</span></span>  

![Captura de pantalla de opciones de importación masiva de Azure Cosmos DB](./media/import-data/documentdbbulk.png)

<span data-ttu-id="10ef7-277">El formato de la cadena de conexión de Azure Cosmos DB es:</span><span class="sxs-lookup"><span data-stu-id="10ef7-277">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="10ef7-278">La cadena de conexión de la cuenta de Azure Cosmos DB se puede obtener en la hoja Claves de Azure Portal, como se describe en [Administración de una cuenta de Azure Cosmos DB](manage-account.md); sin embargo, el nombre de la base de datos se debe anexar a la cadena de conexión con el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="10ef7-278">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="10ef7-279">Use el comando Verify para asegurarse de que se puede tener acceso a la instancia de Azure Cosmos DB especificada en el campo de la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="10ef7-279">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="10ef7-280">Para realizar la importación en una sola colección, escriba el nombre de la colección en la que se van a importar los datos y haga clic en el botón Agregar.</span><span class="sxs-lookup"><span data-stu-id="10ef7-280">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="10ef7-281">Para importar en varias colecciones, escriba el nombre de cada colección individualmente o use la siguiente sintaxis para especificar varias colecciones: *collection_prefix*[índice inicial - índice final].</span><span class="sxs-lookup"><span data-stu-id="10ef7-281">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="10ef7-282">Si va a especificar varias colecciones a través de esta sintaxis, tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="10ef7-282">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="10ef7-283">Solo se admiten patrones de nombre de intervalo entero.</span><span class="sxs-lookup"><span data-stu-id="10ef7-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="10ef7-284">Por ejemplo, la especificación de colección [0-3] generará las siguientes colecciones: colección0, colección1, colección2, colección3.</span><span class="sxs-lookup"><span data-stu-id="10ef7-284">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="10ef7-285">Puede usar una sintaxis abreviada: colección[3] generará el mismo conjunto de colecciones que el paso 1.</span><span class="sxs-lookup"><span data-stu-id="10ef7-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="10ef7-286">Se pueden proporcionar varias sustituciones.</span><span class="sxs-lookup"><span data-stu-id="10ef7-286">More than one substitution can be provided.</span></span> <span data-ttu-id="10ef7-287">Por ejemplo, colección[0-1] [0-9] 20 nombres de colección con ceros delante (colección01,... 02... 03).</span><span class="sxs-lookup"><span data-stu-id="10ef7-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="10ef7-288">Una vez especificados los nombres de las colecciones, elija la capacidad de proceso deseada de la colección (de 400 RU a 10 000 RU).</span><span class="sxs-lookup"><span data-stu-id="10ef7-288">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 10,000 RUs).</span></span> <span data-ttu-id="10ef7-289">Para conseguir el mejor rendimiento en la importación, elija una mayor capacidad de proceso.</span><span class="sxs-lookup"><span data-stu-id="10ef7-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="10ef7-290">Para más información sobre los niveles de rendimiento, consulte [Niveles de rendimiento en Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="10ef7-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="10ef7-291">La configuración del nivel de rendimiento solo se aplica a la creación de la colección.</span><span class="sxs-lookup"><span data-stu-id="10ef7-291">The performance throughput setting only applies to collection creation.</span></span> <span data-ttu-id="10ef7-292">Si la colección especificada ya existe, no se modificará su capacidad de proceso.</span><span class="sxs-lookup"><span data-stu-id="10ef7-292">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="10ef7-293">Cuando se importa a varias colecciones, la herramienta de importación admite el particionamiento basado en hash.</span><span class="sxs-lookup"><span data-stu-id="10ef7-293">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="10ef7-294">En este escenario, especifique la propiedad de documento que desea utilizar como clave de partición (si el valor de Clave de partición se deja en blanco, los documentos se particionarán aleatoriamente entre las colecciones de destino).</span><span class="sxs-lookup"><span data-stu-id="10ef7-294">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="10ef7-295">También puede especificar qué campo del origen de importación debe utilizarse como la propiedad de identificador de documentos Azure Cosmos DB durante la importación (tenga en cuenta que si los documentos no contienen esta propiedad, a continuación, la herramienta de importación generará un GUID como el valor de la propiedad del identificador).</span><span class="sxs-lookup"><span data-stu-id="10ef7-295">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="10ef7-296">Hay una serie de opciones avanzadas disponibles durante la importación.</span><span class="sxs-lookup"><span data-stu-id="10ef7-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="10ef7-297">En primer lugar, mientras que la herramienta incluye un procedimiento predeterminado almacenado de importación masiva (BulkInsert.js), puede especificar su propio procedimiento almacenado de importación:</span><span class="sxs-lookup"><span data-stu-id="10ef7-297">First, while the tool includes a default bulk import stored procedure (BulkInsert.js), you may choose to specify your own import stored procedure:</span></span>

 ![Captura de pantalla de opciones de importación de insert sproc masiva de Azure Cosmos DB](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="10ef7-299">Además, al importar los tipos de fecha (por ejemplo, desde SQL Server o MongoDB), puede elegir entre tres opciones de importación:</span><span class="sxs-lookup"><span data-stu-id="10ef7-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Captura de pantalla de opciones de importación de fecha y hora de Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="10ef7-301">Cadena: conservar como un valor de cadena</span><span class="sxs-lookup"><span data-stu-id="10ef7-301">String: Persist as a string value</span></span>
* <span data-ttu-id="10ef7-302">Tiempo: conservar como un valor de número de tiempo</span><span class="sxs-lookup"><span data-stu-id="10ef7-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="10ef7-303">Ambos: conservar los valores de cadena y de número </span><span class="sxs-lookup"><span data-stu-id="10ef7-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="10ef7-304">Esta opción creará un subdocumento, por ejemplo "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="10ef7-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="10ef7-305">El importador masivo de Azure Cosmos DB tiene las siguientes opciones avanzadas adicionales:</span><span class="sxs-lookup"><span data-stu-id="10ef7-305">The Azure Cosmos DB Bulk importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="10ef7-306">Tamaño del lote: el tamaño de lote predeterminado de la herramienta es 50.</span><span class="sxs-lookup"><span data-stu-id="10ef7-306">Batch Size: The tool defaults to a batch size of 50.</span></span>  <span data-ttu-id="10ef7-307">Si los documentos que desea importar son grandes, considere la posibilidad de reducir el tamaño del lote.</span><span class="sxs-lookup"><span data-stu-id="10ef7-307">If the documents to be imported are large, consider lowering the batch size.</span></span> <span data-ttu-id="10ef7-308">Si los documentos que desea importar son pequeños, considere la posibilidad de aumentar el tamaño del lote.</span><span class="sxs-lookup"><span data-stu-id="10ef7-308">Conversely, if the documents to be imported are small, consider raising the batch size.</span></span>
2. <span data-ttu-id="10ef7-309">Tamaño máximo de script (bytes): el valor predeterminado máximo del script en la herramienta es de 512 KB.</span><span class="sxs-lookup"><span data-stu-id="10ef7-309">Max Script Size (bytes): The tool defaults to a max script size of 512KB</span></span>
3. <span data-ttu-id="10ef7-310">Deshabilitar generación de Id. automática: si cada documento que se va a importar contiene un campo de Id., seleccione esta opción para aumentar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="10ef7-310">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="10ef7-311">No se importarán los documentos  que no contengan el campo de identificador exclusivo.</span><span class="sxs-lookup"><span data-stu-id="10ef7-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="10ef7-312">Actualización de documentos existentes: la opción predeterminada es no reemplazar los documentos existentes por conflictos de identificador.</span><span class="sxs-lookup"><span data-stu-id="10ef7-312">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="10ef7-313">Si selecciona esta opción, permitirá que se sobrescriban los documentos existentes con identificadores que coinciden entre sí.</span><span class="sxs-lookup"><span data-stu-id="10ef7-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="10ef7-314">Esta característica es útil para las migraciones de datos programadas que actualizan los documentos existentes.</span><span class="sxs-lookup"><span data-stu-id="10ef7-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="10ef7-315">Número de reintentos en caso de error: especifica el número de veces que se intentará la conexión a Azure Cosmos DB en caso de errores transitorios (por ejemplo, interrupciones de conectividad de red).</span><span class="sxs-lookup"><span data-stu-id="10ef7-315">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="10ef7-316">Intervalo de reintento: especifica el tiempo de espera entre los reintentos de restablecimiento de conexión a Azure Cosmos DB en caso de errores transitorios (por ejemplo, interrupción de la conectividad de red).</span><span class="sxs-lookup"><span data-stu-id="10ef7-316">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="10ef7-317">Modo de conexión: especifica el modo de conexión para utilizar con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="10ef7-317">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="10ef7-318">Las opciones disponibles son DirectTcp, DirectHttps y puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="10ef7-318">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="10ef7-319">Los modos de conexión directa son más rápidos, mientras que el modo de puerta de enlace es compatible con el firewall, ya que sólo usa el puerto 443.</span><span class="sxs-lookup"><span data-stu-id="10ef7-319">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Captura de pantalla de opciones avanzadas de importación masiva de Azure Cosmos DB](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="10ef7-321">El modo de conexión predeterminado de la herramienta de importación es DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="10ef7-321">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="10ef7-322">Si experimenta problemas de firewall, cambie al modo de conexión puerta de enlace, ya que sólo requiere el puerto 443.</span><span class="sxs-lookup"><span data-stu-id="10ef7-322">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="10ef7-323"><a id="DocumentDBSeqTarget"></a>Para importar a la API de DocumentDB (importación de registros secuenciales)</span><span class="sxs-lookup"><span data-stu-id="10ef7-323"><a id="DocumentDBSeqTarget"></a>To import to the DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="10ef7-324">El importador de registros secuenciales de Azure Cosmos DB permite importar desde cualquiera de las opciones de origen disponibles según cada registro.</span><span class="sxs-lookup"><span data-stu-id="10ef7-324">The Azure Cosmos DB sequential record importer allows you to import from any of the available source options on a record by record basis.</span></span> <span data-ttu-id="10ef7-325">Puede elegir esta opción si va a importar a una colección existente que ha alcanzado su cuota de procedimientos almacenados.</span><span class="sxs-lookup"><span data-stu-id="10ef7-325">You might choose this option if you’re importing to an existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="10ef7-326">La herramienta admite la importación en una única colección de Azure Cosmos DB (de una o varias particiones), así como la importación con particiones por la cual los datos se dividen entre varias colecciones de Azure Cosmos DB de una o varias particiones.</span><span class="sxs-lookup"><span data-stu-id="10ef7-326">The tool supports import to a single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="10ef7-327">Para más información sobre la creación de particiones de datos, consulte [Partición y escalado de datos en Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="10ef7-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Captura de pantalla de opciones de importación de registros secuenciales de Azure Cosmos DB](./media/import-data/documentdbsequential.png)

<span data-ttu-id="10ef7-329">El formato de la cadena de conexión de Azure Cosmos DB es:</span><span class="sxs-lookup"><span data-stu-id="10ef7-329">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="10ef7-330">La cadena de conexión de la cuenta de Azure Cosmos DB se puede obtener en la hoja Claves de Azure Portal, como se describe en [Administración de una cuenta de Azure Cosmos DB](manage-account.md); sin embargo, el nombre de la base de datos se debe anexar a la cadena de conexión con el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="10ef7-330">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="10ef7-331">Use el comando Verify para asegurarse de que se puede tener acceso a la instancia de Azure Cosmos DB especificada en el campo de la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="10ef7-331">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="10ef7-332">Para realizar la importación en una sola colección, escriba el nombre de la colección en la que se van a importar los datos y haga clic en el botón Agregar.</span><span class="sxs-lookup"><span data-stu-id="10ef7-332">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="10ef7-333">Para importar en varias colecciones, escriba el nombre de cada colección individualmente o use la siguiente sintaxis para especificar varias colecciones: *collection_prefix*[índice inicial - índice final].</span><span class="sxs-lookup"><span data-stu-id="10ef7-333">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="10ef7-334">Si va a especificar varias colecciones a través de esta sintaxis, tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="10ef7-334">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="10ef7-335">Solo se admiten patrones de nombre de intervalo entero.</span><span class="sxs-lookup"><span data-stu-id="10ef7-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="10ef7-336">Por ejemplo, la especificación de colección [0-3] generará las siguientes colecciones: colección0, colección1, colección2, colección3.</span><span class="sxs-lookup"><span data-stu-id="10ef7-336">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="10ef7-337">Puede usar una sintaxis abreviada: colección[3] generará el mismo conjunto de colecciones que el paso 1.</span><span class="sxs-lookup"><span data-stu-id="10ef7-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="10ef7-338">Se pueden proporcionar varias sustituciones.</span><span class="sxs-lookup"><span data-stu-id="10ef7-338">More than one substitution can be provided.</span></span> <span data-ttu-id="10ef7-339">Por ejemplo, colección[0-1] [0-9] 20 nombres de colección con ceros delante (colección01,... 02... 03).</span><span class="sxs-lookup"><span data-stu-id="10ef7-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="10ef7-340">Una vez especificados los nombres de las colecciones, elija la capacidad de proceso deseada de la colección (de 400 RU a 250 000 RU).</span><span class="sxs-lookup"><span data-stu-id="10ef7-340">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 250,000 RUs).</span></span> <span data-ttu-id="10ef7-341">Para conseguir el mejor rendimiento en la importación, elija una mayor capacidad de proceso.</span><span class="sxs-lookup"><span data-stu-id="10ef7-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="10ef7-342">Para más información sobre los niveles de rendimiento, consulte [Niveles de rendimiento en Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="10ef7-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="10ef7-343">Cualquier importación a colecciones con una capacidad de proceso de >10 000 RU requerirá una clave de partición.</span><span class="sxs-lookup"><span data-stu-id="10ef7-343">Any import to collections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="10ef7-344">Si elige tener más de 250 000 RU, debe registrar una solicitud en el portal para que le aumenten su cuenta.</span><span class="sxs-lookup"><span data-stu-id="10ef7-344">If you choose to have more than 250,000 RUs, you will need to file a request in the portal to have your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="10ef7-345">La configuración de la capacidad de proceso solo se aplica a la creación de colecciones.</span><span class="sxs-lookup"><span data-stu-id="10ef7-345">The throughput setting only applies to collection creation.</span></span> <span data-ttu-id="10ef7-346">Si la colección especificada ya existe, no se modificará su capacidad de proceso.</span><span class="sxs-lookup"><span data-stu-id="10ef7-346">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="10ef7-347">Cuando se importa a varias colecciones, la herramienta de importación admite el particionamiento basado en hash.</span><span class="sxs-lookup"><span data-stu-id="10ef7-347">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="10ef7-348">En este escenario, especifique la propiedad de documento que desea utilizar como clave de partición (si el valor de Clave de partición se deja en blanco, los documentos se particionarán aleatoriamente entre las colecciones de destino).</span><span class="sxs-lookup"><span data-stu-id="10ef7-348">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="10ef7-349">También puede especificar qué campo del origen de importación debe utilizarse como la propiedad de identificador de documentos Azure Cosmos DB durante la importación (tenga en cuenta que si los documentos no contienen esta propiedad, a continuación, la herramienta de importación generará un GUID como el valor de la propiedad del identificador).</span><span class="sxs-lookup"><span data-stu-id="10ef7-349">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="10ef7-350">Hay una serie de opciones avanzadas disponibles durante la importación.</span><span class="sxs-lookup"><span data-stu-id="10ef7-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="10ef7-351">En primer lugar, al importar los tipos de fecha (por ejemplo, desde SQL Server o MongoDB), puede elegir entre tres opciones de importación:</span><span class="sxs-lookup"><span data-stu-id="10ef7-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Captura de pantalla de opciones de importación de fecha y hora de Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="10ef7-353">Cadena: conservar como un valor de cadena</span><span class="sxs-lookup"><span data-stu-id="10ef7-353">String: Persist as a string value</span></span>
* <span data-ttu-id="10ef7-354">Tiempo: conservar como un valor de número de tiempo</span><span class="sxs-lookup"><span data-stu-id="10ef7-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="10ef7-355">Ambos: conservar los valores de cadena y de número </span><span class="sxs-lookup"><span data-stu-id="10ef7-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="10ef7-356">Esta opción creará un subdocumento, por ejemplo "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="10ef7-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="10ef7-357">El importador de registros secuenciales de Azure Cosmos DB tiene estas opciones avanzadas adicionales:</span><span class="sxs-lookup"><span data-stu-id="10ef7-357">The Azure Cosmos DB - Sequential record importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="10ef7-358">Número de solicitudes paralelas: la opción predeterminada es 2.</span><span class="sxs-lookup"><span data-stu-id="10ef7-358">Number of Parallel Requests: The tool defaults to 2 parallel requests.</span></span> <span data-ttu-id="10ef7-359">Si los documentos que desea importar son pequeños, considere la posibilidad de aumentar el número de solicitudes paralelas.</span><span class="sxs-lookup"><span data-stu-id="10ef7-359">If the documents to be imported are small, consider raising the number of parallel requests.</span></span> <span data-ttu-id="10ef7-360">Tenga en cuenta que si este número es demasiado elevado, podrá haber limitaciones en la importación.</span><span class="sxs-lookup"><span data-stu-id="10ef7-360">Note that if this number is raised too much, the import may experience throttling.</span></span>
2. <span data-ttu-id="10ef7-361">Deshabilitar generación de Id. automática: si cada documento que se va a importar contiene un campo de Id., seleccione esta opción para aumentar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="10ef7-361">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="10ef7-362">No se importarán los documentos  que no contengan el campo de identificador exclusivo.</span><span class="sxs-lookup"><span data-stu-id="10ef7-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="10ef7-363">Actualización de documentos existentes: la opción predeterminada es no reemplazar los documentos existentes por conflictos de identificador.</span><span class="sxs-lookup"><span data-stu-id="10ef7-363">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="10ef7-364">Si selecciona esta opción, permitirá que se sobrescriban los documentos existentes con identificadores que coinciden entre sí.</span><span class="sxs-lookup"><span data-stu-id="10ef7-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="10ef7-365">Esta característica es útil para las migraciones de datos programadas que actualizan los documentos existentes.</span><span class="sxs-lookup"><span data-stu-id="10ef7-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="10ef7-366">Número de reintentos en caso de error: especifica el número de veces que se intentará la conexión a Azure Cosmos DB en caso de errores transitorios (por ejemplo, interrupciones de conectividad de red).</span><span class="sxs-lookup"><span data-stu-id="10ef7-366">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="10ef7-367">Intervalo de reintento: especifica el tiempo de espera entre los reintentos de restablecimiento de conexión a Azure Cosmos DB en caso de errores transitorios (por ejemplo, interrupción de la conectividad de red).</span><span class="sxs-lookup"><span data-stu-id="10ef7-367">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="10ef7-368">Modo de conexión: especifica el modo de conexión para utilizar con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="10ef7-368">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="10ef7-369">Las opciones disponibles son DirectTcp, DirectHttps y puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="10ef7-369">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="10ef7-370">Los modos de conexión directa son más rápidos, mientras que el modo de puerta de enlace es compatible con el firewall, ya que sólo usa el puerto 443.</span><span class="sxs-lookup"><span data-stu-id="10ef7-370">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Captura de pantalla de opciones avanzadas de importación de registros secuenciales de Azure Cosmos DB](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="10ef7-372">El modo de conexión predeterminado de la herramienta de importación es DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="10ef7-372">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="10ef7-373">Si experimenta problemas de firewall, cambie al modo de conexión puerta de enlace, ya que sólo requiere el puerto 443.</span><span class="sxs-lookup"><span data-stu-id="10ef7-373">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="10ef7-374"><a id="IndexingPolicy"></a>Especificar una directiva de indexación al crear colecciones de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="10ef7-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="10ef7-375">Si permite que la herramienta de migración cree colecciones durante la importación, puede especificar la directiva de indización de las colecciones.</span><span class="sxs-lookup"><span data-stu-id="10ef7-375">When you allow the migration tool to create collections during import, you can specify the indexing policy of the collections.</span></span> <span data-ttu-id="10ef7-376">En la sección de opciones avanzadas de las opciones de Importación masiva de Azure Cosmos DB y Registro secuencial de Azure Cosmos DB, vaya a la sección de la directiva de indexación.</span><span class="sxs-lookup"><span data-stu-id="10ef7-376">In the advanced options section of the Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate to the Indexing Policy section.</span></span>

![Captura de pantalla de opciones avanzadas de política de indexación de Azure Cosmos DB](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="10ef7-378">Mediante la opción avanzada de Directiva de indización, puede seleccionar un archivo de directiva de indización, especificar manualmente una directiva de indización o seleccionar de un conjunto de plantillas predeterminadas (haciendo clic con el botón derecho en el cuadro de texto de la directiva de indización).</span><span class="sxs-lookup"><span data-stu-id="10ef7-378">Using the Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in the indexing policy textbox).</span></span>

<span data-ttu-id="10ef7-379">La herramienta proporciona las plantillas de directiva siguientes:</span><span class="sxs-lookup"><span data-stu-id="10ef7-379">The policy templates the tool provides are:</span></span>

* <span data-ttu-id="10ef7-380">Predeterminada.</span><span class="sxs-lookup"><span data-stu-id="10ef7-380">Default.</span></span> <span data-ttu-id="10ef7-381">Esta directiva es mejor cuando se realizan consultas de igualdad en cadenas y se usan consultas ORDER BY, de rango y de igualdad para números.</span><span class="sxs-lookup"><span data-stu-id="10ef7-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="10ef7-382">Esta directiva tiene una sobrecarga de almacenamiento de índices menor que la de intervalo.</span><span class="sxs-lookup"><span data-stu-id="10ef7-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="10ef7-383">Intervalo.</span><span class="sxs-lookup"><span data-stu-id="10ef7-383">Range.</span></span> <span data-ttu-id="10ef7-384">Esta directiva es mejor si está usando consultas de ORDER BY, intervalo e igualdad en números y cadenas.</span><span class="sxs-lookup"><span data-stu-id="10ef7-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="10ef7-385">Esta directiva tiene una mayor sobrecarga de almacenamiento de índice que la Predeterminada o Hash.</span><span class="sxs-lookup"><span data-stu-id="10ef7-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Captura de pantalla de opciones avanzadas de política de indexación de Azure Cosmos DB](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="10ef7-387">Si no especifica una directiva de indización, se aplicará la directiva predeterminada.</span><span class="sxs-lookup"><span data-stu-id="10ef7-387">If you do not specify an indexing policy, then the default policy will be applied.</span></span> <span data-ttu-id="10ef7-388">Para más información sobre las directivas de indexación, consulte [Directivas de indexación de Azure Cosmos DB](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="10ef7-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-to-json-file"></a><span data-ttu-id="10ef7-389">Exportación a archivos JSON</span><span class="sxs-lookup"><span data-stu-id="10ef7-389">Export to JSON file</span></span>
<span data-ttu-id="10ef7-390">El exportador JSON de Azure Cosmos DB permite exportar cualquiera de las opciones de origen disponibles a un archivo JSON que contiene una matriz de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="10ef7-390">The Azure Cosmos DB JSON exporter allows you to export any of the available source options to a JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="10ef7-391">La herramienta controlará la exportación por usted, o puede ver el comando resultante de la migración y ejecutar el comando usted mismo.</span><span class="sxs-lookup"><span data-stu-id="10ef7-391">The tool will handle the export for you, or you can choose to view the resulting migration command and run the command yourself.</span></span> <span data-ttu-id="10ef7-392">El archivo JSON resultante puede almacenarse localmente o en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="10ef7-392">The resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Captura de pantalla de opción de exportación de archivo local JSON de Azure Cosmos DB](./media/import-data/jsontarget.png)

![Captura de pantalla de opción de exportación de Azure Blob Storage de JSON de Azure Cosmos DB](./media/import-data/jsontarget2.png)

<span data-ttu-id="10ef7-395">Opcionalmente, puede optar por adornar el JSON resultante, lo que aumentará el tamaño del documento resultante al mismo tiempo que el contenido será más legibles.</span><span class="sxs-lookup"><span data-stu-id="10ef7-395">You may optionally choose to prettify the resulting JSON, which will increase the size of the resulting document while making the contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places to see in Paris"}]}]

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
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places to see in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a><span data-ttu-id="10ef7-396">Configuración avanzada</span><span class="sxs-lookup"><span data-stu-id="10ef7-396">Advanced configuration</span></span>
<span data-ttu-id="10ef7-397">En la pantalla Configuración avanzada, especifique la ubicación del archivo de registro en que desee que se escriban los errores.</span><span class="sxs-lookup"><span data-stu-id="10ef7-397">In the Advanced configuration screen, specify the location of the log file to which you would like any errors written.</span></span> <span data-ttu-id="10ef7-398">Las siguientes reglas se aplican a esta página:</span><span class="sxs-lookup"><span data-stu-id="10ef7-398">The following rules apply to this page:</span></span>

1. <span data-ttu-id="10ef7-399">Si no se proporciona un nombre de archivo, todos los errores se devolverán a la página de resultados.</span><span class="sxs-lookup"><span data-stu-id="10ef7-399">If a file name is not provided, then all errors will be returned on the Results page.</span></span>
2. <span data-ttu-id="10ef7-400">Si se proporciona un nombre de archivo sin un directorio, el archivo se creará (o sobrescribirá) en el directorio del entorno actual.</span><span class="sxs-lookup"><span data-stu-id="10ef7-400">If a file name is provided without a directory, then the file will be created (or overwritten) in the current environment directory.</span></span>
3. <span data-ttu-id="10ef7-401">Si selecciona un archivo existente, este se sobrescribirá, ya que no hay opción de anexar.</span><span class="sxs-lookup"><span data-stu-id="10ef7-401">If you select an existing file, then the file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="10ef7-402">A continuación, elija si desea registrar todos los mensajes de error, los críticos o ninguno.</span><span class="sxs-lookup"><span data-stu-id="10ef7-402">Then, choose whether to log all, critical, or no error messages.</span></span> <span data-ttu-id="10ef7-403">Por último, decida con qué frecuencia se actualizará el progreso en el mensaje de transferencia en pantalla.</span><span class="sxs-lookup"><span data-stu-id="10ef7-403">Finally, decide how frequently the on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="10ef7-404">Confirmación de las opciones de importación y visualización de la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="10ef7-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="10ef7-405">Después de especificar la información de origen y destino, y la configuración avanzada, revise el resumen de la migración y, opcionalmente, vea o copie el comando resultante de la migración (copiar el comando es útil para automatizar las operaciones de importación):</span><span class="sxs-lookup"><span data-stu-id="10ef7-405">After specifying source information, target information, and advanced configuration, review the migration summary and, optionally, view/copy the resulting migration command (copying the command is useful to automate import operations):</span></span>
   
    ![Screenshot of summary screen](./media/import-data/summary.png)
   
    ![Screenshot of summary screen](./media/import-data/summarycommand.png)
2. <span data-ttu-id="10ef7-408">Una vez que esté satisfecho con las opciones de origen y de destino, haga clic en **Importar**.</span><span class="sxs-lookup"><span data-stu-id="10ef7-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="10ef7-409">El tiempo transcurrido, el número transferido y la información sobre los errores (si no se ha especificado un nombre de archivo en la configuración avanzada) se actualizarán mientras la importación está curso.</span><span class="sxs-lookup"><span data-stu-id="10ef7-409">The elapsed time, transferred count, and failure information (if you didn't provide a file name in the Advanced configuration) will update as the import is in process.</span></span> <span data-ttu-id="10ef7-410">Una vez que haya finalizado, puede exportar los resultados (por ejemplo, para tratar los errores de importación).</span><span class="sxs-lookup"><span data-stu-id="10ef7-410">Once complete, you can export the results (e.g. to deal with any import failures).</span></span>
   
    ![Captura de pantalla de opción de exportación de JSON de Azure Cosmos DB](./media/import-data/viewresults.png)
3. <span data-ttu-id="10ef7-412">También puede iniciar una nueva importación, conservando la configuración existente (por ejemplo, elección de información de origen y de destino de la cadena de conexión, etc.) o restableciendo todos los valores.</span><span class="sxs-lookup"><span data-stu-id="10ef7-412">You may also start a new import, either keeping the existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Captura de pantalla de opción de exportación de JSON de Azure Cosmos DB](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="10ef7-414">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="10ef7-414">Next steps</span></span>

<span data-ttu-id="10ef7-415">En este tutorial, ha hecho lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="10ef7-415">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="10ef7-416">Instalación de la herramienta de migración de datos</span><span class="sxs-lookup"><span data-stu-id="10ef7-416">Installed the Data Migration tool</span></span>
> * <span data-ttu-id="10ef7-417">Importación de datos de orígenes de datos diferentes</span><span class="sxs-lookup"><span data-stu-id="10ef7-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="10ef7-418">Exportación desde Azure Cosmos DB a JSON</span><span class="sxs-lookup"><span data-stu-id="10ef7-418">Exported from Azure Cosmos DB to JSON</span></span>

<span data-ttu-id="10ef7-419">Ahora puede pasar al siguiente tutorial y obtener más información sobre cómo consultar los datos con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="10ef7-419">You can now proceed to the next tutorial and learn how to query data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="10ef7-420">Consulta de datos</span><span class="sxs-lookup"><span data-stu-id="10ef7-420">How to query data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
