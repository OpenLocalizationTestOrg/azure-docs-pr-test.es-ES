---
title: "aaaConfigure autenticación y autorización para una aplicación personalizada que llama hello Azure tiempo serie visión API | Documentos de Microsoft"
description: "Este tutorial le explica cómo tooconfigure autenticación y autorización para una aplicación personalizada que llama hello Azure tiempo serie visión API"
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a><span data-ttu-id="2c42f-103">Autenticación y autorización para la API de Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="2c42f-103">Authentication and authorization for Azure Time Series Insights API</span></span>

<span data-ttu-id="2c42f-104">Este artículo explica cómo tooconfigure una aplicación personalizada que llama hello Azure tiempo serie visión API.</span><span class="sxs-lookup"><span data-stu-id="2c42f-104">This article explains how tooconfigure a custom application that calls hello Azure Time Series Insights API.</span></span>

## <a name="service-principal"></a><span data-ttu-id="2c42f-105">Entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="2c42f-105">Service principal</span></span>

<span data-ttu-id="2c42f-106">Esta sección explica cómo tooconfigure tooaccess de una aplicación Hola tiempo serie visión API en nombre de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="2c42f-106">This section explains how tooconfigure an application tooaccess hello Time Series Insights API on behalf of hello application.</span></span> <span data-ttu-id="2c42f-107">aplicación Hello puede consultar datos o publicar datos de referencia en entorno de visión de la serie de tiempo de hello con credenciales de la aplicación y no las credenciales de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c42f-107">hello application can then query data or publish reference data in hello Time Series Insights environment with application credentials and not hello user credentials.</span></span>

<span data-ttu-id="2c42f-108">Cuando haya una aplicación que necesite tooaccess visión de la serie de tiempo, debe configurar una aplicación de Azure Active Directory y asignar directivas de acceso de datos de hello en entorno de visión de la serie de tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c42f-108">When you have an application that needs tooaccess Time Series Insights, you must set up an Azure Active Directory application and assign hello data access policies in hello Time Series Insights environment.</span></span> <span data-ttu-id="2c42f-109">Este enfoque es preferible toorunning Hola aplicación bajo sus propias credenciales porque:</span><span class="sxs-lookup"><span data-stu-id="2c42f-109">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="2c42f-110">Puede asignar permisos de identidad de aplicación de toohello que son diferentes de sus propios permisos.</span><span class="sxs-lookup"><span data-stu-id="2c42f-110">You can assign permissions toohello app identity that are different from your own permissions.</span></span> <span data-ttu-id="2c42f-111">Normalmente, estos permisos son tooexactly restringido qué aplicación hello necesita toodo.</span><span class="sxs-lookup"><span data-stu-id="2c42f-111">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span> <span data-ttu-id="2c42f-112">Por ejemplo, puede permitir Hola aplicación tooonly lee datos en un entorno de visión de la serie de tiempo determinado.</span><span class="sxs-lookup"><span data-stu-id="2c42f-112">For example, you can allow hello app tooonly read data in a particular Time Series Insights environment.</span></span>
* <span data-ttu-id="2c42f-113">No tiene credenciales de la aplicación de toochange Hola si cambian sus responsabilidades.</span><span class="sxs-lookup"><span data-stu-id="2c42f-113">You don't have toochange hello app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="2c42f-114">Puede usar una autenticación de certificados o una aplicación clave tooautomate si ejecuta un script de instalación desatendida.</span><span class="sxs-lookup"><span data-stu-id="2c42f-114">You can use a certificate or an application key tooautomate authentication when you're running an unattended script.</span></span>

<span data-ttu-id="2c42f-115">Este artículo muestra cómo tooperform los pasos a través de Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2c42f-115">This article shows you how tooperform those steps through hello Azure portal.</span></span> <span data-ttu-id="2c42f-116">Se centra en una aplicación de inquilino único donde la aplicación hello es toorun previsto en sólo una organización.</span><span class="sxs-lookup"><span data-stu-id="2c42f-116">It focuses on a single-tenant application where hello application is intended toorun in only one organization.</span></span> <span data-ttu-id="2c42f-117">El usuario normalmente usa aplicaciones de un único inquilino para aplicaciones de línea de negocio que se ejecutan en la organización.</span><span class="sxs-lookup"><span data-stu-id="2c42f-117">You typically use single-tenant applications for line-of-business applications that run in your organization.</span></span>

<span data-ttu-id="2c42f-118">flujo del programa de instalación de Hello consta de tres pasos principales:</span><span class="sxs-lookup"><span data-stu-id="2c42f-118">hello setup flow consists of three high-level steps:</span></span>

1. <span data-ttu-id="2c42f-119">Creación de una aplicación en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2c42f-119">Create an application in Azure Active Directory.</span></span>
2. <span data-ttu-id="2c42f-120">Autorizar este entorno de visión de la serie de tiempo de aplicación tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="2c42f-120">Authorize this application tooaccess hello Time Series Insights environment.</span></span>
3. <span data-ttu-id="2c42f-121">Usar Id. de aplicación de Hola y clave tooacquire un token toohello `"https://api.timeseries.azure.com/"` público o recurso.</span><span class="sxs-lookup"><span data-stu-id="2c42f-121">Use hello application ID and key tooacquire a token toohello `"https://api.timeseries.azure.com/"` audience or resource.</span></span> <span data-ttu-id="2c42f-122">símbolo (token) de Hello, a continuación, puede ser hello toocall usa API de visión de Series de tiempo.</span><span class="sxs-lookup"><span data-stu-id="2c42f-122">hello token can then be used toocall hello Time Series Insights API.</span></span>

<span data-ttu-id="2c42f-123">Estos son los pasos detallados de Hola:</span><span class="sxs-lookup"><span data-stu-id="2c42f-123">Here are hello detailed steps:</span></span>

1. <span data-ttu-id="2c42f-124">Hola portal de Azure, seleccione **Azure Active Directory** > **registros de aplicaciones** > **nuevo registro de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="2c42f-124">In hello Azure portal, select **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

   ![Nuevo registro de aplicaciones en Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. <span data-ttu-id="2c42f-126">Asigne aplicación hello un toobe del tipo de nombre, seleccione hello **aplicación Web / API**, seleccione cualquier URI válido para **dirección URL de inicio de sesión**y haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="2c42f-126">Give hello application a name, select hello type toobe **Web app / API**, select any valid URI for **Sign-on URL**, and click **Create**.</span></span>

   ![Crear aplicación hello en Azure Active Directory](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. <span data-ttu-id="2c42f-128">Seleccione la aplicación recién creada y copie su editor de texto favorito de tooyour de Id. de aplicación.</span><span class="sxs-lookup"><span data-stu-id="2c42f-128">Select your newly created application and copy its application ID tooyour favorite text editor.</span></span>

   ![Copie el identificador de la aplicación hello](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. <span data-ttu-id="2c42f-130">Seleccione **claves**, escriba el nombre de clave de hello, expiración de hello seleccione y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="2c42f-130">Select **Keys**, enter hello key name, select hello expiration, and click **Save**.</span></span>

   ![Selección de las claves de aplicación](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Escriba el nombre de clave de Hola y de expiración y haga clic en Guardar](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. <span data-ttu-id="2c42f-133">Copiar clave tooyour de hello, editor de texto que prefiera.</span><span class="sxs-lookup"><span data-stu-id="2c42f-133">Copy hello key tooyour favorite text editor.</span></span>

   ![Copie la clave de la aplicación hello](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. <span data-ttu-id="2c42f-135">Para entorno de visión de la serie de tiempo de hello, seleccione **directivas de acceso de datos** y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="2c42f-135">For hello Time Series Insights environment, select **Data Access Policies** and click **Add**.</span></span>

   ![Agregar entorno de visión de la serie de tiempo de toohello directiva de acceso de datos nueva](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. <span data-ttu-id="2c42f-137">Hola **Seleccionar usuario** cuadro de diálogo, nombre de la aplicación hello pegar (del paso 2) o identificador de la aplicación (del paso 3).</span><span class="sxs-lookup"><span data-stu-id="2c42f-137">In hello **Select User** dialog box, paste hello application name (from step 2) or application ID (from step 3).</span></span>

   ![Buscar una aplicación en el cuadro de diálogo Seleccionar usuario Hola](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. <span data-ttu-id="2c42f-139">Rol de hello seleccione (**lector** para consultar los datos, **colaborador** para consultar los datos y cambiar los datos de referencia) y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2c42f-139">Select hello role (**Reader** for querying data, **Contributor** for querying data and changing reference data) and click **Ok**.</span></span>

   ![Selección de lector o colaborador en el cuadro de diálogo Seleccionar rol Hola](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. <span data-ttu-id="2c42f-141">Guardar directiva Hola haciendo clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2c42f-141">Save hello policy by clicking **Ok**.</span></span>

10. <span data-ttu-id="2c42f-142">Id. de aplicación de uso hello (del paso 3) y token de hello tooacquire clave (del paso 5) la aplicación en nombre de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="2c42f-142">Use hello application ID (from step 3) and application key (from step 5) tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="2c42f-143">Hello token, a continuación, se puede pasar en hello `Authorization` encabezado cuando las llamadas de aplicación Hola Hola API de visión de Series de tiempo.</span><span class="sxs-lookup"><span data-stu-id="2c42f-143">hello token can then be passed in hello `Authorization` header when hello application calls hello Time Series Insights API.</span></span>

    <span data-ttu-id="2c42f-144">Si está utilizando C#, puede usar Hola después código tooacquire Hola símbolo (token) en nombre de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="2c42f-144">If you're using C#, you can use hello following code tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="2c42f-145">Para obtener un ejemplo completo, vea [Consulta de datos mediante C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="2c42f-145">For a complete sample, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a><span data-ttu-id="2c42f-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2c42f-146">Next steps</span></span>

<span data-ttu-id="2c42f-147">Identificador de la aplicación de uso hello y clave en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2c42f-147">Use hello application ID and key in your application.</span></span> <span data-ttu-id="2c42f-148">Para el código de ejemplo que llama Hola tiempo serie visión API, consulte [consultar datos utilizando C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="2c42f-148">For sample code that calls hello Time Series Insights API, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="2c42f-149">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="2c42f-149">See also</span></span>

* <span data-ttu-id="2c42f-150">[API de consulta](/rest/api/time-series-insights/time-series-insights-reference-queryapi) de referencia de API de consulta completa Hola</span><span class="sxs-lookup"><span data-stu-id="2c42f-150">[Query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) for hello full Query API reference</span></span>
* [<span data-ttu-id="2c42f-151">Crear un servicio principal Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="2c42f-151">Create a service principal in hello Azure portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
