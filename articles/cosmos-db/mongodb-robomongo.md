---
title: Uso de Robomongo para Azure Cosmos DB | Microsoft Docs
description: "Obtenga información sobre cómo usar Robomongo con una cuenta de Azure Cosmos DB: API para MongoDB."
keywords: Robomongo
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
ms.openlocfilehash: 8983594776a1bbe413a6d7cf2cd518f0e327648a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="4db71-104">Uso de Robomongo con una cuenta de Azure Cosmos DB: API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="4db71-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span></span>
<span data-ttu-id="4db71-105">Para conectarse a una cuenta de Azure Cosmos DB: API para MongoDB con Robomongo, debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4db71-105">To connect to an Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="4db71-106">Descargar e instalar [Robomongo](https://robomongo.org/)</span><span class="sxs-lookup"><span data-stu-id="4db71-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="4db71-107">Disponer de la información de la [cadena de conexión](connect-mongodb-account.md) de la cuenta de Cosmos DB: API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="4db71-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="4db71-108">Conectarse mediante Robomongo</span><span class="sxs-lookup"><span data-stu-id="4db71-108">Connect using Robomongo</span></span>
<span data-ttu-id="4db71-109">Para agregar la cuenta de Azure Cosmos DB: API para MongoDB a las conexiones de MongoDB de Robomongo, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="4db71-109">To add your Azure Cosmos DB: API for MongoDB account to the Robomongo MongoDB Connections, perform the following steps.</span></span>

1. <span data-ttu-id="4db71-110">Recupere la información de conexión de la cuenta de Azure Cosmos DB: API para MongoDB siguiendo [estas](connect-mongodb-account.md) instrucciones.</span><span class="sxs-lookup"><span data-stu-id="4db71-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using the instructions [here](connect-mongodb-account.md).</span></span>

    ![Captura de pantalla de la hoja Cadena de conexión](./media/mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="4db71-112">Ejecute *Robomongo.exe*.</span><span class="sxs-lookup"><span data-stu-id="4db71-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="4db71-113">Haga clic en el botón de conexión, que está bajo **File** (Archivo), para administrar las conexiones.</span><span class="sxs-lookup"><span data-stu-id="4db71-113">Click the connection button under **File** to manage your connections.</span></span> <span data-ttu-id="4db71-114">Después, haga clic en la opción **Create** (Create) de la ventana **MongoDB Connections**; se abrirá **Connection Settings** (Configuración de conexiones).</span><span class="sxs-lookup"><span data-stu-id="4db71-114">Then, click **Create** in the **MongoDB Connections** window, which will open up the **Connection Settings** window.</span></span>

4. <span data-ttu-id="4db71-115">En la ventana **Connection Settings** (Configuración de conexiones), elija un nombre.</span><span class="sxs-lookup"><span data-stu-id="4db71-115">In the **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="4db71-116">Después, busque el **host** y **puerto** en la información de conexión del paso 1 y escríbalos en **Address** (Dirección) y **Port** (Puerto) respectivamente.</span><span class="sxs-lookup"><span data-stu-id="4db71-116">Then, find the **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![Captura de pantalla de la funcionalidad de administración de conexiones de Robomongo](./media/mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="4db71-118">En la pestaña **Authentication** (Autenticación), haga clic en **Perform authentication** (Realizar autenticación).</span><span class="sxs-lookup"><span data-stu-id="4db71-118">On the **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="4db71-119">Después, escriba la base de datos (el valor predeterminado es *Admin*), el **nombre de usuario** y la **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="4db71-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="4db71-120">Tanto el **nombre de usuario** como la **contraseña** están en la información de conexión del paso 1.</span><span class="sxs-lookup"><span data-stu-id="4db71-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Captura de pantalla de la pestaña de autenticación de Robomongo](./media/mongodb-robomongo/authentication.png)
6. <span data-ttu-id="4db71-122">En la pestaña **SSL**, marque **Use SSL protocol** (Usar protocolo SSL) y, luego, cambie el **método de autenticación** a **Self-signed Certificate** (Certificado autofirmado).</span><span class="sxs-lookup"><span data-stu-id="4db71-122">On the **SSL** tab, check **Use SSL protocol**, then change the **Authentication Method** to **Self-signed Certificate**.</span></span>

    ![Captura de pantalla de la pestaña SSL de Robomongo](./media/mongodb-robomongo/SSL.png)
7. <span data-ttu-id="4db71-124">Por último, haga clic en **Test** (Probar) para comprobar que puede conectarse. Después, seleccione **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="4db71-124">Finally, click **Test** to verify that you are able to connect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4db71-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4db71-125">Next steps</span></span>
* <span data-ttu-id="4db71-126">Explore [ejemplos](mongodb-samples.md) de Azure Cosmos DB: API para MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4db71-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
