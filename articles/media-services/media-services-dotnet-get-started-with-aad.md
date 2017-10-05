---
title: "Uso de la autenticación de Azure AD para acceder a la API de Azure Media Services con .NET | Microsoft Docs"
description: "En este tema se explica cómo usar la autenticación de Azure Active Directory (Azure AD) para acceder a la API de Azure Media Services (AMS) con .NET"
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
ms.openlocfilehash: a9355200a05a3aa1b494b76977d38ddc42bfe179
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-ad-authentication-to-access-azure-media-services-api-with-net"></a><span data-ttu-id="047af-103">Uso de la autenticación de Azure AD para acceder a la API de Azure Media Services con .NET</span><span class="sxs-lookup"><span data-stu-id="047af-103">Use Azure AD authentication to access Azure Media Services API with .NET</span></span>

<span data-ttu-id="047af-104">A partir de windowsazure.mediaservices 4.0.0.4, Azure Media Services admite la autenticación basada en Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="047af-104">Starting with windowsazure.mediaservices 4.0.0.4, Azure Media Services supports authentication based on Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="047af-105">En este tema se explica cómo usar la autenticación de Azure AD para acceder a la API de Azure Media Services con Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="047af-105">This topic shows you how to use Azure AD  authentication to access Azure Media Services API with Microsoft .NET.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="047af-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="047af-106">Prerequisites</span></span>

- <span data-ttu-id="047af-107">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="047af-107">An Azure account.</span></span> <span data-ttu-id="047af-108">Para más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="047af-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="047af-109">Una cuenta de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="047af-109">A Media Services account.</span></span> <span data-ttu-id="047af-110">Para más información, vea [Creación de una cuenta de Azure Media Services mediante Azure Portal](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="047af-110">For more information, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="047af-111">El último paquete [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices).</span><span class="sxs-lookup"><span data-stu-id="047af-111">The latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span>
- <span data-ttu-id="047af-112">Familiarícese con el tema de [información general sobre el acceso a la API de Azure Media Services con la autenticación de AAD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="047af-112">Familiarity with the topic [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="047af-113">Si usa la autenticación de Azure AD con Azure Media Services, puede autenticarse de alguna de estas dos formas:</span><span class="sxs-lookup"><span data-stu-id="047af-113">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="047af-114">**Autenticación de usuario** autentica a una persona que está usando la aplicación para interactuar con los recursos de Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="047af-114">**User authentication** authenticates a person who is using the app to interact with Azure Media Services resources.</span></span> <span data-ttu-id="047af-115">La aplicación interactiva en primer lugar debe solicitar al usuario las credenciales.</span><span class="sxs-lookup"><span data-stu-id="047af-115">The interactive application should first prompt the user for credentials.</span></span> <span data-ttu-id="047af-116">Un ejemplo es una aplicación de consola de administración que usan los usuarios autorizados para supervisar trabajos de codificación o streaming en vivo.</span><span class="sxs-lookup"><span data-stu-id="047af-116">An example is a management console app that's used by authorized users to monitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="047af-117">**Autenticación de entidad de servicio** autentica un servicio.</span><span class="sxs-lookup"><span data-stu-id="047af-117">**Service principal authentication** authenticates a service.</span></span> <span data-ttu-id="047af-118">Las aplicaciones que normalmente utilizan este método de autenticación son aplicaciones que ejecutan servicios de demonio, servicios de nivel intermedio o trabajos programados, como Web Apps, Function Apps, Logic Apps, API o microservicios.</span><span class="sxs-lookup"><span data-stu-id="047af-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span></span>

>[!IMPORTANT]
><span data-ttu-id="047af-119">Azure Media Services actualmente admite un modelo de autenticación de Azure Access Control Service.</span><span class="sxs-lookup"><span data-stu-id="047af-119">Azure Media Service currently supports an Azure Access Control Service  authentication model.</span></span> <span data-ttu-id="047af-120">Pero la autenticación de Access Control dejará de usarse el 1 de junio de 2018.</span><span class="sxs-lookup"><span data-stu-id="047af-120">However, Access Control authorization is going to be deprecated on June 1, 2018.</span></span> <span data-ttu-id="047af-121">Se recomienda migrar tan pronto como sea posible a un modelo de autenticación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="047af-121">We recommend that you migrate to an Azure Active Directory authentication model as soon as possible.</span></span>

## <a name="get-an-azure-ad-access-token"></a><span data-ttu-id="047af-122">Obtención de un token de acceso de Azure AD</span><span class="sxs-lookup"><span data-stu-id="047af-122">Get an Azure AD access token</span></span>

<span data-ttu-id="047af-123">Para conectarse a la API de Azure Media Services con la autenticación de Azure AD, la aplicación cliente debe solicitar un token de acceso de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="047af-123">To connect to the Azure Media Services API with Azure AD authentication, the client app needs to request an Azure AD access token.</span></span> <span data-ttu-id="047af-124">Si usa el SDK del cliente .NET de Media Services .NET, muchos de los detalles sobre cómo adquirir un token de acceso de Azure AD se ajustan y simplifican en función del caso en las clases [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) y [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs).</span><span class="sxs-lookup"><span data-stu-id="047af-124">When you use the Media Services .NET client SDK, many of the details about how to acquire an Azure AD access token are wrapped and simplified for you in the [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) and [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span></span> 

<span data-ttu-id="047af-125">Por ejemplo, no es necesario proporcionar el URI de autoridad de Azure AD, el URI de recurso de Media Services ni los detalles de la aplicación nativa de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="047af-125">For example, you don't need to provide the Azure AD authority, Media Services resource URI, or native Azure AD application details.</span></span> <span data-ttu-id="047af-126">Se trata de valores conocidos que ya están configurados por la clase de proveedor de tokens de acceso de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="047af-126">These are well-known values that are already configured by the Azure AD access token provider class.</span></span> 

<span data-ttu-id="047af-127">Si no utiliza el SDK de Azure Media Services para .NET, se recomienda que use la [biblioteca de autenticación de Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="047af-127">If you are not using Azure Media Service .NET SDK, we recommend that you use the [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="047af-128">Para obtener los valores de los parámetros necesarios para usarlos con la biblioteca de autenticación de Azure AD, vea [Uso de Azure Portal para acceder a la configuración de autenticación de Azure AD](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="047af-128">To get values for the parameters that you need to use with Azure AD Authentication Library, see [Use the Azure portal to access Azure AD authentication settings](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="047af-129">También tiene la opción de sustituir la implementación predeterminada de **AzureAdTokenProvider** por su propia implementación.</span><span class="sxs-lookup"><span data-stu-id="047af-129">You also have the option of replacing the default implementation of the **AzureAdTokenProvider** with your own implementation.</span></span>

## <a name="install-and-configure-azure-media-services-net-sdk"></a><span data-ttu-id="047af-130">Instalación y configuración del SDK de Azure Media Services para .NET</span><span class="sxs-lookup"><span data-stu-id="047af-130">Install and configure Azure Media Services .NET SDK</span></span>

>[!NOTE] 
><span data-ttu-id="047af-131">Para usar la autenticación de Azure AD con el SDK de Media Services para .NET, debe disponer del último paquete [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices).</span><span class="sxs-lookup"><span data-stu-id="047af-131">To use Azure AD authentication with the Media Services .NET SDK, you need to have the latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span> <span data-ttu-id="047af-132">Además, agregue una referencia al ensamblado **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="047af-132">Also, add a reference to the **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span></span> <span data-ttu-id="047af-133">Si usa una aplicación existente, incluya el ensamblado **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll**.</span><span class="sxs-lookup"><span data-stu-id="047af-133">If you are using an existing app, include the **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span></span> 

1. <span data-ttu-id="047af-134">Cree una aplicación de consola en C# mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="047af-134">Create a new C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="047af-135">Use el paquete NuGet [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) para instalar el **SDK de Azure Media Services para .NET**.</span><span class="sxs-lookup"><span data-stu-id="047af-135">Use the [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet package to install **Azure Media Services .NET SDK**.</span></span> 

    <span data-ttu-id="047af-136">Para agregar referencias con NuGet, siga estos pasos: en el **Explorador de soluciones**, haga clic con el botón derecho en el nombre del proyecto y, después, seleccione **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="047af-136">To add references by using NuGet, take the following steps: in **Solution Explorer**, right-click the project name, and then select **Manage NuGet packages**.</span></span> <span data-ttu-id="047af-137">Después, busque **windowsazure.mediaservices** y seleccione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="047af-137">Then, search for **windowsazure.mediaservices** and select **Install**.</span></span>
    
    <span data-ttu-id="047af-138">O bien</span><span class="sxs-lookup"><span data-stu-id="047af-138">-or-</span></span>

    <span data-ttu-id="047af-139">Ejecute el siguiente comando en la **Consola del Administrador de paquetes** de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="047af-139">Run the following command in **Package Manager Console** in Visual Studio.</span></span>

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. <span data-ttu-id="047af-140">Agregue **using** al código fuente.</span><span class="sxs-lookup"><span data-stu-id="047af-140">Add **using** to your source code.</span></span>

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a><span data-ttu-id="047af-141">Uso de la autenticación de usuario</span><span class="sxs-lookup"><span data-stu-id="047af-141">Use user authentication</span></span>

<span data-ttu-id="047af-142">Para conectarse a la API de Azure Media Services mediante la opción de autenticación de usuario, la aplicación cliente debe solicitar un token de Azure AD con el uso de los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="047af-142">To connect to the Azure Media Service API with the user authentication option, the client app needs to request an Azure AD token by using the following parameters:</span></span>  

- <span data-ttu-id="047af-143">Punto de conexión de inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="047af-143">Azure AD tenant endpoint.</span></span> <span data-ttu-id="047af-144">La información del inquilino se puede recuperar desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="047af-144">The tenant information can be retrieved from the Azure portal.</span></span> <span data-ttu-id="047af-145">Mantenga el puntero sobre el usuario que inició sesión en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="047af-145">Hover over the signed-in user in the upper-right corner.</span></span>
- <span data-ttu-id="047af-146">URI del recurso de Media Services</span><span class="sxs-lookup"><span data-stu-id="047af-146">Media Services resource URI.</span></span>
- <span data-ttu-id="047af-147">Id. de cliente de aplicación de Media Services (nativo)</span><span class="sxs-lookup"><span data-stu-id="047af-147">Media Services (native) application client ID.</span></span> 
- <span data-ttu-id="047af-148">URI de redireccionamiento de aplicación de Media Services (nativo)</span><span class="sxs-lookup"><span data-stu-id="047af-148">Media Services (native) application redirect URI.</span></span> 

<span data-ttu-id="047af-149">Los valores para estos parámetros se pueden encontrar en **AzureEnvironments.AzureCloudEnvironment**.</span><span class="sxs-lookup"><span data-stu-id="047af-149">The values for these parameters can be found in **AzureEnvironments.AzureCloudEnvironment**.</span></span> <span data-ttu-id="047af-150">La constante **AzureEnvironments.AzureCloudEnvironment** es una aplicación auxiliar del SDK para .NET para obtener la configuración adecuada de la variable de entorno para un centro de datos de Azure público.</span><span class="sxs-lookup"><span data-stu-id="047af-150">The **AzureEnvironments.AzureCloudEnvironment** constant is a helper in the .NET SDK to get the right environment variable settings for a public Azure Data Center.</span></span> 

<span data-ttu-id="047af-151">Contiene la configuración predefinida del entorno para acceder a Media Services solo en los centros de datos públicos.</span><span class="sxs-lookup"><span data-stu-id="047af-151">It contains pre-defined environment settings for accessing Media Services in the public data centers only.</span></span> <span data-ttu-id="047af-152">Para regiones con entornos de nube de administración pública o soberana, puede usar **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment** o **AzureGermanCloudEnvironment**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="047af-152">For sovereign or government cloud regions, you can use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, or **AzureGermanCloudEnvironment** respectively.</span></span>

<span data-ttu-id="047af-153">En el ejemplo de código siguiente se crea un token:</span><span class="sxs-lookup"><span data-stu-id="047af-153">The following code example creates a token:</span></span>
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
<span data-ttu-id="047af-154">Para empezar a programar con Media Services, tiene que crear una instancia de **CloudMediaContext** que representa el contexto del servidor.</span><span class="sxs-lookup"><span data-stu-id="047af-154">To start programming against Media Services, you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="047af-155">**CloudMediaContext** incluye referencias a colecciones importantes, como trabajos, recursos, archivos, directivas de acceso y localizadores.</span><span class="sxs-lookup"><span data-stu-id="047af-155">The **CloudMediaContext** includes references to important collections including jobs, assets, files, access policies, and locators.</span></span> 

<span data-ttu-id="047af-156">También necesita pasar el **URI de recurso de Media REST Services** al constructor **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="047af-156">You also need to pass the **resource URI for Media REST Services** to the **CloudMediaContext** constructor.</span></span> <span data-ttu-id="047af-157">Para obtener el URI de recurso de Media REST Services, inicie sesión en Azure Portal, seleccione la cuenta de Azure Media Services, seleccione **Acceso de API** y después seleccione **Connect to Azure Media Services with user authentication** (Conexión a Azure Media Services con la autenticación de usuario).</span><span class="sxs-lookup"><span data-stu-id="047af-157">To get the resource URI for Media REST Services, sign in to the Azure portal, select your Azure Media Services account, select **API access**, and then select **Connect to Azure Media Services with user authentication**.</span></span> 

<span data-ttu-id="047af-158">En el ejemplo de código siguiente se crea una instancia de **CloudMediaContext**:</span><span class="sxs-lookup"><span data-stu-id="047af-158">The following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

<span data-ttu-id="047af-159">En el ejemplo siguiente se muestra cómo crear el token de Azure AD y el contexto:</span><span class="sxs-lookup"><span data-stu-id="047af-159">The following example shows how to create the Azure AD token and the context:</span></span>

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
><span data-ttu-id="047af-160">Si obtiene una excepción que indica "Error en el servidor remoto: 401 - No autorizado", vea la sección [Control de acceso](media-services-use-aad-auth-to-access-ams-api.md#access-control) de la información general sobre el acceso a la API de Azure Media Services con la autenticación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="047af-160">If you get an exception that says "The remote server returned an error: (401) Unauthorized," see the [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section of Accessing Azure Media Services API with Azure AD authentication overview.</span></span>

## <a name="use-service-principal-authentication"></a><span data-ttu-id="047af-161">Uso de la autenticación de entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="047af-161">Use service principal authentication</span></span>
    
<span data-ttu-id="047af-162">Para conectarse a la API de Media Services mediante la opción de la entidad de servicio, la aplicación de nivel intermedio (Web API o aplicación web) necesita solicitar un token de Azure AD que tenga los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="047af-162">To connect to the Azure Media Services API with the service principal option, your middle-tier app (web API or web application) needs to requests an Azure AD token with the following parameters:</span></span>  

- <span data-ttu-id="047af-163">Punto de conexión de inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="047af-163">Azure AD tenant endpoint.</span></span> <span data-ttu-id="047af-164">La información del inquilino se puede recuperar desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="047af-164">The tenant information can be retrieved from the Azure portal.</span></span> <span data-ttu-id="047af-165">Mantenga el puntero sobre el usuario que inició sesión en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="047af-165">Hover over the signed-in user in the upper-right corner.</span></span>
- <span data-ttu-id="047af-166">URI del recurso de Media Services</span><span class="sxs-lookup"><span data-stu-id="047af-166">Media Services resource URI.</span></span>
- <span data-ttu-id="047af-167">Valores de aplicación de Azure AD: el **Id. de cliente** y el **secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="047af-167">Azure AD application values: the **Client ID** and **Client secret**.</span></span>

<span data-ttu-id="047af-168">Los valores para los parámetros **Id. de cliente** y **secreto de cliente** pueden encontrarse en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="047af-168">The values for the **Client ID** and **Client secret** parameters can be found in the Azure portal.</span></span> <span data-ttu-id="047af-169">Para más información, vea [Introducción a la autenticación de Azure AD mediante Azure Portal](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="047af-169">For more information, see [Getting started with Azure AD authentication using the Azure portal](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="047af-170">El ejemplo de código siguiente crea un token con el uso del constructor **AzureAdTokenCredentials** que adopta **AzureAdClientSymmetricKey** como parámetro:</span><span class="sxs-lookup"><span data-stu-id="047af-170">The following code example creates a token by using the **AzureAdTokenCredentials** constructor that takes **AzureAdClientSymmetricKey** as a parameter:</span></span> 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

<span data-ttu-id="047af-171">También puede especificar el constructor **AzureAdTokenCredentials** que adopta **AzureAdClientCertificate** como parámetro.</span><span class="sxs-lookup"><span data-stu-id="047af-171">You can also specify the **AzureAdTokenCredentials** constructor that takes **AzureAdClientCertificate** as a parameter.</span></span> 

<span data-ttu-id="047af-172">Para obtener instrucciones sobre cómo crear y configurar un certificado de una forma que Azure AD puede utilizar, vea [Authenticating to Azure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md) (Autenticación en aplicaciones de demonio de Azure AD con certificados: pasos de configuración manual).</span><span class="sxs-lookup"><span data-stu-id="047af-172">For instructions about how to create and configure a certificate in a form that can be used by Azure AD, see [Authenticating to Azure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span></span>

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

<span data-ttu-id="047af-173">Para empezar a programar con Media Services, tiene que crear una instancia de **CloudMediaContext** que representa el contexto del servidor.</span><span class="sxs-lookup"><span data-stu-id="047af-173">To start programming against Media Services, you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="047af-174">También necesita pasar el **URI de recurso de Media REST Services** al constructor **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="047af-174">You also need to pass the **resource URI for Media REST Services** to the **CloudMediaContext** constructor.</span></span> <span data-ttu-id="047af-175">También puede obtener el valor del **URI de recurso para Media REST Services** en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="047af-175">You can get the **resource URI for Media REST Services** value from the Azure portal as well.</span></span>

<span data-ttu-id="047af-176">En el ejemplo de código siguiente se crea una instancia de **CloudMediaContext**:</span><span class="sxs-lookup"><span data-stu-id="047af-176">The following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
<span data-ttu-id="047af-177">En el ejemplo siguiente se muestra cómo crear el token de Azure AD y el contexto:</span><span class="sxs-lookup"><span data-stu-id="047af-177">The following example shows how to create the Azure AD token and the context:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="047af-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="047af-178">Next steps</span></span>

<span data-ttu-id="047af-179">Empiece a trabajar en la [carga de archivos en la cuenta](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="047af-179">Get started with [uploading files to your account](media-services-dotnet-upload-files.md).</span></span>
