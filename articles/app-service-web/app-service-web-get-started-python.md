---
title: "aaaCreate una aplicación web de Python en Azure | Documentos de Microsoft"
description: "Implementación de su primera aplicación Hola mundo de Python en Azure App Service Web Apps en cuestión de minutos."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 928ee2e5-6143-4c0c-8546-366f5a3d80ce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 03/17/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 42178d490d8aa8eaf93710667aad598794c62c8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-python-web-app-in-azure"></a><span data-ttu-id="317bb-103">Creación de una aplicación web de Python en Azure</span><span class="sxs-lookup"><span data-stu-id="317bb-103">Create a Python web app in Azure</span></span>

<span data-ttu-id="317bb-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="317bb-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="317bb-105">Este tutorial le guía por el proceso de toodevelop e implementar un tooAzure de aplicación de Python aplicaciones Web.</span><span class="sxs-lookup"><span data-stu-id="317bb-105">This quickstart walks through how toodevelop and deploy a Python app tooAzure Web Apps.</span></span> <span data-ttu-id="317bb-106">Crear una aplicación de web de hello usando hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), y usar Git toodeploy ejemplo Python código toohello web app.</span><span class="sxs-lookup"><span data-stu-id="317bb-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Python code toohello web app.</span></span>

![Aplicación de ejemplo que se ejecuta en Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="317bb-108">Puede seguir pasos de hello siguientes a través de un equipo Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="317bb-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="317bb-109">Una vez instalados los requisitos previos de hello, tarda aproximadamente cinco minutos toocomplete pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="317bb-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="317bb-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="317bb-110">Prerequisites</span></span>

<span data-ttu-id="317bb-111">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="317bb-111">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="317bb-112">Instalación de Git</span><span class="sxs-lookup"><span data-stu-id="317bb-112">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="317bb-113">Instalación de Python</span><span class="sxs-lookup"><span data-stu-id="317bb-113">Install Python</span></span>](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="317bb-114">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="317bb-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="317bb-115">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="317bb-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="317bb-116">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="317bb-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="317bb-117">Descargar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="317bb-117">Download hello sample</span></span>

<span data-ttu-id="317bb-118">En una ventana de terminal, ejecute hello después comando tooclone Hola ejemplo aplicación repositorio tooyour equipo local.</span><span class="sxs-lookup"><span data-stu-id="317bb-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

<span data-ttu-id="317bb-119">Utilice esta ventana de terminal toorun todos los comandos de hello en este tutorial rápido.</span><span class="sxs-lookup"><span data-stu-id="317bb-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="317bb-120">Cambie el directorio toohello que contiene código de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="317bb-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="317bb-121">Ejecutar la aplicación hello localmente</span><span class="sxs-lookup"><span data-stu-id="317bb-121">Run hello app locally</span></span>

<span data-ttu-id="317bb-122">Instalar paquetes de saludo necesario mediante `pip`.</span><span class="sxs-lookup"><span data-stu-id="317bb-122">Install hello required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="317bb-123">Ejecutar la aplicación hello localmente o abriendo una ventana de terminal y utilizando hello `Python` comando toolaunch Hola Python servidor web integrado de.</span><span class="sxs-lookup"><span data-stu-id="317bb-123">Run hello application locally by opening a terminal window and using hello `Python` command toolaunch hello built-in Python web server.</span></span>

```bash
python main.py
```

<span data-ttu-id="317bb-124">Abra un explorador web y navegar por la aplicación de ejemplo de toohello en http://localhost: 5000.</span><span class="sxs-lookup"><span data-stu-id="317bb-124">Open a web browser, and navigate toohello sample app at http://localhost:5000.</span></span>

<span data-ttu-id="317bb-125">Puede ver hello **Hello World** mensaje desde la aplicación de ejemplo de Hola mostrado en la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="317bb-125">You can see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![Aplicación de ejemplo que se ejecuta localmente](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

<span data-ttu-id="317bb-127">En la ventana de terminal, presione **Ctrl + C** servidor web de tooexit Hola.</span><span class="sxs-lookup"><span data-stu-id="317bb-127">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Página de la aplicación web vacía](media/app-service-web-get-started-python/app-service-web-service-created.png)

<span data-ttu-id="317bb-129">Ha creado una nueva aplicación web vacía en Azure.</span><span class="sxs-lookup"><span data-stu-id="317bb-129">You’ve created an empty new web app in Azure.</span></span>

## <a name="configure-toouse-python"></a><span data-ttu-id="317bb-130">Configurar toouse Python</span><span class="sxs-lookup"><span data-stu-id="317bb-130">Configure toouse Python</span></span>

<span data-ttu-id="317bb-131">Hola de uso [conjunto de configuración de aplicación Web de az](/cli/azure/webapp/config#set) comando tooconfigure hello web app toouse Python version `3.4`.</span><span class="sxs-lookup"><span data-stu-id="317bb-131">Use hello [az webapp config set](/cli/azure/webapp/config#set) command tooconfigure hello web app toouse Python version `3.4`.</span></span>

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


<span data-ttu-id="317bb-132">Versión de Python de hello al establecer este modo usa un contenedor predeterminado proporcionado por la plataforma de Hola.</span><span class="sxs-lookup"><span data-stu-id="317bb-132">Setting hello Python version this way uses a default container provided by hello platform.</span></span> <span data-ttu-id="317bb-133">toouse su propio contenedor, consulte Referencia CLI de Hola Hola [az webapp config contenedor conjunto](/cli/azure/webapp/config/container#set) comando.</span><span class="sxs-lookup"><span data-stu-id="317bb-133">toouse your own container, see hello CLI reference for hello [az webapp config container set](/cli/azure/webapp/config/container#set) command.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up too4 threads.
Compressing objects: 100% (16/16), done.
Writing objects: 100% (18/18), 4.31 KiB | 0 bytes/s, done.
Total 18 (delta 4), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '44e74fe7dd'.
remote: Generating deployment script.
remote: Generating deployment script for python Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling python deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'main.py'
remote: Copying file: 'README.md'
remote: Copying file: 'requirements.txt'
remote: Copying file: 'virtualenv_proxy.py'
remote: Copying file: 'web.2.7.config'
remote: Copying file: 'web.3.4.config'
remote: Detected requirements.txt.  You can skip Python specific steps with a .skipPythonDeployment file.
remote: Detecting Python runtime from site configuration
remote: Detected python-3.4
remote: Creating python-3.4 virtual environment.
remote: .................................
remote: Pip install requirements.
remote: Successfully installed Flask click itsdangerous Jinja2 Werkzeug MarkupSafe
remote: Cleaning up...
remote: .
remote: Overwriting web.config with web.3.4.config
remote:         1 file(s) copied.
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="317bb-134">Examinar toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="317bb-134">Browse toohello app</span></span>

<span data-ttu-id="317bb-135">Examinar toohello implementa la aplicación mediante el explorador web.</span><span class="sxs-lookup"><span data-stu-id="317bb-135">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="317bb-136">Hola código Python con el ejemplo se ejecuta en una aplicación web de servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="317bb-136">hello Python sample code is running in an Azure App Service web app.</span></span>

![Aplicación de ejemplo que se ejecuta en Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="317bb-138">**¡Enhorabuena!**</span><span class="sxs-lookup"><span data-stu-id="317bb-138">**Congratulations!**</span></span> <span data-ttu-id="317bb-139">Ha implementado la primera tooApp de aplicación de Python servicio.</span><span class="sxs-lookup"><span data-stu-id="317bb-139">You've deployed your first Python app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="317bb-140">Actualizar y volver a implementar código de hello</span><span class="sxs-lookup"><span data-stu-id="317bb-140">Update and redeploy hello code</span></span>

<span data-ttu-id="317bb-141">Use un editor de texto local, abrir hello `main.py` de archivos de aplicación de Python de hello y realizar un toohello siguiente de cambio pequeño toohello texto `return` instrucción:</span><span class="sxs-lookup"><span data-stu-id="317bb-141">Using a local text editor, open hello `main.py` file in hello Python app, and make a small change toohello text next toohello `return` statement:</span></span>

```python
return 'Hello, Azure!'
```

<span data-ttu-id="317bb-142">Confirmar los cambios de Git y, a continuación, insertar tooAzure de cambios de código de hello.</span><span class="sxs-lookup"><span data-stu-id="317bb-142">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="317bb-143">Una vez completada la implementación, cambie toohello atrás ventana del explorador que abrió en hello [examinar toohello aplicación](#browse-to-the-app) paso y página de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="317bb-143">Once deployment has completed, switch back toohello browser window that opened in hello [Browse toohello app](#browse-to-the-app) step, and refresh hello page.</span></span>

![Aplicación de ejemplo actualizada que se ejecuta en Azure](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="317bb-145">Administración de la nueva aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="317bb-145">Manage your new Azure web app</span></span>

<span data-ttu-id="317bb-146">Vaya toohello <a href="https://portal.azure.com" target="_blank">portal de Azure</a> toomanage hello web aplicación que creó.</span><span class="sxs-lookup"><span data-stu-id="317bb-146">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="317bb-147">Hola menú izquierdo, haga clic en **servicios de aplicaciones**y, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="317bb-147">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="317bb-149">Podrá ver la página de información general de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="317bb-149">You see your web app's Overview page.</span></span> <span data-ttu-id="317bb-150">En este caso, puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="317bb-150">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Hoja de App Service en Azure Portal](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="317bb-152">menú de la izquierda Hola proporciona distintas páginas para configurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="317bb-152">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="317bb-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="317bb-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="317bb-154">Python con PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="317bb-154">Python with PostgreSQL</span></span>](app-service-web-tutorial-docker-python-postgresql-app.md)
