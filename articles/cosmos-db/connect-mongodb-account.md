---
title: "cadena de conexión de aaaMongoDB para una cuenta de base de datos de Azure Cosmos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconnect su tooan de aplicación de MongoDB base de datos de Azure Cosmos cuenta a través de una cadena de conexión de MongoDB."
keywords: "cadena de conexión de mongodb"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a><span data-ttu-id="47414-104">Conectar un tooAzure de aplicación de MongoDB Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="47414-104">Connect a MongoDB application tooAzure Cosmos DB</span></span>
<span data-ttu-id="47414-105">Obtenga información acerca de cómo tooconnect su tooan de aplicación de MongoDB base de datos de Azure Cosmos cuenta a través de una cadena de conexión de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="47414-105">Learn how tooconnect your MongoDB app tooan Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="47414-106">A continuación, puede usar una base de datos de la base de datos de Azure Cosmos como datos de hello almacenar para la aplicación de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="47414-106">You can then use an Azure Cosmos DB database as hello data store for your MongoDB app.</span></span> 

<span data-ttu-id="47414-107">Este tutorial proporciona tooretrieve información de la cadena de conexión de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="47414-107">This tutorial provides two ways tooretrieve connection string information:</span></span>

- <span data-ttu-id="47414-108">[Hola quick start (método)](#QuickstartConnection), para su uso con controladores. NET, Node.js, MongoDB Shell, Java y Python</span><span class="sxs-lookup"><span data-stu-id="47414-108">[hello quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="47414-109">[Hola método de cadena de conexión personalizada](#GetCustomConnection), para su uso con otros controladores</span><span class="sxs-lookup"><span data-stu-id="47414-109">[hello custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47414-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="47414-110">Prerequisites</span></span>

- <span data-ttu-id="47414-111">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="47414-111">An Azure account.</span></span> <span data-ttu-id="47414-112">Si no tiene una cuenta de Azure, cree ahora una [cuenta de Azure gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="47414-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="47414-113">Una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47414-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="47414-114">Para obtener instrucciones, consulte [compilar una aplicación web de API de MongoDB con .NET y Hola portal de Azure](create-mongodb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="47414-114">For instructions, see [Build a MongoDB API web app with .NET and hello Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="47414-115"><a id="QuickstartConnection"></a>Obtener cadena de conexión de MongoDB hello mediante Inicio rápido de Hola</span><span class="sxs-lookup"><span data-stu-id="47414-115"><a id="QuickstartConnection"></a>Get hello MongoDB connection string by using hello quick start</span></span>
1. <span data-ttu-id="47414-116">En un explorador de Internet, inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="47414-116">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="47414-117">Hola **base de datos de Azure Cosmos** hoja, seleccione Hola API para la cuenta de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="47414-117">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="47414-118">En el panel izquierdo de Hola de hoja de la cuenta de hello, haga clic en **inicio rápido**.</span><span class="sxs-lookup"><span data-stu-id="47414-118">In hello left pane of hello account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="47414-119">Elija la plataforma (**.NET**, **Node.js**, **Shell de MongoDB**, **Java**, **Python**).</span><span class="sxs-lookup"><span data-stu-id="47414-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="47414-120">Si no ve el controlador o la herramienta en la lista, no se preocupe, documentamos constantemente más fragmentos de código de conexión.</span><span class="sxs-lookup"><span data-stu-id="47414-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="47414-121">Comentar a continuación, en lo que gustaría toosee.</span><span class="sxs-lookup"><span data-stu-id="47414-121">Please comment below on what you'd like toosee.</span></span> <span data-ttu-id="47414-122">toolearn cómo toocraft su propia conexión, leer [obtener información de cadena de conexión de la cuenta de hello](#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="47414-122">toolearn how toocraft your own connection, read [Get hello account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="47414-123">Copie y pegue el fragmento de código de hello en la aplicación de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="47414-123">Copy and paste hello code snippet into your MongoDB app.</span></span>

    ![Hoja de inicio rápido](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="47414-125"><a id="GetCustomConnection"></a>Obtener toocustomize de cadena de conexión de MongoDB Hola</span><span class="sxs-lookup"><span data-stu-id="47414-125"><a id="GetCustomConnection"></a> Get hello MongoDB connection string toocustomize</span></span>
1. <span data-ttu-id="47414-126">En un explorador de Internet, inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="47414-126">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="47414-127">Hola **base de datos de Azure Cosmos** hoja, seleccione Hola API para la cuenta de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="47414-127">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="47414-128">En el panel izquierdo de Hola de hoja de la cuenta de hello, haga clic en **cadena de conexión**.</span><span class="sxs-lookup"><span data-stu-id="47414-128">In hello left pane of hello account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="47414-129">Hola **cadena de conexión** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="47414-129">hello **Connection String** blade opens.</span></span> <span data-ttu-id="47414-130">Tiene todos los Hola información necesarios tooconnect toohello cuenta con un controlador para MongoDB, incluida una cadena de conexión preconstructed.</span><span class="sxs-lookup"><span data-stu-id="47414-130">It has all hello information necessary tooconnect toohello account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![Hoja Cadena de conexión](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="47414-132">Requisitos de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="47414-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="47414-133">Azure Cosmos DB tiene estándares y requisitos de seguridad estrictos.</span><span class="sxs-lookup"><span data-stu-id="47414-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="47414-134">Las cuentas de Azure Cosmos DB requieren autenticación y comunicación segura a través de *SSL*.</span><span class="sxs-lookup"><span data-stu-id="47414-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="47414-135">Base de datos de Azure Cosmos admite Hola MongoDB conexión cadena URI formato estándar, con un par de requisitos específicos: cuentas de base de datos de Azure Cosmos requieren autenticación y comunicación segura mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="47414-135">Azure Cosmos DB supports hello standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="47414-136">Por lo tanto, el formato de cadena de conexión de hello es:</span><span class="sxs-lookup"><span data-stu-id="47414-136">So, hello connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="47414-137">valores de Hello de esta cadena están disponibles en hello **cadena de conexión** hoja mostrada anteriormente:</span><span class="sxs-lookup"><span data-stu-id="47414-137">hello values of this string are available in hello **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="47414-138">Username (obligatorio): nombre de la cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47414-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="47414-139">Password (obligatorio): contraseña de la cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47414-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="47414-140">Host (obligatorio): el FQDN de la cuenta de base de datos de Azure Cosmos Hola.</span><span class="sxs-lookup"><span data-stu-id="47414-140">Host (required): FQDN of hello Azure Cosmos DB account.</span></span>
* <span data-ttu-id="47414-141">Port (obligatorio): 10255.</span><span class="sxs-lookup"><span data-stu-id="47414-141">Port (required): 10255.</span></span>
* <span data-ttu-id="47414-142">(Opcional) de la base de datos: base de datos de Hola que Hola conexión utiliza.</span><span class="sxs-lookup"><span data-stu-id="47414-142">Database (optional): hello database that hello connection uses.</span></span> <span data-ttu-id="47414-143">Si no se proporciona ninguna base de datos, base de datos de hello predeterminada es "test".</span><span class="sxs-lookup"><span data-stu-id="47414-143">If no database is provided, hello default database is "test."</span></span>
* <span data-ttu-id="47414-144">ssl=true (obligatorio)</span><span class="sxs-lookup"><span data-stu-id="47414-144">ssl=true (required)</span></span>

<span data-ttu-id="47414-145">Por ejemplo, considere la posibilidad de cuenta de hello mostrado en hello **cadena de conexión** hoja.</span><span class="sxs-lookup"><span data-stu-id="47414-145">For example, consider hello account shown in hello **Connection String** blade.</span></span> <span data-ttu-id="47414-146">Una cadena de conexión válida es:</span><span class="sxs-lookup"><span data-stu-id="47414-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="47414-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="47414-147">Next steps</span></span>
* <span data-ttu-id="47414-148">Obtenga información acerca de cómo demasiado[usar MongoChef](mongodb-mongochef.md) con una API de base de datos de Azure Cosmos para cuenta de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="47414-148">Learn how too[use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="47414-149">Explorar Hola API de base de datos de Azure Cosmos para MongoDB observando [ejemplos](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="47414-149">Explore hello Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
