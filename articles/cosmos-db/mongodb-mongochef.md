---
title: aaaUse MongoChef para la base de datos de Azure Cosmos | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse MongoChef con una base de datos de Azure Cosmos: API de MongoDB cuenta"
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
ms.openlocfilehash: 4b047797b231c34ccc6f2ed02416525c6228d596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="63abc-104">Uso de MongoChef con una cuenta de Azure Cosmos DB: API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="63abc-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="63abc-105">tooconnect tooan base de datos de Azure Cosmos: API de MongoDB cuenta, debe:</span><span class="sxs-lookup"><span data-stu-id="63abc-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="63abc-106">Descargar e instalar [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="63abc-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="63abc-107">Disponer de la información de la [cadena de conexión](connect-mongodb-account.md) de la cuenta de Cosmos DB: API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="63abc-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-hello-connection-in-mongochef"></a><span data-ttu-id="63abc-108">Crear conexiones de hello en MongoChef</span><span class="sxs-lookup"><span data-stu-id="63abc-108">Create hello connection in MongoChef</span></span>
<span data-ttu-id="63abc-109">tooadd la base de datos de Azure Cosmos: API de MongoDB cuenta toohello MongoChef Administrador de conexiones, realizar Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="63abc-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello MongoChef connection manager, perform hello following steps.</span></span>

1. <span data-ttu-id="63abc-110">Recuperar la base de datos de Azure Cosmos: API para obtener información de conexión de MongoDB utilizando instrucciones de hello [aquí](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="63abc-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Captura de pantalla de hoja de cadena de conexión de Hola](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="63abc-112">Haga clic en **conectar** tooopen Hola Connection Manager, a continuación, haga clic en **nueva conexión**</span><span class="sxs-lookup"><span data-stu-id="63abc-112">Click **Connect** tooopen hello Connection Manager, then click **New Connection**</span></span>

    ![Captura de pantalla del Administrador de conexiones de hello MongoChef](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="63abc-114">Hola **nueva conexión** Hola la ventana **Server** ficha, escriba Hola HOST (FQDN) de la base de datos de Azure Cosmos hello: API para el puerto de hello y cuenta de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="63abc-114">In hello **New Connection** window, on hello **Server** tab, enter hello HOST (FQDN) of hello Azure Cosmos DB: API for MongoDB account and hello PORT.</span></span>

    ![Captura de pantalla de la ficha de servidor de administrador de conexión de hello MongoChef](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="63abc-116">Hola **nueva conexión** ventana hello **autenticación** ficha, elija el modo de autenticación **estándar (MONGODB CR o SCARM-SHA-1)** y escriba el nombre de usuario de Hola y CONTRASEÑA.</span><span class="sxs-lookup"><span data-stu-id="63abc-116">In hello **New Connection** window, on hello **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter hello USERNAME and PASSWORD.</span></span>  <span data-ttu-id="63abc-117">Aceptar Hola predeterminado autenticación db (admin) o proporcionar su propio valor.</span><span class="sxs-lookup"><span data-stu-id="63abc-117">Accept hello default authentication db (admin) or provide your own value.</span></span>

    ![Captura de pantalla de la ficha de autenticación de administrador de conexión de hello MongoChef](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="63abc-119">Hola **nueva conexión** Hola la ventana **SSL** ficha, compruebe hello **usar SSL protocolo tooconnect** hello y casilla de verificación **Accept servidor autofirmado SSL certificados** botón de radio.</span><span class="sxs-lookup"><span data-stu-id="63abc-119">In hello **New Connection** window, on hello **SSL** tab, check hello **Use SSL protocol tooconnect** check box and hello **Accept server self-signed SSL certificates** radio button.</span></span>

    ![Captura de pantalla de la pestaña SSL de administrador de conexión de hello MongoChef](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="63abc-121">Haga clic en hello **Probar conexión** botón información de conexión de hello toovalidate, haga clic en **Aceptar** ventana de nueva conexión de tooreturn toohello y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="63abc-121">Click hello **Test Connection** button toovalidate hello connection information, click **OK** tooreturn toohello New Connection window, and then click **Save**.</span></span>

    ![Captura de pantalla de ventana de conexión de prueba de hello MongoChef](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a><span data-ttu-id="63abc-123">Usar MongoChef toocreate una base de datos, la recopilación y documentos</span><span class="sxs-lookup"><span data-stu-id="63abc-123">Use MongoChef toocreate a database, collection, and documents</span></span>
<span data-ttu-id="63abc-124">toocreate una base de datos, la recopilación y documentos mediante MongoChef, realizan Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="63abc-124">toocreate a database, collection, and documents using MongoChef, perform hello following steps.</span></span>

1. <span data-ttu-id="63abc-125">En **Connection Manager**, resalte la conexión de Hola y haga clic en **conectar**.</span><span class="sxs-lookup"><span data-stu-id="63abc-125">In **Connection Manager**, highlight hello connection and click **Connect**.</span></span>

    ![Captura de pantalla del Administrador de conexiones de hello MongoChef](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="63abc-127">Haga clic en el host de Hola y elija **Agregar base de datos**.</span><span class="sxs-lookup"><span data-stu-id="63abc-127">Right click hello host and choose **Add Database**.</span></span>  <span data-ttu-id="63abc-128">Especifique un nombre de base de datos y haga clic en **OK**(Aceptar).</span><span class="sxs-lookup"><span data-stu-id="63abc-128">Provide a database name and click **OK**.</span></span>

    ![Captura de pantalla de hello opción MongoChef Agregar base de datos](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="63abc-130">Haga clic en la base de datos de Hola y elija **agregar colección**.</span><span class="sxs-lookup"><span data-stu-id="63abc-130">Right click hello database and choose **Add Collection**.</span></span>  <span data-ttu-id="63abc-131">Especifique un nombre para la colección y haga clic en **Create**(Create).</span><span class="sxs-lookup"><span data-stu-id="63abc-131">Provide a collection name and click **Create**.</span></span>

    ![Captura de pantalla de hello opción MongoChef agregar colección](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="63abc-133">Haga clic en hello **colección** menú elemento, a continuación, haga clic en **Agregar documento**.</span><span class="sxs-lookup"><span data-stu-id="63abc-133">Click hello **Collection** menu item, then click **Add Document**.</span></span>

    ![Captura de pantalla de elemento de menú de hello MongoChef Agregar documento](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="63abc-135">En el cuadro de diálogo de Agregar documento hello, pegue el siguiente de Hola y, a continuación, haga clic en **Agregar documento**.</span><span class="sxs-lookup"><span data-stu-id="63abc-135">In hello Add Document dialog, paste hello following and then click **Add Document**.</span></span>

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
6. <span data-ttu-id="63abc-136">Agregar otro documento, en este momento con hello siguen contenido.</span><span class="sxs-lookup"><span data-stu-id="63abc-136">Add another document, this time with hello following content.</span></span>

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
7. <span data-ttu-id="63abc-137">Ejecute una consulta de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="63abc-137">Execute a sample query.</span></span> <span data-ttu-id="63abc-138">Por ejemplo, busque familias con hello last name 'Andersen' y elementos primarios de hello devuelto y campos de estado.</span><span class="sxs-lookup"><span data-stu-id="63abc-138">For example, search for families with hello last name 'Andersen' and return hello parents and state fields.</span></span>

    ![Captura de pantalla de resultados de la consulta de MongoChef](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="63abc-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="63abc-140">Next steps</span></span>
* <span data-ttu-id="63abc-141">Explore [ejemplos](mongodb-samples.md) de Azure Cosmos DB: API para MongoDB.</span><span class="sxs-lookup"><span data-stu-id="63abc-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
