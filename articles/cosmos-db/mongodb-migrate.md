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
# <a name="azure-cosmos-db-import-mongodb-data"></a>Azure Cosmos DB: importar datos de MongoDB 

toomigrate datos de MongoDB tooan cuenta de base de datos de Azure Cosmos para su uso con hello API para MongoDB, debe:

* Descargar cualquiera *mongoimport.exe* o *mongorestore.exe* de hello [centro de descarga de MongoDB](https://www.mongodb.com/download-center).
* Obtenga su [cadena de conexión de la API de MongoDB](connect-mongodb-account.md).

Si va a importar datos de MongoDB y plan toouse con hello Azure Cosmos DB, debe usar hello [herramienta de migración de datos](import-data.md) datos tooimport.

Este tutorial trata Hola siguientes tareas:

> [!div class="checklist"]
> * Recuperación de la cadena de conexión
> * Importación de datos de MongoDB mediante mongoimport
> * Importación de datos de MongoDB mediante mongorestore

## <a name="prerequisites"></a>Requisitos previos

* Aumentar el rendimiento: duración de Hola de migración de los datos depende de la cantidad de Hola de rendimiento configurado para las colecciones. Estar seguro de rendimiento de hello tooincrease para las migraciones de datos más grandes. Después de haber completado la migración de hello, reducir los costos de toosave de rendimiento de Hola. Para obtener más información sobre cómo aumentar el rendimiento en hello [portal de Azure](https://portal.azure.com), consulte [niveles de rendimiento y los niveles de precios de base de datos de Azure Cosmos](performance-levels.md).

* Habilite SSL: Azure Cosmos DB tiene estrictos estándares y requisitos de seguridad. Ser tooenable seguro SSL cuando se interactúa con su cuenta. procedimientos de Hola de rest de Hola de artículo Hola incluyen cómo tooenable SSL para mongoimport y mongorestore.

## <a name="find-your-connection-string-information-host-port-username-and-password"></a>Búsqueda de la información de la cadena de conexión (host, puerto, nombre de usuario y contraseña)

1. Hola [portal de Azure](https://portal.azure.com), en Hola panel izquierdo, haga clic en hello **base de datos de Azure Cosmos** entrada.
2. Hola **suscripciones** panel, seleccione el nombre de cuenta.
3. Hola **cadena de conexión** hoja, haga clic en **cadena de conexión**.  
Hola derecho panel contiene toda la información de Hola que necesita toosuccessfully conectar tooyour cuenta.

    ![Hoja Cadena de conexión](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a>Importar datos toohello API para MongoDB mediante mongoimport

tooimport datos tooyour cuenta de base de datos de Azure Cosmos, utilice Hola después de la plantilla. Rellene *host*, *nombre de usuario*, y *contraseña* con valores de hello cuenta tooyour específico.  

Plantilla:

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

Ejemplo:  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a>Importar datos toohello API para MongoDB mediante mongorestore

toorestore datos tooyour API para la cuenta de MongoDB, utilice Hola después de importar la plantilla tooexecute Hola. Rellene *host*, *nombre de usuario*, y *contraseña* con valores de hello cuenta tooyour específico.

Plantilla:

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

Ejemplo:

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a>Guía para una migración correcta

1. Cree previamente las colecciones y escálelas:
        
    * De forma predeterminada, Azure Cosmos DB aprovisiona una nueva colección de MongoDB con 1000 unidades de solicitud (RU). Antes de empezar la migración de hello mediante mongoimport, mongorestore o mongomirror, crear previamente todas las colecciones de hello [portal de Azure](https://portal.azure.com) o procedentes de controladores de MongoDB y herramientas. Si la colección es mayor que 10 GB, asegúrese de que toocreate una [colección particionada/particiones](partition-data.md) con una clave de partición adecuado.

    * De hello [portal de Azure](https://portal.azure.com), aumentar el rendimiento de las colecciones de 1.000 RUs para una colección de una sola partición y 2.500 RUs para una colección particionada solo para la migración de Hola. Con un rendimiento mayor hello, puede evitar la limitación y migrar en menos tiempo. Con cada hora facturación en base de datos de Azure Cosmos, puede reducir el rendimiento de hello inmediatamente después de los costos de toosave de migración de Hola.

2. Calcular la carga RU aproximado de Hola para una operación de escritura único documento:

    a. Conectar la base de datos de Azure Cosmos DB MongoDB de tooyour de hello MongoDB Shell. Encontrará instrucciones en [conectarse un tooAzure de aplicación de MongoDB Cosmos DB](connect-mongodb-account.md).
    
    b. Ejecutar un comando de inserción de ejemplo mediante uno de los documentos de ejemplo de Hola MongoDB Shell:
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    c. Ejecute ```db.runCommand({getLastRequestStatistics: 1})``` y recibirá una respuesta como la siguiente:
     
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
        
    d. Tome nota de forma gratuita de solicitud de saludo.
    
3. Determinar la latencia de Hola desde su servicio en la base de datos de Azure Cosmos nube de máquina toohello:
    
    a. Habilitar el registro detallado de hello MongoDB Shell mediante el uso de este comando:```setVerboseShell(true)```
    
    b. Ejecutar una consulta simple en la base de datos de hello: ```db.coll.find().limit(1)```. Recibirá una respuesta como la siguiente:

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. Quitar documento Hola insertado antes de hello tooensure de migración que no hay ningún documento duplicado. Puede quitar los documentos con este comando: ```db.coll.remove({})```.

5. Calcular Hola aproximado *batchSize* y *numInsertionWorkers* valores:

    * Para *batchSize*, división Hola total aprovisionado RUs por RUs Hola consumidos de único documento escribe en el paso 3.
    
    * Si se calcula hello *batchSize* < = 24, utilice ese número como su *batchSize* valor.
    
    * Si se calcula hello *batchSize* > 24, conjunto hello *batchSize* too24 de valor.
    
    * En el caso de *numInsertionWorkers*, use esta ecuación: *numInsertionWorkers = (rendimiento aprovisionado * latencia en segundos) / (tamaño del lote * RU usadas en una sola operación de escritura)*.
        
    |Propiedad|Valor|
    |--------|-----|
    |batchSize| 24 |
    |RU aprovisionadas | 10000 |
    |Latency | 0,100 s |
    |RU cargadas en una sola operación de escritura de documento | 10 RU |
    |numInsertionWorkers | ? |
    
    *numInsertionWorkers = (10 000 RU x 0,1 s) / (24 x 10 RU) = 4,1666*

6. Ejecute comandos de migración final hello:

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a>Pasos siguientes

Puede continuar el tutorial siguiente toohello y obtenga información acerca de cómo tooquery datos MongoDB mediante el uso de la base de datos de Azure Cosmos. 

> [!div class="nextstepaction"]
>[¿Cómo tooquery datos MongoDB?](../cosmos-db/tutorial-query-mongodb.md)
