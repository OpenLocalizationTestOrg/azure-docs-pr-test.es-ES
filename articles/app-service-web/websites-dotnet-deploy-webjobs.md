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
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="1dcdc-103">Implementar trabajos web con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1dcdc-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="1dcdc-104">Información general</span><span class="sxs-lookup"><span data-stu-id="1dcdc-104">Overview</span></span>
<span data-ttu-id="1dcdc-105">Este tema explica cómo toouse Visual Studio toodeploy una aplicación de consola de proyecto aplicación web de tooa en [servicio de aplicaciones](http://go.microsoft.com/fwlink/?LinkId=529714) como un [WebJob de Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="1dcdc-105">This topic explains how toouse Visual Studio toodeploy a Console Application project tooa web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="1dcdc-106">Para obtener información acerca de cómo toodeploy trabajos Web mediante el uso de Hola [Portal de Azure](https://portal.azure.com), consulte [tareas en segundo plano ejecutar trabajos Web](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="1dcdc-106">For information about how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="1dcdc-107">Cuando Visual Studio implementa un proyecto de aplicación de consola con funcionalidad WebJobs, realiza dos tareas:</span><span class="sxs-lookup"><span data-stu-id="1dcdc-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="1dcdc-108">En tiempo de ejecución de copias de archivos toohello de carpeta correspondiente en la aplicación web de hello (*App_Data/trabajos/continua* para trabajos Web continuos, *App_Data, trabajos/desencadena* de trabajos Web a petición y programado).</span><span class="sxs-lookup"><span data-stu-id="1dcdc-108">Copies runtime files toohello appropriate folder in hello web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="1dcdc-109">Configura [trabajos del programador de Azure](#scheduler) de trabajos Web que están programado toorun en momentos concretos.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled toorun at particular times.</span></span> <span data-ttu-id="1dcdc-110">(Esto no se necesita para WebJobs continuos.)</span><span class="sxs-lookup"><span data-stu-id="1dcdc-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="1dcdc-111">Un proyecto habilitado trabajos Web tiene Hola después tooit agregado elementos:</span><span class="sxs-lookup"><span data-stu-id="1dcdc-111">A WebJobs-enabled project has hello following items added tooit:</span></span>

* <span data-ttu-id="1dcdc-112">Hola [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-112">hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="1dcdc-113">Un archivo [webjob-publish-settings.json](#publishsettings) que contiene configuración de implementación y del programador.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Diagrama que muestra lo que se agrega la implementación de tooenable de aplicación de consola tooa como un trabajo Web](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="1dcdc-115">Puede agregar estos tooan elementos proyecto de aplicación de consola existente o utilizar una toocreate de plantilla un nuevo proyecto de aplicación de consola habilitada para trabajos Web.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-115">You can add these items tooan existing Console Application project or use a template toocreate a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="1dcdc-116">Puede implementar un proyecto como un trabajo Web por sí solo o vincularlo tooa proyecto de web para que se implemente automáticamente cada vez que implementar el proyecto web de Hola.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-116">You can deploy a project as a WebJob by itself, or link it tooa web project so that it automatically deploys whenever you deploy hello web project.</span></span> <span data-ttu-id="1dcdc-117">toolink proyectos, Visual Studio incluye nombre Hola Hola habilitado trabajos Web del proyecto de en un [webjobs list.json](#webjobslist) archivo de proyecto web de Hola.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-117">toolink projects, Visual Studio includes hello name of hello WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in hello web project.</span></span>

![Diagrama que muestra el proyecto WebJob vinculando tooweb proyecto](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="1dcdc-119">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1dcdc-119">Prerequisites</span></span>
<span data-ttu-id="1dcdc-120">Características de implementación de trabajos Web están disponibles en Visual Studio cuando se instala hello Azure SDK para. NET:</span><span class="sxs-lookup"><span data-stu-id="1dcdc-120">WebJobs deployment features are available in Visual Studio when you install hello Azure SDK for .NET:</span></span>

* <span data-ttu-id="1dcdc-121">[SDK de Azure para .NET (Visual Studio)](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="1dcdc-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="1dcdc-122"><a id="convert"></a>Activación de la implementación de trabajos web para un proyecto de Aplicación de consola existente</span><span class="sxs-lookup"><span data-stu-id="1dcdc-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="1dcdc-123">Tiene dos opciones:</span><span class="sxs-lookup"><span data-stu-id="1dcdc-123">You have two options:</span></span>

* <span data-ttu-id="1dcdc-124">[Activación de la implementación automática con un proyecto web](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="1dcdc-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="1dcdc-125">Configure un proyecto de aplicación de consola existente de forma que se implemente automáticamente como un WebJob cuando implemente un proyecto web.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="1dcdc-126">Utilice esta opción cuando desee toorun su trabajo Web en hello misma aplicación web en el que se ejecute hello relacionados con la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-126">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>
* <span data-ttu-id="1dcdc-127">[Activación de la implementación sin un proyecto web](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="1dcdc-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="1dcdc-128">Configurar una toodeploy de proyecto de aplicación de consola existente como un trabajo Web por sí mismo, con ningún proyecto de web tooa de vínculo.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-128">Configure an existing Console Application project toodeploy as a WebJob by itself, with no link tooa web project.</span></span> <span data-ttu-id="1dcdc-129">Utilice esta opción cuando desee toorun un trabajo Web en una aplicación web por sí mismo, con ninguna aplicación web que se ejecuta en la aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-129">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="1dcdc-130">Es recomendable toodo esto en orden toobe puede tooscale los recursos de trabajo Web independientemente de los recursos de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-130">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="1dcdc-131"><a id="convertlink"></a> Activación de la implementación de WebJobs automática con un proyecto web</span><span class="sxs-lookup"><span data-stu-id="1dcdc-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="1dcdc-132">Proyecto de web contextual hello en **el Explorador de soluciones**y, a continuación, haga clic en **agregar** > **proyecto existente como WebJob de Azure**.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-132">Right-click hello web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Proyecto existente como trabajo web de Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="1dcdc-134">Hola [Agregar trabajo Web de Azure](#configure) aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-134">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="1dcdc-135">Hola **nombre del proyecto** lista desplegable, seleccione hello tooadd de proyecto de aplicación de consola como un trabajo Web.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-135">In hello **Project name** drop-down list, select hello Console Application project tooadd as a WebJob.</span></span>
   
    ![Selecting project in Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="1dcdc-137">Hola completa [Agregar trabajo Web de Azure](#configure) cuadro de diálogo y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-137">Complete hello [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="1dcdc-138"><a id="convertnolink"></a> Activación de la implementación de WebJobs sin un proyecto web</span><span class="sxs-lookup"><span data-stu-id="1dcdc-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="1dcdc-139">Proyecto de aplicación de consola contextual hello en **el Explorador de soluciones**y, a continuación, haga clic en **publicar como trabajos Web de Azure...** .</span><span class="sxs-lookup"><span data-stu-id="1dcdc-139">Right-click hello Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Publicar como WebJob de Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="1dcdc-141">Hola [Agregar trabajo Web de Azure](#configure) aparecerá el cuadro de diálogo, seleccione proyecto hello en hello **nombre del proyecto** cuadro.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-141">hello [Add Azure WebJob](#configure) dialog box appears, with hello project selected in hello **Project name** box.</span></span>
2. <span data-ttu-id="1dcdc-142">Hola completa [Agregar trabajo Web de Azure](#configure) cuadro de diálogo y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-142">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="1dcdc-143">Hola **Publicar Web** aparece el Asistente para.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-143">hello **Publish Web** wizard appears.</span></span>  <span data-ttu-id="1dcdc-144">Si no desea toopublish inmediatamente, cierre al Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-144">If you do not want toopublish immediately, close hello wizard.</span></span> <span data-ttu-id="1dcdc-145">configuración de Hola que ya ha escrito se guarda para cuando desee demasiado[implementar proyecto de hello](#deploy).</span><span class="sxs-lookup"><span data-stu-id="1dcdc-145">hello settings that you've entered are saved for when you do want too[deploy hello project](#deploy).</span></span>

## <span data-ttu-id="1dcdc-146"><a id="create"></a>Creación de un nuevo proyecto con funcionalidad WebJobs</span><span class="sxs-lookup"><span data-stu-id="1dcdc-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="1dcdc-147">toocreate un nuevo proyecto de trabajos Web habilitada, puede usar Hola aplicación de consola plantilla y habilitar trabajos Web implementación del proyecto como se explica en [Hola sección anterior](#convert).</span><span class="sxs-lookup"><span data-stu-id="1dcdc-147">toocreate a new WebJobs-enabled project, you can use hello Console Application project template and enable WebJobs deployment as explained in [hello previous section](#convert).</span></span> <span data-ttu-id="1dcdc-148">Como alternativa, puede usar la plantilla de proyecto nuevo de hello trabajos Web:</span><span class="sxs-lookup"><span data-stu-id="1dcdc-148">As an alternative, you can use hello WebJobs new-project template:</span></span>

* [<span data-ttu-id="1dcdc-149">Usar plantilla de proyecto nuevo de hello trabajos Web para un trabajo Web independiente</span><span class="sxs-lookup"><span data-stu-id="1dcdc-149">Use hello WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="1dcdc-150">Crear un proyecto y lo configurará toodeploy por sí solo como un trabajo Web, con ningún proyecto de web tooa de vínculo.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-150">Create a project and configure it toodeploy by itself as a WebJob, with no link tooa web project.</span></span> <span data-ttu-id="1dcdc-151">Utilice esta opción cuando desee toorun un trabajo Web en una aplicación web por sí mismo, con ninguna aplicación web que se ejecuta en la aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-151">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="1dcdc-152">Es recomendable toodo esto en orden toobe puede tooscale los recursos de trabajo Web independientemente de los recursos de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-152">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="1dcdc-153">Usar plantilla de proyecto nuevo de hello trabajos Web para un proyecto de web de trabajo Web tooa vinculado</span><span class="sxs-lookup"><span data-stu-id="1dcdc-153">Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>](#createlink)
  
    <span data-ttu-id="1dcdc-154">Cree un proyecto que esté configurado toodeploy automáticamente como un trabajo Web cuando un proyecto web en Hola se implementa la misma solución.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-154">Create a project that is configured toodeploy automatically as a WebJob when a web project in hello same solution is deployed.</span></span> <span data-ttu-id="1dcdc-155">Utilice esta opción cuando desee toorun su trabajo Web en hello misma aplicación web en el que se ejecute hello relacionados con la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-155">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="1dcdc-156">plantilla de proyecto nuevo de trabajos Web Hola automáticamente instala los paquetes de NuGet e incluye el código en *Program.cs* para hello [SDK de WebJobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="1dcdc-156">hello WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for hello [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="1dcdc-157">Si no desea toouse Hola SDK de WebJobs, quitar o cambiar hello `host.RunAndBlock` instrucción *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-157">If you don't want toouse hello WebJobs SDK, remove or change hello `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="1dcdc-158"><a id="createnolink"></a>Usar plantilla de proyecto nuevo de hello trabajos Web para un trabajo Web independiente</span><span class="sxs-lookup"><span data-stu-id="1dcdc-158"><a id="createnolink"></a> Use hello WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="1dcdc-159">Haga clic en **archivo** > **nuevo proyecto**y, a continuación, en hello **nuevo proyecto** haga clic en el cuadro de diálogo **nube**  >   **WebJob de Azure (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-159">Click **File** > **New Project**, and then in hello **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![New Project dialog showing WebJob template](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="1dcdc-161">Siga instrucciones Hola mostrados anteriormente demasiado[realizar Hola proyecto aplicación de consola en un proyecto independiente de trabajos Web](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="1dcdc-161">Follow hello directions shown earlier too[make hello Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="1dcdc-162"><a id="createlink"></a>Usar plantilla de proyecto nuevo de hello trabajos Web para un proyecto de web de trabajo Web tooa vinculado</span><span class="sxs-lookup"><span data-stu-id="1dcdc-162"><a id="createlink"></a> Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>
1. <span data-ttu-id="1dcdc-163">Proyecto de web contextual hello en **el Explorador de soluciones**y, a continuación, haga clic en **agregar** > **nuevo proyecto de WebJob de Azure**.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-163">Right-click hello web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![New Azure WebJob Project menu entry](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="1dcdc-165">Hola [Agregar trabajo Web de Azure](#configure) aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-165">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="1dcdc-166">Hola completa [Agregar trabajo Web de Azure](#configure) cuadro de diálogo y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-166">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="1dcdc-167"><a id="configure"></a>cuadro de diálogo de Hello Agregar trabajo Web de Azure</span><span class="sxs-lookup"><span data-stu-id="1dcdc-167"><a id="configure"></a>hello Add Azure WebJob dialog</span></span>
<span data-ttu-id="1dcdc-168">Hola **Agregar trabajo Web de Azure** cuadro de diálogo permite escriba el nombre del trabajo Web hello y ejecutar la configuración del modo de su trabajo Web.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-168">hello **Add Azure WebJob** dialog lets you enter hello WebJob name and run mode setting for your WebJob.</span></span> 

![Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="1dcdc-170">campos de Hello en este cuadro de diálogo corresponden toofields en hello **nuevo trabajo** cuadro de diálogo de hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-170">hello fields in this dialog correspond toofields on hello **New Job** dialog of hello Azure Portal.</span></span> <span data-ttu-id="1dcdc-171">Para obtener más información, consulte [Ejecución de tareas en segundo plano con WebJobs](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="1dcdc-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="1dcdc-172">Para obtener información sobre la implementación de línea de comandos, consulte [Activación de la línea de comandos o de la entrega continua de WebJobs de Azure](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="1dcdc-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="1dcdc-173">Si implementa un trabajo Web y, a continuación, decide que desea toochange Hola tipo de trabajo Web y volver a implementar, necesitará el archivo de toodelete hello settings.json publicar trabajos Web.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-173">If you deploy a WebJob and then decide you want toochange hello type of WebJob and redeploy, you'll need toodelete hello webjobs-publish-settings.json file.</span></span> <span data-ttu-id="1dcdc-174">Esto hará que Visual Studio mostrar hello opciones de publicación de nuevo, por lo que puede cambiar el tipo de saludo de trabajo Web.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-174">This will make Visual Studio show hello publishing options again, so you can change hello type of WebJob.</span></span>
> * <span data-ttu-id="1dcdc-175">Si implementa un trabajo Web y posteriormente se cambia Hola a modo de ejecución de continuo toonon continua o viceversa, Visual Studio crea un trabajo Web nuevo en Azure al implementar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-175">If you deploy a WebJob and later change hello run mode from continuous toonon-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="1dcdc-176">Si cambiar otras opciones de programación, pero deje ejecutar modo Hola igual o alternar entre programada y a petición, actualizaciones de Visual Studio Hola trabajo existente en lugar de crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-176">If you change other scheduling settings but leave run mode hello same or switch between Scheduled and On Demand, Visual Studio updates hello existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="1dcdc-177"><a id="publishsettings"></a>webjob-publish-settings.json</span><span class="sxs-lookup"><span data-stu-id="1dcdc-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="1dcdc-178">Cuando se configura una aplicación de consola para la implementación de trabajos Web, Visual Studio instala hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet paquete y almacenes de información de la programación una *settings.json publicar el trabajo Web*  archivo hello proyecto *propiedades* carpeta del proyecto de trabajos Web Hola.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in hello project *Properties* folder of hello WebJobs project.</span></span> <span data-ttu-id="1dcdc-179">A continuación se muestra un ejemplo de ese archivo:</span><span class="sxs-lookup"><span data-stu-id="1dcdc-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="1dcdc-180">Puede editar este archivo directamente y Visual Studio proporciona IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="1dcdc-181">esquema de archivo de Hola se almacena en [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) y se podrán ver allí.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-181">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="1dcdc-182"><a id="webjobslist"></a>webjobs-list.json</span><span class="sxs-lookup"><span data-stu-id="1dcdc-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="1dcdc-183">Al vincular un proyecto web de tooa de proyecto compatible con trabajos Web, Visual Studio almacena el nombre de Hola Hola trabajos Web del proyecto de en un *webjobs list.json* archivo hello web proyecto *propiedades* carpeta.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-183">When you link a WebJobs-enabled project tooa web project, Visual Studio stores hello name of hello WebJobs project in a *webjobs-list.json* file in hello web project's *Properties* folder.</span></span> <span data-ttu-id="1dcdc-184">lista de Hello podría contener varios proyectos de trabajos Web, como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="1dcdc-184">hello list might contain multiple WebJobs projects, as shown in hello following example:</span></span>

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

<span data-ttu-id="1dcdc-185">Puede editar este archivo directamente y Visual Studio proporciona IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="1dcdc-186">esquema de archivo de Hola se almacena en [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) y se podrán ver allí.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-186">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="1dcdc-187"><a id="deploy"></a>Implementación de un proyecto de WebJobs</span><span class="sxs-lookup"><span data-stu-id="1dcdc-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="1dcdc-188">Un proyecto de trabajos Web que se ha vinculado tooa proyecto de web se implementa automáticamente con un proyecto web de Hola.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-188">A WebJobs project that you have linked tooa web project deploys automatically with hello web project.</span></span> <span data-ttu-id="1dcdc-189">Para obtener información acerca de la implementación de proyectos web, vea [cómo toodeploy tooWeb aplicaciones](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="1dcdc-189">For information about web project deployment, see [How toodeploy tooWeb Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="1dcdc-190">toodeploy un proyecto de trabajos Web por sí mismo, haga clic en proyecto de hello en **el Explorador de soluciones** y haga clic en **publicar como trabajos Web de Azure...** .</span><span class="sxs-lookup"><span data-stu-id="1dcdc-190">toodeploy a WebJobs project by itself, right-click hello project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Publicar como WebJob de Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="1dcdc-192">Para un trabajo Web independiente, Hola mismo **Publicar Web** asistente que se utiliza para proyectos web aparece, pero con menos toochange de configuración disponibles.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-192">For an independent WebJob, hello same **Publish Web** wizard that is used for web projects appears, but with fewer settings available toochange.</span></span>

## <span data-ttu-id="1dcdc-193"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1dcdc-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="1dcdc-194">En este artículo se ha explicado cómo toodeploy trabajos Web mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1dcdc-194">This article has explained how toodeploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="1dcdc-195">Para obtener más información acerca de cómo toodeploy WebJobs de Azure, consulte [WebJobs de Azure - recomienda recursos - implementación](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span><span class="sxs-lookup"><span data-stu-id="1dcdc-195">For more information about how toodeploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

