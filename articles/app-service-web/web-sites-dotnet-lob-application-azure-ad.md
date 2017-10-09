---
title: "aaaCreate una aplicación de Azure de línea de negocio con la autenticación de Active Directory de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un ASP.NET MVC de línea de negocio de aplicación de servicio de aplicaciones de Azure que autentica con Azure Active Directory"
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="5d6c0-103">Creación de una aplicación de línea de negocio de Azure con autenticación de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d6c0-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="5d6c0-104">Este artículo muestra cómo toocreate un .NET de línea de negocio de aplicación en [aplicaciones de Web del servicio de aplicación de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) con hello [autenticación / autorización](../app-service/app-service-authentication-overview.md) característica.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-104">This article shows you how toocreate a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using hello [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="5d6c0-105">También muestra cómo hello toouse [API Graph de Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery datos de directorio de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-105">It also shows how toouse hello [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery directory data in hello application.</span></span>

<span data-ttu-id="5d6c0-106">inquilino de Azure Active Directory de Hola que usa puede ser un directorio de solo Azure.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-106">hello Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="5d6c0-107">O bien, puede ser [sincronizado con su Active Directory local](../active-directory/active-directory-aadconnect.md) toocreate una experiencia de inicio de sesión única para los trabajadores que son locales y remotos.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-107">Or, it can be [synced with your on-premises Active Directory](../active-directory/active-directory-aadconnect.md) toocreate a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="5d6c0-108">En este artículo usa el directorio predeterminado de Hola para su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-108">This article uses hello default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="5d6c0-109">Lo que va a crear</span><span class="sxs-lookup"><span data-stu-id="5d6c0-109">What you will build</span></span>
<span data-ttu-id="5d6c0-110">Va a compilar una aplicación sencilla de crear-lectura-actualización y eliminación (CRUD) de línea de negocio en aplicaciones Web de servicio de aplicación que realiza un seguimiento de elementos de trabajo con hello siguientes características:</span><span class="sxs-lookup"><span data-stu-id="5d6c0-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with hello following features:</span></span>

* <span data-ttu-id="5d6c0-111">Autentica los usuarios contra Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d6c0-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="5d6c0-112">Consulta los usuarios y grupos del directorio con la [API Graph de Azure Active Directory](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="5d6c0-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="5d6c0-113">Use Hola ASP.NET MVC *sin autenticación* plantilla</span><span class="sxs-lookup"><span data-stu-id="5d6c0-113">Use hello ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="5d6c0-114">Si necesita control de acceso basado en roles (RBAC) para la aplicación de línea de negocio en Azure, consulte el [siguiente paso](#next).</span><span class="sxs-lookup"><span data-stu-id="5d6c0-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="5d6c0-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="5d6c0-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="5d6c0-116">Necesita Hola siguientes toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="5d6c0-116">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="5d6c0-117">Un inquilino de Azure Active Directory con usuarios en varios grupos</span><span class="sxs-lookup"><span data-stu-id="5d6c0-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="5d6c0-118">Aplicaciones de toocreate de permisos en el inquilino de Azure Active Directory Hola</span><span class="sxs-lookup"><span data-stu-id="5d6c0-118">Permissions toocreate applications on hello Azure Active Directory tenant</span></span>
* <span data-ttu-id="5d6c0-119">Visual Studio 2013, actualización 4 o posterior</span><span class="sxs-lookup"><span data-stu-id="5d6c0-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="5d6c0-120">SDK de Azure 2.8.1 o posterior</span><span class="sxs-lookup"><span data-stu-id="5d6c0-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a><span data-ttu-id="5d6c0-121">Crear e implementar un tooAzure de aplicación web</span><span class="sxs-lookup"><span data-stu-id="5d6c0-121">Create and deploy a web app tooAzure</span></span>
1. <span data-ttu-id="5d6c0-122">En Visual Studio, haga clic en **Archivo** > **Nuevo** > **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="5d6c0-123">Seleccione **Aplicación web ASP.NET**, elija el nombre del proyecto y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="5d6c0-124">Seleccione hello **MVC** plantilla, a continuación, cambie la autenticación Hola demasiado**sin autenticación**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-124">Select hello **MVC** template, then change hello authentication too**No Authentication**.</span></span> <span data-ttu-id="5d6c0-125">Asegúrese de que **Host Hola nube** está seleccionada y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-125">Make sure **Host in hello Cloud** is selected and click **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="5d6c0-126">Hola **crear servicio en la aplicación** cuadro de diálogo, haga clic en **agregar una cuenta** (y, a continuación, **agregar una cuenta** en la lista desplegable de hello) toolog en tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-126">In hello **Create App Service** dialog, click **Add an account** (and then **Add an account** in hello dropdown) toolog in tooyour Azure account.</span></span>
5. <span data-ttu-id="5d6c0-127">Después de iniciar sesión, configure la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-127">Once logged in configure your web app.</span></span> <span data-ttu-id="5d6c0-128">Cree un grupo de recursos y un nuevo plan de servicio de aplicaciones haciendo clic en hello respectivo **New** botón.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-128">Create a resource group and a new App Service plan by clicking hello respective **New** button.</span></span> <span data-ttu-id="5d6c0-129">Haga clic en **explorar servicios adicionales de Azure** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-129">Click **Explore additional Azure services** toocontinue.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="5d6c0-130">Hola **servicios** , haga clic en  **+**  tooadd una base de datos de SQL para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-130">In hello **Services** tab, click **+** tooadd a SQL Database for your app.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="5d6c0-131">En **Configurar base de datos de SQL**, haga clic en **New** toocreate una instancia de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-131">In **Configure SQL Database**, click **New** toocreate a SQL Server instance.</span></span>
8. <span data-ttu-id="5d6c0-132">En **Configurar SQL Server**, configure la instancia de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="5d6c0-133">A continuación, haga clic en **Aceptar**, **Aceptar**, y **crear** tookick desactivar la creación de la aplicación de hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-133">Then, click **OK**, **OK**, and **Create** tookick off hello app creation in Azure.</span></span>
9. <span data-ttu-id="5d6c0-134">En **actividad de servicio de aplicación de Azure**, puede ver cuando finalice la creación de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-134">In **Azure App Service Activity**, you can see when hello app creation is finished.</span></span> <span data-ttu-id="5d6c0-135">Haga clic en  **publicar &lt;* appname*> toothis aplicación Web ahora **, a continuación, haga clic en **publicar**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-135">Click **Publish &lt;*appname*> toothis Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="5d6c0-136">Una vez finalizada de Visual Studio, abre Hola publicar la aplicación en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-136">Once Visual Studio finishes, it opens hello publish app in hello browser.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="5d6c0-137">Configuración de la autenticación y el acceso al directorio</span><span class="sxs-lookup"><span data-stu-id="5d6c0-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="5d6c0-138">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5d6c0-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5d6c0-139">Hola menú izquierdo, haga clic en **servicios de aplicaciones** > **&lt;*appname*> ** > **autenticación / autorización**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-139">From hello left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="5d6c0-140">Active la autenticación de Azure Active Directory con un clic en **Activada** > **Azure Active Directory** > **Rápido** > **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="5d6c0-141">Haga clic en **guardar** en la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-141">Click **Save** in hello command bar.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="5d6c0-142">Una vez que se guardó correctamente la configuración de autenticación de hello, pruebe a navegar por la aplicación de tooyour nuevo en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-142">Once hello authentication settings are saved successfully, try navigating tooyour app again in hello browser.</span></span> <span data-ttu-id="5d6c0-143">La configuración predeterminada exigen la autenticación en la aplicación completa de hello.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-143">Your default settings enforce authentication on hello whole app.</span></span> <span data-ttu-id="5d6c0-144">Si ya no inició sesión, es redirigido tooa pantalla de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-144">If you aren't already logged in, you are redirected tooa login screen.</span></span> <span data-ttu-id="5d6c0-145">Una vez iniciada la sesión, verá la aplicación protegida por HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="5d6c0-146">A continuación, debe acceder a los tooenable toodirectory datos.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-146">Next, you need tooenable access toodirectory data.</span></span> 
5. <span data-ttu-id="5d6c0-147">Navegue toohello [portal clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="5d6c0-147">Navigate toohello [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="5d6c0-148">Hola menú izquierdo, haga clic en **Active Directory** > **directorio predeterminado** > **aplicaciones**  >   **&lt;* appname*> **.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-148">From hello left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="5d6c0-149">Se trata de aplicaciones de Azure Active Directory de Hola que creó el servicio de aplicación para tooenable Hola autorización o característica de autenticación.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-149">This is hello Azure Active Directory application that App Service created for you tooenable hello Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="5d6c0-150">Haga clic en **usuarios** y **grupos** toomake seguro de que tiene algunos usuarios y grupos en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-150">Click **Users** and **Groups** toomake sure that you have some users and groups in hello directory.</span></span> <span data-ttu-id="5d6c0-151">Si no es así, cree grupos y usuarios de prueba.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-151">If not, create a few test users and groups.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="5d6c0-152">Haga clic en **configurar** tooconfigure esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-152">Click **Configure** tooconfigure this application.</span></span>
9. <span data-ttu-id="5d6c0-153">Desplácese hacia abajo toohello **claves** sección y agregar una clave, seleccione una duración.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-153">Scroll down toohello **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="5d6c0-154">A continuación, haga clic en **Permisos delegados** y seleccione **Leer datos de directorio**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="5d6c0-155">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-155">Click **Save**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="5d6c0-156">Una vez que se guarda la configuración, se desplaza hacia arriba toohello **claves** sección y haga clic en hello **copia** clave de cliente de botón toocopy Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-156">Once your settings are saved, scroll back up toohello **Keys** section and click hello **Copy** button toocopy hello client key.</span></span> 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="5d6c0-157">Si sale ahora esta página, no será capaz de tooaccess este cliente clave nunca más.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-157">If you navigate away from this page now, you won't be able tooaccess this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="5d6c0-158">A continuación, debe tooconfigure su aplicación web con esta clave.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-158">Next, you need tooconfigure your web app with this key.</span></span> <span data-ttu-id="5d6c0-159">Inicie sesión en toohello [Explorador de recursos de Azure](https://resources.azure.com) con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-159">Log in toohello [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="5d6c0-160">En la parte superior de Hola de página de hello, haga clic en **lectura/escritura** toomake cambios en hello Explorador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-160">At hello top of hello page, click **Read/Write** toomake changes in hello Azure Resource Explorer.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="5d6c0-161">Buscar valores de autenticación para la aplicación, que se encuentra en las suscripciones de hello >  **&lt;* subscriptionname*> ** > **resourceGroups**  >   **&lt;* resourcegroupname*> ** > **proveedores** > **Microsoft.Web**  >  **sitios** > **&lt;*appname*> ** > **config**  >  **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-161">Find hello authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="5d6c0-162">Haga clic en **Editar**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-162">Click **Edit**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="5d6c0-163">Hola panel de edición, establezca hello `clientSecret` y `additionalLoginParams` propiedades como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-163">In hello editing pane, set hello `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="5d6c0-164">Haga clic en **colocar** en Hola superior toosubmit los cambios.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-164">Click **Put** at hello top toosubmit your changes.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="5d6c0-165">Ahora, tootest si tienen autorización Hola token tooaccess Hola API Graph de Azure Active Directory, simplemente vaya a  **https://&lt;*appname*>.azurewebsites.net/.auth/me** en el Explorador.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-165">Now, tootest if you have hello authorization token tooaccess hello Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="5d6c0-166">Si ha configurado todo correctamente, debería ver Hola `access_token` propiedad Hola respuesta JSON.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-166">If you configured everything correctly, you should see hello `access_token` property in hello JSON response.</span></span>
    
    <span data-ttu-id="5d6c0-167">Hola `~/.auth/me` ruta de acceso de dirección URL se administra mediante la autenticación de servicio de aplicación / toogive de autorización toda la información de Hola relacionados con la sesión tooyour autenticado.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-167">hello `~/.auth/me` URL path is managed by App Service Authentication / Authorization toogive you all hello information related tooyour authenticated session.</span></span> <span data-ttu-id="5d6c0-168">Para obtener más información, consulte [Autenticación y autorización en el Servicio de aplicaciones de Azure](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5d6c0-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="5d6c0-169">Hola `access_token` tiene un período de caducidad.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-169">hello `access_token` has an expiration period.</span></span> <span data-ttu-id="5d6c0-170">Sin embargo, la autorización y autenticación de App Service proporciona una funcionalidad de actualización del token con `~/.auth/refresh`.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="5d6c0-171">Para obtener más información acerca de cómo toouse, consulte [tienda de símbolo (token) de servicio de aplicaciones](https://cgillum.tech/2016/03/07/app-service-token-store/).</span><span class="sxs-lookup"><span data-stu-id="5d6c0-171">For more information on how toouse it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="5d6c0-172">A continuación, hará algo útil con los datos del directorio.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a><span data-ttu-id="5d6c0-173">Agregar funcionalidad de línea de negocio tooyour aplicación</span><span class="sxs-lookup"><span data-stu-id="5d6c0-173">Add line-of-business functionality tooyour app</span></span>
<span data-ttu-id="5d6c0-174">Ahora, cree un rastreador de elementos de trabajo CRUD sencillo.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="5d6c0-175">En la carpeta de ~\Models hello, cree un archivo de clase denominado WorkItem.cs y reemplace `public class WorkItem {...}` con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="5d6c0-175">In hello ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with hello following code:</span></span>
   
     <span data-ttu-id="5d6c0-176">using System.ComponentModel.DataAnnotations;</span><span class="sxs-lookup"><span data-stu-id="5d6c0-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="5d6c0-177">public class WorkItem   {</span><span class="sxs-lookup"><span data-stu-id="5d6c0-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="5d6c0-178">}</span><span class="sxs-lookup"><span data-stu-id="5d6c0-178">}</span></span>
   
     <span data-ttu-id="5d6c0-179">public enum WorkItemStatus   {</span><span class="sxs-lookup"><span data-stu-id="5d6c0-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="5d6c0-180">}</span><span class="sxs-lookup"><span data-stu-id="5d6c0-180">}</span></span>
2. <span data-ttu-id="5d6c0-181">Crear Hola proyecto toomake su nueva lógica de scaffolding de toohello accesible de modelo en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-181">Build hello project toomake your new model accessible toohello scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="5d6c0-182">Agregar un nuevo elemento con scaffolding `WorkItemsController` toohello ~\Controllers carpeta (haga clic en **controladores**, seleccione demasiado**agregar**y seleccione **nuevo elemento con scaffolding**).</span><span class="sxs-lookup"><span data-stu-id="5d6c0-182">Add a new scaffolded item `WorkItemsController` toohello ~\Controllers folder (right-click **Controllers**, point too**Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="5d6c0-183">Seleccione **Controlador MVC 5 con vistas, usando Entity Framework** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="5d6c0-184">A continuación, haga clic en el modelo Hola SELECT que ha creado,  **+**  y, a continuación, **agregar** tooadd un contexto de datos y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-184">Select hello model that you created, then click **+** and then **Add** tooadd a data context, and then click **Add**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="5d6c0-185">En ~\Views\WorkItems\Create.cshtml (un elemento con scaffolding automáticamente), busque hello `Html.BeginForm` método auxiliar y asegúrese de hello siguiendo el resaltado cambios:</span><span class="sxs-lookup"><span data-stu-id="5d6c0-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find hello `Html.BeginForm` helper method and make hello following highlighted changes:</span></span>  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="5d6c0-186">Tenga en cuenta que `token` y `tenant` usan hello `AadPicker` toomake objeto llamadas de API Graph de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-186">Note that `token` and `tenant` are used by hello `AadPicker` object toomake Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="5d6c0-187">Agregará `AadPicker` más adelante.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="5d6c0-188">Igual de bien que puedas `token` y `tenant` del lado de cliente de hello con `~/.auth/me`, sino que sería una llamada adicional del servidor.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-188">You can just as well get `token` and `tenant` from hello client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="5d6c0-189">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5d6c0-189">For example:</span></span>
   > 
   > <span data-ttu-id="5d6c0-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span><span class="sxs-lookup"><span data-stu-id="5d6c0-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="5d6c0-191">Realizar Hola mismos cambios con ~ \Views\WorkItems\Edit.cshtml.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-191">Make hello same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="5d6c0-192">Hola `AadPicker` objeto se define en una secuencia de comandos que necesita tooadd tooyour proyecto.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-192">hello `AadPicker` object is defined in a script that you need tooadd tooyour project.</span></span> <span data-ttu-id="5d6c0-193">Haga clic en hello ~\Scripts carpeta, seleccione demasiado**agregar**y haga clic en **archivo JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-193">Right-click hello ~\Scripts folder, point too**Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="5d6c0-194">Tipo de `AadPickerLibrary` Hola filename y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-194">Type `AadPickerLibrary` for hello filename and click **OK**.</span></span>
9. <span data-ttu-id="5d6c0-195">Copiar el contenido de Hola de [aquí](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) en ~ \Scripts\AadPickerLibrary.js.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-195">Copy hello content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="5d6c0-196">En el script de Hola, Hola `AadPicker` objeto llamadas [API Graph de Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch para usuarios y grupos que coinciden con la entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-196">In hello script, hello `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch for users and groups that match hello input.</span></span>  
10. <span data-ttu-id="5d6c0-197">~\Scripts\AadPickerLibrary.js también utiliza hello [jQuery UI Autocompletar widget](https://jqueryui.com/autocomplete/).</span><span class="sxs-lookup"><span data-stu-id="5d6c0-197">~\Scripts\AadPickerLibrary.js also uses hello [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="5d6c0-198">Por lo que deberá proyecto tooyour de tooadd jQuery UI.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-198">So you need tooadd jQuery UI tooyour project.</span></span> <span data-ttu-id="5d6c0-199">Haga clic con el botón derecho en el proyecto y haga clic en **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="5d6c0-200">En el Administrador de paquetes de NuGet hello, haga clic en Examinar, tipo **jquery ui** en Hola barra de búsqueda y haga clic en **jQuery.UI.Combined**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-200">In hello NuGet Package Manager, click Browse, type **jquery-ui** in hello search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="5d6c0-201">En el panel derecho de hello, haga clic en **instalar**, a continuación, haga clic en **Aceptar** tooproceed.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-201">In hello right pane, click **Install**, then click **OK** tooproceed.</span></span>
13. <span data-ttu-id="5d6c0-202">Abra ~\App_Start\BundleConfig.cs y realice Hola siguiendo el resaltado cambios:</span><span class="sxs-lookup"><span data-stu-id="5d6c0-202">Open ~\App_Start\BundleConfig.cs and make hello following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    <span data-ttu-id="5d6c0-203">Hay más rendimiento maneras toomanage JavaScript y archivos CSS en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-203">There are more performant ways toomanage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="5d6c0-204">Sin embargo, para simplificar el trabajo solo va toopiggyback en las agrupaciones de Hola que se cargan con cada vista.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-204">However, for simplicity you're just going toopiggyback on hello bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="5d6c0-205">Por último, en ~ \Global.asax, agregar Hola después de la línea de código de hello `Application_Start()` método.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-205">Finally, in ~\Global.asax, add hello following line of code in hello `Application_Start()` method.</span></span> <span data-ttu-id="5d6c0-206">`Ctrl`+`.`en cada error de resolución de nombres demasiado corregirlo.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-206">`Ctrl`+`.` on each naming resolution error too fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="5d6c0-207">Necesita esta línea de código porque usa la plantilla MVC predeterminada hello <code>[ValidateAntiForgeryToken]</code> decoración en algunas de las acciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-207">You need this line of code because hello default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of hello actions.</span></span> <span data-ttu-id="5d6c0-208">Pagar comportamiento toohello descrito por [Allen Brock](https://twitter.com/BrockLAllen) en [MVC 4, AntiForgeryToken y notificaciones](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) su HTTP POST puede producir un error de validación del token antifalsificación porque:</span><span class="sxs-lookup"><span data-stu-id="5d6c0-208">Due toohello behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="5d6c0-209">Azure Active Directory no envía http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider hello, y es necesario de forma predeterminada para el token antifalsificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-209">Azure Active Directory does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by hello anti-forgery token.</span></span>
    > * <span data-ttu-id="5d6c0-210">Si Azure Active Directory directory sincronizado con AD FS, confianza Hola AD FS de forma predeterminada no enviar hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider notificación, aunque puede configurar manualmente AD FS toosend Esta notificación.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-210">If Azure Active Directory is directory synced with AD FS, hello AD FS trust by default does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS toosend this claim.</span></span>
    > 
    > <span data-ttu-id="5d6c0-211">`ClaimTypes.NameIdentifies`Especifica la notificación de hello `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, que proporciona Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-211">`ClaimTypes.NameIdentifies` specifies hello claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="5d6c0-212">Ahora, publique los cambios.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-212">Now, publish your changes.</span></span> <span data-ttu-id="5d6c0-213">Haga clic con el botón derecho en el proyecto y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="5d6c0-214">Haga clic en **configuración**, asegúrese de que hay un tooyour de cadena de conexión base de datos SQL, seleccione **Actualizar base de datos** toomake Hola cambios de esquema para el modelo y haga clic en **publicar** .</span><span class="sxs-lookup"><span data-stu-id="5d6c0-214">Click **Settings**, make sure there is a connection string tooyour SQL Database, select **Update Database** toomake hello schema changes for your model, and click **Publish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="5d6c0-215">En el Explorador de hello, desplácese toohttps: / /&lt;*appname*>.azurewebsites.net/workitems y haga clic en **crear nuevo**.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-215">In hello browser, navigate toohttps://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="5d6c0-216">Haga clic en hello **AssignedToName** cuadro.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-216">Click in hello **AssignedToName** box.</span></span> <span data-ttu-id="5d6c0-217">Ahora debería ver los usuarios y grupos desde el inquilino de Azure Active Directory en una lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="5d6c0-218">Puede escribir toofilter, o usar hello `Up` o `Down` clave o haga clic en tooselect Hola usuario o grupo.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-218">You can type toofilter, or use hello `Up` or `Down` key or click tooselect hello user or group.</span></span> 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="5d6c0-219">Haga clic en **crear** cambios de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-219">Click **Create** toosave hello changes.</span></span> <span data-ttu-id="5d6c0-220">A continuación, haga clic en **editar** en el trabajo de hello creado elemento tooobserve Hola mismo comportamiento.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-220">Then, click **Edit** on hello created work item tooobserve hello same behavior.</span></span>

<span data-ttu-id="5d6c0-221">Enhorabuena, está ejecutando una aplicación de línea de negocio en Azure con acceso al directorio.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="5d6c0-222">No hay mucho más que puede hacer con hello API Graph.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-222">There's a lot more you can do with hello Graph API.</span></span> <span data-ttu-id="5d6c0-223">Consulte [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog)(Referencias de la API Graph de Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5d6c0-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="5d6c0-224">siguiente paso</span><span class="sxs-lookup"><span data-stu-id="5d6c0-224">Next Step</span></span>
<span data-ttu-id="5d6c0-225">Si tiene el control de acceso basado en roles (RBAC) para la aplicación de línea de negocio de azure, consulte [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) para obtener un ejemplo de equipo de Azure Active Directory Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from hello Azure Active Directory team.</span></span> <span data-ttu-id="5d6c0-226">Muestra cómo tooenable roles para la aplicación de Azure Active Directory y, a continuación, autorizar a los usuarios con hello `[Authorize]` decoración.</span><span class="sxs-lookup"><span data-stu-id="5d6c0-226">It shows you how tooenable roles for your Azure Active Directory application, and then authorize users with hello `[Authorize]` decoration.</span></span>

<span data-ttu-id="5d6c0-227">Si la aplicación de línea de negocio debe tener acceso a datos tooon locales, consulte [acceder a recursos usando conexiones híbridas en el servicio de aplicación de Azure local](web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5d6c0-227">If your line-of-business app needs access tooon-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="5d6c0-228">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="5d6c0-228">Further resources</span></span>
* [<span data-ttu-id="5d6c0-229">Autenticación y autorización en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="5d6c0-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="5d6c0-230">Autenticación con Active Directory local en aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="5d6c0-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="5d6c0-231">Creación de una aplicación de línea de negocio en Azure con autenticación de AD FS</span><span class="sxs-lookup"><span data-stu-id="5d6c0-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="5d6c0-232">Hello Azure AD Graph API y autenticación de servicio de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5d6c0-232">App Service Auth and hello Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="5d6c0-233">Ejemplos y documentación de Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d6c0-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="5d6c0-234">Tipos de notificaciones y tokens admitidos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d6c0-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)
