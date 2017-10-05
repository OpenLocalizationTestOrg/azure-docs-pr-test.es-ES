---
title: "Introducción a Azure Active Directory Identity Protection y Microsoft Graph | Microsoft Docs"
description: "Proporciona una introducción a la consulta de Microsoft Graph para obtener una lista de eventos de riesgo e información asociada desde Azure Active Directory."
services: active-directory
keywords: azure active directory identity protection, evento de riesgo, vulnerabilidad, directiva de seguridad, Microsoft Graph
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 9b01ff86da6a1fd4a439a6ba59ea15ed6480cdad
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="96aa1-104">Introducción a Azure Active Directory Identity Protection y Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="96aa1-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="96aa1-105">Microsoft Graph es el punto de conexión de API unificada de Microsoft y donde se encuentran las API de [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="96aa1-105">Microsoft Graph is the Microsoft unified API endpoint and the home of [Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="96aa1-106">La primera API, **identityRiskEvents**, le permite consultar una lista de Microsoft Graph de [eventos de riesgo](active-directory-identityprotection-risk-events-types.md) así como información asociada.</span><span class="sxs-lookup"><span data-stu-id="96aa1-106">The first API, **identityRiskEvents**, allows you to query Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="96aa1-107">Este artículo es una introducción a cómo consultar esta API.</span><span class="sxs-lookup"><span data-stu-id="96aa1-107">This article gets you started querying this API.</span></span> <span data-ttu-id="96aa1-108">Para una introducción más detallada, consulte la documentación completa y el acceso al explorador de Graph en [sitio web de Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="96aa1-108">For an in-depth introduction, full documentation, and access to the Graph Explorer, see the [Microsoft Graph site](https://graph.microsoft.io/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96aa1-109">Microsoft recomienda administrar Azure AD con el [Centro de administración de Azure AD](https://aad.portal.azure.com) en Azure Portal en lugar de usar el portal de Azure clásico al que se hace referencia en este artículo.</span><span class="sxs-lookup"><span data-stu-id="96aa1-109">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="96aa1-110">Hay tres pasos para acceder a los datos de Identity Protection a través de Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="96aa1-110">There are three steps to accessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="96aa1-111">Agregar una aplicación con un secreto de cliente.</span><span class="sxs-lookup"><span data-stu-id="96aa1-111">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="96aa1-112">Use este secreto y otro tipo de información para autenticarse en Microsoft Graph, donde recibirá un token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="96aa1-112">Use this secret and a few other pieces of information to authenticate to Microsoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="96aa1-113">Utilice este token para realizar solicitudes en el punto de conexión de API y obtener datos de Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="96aa1-113">Use this token to make requests to the API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="96aa1-114">Antes de comenzar, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="96aa1-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="96aa1-115">Privilegios de administrador para crear la aplicación en Azure AD</span><span class="sxs-lookup"><span data-stu-id="96aa1-115">Administrator privileges to create the application in Azure AD</span></span>
* <span data-ttu-id="96aa1-116">El nombre de dominio del inquilino (por ejemplo, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="96aa1-116">The name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="96aa1-117">Agregar una aplicación con un secreto de cliente</span><span class="sxs-lookup"><span data-stu-id="96aa1-117">Add an application with a client secret</span></span>
1. <span data-ttu-id="96aa1-118">[Inicie sesión](https://manage.windowsazure.com) como administrador en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="96aa1-118">[Sign in](https://manage.windowsazure.com) to your Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="96aa1-119">En el panel de navegación izquierdo,haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="96aa1-119">On on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="96aa1-121">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="96aa1-121">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
4. <span data-ttu-id="96aa1-122">En el menú superior, haga clic en **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="96aa1-122">In the menu on the top, click **Applications**.</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="96aa1-124">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="96aa1-124">Click **Add** at the bottom of the page.</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="96aa1-126">En la página de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación que mi organización está desarrollando**.</span><span class="sxs-lookup"><span data-stu-id="96aa1-126">On the **What do you want to do** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="96aa1-128">En la cuadro de diálogo **Proporcione información sobre este usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="96aa1-128">On the **Tell us about your application** dialog, perform the following steps:</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="96aa1-130">a.</span><span class="sxs-lookup"><span data-stu-id="96aa1-130">a.</span></span> <span data-ttu-id="96aa1-131">En el cuadro de texto **Nombre** , escriba un nombre para la aplicación (por ejemplo: aplicación de API de eventos de riesgo AADIP).</span><span class="sxs-lookup"><span data-stu-id="96aa1-131">In the **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="96aa1-132">b.</span><span class="sxs-lookup"><span data-stu-id="96aa1-132">b.</span></span> <span data-ttu-id="96aa1-133">Como **Tipo**, seleccione **Aplicación web y/o API web**.</span><span class="sxs-lookup"><span data-stu-id="96aa1-133">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="96aa1-134">c.</span><span class="sxs-lookup"><span data-stu-id="96aa1-134">c.</span></span> <span data-ttu-id="96aa1-135">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="96aa1-135">Click **Next**.</span></span>
8. <span data-ttu-id="96aa1-136">En el cuadro de diálogo **Agregar propiedades** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="96aa1-136">On the **App properties** dialog, perform the following steps:</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="96aa1-138">a.</span><span class="sxs-lookup"><span data-stu-id="96aa1-138">a.</span></span> <span data-ttu-id="96aa1-139">En el cuadro de texto **URL de inicio de sesión**, escriba `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="96aa1-139">In the **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="96aa1-140">b.</span><span class="sxs-lookup"><span data-stu-id="96aa1-140">b.</span></span> <span data-ttu-id="96aa1-141">En el cuadro de texto **URI de id. de aplicación**, escriba `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="96aa1-141">In the **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="96aa1-142">c.</span><span class="sxs-lookup"><span data-stu-id="96aa1-142">c.</span></span> <span data-ttu-id="96aa1-143">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="96aa1-143">Click **Complete**.</span></span>

<span data-ttu-id="96aa1-144">Ahora puede configurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="96aa1-144">Your can now configure your application.</span></span>

![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="96aa1-146">Conceder a la aplicación permiso para usar la API</span><span class="sxs-lookup"><span data-stu-id="96aa1-146">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="96aa1-147">En la página de la aplicación, en el menú de la parte superior, haga clic en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="96aa1-147">On your application's page, in the menu on the top, click **Configure**.</span></span> 
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="96aa1-149">En la sección **Permisos para otras aplicaciones**, haga clic en **Agregar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="96aa1-149">In the **permissions to other applications** section, click **Add application**.</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="96aa1-151">En el cuadro de diálogo **Permisos para otras aplicaciones** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="96aa1-151">On the **permissions to other applications** dialog, perform the following steps:</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="96aa1-153">a.</span><span class="sxs-lookup"><span data-stu-id="96aa1-153">a.</span></span> <span data-ttu-id="96aa1-154">Seleccione **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="96aa1-154">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="96aa1-155">b.</span><span class="sxs-lookup"><span data-stu-id="96aa1-155">b.</span></span> <span data-ttu-id="96aa1-156">Haga clic en **Complete**.</span><span class="sxs-lookup"><span data-stu-id="96aa1-156">Click **Complete**.</span></span>
4. <span data-ttu-id="96aa1-157">Haga clic en **Permisos de la aplicación: 0** y seleccione **Read all identity risk event information** (Leer toda la información de eventos de riesgo de identidad).</span><span class="sxs-lookup"><span data-stu-id="96aa1-157">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="96aa1-159">Haga clic en **Guardar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="96aa1-159">Click **Save** at the bottom of the page.</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="96aa1-161">Obtención de una clave de acceso</span><span class="sxs-lookup"><span data-stu-id="96aa1-161">Get an access key</span></span>
1. <span data-ttu-id="96aa1-162">En la página de la aplicación, en la sección de **claves** , seleccione 1 año como duración.</span><span class="sxs-lookup"><span data-stu-id="96aa1-162">On your application's page, in the **keys** section, select 1 year as duration.</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="96aa1-164">Haga clic en **Guardar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="96aa1-164">Click **Save** at the bottom of the page.</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="96aa1-166">En la sección de claves, copie el valor de la clave recién creada y péguelo en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="96aa1-166">in the keys section, copy the value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="96aa1-168">Si pierde esta clave, tendrá que volver a esta sección y crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="96aa1-168">If you lose this key, you will have to return to this section and create a new key.</span></span> <span data-ttu-id="96aa1-169">Guarde esta clave como un secreto: cualquier persona que la tenga accederá a sus datos.</span><span class="sxs-lookup"><span data-stu-id="96aa1-169">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="96aa1-170">En la sección **Propiedades**, copie el **identificador de cliente** y péguelo en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="96aa1-170">In the **properties** section, copy the **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-to-microsoft-graph-and-query-the-identity-risk-events-api"></a><span data-ttu-id="96aa1-171">Autenticación en Microsoft Graph y consulta a Identity Risk Events API</span><span class="sxs-lookup"><span data-stu-id="96aa1-171">Authenticate to Microsoft Graph and query the Identity Risk Events API</span></span>
<span data-ttu-id="96aa1-172">En este momento, debe tener:</span><span class="sxs-lookup"><span data-stu-id="96aa1-172">At this point, you should have:</span></span>

* <span data-ttu-id="96aa1-173">El identificador de cliente que copió anteriormente</span><span class="sxs-lookup"><span data-stu-id="96aa1-173">The client ID you copied above</span></span>
* <span data-ttu-id="96aa1-174">La clave que copió antes</span><span class="sxs-lookup"><span data-stu-id="96aa1-174">The key you copied above</span></span>
* <span data-ttu-id="96aa1-175">El nombre de dominio del inquilino</span><span class="sxs-lookup"><span data-stu-id="96aa1-175">The name of your tenant's domain</span></span>

<span data-ttu-id="96aa1-176">Para autenticarse, envíe una solicitud post a `https://login.microsoft.com` con los siguientes parámetros en el cuerpo:</span><span class="sxs-lookup"><span data-stu-id="96aa1-176">To authenticate, send a post request to `https://login.microsoft.com` with the following parameters in the body:</span></span>

* <span data-ttu-id="96aa1-177">grant_type: “**client_credentials**”</span><span class="sxs-lookup"><span data-stu-id="96aa1-177">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="96aa1-178">resource: “**https://graph.microsoft.com**”</span><span class="sxs-lookup"><span data-stu-id="96aa1-178">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="96aa1-179">client_id: <your client ID></span><span class="sxs-lookup"><span data-stu-id="96aa1-179">client_id: <your client ID></span></span>
* <span data-ttu-id="96aa1-180">client_secret: <your key></span><span class="sxs-lookup"><span data-stu-id="96aa1-180">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="96aa1-181">Debe proporcionar valores para los parámetros **client_id** y **client_secret**.</span><span class="sxs-lookup"><span data-stu-id="96aa1-181">You need to provide values for the **client_id** and the **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="96aa1-182">Si se realiza correctamente, devuelve un token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="96aa1-182">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="96aa1-183">Para llamar a la API, cree un encabezado con el parámetro siguiente:</span><span class="sxs-lookup"><span data-stu-id="96aa1-183">To call the API, create a header with the following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="96aa1-184">Al autenticar, puede encontrar el tipo de token y el token de acceso en el token devuelto.</span><span class="sxs-lookup"><span data-stu-id="96aa1-184">When authenticating, you can find the token type and access token in the returned token.</span></span>

<span data-ttu-id="96aa1-185">Envíe este encabezado como una solicitud a la siguiente dirección URL de la API: `https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="96aa1-185">Send this header as a request to the following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="96aa1-186">La respuesta, si se ha realizado correctamente, es una colección de eventos de riesgo de identidad y datos asociados en formato JSON de OData, que se pueden analizar y tratar como convenga.</span><span class="sxs-lookup"><span data-stu-id="96aa1-186">The response, if successful, is a collection of identity risk events and associated data in the OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="96aa1-187">Este es el código de ejemplo para autenticar y llamar a la API mediante Powershell.</span><span class="sxs-lookup"><span data-stu-id="96aa1-187">Here’s sample code for authenticating and calling the API using Powershell.</span></span>  
<span data-ttu-id="96aa1-188">Solo tiene que agregar el identificador de cliente, la clave y el dominio del inquilino.</span><span class="sxs-lookup"><span data-stu-id="96aa1-188">Just add your client ID, key, and tenant domain.</span></span>

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a><span data-ttu-id="96aa1-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="96aa1-189">Next steps</span></span>
<span data-ttu-id="96aa1-190">Enhorabuena, acaba de hacer la primera llamada a Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="96aa1-190">Congratulations, you just made your first call to Microsoft Graph!</span></span>  
<span data-ttu-id="96aa1-191">Ahora puede consultar los eventos de riesgo de identidad y utilizar los datos cuando lo estime necesario.</span><span class="sxs-lookup"><span data-stu-id="96aa1-191">Now you can query identity risk events and use the data however you see fit.</span></span>

<span data-ttu-id="96aa1-192">Para obtener más información sobre Microsoft Graph y cómo crear aplicaciones con la API Graph, consulte la [documentación](https://graph.microsoft.io/docs) y muchos más detalles en el [sitio web de Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="96aa1-192">To learn more about Microsoft Graph and how to build applications using the Graph API, check out the [documentation](https://graph.microsoft.io/docs) and much more on the [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="96aa1-193">Además, asegúrese de guardar en sus favoritos la página de las [API de Azure AD Identity Protection](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) , donde se enumeran todas las API de Identity Protection disponibles en Graph.</span><span class="sxs-lookup"><span data-stu-id="96aa1-193">Also, make sure to bookmark the [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of the Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="96aa1-194">A medida que se agreguen nuevas formas de trabajar con Identity Protection a través de la API, los verá en la página.</span><span class="sxs-lookup"><span data-stu-id="96aa1-194">As we add new ways to work with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="96aa1-195">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="96aa1-195">Additional resources</span></span>
* [<span data-ttu-id="96aa1-196">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="96aa1-196">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="96aa1-197">Types of risk events detected by Azure Active Directory Identity Protection (Tipos de eventos de riesgo que detecta Azure Active Directory Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="96aa1-197">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="96aa1-198">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="96aa1-198">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="96aa1-199">Overview of Microsoft Graph (Información general de Microsoft Graph)</span><span class="sxs-lookup"><span data-stu-id="96aa1-199">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="96aa1-200">Azure AD Identity Protection Service Root (Raíz del servicio de Azure AD Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="96aa1-200">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

