---
title: "llamar a aaaDeploy y autenticar las API web y las API de REST para las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: Implemente, autentique y llame a API web y API de REST en flujos de trabajo para integraciones de sistemas con Azure Logic Apps
keywords: API web, API de REST, conectores, flujos de trabajo, integraciones de sistemas, autenticar
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="66e98-104">Implementación, llamada y autenticación de API personalizadas como conectores para aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="66e98-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="66e98-105">Después de [crear API personalizadas](./logic-apps-create-api-app.md) que proporcione toouse acciones o desencadenadores en la lógica de flujos de trabajo de aplicaciones, debe implementar las API antes de que se pueden llamar.</span><span class="sxs-lookup"><span data-stu-id="66e98-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers toouse in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="66e98-106">Y aunque se puede llamar a cualquier API desde una aplicación de la lógica para la mejor experiencia de hello, agregue [Swagger metadatos](http://swagger.io/specification/) que describe las operaciones y los parámetros de la API.</span><span class="sxs-lookup"><span data-stu-id="66e98-106">And although you can call any API from a logic app, for hello best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="66e98-107">Este archivo de Swagger ayuda a que su API funcione mejor y se integre con más facilidad con aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="66e98-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="66e98-108">Puede implementar las API como [aplicaciones web](../app-service-web/app-service-web-overview.md), pero considere la posibilidad de implementar las API como [aplicaciones de API](../app-service-api/app-service-api-apps-why-best-platform.md), que puede facilitar su trabajo al compilar, hospedar y utilizar las API en la nube de Hola y de forma local.</span><span class="sxs-lookup"><span data-stu-id="66e98-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in hello cloud and on premises.</span></span> <span data-ttu-id="66e98-109">No tienes toochange cualquier código en las API, implemente la aplicación de API de código tooan.</span><span class="sxs-lookup"><span data-stu-id="66e98-109">You don't have toochange any code in your APIs -- just deploy your code tooan API app.</span></span> <span data-ttu-id="66e98-110">Puede hospedar las API en [servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md), un plataforma como-servicio (PaaS) de la oferta que proporciona una de las maneras de mejor, más fáciles y más escalables de hello para la API de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="66e98-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of hello best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="66e98-111">tooauthenticate las llamadas de lógica aplicaciones tooyour API, puede configurar Active Directory de Azure en hello portal de Azure para que no tenga tooupdate el código.</span><span class="sxs-lookup"><span data-stu-id="66e98-111">tooauthenticate calls from logic apps tooyour APIs, you can set up Azure Active Directory in hello Azure portal so you don't have tooupdate your code.</span></span> <span data-ttu-id="66e98-112">También puede requerir y aplicar la autenticación a través del código de la API.</span><span class="sxs-lookup"><span data-stu-id="66e98-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="66e98-113">Implementación de la API como aplicación web o aplicación de API</span><span class="sxs-lookup"><span data-stu-id="66e98-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="66e98-114">Para poder invocar la API personalizada desde una aplicación de lógica, implementar la API como una aplicación web o aplicación de API tooAzure servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="66e98-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app tooAzure App Service.</span></span> <span data-ttu-id="66e98-115">Además, la toomake el documento de Swagger legible por hello diseñador la lógica de aplicación, establecer las propiedades de definición de API de Hola y activar [recursos entre orígenes (CORS) de uso compartido](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) para su aplicación web o aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="66e98-115">Also, toomake your Swagger document readable by hello Logic App Designer, set hello API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="66e98-116">Hola portal de Azure, seleccione la aplicación web o una aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="66e98-116">In hello Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="66e98-117">En la hoja de Hola que se abre, en **API**, elija **definición de la API**.</span><span class="sxs-lookup"><span data-stu-id="66e98-117">In hello blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="66e98-118">Conjunto hello **ubicación de la definición de API** toohello URL para el archivo swagger.json.</span><span class="sxs-lookup"><span data-stu-id="66e98-118">Set hello **API definition location** toohello URL for your swagger.json file.</span></span>

   <span data-ttu-id="66e98-119">Por lo general, dirección URL de hello aparece en este formato:`https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="66e98-119">Usually, hello URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![Archivo de vínculo de tooSwagger de la API personalizada](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="66e98-121">En **API**, elija **CORS**.</span><span class="sxs-lookup"><span data-stu-id="66e98-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="66e98-122">Establecer una directiva CORS de Hola para **permite orígenes** demasiado**'*'** (permitir todo).</span><span class="sxs-lookup"><span data-stu-id="66e98-122">Set hello CORS policy for **Allowed origins** too**'*'** (allow all).</span></span>

   <span data-ttu-id="66e98-123">Esta configuración permite solicitudes del Diseñador de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="66e98-123">This setting permits requests from Logic App Designer.</span></span>

   ![Permitir solicitudes de API de diseñador de la aplicación lógica tooyour personalizada](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="66e98-125">Para obtener más información, consulte estos artículos:</span><span class="sxs-lookup"><span data-stu-id="66e98-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="66e98-126">Incorporación de metadatos de Swagger para las API web de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="66e98-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="66e98-127">Implementar ASP.NET web API tooAzure servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="66e98-127">Deploy ASP.NET web APIs tooAzure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="66e98-128">Llamada a la API personalizada desde flujos de trabajo de aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="66e98-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="66e98-129">Después de configurar las propiedades de definición de API de Hola y CORS, los desencadenadores y las acciones de la API personalizada deben estar disponibles para tooinclude en el flujo de trabajo de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="66e98-129">After you set up hello API definition properties and CORS, your custom API's triggers and actions should become available for you tooinclude in your logic app workflow.</span></span> 

*  <span data-ttu-id="66e98-130">tooview sitios Web de Hola que tiene direcciones URL de Swagger, puede examinar los sitios Web de suscripción en hello lógica el Diseñador de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="66e98-130">tooview hello websites that have Swagger URLs, you can browse your subscription websites in hello Logic Apps Designer.</span></span>

*  <span data-ttu-id="66e98-131">acciones disponibles tooview y entradas, que señala a un documento de Swagger usar hello [HTTP + Swagger acción](../connectors/connectors-native-http-swagger.md).</span><span class="sxs-lookup"><span data-stu-id="66e98-131">tooview available actions and inputs by pointing at a Swagger document, use hello [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="66e98-132">toocall cualquier API, incluidas las API que no tengan o exponer un documento de Swagger, siempre puede crear una solicitud con hello [acción HTTP](../connectors/connectors-native-http.md).</span><span class="sxs-lookup"><span data-stu-id="66e98-132">toocall any API, including APIs that don't have or expose a Swagger document, you can always create a request with hello [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-tooyour-custom-api"></a><span data-ttu-id="66e98-133">Autenticar la API personalizada de llamadas tooyour</span><span class="sxs-lookup"><span data-stu-id="66e98-133">Authenticate calls tooyour custom API</span></span>

<span data-ttu-id="66e98-134">Puede proteger las llamadas tooyour API personalizada de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="66e98-134">You can secure calls tooyour custom API in these ways:</span></span>

* <span data-ttu-id="66e98-135">[Ningún cambio de código](#no-code): proteger su API con [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) a través de hello portal de Azure, por lo que no dispone de tooupdate el código o volver a implementar la API.</span><span class="sxs-lookup"><span data-stu-id="66e98-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through hello Azure portal, so you don't have tooupdate your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="66e98-136">De forma predeterminada, la autenticación de Azure AD de hello activar Hola portal de Azure no proporciona autorización específica.</span><span class="sxs-lookup"><span data-stu-id="66e98-136">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="66e98-137">Por ejemplo, esta autenticación bloquea su toojust API una específicos del inquilino, no tooa un usuario específico o una aplicación.</span><span class="sxs-lookup"><span data-stu-id="66e98-137">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

* <span data-ttu-id="66e98-138">[Actualice el código de la API](#update-code): proteja su API aplicando la [autenticación de certificado](#certificate), la [autenticación básica](#basic) o la [autenticación de Azure AD](#azure-ad-code) mediante código.</span><span class="sxs-lookup"><span data-stu-id="66e98-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a><span data-ttu-id="66e98-139">Autenticar las llamadas API de tooyour sin cambiar el código</span><span class="sxs-lookup"><span data-stu-id="66e98-139">Authenticate calls tooyour API without changing code</span></span>

<span data-ttu-id="66e98-140">Aquí es pasos generales de Hola para este método:</span><span class="sxs-lookup"><span data-stu-id="66e98-140">Here's hello general steps for this method:</span></span>

1. <span data-ttu-id="66e98-141">Cree dos [identidades de aplicación de Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md): una para la aplicación lógica y otra para la aplicación web (o aplicación de API).</span><span class="sxs-lookup"><span data-stu-id="66e98-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="66e98-142">tooauthenticate tooyour de llamadas API, utilice credenciales de hello (Id. de cliente y secreto) para hello [entidad de servicio](../app-service-api/app-service-api-dotnet-service-principal-auth.md) que tiene asociados con hello identidad de aplicación de Azure AD para la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="66e98-142">tooauthenticate calls tooyour API, use hello credentials (client ID and secret) for hello [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with hello Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="66e98-143">Incluir identificadores de aplicaciones de hello en la definición de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="66e98-143">Include hello application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="66e98-144">Parte 1: Creación de una identidad de aplicación de Azure AD para la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="66e98-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="66e98-145">La aplicación lógica usa este tooauthenticate de identidad de aplicación de Azure AD en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66e98-145">Your logic app uses this Azure AD application identity tooauthenticate against Azure AD.</span></span> <span data-ttu-id="66e98-146">Solo tiene tooset esta identidad de una vez para su directorio.</span><span class="sxs-lookup"><span data-stu-id="66e98-146">You only have tooset up this identity one time for your directory.</span></span> <span data-ttu-id="66e98-147">Por ejemplo, puede elegir toouse Hola misma identidad para todas las aplicaciones lógicas, aunque puede crear identidades únicas para cada aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="66e98-147">For example, you can choose toouse hello same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="66e98-148">Puede configurar estas identidades en el portal de Azure, hello [portal de Azure clásico](#app-identity-logic-classic), o use [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="66e98-148">You can set up these identities in hello Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="66e98-149">**Crear la identidad de aplicación de hello para la aplicación lógica en hello portal de Azure**</span><span class="sxs-lookup"><span data-stu-id="66e98-149">**Create hello application identity for your logic app in hello Azure portal**</span></span>

1. <span data-ttu-id="66e98-150">Hola [portal de Azure](https://portal.azure.com "https://portal.azure.com"), elija **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="66e98-150">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="66e98-151">Confirme que se encuentra en hello mismo directorio que la aplicación web o una aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="66e98-151">Confirm that you're in hello same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="66e98-152">directorios de tooswitch, haga clic en el perfil y seleccionar otro directorio.</span><span class="sxs-lookup"><span data-stu-id="66e98-152">tooswitch directories, click your profile and select another directory.</span></span> <span data-ttu-id="66e98-153">O bien, elija **Información general** > **Cambiar directorio**.</span><span class="sxs-lookup"><span data-stu-id="66e98-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="66e98-154">En el menú de directorio de hello, en **administrar**, elija **registros de aplicaciones** > **nuevo registro de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="66e98-154">On hello directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="66e98-155">De forma predeterminada, lista de registros de aplicaciones de hello muestra todos los registros de aplicación en el directorio.</span><span class="sxs-lookup"><span data-stu-id="66e98-155">By default, hello app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="66e98-156">tooview sólo los registros de aplicación, cuadro de búsqueda de toohello siguiente, seleccione **mis aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="66e98-156">tooview only your app registrations, next toohello search box, select **My apps**.</span></span> 

   ![Crear registro de aplicaciones](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="66e98-158">Asigne un nombre a la identidad de aplicación, deje **tipo de aplicación** establecido demasiado**aplicación Web / API**, proporcionar una única cadena con formato como un dominio para **dirección URL de inicio de sesión**y elija  **Crear**.</span><span class="sxs-lookup"><span data-stu-id="66e98-158">Give your application identity a name, leave **Application type** set too**Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![Proporcionar un nombre y una dirección URL de inicio de sesión para la identidad de aplicación](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="66e98-160">identidad de aplicación Hola que creó para la aplicación lógica ahora aparece en la lista de registros de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="66e98-160">hello application identity that you created for your logic app now appears in hello app registrations list.</span></span>

   ![Identidad de aplicación para la aplicación lógica](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="66e98-162">En la lista de registros de aplicaciones de hello, seleccione la nueva identidad de aplicación.</span><span class="sxs-lookup"><span data-stu-id="66e98-162">In hello app registrations list, select your new application identity.</span></span> <span data-ttu-id="66e98-163">Copie y guarde hello **Id. de aplicación** toouse como Hola "Id. de cliente" de la aplicación lógica en la parte 3.</span><span class="sxs-lookup"><span data-stu-id="66e98-163">Copy and save hello **Application ID** toouse as hello "client ID" for your logic app in Part 3.</span></span>

   ![Copiar y guardar el identificador de aplicación para la aplicación lógica](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="66e98-165">Si la configuración de la identidad de aplicación no está visible, elija **Configuración** o **Toda la configuración**.</span><span class="sxs-lookup"><span data-stu-id="66e98-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="66e98-166">En **Acceso de API**, elija **Claves**.</span><span class="sxs-lookup"><span data-stu-id="66e98-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="66e98-167">En **Descripción**, proporcione un nombre para la clave.</span><span class="sxs-lookup"><span data-stu-id="66e98-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="66e98-168">En **Expira**, seleccione una duración para la clave.</span><span class="sxs-lookup"><span data-stu-id="66e98-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="66e98-169">clave de Hola que va a crear actúa como de la identidad de aplicación de Hola "secreto" o la contraseña para la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="66e98-169">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

   ![Crear clave para la identidad de aplicación lógica](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="66e98-171">En la barra de herramientas de hello, elija **guardar**.</span><span class="sxs-lookup"><span data-stu-id="66e98-171">On hello toolbar, choose **Save**.</span></span> <span data-ttu-id="66e98-172">En **Valor**, ahora aparece su clave.</span><span class="sxs-lookup"><span data-stu-id="66e98-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="66e98-173">**Asegúrese de toocopy seguro y guardar la clave de** para su uso posterior porque la clave de hello está oculto cuando sale de hoja clave Hola.</span><span class="sxs-lookup"><span data-stu-id="66e98-173">**Make sure toocopy and save your key** for later use because hello key is hidden when you leave hello key blade.</span></span>

   <span data-ttu-id="66e98-174">Cuando se configura la aplicación lógica en la parte 3, especifique esta clave como Hola "secreto" o la contraseña.</span><span class="sxs-lookup"><span data-stu-id="66e98-174">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

   ![Copiar y guardar la clave para más tarde](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="66e98-176">**Crear la identidad de aplicación de hello para la aplicación lógica en hello portal de Azure clásico**</span><span class="sxs-lookup"><span data-stu-id="66e98-176">**Create hello application identity for your logic app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="66e98-177">En el portal de Azure clásico de Hola, elija [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="66e98-177">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="66e98-178">Seleccione Hola mismo directorio que se use para la aplicación web o una aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="66e98-178">Select hello same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="66e98-179">En hello **aplicaciones** ficha, elija **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="66e98-179">On hello **Applications** tab, choose **Add** at hello bottom of hello page.</span></span>

4. <span data-ttu-id="66e98-180">Asigne un nombre a la identidad de aplicación y elija **Siguiente** (flecha derecha).</span><span class="sxs-lookup"><span data-stu-id="66e98-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="66e98-181">En **Propiedades de la aplicación**, proporcione una cadena única con formato de dominio para **Dirección URL de inicio de sesión** y **URI de id. de aplicación**, y elija **Completar** (marca de verificación).</span><span class="sxs-lookup"><span data-stu-id="66e98-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="66e98-182">En hello **configurar** ficha, copiar y guardar hello **Id. de cliente** para su toouse de aplicación lógica en la parte 3.</span><span class="sxs-lookup"><span data-stu-id="66e98-182">On hello **Configure** tab, copy and save hello **Client ID** for your logic app toouse in Part 3.</span></span>

7. <span data-ttu-id="66e98-183">En **claves**, abra hello **seleccione duración** lista.</span><span class="sxs-lookup"><span data-stu-id="66e98-183">Under **Keys**, open hello **Select duration** list.</span></span> <span data-ttu-id="66e98-184">Seleccione una duración para la clave.</span><span class="sxs-lookup"><span data-stu-id="66e98-184">Select a duration for your key.</span></span>

   <span data-ttu-id="66e98-185">clave de Hola que va a crear actúa como de la identidad de aplicación de Hola "secreto" o la contraseña para la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="66e98-185">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="66e98-186">En hello parte inferior de la página de hello, elija **guardar**.</span><span class="sxs-lookup"><span data-stu-id="66e98-186">At hello bottom of hello page, choose **Save**.</span></span> <span data-ttu-id="66e98-187">Es posible que tenga toowait unos segundos.</span><span class="sxs-lookup"><span data-stu-id="66e98-187">You might have toowait a few seconds.</span></span>

9. <span data-ttu-id="66e98-188">En **claves**, realice toocopy seguro y Guardar clave de Hola que aparece ahora.</span><span class="sxs-lookup"><span data-stu-id="66e98-188">Under **Keys**, make sure toocopy and save hello key that now appears.</span></span> 

   <span data-ttu-id="66e98-189">Cuando se configura la aplicación lógica en la parte 3, especifique esta clave como Hola "secreto" o la contraseña.</span><span class="sxs-lookup"><span data-stu-id="66e98-189">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

<span data-ttu-id="66e98-190">Para obtener más información, obtenga información acerca de cómo demasiado [configurar el inicio de sesión de Azure Active Directory de servicio de aplicaciones aplicación toouse](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="66e98-190">For more information, learn how too [configure your App Service application toouse Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="66e98-191">**Crear la identidad de aplicación de hello para la aplicación lógica en PowerShell**</span><span class="sxs-lookup"><span data-stu-id="66e98-191">**Create hello application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="66e98-192">Puede realizar esta tarea mediante Azure Resource Manager con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66e98-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="66e98-193">En PowerShell, ejecute estos comandos:</span><span class="sxs-lookup"><span data-stu-id="66e98-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="66e98-194">Realizar seguro hello toocopy **Id. de inquilino** Hola (GUID para el inquilino de Azure AD), **Id. de aplicación**y la contraseña de Hola que ha usado.</span><span class="sxs-lookup"><span data-stu-id="66e98-194">Make sure toocopy hello **Tenant ID** (GUID for your Azure AD tenant), hello **Application ID**, and hello password that you used.</span></span>

<span data-ttu-id="66e98-195">Para obtener más información, obtenga información acerca de cómo demasiado [crear una entidad de servicio con PowerShell tooaccess recursos](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="66e98-195">For more information, learn how too [create a service principal with PowerShell tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="66e98-196">Parte 2: Creación de una identidad de aplicación de Azure AD para la aplicación web o de API</span><span class="sxs-lookup"><span data-stu-id="66e98-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="66e98-197">Si ya se ha implementado la aplicación web o una aplicación de API, puede activar la autenticación y crear identidad de aplicación Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="66e98-197">If your web app or API app is already deployed, you can turn on authentication and create hello application identity in hello Azure portal.</span></span> <span data-ttu-id="66e98-198">En caso contrario, puede [activar la autenticación cuando implemente con una plantilla de Azure Resource Manager](#authen-deploy).</span><span class="sxs-lookup"><span data-stu-id="66e98-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="66e98-199">**Crear la identidad de aplicación hello y activar la autenticación en el portal de Azure para aplicaciones implementadas de Hola**</span><span class="sxs-lookup"><span data-stu-id="66e98-199">**Create hello application identity and turn on authentication in hello Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="66e98-200">Hola [portal de Azure](https://portal.azure.com "https://portal.azure.com"), busque y seleccione la aplicación web o una aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="66e98-200">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="66e98-201">Haga clic en **Configuración** y elija **Autenticación/autorización**.</span><span class="sxs-lookup"><span data-stu-id="66e98-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="66e98-202">En **Autenticación de App Service**, elija **Activar** la autenticación.</span><span class="sxs-lookup"><span data-stu-id="66e98-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="66e98-203">En **Proveedores de autenticación**, elija **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="66e98-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![Activar la autenticación](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="66e98-205">Ahora cree una identidad de aplicación para la aplicación web o de API como se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="66e98-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="66e98-206">En hello **configuración de Azure Active Directory** hoja, establezca **modo de administración** demasiado**Express**.</span><span class="sxs-lookup"><span data-stu-id="66e98-206">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Express**.</span></span> <span data-ttu-id="66e98-207">Elija **Crear nueva aplicación de AD**.</span><span class="sxs-lookup"><span data-stu-id="66e98-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="66e98-208">Asigne un nombre a la identidad de aplicación y elija **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="66e98-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![Crear una identidad de aplicación para la aplicación web o de API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="66e98-210">En hello **autenticación / hoja de autorización**, elija **guardar**.</span><span class="sxs-lookup"><span data-stu-id="66e98-210">On hello **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="66e98-211">Ahora debe buscar Id. de cliente de Hola e Id. de inquilino para identidad de aplicación Hola que esté asociada con la aplicación web o una aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="66e98-211">Now you must find hello client ID and tenant ID for hello application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="66e98-212">Ha usado estos identificadores en la parte 3.</span><span class="sxs-lookup"><span data-stu-id="66e98-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="66e98-213">Por tanto, continúe con estos pasos para el portal de Azure de Hola o [portal de Azure clásico](#find-id-classic).</span><span class="sxs-lookup"><span data-stu-id="66e98-213">So continue with these steps for hello Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="66e98-214">**Encuentra el Id. de cliente de la identidad de aplicación y el identificador de inquilinos para su aplicación web o API en hello portal de Azure**</span><span class="sxs-lookup"><span data-stu-id="66e98-214">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure portal**</span></span>

1. <span data-ttu-id="66e98-215">En **Proveedores de autenticación**, elija **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="66e98-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   ![Elegir "Azure Active Directory"](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="66e98-217">En hello **configuración de Azure Active Directory** hoja, establezca **modo de administración** demasiado**avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="66e98-217">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Advanced**.</span></span>

3. <span data-ttu-id="66e98-218">Hola copia **Id. de cliente**y guardar dicho GUID para su uso en la parte 3.</span><span class="sxs-lookup"><span data-stu-id="66e98-218">Copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="66e98-219">Si **Id. de cliente** y **dirección Url del emisor** no aparecen, pruebe a actualizar Hola portal de Azure y repita el paso 1.</span><span class="sxs-lookup"><span data-stu-id="66e98-219">If **Client ID** and **Issuer Url** don't appear, try refreshing hello Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="66e98-220">En **dirección Url del emisor**, copiar y guardar solo Hola parte 3 como GUID.</span><span class="sxs-lookup"><span data-stu-id="66e98-220">Under **Issuer Url**, copy and save just hello GUID for Part 3.</span></span> <span data-ttu-id="66e98-221">También puede usar este GUID en la plantilla de implementación de su aplicación web o de API, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="66e98-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="66e98-222">Este GUID es para su inquilino específico ("Identificador de inquilino") y debería aparecer en esta dirección URL: `https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="66e98-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="66e98-223">Sin guardar los cambios, cierre hello **configuración de Azure Active Directory** hoja.</span><span class="sxs-lookup"><span data-stu-id="66e98-223">Without saving your changes, close hello **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="66e98-224">**Encuentra el Id. de cliente de la identidad de aplicación y el Id. de inquilinos para su aplicación web o API en hello portal de Azure clásico**</span><span class="sxs-lookup"><span data-stu-id="66e98-224">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="66e98-225">En el portal de Azure clásico de Hola, elija [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="66e98-225">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="66e98-226">Seleccione el directorio de Hola que usas para su aplicación web o aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="66e98-226">Select hello directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="66e98-227">Hola **búsqueda** cuadro, busque y seleccione la identidad de aplicación Hola para su aplicación web o aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="66e98-227">In hello **Search** box, find and select hello application identity for your web app or API app.</span></span>

4. <span data-ttu-id="66e98-228">En hello **configurar** ficha, Hola copia **Id. de cliente**y guardar dicho GUID para su uso en la parte 3.</span><span class="sxs-lookup"><span data-stu-id="66e98-228">On hello **Configure** tab, copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="66e98-229">Después de obtener Id. de cliente de hello, en parte inferior de Hola de hello **configurar** ficha, elija **ver extremos**.</span><span class="sxs-lookup"><span data-stu-id="66e98-229">After you get hello client ID, at hello bottom of hello **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="66e98-230">Copiar dirección URL de Hola para **documento de metadatos de federación**y busque la dirección URL de toothat.</span><span class="sxs-lookup"><span data-stu-id="66e98-230">Copy hello URL for **Federation Metadata Document**, and browse toothat URL.</span></span>

7. <span data-ttu-id="66e98-231">En el documento de metadatos de Hola que se abre, busque raíz hello **EntityDescriptor identificador** elemento, que tiene un **entityID** atributo con este formato:`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="66e98-231">In hello metadata document that opens, find hello root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="66e98-232">Hola GUID en este atributo es GUID específico de su inquilino (identificador de inquilino).</span><span class="sxs-lookup"><span data-stu-id="66e98-232">hello GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="66e98-233">Copie el Id. de inquilino de Hola y guardar ese identificador para su uso en la parte 3 así como toouse en la aplicación web o una plantilla de implementación de la aplicación de API, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="66e98-233">Copy hello tenant ID and save that ID for use in Part 3, and also toouse in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="66e98-234">Para más información, consulte los temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="66e98-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="66e98-235">Autenticación de usuario para aplicaciones de API en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="66e98-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="66e98-236">Autenticación y autorización en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="66e98-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="66e98-237">**Activación de la autenticación cuando implemente con una plantilla de Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="66e98-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="66e98-238">Todavía debe crear una identidad de aplicación de Azure AD para su aplicación web o API que difiera de la identidad de aplicación hello para la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="66e98-238">You must still create an Azure AD application identity for your web app or API app that differs from hello app identity for your logic app.</span></span> <span data-ttu-id="66e98-239">identidad de aplicación de hello toocreate, Hola de seguimiento anterior pasos en la parte 2 de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="66e98-239">toocreate hello application identity, follow hello previous steps in Part 2 for hello Azure portal.</span></span> <span data-ttu-id="66e98-240">También puede seguir los pasos de hello en la parte 1, pero debe toouse seguro de la aplicación web o una aplicación de API real `https://{URL}` para **dirección URL de inicio de sesión** y **App ID URI**.</span><span class="sxs-lookup"><span data-stu-id="66e98-240">You can also follow hello steps in Part 1, but make sure toouse your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="66e98-241">De estos pasos, tendrá toosave tanto cliente hello identificador y el identificador de inquilino para su uso en la plantilla de implementación de la aplicación y también para parte 3.</span><span class="sxs-lookup"><span data-stu-id="66e98-241">From these steps, you have toosave both hello client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="66e98-242">Cuando se crea la identidad de aplicación hello Azure AD de su aplicación web o aplicación de API, debe usar Hola portal de Azure o portal de Azure clásico, en lugar de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66e98-242">When you create hello Azure AD application identity for your web app or API app, you must use hello Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="66e98-243">Hola PowerShell commandlet no configure los permisos de hello necesario toosign a los usuarios en un sitio Web.</span><span class="sxs-lookup"><span data-stu-id="66e98-243">hello PowerShell commandlet doesn't set up hello required permissions toosign users into a website.</span></span>

<span data-ttu-id="66e98-244">Después de obtener Id. de cliente de Hola y el Id. de inquilino, incluir estos identificadores como un subresource de su aplicación web o aplicación de API en la plantilla de implementación:</span><span class="sxs-lookup"><span data-stu-id="66e98-244">After you get hello client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

<span data-ttu-id="66e98-245">tooautomatically implementar una aplicación web en blanco y una aplicación lógica junto con la autenticación de Azure Active Directory, [vista Hola plantilla completa aquí](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), o haga clic en **implementar tooAzure** aquí:</span><span class="sxs-lookup"><span data-stu-id="66e98-245">tooautomatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view hello complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy tooAzure** here:</span></span>

<span data-ttu-id="66e98-246">[![Implementar tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="66e98-246">[![Deploy tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a><span data-ttu-id="66e98-247">Parte 3: Rellenar la sección de autorización de hello en la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="66e98-247">Part 3: Populate hello Authorization section in your logic app</span></span>

<span data-ttu-id="66e98-248">plantilla anterior Hola ya tiene esta sección autorización configurar, pero si directamente a crear la aplicación de la lógica de hello, debe incluir la sección de hello autorización completa.</span><span class="sxs-lookup"><span data-stu-id="66e98-248">hello previous template already has this authorization section set up, but if you are directly authoring hello logic app, you must include hello full authorization section.</span></span>

<span data-ttu-id="66e98-249">Abra la definición de aplicación lógica en la vista de código, vaya toohello **HTTP** Hola de búsqueda, en una sección de acción **autorización** sección e incluya esta línea:</span><span class="sxs-lookup"><span data-stu-id="66e98-249">Open your logic app definition in code view, go toohello **HTTP** action section, find hello **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="66e98-250">Elemento</span><span class="sxs-lookup"><span data-stu-id="66e98-250">Element</span></span> | <span data-ttu-id="66e98-251">Descripción</span><span class="sxs-lookup"><span data-stu-id="66e98-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="66e98-252">tenant</span><span class="sxs-lookup"><span data-stu-id="66e98-252">tenant</span></span> |<span data-ttu-id="66e98-253">Hola GUID para el inquilino de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="66e98-253">hello GUID for hello Azure AD tenant</span></span> |
| <span data-ttu-id="66e98-254">audience</span><span class="sxs-lookup"><span data-stu-id="66e98-254">audience</span></span> |<span data-ttu-id="66e98-255">Necesario.</span><span class="sxs-lookup"><span data-stu-id="66e98-255">Required.</span></span> <span data-ttu-id="66e98-256">Hola GUID para el recurso de destino de Hola que desea tooaccess - Hola Id. de cliente de la identidad de aplicación Hola para su aplicación web o aplicación de API</span><span class="sxs-lookup"><span data-stu-id="66e98-256">hello GUID for hello target resource that you want tooaccess - hello client ID from hello application identity for your web app or API app</span></span> |
| <span data-ttu-id="66e98-257">clientId</span><span class="sxs-lookup"><span data-stu-id="66e98-257">clientId</span></span> |<span data-ttu-id="66e98-258">Hola GUID para solicitar acceso - Hola Id. de cliente de la identidad de aplicación hello para la aplicación lógica de cliente de Hola</span><span class="sxs-lookup"><span data-stu-id="66e98-258">hello GUID for hello client requesting access - hello client ID from hello application identity for your logic app</span></span> |
| <span data-ttu-id="66e98-259">secret</span><span class="sxs-lookup"><span data-stu-id="66e98-259">secret</span></span> |<span data-ttu-id="66e98-260">Necesario.</span><span class="sxs-lookup"><span data-stu-id="66e98-260">Required.</span></span> <span data-ttu-id="66e98-261">Hola clave o contraseña de identidad de aplicación cliente de Hola que está solicitando el token de acceso de Hola Hola</span><span class="sxs-lookup"><span data-stu-id="66e98-261">hello key or password from hello application identity for hello client that's requesting hello access token</span></span> |
| <span data-ttu-id="66e98-262">type</span><span class="sxs-lookup"><span data-stu-id="66e98-262">type</span></span> |<span data-ttu-id="66e98-263">tipo de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="66e98-263">hello authentication type.</span></span> <span data-ttu-id="66e98-264">Para la autenticación ActiveDirectoryOAuth, el valor de hello es `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="66e98-264">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="66e98-265">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="66e98-265">For example:</span></span>

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="66e98-266">Protección de las llamadas API mediante código</span><span class="sxs-lookup"><span data-stu-id="66e98-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="66e98-267">Autenticación de certificados</span><span class="sxs-lookup"><span data-stu-id="66e98-267">Certificate authentication</span></span>

<span data-ttu-id="66e98-268">toovalidate hello las solicitudes entrantes de su aplicación web de lógica aplicación tooyour o API, puede usar certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="66e98-268">toovalidate hello incoming requests from your logic app tooyour web app or API app, you can use client certificates.</span></span> <span data-ttu-id="66e98-269">Obtenga información acerca de tooset el código, [la autenticación mutua de tooconfigure TLS](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span><span class="sxs-lookup"><span data-stu-id="66e98-269">tooset up your code, learn [how tooconfigure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="66e98-270">Hola **autorización** sección, incluya esta línea:</span><span class="sxs-lookup"><span data-stu-id="66e98-270">In hello **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="66e98-271">Elemento</span><span class="sxs-lookup"><span data-stu-id="66e98-271">Element</span></span> | <span data-ttu-id="66e98-272">Descripción</span><span class="sxs-lookup"><span data-stu-id="66e98-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="66e98-273">type</span><span class="sxs-lookup"><span data-stu-id="66e98-273">type</span></span> |<span data-ttu-id="66e98-274">Necesario.</span><span class="sxs-lookup"><span data-stu-id="66e98-274">Required.</span></span> <span data-ttu-id="66e98-275">tipo de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="66e98-275">hello authentication type.</span></span> <span data-ttu-id="66e98-276">Para los certificados de cliente SSL, debe ser el valor de hello `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="66e98-276">For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="66e98-277">Contraseña</span><span class="sxs-lookup"><span data-stu-id="66e98-277">password</span></span> |<span data-ttu-id="66e98-278">Necesario.</span><span class="sxs-lookup"><span data-stu-id="66e98-278">Required.</span></span> <span data-ttu-id="66e98-279">contraseña de Hola para acceder al certificado de cliente de hello (archivo PFX)</span><span class="sxs-lookup"><span data-stu-id="66e98-279">hello password for accessing hello client certificate (PFX file)</span></span> |
| <span data-ttu-id="66e98-280">pfx</span><span class="sxs-lookup"><span data-stu-id="66e98-280">pfx</span></span> |<span data-ttu-id="66e98-281">Necesario.</span><span class="sxs-lookup"><span data-stu-id="66e98-281">Required.</span></span> <span data-ttu-id="66e98-282">Contenido codificado en base64 del certificado de cliente de hello (archivo PFX)</span><span class="sxs-lookup"><span data-stu-id="66e98-282">Base64-encoded contents of hello client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="66e98-283">Autenticación básica</span><span class="sxs-lookup"><span data-stu-id="66e98-283">Basic authentication</span></span>

<span data-ttu-id="66e98-284">toovalidate las solicitudes entrantes de su aplicación web de lógica aplicación tooyour o API, puede usar la autenticación básica, por ejemplo, un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="66e98-284">toovalidate incoming requests from your logic app tooyour web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="66e98-285">La autenticación básica es un patrón común, y puede utilizar esta autenticación en cualquier toobuild de lenguaje que se utiliza la aplicación web o una aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="66e98-285">Basic authentication is a common pattern, and you can use this authentication in any language used toobuild your web app or API app.</span></span>

<span data-ttu-id="66e98-286">Hola **autorización** sección, incluya esta línea:</span><span class="sxs-lookup"><span data-stu-id="66e98-286">In hello **Authorization** section, include this line:</span></span>

<span data-ttu-id="66e98-287">`{"type": "basic", "username": "username", "password": "password"}`.</span><span class="sxs-lookup"><span data-stu-id="66e98-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="66e98-288">Elemento</span><span class="sxs-lookup"><span data-stu-id="66e98-288">Element</span></span> | <span data-ttu-id="66e98-289">Descripción</span><span class="sxs-lookup"><span data-stu-id="66e98-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66e98-290">type</span><span class="sxs-lookup"><span data-stu-id="66e98-290">type</span></span> |<span data-ttu-id="66e98-291">Necesario.</span><span class="sxs-lookup"><span data-stu-id="66e98-291">Required.</span></span> <span data-ttu-id="66e98-292">tipo de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="66e98-292">hello authentication type.</span></span> <span data-ttu-id="66e98-293">Para la autenticación básica, debe ser el valor de hello `Basic`.</span><span class="sxs-lookup"><span data-stu-id="66e98-293">For basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="66e98-294">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="66e98-294">username</span></span> |<span data-ttu-id="66e98-295">Necesario.</span><span class="sxs-lookup"><span data-stu-id="66e98-295">Required.</span></span> <span data-ttu-id="66e98-296">nombre de usuario de Hello para la autenticación</span><span class="sxs-lookup"><span data-stu-id="66e98-296">hello username for authentication</span></span> |
| <span data-ttu-id="66e98-297">Contraseña</span><span class="sxs-lookup"><span data-stu-id="66e98-297">password</span></span> |<span data-ttu-id="66e98-298">Necesario.</span><span class="sxs-lookup"><span data-stu-id="66e98-298">Required.</span></span> <span data-ttu-id="66e98-299">contraseña de Hello para la autenticación</span><span class="sxs-lookup"><span data-stu-id="66e98-299">hello password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="66e98-300">Autenticación de Azure Active Directory mediante código</span><span class="sxs-lookup"><span data-stu-id="66e98-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="66e98-301">De forma predeterminada, la autenticación de Azure AD de hello activar Hola portal de Azure no proporciona autorización específica.</span><span class="sxs-lookup"><span data-stu-id="66e98-301">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="66e98-302">Por ejemplo, esta autenticación bloquea su toojust API una específicos del inquilino, no tooa un usuario específico o una aplicación.</span><span class="sxs-lookup"><span data-stu-id="66e98-302">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

<span data-ttu-id="66e98-303">acceso de aplicación lógica toorestrict API tooyour a través del código, extraer el encabezado de Hola que tiene Hola JSON web token (JWT).</span><span class="sxs-lookup"><span data-stu-id="66e98-303">toorestrict API access tooyour logic app through code, extract hello header that has hello JSON web token (JWT).</span></span> <span data-ttu-id="66e98-304">Comprobar la identidad del llamador de Hola y rechazar las solicitudes que no coinciden.</span><span class="sxs-lookup"><span data-stu-id="66e98-304">Check hello caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="66e98-305">Si sigue adelante, tooimplement esta autenticación completamente en su propio código, no use hello y portal de Azure, obtenga información acerca de cómo demasiado [autenticarse con local de Active Directory en la aplicación de Azure](../app-service-web/web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="66e98-305">Going further, tooimplement this authentication entirely in your own code, and not use hello Azure portal, learn how too [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="66e98-306">toocreate una identidad de aplicación para la aplicación lógica y utiliza esa identidad toocall su API, debe seguir los pasos anteriores de Hola.</span><span class="sxs-lookup"><span data-stu-id="66e98-306">toocreate an application identity for your logic app and use that identity toocall your API, you must follow hello previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66e98-307">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="66e98-307">Next steps</span></span>

* [<span data-ttu-id="66e98-308">Comprobación del rendimiento de la aplicación lógica con alertas y registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="66e98-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)