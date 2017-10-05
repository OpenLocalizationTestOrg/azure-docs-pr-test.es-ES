---
title: "Creación de una aplicación web de PHP en Azure | Microsoft Docs"
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
ms.openlocfilehash: 3a78e0b485046ad6228bf4819d3908042c298d1a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-php-web-app-in-azure"></a><span data-ttu-id="3ea7a-103">Creación de una aplicación web de PHP en Azure</span><span class="sxs-lookup"><span data-stu-id="3ea7a-103">Create a PHP web app in Azure</span></span>

<span data-ttu-id="3ea7a-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="3ea7a-105">En esta guía de inicio rápido se explica cómo se implementa una aplicación de PHP en Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-105">This quickstart tutorial shows how to deploy a PHP app to Azure Web Apps.</span></span> <span data-ttu-id="3ea7a-106">Se crea la aplicación web con la [CLI de Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) en Cloud Shell y se usa Git para implementar el código PHP de ejemplo en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git to deploy sample PHP code to the web app.</span></span>

<span data-ttu-id="3ea7a-107">![Sample app running in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span><span class="sxs-lookup"><span data-stu-id="3ea7a-107">![Sample app running in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span></span>

<span data-ttu-id="3ea7a-108">Estos pasos se pueden realizar con un equipo Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="3ea7a-109">Una vez instalados los requisitos previos, tardará aproximadamente cinco minutos en completar los pasos.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ea7a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3ea7a-110">Prerequisites</span></span>

<span data-ttu-id="3ea7a-111">Para completar esta guía de inicio rápido:</span><span class="sxs-lookup"><span data-stu-id="3ea7a-111">To complete this quickstart:</span></span>

* [<span data-ttu-id="3ea7a-112">Instalación de Git</span><span class="sxs-lookup"><span data-stu-id="3ea7a-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="3ea7a-113">Instalación de PHP</span><span class="sxs-lookup"><span data-stu-id="3ea7a-113">Install PHP</span></span>](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample-locally"></a><span data-ttu-id="3ea7a-114">Descarga local del código</span><span class="sxs-lookup"><span data-stu-id="3ea7a-114">Download the sample locally</span></span>

<span data-ttu-id="3ea7a-115">Ejecute los siguientes comandos en una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-115">In a terminal window, run the following commands.</span></span> <span data-ttu-id="3ea7a-116">Con ello, se clonará la aplicación de ejemplo en el equipo local y se desplazará al directorio que contiene el código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-116">This will clone the sample application to your local machine, and navigate to the directory containing the sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="3ea7a-117">Ejecución de la aplicación de forma local</span><span class="sxs-lookup"><span data-stu-id="3ea7a-117">Run the app locally</span></span>

<span data-ttu-id="3ea7a-118">Ejecute la aplicación localmente abriendo una ventana de terminal y utilizando el comando `php` para iniciar el servidor web de PHP integrado.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-118">Run the application locally by opening a terminal window and using the `php` command to launch the built-in PHP web server.</span></span>

```bash
php -S localhost:8080
```

<span data-ttu-id="3ea7a-119">Abra un explorador web y navegue a la aplicación de ejemplo en http://localhost:8080.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-119">Open a web browser, and navigate to the sample app at http://localhost:8080.</span></span>

<span data-ttu-id="3ea7a-120">Verá el mensaje **Hola mundo**</span><span class="sxs-lookup"><span data-stu-id="3ea7a-120">You see the **Hello World!**</span></span> <span data-ttu-id="3ea7a-121">desde la aplicación de ejemplo mostrada en la página.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-121">message from the sample app displayed in the page.</span></span>

![Aplicación de ejemplo que se ejecuta localmente](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

<span data-ttu-id="3ea7a-123">En la ventana de terminal, presione **Ctrl + C** para salir del servidor web.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-123">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Página de la aplicación web vacía](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="3ea7a-125">Ha creado una nueva aplicación web vacía en Azure.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-125">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up to 4 threads.
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
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-to-the-app-locally"></a><span data-ttu-id="3ea7a-126">Navegación local hasta la aplicación</span><span class="sxs-lookup"><span data-stu-id="3ea7a-126">Browse to the app locally</span></span>

<span data-ttu-id="3ea7a-127">Vaya a la aplicación implementada mediante el explorador web.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-127">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="3ea7a-128">El código de ejemplo de PHP se está ejecutando en una aplicación web de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-128">The PHP sample code is running in an Azure App Service web app.</span></span>

![Aplicación de ejemplo que se ejecuta en Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

<span data-ttu-id="3ea7a-130">**¡Enhorabuena!**</span><span class="sxs-lookup"><span data-stu-id="3ea7a-130">**Congratulations!**</span></span> <span data-ttu-id="3ea7a-131">Ha implementado la primera aplicación PHP en App Service.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-131">You've deployed your first PHP app to App Service.</span></span>

## <a name="update-locally-and-redeploy-the-code"></a><span data-ttu-id="3ea7a-132">Actualización local y nueva implementación del código</span><span class="sxs-lookup"><span data-stu-id="3ea7a-132">Update locally and redeploy the code</span></span>

<span data-ttu-id="3ea7a-133">Con un editor de texto local, abra el archivo `index.php` dentro de la aplicación PHP y realice un pequeño cambio en el texto dentro de la cadena situada junto a `echo`:</span><span class="sxs-lookup"><span data-stu-id="3ea7a-133">Using a local text editor, open the `index.php` file within the PHP app, and make a small change to the text within the string next to `echo`:</span></span>

```php
echo "Hello Azure!";
```

<span data-ttu-id="3ea7a-134">Confirme los cambios en Git y, después, inserte los cambios de código en Azure.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-134">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="3ea7a-135">Una vez que la implementación haya finalizado, vuelva a la ventana del explorador que abrió en el paso **Navegación hasta la aplicación** y actualice la página.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-135">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and refresh the page.</span></span>

![Aplicación de ejemplo actualizada que se ejecuta en Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="3ea7a-137">Administración de la nueva aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="3ea7a-137">Manage your new Azure web app</span></span>

<span data-ttu-id="3ea7a-138">Vaya a <a href="https://portal.azure.com" target="_blank">Azure Portal</a> para administrar la aplicación web que ha creado.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-138">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="3ea7a-139">En el menú izquierdo, haga clic en **App Services** y, a continuación, haga clic en el nombre de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-139">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Navegación desde el portal a la aplicación web de Azure](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

<span data-ttu-id="3ea7a-141">Podrá ver la página de información general de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-141">You see your web app's Overview page.</span></span> <span data-ttu-id="3ea7a-142">En este caso, puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![Hoja de App Service en Azure Portal](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

<span data-ttu-id="3ea7a-144">El menú izquierdo proporciona distintas páginas para configurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3ea7a-144">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="3ea7a-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3ea7a-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3ea7a-146">PHP con MySQL</span><span class="sxs-lookup"><span data-stu-id="3ea7a-146">PHP with MySQL</span></span>](app-service-web-tutorial-php-mysql.md)
