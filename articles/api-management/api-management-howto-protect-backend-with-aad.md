---
title: "Protección de un back-end de API web con Azure Active Directory API Management | Microsoft Docs"
description: "Obtenga información sobre cómo proteger un back-end de API web con Azure Active Directory y la administración de API"
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
ms.openlocfilehash: 0dfb4102904c2e972e6617fd3851fb1c50147357
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-protect-a-web-api-backend-with-azure-active-directory-and-api-management"></a><span data-ttu-id="6c580-103">Cómo proteger un back-end de API web con Azure Active Directory y la administración de API</span><span class="sxs-lookup"><span data-stu-id="6c580-103">How to protect a Web API backend with Azure Active Directory and API Management</span></span>
<span data-ttu-id="6c580-104">En el vídeo siguiente se muestra cómo crear un back-end de API web cómo protegerlo mediante el protocolo OAuth 2.0 con Azure Active Directory y la administración de API.</span><span class="sxs-lookup"><span data-stu-id="6c580-104">The following video shows how to build a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span></span>  <span data-ttu-id="6c580-105">En este artículo se ofrece una introducción e información adicional de los pasos del vídeo.</span><span class="sxs-lookup"><span data-stu-id="6c580-105">This article provides an overview and additional information for the steps in the video.</span></span> <span data-ttu-id="6c580-106">Este vídeo de 24 minutos le muestra cómo:</span><span class="sxs-lookup"><span data-stu-id="6c580-106">This 24 minute video shows you how to:</span></span>

* <span data-ttu-id="6c580-107">Crear un back-end de API web y protegerlo con AAD, a partir de la 1:30</span><span class="sxs-lookup"><span data-stu-id="6c580-107">Build a Web API backend and secure it with AAD - starting at 1:30</span></span>
* <span data-ttu-id="6c580-108">Importar la API en la administración de API, a partir de las 7:10</span><span class="sxs-lookup"><span data-stu-id="6c580-108">Import the API into API Management - starting at 7:10</span></span>
* <span data-ttu-id="6c580-109">Configurar el portal para desarrolladores para llamar a la API, a partir de las 9:09</span><span class="sxs-lookup"><span data-stu-id="6c580-109">Configure the Developer portal to call the API - starting at 9:09</span></span>
* <span data-ttu-id="6c580-110">Configurar una aplicación de escritorio para llamar a la API, a partir de las 18:08</span><span class="sxs-lookup"><span data-stu-id="6c580-110">Configure a desktop application to call the API - starting at 18:08</span></span>
* <span data-ttu-id="6c580-111">Configurar una directiva de validación de JWT para autorizar previamente las solicitudes, a partir de las 20:47</span><span class="sxs-lookup"><span data-stu-id="6c580-111">Configure a JWT validation policy to pre-authorize requests - starting at 20:47</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a><span data-ttu-id="6c580-112">Crear un directorio de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c580-112">Create an Azure AD directory</span></span>
<span data-ttu-id="6c580-113">Para proteger su API web con copia de seguridad con Azure Active Directory, primero debe disponer de un inquilino de AAD.</span><span class="sxs-lookup"><span data-stu-id="6c580-113">To secure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span></span> <span data-ttu-id="6c580-114">En este vídeo se usa un inquilino denominado **APIMDemo** .</span><span class="sxs-lookup"><span data-stu-id="6c580-114">In this video a tenant named **APIMDemo** is used.</span></span> <span data-ttu-id="6c580-115">Para crear un inquilino de AAD, inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com) y haga clic en **Nuevo**->**App Services**->**Active Directory**->**Directorio**->**Creación personalizada**.</span><span class="sxs-lookup"><span data-stu-id="6c580-115">To create an AAD tenant, sign-in to the [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span></span> 

![Azure Active Directory][api-management-create-aad-menu]

<span data-ttu-id="6c580-117">En este ejemplo, se crea un directorio denominado **APIMDemo** con un dominio predeterminado denominado **DemoAPIM.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="6c580-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**.</span></span> <span data-ttu-id="6c580-118">Este directorio se usa en todo el vídeo.</span><span class="sxs-lookup"><span data-stu-id="6c580-118">This directory is used throughout the video.</span></span>

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a><span data-ttu-id="6c580-120">Crear un servicio de API web protegido con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6c580-120">Create a Web API service secured by Azure Active Directory</span></span>
<span data-ttu-id="6c580-121">En este paso, se crea un back-end API Web con Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="6c580-121">In this step, a Web API backend is created using Visual Studio 2013.</span></span> <span data-ttu-id="6c580-122">Este paso del vídeo comienza en 1:30.</span><span class="sxs-lookup"><span data-stu-id="6c580-122">This step of the video starts at 1:30.</span></span> <span data-ttu-id="6c580-123">Para crear el proyecto de back-end de API web en Visual Studio, haga clic en **Archivo**->**Nuevo**->**Proyecto** y elija **Aplicación web ASP.NET** en la lista de plantillas **Web**.</span><span class="sxs-lookup"><span data-stu-id="6c580-123">To create Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from the **Web** templates list.</span></span> <span data-ttu-id="6c580-124">En este vídeo el proyecto se denomina **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="6c580-124">In this video the project is named **APIMAADDemo**.</span></span> <span data-ttu-id="6c580-125">Haga clic en **Aceptar** para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="6c580-125">Click **OK** to create the project.</span></span> 

![Visual Studio][api-management-new-web-app]

<span data-ttu-id="6c580-127">Haga clic en **API web** en **Seleccionar una lista de plantillas** para crear un proyecto de API web.</span><span class="sxs-lookup"><span data-stu-id="6c580-127">Click **Web API** from the **Select a template list** to create a Web API project.</span></span> <span data-ttu-id="6c580-128">Para configurar la autenticación de Azure Directory haga clic en **Cambiar autenticación**.</span><span class="sxs-lookup"><span data-stu-id="6c580-128">To configure Azure Directory Authentication click **Change Authentication**.</span></span>

![Nuevo proyecto][api-management-new-project]

<span data-ttu-id="6c580-130">Haga clic en **Cuentas organizativas** y especifique el **Dominio** de su inquilino de AAD.</span><span class="sxs-lookup"><span data-stu-id="6c580-130">Click **Organizational Accounts**, and specify the **Domain** of your AAD tenant.</span></span> <span data-ttu-id="6c580-131">En este ejemplo el dominio es **DemoAPIM.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="6c580-131">In this example the domain is **DemoAPIM.onmicrosoft.com**.</span></span> <span data-ttu-id="6c580-132">El dominio del directorio se puede obtener en la pestaña **Dominios** del directorio.</span><span class="sxs-lookup"><span data-stu-id="6c580-132">The domain of your directory can be obtained from the **Domains** tab of your directory.</span></span>

![Dominios][api-management-aad-domains]

<span data-ttu-id="6c580-134">Configure las opciones que desee en el cuadro de diálogo **Cambiar autenticación** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6c580-134">Configure the desired settings in the **Change Authentication** dialog box and click **OK**.</span></span>

![Cambiar autenticación][api-management-change-authentication]

<span data-ttu-id="6c580-136">Cuando haga clic en **Aceptar** Visual Studio intentará registrar la aplicación con su directorio de Azure AD y es posible que se le pida que inicie sesión en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6c580-136">When you click **OK** Visual Studio will attempt to register your application with your Azure AD directory and you may be prompted to sign in by Visual Studio.</span></span> <span data-ttu-id="6c580-137">Inicie sesión con una cuenta administrativa para el directorio.</span><span class="sxs-lookup"><span data-stu-id="6c580-137">Sign in using an administrative account for your directory.</span></span>

![Iniciar sesión en Visual Studio][api-management-sign-in-vidual-studio]

<span data-ttu-id="6c580-139">Para configurar este proyecto como una API web de Azure, active la casilla para **Host en la nube**y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6c580-139">To configure this project as an Azure Web API check the box for **Host in the cloud** and then click **OK**.</span></span>

![Nuevo proyecto][api-management-new-project-cloud]

<span data-ttu-id="6c580-141">Puede que se le pida que inicie sesión en Azure y después podrá configurar la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="6c580-141">You may be prompted to sign in to Azure, and then you can configure the Web App.</span></span>

![Configuración][api-management-configure-web-app]

<span data-ttu-id="6c580-143">En este ejemplo se especifica un nuevo **plan de App Service** denominado **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="6c580-143">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span></span>

<span data-ttu-id="6c580-144">Haga clic en **Aceptar** para configurar la aplicación web y crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="6c580-144">Click **OK** to configure the Web App and create the project.</span></span>

## <a name="add-the-code-to-the-web-api-project"></a><span data-ttu-id="6c580-145">Agregar el código para el proyecto de API web</span><span class="sxs-lookup"><span data-stu-id="6c580-145">Add the code to the Web API project</span></span>
<span data-ttu-id="6c580-146">En el siguiente paso del vídeo se agrega el código para el proyecto de la API web.</span><span class="sxs-lookup"><span data-stu-id="6c580-146">The next step in the video adds the code to the Web API project.</span></span> <span data-ttu-id="6c580-147">Este paso empieza en 4:35.</span><span class="sxs-lookup"><span data-stu-id="6c580-147">This step starts at 4:35.</span></span>

<span data-ttu-id="6c580-148">La API web de este ejemplo implementa un servicio básico de calculadora mediante un modelo y un controlador.</span><span class="sxs-lookup"><span data-stu-id="6c580-148">The Web API in this example implements a basic calculator service using a model and a controller.</span></span> <span data-ttu-id="6c580-149">Para agregar el modelo para el servicio, haga clic con el botón derecho en **Modelos** en el **Explorador de soluciones** y elija **Agregar**, **Clase**.</span><span class="sxs-lookup"><span data-stu-id="6c580-149">To add the model for the service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span></span> <span data-ttu-id="6c580-150">Asigne un nombre a la clase `CalcInput` y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6c580-150">Name the class `CalcInput` and click **Add**.</span></span>

<span data-ttu-id="6c580-151">Agregue la siguiente instrucción `using` en la parte superior del archivo `CalcInput.cs`.</span><span class="sxs-lookup"><span data-stu-id="6c580-151">Add the following `using` statement to the top of the `CalcInput.cs` file.</span></span>

```c#
using Newtonsoft.Json;
```

<span data-ttu-id="6c580-152">Reemplace la clase generada por el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="6c580-152">Replace the generated class with the following code.</span></span>

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

<span data-ttu-id="6c580-153">Haga clic con el botón derecho en **Controladores** en el **Explorador de soluciones** y elija **Agregar**->**Controlador**.</span><span class="sxs-lookup"><span data-stu-id="6c580-153">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span></span> <span data-ttu-id="6c580-154">Elija **Controlador Web API 2 - Vacío** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6c580-154">Choose **Web API 2 Controller - Empty** and click **Add**.</span></span> <span data-ttu-id="6c580-155">Escriba **CalcController**para el controlador de nombre y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6c580-155">Type **CalcController** for the Controller name and click **Add**.</span></span>

![Agregar controlador][api-management-add-controller]

<span data-ttu-id="6c580-157">Agregue la siguiente instrucción `using` en la parte superior del archivo `CalcController.cs`.</span><span class="sxs-lookup"><span data-stu-id="6c580-157">Add the following `using` statement to the top of the `CalcController.cs` file.</span></span>

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

<span data-ttu-id="6c580-158">Reemplace la clase del controlador generada por el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="6c580-158">Replace the generated controller class with the following code.</span></span> <span data-ttu-id="6c580-159">Este código implementa las operaciones `Add`, `Subtract`, `Multiply` y `Divide` de la API de calculadora básica.</span><span class="sxs-lookup"><span data-stu-id="6c580-159">This code implements the `Add`, `Subtract`, `Multiply`, and `Divide` operations of the Basic Calculator API.</span></span>

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

<span data-ttu-id="6c580-160">Presione **F6** para crear y comprobar la solución.</span><span class="sxs-lookup"><span data-stu-id="6c580-160">Press **F6** to build and verify the solution.</span></span>

## <a name="publish-the-project-to-azure"></a><span data-ttu-id="6c580-161">Publicar el proyecto en Azure</span><span class="sxs-lookup"><span data-stu-id="6c580-161">Publish the project to Azure</span></span>
<span data-ttu-id="6c580-162">En este paso el proyecto de Visual Studio se publicará en Azure.</span><span class="sxs-lookup"><span data-stu-id="6c580-162">In this step the Visual Studio project is published to Azure.</span></span> <span data-ttu-id="6c580-163">Este paso del vídeo comienza en 5:45.</span><span class="sxs-lookup"><span data-stu-id="6c580-163">This step of the video starts at 5:45.</span></span>

<span data-ttu-id="6c580-164">Para publicar el proyecto en Azure, haga clic con el botón derecho en el proyecto **APIMAADDemo** en Visual Studio y elija **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="6c580-164">To publish the project to Azure, right-click the **APIMAADDemo** project in Visual Studio and choose **Publish**.</span></span> <span data-ttu-id="6c580-165">Mantenga la configuración predeterminada del cuadro de diálogo **Publicación web** y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="6c580-165">Keep the default settings in the **Publish Web** dialog box and click **Publish**.</span></span>

![Publicación web][api-management-web-publish]

## <a name="grant-permissions-to-the-azure-ad-backend-service-application"></a><span data-ttu-id="6c580-167">Conceder permisos a la aplicación de servicio de back-end de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c580-167">Grant permissions to the Azure AD backend service application</span></span>
<span data-ttu-id="6c580-168">Se crea una nueva aplicación para el servicio back-end en su directorio de Azure AD como parte del proceso de configuración y publicación del proyecto de API web.</span><span class="sxs-lookup"><span data-stu-id="6c580-168">A new application for the backend service is created in your Azure AD directory as part of the configuring and publishing process of your Web API project.</span></span> <span data-ttu-id="6c580-169">En este paso del vídeo, que empieza en 6:13, se conceden permisos al back-end de la API web.</span><span class="sxs-lookup"><span data-stu-id="6c580-169">In this step of the video, starting at 6:13, permissions are granted to the Web API backend.</span></span>

![Application][api-management-aad-backend-app]

<span data-ttu-id="6c580-171">Haga clic en el nombre de la aplicación para configurar los permisos necesarios.</span><span class="sxs-lookup"><span data-stu-id="6c580-171">Click the name of the application to configure the required permissions.</span></span> <span data-ttu-id="6c580-172">Navegue hasta la pestaña **Configurar** y desplácese hasta la sección **Permisos para otras aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6c580-172">Navigate to the **Configure** tab and scroll down to the **permissions to other applications** section.</span></span> <span data-ttu-id="6c580-173">Haga clic en el menú desplegable **Permisos de la aplicación** junto a **Windows** **Azure Active Directory**, active la casilla para **Leer datos de directorio** y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6c580-173">Click the **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check the box for **Read directory data**, and click **Save**.</span></span>

![Adición de permisos][api-management-aad-add-permissions]

> [!NOTE]
> <span data-ttu-id="6c580-175">Si **Windows** **Azure Active Directory** no aparece en los permisos para otras aplicaciones, haga clic en **Agregar aplicación** y agréguelo de la lista.</span><span class="sxs-lookup"><span data-stu-id="6c580-175">If **Windows** **Azure Active Directory** is not listed under permissions to other applications, click **Add application** and add it from the list.</span></span>
> 
> 

<span data-ttu-id="6c580-176">Anote el **URI de id. de aplicación** para usarlo en un paso posterior cuando se configure una aplicación de Azure AD para el portal para desarrolladores de la administración de API.</span><span class="sxs-lookup"><span data-stu-id="6c580-176">Make a note of the **App Id URI** for use in a subsequent step when an Azure AD application is configured for the API Management developer portal.</span></span>

![URI de id. de aplicación][api-management-aad-sso-uri]

## <a name="import-the-web-api-into-api-management"></a><span data-ttu-id="6c580-178">Importar la API web en la administración de API</span><span class="sxs-lookup"><span data-stu-id="6c580-178">Import the Web API into API Management</span></span>
<span data-ttu-id="6c580-179">Las API se configuran desde el portal para editores de API al que se accede a través de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6c580-179">APIs are configured from the API publisher portal, which is accessed through the Azure Portal.</span></span> <span data-ttu-id="6c580-180">Para llegar a él, haga clic en **Portal para editores** desde la barra de herramientas del servicio de API Management.</span><span class="sxs-lookup"><span data-stu-id="6c580-180">To reach it, click **Publisher portal** from the toolbar of your API Management service.</span></span> <span data-ttu-id="6c580-181">Si todavía no ha creado una instancia del servicio API Management, consulte la sección de [creación de una instancia del servicio de API Management][Create an API Management service instance] en el tutorial sobre cómo [administrar su primera API][Manage your first API].</span><span class="sxs-lookup"><span data-stu-id="6c580-181">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Manage your first API][Manage your first API] tutorial.</span></span>

![Portal del publicador][api-management-management-console]

<span data-ttu-id="6c580-183">Las operaciones se puede [agregar a las API manualmente](api-management-howto-add-operations.md)o se pueden importar.</span><span class="sxs-lookup"><span data-stu-id="6c580-183">Operations can be [added to APIs manually](api-management-howto-add-operations.md), or they can be imported.</span></span> <span data-ttu-id="6c580-184">En este vídeo, las operaciones se importan en formato Swagger empezando en 6:40.</span><span class="sxs-lookup"><span data-stu-id="6c580-184">In this video, operations are imported in Swagger format starting at 6:40.</span></span>

<span data-ttu-id="6c580-185">Cree un archivo denominado `calcapi.json` con el siguiente contenido y guárdelo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="6c580-185">Create a file named `calcapi.json` with following contents and save it to your computer.</span></span> <span data-ttu-id="6c580-186">Asegúrese de que el atributo `host` señala a su back-end de API web.</span><span class="sxs-lookup"><span data-stu-id="6c580-186">Ensure that the `host` attribute points to your Web API backend.</span></span> <span data-ttu-id="6c580-187">En este ejemplo se usa `"host": "apimaaddemo.azurewebsites.net"` .</span><span class="sxs-lookup"><span data-stu-id="6c580-187">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span></span>

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

<span data-ttu-id="6c580-188">Para importar la API de la calculadora, haga clic en **API** en el menú **Administración de API** de la izquierda y haga clic en **Importar API**.</span><span class="sxs-lookup"><span data-stu-id="6c580-188">To import the calculator API, click **APIs** from the **API Management** menu on the left, and then click **Import API**.</span></span>

![Botón Importar API][api-management-import-api]

<span data-ttu-id="6c580-190">Siga los pasos siguientes para configurar la API de la calculadora.</span><span class="sxs-lookup"><span data-stu-id="6c580-190">Perform the following steps to configure the calculator API.</span></span>

1. <span data-ttu-id="6c580-191">Haga clic en **Desde el archivo`calculator.json`, vaya al archivo** que ha guardado y haga clic en el botón de radio **Swagger**.</span><span class="sxs-lookup"><span data-stu-id="6c580-191">Click **From file**, browse to the `calculator.json` file you saved, and click the **Swagger** radio button.</span></span>
2. <span data-ttu-id="6c580-192">Escriba **calc** en el cuadro de texto **Sufijo de la dirección URL de la API web**.</span><span class="sxs-lookup"><span data-stu-id="6c580-192">Type **calc** into the **Web API URL suffix** textbox.</span></span>
3. <span data-ttu-id="6c580-193">Haga clic en el cuadro **Productos (opcional)** [Productos (opcional)] y elija **Starter**.</span><span class="sxs-lookup"><span data-stu-id="6c580-193">Click in the **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="6c580-194">Haga clic en **Guardar** para importar la API.</span><span class="sxs-lookup"><span data-stu-id="6c580-194">Click **Save** to import the API.</span></span>

![Add new API][api-management-import-new-api]

<span data-ttu-id="6c580-196">Una vez importada la API, se muestra la página de resumen de la API en el portal para editores.</span><span class="sxs-lookup"><span data-stu-id="6c580-196">Once the API is imported, the summary page for the API is displayed in the publisher portal.</span></span>

## <a name="call-the-api-unsuccessfully-from-the-developer-portal"></a><span data-ttu-id="6c580-197">Llamar a la API sin éxito desde el portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="6c580-197">Call the API unsuccessfully from the developer portal</span></span>
<span data-ttu-id="6c580-198">En este momento, la API se ha importado en la administración de API, pero no se puede llamar aún a ella correctamente desde el portal para desarrolladores porque el servicio de back-end está protegido con la autenticación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c580-198">At this point, the API has been imported into API Management, but cannot yet be called successfully from the developer portal because the backend service is protected with Azure AD authentication.</span></span> <span data-ttu-id="6c580-199">Esto se demuestra en el vídeo empezando en 7:40 mediante los pasos que se indican a continuación.</span><span class="sxs-lookup"><span data-stu-id="6c580-199">This is demonstrated in the video starting at 7:40 using the following steps.</span></span>

<span data-ttu-id="6c580-200">Haga clic en el **portal para desarrolladores** en la parte superior derecha del portal para editores.</span><span class="sxs-lookup"><span data-stu-id="6c580-200">Click **Developer portal** from the top-right side of the publisher portal.</span></span>

![portal para desarrolladores][api-management-developer-portal-menu]

<span data-ttu-id="6c580-202">Haga clic en **API** y en la API de la **Calculadora**.</span><span class="sxs-lookup"><span data-stu-id="6c580-202">Click **APIs** and click the **Calculator** API.</span></span>

![portal para desarrolladores][api-management-dev-portal-apis]

<span data-ttu-id="6c580-204">Haga clic en **Pruébelo**.</span><span class="sxs-lookup"><span data-stu-id="6c580-204">Click **Try it**.</span></span>

![Pruébelo][api-management-dev-portal-try-it]

<span data-ttu-id="6c580-206">Haga clic en **Enviar** y tenga en cuenta el estado de respuesta de **401 No autorizado**.</span><span class="sxs-lookup"><span data-stu-id="6c580-206">Click **Send** and note the response status of **401 Unauthorized**.</span></span>

![Los métodos Send][api-management-dev-portal-send-401]

<span data-ttu-id="6c580-208">La solicitud está autorizada porque la API de back-end está protegida con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6c580-208">The request is unauthorized because the backend API is protected by Azure Active Directory.</span></span> <span data-ttu-id="6c580-209">Antes de llamar correctamente a la API, el portal para desarrolladores debe configurarse para autorizar a los desarrolladores que usan OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="6c580-209">Before successfully calling the API the developer portal must be configured to authorize developers using OAuth 2.0.</span></span> <span data-ttu-id="6c580-210">Este proceso se describe en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="6c580-210">This process is described in the following sections.</span></span>

## <a name="register-the-developer-portal-as-an-aad-application"></a><span data-ttu-id="6c580-211">Registrar el portal para desarrolladores como una aplicación de AAD</span><span class="sxs-lookup"><span data-stu-id="6c580-211">Register the developer portal as an AAD application</span></span>
<span data-ttu-id="6c580-212">El primer paso en la configuración del portal para desarrolladores para autorizar a los desarrolladores a usar OAuth 2.0 es registrar el portal para desarrolladores como una aplicación de AAD.</span><span class="sxs-lookup"><span data-stu-id="6c580-212">The first step in configuring the developer portal to authorize developers using OAuth 2.0 is to register the developer portal as an AAD application.</span></span> <span data-ttu-id="6c580-213">Esto se muestra empezando en 8:27 del vídeo.</span><span class="sxs-lookup"><span data-stu-id="6c580-213">This is demonstrated starting at 8:27 in the video.</span></span>

<span data-ttu-id="6c580-214">Navegue hasta el inquilino de Azure AD desde el primer paso de este vídeo, en este ejemplo **APIMDemo** y navegue hasta la pestaña **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6c580-214">Navigate to the Azure AD tenant from the first step of this video, in this example **APIMDemo** and navigate to the **Applications** tab.</span></span>

![Nueva aplicación][api-management-aad-new-application-devportal]

<span data-ttu-id="6c580-216">Haga clic en el botón **Agregar** para crear una nueva aplicación de Azure Active Directory y, a continuación, elija **Agregar una aplicación que mi organización está desarrollando**.</span><span class="sxs-lookup"><span data-stu-id="6c580-216">Click the **Add** button to create a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Nueva aplicación][api-management-new-aad-application-menu]

<span data-ttu-id="6c580-218">Elija **Aplicación web y/o API web**, escriba un nombre y haga clic en la flecha siguiente.</span><span class="sxs-lookup"><span data-stu-id="6c580-218">Choose **Web application and/or Web API**, enter a name, and click the next arrow.</span></span> <span data-ttu-id="6c580-219">En este ejemplo se usa **APIMDeveloperPortal** .</span><span class="sxs-lookup"><span data-stu-id="6c580-219">In this example **APIMDeveloperPortal** is used.</span></span>

![Nueva aplicación][api-management-aad-new-application-devportal-1]

<span data-ttu-id="6c580-221">Para la **Dirección URL de inicio de sesión** escriba la dirección URL de su servicio API Management y anexe `/signin`.</span><span class="sxs-lookup"><span data-stu-id="6c580-221">For **Sign-on URL** enter the URL of your API Management service and append `/signin`.</span></span> <span data-ttu-id="6c580-222">En este ejemplo se usa `https://contoso5.portal.azure-api.net/signin` .</span><span class="sxs-lookup"><span data-stu-id="6c580-222">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span></span>

<span data-ttu-id="6c580-223">Para la **dirección URL de id. de aplicación** escriba la dirección URL de su servicio API Management y anexe algunos caracteres únicos.</span><span class="sxs-lookup"><span data-stu-id="6c580-223">For **App Id URL** enter the URL of your API Management service and append some unique characters.</span></span> <span data-ttu-id="6c580-224">Puede tratarse de cualquier carácter que se desee y en este ejemplo se usa `https://contoso5.portal.azure-api.net/dp`.</span><span class="sxs-lookup"><span data-stu-id="6c580-224">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span></span> <span data-ttu-id="6c580-225">Cuando se configuran las **propiedades de la aplicación** deseadas, haga clic en la marca de verificación para crear la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c580-225">When the  desired **App properties** are configured, click the check mark to create the application.</span></span>

![Nueva aplicación][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a><span data-ttu-id="6c580-227">Configurar un servidor de autorización OAuth 2.0 en la administración de API</span><span class="sxs-lookup"><span data-stu-id="6c580-227">Configure an API Management OAuth 2.0 authorization server</span></span>
<span data-ttu-id="6c580-228">El siguiente paso es configurar un servidor de autorización OAuth 2.0 en la administración de API</span><span class="sxs-lookup"><span data-stu-id="6c580-228">The next step is to configure an OAuth 2.0 authorization server in API Management.</span></span> <span data-ttu-id="6c580-229">Este paso se muestra en el vídeo a partir de 9:43.</span><span class="sxs-lookup"><span data-stu-id="6c580-229">This step is demonstrated in the video starting at 9:43.</span></span>

<span data-ttu-id="6c580-230">Haga clic en **Seguridad** en el menú API Management de la izquierda, haga clic en **OAuth 2.0** y, después, en **Agregar servidor de autorización**.</span><span class="sxs-lookup"><span data-stu-id="6c580-230">Click **Security** from the API Management menu on the left, click **OAuth 2.0**, and then click **Add authorization** server.</span></span>

![Agregar servidor de autorización][api-management-add-authorization-server]

<span data-ttu-id="6c580-232">Escriba un nombre y una descripción opcional en los campos **Nombre** y **Descripción**.</span><span class="sxs-lookup"><span data-stu-id="6c580-232">Enter a name and an optional description in the **Name** and **Description** fields.</span></span> <span data-ttu-id="6c580-233">Estos campos sirven para identificar el servidor de autorización OAuth 2.0 en la instancia del servicio Administración de API.</span><span class="sxs-lookup"><span data-stu-id="6c580-233">These fields are used to identify the OAuth 2.0 authorization server within the API Management service instance.</span></span> <span data-ttu-id="6c580-234">En este ejemplo se usa la **demostración del servidor de autorización** .</span><span class="sxs-lookup"><span data-stu-id="6c580-234">In this example **Authorization server demo** is used.</span></span> <span data-ttu-id="6c580-235">Más adelante al especificar un servidor OAuth 2.0 que se usará para la autenticación para una API, seleccionará este nombre.</span><span class="sxs-lookup"><span data-stu-id="6c580-235">Later when you specify an OAuth 2.0 server to be used for authentication for an API, you will select this name.</span></span>

<span data-ttu-id="6c580-236">Para la **URL de página de registro de cliente** escriba un valor de marcador de posición como `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="6c580-236">For the **Client registration page URL** enter a placeholder value such as `http://localhost`.</span></span>  <span data-ttu-id="6c580-237">La **URL de la página de registro de cliente** señala a la página que los usuarios pueden utilizar para crear y configurar sus propias cuentas para proveedores de OAuth 2.0 que admiten la administración de usuarios de las cuentas.</span><span class="sxs-lookup"><span data-stu-id="6c580-237">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="6c580-238">En este ejemplo los usuarios no crean ni configuran sus propias cuentas, por lo que se usa un marcador de posición.</span><span class="sxs-lookup"><span data-stu-id="6c580-238">In this example users do not create and configure their own accounts so a placeholder is used.</span></span>

![Agregar servidor de autorización][api-management-add-authorization-server-1]

<span data-ttu-id="6c580-240">A continuación, especifique la **URL del punto de conexión de autorización** y la **URL del punto de conexión de token**.</span><span class="sxs-lookup"><span data-stu-id="6c580-240">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span></span>

![Servidor de autorización][api-management-add-authorization-server-1a]

<span data-ttu-id="6c580-242">Estos valores se pueden recuperar en la página **Puntos de conexión de la aplicación** de la aplicación de AAD que creó para el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="6c580-242">These values can be retrieved from the **App Endpoints** page of the AAD application you created for the developer portal.</span></span> <span data-ttu-id="6c580-243">Para obtener acceso a los puntos de conexión navegue a la pestaña **Configurar** para la aplicación de AAD y haga clic en **Ver extremos**.</span><span class="sxs-lookup"><span data-stu-id="6c580-243">To access the endpoints navigate to the **Configure** tab for the AAD application and click **View endpoints**.</span></span>

![Application][api-management-aad-devportal-application]

![Ver extremos][api-management-aad-view-endpoints]

<span data-ttu-id="6c580-246">Copie el **punto de conexión de autorización OAuth 2.0** y péguelo en el cuadro de texto **URL del punto de conexión de autorización**.</span><span class="sxs-lookup"><span data-stu-id="6c580-246">Copy the **OAuth 2.0 authorization endpoint** and paste it into the **Authorization endpoint URL** textbox.</span></span>

![Agregar servidor de autorización][api-management-add-authorization-server-2]

<span data-ttu-id="6c580-248">Copie el **punto de conexión de token de OAuth 2.0** y péguelo en el cuadro de texto **URL del extremo de autorización**.</span><span class="sxs-lookup"><span data-stu-id="6c580-248">Copy the **OAuth 2.0 token endpoint** and paste it into the **Token endpoint URL** textbox.</span></span>

![Agregar servidor de autorización][api-management-add-authorization-server-2a]

<span data-ttu-id="6c580-250">Además de pegar el punto de conexión de token, agregue un parámetro de cuerpo adicional denominado **recurso** y para el valor use el **URI de id. de aplicación** de la aplicación de AAD para el servicio de back-end que se creó cuando se publicó el proyecto de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6c580-250">In addition to pasting in the token endpoint, add an additional body parameter named **resource** and for the value use the **App Id URI** from the AAD application for the backend service that was created when the Visual Studio project was published.</span></span>

![URI de id. de aplicación][api-management-aad-sso-uri]

<span data-ttu-id="6c580-252">A continuación, especifique las credenciales del cliente.</span><span class="sxs-lookup"><span data-stu-id="6c580-252">Next, specify the client credentials.</span></span> <span data-ttu-id="6c580-253">Estas son las credenciales para el recurso al que desea obtener acceso, en este caso, el portal de desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="6c580-253">These are the credentials for the resource you want to access, in this case the developer portal.</span></span>

![Credenciales de cliente][api-management-client-credentials]

<span data-ttu-id="6c580-255">Para obtener el **Id. de cliente**, navegue hasta la pestaña **Configurar** de la aplicación AAD para el portal de desarrolladores y copie el **Id. de cliente**.</span><span class="sxs-lookup"><span data-stu-id="6c580-255">To get the **Client Id**, navigate to the **Configure** tab of the AAD application for the developer portal and copy the **Client Id**.</span></span>

<span data-ttu-id="6c580-256">Para obtener el **Secreto de cliente** haga clic en el menú desplegable **Seleccionar duración** en la sección **Claves** y especifique un intervalo.</span><span class="sxs-lookup"><span data-stu-id="6c580-256">To get the **Client Secret** click the **Select duration** drop-down in the **Keys** section and specify an interval.</span></span> <span data-ttu-id="6c580-257">En este ejemplo se usa el año 1.</span><span class="sxs-lookup"><span data-stu-id="6c580-257">In this example 1 year is used.</span></span>

![Id. de cliente][api-management-aad-client-id]

<span data-ttu-id="6c580-259">Haga clic en **Guardar** para guardar la configuración y mostrar la clave.</span><span class="sxs-lookup"><span data-stu-id="6c580-259">Click **Save** to save the configuration and display the key.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6c580-260">Anote esta clave.</span><span class="sxs-lookup"><span data-stu-id="6c580-260">Make a note of this key.</span></span> <span data-ttu-id="6c580-261">Una vez que se cierre la ventana de configuración de Azure Active Directory, la clave no se puede mostrar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="6c580-261">Once you close the Azure Active Directory configuration window, the key cannot be displayed again.</span></span>
> 
> 

<span data-ttu-id="6c580-262">Copie la clave en el portapapeles, vuelva al portal para editores, pegue la clave en el cuadro de texto **Secreto de cliente** y haga clic en**Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6c580-262">Copy the key to the clipboard, switch back to the publisher portal, paste the key into the **Client Secret** textbox, and click **Save**.</span></span>

![Agregar servidor de autorización][api-management-add-authorization-server-3]

<span data-ttu-id="6c580-264">Inmediatamente después de las credenciales del cliente hay una concesión de código de autorización.</span><span class="sxs-lookup"><span data-stu-id="6c580-264">Immediately following the client credentials is an authorization code grant.</span></span> <span data-ttu-id="6c580-265">Copie este código de autorización y vuelva a la página de configuración de aplicación del portal para desarrolladores de Azure AD y pegue la concesión de la autorización en el campo **URL de respuesta** y haga clic en **Guardar** de nuevo.</span><span class="sxs-lookup"><span data-stu-id="6c580-265">Copy this authorization code and switch back to your Azure AD developer portal application configure page, and paste the authorization grant into the **Reply URL** field, and click **Save** again.</span></span>

![URL de respuesta][api-management-aad-reply-url]

<span data-ttu-id="6c580-267">El siguiente paso es configurar los permisos para la aplicación de AAD del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="6c580-267">The next step is to configure the permissions for the developer portal AAD application.</span></span> <span data-ttu-id="6c580-268">Haga clic en **Permisos de la aplicación** y active la casilla para **Leer datos de directorio**.</span><span class="sxs-lookup"><span data-stu-id="6c580-268">Click **Application Permissions** and check the box for **Read directory data**.</span></span> <span data-ttu-id="6c580-269">Haga clic en **Guardar** para guardar este cambios y luego haga clic en **Agregar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="6c580-269">Click **Save** to save this change, and then click **Add application**.</span></span>

![Adición de permisos][api-management-add-devportal-permissions]

<span data-ttu-id="6c580-271">Haga clic en el icono de búsqueda, escriba **APIM** en el cuadro Empezando por, seleccione **APIMAADDemo** y haga clic en la marca de verificación para guardar.</span><span class="sxs-lookup"><span data-stu-id="6c580-271">Click the search icon, type **APIM** into the Starting with box, select **APIMAADDemo**, and click the check mark to save.</span></span>

![Adición de permisos][api-management-aad-add-app-permissions]

<span data-ttu-id="6c580-273">Haga clic en **Permisos delegados** para **APIMAADDemo** y active la casilla para **acceso APIMAADDemo** y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6c580-273">Click **Delegated Permissions** for **APIMAADDemo** and check the box for **Access APIMAADDemo**, and click **Save**.</span></span> <span data-ttu-id="6c580-274">Esto permite a la aplicación del portal para desarrolladores tener acceso al servicio de back-end.</span><span class="sxs-lookup"><span data-stu-id="6c580-274">This allows the developer portal application to access the backend service.</span></span>

![Adición de permisos][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-the-calculator-api"></a><span data-ttu-id="6c580-276">Habilitar la autorización de usuario de OAuth 2.0 para la API de la calculadora</span><span class="sxs-lookup"><span data-stu-id="6c580-276">Enable OAuth 2.0 user authorization for the Calculator API</span></span>
<span data-ttu-id="6c580-277">Ahora que el servidor de OAuth 2.0 está configurado, puede especificarlo en la configuración de seguridad de la API.</span><span class="sxs-lookup"><span data-stu-id="6c580-277">Now that the OAuth 2.0 server is configured, you can specify it in the security settings for your API.</span></span> <span data-ttu-id="6c580-278">Este paso se muestra en el vídeo a partir de 14:30.</span><span class="sxs-lookup"><span data-stu-id="6c580-278">This step is demonstrated in the video starting at 14:30.</span></span>

<span data-ttu-id="6c580-279">Haga clic en **API** en el menú de la izquierda y haga clic en **Calculadora** para ver y configurar sus opciones.</span><span class="sxs-lookup"><span data-stu-id="6c580-279">Click **APIs** in the left menu, and click  **Calculator** to view and configure its settings.</span></span>

![API de calculadora][api-management-calc-api]

<span data-ttu-id="6c580-281">Navegue hasta la pestaña **Seguridad**, active la casilla **OAuth 2.0**, seleccione el servidor de autorización que desee en el menú desplegable **Servidor de autorización** y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6c580-281">Navigate to the **Security** tab, check the **OAuth 2.0** checkbox, select the desired authorization server from the **Authorization server** drop-down, and click **Save**.</span></span>

![API de calculadora][api-management-enable-aad-calculator]

## <a name="successfully-call-the-calculator-api-from-the-developer-portal"></a><span data-ttu-id="6c580-283">Llamar correctamente a la API de la Calculadora desde el portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="6c580-283">Successfully call the Calculator API from the developer portal</span></span>
<span data-ttu-id="6c580-284">Ahora que la autorización de OAuth 2.0 está configurada en la API, es posible llamar a sus operaciones correctamente desde el centro para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="6c580-284">Now that the OAuth 2.0 authorization is configured on the API, its operations can be successfully called from the developer center.</span></span> <span data-ttu-id="6c580-285">Este paso se muestra en el vídeo a partir de 15:00.</span><span class="sxs-lookup"><span data-stu-id="6c580-285">THis step is demonstrated in the video starting at 15:00.</span></span>

<span data-ttu-id="6c580-286">Regrese a la operación **Agregar dos enteros** del servicio de calculadora en el portal para desarrolladores y haga clic en **Pruébelo**.</span><span class="sxs-lookup"><span data-stu-id="6c580-286">Navigate back to the **Add two integers** operation of the calculator service in the developer portal and click **Try it**.</span></span> <span data-ttu-id="6c580-287">Tenga en cuenta el nuevo elemento de la sección **Autorización** correspondiente al servidor de autorización que acaba de agregar.</span><span class="sxs-lookup"><span data-stu-id="6c580-287">Note the new item in the **Authorization** section corresponding to the authorization server you just added.</span></span>

![API de calculadora][api-management-calc-authorization-server]

<span data-ttu-id="6c580-289">Seleccione el **Código de autorización** en la lista desplegable de autorización y escriba las credenciales de la cuenta que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="6c580-289">Select **Authorization code** from the authorization drop-down list and enter the credentials of the account to use.</span></span> <span data-ttu-id="6c580-290">Si ya ha iniciado sesión con la cuenta es posible que no se le solicite información.</span><span class="sxs-lookup"><span data-stu-id="6c580-290">If you are already signed in with the account you may not be prompted.</span></span>

![API de calculadora][api-management-devportal-authorization-code]

<span data-ttu-id="6c580-292">Haga clic en **Enviar** y tenga en cuenta el **Estado de respuesta** de **200 Aceptar** y los resultados de la operación en el contenido de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="6c580-292">Click **Send** and note the **Response status** of **200 OK** and the results of the operation in the response content.</span></span>

![API de calculadora][api-management-devportal-response]

## <a name="configure-a-desktop-application-to-call-the-api"></a><span data-ttu-id="6c580-294">Configurar una aplicación de escritorio para llamar a la API</span><span class="sxs-lookup"><span data-stu-id="6c580-294">Configure a desktop application to call the API</span></span>
<span data-ttu-id="6c580-295">El siguiente procedimiento en el vídeo empieza en 16:30 y configura una aplicación de escritorio sencilla para llamar a la API.</span><span class="sxs-lookup"><span data-stu-id="6c580-295">The next procedure in the video starts at 16:30 and configures a simple desktop application to call the API.</span></span> <span data-ttu-id="6c580-296">El primer paso es registrar la aplicación de escritorio en Azure AD y darle acceso al directorio y el servicio de back-end.</span><span class="sxs-lookup"><span data-stu-id="6c580-296">The first step is to register the desktop application in Azure AD and give it access to the directory and to the backend service.</span></span> <span data-ttu-id="6c580-297">En 18:25 hay una demostración de la aplicación de escritorio que llama a una operación en la API de la calculadora.</span><span class="sxs-lookup"><span data-stu-id="6c580-297">At 18:25 there is a demonstration of the desktop application calling an operation on the calculator API.</span></span>

## <a name="configure-a-jwt-validation-policy-to-pre-authorize-requests"></a><span data-ttu-id="6c580-298">Configurar una directiva de validación de JWT para autorizar previamente las solicitudes</span><span class="sxs-lookup"><span data-stu-id="6c580-298">Configure a JWT validation policy to pre-authorize requests</span></span>
<span data-ttu-id="6c580-299">El procedimiento final en el vídeo empieza en 20:48 y muestra cómo usar la directiva [Validar JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) para autorizar previamente las solicitudes validando los tokens de acceso de cada solicitud entrante.</span><span class="sxs-lookup"><span data-stu-id="6c580-299">The final procedure in the video starts at 20:48 and shows you how to use the [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy to pre-authorize requests by validating the access tokens of each incoming request.</span></span> <span data-ttu-id="6c580-300">Si la directiva Validar JWT no valida la solicitud, la solicitud se bloquea por la administración de API y no se pasa a lo largo del back-end.</span><span class="sxs-lookup"><span data-stu-id="6c580-300">If the request is not validated by the Validate JWT policy, the request is blocked by API Management and is not passed along to the backend.</span></span>

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

<span data-ttu-id="6c580-301">Para ver otra demostración de cómo configurar y usar esta directiva, consulte [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avance rápidamente hasta 13:50.</span><span class="sxs-lookup"><span data-stu-id="6c580-301">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="6c580-302">Avance rápidamente hasta 15:00 para ver las directivas configuradas en el editor de directivas y hasta 18:50 para ver una demostración de llamada de una operación desde el portal para desarrolladores tanto con y sin el token de autorización necesario.</span><span class="sxs-lookup"><span data-stu-id="6c580-302">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c580-303">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6c580-303">Next steps</span></span>
* <span data-ttu-id="6c580-304">Consulte más [vídeos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) sobre la administración de API.</span><span class="sxs-lookup"><span data-stu-id="6c580-304">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="6c580-305">Para conocer otras formas de proteger el servicio back-end, consulte [Autenticación de certificado mutua](api-management-howto-mutual-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="6c580-305">For other ways to secure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

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
