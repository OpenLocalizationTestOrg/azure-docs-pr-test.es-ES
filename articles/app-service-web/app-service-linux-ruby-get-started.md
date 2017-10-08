---
title: "una aplicación de Ruby con las aplicaciones Web en Linux aaaCreate | Documentos de Microsoft"
description: "Obtenga información acerca de toocreate Ruby aplicaciones con Azure web wpp en Linux."
keywords: azure app service, linux, oss, ruby
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 6d00c73c-13cb-446f-8926-923db4101afa
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: wesmc;rachelap
ms.openlocfilehash: 99ce3b5ee16703a147787387bb02973defce8190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a><span data-ttu-id="b3bd6-104">Creación de una aplicación de Ruby con Web Apps en Linux</span><span class="sxs-lookup"><span data-stu-id="b3bd6-104">Create a Ruby App with Web Apps on Linux</span></span> 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="b3bd6-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="b3bd6-106">Este tutorial rápido muestra cómo toocreate un Ruby básico en la aplicación raíles, a continuación, implementarlo tooAzure como una aplicación Web en Linux.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-106">This quickstart shows you how toocreate a basic Ruby on Rails application you then deploy it tooAzure as a Web App on Linux.</span></span>

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a><span data-ttu-id="b3bd6-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b3bd6-108">Prerequisites</span></span>

* <span data-ttu-id="b3bd6-109">[Ruby 2.4.1 o superior](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span><span class="sxs-lookup"><span data-stu-id="b3bd6-109">[Ruby 2.4.1 or higher](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span></span>
* <span data-ttu-id="b3bd6-110">[Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="b3bd6-110">[Git](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="b3bd6-111">Una [suscripción de Azure activa](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b3bd6-111">An [active Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="b3bd6-112">Descargar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="b3bd6-112">Download hello sample</span></span>

<span data-ttu-id="b3bd6-113">En una ventana de terminal, ejecute hello después comando tooclone Hola ejemplo aplicación repositorio tooyour equipo local:</span><span class="sxs-lookup"><span data-stu-id="b3bd6-113">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a><span data-ttu-id="b3bd6-114">Ejecutar la aplicación hello localmente</span><span class="sxs-lookup"><span data-stu-id="b3bd6-114">Run hello application locally</span></span>

<span data-ttu-id="b3bd6-115">Ejecuta el servidor de raíles de hello en orden para toowork de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-115">Run hello rails server in order for hello application toowork.</span></span> <span data-ttu-id="b3bd6-116">Cambiar toohello *hello world* hello y directorio `rails server` comando inicia Hola server.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-116">Change toohello *hello-world* directory, and hello `rails server` command starts hello server.</span></span>

```bash
cd hello-world\bin
rails server
```
    
<span data-ttu-id="b3bd6-117">Mediante el explorador web, navegue demasiado`http://localhost:3000` tootest Hola aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-117">Using your web browser, navigate too`http://localhost:3000` tootest hello app locally.</span></span>  

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a><span data-ttu-id="b3bd6-119">Modificar el mensaje de bienvenida de toodisplay de aplicación</span><span class="sxs-lookup"><span data-stu-id="b3bd6-119">Modify app toodisplay welcome message</span></span>

<span data-ttu-id="b3bd6-120">Modificar la aplicación hello por lo que mostrará un mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-120">Modify hello application so it displays a welcome message.</span></span> <span data-ttu-id="b3bd6-121">Cambiar el controlador de la aplicación hello para que devuelva el mensaje de saludo como explorador toohello HTML.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-121">Change hello application's controller so it returns hello message as HTML toohello browser.</span></span> 

<span data-ttu-id="b3bd6-122">Abra *~/workspace/hello-world/app/controllers/application_controller.rb* para editarla.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-122">Open *~/workspace/hello-world/app/controllers/application_controller.rb* for editing.</span></span> <span data-ttu-id="b3bd6-123">Modificar hello `ApplicationController` toolook de clase como Hola siguiendo el ejemplo de código:</span><span class="sxs-lookup"><span data-stu-id="b3bd6-123">Modify hello `ApplicationController` class toolook like hello following code sample:</span></span>

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

<span data-ttu-id="b3bd6-124">La aplicación ya está configurada.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-124">Your app is now configured.</span></span> <span data-ttu-id="b3bd6-125">Mediante el explorador web, navegue demasiado`http://localhost:3000` página de aterrizaje de tooconfirm Hola raíz.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-125">Using your web browser, navigate too`http://localhost:3000` tooconfirm hello root landing page.</span></span>

![Hello World configurada](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a><span data-ttu-id="b3bd6-127">Creación de una aplicación web de Ruby en Azure</span><span class="sxs-lookup"><span data-stu-id="b3bd6-127">Create a Ruby web app on Azure</span></span>

<span data-ttu-id="b3bd6-128">Hola de uso [Crear plan de servicio de aplicaciones az](https://docs.microsoft.com/cli/azure/appservice/plan#create) comando toocreate un plan de servicio de aplicación de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-128">Use hello [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) command toocreate an app service plan for your web app.</span></span> 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

<span data-ttu-id="b3bd6-129">A continuación, emita hello [crear webapp az](https://docs.microsoft.com/cli/azure/webapp) comando toocreate hello web aplicación que utiliza el plan de servicio Hola recién creado.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-129">Next, issue hello [az webapp create](https://docs.microsoft.com/cli/azure/webapp) command toocreate hello web app that uses hello newly created service plan.</span></span> <span data-ttu-id="b3bd6-130">Tenga en cuenta que en tiempo de ejecución de Hola se establece demasiado`ruby|2.3`.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-130">Notice that hello runtime is set too`ruby|2.3`.</span></span> <span data-ttu-id="b3bd6-131">No olvide tooreplace `<app name>` con un nombre de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-131">Don't forget tooreplace `<app name>` with a unique app name.</span></span>

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

<span data-ttu-id="b3bd6-132">Una vez creada la aplicación web de hello, un **Introducción** página es tooview disponible.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-132">Once hello web app is created, an **Overview** page is available tooview.</span></span> <span data-ttu-id="b3bd6-133">Navegue tooit.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-133">Navigate tooit.</span></span> <span data-ttu-id="b3bd6-134">Hola después de la página de bienvenida se muestra:</span><span class="sxs-lookup"><span data-stu-id="b3bd6-134">hello following splash page is displayed:</span></span>

![Página de presentación](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a><span data-ttu-id="b3bd6-136">Implementación de aplicación</span><span class="sxs-lookup"><span data-stu-id="b3bd6-136">Deploy your application</span></span>

<span data-ttu-id="b3bd6-137">Usar Git toodeploy Hola aplicación Ruby tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-137">Use Git toodeploy hello Ruby application tooAzure.</span></span> <span data-ttu-id="b3bd6-138">aplicación web de Hello ya tiene una implementación de Git configurada.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-138">hello web app already has a Git deployment configured.</span></span> <span data-ttu-id="b3bd6-139">Puede recuperar la dirección URL de implementación de hello emitiendo una [implementación de aplicación Web de az](https://docs.microsoft.com/cli/azure/webapp/deployment) comando.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-139">You can retrieve hello deployment URL by issuing an [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment) command.</span></span>  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="b3bd6-140">Tenga en cuenta que la dirección URL de Git de Hola tiene Hola siguiente formulario basado en el nombre de la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="b3bd6-140">Notice that hello Git URL has hello following form based on your web app name:</span></span>

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

<span data-ttu-id="b3bd6-141">Ejecute hello después comandos toodeploy Hola aplicación local tooyour sitio Web de Azure:</span><span class="sxs-lookup"><span data-stu-id="b3bd6-141">Run hello following commands toodeploy hello local application tooyour Azure website:</span></span>

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="b3bd6-142">Confirme que las operaciones de implementación remota de hello informan correcto.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-142">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="b3bd6-143">Hola comandos generan resultados similares toohello siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="b3bd6-143">hello commands produce output similar toohello following text:</span></span>

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

<span data-ttu-id="b3bd6-144">Cuando haya completado la implementación de hello, reinicie la aplicación web con efecto de hello implementación tootake mediante hello [reinicio de webapp az](https://docs.microsoft.com/cli/azure/webapp#restart) de comandos, como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="b3bd6-144">Once hello deployment has completed, restart your web app for hello deployment tootake effect by using hello [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart) command, as shown here:</span></span>

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="b3bd6-145">Navegar por el sitio de tooyour y comprobar los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-145">Navigate tooyour site and verify hello results.</span></span>

```bash
http://<your web app name>.azurewebsites.net
```
![Aplicación web actualizada](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> <span data-ttu-id="b3bd6-147">Mientras se reinicia la aplicación hello, intentar toobrowse Hola sitio da como resultado un código de estado HTTP `Error 503 Server unavailable`.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-147">While hello app is restarting, attempting toobrowse hello site results in an HTTP status code `Error 503 Server unavailable`.</span></span> <span data-ttu-id="b3bd6-148">Puede tardar unos minutos toofully reinicio.</span><span class="sxs-lookup"><span data-stu-id="b3bd6-148">It may take a few minutes toofully restart.</span></span>
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a><span data-ttu-id="b3bd6-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b3bd6-149">Next steps</span></span>

[<span data-ttu-id="b3bd6-150">Preguntas más frecuentes sobre Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b3bd6-150">Azure App Service Web App on Linux FAQ</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)