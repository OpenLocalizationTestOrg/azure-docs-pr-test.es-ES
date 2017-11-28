---
title: "Implementación, llamada y autenticación de API web y API de REST para Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: 88c62d5ab046d8cf4bce5d23b776e517bb0e1d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="79127-104">Implementación, llamada y autenticación de API personalizadas como conectores para aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="79127-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="79127-105">Después de [crear API personalizadas](./logic-apps-create-api-app.md) que proporcionan acciones o desencadenadores para usarlos en flujos de trabajo de aplicaciones lógicas, debe implementar las API antes de poder llamarlas.</span><span class="sxs-lookup"><span data-stu-id="79127-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers to use in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="79127-106">Aunque se puede llamar a cualquier API desde una aplicación lógica, para lograr una experiencia óptima, agregue [metadatos de Swagger](http://swagger.io/specification/) que describan las operaciones y los parámetros de la API.</span><span class="sxs-lookup"><span data-stu-id="79127-106">And although you can call any API from a logic app, for the best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="79127-107">Este archivo de Swagger ayuda a que su API funcione mejor y se integre con más facilidad con aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="79127-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="79127-108">Puede implementar las API como [aplicaciones web](../app-service-web/app-service-web-overview.md), pero considere la posibilidad de implementarlas como [aplicaciones de API](../app-service-api/app-service-api-apps-why-best-platform.md), que pueden facilitarle su trabajo al compilar, hospedar y consumir API en la nube y en el entorno local.</span><span class="sxs-lookup"><span data-stu-id="79127-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in the cloud and on premises.</span></span> <span data-ttu-id="79127-109">No tiene que cambiar ningún código en las API; basta con implementar el código en una aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="79127-109">You don't have to change any code in your APIs -- just deploy your code to an API app.</span></span> <span data-ttu-id="79127-110">Puede hospedar las API en [Azure App Service](../app-service/app-service-value-prop-what-is.md), una oferta de plataforma como servicio (PaaS) que proporciona una de las maneras más adecuadas, fáciles y escalables de hospedar API.</span><span class="sxs-lookup"><span data-stu-id="79127-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of the best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="79127-111">Para autenticar llamadas desde aplicaciones lógicas a las API, puede configurar Azure Active Directory en Azure Portal para no tener que actualizar el código.</span><span class="sxs-lookup"><span data-stu-id="79127-111">To authenticate calls from logic apps to your APIs, you can set up Azure Active Directory in the Azure portal so you don't have to update your code.</span></span> <span data-ttu-id="79127-112">También puede requerir y aplicar la autenticación a través del código de la API.</span><span class="sxs-lookup"><span data-stu-id="79127-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="79127-113">Implementación de la API como aplicación web o aplicación de API</span><span class="sxs-lookup"><span data-stu-id="79127-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="79127-114">Para poder llamar a su API personalizada desde una aplicación lógica, impleméntela como aplicación web o aplicación de API en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="79127-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app to Azure App Service.</span></span> <span data-ttu-id="79127-115">Además, para mejorar la legibilidad del documento de Swagger en el Diseñador de aplicación lógica, establezca las propiedades de definición de la API y active [Uso compartido de recursos entre orígenes (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) para su aplicación web o de API.</span><span class="sxs-lookup"><span data-stu-id="79127-115">Also, to make your Swagger document readable by the Logic App Designer, set the API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="79127-116">En Azure Portal, seleccione la aplicación web o de API.</span><span class="sxs-lookup"><span data-stu-id="79127-116">In the Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="79127-117">En la hoja que se abre, en **API**, elija **Definición de la API**.</span><span class="sxs-lookup"><span data-stu-id="79127-117">In the blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="79127-118">Establezca **Ubicación de la definición de la API** en la dirección URL del archivo swagger.json.</span><span class="sxs-lookup"><span data-stu-id="79127-118">Set the **API definition location** to the URL for your swagger.json file.</span></span>

   <span data-ttu-id="79127-119">Por lo general, la dirección URL aparece en este formato: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="79127-119">Usually, the URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![Vincular al archivo de Swagger para la API personalizada](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="79127-121">En **API**, elija **CORS**.</span><span class="sxs-lookup"><span data-stu-id="79127-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="79127-122">Establezca la directiva CORS para **Orígenes permitidos** en  **"*"** (permitir todos).</span><span class="sxs-lookup"><span data-stu-id="79127-122">Set the CORS policy for **Allowed origins** to **'*'** (allow all).</span></span>

   <span data-ttu-id="79127-123">Esta configuración permite solicitudes del Diseñador de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="79127-123">This setting permits requests from Logic App Designer.</span></span>

   ![Permitir solicitudes del Diseñador de aplicación lógica a la API personalizada](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="79127-125">Para obtener más información, consulte estos artículos:</span><span class="sxs-lookup"><span data-stu-id="79127-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="79127-126">Incorporación de metadatos de Swagger para las API web de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="79127-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="79127-127">Implementación de las API web de ASP.NET en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="79127-127">Deploy ASP.NET web APIs to Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="79127-128">Llamada a la API personalizada desde flujos de trabajo de aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="79127-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="79127-129">Después de configurar las propiedades de definición de la API y de CORS, los desencadenadores y las acciones de la API personalizada deberían estar disponibles para incluirlos en el flujo de trabajo de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="79127-129">After you set up the API definition properties and CORS, your custom API's triggers and actions should become available for you to include in your logic app workflow.</span></span> 

*  <span data-ttu-id="79127-130">Para ver los sitios web que tengan direcciones URL de Swagger, puede examinar los sitios web de su suscripción en el Diseñador de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="79127-130">To view the websites that have Swagger URLs, you can browse your subscription websites in the Logic Apps Designer.</span></span>

*  <span data-ttu-id="79127-131">Para ver las acciones y entradas disponibles señalando a un documento de Swagger, use la [acción HTTP + Swagger](../connectors/connectors-native-http-swagger.md).</span><span class="sxs-lookup"><span data-stu-id="79127-131">To view available actions and inputs by pointing at a Swagger document, use the [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="79127-132">Para llamar a cualquier API, incluso aquellas que no tengan ni expongan un documento de Swagger, siempre puede crear una solicitud con la [acción HTTP](../connectors/connectors-native-http.md).</span><span class="sxs-lookup"><span data-stu-id="79127-132">To call any API, including APIs that don't have or expose a Swagger document, you can always create a request with the [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-to-your-custom-api"></a><span data-ttu-id="79127-133">Autenticación de las llamadas a la API personalizada</span><span class="sxs-lookup"><span data-stu-id="79127-133">Authenticate calls to your custom API</span></span>

<span data-ttu-id="79127-134">Puede proteger las llamadas a la API personalizada de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="79127-134">You can secure calls to your custom API in these ways:</span></span>

* <span data-ttu-id="79127-135">[Ningún cambio de código](#no-code): proteja su API con [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) por medio de Azure Portal, de forma que no tenga que actualizar el código ni volver a implementar la API.</span><span class="sxs-lookup"><span data-stu-id="79127-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through the Azure portal, so you don't have to update your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="79127-136">De forma predeterminada, la autenticación de Azure AD que se activa en Azure Portal no lleva a cabo una autorización específica.</span><span class="sxs-lookup"><span data-stu-id="79127-136">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="79127-137">Por ejemplo, esta autenticación bloquea la API a un solo inquilino concreto, no a una aplicación o un usuario específicos.</span><span class="sxs-lookup"><span data-stu-id="79127-137">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span></span> 

* <span data-ttu-id="79127-138">[Actualice el código de la API](#update-code): proteja su API aplicando la [autenticación de certificado](#certificate), la [autenticación básica](#basic) o la [autenticación de Azure AD](#azure-ad-code) mediante código.</span><span class="sxs-lookup"><span data-stu-id="79127-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-to-your-api-without-changing-code"></a><span data-ttu-id="79127-139">Autenticación de las llamadas a la API sin cambiar el código</span><span class="sxs-lookup"><span data-stu-id="79127-139">Authenticate calls to your API without changing code</span></span>

<span data-ttu-id="79127-140">Estos son los pasos generales para este método:</span><span class="sxs-lookup"><span data-stu-id="79127-140">Here's the general steps for this method:</span></span>

1. <span data-ttu-id="79127-141">Cree dos [identidades de aplicación de Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md): una para la aplicación lógica y otra para la aplicación web (o aplicación de API).</span><span class="sxs-lookup"><span data-stu-id="79127-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="79127-142">Para autenticar llamadas a la API, use las credenciales (identificador de cliente y secreto) de la [entidad de servicio](../app-service-api/app-service-api-dotnet-service-principal-auth.md) asociada con la identidad de aplicación de Azure AD para su aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="79127-142">To authenticate calls to your API, use the credentials (client ID and secret) for the [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with the Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="79127-143">Incluya los identificadores de aplicación en la definición de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="79127-143">Include the application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="79127-144">Parte 1: Creación de una identidad de aplicación de Azure AD para la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="79127-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="79127-145">La aplicación lógica usa esta identidad de aplicación de Azure AD para autenticarse en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79127-145">Your logic app uses this Azure AD application identity to authenticate against Azure AD.</span></span> <span data-ttu-id="79127-146">Solo tiene que establecer esta identidad una vez para el directorio.</span><span class="sxs-lookup"><span data-stu-id="79127-146">You only have to set up this identity one time for your directory.</span></span> <span data-ttu-id="79127-147">Por ejemplo, puede usar la misma identidad para todas las aplicaciones lógicas, aunque puede crear identidades únicas para cada una.</span><span class="sxs-lookup"><span data-stu-id="79127-147">For example, you can choose to use the same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="79127-148">Puede configurar estas identidades en Azure Portal, en el [Portal de Azure clásico](#app-identity-logic-classic) o con [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="79127-148">You can set up these identities in the Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="79127-149">**Creación de la identidad de aplicación para la aplicación lógica en Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="79127-149">**Create the application identity for your logic app in the Azure portal**</span></span>

1. <span data-ttu-id="79127-150">En [Azure Portal](https://portal.azure.com "https://portal.azure.com"), elija **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79127-150">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="79127-151">Confirme que se encuentra en el mismo directorio que la aplicación web o de API.</span><span class="sxs-lookup"><span data-stu-id="79127-151">Confirm that you're in the same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="79127-152">Para cambiar de directorio, haga clic en el perfil y seleccione otro.</span><span class="sxs-lookup"><span data-stu-id="79127-152">To switch directories, click your profile and select another directory.</span></span> <span data-ttu-id="79127-153">O bien, elija **Información general** > **Cambiar directorio**.</span><span class="sxs-lookup"><span data-stu-id="79127-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="79127-154">En el menú de directorio, en **Administrar**, elija **Registros de aplicaciones** > **Nuevo registro de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="79127-154">On the directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="79127-155">De forma predeterminada, la lista de registros de aplicaciones muestra todos los presentes en el directorio.</span><span class="sxs-lookup"><span data-stu-id="79127-155">By default, the app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="79127-156">Para ver solo sus registros de aplicaciones, junto al cuadro de búsqueda, seleccione **Mis aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="79127-156">To view only your app registrations, next to the search box, select **My apps**.</span></span> 

   ![Crear registro de aplicaciones](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="79127-158">Asigne un nombre a la identidad de aplicación, deje **Tipo de aplicación** establecido en **Aplicación web o API**, proporcione una cadena única con formato de dominio para **Dirección URL de inicio de sesión** y elija **Crear**.</span><span class="sxs-lookup"><span data-stu-id="79127-158">Give your application identity a name, leave **Application type** set to **Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![Proporcionar un nombre y una dirección URL de inicio de sesión para la identidad de aplicación](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="79127-160">La identidad de aplicación que ha creado para la aplicación lógica aparece ahora en la lista de registros de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="79127-160">The application identity that you created for your logic app now appears in the app registrations list.</span></span>

   ![Identidad de aplicación para la aplicación lógica](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="79127-162">En la lista de registros de aplicaciones, seleccione la nueva identidad de aplicación.</span><span class="sxs-lookup"><span data-stu-id="79127-162">In the app registrations list, select your new application identity.</span></span> <span data-ttu-id="79127-163">Copie y guarde el valor de **Id. de la aplicación** para usarlo como "identificador de cliente" de la aplicación lógica en la parte 3.</span><span class="sxs-lookup"><span data-stu-id="79127-163">Copy and save the **Application ID** to use as the "client ID" for your logic app in Part 3.</span></span>

   ![Copiar y guardar el identificador de aplicación para la aplicación lógica](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="79127-165">Si la configuración de la identidad de aplicación no está visible, elija **Configuración** o **Toda la configuración**.</span><span class="sxs-lookup"><span data-stu-id="79127-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="79127-166">En **Acceso de API**, elija **Claves**.</span><span class="sxs-lookup"><span data-stu-id="79127-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="79127-167">En **Descripción**, proporcione un nombre para la clave.</span><span class="sxs-lookup"><span data-stu-id="79127-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="79127-168">En **Expira**, seleccione una duración para la clave.</span><span class="sxs-lookup"><span data-stu-id="79127-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="79127-169">La clave que va a crear actúa como "secreto" o contraseña de la identidad de aplicación para la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="79127-169">The key that you're creating acts as the application identity's "secret" or password for your logic app.</span></span>

   ![Crear clave para la identidad de aplicación lógica](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="79127-171">En la barra de herramientas, elija **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="79127-171">On the toolbar, choose **Save**.</span></span> <span data-ttu-id="79127-172">En **Valor**, ahora aparece su clave.</span><span class="sxs-lookup"><span data-stu-id="79127-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="79127-173">**Asegúrese de copiar y guardar la clave** para usarla más adelante, ya que está oculta una vez que se sale de la hoja Claves.</span><span class="sxs-lookup"><span data-stu-id="79127-173">**Make sure to copy and save your key** for later use because the key is hidden when you leave the key blade.</span></span>

   <span data-ttu-id="79127-174">Cuando configure la aplicación lógica en la parte 3, especifique esta clave como "secreto" o contraseña.</span><span class="sxs-lookup"><span data-stu-id="79127-174">When you configure your logic app in Part 3, you specify this key as the "secret" or password.</span></span>

   ![Copiar y guardar la clave para más tarde](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="79127-176">**Creación de la identidad de aplicación para la aplicación lógica en el Portal de Azure clásico**</span><span class="sxs-lookup"><span data-stu-id="79127-176">**Create the application identity for your logic app in the Azure classic portal**</span></span>

1. <span data-ttu-id="79127-177">En el Portal de Azure clásico, elija [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="79127-177">In the Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="79127-178">Seleccione el directorio que usó para la aplicación web o de API.</span><span class="sxs-lookup"><span data-stu-id="79127-178">Select the same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="79127-179">En la pestaña **Aplicaciones**, elija **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="79127-179">On the **Applications** tab, choose **Add** at the bottom of the page.</span></span>

4. <span data-ttu-id="79127-180">Asigne un nombre a la identidad de aplicación y elija **Siguiente** (flecha derecha).</span><span class="sxs-lookup"><span data-stu-id="79127-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="79127-181">En **Propiedades de la aplicación**, proporcione una cadena única con formato de dominio para **Dirección URL de inicio de sesión** y **URI de id. de aplicación**, y elija **Completar** (marca de verificación).</span><span class="sxs-lookup"><span data-stu-id="79127-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="79127-182">En la pestaña **Configurar**, copie y guarde el valor de **Id. de cliente** para usarlo con la aplicación lógica en la parte 3.</span><span class="sxs-lookup"><span data-stu-id="79127-182">On the **Configure** tab, copy and save the **Client ID** for your logic app to use in Part 3.</span></span>

7. <span data-ttu-id="79127-183">En **Claves**, abra la lista **Seleccionar duración**.</span><span class="sxs-lookup"><span data-stu-id="79127-183">Under **Keys**, open the **Select duration** list.</span></span> <span data-ttu-id="79127-184">Seleccione una duración para la clave.</span><span class="sxs-lookup"><span data-stu-id="79127-184">Select a duration for your key.</span></span>

   <span data-ttu-id="79127-185">La clave que va a crear actúa como "secreto" o contraseña de la identidad de aplicación para la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="79127-185">The key that you're creating acts as the application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="79127-186">En la parte inferior de la página, elija **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="79127-186">At the bottom of the page, choose **Save**.</span></span> <span data-ttu-id="79127-187">Quizás tenga que esperar unos segundos.</span><span class="sxs-lookup"><span data-stu-id="79127-187">You might have to wait a few seconds.</span></span>

9. <span data-ttu-id="79127-188">En **Claves**, asegúrese de copiar y guardar la clave que ahora aparece.</span><span class="sxs-lookup"><span data-stu-id="79127-188">Under **Keys**, make sure to copy and save the key that now appears.</span></span> 

   <span data-ttu-id="79127-189">Cuando configure la aplicación lógica en la parte 3, especifique esta clave como "secreto" o contraseña.</span><span class="sxs-lookup"><span data-stu-id="79127-189">When you configure your logic app in Part 3, you specify this key as the "secret" or password.</span></span>

<span data-ttu-id="79127-190">Para más información, aprenda a [configurar la aplicación de App Service para usar el inicio de sesión de Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="79127-190">For more information, learn how to [configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="79127-191">**Creación de la identidad de aplicación para la aplicación lógica en PowerShell**</span><span class="sxs-lookup"><span data-stu-id="79127-191">**Create the application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="79127-192">Puede realizar esta tarea mediante Azure Resource Manager con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79127-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="79127-193">En PowerShell, ejecute estos comandos:</span><span class="sxs-lookup"><span data-stu-id="79127-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="79127-194">Asegúrese de copiar el valor de **Identificador de inquilino** (GUID para el inquilino de Azure AD), el de **Id. de la aplicación** y la contraseña que usó.</span><span class="sxs-lookup"><span data-stu-id="79127-194">Make sure to copy the **Tenant ID** (GUID for your Azure AD tenant), the **Application ID**, and the password that you used.</span></span>

<span data-ttu-id="79127-195">Para más información, consulte cómo [crear una entidad de servicio con PowerShell para acceder a recursos](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="79127-195">For more information, learn how to [create a service principal with PowerShell to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="79127-196">Parte 2: Creación de una identidad de aplicación de Azure AD para la aplicación web o de API</span><span class="sxs-lookup"><span data-stu-id="79127-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="79127-197">Si ya se ha implementado la aplicación web o de API, puede activar la autenticación y crear la identidad de aplicación en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="79127-197">If your web app or API app is already deployed, you can turn on authentication and create the application identity in the Azure portal.</span></span> <span data-ttu-id="79127-198">En caso contrario, puede [activar la autenticación cuando implemente con una plantilla de Azure Resource Manager](#authen-deploy).</span><span class="sxs-lookup"><span data-stu-id="79127-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="79127-199">**Creación de la identidad de aplicación y activación de la autenticación en Azure Portal para aplicaciones implementadas**</span><span class="sxs-lookup"><span data-stu-id="79127-199">**Create the application identity and turn on authentication in the Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="79127-200">En [Azure Portal](https://portal.azure.com "https://portal.azure.com"), busque y seleccione la aplicación web o de API.</span><span class="sxs-lookup"><span data-stu-id="79127-200">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="79127-201">Haga clic en **Configuración** y elija **Autenticación/autorización**.</span><span class="sxs-lookup"><span data-stu-id="79127-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="79127-202">En **Autenticación de App Service**, elija **Activar** la autenticación.</span><span class="sxs-lookup"><span data-stu-id="79127-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="79127-203">En **Proveedores de autenticación**, elija **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79127-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![Activar la autenticación](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="79127-205">Ahora cree una identidad de aplicación para la aplicación web o de API como se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="79127-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="79127-206">En la hoja **Configuración de Azure Active Directory**, establezca **Modo de administración** en **Rápido**.</span><span class="sxs-lookup"><span data-stu-id="79127-206">On the **Azure Active Directory Settings** blade, set **Management mode** to **Express**.</span></span> <span data-ttu-id="79127-207">Elija **Crear nueva aplicación de AD**.</span><span class="sxs-lookup"><span data-stu-id="79127-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="79127-208">Asigne un nombre a la identidad de aplicación y elija **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="79127-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![Crear una identidad de aplicación para la aplicación web o de API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="79127-210">En la **hoja Autenticación o autorización**, elija **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="79127-210">On the **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="79127-211">Ahora debe buscar el identificador de cliente y el de inquilino para la identidad de aplicación que esté asociada con la aplicación web o de API.</span><span class="sxs-lookup"><span data-stu-id="79127-211">Now you must find the client ID and tenant ID for the application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="79127-212">Ha usado estos identificadores en la parte 3.</span><span class="sxs-lookup"><span data-stu-id="79127-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="79127-213">Por tanto, continúe con estos pasos para Azure Portal o el [Portal de Azure clásico](#find-id-classic).</span><span class="sxs-lookup"><span data-stu-id="79127-213">So continue with these steps for the Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="79127-214">**Búsqueda de los identificadores de cliente y de inquilino de la identidad de aplicación para su aplicación web o de API en Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="79127-214">**Find application identity's client ID and tenant ID for your web app or API app in the Azure portal**</span></span>

1. <span data-ttu-id="79127-215">En **Proveedores de autenticación**, elija **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79127-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   ![Elegir "Azure Active Directory"](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="79127-217">En la hoja **Configuración de Azure Active Directory**, establezca **Modo de administración** en **Avanzado**.</span><span class="sxs-lookup"><span data-stu-id="79127-217">On the **Azure Active Directory Settings** blade, set **Management mode** to **Advanced**.</span></span>

3. <span data-ttu-id="79127-218">Copie el valor de **Id. de cliente** y guarde ese GUID para usarlo en la parte 3.</span><span class="sxs-lookup"><span data-stu-id="79127-218">Copy the **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="79127-219">Si **Id. de cliente** y **URL del emisor** no aparecen, pruebe a actualizar Azure Portal y repita el paso 1.</span><span class="sxs-lookup"><span data-stu-id="79127-219">If **Client ID** and **Issuer Url** don't appear, try refreshing the Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="79127-220">En **URL del emisor**, copie y guarde solo el GUID para la parte 3.</span><span class="sxs-lookup"><span data-stu-id="79127-220">Under **Issuer Url**, copy and save just the GUID for Part 3.</span></span> <span data-ttu-id="79127-221">También puede usar este GUID en la plantilla de implementación de su aplicación web o de API, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="79127-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="79127-222">Este GUID es para su inquilino específico ("Identificador de inquilino") y debería aparecer en esta dirección URL: `https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="79127-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="79127-223">Sin guardar los cambios, cierre la hoja **Configuración de Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79127-223">Without saving your changes, close the **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="79127-224">**Búsqueda de los identificadores de cliente y de inquilino de la identidad de aplicación para su aplicación web o de API en Portal de Azure clásico**</span><span class="sxs-lookup"><span data-stu-id="79127-224">**Find application identity's client ID and tenant ID for your web app or API app in the Azure classic portal**</span></span>

1. <span data-ttu-id="79127-225">En el Portal de Azure clásico, elija [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="79127-225">In the Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="79127-226">Seleccione el directorio que usó para la aplicación web o de API.</span><span class="sxs-lookup"><span data-stu-id="79127-226">Select the directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="79127-227">En el cuadro **Búsqueda**, busque y seleccione la identidad de aplicación para su aplicación web o de API.</span><span class="sxs-lookup"><span data-stu-id="79127-227">In the **Search** box, find and select the application identity for your web app or API app.</span></span>

4. <span data-ttu-id="79127-228">En la pestaña **Configurar**, copie el valor de **Id. de cliente** y guarde ese GUID para usarlo en la parte 3.</span><span class="sxs-lookup"><span data-stu-id="79127-228">On the **Configure** tab, copy the **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="79127-229">Después de obtener el identificador de cliente, en la parte inferior de la pestaña **Configurar**, elija **Ver extremos**.</span><span class="sxs-lookup"><span data-stu-id="79127-229">After you get the client ID, at the bottom of the **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="79127-230">Copie la dirección URL para **Documento de metadatos de federación** y vaya a ella.</span><span class="sxs-lookup"><span data-stu-id="79127-230">Copy the URL for **Federation Metadata Document**, and browse to that URL.</span></span>

7. <span data-ttu-id="79127-231">En el documento de metadatos que se abre, busque el elemento **Id. de EntityDescriptor** raíz, que tiene un atributo **entityID** con este formato: `https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="79127-231">In the metadata document that opens, find the root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="79127-232">El GUID de este atributo es el del inquilino específico (Identificador de inquilino).</span><span class="sxs-lookup"><span data-stu-id="79127-232">The GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="79127-233">Copie el identificador del inquilino y guárdelo para usarlo en la parte 3 y también en la plantilla de implementación de su aplicación web o de API, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="79127-233">Copy the tenant ID and save that ID for use in Part 3, and also to use in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="79127-234">Para más información, consulte los temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="79127-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="79127-235">Autenticación de usuario para aplicaciones de API en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="79127-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="79127-236">Autenticación y autorización en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="79127-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="79127-237">**Activación de la autenticación cuando implemente con una plantilla de Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="79127-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="79127-238">Todavía debe crear para su aplicación web o de API una identidad de aplicación de Azure AD que difiera de la de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="79127-238">You must still create an Azure AD application identity for your web app or API app that differs from the app identity for your logic app.</span></span> <span data-ttu-id="79127-239">Para crear la identidad de aplicación, siga los pasos anteriores en la parte 2 para Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="79127-239">To create the application identity, follow the previous steps in Part 2 for the Azure portal.</span></span> <span data-ttu-id="79127-240">También puede seguir los pasos en la parte 1, pero asegúrese de usar `https://{URL}` para la aplicación web o de API en **Dirección URL de inicio de sesión** y **URI de id. de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="79127-240">You can also follow the steps in Part 1, but make sure to use your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="79127-241">En estos pasos, tiene que guardar el identificador de cliente y el de inquilino para usarlos en la plantilla de implementación de la aplicación y también en la parte 3.</span><span class="sxs-lookup"><span data-stu-id="79127-241">From these steps, you have to save both the client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="79127-242">Cuando cree la identidad de aplicación de Azure AD para su aplicación web o de API, debe usar Azure Portal o el Portal de Azure clásico, en lugar de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79127-242">When you create the Azure AD application identity for your web app or API app, you must use the Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="79127-243">El cmdlet de PowerShell no configura los permisos necesarios para iniciar la sesión de los usuarios en un sitio web.</span><span class="sxs-lookup"><span data-stu-id="79127-243">The PowerShell commandlet doesn't set up the required permissions to sign users into a website.</span></span>

<span data-ttu-id="79127-244">Una vez que obtenga los identificadores de cliente y de inquilino, inclúyalos como un subrecurso de la aplicación web o de API en la plantilla de implementación:</span><span class="sxs-lookup"><span data-stu-id="79127-244">After you get the client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

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

<span data-ttu-id="79127-245">Para implementar automáticamente una aplicación web en blanco y una aplicación lógica juntas con la autenticación de Azure Active Directory, [vea la plantilla completa aquí](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json) o haga clic en **Implementar en Azure** aquí:</span><span class="sxs-lookup"><span data-stu-id="79127-245">To automatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view the complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy to Azure** here:</span></span>

<span data-ttu-id="79127-246">[![Implementación en Azure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="79127-246">[![Deploy to Azure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-the-authorization-section-in-your-logic-app"></a><span data-ttu-id="79127-247">Parte 3: Relleno de la sección de autorización en la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="79127-247">Part 3: Populate the Authorization section in your logic app</span></span>

<span data-ttu-id="79127-248">La plantilla anterior ya tiene esta sección de autorización configurada pero, si va a crear la aplicación lógica directamente, debe incluir la sección de autorización completa.</span><span class="sxs-lookup"><span data-stu-id="79127-248">The previous template already has this authorization section set up, but if you are directly authoring the logic app, you must include the full authorization section.</span></span>

<span data-ttu-id="79127-249">Abra la definición de aplicación lógica en la vista de código, vaya a la sección de la acción **HTTP**, busque la sección **Authorization** e incluya esta línea:</span><span class="sxs-lookup"><span data-stu-id="79127-249">Open your logic app definition in code view, go to the **HTTP** action section, find the **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="79127-250">Elemento</span><span class="sxs-lookup"><span data-stu-id="79127-250">Element</span></span> | <span data-ttu-id="79127-251">Descripción</span><span class="sxs-lookup"><span data-stu-id="79127-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="79127-252">tenant</span><span class="sxs-lookup"><span data-stu-id="79127-252">tenant</span></span> |<span data-ttu-id="79127-253">El GUID para el inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="79127-253">The GUID for the Azure AD tenant</span></span> |
| <span data-ttu-id="79127-254">audience</span><span class="sxs-lookup"><span data-stu-id="79127-254">audience</span></span> |<span data-ttu-id="79127-255">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="79127-255">Required.</span></span> <span data-ttu-id="79127-256">El GUID para el recurso de destino al que desea acceder: el identificador de cliente de la identidad de aplicación para su aplicación web o de API</span><span class="sxs-lookup"><span data-stu-id="79127-256">The GUID for the target resource that you want to access - the client ID from the application identity for your web app or API app</span></span> |
| <span data-ttu-id="79127-257">clientId</span><span class="sxs-lookup"><span data-stu-id="79127-257">clientId</span></span> |<span data-ttu-id="79127-258">El GUID para el cliente que solicita acceso: el identificador de cliente de la identidad de aplicación para la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="79127-258">The GUID for the client requesting access - the client ID from the application identity for your logic app</span></span> |
| <span data-ttu-id="79127-259">secret</span><span class="sxs-lookup"><span data-stu-id="79127-259">secret</span></span> |<span data-ttu-id="79127-260">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="79127-260">Required.</span></span> <span data-ttu-id="79127-261">La clave o contraseña de la identidad de aplicación para el cliente que solicita el token de acceso</span><span class="sxs-lookup"><span data-stu-id="79127-261">The key or password from the application identity for the client that's requesting the access token</span></span> |
| <span data-ttu-id="79127-262">type</span><span class="sxs-lookup"><span data-stu-id="79127-262">type</span></span> |<span data-ttu-id="79127-263">El tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="79127-263">The authentication type.</span></span> <span data-ttu-id="79127-264">En autenticación ActiveDirectoryOAuth, el valor es `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="79127-264">For ActiveDirectoryOAuth authentication, the value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="79127-265">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="79127-265">For example:</span></span>

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

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="79127-266">Protección de las llamadas API mediante código</span><span class="sxs-lookup"><span data-stu-id="79127-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="79127-267">Autenticación de certificados</span><span class="sxs-lookup"><span data-stu-id="79127-267">Certificate authentication</span></span>

<span data-ttu-id="79127-268">Para validar las solicitudes entrantes desde la aplicación lógica hacia la aplicación web o de API, puede usar certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="79127-268">To validate the incoming requests from your logic app to your web app or API app, you can use client certificates.</span></span> <span data-ttu-id="79127-269">Para configurar su código, aprenda a [configurar la autenticación mutua de TLS](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span><span class="sxs-lookup"><span data-stu-id="79127-269">To set up your code, learn [how to configure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="79127-270">En la sección **Authorization**, incluya esta línea:</span><span class="sxs-lookup"><span data-stu-id="79127-270">In the **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="79127-271">Elemento</span><span class="sxs-lookup"><span data-stu-id="79127-271">Element</span></span> | <span data-ttu-id="79127-272">Descripción</span><span class="sxs-lookup"><span data-stu-id="79127-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="79127-273">type</span><span class="sxs-lookup"><span data-stu-id="79127-273">type</span></span> |<span data-ttu-id="79127-274">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="79127-274">Required.</span></span> <span data-ttu-id="79127-275">El tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="79127-275">The authentication type.</span></span> <span data-ttu-id="79127-276">Para los certificados de cliente SSL, el valor debe ser `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="79127-276">For SSL client certificates, the value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="79127-277">Contraseña</span><span class="sxs-lookup"><span data-stu-id="79127-277">password</span></span> |<span data-ttu-id="79127-278">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="79127-278">Required.</span></span> <span data-ttu-id="79127-279">La contraseña para acceder al certificado de cliente (archivo PFX)</span><span class="sxs-lookup"><span data-stu-id="79127-279">The password for accessing the client certificate (PFX file)</span></span> |
| <span data-ttu-id="79127-280">pfx</span><span class="sxs-lookup"><span data-stu-id="79127-280">pfx</span></span> |<span data-ttu-id="79127-281">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="79127-281">Required.</span></span> <span data-ttu-id="79127-282">Contenido con codificación base64 del certificado del cliente (archivo PFX)</span><span class="sxs-lookup"><span data-stu-id="79127-282">Base64-encoded contents of the client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="79127-283">Autenticación básica</span><span class="sxs-lookup"><span data-stu-id="79127-283">Basic authentication</span></span>

<span data-ttu-id="79127-284">Para validar solicitudes entrantes desde la aplicación lógica hacia la aplicación web o de API, puede usar la autenticación básica, por ejemplo, un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="79127-284">To validate incoming requests from your logic app to your web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="79127-285">La autenticación básica es un patrón habitual, y puede usarla en cualquier lenguaje utilizado para compilar la aplicación web o de API.</span><span class="sxs-lookup"><span data-stu-id="79127-285">Basic authentication is a common pattern, and you can use this authentication in any language used to build your web app or API app.</span></span>

<span data-ttu-id="79127-286">En la sección **Authorization**, incluya esta línea:</span><span class="sxs-lookup"><span data-stu-id="79127-286">In the **Authorization** section, include this line:</span></span>

<span data-ttu-id="79127-287">`{"type": "basic", "username": "username", "password": "password"}`.</span><span class="sxs-lookup"><span data-stu-id="79127-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="79127-288">Elemento</span><span class="sxs-lookup"><span data-stu-id="79127-288">Element</span></span> | <span data-ttu-id="79127-289">Descripción</span><span class="sxs-lookup"><span data-stu-id="79127-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="79127-290">type</span><span class="sxs-lookup"><span data-stu-id="79127-290">type</span></span> |<span data-ttu-id="79127-291">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="79127-291">Required.</span></span> <span data-ttu-id="79127-292">El tipo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="79127-292">The authentication type.</span></span> <span data-ttu-id="79127-293">Para la autenticación básica, el valor debe ser `Basic`.</span><span class="sxs-lookup"><span data-stu-id="79127-293">For basic authentication, the value must be `Basic`.</span></span> |
| <span data-ttu-id="79127-294">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="79127-294">username</span></span> |<span data-ttu-id="79127-295">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="79127-295">Required.</span></span> <span data-ttu-id="79127-296">El nombre de usuario para la autenticación</span><span class="sxs-lookup"><span data-stu-id="79127-296">The username for authentication</span></span> |
| <span data-ttu-id="79127-297">Contraseña</span><span class="sxs-lookup"><span data-stu-id="79127-297">password</span></span> |<span data-ttu-id="79127-298">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="79127-298">Required.</span></span> <span data-ttu-id="79127-299">La contraseña para la autenticación</span><span class="sxs-lookup"><span data-stu-id="79127-299">The password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="79127-300">Autenticación de Azure Active Directory mediante código</span><span class="sxs-lookup"><span data-stu-id="79127-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="79127-301">De forma predeterminada, la autenticación de Azure AD que se activa en Azure Portal no lleva a cabo una autorización específica.</span><span class="sxs-lookup"><span data-stu-id="79127-301">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="79127-302">Por ejemplo, esta autenticación bloquea la API a un solo inquilino concreto, no a una aplicación o un usuario específicos.</span><span class="sxs-lookup"><span data-stu-id="79127-302">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span></span> 

<span data-ttu-id="79127-303">Para restringir el acceso de la API a la aplicación lógica por medio de código, extraiga el encabezado que tenga JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="79127-303">To restrict API access to your logic app through code, extract the header that has the JSON web token (JWT).</span></span> <span data-ttu-id="79127-304">Compruebe la identidad del llamador y rechace las solicitudes que no coinciden.</span><span class="sxs-lookup"><span data-stu-id="79127-304">Check the caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="79127-305">Además, para implementar esta autenticación totalmente en su propio código sin usar Azure Portal, aprenda a [autenticarse con su entorno Active Directory local en su aplicación de Azure](../app-service-web/web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="79127-305">Going further, to implement this authentication entirely in your own code, and not use the Azure portal, learn how to [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="79127-306">Para crear una identidad de aplicación para la aplicación lógica y usarla para llamar a la API, debe seguir los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="79127-306">To create an application identity for your logic app and use that identity to call your API, you must follow the previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79127-307">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="79127-307">Next steps</span></span>

* [<span data-ttu-id="79127-308">Comprobación del rendimiento de la aplicación lógica con alertas y registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="79127-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)