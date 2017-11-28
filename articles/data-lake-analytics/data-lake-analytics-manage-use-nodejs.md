---
title: "Análisis de Data Lake de Azure con Azure SDK para Node.js aaaManage | Documentos de Microsoft"
description: "Obtenga información acerca de cómo cuentas de análisis de Data Lake toomanage, orígenes de datos, trabajos y usuarios con Azure SDK para Node.js"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 9de1bcf4-b15b-4d0b-9284-8889ecf0c438
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 07acd058bf252af2fc98c4cfe87a135e0b79900f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-sdk-for-nodejs"></a><span data-ttu-id="d9802-103">Administración de Análisis de Azure Data Lake mediante Azure SDK para Node.js</span><span class="sxs-lookup"><span data-stu-id="d9802-103">Manage Azure Data Lake Analytics using Azure SDK for Node.js</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="d9802-104">Hello Azure SDK para Node.js puede usarse para administrar las cuentas, los trabajos y catálogos de análisis de Data Lake de Azure.</span><span class="sxs-lookup"><span data-stu-id="d9802-104">hello Azure SDK for Node.js can be used for managing Azure Data Lake Analytics accounts, jobs and catalogs.</span></span> <span data-ttu-id="d9802-105">tema de administración de toosee con otras herramientas, haga clic en Seleccionar de pestaña de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="d9802-105">toosee management topic using other tools, click hello tab select above.</span></span>

<span data-ttu-id="d9802-106">Ahora es compatible con:</span><span class="sxs-lookup"><span data-stu-id="d9802-106">Right now it supports:</span></span>

* <span data-ttu-id="d9802-107">**Versión de Node.js: 0.10.0 o superior**</span><span class="sxs-lookup"><span data-stu-id="d9802-107">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="d9802-108">**Versión de API de REST para la cuenta: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="d9802-108">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="d9802-109">**Versión de API de REST para el catálogo: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="d9802-109">**REST API version for Catalog: 2015-10-01-preview**</span></span>
* <span data-ttu-id="d9802-110">**Versión de API de REST para el trabajo: 2016-03-20-preview**</span><span class="sxs-lookup"><span data-stu-id="d9802-110">**REST API version for Job: 2016-03-20-preview**</span></span>

## <a name="features"></a><span data-ttu-id="d9802-111">Características</span><span class="sxs-lookup"><span data-stu-id="d9802-111">Features</span></span>
* <span data-ttu-id="d9802-112">Administración de cuentas: crear, obtener, enumerar, actualizar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="d9802-112">Account management: create, get, list, update, and delete.</span></span>
* <span data-ttu-id="d9802-113">Administración de trabajos: enviar, obtener, enumerar y cancelar.</span><span class="sxs-lookup"><span data-stu-id="d9802-113">Job management: submit, get, list, and cancel.</span></span>
* <span data-ttu-id="d9802-114">Administración de catálogos: obtener y lista.</span><span class="sxs-lookup"><span data-stu-id="d9802-114">Catalog management: get and list.</span></span>

## <a name="how-tooinstall"></a><span data-ttu-id="d9802-115">Cómo tooInstall</span><span class="sxs-lookup"><span data-stu-id="d9802-115">How tooInstall</span></span>
```bash
npm install azure-arm-datalake-analytics
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="d9802-116">Autenticación mediante Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9802-116">Authenticate using Azure Active Directory</span></span>
 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-analytics-client"></a><span data-ttu-id="d9802-117">Crear el cliente de análisis de Data Lake Hola</span><span class="sxs-lookup"><span data-stu-id="d9802-117">Create hello Data Lake Analytics client</span></span>
```javascript
var adlaManagement = require("azure-arm-datalake-analytics");
var acccountClient = new adlaManagement.DataLakeAnalyticsAccountClient(credentials, 'your-subscription-id');
var jobClient = new adlaManagement.DataLakeAnalyticsJobClient(credentials, 'azuredatalakeanalytics.net');
var catalogClient = new adlaManagement.DataLakeAnalyticsCatalogClient(credentials, 'azuredatalakeanalytics.net');
```

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="d9802-118">Creación de una cuenta de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="d9802-118">Create a Data Lake Analytics account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlaacct';
var location = 'eastus2';

// A Data Lake Store account must already have been created toocreate
// a Data Lake Analytics account. See hello Data Lake Store readme for
// information on doing so. For now, we assume one exists already.
var datalakeStoreAccountName = 'existingadlsaccount';

// account object toocreate
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location,
  properties: {
    defaultDataLakeStoreAccount: datalakeStoreAccountName,
    dataLakeStoreAccounts: [
      {
        name: datalakeStoreAccountName
      }
    ]
  }
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

## <a name="get-a-list-of-jobs"></a><span data-ttu-id="d9802-119">Obtención de una lista de dominios</span><span class="sxs-lookup"><span data-stu-id="d9802-119">Get a list of jobs</span></span>
```javascript
var util = require('util');
var accountName = 'testadlaacct';
jobClient.job.list(accountName, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="get-a-list-of-databases-in-hello-data-lake-analytics-catalog"></a><span data-ttu-id="d9802-120">Obtener una lista de bases de datos de hello datos Lake Analytics catálogo</span><span class="sxs-lookup"><span data-stu-id="d9802-120">Get a list of databases in hello Data Lake Analytics Catalog</span></span>
```javascript
var util = require('util');
var accountName = 'testadlaacct';
catalogClient.catalog.listDatabases(accountName, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a><span data-ttu-id="d9802-121">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="d9802-121">See also</span></span>
* [<span data-ttu-id="d9802-122">Microsoft Azure SDK for Node.js</span><span class="sxs-lookup"><span data-stu-id="d9802-122">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="d9802-123">Microsoft Azure SDK for Node.js - Data Lake Store Management</span><span class="sxs-lookup"><span data-stu-id="d9802-123">Microsoft Azure SDK for Node.js - Data Lake Store Management</span></span>](https://github.com/Azure/azure-sdk-for-node/tree/autorest/lib/services/dataLake.Store)

