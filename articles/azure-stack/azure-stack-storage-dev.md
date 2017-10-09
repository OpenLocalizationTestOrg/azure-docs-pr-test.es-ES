---
title: aaaGet a trabajar con herramientas de desarrollo de almacenamiento de la pila de Azure
description: "Tooget instrucciones Introducción al uso de herramientas de desarrollo de almacenamiento de la pila de Azure"
services: azure-stack
author: xiaofmao
ms.author: xiaofmao
ms.date: 7/21/2017
ms.topic: get-started-article
ms.service: azure-stack
ms.openlocfilehash: 0756ed1b9fad4aed0cca4cfd719ef3334dec6700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-stack-storage-development-tools"></a>Empezar a trabajar con herramientas de desarrollo de Azure Stack Storage 

Microsoft Azure Stack proporciona un conjunto de servicios de almacenamiento que incluye Azure Blob Storage, Table Storage y Queue Storage.

Este artículo proporciona una guía rápida acerca de cómo toostart con herramientas de desarrollo de almacenamiento de la pila de Azure. Puede encontrar información más detallada y código de ejemplo en tutoriales Hola correspondientes en el almacenamiento de Azure.

Hay algunas diferencias conocidas entre Azure Storage y Azure Stack Storage, incluidos algunos requisitos específicos para cada plataforma. Por ejemplo, hay requisitos de bibliotecas de cliente y de sufijos de puntos de conexión que son específicos de Azure Stack. Para más información, consulte [Azure Stack Storage: Diferencias y consideraciones](azure-stack-acs-differences.md).

## <a name="azure-client-libraries"></a>Bibliotecas de clientes de Azure
Hola admitida la versión de API de REST para el almacenamiento de la pila de Azure es 2015-04-05. No tiene paridad completa con la versión más reciente de Hola de hello API de REST de almacenamiento de Azure. Por lo que para las bibliotecas de cliente de almacenamiento de hello, deberá toobe consciente de la versión de Hola que sea compatible con REST API 2015-04-05.


|Biblioteca de cliente|Versión compatible de Azure Stack|Vínculo|Especificación de punto de conexión|
|---------|---------|---------|---------|
|.NET     |6.2.0|Paquete NuGet:<br>[https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0](https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)<br><br>Versión de GitHub:<br>[https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1](https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1)|archivo app.config|
|Java|4.1.0|Paquete Maven:<br>[http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0)<br><br>Versión de GitHub:<br> [https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0](https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0)|Configuración de la cadena de conexión|
|Node.js     |1.1.0|Vínculo NPM:<br>[https://www.npmjs.com/package/azure-storage](https://www.npmjs.com/package/azure-storage)<br>(ejecute: `npm install azure-storage@1.1.0)`<br><br>Versión de GitHub:<br>[https://github.com/Azure/azure-storage-node/releases/tag/1.1.0](https://github.com/Azure/azure-storage-node/releases/tag/1.1.0)|Declaración de instancia de servicio||C++|2.4.0|Paquete NuGet:<br>[https://www.nuget.org/packages/wastorage.v140/2.4.0](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br>Versión de GitHub:<br>[https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|Configuración de la cadena de conexión|
|C++|2.4.0|Paquete NuGet:<br>[https://www.nuget.org/packages/wastorage.v140/2.4.0](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br>Versión de GitHub:<br>[https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|Configuración de la cadena de conexión|
|PHP|0.15.0|Versión de GitHub:<br>[https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0](https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0)<br><br>Instalación a través de Composer (consulte los detalles a continuación)|Configuración de la cadena de conexión|
|Python     |0.30.0|Paquete PIP:<br> [https://pypi.python.org/pypi/azure-storage/0.30.0](https://pypi.python.org/pypi/azure-storage/0.30.0)<br>(Ejecute: `pip install -v azure-storage==0.30.0)`<br><br>Versión de GitHub:<br> [https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0](https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0)|Declaración de instancia de servicio|
|Ruby|0.12.1<br>Vista previa|Paquete de RubyGems:<br> [https://rubygems.org/gems/azure-storage/versions/0.12.1.preview](https://rubygems.org/gems/azure-storage/versions/0.12.1.preview)<br><br>Versión de GitHub:<br> [https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1](https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1)|Configuración de la cadena de conexión|

> [!NOTE]
> Detalles de PHP<br><br>
>tooinstall a través de compositor:
>1. Cree un archivo denominado `composer.json` en raíz de Hola de proyecto Hola con el código siguiente:<br>
>
>   ```
>   {
>       "require":{
>           "Microsoft/azure-storage":"0.15.0"
>        }
>    }
>   ```
>
>2. Descargar [composer.phar](http://getcomposer.org/composer.phar) en la raíz del proyecto Hola.
>3. Ejecute `php composer.phar install`.
>


## <a name="endpoint-declaration"></a>Declaración de punto de conexión
Un punto de conexión de la pila de Azure incluye dos partes: nombre de Hola de un dominio de Azure pila hello y región.
Hola Kit de desarrollo de pila de Azure, es el punto de conexión de hello predeterminado **local.azurestack.external**.
Si no está seguro de cuál es su punto de conexión, póngase en contacto con el administrador de la nube.

## <a name="examples"></a>Ejemplos


### <a name="net"></a>.NET

Para la pila de Azure, el sufijo del extremo de Hola se especifica en el archivo app.config de hello:

```
<add key="StorageConnectionString" 
value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;
EndpointSuffix=local.azurestack.external;" />
```
### <a name="java"></a>Java

Para la pila de Azure, el sufijo del extremo de Hola se especifica en el programa de instalación de Hola de cadena de conexión:

```
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key;" +
    "EndpointSuffix=local.azurestack.external";
```

### <a name="nodejs"></a>Node.js

Para la pila de Azure, el sufijo del extremo de Hola se especifica en la instancia de la declaración de Hola:

```
var blobSvc = azure.createBlobService('myaccount', 'mykey',
'myaccount.blob.local.azurestack.external');
```
### <a name="c"></a>C++

Para la pila de Azure, el sufijo del extremo de Hola se especifica en el programa de instalación de Hola de cadena de conexión:

```
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;
AccountName=your_storage_account;
AccountKey=your_storage_account_key;
EndpointSuffix=local.azurestack.external"));
```

### <a name="php"></a>PHP

Para la pila de Azure, el sufijo del extremo de Hola se especifica en el programa de instalación de Hola de cadena de conexión:

```
$connectionString = 'BlobEndpoint=http://<storage account name>.blob.local.azurestack.external/;
QueueEndpoint=http:// <storage account name>.queue.local.azurestack.external/;
TableEndpoint=http:// <storage account name>.table.local.azurestack.external/;
AccountName=<storage account name>;AccountKey=<storage account key>'
```

### <a name="python"></a>Python

Para la pila de Azure, el sufijo del extremo de Hola se especifica en la instancia de la declaración de Hola:

```
block_blob_service = BlockBlobService(account_name='myaccount',
account_key='mykey',
endpoint_suffix='local.azurestack.external')
```
### <a name="ruby"></a>Ruby

Para la pila de Azure, el sufijo del extremo de Hola se especifica en el programa de instalación de Hola de cadena de conexión:

```
set
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;
AccountName=myaccount;
AccountKey=mykey;
EndpointSuffix=local.azurestack.external
```

## <a name="blob-storage"></a>Almacenamiento de blobs

Hello siguientes tutoriales de almacenamiento de blobs de Azure son aplicable tooAzure pila. Requisito de sufijo de nota Hola extremo concreto para la pila de Azure se describe en hello anterior [ejemplos](#examples) sección.

* [Introducción al Almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [¿Cómo toouse almacenamiento de blobs desde Java](../storage/blobs/storage-java-how-to-use-blob-storage.md)
* [¿Cómo toouse almacenamiento de blobs de Node.js](../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)
* [¿Cómo toouse almacenamiento de blobs de C++](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [¿Cómo toouse almacenamiento de blobs de PHP](../storage/blobs/storage-php-how-to-use-blobs.md)
* [¿Cómo toouse almacenamiento de blobs de Azure de Python](../storage/blobs/storage-python-how-to-use-blob-storage.md)
* [¿Cómo toouse almacenamiento de blobs de Ruby](../storage/blobs/storage-ruby-how-to-use-blob-storage.md)

## <a name="queue-storage"></a>Queue Storage

Hello siguientes tutoriales de almacenamiento de cola de Azure son aplicable tooAzure pila. Requisito de sufijo de nota Hola extremo concreto para la pila de Azure se describe en hello anterior [ejemplos](#examples) sección.

* [Introducción a Azure Queue Storage mediante .NET](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [¿Cómo toouse almacenamiento de cola en Java](../storage/queues/storage-java-how-to-use-queue-storage.md)
* [¿Cómo toouse almacenamiento de cola de Node.js](../storage/queues/storage-nodejs-how-to-use-queues.md)
* [¿Cómo toouse almacenamiento de cola desde C++](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [¿Cómo toouse almacenamiento de cola de PHP](../storage/queues/storage-php-how-to-use-queues.md)
* [¿Cómo toouse almacenamiento de cola de Python](../storage/queues/storage-python-how-to-use-queue-storage.md)
* [¿Cómo toouse Queue storage from. Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md)


## <a name="table-storage"></a>Almacenamiento de tablas

Hello siguientes tutoriales de almacenamiento de tabla de Azure son aplicable tooAzure pila. Requisito de sufijo de nota Hola extremo concreto para la pila de Azure se describe en hello anterior [ejemplos](#examples) sección.

* [Introducción a Azure Table Storage mediante .NET](../cosmos-db/table-storage-how-to-use-dotnet.md)
* [¿Cómo toouse almacenamiento de tablas de Java](../cosmos-db/table-storage-how-to-use-java.md)
* [¿Cómo toouse almacenamiento de tablas de Azure de Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md)
* [¿Cómo toouse almacenamiento de tablas de C++](../cosmos-db/table-storage-how-to-use-c-plus.md)
* [¿Cómo toouse almacenamiento de tablas de PHP](../cosmos-db/table-storage-how-to-use-php.md)
* [¿Cómo toouse almacenamiento de tablas en Python](../cosmos-db/table-storage-how-to-use-python.md)
* [¿Cómo toouse almacenamiento de tablas de Ruby](../cosmos-db/table-storage-how-to-use-ruby.md)

## <a name="next-steps"></a>Pasos siguientes

* [Introducción tooMicrosoft almacenamiento de Azure](../storage/common/storage-introduction.md)
