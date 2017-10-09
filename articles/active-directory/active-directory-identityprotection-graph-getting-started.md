---
title: aaaGet a trabajar con Azure Active Directory Identity Protection y Microsoft Graph | Documentos de Microsoft
description: "Proporciona un tooquery Introducción Microsoft Graph para obtener una lista de eventos de riesgos y la información asociada de Azure Active Directory."
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
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="17e71-104">Introducción a Azure Active Directory Identity Protection y Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="17e71-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="17e71-105">Microsoft Graph es Microsoft unified extremo de la API de Hola y Hola particular de [Azure Active Directory Identity Protection](active-directory-identityprotection.md) API.</span><span class="sxs-lookup"><span data-stu-id="17e71-105">Microsoft Graph is hello Microsoft unified API endpoint and hello home of [Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="17e71-106">Hola primera API, **identityRiskEvents**, permite tooquery Microsoft Graph para obtener una lista de [el riesgo de eventos](active-directory-identityprotection-risk-events-types.md) y la información asociada.</span><span class="sxs-lookup"><span data-stu-id="17e71-106">hello first API, **identityRiskEvents**, allows you tooquery Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="17e71-107">Este artículo es una introducción a cómo consultar esta API.</span><span class="sxs-lookup"><span data-stu-id="17e71-107">This article gets you started querying this API.</span></span> <span data-ttu-id="17e71-108">Para una introducción detallada, documentación completa y acceso toohello Explorador de gráficos, vea hello [sitio Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="17e71-108">For an in-depth introduction, full documentation, and access toohello Graph Explorer, see hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17e71-109">Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo.</span><span class="sxs-lookup"><span data-stu-id="17e71-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="17e71-110">Hay tres pasos tooaccessing identidad protección de datos a través de Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="17e71-110">There are three steps tooaccessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="17e71-111">Agregar una aplicación con un secreto de cliente.</span><span class="sxs-lookup"><span data-stu-id="17e71-111">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="17e71-112">Use este secreto y algunas otras partes de información tooauthenticate tooMicrosoft gráfico, que recibe un token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="17e71-112">Use this secret and a few other pieces of information tooauthenticate tooMicrosoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="17e71-113">Use este extremo de token toomake solicitudes toohello API y obtener datos de protección de identidad.</span><span class="sxs-lookup"><span data-stu-id="17e71-113">Use this token toomake requests toohello API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="17e71-114">Antes de comenzar, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="17e71-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="17e71-115">Aplicación de hello de toocreate de privilegios de administrador en Azure AD</span><span class="sxs-lookup"><span data-stu-id="17e71-115">Administrator privileges toocreate hello application in Azure AD</span></span>
* <span data-ttu-id="17e71-116">nombre de Hola de dominio de su inquilino (por ejemplo, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="17e71-116">hello name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="17e71-117">Agregar una aplicación con un secreto de cliente</span><span class="sxs-lookup"><span data-stu-id="17e71-117">Add an application with a client secret</span></span>
1. <span data-ttu-id="17e71-118">[Inicie sesión en](https://manage.windowsazure.com) tooyour portal de Azure clásico como administrador.</span><span class="sxs-lookup"><span data-stu-id="17e71-118">[Sign in](https://manage.windowsazure.com) tooyour Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="17e71-119">En el panel de navegación izquierdo de hello, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="17e71-119">On on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="17e71-121">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="17e71-121">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
4. <span data-ttu-id="17e71-122">En el menú de hello en la parte superior de hello, haga clic en **aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="17e71-122">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="17e71-124">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="17e71-124">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="17e71-126">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación que mi organización está desarrollando**.</span><span class="sxs-lookup"><span data-stu-id="17e71-126">On hello **What do you want toodo** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="17e71-128">En hello **envíenos comentarios acerca de la aplicación** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="17e71-128">On hello **Tell us about your application** dialog, perform hello following steps:</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="17e71-130">a.</span><span class="sxs-lookup"><span data-stu-id="17e71-130">a.</span></span> <span data-ttu-id="17e71-131">Hola **nombre** cuadro de texto, escriba un nombre para la aplicación (p. ej.: aplicación de API de eventos de riesgo AADIP).</span><span class="sxs-lookup"><span data-stu-id="17e71-131">In hello **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="17e71-132">b.</span><span class="sxs-lookup"><span data-stu-id="17e71-132">b.</span></span> <span data-ttu-id="17e71-133">Como **Tipo**, seleccione **Aplicación web y/o API web**.</span><span class="sxs-lookup"><span data-stu-id="17e71-133">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="17e71-134">c.</span><span class="sxs-lookup"><span data-stu-id="17e71-134">c.</span></span> <span data-ttu-id="17e71-135">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="17e71-135">Click **Next**.</span></span>
8. <span data-ttu-id="17e71-136">En hello **propiedades de la aplicación** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="17e71-136">On hello **App properties** dialog, perform hello following steps:</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="17e71-138">a.</span><span class="sxs-lookup"><span data-stu-id="17e71-138">a.</span></span> <span data-ttu-id="17e71-139">Hola **dirección URL de inicio de sesión** cuadro de texto, tipo `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="17e71-139">In hello **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="17e71-140">b.</span><span class="sxs-lookup"><span data-stu-id="17e71-140">b.</span></span> <span data-ttu-id="17e71-141">Hola **App ID URI** cuadro de texto, tipo `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="17e71-141">In hello **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="17e71-142">c.</span><span class="sxs-lookup"><span data-stu-id="17e71-142">c.</span></span> <span data-ttu-id="17e71-143">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="17e71-143">Click **Complete**.</span></span>

<span data-ttu-id="17e71-144">Ahora puede configurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="17e71-144">Your can now configure your application.</span></span>

![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="17e71-146">Conceder su hello toouse de permiso de aplicación API</span><span class="sxs-lookup"><span data-stu-id="17e71-146">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="17e71-147">En la página de la aplicación, en el menú de hello en la parte superior de hello, haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="17e71-147">On your application's page, in hello menu on hello top, click **Configure**.</span></span> 
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="17e71-149">Hola **permisos tooother aplicaciones** sección, haga clic en **Agregar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="17e71-149">In hello **permissions tooother applications** section, click **Add application**.</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="17e71-151">En hello **permisos tooother aplicaciones** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="17e71-151">On hello **permissions tooother applications** dialog, perform hello following steps:</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="17e71-153">a.</span><span class="sxs-lookup"><span data-stu-id="17e71-153">a.</span></span> <span data-ttu-id="17e71-154">Seleccione **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="17e71-154">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="17e71-155">b.</span><span class="sxs-lookup"><span data-stu-id="17e71-155">b.</span></span> <span data-ttu-id="17e71-156">Haga clic en **Complete**.</span><span class="sxs-lookup"><span data-stu-id="17e71-156">Click **Complete**.</span></span>
4. <span data-ttu-id="17e71-157">Haga clic en **Permisos de la aplicación: 0** y seleccione **Read all identity risk event information** (Leer toda la información de eventos de riesgo de identidad).</span><span class="sxs-lookup"><span data-stu-id="17e71-157">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="17e71-159">Haga clic en **guardar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="17e71-159">Click **Save** at hello bottom of hello page.</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="17e71-161">Obtención de una clave de acceso</span><span class="sxs-lookup"><span data-stu-id="17e71-161">Get an access key</span></span>
1. <span data-ttu-id="17e71-162">En la página de su aplicación, en hello **claves** sección, seleccione 1 año como duración.</span><span class="sxs-lookup"><span data-stu-id="17e71-162">On your application's page, in hello **keys** section, select 1 year as duration.</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="17e71-164">Haga clic en **guardar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="17e71-164">Click **Save** at hello bottom of hello page.</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="17e71-166">en la sección de claves de hello, Copiar valor de saludo de la clave recién creada y, a continuación, péguelo en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="17e71-166">in hello keys section, copy hello value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="17e71-168">Si pierde esta clave, tendrá tooreturn toothis sección y cree una nueva clave.</span><span class="sxs-lookup"><span data-stu-id="17e71-168">If you lose this key, you will have tooreturn toothis section and create a new key.</span></span> <span data-ttu-id="17e71-169">Guarde esta clave como un secreto: cualquier persona que la tenga accederá a sus datos.</span><span class="sxs-lookup"><span data-stu-id="17e71-169">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="17e71-170">Hola **propiedades** Hola de copia, en una sección **Id. de cliente**y, a continuación, péguelo en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="17e71-170">In hello **properties** section, copy hello **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a><span data-ttu-id="17e71-171">Autenticar hello de consulta API de eventos de riesgo de identidad y tooMicrosoft gráfico</span><span class="sxs-lookup"><span data-stu-id="17e71-171">Authenticate tooMicrosoft Graph and query hello Identity Risk Events API</span></span>
<span data-ttu-id="17e71-172">En este momento, debe tener:</span><span class="sxs-lookup"><span data-stu-id="17e71-172">At this point, you should have:</span></span>

* <span data-ttu-id="17e71-173">Id. de cliente de Hola que copió anteriormente</span><span class="sxs-lookup"><span data-stu-id="17e71-173">hello client ID you copied above</span></span>
* <span data-ttu-id="17e71-174">clave de Hola que copió anteriormente</span><span class="sxs-lookup"><span data-stu-id="17e71-174">hello key you copied above</span></span>
* <span data-ttu-id="17e71-175">nombre de Hola de dominio de su inquilino</span><span class="sxs-lookup"><span data-stu-id="17e71-175">hello name of your tenant's domain</span></span>

<span data-ttu-id="17e71-176">tooauthenticate, enviar una entrada de solicitud demasiado`https://login.microsoft.com` con hello parámetros en el cuerpo de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="17e71-176">tooauthenticate, send a post request too`https://login.microsoft.com` with hello following parameters in hello body:</span></span>

* <span data-ttu-id="17e71-177">grant_type: “**client_credentials**”</span><span class="sxs-lookup"><span data-stu-id="17e71-177">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="17e71-178">resource: “**https://graph.microsoft.com**”</span><span class="sxs-lookup"><span data-stu-id="17e71-178">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="17e71-179">client_id: <your client ID></span><span class="sxs-lookup"><span data-stu-id="17e71-179">client_id: <your client ID></span></span>
* <span data-ttu-id="17e71-180">client_secret: <your key></span><span class="sxs-lookup"><span data-stu-id="17e71-180">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="17e71-181">Necesita tooprovide valores para hello **client_id** hello y **client_secret** parámetro.</span><span class="sxs-lookup"><span data-stu-id="17e71-181">You need tooprovide values for hello **client_id** and hello **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="17e71-182">Si se realiza correctamente, devuelve un token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="17e71-182">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="17e71-183">Hola toocall API, cree un encabezado con hello después de parámetro:</span><span class="sxs-lookup"><span data-stu-id="17e71-183">toocall hello API, create a header with hello following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="17e71-184">Al autenticar, puede encontrar el tipo de token Hola y el token de acceso en hello devolvió el token.</span><span class="sxs-lookup"><span data-stu-id="17e71-184">When authenticating, you can find hello token type and access token in hello returned token.</span></span>

<span data-ttu-id="17e71-185">Enviar este encabezado como un toohello de solicitud después de la dirección URL de API:`https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="17e71-185">Send this header as a request toohello following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="17e71-186">respuesta de Hello, si es correcto, es una colección de identidad eventos de riesgo y datos en formato JSON de OData, que se pueden analizar y controlar como considere oportuno Hola asociados.</span><span class="sxs-lookup"><span data-stu-id="17e71-186">hello response, if successful, is a collection of identity risk events and associated data in hello OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="17e71-187">Este es el código de ejemplo para autenticar y llamar a API de hello mediante Powershell.</span><span class="sxs-lookup"><span data-stu-id="17e71-187">Here’s sample code for authenticating and calling hello API using Powershell.</span></span>  
<span data-ttu-id="17e71-188">Solo tiene que agregar el identificador de cliente, la clave y el dominio del inquilino.</span><span class="sxs-lookup"><span data-stu-id="17e71-188">Just add your client ID, key, and tenant domain.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="17e71-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="17e71-189">Next steps</span></span>
<span data-ttu-id="17e71-190">Enhorabuena, que acaba de crear su primer tooMicrosoft de llamada Graph.</span><span class="sxs-lookup"><span data-stu-id="17e71-190">Congratulations, you just made your first call tooMicrosoft Graph!</span></span>  
<span data-ttu-id="17e71-191">Ahora puede consultar los eventos de riesgo de identidad y usar datos de hello le convenga.</span><span class="sxs-lookup"><span data-stu-id="17e71-191">Now you can query identity risk events and use hello data however you see fit.</span></span>

<span data-ttu-id="17e71-192">toolearn más información acerca de Microsoft Graph y cómo las aplicaciones que toobuild usan Hola API Graph, visite hello [documentación](https://graph.microsoft.io/docs) y mucho más en hello [sitio Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="17e71-192">toolearn more about Microsoft Graph and how toobuild applications using hello Graph API, check out hello [documentation](https://graph.microsoft.io/docs) and much more on hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="17e71-193">Además, asegúrese de que hello toobookmark [API de protección de Azure AD Identity](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) página que enumera la lista de hello las API de protección de identidad disponible en el gráfico.</span><span class="sxs-lookup"><span data-stu-id="17e71-193">Also, make sure toobookmark hello [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of hello Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="17e71-194">Cuando se agrega toowork de maneras nuevas con protección de identidad a través de API, los verá en la página.</span><span class="sxs-lookup"><span data-stu-id="17e71-194">As we add new ways toowork with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="17e71-195">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="17e71-195">Additional resources</span></span>
* [<span data-ttu-id="17e71-196">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="17e71-196">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="17e71-197">Types of risk events detected by Azure Active Directory Identity Protection (Tipos de eventos de riesgo que detecta Azure Active Directory Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="17e71-197">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="17e71-198">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="17e71-198">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="17e71-199">Overview of Microsoft Graph (Información general de Microsoft Graph)</span><span class="sxs-lookup"><span data-stu-id="17e71-199">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="17e71-200">Azure AD Identity Protection Service Root (Raíz del servicio de Azure AD Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="17e71-200">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

