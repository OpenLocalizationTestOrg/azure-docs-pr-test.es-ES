---
title: "Uso de Azure Active Directory para autenticar soluciones de administración de Batch | Microsoft Docs"
description: Las aplicaciones creadas con Azure Resource Manager y el proveedor de recursos de Batch se autentican con Azure AD.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: tamram
ms.openlocfilehash: 26d4adf4f74f9aacc4cf8cf24be293ebdb4d63c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="dd3ce-103">Autenticación de soluciones de administración de Batch con Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd3ce-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="dd3ce-104">Las aplicaciones que llaman al servicio de administración de Azure Batch se autentican con [Azure Active Directory][aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dd3ce-104">Applications that call the Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="dd3ce-105">Azure Active Directory es el directorio basado en la nube multiinquilino y el servicio de administración de identidades de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="dd3ce-106">El propio Azure usa Azure Active Directory (AAD) para la autenticación de sus clientes, administradores de servicios y usuarios de la organización.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-106">Azure itself uses Azure AD for the authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="dd3ce-107">La biblioteca Batch Management .NET expone tipos para trabajar con cuentas, claves de cuenta, aplicaciones y paquetes de aplicaciones de Batch.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-107">The Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="dd3ce-108">La biblioteca Batch Management .NET es un cliente de proveedor de recursos de Azure y se utiliza junto con [Azure Resource Manager][resman_overview] para administrar estos recursos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-108">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage these resources programmatically.</span></span> <span data-ttu-id="dd3ce-109">Se requiere Azure AD para autenticar las solicitudes realizadas a través de cualquier cliente de proveedor de recursos de Azure, incluida la biblioteca Batch Management .NET y a través de [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="dd3ce-109">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="dd3ce-110">En este artículo, se describe el uso de Azure AD para autenticar desde aplicaciones que utilizan la biblioteca Batch Management .NET.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-110">In this article, we explore using Azure AD to authenticate from applications that use the Batch Management .NET library.</span></span> <span data-ttu-id="dd3ce-111">Se muestra cómo usar Azure AD para autenticar a un administrador o coadministrador de la suscripción mediante la autenticación integrada.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-111">We show how to use Azure AD to authenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="dd3ce-112">Se utiliza el proyecto de ejemplo [AccountManagement][acct_mgmt_sample], disponible en GitHub, para guiarle en el uso de Azure AD con la biblioteca Batch Management .NET.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-112">We use the [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, to walk through using Azure AD with the Batch Management .NET library.</span></span>

<span data-ttu-id="dd3ce-113">Para más información sobre el uso de la biblioteca Batch Management .NET y el ejemplo de AccountManagement, consulte [Administración de cuentas y cuotas de Batch con la biblioteca cliente de administración de Batch para .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="dd3ce-113">To learn more about using the Batch Management .NET library and the AccountManagement sample, see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="dd3ce-114">Registro de la aplicación con Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd3ce-114">Register your application with Azure AD</span></span>

<span data-ttu-id="dd3ce-115">La [biblioteca de autenticación de Azure Active Directory][aad_adal] (ADAL) proporciona una interfaz de programación para Azure AD para usarla en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-115">The Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface to Azure AD for use within your applications.</span></span> <span data-ttu-id="dd3ce-116">Para llamar a ADAL desde la aplicación, debe registrar la aplicación en un inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-116">To call ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="dd3ce-117">Al registrar la aplicación, se facilita a Azure AD información acerca de esta, incluido un nombre para ella en el inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-117">When you register your application, you supply Azure AD with information about your application, including a name for it within the Azure AD tenant.</span></span> <span data-ttu-id="dd3ce-118">Azure AD proporciona un identificador de aplicación que se utiliza para asociar la aplicación con Azure AD en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-118">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="dd3ce-119">Para conocer más detalles acerca del identificador de la aplicación, consulte [Objetos de aplicación y de entidad de servicio de Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="dd3ce-119">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="dd3ce-120">Siga los pasos que aparecen en la sección [Incorporación de una aplicación](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) en [Integración de aplicaciones con Azure Active Directory][aad_integrate] para registrar la aplicación de ejemplo AccountManagement.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-120">To register the AccountManagement sample application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="dd3ce-121">Especifique **Aplicación de cliente nativo** como tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-121">Specify **Native Client Application** for the type of application.</span></span> <span data-ttu-id="dd3ce-122">El identificador URI OAuth 2.0 estándar del sector para el **URI de redireccionamiento** es `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-122">The industry standard OAuth 2.0 URI for the **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="dd3ce-123">Sin embargo, puede especificar un identificador URI válido (como `http://myaccountmanagementsample`) para el **identificador URI de redireccionamiento**, puesto que no necesita ser un punto de conexión real:</span><span class="sxs-lookup"><span data-stu-id="dd3ce-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for the **Redirect URI**, as it does not need to be a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="dd3ce-124">Una vez completado el proceso de registro, verá que aparecen el identificador de la aplicación y el identificador de objeto (entidad de servicio) para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-124">Once you complete the registration process, you'll see the application ID and the object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-the-azure-resource-manager-api-access-to-your-application"></a><span data-ttu-id="dd3ce-125">Concesión a la API de Azure Resource Manager de acceso a la aplicación</span><span class="sxs-lookup"><span data-stu-id="dd3ce-125">Grant the Azure Resource Manager API access to your application</span></span>

<span data-ttu-id="dd3ce-126">A continuación, debe delegar el acceso a la aplicación a la API de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-126">Next, you'll need to delegate access to your application to the Azure Resource Manager API.</span></span> <span data-ttu-id="dd3ce-127">El identificador de Azure AD para la API de Resource Manager es **Windows Azure Service Management API**.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-127">The Azure AD identifier for the Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="dd3ce-128">Siga estos pasos en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="dd3ce-128">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="dd3ce-129">En el panel de navegación izquierdo de Azure Portal, elija **Más servicios**, haga clic en **Registros de aplicaciones**y, luego, en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-129">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="dd3ce-130">Busque el nombre de la aplicación en la lista de registros de aplicación:</span><span class="sxs-lookup"><span data-stu-id="dd3ce-130">Search for the name of your application in the list of app registrations:</span></span>

    ![Buscar el nombre de la aplicación](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="dd3ce-132">Se mostrará la hoja **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-132">Display the **Settings** blade.</span></span> <span data-ttu-id="dd3ce-133">En la sección **Acceso de API**, seleccione **Permisos necesarios**.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-133">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="dd3ce-134">Haga clic en **Agregar** para agregar un nuevo permiso necesario.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-134">Click **Add** to add a new required permission.</span></span> 
5. <span data-ttu-id="dd3ce-135">En el paso 1, escriba **Windows Azure Service Management API**, seleccione esa API en la lista de resultados y haga clic en el botón **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-135">In step 1, enter **Windows Azure Service Management API**, select that API from the list of results, and click the **Select** button.</span></span>
6. <span data-ttu-id="dd3ce-136">En el paso 2, active la casilla de verificación situada junto a **Access Azure classic deployment model as organization users** (Acceder al modelo de implementación clásica como usuarios de la organización) y haga clic en el botón **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-136">In step 2, select the check box next to **Access Azure classic deployment model as organization users**, and click the **Select** button.</span></span>
7. <span data-ttu-id="dd3ce-137">Haga clic en el botón **Listo**.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-137">Click the **Done** button.</span></span>

<span data-ttu-id="dd3ce-138">La hoja **Permisos necesarios** ya muestra que se han concedido permisos a la aplicación para las API de ADAL y de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-138">The **Required Permissions** blade now shows that permissions to your application are granted to both the ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="dd3ce-139">La primera vez que registra la aplicación con Azure AD, se conceden permisos a ADAL de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-139">Permissions are granted to ADAL by default when you first register your app with Azure AD.</span></span>

![Delegar permisos para la API de Azure Resource Manager](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="dd3ce-141">Puntos de conexión de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd3ce-141">Azure AD endpoints</span></span>

<span data-ttu-id="dd3ce-142">Para autenticar sus soluciones de administración de Batch con Azure AD, necesitará dos puntos de conexión conocidos.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-142">To authenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="dd3ce-143">El **punto de conexión común de Azure AD** proporciona una interfaz genérica de recopilación de credenciales cuando no se proporciona un inquilino específico, como en el caso de la autenticación integrada:</span><span class="sxs-lookup"><span data-stu-id="dd3ce-143">The **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in the case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="dd3ce-144">El **punto de conexión de Azure Resource Manager** se usa para adquirir un token para la autenticación de solicitudes en el servicio de administración de Batch:</span><span class="sxs-lookup"><span data-stu-id="dd3ce-144">The **Azure Resource Manager endpoint** is used to acquire a token for authenticating requests to the Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="dd3ce-145">La aplicación de ejemplo de AccountManagement define las constantes para estos puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-145">The AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="dd3ce-146">No cambie estas constantes:</span><span class="sxs-lookup"><span data-stu-id="dd3ce-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="dd3ce-147">Referencia al identificador de aplicación</span><span class="sxs-lookup"><span data-stu-id="dd3ce-147">Reference your application ID</span></span> 

<span data-ttu-id="dd3ce-148">La aplicación cliente usa el identificador de aplicación (conocido también como identificador de cliente) para acceder a Azure AD en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-148">Your client application uses the application ID (also referred to as the client ID) to access Azure AD at runtime.</span></span> <span data-ttu-id="dd3ce-149">Una vez que haya registrado la aplicación en Azure Portal, actualice el código para usar el identificador de aplicación proporcionado por Azure AD para la aplicación registrada.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-149">Once you've registered your application in the Azure portal, update your code to use the application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="dd3ce-150">En la aplicación de ejemplo AccountManagement, copie el identificador de la aplicación desde Azure Portal a la constante adecuada:</span><span class="sxs-lookup"><span data-stu-id="dd3ce-150">In the AccountManagement sample application, copy your application ID from the Azure portal to the appropriate constant:</span></span>

```csharp
// Specify the unique identifier (the "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access the Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="dd3ce-151">Copie también el URI de redirección especificado durante el proceso de registro.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-151">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="dd3ce-152">El identificador URI de redireccionamiento especificado en el código debe coincidir con el identificador URI de redireccionamiento que proporcionó al registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-152">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application.</span></span>

```csharp
// The URI to which Azure AD will redirect in response to an OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need to be a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="dd3ce-153">Adquisición de un token de autenticación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd3ce-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="dd3ce-154">Después de registrar el ejemplo de AccountManagement en el inquilino de Azure AD y actualizar el código fuente de ejemplo con sus valores, el ejemplo estará listo para autenticarse con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-154">After you register the AccountManagement sample in the Azure AD tenant and update the sample source code with your values, the sample is ready to authenticate using Azure AD.</span></span> <span data-ttu-id="dd3ce-155">Cuando ejecute el ejemplo, ADAL intentará adquirir un token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-155">When you run the sample, the ADAL attempts to acquire an authentication token.</span></span> <span data-ttu-id="dd3ce-156">En este paso, le pedirá las credenciales de Microsoft:</span><span class="sxs-lookup"><span data-stu-id="dd3ce-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using the "common" AAD resource. This allows the application
// to query AAD for information that lies outside the application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="dd3ce-157">Después de proporcionar sus credenciales, la aplicación de ejemplo emitirá las solicitudes autenticadas para el servicio de administración de Batch.</span><span class="sxs-lookup"><span data-stu-id="dd3ce-157">After you provide your credentials, the sample application can proceed to issue authenticated requests to the Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="dd3ce-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dd3ce-158">Next steps</span></span>

<span data-ttu-id="dd3ce-159">Para más información sobre la ejecución de la [aplicación de ejemplo AccountManagement][acct_mgmt_sample], consulte [Administración de cuentas y cuotas de Batch con la biblioteca cliente de administración de Batch para .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="dd3ce-159">For more information on running the [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="dd3ce-160">Para más información acerca de Azure AD, consulte la [Documentación de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="dd3ce-160">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="dd3ce-161">Puede consultar los ejemplos detallados sobre el uso de ADAL que están disponibles en la biblioteca de [ejemplos de código de Azure](https://azure.microsoft.com/resources/samples/?service=active-directory).</span><span class="sxs-lookup"><span data-stu-id="dd3ce-161">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="dd3ce-162">Para autenticar aplicaciones de servicio de Batch con Azure AD, vea [Autenticación de soluciones de servicio de Batch con Active Directory](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="dd3ce-162">To authenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


<span data-ttu-id="dd3ce-163">[aad_about]: ../active-directory/active-directory-whatis.md "¿Qué es Azure Active Directory?"</span><span class="sxs-lookup"><span data-stu-id="dd3ce-163">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="dd3ce-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Escenarios de autenticación para Azure AD"</span><span class="sxs-lookup"><span data-stu-id="dd3ce-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="dd3ce-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integración de aplicaciones con Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="dd3ce-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
