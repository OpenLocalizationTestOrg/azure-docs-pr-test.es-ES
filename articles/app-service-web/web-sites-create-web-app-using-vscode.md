---
title: "aaaCreate una aplicación web de ASP.NET Core en código de Visual Studio"
description: "Este tutorial ilustra cómo toocreate un núcleo de ASP.NET web app mediante código de Visual Studio."
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a>Creación de una aplicación web ASP.NET Core en Visual Studio Code
## <a name="overview"></a>Información general
Este tutorial muestra cómo toocreate un núcleo de ASP.NET web de aplicación con [código de Visual Studio (VS Code)](http://code.visualstudio.com//Docs/whyvscode) e implementarlo demasiado[servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md). 

> [!NOTE]
> Aunque en este artículo se refiere a aplicaciones tooweb, también se aplica tooAPI aplicaciones y aplicaciones móviles. 
> 
> 

ASP.NET Core es un rediseño significativo de ASP.NET. ASP.NET Core es un nuevo marco de código abierto multiplataforma diseñado para crear modernas aplicaciones web basadas en la nube con .NET. Para obtener más información, consulte [Introducción tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html). Para obtener información sobre Aplicaciones web del Servicio de aplicaciones de Azure, consulte [Introducción a aplicaciones web](app-service-web-overview.md).

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a>Requisitos previos
* Instalación de [VS Code](http://code.visualstudio.com/Docs/setup).
* Instalación de Git. Puede instalarlo desde cualquiera de estas ubicaciones: [Chocolatey](https://chocolatey.org/packages/git) o [git-scm.com](http://git-scm.com/downloads). Si está tooGit nueva, elija [git scm.com](http://git-scm.com/downloads) y seleccione la opción de hello demasiado**Use Git desde el símbolo del sistema de Windows hello**. Una vez que instale Git, también necesitará nombre de usuario de tooset Hola Git y correo electrónico porque es necesaria más adelante en el tutorial de hello (al realizar una confirmación de VS Code).  

## <a name="install-aspnet-core"></a>Instalación de ASP.NET Core
ASP.NET Core es una pila de .NET eficiente que sirve para crear aplicaciones web y de nube modernas que se ejecutan en OS X, Linux y Windows. Se ha generado desde Hola masa seguridad tooprovide un marco de trabajo de desarrollo optimizado para las aplicaciones que están ya sea en la nube implementado toohello o ejecutar de forma local. Consta de componentes modulares con una sobrecarga mínima, para continuar disfrutando de flexibilidad al crear soluciones.

Este tutorial está diseñado tooget empezó a crear aplicaciones con las últimas versiones de desarrollo Hola de ASP.NET Core. Hola siguiendo las instrucciones es tooWindows específico. Para obtener instrucciones de instalación en OS X, Linux y Windows, consulte [Introducción a ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started). 


> [!NOTE]
> Para obtener instrucciones de instalación más detalladas para Windows, Linux y OS X, consulte [Instalación de ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx). 
> 
> 

## <a name="create-hello-web-app"></a>Crear una aplicación web de Hola
Esta sección muestra cómo tooscaffold una nueva aplicación ASP.NET web aplicación mediante herramientas de .NET CLI Hola. 

1. Escriba Hola siguiente en el símbolo del sistema toocreate Hola proyecto carpeta y scaffold Hola aplicación hello.
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![CLI de donet: Generador de ASP.NET Core](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. toorestore Hola paquetes de NuGet es necesarios, ejecute el siguiente comando de hello:
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a>Ejecutar la aplicación web de hello localmente
Ahora que ha creado la aplicación web de hello y recuperar todos los paquetes de NuGet de hello para la aplicación hello, puede ejecutar la aplicación web de hello localmente.

1. Ejecutar aplicación hello (hello `dotnet run` comando creará una aplicación hello cuando está anticuada):
    ```terminal
    dotnet run
    ```
2. Abra un explorador y navegue toohello después de la dirección URL.
   
    **http://localhost:5000**
   
    página predeterminada de Hola de aplicación web de hello aparecerán como se indica a continuación.
   
    ![Aplicación web local en un explorador](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. Cierre el explorador. Hola **ventana de comandos**, presione **Ctrl + C** tooshut hacia abajo de la aplicación hello y cerrar hello **ventana de comandos**. 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Crear una aplicación web en hello Portal de Azure
Hello siguientes pasos le guiarán por la creación de una aplicación web en hello Portal de Azure.

1. Inicie sesión en toohello [Portal de Azure](https://portal.azure.com).
2. Haga clic en **NEW** en hello parte superior izquierda de hello Portal.
3. Haga clic en **Web Apps > Aplicación web**.
   
    ![Nueva aplicación web de Azure](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. Escriba un valor para **Nombre**, como **SampleWebAppDemo**. Tenga en cuenta que este nombre debe toobe único y portal de hello aplicará cuando intente nombre de hello tooenter. Por lo tanto, si selecciona un especifique un valor diferente, necesitará toosubstitute ese valor para cada aparición de **SampleWebAppDemo** que se ven en este tutorial. 
5. Seleccione un **plan de Servicio de aplicaciones** ya existente o cree uno nuevo. Si crea un nuevo plan, seleccione Hola plan de tarifa, ubicación y otras opciones. Para obtener más información sobre los planes de servicio de aplicaciones, vea el artículo de hello [información general detallada de planes de servicio de aplicaciones de Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
   
    ![Hoja de la nueva aplicación web de Azure](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. Haga clic en **Crear**.
   
    ![hoja de aplicación web](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a>Habilitar la publicación de Git para la aplicación web nueva de Hola
GIT es un sistema de control de versiones distribuidas puede usar toodeploy en la aplicación web de servicio de aplicaciones de Azure. Va a almacenar el código de hello que escribir para la aplicación web en un repositorio Git local y va a implementar el código tooAzure insertando repositorio remoto tooa.   

1. Inicie sesión en hello [Portal de Azure](https://portal.azure.com).
2. Haga clic en **Examinar**.
3. Haga clic en **aplicaciones Web** tooview una lista de aplicaciones web de hello asociada a su suscripción de Azure.
4. Seleccione la aplicación web de Hola que creó en este tutorial.
5. En la hoja de la aplicación hello web, haga clic en **configuración** > **implementación continua**. 
   
    ![Host de la aplicación web de Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. Haga clic en **Elegir origen > Repositorio de Git local**.
7. Haga clic en **OK**.
   
    ![Repositorio de Git local de Azure](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. Si no ha configurado previamente las credenciales de implementación para publicar una aplicación web u otra aplicación del Servicio de aplicaciones, configúrelas ahora:
   
   * Haga clic en **Configuración** > **Credenciales de implementación**. Hola **configurar credenciales de implementación** hoja se mostrarán.
   * Cree un nombre de usuario y una contraseña.  Necesitará esta contraseña más tarde al configurar Git.
   * Haga clic en **Guardar**.
9. En la hoja de la aplicación web, haga clic en **Configuración > Propiedades**. dirección URL de Hola de hello repositorio de Git remoto que se va a implementar toois se muestra en **dirección URL de GIT**.
10. Hola copia **dirección URL de GIT** valor para su uso posterior en el tutorial de Hola.
    
    ![Dirección URL de Git de Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a>Publicar su tooAzure de aplicación web servicio de aplicaciones
En esta sección, creará un repositorio Git local y su tooAzure de aplicación web de inserción desde ese toodeploy tooAzure de repositorio.

1. En el código de VS, seleccione hello **Git** opción en la barra de navegación izquierda de Hola.
   
    ![Icono de Git en VS Code](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. Seleccione **repositorio de git Initialize** toomake seguro de que el área de trabajo está bajo control de código fuente git. 
   
    ![Inicializar Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. Abra Hola ventana de comandos y cambie el directorio de toohello de directorios de la aplicación web. A continuación, escriba Hola siguiente comando:
   
        git config core.autocrlf false
   
    Este comando evita problemas relacionados con el texto donde existen las finalizaciones CRLF y LF.
4. En el código de VS, agregar un mensaje de confirmación y haga clic en hello **confirmación todos los** icono de comprobación.
   
    ![Confirmar todo de Git](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. Una vez haya completado el procesamiento Git, verá que no hay archivos enumerados en la ventana de Git de hello en **cambios**. 
   
    ![Sin cambios de Git](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. Cambiar toohello back-ventana de comandos donde hello símbolo apunta toohello directorio donde se encuentra la aplicación web.
7. Crear una referencia remota para insertar actualizaciones tooyour web app mediante el uso de hello dirección URL de Git (que termina en ".git") que copió anteriormente.
   
        git remote add azure [URL for remote repository]
8. Configurar Git toosave sus credenciales localmente para que estén tooyour anexado automáticamente comandos de inserción generados a partir de código de VS.
   
        git config credential.helper store
9. Insertar su tooAzure cambios escribiendo el siguiente comando de Hola. Después de este tooAzure inserción inicial, será toodo capaz de inserción de hello todos los comandos desde el código de VS. 
   
        git push -u azure master
   
    Se le pediremos la contraseña de Hola que creó anteriormente en Azure. **Nota: La contraseña no será visible.**
   
    salida de Hello de hello encima comando finaliza con un mensaje que la implementación es correcta.
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> Si realiza cambios tooyour aplicación, puede volver a publicar directamente en el código de VS mediante la funcionalidad integrada de Git de hello seleccionando hello **confirmar todos los** opción seguida de hello **Push** opción. Encontrará hello **Push** opción disponible en hello menú desplegable siguiente toohello **confirmar todos los** y **actualizar** botones.
> 
> 

Si necesita toocollaborate en un proyecto, considere la posibilidad de insertar tooGitHub entre insertar tooAzure.

## <a name="run-hello-app-in-azure"></a>Ejecutar la aplicación hello en Azure
Ahora que ha implementado la aplicación web, vamos a ejecutar aplicación de hello mientras hospedada en Azure. 

Esto puede hacerse de dos maneras:

* Abra un explorador y escriba el nombre de saludo de la aplicación web como se indica a continuación.   
  
        http://SampleWebAppDemo.azurewebsites.net
* Hola Portal de Azure, localice la hoja de la aplicación hello web para la aplicación web y haga clic en **examinar** tooview la aplicación 
* en el explorador predeterminado.

![Aplicación web de Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a>Resumen
En este tutorial, se habrá aprendido cómo toocreate una aplicación web en VS Code e implementar tooAzure. Para obtener más información sobre el código de VS, vea el artículo de hello [¿por qué el código de Visual Studio?](https://code.visualstudio.com/Docs/) Para más información sobre App Service Web Apps, consulte [Información general de Web Apps](app-service-web-overview.md). 

