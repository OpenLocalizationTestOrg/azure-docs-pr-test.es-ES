---
title: aplicaciones de aaaDebugging en un contenedor de Docker local | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomodify una aplicación que se ejecuta en un contenedor de Docker local, actualizar el contenedor de Hola a través de la edición y la actualización y establecer puntos de interrupción de depuración"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: ff64e62fbb93901a29b5496bd5e17d2c4ea5ca99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a>Depuración de aplicaciones en un contenedor de Docker local
## <a name="overview"></a>Información general
Hola Visual Studio Tools para Docker proporciona un toodevelop de forma coherente en y validar la aplicación localmente en un contenedor Linux Docker.
No tiene el contenedor de hello toorestart cada vez que realice un código de cambiar.
Este artículo explica cómo toouse Hola "Editar y actualizar" característica toostart una aplicación Web de ASP.NET Core en un contenedor de Docker local, realice los cambios necesarios y, después, actualizar Hola explorador toosee esos cambios.
Este artículo también muestra cómo tooset los puntos de interrupción para la depuración.

> [!NOTE]
> La compatibilidad con el contenedor de Windows estará disponible en una versión futura
>
>

## <a name="prerequisites"></a>Requisitos previos
Hola después herramientas debe estar instalado.

* [Versión más reciente de Visual Studio](https://www.visualstudio.com/downloads/)
* [SDK de Microsoft ASP.NET Core 1.0](https://go.microsoft.com/fwlink/?LinkID=809122)

toorun localmente contenedores de Docker, necesitará a un cliente local.
Puede usar hello [cuadro de herramientas de Docker](https://www.docker.com/products/docker-toolbox), lo que requiere toobe de Hyper-V deshabilitado, o puede usar [Docker para Windows](https://www.docker.com/get-docker), que usa Hyper-V y requiere Windows 10.

Si usa el cuadro de herramientas de Docker, necesitará demasiado[configurar cliente hello](vs-azure-tools-docker-setup.md)

## <a name="1-create-a-web-app"></a>1. Creación de una aplicación web
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Agregue compatibilidad con Docker
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a>3. Edición del código y actualización
tooquickly iterar cambios, puede iniciar la aplicación dentro de un contenedor y continuar toomake cambios, verlos como lo haría con IIS Express.

1. Establecer configuración de soluciones de hello demasiado`Debug` y presione  **&lt;CTRL + F5 >** toobuild el docker de la imagen y lo ejecuta localmente.

    Una vez que la imagen de contenedor de Hola se ha creado y se está ejecutando en un contenedor de Docker, Visual Studio iniciará la aplicación Web de hello en el explorador predeterminado.
    Si está utilizando el Explorador de Microsoft Edge Hola o en caso contrario, tiene errores, vea [solución de problemas](vs-azure-tools-docker-troubleshooting-docker-errors.md) sección.
2. Vaya toohello acerca de la página, que es donde veremos toomake los cambios.
3. Devolver tooVisual Studio y abra `Views\Home\About.cshtml`.
4. Agregar Hola siguiente HTML toohello contenido final de archivo hello y guardar los cambios de Hola.

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. Ver la ventana de salida de hello, cuando se completa Hola compilación de .NET y ver las siguientes líneas, cambiar explorador tooyour atrás y actualizar Hola acerca de la página.

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. Se han aplicado los cambios.

## <a name="4-debug-with-breakpoints"></a>4. Depuración con puntos de interrupción
A menudo, cambios deberán aún más la inspección, aprovechando Hola características de Visual Studio de depuración.

1. Devolver tooVisual Studio y abra`Controllers\HomeController.cs`
2. Reemplace el contenido de hello del método de hello About() con siguiente hello:

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. Conjunto toohello de un punto de interrupción a la izquierda de hello `string message`... línea.
4. Aciertos  **&lt;F5 >** toostart depuración.
5. Navegue toohello sobre toohit de página en el punto de interrupción.
6. Conmutador tooVisual Studio tooview Hola punto de interrupción e inspeccionar Hola valor del mensaje.

   ![][2]

## <a name="summary"></a>Resumen
Con [Visual Studio 2015 Tools para Docker](https://aka.ms/DockerToolsForVS), puede obtener la productividad de Hola de trabajar de forma local, con realismo de producción de hello de desarrollo dentro de un contenedor de Docker.

## <a name="troubleshooting"></a>Solución de problemas
[Solución de problemas de desarrollo de Docker en Visual Studio](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a>Más información acerca de Docker con Visual Studio, Windows y Azure
* [Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) : desarrollo de código de .NET Core en un contenedor
* [Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) : compilación e implementación de contenedores de Docker
* [Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) : servicios de lenguaje para editar archivos de Docker, a los que próximamente se incorporarán más escenarios de E2E
* [Documentación acerca de los contenedores de Windows](http://aka.ms/containers): información de Windows Server y Nano Server
* [Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Contenido de Azure Container Service](http://aka.ms/AzureContainerService)
* Para obtener más ejemplos del uso de Docker, consulte [trabajar con Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) de hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) conectar 2015 [demostración](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/). Encontrará tutoriales más rápidos de demostración de hello HealthClinic.biz, [tutoriales de herramientas de desarrollador de Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).

## <a name="various-docker-tools"></a>Varias herramientas de Docker
[Some great docker tools (Steve Lasker's blog) (Herramientas excelentes de Docker [blog de Steve])](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a>Buenos artículos
[Introducción tooMicroservices desde NGINX](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a>Presentaciones
* [Steve Lasker: VS Live Las Vegas 2016 - Docker e2e](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [Introducción tooASP.NET Core @ compilación 2016 - donde se en demostración](https://channel9.msdn.com/Events/Build/2016/B810)
* [Developing .NET apps in containers, Channel 9 (Desarrollo de aplicaciones .NET en contenedores, Channel 9)](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
