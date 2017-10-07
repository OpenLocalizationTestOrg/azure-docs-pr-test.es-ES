---
title: "aaaProtect un back-end de API Web con Azure Active Directory y administración de API | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooprotect un back-end de API Web con Azure Active Directory y administración de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a><span data-ttu-id="12c2c-103">¿Cómo tooprotect un back-end de API Web con Azure Active Directory y administración de API</span><span class="sxs-lookup"><span data-stu-id="12c2c-103">How tooprotect a Web API backend with Azure Active Directory and API Management</span></span>
<span data-ttu-id="12c2c-104">Hola siguiendo el vídeo muestra cómo toobuild un API Web de back-end y la protección mediante el protocolo OAuth 2.0 con Azure Active Directory y administración de API.</span><span class="sxs-lookup"><span data-stu-id="12c2c-104">hello following video shows how toobuild a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span></span>  <span data-ttu-id="12c2c-105">Este artículo proporciona información general y los pasos de información adicional de hello en vídeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c2c-105">This article provides an overview and additional information for hello steps in hello video.</span></span> <span data-ttu-id="12c2c-106">Este vídeo de 24 minutos le muestra cómo:</span><span class="sxs-lookup"><span data-stu-id="12c2c-106">This 24 minute video shows you how to:</span></span>

* <span data-ttu-id="12c2c-107">Crear un back-end de API web y protegerlo con AAD, a partir de la 1:30</span><span class="sxs-lookup"><span data-stu-id="12c2c-107">Build a Web API backend and secure it with AAD - starting at 1:30</span></span>
* <span data-ttu-id="12c2c-108">Importar Hola API Administración de API - empezando a las 7:10</span><span class="sxs-lookup"><span data-stu-id="12c2c-108">Import hello API into API Management - starting at 7:10</span></span>
* <span data-ttu-id="12c2c-109">Configurar Hola Developer portal toocall Hola API - a partir de 9:09</span><span class="sxs-lookup"><span data-stu-id="12c2c-109">Configure hello Developer portal toocall hello API - starting at 9:09</span></span>
* <span data-ttu-id="12c2c-110">Configurar un hello toocall de aplicación de escritorio API - a partir de 18:08</span><span class="sxs-lookup"><span data-stu-id="12c2c-110">Configure a desktop application toocall hello API - starting at 18:08</span></span>
* <span data-ttu-id="12c2c-111">Configurar una toopre de directiva de validación de JWT-autorizar las solicitudes - a partir de 20:47</span><span class="sxs-lookup"><span data-stu-id="12c2c-111">Configure a JWT validation policy toopre-authorize requests - starting at 20:47</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a><span data-ttu-id="12c2c-112">Crear un directorio de Azure AD</span><span class="sxs-lookup"><span data-stu-id="12c2c-112">Create an Azure AD directory</span></span>
<span data-ttu-id="12c2c-113">toosecure su API Web realizar una copia de Azure Active Directory, debe tener un un inquilino de AAD.</span><span class="sxs-lookup"><span data-stu-id="12c2c-113">toosecure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span></span> <span data-ttu-id="12c2c-114">En este vídeo se usa un inquilino denominado **APIMDemo** .</span><span class="sxs-lookup"><span data-stu-id="12c2c-114">In this video a tenant named **APIMDemo** is used.</span></span> <span data-ttu-id="12c2c-115">toocreate un inquilino de AAD, inicio de sesión toohello [Portal clásico de Azure](https://manage.windowsazure.com) y haga clic en **New**->**servicios de aplicaciones**->**Active Directorio**->**directorio**->**creación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-115">toocreate an AAD tenant, sign-in toohello [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span></span> 

![Azure Active Directory][api-management-create-aad-menu]

<span data-ttu-id="12c2c-117">En este ejemplo, se crea un directorio denominado **APIMDemo** con un dominio predeterminado denominado **DemoAPIM.onmicrosoft.com**. Este directorio se utiliza a lo largo de vídeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c2c-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**. This directory is used throughout hello video.</span></span>

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a><span data-ttu-id="12c2c-119">Crear un servicio de API web protegido con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12c2c-119">Create a Web API service secured by Azure Active Directory</span></span>
<span data-ttu-id="12c2c-120">En este paso, se crea un back-end API Web con Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="12c2c-120">In this step, a Web API backend is created using Visual Studio 2013.</span></span> <span data-ttu-id="12c2c-121">Este paso de hello vídeo comienza en 1:30.</span><span class="sxs-lookup"><span data-stu-id="12c2c-121">This step of hello video starts at 1:30.</span></span> <span data-ttu-id="12c2c-122">proyecto de back-end de API Web toocreate en haga clic en Visual Studio **archivo**->**New**->**proyecto**y elija **Web de ASP.NET Aplicación** de hello **Web** lista de plantillas.</span><span class="sxs-lookup"><span data-stu-id="12c2c-122">toocreate Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from hello **Web** templates list.</span></span> <span data-ttu-id="12c2c-123">En este vídeo Hola se denomina proyecto **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-123">In this video hello project is named **APIMAADDemo**.</span></span> <span data-ttu-id="12c2c-124">Haga clic en **Aceptar** proyecto de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="12c2c-124">Click **OK** toocreate hello project.</span></span> 

![Visual Studio][api-management-new-web-app]

<span data-ttu-id="12c2c-126">Haga clic en **API Web** de hello **seleccionar una lista de plantilla** toocreate un proyecto de API Web.</span><span class="sxs-lookup"><span data-stu-id="12c2c-126">Click **Web API** from hello **Select a template list** toocreate a Web API project.</span></span> <span data-ttu-id="12c2c-127">Haga clic en autenticación de Azure Directory tooconfigure **Cambiar autenticación**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-127">tooconfigure Azure Directory Authentication click **Change Authentication**.</span></span>

![Nuevo proyecto][api-management-new-project]

<span data-ttu-id="12c2c-129">Haga clic en **cuentas organizativas**y especifique hello **dominio** de su inquilino de AAD.</span><span class="sxs-lookup"><span data-stu-id="12c2c-129">Click **Organizational Accounts**, and specify hello **Domain** of your AAD tenant.</span></span> <span data-ttu-id="12c2c-130">En este Hola de ejemplo es dominio **DemoAPIM.onmicrosoft.com**. dominio hello del directorio puede obtenerse de hello **dominios** pestaña del directorio.</span><span class="sxs-lookup"><span data-stu-id="12c2c-130">In this example hello domain is **DemoAPIM.onmicrosoft.com**. hello domain of your directory can be obtained from hello **Domains** tab of your directory.</span></span>

![Dominios][api-management-aad-domains]

<span data-ttu-id="12c2c-132">Configurar opciones de hello deseado en hello **Cambiar autenticación** cuadro de diálogo y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-132">Configure hello desired settings in hello **Change Authentication** dialog box and click **OK**.</span></span>

![Cambiar autenticación][api-management-change-authentication]

<span data-ttu-id="12c2c-134">Al hacer clic en **Aceptar** Visual Studio intentará tooregister la aplicación con su directorio Azure AD y es posible que toosign solicitada en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="12c2c-134">When you click **OK** Visual Studio will attempt tooregister your application with your Azure AD directory and you may be prompted toosign in by Visual Studio.</span></span> <span data-ttu-id="12c2c-135">Inicie sesión con una cuenta administrativa para el directorio.</span><span class="sxs-lookup"><span data-stu-id="12c2c-135">Sign in using an administrative account for your directory.</span></span>

![Inicie sesión en tooVisual Studio][api-management-sign-in-vidual-studio]

<span data-ttu-id="12c2c-137">cuadro de tooconfigure este proyecto como un Hola de comprobación de la API Web de Azure para **Host en la nube de hello** y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-137">tooconfigure this project as an Azure Web API check hello box for **Host in hello cloud** and then click **OK**.</span></span>

![Nuevo proyecto][api-management-new-project-cloud]

<span data-ttu-id="12c2c-139">Es posible que toosign solicitada en tooAzure y, a continuación, puede configurar Hola aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="12c2c-139">You may be prompted toosign in tooAzure, and then you can configure hello Web App.</span></span>

![Configuración][api-management-configure-web-app]

<span data-ttu-id="12c2c-141">En este ejemplo se especifica un nuevo **plan de App Service** denominado **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-141">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span></span>

<span data-ttu-id="12c2c-142">Haga clic en **Aceptar** tooconfigure Hola aplicación Web y crear el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c2c-142">Click **OK** tooconfigure hello Web App and create hello project.</span></span>

## <a name="add-hello-code-toohello-web-api-project"></a><span data-ttu-id="12c2c-143">Agregar proyecto de API Web de hello código toohello</span><span class="sxs-lookup"><span data-stu-id="12c2c-143">Add hello code toohello Web API project</span></span>
<span data-ttu-id="12c2c-144">paso siguiente de Hello en vídeo de hello agrega proyecto de API Web de hello código toohello.</span><span class="sxs-lookup"><span data-stu-id="12c2c-144">hello next step in hello video adds hello code toohello Web API project.</span></span> <span data-ttu-id="12c2c-145">Este paso empieza en 4:35.</span><span class="sxs-lookup"><span data-stu-id="12c2c-145">This step starts at 4:35.</span></span>

<span data-ttu-id="12c2c-146">Hola API Web en este ejemplo implementa un servicio de calculadora básica mediante un modelo y un controlador.</span><span class="sxs-lookup"><span data-stu-id="12c2c-146">hello Web API in this example implements a basic calculator service using a model and a controller.</span></span> <span data-ttu-id="12c2c-147">Pulse el botón derecho en el modelo de hello tooadd para el servicio de hello, **modelos** en **el Explorador de soluciones** y elija **agregar**, **clase**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-147">tooadd hello model for hello service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span></span> <span data-ttu-id="12c2c-148">Nombre de la clase hello `CalcInput` y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-148">Name hello class `CalcInput` and click **Add**.</span></span>

<span data-ttu-id="12c2c-149">Agregue Hola siguiente `using` arriba toohello de instrucción de hello `CalcInput.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="12c2c-149">Add hello following `using` statement toohello top of hello `CalcInput.cs` file.</span></span>

```c#
using Newtonsoft.Json;
```

<span data-ttu-id="12c2c-150">Reemplace clase hello generado con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="12c2c-150">Replace hello generated class with hello following code.</span></span>

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

<span data-ttu-id="12c2c-151">Haga clic con el botón derecho en **Controladores** en el **Explorador de soluciones** y elija **Agregar**->**Controlador**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-151">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span></span> <span data-ttu-id="12c2c-152">Elija **Controlador Web API 2 - Vacío** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-152">Choose **Web API 2 Controller - Empty** and click **Add**.</span></span> <span data-ttu-id="12c2c-153">Tipo de **CalcController** para hello controlador el nombre y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-153">Type **CalcController** for hello Controller name and click **Add**.</span></span>

![Agregar controlador][api-management-add-controller]

<span data-ttu-id="12c2c-155">Agregue Hola siguiente `using` arriba toohello de instrucción de hello `CalcController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="12c2c-155">Add hello following `using` statement toohello top of hello `CalcController.cs` file.</span></span>

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

<span data-ttu-id="12c2c-156">Reemplace la clase de controlador de Hola generado con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="12c2c-156">Replace hello generated controller class with hello following code.</span></span> <span data-ttu-id="12c2c-157">Este código implementa hello `Add`, `Subtract`, `Multiply`, y `Divide` las operaciones de hello API calculadora básica.</span><span class="sxs-lookup"><span data-stu-id="12c2c-157">This code implements hello `Add`, `Subtract`, `Multiply`, and `Divide` operations of hello Basic Calculator API.</span></span>

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

<span data-ttu-id="12c2c-158">Presione **F6** toobuild y compruebe la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c2c-158">Press **F6** toobuild and verify hello solution.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="12c2c-159">Publicar Hola proyecto tooAzure</span><span class="sxs-lookup"><span data-stu-id="12c2c-159">Publish hello project tooAzure</span></span>
<span data-ttu-id="12c2c-160">En este Hola paso Visual Studio proyecto es tooAzure publicado.</span><span class="sxs-lookup"><span data-stu-id="12c2c-160">In this step hello Visual Studio project is published tooAzure.</span></span> <span data-ttu-id="12c2c-161">Este paso de hello vídeo comienza en 5:45.</span><span class="sxs-lookup"><span data-stu-id="12c2c-161">This step of hello video starts at 5:45.</span></span>

<span data-ttu-id="12c2c-162">toopublish Hola tooAzure de proyecto, haga clic en hello **APIMAADDemo** proyecto en Visual Studio y elija **publicar**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-162">toopublish hello project tooAzure, right-click hello **APIMAADDemo** project in Visual Studio and choose **Publish**.</span></span> <span data-ttu-id="12c2c-163">Mantener la configuración predeterminada de Hola en hello **Publicar Web** cuadro de diálogo y haga clic en **publicar**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-163">Keep hello default settings in hello **Publish Web** dialog box and click **Publish**.</span></span>

![Publicación web][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a><span data-ttu-id="12c2c-165">Conceder permisos de aplicación de servicio de back-end de toohello Azure AD</span><span class="sxs-lookup"><span data-stu-id="12c2c-165">Grant permissions toohello Azure AD backend service application</span></span>
<span data-ttu-id="12c2c-166">Se crea una nueva aplicación de servicio de back-end de hello en su directorio de Azure AD como parte de la configuración de Hola y el proceso de publicación de su proyecto de API Web.</span><span class="sxs-lookup"><span data-stu-id="12c2c-166">A new application for hello backend service is created in your Azure AD directory as part of hello configuring and publishing process of your Web API project.</span></span> <span data-ttu-id="12c2c-167">En este paso de hello vídeo, a partir de 6:13, se conceden permisos back-end de toohello API Web.</span><span class="sxs-lookup"><span data-stu-id="12c2c-167">In this step of hello video, starting at 6:13, permissions are granted toohello Web API backend.</span></span>

![Application][api-management-aad-backend-app]

<span data-ttu-id="12c2c-169">Haga clic en el nombre de Hola de permisos de hello aplicación tooconfigure Hola necesario.</span><span class="sxs-lookup"><span data-stu-id="12c2c-169">Click hello name of hello application tooconfigure hello required permissions.</span></span> <span data-ttu-id="12c2c-170">Navegue toohello **configurar** ficha y desplácese hacia abajo toohello **permisos tooother aplicaciones** sección.</span><span class="sxs-lookup"><span data-stu-id="12c2c-170">Navigate toohello **Configure** tab and scroll down toohello **permissions tooother applications** section.</span></span> <span data-ttu-id="12c2c-171">Haga clic en hello **permisos de aplicación** lista desplegable situada junto a **Windows** **Azure Active Directory**, casilla Hola para **leer datos de directorio**y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-171">Click hello **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check hello box for **Read directory data**, and click **Save**.</span></span>

![Adición de permisos][api-management-aad-add-permissions]

> [!NOTE]
> <span data-ttu-id="12c2c-173">Si **Windows** **Azure Active Directory** no es aparecen en las aplicaciones de tooother de permisos, haga clic en **Agregar aplicación** y agréguelo desde la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c2c-173">If **Windows** **Azure Active Directory** is not listed under permissions tooother applications, click **Add application** and add it from hello list.</span></span>
> 
> 

<span data-ttu-id="12c2c-174">Tome nota de hello **App Id URI** para su uso en un paso posterior cuando se configura una aplicación de Azure AD para el portal para desarrolladores de administración de API de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c2c-174">Make a note of hello **App Id URI** for use in a subsequent step when an Azure AD application is configured for hello API Management developer portal.</span></span>

![URI de id. de aplicación][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a><span data-ttu-id="12c2c-176">Importar Hola API Web en administración de API</span><span class="sxs-lookup"><span data-stu-id="12c2c-176">Import hello Web API into API Management</span></span>
<span data-ttu-id="12c2c-177">Se configuran las API de portal para desarrolladores de API hello, que se obtiene acceso a través de hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="12c2c-177">APIs are configured from hello API publisher portal, which is accessed through hello Azure Portal.</span></span> <span data-ttu-id="12c2c-178">tooreach, haga clic en **portal para desarrolladores de** de barra de herramientas de Hola de su servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="12c2c-178">tooreach it, click **Publisher portal** from hello toolbar of your API Management service.</span></span> <span data-ttu-id="12c2c-179">Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [administrar su primera API] [ Manage your first API] tutorial.</span><span class="sxs-lookup"><span data-stu-id="12c2c-179">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API][Manage your first API] tutorial.</span></span>

![Portal del publicador][api-management-management-console]

<span data-ttu-id="12c2c-181">Las operaciones se pueden [agregado manualmente tooAPIs](api-management-howto-add-operations.md), o se pueden importar.</span><span class="sxs-lookup"><span data-stu-id="12c2c-181">Operations can be [added tooAPIs manually](api-management-howto-add-operations.md), or they can be imported.</span></span> <span data-ttu-id="12c2c-182">En este vídeo, las operaciones se importan en formato Swagger empezando en 6:40.</span><span class="sxs-lookup"><span data-stu-id="12c2c-182">In this video, operations are imported in Swagger format starting at 6:40.</span></span>

<span data-ttu-id="12c2c-183">Cree un archivo denominado `calcapi.json` con después de contenido y guárdelo tooyour equipo.</span><span class="sxs-lookup"><span data-stu-id="12c2c-183">Create a file named `calcapi.json` with following contents and save it tooyour computer.</span></span> <span data-ttu-id="12c2c-184">Asegúrese de que hello `host` atributo apunta back-end de tooyour API Web.</span><span class="sxs-lookup"><span data-stu-id="12c2c-184">Ensure that hello `host` attribute points tooyour Web API backend.</span></span> <span data-ttu-id="12c2c-185">En este ejemplo se usa `"host": "apimaaddemo.azurewebsites.net"` .</span><span class="sxs-lookup"><span data-stu-id="12c2c-185">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span></span>

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

<span data-ttu-id="12c2c-186">Calculadora de hello tooimport API, haga clic en **API** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **API de importación**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-186">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![Botón Importar API][api-management-import-api]

<span data-ttu-id="12c2c-188">Realizar Hola siguiendo los pasos tooconfigure Hola calculadora API.</span><span class="sxs-lookup"><span data-stu-id="12c2c-188">Perform hello following steps tooconfigure hello calculator API.</span></span>

1. <span data-ttu-id="12c2c-189">Haga clic en **archivo**, examinar toohello `calculator.json` archivo guardado y haga clic en hello **Swagger** botón de radio.</span><span class="sxs-lookup"><span data-stu-id="12c2c-189">Click **From file**, browse toohello `calculator.json` file you saved, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="12c2c-190">Tipo de **calc** en hello **sufijo de URL de la API de Web** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="12c2c-190">Type **calc** into hello **Web API URL suffix** textbox.</span></span>
3. <span data-ttu-id="12c2c-191">Haga clic en hello **productos (opcionales)** cuadro y elija **Starter**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-191">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="12c2c-192">Haga clic en **guardar** tooimport Hola API.</span><span class="sxs-lookup"><span data-stu-id="12c2c-192">Click **Save** tooimport hello API.</span></span>

![Add new API][api-management-import-new-api]

<span data-ttu-id="12c2c-194">Una vez que se importa la API de hello, hello página de resumen de la API de Hola se muestra en portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c2c-194">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a><span data-ttu-id="12c2c-195">Llamar a API de hello correctamente desde el portal para desarrolladores de Hola</span><span class="sxs-lookup"><span data-stu-id="12c2c-195">Call hello API unsuccessfully from hello developer portal</span></span>
<span data-ttu-id="12c2c-196">En este momento, Hola API se ha importado a la API de administración, pero no se puede aún puede llamar correctamente desde el portal para desarrolladores de hello porque el servicio de back-end de hello está protegido con autenticación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12c2c-196">At this point, hello API has been imported into API Management, but cannot yet be called successfully from hello developer portal because hello backend service is protected with Azure AD authentication.</span></span> <span data-ttu-id="12c2c-197">Esto se demuestra en vídeo de Hola a partir de 7:40 con hello pasos.</span><span class="sxs-lookup"><span data-stu-id="12c2c-197">This is demonstrated in hello video starting at 7:40 using hello following steps.</span></span>

<span data-ttu-id="12c2c-198">Haga clic en **portal para desarrolladores de** de hello parte superior derecha del portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c2c-198">Click **Developer portal** from hello top-right side of hello publisher portal.</span></span>

![portal para desarrolladores][api-management-developer-portal-menu]

<span data-ttu-id="12c2c-200">Haga clic en **API** y haga clic en hello **calculadora** API.</span><span class="sxs-lookup"><span data-stu-id="12c2c-200">Click **APIs** and click hello **Calculator** API.</span></span>

![portal para desarrolladores][api-management-dev-portal-apis]

<span data-ttu-id="12c2c-202">Haga clic en **Pruébelo**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-202">Click **Try it**.</span></span>

![Pruébelo][api-management-dev-portal-try-it]

<span data-ttu-id="12c2c-204">Haga clic en **enviar** y observe el estado de la respuesta de Hola de **401 no autorizado**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-204">Click **Send** and note hello response status of **401 Unauthorized**.</span></span>

![Los métodos Send][api-management-dev-portal-send-401]

<span data-ttu-id="12c2c-206">Hola solicitud no está autorizada porque Hola back-end API está protegido por Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="12c2c-206">hello request is unauthorized because hello backend API is protected by Azure Active Directory.</span></span> <span data-ttu-id="12c2c-207">Antes de llamar correctamente a la API de hello portal para desarrolladores de hello debe estar configurado tooauthorize a los desarrolladores mediante OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="12c2c-207">Before successfully calling hello API hello developer portal must be configured tooauthorize developers using OAuth 2.0.</span></span> <span data-ttu-id="12c2c-208">Este proceso se describe en las secciones siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c2c-208">This process is described in hello following sections.</span></span>

## <a name="register-hello-developer-portal-as-an-aad-application"></a><span data-ttu-id="12c2c-209">Registrar el portal para desarrolladores de hello como una aplicación de AAD</span><span class="sxs-lookup"><span data-stu-id="12c2c-209">Register hello developer portal as an AAD application</span></span>
<span data-ttu-id="12c2c-210">Hola primer paso para configurar Hola developer portal tooauthorize a los desarrolladores mediante OAuth 2.0 es portal para desarrolladores de tooregister hello como una aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="12c2c-210">hello first step in configuring hello developer portal tooauthorize developers using OAuth 2.0 is tooregister hello developer portal as an AAD application.</span></span> <span data-ttu-id="12c2c-211">Esto último se muestra a partir de 8:27 en vídeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c2c-211">This is demonstrated starting at 8:27 in hello video.</span></span>

<span data-ttu-id="12c2c-212">Navegar por el inquilino de Azure AD toohello desde el primer paso de este vídeo, en este ejemplo de Hola **APIMDemo** y navegue toohello **aplicaciones** ficha.</span><span class="sxs-lookup"><span data-stu-id="12c2c-212">Navigate toohello Azure AD tenant from hello first step of this video, in this example **APIMDemo** and navigate toohello **Applications** tab.</span></span>

![Nueva aplicación][api-management-aad-new-application-devportal]

<span data-ttu-id="12c2c-214">Haga clic en hello **agregar** toocreate una nueva aplicación de Azure Active Directory de botón y elija **agregar una aplicación que mi organización está desarrollando**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-214">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Nueva aplicación][api-management-new-aad-application-menu]

<span data-ttu-id="12c2c-216">Elija **Web de aplicación o Web API**, escriba un nombre y haga clic en la flecha siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="12c2c-216">Choose **Web application and/or Web API**, enter a name, and click hello next arrow.</span></span> <span data-ttu-id="12c2c-217">En este ejemplo se usa **APIMDeveloperPortal** .</span><span class="sxs-lookup"><span data-stu-id="12c2c-217">In this example **APIMDeveloperPortal** is used.</span></span>

![Nueva aplicación][api-management-aad-new-application-devportal-1]

<span data-ttu-id="12c2c-219">Para **dirección URL de inicio de sesión** escriba Hola URL de su servicio de administración de API y anexe `/signin`.</span><span class="sxs-lookup"><span data-stu-id="12c2c-219">For **Sign-on URL** enter hello URL of your API Management service and append `/signin`.</span></span> <span data-ttu-id="12c2c-220">En este ejemplo se usa `https://contoso5.portal.azure-api.net/signin` .</span><span class="sxs-lookup"><span data-stu-id="12c2c-220">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span></span>

<span data-ttu-id="12c2c-221">Para **URL de Id. de aplicación** escriba Hola URL de su servicio de administración de API y anexe algunos caracteres únicos.</span><span class="sxs-lookup"><span data-stu-id="12c2c-221">For **App Id URL** enter hello URL of your API Management service and append some unique characters.</span></span> <span data-ttu-id="12c2c-222">Puede tratarse de cualquier carácter que se desee y en este ejemplo se usa `https://contoso5.portal.azure-api.net/dp`.</span><span class="sxs-lookup"><span data-stu-id="12c2c-222">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span></span> <span data-ttu-id="12c2c-223">Cuando desea hello **propiedades de la aplicación** están configurados, haga clic en la aplicación hello de hello marca de verificación toocreate.</span><span class="sxs-lookup"><span data-stu-id="12c2c-223">When hello  desired **App properties** are configured, click hello check mark toocreate hello application.</span></span>

![Nueva aplicación][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a><span data-ttu-id="12c2c-225">Configurar un servidor de autorización OAuth 2.0 en la administración de API</span><span class="sxs-lookup"><span data-stu-id="12c2c-225">Configure an API Management OAuth 2.0 authorization server</span></span>
<span data-ttu-id="12c2c-226">Hola siguiente paso es tooconfigure un servidor de autorización de OAuth 2.0 en administración de API.</span><span class="sxs-lookup"><span data-stu-id="12c2c-226">hello next step is tooconfigure an OAuth 2.0 authorization server in API Management.</span></span> <span data-ttu-id="12c2c-227">Este paso se demuestra en hello vídeo a partir de 9:43.</span><span class="sxs-lookup"><span data-stu-id="12c2c-227">This step is demonstrated in hello video starting at 9:43.</span></span>

<span data-ttu-id="12c2c-228">Haga clic en **seguridad** Hola administración de API en menú Hola izquierda, haga clic en **OAuth 2.0**y, a continuación, haga clic en **agrega autorización** server.</span><span class="sxs-lookup"><span data-stu-id="12c2c-228">Click **Security** from hello API Management menu on hello left, click **OAuth 2.0**, and then click **Add authorization** server.</span></span>

![Agregar servidor de autorización][api-management-add-authorization-server]

<span data-ttu-id="12c2c-230">Escriba un nombre y una descripción opcional en hello **nombre** y **descripción** campos.</span><span class="sxs-lookup"><span data-stu-id="12c2c-230">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> <span data-ttu-id="12c2c-231">Estos campos son servidor de autorización de hello OAuth 2.0 tooidentify utilizados dentro de la instancia de servicio de administración de API de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c2c-231">These fields are used tooidentify hello OAuth 2.0 authorization server within hello API Management service instance.</span></span> <span data-ttu-id="12c2c-232">En este ejemplo se usa la **demostración del servidor de autorización** .</span><span class="sxs-lookup"><span data-stu-id="12c2c-232">In this example **Authorization server demo** is used.</span></span> <span data-ttu-id="12c2c-233">Más adelante al especificar un toobe de servidor de OAuth 2.0 utilizado para la autenticación de una API, seleccionará este nombre.</span><span class="sxs-lookup"><span data-stu-id="12c2c-233">Later when you specify an OAuth 2.0 server toobe used for authentication for an API, you will select this name.</span></span>

<span data-ttu-id="12c2c-234">Para hello **dirección URL de página de registro de cliente** escriba un valor de marcador de posición como `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="12c2c-234">For hello **Client registration page URL** enter a placeholder value such as `http://localhost`.</span></span>  <span data-ttu-id="12c2c-235">Hola **dirección URL de página de registro de cliente** puntos de toohello página que los usuarios pueden usar toocreate y configurar sus propias cuentas para los proveedores de OAuth 2.0 que admiten la administración de usuarios de cuentas.</span><span class="sxs-lookup"><span data-stu-id="12c2c-235">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="12c2c-236">En este ejemplo los usuarios no crean ni configuran sus propias cuentas, por lo que se usa un marcador de posición.</span><span class="sxs-lookup"><span data-stu-id="12c2c-236">In this example users do not create and configure their own accounts so a placeholder is used.</span></span>

![Agregar servidor de autorización][api-management-add-authorization-server-1]

<span data-ttu-id="12c2c-238">A continuación, especifique la **URL del punto de conexión de autorización** y la **URL del punto de conexión de token**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-238">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span></span>

![Servidor de autorización][api-management-add-authorization-server-1a]

<span data-ttu-id="12c2c-240">Estos valores se pueden recuperar de hello **extremos de la aplicación** página de aplicación de AAD que ha creado para el portal para desarrolladores de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="12c2c-240">These values can be retrieved from hello **App Endpoints** page of hello AAD application you created for hello developer portal.</span></span> <span data-ttu-id="12c2c-241">los extremos de hello tooaccess navegue toohello **configurar** pestaña aplicación AAD de hello y haga clic en **ver extremos**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-241">tooaccess hello endpoints navigate toohello **Configure** tab for hello AAD application and click **View endpoints**.</span></span>

![Application][api-management-aad-devportal-application]

![Ver extremos][api-management-aad-view-endpoints]

<span data-ttu-id="12c2c-244">Hola copia **extremo de autorización de OAuth 2.0** y péguelo en hello **dirección URL del extremo de autorización** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="12c2c-244">Copy hello **OAuth 2.0 authorization endpoint** and paste it into hello **Authorization endpoint URL** textbox.</span></span>

![Agregar servidor de autorización][api-management-add-authorization-server-2]

<span data-ttu-id="12c2c-246">Hola copia **extremo de token de OAuth 2.0** y péguelo en hello **dirección URL del extremo de Token** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="12c2c-246">Copy hello **OAuth 2.0 token endpoint** and paste it into hello **Token endpoint URL** textbox.</span></span>

![Agregar servidor de autorización][api-management-add-authorization-server-2a]

<span data-ttu-id="12c2c-248">Además toopasting en extremo de token de Hola y agregar un parámetro de cuerpo adicional denominado **recursos** y use hello para el valor de hello **App Id URI** de hello aplicación AAD para el servicio de back-end de Hola que estaba se crea cuando se publicó el proyecto de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="12c2c-248">In addition toopasting in hello token endpoint, add an additional body parameter named **resource** and for hello value use hello **App Id URI** from hello AAD application for hello backend service that was created when hello Visual Studio project was published.</span></span>

![URI de id. de aplicación][api-management-aad-sso-uri]

<span data-ttu-id="12c2c-250">A continuación, especifique las credenciales del cliente Hola.</span><span class="sxs-lookup"><span data-stu-id="12c2c-250">Next, specify hello client credentials.</span></span> <span data-ttu-id="12c2c-251">Estas son las credenciales de hello para el recurso de Hola que desee tooaccess, en este caso Hola portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="12c2c-251">These are hello credentials for hello resource you want tooaccess, in this case hello developer portal.</span></span>

![Credenciales de cliente][api-management-client-credentials]

<span data-ttu-id="12c2c-253">Hola tooget **Id. de cliente**, navegue toohello **configurar** ficha de hello aplicación AAD para Hola Hola de portal y copia de desarrollador **Id. de cliente**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-253">tooget hello **Client Id**, navigate toohello **Configure** tab of hello AAD application for hello developer portal and copy hello **Client Id**.</span></span>

<span data-ttu-id="12c2c-254">Hola tooget **secreto de cliente** haga clic en hello **seleccione duración** desplegable Hola **claves** sección y especificar un intervalo.</span><span class="sxs-lookup"><span data-stu-id="12c2c-254">tooget hello **Client Secret** click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="12c2c-255">En este ejemplo se usa el año 1.</span><span class="sxs-lookup"><span data-stu-id="12c2c-255">In this example 1 year is used.</span></span>

![id. de cliente][api-management-aad-client-id]

<span data-ttu-id="12c2c-257">Haga clic en **guardar** toosave Hola configuración y mostrar hello la clave.</span><span class="sxs-lookup"><span data-stu-id="12c2c-257">Click **Save** toosave hello configuration and display hello key.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="12c2c-258">Anote esta clave.</span><span class="sxs-lookup"><span data-stu-id="12c2c-258">Make a note of this key.</span></span> <span data-ttu-id="12c2c-259">Una vez que cierre la ventana de configuración de Azure Active Directory de hello, no se puede mostrar clave Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="12c2c-259">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

<span data-ttu-id="12c2c-260">Pegado desde el Portapapeles de toohello clave de copia hello, portal para desarrolladores de conmutador toohello atrás, clave de hello en hello **secreto de cliente** cuadro de texto y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-260">Copy hello key toohello clipboard, switch back toohello publisher portal, paste hello key into hello **Client Secret** textbox, and click **Save**.</span></span>

![Agregar servidor de autorización][api-management-add-authorization-server-3]

<span data-ttu-id="12c2c-262">Inmediatamente después de las credenciales del cliente hello es una concesión de código de autorización.</span><span class="sxs-lookup"><span data-stu-id="12c2c-262">Immediately following hello client credentials is an authorization code grant.</span></span> <span data-ttu-id="12c2c-263">Copie este código de autorización y conmutador atrás tooyour aplicación de portal de Azure AD para desarrolladores Configurar página y pegue la concesión de autorización de hello en hello **dirección URL de respuesta** campo y haga clic en **guardar** nuevo.</span><span class="sxs-lookup"><span data-stu-id="12c2c-263">Copy this authorization code and switch back tooyour Azure AD developer portal application configure page, and paste hello authorization grant into hello **Reply URL** field, and click **Save** again.</span></span>

![URL de respuesta][api-management-aad-reply-url]

<span data-ttu-id="12c2c-265">Hola siguiente paso es tooconfigure permisos de hello para el portal para desarrolladores de hello aplicación AAD.</span><span class="sxs-lookup"><span data-stu-id="12c2c-265">hello next step is tooconfigure hello permissions for hello developer portal AAD application.</span></span> <span data-ttu-id="12c2c-266">Haga clic en **permisos de aplicación** y casilla de Hola para **leer datos de directorio**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-266">Click **Application Permissions** and check hello box for **Read directory data**.</span></span> <span data-ttu-id="12c2c-267">Haga clic en **guardar** toosave esto cambiar y, a continuación, haga clic en **Agregar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-267">Click **Save** toosave this change, and then click **Add application**.</span></span>

![Adición de permisos][api-management-add-devportal-permissions]

<span data-ttu-id="12c2c-269">Haga clic en el icono de búsqueda de hello, tipo **APIM** en hello a partir de cuadro, seleccione **APIMAADDemo**y haga clic en hello toosave de marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="12c2c-269">Click hello search icon, type **APIM** into hello Starting with box, select **APIMAADDemo**, and click hello check mark toosave.</span></span>

![Adición de permisos][api-management-aad-add-app-permissions]

<span data-ttu-id="12c2c-271">Haga clic en **permisos delegados** para **APIMAADDemo** y casilla de Hola para **acceso APIMAADDemo**y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-271">Click **Delegated Permissions** for **APIMAADDemo** and check hello box for **Access APIMAADDemo**, and click **Save**.</span></span> <span data-ttu-id="12c2c-272">Esto permite al desarrollador Hola servicio back-end de aplicación de portal tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="12c2c-272">This allows hello developer portal application tooaccess hello backend service.</span></span>

![Adición de permisos][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a><span data-ttu-id="12c2c-274">Habilitar la autorización de usuario de OAuth 2.0 para hello API de calculadora</span><span class="sxs-lookup"><span data-stu-id="12c2c-274">Enable OAuth 2.0 user authorization for hello Calculator API</span></span>
<span data-ttu-id="12c2c-275">Ahora que hello OAuth 2.0 servidor está configurado, puede especificar en la configuración de seguridad de saludo de la API.</span><span class="sxs-lookup"><span data-stu-id="12c2c-275">Now that hello OAuth 2.0 server is configured, you can specify it in hello security settings for your API.</span></span> <span data-ttu-id="12c2c-276">Este paso se demuestra en hello vídeo a partir de 14:30.</span><span class="sxs-lookup"><span data-stu-id="12c2c-276">This step is demonstrated in hello video starting at 14:30.</span></span>

<span data-ttu-id="12c2c-277">Haga clic en **API** en Hola menú izquierdo y haga clic en **calculadora** tooview y configurar sus valores.</span><span class="sxs-lookup"><span data-stu-id="12c2c-277">Click **APIs** in hello left menu, and click  **Calculator** tooview and configure its settings.</span></span>

![API de calculadora][api-management-calc-api]

<span data-ttu-id="12c2c-279">Navegue toohello **seguridad** ficha, compruebe hello **OAuth 2.0** casilla de verificación, servidor de autorización deseado seleccione Hola de hello **servidor de autorización** lista desplegable y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-279">Navigate toohello **Security** tab, check hello **OAuth 2.0** checkbox, select hello desired authorization server from hello **Authorization server** drop-down, and click **Save**.</span></span>

![API de calculadora][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a><span data-ttu-id="12c2c-281">Llamar correctamente a Hola calculadora API desde portal para desarrolladores de Hola</span><span class="sxs-lookup"><span data-stu-id="12c2c-281">Successfully call hello Calculator API from hello developer portal</span></span>
<span data-ttu-id="12c2c-282">Ahora que autorización hello OAuth 2.0 está configurada en hello API, se pueden llamar correctamente sus operaciones del Centro para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c2c-282">Now that hello OAuth 2.0 authorization is configured on hello API, its operations can be successfully called from hello developer center.</span></span> <span data-ttu-id="12c2c-283">Este paso se demuestra en hello vídeo a partir de 15:00.</span><span class="sxs-lookup"><span data-stu-id="12c2c-283">THis step is demonstrated in hello video starting at 15:00.</span></span>

<span data-ttu-id="12c2c-284">Desplácese atrás toohello **agrega dos enteros** operación del servicio de calculadora de hello en el portal para desarrolladores de Hola y haga clic en **Pruébelo**.</span><span class="sxs-lookup"><span data-stu-id="12c2c-284">Navigate back toohello **Add two integers** operation of hello calculator service in hello developer portal and click **Try it**.</span></span> <span data-ttu-id="12c2c-285">Nuevo elemento de Hola de nota en hello **autorización** sección servidor de autorización toohello correspondiente que acaba de agregar.</span><span class="sxs-lookup"><span data-stu-id="12c2c-285">Note hello new item in hello **Authorization** section corresponding toohello authorization server you just added.</span></span>

![API de calculadora][api-management-calc-authorization-server]

<span data-ttu-id="12c2c-287">Seleccione **código de autorización** de autorización de hello desplegable lista y escriba las credenciales de Hola de hello cuenta toouse.</span><span class="sxs-lookup"><span data-stu-id="12c2c-287">Select **Authorization code** from hello authorization drop-down list and enter hello credentials of hello account toouse.</span></span> <span data-ttu-id="12c2c-288">Si ya inició sesión con la cuenta de hello que no se le pedirá.</span><span class="sxs-lookup"><span data-stu-id="12c2c-288">If you are already signed in with hello account you may not be prompted.</span></span>

![API de calculadora][api-management-devportal-authorization-code]

<span data-ttu-id="12c2c-290">Haga clic en **enviar** Nota hello y **estado de respuesta** de **200 Aceptar** y resultados de Hola de operación de hello en el contenido de la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c2c-290">Click **Send** and note hello **Response status** of **200 OK** and hello results of hello operation in hello response content.</span></span>

![API de calculadora][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a><span data-ttu-id="12c2c-292">Configurar un Hola de toocall API de aplicación de escritorio</span><span class="sxs-lookup"><span data-stu-id="12c2c-292">Configure a desktop application toocall hello API</span></span>
<span data-ttu-id="12c2c-293">procedimiento siguiente de Hola Hola vídeo comienza a las 16:30 y configura un hello toocall de aplicación de escritorio simple API.</span><span class="sxs-lookup"><span data-stu-id="12c2c-293">hello next procedure in hello video starts at 16:30 and configures a simple desktop application toocall hello API.</span></span> <span data-ttu-id="12c2c-294">primer paso de Hello es aplicación de escritorio de hello tooregister en Azure AD y asígnele el servicio de back-end de directorio y toohello de toohello de acceso.</span><span class="sxs-lookup"><span data-stu-id="12c2c-294">hello first step is tooregister hello desktop application in Azure AD and give it access toohello directory and toohello backend service.</span></span> <span data-ttu-id="12c2c-295">No hay una demostración de la aplicación de escritorio de hello llamar a una operación de calculadora de hello API a 18:25.</span><span class="sxs-lookup"><span data-stu-id="12c2c-295">At 18:25 there is a demonstration of hello desktop application calling an operation on hello calculator API.</span></span>

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a><span data-ttu-id="12c2c-296">Configurar una toopre de directiva de validación de JWT-autorizar las solicitudes</span><span class="sxs-lookup"><span data-stu-id="12c2c-296">Configure a JWT validation policy toopre-authorize requests</span></span>
<span data-ttu-id="12c2c-297">comienza en 20:48 Hello procedimiento final en vídeo de Hola y muestra cómo hello toouse [validar JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) toopre directiva-autorizar las solicitudes mediante la validación de tokens de acceso de Hola de cada solicitud entrante.</span><span class="sxs-lookup"><span data-stu-id="12c2c-297">hello final procedure in hello video starts at 20:48 and shows you how toouse hello [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy toopre-authorize requests by validating hello access tokens of each incoming request.</span></span> <span data-ttu-id="12c2c-298">Si Hola directiva validar JWT no valida las solicitudes de hello, solicitud de hello está bloqueado por la API de administración y no se pasa a lo largo de toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="12c2c-298">If hello request is not validated by hello Validate JWT policy, hello request is blocked by API Management and is not passed along toohello backend.</span></span>

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

<span data-ttu-id="12c2c-299">Para otra demostración de cómo configurar y usar esta directiva, consulte [177 episodio abarcan de nube: más características de administración de API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avancemos too13:50.</span><span class="sxs-lookup"><span data-stu-id="12c2c-299">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="12c2c-300">Avance rápido too15:00 las directivas de hello toosee configuradas en el editor de directiva de hello y, a continuación, too18:50 para ver una demostración de la llamada a una operación de portal para desarrolladores de hello con y sin Hola necesario token de autorización.</span><span class="sxs-lookup"><span data-stu-id="12c2c-300">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12c2c-301">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="12c2c-301">Next steps</span></span>
* <span data-ttu-id="12c2c-302">Consulte más [vídeos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) sobre la administración de API.</span><span class="sxs-lookup"><span data-stu-id="12c2c-302">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="12c2c-303">Para otro toosecure formas el servicio back-end, vea [autenticación de certificado mutua](api-management-howto-mutual-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="12c2c-303">For other ways toosecure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
