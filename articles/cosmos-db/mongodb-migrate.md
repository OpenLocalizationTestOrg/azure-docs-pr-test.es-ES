---
title: Usar mongoimport y mongorestore con la API de Azure Cosmos DB para MongoDB | Microsoft Docs
description: "Obtenga información sobre cómo usar mongoimport y mongorestore para importar datos a una API para la cuenta de MongoDB"
keywords: mongoimport, mongorestore
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 1555f13c3ea88b61be0ea240b51218b83f6f9724
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-import-mongodb-data"></a><span data-ttu-id="5dba0-104">Azure Cosmos DB: importar datos de MongoDB</span><span class="sxs-lookup"><span data-stu-id="5dba0-104">Azure Cosmos DB: Import MongoDB data</span></span> 

<span data-ttu-id="5dba0-105">Para migrar datos de MongoDB a una cuenta de Azure Cosmos DB para su uso con la API de MongoDB, debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5dba0-105">To migrate data from MongoDB to an Azure Cosmos DB account for use with the API for MongoDB, you must:</span></span>

* <span data-ttu-id="5dba0-106">Descargar *mongoimport.exe* o *mongorestore.exe* desde el [centro de descarga de MongoDB](https://www.mongodb.com/download-center).</span><span class="sxs-lookup"><span data-stu-id="5dba0-106">Download either *mongoimport.exe* or *mongorestore.exe* from the [MongoDB Download Center](https://www.mongodb.com/download-center).</span></span>
* <span data-ttu-id="5dba0-107">Obtenga su [cadena de conexión de la API de MongoDB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="5dba0-107">Get your [API for MongoDB connection string](connect-mongodb-account.md).</span></span>

<span data-ttu-id="5dba0-108">Si está importando datos de MongoDB y planea usarlos con Azure Cosmos DB, debe usar la [Herramienta de migración de datos](import-data.md) para importarlos.</span><span class="sxs-lookup"><span data-stu-id="5dba0-108">If you are importing data from MongoDB and plan to use it with the Azure Cosmos DB, you should use the [Data Migration tool](import-data.md) to import data.</span></span>

<span data-ttu-id="5dba0-109">En este tutorial se describen las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="5dba0-109">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5dba0-110">Recuperación de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="5dba0-110">Retrieving your connection string</span></span>
> * <span data-ttu-id="5dba0-111">Importación de datos de MongoDB mediante mongoimport</span><span class="sxs-lookup"><span data-stu-id="5dba0-111">Importing MongoDB data by using mongoimport</span></span>
> * <span data-ttu-id="5dba0-112">Importación de datos de MongoDB mediante mongorestore</span><span class="sxs-lookup"><span data-stu-id="5dba0-112">Importing MongoDB data by using mongorestore</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5dba0-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5dba0-113">Prerequisites</span></span>

* <span data-ttu-id="5dba0-114">Aumente el rendimiento: la duración de la migración de datos depende de la cantidad de rendimiento configurado para las colecciones.</span><span class="sxs-lookup"><span data-stu-id="5dba0-114">Increase throughput: The duration of your data migration depends on the amount of throughput you set up for your collections.</span></span> <span data-ttu-id="5dba0-115">Asegúrese de aumentar el rendimiento para migraciones de datos más grandes.</span><span class="sxs-lookup"><span data-stu-id="5dba0-115">Be sure to increase the throughput for larger data migrations.</span></span> <span data-ttu-id="5dba0-116">Después de haber completado la migración, reduzca el rendimiento para ahorrar costos.</span><span class="sxs-lookup"><span data-stu-id="5dba0-116">After you've completed the migration, decrease the throughput to save costs.</span></span> <span data-ttu-id="5dba0-117">Para más información sobre cómo aumentar el rendimiento en [Azure Portal](https://portal.azure.com), consulte [Niveles de rendimiento y planes de tarifa de Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="5dba0-117">For more information about increasing throughput in the [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in Azure Cosmos DB](performance-levels.md).</span></span>

* <span data-ttu-id="5dba0-118">Habilite SSL: Azure Cosmos DB tiene estrictos estándares y requisitos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="5dba0-118">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="5dba0-119">No olvide habilitar SSL al interactuar con la cuenta.</span><span class="sxs-lookup"><span data-stu-id="5dba0-119">Be sure to enable SSL when you interact with your account.</span></span> <span data-ttu-id="5dba0-120">Los procedimientos del resto del artículo incluyen cómo habilitar SSL para mongoimport y mongorestore.</span><span class="sxs-lookup"><span data-stu-id="5dba0-120">The procedures in the rest of the article include how to enable SSL for mongoimport and mongorestore.</span></span>

## <a name="find-your-connection-string-information-host-port-username-and-password"></a><span data-ttu-id="5dba0-121">Búsqueda de la información de la cadena de conexión (host, puerto, nombre de usuario y contraseña)</span><span class="sxs-lookup"><span data-stu-id="5dba0-121">Find your connection string information (host, port, username, and password)</span></span>

1. <span data-ttu-id="5dba0-122">En [Azure Portal](https://portal.azure.com), en el panel izquierdo, haga clic en la entrada **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="5dba0-122">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Cosmos DB** entry.</span></span>
2. <span data-ttu-id="5dba0-123">En el panel **Suscripciones**, seleccione el nombre de cuenta.</span><span class="sxs-lookup"><span data-stu-id="5dba0-123">In the **Subscriptions** pane, select your account name.</span></span>
3. <span data-ttu-id="5dba0-124">En la hoja **Cadena de conexión**, haga clic en **Cadena de conexión**.</span><span class="sxs-lookup"><span data-stu-id="5dba0-124">In the **Connection String** blade, click **Connection String**.</span></span>  
<span data-ttu-id="5dba0-125">El panel derecho contiene toda la información que necesita para conectarse correctamente a la cuenta.</span><span class="sxs-lookup"><span data-stu-id="5dba0-125">The right pane contains all the information that you need to successfully connect to your account.</span></span>

    ![Hoja Cadena de conexión](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-to-the-api-for-mongodb-by-using-mongoimport"></a><span data-ttu-id="5dba0-127">Importar datos a la API para MongoDB mediante mongoimport</span><span class="sxs-lookup"><span data-stu-id="5dba0-127">Import data to the API for MongoDB by using mongoimport</span></span>

<span data-ttu-id="5dba0-128">Para importar datos a la cuenta de Azure Cosmos DB, use la plantilla siguiente.</span><span class="sxs-lookup"><span data-stu-id="5dba0-128">To import data to your Azure Cosmos DB account, use the following template.</span></span> <span data-ttu-id="5dba0-129">Rellene *host*, *nombre de usuario* y *contraseña* con los valores específicos de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="5dba0-129">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span></span>  

<span data-ttu-id="5dba0-130">Plantilla:</span><span class="sxs-lookup"><span data-stu-id="5dba0-130">Template:</span></span>

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

<span data-ttu-id="5dba0-131">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5dba0-131">Example:</span></span>  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-to-the-api-for-mongodb-by-using-mongorestore"></a><span data-ttu-id="5dba0-132">Importar datos a la API para MongoDB mediante mongorestore</span><span class="sxs-lookup"><span data-stu-id="5dba0-132">Import data to the API for MongoDB by using mongorestore</span></span>

<span data-ttu-id="5dba0-133">Para restaurar datos en la cuenta de la API para MongoDB, utilice la siguiente plantilla para ejecutar la importación.</span><span class="sxs-lookup"><span data-stu-id="5dba0-133">To restore data to your API for MongoDB account, use the following template to execute the import.</span></span> <span data-ttu-id="5dba0-134">Rellene *host*, *nombre de usuario* y *contraseña* con los valores específicos de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="5dba0-134">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span></span>

<span data-ttu-id="5dba0-135">Plantilla:</span><span class="sxs-lookup"><span data-stu-id="5dba0-135">Template:</span></span>

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

<span data-ttu-id="5dba0-136">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5dba0-136">Example:</span></span>

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a><span data-ttu-id="5dba0-137">Guía para una migración correcta</span><span class="sxs-lookup"><span data-stu-id="5dba0-137">Guide for a successful migration</span></span>

1. <span data-ttu-id="5dba0-138">Cree previamente las colecciones y escálelas:</span><span class="sxs-lookup"><span data-stu-id="5dba0-138">Pre-create and scale your collections:</span></span>
        
    * <span data-ttu-id="5dba0-139">De forma predeterminada, Azure Cosmos DB aprovisiona una nueva colección de MongoDB con 1000 unidades de solicitud (RU).</span><span class="sxs-lookup"><span data-stu-id="5dba0-139">By default, Azure Cosmos DB provisions a new MongoDB collection with 1,000 request units (RUs).</span></span> <span data-ttu-id="5dba0-140">Antes de empezar la migración mediante mongoimport, mongorestore o mongomirror, cree todas las colecciones mediante [Azure Portal](https://portal.azure.com) o mediante los controladores y herramientas de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5dba0-140">Before you start the migration by using mongoimport, mongorestore, or mongomirror, pre-create all your collections from the [Azure portal](https://portal.azure.com) or from MongoDB drivers and tools.</span></span> <span data-ttu-id="5dba0-141">Si la colección supera los 10 GB, asegúrese de crear una [colección con particiones](partition-data.md) con una clave de partición adecuada.</span><span class="sxs-lookup"><span data-stu-id="5dba0-141">If your collection is greater than 10 GB, make sure to create a [sharded/partitioned collection](partition-data.md) with an appropriate shard key.</span></span>

    * <span data-ttu-id="5dba0-142">En [Azure Portal](https://portal.azure.com), aumente el valor de rendimiento de las colecciones de 1000 RU para una colección con una sola partición y 2500 RU para una colección con particiones simplemente para la migración.</span><span class="sxs-lookup"><span data-stu-id="5dba0-142">From the [Azure portal](https://portal.azure.com), increase your collections' throughput from 1,000 RUs for a single partition collection and 2,500 RUs for a sharded collection just for the migration.</span></span> <span data-ttu-id="5dba0-143">Gracias al mayor rendimiento, puede evitar la limitación y realizar la migración en menos tiempo.</span><span class="sxs-lookup"><span data-stu-id="5dba0-143">With the higher throughput, you can avoid throttling and migrate in less time.</span></span> <span data-ttu-id="5dba0-144">Con la facturación por horas en Azure Cosmos DB, puede reducir el rendimiento inmediatamente después de la migración para ahorrar costes.</span><span class="sxs-lookup"><span data-stu-id="5dba0-144">With hourly billing in Azure Cosmos DB, you can reduce the throughput immediately after the migration to save costs.</span></span>

2. <span data-ttu-id="5dba0-145">Calcule la carga de RU aproximada para una sola operación de escritura de documento:</span><span class="sxs-lookup"><span data-stu-id="5dba0-145">Calculate the approximate RU charge for a single document write:</span></span>

    <span data-ttu-id="5dba0-146">a.</span><span class="sxs-lookup"><span data-stu-id="5dba0-146">a.</span></span> <span data-ttu-id="5dba0-147">Conéctese a la base de datos MongoDB de Azure Cosmos DB desde el shell de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5dba0-147">Connect to your Azure Cosmos DB MongoDB database from the MongoDB Shell.</span></span> <span data-ttu-id="5dba0-148">Encontrará instrucciones en [Connect a MongoDB application to Azure Cosmos DB](connect-mongodb-account.md) (Conectar una aplicación de MongoDB a Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="5dba0-148">You can find instructions in [Connect a MongoDB application to Azure Cosmos DB](connect-mongodb-account.md).</span></span>
    
    <span data-ttu-id="5dba0-149">b.</span><span class="sxs-lookup"><span data-stu-id="5dba0-149">b.</span></span> <span data-ttu-id="5dba0-150">Ejecute un comando de inserción de ejemplo en uno de los documentos de ejemplo desde el shell de MongoDB:</span><span class="sxs-lookup"><span data-stu-id="5dba0-150">Run a sample insert command by using one of your sample documents from the MongoDB Shell:</span></span>
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    <span data-ttu-id="5dba0-151">c.</span><span class="sxs-lookup"><span data-stu-id="5dba0-151">c.</span></span> <span data-ttu-id="5dba0-152">Ejecute ```db.runCommand({getLastRequestStatistics: 1})``` y recibirá una respuesta como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="5dba0-152">Run ```db.runCommand({getLastRequestStatistics: 1})``` and you will receive a response like this one:</span></span>
     
        ```
        globaldb:PRIMARY> db.runCommand({getLastRequestStatistics: 1})
        {
            "_t": "GetRequestStatisticsResponse",
            "ok": 1,
            "CommandName": "insert",
            "RequestCharge": 10,
            "RequestDurationInMilliSeconds": NumberLong(50)
        }
        ```
        
    <span data-ttu-id="5dba0-153">d.</span><span class="sxs-lookup"><span data-stu-id="5dba0-153">d.</span></span> <span data-ttu-id="5dba0-154">Tome nota de la carga de solicitudes.</span><span class="sxs-lookup"><span data-stu-id="5dba0-154">Take note of the request charge.</span></span>
    
3. <span data-ttu-id="5dba0-155">Determine la latencia del equipo en el servicio en la nube de Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="5dba0-155">Determine the latency from your machine to the Azure Cosmos DB cloud service:</span></span>
    
    <span data-ttu-id="5dba0-156">a.</span><span class="sxs-lookup"><span data-stu-id="5dba0-156">a.</span></span> <span data-ttu-id="5dba0-157">Habilite el registro detallado desde el shell de MongoDB mediante este comando: ```setVerboseShell(true)```.</span><span class="sxs-lookup"><span data-stu-id="5dba0-157">Enable verbose logging from the MongoDB Shell by using this command: ```setVerboseShell(true)```</span></span>
    
    <span data-ttu-id="5dba0-158">b.</span><span class="sxs-lookup"><span data-stu-id="5dba0-158">b.</span></span> <span data-ttu-id="5dba0-159">Ejecute una consulta simple en la base de datos: ```db.coll.find().limit(1)```.</span><span class="sxs-lookup"><span data-stu-id="5dba0-159">Run a simple query against the database: ```db.coll.find().limit(1)```.</span></span> <span data-ttu-id="5dba0-160">Recibirá una respuesta como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="5dba0-160">You will receive a response like this one:</span></span>

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. <span data-ttu-id="5dba0-161">Quite el documento insertado antes de la migración para asegurarse de que no hay ningún documento duplicado.</span><span class="sxs-lookup"><span data-stu-id="5dba0-161">Remove the inserted document before the migration to ensure that there are no duplicate documents.</span></span> <span data-ttu-id="5dba0-162">Puede quitar los documentos con este comando: ```db.coll.remove({})```.</span><span class="sxs-lookup"><span data-stu-id="5dba0-162">You can remove documents by using this command: ```db.coll.remove({})```</span></span>

5. <span data-ttu-id="5dba0-163">Calcular los valores aproximados de *batchSize* y *numInsertionWorkers*:</span><span class="sxs-lookup"><span data-stu-id="5dba0-163">Calculate the approximate *batchSize* and *numInsertionWorkers* values:</span></span>

    * <span data-ttu-id="5dba0-164">En el caso de *batchSize*, divida el total de RU aprovisionadas entre las RU consumidas en la operación de escritura de documento del paso 3.</span><span class="sxs-lookup"><span data-stu-id="5dba0-164">For *batchSize*, divide the total provisioned RUs by the RUs consumed from your single document write in step 3.</span></span>
    
    * <span data-ttu-id="5dba0-165">Si el valor de *batchSize* calculado es <= 24, use ese número como valor de *batchSize*.</span><span class="sxs-lookup"><span data-stu-id="5dba0-165">If the calculated *batchSize* <= 24, use that number as your *batchSize* value.</span></span>
    
    * <span data-ttu-id="5dba0-166">Si el valor de *batchSize* calculado es > 24, establezca *batchSize* en 24.</span><span class="sxs-lookup"><span data-stu-id="5dba0-166">If the calculated *batchSize* > 24, set the *batchSize* value to 24.</span></span>
    
    * <span data-ttu-id="5dba0-167">En el caso de *numInsertionWorkers*, use esta ecuación: *numInsertionWorkers = (rendimiento aprovisionado * latencia en segundos) / (tamaño del lote * RU usadas en una sola operación de escritura)*.</span><span class="sxs-lookup"><span data-stu-id="5dba0-167">For *numInsertionWorkers*, use this equation:   *numInsertionWorkers =  (provisioned throughput * latency in seconds) / (batch size * consumed RUs for a single write)*.</span></span>
        
    |<span data-ttu-id="5dba0-168">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5dba0-168">Property</span></span>|<span data-ttu-id="5dba0-169">Valor</span><span class="sxs-lookup"><span data-stu-id="5dba0-169">Value</span></span>|
    |--------|-----|
    |<span data-ttu-id="5dba0-170">batchSize</span><span class="sxs-lookup"><span data-stu-id="5dba0-170">batchSize</span></span>| <span data-ttu-id="5dba0-171">24</span><span class="sxs-lookup"><span data-stu-id="5dba0-171">24</span></span> |
    |<span data-ttu-id="5dba0-172">RU aprovisionadas</span><span class="sxs-lookup"><span data-stu-id="5dba0-172">RUs provisioned</span></span> | <span data-ttu-id="5dba0-173">10000</span><span class="sxs-lookup"><span data-stu-id="5dba0-173">10000</span></span> |
    |<span data-ttu-id="5dba0-174">Latency</span><span class="sxs-lookup"><span data-stu-id="5dba0-174">Latency</span></span> | <span data-ttu-id="5dba0-175">0,100 s</span><span class="sxs-lookup"><span data-stu-id="5dba0-175">0.100 s</span></span> |
    |<span data-ttu-id="5dba0-176">RU cargadas en una sola operación de escritura de documento</span><span class="sxs-lookup"><span data-stu-id="5dba0-176">RU charged for 1 doc write</span></span> | <span data-ttu-id="5dba0-177">10 RU</span><span class="sxs-lookup"><span data-stu-id="5dba0-177">10 RUs</span></span> |
    |<span data-ttu-id="5dba0-178">numInsertionWorkers</span><span class="sxs-lookup"><span data-stu-id="5dba0-178">numInsertionWorkers</span></span> | <span data-ttu-id="5dba0-179">?</span><span class="sxs-lookup"><span data-stu-id="5dba0-179">?</span></span> |
    
    <span data-ttu-id="5dba0-180">*numInsertionWorkers = (10 000 RU x 0,1 s) / (24 x 10 RU) = 4,1666*</span><span class="sxs-lookup"><span data-stu-id="5dba0-180">*numInsertionWorkers = (10000 RUs x 0.1 s) / (24 x 10 RUs) = 4.1666*</span></span>

6. <span data-ttu-id="5dba0-181">Ejecute el comando de migración final:</span><span class="sxs-lookup"><span data-stu-id="5dba0-181">Run the final migration command:</span></span>

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a><span data-ttu-id="5dba0-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5dba0-182">Next steps</span></span>

<span data-ttu-id="5dba0-183">Puede pasar al tutorial siguiente y obtener más información sobre cómo consultar datos de MongoDB con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5dba0-183">You can proceed to the next tutorial and learn how to query MongoDB data by using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="5dba0-184">¿Cómo consultar datos de MongoDB?</span><span class="sxs-lookup"><span data-stu-id="5dba0-184">How to query MongoDB data?</span></span>](../cosmos-db/tutorial-query-mongodb.md)
