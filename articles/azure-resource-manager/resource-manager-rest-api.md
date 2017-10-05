---
title: API de REST de Resource Manager | Microsoft Docs
description: "Información general sobre la autenticación de las API de REST de Resource Manager y ejemplos de uso"
services: azure-resource-manager
documentationcenter: na
author: navalev
manager: timlt
editor: 
ms.assetid: e8d7a1d2-1e82-4212-8288-8697341408c5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: navale;tomfitz;
ms.openlocfilehash: 2f7ba23775545637de865f9ef63680ae22c62164
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="3ed92-103">API de REST de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3ed92-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ed92-104">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ed92-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="3ed92-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="3ed92-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="3ed92-106">Portal</span><span class="sxs-lookup"><span data-stu-id="3ed92-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="3ed92-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="3ed92-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="3ed92-108">Detrás de cada llamada a Azure Resource Manager, detrás de cada plantilla implementada, detrás de cada cuenta de almacenamiento configurada hay una o varias llamadas a la API de RESTful de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3ed92-108">Behind every call to Azure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls to the Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="3ed92-109">En este tema se describen estas API y cómo se les puede llamar sin usar ningún SDK.</span><span class="sxs-lookup"><span data-stu-id="3ed92-109">This topic is devoted to those APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="3ed92-110">Este planteamiento puede resultar muy útil si quiere un control total de las solicitudes realizadas en Azure, o si el SDK para su idioma preferido no está disponible o no es compatible con las operaciones que necesita.</span><span class="sxs-lookup"><span data-stu-id="3ed92-110">This approach is useful if you want full control of requests to Azure, or if the SDK for your preferred language is not available or doesn't support the operations you need.</span></span>

<span data-ttu-id="3ed92-111">En este artículo no se describen todas las API que se muestran en Azure, sino que se utilizan algunas operaciones como ejemplo de cómo conectarse a ellas.</span><span class="sxs-lookup"><span data-stu-id="3ed92-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect to them.</span></span> <span data-ttu-id="3ed92-112">Tras comprender los conceptos básicos, podrá leer el artículo [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) (Referencia de la API de REST de Azure Resource Manager) para buscar información detallada sobre cómo usar el resto de las API.</span><span class="sxs-lookup"><span data-stu-id="3ed92-112">After you understand the basics, you can read the [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) to find detailed information on how to use the rest of the APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="3ed92-113">Autenticación</span><span class="sxs-lookup"><span data-stu-id="3ed92-113">Authentication</span></span>
<span data-ttu-id="3ed92-114">La autenticación para Resource Manager se controla mediante Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="3ed92-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="3ed92-115">Para conectarse a cualquier API, primero debe autenticarse con Azure AD para recibir un token de autenticación que pueda pasar a cada solicitud.</span><span class="sxs-lookup"><span data-stu-id="3ed92-115">To connect to any API, you first need to authenticate with Azure AD to receive an authentication token that you can pass on to every request.</span></span> <span data-ttu-id="3ed92-116">Como se describe una llamada pura directamente a las API de REST, se asume que no desea autenticar por medio de una solicitud de nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="3ed92-116">As we are describing a pure call directly to the REST APIs, we assume that you don't want to authenticate by being prompted for a username and password.</span></span> <span data-ttu-id="3ed92-117">También se supone que no usa dos mecanismos de autenticación en dos fases.</span><span class="sxs-lookup"><span data-stu-id="3ed92-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="3ed92-118">Por tanto, creamos lo que se denomina una aplicación de Azure AD y una entidad de servicio que se usan para iniciar la sesión.</span><span class="sxs-lookup"><span data-stu-id="3ed92-118">Therefore, we create what is called an Azure AD Application and a service principal that are used to log in.</span></span> <span data-ttu-id="3ed92-119">Pero recuerde que Azure AD admite varios procedimientos de autenticación y todos ellos podrían usarse para recuperar el token de autenticación que se necesita para las solicitudes posteriores de API.</span><span class="sxs-lookup"><span data-stu-id="3ed92-119">But remember that Azure AD support several authentication procedures and all of them could be used to retrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="3ed92-120">Siga las instrucciones paso a paso disponibles en [Uso del portal para crear una aplicación de Active Directory y una entidad de servicio con acceso a los recursos](resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3ed92-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="3ed92-121">Generación de un token de acceso</span><span class="sxs-lookup"><span data-stu-id="3ed92-121">Generating an Access Token</span></span>
<span data-ttu-id="3ed92-122">La autenticación en Azure AD se realiza llamando a Azure AD, ubicado en login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="3ed92-122">Authentication against Azure AD is done by calling out to Azure AD, located at login.microsoftonline.com.</span></span> <span data-ttu-id="3ed92-123">Para realizar la autenticación, se necesita la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="3ed92-123">To authenticate, you need to have the following information:</span></span>

* <span data-ttu-id="3ed92-124">El identificador del inquilino de Azure AD (el nombre de Azure AD que está usando para iniciar sesión, que suele ser el mismo que el de su empresa, aunque no necesariamente)</span><span class="sxs-lookup"><span data-stu-id="3ed92-124">Azure AD Tenant ID (the name of that Azure AD you are using to log in, often the same as your company but not necessary)</span></span>
* <span data-ttu-id="3ed92-125">El identificador de la aplicación (tomado durante el paso de creación de la aplicación de Azure AD)</span><span class="sxs-lookup"><span data-stu-id="3ed92-125">Application ID (taken during the Azure AD application creation step)</span></span>
* <span data-ttu-id="3ed92-126">Contraseña (que seleccionó al crear la aplicación de Azure AD)</span><span class="sxs-lookup"><span data-stu-id="3ed92-126">Password (that you selected while creating the Azure AD Application)</span></span>

<span data-ttu-id="3ed92-127">En la siguiente solicitud HTTP, asegúrese de reemplazar "Azure AD Tenant ID" (Id. del inquilino de Azure AD), "Application ID" (Id. de aplicación) y "Password" (Contraseña) por los valores correctos.</span><span class="sxs-lookup"><span data-stu-id="3ed92-127">In the following HTTP request, make sure to replace "Azure AD Tenant ID", "Application ID" and "Password" with the correct values.</span></span>

<span data-ttu-id="3ed92-128">**Solicitud HTTP genérica:**</span><span class="sxs-lookup"><span data-stu-id="3ed92-128">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="3ed92-129">... dará como resultado (si la autenticación se realiza correctamente) una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="3ed92-129">... will (if authentication succeeds) result in a response similar to the following response:</span></span>

```json
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1448199959",
  "not_before": "1448196059",
  "resource": "https://management.core.windows.net/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhb...86U3JI_0InPUk_lZqWvKiEWsayA"
}
```
<span data-ttu-id="3ed92-130">(El elemento access_token de la respuesta anterior se ha abreviado para mejorar la legibilidad).</span><span class="sxs-lookup"><span data-stu-id="3ed92-130">(The access_token in the preceding response have been shortened to increase readability)</span></span>

<span data-ttu-id="3ed92-131">**Generación del token de acceso con Bash:**</span><span class="sxs-lookup"><span data-stu-id="3ed92-131">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="3ed92-132">**Generación del token de acceso con PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="3ed92-132">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="3ed92-133">La respuesta contiene un token de acceso, información sobre por cuánto tiempo es válido el token e información acerca de para qué recurso se puede utilizar ese token.</span><span class="sxs-lookup"><span data-stu-id="3ed92-133">The response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="3ed92-134">El token de acceso que ha recibido en la llamada HTTP anterior se debe pasar para todas las solicitudes a la API de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3ed92-134">The access token you received in the previous HTTP call must be passed in for all request to the Resource Manager API.</span></span> <span data-ttu-id="3ed92-135">Se pasa como un valor de encabezado denominado "Authorization" con el valor "Bearer YOUR_ACCESS_TOKEN".</span><span class="sxs-lookup"><span data-stu-id="3ed92-135">You pass it as a header value named "Authorization" with the value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="3ed92-136">Observe el espacio entre "Bearer" y el token de acceso.</span><span class="sxs-lookup"><span data-stu-id="3ed92-136">Notice the space between "Bearer" and your access token.</span></span>

<span data-ttu-id="3ed92-137">Como puede ver en el resultado HTTP anterior, el token es válido durante un período específico de tiempo durante el cual debe almacenar en caché y volver a usar ese mismo token.</span><span class="sxs-lookup"><span data-stu-id="3ed92-137">As you can see from the above HTTP Result, the token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="3ed92-138">Aunque es posible autenticarse en Azure AD para cada llamada de API, sería muy ineficaz.</span><span class="sxs-lookup"><span data-stu-id="3ed92-138">Even if it is possible to authenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="3ed92-139">Llamada a las API de REST de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3ed92-139">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="3ed92-140">Este tema usa solo unas pocas API para explicar el uso básico de las operaciones de REST.</span><span class="sxs-lookup"><span data-stu-id="3ed92-140">This topic only uses a few APIs to explain the basic usage of the REST operations.</span></span> <span data-ttu-id="3ed92-141">Para obtener información acerca de todas las operaciones, vea [API de REST de Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="3ed92-141">For information about all the operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="3ed92-142">Enumeración de todas las suscripciones</span><span class="sxs-lookup"><span data-stu-id="3ed92-142">List all subscriptions</span></span>
<span data-ttu-id="3ed92-143">Una de las operaciones más sencillas que se pueden realizar es enumerar las suscripciones disponibles a las que se puede acceder.</span><span class="sxs-lookup"><span data-stu-id="3ed92-143">One of the simplest operations you can do is to list the available subscriptions that you can access.</span></span> <span data-ttu-id="3ed92-144">En la siguiente solicitud puede ver cómo se pasa el token de acceso como un encabezado:</span><span class="sxs-lookup"><span data-stu-id="3ed92-144">In the following request, you see how the access token is passed in as a header:</span></span>

<span data-ttu-id="3ed92-145">(Reemplace YOUR_ACCESS_TOKEN por el token de acceso real).</span><span class="sxs-lookup"><span data-stu-id="3ed92-145">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="3ed92-146">... y como resultado, obtendrá una lista de suscripciones a las que puede acceder a esta entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="3ed92-146">... and as a result, you get a list of subscriptions that this service principal is allowed to access</span></span>

<span data-ttu-id="3ed92-147">(Los identificadores de suscripción se han abreviado para mejorar la legibilidad).</span><span class="sxs-lookup"><span data-stu-id="3ed92-147">(Subscription IDs have been shortened for readability)</span></span>

```json
{
  "value": [
    {
      "id": "/subscriptions/3a8555...555995",
      "subscriptionId": "3a8555...555995",
      "displayName": "Azure Subscription",
      "state": "Enabled",
      "subscriptionPolicies": {
        "locationPlacementId": "Internal_2014-09-01",
        "quotaId": "Internal_2014-09-01"
      }
    }
  ]
}
```

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="3ed92-148">Enumeración de todos los grupos de recursos en una suscripción específica</span><span class="sxs-lookup"><span data-stu-id="3ed92-148">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="3ed92-149">Todos los recursos disponibles con las API de Resource Manager se anidan dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3ed92-149">All resources available with the Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="3ed92-150">Puede consultar a Resource Manager los grupos de recursos existentes en su suscripción con la siguiente solicitud HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="3ed92-150">You can query Resource Manager for existing resource groups in your subscription using the following HTTP GET request.</span></span> <span data-ttu-id="3ed92-151">Observe cómo el identificador de suscripción se transmite como parte de la dirección URL de este momento.</span><span class="sxs-lookup"><span data-stu-id="3ed92-151">Notice how the subscription ID is passed in as part of the URL this time.</span></span>

<span data-ttu-id="3ed92-152">(Reemplace YOUR_ACCESS_TOKEN y SUBSCRIPTION_ID por su token de acceso e identificador de suscripción reales).</span><span class="sxs-lookup"><span data-stu-id="3ed92-152">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="3ed92-153">La respuesta que obtenga dependerá de si tiene definido algún grupo de recursos y si es así, cuántos.</span><span class="sxs-lookup"><span data-stu-id="3ed92-153">The response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="3ed92-154">(Los identificadores de suscripción se han abreviado para mejorar la legibilidad).</span><span class="sxs-lookup"><span data-stu-id="3ed92-154">(Subscription IDs have been shortened for readability)</span></span>

```json
{
    "value": [
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/myfirstresourcegroup",
            "name": "myfirstresourcegroup",
            "location": "eastus",
            "properties": {
                "provisioningState": "Succeeded"
            }
        },
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/mysecondresourcegroup",
            "name": "mysecondresourcegroup",
            "location": "northeurope",
            "tags": {
                "tagname1": "My first tag"
            },
            "properties": {
                "provisioningState": "Succeeded"
            }
        }
    ]
}
```

### <a name="create-a-resource-group"></a><span data-ttu-id="3ed92-155">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="3ed92-155">Create a resource group</span></span>
<span data-ttu-id="3ed92-156">Hasta ahora, solo hemos consultado a las API de Resource Manager para obtener información.</span><span class="sxs-lookup"><span data-stu-id="3ed92-156">So far, we've only been querying the Resource Manager APIs for information.</span></span> <span data-ttu-id="3ed92-157">Es hora de crear algunos recursos; empecemos por el más sencillo de todos ellos: un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3ed92-157">It's time we create some resources, and let's start by the simplest of them all, a resource group.</span></span> <span data-ttu-id="3ed92-158">La solicitud HTTP siguiente crea un grupo de recursos en una región o ubicación de su elección y le agrega una etiqueta.</span><span class="sxs-lookup"><span data-stu-id="3ed92-158">The following HTTP request creates a resource group in a region/location of your choice, and adds a tag to it.</span></span>

<span data-ttu-id="3ed92-159">(Reemplace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME por el token de acceso, identificador de suscripción y nombre del grupo de recursos reales que va a crear).</span><span class="sxs-lookup"><span data-stu-id="3ed92-159">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of the Resource Group you want to create)</span></span>

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  }
}
```

<span data-ttu-id="3ed92-160">Si se completa correctamente, obtendrá una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="3ed92-160">If successful, you get a response that is similar to the following response:</span></span>

```json
{
  "id": "/subscriptions/3a8555...555995/resourceGroups/RESOURCE_GROUP_NAME",
  "name": "RESOURCE_GROUP_NAME",
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  },
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<span data-ttu-id="3ed92-161">Ha creado correctamente un grupo de recursos en Azure.</span><span class="sxs-lookup"><span data-stu-id="3ed92-161">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="3ed92-162">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="3ed92-162">Congratulations!</span></span>

### <a name="deploy-resources-to-a-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="3ed92-163">Implementación de recursos en un grupo de recursos mediante una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3ed92-163">Deploy resources to a resource group using a Resource Manager Template</span></span>
<span data-ttu-id="3ed92-164">Con Resource Manager, puede implementar los recursos mediante plantillas.</span><span class="sxs-lookup"><span data-stu-id="3ed92-164">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="3ed92-165">Una plantilla define varios recursos y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="3ed92-165">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="3ed92-166">En esta sección se supone que está familiarizado con las plantillas de Resource Manager y solo le mostramos cómo realizar la llamada de API para iniciar la implementación.</span><span class="sxs-lookup"><span data-stu-id="3ed92-166">For this section, we assume you are familiar with Resource Manager templates, and we just show you how to make the API call to start deployment.</span></span> <span data-ttu-id="3ed92-167">Para obtener más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md) (Creación de plantillas de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="3ed92-167">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="3ed92-168">La implementación de una plantilla no difiere mucho del modo de llamar a otras API.</span><span class="sxs-lookup"><span data-stu-id="3ed92-168">Deployment of a template doesn't differ much to how you call other APIs.</span></span> <span data-ttu-id="3ed92-169">Un aspecto importante es que la implementación de una plantilla puede tardar bastante tiempo.</span><span class="sxs-lookup"><span data-stu-id="3ed92-169">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="3ed92-170">La llamada de la API simplemente vuelve, y es el propio desarrollador quien tiene que consultar el estado de la implementación para averiguar cuándo se ha realizado.</span><span class="sxs-lookup"><span data-stu-id="3ed92-170">The API call just returns, and it's up to you as developer to query for status of the deployment to find out when the deployment is done.</span></span> <span data-ttu-id="3ed92-171">Para obtener más información, consulte [Seguimiento de las operaciones asincrónicas de Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="3ed92-171">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="3ed92-172">En este ejemplo, se usa una plantilla publicada y disponible en [GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="3ed92-172">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="3ed92-173">Dicha plantilla implementa una máquina virtual Linux en la región Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="3ed92-173">The template we use deploys a Linux VM to the West US region.</span></span> <span data-ttu-id="3ed92-174">Aunque en este ejemplo se utiliza una plantilla disponible en un repositorio público como GitHub, también puede pasar la plantilla completa como parte de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="3ed92-174">Even though this example uses a template available in a public repository like GitHub, you can instead pass the full template as part of the request.</span></span> <span data-ttu-id="3ed92-175">Tenga en cuenta que se proporcionan valores de parámetro en la solicitud que se utilizan dentro de la plantilla implementada.</span><span class="sxs-lookup"><span data-stu-id="3ed92-175">Note that we provide parameter values in the request that are used inside the deployed template.</span></span>

<span data-ttu-id="3ed92-176">(Reemplace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME,ADMIN_PASSWORD y DNS_NAME_FOR_PUBLIC_IP por los valores pertinentes para su solicitud).</span><span class="sxs-lookup"><span data-stu-id="3ed92-176">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP to values appropriate for your request)</span></span>

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME/providers/microsoft.resources/deployments/DEPLOYMENT_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "properties": {
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json",
      "contentVersion": "1.0.0.0",
    },
    "mode": "Incremental",
    "parameters": {
        "newStorageAccountName": {
          "value": "GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME"
        },
        "adminUsername": {
          "value": "ADMIN_USER_NAME"
        },
        "adminPassword": {
          "value": "ADMIN_PASSWORD"
        },
        "dnsNameForPublicIP": {
          "value": "DNS_NAME_FOR_PUBLIC_IP"
        },
        "ubuntuOSVersion": {
          "value": "15.04"
        }
    }
  }
}
```

<span data-ttu-id="3ed92-177">La larga respuesta JSON a esta solicitud se ha omitido para mejorar la legibilidad de esta documentación.</span><span class="sxs-lookup"><span data-stu-id="3ed92-177">The long JSON response for this request has been omitted to improve readability of this documentation.</span></span> <span data-ttu-id="3ed92-178">La respuesta contiene información sobre la implementación de la plantilla que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="3ed92-178">The response contains information about the templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ed92-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3ed92-179">Next steps</span></span>

- <span data-ttu-id="3ed92-180">Para obtener información sobre el control de operaciones asincrónicas de REST, vea [Seguimiento de las operaciones asincrónicas de Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="3ed92-180">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
