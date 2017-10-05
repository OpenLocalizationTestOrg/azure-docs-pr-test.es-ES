---
title: "Creación de una aplicación web de Node.js en Azure | Microsoft Docs"
description: "Implementación de su primera aplicación Hola mundo de Node.js en Azure App Service Web Apps en cuestión de minutos."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 582bb3c2-164b-42f5-b081-95bfcb7a502a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/05/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: ce845da09a7c088b8a2ba29b818a46a3b41aa4e7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a><span data-ttu-id="ceeb4-103">Creación de una aplicación web de Node.js en Azure</span><span class="sxs-lookup"><span data-stu-id="ceeb4-103">Create a Node.js web app in Azure</span></span>

<span data-ttu-id="ceeb4-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="ceeb4-105">En esta guía de inicio rápido se explica cómo se implementa una aplicación de Node.js en Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-105">This quickstart shows how to deploy a Node.js app to Azure Web Apps.</span></span> <span data-ttu-id="ceeb4-106">Se crea la aplicación web con la [CLI de Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) y se usa Git para implementar el código Node.js de ejemplo en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample Node.js code to the web app.</span></span>

![Aplicación de ejemplo que se ejecuta en Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="ceeb4-108">Estos pasos se pueden realizar con un equipo Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="ceeb4-109">Una vez instalados los requisitos previos, tardará aproximadamente cinco minutos en completar los pasos.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a><span data-ttu-id="ceeb4-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ceeb4-110">Prerequisites</span></span>

<span data-ttu-id="ceeb4-111">Para completar esta guía de inicio rápido:</span><span class="sxs-lookup"><span data-stu-id="ceeb4-111">To complete this quickstart:</span></span>

* [<span data-ttu-id="ceeb4-112">Instalación de Git</span><span class="sxs-lookup"><span data-stu-id="ceeb4-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="ceeb4-113">Instalación de Node.js y NPM</span><span class="sxs-lookup"><span data-stu-id="ceeb4-113">Install Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ceeb4-114">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ceeb4-115">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="ceeb4-116">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ceeb4-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="ceeb4-117">Descarga del ejemplo</span><span class="sxs-lookup"><span data-stu-id="ceeb4-117">Download the sample</span></span>

<span data-ttu-id="ceeb4-118">En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de la aplicación de ejemplo en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-118">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

<span data-ttu-id="ceeb4-119">Utilice esta ventana de terminal para ejecutar todos los comandos de esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-119">You use this terminal window to run all the commands in this quickstart.</span></span>

<span data-ttu-id="ceeb4-120">Cambie al directorio que contiene el código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-120">Change to the directory that contains the sample code.</span></span>

```bash
cd nodejs-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="ceeb4-121">Ejecución de la aplicación de forma local</span><span class="sxs-lookup"><span data-stu-id="ceeb4-121">Run the app locally</span></span>

<span data-ttu-id="ceeb4-122">Ejecute la aplicación localmente abriendo una ventana de terminal y utilizando el script `npm start` para iniciar el servidor HTTP de Node.js integrado.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-122">Run the application locally by opening a terminal window and using the `npm start` script to launch the built in Node.js HTTP server.</span></span>

```bash
npm start
```

<span data-ttu-id="ceeb4-123">Abra un explorador web y navegue a la aplicación de ejemplo en http://localhost:1337.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-123">Open a web browser, and navigate to the sample app at http://localhost:1337.</span></span>

<span data-ttu-id="ceeb4-124">Verá el mensaje **Hola mundo** de la aplicación de ejemplo que aparece en la página.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-124">You see the **Hello World** message from the sample app displayed in the page.</span></span>

![Aplicación de ejemplo que se ejecuta localmente](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

<span data-ttu-id="ceeb4-126">En la ventana de terminal, presione **Ctrl + C** para salir del servidor web.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-126">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Página de la aplicación web vacía](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="ceeb4-128">Ha creado una nueva aplicación web vacía en Azure.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-128">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (21/21), done.
Writing objects: 100% (23/23), 3.71 KiB | 0 bytes/s, done.
Total 23 (delta 8), reused 7 (delta 1)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'bf114df591'.
remote: Generating deployment script.
remote: Generating deployment script for node.js Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling node.js deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.js'
remote: Copying file: 'package.json'
remote: Copying file: 'process.json'
remote: Deleting file: 'hostingstart.html'
remote: Ignoring: .git
remote: Using start-up script index.js from package.json.
remote: Node.js versions available on the platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file to choose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="ceeb4-129">Navegación hasta la aplicación</span><span class="sxs-lookup"><span data-stu-id="ceeb4-129">Browse to the app</span></span>

<span data-ttu-id="ceeb4-130">Vaya a la aplicación implementada mediante el explorador web.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-130">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="ceeb4-131">El código de ejemplo de Node.js se está ejecutando en una aplicación web de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-131">The Node.js sample code is running in an Azure App Service web app.</span></span>

![Aplicación de ejemplo que se ejecuta en Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="ceeb4-133">**¡Enhorabuena!**</span><span class="sxs-lookup"><span data-stu-id="ceeb4-133">**Congratulations!**</span></span> <span data-ttu-id="ceeb4-134">Ha implementado la primera aplicación de Node.js en App Service.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-134">You've deployed your first Node.js app to App Service.</span></span>

## <a name="update-and-redeploy-the-code"></a><span data-ttu-id="ceeb4-135">Actualización del código y nueva implementación</span><span class="sxs-lookup"><span data-stu-id="ceeb4-135">Update and redeploy the code</span></span>

<span data-ttu-id="ceeb4-136">Con un editor de texto, abra el archivo `index.js` en la aplicación de Node.js y realice un pequeño cambio en el texto en la llamada a `response.end`:</span><span class="sxs-lookup"><span data-stu-id="ceeb4-136">Using a text editor, open the `index.js` file in the Node.js app, and make a small change to the text in the call to `response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="ceeb4-137">Confirme los cambios en Git y, después, inserte los cambios de código en Azure.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-137">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="ceeb4-138">Una vez que la implementación haya finalizado, vuelva a cambiar la ventana del explorador que se abrió en el paso **Navegación hasta la aplicación** y actualice la vista.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-138">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and hit refresh.</span></span>

![Aplicación de ejemplo actualizada que se ejecuta en Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="ceeb4-140">Administración de la nueva aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="ceeb4-140">Manage your new Azure web app</span></span>

<span data-ttu-id="ceeb4-141">Vaya a <a href="https://portal.azure.com" target="_blank">Azure Portal</a> para administrar la aplicación web que ha creado.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-141">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="ceeb4-142">En el menú izquierdo, haga clic en **App Services** y, a continuación, haga clic en el nombre de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-142">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Navegación desde el portal a la aplicación web de Azure](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="ceeb4-144">Podrá ver la página de información general de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-144">You see your web app's Overview page.</span></span> <span data-ttu-id="ceeb4-145">En este caso, puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-145">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Hoja de App Service en Azure Portal](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="ceeb4-147">El menú izquierdo proporciona distintas páginas para configurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ceeb4-147">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="ceeb4-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ceeb4-148">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ceeb4-149">Node.js con MongoDB</span><span class="sxs-lookup"><span data-stu-id="ceeb4-149">Node.js with MongoDB</span></span>](app-service-web-tutorial-nodejs-mongodb-app.md)
