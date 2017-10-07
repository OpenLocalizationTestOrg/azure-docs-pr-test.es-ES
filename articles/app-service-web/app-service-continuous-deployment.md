---
title: "aaaContinuous implementación tooAzure servicio de aplicaciones | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooenable implementación continua tooAzure servicio de aplicaciones."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a>TooAzure de implementación continua servicio de aplicaciones
Este tutorial muestra cómo tooconfigure un flujo de trabajo de implementación continua para su [servicio de aplicaciones de Azure] aplicación. Integración con el servicio de aplicación con BitBucket, GitHub, y [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) permite una continua donde Azure extrae las actualizaciones más recientes de Hola desde el proyecto de flujo de trabajo de implementación publica tooone de estos servicios. La implementación continua representa una buena opción para los proyectos donde se integran contribuciones diversas y frecuentes.

toofind out cómo manualmente desde un repositorio de nube no aparece en una implementación continua tooconfigure Hola Portal de Azure (como [GitLab](https://gitlab.com/)), consulte [configurando la implementación continua mediante procesos manuales](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="overview"></a>Habilitación de la implementación continua
implementación continua tooenable,

1. Publicar su repositorio de contenido toohello de aplicación que se usará para la implementación continuada.  
    Para obtener más información sobre cómo publicar los servicios de toothese de proyecto, vea [crear un repositorio (GitHub)], [crear un repositorio (BitBucket)], y [empezar a trabajar con VSTS].
2. En la hoja de menú de la aplicación Hola [portal de Azure], haga clic en **la implementación de aplicación > Opciones de implementación**. Haga clic en **Elegir origen**, a continuación, seleccione origen de la implementación de Hola.  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > tooconfigure una cuenta VSTS de implementación de servicio de aplicaciones Vea este [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).
   > 
   > 
3. Completar flujo de trabajo de autorización de Hola.
4. Hola **origen de la implementación** hoja, elija el proyecto de Hola y crear una bifurcación toodeploy desde. Cuando haya terminado, haga clic en **Aceptar**.
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > Al habilitar la implementación continua con GitHub o BitBucket, se mostrarán tanto los proyectos públicos como privados.
   > 
   > 
   
    Servicio de aplicaciones crea una asociación con el repositorio seleccionado hello, extrae archivos Hola de bifurcación especificada hello y mantiene un clon del repositorio para la aplicación de servicio de aplicaciones. Al configurar la implementación continua de VSTS desde el portal de Azure hello, integración de hello usa Hola servicio de aplicaciones [motor de implementación de Kudu](https://github.com/projectkudu/kudu/wiki), que ya automatiza las tareas de compilación e implementación con cada `git push`. No es necesario tooseparately configurar la implementación continua en VSTS. Al finalizar este proceso, hello **opciones de implementación** hoja de la aplicación mostrará una implementación activa que indica que la implementación se ha realizado correctamente.
5. aplicación de hello tooverify se implementa correctamente, haga clic en hello **URL** princip Hola de hoja de la aplicación Hola Hola portal de Azure.
6. tooverify que se está produciendo una implementación continua desde el repositorio de Hola de su elección, inserte un repositorio de toohello de cambio. La aplicación debe actualizar los cambios de hello tooreflect poco después de repositorio de hello inserción toohello completa. Puede comprobar que ha extraído en la actualización de Hola Hola **opciones de implementación** hoja de la aplicación.

## <a name="VSsolution"></a>Implementación continua de una solución de Visual Studio
Insertar un tooAzure de solución de Visual Studio servicio de aplicaciones es tan fácil como insertar un archivo index.html simple. Hola proceso de implementación de servicio de aplicaciones optimiza todos los detalles de hello, incluida la restauración de las dependencias de NuGet y generar archivos binarios de aplicación Hola. Puede seguir Hola origen control los procedimientos recomendados de mantenimiento del código solo en el repositorio Git y permiten la implementación de servicio de aplicaciones tenga cuidado de rest de Hola.

Hello pasos para insertar su tooApp de solución de Visual Studio son servicio Hola mismo como en hello [sección anterior](#overview), siempre que configure su solución y del repositorio como sigue:

* Usar Hola Visual Studio origen control opción toogenerate una `.gitignore` de archivo como imagen de hello siguiente o agregar manualmente un `.gitignore` archivo en la raíz del repositorio con contenido toothis similar [.gitignore ejemplo](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* Agregar repositorio de tooyour de árbol del hello toda la solución directorio, con el archivo .sln de hello en el directorio raíz del repositorio Hola.

Una vez haya configurado el repositorio tal como se describe y configurado la aplicación en Azure para la publicación continua desde uno de los repositorios de Git en línea hello, puede desarrollar su aplicación de ASP.NET localmente en Visual Studio y continuamente simplemente a implementar el código Insertar el repositorio de Git cambios tooyour en línea.

## <a name="disableCD"></a>Deshabilitación de la implementación continua
implementación continua toodisable,

1. En la hoja de menú de la aplicación Hola [portal de Azure], haga clic en **la implementación de aplicación > Opciones de implementación**. A continuación, haga clic en **desconexión** en hello **opciones de implementación** hoja.
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. Después de contestarse **Sí** toohello mensaje de confirmación, puede devolver la hoja de la aplicación tooyour y haga clic en **la implementación de aplicación > Opciones de implementación** si desea que tooset la publicación desde otro origen.

## <a name="additional-resources"></a>Recursos adicionales
* [¿Cómo se problemas comunes de tooinvestigate con una implementación continua](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* [¿Cómo toouse PowerShell de Azure]
* [¿Cómo toouse Hola herramientas de línea de comandos de Azure para Mac y Linux]
* [Documentación de Git]
* [Project Kudu](https://github.com/projectkudu/kudu/wiki)
* [Usar Azure tooautomatically generar una aplicación de integración continua/CD canalización toodeploy un ASP.NET 4](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

[servicio de aplicaciones de Azure]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[portal de Azure]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[¿Cómo toouse PowerShell de Azure]: /powershell/azureps-cmdlets-docs
[¿Cómo toouse Hola herramientas de línea de comandos de Azure para Mac y Linux]:../cli-install-nodejs.md
[Documentación de Git]: http://git-scm.com/documentation

[crear un repositorio (GitHub)]: https://help.github.com/articles/create-a-repo
[crear un repositorio (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[empezar a trabajar con VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview
