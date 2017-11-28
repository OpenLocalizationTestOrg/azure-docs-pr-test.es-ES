---
title: "Azure Cosmos DB: Compilación de una aplicación web con la autenticación de Xamarin y Facebook | Microsoft Docs"
description: "Presenta un ejemplo de código de .NET puede usar tooconnect tooand consultar la base de datos de Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a><span data-ttu-id="0575e-103">Azure Cosmos DB: Compilación de una aplicación web con la autenticación de .NET, Xamarin y Facebook</span><span class="sxs-lookup"><span data-stu-id="0575e-103">Azure Cosmos DB: Build a web app with .NET, Xamarin, and Facebook authentication</span></span>

<span data-ttu-id="0575e-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0575e-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="0575e-105">Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="0575e-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="0575e-106">Este inicio rápido muestra cómo toocreate una cuenta de base de datos de Azure Cosmos, la base de datos de documento y la colección mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0575e-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="0575e-107">A continuación, podrá compilar e implementar una aplicación de web de lista de tareas integrada en hello [API de .NET de DocumentDB](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/)y motor de autorización de base de datos de Azure Cosmos Hola.</span><span class="sxs-lookup"><span data-stu-id="0575e-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), and hello Azure Cosmos DB authorization engine.</span></span> <span data-ttu-id="0575e-108">aplicación de web de lista de tareas de Hello implementa un patrón de datos por el usuario que permite toologin de los usuarios mediante Facebook Auth y administrar sus propios elementos de toodo.</span><span class="sxs-lookup"><span data-stu-id="0575e-108">hello todo list web app implements a per-user data pattern that enables users toologin using Facebook Auth and manage their own toodo items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0575e-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0575e-109">Prerequisites</span></span>

<span data-ttu-id="0575e-110">Si aún no tiene Visual Studio de 2017 instalado, puede descargar y usar hello **libre** [2017 Community Edition de Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0575e-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="0575e-111">Asegúrese de que habilitar **desarrollo Azure** durante la instalación de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="0575e-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="0575e-112">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="0575e-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="0575e-113">Incorporación de una colección</span><span class="sxs-lookup"><span data-stu-id="0575e-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="0575e-114">Clonar aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="0575e-114">Clone hello sample application</span></span>

<span data-ttu-id="0575e-115">Ahora vamos a clonar una API de documentos de aplicación de github, establezca la cadena de conexión de Hola y ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="0575e-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="0575e-116">Podrá ver lo fácil que es toowork con datos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="0575e-116">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="0575e-117">Abra una ventana de terminal de git, como git bash, y `cd` tooa directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0575e-117">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="0575e-118">Ejecute hello después de repositorio de ejemplo de comando tooclone Hola.</span><span class="sxs-lookup"><span data-stu-id="0575e-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. <span data-ttu-id="0575e-119">A continuación, abra el archivo DocumentDBTodo.sln de hello de carpeta de samples/xamarin/UserItems/xamarin.forms de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0575e-119">Then open hello DocumentDBTodo.sln file from hello samples/xamarin/UserItems/xamarin.forms folder in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="0575e-120">Revise el código de hello</span><span class="sxs-lookup"><span data-stu-id="0575e-120">Review hello code</span></span>

<span data-ttu-id="0575e-121">contiene el código de Hello en la carpeta de hello Xamarin:</span><span class="sxs-lookup"><span data-stu-id="0575e-121">hello code in hello Xamarin folder contains:</span></span>

* <span data-ttu-id="0575e-122">Aplicación de Xamarin.</span><span class="sxs-lookup"><span data-stu-id="0575e-122">Xamarin app.</span></span> <span data-ttu-id="0575e-123">aplicación Hello almacena elementos de lista de tareas del usuario de hello en una colección con particiones denominada UserItems.</span><span class="sxs-lookup"><span data-stu-id="0575e-123">hello app stores hello user's todo items in a partitioned collection named UserItems.</span></span>
* <span data-ttu-id="0575e-124">Resource token broker API.</span><span class="sxs-lookup"><span data-stu-id="0575e-124">Resource token broker API.</span></span> <span data-ttu-id="0575e-125">Un recurso de base de datos de Azure Cosmos de toobroker simple de ASP.NET Web API tokens toohello registrado en los usuarios de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0575e-125">A simple ASP.NET Web API toobroker Azure Cosmos DB resource tokens toohello logged in users of hello app.</span></span> <span data-ttu-id="0575e-126">Tokens de recursos son tokens de acceso de corta duración que brindan aplicación hello Hola acceso toohello registrado en los datos del usuario.</span><span class="sxs-lookup"><span data-stu-id="0575e-126">Resource tokens are short-lived access tokens that provide hello app with hello access toohello logged in user's data.</span></span>

<span data-ttu-id="0575e-127">Hola autenticación y flujo de datos se muestra en el siguiente diagrama de Hola.</span><span class="sxs-lookup"><span data-stu-id="0575e-127">hello authentication and data flow is illustrated in hello diagram below.</span></span>

* <span data-ttu-id="0575e-128">Hola UserItems colección se crea con la clave de partición de hello ' / userid'.</span><span class="sxs-lookup"><span data-stu-id="0575e-128">hello UserItems collection is created with hello partition key '/userid'.</span></span> <span data-ttu-id="0575e-129">Especificar que una clave de partición para una colección permite tooscale de base de datos de Azure Cosmos infinitamente como número de Hola de usuarios y elementos aumenta de tamaño.</span><span class="sxs-lookup"><span data-stu-id="0575e-129">Specifying a partition key for a collection allows Azure Cosmos DB tooscale infinitely as hello number of users and items grows.</span></span>
* <span data-ttu-id="0575e-130">aplicación de Xamarin Hello permite toologin a los usuarios con credenciales de Facebook.</span><span class="sxs-lookup"><span data-stu-id="0575e-130">hello Xamarin app allows users toologin with Facebook credentials.</span></span>
* <span data-ttu-id="0575e-131">aplicación de Xamarin Hello usa tooauthenticate de token de acceso de Facebook con API de ResourceTokenBroker</span><span class="sxs-lookup"><span data-stu-id="0575e-131">hello Xamarin app uses Facebook access token tooauthenticate with ResourceTokenBroker API</span></span>
* <span data-ttu-id="0575e-132">broker de token de recurso de Hello API autentica mediante la característica de autenticación de servicio de la aplicación de solicitud de Hola y solicita un token de recurso de base de datos de Azure Cosmos con documentos de tooall de acceso de lectura/escritura compartir la clave de partición del usuario autenticado de Hola.</span><span class="sxs-lookup"><span data-stu-id="0575e-132">hello resource token broker API authenticates hello request using App Service Auth feature, and requests an Azure Cosmos DB resource token with read/write access tooall documents sharing hello authenticated user's partition key.</span></span>
* <span data-ttu-id="0575e-133">Broker de token de recurso devuelve aplicación de cliente de hello recursos toohello símbolo (token).</span><span class="sxs-lookup"><span data-stu-id="0575e-133">Resource token broker returns hello resource token toohello client app.</span></span>
* <span data-ttu-id="0575e-134">aplicación Hello tiene acceso a elementos de tareas del usuario de hello mediante el token de recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="0575e-134">hello app accesses hello user's todo items using hello resource token.</span></span>

![Aplicación de tareas pendientes con datos de ejemplo](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a><span data-ttu-id="0575e-136">Actualizar la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="0575e-136">Update your connection string</span></span>

<span data-ttu-id="0575e-137">Ahora vuelva atrás toohello tooget portal Azure la información de la cadena de conexión y se copia en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0575e-137">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="0575e-138">Hola [portal de Azure](http://portal.azure.com/), en la base de datos de Azure Cosmos account, Hola barra de navegación izquierda, haga clic en **claves**y, a continuación, haga clic en **claves de lectura y escritura**.</span><span class="sxs-lookup"><span data-stu-id="0575e-138">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="0575e-139">Deberá usar botones de copia de hello en hello derecha de hello toocopy de pantalla Hola URI y la clave principal en el archivo Web.config de hello en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="0575e-139">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello Web.config file in hello next step.</span></span>

    ![Ver y copiar una clave de acceso en hello portal de Azure, hoja de claves](./media/create-documentdb-xamarin-dotnet/keys.png)

2. <span data-ttu-id="0575e-141">En 2017 de Visual Studio, abra el archivo Web.config de hello en la carpeta de azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker de Hola.</span><span class="sxs-lookup"><span data-stu-id="0575e-141">In Visual Studio 2017, open hello Web.config file in hello azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker folder.</span></span> 

3. <span data-ttu-id="0575e-142">Copie el valor URI de portal hello (mediante el botón Copiar de Hola) y hacerla Hola valo accountUrl hello en el archivo Web.config.</span><span class="sxs-lookup"><span data-stu-id="0575e-142">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello accountUrl in Web.config.</span></span> 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. <span data-ttu-id="0575e-143">A continuación, copie el valor de clave principal del portal de Hola y hacerla Hola valo hello accountKey en Web.congif.</span><span class="sxs-lookup"><span data-stu-id="0575e-143">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello accountKey in Web.congif.</span></span> 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

<span data-ttu-id="0575e-144">Ahora ha actualizado la aplicación con toda la información de hello debe toocommunicate con base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0575e-144">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="build-and-deploy-hello-web-app"></a><span data-ttu-id="0575e-145">Compilar e implementar la aplicación web de hello</span><span class="sxs-lookup"><span data-stu-id="0575e-145">Build and deploy hello web app</span></span>

1. <span data-ttu-id="0575e-146">Hola portal de Azure, crear a un servicio de aplicación sitio Web toohost Hola recursos token broker API.</span><span class="sxs-lookup"><span data-stu-id="0575e-146">In hello Azure portal, create an App Service website toohost hello Resource token broker API.</span></span>
2. <span data-ttu-id="0575e-147">En hello portal de Azure, abra la hoja de configuración de la aplicación hello del agente de token de recurso de hello sitio Web de API de.</span><span class="sxs-lookup"><span data-stu-id="0575e-147">In hello Azure portal, open hello App Settings blade of hello Resource token broker API website.</span></span> <span data-ttu-id="0575e-148">Rellene Hola después de la configuración de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="0575e-148">Fill in hello following app settings:</span></span>

    * <span data-ttu-id="0575e-149">accountUrl - URL hello de la cuenta de base de datos de Azure Cosmos desde la pestaña de claves de saludo de la cuenta de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0575e-149">accountUrl - hello Azure Cosmos DB account URL from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="0575e-150">accountKey - clave maestra de la cuenta de la base de datos de Azure Cosmos Hola desde la pestaña de claves de saludo de la cuenta de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0575e-150">accountKey - hello Azure Cosmos DB account master key from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="0575e-151">databaseId y collectionId de la base de datos y de la colección creadas</span><span class="sxs-lookup"><span data-stu-id="0575e-151">databaseId and collectionId of your created database and collection</span></span>

3. <span data-ttu-id="0575e-152">Publicar hello ResourceTokenBroker solución tooyour creado sitio Web.</span><span class="sxs-lookup"><span data-stu-id="0575e-152">Publish hello ResourceTokenBroker solution tooyour created website.</span></span>

4. <span data-ttu-id="0575e-153">Abra el proyecto de Xamarin hello y navegue tooTodoItemManager.cs.</span><span class="sxs-lookup"><span data-stu-id="0575e-153">Open hello Xamarin project, and navigate tooTodoItemManager.cs.</span></span> <span data-ttu-id="0575e-154">Rellene los valores de hello para accountURL, collectionId, databaseId, así como resourceTokenBrokerURL como dirección url base https de hello para el sitio Web de broker de token de recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="0575e-154">Fill in hello values for accountURL, collectionId, databaseId, as well as resourceTokenBrokerURL as hello base https url for hello resource token broker website.</span></span>

5. <span data-ttu-id="0575e-155">Hola completa [cómo tooconfigure su inicio de sesión de servicio de aplicaciones aplicación toouse Facebook](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) toosetup tutorial autenticación de Facebook y configurar el sitio Web de ResourceTokenBroker Hola.</span><span class="sxs-lookup"><span data-stu-id="0575e-155">Complete hello [How tooconfigure your App Service application toouse Facebook login](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) tutorial toosetup Facebook authentication and configure hello ResourceTokenBroker website.</span></span>

    <span data-ttu-id="0575e-156">Ejecute la aplicación de Xamarin hello.</span><span class="sxs-lookup"><span data-stu-id="0575e-156">Run hello Xamarin app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="0575e-157">Revise los SLA de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0575e-157">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="0575e-158">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="0575e-158">Clean up resources</span></span>

<span data-ttu-id="0575e-159">Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="0575e-159">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="0575e-160">En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="0575e-160">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you just created.</span></span> 
2. <span data-ttu-id="0575e-161">En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="0575e-161">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0575e-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0575e-162">Next steps</span></span>

<span data-ttu-id="0575e-163">En este tutorial, ha aprendido cómo crear una colección mediante Hola Explorador de datos, toocreate una cuenta de base de datos de Azure Cosmos y compilar e implementar una aplicación de Xamarin.</span><span class="sxs-lookup"><span data-stu-id="0575e-163">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and build and deploy a Xamarin app.</span></span> <span data-ttu-id="0575e-164">Ahora puede importar la cuenta de base de datos de Cosmos tooyour datos adicionales.</span><span class="sxs-lookup"><span data-stu-id="0575e-164">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="0575e-165">Importación de datos a Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0575e-165">Import data into Azure Cosmos DB</span></span>](import-data.md)
