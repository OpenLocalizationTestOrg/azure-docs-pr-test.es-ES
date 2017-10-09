---
title: aaaAuthenticate con las API de REST de Mobile Engagement
description: "Describe cómo tooauthenticate con API de REST de Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a><span data-ttu-id="c4576-103">Autenticación con las API de REST de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c4576-103">Authenticate with Mobile Engagement REST APIs</span></span>
## <a name="overview"></a><span data-ttu-id="c4576-104">Información general</span><span class="sxs-lookup"><span data-stu-id="c4576-104">Overview</span></span>
<span data-ttu-id="c4576-105">Este documento describe cómo tooget un Oauth de AAD válido token tooauthenticate con hello las API de REST de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="c4576-105">This document describes how tooget a valid AAD Oauth token tooauthenticate with hello Mobile Engagement REST APIs.</span></span> 

<span data-ttu-id="c4576-106">Se supone que tiene una suscripción válida a Azure y que ha creado una aplicación de Mobile Engagement con uno de nuestros [tutoriales para desarrolladores](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c4576-106">It is assumed that you have a valid Azure subscription and you have created a Mobile Engagement app using one of our [Developer Tutorials](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="c4576-107">Autenticación</span><span class="sxs-lookup"><span data-stu-id="c4576-107">Authentication</span></span>
<span data-ttu-id="c4576-108">Se usa un token de OAuth basado en Microsoft Azure Active Directory para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="c4576-108">A Microsoft Azure Active Directory based OAuth token is used for authentication.</span></span> 

<span data-ttu-id="c4576-109">En la solicitud de pedido de tooauthentication una API, un encabezado de autorización debe agregarse solicitud tooevery que es de hello siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="c4576-109">In order tooauthentication an API request, an authorization header must be added tooevery request which is of hello following form:</span></span>

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> <span data-ttu-id="c4576-110">Los tokens de Azure Active Directory caducan en 1 hora.</span><span class="sxs-lookup"><span data-stu-id="c4576-110">Azure Active Directory tokens expire in 1 hour.</span></span>
> 
> 

<span data-ttu-id="c4576-111">Hay varias tooget formas un token.</span><span class="sxs-lookup"><span data-stu-id="c4576-111">There are several ways tooget a token.</span></span> <span data-ttu-id="c4576-112">Desde Hola que suele llamar a las API de un servicio de nube que desee toouse una clave de API.</span><span class="sxs-lookup"><span data-stu-id="c4576-112">Since hello APIs are generally called from a cloud service, you want toouse an API key.</span></span> <span data-ttu-id="c4576-113">En la terminología de Azure, a una clave de API se la conoce como contraseña de entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="c4576-113">An API key in Azure terminology is called a Service principal password.</span></span> <span data-ttu-id="c4576-114">Hello siguiente procedimiento describe una manera de toosetting una copia de seguridad manualmente.</span><span class="sxs-lookup"><span data-stu-id="c4576-114">hello following procedure describes one way toosetting it up manually.</span></span>

### <a name="one-time-setup-using-script"></a><span data-ttu-id="c4576-115">Instalación única (mediante script)</span><span class="sxs-lookup"><span data-stu-id="c4576-115">One-time setup (using script)</span></span>
<span data-ttu-id="c4576-116">Conjunto de Hola de instrucciones que aparecen debajo de la instalación de hello tooperform mediante un script de PowerShell que lleva tiempo mínimo de hello para el programa de instalación, pero utiliza valores predeterminados más admisibles de hello debe seguir.</span><span class="sxs-lookup"><span data-stu-id="c4576-116">You should follow hello set of instructions below tooperform hello setup using a PowerShell script which takes hello minimum time for setup but uses hello most permissible defaults.</span></span> <span data-ttu-id="c4576-117">Si lo desea, también puede seguir las instrucciones de Hola Hola [el programa de instalación manual](mobile-engagement-api-authentication-manual.md) para hacer esto desde Hola directamente portal de Azure y la configuración más preciso de.</span><span class="sxs-lookup"><span data-stu-id="c4576-117">Optionally, you can also follow hello instructions in hello [manual setup](mobile-engagement-api-authentication-manual.md) for doing this from hello Azure portal directly and do finer configuration.</span></span> 

1. <span data-ttu-id="c4576-118">Obtener la versión más reciente de Hola de PowerShell de Azure desde [aquí](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="c4576-118">Get hello latest version of Azure PowerShell from [here](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="c4576-119">Para obtener más información sobre las instrucciones de descarga de hello, puede ver esto [vínculo](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c4576-119">For more information on hello download instructions, you can see this [link](/powershell/azure/overview).</span></span>  
2. <span data-ttu-id="c4576-120">Una vez instalado Azure PowerShell, siguiente Hola de uso comandos tooensure que tengan hello **módulo de Azure** instalado:</span><span class="sxs-lookup"><span data-stu-id="c4576-120">Once Azure PowerShell is installed, use hello following commands tooensure that you have hello **Azure module** installed:</span></span>
   
    <span data-ttu-id="c4576-121">a.</span><span class="sxs-lookup"><span data-stu-id="c4576-121">a.</span></span> <span data-ttu-id="c4576-122">Asegúrese de que el módulo de Azure PowerShell Hola está disponible en la lista Hola de los módulos disponibles.</span><span class="sxs-lookup"><span data-stu-id="c4576-122">Make sure hello Azure PowerShell module is available in hello list of available modules.</span></span> 
   
        Get-Module –ListAvailable 
   
    ![Módulos de Azure disponibles][1]
   
    <span data-ttu-id="c4576-124">b.</span><span class="sxs-lookup"><span data-stu-id="c4576-124">b.</span></span> <span data-ttu-id="c4576-125">Si no encontró el módulo de PowerShell de Azure de Hola Hola por encima de la lista, a continuación, necesita toorun Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="c4576-125">If you do not find hello Azure PowerShell module in hello above list then you need toorun hello following:</span></span>
   
        Import-Module Azure 
3. <span data-ttu-id="c4576-126">Inicio de sesión toohello Azure Resource Manager desde PowerShell mediante la ejecución de Hola siguiente comando y proporcionar su nombre de usuario y contraseña para su cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="c4576-126">Login toohello Azure Resource Manager from PowerShell by running hello following command and providing your user name and password for your Azure account:</span></span> 
   
        Login-AzureRmAccount
4. <span data-ttu-id="c4576-127">Si tiene varias suscripciones, a continuación, se deben ejecutar siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="c4576-127">If you have multiple subscriptions then you should run hello following:</span></span>
   
    <span data-ttu-id="c4576-128">a.</span><span class="sxs-lookup"><span data-stu-id="c4576-128">a.</span></span> <span data-ttu-id="c4576-129">Obtener una lista de todas las suscripciones y Hola copia SubscriptionId de suscripción de hello que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="c4576-129">Get a list of all your subscriptions and copy hello SubscriptionId of hello subscription you want toouse.</span></span> <span data-ttu-id="c4576-130">Asegúrese de que esta suscripción es igual a uno que tenga Hola aplicación de interacción móvil que va de hello toointeract con el uso de las API de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4576-130">Make sure this subscription is hello same one which has hello Mobile Engagement App which you are going toointeract with using hello APIs.</span></span> 
   
        Get-AzureRmSubscription
   
    <span data-ttu-id="c4576-131">b.</span><span class="sxs-lookup"><span data-stu-id="c4576-131">b.</span></span> <span data-ttu-id="c4576-132">Siguiente ejecución Hola comando proporcionando Hola SubscriptionId tooconfigure Hola suscripción toobe usa.</span><span class="sxs-lookup"><span data-stu-id="c4576-132">Run hello following command providing hello SubscriptionId tooconfigure hello subscription toobe used.</span></span>
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. <span data-ttu-id="c4576-133">Copiar texto de Hola de hello [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) equipo local tooyour de script y guárdelo como un cmdlet de PowerShell (p. ej. `APIAuth.ps1`) y lo ejecuta `.\APIAuth.ps1`.</span><span class="sxs-lookup"><span data-stu-id="c4576-133">Copy hello text for hello [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script tooyour local machine and save it as a PowerShell cmdlet (e.g. `APIAuth.ps1`) and execute it `.\APIAuth.ps1`.</span></span> 
6. <span data-ttu-id="c4576-134">Hello script le pedirá que tooprovide una entrada de **principalName**.</span><span class="sxs-lookup"><span data-stu-id="c4576-134">hello script will ask you tooprovide an input for **principalName**.</span></span> <span data-ttu-id="c4576-135">Proporcionar un nombre adecuado que desea toouse toocreate la aplicación de Active Directory (por ejemplo, APIAuth).</span><span class="sxs-lookup"><span data-stu-id="c4576-135">Provide a suitable name here that you want toouse toocreate your Active Directory application (e.g. APIAuth).</span></span> 
7. <span data-ttu-id="c4576-136">Una vez completado el script de Hola, mostrará Hola después de cuatro valores que necesitará tooauthenticate mediante programación con AD, así que haga toocopy seguro de ellos.</span><span class="sxs-lookup"><span data-stu-id="c4576-136">After hello script completes, it will display hello following four values that you will need tooauthenticate programmatically with AD so make sure toocopy them.</span></span> 
   
    <span data-ttu-id="c4576-137">**TenantId**, **SubscriptionId**, **ApplicationId** y **Secret**.</span><span class="sxs-lookup"><span data-stu-id="c4576-137">**TenantId**, **SubscriptionId**, **ApplicationId**, and **Secret**.</span></span>
   
    <span data-ttu-id="c4576-138">Usará TenantId como `{TENANT_ID}`, ApplicationId como `{CLIENT_ID}` y Secret como `{CLIENT_SECRET}`.</span><span class="sxs-lookup"><span data-stu-id="c4576-138">You will use TenantId as `{TENANT_ID}`, ApplicationId as `{CLIENT_ID}` and Secret as `{CLIENT_SECRET}`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c4576-139">Es posible que la directiva de seguridad predeterminada le impida ejecutar scripts de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4576-139">Your default security policy may block you from running a PowerShell scripts.</span></span> <span data-ttu-id="c4576-140">Si es así, configure temporalmente la ejecución de secuencia de comandos tooallow de la directiva de ejecución mediante el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="c4576-140">If so, you temporarily configure your execution policy tooallow script execution using hello following command:</span></span>
   > 
   > <span data-ttu-id="c4576-141">Set-ExecutionPolicy RemoteSigned</span><span class="sxs-lookup"><span data-stu-id="c4576-141">Set-ExecutionPolicy RemoteSigned</span></span>
   > 
   > 
8. <span data-ttu-id="c4576-142">Este es el aspecto que tendría el conjunto de cmdlets de PS de hello como.</span><span class="sxs-lookup"><span data-stu-id="c4576-142">Here is how hello set of PS cmdlets would look like.</span></span> 
   
    ![][3]
9. <span data-ttu-id="c4576-143">Compruebe en el portal de administración de Azure de Hola que una nueva aplicación de AD se creó con el nombre de Hola siempre toohello script llama **principalName** en **mostrar aplicaciones que tiene mi compañía**.</span><span class="sxs-lookup"><span data-stu-id="c4576-143">Check in hello Azure Management portal that a new AD application was created with hello name you provided toohello script called **principalName** under **Show Applications my company owns**.</span></span>
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a><span data-ttu-id="c4576-144">Pasos tooget un token válido</span><span class="sxs-lookup"><span data-stu-id="c4576-144">Steps tooget a valid token</span></span>
1. <span data-ttu-id="c4576-145">Llamada API de hello con hello parámetros siguientes y realizar seguro tooreplace Hola INQUILINO\_Id., cliente\_identificador y el cliente\_secreto:</span><span class="sxs-lookup"><span data-stu-id="c4576-145">Call hello API with hello following parameters and make sure tooreplace hello TENANT\_ID, CLIENT\_ID and CLIENT\_SECRET:</span></span>
   
   * <span data-ttu-id="c4576-146">**URL de solicitud** como *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span><span class="sxs-lookup"><span data-stu-id="c4576-146">**Request URL** as *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span></span>
   * <span data-ttu-id="c4576-147">**Encabezado Content-Type HTTP** como *application/x-www-form-urlencoded*</span><span class="sxs-lookup"><span data-stu-id="c4576-147">**HTTP Content-Type header** as *application/x-www-form-urlencoded*</span></span>
   * <span data-ttu-id="c4576-148">**Cuerpo de solicitud HTTP** como *grant\_type=client\_credentials&amp;client_id={CLIENT\_ID}&amp;client_secret={CLIENT\_SECRET}&amp;resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span><span class="sxs-lookup"><span data-stu-id="c4576-148">**HTTP Request Body** as *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span></span>
     
     <span data-ttu-id="c4576-149">Hola te mostramos una solicitud de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c4576-149">hello following is an example request:</span></span>
     
       <span data-ttu-id="c4576-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span><span class="sxs-lookup"><span data-stu-id="c4576-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span></span>
     
     <span data-ttu-id="c4576-151">Este es un ejemplo de respuesta:</span><span class="sxs-lookup"><span data-stu-id="c4576-151">Here is an example response:</span></span>
     
       <span data-ttu-id="c4576-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span><span class="sxs-lookup"><span data-stu-id="c4576-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span></span>
     
       <span data-ttu-id="c4576-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span><span class="sxs-lookup"><span data-stu-id="c4576-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span></span>
     
     <span data-ttu-id="c4576-154">Este ejemplo incluye codificación URL de los parámetros de envío de hello, `resource` valor es realmente `https://management.core.windows.net/`.</span><span class="sxs-lookup"><span data-stu-id="c4576-154">This example included URL encoding of hello POST parameters, `resource` value is actually `https://management.core.windows.net/`.</span></span> <span data-ttu-id="c4576-155">Tenga cuidado de codificar como dirección URL de tooalso `{CLIENT_SECRET}` ya que puede contener caracteres especiales.</span><span class="sxs-lookup"><span data-stu-id="c4576-155">Be careful tooalso URL encode `{CLIENT_SECRET}` as it may contain special characters.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="c4576-156">Para las pruebas, puede usar una herramienta de cliente HTTP, como [Fiddler](http://www.telerik.com/fiddler) o la extensión [Postman de Chrome](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop).</span><span class="sxs-lookup"><span data-stu-id="c4576-156">For testing, you can use an HTTP client tool like [Fiddler](http://www.telerik.com/fiddler) or [Chrome Postman extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span></span> 
     > 
     > 
2. <span data-ttu-id="c4576-157">Ahora en cada llamada API, incluya el encabezado de solicitud de autorización de Hola:</span><span class="sxs-lookup"><span data-stu-id="c4576-157">Now in every API call, include hello authorization request header:</span></span>
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    <span data-ttu-id="c4576-158">Si recibe un código de 401 estado devuelve, cuerpo de respuesta de comprobación de hello, podría indicarle Hola token ha caducado.</span><span class="sxs-lookup"><span data-stu-id="c4576-158">If you get a 401 status code returned, check hello response body, it might tell you hello token is expired.</span></span> <span data-ttu-id="c4576-159">En ese caso, obtenga un nuevo token.</span><span class="sxs-lookup"><span data-stu-id="c4576-159">In that case, get a new token.</span></span>

## <a name="using-hello-apis"></a><span data-ttu-id="c4576-160">Usar las API de Hola</span><span class="sxs-lookup"><span data-stu-id="c4576-160">Using hello APIs</span></span>
<span data-ttu-id="c4576-161">Ahora que tiene un token válido, está listo toomake Hola API llamadas.</span><span class="sxs-lookup"><span data-stu-id="c4576-161">Now that you have a valid token, you are ready toomake hello API calls.</span></span>

1. <span data-ttu-id="c4576-162">En cada solicitud de API, deberá toopass un token válido y vigente que obtuvo en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4576-162">In each API request, you will need toopass a valid, unexpired token which you obtained in hello previous section.</span></span>
2. <span data-ttu-id="c4576-163">Necesitará tooplug algunos parámetros en la solicitud de hello URI que identifica la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c4576-163">You will need tooplug in some parameters into hello request URI which identifies your application.</span></span> <span data-ttu-id="c4576-164">URI de solicitud de Hello aspecto Hola siguiente</span><span class="sxs-lookup"><span data-stu-id="c4576-164">hello request URI looks like hello following</span></span>
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    <span data-ttu-id="c4576-165">parámetros de hello tooget, haga clic en el nombre de la aplicación y haga clic en el panel y verá una página como siguiente de Hola a todos Hola 3 parámetros.</span><span class="sxs-lookup"><span data-stu-id="c4576-165">tooget hello parameters, click on your application name and click Dashboard and you will see a page like hello following with all hello 3 parameters.</span></span>
   
   * <span data-ttu-id="c4576-166">**1**`{subscription-id}`</span><span class="sxs-lookup"><span data-stu-id="c4576-166">**1** `{subscription-id}`</span></span>
   * <span data-ttu-id="c4576-167">**2**`{app-collection}`</span><span class="sxs-lookup"><span data-stu-id="c4576-167">**2** `{app-collection}`</span></span>
   * <span data-ttu-id="c4576-168">**3**`{app-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="c4576-168">**3** `{app-resource-name}`</span></span>
   * <span data-ttu-id="c4576-169">**4** nombre de su grupo de recursos va toobe **MobileEngagement** a menos que cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="c4576-169">**4** Your Resource Group name is going toobe **MobileEngagement** unless you created a new one.</span></span> 
     
     ![Parámetros de URI de la API de Mobile Engagement][2]

> [!NOTE]
> <br/>
> 
> 1. <span data-ttu-id="c4576-171">Omitir Hola API raíz dirección tal y como se trataba de hello API anteriores.</span><span class="sxs-lookup"><span data-stu-id="c4576-171">Ignore hello API Root Address as this was for hello previous APIs.</span></span><br/>
> 2. <span data-ttu-id="c4576-172">Si ha creado la aplicación hello mediante el portal de Azure clásico, a continuación, necesita nombre de recurso de la aplicación de hello toouse que es diferente del nombre de la aplicación hello propio.</span><span class="sxs-lookup"><span data-stu-id="c4576-172">If you created hello app using Azure Classic portal then you need toouse hello Application Resource name which is different than hello Application name itself.</span></span> <span data-ttu-id="c4576-173">Si ha creado la aplicación hello en hello Portal de Azure, a continuación, debe usar Hola nombre de aplicación (no hay ningún diferenciación entre el nombre del recurso de aplicación y el nombre de aplicación para las aplicaciones creadas en el nuevo portal de hello).</span><span class="sxs-lookup"><span data-stu-id="c4576-173">If you created hello app in hello Azure Portal then you should use hello App Name itself (there is no differentiation between Application Resource Name and App Name for apps created in hello new portal).</span></span>  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



