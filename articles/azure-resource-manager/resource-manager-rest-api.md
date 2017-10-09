---
title: aaaResource API de REST del administrador | Documentos de Microsoft
description: "Información general de hello autenticación de las API de REST del Administrador de recursos y ejemplos de uso"
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
ms.openlocfilehash: 3ccc3575c5e06c41f2fdc5317711980fc6a2f649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="38ac5-103">API de REST de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="38ac5-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="38ac5-104">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="38ac5-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="38ac5-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="38ac5-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="38ac5-106">Portal</span><span class="sxs-lookup"><span data-stu-id="38ac5-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="38ac5-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="38ac5-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="38ac5-108">Detrás de cada llamada tooAzure Administrador de recursos, detrás de cada plantilla de implementada, detrás de cada cuenta de almacenamiento configurada existen API de REST de uno o más llamadas toohello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="38ac5-108">Behind every call tooAzure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls toohello Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="38ac5-109">Este tema es toothose destinado API y cómo se puede llamar sin usar ningún SDK en absoluto.</span><span class="sxs-lookup"><span data-stu-id="38ac5-109">This topic is devoted toothose APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="38ac5-110">Este enfoque es útil si desea un control total de solicitudes tooAzure u Hola SDK para su idioma preferido no está disponible o no es compatible con operaciones de Hola que necesita.</span><span class="sxs-lookup"><span data-stu-id="38ac5-110">This approach is useful if you want full control of requests tooAzure, or if hello SDK for your preferred language is not available or doesn't support hello operations you need.</span></span>

<span data-ttu-id="38ac5-111">En este artículo no pasa por todas las API que se expone en Azure, sino que usa algunas operaciones como ejemplos de cómo conectar toothem.</span><span class="sxs-lookup"><span data-stu-id="38ac5-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect toothem.</span></span> <span data-ttu-id="38ac5-112">Una vez que comprenda los conceptos básicos de hello, puede leer hello [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) toofind información detallada sobre cómo rest de hello toouse de Hola API.</span><span class="sxs-lookup"><span data-stu-id="38ac5-112">After you understand hello basics, you can read hello [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) toofind detailed information on how toouse hello rest of hello APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="38ac5-113">Autenticación</span><span class="sxs-lookup"><span data-stu-id="38ac5-113">Authentication</span></span>
<span data-ttu-id="38ac5-114">La autenticación para Resource Manager se controla mediante Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="38ac5-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="38ac5-115">tooconnect tooany API, primero debe tooauthenticate con Azure AD tooreceive un token de autenticación que se puede pasar en tooevery solicitud.</span><span class="sxs-lookup"><span data-stu-id="38ac5-115">tooconnect tooany API, you first need tooauthenticate with Azure AD tooreceive an authentication token that you can pass on tooevery request.</span></span> <span data-ttu-id="38ac5-116">Como describimos una llamada pura directamente toohello las API de REST, suponemos que no quiere tooauthenticate, que se le pida un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="38ac5-116">As we are describing a pure call directly toohello REST APIs, we assume that you don't want tooauthenticate by being prompted for a username and password.</span></span> <span data-ttu-id="38ac5-117">También se supone que no usa dos mecanismos de autenticación en dos fases.</span><span class="sxs-lookup"><span data-stu-id="38ac5-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="38ac5-118">Por lo tanto, creamos lo que se conoce como una aplicación de Azure AD y una entidad de servicio que son toolog usado en.</span><span class="sxs-lookup"><span data-stu-id="38ac5-118">Therefore, we create what is called an Azure AD Application and a service principal that are used toolog in.</span></span> <span data-ttu-id="38ac5-119">Pero recuerde que Azure AD admite varios procedimientos de autenticación y todas ellas podría ser tooretrieve usa ese token de autenticación que necesitamos para las solicitudes posteriores de API.</span><span class="sxs-lookup"><span data-stu-id="38ac5-119">But remember that Azure AD support several authentication procedures and all of them could be used tooretrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="38ac5-120">Siga las instrucciones paso a paso disponibles en [Uso del portal para crear una aplicación de Active Directory y una entidad de servicio con acceso a los recursos](resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="38ac5-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="38ac5-121">Generación de un token de acceso</span><span class="sxs-lookup"><span data-stu-id="38ac5-121">Generating an Access Token</span></span>
<span data-ttu-id="38ac5-122">Autenticación en Azure AD se realiza llamando al exterior tooAzure AD, ubicado en login.microsoftonline.com. tooauthenticate, necesita hello toohave siguiente información:</span><span class="sxs-lookup"><span data-stu-id="38ac5-122">Authentication against Azure AD is done by calling out tooAzure AD, located at login.microsoftonline.com. tooauthenticate, you need toohave hello following information:</span></span>

* <span data-ttu-id="38ac5-123">Id. de inquilino de Azure AD (Hola nombre de que Azure AD que usa toolog en, a menudo Hola igual que su empresa, pero no es necesario)</span><span class="sxs-lookup"><span data-stu-id="38ac5-123">Azure AD Tenant ID (hello name of that Azure AD you are using toolog in, often hello same as your company but not necessary)</span></span>
* <span data-ttu-id="38ac5-124">Identificador de la aplicación (realizada durante el paso de creación de la aplicación hello Azure AD)</span><span class="sxs-lookup"><span data-stu-id="38ac5-124">Application ID (taken during hello Azure AD application creation step)</span></span>
* <span data-ttu-id="38ac5-125">Contraseña (que seleccionó durante la creación de hello aplicación de Azure AD)</span><span class="sxs-lookup"><span data-stu-id="38ac5-125">Password (that you selected while creating hello Azure AD Application)</span></span>

<span data-ttu-id="38ac5-126">Hola después de la solicitud HTTP, asegúrese de tooreplace seguro "Identificador de inquilino de Azure AD," "Id. de aplicación" y "Contraseña" con los valores correctos de Hola.</span><span class="sxs-lookup"><span data-stu-id="38ac5-126">In hello following HTTP request, make sure tooreplace "Azure AD Tenant ID", "Application ID" and "Password" with hello correct values.</span></span>

<span data-ttu-id="38ac5-127">**Solicitud HTTP genérica:**</span><span class="sxs-lookup"><span data-stu-id="38ac5-127">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="38ac5-128">... will (si la autenticación se realiza correctamente) como resultado un toohello similar de respuesta después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="38ac5-128">... will (if authentication succeeds) result in a response similar toohello following response:</span></span>

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
<span data-ttu-id="38ac5-129">(access_token Hola Hola anterior respuesta ha sido tooincrease abreviado legibilidad)</span><span class="sxs-lookup"><span data-stu-id="38ac5-129">(hello access_token in hello preceding response have been shortened tooincrease readability)</span></span>

<span data-ttu-id="38ac5-130">**Generación del token de acceso con Bash:**</span><span class="sxs-lookup"><span data-stu-id="38ac5-130">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="38ac5-131">**Generación del token de acceso con PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="38ac5-131">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="38ac5-132">respuesta de Hello contiene un token de acceso, la información sobre cuánto tiempo ese token es válido y la información sobre qué recursos puede usar ese token para.</span><span class="sxs-lookup"><span data-stu-id="38ac5-132">hello response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="38ac5-133">token de acceso de Hola que recibiste por llamada HTTP anterior Hola debe pasarse en para todos los toohello de solicitud API del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="38ac5-133">hello access token you received in hello previous HTTP call must be passed in for all request toohello Resource Manager API.</span></span> <span data-ttu-id="38ac5-134">Pasa dicho valor como un valor de encabezado denominado "Autorización" con el valor de Hola "Portador YOUR_ACCESS_TOKEN".</span><span class="sxs-lookup"><span data-stu-id="38ac5-134">You pass it as a header value named "Authorization" with hello value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="38ac5-135">Observe el espacio de hello entre "Portador" y el token de acceso.</span><span class="sxs-lookup"><span data-stu-id="38ac5-135">Notice hello space between "Bearer" and your access token.</span></span>

<span data-ttu-id="38ac5-136">Como puede ver de Hola por encima del resultado de HTTP, el token de hello es válido durante un período de tiempo durante el cual se debe almacenar en caché y volver a ese mismo token específico.</span><span class="sxs-lookup"><span data-stu-id="38ac5-136">As you can see from hello above HTTP Result, hello token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="38ac5-137">Aunque es posible tooauthenticate en Azure AD para cada llamada API, sería muy ineficiente.</span><span class="sxs-lookup"><span data-stu-id="38ac5-137">Even if it is possible tooauthenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="38ac5-138">Llamada a las API de REST de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="38ac5-138">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="38ac5-139">Este tema utiliza sólo algunas API tooexplain Hola uso básico de operaciones de REST de Hola.</span><span class="sxs-lookup"><span data-stu-id="38ac5-139">This topic only uses a few APIs tooexplain hello basic usage of hello REST operations.</span></span> <span data-ttu-id="38ac5-140">Para obtener información acerca de todas las operaciones de hello, consulte [API de REST del Administrador de recursos de Azure](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="38ac5-140">For information about all hello operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="38ac5-141">Enumeración de todas las suscripciones</span><span class="sxs-lookup"><span data-stu-id="38ac5-141">List all subscriptions</span></span>
<span data-ttu-id="38ac5-142">Uno de operaciones más sencillas de hello que puede realizar es toolist Hola disponibles las suscripciones que pueda tener acceso.</span><span class="sxs-lookup"><span data-stu-id="38ac5-142">One of hello simplest operations you can do is toolist hello available subscriptions that you can access.</span></span> <span data-ttu-id="38ac5-143">Hola después de la solicitud, verá cómo se pasa el token de acceso de Hola como un encabezado:</span><span class="sxs-lookup"><span data-stu-id="38ac5-143">In hello following request, you see how hello access token is passed in as a header:</span></span>

<span data-ttu-id="38ac5-144">(Reemplace YOUR_ACCESS_TOKEN por el token de acceso real).</span><span class="sxs-lookup"><span data-stu-id="38ac5-144">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="38ac5-145">... y como resultado, obtendrá una lista de suscripciones que esta entidad de servicio se permite tooaccess</span><span class="sxs-lookup"><span data-stu-id="38ac5-145">... and as a result, you get a list of subscriptions that this service principal is allowed tooaccess</span></span>

<span data-ttu-id="38ac5-146">(Los identificadores de suscripción se han abreviado para mejorar la legibilidad).</span><span class="sxs-lookup"><span data-stu-id="38ac5-146">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="38ac5-147">Enumeración de todos los grupos de recursos en una suscripción específica</span><span class="sxs-lookup"><span data-stu-id="38ac5-147">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="38ac5-148">Todos los recursos disponibles con las API del Administrador de recursos de hello están anidados dentro de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="38ac5-148">All resources available with hello Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="38ac5-149">Puede consultar el Administrador de recursos para los grupos de recursos existentes en su suscripción mediante Hola después de la solicitud HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="38ac5-149">You can query Resource Manager for existing resource groups in your subscription using hello following HTTP GET request.</span></span> <span data-ttu-id="38ac5-150">Tenga en cuenta cómo Id. de suscripción de Hola se pasa como parte de la dirección URL de hello este momento.</span><span class="sxs-lookup"><span data-stu-id="38ac5-150">Notice how hello subscription ID is passed in as part of hello URL this time.</span></span>

<span data-ttu-id="38ac5-151">(Reemplace YOUR_ACCESS_TOKEN y SUBSCRIPTION_ID por su token de acceso e identificador de suscripción reales).</span><span class="sxs-lookup"><span data-stu-id="38ac5-151">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="38ac5-152">Hello respuesta obtendrá depende de si tiene algún grupo de recursos definido y si es así, ¿cuántos.</span><span class="sxs-lookup"><span data-stu-id="38ac5-152">hello response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="38ac5-153">(Los identificadores de suscripción se han abreviado para mejorar la legibilidad).</span><span class="sxs-lookup"><span data-stu-id="38ac5-153">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="create-a-resource-group"></a><span data-ttu-id="38ac5-154">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="38ac5-154">Create a resource group</span></span>
<span data-ttu-id="38ac5-155">Hasta ahora, nos hemos solo ha consultar Hola API del Administrador de recursos para obtener información.</span><span class="sxs-lookup"><span data-stu-id="38ac5-155">So far, we've only been querying hello Resource Manager APIs for information.</span></span> <span data-ttu-id="38ac5-156">Es hora de crear algunos recursos y Empecemos por hello más simple de todos ellos, un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="38ac5-156">It's time we create some resources, and let's start by hello simplest of them all, a resource group.</span></span> <span data-ttu-id="38ac5-157">Hola solicitud HTTP siguiente crea un grupo de recursos en una región o ubicación de su elección y agrega una etiqueta tooit.</span><span class="sxs-lookup"><span data-stu-id="38ac5-157">hello following HTTP request creates a resource group in a region/location of your choice, and adds a tag tooit.</span></span>

<span data-ttu-id="38ac5-158">(Reemplace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME por su real del Token de acceso, Id. de suscripción y nombre del grupo de recursos que desee toocreate Hola)</span><span class="sxs-lookup"><span data-stu-id="38ac5-158">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of hello Resource Group you want toocreate)</span></span>

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

<span data-ttu-id="38ac5-159">Si se realiza correctamente, obtendrá una respuesta similar toohello después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="38ac5-159">If successful, you get a response that is similar toohello following response:</span></span>

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

<span data-ttu-id="38ac5-160">Ha creado correctamente un grupo de recursos en Azure.</span><span class="sxs-lookup"><span data-stu-id="38ac5-160">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="38ac5-161">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="38ac5-161">Congratulations!</span></span>

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="38ac5-162">Implementar grupo de recursos de tooa de recursos utilizando una plantilla de administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="38ac5-162">Deploy resources tooa resource group using a Resource Manager Template</span></span>
<span data-ttu-id="38ac5-163">Con Resource Manager, puede implementar los recursos mediante plantillas.</span><span class="sxs-lookup"><span data-stu-id="38ac5-163">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="38ac5-164">Una plantilla define varios recursos y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="38ac5-164">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="38ac5-165">En esta sección se supone está familiarizado con las plantillas de administrador de recursos y simplemente le mostraremos cómo toomake Hola API llamar a la implementación de toostart.</span><span class="sxs-lookup"><span data-stu-id="38ac5-165">For this section, we assume you are familiar with Resource Manager templates, and we just show you how toomake hello API call toostart deployment.</span></span> <span data-ttu-id="38ac5-166">Para obtener más información sobre la creación de plantillas, consulte [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md) (Creación de plantillas de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="38ac5-166">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="38ac5-167">Implementación de una plantilla no difieren mucho toohow llamar a otras API.</span><span class="sxs-lookup"><span data-stu-id="38ac5-167">Deployment of a template doesn't differ much toohow you call other APIs.</span></span> <span data-ttu-id="38ac5-168">Un aspecto importante es que la implementación de una plantilla puede tardar bastante tiempo.</span><span class="sxs-lookup"><span data-stu-id="38ac5-168">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="38ac5-169">simplemente devuelve la llamada de API de Hola y es una tooyou como tooquery de desarrollador para estado de hello implementación toofind espera cuando se realice la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="38ac5-169">hello API call just returns, and it's up tooyou as developer tooquery for status of hello deployment toofind out when hello deployment is done.</span></span> <span data-ttu-id="38ac5-170">Para obtener más información, consulte [Seguimiento de las operaciones asincrónicas de Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="38ac5-170">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="38ac5-171">En este ejemplo, se usa una plantilla publicada y disponible en [GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="38ac5-171">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="38ac5-172">plantilla de Hello que usamos implementa una región de VM de Linux toohello oeste de Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="38ac5-172">hello template we use deploys a Linux VM toohello West US region.</span></span> <span data-ttu-id="38ac5-173">Aunque este ejemplo usa una plantilla disponible en un repositorio público como GitHub, puede pasar en su lugar plantilla completa hello como parte de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="38ac5-173">Even though this example uses a template available in a public repository like GitHub, you can instead pass hello full template as part of hello request.</span></span> <span data-ttu-id="38ac5-174">Tenga en cuenta que se proporcionan valores de parámetro de solicitud de Hola que se utilizan dentro de hello implementa la plantilla.</span><span class="sxs-lookup"><span data-stu-id="38ac5-174">Note that we provide parameter values in hello request that are used inside hello deployed template.</span></span>

<span data-ttu-id="38ac5-175">(Reemplace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD y DNS_NAME_FOR_PUBLIC_IP toovalues adecuado para su solicitud)</span><span class="sxs-lookup"><span data-stu-id="38ac5-175">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP toovalues appropriate for your request)</span></span>

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

<span data-ttu-id="38ac5-176">respuesta JSON largos de Hola para esta solicitud ha sido omitido tooimprove facilitar la lectura de esta documentación.</span><span class="sxs-lookup"><span data-stu-id="38ac5-176">hello long JSON response for this request has been omitted tooimprove readability of this documentation.</span></span> <span data-ttu-id="38ac5-177">respuesta de Hello contiene información acerca de la implementación de plantillas de Hola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="38ac5-177">hello response contains information about hello templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38ac5-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="38ac5-178">Next steps</span></span>

- <span data-ttu-id="38ac5-179">toolearn sobre el control de operaciones asincrónicas de REST, consulte [realizar un seguimiento de las operaciones asincrónicas de Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="38ac5-179">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
