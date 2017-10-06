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
# <a name="create-a-python-web-app-in-azure"></a>Creación de una aplicación web de Python en Azure

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.  Este tutorial le guía por el proceso de toodevelop e implementar un tooAzure de aplicación de Python aplicaciones Web. Crear una aplicación de web de hello usando hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), y usar Git toodeploy ejemplo Python código toohello web app.

![Aplicación de ejemplo que se ejecuta en Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

Puede seguir pasos de hello siguientes a través de un equipo Mac, Windows o Linux. Una vez instalados los requisitos previos de hello, tarda aproximadamente cinco minutos toocomplete pasos Hola.
## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial:

1. [Instalación de Git](https://git-scm.com/)
1. [Instalación de Python](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Descargar el ejemplo hello

En una ventana de terminal, ejecute hello después comando tooclone Hola ejemplo aplicación repositorio tooyour equipo local.

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

Utilice esta ventana de terminal toorun todos los comandos de hello en este tutorial rápido.

Cambie el directorio toohello que contiene código de ejemplo de Hola.

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Ejecutar la aplicación hello localmente

Instalar paquetes de saludo necesario mediante `pip`.

```bash
pip install -r requirements.txt
```

Ejecutar la aplicación hello localmente o abriendo una ventana de terminal y utilizando hello `Python` comando toolaunch Hola Python servidor web integrado de.

```bash
python main.py
```

Abra un explorador web y navegar por la aplicación de ejemplo de toohello en http://localhost: 5000.

Puede ver hello **Hello World** mensaje desde la aplicación de ejemplo de Hola mostrado en la página de Hola.

![Aplicación de ejemplo que se ejecuta localmente](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

En la ventana de terminal, presione **Ctrl + C** servidor web de tooexit Hola.

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Página de la aplicación web vacía](media/app-service-web-get-started-python/app-service-web-service-created.png)

Ha creado una nueva aplicación web vacía en Azure.

## <a name="configure-toouse-python"></a>Configurar toouse Python

Hola de uso [conjunto de configuración de aplicación Web de az](/cli/azure/webapp/config#set) comando tooconfigure hello web app toouse Python version `3.4`.

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


Versión de Python de hello al establecer este modo usa un contenedor predeterminado proporcionado por la plataforma de Hola. toouse su propio contenedor, consulte Referencia CLI de Hola Hola [az webapp config contenedor conjunto](/cli/azure/webapp/config/container#set) comando.

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

## <a name="browse-toohello-app"></a>Examinar toohello aplicación

Examinar toohello implementa la aplicación mediante el explorador web.

```bash
http://<app_name>.azurewebsites.net
```

Hola código Python con el ejemplo se ejecuta en una aplicación web de servicio de aplicaciones de Azure.

![Aplicación de ejemplo que se ejecuta en Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

**¡Enhorabuena!** Ha implementado la primera tooApp de aplicación de Python servicio.

## <a name="update-and-redeploy-hello-code"></a>Actualizar y volver a implementar código de hello

Use un editor de texto local, abrir hello `main.py` de archivos de aplicación de Python de hello y realizar un toohello siguiente de cambio pequeño toohello texto `return` instrucción:

```python
return 'Hello, Azure!'
```

Confirmar los cambios de Git y, a continuación, insertar tooAzure de cambios de código de hello.

```bash
git commit -am "updated output"
git push azure master
```

Una vez completada la implementación, cambie toohello atrás ventana del explorador que abrió en hello [examinar toohello aplicación](#browse-to-the-app) paso y página de actualización de Hola.

![Aplicación de ejemplo actualizada que se ejecuta en Azure](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Administración de la nueva aplicación web de Azure

Vaya toohello <a href="https://portal.azure.com" target="_blank">portal de Azure</a> toomanage hello web aplicación que creó.

Hola menú izquierdo, haga clic en **servicios de aplicaciones**y, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

Podrá ver la página de información general de la aplicación web. En este caso, puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar. 

![Hoja de App Service en Azure Portal](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

menú de la izquierda Hola proporciona distintas páginas para configurar la aplicación. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Python con PostgreSQL](app-service-web-tutorial-docker-python-postgresql-app.md)
