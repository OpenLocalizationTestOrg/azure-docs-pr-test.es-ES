---
title: "Creación de una aplicación de Ruby con Web Apps en Linux | Microsoft Docs"
description: Aprenda a crear aplicaciones de Ruby con Azure Web Apps en Linux.
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
ms.openlocfilehash: 17f3f1a2122c508501134a0c43ab6abce412fb44
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a>Creación de una aplicación de Ruby con Web Apps en Linux 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático. En esta guía de inicio rápido se muestra cómo crear una aplicación de Ruby on Rails básica en la aplicación e implementarla a continuación en Azure como Aplicación web en Linux.

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a>Requisitos previos

* [Ruby 2.4.1 o superior](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).
* [Git](https://git-scm.com/downloads).
* Una [suscripción de Azure activa](https://azure.microsoft.com/pricing/free-trial/).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a>Descarga del ejemplo

En una ventana de terminal, ejecute el siguiente comando para clonar el repositorio de la aplicación de ejemplo en el equipo local:

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-the-application-locally"></a>Ejecución de la aplicación de forma local

Ejecute el servidor de Rails para que funcione la aplicación. Cambie al directorio *hello-world* y el comando `rails server` iniciará el servidor.

```bash
cd hello-world\bin
rails server
```
    
Mediante el explorador web, vaya a `http://localhost:3000` para probar la aplicación localmente.    

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-to-display-welcome-message"></a>Modificación de la aplicación para mostrar el mensaje de bienvenida

Modifique la aplicación para que aparezca en ella un mensaje de bienvenida. Cambie el controlador de la aplicación para que devuelva el mensaje como HTML al explorador. 

Abra *~/workspace/hello-world/app/controllers/application_controller.rb* para editarla. Modifique la clase `ApplicationController` para que sea como el siguiente código de ejemplo:

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

La aplicación ya está configurada. Mediante el explorador web, vaya a `http://localhost:3000` para confirmar la página de aterrizaje de raíz.

![Hello World configurada](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a>Creación de una aplicación web de Ruby en Azure

Use el comando [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) para crear un plan de App Service para su aplicación web. 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

A continuación, emita el comando [az webapp create](https://docs.microsoft.com/cli/azure/webapp) para crear la aplicación web que usa el plan de App Service recién creado. Tenga en cuenta que el tiempo de ejecución se establece en `ruby|2.3`. No olvide reemplazar `<app name>` por un nombre de aplicación único.

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

Una vez creada la aplicación web, podrá verse la página **Información general**. Vaya a esta. Se muestra la siguiente página de presentación:

![Página de presentación](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a>Implementación de aplicación

Use Git para implementar la aplicación de Ruby en Azure. La aplicación web ya tiene configurada una implementación de Git. Puede recuperar la dirección URL de implementación mediante la emisión de un comando [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment).  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

Tenga en cuenta que la dirección URL de Git tiene el formato siguiente en función del nombre de la aplicación web:

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

Ejecute los comandos siguientes para implementar la aplicación local en el sitio web de Azure:

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

Confirme que las operaciones de implementación remota se han realizado correctamente. Los comandos generan una salida similar al texto siguiente:

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

Una vez que la implementación haya finalizado, reinicie la aplicación web para que la implementación surta efecto mediante el comando [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart), como se muestra aquí:

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

Vaya al sitio y verifique los resultados.

```bash
http://<your web app name>.azurewebsites.net
```
![Aplicación web actualizada](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> Mientras se reinicia la aplicación, al tratar de obtener acceso al sitio, se obtendrá un código de estado HTTP `Error 503 Server unavailable`. Puede tardar unos minutos en reiniciarse completamente.
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a>Pasos siguientes

[Preguntas más frecuentes sobre Web App on Linux de Azure App Service](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)