---
title: aaaUse Robomongo para la base de datos de Azure Cosmos | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Robomongo con una base de datos de Azure Cosmos: API de MongoDB cuenta"
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
ms.openlocfilehash: 3018243e904015426dc69a69b26fb53421e1fe4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="94381-104">Uso de Robomongo con una cuenta de Azure Cosmos DB: API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="94381-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span></span>
<span data-ttu-id="94381-105">tooconnect tooan base de datos de Azure Cosmos: API de cuenta de MongoDB utilizando Robomongo, debe:</span><span class="sxs-lookup"><span data-stu-id="94381-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="94381-106">Descargar e instalar [Robomongo](https://robomongo.org/)</span><span class="sxs-lookup"><span data-stu-id="94381-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="94381-107">Disponer de la información de la [cadena de conexión](connect-mongodb-account.md) de la cuenta de Cosmos DB: API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="94381-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="94381-108">Conectarse mediante Robomongo</span><span class="sxs-lookup"><span data-stu-id="94381-108">Connect using Robomongo</span></span>
<span data-ttu-id="94381-109">tooadd la base de datos de Azure Cosmos: API de MongoDB cuenta toohello Robomongo MongoDB conexiones, realizar Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="94381-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello Robomongo MongoDB Connections, perform hello following steps.</span></span>

1. <span data-ttu-id="94381-110">Recuperar la base de datos de Azure Cosmos: API para obtener información de conexión de cuenta MongoDB utilizando instrucciones de hello [aquí](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="94381-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Captura de pantalla de hoja de cadena de conexión de Hola](./media/mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="94381-112">Ejecute *Robomongo.exe*.</span><span class="sxs-lookup"><span data-stu-id="94381-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="94381-113">Haga clic en el botón de conexión de hello en **archivo** toomanage las conexiones.</span><span class="sxs-lookup"><span data-stu-id="94381-113">Click hello connection button under **File** toomanage your connections.</span></span> <span data-ttu-id="94381-114">A continuación, haga clic en **crear** en hello **las conexiones de MongoDB** ventana, que se abrirá hello **configuración de conexión** ventana.</span><span class="sxs-lookup"><span data-stu-id="94381-114">Then, click **Create** in hello **MongoDB Connections** window, which will open up hello **Connection Settings** window.</span></span>

4. <span data-ttu-id="94381-115">Hola **configuración de conexión** ventana, elija un nombre.</span><span class="sxs-lookup"><span data-stu-id="94381-115">In hello **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="94381-116">A continuación, busque hello **Host** y **puerto** de la información de conexión en el paso 1 y escribirlos en **dirección** y **puerto**, respectivamente .</span><span class="sxs-lookup"><span data-stu-id="94381-116">Then, find hello **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![Captura de pantalla de hello Robomongo administrar conexiones](./media/mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="94381-118">En hello **autenticación** , haga clic en **realizar autenticación**.</span><span class="sxs-lookup"><span data-stu-id="94381-118">On hello **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="94381-119">Después, escriba la base de datos (el valor predeterminado es *Admin*), el **nombre de usuario** y la **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="94381-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="94381-120">Tanto el **nombre de usuario** como la **contraseña** están en la información de conexión del paso 1.</span><span class="sxs-lookup"><span data-stu-id="94381-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Captura de pantalla de hello Robomongo ficha de autenticación](./media/mongodb-robomongo/authentication.png)
6. <span data-ttu-id="94381-122">En hello **SSL** ficha, verificación **usar protocolo SSL**, a continuación, cambie hello **método de autenticación** demasiado**certificado autofirmado**.</span><span class="sxs-lookup"><span data-stu-id="94381-122">On hello **SSL** tab, check **Use SSL protocol**, then change hello **Authentication Method** too**Self-signed Certificate**.</span></span>

    ![Captura de pantalla de hello Robomongo SSL pestaña](./media/mongodb-robomongo/SSL.png)
7. <span data-ttu-id="94381-124">Por último, haga clic en **prueba** tooverify que es capaz de tooconnect, a continuación, **guardar**.</span><span class="sxs-lookup"><span data-stu-id="94381-124">Finally, click **Test** tooverify that you are able tooconnect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94381-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="94381-125">Next steps</span></span>
* <span data-ttu-id="94381-126">Explore [ejemplos](mongodb-samples.md) de Azure Cosmos DB: API para MongoDB.</span><span class="sxs-lookup"><span data-stu-id="94381-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
