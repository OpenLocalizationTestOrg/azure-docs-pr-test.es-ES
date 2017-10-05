---
title: "Cadena de conexión de MongoDB para una cuenta de Azure Cosmos DB | Microsoft Docs"
description: "Aprenda a conectar su aplicación de MongoDB a una cuenta de Azure Cosmos DB mediante una cadena de conexión de MongoDB."
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
ms.openlocfilehash: 5a47001705531d971d3181df9c0aa8f957168845
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-mongodb-application-to-azure-cosmos-db"></a><span data-ttu-id="7cac4-104">Conectar una aplicación de MongoDB a Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7cac4-104">Connect a MongoDB application to Azure Cosmos DB</span></span>
<span data-ttu-id="7cac4-105">Aprenda a conectar su aplicación de MongoDB a una cuenta de Azure Cosmos DB mediante una cadena de conexión de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7cac4-105">Learn how to connect your MongoDB app to an Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="7cac4-106">Después, puede usar una base de datos de Azure Cosmos DB como almacén de datos de la aplicación MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7cac4-106">You can then use an Azure Cosmos DB database as the data store for your MongoDB app.</span></span> 

<span data-ttu-id="7cac4-107">En este tutorial se proporcionan dos maneras de recuperar información de la cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="7cac4-107">This tutorial provides two ways to retrieve connection string information:</span></span>

- <span data-ttu-id="7cac4-108">[El método de inicio rápido](#QuickstartConnection), para su uso con controladores de .NET, Node.js, MongoDB Shell, Java y Python.</span><span class="sxs-lookup"><span data-stu-id="7cac4-108">[The quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="7cac4-109">[El método de la cadena de conexión personalizada](#GetCustomConnection), para su uso con otros controladores.</span><span class="sxs-lookup"><span data-stu-id="7cac4-109">[The custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cac4-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7cac4-110">Prerequisites</span></span>

- <span data-ttu-id="7cac4-111">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="7cac4-111">An Azure account.</span></span> <span data-ttu-id="7cac4-112">Si no tiene una cuenta de Azure, cree ahora una [cuenta de Azure gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="7cac4-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="7cac4-113">Una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7cac4-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="7cac4-114">Para obtener instrucciones, vea [Compilar una aplicación web de API MongoDB con .NET y Azure Portal](create-mongodb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="7cac4-114">For instructions, see [Build a MongoDB API web app with .NET and the Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="7cac4-115"><a id="QuickstartConnection"></a>Obtener la cadena de conexión de MongoDB mediante el menú de inicio rápido</span><span class="sxs-lookup"><span data-stu-id="7cac4-115"><a id="QuickstartConnection"></a>Get the MongoDB connection string by using the quick start</span></span>
1. <span data-ttu-id="7cac4-116">En un explorador de Internet, inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7cac4-116">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7cac4-117">En la hoja **Azure Cosmos DB**, seleccione la API de la cuenta de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7cac4-117">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="7cac4-118">En el panel izquierdo de la hoja de la cuenta, haga clic en **Inicio rápido**.</span><span class="sxs-lookup"><span data-stu-id="7cac4-118">In the left pane of the account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="7cac4-119">Elija la plataforma (**.NET**, **Node.js**, **Shell de MongoDB**, **Java**, **Python**).</span><span class="sxs-lookup"><span data-stu-id="7cac4-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="7cac4-120">Si no ve el controlador o la herramienta en la lista, no se preocupe, documentamos constantemente más fragmentos de código de conexión.</span><span class="sxs-lookup"><span data-stu-id="7cac4-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="7cac4-121">Comente a continuación lo que le gustaría ver.</span><span class="sxs-lookup"><span data-stu-id="7cac4-121">Please comment below on what you'd like to see.</span></span> <span data-ttu-id="7cac4-122">Para aprender a crear su propia conexión, lea la sección sobre cómo [obtener información de la cadena de conexión de la cuenta](#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="7cac4-122">To learn how to craft your own connection, read [Get the account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="7cac4-123">Copie y pegue el fragmento de código en la aplicación MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7cac4-123">Copy and paste the code snippet into your MongoDB app.</span></span>

    ![Hoja de inicio rápido](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="7cac4-125"><a id="GetCustomConnection"></a> Obtención de la cadena de conexión de MongoDB para personalizar</span><span class="sxs-lookup"><span data-stu-id="7cac4-125"><a id="GetCustomConnection"></a> Get the MongoDB connection string to customize</span></span>
1. <span data-ttu-id="7cac4-126">En un explorador de Internet, inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7cac4-126">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7cac4-127">En la hoja **Azure Cosmos DB**, seleccione la API de la cuenta de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7cac4-127">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="7cac4-128">En el panel izquierdo de la hoja de la cuenta, haga clic en **Cadena de conexión**.</span><span class="sxs-lookup"><span data-stu-id="7cac4-128">In the left pane of the account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="7cac4-129">Se abre la hoja **Cadena de conexión**,</span><span class="sxs-lookup"><span data-stu-id="7cac4-129">The **Connection String** blade opens.</span></span> <span data-ttu-id="7cac4-130">que contiene toda la información necesaria para conectarse a la cuenta con un controlador para MongoDB, incluida una cadena de conexión precreada.</span><span class="sxs-lookup"><span data-stu-id="7cac4-130">It has all the information necessary to connect to the account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![Hoja Cadena de conexión](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="7cac4-132">Requisitos de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="7cac4-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="7cac4-133">Azure Cosmos DB tiene estándares y requisitos de seguridad estrictos.</span><span class="sxs-lookup"><span data-stu-id="7cac4-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="7cac4-134">Las cuentas de Azure Cosmos DB requieren autenticación y comunicación segura a través de *SSL*.</span><span class="sxs-lookup"><span data-stu-id="7cac4-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="7cac4-135">Azure Cosmos DB admite el formato estándar de URI de cadena de conexión de MongoDB, con un par de requisitos específicos: las cuentas de Azure Cosmos DB requieren autenticación y comunicación segura mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="7cac4-135">Azure Cosmos DB supports the standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="7cac4-136">Por tanto, el formato de la cadena de conexión es:</span><span class="sxs-lookup"><span data-stu-id="7cac4-136">So, the connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="7cac4-137">Los valores de esta cadena están disponibles en la hoja **Cadena de conexión** mostrada antes:</span><span class="sxs-lookup"><span data-stu-id="7cac4-137">The values of this string are available in the **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="7cac4-138">Username (obligatorio): nombre de la cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7cac4-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="7cac4-139">Password (obligatorio): contraseña de la cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7cac4-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="7cac4-140">Host (obligatorio): FQDN de la cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7cac4-140">Host (required): FQDN of the Azure Cosmos DB account.</span></span>
* <span data-ttu-id="7cac4-141">Port (obligatorio): 10255.</span><span class="sxs-lookup"><span data-stu-id="7cac4-141">Port (required): 10255.</span></span>
* <span data-ttu-id="7cac4-142">Database (opcional): base de datos que usa la conexión.</span><span class="sxs-lookup"><span data-stu-id="7cac4-142">Database (optional): The database that the connection uses.</span></span> <span data-ttu-id="7cac4-143">Si no se proporciona ninguna base de datos, la base de datos predeterminada es "test".</span><span class="sxs-lookup"><span data-stu-id="7cac4-143">If no database is provided, the default database is "test."</span></span>
* <span data-ttu-id="7cac4-144">ssl=true (obligatorio)</span><span class="sxs-lookup"><span data-stu-id="7cac4-144">ssl=true (required)</span></span>

<span data-ttu-id="7cac4-145">Por ejemplo, considere la cuenta que aparece en la hoja **Cadena de conexión**.</span><span class="sxs-lookup"><span data-stu-id="7cac4-145">For example, consider the account shown in the **Connection String** blade.</span></span> <span data-ttu-id="7cac4-146">Una cadena de conexión válida es:</span><span class="sxs-lookup"><span data-stu-id="7cac4-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="7cac4-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7cac4-147">Next steps</span></span>
* <span data-ttu-id="7cac4-148">Obtenga información sobre cómo [usar MongoChef](mongodb-mongochef.md) con una API de Azure Cosmos DB para una cuenta de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7cac4-148">Learn how to [use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="7cac4-149">Explore [ejemplos](mongodb-samples.md) de la API de Azure Cosmos DB para MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7cac4-149">Explore the Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
