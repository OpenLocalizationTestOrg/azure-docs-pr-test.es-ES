---
title: "aaaCreate una aplicación web de Node.js en Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 163edf83b2353755fc9fa2d75aed489038cf7c81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a><span data-ttu-id="f635e-103">Creación de una aplicación web de Node.js en Azure</span><span class="sxs-lookup"><span data-stu-id="f635e-103">Create a Node.js web app in Azure</span></span>

<span data-ttu-id="f635e-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="f635e-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="f635e-105">Este tutorial rápido muestra cómo toodeploy una tooAzure de aplicación Node.js aplicaciones Web.</span><span class="sxs-lookup"><span data-stu-id="f635e-105">This quickstart shows how toodeploy a Node.js app tooAzure Web Apps.</span></span> <span data-ttu-id="f635e-106">Crear una aplicación de web de hello usando hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), y usar Git toodeploy ejemplo Node.js código toohello web app.</span><span class="sxs-lookup"><span data-stu-id="f635e-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Node.js code toohello web app.</span></span>

![Aplicación de ejemplo que se ejecuta en Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="f635e-108">Puede seguir pasos de hello siguientes a través de un equipo Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="f635e-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="f635e-109">Una vez instalados los requisitos previos de hello, tarda aproximadamente cinco minutos toocomplete pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="f635e-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a><span data-ttu-id="f635e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f635e-110">Prerequisites</span></span>

<span data-ttu-id="f635e-111">toocomplete este tutorial rápido:</span><span class="sxs-lookup"><span data-stu-id="f635e-111">toocomplete this quickstart:</span></span>

* [<span data-ttu-id="f635e-112">Instalación de Git</span><span class="sxs-lookup"><span data-stu-id="f635e-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="f635e-113">Instalación de Node.js y NPM</span><span class="sxs-lookup"><span data-stu-id="f635e-113">Install Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f635e-114">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="f635e-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f635e-115">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="f635e-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f635e-116">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f635e-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="f635e-117">Descargar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="f635e-117">Download hello sample</span></span>

<span data-ttu-id="f635e-118">En una ventana de terminal, ejecute hello después comando tooclone Hola ejemplo aplicación repositorio tooyour equipo local.</span><span class="sxs-lookup"><span data-stu-id="f635e-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

<span data-ttu-id="f635e-119">Utilice esta ventana de terminal toorun todos los comandos de hello en este tutorial rápido.</span><span class="sxs-lookup"><span data-stu-id="f635e-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="f635e-120">Cambie el directorio toohello que contiene código de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f635e-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd nodejs-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="f635e-121">Ejecutar la aplicación hello localmente</span><span class="sxs-lookup"><span data-stu-id="f635e-121">Run hello app locally</span></span>

<span data-ttu-id="f635e-122">Ejecutar la aplicación hello localmente o abriendo una ventana de terminal y utilizando hello `npm start` hello toolaunch de secuencia de comandos integrada en el servidor HTTP de Node.js.</span><span class="sxs-lookup"><span data-stu-id="f635e-122">Run hello application locally by opening a terminal window and using hello `npm start` script toolaunch hello built in Node.js HTTP server.</span></span>

```bash
npm start
```

<span data-ttu-id="f635e-123">Abra un explorador web y navegar por la aplicación de ejemplo de toohello en http://localhost:1337.</span><span class="sxs-lookup"><span data-stu-id="f635e-123">Open a web browser, and navigate toohello sample app at http://localhost:1337.</span></span>

<span data-ttu-id="f635e-124">Vea hello **Hello World** mensaje desde la aplicación de ejemplo de Hola mostrado en la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="f635e-124">You see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![Aplicación de ejemplo que se ejecuta localmente](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

<span data-ttu-id="f635e-126">En la ventana de terminal, presione **Ctrl + C** servidor web de tooexit Hola.</span><span class="sxs-lookup"><span data-stu-id="f635e-126">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Página de la aplicación web vacía](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="f635e-128">Ha creado una nueva aplicación web vacía en Azure.</span><span class="sxs-lookup"><span data-stu-id="f635e-128">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up too4 threads.
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
remote: Node.js versions available on hello platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file toochoose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="f635e-129">Examinar toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="f635e-129">Browse toohello app</span></span>

<span data-ttu-id="f635e-130">Examinar toohello implementa la aplicación mediante el explorador web.</span><span class="sxs-lookup"><span data-stu-id="f635e-130">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="f635e-131">Hola Node.js código de ejemplo se ejecuta en una aplicación web de servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="f635e-131">hello Node.js sample code is running in an Azure App Service web app.</span></span>

![Aplicación de ejemplo que se ejecuta en Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="f635e-133">**¡Enhorabuena!**</span><span class="sxs-lookup"><span data-stu-id="f635e-133">**Congratulations!**</span></span> <span data-ttu-id="f635e-134">Ha implementado la primera tooApp de aplicación Node.js servicio.</span><span class="sxs-lookup"><span data-stu-id="f635e-134">You've deployed your first Node.js app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="f635e-135">Actualizar y volver a implementar código de hello</span><span class="sxs-lookup"><span data-stu-id="f635e-135">Update and redeploy hello code</span></span>

<span data-ttu-id="f635e-136">Con un editor de texto, abra hello `index.js` de archivos de aplicación de Node.js hello y realizar un pequeño cambio de texto toohello en llamada de hello demasiado`response.end`:</span><span class="sxs-lookup"><span data-stu-id="f635e-136">Using a text editor, open hello `index.js` file in hello Node.js app, and make a small change toohello text in hello call too`response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="f635e-137">Confirmar los cambios de Git y, a continuación, insertar tooAzure de cambios de código de hello.</span><span class="sxs-lookup"><span data-stu-id="f635e-137">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="f635e-138">Una vez completada la implementación, cambie toohello atrás ventana del explorador que abrió en hello **examinar toohello aplicación** paso a paso y actualice la vista.</span><span class="sxs-lookup"><span data-stu-id="f635e-138">Once deployment has completed, switch back toohello browser window that opened in hello **Browse toohello app** step, and hit refresh.</span></span>

![Aplicación de ejemplo actualizada que se ejecuta en Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="f635e-140">Administración de la nueva aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="f635e-140">Manage your new Azure web app</span></span>

<span data-ttu-id="f635e-141">Vaya toohello <a href="https://portal.azure.com" target="_blank">portal de Azure</a> toomanage hello web aplicación que creó.</span><span class="sxs-lookup"><span data-stu-id="f635e-141">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="f635e-142">Hola menú izquierdo, haga clic en **servicios de aplicaciones**y, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="f635e-142">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="f635e-144">Podrá ver la página de información general de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f635e-144">You see your web app's Overview page.</span></span> <span data-ttu-id="f635e-145">En este caso, puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="f635e-145">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Hoja de App Service en Azure Portal](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="f635e-147">menú de la izquierda Hola proporciona distintas páginas para configurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f635e-147">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="f635e-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f635e-148">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f635e-149">Node.js con MongoDB</span><span class="sxs-lookup"><span data-stu-id="f635e-149">Node.js with MongoDB</span></span>](app-service-web-tutorial-nodejs-mongodb-app.md)
