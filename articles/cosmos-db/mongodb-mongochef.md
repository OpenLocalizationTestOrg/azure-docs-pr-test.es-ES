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
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a>Uso de MongoChef con una cuenta de Azure Cosmos DB: API para MongoDB

tooconnect tooan base de datos de Azure Cosmos: API de MongoDB cuenta, debe:

* Descargar e instalar [MongoChef](http://3t.io/mongochef)
* Disponer de la información de la [cadena de conexión](connect-mongodb-account.md) de la cuenta de Cosmos DB: API para MongoDB

## <a name="create-hello-connection-in-mongochef"></a>Crear conexiones de hello en MongoChef
tooadd la base de datos de Azure Cosmos: API de MongoDB cuenta toohello MongoChef Administrador de conexiones, realizar Hola pasos.

1. Recuperar la base de datos de Azure Cosmos: API para obtener información de conexión de MongoDB utilizando instrucciones de hello [aquí](connect-mongodb-account.md).

    ![Captura de pantalla de hoja de cadena de conexión de Hola](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. Haga clic en **conectar** tooopen Hola Connection Manager, a continuación, haga clic en **nueva conexión**

    ![Captura de pantalla del Administrador de conexiones de hello MongoChef](./media/mongodb-mongochef/ConnectionManager.png)
3. Hola **nueva conexión** Hola la ventana **Server** ficha, escriba Hola HOST (FQDN) de la base de datos de Azure Cosmos hello: API para el puerto de hello y cuenta de MongoDB.

    ![Captura de pantalla de la ficha de servidor de administrador de conexión de hello MongoChef](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. Hola **nueva conexión** ventana hello **autenticación** ficha, elija el modo de autenticación **estándar (MONGODB CR o SCARM-SHA-1)** y escriba el nombre de usuario de Hola y CONTRASEÑA.  Aceptar Hola predeterminado autenticación db (admin) o proporcionar su propio valor.

    ![Captura de pantalla de la ficha de autenticación de administrador de conexión de hello MongoChef](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. Hola **nueva conexión** Hola la ventana **SSL** ficha, compruebe hello **usar SSL protocolo tooconnect** hello y casilla de verificación **Accept servidor autofirmado SSL certificados** botón de radio.

    ![Captura de pantalla de la pestaña SSL de administrador de conexión de hello MongoChef](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. Haga clic en hello **Probar conexión** botón información de conexión de hello toovalidate, haga clic en **Aceptar** ventana de nueva conexión de tooreturn toohello y, a continuación, haga clic en **guardar**.

    ![Captura de pantalla de ventana de conexión de prueba de hello MongoChef](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a>Usar MongoChef toocreate una base de datos, la recopilación y documentos
toocreate una base de datos, la recopilación y documentos mediante MongoChef, realizan Hola pasos.

1. En **Connection Manager**, resalte la conexión de Hola y haga clic en **conectar**.

    ![Captura de pantalla del Administrador de conexiones de hello MongoChef](./media/mongodb-mongochef/ConnectToAccount.png)
2. Haga clic en el host de Hola y elija **Agregar base de datos**.  Especifique un nombre de base de datos y haga clic en **OK**(Aceptar).

    ![Captura de pantalla de hello opción MongoChef Agregar base de datos](./media/mongodb-mongochef/AddDatabase1.png)
3. Haga clic en la base de datos de Hola y elija **agregar colección**.  Especifique un nombre para la colección y haga clic en **Create**(Create).

    ![Captura de pantalla de hello opción MongoChef agregar colección](./media/mongodb-mongochef/AddCollection.png)
4. Haga clic en hello **colección** menú elemento, a continuación, haga clic en **Agregar documento**.

    ![Captura de pantalla de elemento de menú de hello MongoChef Agregar documento](./media/mongodb-mongochef/AddDocument1.png)
5. En el cuadro de diálogo de Agregar documento hello, pegue el siguiente de Hola y, a continuación, haga clic en **Agregar documento**.

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
6. Agregar otro documento, en este momento con hello siguen contenido.

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
7. Ejecute una consulta de ejemplo. Por ejemplo, busque familias con hello last name 'Andersen' y elementos primarios de hello devuelto y campos de estado.

    ![Captura de pantalla de resultados de la consulta de MongoChef](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a>Pasos siguientes
* Explore [ejemplos](mongodb-samples.md) de Azure Cosmos DB: API para MongoDB.
