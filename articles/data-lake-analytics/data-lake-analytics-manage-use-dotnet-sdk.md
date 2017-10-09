---
title: "Análisis de Data Lake de Azure con Azure SDK para .NET aaaManage | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage análisis de Data Lake trabajos, orígenes de datos, los usuarios. "
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
ms.openlocfilehash: 98630ba411823644a8bce1f1b0c1331f689cbb0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a><span data-ttu-id="018e5-103">Administración de Azure Data Lake Analytics con el SDK de .NET para Azure</span><span class="sxs-lookup"><span data-stu-id="018e5-103">Manage Azure Data Lake Analytics using Azure .NET SDK</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="018e5-104">Obtenga información acerca de cómo las cuentas de análisis de Azure Data Lake toomanage, orígenes de datos, los usuarios y trabajos mediante hello Azure .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="018e5-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, users, and jobs using hello Azure .NET SDK.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="018e5-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="018e5-105">Prerequisites</span></span>

* <span data-ttu-id="018e5-106">**Visual Studio 2015, Visual Studio 2013 Update 4 o Visual Studio 2012 con Visual C++ instalado**.</span><span class="sxs-lookup"><span data-stu-id="018e5-106">**Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed**.</span></span>
* <span data-ttu-id="018e5-107">**SDK de Microsoft Azure para .NET versión 2.5 o posterior**.</span><span class="sxs-lookup"><span data-stu-id="018e5-107">**Microsoft Azure SDK for .NET version 2.5 or above**.</span></span>  <span data-ttu-id="018e5-108">Instalar mediante hello [instalador de plataforma Web](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="018e5-108">Install it using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="018e5-109">**Paquetes de NuGet requeridos**</span><span class="sxs-lookup"><span data-stu-id="018e5-109">**Required NuGet Packages**</span></span>

### <a name="install-nuget-packages"></a><span data-ttu-id="018e5-110">Instalación de paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="018e5-110">Install NuGet packages</span></span>

|<span data-ttu-id="018e5-111">Paquete</span><span class="sxs-lookup"><span data-stu-id="018e5-111">Package</span></span>|<span data-ttu-id="018e5-112">Versión</span><span class="sxs-lookup"><span data-stu-id="018e5-112">Version</span></span>|
|-------|-------|
|[<span data-ttu-id="018e5-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span><span class="sxs-lookup"><span data-stu-id="018e5-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span></span>](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime.Azure.Authentication)| <span data-ttu-id="018e5-114">2.3.1</span><span class="sxs-lookup"><span data-stu-id="018e5-114">2.3.1</span></span>|
|[<span data-ttu-id="018e5-115">Microsoft.Azure.Management.DataLake.Analytics</span><span class="sxs-lookup"><span data-stu-id="018e5-115">Microsoft.Azure.Management.DataLake.Analytics</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)|<span data-ttu-id="018e5-116">3.0.0</span><span class="sxs-lookup"><span data-stu-id="018e5-116">3.0.0</span></span>|
|[<span data-ttu-id="018e5-117">Microsoft.Azure.Management.DataLake.Store</span><span class="sxs-lookup"><span data-stu-id="018e5-117">Microsoft.Azure.Management.DataLake.Store</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)|<span data-ttu-id="018e5-118">2.2.0</span><span class="sxs-lookup"><span data-stu-id="018e5-118">2.2.0</span></span>|
|[<span data-ttu-id="018e5-119">Microsoft.Azure.Management.ResourceManager</span><span class="sxs-lookup"><span data-stu-id="018e5-119">Microsoft.Azure.Management.ResourceManager</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="018e5-120">1.6.0-preview</span><span class="sxs-lookup"><span data-stu-id="018e5-120">1.6.0-preview</span></span>|
|[<span data-ttu-id="018e5-121">Microsoft.Azure.Graph.RBAC</span><span class="sxs-lookup"><span data-stu-id="018e5-121">Microsoft.Azure.Graph.RBAC</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="018e5-122">3.4.0-preview</span><span class="sxs-lookup"><span data-stu-id="018e5-122">3.4.0-preview</span></span>|

<span data-ttu-id="018e5-123">Puede instalar estos paquetes a través de la línea de comandos de NuGet Hola con hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="018e5-123">You can install these packages via hello NuGet command line with hello following commands:</span></span>

```
Install-Package -Id Microsoft.Rest.ClientRuntime.Azure.Authentication  -Version 2.3.1
Install-Package -Id Microsoft.Azure.Management.DataLake.Analytics  -Version 3.0.0
Install-Package -Id Microsoft.Azure.Management.DataLake.Store  -Version 2.2.0
Install-Package -Id Microsoft.Azure.Management.ResourceManager  -Version 1.6.0-preview
Install-Package -Id Microsoft.Azure.Graph.RBAC -Version 3.4.0-preview
```

## <a name="common-variables"></a><span data-ttu-id="018e5-124">Variables comunes</span><span class="sxs-lookup"><span data-stu-id="018e5-124">Common variables</span></span>

``` csharp
string subid = "<Subscription ID>"; // Subscription ID (a GUID)
string tenantid = "<Tenant ID>"; // AAD tenant ID or domain. For example, "contoso.onmicrosoft.com"
string rg == "<value>"; // Resource  group name
string clientid = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID (this will work, but you should pick your own)
```

## <a name="authentication"></a><span data-ttu-id="018e5-125">Autenticación</span><span class="sxs-lookup"><span data-stu-id="018e5-125">Authentication</span></span>

<span data-ttu-id="018e5-126">Tiene varias opciones para iniciar la sesión tooAzure análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="018e5-126">You have multiple options for logging on tooAzure Data Lake Analytics.</span></span> <span data-ttu-id="018e5-127">Hello fragmento de código siguiente muestra un ejemplo de autenticación con la autenticación de usuario interactivo con un elemento emergente.</span><span class="sxs-lookup"><span data-stu-id="018e5-127">hello following snippet shows an example of authentication with interactive user authentication with a pop-up.</span></span>

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

<span data-ttu-id="018e5-128">Hola código fuente de **GetCreds_User_Popup** y Hola código para otras opciones para la autenticación se tratan en [opciones de autenticación de Data Lake Analytics. NET](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span><span class="sxs-lookup"><span data-stu-id="018e5-128">hello source code for **GetCreds_User_Popup** and hello code for other options for authentication are covered in [Data Lake Analytics .NET authentication options](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span></span>


## <a name="create-hello-client-management-objects"></a><span data-ttu-id="018e5-129">Crear objetos de administración de cliente de Hola</span><span class="sxs-lookup"><span data-stu-id="018e5-129">Create hello client management objects</span></span>

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

## <a name="manage-accounts"></a><span data-ttu-id="018e5-130">Administrar cuentas</span><span class="sxs-lookup"><span data-stu-id="018e5-130">Manage accounts</span></span>

### <a name="create-an-azure-resource-group"></a><span data-ttu-id="018e5-131">Crear un grupo de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="018e5-131">Create an Azure Resource Group</span></span>

<span data-ttu-id="018e5-132">Si ya no ha creado uno, debe tener un grupo de recursos de Azure toocreate los componentes de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="018e5-132">If you haven't already created one, you must have an Azure Resource Group toocreate your Data Lake Analytics components.</span></span> <span data-ttu-id="018e5-133">Necesita las credenciales de autenticación, el identificador de la suscripción y una ubicación.</span><span class="sxs-lookup"><span data-stu-id="018e5-133">You  need your authentication credentials, subscription ID, and a location.</span></span> <span data-ttu-id="018e5-134">Hola el siguiente código muestra cómo toocreate un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="018e5-134">hello following code shows how toocreate a resource group:</span></span>

``` csharp
var resourceGroup = new ResourceGroup { Location = location };
resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rg);
```
<span data-ttu-id="018e5-135">Para más información, vea [Grupos de recursos de Azure y Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span><span class="sxs-lookup"><span data-stu-id="018e5-135">For more information, see [Azure Resource Groups and Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span></span>

### <a name="create-a-data-lake-store-account"></a><span data-ttu-id="018e5-136">Crear una cuenta de Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="018e5-136">Create a Data Lake Store account</span></span>

<span data-ttu-id="018e5-137">Todas las cuenta ADLA requieren una cuenta ADLS.</span><span class="sxs-lookup"><span data-stu-id="018e5-137">Ever ADLA account requires an ADLS account.</span></span> <span data-ttu-id="018e5-138">Si aún no tiene una toouse, puede crear uno con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="018e5-138">If you don't already have one toouse, you can create one with hello following code:</span></span>

``` csharp
var new_adls_params = new DataLakeStoreAccount(location: _location);
adlsAccountClient.Account.Create(rg, adls, new_adls_params);
```

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="018e5-139">Creación de una cuenta de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="018e5-139">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="018e5-140">Hola siguiente código crea una cuenta ADLS</span><span class="sxs-lookup"><span data-stu-id="018e5-140">hello following code creates an ADLS account</span></span>

``` csharp
var new_adla_params = new DataLakeAnalyticsAccount()
{
   DefaultDataLakeStoreAccount = adls,
   Location = location
};

adlaClient.Account.Create(rg, adla, new_adla_params);
```

### <a name="list-data-lake-store-accounts"></a><span data-ttu-id="018e5-141">Enumeración de cuentas de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="018e5-141">List Data Lake Store accounts</span></span>

``` csharp
var adlsAccounts = adlsAccountClient.Account.List().ToList();
foreach (var adls in adlsAccounts)
{
   Console.WriteLine($"ADLS: {0}", adls.Name);
}
```

### <a name="list-data-lake-analytics-accounts"></a><span data-ttu-id="018e5-142">Enumeración de cuentas de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="018e5-142">List Data Lake Analytics accounts</span></span>

``` csharp
var adlaAccounts = adlaClient.Account.List().ToList();

for (var adla in AdlaAccounts)
{
   Console.WriteLine($"ADLA: {0}, adla.Name");
}
```

### <a name="checking-if-an-account-exists"></a><span data-ttu-id="018e5-143">Comprobando si existe una cuenta</span><span class="sxs-lookup"><span data-stu-id="018e5-143">Checking if an account exists</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="018e5-144">Obtener información de una cuenta</span><span class="sxs-lookup"><span data-stu-id="018e5-144">Get information about an account</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
if (exists)
{
   var adla_accnt = adlaClient.Account.Get(rg, adla);
}
```

### <a name="delete-an-account"></a><span data-ttu-id="018e5-145">Eliminación de una cuenta</span><span class="sxs-lookup"><span data-stu-id="018e5-145">Delete an account</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
   adlaClient.Account.Delete(rg, adla);
}
```

### <a name="get-hello-default-data-lake-store-account"></a><span data-ttu-id="018e5-146">Obtener la cuenta de almacén de Data Lake Hola predeterminada</span><span class="sxs-lookup"><span data-stu-id="018e5-146">Get hello default Data Lake Store account</span></span>

<span data-ttu-id="018e5-147">Cada cuenta de Data Lake Analytics requiere una cuenta de Data Lake Store predeterminada.</span><span class="sxs-lookup"><span data-stu-id="018e5-147">Every Data Lake Analytics account requires a default Data Lake Store account.</span></span> <span data-ttu-id="018e5-148">Utilice esta cuenta de almacén de código toodetermine Hola predeterminado para una cuenta de análisis.</span><span class="sxs-lookup"><span data-stu-id="018e5-148">Use this code toodetermine hello default Store account for an Analytics account.</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
  var adla_accnt = adlaClient.Account.Get(rg, adla);
  string def_adls_account = adla_accnt.DefaultDataLakeStoreAccount;
}
```

## <a name="manage-data-sources"></a><span data-ttu-id="018e5-149">Administración de orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="018e5-149">Manage data sources</span></span>

<span data-ttu-id="018e5-150">Análisis de Data Lake admite actualmente Hola siguientes orígenes de datos:</span><span class="sxs-lookup"><span data-stu-id="018e5-150">Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="018e5-151">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="018e5-151">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="018e5-152">Cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="018e5-152">Azure Storage Account</span></span>](../storage/common/storage-introduction.md)

### <a name="link-tooan-azure-storage-account"></a><span data-ttu-id="018e5-153">Vínculo tooan cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="018e5-153">Link tooan Azure Storage account</span></span>

<span data-ttu-id="018e5-154">Puede crear vínculos tooAzure cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="018e5-154">You can create links tooAzure Storage accounts.</span></span>

``` csharp
string storage_key = "xxxxxxxxxxxxxxxxxxxx";
string storage_account = "mystorageaccount";
var addParams = new AddStorageAccountParameters(storage_key);            
adlaClient.StorageAccounts.Add(rg, adla, storage_account, addParams);
```

### <a name="list-azure-storage-data-sources"></a><span data-ttu-id="018e5-155">Enumeración de orígenes de datos de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="018e5-155">List Azure Storage data sources</span></span>

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

### <a name="list-data-lake-store-data-sources"></a><span data-ttu-id="018e5-156">Lista de orígenes de datos de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="018e5-156">List Data Lake Store data sources</span></span>

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

### <a name="upload-and-download-folders-and-files"></a><span data-ttu-id="018e5-157">Cargar y descargar archivos y carpetas</span><span class="sxs-lookup"><span data-stu-id="018e5-157">Upload and download folders and files</span></span>
<span data-ttu-id="018e5-158">Puede utilizar tooupload de objeto administración de hello almacén de Data Lake archivo sistema cliente y descargar los archivos o carpetas desde Azure tooyour equipo local, mediante Hola siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="018e5-158">You can use hello Data Lake Store file system client management object tooupload and download individual files or folders from Azure tooyour local computer, using hello following methods:</span></span>

- <span data-ttu-id="018e5-159">UploadFolder</span><span class="sxs-lookup"><span data-stu-id="018e5-159">UploadFolder</span></span>
- <span data-ttu-id="018e5-160">UploadFile</span><span class="sxs-lookup"><span data-stu-id="018e5-160">UploadFile</span></span>
- <span data-ttu-id="018e5-161">DownloadFolder</span><span class="sxs-lookup"><span data-stu-id="018e5-161">DownloadFolder</span></span>
- <span data-ttu-id="018e5-162">DownloadFile</span><span class="sxs-lookup"><span data-stu-id="018e5-162">DownloadFile</span></span>

<span data-ttu-id="018e5-163">Hola primer parámetro de estos métodos es nombre Hola de hello cuenta de almacén de Data Lake, seguido de los parámetros de ruta de acceso de origen de Hola y ruta de acceso de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="018e5-163">hello first parameter for these methods is hello name of hello Data Lake Store Account, followed by parameters for hello source path and hello destination path.</span></span>

<span data-ttu-id="018e5-164">Hola de ejemplo siguiente muestra cómo toodownload una carpeta en Hola almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="018e5-164">hello following example shows how toodownload a folder in hello Data Lake Store.</span></span>

``` csharp
adlsFileSystemClient.FileSystem.DownloadFolder(adls, sourcePath, destinationPath);
```

### <a name="create-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="018e5-165">Crear un archivo en una cuenta de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="018e5-165">Create a file in a Data Lake Store account</span></span>

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

### <a name="verify-azure-storage-account-paths"></a><span data-ttu-id="018e5-166">Verificación de las rutas de acceso a la cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="018e5-166">Verify Azure Storage account paths</span></span>
<span data-ttu-id="018e5-167">Hello código siguiente comprueba si existe una cuenta de almacenamiento de Azure (storageAccntName) en una cuenta de análisis de Data Lake (analyticsAccountName), y si existe un contenedor (containerName) en la cuenta de almacenamiento de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="018e5-167">hello following code checks if an Azure Storage account (storageAccntName) exists in a Data Lake Analytics account (analyticsAccountName), and if a container (containerName) exists in hello Azure Storage account.</span></span>

``` csharp
string storage_account = "mystorageaccount";
string storage_container = "mycontainer";
bool accountExists = adlaClient.Account.StorageAccountExists(rg, adla, storage_account));
bool containerExists = adlaClient.Account.StorageContainerExists(rg, adla, storage_account, storage_container));
```

## <a name="manage-catalog-and-jobs"></a><span data-ttu-id="018e5-168">Administración del catálogo y los trabajos</span><span class="sxs-lookup"><span data-stu-id="018e5-168">Manage catalog and jobs</span></span>
<span data-ttu-id="018e5-169">objeto de Hello DataLakeAnalyticsCatalogManagementClient proporciona métodos para administrar la base de datos SQL de hello proporcionada para cada cuenta de análisis de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="018e5-169">hello DataLakeAnalyticsCatalogManagementClient object provides methods for managing hello SQL database provided for each Azure Data Lake Analytics account.</span></span> <span data-ttu-id="018e5-170">Hola DataLakeAnalyticsJobManagementClient proporciona métodos toosubmit y administrar trabajos se ejecutan en la base de datos de hello con secuencias de comandos SQL U.</span><span class="sxs-lookup"><span data-stu-id="018e5-170">hello DataLakeAnalyticsJobManagementClient provides methods toosubmit and manage jobs run on hello database with U-SQL scripts.</span></span>

### <a name="list-databases-and-schemas"></a><span data-ttu-id="018e5-171">Lista de bases de datos y esquemas</span><span class="sxs-lookup"><span data-stu-id="018e5-171">List databases and schemas</span></span>
<span data-ttu-id="018e5-172">Entre Hola varias cosas que puede mostrar, hello más comunes son las bases de datos y su esquema.</span><span class="sxs-lookup"><span data-stu-id="018e5-172">Among hello several things you can list, hello most common are databases and their schema.</span></span> <span data-ttu-id="018e5-173">Hello código siguiente obtiene una colección de bases de datos y, a continuación, enumera el esquema de Hola para cada base de datos.</span><span class="sxs-lookup"><span data-stu-id="018e5-173">hello following code obtains a collection of databases, and then enumerates hello schema for each database.</span></span>

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

### <a name="list-table-columns"></a><span data-ttu-id="018e5-174">Lista de columnas de la tabla</span><span class="sxs-lookup"><span data-stu-id="018e5-174">List table columns</span></span>
<span data-ttu-id="018e5-175">Hello código siguiente muestra cómo tooaccess Hola base de datos con un catálogo de análisis de datos Lake administración cliente toolist hello las columnas de una tabla especificada.</span><span class="sxs-lookup"><span data-stu-id="018e5-175">hello following code shows how tooaccess hello database with a Data Lake Analytics Catalog management client toolist hello columns in a specified table.</span></span>

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

### <a name="list-failed-jobs"></a><span data-ttu-id="018e5-176">Lista de trabajos con errores</span><span class="sxs-lookup"><span data-stu-id="018e5-176">List failed jobs</span></span>
<span data-ttu-id="018e5-177">Hello código siguiente muestra información sobre los trabajos que no se pudo.</span><span class="sxs-lookup"><span data-stu-id="018e5-177">hello following code lists information about jobs that failed.</span></span>

``` csharp
var odq = new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" };
var jobs = adlaJobClient.Job.List(adla, odq);
foreach (var j in jobs)
{
   Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
}
```

### <a name="list-pipelines"></a><span data-ttu-id="018e5-178">Enumerar canalizaciones</span><span class="sxs-lookup"><span data-stu-id="018e5-178">List pipelines</span></span>
<span data-ttu-id="018e5-179">Hello código siguiente muestra información sobre cada canalización de trabajos enviados toohello cuenta.</span><span class="sxs-lookup"><span data-stu-id="018e5-179">hello following code lists information about each pipeline of jobs submitted toohello account.</span></span>

``` csharp
var pipelines = adlaJobClient.Pipeline.List(adla);
foreach (var p in pipelines)
{
   Console.WriteLine($"Pipeline: {p.Name}\t{p.PipelineId}\t{p.LastSubmitTime}");
}
```

### <a name="list-recurrences"></a><span data-ttu-id="018e5-180">Enumerar repeticiones</span><span class="sxs-lookup"><span data-stu-id="018e5-180">List recurrences</span></span>
<span data-ttu-id="018e5-181">Hello código siguiente muestra información sobre cada repetición de trabajos enviados toohello cuenta.</span><span class="sxs-lookup"><span data-stu-id="018e5-181">hello following code lists information about each recurrence of jobs submitted toohello account.</span></span>

``` csharp
var recurrences = adlaJobClient.Recurrence.List(adla);
foreach (var r in recurrences)
{
   Console.WriteLine($"Recurrence: {r.Name}\t{r.RecurrenceId}\t{r.LastSubmitTime}");
}
```

## <a name="common-graph-scenarios"></a><span data-ttu-id="018e5-182">Escenarios comunes de grafos</span><span class="sxs-lookup"><span data-stu-id="018e5-182">Common graph scenarios</span></span>

### <a name="look-up-user-in-hello-aad-directory"></a><span data-ttu-id="018e5-183">Buscar el usuario en el directorio de AAD Hola</span><span class="sxs-lookup"><span data-stu-id="018e5-183">Look up user in hello AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
```

### <a name="get-hello-objectid-of-a-user-in-hello-aad-directory"></a><span data-ttu-id="018e5-184">Obtener Hola ObjectId de un usuario en el directorio de AAD Hola</span><span class="sxs-lookup"><span data-stu-id="018e5-184">Get hello ObjectId of a user in hello AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
Console.WriteLine( userinfo.ObjectId )
```

## <a name="manage-compute-policies"></a><span data-ttu-id="018e5-185">Administración de nodos directivas de proceso</span><span class="sxs-lookup"><span data-stu-id="018e5-185">Manage compute policies</span></span>
<span data-ttu-id="018e5-186">objeto de Hello DataLakeAnalyticsAccountManagementClient proporciona métodos para administrar Hola proceso directivas para una cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="018e5-186">hello DataLakeAnalyticsAccountManagementClient object provides methods for managing hello compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="018e5-187">Enumeración de directivas de proceso</span><span class="sxs-lookup"><span data-stu-id="018e5-187">List compute policies</span></span>
<span data-ttu-id="018e5-188">Hola siguiente código recupera una lista de las directivas de proceso para una cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="018e5-188">hello following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

``` csharp
var policies = adlaAccountClient.ComputePolicies.ListByAccount(rg, adla);
foreach (var p in policies)
{
   Console.WriteLine($"Name: {p.Name}\tType: {p.ObjectType}\tMax AUs / job: {p.MaxDegreeOfParallelismPerJob}\tMin priority / job: {p.MinPriorityPerJob}");
}
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="018e5-189">Creación de una nueva directiva de proceso</span><span class="sxs-lookup"><span data-stu-id="018e5-189">Create a new compute policy</span></span>
<span data-ttu-id="018e5-190">Hola siguiente código crea una nueva directiva de cálculo para una cuenta de análisis de Data Lake, configuración Hola máximo AUs disponible toohello especificada too50 de usuario y too250 de prioridad de trabajo mínimo de Hola.</span><span class="sxs-lookup"><span data-stu-id="018e5-190">hello following code creates a new compute policy for a Data Lake Analytics account, setting hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

``` csharp
var userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde";
var newPolicyParams = new ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250);
adlaAccountClient.ComputePolicies.CreateOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams);
```

## <a name="next-steps"></a><span data-ttu-id="018e5-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="018e5-191">Next steps</span></span>
* [<span data-ttu-id="018e5-192">Información general de Análisis de Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="018e5-192">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="018e5-193">Administración de Azure Data Lake Analytics con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="018e5-193">Manage Azure Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="018e5-194">Supervisión y solución de problemas de trabajos de Azure Data Lake Analytics con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="018e5-194">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
