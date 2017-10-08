---
title: "aaaCreate un PHP web aplicación en Azure | Documentos de Microsoft"
description: "Implementación de su primera aplicación Hola mundo de PHP en Azure App Service Web Apps en cuestión de minutos."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/21/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 8e1022889ca162f8f15ce7435cc9393cc6efef06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-web-app-in-azure"></a><span data-ttu-id="42d27-103">Creación de una aplicación web de PHP en Azure</span><span class="sxs-lookup"><span data-stu-id="42d27-103">Create a PHP web app in Azure</span></span>

<span data-ttu-id="42d27-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="42d27-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="42d27-105">Este tutorial de inicio rápido se muestra cómo toodeploy una tooAzure de aplicación PHP aplicaciones Web.</span><span class="sxs-lookup"><span data-stu-id="42d27-105">This quickstart tutorial shows how toodeploy a PHP app tooAzure Web Apps.</span></span> <span data-ttu-id="42d27-106">Crear una aplicación de web de hello usando hello [CLI de Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) en el Shell de nube y usar Git toodeploy ejemplo PHP código toohello web app.</span><span class="sxs-lookup"><span data-stu-id="42d27-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git toodeploy sample PHP code toohello web app.</span></span>

<span data-ttu-id="42d27-107">![Sample app running in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span><span class="sxs-lookup"><span data-stu-id="42d27-107">![Sample app running in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span></span>

<span data-ttu-id="42d27-108">Puede seguir pasos de hello siguientes a través de un equipo Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="42d27-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="42d27-109">Una vez instalados los requisitos previos de hello, tarda aproximadamente cinco minutos toocomplete pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="42d27-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42d27-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="42d27-110">Prerequisites</span></span>

<span data-ttu-id="42d27-111">toocomplete este tutorial rápido:</span><span class="sxs-lookup"><span data-stu-id="42d27-111">toocomplete this quickstart:</span></span>

* [<span data-ttu-id="42d27-112">Instalación de Git</span><span class="sxs-lookup"><span data-stu-id="42d27-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="42d27-113">Instalación de PHP</span><span class="sxs-lookup"><span data-stu-id="42d27-113">Install PHP</span></span>](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a><span data-ttu-id="42d27-114">Descargar el ejemplo hello localmente</span><span class="sxs-lookup"><span data-stu-id="42d27-114">Download hello sample locally</span></span>

<span data-ttu-id="42d27-115">En una ventana de terminal, ejecute hello siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="42d27-115">In a terminal window, run hello following commands.</span></span> <span data-ttu-id="42d27-116">Esto clonar la máquina local de tooyour de aplicación de ejemplo de Hola y navegar por el código de ejemplo de toohello directory contenedor Hola.</span><span class="sxs-lookup"><span data-stu-id="42d27-116">This will clone hello sample application tooyour local machine, and navigate toohello directory containing hello sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="42d27-117">Ejecutar la aplicación hello localmente</span><span class="sxs-lookup"><span data-stu-id="42d27-117">Run hello app locally</span></span>

<span data-ttu-id="42d27-118">Ejecutar la aplicación hello localmente o abriendo una ventana de terminal y utilizando hello `php` comando toolaunch Hola PHP servidor web integrado de.</span><span class="sxs-lookup"><span data-stu-id="42d27-118">Run hello application locally by opening a terminal window and using hello `php` command toolaunch hello built-in PHP web server.</span></span>

```bash
php -S localhost:8080
```

<span data-ttu-id="42d27-119">Abra un explorador web y navegar por la aplicación de ejemplo de toohello en http://localhost: 8080.</span><span class="sxs-lookup"><span data-stu-id="42d27-119">Open a web browser, and navigate toohello sample app at http://localhost:8080.</span></span>

<span data-ttu-id="42d27-120">Vea hello **Hola a todos!**</span><span class="sxs-lookup"><span data-stu-id="42d27-120">You see hello **Hello World!**</span></span> <span data-ttu-id="42d27-121">mensaje de la aplicación de ejemplo de Hola mostrado en la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="42d27-121">message from hello sample app displayed in hello page.</span></span>

![Aplicación de ejemplo que se ejecuta localmente](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

<span data-ttu-id="42d27-123">En la ventana de terminal, presione **Ctrl + C** servidor web de tooexit Hola.</span><span class="sxs-lookup"><span data-stu-id="42d27-123">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Página de la aplicación web vacía](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="42d27-125">Ha creado una nueva aplicación web vacía en Azure.</span><span class="sxs-lookup"><span data-stu-id="42d27-125">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up too4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 352 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '25f18051e9'.
remote: Generating deployment script.
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.php'
remote: Ignoring: .git
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-toohello-app-locally"></a><span data-ttu-id="42d27-126">Examinar toohello aplicación localmente</span><span class="sxs-lookup"><span data-stu-id="42d27-126">Browse toohello app locally</span></span>

<span data-ttu-id="42d27-127">Examinar toohello implementa la aplicación mediante el explorador web.</span><span class="sxs-lookup"><span data-stu-id="42d27-127">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="42d27-128">Hola código de ejemplo PHP se está ejecutando en una aplicación web de servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="42d27-128">hello PHP sample code is running in an Azure App Service web app.</span></span>

![Aplicación de ejemplo que se ejecuta en Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

<span data-ttu-id="42d27-130">**¡Enhorabuena!**</span><span class="sxs-lookup"><span data-stu-id="42d27-130">**Congratulations!**</span></span> <span data-ttu-id="42d27-131">Ha implementado la primera tooApp de aplicación PHP servicio.</span><span class="sxs-lookup"><span data-stu-id="42d27-131">You've deployed your first PHP app tooApp Service.</span></span>

## <a name="update-locally-and-redeploy-hello-code"></a><span data-ttu-id="42d27-132">Actualizar de forma local e implementar código de hello</span><span class="sxs-lookup"><span data-stu-id="42d27-132">Update locally and redeploy hello code</span></span>

<span data-ttu-id="42d27-133">Use un editor de texto local, abrir hello `index.php` archivo dentro de la aplicación PHP de hello y aplique un pequeño cambio toohello al texto en cadena Hola junto demasiado`echo`:</span><span class="sxs-lookup"><span data-stu-id="42d27-133">Using a local text editor, open hello `index.php` file within hello PHP app, and make a small change toohello text within hello string next too`echo`:</span></span>

```php
echo "Hello Azure!";
```

<span data-ttu-id="42d27-134">Confirmar los cambios de Git y, a continuación, insertar tooAzure de cambios de código de hello.</span><span class="sxs-lookup"><span data-stu-id="42d27-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="42d27-135">Una vez completada la implementación, cambie toohello atrás ventana del explorador que abrió en hello **examinar toohello aplicación** paso y página de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="42d27-135">Once deployment has completed, switch back toohello browser window that opened in hello **Browse toohello app** step, and refresh hello page.</span></span>

![Aplicación de ejemplo actualizada que se ejecuta en Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="42d27-137">Administración de la nueva aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="42d27-137">Manage your new Azure web app</span></span>

<span data-ttu-id="42d27-138">Vaya toohello <a href="https://portal.azure.com" target="_blank">portal de Azure</a> toomanage hello web aplicación que creó.</span><span class="sxs-lookup"><span data-stu-id="42d27-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="42d27-139">Hola menú izquierdo, haga clic en **servicios de aplicaciones**y, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="42d27-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

<span data-ttu-id="42d27-141">Podrá ver la página de información general de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="42d27-141">You see your web app's Overview page.</span></span> <span data-ttu-id="42d27-142">En este caso, puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="42d27-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![Hoja de App Service en Azure Portal](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

<span data-ttu-id="42d27-144">menú de la izquierda Hola proporciona distintas páginas para configurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="42d27-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="42d27-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="42d27-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="42d27-146">PHP con MySQL</span><span class="sxs-lookup"><span data-stu-id="42d27-146">PHP with MySQL</span></span>](app-service-web-tutorial-php-mysql.md)
