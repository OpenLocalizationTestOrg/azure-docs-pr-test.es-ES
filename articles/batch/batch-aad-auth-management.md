---
title: "soluciones de administración de lotes de aaaUse Azure Active Directory tooauthenticate | Documentos de Microsoft"
description: Las aplicaciones compilan con el Administrador de recursos de Azure y proveedor de recursos de proceso por lotes de hello autenticarse con Azure AD.
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
ms.openlocfilehash: 192aa9f8d7cbfc0282a4a0c33ab1659f1f351525
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="32ce8-103">Autenticación de soluciones de administración de Batch con Active Directory</span><span class="sxs-lookup"><span data-stu-id="32ce8-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="32ce8-104">Las aplicaciones que llaman a servicio de administración de lotes de Azure de hello autenticarse con [Azure Active Directory] [ aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32ce8-104">Applications that call hello Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="32ce8-105">Azure Active Directory es el directorio basado en la nube multiinquilino y el servicio de administración de identidades de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="32ce8-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="32ce8-106">Azure por sí mismo utiliza Azure AD para la autenticación de Hola de sus clientes, los administradores de servicios y usuarios de la organización.</span><span class="sxs-lookup"><span data-stu-id="32ce8-106">Azure itself uses Azure AD for hello authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="32ce8-107">biblioteca de .NET de administración de lotes de Hello expone tipos para trabajar con cuentas de lote, las claves de cuenta, aplicaciones y paquetes de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="32ce8-107">hello Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="32ce8-108">biblioteca de .NET de administración de lotes de Hello es un cliente de proveedor de recursos de Azure y se utiliza junto con [Azure Resource Manager] [ resman_overview] toomanage estos recursos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="32ce8-108">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage these resources programmatically.</span></span> <span data-ttu-id="32ce8-109">Azure AD es las solicitudes de tooauthenticate necesario realizadas a través de cualquier cliente de proveedor de recursos de Azure, incluidos la biblioteca de .NET de administración de lotes de hello y [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="32ce8-109">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="32ce8-110">En este artículo se explican cómo utilizar el tooauthenticate de Azure AD desde las aplicaciones que utilizan la biblioteca de .NET de administración de lotes de Hola.</span><span class="sxs-lookup"><span data-stu-id="32ce8-110">In this article, we explore using Azure AD tooauthenticate from applications that use hello Batch Management .NET library.</span></span> <span data-ttu-id="32ce8-111">Le mostramos cómo toouse Azure AD tooauthenticate un administrador de la suscripción o Coadministrador, mediante la autenticación integrada.</span><span class="sxs-lookup"><span data-stu-id="32ce8-111">We show how toouse Azure AD tooauthenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="32ce8-112">Usamos hello [AccountManagment] [ acct_mgmt_sample] proyecto de ejemplo, disponible en GitHub, toowalk a través mediante Azure AD con la biblioteca de .NET de administración de lotes de Hola.</span><span class="sxs-lookup"><span data-stu-id="32ce8-112">We use hello [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, toowalk through using Azure AD with hello Batch Management .NET library.</span></span>

<span data-ttu-id="32ce8-113">vea toolearn más sobre el uso de la biblioteca de .NET de administración de lotes de Hola y ejemplo de Hola a AccountManagement, [lote administrar cuentas y cuotas con la biblioteca de cliente de administración de lotes de Hola para .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="32ce8-113">toolearn more about using hello Batch Management .NET library and hello AccountManagement sample, see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="32ce8-114">Registro de la aplicación con Azure AD</span><span class="sxs-lookup"><span data-stu-id="32ce8-114">Register your application with Azure AD</span></span>

<span data-ttu-id="32ce8-115">Hello Azure [biblioteca de autenticación de Active Directory] [ aad_adal] (AAL) proporciona una interfaz de programación de tooAzure AD para su uso dentro de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="32ce8-115">hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface tooAzure AD for use within your applications.</span></span> <span data-ttu-id="32ce8-116">toocall AAL desde su aplicación, debe registrar la aplicación en un inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32ce8-116">toocall ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="32ce8-117">Al registrar la aplicación, se facilita Azure AD con información acerca de la aplicación, incluido un nombre para ella en el inquilino de Azure AD Hola.</span><span class="sxs-lookup"><span data-stu-id="32ce8-117">When you register your application, you supply Azure AD with information about your application, including a name for it within hello Azure AD tenant.</span></span> <span data-ttu-id="32ce8-118">Azure AD, a continuación, proporciona un identificador de la aplicación usa tooassociate de su aplicación con Azure AD en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="32ce8-118">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="32ce8-119">vea toolearn más información sobre el identificador de la aplicación hello [aplicación y objetos de entidad de servicio en Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="32ce8-119">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="32ce8-120">Hola tooregister aplicación de ejemplo de AccountManagement, siga los pasos de Hola Hola [agregar una aplicación](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) sección [integrar aplicaciones con Azure Active Directory] [ aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="32ce8-120">tooregister hello AccountManagement sample application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="32ce8-121">Especifique **aplicación cliente nativa** para el tipo de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="32ce8-121">Specify **Native Client Application** for hello type of application.</span></span> <span data-ttu-id="32ce8-122">Hola sector estándar OAuth 2.0 URI para hello **URI de redireccionamiento** es `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="32ce8-122">hello industry standard OAuth 2.0 URI for hello **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="32ce8-123">Sin embargo, puede especificar cualquier URI válido (como `http://myaccountmanagementsample`) para hello **URI de redireccionamiento**, ya que no es necesario toobe un punto de conexión real:</span><span class="sxs-lookup"><span data-stu-id="32ce8-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for hello **Redirect URI**, as it does not need toobe a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="32ce8-124">Cuando se haya completado el proceso de registro de hello, verá Id. de aplicación de Hola y Hola identificador de objeto (entidad de servicio) que aparece para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="32ce8-124">Once you complete hello registration process, you'll see hello application ID and hello object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a><span data-ttu-id="32ce8-125">Conceda acceso tooyour aplicación de hello API del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="32ce8-125">Grant hello Azure Resource Manager API access tooyour application</span></span>

<span data-ttu-id="32ce8-126">A continuación, deberá toodelegate acceso tooyour aplicación toohello API del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="32ce8-126">Next, you'll need toodelegate access tooyour application toohello Azure Resource Manager API.</span></span> <span data-ttu-id="32ce8-127">identificador de Hello Azure AD para hello API del Administrador de recursos es **API de administración de servicios de Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="32ce8-127">hello Azure AD identifier for hello Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="32ce8-128">Siga estos pasos en hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="32ce8-128">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="32ce8-129">En el panel de navegación izquierdo de Hola de hello portal de Azure, elija **más servicios**, haga clic en **registros de aplicaciones**y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="32ce8-129">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="32ce8-130">Busque el nombre de saludo de la aplicación en la lista de Hola de registros de aplicación:</span><span class="sxs-lookup"><span data-stu-id="32ce8-130">Search for hello name of your application in hello list of app registrations:</span></span>

    ![Buscar el nombre de la aplicación](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="32ce8-132">Hola de presentación **configuración** hoja.</span><span class="sxs-lookup"><span data-stu-id="32ce8-132">Display hello **Settings** blade.</span></span> <span data-ttu-id="32ce8-133">Hola **el acceso de API** sección, seleccione **los permisos necesarios**.</span><span class="sxs-lookup"><span data-stu-id="32ce8-133">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="32ce8-134">Haga clic en **agregar** tooadd un nuevo permiso requerido.</span><span class="sxs-lookup"><span data-stu-id="32ce8-134">Click **Add** tooadd a new required permission.</span></span> 
5. <span data-ttu-id="32ce8-135">En el paso 1, escriba **API de administración de servicios de Windows Azure**, seleccione esa API de lista de Hola de resultados y haga clic en hello **seleccione** botón.</span><span class="sxs-lookup"><span data-stu-id="32ce8-135">In step 1, enter **Windows Azure Service Management API**, select that API from hello list of results, and click hello **Select** button.</span></span>
6. <span data-ttu-id="32ce8-136">En el paso 2, seleccione Hola casilla de verificación junto demasiado**modelo de implementación clásica de Azure de acceso como los usuarios de la organización**y haga clic en hello **seleccione** botón.</span><span class="sxs-lookup"><span data-stu-id="32ce8-136">In step 2, select hello check box next too**Access Azure classic deployment model as organization users**, and click hello **Select** button.</span></span>
7. <span data-ttu-id="32ce8-137">Haga clic en hello **realiza** botón.</span><span class="sxs-lookup"><span data-stu-id="32ce8-137">Click hello **Done** button.</span></span>

<span data-ttu-id="32ce8-138">Hola **permisos necesarios** hoja ahora muestra que aplicación de tooyour permisos se conceden tooboth Hola AAL y las API del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="32ce8-138">hello **Required Permissions** blade now shows that permissions tooyour application are granted tooboth hello ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="32ce8-139">Se conceden permisos tooADAL de forma predeterminada al registrar primero la aplicación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32ce8-139">Permissions are granted tooADAL by default when you first register your app with Azure AD.</span></span>

![Delegar permisos toohello API del Administrador de recursos de Azure](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="32ce8-141">Puntos de conexión de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32ce8-141">Azure AD endpoints</span></span>

<span data-ttu-id="32ce8-142">tooauthenticate sus soluciones de administración de lotes con Azure AD, necesitará dos puntos de conexión conocidos.</span><span class="sxs-lookup"><span data-stu-id="32ce8-142">tooauthenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="32ce8-143">Hola **extremo comunes de Azure AD** proporciona una credencial genérica recopilación interfaz cuando no se proporciona un inquilino específico, como en caso de hello de la autenticación integrada:</span><span class="sxs-lookup"><span data-stu-id="32ce8-143">hello **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in hello case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="32ce8-144">Hola **punto de conexión de Azure Resource Manager** es tooacquire usa un token para autenticar el servicio de administración de solicitudes toohello por lotes:</span><span class="sxs-lookup"><span data-stu-id="32ce8-144">hello **Azure Resource Manager endpoint** is used tooacquire a token for authenticating requests toohello Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="32ce8-145">aplicación de ejemplo de AccountManagement Hola define las constantes para estos puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="32ce8-145">hello AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="32ce8-146">No cambie estas constantes:</span><span class="sxs-lookup"><span data-stu-id="32ce8-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="32ce8-147">Referencia al identificador de aplicación</span><span class="sxs-lookup"><span data-stu-id="32ce8-147">Reference your application ID</span></span> 

<span data-ttu-id="32ce8-148">La aplicación cliente usa tooaccess (también denominado tooas Hola Id. de cliente) de Id. de aplicación hello Azure AD en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="32ce8-148">Your client application uses hello application ID (also referred tooas hello client ID) tooaccess Azure AD at runtime.</span></span> <span data-ttu-id="32ce8-149">Una vez que ha registrado su aplicación Hola portal de Azure, actualice el identificador de aplicación de código toouse Hola proporcionado por Azure AD para la aplicación registrada.</span><span class="sxs-lookup"><span data-stu-id="32ce8-149">Once you've registered your application in hello Azure portal, update your code toouse hello application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="32ce8-150">En la aplicación de ejemplo de AccountManagement hello, copie el identificador de la aplicación de constante adecuada de hello toohello de portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="32ce8-150">In hello AccountManagement sample application, copy your application ID from hello Azure portal toohello appropriate constant:</span></span>

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="32ce8-151">Copie también URI especificado durante el proceso de registro de hello de redirección de Hola.</span><span class="sxs-lookup"><span data-stu-id="32ce8-151">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="32ce8-152">Hola redirección URI especificado en el código debe coincidir con el URI que proporcionó al registrar la aplicación hello de redirección de Hola.</span><span class="sxs-lookup"><span data-stu-id="32ce8-152">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application.</span></span>

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="32ce8-153">Adquisición de un token de autenticación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32ce8-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="32ce8-154">Después de registrar el ejemplo de Hola AccountManagement en inquilino de Azure AD de Hola y actualizar el código fuente de ejemplo de Hola con sus valores, el ejemplo hello es tooauthenticate listo con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32ce8-154">After you register hello AccountManagement sample in hello Azure AD tenant and update hello sample source code with your values, hello sample is ready tooauthenticate using Azure AD.</span></span> <span data-ttu-id="32ce8-155">Al ejecutar el ejemplo hello, Hola AAL intenta tooacquire un token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="32ce8-155">When you run hello sample, hello ADAL attempts tooacquire an authentication token.</span></span> <span data-ttu-id="32ce8-156">En este paso, le pedirá las credenciales de Microsoft:</span><span class="sxs-lookup"><span data-stu-id="32ce8-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using hello "common" AAD resource. This allows hello application
// tooquery AAD for information that lies outside hello application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="32ce8-157">Después de proporcionar sus credenciales, aplicación de ejemplo de Hola puede continuar tooissue autenticado las solicitudes toohello servicio de administración de proceso por lotes.</span><span class="sxs-lookup"><span data-stu-id="32ce8-157">After you provide your credentials, hello sample application can proceed tooissue authenticated requests toohello Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="32ce8-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="32ce8-158">Next steps</span></span>

<span data-ttu-id="32ce8-159">Para obtener más información acerca de cómo ejecutar hello [aplicación de ejemplo de AccountManagement][acct_mgmt_sample], consulte [lote administrar cuentas y cuotas con la biblioteca de cliente de administración de lotes de Hola para .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="32ce8-159">For more information on running hello [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="32ce8-160">toolearn más información acerca de Azure AD, vea hello [documentación de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="32ce8-160">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="32ce8-161">Ejemplos detallados que muestran cómo toouse AAL está disponible en hello [ejemplos de código de Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) biblioteca.</span><span class="sxs-lookup"><span data-stu-id="32ce8-161">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="32ce8-162">las aplicaciones de servicio de lote tooauthenticate mediante Azure AD, vea [soluciones de servicio de lote autenticarse con Active Directory](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="32ce8-162">tooauthenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


[aad_about]: ../active-directory/active-directory-whatis.md "¿Qué es Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Escenarios de autenticación para Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integración de aplicaciones con Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
