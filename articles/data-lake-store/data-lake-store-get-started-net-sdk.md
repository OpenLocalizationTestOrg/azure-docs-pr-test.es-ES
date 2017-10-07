---
title: "las aplicaciones de .NET SDK toodevelop Hola de aaaUse en el almacén de Azure Data Lake | Documentos de Microsoft"
description: "Usar una cuenta de almacén de Data Lake del almacén .NET SDK de Azure Data Lake toocreate y realizar operaciones básicas en hello almacén de Data Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ea57d5a9-2929-4473-9d30-08227912aba7
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: nitinme
ms.openlocfilehash: cb3a1dfb2f6379f728069d66b0ee77ce0f838fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a><span data-ttu-id="de807-103">Introducción al Almacén de Azure Data Lake mediante SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="de807-103">Get started with Azure Data Lake Store using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="de807-104">Portal</span><span class="sxs-lookup"><span data-stu-id="de807-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="de807-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="de807-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="de807-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="de807-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="de807-107">SDK de Java</span><span class="sxs-lookup"><span data-stu-id="de807-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="de807-108">API de REST</span><span class="sxs-lookup"><span data-stu-id="de807-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="de807-109">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="de807-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="de807-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="de807-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="de807-111">Python</span><span class="sxs-lookup"><span data-stu-id="de807-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="de807-112">Obtenga información acerca de cómo hello toouse [almacén .NET SDK de Azure Data Lake](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform operaciones básicas, como crear carpetas, cargar y descargar archivos de datos, etcetera. Para más información sobre Data Lake, consulte [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="de807-112">Learn how toouse hello [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de807-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="de807-113">Prerequisites</span></span>
* <span data-ttu-id="de807-114">**Visual Studio 2013, 2015 o 2017**.</span><span class="sxs-lookup"><span data-stu-id="de807-114">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="de807-115">Estas instrucciones Hola usan Visual Studio 2015 Update 2.</span><span class="sxs-lookup"><span data-stu-id="de807-115">hello instructions below use Visual Studio 2015 Update 2.</span></span>

* <span data-ttu-id="de807-116">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="de807-116">**An Azure subscription**.</span></span> <span data-ttu-id="de807-117">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="de807-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="de807-118">**Cuenta del Almacén de Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="de807-118">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="de807-119">Para obtener instrucciones sobre cómo toocreate una cuenta, consulte [empezar a trabajar con el almacén de Azure Data Lake](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="de807-119">For instructions on how toocreate an account, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

* <span data-ttu-id="de807-120">**Cree una aplicación de Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de807-120">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="de807-121">Usar la aplicación de almacén de Data Lake de hello Azure AD aplicación tooauthenticate Hola con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de807-121">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="de807-122">Hay diferentes enfoques tooauthenticate con Azure AD, que son **autenticación de usuario final** o **autenticación del servicio a servicio**.</span><span class="sxs-lookup"><span data-stu-id="de807-122">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="de807-123">Para obtener instrucciones y obtener más información acerca de cómo tooauthenticate, consulte [autenticación de usuario final](data-lake-store-end-user-authenticate-using-active-directory.md) o [autenticación del servicio a servicio](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="de807-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="de807-124">Creación de una aplicación .NET</span><span class="sxs-lookup"><span data-stu-id="de807-124">Create a .NET application</span></span>
1. <span data-ttu-id="de807-125">Abra Visual Studio y cree una aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="de807-125">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="de807-126">De hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="de807-126">From hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="de807-127">De **nuevo proyecto**, escriba o seleccione Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="de807-127">From **New Project**, type or select hello following values:</span></span>

   | <span data-ttu-id="de807-128">Propiedad</span><span class="sxs-lookup"><span data-stu-id="de807-128">Property</span></span> | <span data-ttu-id="de807-129">Valor</span><span class="sxs-lookup"><span data-stu-id="de807-129">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="de807-130">Categoría</span><span class="sxs-lookup"><span data-stu-id="de807-130">Category</span></span> |<span data-ttu-id="de807-131">Plantillas/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="de807-131">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="de807-132">Plantilla</span><span class="sxs-lookup"><span data-stu-id="de807-132">Template</span></span> |<span data-ttu-id="de807-133">Aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="de807-133">Console Application</span></span> |
   | <span data-ttu-id="de807-134">Nombre</span><span class="sxs-lookup"><span data-stu-id="de807-134">Name</span></span> |<span data-ttu-id="de807-135">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="de807-135">CreateADLApplication</span></span> |
4. <span data-ttu-id="de807-136">Haga clic en **Aceptar** proyecto de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="de807-136">Click **OK** toocreate hello project.</span></span>
5. <span data-ttu-id="de807-137">Agregar proyecto de tooyour de paquetes de Nuget Hola.</span><span class="sxs-lookup"><span data-stu-id="de807-137">Add hello Nuget packages tooyour project.</span></span>

   1. <span data-ttu-id="de807-138">Haga clic en el nombre del proyecto Hola Hola el Explorador de soluciones y haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="de807-138">Right-click hello project name in hello Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="de807-139">Hola **Administrador de paquetes de Nuget** ficha, asegúrese de que **origen del paquete** se establece demasiado**nuget.org** y que **incluir versión preliminar** casilla de verificación está activada.</span><span class="sxs-lookup"><span data-stu-id="de807-139">In hello **Nuget Package Manager** tab, make sure that **Package source** is set too**nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="de807-140">Buscar e instalar los siguientes paquetes de NuGet de Hola:</span><span class="sxs-lookup"><span data-stu-id="de807-140">Search for and install hello following NuGet packages:</span></span>

      * <span data-ttu-id="de807-141">`Microsoft.Azure.Management.DataLake.Store` - En este tutorial se usa v2.1.3 (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="de807-141">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span></span>
      * <span data-ttu-id="de807-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - En este tutorial se usa v2.2.12.</span><span class="sxs-lookup"><span data-stu-id="de807-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span></span>

        <span data-ttu-id="de807-143">![Incorporación de un origen de Nuget](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Creación de una cuenta de Azure Data Lake")</span><span class="sxs-lookup"><span data-stu-id="de807-143">![Add a Nuget source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span></span>
   4. <span data-ttu-id="de807-144">Hola cerrar **Administrador de paquetes de Nuget**.</span><span class="sxs-lookup"><span data-stu-id="de807-144">Close hello **Nuget Package Manager**.</span></span>
6. <span data-ttu-id="de807-145">Abra **Program.cs**, eliminar código existente de hello y, a continuación, incluir Hola siguiendo las instrucciones tooadd referencias toonamespaces.</span><span class="sxs-lookup"><span data-stu-id="de807-145">Open **Program.cs**, delete hello existing code, and then include hello following statements tooadd references toonamespaces.</span></span>

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. <span data-ttu-id="de807-146">Declarar variables de hello tal y como se muestra a continuación y proporcione valores de hello para el nombre de almacén de Data Lake y nombre de grupo de recursos de Hola que ya existen.</span><span class="sxs-lookup"><span data-stu-id="de807-146">Declare hello variables as shown below, and provide hello values for Data Lake Store name and hello resource group name that already exist.</span></span> <span data-ttu-id="de807-147">Además, asegúrese de hello ruta de acceso y nombre local que proporciona aquí debe existir en el equipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="de807-147">Also, make sure hello local path and file name you provide here must exist on hello computer.</span></span> <span data-ttu-id="de807-148">Agregar Hola siguiente fragmento de código después de las declaraciones de espacio de nombres de Hola.</span><span class="sxs-lookup"><span data-stu-id="de807-148">Add hello following code snippet after hello namespace declarations.</span></span>

        namespace SdkSample
        {
            class Program
            {
                private static DataLakeStoreAccountManagementClient _adlsClient;
                private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;

                private static string _adlsAccountName;
                private static string _resourceGroupName;
                private static string _location;
                private static string _subId;

                private static void Main(string[] args)
                {
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with hello name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with hello name of hello resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

<span data-ttu-id="de807-149">Hola restantes secciones de artículo de hello, puede ver cómo toouse Hola operaciones de tooperform de métodos de .NET disponibles, como la autenticación, la carga de archivos etcetera.</span><span class="sxs-lookup"><span data-stu-id="de807-149">In hello remaining sections of hello article, you can see how toouse hello available .NET methods tooperform operations such as authentication, file upload, etc.</span></span>

## <a name="authentication"></a><span data-ttu-id="de807-150">Autenticación</span><span class="sxs-lookup"><span data-stu-id="de807-150">Authentication</span></span>

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a><span data-ttu-id="de807-151">Si utiliza la autenticación de usuario final (recomendada para este tutorial)</span><span class="sxs-lookup"><span data-stu-id="de807-151">If you are using end-user authentication (recommended for this tutorial)</span></span>

<span data-ttu-id="de807-152">Usar esta opción con un tooauthenticate de aplicación nativa de Azure AD existente de la aplicación **interactivamente**, que significa que podrá solicita tooenter sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="de807-152">Use this with an existing Azure AD native application tooauthenticate your application **interactively**, which means you will be prompted tooenter your Azure credentials.</span></span>

<span data-ttu-id="de807-153">Para facilitar su uso, el siguiente fragmento de Hola usa valores predeterminados para URI que funcionará con cualquier suscripción de Azure de redirección e identificador de cliente.</span><span class="sxs-lookup"><span data-stu-id="de807-153">For ease of use, hello snippet below uses default values for client ID and redirect URI that will work with any Azure subscription.</span></span> <span data-ttu-id="de807-154">toohelp completar este tutorial con mayor rapidez, se recomienda que usar este enfoque.</span><span class="sxs-lookup"><span data-stu-id="de807-154">toohelp you complete this tutorial faster, we recommend you use this approach.</span></span> <span data-ttu-id="de807-155">En el siguiente fragmento de hello, basta con que proporcione el valor de hello para el identificador del inquilino.</span><span class="sxs-lookup"><span data-stu-id="de807-155">In hello snippet below, just provide hello value for your tenant ID.</span></span> <span data-ttu-id="de807-156">Puede recuperarlo mediante instrucciones de hello proporcionadas en [crear un Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="de807-156">You can retrieve it using hello instructions provided at [Create an Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

<span data-ttu-id="de807-157">Un par de cosas tooknow acerca de este fragmento de código anterior:</span><span class="sxs-lookup"><span data-stu-id="de807-157">A couple of things tooknow about this snippet above:</span></span>

* <span data-ttu-id="de807-158">toohelp completar el tutorial de hello con mayor rapidez, este fragmento de código utiliza un Azure AD Id. de dominio y el cliente que está disponible de forma predeterminada para todas las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="de807-158">toohelp you complete hello tutorial faster, this snippet uses an an Azure AD domain and client ID that is available by default for all Azure subscriptions.</span></span> <span data-ttu-id="de807-159">Por lo tanto, puede **usar este fragmento de código tal cual en la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="de807-159">So, you can **use this snippet as-is in your application**.</span></span>
* <span data-ttu-id="de807-160">Sin embargo, si desea toouse su propio dominio de Azure AD e Id. de aplicación cliente, debe crear una aplicación nativa de Azure AD y, a continuación, use hello Azure AD ID, Id. de cliente, de inquilinos y URI de redirección de la aplicación hello creado.</span><span class="sxs-lookup"><span data-stu-id="de807-160">However, if you do want toouse your own Azure AD domain and application client ID, you must create an Azure AD native application and then use hello Azure AD tenant ID, client ID, and redirect URI for hello application you created.</span></span> <span data-ttu-id="de807-161">Consulte [Autenticación de usuario final con Data Lake Store mediante Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="de807-161">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span></span>

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a><span data-ttu-id="de807-162">Si utiliza la autenticación de servicio a servicio con el secreto de cliente</span><span class="sxs-lookup"><span data-stu-id="de807-162">If you are using service-to-service authentication with client secret</span></span>
<span data-ttu-id="de807-163">Hola siguiente fragmento de código puede ser tooauthenticate usa la aplicación **una manera no interactiva**, utilizando la clave secreta de cliente de Hola / clave para una identidad de aplicación / servicio.</span><span class="sxs-lookup"><span data-stu-id="de807-163">hello following snippet can be used tooauthenticate your application **non-interactively**, using hello client secret / key for an application / service principal.</span></span> <span data-ttu-id="de807-164">Utilícelo con una aplicación web de Azure AD ya existente.</span><span class="sxs-lookup"><span data-stu-id="de807-164">Use this with an existing Azure AD "Web App" Application.</span></span> <span data-ttu-id="de807-165">Para obtener instrucciones sobre cómo ver la aplicación web de toocreate hello Azure AD y cómo tooretrieve Hola Id. de cliente y el secreto de cliente necesario en la siguiente, el fragmento de hello [crear una aplicación de directorio activo para la autenticación de servicio al servicio con datos Almacén Lake](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="de807-165">For instructions on how toocreate hello Azure AD web application and how tooretrieve hello client ID and client secret required in hello snippet below, see [Create an Active Directory Application for service-to-service authentication with Data Lake Store](data-lake-store-authenticate-using-active-directory.md).</span></span>

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a><span data-ttu-id="de807-166">Si utilice autenticación de servicio a servicio con certificado</span><span class="sxs-lookup"><span data-stu-id="de807-166">If you are using service-to-service authentication with certificate</span></span>

<span data-ttu-id="de807-167">Como una tercera opción, hello siguiente fragmento de código puede ser tooauthenticate usa la aplicación **una manera no interactiva**, utilizando el certificado de Hola para una aplicación de Azure Active Directory / entidad de seguridad de servicio.</span><span class="sxs-lookup"><span data-stu-id="de807-167">As a third option, hello following snippet can be used tooauthenticate your application **non-interactively**, using hello certificate for an Azure Active Directory application / service principal.</span></span> <span data-ttu-id="de807-168">Utilícelo con una [aplicación de Azure AD con certificados](../azure-resource-manager/resource-group-authenticate-service-principal.md) ya existente.</span><span class="sxs-lookup"><span data-stu-id="de807-168">Use this with an existing [Azure AD Application with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a><span data-ttu-id="de807-169">Creación de objetos de cliente</span><span class="sxs-lookup"><span data-stu-id="de807-169">Create client objects</span></span>
<span data-ttu-id="de807-170">Hello fragmento de código siguiente crea cuenta de almacén de Data Lake hello y filesystem objetos de cliente, que se usan tooissue solicitudes de servicio de toohello.</span><span class="sxs-lookup"><span data-stu-id="de807-170">hello following snippet creates hello Data Lake Store account and filesystem client objects, which are used tooissue requests toohello service.</span></span>

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a><span data-ttu-id="de807-171">Enumeración de todas las cuentas de Data Lake Store de una suscripción</span><span class="sxs-lookup"><span data-stu-id="de807-171">List all Data Lake Store accounts within a subscription</span></span>
<span data-ttu-id="de807-172">Hello fragmento de código siguiente enumera todas las cuentas de almacén de Data Lake dentro de una determinada suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="de807-172">hello following snippet lists all Data Lake Store accounts within a given Azure subscription.</span></span>

    // List all ADLS accounts within hello subscription
    public static async Task<List<DataLakeStoreAccount>> ListAdlStoreAccounts()
    {
        var response = await _adlsClient.Account.ListAsync();
        var accounts = new List<DataLakeStoreAccount>(response);

        while (response.NextPageLink != null)
        {
            response = _adlsClient.Account.ListNext(response.NextPageLink);
            accounts.AddRange(response);
        }

        return accounts;
    }

## <a name="create-a-directory"></a><span data-ttu-id="de807-173">Creación de directorios</span><span class="sxs-lookup"><span data-stu-id="de807-173">Create a directory</span></span>
<span data-ttu-id="de807-174">Hola fragmento siguiente muestra un `CreateDirectory` método que puede utilizar un directorio en una cuenta de almacén de Data Lake toocreate.</span><span class="sxs-lookup"><span data-stu-id="de807-174">hello following snippet shows a `CreateDirectory` method that you can use toocreate a directory within a Data Lake Store account.</span></span>

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a><span data-ttu-id="de807-175">Cargar un archivo</span><span class="sxs-lookup"><span data-stu-id="de807-175">Upload a file</span></span>
<span data-ttu-id="de807-176">Hola fragmento siguiente muestra un `UploadFile` método que puede utilizar tooupload archivos tooa cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="de807-176">hello following snippet shows an `UploadFile` method that you can use tooupload files tooa Data Lake Store account.</span></span>

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

<span data-ttu-id="de807-177">Hola SDK admite recursiva carga y descarga entre una ruta de acceso de archivo local y una ruta de acceso del archivo de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="de807-177">hello SDK supports recursive upload and download between a local file path and a Data Lake Store file path.</span></span>    

## <a name="get-file-or-directory-info"></a><span data-ttu-id="de807-178">Obtención de información de un archivo o directorio</span><span class="sxs-lookup"><span data-stu-id="de807-178">Get file or directory info</span></span>
<span data-ttu-id="de807-179">Hola fragmento siguiente muestra un `GetItemInfo` método que puede utilizar tooretrieve información acerca de un archivo o directorio disponible en el almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="de807-179">hello following snippet shows a `GetItemInfo` method that you can use tooretrieve information about a file or directory available in Data Lake Store.</span></span>

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a><span data-ttu-id="de807-180">Enumeración de archivos o directorios</span><span class="sxs-lookup"><span data-stu-id="de807-180">List file or directories</span></span>
<span data-ttu-id="de807-181">Hola fragmento siguiente muestra un `ListItem` método que puede usar toolist Hola archivos y directorios en una cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="de807-181">hello following snippet shows a `ListItem` method that can use toolist hello file and directories in a Data Lake Store account.</span></span>

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a><span data-ttu-id="de807-182">Concatenación de archivos</span><span class="sxs-lookup"><span data-stu-id="de807-182">Concatenate files</span></span>
<span data-ttu-id="de807-183">Hola fragmento siguiente muestra un `ConcatenateFiles` método que se usan archivos de tooconcatenate.</span><span class="sxs-lookup"><span data-stu-id="de807-183">hello following snippet shows a `ConcatenateFiles` method that you use tooconcatenate files.</span></span>

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a><span data-ttu-id="de807-184">Anexar el archivo de tooa</span><span class="sxs-lookup"><span data-stu-id="de807-184">Append tooa file</span></span>
<span data-ttu-id="de807-185">Hola fragmento siguiente muestra un `AppendToFile` método que use anexar el archivo de tooa de datos ya estén almacenado en una cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="de807-185">hello following snippet shows a `AppendToFile` method that you use append data tooa file already stored in a Data Lake Store account.</span></span>

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a><span data-ttu-id="de807-186">Descarga de un archivo</span><span class="sxs-lookup"><span data-stu-id="de807-186">Download a file</span></span>
<span data-ttu-id="de807-187">Hola fragmento siguiente muestra un `DownloadFile` método que se utiliza un archivo de una cuenta de almacén de Data Lake toodownload.</span><span class="sxs-lookup"><span data-stu-id="de807-187">hello following snippet shows a `DownloadFile` method that you use toodownload a file from a Data Lake Store account.</span></span>

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a><span data-ttu-id="de807-188">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="de807-188">Next steps</span></span>
* [<span data-ttu-id="de807-189">Protección de los datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="de807-189">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="de807-190">Uso de Análisis de Azure Data Lake con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="de807-190">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="de807-191">Uso de HDInsight de Azure con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="de807-191">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="de807-192">Referencia de SDK de .NET de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="de807-192">Data Lake Store .NET SDK Reference</span></span>](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [<span data-ttu-id="de807-193">Referencia de REST de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="de807-193">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
