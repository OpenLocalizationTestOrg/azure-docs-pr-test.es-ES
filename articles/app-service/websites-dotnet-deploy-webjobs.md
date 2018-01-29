---
title: "Desarrollo e implementación de WebJobs mediante Visual Studio - Azure"
description: "Obtenga información sobre cómo desarrollar e implementar Azure WebJobs en Azure App Service mediante Visual Studio."
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
ms.date: 09/12/2017
ms.author: glenga;david.ebbo;suwatch;pbatum;naren.soni
ms.openlocfilehash: 8793485f2f1967e8c14ef335f14f81c9b946f974
ms.sourcegitcommit: 62eaa376437687de4ef2e325ac3d7e195d158f9f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2017
---
# <a name="develop-and-deploy-webjobs-using-visual-studio---azure-app-service"></a>Desarrollo e implementación de WebJobs mediante Visual Studio - Azure App Service

## <a name="overview"></a>Información general

En este tema se explica cómo usar Visual Studio para implementar un proyecto de aplicación de consola en una aplicación web en [App Service](app-service-web-overview.md) como [WebJob de Azure](http://go.microsoft.com/fwlink/?LinkId=390226). Para información sobre cómo implementar WebJobs con [Azure Portal](https://portal.azure.com), consulte [Ejecución de tareas en segundo plano con WebJobs](web-sites-create-web-jobs.md).

Cuando Visual Studio implementa un proyecto de aplicación de consola con funcionalidad WebJobs, realiza dos tareas:

* Copia archivos de tiempo de ejecución a la carpeta apropiada en la aplicación web (*App_Data/jobs/continuous* para WebJobs continuos, *App_Data/jobs/triggered* para WebJobs programados y a petición).
* Configura [trabajos de Azure Scheduler](#scheduler) para WebJobs que se programan para ejecutarse en momentos concretos. (Esto no se necesita para WebJobs continuos.)

Un proyecto con funcionalidad WebJobs tiene los siguientes elementos agregados:

* El paquete de NuGet [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) .
* Un archivo [webjob-publish-settings.json](#publishsettings) que contiene configuración de implementación y del programador. 

![Diagram showing what is added to a Console App to enable deployment as a WebJob](./media/websites-dotnet-deploy-webjobs/convert.png)

Puede agregar estos elementos a un proyecto de aplicación de consola existente o usar una plantilla para crear un nuevo proyecto de aplicación de consola con funcionalidad WebJobs. 

Puede implementar un proyecto como un WebJob por sí mismo o vincularlo a un proyecto web que se implemente automáticamente siempre que implemente el proyecto web. Para vincular proyectos, Visual Studio incluye el nombre del proyecto con funcionalidad WebJob en un archivo [webjobs-list.json](#webjobslist) en el proyecto web.

![Diagram showing WebJob project linking to web project](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a>Requisitos previos

Si usa Visual Studio 2015, instale el [Azure SDK para .NET (Visual Studio 2015)](https://azure.microsoft.com/downloads/).

Si usa Visual Studio 2017, instale la [carga de trabajo de desarrollo de Azure](https://docs.microsoft.com/visualstudio/install/install-visual-studio#step-4---select-workloads).

## <a id="convert"></a> Habilitación de la implementación de WebJobs para un proyecto de aplicación de consola existente

Tiene dos opciones:

* [Activación de la implementación automática con un proyecto web](#convertlink).

  Configure un proyecto de aplicación de consola existente de forma que se implemente automáticamente como un WebJob cuando implemente un proyecto web. Utilice esta opción cuando desee ejecutar su trabajo web en la misma aplicación web en la que ejecuta la aplicación web relacionada.

* [Activación de la implementación sin un proyecto web](#convertnolink).

  Configure un proyecto de aplicación de consola existente para implementar como WebJob por sí mismo, sin vínculo a un proyecto web. Use esta opción cuando desee ejecutar un trabajo web en una aplicación web por sí mismo, sin ninguna aplicación web ejecutándose en dicha aplicación web. Puede que desee hacer esto para poder escalar los recursos de su WebJob independientemente de los recursos de la aplicación web.

### <a id="convertlink"></a> Activación de la implementación de WebJobs automática con un proyecto web

1. Haga clic con el botón derecho en el proyecto web en el **Explorador de soluciones** y luego haga clic en **Agregar** > **Proyecto existente como WebJob de Azure**.
   
    ![Proyecto existente como trabajo web de Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    Aparecerá el cuadro de diálogo [Agregar WebJob de Azure](#configure) .
2. En la lista desplegable **Nombre de proyecto** , seleccione el proyecto de aplicación de consola para agregar como WebJob.
   
    ![Selecting project in Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. Complete el cuadro de diálogo [Agregar WebJob de Azure](#configure) y haga clic en **Aceptar**. 

### <a id="convertnolink"></a> Activación de la implementación de WebJobs sin un proyecto web
1. Haga clic con el botón derecho en el proyecto de aplicación de consola en el **Explorador de soluciones** y haga clic en **Publicar como WebJob de Azure...** 
   
    ![Publicar como WebJob de Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    Aparecerá el cuadro de diálogo [Agregar WebJob de Azure](#configure) , con el proyecto seleccionado en el cuadro **Nombre de proyecto** .
2. Complete el cuadro de diálogo [Agregar WebJob de Azure](#configure) y haga clic en **Aceptar**.
   
   Aparece el asistente de **Publicación web** .  Si no quiere realizar la publicación inmediatamente, cierre el asistente. La configuración que ha escrito se guarda para cuando desee [implementar el proyecto](#deploy).

## <a id="create"></a>Creación de un nuevo proyecto con funcionalidad WebJobs
Para crear un nuevo proyecto con funcionalidad WebJobs, puede usar la plantilla de proyecto de aplicación de consola y habilitar la implementación de WebJobs tal y como se explicó en la [sección anterior](#convert). Como alternativa, puede usar la plantilla para nuevos proyectos WebJobs:

* [Uso de la plantilla para nuevos proyectos de WebJobs para WebJob independiente](#createnolink)
  
    Cree un proyecto y configúrelo para implementarse por sí mismo como WebJob, sin vínculo a un proyecto web. Use esta opción cuando desee ejecutar un trabajo web en una aplicación web por sí mismo, sin ninguna aplicación web ejecutándose en dicha aplicación web. Puede que desee hacer esto para poder escalar los recursos de su WebJob independientemente de los recursos de la aplicación web.
* [Uso de la plantilla para nuevos proyectos de WebJobs para un WebJob vinculado a un proyecto web](#createlink)
  
    Cree un proyecto configurado para implementarse automáticamente como WebJob cuando se implementa un proyecto web en la misma solución. Utilice esta opción cuando desee ejecutar su trabajo web en la misma aplicación web en la que ejecuta la aplicación web relacionada.

> [!NOTE]
> La plantilla new-project de WebJobs instala automáticamente los paquetes NuGet e incluye código en *Program.cs* para el [SDK de WebJobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs). Si no quiere usar el SDK de WebJobs, quite o cambie la instrucción `host.RunAndBlock` en *Program.cs*.
> 
> 

### <a id="createnolink"></a> Uso de la plantilla para nuevos proyectos de WebJobs para WebJob independiente
1. Haga clic en **Archivo** > **Nuevo proyecto** y, en el cuadro de diálogo **Nuevo proyecto**, haga clic en **Nube** > **Azure WebJob (.NET Framework)**.
   
    ![New Project dialog showing WebJob template](./media/websites-dotnet-deploy-webjobs/np.png)
2. Siga las instrucciones mostradas anteriormente para [crear el proyecto de aplicación de consola para un proyecto de WebJobs independiente](#convertnolink).

### <a id="createlink"></a> Uso de la plantilla para nuevos proyectos de WebJobs para un WebJob vinculado a un proyecto web
1. Haga clic con el botón derecho en el proyecto web en el **Explorador de soluciones** y haga clic en **Agregar** > **Nuevo proyecto de WebJob de Azure**.
   
    ![New Azure WebJob Project menu entry](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    Aparecerá el cuadro de diálogo [Agregar WebJob de Azure](#configure) .
2. Complete el cuadro de diálogo [Agregar WebJob de Azure](#configure) y haga clic en **Aceptar**.

## <a id="configure"></a>Cuadro de diálogo Agregar WebJob de Azure
El cuadro de diálogo **Agregar Azure WebJob** le permite escribir el nombre de WebJob y ejecutar la configuración del modo de WebJob. 

![Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw2.png)

Los campos de este cuadro de diálogo corresponden a los campos del cuadro de diálogo **Agregar WebJob** de Azure Portal. Para obtener más información, consulte [Ejecución de tareas en segundo plano con WebJobs](web-sites-create-web-jobs.md).

> [!NOTE]
> * Para obtener información sobre la implementación de línea de comandos, consulte [Activación de la línea de comandos o de la entrega continua de Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).
> * Si implementa un WebJob y, a continuación, decide que desea cambiar el tipo de WebJob y volver a implementarlo, deberá eliminar el archivo *webjobs-publish-settings.json*. Esto hará que Visual Studio muestre de nuevo las opciones de publicación para que pueda cambiar el tipo de WebJob.
> * Si implementa un WebJob y más tarde cambia el modo de ejecución de continuo a no continuo o viceversa, Visual Studio crea un nuevo WebJob en Azure cuando vuelva a implementar. Si cambia otra configuración de programación pero deja el mismo modo de ejecución o cambia entre el modo Programado y Bajo demanda, Visual Studio actualiza el trabajo existente en lugar de crear uno nuevo.
> 
> 

## <a id="publishsettings"></a>webjob-publish-settings.json
Cuando crea una aplicación de consola para la implementación de WebJobs, Visual Studio instala el paquete de NuGet [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) y almacena la información de programación en un archivo *webjob-publish-settings.json* en la carpeta *Properties* del proyecto WebJobs. A continuación se muestra un ejemplo de ese archivo:

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

Puede editar este archivo directamente y Visual Studio proporciona IntelliSense. El archivo de esquema se almacena en [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) y se puede ver allí.  

## <a id="webjobslist"></a>webjobs-list.json
Cuando vincule un proyecto con funcionalidad WebJobs a un proyecto web, Visual Studio almacenará el nombre del proyecto WebJobs en un archivo *webjobs-list.json* en la carpeta *Properties* del proyecto web. La lista puede contener varios proyectos de WebJobs, tal y como se muestra en el siguiente ejemplo:

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

Puede editar este archivo directamente y Visual Studio proporciona IntelliSense. El archivo de esquema se almacena en [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) y se puede ver allí.

## <a id="deploy"></a>Implementación de un proyecto de WebJobs
Un proyecto WebJobs que ha vinculado a un proyecto web se implementa automáticamente con este último. Para información sobre la implementación de proyectos web, consulte las **guías** > **Implementar aplicación** del panel de navegación izquierdo.

Para implementar un proyecto de WebJobs por sí mismo, haga clic con el botón derecho en **Explorador de soluciones** y luego haga clic en **Publicar como Azure WebJob...** 

![Publicar como WebJob de Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

Para un trabajo web independiente, aparece el mismo asistente **Publicación web** que se usa para los proyectos web, pero con menos configuraciones disponibles para cambiar.
