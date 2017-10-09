---
title: aaaUse mongoimport y mongorestore con hello API de base de datos de Azure Cosmos para MongoDB | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse mongoimport y mongorestore tooimport datos tooan API para la cuenta de MongoDB"
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
ms.openlocfilehash: 921354bc7b09a076a73e0cbf5e4aabcc9e83d5a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-import-mongodb-data"></a><span data-ttu-id="dd83e-104">Azure Cosmos DB: importar datos de MongoDB</span><span class="sxs-lookup"><span data-stu-id="dd83e-104">Azure Cosmos DB: Import MongoDB data</span></span> 

<span data-ttu-id="dd83e-105">toomigrate datos de MongoDB tooan cuenta de base de datos de Azure Cosmos para su uso con hello API para MongoDB, debe:</span><span class="sxs-lookup"><span data-stu-id="dd83e-105">toomigrate data from MongoDB tooan Azure Cosmos DB account for use with hello API for MongoDB, you must:</span></span>

* <span data-ttu-id="dd83e-106">Descargar cualquiera *mongoimport.exe* o *mongorestore.exe* de hello [centro de descarga de MongoDB](https://www.mongodb.com/download-center).</span><span class="sxs-lookup"><span data-stu-id="dd83e-106">Download either *mongoimport.exe* or *mongorestore.exe* from hello [MongoDB Download Center](https://www.mongodb.com/download-center).</span></span>
* <span data-ttu-id="dd83e-107">Obtenga su [cadena de conexión de la API de MongoDB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="dd83e-107">Get your [API for MongoDB connection string](connect-mongodb-account.md).</span></span>

<span data-ttu-id="dd83e-108">Si va a importar datos de MongoDB y plan toouse con hello Azure Cosmos DB, debe usar hello [herramienta de migración de datos](import-data.md) datos tooimport.</span><span class="sxs-lookup"><span data-stu-id="dd83e-108">If you are importing data from MongoDB and plan toouse it with hello Azure Cosmos DB, you should use hello [Data Migration tool](import-data.md) tooimport data.</span></span>

<span data-ttu-id="dd83e-109">Este tutorial trata Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="dd83e-109">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dd83e-110">Recuperación de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="dd83e-110">Retrieving your connection string</span></span>
> * <span data-ttu-id="dd83e-111">Importación de datos de MongoDB mediante mongoimport</span><span class="sxs-lookup"><span data-stu-id="dd83e-111">Importing MongoDB data by using mongoimport</span></span>
> * <span data-ttu-id="dd83e-112">Importación de datos de MongoDB mediante mongorestore</span><span class="sxs-lookup"><span data-stu-id="dd83e-112">Importing MongoDB data by using mongorestore</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd83e-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dd83e-113">Prerequisites</span></span>

* <span data-ttu-id="dd83e-114">Aumentar el rendimiento: duración de Hola de migración de los datos depende de la cantidad de Hola de rendimiento configurado para las colecciones.</span><span class="sxs-lookup"><span data-stu-id="dd83e-114">Increase throughput: hello duration of your data migration depends on hello amount of throughput you set up for your collections.</span></span> <span data-ttu-id="dd83e-115">Estar seguro de rendimiento de hello tooincrease para las migraciones de datos más grandes.</span><span class="sxs-lookup"><span data-stu-id="dd83e-115">Be sure tooincrease hello throughput for larger data migrations.</span></span> <span data-ttu-id="dd83e-116">Después de haber completado la migración de hello, reducir los costos de toosave de rendimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd83e-116">After you've completed hello migration, decrease hello throughput toosave costs.</span></span> <span data-ttu-id="dd83e-117">Para obtener más información sobre cómo aumentar el rendimiento en hello [portal de Azure](https://portal.azure.com), consulte [niveles de rendimiento y los niveles de precios de base de datos de Azure Cosmos](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="dd83e-117">For more information about increasing throughput in hello [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in Azure Cosmos DB](performance-levels.md).</span></span>

* <span data-ttu-id="dd83e-118">Habilite SSL: Azure Cosmos DB tiene estrictos estándares y requisitos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="dd83e-118">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="dd83e-119">Ser tooenable seguro SSL cuando se interactúa con su cuenta.</span><span class="sxs-lookup"><span data-stu-id="dd83e-119">Be sure tooenable SSL when you interact with your account.</span></span> <span data-ttu-id="dd83e-120">procedimientos de Hola de rest de Hola de artículo Hola incluyen cómo tooenable SSL para mongoimport y mongorestore.</span><span class="sxs-lookup"><span data-stu-id="dd83e-120">hello procedures in hello rest of hello article include how tooenable SSL for mongoimport and mongorestore.</span></span>

## <a name="find-your-connection-string-information-host-port-username-and-password"></a><span data-ttu-id="dd83e-121">Búsqueda de la información de la cadena de conexión (host, puerto, nombre de usuario y contraseña)</span><span class="sxs-lookup"><span data-stu-id="dd83e-121">Find your connection string information (host, port, username, and password)</span></span>

1. <span data-ttu-id="dd83e-122">Hola [portal de Azure](https://portal.azure.com), en Hola panel izquierdo, haga clic en hello **base de datos de Azure Cosmos** entrada.</span><span class="sxs-lookup"><span data-stu-id="dd83e-122">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Cosmos DB** entry.</span></span>
2. <span data-ttu-id="dd83e-123">Hola **suscripciones** panel, seleccione el nombre de cuenta.</span><span class="sxs-lookup"><span data-stu-id="dd83e-123">In hello **Subscriptions** pane, select your account name.</span></span>
3. <span data-ttu-id="dd83e-124">Hola **cadena de conexión** hoja, haga clic en **cadena de conexión**.</span><span class="sxs-lookup"><span data-stu-id="dd83e-124">In hello **Connection String** blade, click **Connection String**.</span></span>  
<span data-ttu-id="dd83e-125">Hola derecho panel contiene toda la información de Hola que necesita toosuccessfully conectar tooyour cuenta.</span><span class="sxs-lookup"><span data-stu-id="dd83e-125">hello right pane contains all hello information that you need toosuccessfully connect tooyour account.</span></span>

    ![Hoja Cadena de conexión](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a><span data-ttu-id="dd83e-127">Importar datos toohello API para MongoDB mediante mongoimport</span><span class="sxs-lookup"><span data-stu-id="dd83e-127">Import data toohello API for MongoDB by using mongoimport</span></span>

<span data-ttu-id="dd83e-128">tooimport datos tooyour cuenta de base de datos de Azure Cosmos, utilice Hola después de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="dd83e-128">tooimport data tooyour Azure Cosmos DB account, use hello following template.</span></span> <span data-ttu-id="dd83e-129">Rellene *host*, *nombre de usuario*, y *contraseña* con valores de hello cuenta tooyour específico.</span><span class="sxs-lookup"><span data-stu-id="dd83e-129">Fill in *host*, *username*, and *password* with hello values that are specific tooyour account.</span></span>  

<span data-ttu-id="dd83e-130">Plantilla:</span><span class="sxs-lookup"><span data-stu-id="dd83e-130">Template:</span></span>

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

<span data-ttu-id="dd83e-131">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dd83e-131">Example:</span></span>  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a><span data-ttu-id="dd83e-132">Importar datos toohello API para MongoDB mediante mongorestore</span><span class="sxs-lookup"><span data-stu-id="dd83e-132">Import data toohello API for MongoDB by using mongorestore</span></span>

<span data-ttu-id="dd83e-133">toorestore datos tooyour API para la cuenta de MongoDB, utilice Hola después de importar la plantilla tooexecute Hola.</span><span class="sxs-lookup"><span data-stu-id="dd83e-133">toorestore data tooyour API for MongoDB account, use hello following template tooexecute hello import.</span></span> <span data-ttu-id="dd83e-134">Rellene *host*, *nombre de usuario*, y *contraseña* con valores de hello cuenta tooyour específico.</span><span class="sxs-lookup"><span data-stu-id="dd83e-134">Fill in *host*, *username*, and *password* with hello values that are specific tooyour account.</span></span>

<span data-ttu-id="dd83e-135">Plantilla:</span><span class="sxs-lookup"><span data-stu-id="dd83e-135">Template:</span></span>

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

<span data-ttu-id="dd83e-136">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dd83e-136">Example:</span></span>

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a><span data-ttu-id="dd83e-137">Guía para una migración correcta</span><span class="sxs-lookup"><span data-stu-id="dd83e-137">Guide for a successful migration</span></span>

1. <span data-ttu-id="dd83e-138">Cree previamente las colecciones y escálelas:</span><span class="sxs-lookup"><span data-stu-id="dd83e-138">Pre-create and scale your collections:</span></span>
        
    * <span data-ttu-id="dd83e-139">De forma predeterminada, Azure Cosmos DB aprovisiona una nueva colección de MongoDB con 1000 unidades de solicitud (RU).</span><span class="sxs-lookup"><span data-stu-id="dd83e-139">By default, Azure Cosmos DB provisions a new MongoDB collection with 1,000 request units (RUs).</span></span> <span data-ttu-id="dd83e-140">Antes de empezar la migración de hello mediante mongoimport, mongorestore o mongomirror, crear previamente todas las colecciones de hello [portal de Azure](https://portal.azure.com) o procedentes de controladores de MongoDB y herramientas.</span><span class="sxs-lookup"><span data-stu-id="dd83e-140">Before you start hello migration by using mongoimport, mongorestore, or mongomirror, pre-create all your collections from hello [Azure portal](https://portal.azure.com) or from MongoDB drivers and tools.</span></span> <span data-ttu-id="dd83e-141">Si la colección es mayor que 10 GB, asegúrese de que toocreate una [colección particionada/particiones](partition-data.md) con una clave de partición adecuado.</span><span class="sxs-lookup"><span data-stu-id="dd83e-141">If your collection is greater than 10 GB, make sure toocreate a [sharded/partitioned collection](partition-data.md) with an appropriate shard key.</span></span>

    * <span data-ttu-id="dd83e-142">De hello [portal de Azure](https://portal.azure.com), aumentar el rendimiento de las colecciones de 1.000 RUs para una colección de una sola partición y 2.500 RUs para una colección particionada solo para la migración de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd83e-142">From hello [Azure portal](https://portal.azure.com), increase your collections' throughput from 1,000 RUs for a single partition collection and 2,500 RUs for a sharded collection just for hello migration.</span></span> <span data-ttu-id="dd83e-143">Con un rendimiento mayor hello, puede evitar la limitación y migrar en menos tiempo.</span><span class="sxs-lookup"><span data-stu-id="dd83e-143">With hello higher throughput, you can avoid throttling and migrate in less time.</span></span> <span data-ttu-id="dd83e-144">Con cada hora facturación en base de datos de Azure Cosmos, puede reducir el rendimiento de hello inmediatamente después de los costos de toosave de migración de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd83e-144">With hourly billing in Azure Cosmos DB, you can reduce hello throughput immediately after hello migration toosave costs.</span></span>

2. <span data-ttu-id="dd83e-145">Calcular la carga RU aproximado de Hola para una operación de escritura único documento:</span><span class="sxs-lookup"><span data-stu-id="dd83e-145">Calculate hello approximate RU charge for a single document write:</span></span>

    <span data-ttu-id="dd83e-146">a.</span><span class="sxs-lookup"><span data-stu-id="dd83e-146">a.</span></span> <span data-ttu-id="dd83e-147">Conectar la base de datos de Azure Cosmos DB MongoDB de tooyour de hello MongoDB Shell.</span><span class="sxs-lookup"><span data-stu-id="dd83e-147">Connect tooyour Azure Cosmos DB MongoDB database from hello MongoDB Shell.</span></span> <span data-ttu-id="dd83e-148">Encontrará instrucciones en [conectarse un tooAzure de aplicación de MongoDB Cosmos DB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="dd83e-148">You can find instructions in [Connect a MongoDB application tooAzure Cosmos DB](connect-mongodb-account.md).</span></span>
    
    <span data-ttu-id="dd83e-149">b.</span><span class="sxs-lookup"><span data-stu-id="dd83e-149">b.</span></span> <span data-ttu-id="dd83e-150">Ejecutar un comando de inserción de ejemplo mediante uno de los documentos de ejemplo de Hola MongoDB Shell:</span><span class="sxs-lookup"><span data-stu-id="dd83e-150">Run a sample insert command by using one of your sample documents from hello MongoDB Shell:</span></span>
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    <span data-ttu-id="dd83e-151">c.</span><span class="sxs-lookup"><span data-stu-id="dd83e-151">c.</span></span> <span data-ttu-id="dd83e-152">Ejecute ```db.runCommand({getLastRequestStatistics: 1})``` y recibirá una respuesta como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="dd83e-152">Run ```db.runCommand({getLastRequestStatistics: 1})``` and you will receive a response like this one:</span></span>
     
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
        
    <span data-ttu-id="dd83e-153">d.</span><span class="sxs-lookup"><span data-stu-id="dd83e-153">d.</span></span> <span data-ttu-id="dd83e-154">Tome nota de forma gratuita de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="dd83e-154">Take note of hello request charge.</span></span>
    
3. <span data-ttu-id="dd83e-155">Determinar la latencia de Hola desde su servicio en la base de datos de Azure Cosmos nube de máquina toohello:</span><span class="sxs-lookup"><span data-stu-id="dd83e-155">Determine hello latency from your machine toohello Azure Cosmos DB cloud service:</span></span>
    
    <span data-ttu-id="dd83e-156">a.</span><span class="sxs-lookup"><span data-stu-id="dd83e-156">a.</span></span> <span data-ttu-id="dd83e-157">Habilitar el registro detallado de hello MongoDB Shell mediante el uso de este comando:```setVerboseShell(true)```</span><span class="sxs-lookup"><span data-stu-id="dd83e-157">Enable verbose logging from hello MongoDB Shell by using this command: ```setVerboseShell(true)```</span></span>
    
    <span data-ttu-id="dd83e-158">b.</span><span class="sxs-lookup"><span data-stu-id="dd83e-158">b.</span></span> <span data-ttu-id="dd83e-159">Ejecutar una consulta simple en la base de datos de hello: ```db.coll.find().limit(1)```.</span><span class="sxs-lookup"><span data-stu-id="dd83e-159">Run a simple query against hello database: ```db.coll.find().limit(1)```.</span></span> <span data-ttu-id="dd83e-160">Recibirá una respuesta como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="dd83e-160">You will receive a response like this one:</span></span>

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. <span data-ttu-id="dd83e-161">Quitar documento Hola insertado antes de hello tooensure de migración que no hay ningún documento duplicado.</span><span class="sxs-lookup"><span data-stu-id="dd83e-161">Remove hello inserted document before hello migration tooensure that there are no duplicate documents.</span></span> <span data-ttu-id="dd83e-162">Puede quitar los documentos con este comando: ```db.coll.remove({})```.</span><span class="sxs-lookup"><span data-stu-id="dd83e-162">You can remove documents by using this command: ```db.coll.remove({})```</span></span>

5. <span data-ttu-id="dd83e-163">Calcular Hola aproximado *batchSize* y *numInsertionWorkers* valores:</span><span class="sxs-lookup"><span data-stu-id="dd83e-163">Calculate hello approximate *batchSize* and *numInsertionWorkers* values:</span></span>

    * <span data-ttu-id="dd83e-164">Para *batchSize*, división Hola total aprovisionado RUs por RUs Hola consumidos de único documento escribe en el paso 3.</span><span class="sxs-lookup"><span data-stu-id="dd83e-164">For *batchSize*, divide hello total provisioned RUs by hello RUs consumed from your single document write in step 3.</span></span>
    
    * <span data-ttu-id="dd83e-165">Si se calcula hello *batchSize* < = 24, utilice ese número como su *batchSize* valor.</span><span class="sxs-lookup"><span data-stu-id="dd83e-165">If hello calculated *batchSize* <= 24, use that number as your *batchSize* value.</span></span>
    
    * <span data-ttu-id="dd83e-166">Si se calcula hello *batchSize* > 24, conjunto hello *batchSize* too24 de valor.</span><span class="sxs-lookup"><span data-stu-id="dd83e-166">If hello calculated *batchSize* > 24, set hello *batchSize* value too24.</span></span>
    
    * <span data-ttu-id="dd83e-167">En el caso de *numInsertionWorkers*, use esta ecuación: *numInsertionWorkers = (rendimiento aprovisionado * latencia en segundos) / (tamaño del lote * RU usadas en una sola operación de escritura)*.</span><span class="sxs-lookup"><span data-stu-id="dd83e-167">For *numInsertionWorkers*, use this equation:   *numInsertionWorkers =  (provisioned throughput * latency in seconds) / (batch size * consumed RUs for a single write)*.</span></span>
        
    |<span data-ttu-id="dd83e-168">Propiedad</span><span class="sxs-lookup"><span data-stu-id="dd83e-168">Property</span></span>|<span data-ttu-id="dd83e-169">Valor</span><span class="sxs-lookup"><span data-stu-id="dd83e-169">Value</span></span>|
    |--------|-----|
    |<span data-ttu-id="dd83e-170">batchSize</span><span class="sxs-lookup"><span data-stu-id="dd83e-170">batchSize</span></span>| <span data-ttu-id="dd83e-171">24</span><span class="sxs-lookup"><span data-stu-id="dd83e-171">24</span></span> |
    |<span data-ttu-id="dd83e-172">RU aprovisionadas</span><span class="sxs-lookup"><span data-stu-id="dd83e-172">RUs provisioned</span></span> | <span data-ttu-id="dd83e-173">10000</span><span class="sxs-lookup"><span data-stu-id="dd83e-173">10000</span></span> |
    |<span data-ttu-id="dd83e-174">Latency</span><span class="sxs-lookup"><span data-stu-id="dd83e-174">Latency</span></span> | <span data-ttu-id="dd83e-175">0,100 s</span><span class="sxs-lookup"><span data-stu-id="dd83e-175">0.100 s</span></span> |
    |<span data-ttu-id="dd83e-176">RU cargadas en una sola operación de escritura de documento</span><span class="sxs-lookup"><span data-stu-id="dd83e-176">RU charged for 1 doc write</span></span> | <span data-ttu-id="dd83e-177">10 RU</span><span class="sxs-lookup"><span data-stu-id="dd83e-177">10 RUs</span></span> |
    |<span data-ttu-id="dd83e-178">numInsertionWorkers</span><span class="sxs-lookup"><span data-stu-id="dd83e-178">numInsertionWorkers</span></span> | <span data-ttu-id="dd83e-179">?</span><span class="sxs-lookup"><span data-stu-id="dd83e-179">?</span></span> |
    
    <span data-ttu-id="dd83e-180">*numInsertionWorkers = (10 000 RU x 0,1 s) / (24 x 10 RU) = 4,1666*</span><span class="sxs-lookup"><span data-stu-id="dd83e-180">*numInsertionWorkers = (10000 RUs x 0.1 s) / (24 x 10 RUs) = 4.1666*</span></span>

6. <span data-ttu-id="dd83e-181">Ejecute comandos de migración final hello:</span><span class="sxs-lookup"><span data-stu-id="dd83e-181">Run hello final migration command:</span></span>

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a><span data-ttu-id="dd83e-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dd83e-182">Next steps</span></span>

<span data-ttu-id="dd83e-183">Puede continuar el tutorial siguiente toohello y obtenga información acerca de cómo tooquery datos MongoDB mediante el uso de la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="dd83e-183">You can proceed toohello next tutorial and learn how tooquery MongoDB data by using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="dd83e-184">¿Cómo tooquery datos MongoDB?</span><span class="sxs-lookup"><span data-stu-id="dd83e-184">How tooquery MongoDB data?</span></span>](../cosmos-db/tutorial-query-mongodb.md)
