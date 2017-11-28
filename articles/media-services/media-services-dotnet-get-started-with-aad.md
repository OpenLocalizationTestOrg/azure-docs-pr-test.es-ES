---
title: "aaaUse tooaccess de autenticación de Azure AD API de servicios multimedia de Azure con .NET | Documentos de Microsoft"
description: "Este tema muestra cómo toouse tooaccess de autenticación de Azure Active Directory (Azure AD) servicios multimedia de Azure (AMS) API con. NET."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 2f750e460d9e476ad92e96adeac6500cb692cd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a><span data-ttu-id="fe897-103">Utilizar autenticación de Azure AD tooaccess API de servicios multimedia de Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="fe897-103">Use Azure AD authentication tooaccess Azure Media Services API with .NET</span></span>

<span data-ttu-id="fe897-104">A partir de windowsazure.mediaservices 4.0.0.4, Azure Media Services admite la autenticación basada en Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fe897-104">Starting with windowsazure.mediaservices 4.0.0.4, Azure Media Services supports authentication based on Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="fe897-105">Este tema muestra cómo toouse tooaccess de autenticación de Azure AD API de servicios multimedia de Azure con Microsoft. NET.</span><span class="sxs-lookup"><span data-stu-id="fe897-105">This topic shows you how toouse Azure AD  authentication tooaccess Azure Media Services API with Microsoft .NET.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe897-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fe897-106">Prerequisites</span></span>

- <span data-ttu-id="fe897-107">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe897-107">An Azure account.</span></span> <span data-ttu-id="fe897-108">Para más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fe897-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="fe897-109">Una cuenta de Media Services.</span><span class="sxs-lookup"><span data-stu-id="fe897-109">A Media Services account.</span></span> <span data-ttu-id="fe897-110">Para obtener más información, consulte [crear una cuenta de servicios multimedia de Azure mediante el portal de Azure de hello](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="fe897-110">For more information, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="fe897-111">Hola más reciente [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) paquete.</span><span class="sxs-lookup"><span data-stu-id="fe897-111">hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span>
- <span data-ttu-id="fe897-112">Está familiarizado con el tema de hello [obtiene acceso a la API de los servicios de multimedia de Azure con información general de autenticación de AAD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="fe897-112">Familiarity with hello topic [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="fe897-113">Si usa la autenticación de Azure AD con Azure Media Services, puede autenticarse de alguna de estas dos formas:</span><span class="sxs-lookup"><span data-stu-id="fe897-113">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="fe897-114">**Autenticación de usuario** autentica una persona que usa Hola aplicación toointeract con recursos de servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe897-114">**User authentication** authenticates a person who is using hello app toointeract with Azure Media Services resources.</span></span> <span data-ttu-id="fe897-115">aplicación interactiva de Hello en primer lugar debe solicitarle las credenciales de usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="fe897-115">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="fe897-116">Un ejemplo es una aplicación de consola de administración que se utiliza por toomonitor de usuarios autorizados trabajos de codificación o streaming en vivo.</span><span class="sxs-lookup"><span data-stu-id="fe897-116">An example is a management console app that's used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="fe897-117">**Autenticación de entidad de servicio** autentica un servicio.</span><span class="sxs-lookup"><span data-stu-id="fe897-117">**Service principal authentication** authenticates a service.</span></span> <span data-ttu-id="fe897-118">Las aplicaciones que normalmente utilizan este método de autenticación son aplicaciones que ejecutan servicios de demonio, servicios de nivel intermedio o trabajos programados, como Web Apps, Function Apps, Logic Apps, API o microservicios.</span><span class="sxs-lookup"><span data-stu-id="fe897-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span></span>

>[!IMPORTANT]
><span data-ttu-id="fe897-119">Azure Media Services actualmente admite un modelo de autenticación de Azure Access Control Service.</span><span class="sxs-lookup"><span data-stu-id="fe897-119">Azure Media Service currently supports an Azure Access Control Service  authentication model.</span></span> <span data-ttu-id="fe897-120">Sin embargo, la autorización de Control de acceso va toobe en desuso en 1 de junio de 2018.</span><span class="sxs-lookup"><span data-stu-id="fe897-120">However, Access Control authorization is going toobe deprecated on June 1, 2018.</span></span> <span data-ttu-id="fe897-121">Se recomienda que migre modelo de autenticación de Azure Active Directory tooan tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="fe897-121">We recommend that you migrate tooan Azure Active Directory authentication model as soon as possible.</span></span>

## <a name="get-an-azure-ad-access-token"></a><span data-ttu-id="fe897-122">Obtención de un token de acceso de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe897-122">Get an Azure AD access token</span></span>

<span data-ttu-id="fe897-123">tooconnect toohello API de servicios multimedia de Azure con autenticación de Azure AD, la aplicación de cliente de hello debe toorequest un token de acceso de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe897-123">tooconnect toohello Azure Media Services API with Azure AD authentication, hello client app needs toorequest an Azure AD access token.</span></span> <span data-ttu-id="fe897-124">Cuando usas SDK, muchos de los detalles de hello acerca de cómo se ajusta y simplificado para usted en hello tooacquire un token de acceso de Azure AD del cliente de .NET de los servicios multimedia de hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) y [AzureAdTokenCredentials ](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) clases.</span><span class="sxs-lookup"><span data-stu-id="fe897-124">When you use hello Media Services .NET client SDK, many of hello details about how tooacquire an Azure AD access token are wrapped and simplified for you in hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) and [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span></span> 

<span data-ttu-id="fe897-125">Por ejemplo, no es necesario tooprovide autoridad de hello Azure AD, URI de recurso de servicios multimedia o nativo detalles de la aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe897-125">For example, you don't need tooprovide hello Azure AD authority, Media Services resource URI, or native Azure AD application details.</span></span> <span data-ttu-id="fe897-126">Se trata de valores conocidos que ya están configurados de hello clase de proveedor de tokens de acceso de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe897-126">These are well-known values that are already configured by hello Azure AD access token provider class.</span></span> 

<span data-ttu-id="fe897-127">Si no utiliza el SDK de .NET de servicios multimedia de Azure, recomendamos que use hello [biblioteca de autenticación de Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="fe897-127">If you are not using Azure Media Service .NET SDK, we recommend that you use hello [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="fe897-128">tooget valores para parámetros de Hola que necesita toouse con la biblioteca de autenticación de Azure AD, consulte [usar la configuración de autenticación de Azure tooaccess portal Azure AD hello](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="fe897-128">tooget values for hello parameters that you need toouse with Azure AD Authentication Library, see [Use hello Azure portal tooaccess Azure AD authentication settings](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="fe897-129">También tiene Hola opción de sustitución de la implementación predeterminada de Hola de hello **AzureAdTokenProvider** con su propia implementación.</span><span class="sxs-lookup"><span data-stu-id="fe897-129">You also have hello option of replacing hello default implementation of hello **AzureAdTokenProvider** with your own implementation.</span></span>

## <a name="install-and-configure-azure-media-services-net-sdk"></a><span data-ttu-id="fe897-130">Instalación y configuración del SDK de Azure Media Services para .NET</span><span class="sxs-lookup"><span data-stu-id="fe897-130">Install and configure Azure Media Services .NET SDK</span></span>

>[!NOTE] 
><span data-ttu-id="fe897-131">autenticación de toouse Azure AD con hello Media Services .NET SDK, deberá toohave hello más reciente [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) paquete.</span><span class="sxs-lookup"><span data-stu-id="fe897-131">toouse Azure AD authentication with hello Media Services .NET SDK, you need toohave hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span> <span data-ttu-id="fe897-132">Además, agregue una referencia toohello **Microsoft.IdentityModel.Clients.ActiveDirectory** ensamblado.</span><span class="sxs-lookup"><span data-stu-id="fe897-132">Also, add a reference toohello **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span></span> <span data-ttu-id="fe897-133">Si utilizas una aplicación existente, incluir hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** ensamblado.</span><span class="sxs-lookup"><span data-stu-id="fe897-133">If you are using an existing app, include hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span></span> 

1. <span data-ttu-id="fe897-134">Cree una aplicación de consola en C# mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe897-134">Create a new C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="fe897-135">Hola de uso [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall de paquete de NuGet **Azure Media Services .NET SDK**.</span><span class="sxs-lookup"><span data-stu-id="fe897-135">Use hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet package tooinstall **Azure Media Services .NET SDK**.</span></span> 

    <span data-ttu-id="fe897-136">tooadd referencias usando NuGet, tomar Hola pasos: en **el Explorador de soluciones**, haga clic en el nombre del proyecto de hello y, a continuación, seleccione **administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="fe897-136">tooadd references by using NuGet, take hello following steps: in **Solution Explorer**, right-click hello project name, and then select **Manage NuGet packages**.</span></span> <span data-ttu-id="fe897-137">Después, busque **windowsazure.mediaservices** y seleccione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="fe897-137">Then, search for **windowsazure.mediaservices** and select **Install**.</span></span>
    
    <span data-ttu-id="fe897-138">O bien</span><span class="sxs-lookup"><span data-stu-id="fe897-138">-or-</span></span>

    <span data-ttu-id="fe897-139">Ejecución hello después del comando en **Package Manager Console** en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe897-139">Run hello following command in **Package Manager Console** in Visual Studio.</span></span>

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. <span data-ttu-id="fe897-140">Agregar **con** tooyour código de origen.</span><span class="sxs-lookup"><span data-stu-id="fe897-140">Add **using** tooyour source code.</span></span>

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a><span data-ttu-id="fe897-141">Uso de la autenticación de usuario</span><span class="sxs-lookup"><span data-stu-id="fe897-141">Use user authentication</span></span>

<span data-ttu-id="fe897-142">tooconnect toohello API de servicios multimedia de Azure con la opción de autenticación de usuario de hello, aplicación de cliente de hello necesita toorequest Hola de un token de Azure AD mediante el uso de parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="fe897-142">tooconnect toohello Azure Media Service API with hello user authentication option, hello client app needs toorequest an Azure AD token by using hello following parameters:</span></span>  

- <span data-ttu-id="fe897-143">Punto de conexión de inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe897-143">Azure AD tenant endpoint.</span></span> <span data-ttu-id="fe897-144">puede recuperar la información de inquilino de Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe897-144">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="fe897-145">Mantenga el mouse sobre Hola usuario con sesión iniciada en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe897-145">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="fe897-146">URI del recurso de Media Services.</span><span class="sxs-lookup"><span data-stu-id="fe897-146">Media Services resource URI.</span></span>
- <span data-ttu-id="fe897-147">Id. de cliente de aplicación de Media Services (nativo)</span><span class="sxs-lookup"><span data-stu-id="fe897-147">Media Services (native) application client ID.</span></span> 
- <span data-ttu-id="fe897-148">URI de redireccionamiento de aplicación de Media Services (nativo).</span><span class="sxs-lookup"><span data-stu-id="fe897-148">Media Services (native) application redirect URI.</span></span> 

<span data-ttu-id="fe897-149">valores de Hello para estos parámetros se pueden encontrar en **AzureEnvironments.AzureCloudEnvironment**.</span><span class="sxs-lookup"><span data-stu-id="fe897-149">hello values for these parameters can be found in **AzureEnvironments.AzureCloudEnvironment**.</span></span> <span data-ttu-id="fe897-150">Hola **AzureEnvironments.AzureCloudEnvironment** constante es una aplicación auxiliar de hello .NET SDK tooget valores de variable de entorno derecho de Hola para un centro de datos de Azure pública.</span><span class="sxs-lookup"><span data-stu-id="fe897-150">hello **AzureEnvironments.AzureCloudEnvironment** constant is a helper in hello .NET SDK tooget hello right environment variable settings for a public Azure Data Center.</span></span> 

<span data-ttu-id="fe897-151">Contiene valores de configuración de entorno predefinidos para tener acceso a servicios multimedia en centros de datos públicos de hello solo.</span><span class="sxs-lookup"><span data-stu-id="fe897-151">It contains pre-defined environment settings for accessing Media Services in hello public data centers only.</span></span> <span data-ttu-id="fe897-152">Para regiones con entornos de nube de administración pública o soberana, puede usar **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment** o **AzureGermanCloudEnvironment**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="fe897-152">For sovereign or government cloud regions, you can use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, or **AzureGermanCloudEnvironment** respectively.</span></span>

<span data-ttu-id="fe897-153">Hola, ejemplo de código siguiente crea un token:</span><span class="sxs-lookup"><span data-stu-id="fe897-153">hello following code example creates a token:</span></span>
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
<span data-ttu-id="fe897-154">toostart programar con servicios multimedia, necesita toocreate una **CloudMediaContext** instancia que representa el contexto de servidor hello.</span><span class="sxs-lookup"><span data-stu-id="fe897-154">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="fe897-155">Hola **CloudMediaContext** incluye referencias tooimportant colecciones incluidos trabajos, activos, archivos, las directivas de acceso y localizadores.</span><span class="sxs-lookup"><span data-stu-id="fe897-155">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span> 

<span data-ttu-id="fe897-156">También necesita hello toopass **recurso URI para los servicios de REST de multimedia** toohello **CloudMediaContext** constructor.</span><span class="sxs-lookup"><span data-stu-id="fe897-156">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="fe897-157">URI del recurso de hello tooget para servicios multimedia de REST, inicio de sesión toohello portal de Azure, seleccione la cuenta de servicios multimedia de Azure, seleccione **el acceso de API**y, a continuación, seleccione **conectar servicios de multimedia de tooAzure con usuario autenticación**.</span><span class="sxs-lookup"><span data-stu-id="fe897-157">tooget hello resource URI for Media REST Services, sign in toohello Azure portal, select your Azure Media Services account, select **API access**, and then select **Connect tooAzure Media Services with user authentication**.</span></span> 

<span data-ttu-id="fe897-158">Hello ejemplo de código siguiente se crea un **CloudMediaContext** instancia:</span><span class="sxs-lookup"><span data-stu-id="fe897-158">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

<span data-ttu-id="fe897-159">Hola de ejemplo siguiente muestra cómo toocreate Hola contexto hello y símbolo (token) de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="fe897-159">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

    namespace AADAuthSample
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Specify your Azure AD tenant domain, for example "microsoft.onmicrosoft.com".
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR AAD TENANT DOMAIN HERE}", AzureEnvironments.AzureCloudEnvironment);
    
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
            }
    
        }
    }

>[!NOTE]
><span data-ttu-id="fe897-160">Si se produce una excepción que indicara "servidor remoto hello devolvió un error: (401) no autorizado," vea hello [el control de acceso](media-services-use-aad-auth-to-access-ams-api.md#access-control) sección de obtener acceso a la API de los servicios de multimedia de Azure con información general de autenticación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe897-160">If you get an exception that says "hello remote server returned an error: (401) Unauthorized," see hello [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section of Accessing Azure Media Services API with Azure AD authentication overview.</span></span>

## <a name="use-service-principal-authentication"></a><span data-ttu-id="fe897-161">Uso de la autenticación de entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="fe897-161">Use service principal authentication</span></span>
    
<span data-ttu-id="fe897-162">tooconnect toohello API de servicios multimedia de Azure con la opción de entidad de seguridad de servicio de hello, necesita la aplicación de nivel intermedio (API de web o aplicación web) toorequests un token de Azure AD con hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="fe897-162">tooconnect toohello Azure Media Services API with hello service principal option, your middle-tier app (web API or web application) needs toorequests an Azure AD token with hello following parameters:</span></span>  

- <span data-ttu-id="fe897-163">Punto de conexión de inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe897-163">Azure AD tenant endpoint.</span></span> <span data-ttu-id="fe897-164">puede recuperar la información de inquilino de Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe897-164">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="fe897-165">Mantenga el mouse sobre Hola usuario con sesión iniciada en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe897-165">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="fe897-166">URI del recurso de Media Services.</span><span class="sxs-lookup"><span data-stu-id="fe897-166">Media Services resource URI.</span></span>
- <span data-ttu-id="fe897-167">Los valores de aplicación de Azure AD: Hola **Id. de cliente** y **secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="fe897-167">Azure AD application values: hello **Client ID** and **Client secret**.</span></span>

<span data-ttu-id="fe897-168">Hola valores de hello **Id. de cliente** y **secreto de cliente** parámetros pueden encontrarse en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe897-168">hello values for hello **Client ID** and **Client secret** parameters can be found in hello Azure portal.</span></span> <span data-ttu-id="fe897-169">Para obtener más información, consulte [Introducción a Azure AD mediante autenticación Hola portal de Azure](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="fe897-169">For more information, see [Getting started with Azure AD authentication using hello Azure portal](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="fe897-170">Hello ejemplo de código siguiente crea un token mediante hello **AzureAdTokenCredentials** constructor que toma **AzureAdClientSymmetricKey** como parámetro:</span><span class="sxs-lookup"><span data-stu-id="fe897-170">hello following code example creates a token by using hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientSymmetricKey** as a parameter:</span></span> 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

<span data-ttu-id="fe897-171">También puede especificar hello **AzureAdTokenCredentials** constructor que toma **AzureAdClientCertificate** como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="fe897-171">You can also specify hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientCertificate** as a parameter.</span></span> 

<span data-ttu-id="fe897-172">Para obtener instrucciones acerca de cómo toocreate y configurar un certificado en un formulario que puede usarse con Azure AD, consulte [tooAzure AD en aplicaciones de demonio con certificados: pasos de configuración manual de autenticación](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span><span class="sxs-lookup"><span data-stu-id="fe897-172">For instructions about how toocreate and configure a certificate in a form that can be used by Azure AD, see [Authenticating tooAzure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span></span>

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

<span data-ttu-id="fe897-173">toostart programar con servicios multimedia, necesita toocreate una **CloudMediaContext** instancia que representa el contexto de servidor hello.</span><span class="sxs-lookup"><span data-stu-id="fe897-173">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="fe897-174">También necesita hello toopass **recurso URI para los servicios de REST de multimedia** toohello **CloudMediaContext** constructor.</span><span class="sxs-lookup"><span data-stu-id="fe897-174">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="fe897-175">Puede obtener hello **recurso URI para los servicios de REST de multimedia** valor de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe897-175">You can get hello **resource URI for Media REST Services** value from hello Azure portal as well.</span></span>

<span data-ttu-id="fe897-176">Hello ejemplo de código siguiente se crea un **CloudMediaContext** instancia:</span><span class="sxs-lookup"><span data-stu-id="fe897-176">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
<span data-ttu-id="fe897-177">Hola de ejemplo siguiente muestra cómo toocreate Hola contexto hello y símbolo (token) de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="fe897-177">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

    namespace AADAuthSample
    {
    
        class Program
        {
            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                            new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                            AzureEnvironments.AzureCloudEnvironment);
            
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".      
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
    
                Console.ReadLine();
            }
    
        }
    }

## <a name="next-steps"></a><span data-ttu-id="fe897-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fe897-178">Next steps</span></span>

<span data-ttu-id="fe897-179">Empezar a trabajar con [cargar archivos tooyour cuenta](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="fe897-179">Get started with [uploading files tooyour account](media-services-dotnet-upload-files.md).</span></span>
