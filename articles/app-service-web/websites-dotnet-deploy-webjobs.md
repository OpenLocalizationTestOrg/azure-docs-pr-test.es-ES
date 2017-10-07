---
title: aaaDeploy WebJobs con Visual Studio
description: "Obtenga información acerca de cómo toodeploy WebJobs de Azure tooAzure aplicación de servicio Web aplicaciones con Visual Studio."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a>Implementar trabajos web con Visual Studio
## <a name="overview"></a>Información general
Este tema explica cómo toouse Visual Studio toodeploy una aplicación de consola de proyecto aplicación web de tooa en [servicio de aplicaciones](http://go.microsoft.com/fwlink/?LinkId=529714) como un [WebJob de Azure](http://go.microsoft.com/fwlink/?LinkId=390226). Para obtener información acerca de cómo toodeploy trabajos Web mediante el uso de Hola [Portal de Azure](https://portal.azure.com), consulte [tareas en segundo plano ejecutar trabajos Web](web-sites-create-web-jobs.md).

Cuando Visual Studio implementa un proyecto de aplicación de consola con funcionalidad WebJobs, realiza dos tareas:

* En tiempo de ejecución de copias de archivos toohello de carpeta correspondiente en la aplicación web de hello (*App_Data/trabajos/continua* para trabajos Web continuos, *App_Data, trabajos/desencadena* de trabajos Web a petición y programado).
* Configura [trabajos del programador de Azure](#scheduler) de trabajos Web que están programado toorun en momentos concretos. (Esto no se necesita para WebJobs continuos.)

Un proyecto habilitado trabajos Web tiene Hola después tooit agregado elementos:

* Hola [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) paquete NuGet.
* Un archivo [webjob-publish-settings.json](#publishsettings) que contiene configuración de implementación y del programador. 

![Diagrama que muestra lo que se agrega la implementación de tooenable de aplicación de consola tooa como un trabajo Web](./media/websites-dotnet-deploy-webjobs/convert.png)

Puede agregar estos tooan elementos proyecto de aplicación de consola existente o utilizar una toocreate de plantilla un nuevo proyecto de aplicación de consola habilitada para trabajos Web. 

Puede implementar un proyecto como un trabajo Web por sí solo o vincularlo tooa proyecto de web para que se implemente automáticamente cada vez que implementar el proyecto web de Hola. toolink proyectos, Visual Studio incluye nombre Hola Hola habilitado trabajos Web del proyecto de en un [webjobs list.json](#webjobslist) archivo de proyecto web de Hola.

![Diagrama que muestra el proyecto WebJob vinculando tooweb proyecto](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a>Requisitos previos
Características de implementación de trabajos Web están disponibles en Visual Studio cuando se instala hello Azure SDK para. NET:

* [SDK de Azure para .NET (Visual Studio)](https://azure.microsoft.com/downloads/)

## <a id="convert"></a>Activación de la implementación de trabajos web para un proyecto de Aplicación de consola existente
Tiene dos opciones:

* [Activación de la implementación automática con un proyecto web](#convertlink).
  
    Configure un proyecto de aplicación de consola existente de forma que se implemente automáticamente como un WebJob cuando implemente un proyecto web. Utilice esta opción cuando desee toorun su trabajo Web en hello misma aplicación web en el que se ejecute hello relacionados con la aplicación web.
* [Activación de la implementación sin un proyecto web](#convertnolink).
  
    Configurar una toodeploy de proyecto de aplicación de consola existente como un trabajo Web por sí mismo, con ningún proyecto de web tooa de vínculo. Utilice esta opción cuando desee toorun un trabajo Web en una aplicación web por sí mismo, con ninguna aplicación web que se ejecuta en la aplicación web de hello. Es recomendable toodo esto en orden toobe puede tooscale los recursos de trabajo Web independientemente de los recursos de la aplicación web.

### <a id="convertlink"></a> Activación de la implementación de WebJobs automática con un proyecto web
1. Proyecto de web contextual hello en **el Explorador de soluciones**y, a continuación, haga clic en **agregar** > **proyecto existente como WebJob de Azure**.
   
    ![Proyecto existente como trabajo web de Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    Hola [Agregar trabajo Web de Azure](#configure) aparece el cuadro de diálogo.
2. Hola **nombre del proyecto** lista desplegable, seleccione hello tooadd de proyecto de aplicación de consola como un trabajo Web.
   
    ![Selecting project in Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. Hola completa [Agregar trabajo Web de Azure](#configure) cuadro de diálogo y, a continuación, haga clic en **Aceptar**. 

### <a id="convertnolink"></a> Activación de la implementación de WebJobs sin un proyecto web
1. Proyecto de aplicación de consola contextual hello en **el Explorador de soluciones**y, a continuación, haga clic en **publicar como trabajos Web de Azure...** . 
   
    ![Publicar como WebJob de Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    Hola [Agregar trabajo Web de Azure](#configure) aparecerá el cuadro de diálogo, seleccione proyecto hello en hello **nombre del proyecto** cuadro.
2. Hola completa [Agregar trabajo Web de Azure](#configure) cuadro de diálogo y, a continuación, haga clic en **Aceptar**.
   
   Hola **Publicar Web** aparece el Asistente para.  Si no desea toopublish inmediatamente, cierre al Asistente de Hola. configuración de Hola que ya ha escrito se guarda para cuando desee demasiado[implementar proyecto de hello](#deploy).

## <a id="create"></a>Creación de un nuevo proyecto con funcionalidad WebJobs
toocreate un nuevo proyecto de trabajos Web habilitada, puede usar Hola aplicación de consola plantilla y habilitar trabajos Web implementación del proyecto como se explica en [Hola sección anterior](#convert). Como alternativa, puede usar la plantilla de proyecto nuevo de hello trabajos Web:

* [Usar plantilla de proyecto nuevo de hello trabajos Web para un trabajo Web independiente](#createnolink)
  
    Crear un proyecto y lo configurará toodeploy por sí solo como un trabajo Web, con ningún proyecto de web tooa de vínculo. Utilice esta opción cuando desee toorun un trabajo Web en una aplicación web por sí mismo, con ninguna aplicación web que se ejecuta en la aplicación web de hello. Es recomendable toodo esto en orden toobe puede tooscale los recursos de trabajo Web independientemente de los recursos de la aplicación web.
* [Usar plantilla de proyecto nuevo de hello trabajos Web para un proyecto de web de trabajo Web tooa vinculado](#createlink)
  
    Cree un proyecto que esté configurado toodeploy automáticamente como un trabajo Web cuando un proyecto web en Hola se implementa la misma solución. Utilice esta opción cuando desee toorun su trabajo Web en hello misma aplicación web en el que se ejecute hello relacionados con la aplicación web.

> [!NOTE]
> plantilla de proyecto nuevo de trabajos Web Hola automáticamente instala los paquetes de NuGet e incluye el código en *Program.cs* para hello [SDK de WebJobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs). Si no desea toouse Hola SDK de WebJobs, quitar o cambiar hello `host.RunAndBlock` instrucción *Program.cs*.
> 
> 

### <a id="createnolink"></a>Usar plantilla de proyecto nuevo de hello trabajos Web para un trabajo Web independiente
1. Haga clic en **archivo** > **nuevo proyecto**y, a continuación, en hello **nuevo proyecto** haga clic en el cuadro de diálogo **nube**  >   **WebJob de Azure (.NET Framework)**.
   
    ![New Project dialog showing WebJob template](./media/websites-dotnet-deploy-webjobs/np.png)
2. Siga instrucciones Hola mostrados anteriormente demasiado[realizar Hola proyecto aplicación de consola en un proyecto independiente de trabajos Web](#convertnolink).

### <a id="createlink"></a>Usar plantilla de proyecto nuevo de hello trabajos Web para un proyecto de web de trabajo Web tooa vinculado
1. Proyecto de web contextual hello en **el Explorador de soluciones**y, a continuación, haga clic en **agregar** > **nuevo proyecto de WebJob de Azure**.
   
    ![New Azure WebJob Project menu entry](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    Hola [Agregar trabajo Web de Azure](#configure) aparece el cuadro de diálogo.
2. Hola completa [Agregar trabajo Web de Azure](#configure) cuadro de diálogo y, a continuación, haga clic en **Aceptar**.

## <a id="configure"></a>cuadro de diálogo de Hello Agregar trabajo Web de Azure
Hola **Agregar trabajo Web de Azure** cuadro de diálogo permite escriba el nombre del trabajo Web hello y ejecutar la configuración del modo de su trabajo Web. 

![Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw2.png)

campos de Hello en este cuadro de diálogo corresponden toofields en hello **nuevo trabajo** cuadro de diálogo de hello Portal de Azure. Para obtener más información, consulte [Ejecución de tareas en segundo plano con WebJobs](web-sites-create-web-jobs.md).

> [!NOTE]
> * Para obtener información sobre la implementación de línea de comandos, consulte [Activación de la línea de comandos o de la entrega continua de WebJobs de Azure](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).
> * Si implementa un trabajo Web y, a continuación, decide que desea toochange Hola tipo de trabajo Web y volver a implementar, necesitará el archivo de toodelete hello settings.json publicar trabajos Web. Esto hará que Visual Studio mostrar hello opciones de publicación de nuevo, por lo que puede cambiar el tipo de saludo de trabajo Web.
> * Si implementa un trabajo Web y posteriormente se cambia Hola a modo de ejecución de continuo toonon continua o viceversa, Visual Studio crea un trabajo Web nuevo en Azure al implementar de nuevo. Si cambiar otras opciones de programación, pero deje ejecutar modo Hola igual o alternar entre programada y a petición, actualizaciones de Visual Studio Hola trabajo existente en lugar de crear uno nuevo.
> 
> 

## <a id="publishsettings"></a>webjob-publish-settings.json
Cuando se configura una aplicación de consola para la implementación de trabajos Web, Visual Studio instala hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet paquete y almacenes de información de la programación una *settings.json publicar el trabajo Web*  archivo hello proyecto *propiedades* carpeta del proyecto de trabajos Web Hola. A continuación se muestra un ejemplo de ese archivo:

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

Puede editar este archivo directamente y Visual Studio proporciona IntelliSense. esquema de archivo de Hola se almacena en [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) y se podrán ver allí.  

## <a id="webjobslist"></a>webjobs-list.json
Al vincular un proyecto web de tooa de proyecto compatible con trabajos Web, Visual Studio almacena el nombre de Hola Hola trabajos Web del proyecto de en un *webjobs list.json* archivo hello web proyecto *propiedades* carpeta. lista de Hello podría contener varios proyectos de trabajos Web, como se muestra en el siguiente ejemplo de Hola:

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

Puede editar este archivo directamente y Visual Studio proporciona IntelliSense. esquema de archivo de Hola se almacena en [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) y se podrán ver allí.

## <a id="deploy"></a>Implementación de un proyecto de WebJobs
Un proyecto de trabajos Web que se ha vinculado tooa proyecto de web se implementa automáticamente con un proyecto web de Hola. Para obtener información acerca de la implementación de proyectos web, vea [cómo toodeploy tooWeb aplicaciones](web-sites-deploy.md).

toodeploy un proyecto de trabajos Web por sí mismo, haga clic en proyecto de hello en **el Explorador de soluciones** y haga clic en **publicar como trabajos Web de Azure...** . 

![Publicar como WebJob de Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

Para un trabajo Web independiente, Hola mismo **Publicar Web** asistente que se utiliza para proyectos web aparece, pero con menos toochange de configuración disponibles.

## <a id="nextsteps"></a>Pasos siguientes
En este artículo se ha explicado cómo toodeploy trabajos Web mediante Visual Studio. Para obtener más información acerca de cómo toodeploy WebJobs de Azure, consulte [WebJobs de Azure - recomienda recursos - implementación](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).

