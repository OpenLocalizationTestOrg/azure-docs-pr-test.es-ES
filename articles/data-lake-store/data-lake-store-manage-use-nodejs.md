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
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a>Introducción a Azure Data Lake Store mediante Azure SDK para Node.js
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [SDK de Java](data-lake-store-get-started-java-sdk.md)
> * [API de REST](data-lake-store-get-started-rest-api.md)
> * [CLI de Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> Para cargar y descargar gran cantidad de datos (archivos de gran tamaño, un gran número de archivos o ambos), se recomienda que realice hello [SDK de Python](data-lake-store-get-started-python.md), hello [.NET SDK](data-lake-store-get-started-net-sdk.md), [CLI de Azure 2.0](data-lake-store-get-started-cli-2.0.md), o [Azure PowerShell](data-lake-store-get-started-powershell.md). Estas opciones tienen un mejor rendimiento que utilizan varios subprocesos tooparallelize Hola el movimiento de datos.
> 
> 

Obtenga información acerca de cómo toouse hello Azure SDK para Node.js toocreate una cuenta de almacén de Data Lake de Azure y realizar operaciones básicas, como por ejemplo crear carpetas, cargar y descargar archivos de datos, eliminar su cuenta, etcetera. Para más información acerca de Data Lake Store, consulte [Información general de Data Lake Store](data-lake-store-overview.md). Actualmente, hello SDK es compatible con

* **Versión de Node.js: 0.10.0 o superior**
* **Versión de API de REST para la cuenta: 2015-10-01-preview**
* **Versión de API de REST para FileSystem: 2015-10-01-preview**

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este artículo, debe tener el siguiente hello:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Cree una aplicación de Azure Active Directory**. Usar la aplicación de almacén de Data Lake de hello Azure AD aplicación tooauthenticate Hola con Azure AD. Hay diferentes enfoques tooauthenticate con Azure AD, que son **autenticación de usuario final** o **autenticación del servicio a servicio**. Para obtener instrucciones y obtener más información acerca de cómo tooauthenticate, consulte [autenticación de usuario final](data-lake-store-end-user-authenticate-using-active-directory.md) o [autenticación del servicio a servicio](data-lake-store-authenticate-using-active-directory.md).

## <a name="how-tooinstall"></a>Cómo tooInstall
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a>Autenticación mediante Azure Active Directory
fragmentos de código de Hello a continuación muestran dos maneras independientes de autenticar con el almacén de Data Lake con Azure AD. Para obtener una explicación detallada sobre toouse de métodos distintos para la autenticación con el almacén de Data Lake, consulte [autenticar con el almacén de Data Lake con Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).

siguiente fragmento de Hello también necesita entradas como nombre de dominio de Azure AD, Id. de cliente para una aplicación de Azure AD, etcetera. Todos estos detalles pueden obtenerse de una aplicación de Azure AD que debe crear, cuyos detalles hello también se incluyen en el vínculo anterior.

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-store-clients"></a>Crear a clientes de la tienda de hello datos Lake
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a>Creación de una cuenta de Almacén de Data Lake
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

## <a name="create-a-file-with-content"></a>Creación de un archivo con contenido
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

## <a name="get-a-list-of-files-and-folders"></a>Obtención de una lista de archivos y carpetas
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

## <a name="see-also"></a>Otras referencias
* [Microsoft Azure SDK for Node.js (Microsoft Azure SDK para Node.js)](https://github.com/azure/azure-sdk-for-node)
* [Microsoft Azure SDK for Node.js - Data Lake Store Management (Microsoft Azure SDK para Node.js: Administración de Análisis de Data Lake)](https://www.npmjs.com/package/azure-arm-datalake-analytics)

