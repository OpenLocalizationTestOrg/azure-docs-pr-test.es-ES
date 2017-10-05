---
title: "Introducción a Azure Data Lake Store mediante Azure SDK para Node.js | Microsoft Docs"
description: Aprenda a usar Node.js para trabajar con cuentas de Data Lake Store y el sistema de archivos.
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 2fee173c-69ae-4e1d-8773-48618cda9e16
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: nitinme
ms.openlocfilehash: 8c7a2e6ca061bbfa077592efb73d592906c3d070
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a><span data-ttu-id="291d4-103">Introducción a Azure Data Lake Store mediante Azure SDK para Node.js</span><span class="sxs-lookup"><span data-stu-id="291d4-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="291d4-104">Portal</span><span class="sxs-lookup"><span data-stu-id="291d4-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="291d4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="291d4-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="291d4-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="291d4-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="291d4-107">SDK de Java</span><span class="sxs-lookup"><span data-stu-id="291d4-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="291d4-108">API de REST</span><span class="sxs-lookup"><span data-stu-id="291d4-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="291d4-109">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="291d4-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="291d4-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="291d4-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="291d4-111">Python</span><span class="sxs-lookup"><span data-stu-id="291d4-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> <span data-ttu-id="291d4-112">Para cargar y descargar gran cantidad de datos (archivos grandes, un gran número de archivos o ambos), se recomienda usar el [SDK de Python](data-lake-store-get-started-python.md), el [SDK de .NET](data-lake-store-get-started-net-sdk.md), la [CLI de Azure 2.0](data-lake-store-get-started-cli-2.0.md) o [Azure PowerShell](data-lake-store-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="291d4-112">For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use the [Python SDK](data-lake-store-get-started-python.md), the [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md).</span></span> <span data-ttu-id="291d4-113">Estas opciones tienen mejor rendimiento, ya que utilizan varios subprocesos para realizar el movimiento de datos en paralelo.</span><span class="sxs-lookup"><span data-stu-id="291d4-113">These options have better performance as they use multiple threads to parallelize the data movement.</span></span>
> 
> 

<span data-ttu-id="291d4-114">Aprenda a usar el SDK de Azure para Node.js para crear una cuenta de Azure Data Lake Store y realizar operaciones básicas como crear carpetas, cargar y descargar archivos de datos, eliminar la cuenta, etc. Para más información acerca de Data Lake Store, consulte [Información general de Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="291d4-114">Learn how to use the Azure SDK for Node.js to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span> <span data-ttu-id="291d4-115">Actualmente, el SDK admite</span><span class="sxs-lookup"><span data-stu-id="291d4-115">Currently, the SDK supports</span></span>

* <span data-ttu-id="291d4-116">**Versión de Node.js: 0.10.0 o superior**</span><span class="sxs-lookup"><span data-stu-id="291d4-116">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="291d4-117">**Versión de API de REST para la cuenta: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="291d4-117">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="291d4-118">**Versión de API de REST para FileSystem: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="291d4-118">**REST API version for FileSystem: 2015-10-01-preview**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="291d4-119">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="291d4-119">Prerequisites</span></span>
<span data-ttu-id="291d4-120">Antes de empezar este artículo, debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="291d4-120">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="291d4-121">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="291d4-121">**An Azure subscription**.</span></span> <span data-ttu-id="291d4-122">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="291d4-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="291d4-123">**Cree una aplicación de Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="291d4-123">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="291d4-124">Utilice la aplicación Azure AD para autenticar la aplicación Data Lake Store con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="291d4-124">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="291d4-125">Existen diferentes enfoques para realizar la autenticación con Azure AD, que son la **autenticación de usuario final** o la **autenticación de servicio a servicio**.</span><span class="sxs-lookup"><span data-stu-id="291d4-125">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="291d4-126">Para obtener instrucciones y más información acerca de cómo realizar la autenticación, consulte [Autenticación de usuario final con Data Lake Store mediante Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md) o [Autenticación entre servicios con Data Lake Store mediante Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="291d4-126">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="how-to-install"></a><span data-ttu-id="291d4-127">Cómo instalarlo</span><span class="sxs-lookup"><span data-stu-id="291d4-127">How to Install</span></span>
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="291d4-128">Autenticación mediante Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="291d4-128">Authenticate using Azure Active Directory</span></span>
<span data-ttu-id="291d4-129">Los fragmentos de código siguientes muestran dos maneras independientes de autenticar con Data Lake Store mediante Azure AD.</span><span class="sxs-lookup"><span data-stu-id="291d4-129">The snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span></span> <span data-ttu-id="291d4-130">Para obtener una explicación detallada sobre diversos métodos para usar para la autenticación con Data Lake Store, consulte [Autenticación con Data Lake Store mediante Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="291d4-130">For a detailed discussion on various methods to use for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="291d4-131">El siguiente fragmento de código también necesita entradas como el nombre de dominio de Azure AD, el identificador de cliente para una aplicación de Azure AD, etc. Todos estos detalles pueden obtenerse de una aplicación de Azure AD que debe crear, que también se incluyen en el vínculo anterior.</span><span class="sxs-lookup"><span data-stu-id="291d4-131">The snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, the details of which are also included in link above.</span></span>

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-the-data-lake-store-clients"></a><span data-ttu-id="291d4-132">Creación de los clientes de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="291d4-132">Create the Data Lake Store Clients</span></span>
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="291d4-133">Creación de una cuenta de Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="291d4-133">Create a Data Lake Store Account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object to create
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location
};

client.account.create(resourceGroupName, accountName, accountToCreate, function (err, result, request, response) {
  if (err) {
    console.log(err);
    /*err has reference to the actual request and response, so you can see what was sent and received on the wire.
      The structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'The response body if any',
        request: reference to a stripped version of http request
        response: reference to a stripped version of the response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a><span data-ttu-id="291d4-134">Creación de un archivo con contenido</span><span class="sxs-lookup"><span data-stu-id="291d4-134">Create a file with content</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var fileToCreate = '/myfolder/myfile.txt';
var options = {
  streamContents: new Buffer('some string content')
}

filesystemClient.fileSystem.listFileStatus(accountName, fileToCreate, options, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    // no result is returned, only a 201 response for success.
    console.log('response is: ' + util.inspect(response, {depth: null}));
  }
});
```

## <a name="get-a-list-of-files-and-folders"></a><span data-ttu-id="291d4-135">Obtención de una lista de archivos y carpetas</span><span class="sxs-lookup"><span data-stu-id="291d4-135">Get a list of files and folders</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var pathToEnumerate = '/myfolder';
filesystemClient.fileSystem.listFileStatus(accountName, pathToEnumerate, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a><span data-ttu-id="291d4-136">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="291d4-136">See also</span></span>
* [<span data-ttu-id="291d4-137">Microsoft Azure SDK for Node.js (Microsoft Azure SDK para Node.js)</span><span class="sxs-lookup"><span data-stu-id="291d4-137">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="291d4-138">Microsoft Azure SDK for Node.js - Data Lake Store Management (Microsoft Azure SDK para Node.js: Administración de Análisis de Data Lake)</span><span class="sxs-lookup"><span data-stu-id="291d4-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span></span>](https://www.npmjs.com/package/azure-arm-datalake-analytics)

