---
title: "aaaCreate un ASP.NET web aplicación en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toorun las aplicaciones web en el servicio de aplicación de Azure mediante la implementación predeterminada de hello ASP.NET web app."
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eec916b3c32b6c8b68083177938c5c822a9782b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a><span data-ttu-id="4791d-103">Creación de una aplicación web ASP.NET en Azure</span><span class="sxs-lookup"><span data-stu-id="4791d-103">Create an ASP.NET web app in Azure</span></span>

<span data-ttu-id="4791d-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="4791d-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="4791d-105">Este tutorial rápido muestra cómo toodeploy su primer ASP.NET web app tooAzure aplicaciones Web.</span><span class="sxs-lookup"><span data-stu-id="4791d-105">This quickstart shows how toodeploy your first ASP.NET web app tooAzure Web Apps.</span></span> <span data-ttu-id="4791d-106">Cuando haya terminado, tendrá un grupo de recursos que consta de un plan de App Service y una aplicación web de Azure con una aplicación web implementada.</span><span class="sxs-lookup"><span data-stu-id="4791d-106">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span></span>

<span data-ttu-id="4791d-107">Ver Hola vídeo toosee este inicio rápido en acción y, a continuación, siga Hola pasos usted mismo toopublish su primera aplicación de .NET en Azure.</span><span class="sxs-lookup"><span data-stu-id="4791d-107">Watch hello video toosee this quickstart in action and then follow hello steps yourself toopublish your first .NET app on Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a><span data-ttu-id="4791d-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4791d-108">Prerequisites</span></span>

<span data-ttu-id="4791d-109">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="4791d-109">toocomplete this tutorial:</span></span>

* <span data-ttu-id="4791d-110">Instalar [2017 de Visual Studio](https://www.visualstudio.com/downloads/) con hello siguiendo las cargas de trabajo:</span><span class="sxs-lookup"><span data-stu-id="4791d-110">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
    - <span data-ttu-id="4791d-111">**ASP.NET y desarrollo web**</span><span class="sxs-lookup"><span data-stu-id="4791d-111">**ASP.NET and web development**</span></span>
    - <span data-ttu-id="4791d-112">**Desarrollo de Azure**</span><span class="sxs-lookup"><span data-stu-id="4791d-112">**Azure development**</span></span>

    ![ASP.NET y desarrollo web y desarrollo de Azure (en web y en la nube)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="4791d-114">Creación de una aplicación web de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4791d-114">Create an ASP.NET web app</span></span>

<span data-ttu-id="4791d-115">Cree un proyecto nuevo en Visual Studio seleccionando **Archivo > Nuevo > Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="4791d-115">In Visual Studio, create a project by selecting **File > New > Project**.</span></span> 

<span data-ttu-id="4791d-116">Hola **nuevo proyecto** cuadro de diálogo, seleccione **Visual C# > Web > aplicación Web de ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="4791d-116">In hello **New Project** dialog, select **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span></span>

<span data-ttu-id="4791d-117">Nombre de la aplicación hello _myFirstAzureWebApp_y, a continuación, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4791d-117">Name hello application _myFirstAzureWebApp_, and then select **OK**.</span></span>
   
![Cuadro de diálogo Nuevo proyecto](./media/app-service-web-get-started-dotnet/new-project.png)

<span data-ttu-id="4791d-119">Puede implementar cualquier tipo de tooAzure de aplicación web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4791d-119">You can deploy any type of ASP.NET web app tooAzure.</span></span> <span data-ttu-id="4791d-120">Para este tutorial rápido, seleccione hello **MVC** plantilla y asegúrese de que la autenticación se establece demasiado**sin autenticación**.</span><span class="sxs-lookup"><span data-stu-id="4791d-120">For this quickstart, select hello **MVC** template, and make sure authentication is set too**No Authentication**.</span></span>
      
<span data-ttu-id="4791d-121">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4791d-121">Select **OK**.</span></span>

![Cuadro de diálogo New ASP.NET Project](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

<span data-ttu-id="4791d-123">En el menú de hello, seleccione **Depurar > Iniciar sin depurar** toorun hello web aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="4791d-123">From hello menu, select **Debug > Start without Debugging** toorun hello web app locally.</span></span>

![Ejecución de la aplicación de forma local](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a><span data-ttu-id="4791d-125">Publicar tooAzure</span><span class="sxs-lookup"><span data-stu-id="4791d-125">Publish tooAzure</span></span>

<span data-ttu-id="4791d-126">Hola **el Explorador de soluciones**, contextual hello **myFirstAzureWebApp** de proyecto y seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="4791d-126">In hello **Solution Explorer**, right-click hello **myFirstAzureWebApp** project and select **Publish**.</span></span>

![Publicar desde el Explorador de soluciones](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

<span data-ttu-id="4791d-128">Asegúrese de que **Microsoft Azure App Service** está seleccionado y seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="4791d-128">Make sure that **Microsoft Azure App Service** is selected and select **Publish**.</span></span>

![Publicar desde la página de información general del proyecto](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

<span data-ttu-id="4791d-130">Se abrirá hello **crear servicio en la aplicación** cuadro de diálogo, que le ayudará a crear la aplicación de todos los hello recursos de Azure necesarios toorun Hola ASP.NET web en Azure.</span><span class="sxs-lookup"><span data-stu-id="4791d-130">This opens hello **Create App Service** dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="4791d-131">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="4791d-131">Sign in tooAzure</span></span>

<span data-ttu-id="4791d-132">Hola **crear servicio en la aplicación** cuadro de diálogo, seleccione **agregar una cuenta**e inicie sesión en tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4791d-132">In hello **Create App Service** dialog, select **Add an account**, and sign in tooyour Azure subscription.</span></span> <span data-ttu-id="4791d-133">Si ya ha iniciado sesión, cuenta de hello select que contenga Hola había deseado suscripción a partir de la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="4791d-133">If you're already signed in, select hello account containing hello desired subscription from hello dropdown.</span></span>

> [!NOTE]
> <span data-ttu-id="4791d-134">Si ya ha iniciado sesión, no seleccione **Crear** todavía.</span><span class="sxs-lookup"><span data-stu-id="4791d-134">If you're already signed in, don't select **Create** yet.</span></span>
>
>
   
![Inicie sesión en tooAzure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a><span data-ttu-id="4791d-136">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="4791d-136">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

<span data-ttu-id="4791d-137">Siguiente demasiado**grupo de recursos**, seleccione **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="4791d-137">Next too**Resource Group**, select **New**.</span></span>

<span data-ttu-id="4791d-138">Grupo de recursos de nombre hello **myResourceGroup** y seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4791d-138">Name hello resource group **myResourceGroup** and select **OK**.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="4791d-139">Creación de un plan de App Service</span><span class="sxs-lookup"><span data-stu-id="4791d-139">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="4791d-140">Siguiente demasiado**Plan de servicio de aplicaciones**, seleccione **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="4791d-140">Next too**App Service Plan**, select **New**.</span></span> 

<span data-ttu-id="4791d-141">Hola **configurar el Plan de servicio de aplicación** cuadro de diálogo, usar la configuración de hello en tabla Hola siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="4791d-141">In hello **Configure App Service Plan** dialog, use hello settings in hello table following hello screenshot.</span></span>

![Creación de un plan de App Service](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| <span data-ttu-id="4791d-143">Configuración</span><span class="sxs-lookup"><span data-stu-id="4791d-143">Setting</span></span> | <span data-ttu-id="4791d-144">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="4791d-144">Suggested Value</span></span> | <span data-ttu-id="4791d-145">Descripción</span><span class="sxs-lookup"><span data-stu-id="4791d-145">Description</span></span> |
|-|-|-|
|<span data-ttu-id="4791d-146">Plan de App Service</span><span class="sxs-lookup"><span data-stu-id="4791d-146">App Service Plan</span></span>| <span data-ttu-id="4791d-147">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="4791d-147">myAppServicePlan</span></span> | <span data-ttu-id="4791d-148">Nombre del plan de servicio de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="4791d-148">Name of hello App Service plan.</span></span> |
| <span data-ttu-id="4791d-149">Ubicación</span><span class="sxs-lookup"><span data-stu-id="4791d-149">Location</span></span> | <span data-ttu-id="4791d-150">Europa occidental</span><span class="sxs-lookup"><span data-stu-id="4791d-150">West Europe</span></span> | <span data-ttu-id="4791d-151">Centro de datos de Hola donde se hospeda la aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="4791d-151">hello datacenter where hello web app is hosted.</span></span> |
| <span data-ttu-id="4791d-152">Tamaño</span><span class="sxs-lookup"><span data-stu-id="4791d-152">Size</span></span> | <span data-ttu-id="4791d-153">Gratuito</span><span class="sxs-lookup"><span data-stu-id="4791d-153">Free</span></span> | <span data-ttu-id="4791d-154">[Plan de tarifa](https://azure.microsoft.com/pricing/details/app-service/) determina las características de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="4791d-154">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/) determines hosting features.</span></span> |

<span data-ttu-id="4791d-155">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4791d-155">Select **OK**.</span></span>

## <a name="create-and-publish-hello-web-app"></a><span data-ttu-id="4791d-156">Crear y publicar la aplicación web de hello</span><span class="sxs-lookup"><span data-stu-id="4791d-156">Create and publish hello web app</span></span>

<span data-ttu-id="4791d-157">En **nombre de la aplicación Web**, escriba un nombre único de aplicación (los caracteres válidos son `a-z`, `0-9`, y `-`), o acepte el nombre único generado automáticamente por Hola.</span><span class="sxs-lookup"><span data-stu-id="4791d-157">In **Web App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept hello automatically generated unique name.</span></span> <span data-ttu-id="4791d-158">dirección URL de Hola de aplicación web de hello es `http://<app_name>.azurewebsites.net`, donde `<app_name>` es el nombre de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4791d-158">hello URL of hello web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your web app name.</span></span>

<span data-ttu-id="4791d-159">Seleccione **crear** toostart crear Hola recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="4791d-159">Select **Create** toostart creating hello Azure resources.</span></span>

![Configurar el nombre de la aplicación web](./media/app-service-web-get-started-dotnet/web-app-name.png)

<span data-ttu-id="4791d-161">Una vez que se complete el Asistente de hello, publica Hola ASP.NET web app tooAzure y, a continuación, inicia Hola aplicación en el Explorador de Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4791d-161">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>

![Aplicación web de ASP.NET publicada en Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

<span data-ttu-id="4791d-163">nombre de la aplicación web Hola especificado en hello [crear y publicar el paso](#create-and-publish-the-web-app) se usa como Hola prefijo de dirección URL en formato de hello `http://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="4791d-163">hello web app name specified in hello [create and publish step](#create-and-publish-the-web-app) is used as hello URL prefix in hello format `http://<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="4791d-164">Su aplicación web ASP.NET se está ejecutando en vivo en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="4791d-164">Congratulations, your ASP.NET web app is running live in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="4791d-165">Volver a implementar y aplicación de hello de actualización</span><span class="sxs-lookup"><span data-stu-id="4791d-165">Update hello app and redeploy</span></span>

<span data-ttu-id="4791d-166">De hello **el Explorador de soluciones**, abra _Views\Home\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="4791d-166">From hello **Solution Explorer**, open _Views\Home\Index.cshtml_.</span></span>

<span data-ttu-id="4791d-167">Buscar hello `<div class="jumbotron">` HTML etiqueta cerca de la parte superior de Hola y reemplace todo elemento de Hola con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="4791d-167">Find hello `<div class="jumbotron">` HTML tag near hello top, and replace hello entire element with hello following code:</span></span>

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

<span data-ttu-id="4791d-168">tooredeploy tooAzure, contextual hello **myFirstAzureWebApp** proyecto en **el Explorador de soluciones** y seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="4791d-168">tooredeploy tooAzure, right-click hello **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span></span>

<span data-ttu-id="4791d-169">Hola, página de publicación, seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="4791d-169">In hello publish page, select **Publish**.</span></span>

<span data-ttu-id="4791d-170">Cuando se completa la publicación, Visual Studio inicia una dirección URL toohello del explorador de la aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="4791d-170">When publishing completes, Visual Studio launches a browser toohello URL of hello web app.</span></span>

![Aplicación web actualizada de ASP.NET en Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="4791d-172">Administrar la aplicación web de Azure de hello</span><span class="sxs-lookup"><span data-stu-id="4791d-172">Manage hello Azure web app</span></span>

<span data-ttu-id="4791d-173">Vaya toohello <a href="https://portal.azure.com" target="_blank">portal de Azure</a> toomanage hello web app.</span><span class="sxs-lookup"><span data-stu-id="4791d-173">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app.</span></span>

<span data-ttu-id="4791d-174">En el menú izquierdo de hello, seleccione **servicios de aplicaciones**y, a continuación, seleccione nombre de saludo de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="4791d-174">From hello left menu, select **App Services**, and then select hello name of your Azure web app.</span></span>

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-get-started-dotnet/access-portal.png)

<span data-ttu-id="4791d-176">Podrá ver la página de información general de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4791d-176">You see your web app's Overview page.</span></span> <span data-ttu-id="4791d-177">En este caso, puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="4791d-177">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Hoja de App Service en Azure Portal](./media/app-service-web-get-started-dotnet/web-app-blade.png)

<span data-ttu-id="4791d-179">menú de la izquierda Hola proporciona distintas páginas para configurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4791d-179">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="4791d-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4791d-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4791d-181">ASP.NET con SQL Database</span><span class="sxs-lookup"><span data-stu-id="4791d-181">ASP.NET with SQL Database</span></span>](app-service-web-tutorial-dotnet-sqldatabase.md)
