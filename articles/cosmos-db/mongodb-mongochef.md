---
title: Uso de MongoChef para Azure Cosmos DB | Microsoft Docs
description: "Obtenga información sobre cómo usar MongoChef con una cuenta de Azure Cosmos DB: API para MongoDB."
keywords: MongoChef
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
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 54c9799bd646b827f602e2ea2f9a15a4fc853f00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="62fb8-104">Uso de MongoChef con una cuenta de Azure Cosmos DB: API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="62fb8-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="62fb8-105">Para conectarse a una cuenta de Azure Cosmos DB: API para MongoDB, debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="62fb8-105">To connect to an Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="62fb8-106">Descargar e instalar [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="62fb8-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="62fb8-107">Disponer de la información de la [cadena de conexión](connect-mongodb-account.md) de la cuenta de Cosmos DB: API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="62fb8-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-the-connection-in-mongochef"></a><span data-ttu-id="62fb8-108">Crear la conexión en MongoChef</span><span class="sxs-lookup"><span data-stu-id="62fb8-108">Create the connection in MongoChef</span></span>
<span data-ttu-id="62fb8-109">Para agregar la cuenta de Cosmos DB: API para MongoDB al administrador de conexiones de MongoChef, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="62fb8-109">To add your Azure Cosmos DB: API for MongoDB account to the MongoChef connection manager, perform the following steps.</span></span>

1. <span data-ttu-id="62fb8-110">Recupere la información de conexión de Azure Cosmos DB: API para MongoDB siguiendo [estas](connect-mongodb-account.md) instrucciones.</span><span class="sxs-lookup"><span data-stu-id="62fb8-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using the instructions [here](connect-mongodb-account.md).</span></span>

    ![Captura de pantalla de la hoja Cadena de conexión](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="62fb8-112">Haga clic en **Connect** (Conectar) para abrir Connection Manager (Administrador de conexiones) y, después, haga clic en **New Connection** (Nueva conexión).</span><span class="sxs-lookup"><span data-stu-id="62fb8-112">Click **Connect** to open the Connection Manager, then click **New Connection**</span></span>

    ![Captura de pantalla del administrador de conexiones de MongoChef](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="62fb8-114">En la ventana **New Connection** (Nueva conexión), en la pestaña **Server** (Servidor), escriba el HOST (FQDN) de la cuenta de Azure Cosmos DB: API para MongoDB y el PUERTO.</span><span class="sxs-lookup"><span data-stu-id="62fb8-114">In the **New Connection** window, on the **Server** tab, enter the HOST (FQDN) of the Azure Cosmos DB: API for MongoDB account and the PORT.</span></span>

    ![Captura de pantalla de la pestaña Server (Servidor) del administrador de conexiones de MongoChef](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="62fb8-116">En la ventana **New Connection** (Nueva conexión), en la pestaña **Authentication** (Autenticación), elija el modo de autenticación **Standard (MONGODB-CR or SCARM-SHA-1)** (Estándar [MONGODB-CR o SCARM-SHA-1]) y escriba el NOMBRE DE USUARIO y la CONTRASEÑA.</span><span class="sxs-lookup"><span data-stu-id="62fb8-116">In the **New Connection** window, on the **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter the USERNAME and PASSWORD.</span></span>  <span data-ttu-id="62fb8-117">Acepte la base de datos de autenticación predeterminada (admin) o proporcione su propio valor.</span><span class="sxs-lookup"><span data-stu-id="62fb8-117">Accept the default authentication db (admin) or provide your own value.</span></span>

    ![Captura de pantalla de la pestaña Authentication (Autenticación) del administrador de conexiones de MongoChef](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="62fb8-119">En la ventana **New Connection** (Nueva conexión), en la pestaña **SSL**, active la casilla **Use SSL protocol to connect** (Usar protocolo SSL para conectar) y el botón de radio **Accept server self-signed SSL certificates** (Aceptar certificados SSL autofirmados del servidor).</span><span class="sxs-lookup"><span data-stu-id="62fb8-119">In the **New Connection** window, on the **SSL** tab, check the **Use SSL protocol to connect** check box and the **Accept server self-signed SSL certificates** radio button.</span></span>

    ![Captura de pantalla de la pestaña SSL del administrador de conexiones de MongoChef](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="62fb8-121">Haga clic en el botón **Test Connection** (Probar conexión) para validar la información de conexión, haga clic en **OK** (Aceptar) para volver a la ventana de la nueva conexión y, finalmente, haga clic en **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="62fb8-121">Click the **Test Connection** button to validate the connection information, click **OK** to return to the New Connection window, and then click **Save**.</span></span>

    ![Captura de pantalla de la ventana de conexión de prueba de MongoChef](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-to-create-a-database-collection-and-documents"></a><span data-ttu-id="62fb8-123">Uso de MongoChef para crear una base de datos, una colección y unos documentos</span><span class="sxs-lookup"><span data-stu-id="62fb8-123">Use MongoChef to create a database, collection, and documents</span></span>
<span data-ttu-id="62fb8-124">Para crear una base de datos, una colección y unos documentos mediante MongoChef, realice los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="62fb8-124">To create a database, collection, and documents using MongoChef, perform the following steps.</span></span>

1. <span data-ttu-id="62fb8-125">En **Connection Manager** (Administrador de conexiones), resalte la conexión y haga clic en **Connect** (Conectar).</span><span class="sxs-lookup"><span data-stu-id="62fb8-125">In **Connection Manager**, highlight the connection and click **Connect**.</span></span>

    ![Captura de pantalla del administrador de conexiones de MongoChef](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="62fb8-127">Haga clic con el botón derecho en el host y elija **Add Database**(Agregar base de datos).</span><span class="sxs-lookup"><span data-stu-id="62fb8-127">Right click the host and choose **Add Database**.</span></span>  <span data-ttu-id="62fb8-128">Especifique un nombre de base de datos y haga clic en **OK**(Aceptar).</span><span class="sxs-lookup"><span data-stu-id="62fb8-128">Provide a database name and click **OK**.</span></span>

    ![Captura de pantalla de la opción Add Database (Agregar base de datos) de MongoChef](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="62fb8-130">Haga clic con el botón derecho en la base de datos y elija **Add Collection**(Agregar colección).</span><span class="sxs-lookup"><span data-stu-id="62fb8-130">Right click the database and choose **Add Collection**.</span></span>  <span data-ttu-id="62fb8-131">Especifique un nombre para la colección y haga clic en **Create**(Create).</span><span class="sxs-lookup"><span data-stu-id="62fb8-131">Provide a collection name and click **Create**.</span></span>

    ![Captura de pantalla de la opción Add Collection (Agregar colección) de MongoChef](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="62fb8-133">Haga clic en el elemento de menú **Collection** (Colección) y en **Add Document** (Agregar documento).</span><span class="sxs-lookup"><span data-stu-id="62fb8-133">Click the **Collection** menu item, then click **Add Document**.</span></span>

    ![Captura de pantalla del elemento de menú Add Document (Agregar documento) de MongoChef](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="62fb8-135">En el cuadro de diálogo Add Document (Agregar documento), pegue lo siguiente y haga clic en **Add Document**(Agregar documento).</span><span class="sxs-lookup"><span data-stu-id="62fb8-135">In the Add Document dialog, paste the following and then click **Add Document**.</span></span>

        {
        "_id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
               { "firstName": "Thomas" },
               { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "isRegistered": true
        }
6. <span data-ttu-id="62fb8-136">Agregue otro documento, esta vez con el contenido siguiente.</span><span class="sxs-lookup"><span data-stu-id="62fb8-136">Add another document, this time with the following content.</span></span>

        {
        "_id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam",
                 "givenName": "Jesse",
                "gender": "female", "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            {
                "familyName": "Miller",
                 "givenName": "Lisa",
                 "gender": "female",
                 "grade": 8 }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
        }
7. <span data-ttu-id="62fb8-137">Ejecute una consulta de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="62fb8-137">Execute a sample query.</span></span> <span data-ttu-id="62fb8-138">Por ejemplo, busque familias con el apellido 'Andersen' y devuelva los campos parents (padres) y state (estado).</span><span class="sxs-lookup"><span data-stu-id="62fb8-138">For example, search for families with the last name 'Andersen' and return the parents and state fields.</span></span>

    ![Captura de pantalla de resultados de la consulta de MongoChef](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="62fb8-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="62fb8-140">Next steps</span></span>
* <span data-ttu-id="62fb8-141">Explore [ejemplos](mongodb-samples.md) de Azure Cosmos DB: API para MongoDB.</span><span class="sxs-lookup"><span data-stu-id="62fb8-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
