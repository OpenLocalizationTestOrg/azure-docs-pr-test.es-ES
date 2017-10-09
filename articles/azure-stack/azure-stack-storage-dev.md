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
# <a name="get-started-with-azure-stack-storage-development-tools"></a><span data-ttu-id="3911b-103">Empezar a trabajar con herramientas de desarrollo de Azure Stack Storage</span><span class="sxs-lookup"><span data-stu-id="3911b-103">Get started with Azure Stack Storage development tools</span></span> 

<span data-ttu-id="3911b-104">Microsoft Azure Stack proporciona un conjunto de servicios de almacenamiento que incluye Azure Blob Storage, Table Storage y Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="3911b-104">Microsoft Azure Stack provides a set of storage services, including Azure Blob, Table, and Queue storage.</span></span>

<span data-ttu-id="3911b-105">Este artículo proporciona una guía rápida acerca de cómo toostart con herramientas de desarrollo de almacenamiento de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="3911b-105">This article provides quick guidance on how toostart using Azure Stack Storage development tools.</span></span> <span data-ttu-id="3911b-106">Puede encontrar información más detallada y código de ejemplo en tutoriales Hola correspondientes en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="3911b-106">You can find more detailed information and sample code in hello corresponding Azure Storage tutorials.</span></span>

<span data-ttu-id="3911b-107">Hay algunas diferencias conocidas entre Azure Storage y Azure Stack Storage, incluidos algunos requisitos específicos para cada plataforma.</span><span class="sxs-lookup"><span data-stu-id="3911b-107">There are known differences between Azure Storage and Azure Stack Storage, including some specific requirements for each platform.</span></span> <span data-ttu-id="3911b-108">Por ejemplo, hay requisitos de bibliotecas de cliente y de sufijos de puntos de conexión que son específicos de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3911b-108">For example, there are specific client libraries and specific endpoint suffix requirements for Azure Stack.</span></span> <span data-ttu-id="3911b-109">Para más información, consulte [Azure Stack Storage: Diferencias y consideraciones](azure-stack-acs-differences.md).</span><span class="sxs-lookup"><span data-stu-id="3911b-109">For more information, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>

## <a name="azure-client-libraries"></a><span data-ttu-id="3911b-110">Bibliotecas de clientes de Azure</span><span class="sxs-lookup"><span data-stu-id="3911b-110">Azure client libraries</span></span>
<span data-ttu-id="3911b-111">Hola admitida la versión de API de REST para el almacenamiento de la pila de Azure es 2015-04-05.</span><span class="sxs-lookup"><span data-stu-id="3911b-111">hello supported REST API version for Azure Stack Storage is 2015-04-05.</span></span> <span data-ttu-id="3911b-112">No tiene paridad completa con la versión más reciente de Hola de hello API de REST de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="3911b-112">It doesn’t have full parity with hello latest version of hello Azure Storage REST API.</span></span> <span data-ttu-id="3911b-113">Por lo que para las bibliotecas de cliente de almacenamiento de hello, deberá toobe consciente de la versión de Hola que sea compatible con REST API 2015-04-05.</span><span class="sxs-lookup"><span data-stu-id="3911b-113">So for hello storage client libraries, you need toobe aware of hello version that is compatible with REST API 2015-04-05.</span></span>


|<span data-ttu-id="3911b-114">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="3911b-114">Client library</span></span>|<span data-ttu-id="3911b-115">Versión compatible de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3911b-115">Azure Stack supported version</span></span>|<span data-ttu-id="3911b-116">Vínculo</span><span class="sxs-lookup"><span data-stu-id="3911b-116">Link</span></span>|<span data-ttu-id="3911b-117">Especificación de punto de conexión</span><span class="sxs-lookup"><span data-stu-id="3911b-117">Endpoint specification</span></span>|
|---------|---------|---------|---------|
|<span data-ttu-id="3911b-118">.NET</span><span class="sxs-lookup"><span data-stu-id="3911b-118">.NET</span></span>     |<span data-ttu-id="3911b-119">6.2.0</span><span class="sxs-lookup"><span data-stu-id="3911b-119">6.2.0</span></span>|<span data-ttu-id="3911b-120">Paquete NuGet:</span><span class="sxs-lookup"><span data-stu-id="3911b-120">Nuget package:</span></span><br>[<span data-ttu-id="3911b-121">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span><span class="sxs-lookup"><span data-stu-id="3911b-121">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)<br><br><span data-ttu-id="3911b-122">Versión de GitHub:</span><span class="sxs-lookup"><span data-stu-id="3911b-122">GitHub release:</span></span><br>[<span data-ttu-id="3911b-123">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span><span class="sxs-lookup"><span data-stu-id="3911b-123">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span></span>](https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1)|<span data-ttu-id="3911b-124">archivo app.config</span><span class="sxs-lookup"><span data-stu-id="3911b-124">app.config file</span></span>|
|<span data-ttu-id="3911b-125">Java</span><span class="sxs-lookup"><span data-stu-id="3911b-125">Java</span></span>|<span data-ttu-id="3911b-126">4.1.0</span><span class="sxs-lookup"><span data-stu-id="3911b-126">4.1.0</span></span>|<span data-ttu-id="3911b-127">Paquete Maven:</span><span class="sxs-lookup"><span data-stu-id="3911b-127">Maven package:</span></span><br>[<span data-ttu-id="3911b-128">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span><span class="sxs-lookup"><span data-stu-id="3911b-128">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span></span>](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0)<br><br><span data-ttu-id="3911b-129">Versión de GitHub:</span><span class="sxs-lookup"><span data-stu-id="3911b-129">GitHub release:</span></span><br> [<span data-ttu-id="3911b-130">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span><span class="sxs-lookup"><span data-stu-id="3911b-130">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span></span>](https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0)|<span data-ttu-id="3911b-131">Configuración de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="3911b-131">Connection string setup</span></span>|
|<span data-ttu-id="3911b-132">Node.js</span><span class="sxs-lookup"><span data-stu-id="3911b-132">Node.js</span></span>     |<span data-ttu-id="3911b-133">1.1.0</span><span class="sxs-lookup"><span data-stu-id="3911b-133">1.1.0</span></span>|<span data-ttu-id="3911b-134">Vínculo NPM:</span><span class="sxs-lookup"><span data-stu-id="3911b-134">NPM link:</span></span><br>[<span data-ttu-id="3911b-135">https://www.npmjs.com/package/azure-storage</span><span class="sxs-lookup"><span data-stu-id="3911b-135">https://www.npmjs.com/package/azure-storage</span></span>](https://www.npmjs.com/package/azure-storage)<br><span data-ttu-id="3911b-136">(ejecute: `npm install azure-storage@1.1.0)`</span><span class="sxs-lookup"><span data-stu-id="3911b-136">(run: `npm install azure-storage@1.1.0)`</span></span><br><br><span data-ttu-id="3911b-137">Versión de GitHub:</span><span class="sxs-lookup"><span data-stu-id="3911b-137">Github release:</span></span><br>[<span data-ttu-id="3911b-138">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span><span class="sxs-lookup"><span data-stu-id="3911b-138">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span></span>](https://github.com/Azure/azure-storage-node/releases/tag/1.1.0)|<span data-ttu-id="3911b-139">Declaración de instancia de servicio</span><span class="sxs-lookup"><span data-stu-id="3911b-139">Service instance declaration</span></span>||<span data-ttu-id="3911b-140">C++</span><span class="sxs-lookup"><span data-stu-id="3911b-140">C++</span></span>|<span data-ttu-id="3911b-141">2.4.0</span><span class="sxs-lookup"><span data-stu-id="3911b-141">2.4.0</span></span>|<span data-ttu-id="3911b-142">Paquete NuGet:</span><span class="sxs-lookup"><span data-stu-id="3911b-142">Nuget package:</span></span><br>[<span data-ttu-id="3911b-143">https://www.nuget.org/packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="3911b-143">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="3911b-144">Versión de GitHub:</span><span class="sxs-lookup"><span data-stu-id="3911b-144">GitHub release:</span></span><br>[<span data-ttu-id="3911b-145">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="3911b-145">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="3911b-146">Configuración de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="3911b-146">Connection string setup</span></span>|
|<span data-ttu-id="3911b-147">C++</span><span class="sxs-lookup"><span data-stu-id="3911b-147">C++</span></span>|<span data-ttu-id="3911b-148">2.4.0</span><span class="sxs-lookup"><span data-stu-id="3911b-148">2.4.0</span></span>|<span data-ttu-id="3911b-149">Paquete NuGet:</span><span class="sxs-lookup"><span data-stu-id="3911b-149">Nuget package:</span></span><br>[<span data-ttu-id="3911b-150">https://www.nuget.org/packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="3911b-150">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="3911b-151">Versión de GitHub:</span><span class="sxs-lookup"><span data-stu-id="3911b-151">GitHub release:</span></span><br>[<span data-ttu-id="3911b-152">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="3911b-152">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="3911b-153">Configuración de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="3911b-153">Connection string setup</span></span>|
|<span data-ttu-id="3911b-154">PHP</span><span class="sxs-lookup"><span data-stu-id="3911b-154">PHP</span></span>|<span data-ttu-id="3911b-155">0.15.0</span><span class="sxs-lookup"><span data-stu-id="3911b-155">0.15.0</span></span>|<span data-ttu-id="3911b-156">Versión de GitHub:</span><span class="sxs-lookup"><span data-stu-id="3911b-156">GitHub release:</span></span><br>[<span data-ttu-id="3911b-157">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span><span class="sxs-lookup"><span data-stu-id="3911b-157">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span></span>](https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0)<br><br><span data-ttu-id="3911b-158">Instalación a través de Composer (consulte los detalles a continuación)</span><span class="sxs-lookup"><span data-stu-id="3911b-158">Install via Composer (see details below)</span></span>|<span data-ttu-id="3911b-159">Configuración de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="3911b-159">Connection string setup</span></span>|
|<span data-ttu-id="3911b-160">Python</span><span class="sxs-lookup"><span data-stu-id="3911b-160">Python</span></span>     |<span data-ttu-id="3911b-161">0.30.0</span><span class="sxs-lookup"><span data-stu-id="3911b-161">0.30.0</span></span>|<span data-ttu-id="3911b-162">Paquete PIP:</span><span class="sxs-lookup"><span data-stu-id="3911b-162">PIP package:</span></span><br> [<span data-ttu-id="3911b-163">https://pypi.python.org/pypi/azure-storage/0.30.0</span><span class="sxs-lookup"><span data-stu-id="3911b-163">https://pypi.python.org/pypi/azure-storage/0.30.0</span></span>](https://pypi.python.org/pypi/azure-storage/0.30.0)<br><span data-ttu-id="3911b-164">(Ejecute: `pip install -v azure-storage==0.30.0)`</span><span class="sxs-lookup"><span data-stu-id="3911b-164">(Run: `pip install -v azure-storage==0.30.0)`</span></span><br><br><span data-ttu-id="3911b-165">Versión de GitHub:</span><span class="sxs-lookup"><span data-stu-id="3911b-165">GitHub release:</span></span><br> [<span data-ttu-id="3911b-166">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span><span class="sxs-lookup"><span data-stu-id="3911b-166">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span></span>](https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0)|<span data-ttu-id="3911b-167">Declaración de instancia de servicio</span><span class="sxs-lookup"><span data-stu-id="3911b-167">Service instance declaration</span></span>|
|<span data-ttu-id="3911b-168">Ruby</span><span class="sxs-lookup"><span data-stu-id="3911b-168">Ruby</span></span>|<span data-ttu-id="3911b-169">0.12.1</span><span class="sxs-lookup"><span data-stu-id="3911b-169">0.12.1</span></span><br><span data-ttu-id="3911b-170">Vista previa</span><span class="sxs-lookup"><span data-stu-id="3911b-170">Preview</span></span>|<span data-ttu-id="3911b-171">Paquete de RubyGems:</span><span class="sxs-lookup"><span data-stu-id="3911b-171">RubyGems package:</span></span><br> [<span data-ttu-id="3911b-172">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span><span class="sxs-lookup"><span data-stu-id="3911b-172">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span></span>](https://rubygems.org/gems/azure-storage/versions/0.12.1.preview)<br><br><span data-ttu-id="3911b-173">Versión de GitHub:</span><span class="sxs-lookup"><span data-stu-id="3911b-173">GitHub release:</span></span><br> [<span data-ttu-id="3911b-174">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span><span class="sxs-lookup"><span data-stu-id="3911b-174">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span></span>](https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1)|<span data-ttu-id="3911b-175">Configuración de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="3911b-175">Connection string setup</span></span>|

> [!NOTE]
> <span data-ttu-id="3911b-176">Detalles de PHP</span><span class="sxs-lookup"><span data-stu-id="3911b-176">PHP details</span></span><br><br>
><span data-ttu-id="3911b-177">tooinstall a través de compositor:</span><span class="sxs-lookup"><span data-stu-id="3911b-177">tooinstall via Composer:</span></span>
>1. <span data-ttu-id="3911b-178">Cree un archivo denominado `composer.json` en raíz de Hola de proyecto Hola con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="3911b-178">Create a file named `composer.json` in hello root of hello project with following code:</span></span><br>
>
>   ```
>   {
>       "require":{
>           "Microsoft/azure-storage":"0.15.0"
>        }
>    }
>   ```
>
>2. <span data-ttu-id="3911b-179">Descargar [composer.phar](http://getcomposer.org/composer.phar) en la raíz del proyecto Hola.</span><span class="sxs-lookup"><span data-stu-id="3911b-179">Download [composer.phar](http://getcomposer.org/composer.phar) into hello project root.</span></span>
>3. <span data-ttu-id="3911b-180">Ejecute `php composer.phar install`.</span><span class="sxs-lookup"><span data-stu-id="3911b-180">Run: `php composer.phar install`.</span></span>
>


## <a name="endpoint-declaration"></a><span data-ttu-id="3911b-181">Declaración de punto de conexión</span><span class="sxs-lookup"><span data-stu-id="3911b-181">Endpoint declaration</span></span>
<span data-ttu-id="3911b-182">Un punto de conexión de la pila de Azure incluye dos partes: nombre de Hola de un dominio de Azure pila hello y región.</span><span class="sxs-lookup"><span data-stu-id="3911b-182">An Azure Stack endpoint includes two parts: hello name of a region and hello Azure Stack domain.</span></span>
<span data-ttu-id="3911b-183">Hola Kit de desarrollo de pila de Azure, es el punto de conexión de hello predeterminado **local.azurestack.external**.</span><span class="sxs-lookup"><span data-stu-id="3911b-183">In hello Azure Stack Development Kit, hello default endpoint is **local.azurestack.external**.</span></span>
<span data-ttu-id="3911b-184">Si no está seguro de cuál es su punto de conexión, póngase en contacto con el administrador de la nube.</span><span class="sxs-lookup"><span data-stu-id="3911b-184">Contact your cloud administrator if you’re not sure about your endpoint.</span></span>

## <a name="examples"></a><span data-ttu-id="3911b-185">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="3911b-185">Examples</span></span>


### <a name="net"></a><span data-ttu-id="3911b-186">.NET</span><span class="sxs-lookup"><span data-stu-id="3911b-186">.NET</span></span>

<span data-ttu-id="3911b-187">Para la pila de Azure, el sufijo del extremo de Hola se especifica en el archivo app.config de hello:</span><span class="sxs-lookup"><span data-stu-id="3911b-187">For Azure Stack, hello endpoint suffix is specified in hello app.config file:</span></span>

```
<add key="StorageConnectionString" 
value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;
EndpointSuffix=local.azurestack.external;" />
```
### <a name="java"></a><span data-ttu-id="3911b-188">Java</span><span class="sxs-lookup"><span data-stu-id="3911b-188">Java</span></span>

<span data-ttu-id="3911b-189">Para la pila de Azure, el sufijo del extremo de Hola se especifica en el programa de instalación de Hola de cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="3911b-189">For Azure Stack, hello endpoint suffix is specified in hello setup of connection string:</span></span>

```
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key;" +
    "EndpointSuffix=local.azurestack.external";
```

### <a name="nodejs"></a><span data-ttu-id="3911b-190">Node.js</span><span class="sxs-lookup"><span data-stu-id="3911b-190">Node.js</span></span>

<span data-ttu-id="3911b-191">Para la pila de Azure, el sufijo del extremo de Hola se especifica en la instancia de la declaración de Hola:</span><span class="sxs-lookup"><span data-stu-id="3911b-191">For Azure Stack, hello endpoint suffix is specified in hello declaration instance:</span></span>

```
var blobSvc = azure.createBlobService('myaccount', 'mykey',
'myaccount.blob.local.azurestack.external');
```
### <a name="c"></a><span data-ttu-id="3911b-192">C++</span><span class="sxs-lookup"><span data-stu-id="3911b-192">C++</span></span>

<span data-ttu-id="3911b-193">Para la pila de Azure, el sufijo del extremo de Hola se especifica en el programa de instalación de Hola de cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="3911b-193">For Azure Stack, hello endpoint suffix is specified in hello setup of connection string:</span></span>

```
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;
AccountName=your_storage_account;
AccountKey=your_storage_account_key;
EndpointSuffix=local.azurestack.external"));
```

### <a name="php"></a><span data-ttu-id="3911b-194">PHP</span><span class="sxs-lookup"><span data-stu-id="3911b-194">PHP</span></span>

<span data-ttu-id="3911b-195">Para la pila de Azure, el sufijo del extremo de Hola se especifica en el programa de instalación de Hola de cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="3911b-195">For Azure Stack, hello endpoint suffix is specified in hello setup of connection string:</span></span>

```
$connectionString = 'BlobEndpoint=http://<storage account name>.blob.local.azurestack.external/;
QueueEndpoint=http:// <storage account name>.queue.local.azurestack.external/;
TableEndpoint=http:// <storage account name>.table.local.azurestack.external/;
AccountName=<storage account name>;AccountKey=<storage account key>'
```

### <a name="python"></a><span data-ttu-id="3911b-196">Python</span><span class="sxs-lookup"><span data-stu-id="3911b-196">Python</span></span>

<span data-ttu-id="3911b-197">Para la pila de Azure, el sufijo del extremo de Hola se especifica en la instancia de la declaración de Hola:</span><span class="sxs-lookup"><span data-stu-id="3911b-197">For Azure Stack, hello endpoint suffix is specified in hello declaration instance:</span></span>

```
block_blob_service = BlockBlobService(account_name='myaccount',
account_key='mykey',
endpoint_suffix='local.azurestack.external')
```
### <a name="ruby"></a><span data-ttu-id="3911b-198">Ruby</span><span class="sxs-lookup"><span data-stu-id="3911b-198">Ruby</span></span>

<span data-ttu-id="3911b-199">Para la pila de Azure, el sufijo del extremo de Hola se especifica en el programa de instalación de Hola de cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="3911b-199">For Azure Stack, hello endpoint suffix is specified in hello setup of connection string:</span></span>

```
set
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;
AccountName=myaccount;
AccountKey=mykey;
EndpointSuffix=local.azurestack.external
```

## <a name="blob-storage"></a><span data-ttu-id="3911b-200">Almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="3911b-200">Blob storage</span></span>

<span data-ttu-id="3911b-201">Hello siguientes tutoriales de almacenamiento de blobs de Azure son aplicable tooAzure pila.</span><span class="sxs-lookup"><span data-stu-id="3911b-201">hello following Azure Blob storage tutorials are applicable tooAzure Stack.</span></span> <span data-ttu-id="3911b-202">Requisito de sufijo de nota Hola extremo concreto para la pila de Azure se describe en hello anterior [ejemplos](#examples) sección.</span><span class="sxs-lookup"><span data-stu-id="3911b-202">Note hello specific endpoint suffix requirement for Azure Stack described in hello previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="3911b-203">Introducción al Almacenamiento de blobs de Azure mediante .NET</span><span class="sxs-lookup"><span data-stu-id="3911b-203">Get started with Azure Blob storage using .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="3911b-204">¿Cómo toouse almacenamiento de blobs desde Java</span><span class="sxs-lookup"><span data-stu-id="3911b-204">How toouse Blob storage from Java</span></span>](../storage/blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="3911b-205">¿Cómo toouse almacenamiento de blobs de Node.js</span><span class="sxs-lookup"><span data-stu-id="3911b-205">How toouse Blob storage from Node.js</span></span>](../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="3911b-206">¿Cómo toouse almacenamiento de blobs de C++</span><span class="sxs-lookup"><span data-stu-id="3911b-206">How toouse Blob storage from C++</span></span>](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="3911b-207">¿Cómo toouse almacenamiento de blobs de PHP</span><span class="sxs-lookup"><span data-stu-id="3911b-207">How toouse Blob storage from PHP</span></span>](../storage/blobs/storage-php-how-to-use-blobs.md)
* [<span data-ttu-id="3911b-208">¿Cómo toouse almacenamiento de blobs de Azure de Python</span><span class="sxs-lookup"><span data-stu-id="3911b-208">How toouse Azure Blob storage from Python</span></span>](../storage/blobs/storage-python-how-to-use-blob-storage.md)
* [<span data-ttu-id="3911b-209">¿Cómo toouse almacenamiento de blobs de Ruby</span><span class="sxs-lookup"><span data-stu-id="3911b-209">How toouse Blob storage from Ruby</span></span>](../storage/blobs/storage-ruby-how-to-use-blob-storage.md)

## <a name="queue-storage"></a><span data-ttu-id="3911b-210">Queue Storage</span><span class="sxs-lookup"><span data-stu-id="3911b-210">Queue storage</span></span>

<span data-ttu-id="3911b-211">Hello siguientes tutoriales de almacenamiento de cola de Azure son aplicable tooAzure pila.</span><span class="sxs-lookup"><span data-stu-id="3911b-211">hello following Azure Queue storage tutorials are applicable tooAzure Stack.</span></span> <span data-ttu-id="3911b-212">Requisito de sufijo de nota Hola extremo concreto para la pila de Azure se describe en hello anterior [ejemplos](#examples) sección.</span><span class="sxs-lookup"><span data-stu-id="3911b-212">Note hello specific endpoint suffix requirement for Azure Stack described in hello previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="3911b-213">Introducción a Azure Queue Storage mediante .NET</span><span class="sxs-lookup"><span data-stu-id="3911b-213">Get started with Azure Queue storage using .NET</span></span>](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="3911b-214">¿Cómo toouse almacenamiento de cola en Java</span><span class="sxs-lookup"><span data-stu-id="3911b-214">How toouse Queue storage from Java</span></span>](../storage/queues/storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="3911b-215">¿Cómo toouse almacenamiento de cola de Node.js</span><span class="sxs-lookup"><span data-stu-id="3911b-215">How toouse Queue storage from Node.js</span></span>](../storage/queues/storage-nodejs-how-to-use-queues.md)
* [<span data-ttu-id="3911b-216">¿Cómo toouse almacenamiento de cola desde C++</span><span class="sxs-lookup"><span data-stu-id="3911b-216">How toouse Queue storage from C++</span></span>](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="3911b-217">¿Cómo toouse almacenamiento de cola de PHP</span><span class="sxs-lookup"><span data-stu-id="3911b-217">How toouse Queue storage from PHP</span></span>](../storage/queues/storage-php-how-to-use-queues.md)
* [<span data-ttu-id="3911b-218">¿Cómo toouse almacenamiento de cola de Python</span><span class="sxs-lookup"><span data-stu-id="3911b-218">How toouse Queue storage from Python</span></span>](../storage/queues/storage-python-how-to-use-queue-storage.md)
* [<span data-ttu-id="3911b-219">¿Cómo toouse Queue storage from. Ruby</span><span class="sxs-lookup"><span data-stu-id="3911b-219">How toouse Queue storage from Ruby</span></span>](../storage/queues/storage-ruby-how-to-use-queue-storage.md)


## <a name="table-storage"></a><span data-ttu-id="3911b-220">Almacenamiento de tablas</span><span class="sxs-lookup"><span data-stu-id="3911b-220">Table storage</span></span>

<span data-ttu-id="3911b-221">Hello siguientes tutoriales de almacenamiento de tabla de Azure son aplicable tooAzure pila.</span><span class="sxs-lookup"><span data-stu-id="3911b-221">hello following Azure Table storage tutorials are applicable tooAzure Stack.</span></span> <span data-ttu-id="3911b-222">Requisito de sufijo de nota Hola extremo concreto para la pila de Azure se describe en hello anterior [ejemplos](#examples) sección.</span><span class="sxs-lookup"><span data-stu-id="3911b-222">Note hello specific endpoint suffix requirement for Azure Stack described in hello previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="3911b-223">Introducción a Azure Table Storage mediante .NET</span><span class="sxs-lookup"><span data-stu-id="3911b-223">Get started with Azure Table storage using .NET</span></span>](../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="3911b-224">¿Cómo toouse almacenamiento de tablas de Java</span><span class="sxs-lookup"><span data-stu-id="3911b-224">How toouse Table storage from Java</span></span>](../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="3911b-225">¿Cómo toouse almacenamiento de tablas de Azure de Node.js</span><span class="sxs-lookup"><span data-stu-id="3911b-225">How toouse Azure Table storage from Node.js</span></span>](../cosmos-db/table-storage-how-to-use-nodejs.md)
* [<span data-ttu-id="3911b-226">¿Cómo toouse almacenamiento de tablas de C++</span><span class="sxs-lookup"><span data-stu-id="3911b-226">How toouse Table storage from C++</span></span>](../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="3911b-227">¿Cómo toouse almacenamiento de tablas de PHP</span><span class="sxs-lookup"><span data-stu-id="3911b-227">How toouse Table storage from PHP</span></span>](../cosmos-db/table-storage-how-to-use-php.md)
* [<span data-ttu-id="3911b-228">¿Cómo toouse almacenamiento de tablas en Python</span><span class="sxs-lookup"><span data-stu-id="3911b-228">How toouse Table storage in Python</span></span>](../cosmos-db/table-storage-how-to-use-python.md)
* [<span data-ttu-id="3911b-229">¿Cómo toouse almacenamiento de tablas de Ruby</span><span class="sxs-lookup"><span data-stu-id="3911b-229">How toouse Table storage from Ruby</span></span>](../cosmos-db/table-storage-how-to-use-ruby.md)

## <a name="next-steps"></a><span data-ttu-id="3911b-230">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3911b-230">Next steps</span></span>

* [<span data-ttu-id="3911b-231">Introducción tooMicrosoft almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="3911b-231">Introduction tooMicrosoft Azure Storage</span></span>](../storage/common/storage-introduction.md)
