---
title: Implementar trabajos web con Visual Studio
description: "Obtenga información sobre cómo implementar trabajos web de Azure en aplicaciones web del servicio de aplicaciones de Azure con Visual Studio."
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
ms.openlocfilehash: 5b0808afdadcf4d86a9a2d07ee6fc63b80b22993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="b2658-103">Implementar trabajos web con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b2658-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="b2658-104">Información general</span><span class="sxs-lookup"><span data-stu-id="b2658-104">Overview</span></span>
<span data-ttu-id="b2658-105">En este tema se explica cómo usar Visual Studio para implementar un proyecto de aplicación de consola en una aplicación web en [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) como [WebJob de Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="b2658-105">This topic explains how to use Visual Studio to deploy a Console Application project to a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="b2658-106">Para información sobre cómo implementar WebJobs con [Azure Portal](https://portal.azure.com), consulte [Ejecución de tareas en segundo plano con WebJobs](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="b2658-106">For information about how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="b2658-107">Cuando Visual Studio implementa un proyecto de aplicación de consola con funcionalidad WebJobs, realiza dos tareas:</span><span class="sxs-lookup"><span data-stu-id="b2658-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="b2658-108">Copia archivos de tiempo de ejecución a la carpeta apropiada en la aplicación web (*App_Data/jobs/continuous* para WebJobs continuos, *App_Data/jobs/triggered* para WebJobs programados y a petición).</span><span class="sxs-lookup"><span data-stu-id="b2658-108">Copies runtime files to the appropriate folder in the web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="b2658-109">Configura [trabajos del Programador de Azure](#scheduler) para WebJobs que se programan para ejecutarse en momentos concretos.</span><span class="sxs-lookup"><span data-stu-id="b2658-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled to run at particular times.</span></span> <span data-ttu-id="b2658-110">(Esto no se necesita para WebJobs continuos.)</span><span class="sxs-lookup"><span data-stu-id="b2658-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="b2658-111">Un proyecto con funcionalidad WebJobs tiene los siguientes elementos agregados:</span><span class="sxs-lookup"><span data-stu-id="b2658-111">A WebJobs-enabled project has the following items added to it:</span></span>

* <span data-ttu-id="b2658-112">El paquete de NuGet [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) .</span><span class="sxs-lookup"><span data-stu-id="b2658-112">The [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="b2658-113">Un archivo [webjob-publish-settings.json](#publishsettings) que contiene configuración de implementación y del programador.</span><span class="sxs-lookup"><span data-stu-id="b2658-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Diagram showing what is added to a Console App to enable deployment as a WebJob](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="b2658-115">Puede agregar estos elementos a un proyecto de aplicación de consola existente o usar una plantilla para crear un nuevo proyecto de aplicación de consola con funcionalidad WebJobs.</span><span class="sxs-lookup"><span data-stu-id="b2658-115">You can add these items to an existing Console Application project or use a template to create a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="b2658-116">Puede implementar un proyecto como un WebJob por sí mismo o vincularlo a un proyecto web que se implemente automáticamente siempre que implemente el proyecto web.</span><span class="sxs-lookup"><span data-stu-id="b2658-116">You can deploy a project as a WebJob by itself, or link it to a web project so that it automatically deploys whenever you deploy the web project.</span></span> <span data-ttu-id="b2658-117">Para vincular proyectos, Visual Studio incluye el nombre del proyecto con funcionalidad WebJob en un archivo [webjobs-list.json](#webjobslist) en el proyecto web.</span><span class="sxs-lookup"><span data-stu-id="b2658-117">To link projects, Visual Studio includes the name of the WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in the web project.</span></span>

![Diagram showing WebJob project linking to web project](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="b2658-119">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b2658-119">Prerequisites</span></span>
<span data-ttu-id="b2658-120">Las características de implementación de WebJobs están disponibles en Visual Studio al instalar el SDK de Azure para .NET:</span><span class="sxs-lookup"><span data-stu-id="b2658-120">WebJobs deployment features are available in Visual Studio when you install the Azure SDK for .NET:</span></span>

* <span data-ttu-id="b2658-121">[SDK de Azure para .NET (Visual Studio)](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="b2658-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="b2658-122"><a id="convert"></a>Activación de la implementación de trabajos web para un proyecto de Aplicación de consola existente</span><span class="sxs-lookup"><span data-stu-id="b2658-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="b2658-123">Tiene dos opciones:</span><span class="sxs-lookup"><span data-stu-id="b2658-123">You have two options:</span></span>

* <span data-ttu-id="b2658-124">[Activación de la implementación automática con un proyecto web](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="b2658-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="b2658-125">Configure un proyecto de aplicación de consola existente de forma que se implemente automáticamente como un WebJob cuando implemente un proyecto web.</span><span class="sxs-lookup"><span data-stu-id="b2658-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="b2658-126">Utilice esta opción cuando desee ejecutar su trabajo web en la misma aplicación web en la que ejecuta la aplicación web relacionada.</span><span class="sxs-lookup"><span data-stu-id="b2658-126">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>
* <span data-ttu-id="b2658-127">[Activación de la implementación sin un proyecto web](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="b2658-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="b2658-128">Configure un proyecto de aplicación de consola existente para implementar como WebJob por sí mismo, sin vínculo a un proyecto web.</span><span class="sxs-lookup"><span data-stu-id="b2658-128">Configure an existing Console Application project to deploy as a WebJob by itself, with no link to a web project.</span></span> <span data-ttu-id="b2658-129">Use esta opción cuando desee ejecutar un trabajo web en una aplicación web por sí mismo, sin ninguna aplicación web ejecutándose en dicha aplicación web.</span><span class="sxs-lookup"><span data-stu-id="b2658-129">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="b2658-130">Puede que desee hacer esto para poder escalar los recursos de su WebJob independientemente de los recursos de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="b2658-130">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="b2658-131"><a id="convertlink"></a> Activación de la implementación de WebJobs automática con un proyecto web</span><span class="sxs-lookup"><span data-stu-id="b2658-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="b2658-132">Haga clic con el botón derecho en el proyecto web en el **Explorador de soluciones** y luego haga clic en **Agregar** > **Proyecto existente como WebJob de Azure**.</span><span class="sxs-lookup"><span data-stu-id="b2658-132">Right-click the web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Proyecto existente como trabajo web de Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="b2658-134">Aparecerá el cuadro de diálogo [Agregar WebJob de Azure](#configure) .</span><span class="sxs-lookup"><span data-stu-id="b2658-134">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="b2658-135">En la lista desplegable **Nombre de proyecto** , seleccione el proyecto de aplicación de consola para agregar como WebJob.</span><span class="sxs-lookup"><span data-stu-id="b2658-135">In the **Project name** drop-down list, select the Console Application project to add as a WebJob.</span></span>
   
    ![Selecting project in Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="b2658-137">Complete el cuadro de diálogo [Agregar WebJob de Azure](#configure) y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b2658-137">Complete the [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="b2658-138"><a id="convertnolink"></a> Activación de la implementación de WebJobs sin un proyecto web</span><span class="sxs-lookup"><span data-stu-id="b2658-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="b2658-139">Haga clic con el botón derecho en el proyecto de aplicación de consola en el **Explorador de soluciones** y haga clic en **Publicar como WebJob de Azure...**</span><span class="sxs-lookup"><span data-stu-id="b2658-139">Right-click the Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Publicar como WebJob de Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="b2658-141">Aparecerá el cuadro de diálogo [Agregar WebJob de Azure](#configure) , con el proyecto seleccionado en el cuadro **Nombre de proyecto** .</span><span class="sxs-lookup"><span data-stu-id="b2658-141">The [Add Azure WebJob](#configure) dialog box appears, with the project selected in the **Project name** box.</span></span>
2. <span data-ttu-id="b2658-142">Complete el cuadro de diálogo [Agregar WebJob de Azure](#configure) y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b2658-142">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="b2658-143">Aparece el asistente de **Publicación web** .</span><span class="sxs-lookup"><span data-stu-id="b2658-143">The **Publish Web** wizard appears.</span></span>  <span data-ttu-id="b2658-144">Si no quiere realizar la publicación inmediatamente, cierre el asistente.</span><span class="sxs-lookup"><span data-stu-id="b2658-144">If you do not want to publish immediately, close the wizard.</span></span> <span data-ttu-id="b2658-145">La configuración que ha escrito se guarda para cuando desee [implementar el proyecto](#deploy).</span><span class="sxs-lookup"><span data-stu-id="b2658-145">The settings that you've entered are saved for when you do want to [deploy the project](#deploy).</span></span>

## <span data-ttu-id="b2658-146"><a id="create"></a>Creación de un nuevo proyecto con funcionalidad WebJobs</span><span class="sxs-lookup"><span data-stu-id="b2658-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="b2658-147">Para crear un nuevo proyecto con funcionalidad WebJobs, puede usar la plantilla de proyecto de aplicación de consola y habilitar la implementación de WebJobs tal y como se explicó en la [sección anterior](#convert).</span><span class="sxs-lookup"><span data-stu-id="b2658-147">To create a new WebJobs-enabled project, you can use the Console Application project template and enable WebJobs deployment as explained in [the previous section](#convert).</span></span> <span data-ttu-id="b2658-148">Como alternativa, puede usar la plantilla para nuevos proyectos WebJobs:</span><span class="sxs-lookup"><span data-stu-id="b2658-148">As an alternative, you can use the WebJobs new-project template:</span></span>

* [<span data-ttu-id="b2658-149">Uso de la plantilla para nuevos proyectos de WebJobs para WebJob independiente</span><span class="sxs-lookup"><span data-stu-id="b2658-149">Use the WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="b2658-150">Cree un proyecto y configúrelo para implementarse por sí mismo como WebJob, sin vínculo a un proyecto web.</span><span class="sxs-lookup"><span data-stu-id="b2658-150">Create a project and configure it to deploy by itself as a WebJob, with no link to a web project.</span></span> <span data-ttu-id="b2658-151">Use esta opción cuando desee ejecutar un trabajo web en una aplicación web por sí mismo, sin ninguna aplicación web ejecutándose en dicha aplicación web.</span><span class="sxs-lookup"><span data-stu-id="b2658-151">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="b2658-152">Puede que desee hacer esto para poder escalar los recursos de su WebJob independientemente de los recursos de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="b2658-152">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="b2658-153">Uso de la plantilla para nuevos proyectos de WebJobs para un WebJob vinculado a un proyecto web</span><span class="sxs-lookup"><span data-stu-id="b2658-153">Use the WebJobs new-project template for a WebJob linked to a web project</span></span>](#createlink)
  
    <span data-ttu-id="b2658-154">Cree un proyecto configurado para implementarse automáticamente como WebJob cuando se implementa un proyecto web en la misma solución.</span><span class="sxs-lookup"><span data-stu-id="b2658-154">Create a project that is configured to deploy automatically as a WebJob when a web project in the same solution is deployed.</span></span> <span data-ttu-id="b2658-155">Utilice esta opción cuando desee ejecutar su trabajo web en la misma aplicación web en la que ejecuta la aplicación web relacionada.</span><span class="sxs-lookup"><span data-stu-id="b2658-155">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="b2658-156">La plantilla new-project de WebJobs instala automáticamente los paquetes NuGet e incluye código en *Program.cs* para el [SDK de WebJobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="b2658-156">The WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for the [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="b2658-157">Si no quiere usar el SDK de WebJobs, quite o cambie la instrucción `host.RunAndBlock` en *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="b2658-157">If you don't want to use the WebJobs SDK, remove or change the `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="b2658-158"><a id="createnolink"></a> Uso de la plantilla para nuevos proyectos de WebJobs para WebJob independiente</span><span class="sxs-lookup"><span data-stu-id="b2658-158"><a id="createnolink"></a> Use the WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="b2658-159">Haga clic en **Archivo** > **Nuevo proyecto** y, en el cuadro de diálogo **Nuevo proyecto**, haga clic en **Nube** > **Azure WebJob (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="b2658-159">Click **File** > **New Project**, and then in the **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![New Project dialog showing WebJob template](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="b2658-161">Siga las instrucciones mostradas anteriormente para [crear el proyecto de aplicación de consola para un proyecto de WebJobs independiente](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="b2658-161">Follow the directions shown earlier to [make the Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="b2658-162"><a id="createlink"></a> Uso de la plantilla para nuevos proyectos de WebJobs para un WebJob vinculado a un proyecto web</span><span class="sxs-lookup"><span data-stu-id="b2658-162"><a id="createlink"></a> Use the WebJobs new-project template for a WebJob linked to a web project</span></span>
1. <span data-ttu-id="b2658-163">Haga clic con el botón derecho en el proyecto web en el **Explorador de soluciones** y haga clic en **Agregar** > **Nuevo proyecto de WebJob de Azure**.</span><span class="sxs-lookup"><span data-stu-id="b2658-163">Right-click the web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![New Azure WebJob Project menu entry](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="b2658-165">Aparecerá el cuadro de diálogo [Agregar WebJob de Azure](#configure) .</span><span class="sxs-lookup"><span data-stu-id="b2658-165">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="b2658-166">Complete el cuadro de diálogo [Agregar WebJob de Azure](#configure) y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b2658-166">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="b2658-167"><a id="configure"></a>Cuadro de diálogo Agregar WebJob de Azure</span><span class="sxs-lookup"><span data-stu-id="b2658-167"><a id="configure"></a>The Add Azure WebJob dialog</span></span>
<span data-ttu-id="b2658-168">El cuadro de diálogo **Agregar Azure WebJob** le permite escribir el nombre de WebJob y ejecutar la configuración del modo de WebJob.</span><span class="sxs-lookup"><span data-stu-id="b2658-168">The **Add Azure WebJob** dialog lets you enter the WebJob name and run mode setting for your WebJob.</span></span> 

![Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="b2658-170">Los campos de este cuadro de diálogo se corresponden con los campos del cuadro de diálogo **Nuevo trabajo** del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b2658-170">The fields in this dialog correspond to fields on the **New Job** dialog of the Azure Portal.</span></span> <span data-ttu-id="b2658-171">Para obtener más información, consulte [Ejecución de tareas en segundo plano con WebJobs](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="b2658-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="b2658-172">Para obtener información sobre la implementación de línea de comandos, consulte [Activación de la línea de comandos o de la entrega continua de WebJobs de Azure](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="b2658-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="b2658-173">Si implementa un WebJob y, a continuación, decide que desea cambiar el tipo de WebJob y volver a implementarlo, deberá eliminar el archivo webjobs-publish-settings.json.</span><span class="sxs-lookup"><span data-stu-id="b2658-173">If you deploy a WebJob and then decide you want to change the type of WebJob and redeploy, you'll need to delete the webjobs-publish-settings.json file.</span></span> <span data-ttu-id="b2658-174">Esto hará que Visual Studio muestre de nuevo las opciones de publicación para que pueda cambiar el tipo de WebJob.</span><span class="sxs-lookup"><span data-stu-id="b2658-174">This will make Visual Studio show the publishing options again, so you can change the type of WebJob.</span></span>
> * <span data-ttu-id="b2658-175">Si implementa un WebJob y más tarde cambia el modo de ejecución de continuo a no continuo o viceversa, Visual Studio crea un nuevo WebJob en Azure cuando vuelva a implementar.</span><span class="sxs-lookup"><span data-stu-id="b2658-175">If you deploy a WebJob and later change the run mode from continuous to non-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="b2658-176">Si cambia otra configuración de programación pero deja el mismo modo de ejecución o cambia entre el modo Programado y Bajo demanda, Visual Studio actualiza el trabajo existente en lugar de crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="b2658-176">If you change other scheduling settings but leave run mode the same or switch between Scheduled and On Demand, Visual Studio updates the existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="b2658-177"><a id="publishsettings"></a>webjob-publish-settings.json</span><span class="sxs-lookup"><span data-stu-id="b2658-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="b2658-178">Cuando crea una aplicación de consola para la implementación de WebJobs, Visual Studio instala el paquete de NuGet [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) y almacena la información de programación en un archivo *webjob-publish-settings.json* en la carpeta *Properties* del proyecto WebJobs.</span><span class="sxs-lookup"><span data-stu-id="b2658-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs the [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in the project *Properties* folder of the WebJobs project.</span></span> <span data-ttu-id="b2658-179">A continuación se muestra un ejemplo de ese archivo:</span><span class="sxs-lookup"><span data-stu-id="b2658-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="b2658-180">Puede editar este archivo directamente y Visual Studio proporciona IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="b2658-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="b2658-181">El archivo de esquema se almacena en [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) y se puede ver allí.</span><span class="sxs-lookup"><span data-stu-id="b2658-181">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="b2658-182"><a id="webjobslist"></a>webjobs-list.json</span><span class="sxs-lookup"><span data-stu-id="b2658-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="b2658-183">Cuando vincule un proyecto con funcionalidad WebJobs a un proyecto web, Visual Studio almacenará el nombre del proyecto WebJobs en un archivo *webjobs-list.json* en la carpeta *Properties* del proyecto web.</span><span class="sxs-lookup"><span data-stu-id="b2658-183">When you link a WebJobs-enabled project to a web project, Visual Studio stores the name of the WebJobs project in a *webjobs-list.json* file in the web project's *Properties* folder.</span></span> <span data-ttu-id="b2658-184">La lista puede contener varios proyectos de WebJobs, tal y como se muestra en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b2658-184">The list might contain multiple WebJobs projects, as shown in the following example:</span></span>

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

<span data-ttu-id="b2658-185">Puede editar este archivo directamente y Visual Studio proporciona IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="b2658-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="b2658-186">El archivo de esquema se almacena en [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) y se puede ver allí.</span><span class="sxs-lookup"><span data-stu-id="b2658-186">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="b2658-187"><a id="deploy"></a>Implementación de un proyecto de WebJobs</span><span class="sxs-lookup"><span data-stu-id="b2658-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="b2658-188">Un proyecto WebJobs que ha vinculado a un proyecto web se implementa automáticamente con este último.</span><span class="sxs-lookup"><span data-stu-id="b2658-188">A WebJobs project that you have linked to a web project deploys automatically with the web project.</span></span> <span data-ttu-id="b2658-189">Para obtener información sobre la implementación de proyectos web, consulte [Implementación en aplicaciones web](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b2658-189">For information about web project deployment, see [How to deploy to Web Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="b2658-190">Para implementar un proyecto de WebJobs por sí mismo, haga clic con el botón derecho en **Explorador de soluciones** y luego haga clic en **Publicar como Azure WebJob...**</span><span class="sxs-lookup"><span data-stu-id="b2658-190">To deploy a WebJobs project by itself, right-click the project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Publicar como WebJob de Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="b2658-192">Para un trabajo web independiente, aparece el mismo asistente **Publicación web** que se usa para los proyectos web, pero con menos configuraciones disponibles para cambiar.</span><span class="sxs-lookup"><span data-stu-id="b2658-192">For an independent WebJob, the same **Publish Web** wizard that is used for web projects appears, but with fewer settings available to change.</span></span>

## <span data-ttu-id="b2658-193"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b2658-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="b2658-194">Este artículo explica cómo implementar WebJobs con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b2658-194">This article has explained how to deploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="b2658-195">Para más información sobre cómo implementar WebJobs de Azure, consulte [Recursos recomendados de WebJobs de Azure: Implementación](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span><span class="sxs-lookup"><span data-stu-id="b2658-195">For more information about how to deploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>
