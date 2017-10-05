---
title: "Administración de Azure Data Lake Analytics con el SDK de .NET de Azure | Microsoft Docs"
description: "Aprenda a administrar trabajos, orígenes de datos y usuarios de Análisis de Data Lake. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 811d172d-9873-4ce9-a6d5-c1a26b374c79
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 0f8a95f96ce4c816dfb9132923faa9a9bf20c205
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a><span data-ttu-id="2609b-103">Administración de Azure Data Lake Analytics con el SDK de .NET para Azure</span><span class="sxs-lookup"><span data-stu-id="2609b-103">Manage Azure Data Lake Analytics using Azure .NET SDK</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="2609b-104">Obtenga información sobre cómo administrar cuentas, orígenes de datos, usuarios y trabajos de Azure Data Lake Analytics mediante el SDK de .NET para Azure.</span><span class="sxs-lookup"><span data-stu-id="2609b-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure .NET SDK.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2609b-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2609b-105">Prerequisites</span></span>

* <span data-ttu-id="2609b-106">**Visual Studio 2015, Visual Studio 2013 Update 4 o Visual Studio 2012 con Visual C++ instalado**.</span><span class="sxs-lookup"><span data-stu-id="2609b-106">**Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed**.</span></span>
* <span data-ttu-id="2609b-107">**SDK de Microsoft Azure para .NET versión 2.5 o posterior**.</span><span class="sxs-lookup"><span data-stu-id="2609b-107">**Microsoft Azure SDK for .NET version 2.5 or above**.</span></span>  <span data-ttu-id="2609b-108">Instálelo usando el [instalador de plataforma web](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="2609b-108">Install it using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="2609b-109">**Paquetes de NuGet requeridos**</span><span class="sxs-lookup"><span data-stu-id="2609b-109">**Required NuGet Packages**</span></span>

### <a name="install-nuget-packages"></a><span data-ttu-id="2609b-110">Instalación de paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="2609b-110">Install NuGet packages</span></span>

|<span data-ttu-id="2609b-111">Paquete</span><span class="sxs-lookup"><span data-stu-id="2609b-111">Package</span></span>|<span data-ttu-id="2609b-112">Versión</span><span class="sxs-lookup"><span data-stu-id="2609b-112">Version</span></span>|
|-------|-------|
|[<span data-ttu-id="2609b-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span><span class="sxs-lookup"><span data-stu-id="2609b-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span></span>](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime.Azure.Authentication)| <span data-ttu-id="2609b-114">2.3.1</span><span class="sxs-lookup"><span data-stu-id="2609b-114">2.3.1</span></span>|
|[<span data-ttu-id="2609b-115">Microsoft.Azure.Management.DataLake.Analytics</span><span class="sxs-lookup"><span data-stu-id="2609b-115">Microsoft.Azure.Management.DataLake.Analytics</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)|<span data-ttu-id="2609b-116">3.0.0</span><span class="sxs-lookup"><span data-stu-id="2609b-116">3.0.0</span></span>|
|[<span data-ttu-id="2609b-117">Microsoft.Azure.Management.DataLake.Store</span><span class="sxs-lookup"><span data-stu-id="2609b-117">Microsoft.Azure.Management.DataLake.Store</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)|<span data-ttu-id="2609b-118">2.2.0</span><span class="sxs-lookup"><span data-stu-id="2609b-118">2.2.0</span></span>|
|[<span data-ttu-id="2609b-119">Microsoft.Azure.Management.ResourceManager</span><span class="sxs-lookup"><span data-stu-id="2609b-119">Microsoft.Azure.Management.ResourceManager</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="2609b-120">1.6.0-preview</span><span class="sxs-lookup"><span data-stu-id="2609b-120">1.6.0-preview</span></span>|
|[<span data-ttu-id="2609b-121">Microsoft.Azure.Graph.RBAC</span><span class="sxs-lookup"><span data-stu-id="2609b-121">Microsoft.Azure.Graph.RBAC</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="2609b-122">3.4.0-preview</span><span class="sxs-lookup"><span data-stu-id="2609b-122">3.4.0-preview</span></span>|

<span data-ttu-id="2609b-123">Estos paquetes se pueden instalar desde la línea de comandos de NuGet con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="2609b-123">You can install these packages via the NuGet command line with the following commands:</span></span>

```
Install-Package -Id Microsoft.Rest.ClientRuntime.Azure.Authentication  -Version 2.3.1
Install-Package -Id Microsoft.Azure.Management.DataLake.Analytics  -Version 3.0.0
Install-Package -Id Microsoft.Azure.Management.DataLake.Store  -Version 2.2.0
Install-Package -Id Microsoft.Azure.Management.ResourceManager  -Version 1.6.0-preview
Install-Package -Id Microsoft.Azure.Graph.RBAC -Version 3.4.0-preview
```

## <a name="common-variables"></a><span data-ttu-id="2609b-124">Variables comunes</span><span class="sxs-lookup"><span data-stu-id="2609b-124">Common variables</span></span>

``` csharp
string subid = "<Subscription ID>"; // Subscription ID (a GUID)
string tenantid = "<Tenant ID>"; // AAD tenant ID or domain. For example, "contoso.onmicrosoft.com"
string rg == "<value>"; // Resource  group name
string clientid = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID (this will work, but you should pick your own)
```

## <a name="authentication"></a><span data-ttu-id="2609b-125">Autenticación</span><span class="sxs-lookup"><span data-stu-id="2609b-125">Authentication</span></span>

<span data-ttu-id="2609b-126">Tiene varias opciones para registrarse en Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2609b-126">You have multiple options for logging on to Azure Data Lake Analytics.</span></span> <span data-ttu-id="2609b-127">El fragmento de código siguiente muestra un ejemplo de autenticación con la autenticación de usuario interactiva con un elemento emergente.</span><span class="sxs-lookup"><span data-stu-id="2609b-127">The following snippet shows an example of authentication with interactive user authentication with a pop-up.</span></span>

``` csharp
using System;
using System.IO;
using System.Threading;
using System.Security.Cryptography.X509Certificates;

using Microsoft.Rest;
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.DataLake.Analytics;
using Microsoft.Azure.Management.DataLake.Analytics.Models;
using Microsoft.Azure.Management.DataLake.Store;
using Microsoft.Azure.Management.DataLake.Store.Models;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using Microsoft.Azure.Graph.RBAC;

public static Program
{
   public static string TENANT = "microsoft.onmicrosoft.com";
   public static string CLIENTID = "1950a258-227b-4e31-a9cf-717495945fc2";
   public static System.Uri ARM_TOKEN_AUDIENCE = new System.Uri( @"https://management.core.windows.net/");
   public static System.Uri ADL_TOKEN_AUDIENCE = new System.Uri( @"https://datalake.azure.net/" );
   public static System.Uri GRAPH_TOKEN_AUDIENCE = new System.Uri( @"https://graph.windows.net/" );

   static void Main(string[] args)
   {
      string MY_DOCUMENTS= System.Environment.GetFolderPath( System.Environment.SpecialFolder.MyDocuments);
      string TOKEN_CACHE_PATH = System.IO.Path.Combine(MY_DOCUMENTS, "my.tokencache");

      var tokenCache = GetTokenCache(TOKEN_CACHE_PATH);
      var armCreds = GetCreds_User_Popup(TENANT, ARM_TOKEN_AUDIENCE, CLIENTID, tokenCache);
      var adlCreds = GetCreds_User_Popup(TENANT, ADL_TOKEN_AUDIENCE, CLIENTID, tokenCache);
      var graphCreds = GetCreds_User_Popup(TENANT, GRAPH_TOKEN_AUDIENCE, CLIENTID, tokenCache);
   }
}
```

<span data-ttu-id="2609b-128">Tanto el código fuente de **GetCreds_User_Popup** como el código de otras opciones de autenticación se tratan en [Data Lake Analytics .NET authentication options](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options) (Opciones de autenticación de .NET de Data Lake Analytics)</span><span class="sxs-lookup"><span data-stu-id="2609b-128">The source code for **GetCreds_User_Popup** and the code for other options for authentication are covered in [Data Lake Analytics .NET authentication options](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span></span>


## <a name="create-the-client-management-objects"></a><span data-ttu-id="2609b-129">Creación de objetos de administración de cliente</span><span class="sxs-lookup"><span data-stu-id="2609b-129">Create the client management objects</span></span>

``` csharp
var resourceManagementClient = new ResourceManagementClient(armCreds) { SubscriptionId = subid };

var adlaAccountClient = new DataLakeAnalyticsAccountManagementClient(armCreds);
adlaAccountClient.SubscriptionId = subid;

var adlsAccountClient = new DataLakeStoreAccountManagementClient(armCreds);
adlsAccountClient.SubscriptionId = subid;

var adlaCatalogClient = new DataLakeAnalyticsCatalogManagementClient(adlCreds);
var adlaJobClient = new DataLakeAnalyticsJobManagementClient(adlCreds);

var adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(adlCreds);

var  graphClient = new GraphRbacManagementClient(graphCreds);
graphClient.TenantID = domain;

```

## <a name="manage-accounts"></a><span data-ttu-id="2609b-130">Administrar cuentas</span><span class="sxs-lookup"><span data-stu-id="2609b-130">Manage accounts</span></span>

### <a name="create-an-azure-resource-group"></a><span data-ttu-id="2609b-131">Crear un grupo de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="2609b-131">Create an Azure Resource Group</span></span>

<span data-ttu-id="2609b-132">Si aún no ha creado ninguno, debe tener un grupo de recursos de Azure para crear los componentes de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2609b-132">If you haven't already created one, you must have an Azure Resource Group to create your Data Lake Analytics components.</span></span> <span data-ttu-id="2609b-133">Necesita las credenciales de autenticación, el identificador de la suscripción y una ubicación.</span><span class="sxs-lookup"><span data-stu-id="2609b-133">You  need your authentication credentials, subscription ID, and a location.</span></span> <span data-ttu-id="2609b-134">El código siguiente muestra cómo crear un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="2609b-134">The following code shows how to create a resource group:</span></span>

``` csharp
var resourceGroup = new ResourceGroup { Location = location };
resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rg);
```
<span data-ttu-id="2609b-135">Para más información, vea [Grupos de recursos de Azure y Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span><span class="sxs-lookup"><span data-stu-id="2609b-135">For more information, see [Azure Resource Groups and Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span></span>

### <a name="create-a-data-lake-store-account"></a><span data-ttu-id="2609b-136">Crear una cuenta de Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="2609b-136">Create a Data Lake Store account</span></span>

<span data-ttu-id="2609b-137">Todas las cuenta ADLA requieren una cuenta ADLS.</span><span class="sxs-lookup"><span data-stu-id="2609b-137">Ever ADLA account requires an ADLS account.</span></span> <span data-ttu-id="2609b-138">Si no tiene ninguna, puede crearla con el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="2609b-138">If you don't already have one to use, you can create one with the following code:</span></span>

``` csharp
var new_adls_params = new DataLakeStoreAccount(location: _location);
adlsAccountClient.Account.Create(rg, adls, new_adls_params);
```

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="2609b-139">Creación de una cuenta de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="2609b-139">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="2609b-140">El siguiente código crea una cuenta ADLS</span><span class="sxs-lookup"><span data-stu-id="2609b-140">The following code creates an ADLS account</span></span>

``` csharp
var new_adla_params = new DataLakeAnalyticsAccount()
{
   DefaultDataLakeStoreAccount = adls,
   Location = location
};

adlaClient.Account.Create(rg, adla, new_adla_params);
```

### <a name="list-data-lake-store-accounts"></a><span data-ttu-id="2609b-141">Enumeración de cuentas de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2609b-141">List Data Lake Store accounts</span></span>

``` csharp
var adlsAccounts = adlsAccountClient.Account.List().ToList();
foreach (var adls in adlsAccounts)
{
   Console.WriteLine($"ADLS: {0}", adls.Name);
}
```

### <a name="list-data-lake-analytics-accounts"></a><span data-ttu-id="2609b-142">Enumeración de cuentas de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="2609b-142">List Data Lake Analytics accounts</span></span>

``` csharp
var adlaAccounts = adlaClient.Account.List().ToList();

for (var adla in AdlaAccounts)
{
   Console.WriteLine($"ADLA: {0}, adla.Name");
}
```

### <a name="checking-if-an-account-exists"></a><span data-ttu-id="2609b-143">Comprobando si existe una cuenta</span><span class="sxs-lookup"><span data-stu-id="2609b-143">Checking if an account exists</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="2609b-144">Obtener información de una cuenta</span><span class="sxs-lookup"><span data-stu-id="2609b-144">Get information about an account</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
if (exists)
{
   var adla_accnt = adlaClient.Account.Get(rg, adla);
}
```

### <a name="delete-an-account"></a><span data-ttu-id="2609b-145">Eliminación de una cuenta</span><span class="sxs-lookup"><span data-stu-id="2609b-145">Delete an account</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
   adlaClient.Account.Delete(rg, adla);
}
```

### <a name="get-the-default-data-lake-store-account"></a><span data-ttu-id="2609b-146">Obtención de la cuenta predeterminada de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2609b-146">Get the default Data Lake Store account</span></span>

<span data-ttu-id="2609b-147">Cada cuenta de Data Lake Analytics requiere una cuenta de Data Lake Store predeterminada.</span><span class="sxs-lookup"><span data-stu-id="2609b-147">Every Data Lake Analytics account requires a default Data Lake Store account.</span></span> <span data-ttu-id="2609b-148">Utilice este código para determinar la cuenta de Store predeterminada para una cuenta de Analytics.</span><span class="sxs-lookup"><span data-stu-id="2609b-148">Use this code to determine the default Store account for an Analytics account.</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
  var adla_accnt = adlaClient.Account.Get(rg, adla);
  string def_adls_account = adla_accnt.DefaultDataLakeStoreAccount;
}
```

## <a name="manage-data-sources"></a><span data-ttu-id="2609b-149">Administración de orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="2609b-149">Manage data sources</span></span>

<span data-ttu-id="2609b-150">Actualmente, Análisis de Data Lake admite los siguientes orígenes de datos:</span><span class="sxs-lookup"><span data-stu-id="2609b-150">Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="2609b-151">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="2609b-151">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="2609b-152">Cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2609b-152">Azure Storage Account</span></span>](../storage/common/storage-introduction.md)

### <a name="link-to-an-azure-storage-account"></a><span data-ttu-id="2609b-153">Vínculo a una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2609b-153">Link to an Azure Storage account</span></span>

<span data-ttu-id="2609b-154">Se pueden crear vínculos a cuentas de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="2609b-154">You can create links to Azure Storage accounts.</span></span>

``` csharp
string storage_key = "xxxxxxxxxxxxxxxxxxxx";
string storage_account = "mystorageaccount";
var addParams = new AddStorageAccountParameters(storage_key);            
adlaClient.StorageAccounts.Add(rg, adla, storage_account, addParams);
```

### <a name="list-azure-storage-data-sources"></a><span data-ttu-id="2609b-155">Enumeración de orígenes de datos de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2609b-155">List Azure Storage data sources</span></span>

``` csharp
var stg_accounts = adlaAccountClient.StorageAccounts.ListByAccount(rg, adla);

if (stg_accounts != null)
{
  foreach (var stg_account in stg_accounts)
  {
      Console.WriteLine($"Storage account: {0}", stg_account.Name);
  }
}
```

### <a name="list-data-lake-store-data-sources"></a><span data-ttu-id="2609b-156">Lista de orígenes de datos de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2609b-156">List Data Lake Store data sources</span></span>

``` csharp
var adls_accounts = adlsClient.Account.List();

if (adls_accounts != null)
{
  foreach (var adls_accnt in adls_accounts)
  {
      Console.WriteLine($"ADLS account: {0}", adls_accnt.Name);
  }
}
```

### <a name="upload-and-download-folders-and-files"></a><span data-ttu-id="2609b-157">Cargar y descargar archivos y carpetas</span><span class="sxs-lookup"><span data-stu-id="2609b-157">Upload and download folders and files</span></span>
<span data-ttu-id="2609b-158">El objeto de administración de cliente del sistema de archivos de Data Lake Store se puede usar para cargar y descargar archivos o carpetas individuales desde Azure al equipo local, usando los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2609b-158">You can use the Data Lake Store file system client management object to upload and download individual files or folders from Azure to your local computer, using the following methods:</span></span>

- <span data-ttu-id="2609b-159">UploadFolder</span><span class="sxs-lookup"><span data-stu-id="2609b-159">UploadFolder</span></span>
- <span data-ttu-id="2609b-160">UploadFile</span><span class="sxs-lookup"><span data-stu-id="2609b-160">UploadFile</span></span>
- <span data-ttu-id="2609b-161">DownloadFolder</span><span class="sxs-lookup"><span data-stu-id="2609b-161">DownloadFolder</span></span>
- <span data-ttu-id="2609b-162">DownloadFile</span><span class="sxs-lookup"><span data-stu-id="2609b-162">DownloadFile</span></span>

<span data-ttu-id="2609b-163">El primer parámetro de estos métodos es el nombre de la cuenta de Data Lake Store, seguido de parámetros para la ruta de acceso de origen y la ruta de acceso de destino.</span><span class="sxs-lookup"><span data-stu-id="2609b-163">The first parameter for these methods is the name of the Data Lake Store Account, followed by parameters for the source path and the destination path.</span></span>

<span data-ttu-id="2609b-164">En el ejemplo siguiente se muestra cómo descargar una carpeta en Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2609b-164">The following example shows how to download a folder in the Data Lake Store.</span></span>

``` csharp
adlsFileSystemClient.FileSystem.DownloadFolder(adls, sourcePath, destinationPath);
```

### <a name="create-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="2609b-165">Crear un archivo en una cuenta de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2609b-165">Create a file in a Data Lake Store account</span></span>

``` csharp
using (var memstream = new MemoryStream())
{
   using (var sw = new StreamWriter(memstream, UTF8Encoding.UTF8))
   {
      sw.WriteLine("Hello World");
      sw.Flush();

      adlsFileSystemClient.FileSystem.Create(adls, "/Samples/Output/randombytes.csv", memstream);
   }
}
```

### <a name="verify-azure-storage-account-paths"></a><span data-ttu-id="2609b-166">Verificación de las rutas de acceso a la cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2609b-166">Verify Azure Storage account paths</span></span>
<span data-ttu-id="2609b-167">El código siguiente comprueba si hay una cuenta de Azure Storage (storageAccntName) en una cuenta de Data Lake Analytics (analyticsAccountName), y si hay un contenedor (containerName) en la cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="2609b-167">The following code checks if an Azure Storage account (storageAccntName) exists in a Data Lake Analytics account (analyticsAccountName), and if a container (containerName) exists in the Azure Storage account.</span></span>

``` csharp
string storage_account = "mystorageaccount";
string storage_container = "mycontainer";
bool accountExists = adlaClient.Account.StorageAccountExists(rg, adla, storage_account));
bool containerExists = adlaClient.Account.StorageContainerExists(rg, adla, storage_account, storage_container));
```

## <a name="manage-catalog-and-jobs"></a><span data-ttu-id="2609b-168">Administración del catálogo y los trabajos</span><span class="sxs-lookup"><span data-stu-id="2609b-168">Manage catalog and jobs</span></span>
<span data-ttu-id="2609b-169">El objeto DataLakeAnalyticsCatalogManagementClient proporciona métodos para administrar la base de datos SQL que se proporciona a cada cuenta de Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2609b-169">The DataLakeAnalyticsCatalogManagementClient object provides methods for managing the SQL database provided for each Azure Data Lake Analytics account.</span></span> <span data-ttu-id="2609b-170">DataLakeAnalyticsJobManagementClient proporciona métodos para enviar y administrar trabajos ejecutados en la base de datos con scripts de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="2609b-170">The DataLakeAnalyticsJobManagementClient provides methods to submit and manage jobs run on the database with U-SQL scripts.</span></span>

### <a name="list-databases-and-schemas"></a><span data-ttu-id="2609b-171">Lista de bases de datos y esquemas</span><span class="sxs-lookup"><span data-stu-id="2609b-171">List databases and schemas</span></span>
<span data-ttu-id="2609b-172">Entre las diversas cosas que puede incluir en la lista, las más comunes son las bases de datos y su esquema.</span><span class="sxs-lookup"><span data-stu-id="2609b-172">Among the several things you can list, the most common are databases and their schema.</span></span> <span data-ttu-id="2609b-173">El código siguiente obtiene una colección de bases de datos y, a continuación, enumera el esquema de cada base de datos.</span><span class="sxs-lookup"><span data-stu-id="2609b-173">The following code obtains a collection of databases, and then enumerates the schema for each database.</span></span>

``` csharp
var databases = adlaCatalogClient.Catalog.ListDatabases(adla);
foreach (var db in databases)
{
  Console.WriteLine($"Database: {db.Name}");
  Console.WriteLine(" - Schemas:");
  var schemas = adlaCatalogClient.Catalog.ListSchemas(adla, db.Name);
  foreach (var schm in schemas)
  {
      Console.WriteLine($"\t{schm.Name}");
  }
}
```

### <a name="list-table-columns"></a><span data-ttu-id="2609b-174">Lista de columnas de la tabla</span><span class="sxs-lookup"><span data-stu-id="2609b-174">List table columns</span></span>
<span data-ttu-id="2609b-175">El código siguiente muestra cómo acceder a la base de datos con un cliente de administración del catálogo de Data Lake Analytics para mostrar las columnas de una tabla especificada.</span><span class="sxs-lookup"><span data-stu-id="2609b-175">The following code shows how to access the database with a Data Lake Analytics Catalog management client to list the columns in a specified table.</span></span>

``` csharp
var tbl = adlaCatalogClient.Catalog.GetTable(adla, "master", "dbo", "MyTableName");
IEnumerable<USqlTableColumn> columns = tbl.ColumnList;

foreach (USqlTableColumn utc in columns)
{
  string scriptPath = "/Samples/Scripts/SearchResults_Wikipedia_Script.txt";
  Stream scriptStrm = adlsFileSystemClient.FileSystem.Open(_adlsAccountName, scriptPath);
  string scriptTxt = string.Empty;
  using (StreamReader sr = new StreamReader(scriptStrm))
  {
      scriptTxt = sr.ReadToEnd();
  }

  var jobName = "SR_Wikipedia";
  var jobId = Guid.NewGuid();
  var properties = new USqlJobProperties(scriptTxt);
  var parameters = new JobInformation(jobName, JobType.USql, properties, priority: 1, degreeOfParallelism: 1, jobId: jobId);
  var jobInfo = adlaJobClient.Job.Create(adla, jobId, parameters);
  Console.WriteLine($"Job {jobName} submitted.");

}
```

### <a name="list-failed-jobs"></a><span data-ttu-id="2609b-176">Lista de trabajos con errores</span><span class="sxs-lookup"><span data-stu-id="2609b-176">List failed jobs</span></span>
<span data-ttu-id="2609b-177">El código siguiente muestra información acerca de trabajos con errores.</span><span class="sxs-lookup"><span data-stu-id="2609b-177">The following code lists information about jobs that failed.</span></span>

``` csharp
var odq = new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" };
var jobs = adlaJobClient.Job.List(adla, odq);
foreach (var j in jobs)
{
   Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
}
```

### <a name="list-pipelines"></a><span data-ttu-id="2609b-178">Enumerar canalizaciones</span><span class="sxs-lookup"><span data-stu-id="2609b-178">List pipelines</span></span>
<span data-ttu-id="2609b-179">El código siguiente muestra información sobre cada canalización de los trabajos enviados a la cuenta.</span><span class="sxs-lookup"><span data-stu-id="2609b-179">The following code lists information about each pipeline of jobs submitted to the account.</span></span>

``` csharp
var pipelines = adlaJobClient.Pipeline.List(adla);
foreach (var p in pipelines)
{
   Console.WriteLine($"Pipeline: {p.Name}\t{p.PipelineId}\t{p.LastSubmitTime}");
}
```

### <a name="list-recurrences"></a><span data-ttu-id="2609b-180">Enumerar repeticiones</span><span class="sxs-lookup"><span data-stu-id="2609b-180">List recurrences</span></span>
<span data-ttu-id="2609b-181">El código siguiente muestra información sobre cada repetición de los trabajos enviados a la cuenta.</span><span class="sxs-lookup"><span data-stu-id="2609b-181">The following code lists information about each recurrence of jobs submitted to the account.</span></span>

``` csharp
var recurrences = adlaJobClient.Recurrence.List(adla);
foreach (var r in recurrences)
{
   Console.WriteLine($"Recurrence: {r.Name}\t{r.RecurrenceId}\t{r.LastSubmitTime}");
}
```

## <a name="common-graph-scenarios"></a><span data-ttu-id="2609b-182">Escenarios comunes de grafos</span><span class="sxs-lookup"><span data-stu-id="2609b-182">Common graph scenarios</span></span>

### <a name="look-up-user-in-the-aad-directory"></a><span data-ttu-id="2609b-183">Buscar usuario en el directorio AAD</span><span class="sxs-lookup"><span data-stu-id="2609b-183">Look up user in the AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
```

### <a name="get-the-objectid-of-a-user-in-the-aad-directory"></a><span data-ttu-id="2609b-184">Obtención de ObjectId de usuario en el directorio de AAD</span><span class="sxs-lookup"><span data-stu-id="2609b-184">Get the ObjectId of a user in the AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
Console.WriteLine( userinfo.ObjectId )
```

## <a name="manage-compute-policies"></a><span data-ttu-id="2609b-185">Administración de nodos directivas de proceso</span><span class="sxs-lookup"><span data-stu-id="2609b-185">Manage compute policies</span></span>
<span data-ttu-id="2609b-186">El objeto de DataLakeAnalyticsAccountManagementClient proporciona métodos para administrar las directivas de proceso de una cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2609b-186">The DataLakeAnalyticsAccountManagementClient object provides methods for managing the compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="2609b-187">Enumeración de directivas de proceso</span><span class="sxs-lookup"><span data-stu-id="2609b-187">List compute policies</span></span>
<span data-ttu-id="2609b-188">El código siguiente recupera una lista de directivas de proceso de una cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2609b-188">The following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

``` csharp
var policies = adlaAccountClient.ComputePolicies.ListByAccount(rg, adla);
foreach (var p in policies)
{
   Console.WriteLine($"Name: {p.Name}\tType: {p.ObjectType}\tMax AUs / job: {p.MaxDegreeOfParallelismPerJob}\tMin priority / job: {p.MinPriorityPerJob}");
}
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="2609b-189">Creación de una nueva directiva de proceso</span><span class="sxs-lookup"><span data-stu-id="2609b-189">Create a new compute policy</span></span>
<span data-ttu-id="2609b-190">El siguiente código crea una nueva directiva de cálculo para una cuenta de análisis de Data Lake y establece que el número máximo de AU disponibles para el usuario especificado en 50 y la prioridad del trabajo mínimo en 250.</span><span class="sxs-lookup"><span data-stu-id="2609b-190">The following code creates a new compute policy for a Data Lake Analytics account, setting the maximum AUs available to the specified user to 50, and the minimum job priority to 250.</span></span>

``` csharp
var userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde";
var newPolicyParams = new ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250);
adlaAccountClient.ComputePolicies.CreateOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams);
```

## <a name="next-steps"></a><span data-ttu-id="2609b-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2609b-191">Next steps</span></span>
* [<span data-ttu-id="2609b-192">Información general de Análisis de Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="2609b-192">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="2609b-193">Administración de Azure Data Lake Analytics con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2609b-193">Manage Azure Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="2609b-194">Supervisión y solución de problemas de trabajos de Azure Data Lake Analytics con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2609b-194">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
