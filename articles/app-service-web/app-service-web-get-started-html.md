---
title: "aplicación web de aaaCreate una HTML estático en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de la aplicación de ejemplo de toorun las aplicaciones web en el servicio de aplicación de Azure implementando una HTML estático."
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
ms.openlocfilehash: efd8c8189a3aa1ac35602b688eeb31bff6f5a373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a><span data-ttu-id="7a10d-103">Creación de una aplicación web HTML estática en Azure</span><span class="sxs-lookup"><span data-stu-id="7a10d-103">Create a static HTML web app in Azure</span></span>

<span data-ttu-id="7a10d-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="7a10d-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="7a10d-105">Este tutorial rápido muestra cómo toodeploy básica HTML + CSS sitio tooAzure las aplicaciones Web.</span><span class="sxs-lookup"><span data-stu-id="7a10d-105">This quickstart shows how toodeploy a basic HTML+CSS site tooAzure Web Apps.</span></span> <span data-ttu-id="7a10d-106">Crear una aplicación de web de hello usando hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), y usar Git toodeploy ejemplo HTML toohello contenido web app.</span><span class="sxs-lookup"><span data-stu-id="7a10d-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample HTML content toohello web app.</span></span>

![Página principal de la aplicación de ejemplo](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="7a10d-108">Puede seguir pasos de hello siguientes a través de un equipo Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="7a10d-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="7a10d-109">Una vez instalados los requisitos previos de hello, tarda aproximadamente cinco minutos toocomplete pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="7a10d-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a10d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7a10d-110">Prerequisites</span></span>

<span data-ttu-id="7a10d-111">toocomplete este tutorial rápido:</span><span class="sxs-lookup"><span data-stu-id="7a10d-111">toocomplete this quickstart:</span></span>

- <span data-ttu-id="7a10d-112">[Instalación de Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span><span class="sxs-lookup"><span data-stu-id="7a10d-112">[Install Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7a10d-113">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="7a10d-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7a10d-114">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="7a10d-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7a10d-115">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7a10d-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="7a10d-116">Descargar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="7a10d-116">Download hello sample</span></span>

<span data-ttu-id="7a10d-117">En una ventana de terminal, ejecute hello después comando tooclone Hola ejemplo aplicación repositorio tooyour equipo local.</span><span class="sxs-lookup"><span data-stu-id="7a10d-117">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

<span data-ttu-id="7a10d-118">Utilice esta ventana de terminal toorun todos los comandos de hello en este tutorial rápido.</span><span class="sxs-lookup"><span data-stu-id="7a10d-118">You use this terminal window toorun all hello commands in this quickstart.</span></span>

## <a name="view-hello-html"></a><span data-ttu-id="7a10d-119">Hola vista HTML</span><span class="sxs-lookup"><span data-stu-id="7a10d-119">View hello HTML</span></span>

<span data-ttu-id="7a10d-120">Navegue toohello directorio que contiene el ejemplo hello HTML.</span><span class="sxs-lookup"><span data-stu-id="7a10d-120">Navigate toohello directory that contains hello sample HTML.</span></span> <span data-ttu-id="7a10d-121">Abra hello *index.html* archivo en el explorador.</span><span class="sxs-lookup"><span data-stu-id="7a10d-121">Open hello *index.html* file in your browser.</span></span>

![Página de inicio de la aplicación de ejemplo](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Página de la aplicación web vacía](media/app-service-web-get-started-html/app-service-web-service-created.png)

<span data-ttu-id="7a10d-124">Ha creado una nueva aplicación web vacía en Azure.</span><span class="sxs-lookup"><span data-stu-id="7a10d-124">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up too4 threads.
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
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="7a10d-125">Examinar toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="7a10d-125">Browse toohello app</span></span>

<span data-ttu-id="7a10d-126">En un explorador, vaya la URL de la aplicación web de Azure toohello:</span><span class="sxs-lookup"><span data-stu-id="7a10d-126">In a browser, go toohello Azure web app URL:</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="7a10d-127">página de saludo se está ejecutando como una aplicación web de servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="7a10d-127">hello page is running as an Azure App Service web app.</span></span>

![Página de inicio de la aplicación de ejemplo](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="7a10d-129">**¡Enhorabuena!**</span><span class="sxs-lookup"><span data-stu-id="7a10d-129">**Congratulations!**</span></span> <span data-ttu-id="7a10d-130">Ha implementado la primera tooApp de aplicación servicio HTML.</span><span class="sxs-lookup"><span data-stu-id="7a10d-130">You've deployed your first HTML app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-app"></a><span data-ttu-id="7a10d-131">Actualizar y volver a implementar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="7a10d-131">Update and redeploy hello app</span></span>

<span data-ttu-id="7a10d-132">Abra hello *index.html* un archivo en un editor de texto y realizar un toohello cambian el formato.</span><span class="sxs-lookup"><span data-stu-id="7a10d-132">Open hello *index.html* file in a text editor, and make a change toohello markup.</span></span> <span data-ttu-id="7a10d-133">Por ejemplo, cambiar encabezado H1 Hola de "Azure aplicación servicio – ejemplo sitio HTML estático" toojust "servicio de aplicaciones de Azure'.</span><span class="sxs-lookup"><span data-stu-id="7a10d-133">For example, change hello H1 heading from "Azure App Service - Sample Static HTML Site" toojust "Azure App Service\`.</span></span>

<span data-ttu-id="7a10d-134">Confirmar los cambios de Git y, a continuación, insertar tooAzure de cambios de código de hello.</span><span class="sxs-lookup"><span data-stu-id="7a10d-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated HTML"
git push azure master
```

<span data-ttu-id="7a10d-135">Una vez completada la implementación, actualización de los cambios de hello toosee de explorador.</span><span class="sxs-lookup"><span data-stu-id="7a10d-135">Once deployment has completed, refresh your browser toosee hello changes.</span></span>

![Página de inicio de la aplicación de ejemplo actualizada](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="7a10d-137">Administración de la nueva aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="7a10d-137">Manage your new Azure web app</span></span>

<span data-ttu-id="7a10d-138">Vaya toohello <a href="https://portal.azure.com" target="_blank">portal de Azure</a> toomanage hello web aplicación que creó.</span><span class="sxs-lookup"><span data-stu-id="7a10d-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="7a10d-139">Hola menú izquierdo, haga clic en **servicios de aplicaciones**y, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="7a10d-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-get-started-html/portal1.png)

<span data-ttu-id="7a10d-141">Podrá ver la página de información general de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="7a10d-141">You see your web app's Overview page.</span></span> <span data-ttu-id="7a10d-142">En este caso, puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="7a10d-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Hoja de App Service en Azure Portal](./media/app-service-web-get-started-html/portal2.png)

<span data-ttu-id="7a10d-144">menú de la izquierda Hola proporciona distintas páginas para configurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7a10d-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="7a10d-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7a10d-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7a10d-146">Asignación de un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="7a10d-146">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
