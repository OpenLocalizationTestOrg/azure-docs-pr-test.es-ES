---
title: Uso del SDK de .NET para desarrollar aplicaciones en Azure Data Lake Store | Microsoft Docs
description: "Uso del SDK de .NET de Azure Data Lake Store para crear una cuenta de Data Lake Store y realizar operaciones básicas en este"
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
ms.openlocfilehash: 70f94a07b0102e3135eaf85e5877e3502762d7e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a><span data-ttu-id="b091e-103">Introducción al Almacén de Azure Data Lake mediante SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="b091e-103">Get started with Azure Data Lake Store using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b091e-104">Portal</span><span class="sxs-lookup"><span data-stu-id="b091e-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="b091e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b091e-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="b091e-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="b091e-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="b091e-107">SDK de Java</span><span class="sxs-lookup"><span data-stu-id="b091e-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="b091e-108">API de REST</span><span class="sxs-lookup"><span data-stu-id="b091e-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="b091e-109">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b091e-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="b091e-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="b091e-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="b091e-111">Python</span><span class="sxs-lookup"><span data-stu-id="b091e-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="b091e-112">Aprenda a usar el [SDK de .NET de Azure Data Lake Store](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) para realizar operaciones básicas como crear carpetas, cargar y descargar archivos de datos, etc. Para más información sobre Data Lake, consulte [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b091e-112">Learn how to use the [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b091e-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b091e-113">Prerequisites</span></span>
* <span data-ttu-id="b091e-114">**Visual Studio 2013, 2015 o 2017**.</span><span class="sxs-lookup"><span data-stu-id="b091e-114">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="b091e-115">Las instrucciones siguientes usan Visual Studio 2015 Update 2.</span><span class="sxs-lookup"><span data-stu-id="b091e-115">The instructions below use Visual Studio 2015 Update 2.</span></span>

* <span data-ttu-id="b091e-116">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="b091e-116">**An Azure subscription**.</span></span> <span data-ttu-id="b091e-117">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b091e-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="b091e-118">**Cuenta del Almacén de Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="b091e-118">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="b091e-119">Para obtener instrucciones acerca de cómo crear una cuenta, consulte [Introducción a Azure Data Lake Store mediante Azure Portal](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b091e-119">For instructions on how to create an account, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

* <span data-ttu-id="b091e-120">**Cree una aplicación de Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b091e-120">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="b091e-121">Utilice la aplicación Azure AD para autenticar la aplicación Data Lake Store con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b091e-121">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="b091e-122">Existen diferentes enfoques para realizar la autenticación con Azure AD, que son la **autenticación de usuario final** o la **autenticación de servicio a servicio**.</span><span class="sxs-lookup"><span data-stu-id="b091e-122">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="b091e-123">Para obtener instrucciones y más información acerca de cómo realizar la autenticación, consulte [Autenticación de usuario final con Data Lake Store mediante Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md) o [Autenticación entre servicios con Data Lake Store mediante Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="b091e-123">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="b091e-124">Creación de una aplicación .NET</span><span class="sxs-lookup"><span data-stu-id="b091e-124">Create a .NET application</span></span>
1. <span data-ttu-id="b091e-125">Abra Visual Studio y cree una aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="b091e-125">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="b091e-126">En el menú **Archivo**, haga clic en **Nuevo** y en **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="b091e-126">From the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="b091e-127">En **Nuevo proyecto**, escriba o seleccione los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="b091e-127">From **New Project**, type or select the following values:</span></span>

   | <span data-ttu-id="b091e-128">Propiedad</span><span class="sxs-lookup"><span data-stu-id="b091e-128">Property</span></span> | <span data-ttu-id="b091e-129">Valor</span><span class="sxs-lookup"><span data-stu-id="b091e-129">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="b091e-130">Categoría</span><span class="sxs-lookup"><span data-stu-id="b091e-130">Category</span></span> |<span data-ttu-id="b091e-131">Plantillas/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="b091e-131">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="b091e-132">Plantilla</span><span class="sxs-lookup"><span data-stu-id="b091e-132">Template</span></span> |<span data-ttu-id="b091e-133">Aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="b091e-133">Console Application</span></span> |
   | <span data-ttu-id="b091e-134">Nombre</span><span class="sxs-lookup"><span data-stu-id="b091e-134">Name</span></span> |<span data-ttu-id="b091e-135">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="b091e-135">CreateADLApplication</span></span> |
4. <span data-ttu-id="b091e-136">Haga clic en **Aceptar** para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="b091e-136">Click **OK** to create the project.</span></span>
5. <span data-ttu-id="b091e-137">Agregue los paquetes de Nuget al proyecto.</span><span class="sxs-lookup"><span data-stu-id="b091e-137">Add the Nuget packages to your project.</span></span>

   1. <span data-ttu-id="b091e-138">Haga clic con el botón derecho en el Explorador de soluciones y haga clic en **Administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b091e-138">Right-click the project name in the Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="b091e-139">En la pestaña **Administrador de paquetes NuGet**, asegúrese de que la opción **Origen del paquete** esté establecida en **nuget.org** y que esté activada la casilla **Incluir versión previa**.</span><span class="sxs-lookup"><span data-stu-id="b091e-139">In the **Nuget Package Manager** tab, make sure that **Package source** is set to **nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="b091e-140">Busque e instale los siguientes paquetes NuGet:</span><span class="sxs-lookup"><span data-stu-id="b091e-140">Search for and install the following NuGet packages:</span></span>

      * <span data-ttu-id="b091e-141">`Microsoft.Azure.Management.DataLake.Store` - En este tutorial se usa v2.1.3 (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="b091e-141">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span></span>
      * <span data-ttu-id="b091e-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - En este tutorial se usa v2.2.12.</span><span class="sxs-lookup"><span data-stu-id="b091e-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span></span>

        <span data-ttu-id="b091e-143">![Incorporación de un origen de Nuget](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Creación de una cuenta de Azure Data Lake")</span><span class="sxs-lookup"><span data-stu-id="b091e-143">![Add a Nuget source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span></span>
   4. <span data-ttu-id="b091e-144">Cierre el **Administrador de paquetes Nuget**.</span><span class="sxs-lookup"><span data-stu-id="b091e-144">Close the **Nuget Package Manager**.</span></span>
6. <span data-ttu-id="b091e-145">Abra **Program.cs**, elimine el código existente e incluya las siguientes instrucciones para agregar referencias a espacios de nombres.</span><span class="sxs-lookup"><span data-stu-id="b091e-145">Open **Program.cs**, delete the existing code, and then include the following statements to add references to namespaces.</span></span>

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. <span data-ttu-id="b091e-146">Declare las variables como se muestra a continuación y especifique los valores del nombre de Data Lake Store y del nombre del grupo de recursos que ya existen.</span><span class="sxs-lookup"><span data-stu-id="b091e-146">Declare the variables as shown below, and provide the values for Data Lake Store name and the resource group name that already exist.</span></span> <span data-ttu-id="b091e-147">Además, asegúrese de que la ruta de acceso local y el nombre de archivo que proporcione aquí deben existir en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b091e-147">Also, make sure the local path and file name you provide here must exist on the computer.</span></span> <span data-ttu-id="b091e-148">Agregue el siguiente fragmento de código después de las declaraciones de espacios de nombres.</span><span class="sxs-lookup"><span data-stu-id="b091e-148">Add the following code snippet after the namespace declarations.</span></span>

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
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with the name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with the name of the resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

<span data-ttu-id="b091e-149">En las restantes secciones de este artículo, se puede ver cómo se utilizan los métodos .NET disponibles para realizar operaciones como la autenticación, la carga de archivos, etc.</span><span class="sxs-lookup"><span data-stu-id="b091e-149">In the remaining sections of the article, you can see how to use the available .NET methods to perform operations such as authentication, file upload, etc.</span></span>

## <a name="authentication"></a><span data-ttu-id="b091e-150">Autenticación</span><span class="sxs-lookup"><span data-stu-id="b091e-150">Authentication</span></span>

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a><span data-ttu-id="b091e-151">Si utiliza la autenticación de usuario final (recomendada para este tutorial)</span><span class="sxs-lookup"><span data-stu-id="b091e-151">If you are using end-user authentication (recommended for this tutorial)</span></span>

<span data-ttu-id="b091e-152">Úsela con una aplicación nativa existente de Azure AD para autenticar la aplicación **interactivamente**, lo que significa que se le pedirá que escriba sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="b091e-152">Use this with an existing Azure AD native application to authenticate your application **interactively**, which means you will be prompted to enter your Azure credentials.</span></span>

<span data-ttu-id="b091e-153">Para facilitar su uso, el siguiente fragmento de código usa valores predeterminados para un identificador de cliente y un URI de redirección que funcionan con cualquier suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="b091e-153">For ease of use, the snippet below uses default values for client ID and redirect URI that will work with any Azure subscription.</span></span> <span data-ttu-id="b091e-154">Para ayudarle a completar este tutorial más rápido, se recomienda que utilice este enfoque.</span><span class="sxs-lookup"><span data-stu-id="b091e-154">To help you complete this tutorial faster, we recommend you use this approach.</span></span> <span data-ttu-id="b091e-155">En el siguiente fragmento de código, bastará con que proporcione el valor del identificador del inquilino.</span><span class="sxs-lookup"><span data-stu-id="b091e-155">In the snippet below, just provide the value for your tenant ID.</span></span> <span data-ttu-id="b091e-156">Puede recuperarlo mediante las instrucciones proporcionadas en [Creación de una aplicación de Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="b091e-156">You can retrieve it using the instructions provided at [Create an Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

    // User login via interactive popup
    // Use the client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with the user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

<span data-ttu-id="b091e-157">Dos cosas que conviene saber acerca del fragmento de código anterior:</span><span class="sxs-lookup"><span data-stu-id="b091e-157">A couple of things to know about this snippet above:</span></span>

* <span data-ttu-id="b091e-158">Para ayudarle a completar este tutorial más rápido, este fragmento de código usa un identificador de dominio y cliente de Azure AD que está disponible de manera predeterminada para todas las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="b091e-158">To help you complete the tutorial faster, this snippet uses an an Azure AD domain and client ID that is available by default for all Azure subscriptions.</span></span> <span data-ttu-id="b091e-159">Por lo tanto, puede **usar este fragmento de código tal cual en la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="b091e-159">So, you can **use this snippet as-is in your application**.</span></span>
* <span data-ttu-id="b091e-160">Sin embargo, si desea utilizar su propio identificador de cliente de dominio y de aplicación de Azure AD, debe crear una aplicación nativa de Azure AD y, después, utilizar el identificador de inquilino de Azure AD, el identificador de cliente y el identificador URI de redirección para la aplicación que ha creado.</span><span class="sxs-lookup"><span data-stu-id="b091e-160">However, if you do want to use your own Azure AD domain and application client ID, you must create an Azure AD native application and then use the Azure AD tenant ID, client ID, and redirect URI for the application you created.</span></span> <span data-ttu-id="b091e-161">Consulte [Autenticación de usuario final con Data Lake Store mediante Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="b091e-161">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span></span>

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a><span data-ttu-id="b091e-162">Si utiliza la autenticación de servicio a servicio con el secreto de cliente</span><span class="sxs-lookup"><span data-stu-id="b091e-162">If you are using service-to-service authentication with client secret</span></span>
<span data-ttu-id="b091e-163">El siguiente fragmento de código se puede utilizar para autenticar la aplicación de forma **no interactiva**, para lo que se usa el secreto o la clave del cliente para una identidad de entidad de servicio o aplicación.</span><span class="sxs-lookup"><span data-stu-id="b091e-163">The following snippet can be used to authenticate your application **non-interactively**, using the client secret / key for an application / service principal.</span></span> <span data-ttu-id="b091e-164">Utilícelo con una aplicación web de Azure AD ya existente.</span><span class="sxs-lookup"><span data-stu-id="b091e-164">Use this with an existing Azure AD "Web App" Application.</span></span> <span data-ttu-id="b091e-165">Para obtener instrucciones sobre cómo crear la aplicación web de Azure AD y cómo recuperar el identificador y el secreto de cliente y necesarios en el siguiente fragmento de código, consulte [Autenticación entre servicios con Data Lake Store mediante Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="b091e-165">For instructions on how to create the Azure AD web application and how to retrieve the client ID and client secret required in the snippet below, see [Create an Active Directory Application for service-to-service authentication with Data Lake Store](data-lake-store-authenticate-using-active-directory.md).</span></span>

    // Service principal / appplication authentication with client secret / key
    // Use the client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a><span data-ttu-id="b091e-166">Si utilice autenticación de servicio a servicio con certificado</span><span class="sxs-lookup"><span data-stu-id="b091e-166">If you are using service-to-service authentication with certificate</span></span>

<span data-ttu-id="b091e-167">Como alternativa, el siguiente fragmento de código puede utilizarse para autenticar la aplicación de forma **no interactiva**, para lo que se usará el certificado para una entidad de servicio o aplicación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b091e-167">As a third option, the following snippet can be used to authenticate your application **non-interactively**, using the certificate for an Azure Active Directory application / service principal.</span></span> <span data-ttu-id="b091e-168">Utilícelo con una [aplicación de Azure AD con certificados](../azure-resource-manager/resource-group-authenticate-service-principal.md) ya existente.</span><span class="sxs-lookup"><span data-stu-id="b091e-168">Use this with an existing [Azure AD Application with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    // Service principal / application authentication with certificate
    // Use the client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a><span data-ttu-id="b091e-169">Creación de objetos de cliente</span><span class="sxs-lookup"><span data-stu-id="b091e-169">Create client objects</span></span>
<span data-ttu-id="b091e-170">El fragmento de código siguiente crea los objetos de cliente del sistema de archivos y cuenta de Data Lake Store, que se usan para emitir solicitudes al servicio.</span><span class="sxs-lookup"><span data-stu-id="b091e-170">The following snippet creates the Data Lake Store account and filesystem client objects, which are used to issue requests to the service.</span></span>

    // Create client objects and set the subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a><span data-ttu-id="b091e-171">Enumeración de todas las cuentas de Data Lake Store de una suscripción</span><span class="sxs-lookup"><span data-stu-id="b091e-171">List all Data Lake Store accounts within a subscription</span></span>
<span data-ttu-id="b091e-172">El siguiente fragmento de código enumera todas las cuentas de Data Lake Store de una suscripción de Azure dada.</span><span class="sxs-lookup"><span data-stu-id="b091e-172">The following snippet lists all Data Lake Store accounts within a given Azure subscription.</span></span>

    // List all ADLS accounts within the subscription
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

## <a name="create-a-directory"></a><span data-ttu-id="b091e-173">Creación de directorios</span><span class="sxs-lookup"><span data-stu-id="b091e-173">Create a directory</span></span>
<span data-ttu-id="b091e-174">El siguiente fragmento muestra un método `CreateDirectory` que puede utilizar para crear un directorio en una cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b091e-174">The following snippet shows a `CreateDirectory` method that you can use to create a directory within a Data Lake Store account.</span></span>

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a><span data-ttu-id="b091e-175">Cargar un archivo</span><span class="sxs-lookup"><span data-stu-id="b091e-175">Upload a file</span></span>
<span data-ttu-id="b091e-176">El siguiente fragmento muestra un método `UploadFile` que puede utilizar para cargar archivos en una cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b091e-176">The following snippet shows an `UploadFile` method that you can use to upload files to a Data Lake Store account.</span></span>

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

<span data-ttu-id="b091e-177">El SDK admite la carga y descarga recursiva entre una ruta de acceso de un archivo local y la ruta de acceso de un archivo de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b091e-177">The SDK supports recursive upload and download between a local file path and a Data Lake Store file path.</span></span>    

## <a name="get-file-or-directory-info"></a><span data-ttu-id="b091e-178">Obtención de información de un archivo o directorio</span><span class="sxs-lookup"><span data-stu-id="b091e-178">Get file or directory info</span></span>
<span data-ttu-id="b091e-179">El siguiente fragmento muestra un método `GetItemInfo` que puede utilizar para recuperar la información sobre un archivo o directorio disponible en Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b091e-179">The following snippet shows a `GetItemInfo` method that you can use to retrieve information about a file or directory available in Data Lake Store.</span></span>

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a><span data-ttu-id="b091e-180">Enumeración de archivos o directorios</span><span class="sxs-lookup"><span data-stu-id="b091e-180">List file or directories</span></span>
<span data-ttu-id="b091e-181">El siguiente fragmento muestra un método `ListItem` que puede utilizar para enumerar el archivo y los directorios de una cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b091e-181">The following snippet shows a `ListItem` method that can use to list the file and directories in a Data Lake Store account.</span></span>

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a><span data-ttu-id="b091e-182">Concatenación de archivos</span><span class="sxs-lookup"><span data-stu-id="b091e-182">Concatenate files</span></span>
<span data-ttu-id="b091e-183">El siguiente fragmento muestra un método `ConcatenateFiles` que se utiliza para concatenar archivos.</span><span class="sxs-lookup"><span data-stu-id="b091e-183">The following snippet shows a `ConcatenateFiles` method that you use to concatenate files.</span></span>

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-to-a-file"></a><span data-ttu-id="b091e-184">Anexión a un archivo</span><span class="sxs-lookup"><span data-stu-id="b091e-184">Append to a file</span></span>
<span data-ttu-id="b091e-185">El siguiente fragmento muestra un método `AppendToFile` que se utiliza para anexar datos a un archivo que ya está almacenado en una cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b091e-185">The following snippet shows a `AppendToFile` method that you use append data to a file already stored in a Data Lake Store account.</span></span>

    // Append to file
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a><span data-ttu-id="b091e-186">Descarga de un archivo</span><span class="sxs-lookup"><span data-stu-id="b091e-186">Download a file</span></span>
<span data-ttu-id="b091e-187">El siguiente fragmento muestra un método `DownloadFile` que se utiliza para descargar un archivo de una cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b091e-187">The following snippet shows a `DownloadFile` method that you use to download a file from a Data Lake Store account.</span></span>

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a><span data-ttu-id="b091e-188">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b091e-188">Next steps</span></span>
* [<span data-ttu-id="b091e-189">Protección de los datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="b091e-189">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="b091e-190">Uso de Análisis de Azure Data Lake con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="b091e-190">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="b091e-191">Uso de HDInsight de Azure con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="b091e-191">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="b091e-192">Referencia de SDK de .NET de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b091e-192">Data Lake Store .NET SDK Reference</span></span>](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [<span data-ttu-id="b091e-193">Referencia de REST de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b091e-193">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
