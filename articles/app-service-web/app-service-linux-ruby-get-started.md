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
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a>Creación de una aplicación de Ruby con Web Apps en Linux 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático. Este tutorial rápido muestra cómo toocreate un Ruby básico en la aplicación raíles, a continuación, implementarlo tooAzure como una aplicación Web en Linux.

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a>Requisitos previos

* [Ruby 2.4.1 o superior](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).
* [Git](https://git-scm.com/downloads).
* Una [suscripción de Azure activa](https://azure.microsoft.com/pricing/free-trial/).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Descargar el ejemplo hello

En una ventana de terminal, ejecute hello después comando tooclone Hola ejemplo aplicación repositorio tooyour equipo local:

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a>Ejecutar la aplicación hello localmente

Ejecuta el servidor de raíles de hello en orden para toowork de aplicación Hola. Cambiar toohello *hello world* hello y directorio `rails server` comando inicia Hola server.

```bash
cd hello-world\bin
rails server
```
    
Mediante el explorador web, navegue demasiado`http://localhost:3000` tootest Hola aplicación localmente.  

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a>Modificar el mensaje de bienvenida de toodisplay de aplicación

Modificar la aplicación hello por lo que mostrará un mensaje de bienvenida. Cambiar el controlador de la aplicación hello para que devuelva el mensaje de saludo como explorador toohello HTML. 

Abra *~/workspace/hello-world/app/controllers/application_controller.rb* para editarla. Modificar hello `ApplicationController` toolook de clase como Hola siguiendo el ejemplo de código:

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

La aplicación ya está configurada. Mediante el explorador web, navegue demasiado`http://localhost:3000` página de aterrizaje de tooconfirm Hola raíz.

![Hello World configurada](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a>Creación de una aplicación web de Ruby en Azure

Hola de uso [Crear plan de servicio de aplicaciones az](https://docs.microsoft.com/cli/azure/appservice/plan#create) comando toocreate un plan de servicio de aplicación de la aplicación web. 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

A continuación, emita hello [crear webapp az](https://docs.microsoft.com/cli/azure/webapp) comando toocreate hello web aplicación que utiliza el plan de servicio Hola recién creado. Tenga en cuenta que en tiempo de ejecución de Hola se establece demasiado`ruby|2.3`. No olvide tooreplace `<app name>` con un nombre de aplicación único.

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

Una vez creada la aplicación web de hello, un **Introducción** página es tooview disponible. Navegue tooit. Hola después de la página de bienvenida se muestra:

![Página de presentación](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a>Implementación de aplicación

Usar Git toodeploy Hola aplicación Ruby tooAzure. aplicación web de Hello ya tiene una implementación de Git configurada. Puede recuperar la dirección URL de implementación de hello emitiendo una [implementación de aplicación Web de az](https://docs.microsoft.com/cli/azure/webapp/deployment) comando.  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

Tenga en cuenta que la dirección URL de Git de Hola tiene Hola siguiente formulario basado en el nombre de la aplicación web:

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

Ejecute hello después comandos toodeploy Hola aplicación local tooyour sitio Web de Azure:

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

Confirme que las operaciones de implementación remota de hello informan correcto. Hola comandos generan resultados similares toohello siguiente texto:

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

Cuando haya completado la implementación de hello, reinicie la aplicación web con efecto de hello implementación tootake mediante hello [reinicio de webapp az](https://docs.microsoft.com/cli/azure/webapp#restart) de comandos, como se muestra aquí:

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

Navegar por el sitio de tooyour y comprobar los resultados de Hola.

```bash
http://<your web app name>.azurewebsites.net
```
![Aplicación web actualizada](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> Mientras se reinicia la aplicación hello, intentar toobrowse Hola sitio da como resultado un código de estado HTTP `Error 503 Server unavailable`. Puede tardar unos minutos toofully reinicio.
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a>Pasos siguientes

[Preguntas más frecuentes sobre Web App on Linux de Azure App Service](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)