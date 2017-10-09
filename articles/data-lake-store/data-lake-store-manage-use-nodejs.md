---
title: "aaaGet a trabajar con el almacén de Data Lake de Azure con Azure SDK para Node.js | Documentos de Microsoft"
description: "Obtenga información acerca de cómo el sistema de archivos toouse Node.js toowork con hello y cuentas de almacén de Data Lake."
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
ms.openlocfilehash: ce36a2e0de4e091a4e85ed784a3381415ef6f9e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a><span data-ttu-id="d8a90-103">Introducción a Azure Data Lake Store mediante Azure SDK para Node.js</span><span class="sxs-lookup"><span data-stu-id="d8a90-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8a90-104">Portal</span><span class="sxs-lookup"><span data-stu-id="d8a90-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="d8a90-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8a90-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="d8a90-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="d8a90-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="d8a90-107">SDK de Java</span><span class="sxs-lookup"><span data-stu-id="d8a90-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="d8a90-108">API de REST</span><span class="sxs-lookup"><span data-stu-id="d8a90-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="d8a90-109">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d8a90-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="d8a90-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="d8a90-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="d8a90-111">Python</span><span class="sxs-lookup"><span data-stu-id="d8a90-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> <span data-ttu-id="d8a90-112">Para cargar y descargar gran cantidad de datos (archivos de gran tamaño, un gran número de archivos o ambos), se recomienda que realice hello [SDK de Python](data-lake-store-get-started-python.md), hello [.NET SDK](data-lake-store-get-started-net-sdk.md), [CLI de Azure 2.0](data-lake-store-get-started-cli-2.0.md), o [Azure PowerShell](data-lake-store-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d8a90-112">For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use hello [Python SDK](data-lake-store-get-started-python.md), hello [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md).</span></span> <span data-ttu-id="d8a90-113">Estas opciones tienen un mejor rendimiento que utilizan varios subprocesos tooparallelize Hola el movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="d8a90-113">These options have better performance as they use multiple threads tooparallelize hello data movement.</span></span>
> 
> 

<span data-ttu-id="d8a90-114">Obtenga información acerca de cómo toouse hello Azure SDK para Node.js toocreate una cuenta de almacén de Data Lake de Azure y realizar operaciones básicas, como por ejemplo crear carpetas, cargar y descargar archivos de datos, eliminar su cuenta, etcetera. Para más información acerca de Data Lake Store, consulte [Información general de Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8a90-114">Learn how toouse hello Azure SDK for Node.js toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span> <span data-ttu-id="d8a90-115">Actualmente, hello SDK es compatible con</span><span class="sxs-lookup"><span data-stu-id="d8a90-115">Currently, hello SDK supports</span></span>

* <span data-ttu-id="d8a90-116">**Versión de Node.js: 0.10.0 o superior**</span><span class="sxs-lookup"><span data-stu-id="d8a90-116">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="d8a90-117">**Versión de API de REST para la cuenta: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="d8a90-117">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="d8a90-118">**Versión de API de REST para FileSystem: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="d8a90-118">**REST API version for FileSystem: 2015-10-01-preview**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8a90-119">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d8a90-119">Prerequisites</span></span>
<span data-ttu-id="d8a90-120">Antes de comenzar este artículo, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="d8a90-120">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="d8a90-121">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="d8a90-121">**An Azure subscription**.</span></span> <span data-ttu-id="d8a90-122">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d8a90-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d8a90-123">**Cree una aplicación de Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d8a90-123">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="d8a90-124">Usar la aplicación de almacén de Data Lake de hello Azure AD aplicación tooauthenticate Hola con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8a90-124">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="d8a90-125">Hay diferentes enfoques tooauthenticate con Azure AD, que son **autenticación de usuario final** o **autenticación del servicio a servicio**.</span><span class="sxs-lookup"><span data-stu-id="d8a90-125">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="d8a90-126">Para obtener instrucciones y obtener más información acerca de cómo tooauthenticate, consulte [autenticación de usuario final](data-lake-store-end-user-authenticate-using-active-directory.md) o [autenticación del servicio a servicio](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="d8a90-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="how-tooinstall"></a><span data-ttu-id="d8a90-127">Cómo tooInstall</span><span class="sxs-lookup"><span data-stu-id="d8a90-127">How tooInstall</span></span>
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="d8a90-128">Autenticación mediante Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8a90-128">Authenticate using Azure Active Directory</span></span>
<span data-ttu-id="d8a90-129">fragmentos de código de Hello a continuación muestran dos maneras independientes de autenticar con el almacén de Data Lake con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8a90-129">hello snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span></span> <span data-ttu-id="d8a90-130">Para obtener una explicación detallada sobre toouse de métodos distintos para la autenticación con el almacén de Data Lake, consulte [autenticar con el almacén de Data Lake con Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="d8a90-130">For a detailed discussion on various methods toouse for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="d8a90-131">siguiente fragmento de Hello también necesita entradas como nombre de dominio de Azure AD, Id. de cliente para una aplicación de Azure AD, etcetera. Todos estos detalles pueden obtenerse de una aplicación de Azure AD que debe crear, cuyos detalles hello también se incluyen en el vínculo anterior.</span><span class="sxs-lookup"><span data-stu-id="d8a90-131">hello snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, hello details of which are also included in link above.</span></span>

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-store-clients"></a><span data-ttu-id="d8a90-132">Crear a clientes de la tienda de hello datos Lake</span><span class="sxs-lookup"><span data-stu-id="d8a90-132">Create hello Data Lake Store Clients</span></span>
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="d8a90-133">Creación de una cuenta de Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="d8a90-133">Create a Data Lake Store Account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object toocreate
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
    /*err has reference toohello actual request and response, so you can see what was sent and received on hello wire.
      hello structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'hello response body if any',
        request: reference tooa stripped version of http request
        response: reference tooa stripped version of hello response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a><span data-ttu-id="d8a90-134">Creación de un archivo con contenido</span><span class="sxs-lookup"><span data-stu-id="d8a90-134">Create a file with content</span></span>
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

## <a name="get-a-list-of-files-and-folders"></a><span data-ttu-id="d8a90-135">Obtención de una lista de archivos y carpetas</span><span class="sxs-lookup"><span data-stu-id="d8a90-135">Get a list of files and folders</span></span>
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

## <a name="see-also"></a><span data-ttu-id="d8a90-136">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="d8a90-136">See also</span></span>
* [<span data-ttu-id="d8a90-137">Microsoft Azure SDK for Node.js (Microsoft Azure SDK para Node.js)</span><span class="sxs-lookup"><span data-stu-id="d8a90-137">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="d8a90-138">Microsoft Azure SDK for Node.js - Data Lake Store Management (Microsoft Azure SDK para Node.js: Administración de Análisis de Data Lake)</span><span class="sxs-lookup"><span data-stu-id="d8a90-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span></span>](https://www.npmjs.com/package/azure-arm-datalake-analytics)

