---
title: "Creación de una aplicación web HTML estática en Azure | Microsoft Docs"
description: "Aprenda a ejecutar aplicaciones web en Azure App Service mediante la implementación de una aplicación HTML estática de ejemplo."
services: app-service\web
documentationcenter: 
author: rick-anderson
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/26/2017
ms.author: riande
ms.custom: mvc
ms.openlocfilehash: 42af5b08b8d2ff0c75fd73dcfa61c861647fd2c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a><span data-ttu-id="c1404-103">Creación de una aplicación web HTML estática en Azure</span><span class="sxs-lookup"><span data-stu-id="c1404-103">Create a static HTML web app in Azure</span></span>

<span data-ttu-id="c1404-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="c1404-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="c1404-105">En esta guía de inicio rápido se explica cómo se implementa un sitio HTML+CSS básico en Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="c1404-105">This quickstart shows how to deploy a basic HTML+CSS site to Azure Web Apps.</span></span> <span data-ttu-id="c1404-106">Se crea la aplicación web con la [CLI de Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) y se usa Git para implementar el contenido HTML de ejemplo en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c1404-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample HTML content to the web app.</span></span>

![Página principal de la aplicación de ejemplo](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="c1404-108">Estos pasos se pueden realizar con un equipo Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="c1404-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="c1404-109">Una vez instalados los requisitos previos, tardará aproximadamente cinco minutos en completar los pasos.</span><span class="sxs-lookup"><span data-stu-id="c1404-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1404-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c1404-110">Prerequisites</span></span>

<span data-ttu-id="c1404-111">Para completar esta guía de inicio rápido:</span><span class="sxs-lookup"><span data-stu-id="c1404-111">To complete this quickstart:</span></span>

- <span data-ttu-id="c1404-112">[Instalación de Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span><span class="sxs-lookup"><span data-stu-id="c1404-112">[Install Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c1404-113">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="c1404-113">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c1404-114">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="c1404-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="c1404-115">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c1404-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="c1404-116">Descarga del ejemplo</span><span class="sxs-lookup"><span data-stu-id="c1404-116">Download the sample</span></span>

<span data-ttu-id="c1404-117">En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de la aplicación de ejemplo en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="c1404-117">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

<span data-ttu-id="c1404-118">Utilice esta ventana de terminal para ejecutar todos los comandos de esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="c1404-118">You use this terminal window to run all the commands in this quickstart.</span></span>

## <a name="view-the-html"></a><span data-ttu-id="c1404-119">Ver el código HTML</span><span class="sxs-lookup"><span data-stu-id="c1404-119">View the HTML</span></span>

<span data-ttu-id="c1404-120">Vaya al directorio que contiene el código HTML de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c1404-120">Navigate to the directory that contains the sample HTML.</span></span> <span data-ttu-id="c1404-121">Abra el archivo *index.html* en el explorador.</span><span class="sxs-lookup"><span data-stu-id="c1404-121">Open the *index.html* file in your browser.</span></span>

![Página de inicio de la aplicación de ejemplo](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Página de la aplicación web vacía](media/app-service-web-get-started-html/app-service-web-service-created.png)

<span data-ttu-id="c1404-124">Ha creado una nueva aplicación web vacía en Azure.</span><span class="sxs-lookup"><span data-stu-id="c1404-124">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 2.07 KiB | 0 bytes/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'cc39b1e4cb'.
remote: Generating deployment script.
remote: Generating deployment script for Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="c1404-125">Navegación hasta la aplicación</span><span class="sxs-lookup"><span data-stu-id="c1404-125">Browse to the app</span></span>

<span data-ttu-id="c1404-126">En un explorador, vaya a la dirección URL de la aplicación web de Azure:</span><span class="sxs-lookup"><span data-stu-id="c1404-126">In a browser, go to the Azure web app URL:</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="c1404-127">La página se ejecuta como una aplicación web de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c1404-127">The page is running as an Azure App Service web app.</span></span>

![Página de inicio de la aplicación de ejemplo](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="c1404-129">**¡Enhorabuena!**</span><span class="sxs-lookup"><span data-stu-id="c1404-129">**Congratulations!**</span></span> <span data-ttu-id="c1404-130">Ha implementado la primera aplicación HTML en App Service.</span><span class="sxs-lookup"><span data-stu-id="c1404-130">You've deployed your first HTML app to App Service.</span></span>

## <a name="update-and-redeploy-the-app"></a><span data-ttu-id="c1404-131">Actualización de la aplicación y nueva implementación</span><span class="sxs-lookup"><span data-stu-id="c1404-131">Update and redeploy the app</span></span>

<span data-ttu-id="c1404-132">Abra el archivo *index.html* en un editor de texto y realice un cambio en el marcado.</span><span class="sxs-lookup"><span data-stu-id="c1404-132">Open the *index.html* file in a text editor, and make a change to the markup.</span></span> <span data-ttu-id="c1404-133">Por ejemplo, cambie el encabezado H1 "Azure App Service - Sample Static HTML Site" por "Azure App Service".</span><span class="sxs-lookup"><span data-stu-id="c1404-133">For example, change the H1 heading from "Azure App Service - Sample Static HTML Site" to just "Azure App Service\`.</span></span>

<span data-ttu-id="c1404-134">Confirme los cambios en Git y, después, inserte los cambios de código en Azure.</span><span class="sxs-lookup"><span data-stu-id="c1404-134">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated HTML"
git push azure master
```

<span data-ttu-id="c1404-135">Una vez completada la implementación, actualice el explorador para ver los cambios.</span><span class="sxs-lookup"><span data-stu-id="c1404-135">Once deployment has completed, refresh your browser to see the changes.</span></span>

![Página de inicio de la aplicación de ejemplo actualizada](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="c1404-137">Administración de la nueva aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="c1404-137">Manage your new Azure web app</span></span>

<span data-ttu-id="c1404-138">Vaya a <a href="https://portal.azure.com" target="_blank">Azure Portal</a> para administrar la aplicación web que ha creado.</span><span class="sxs-lookup"><span data-stu-id="c1404-138">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="c1404-139">En el menú izquierdo, haga clic en **App Services** y, a continuación, haga clic en el nombre de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="c1404-139">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Navegación desde el portal a la aplicación web de Azure](./media/app-service-web-get-started-html/portal1.png)

<span data-ttu-id="c1404-141">Podrá ver la página de información general de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c1404-141">You see your web app's Overview page.</span></span> <span data-ttu-id="c1404-142">En este caso, puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="c1404-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Hoja de App Service en Azure Portal](./media/app-service-web-get-started-html/portal2.png)

<span data-ttu-id="c1404-144">El menú izquierdo proporciona distintas páginas para configurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c1404-144">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="c1404-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c1404-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c1404-146">Asignación de un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="c1404-146">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
