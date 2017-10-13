---
title: Empezar a trabajar con herramientas de desarrollo de Azure Stack Storage
description: "Guía para empezar a trabajar con herramientas de desarrollo de Azure Stack Storage"
services: azure-stack
author: xiaofmao
ms.author: xiaofmao
ms.date: 9/25/2017
ms.topic: get-started-article
ms.service: azure-stack
ms.openlocfilehash: 5b2898c64c0f1b5d804e63fa4e4e1218fa7a672c
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2017
---
# <a name="get-started-with-azure-stack-storage-development-tools"></a><span data-ttu-id="8881f-103">Empezar a trabajar con herramientas de desarrollo de Azure Stack Storage</span><span class="sxs-lookup"><span data-stu-id="8881f-103">Get started with Azure Stack Storage development tools</span></span>

<span data-ttu-id="8881f-104">*Se aplica a: Sistemas integrados de Azure Stack y Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="8881f-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>


<span data-ttu-id="8881f-105">Microsoft Azure Stack proporciona un conjunto de servicios de almacenamiento que incluye Azure Blob Storage, Table Storage y Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="8881f-105">Microsoft Azure Stack provides a set of storage services, including Azure Blob, Table, and Queue storage.</span></span>

<span data-ttu-id="8881f-106">Este artículo proporciona una guía rápida sobre cómo empezar a usar las herramientas de desarrollo de Azure Stack Storage.</span><span class="sxs-lookup"><span data-stu-id="8881f-106">This article provides quick guidance on how to start using Azure Stack Storage development tools.</span></span> <span data-ttu-id="8881f-107">Puede encontrar información más detallada y código de ejemplo en los tutoriales correspondientes de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8881f-107">You can find more detailed information and sample code in the corresponding Azure Storage tutorials.</span></span>

<span data-ttu-id="8881f-108">Hay algunas diferencias conocidas entre Azure Storage y Azure Stack Storage, incluidos algunos requisitos específicos para cada plataforma.</span><span class="sxs-lookup"><span data-stu-id="8881f-108">There are known differences between Azure Storage and Azure Stack Storage, including some specific requirements for each platform.</span></span> <span data-ttu-id="8881f-109">Por ejemplo, hay requisitos de bibliotecas de cliente y de sufijos de puntos de conexión que son específicos de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8881f-109">For example, there are specific client libraries and specific endpoint suffix requirements for Azure Stack.</span></span> <span data-ttu-id="8881f-110">Para más información, consulte [Azure Stack Storage: Diferencias y consideraciones](azure-stack-acs-differences.md).</span><span class="sxs-lookup"><span data-stu-id="8881f-110">For more information, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>

## <a name="azure-client-libraries"></a><span data-ttu-id="8881f-111">Bibliotecas de clientes de Azure</span><span class="sxs-lookup"><span data-stu-id="8881f-111">Azure client libraries</span></span>
<span data-ttu-id="8881f-112">La versión de API de REST compatible con Azure Stack Storage es 2015-04-05.</span><span class="sxs-lookup"><span data-stu-id="8881f-112">The supported REST API version for Azure Stack Storage is 2015-04-05.</span></span> <span data-ttu-id="8881f-113">No tiene una paridad completa con la versión más reciente de la API de REST de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8881f-113">It doesn’t have full parity with the latest version of the Azure Storage REST API.</span></span> <span data-ttu-id="8881f-114">Por tanto, en lo que respecta a las bibliotecas de cliente de almacenamiento debe conocer cuál es la versión compatible con la API de REST 2015-04-05.</span><span class="sxs-lookup"><span data-stu-id="8881f-114">So for the storage client libraries, you need to be aware of the version that is compatible with REST API 2015-04-05.</span></span>


|<span data-ttu-id="8881f-115">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="8881f-115">Client library</span></span>|<span data-ttu-id="8881f-116">Versión compatible de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8881f-116">Azure Stack supported version</span></span>|<span data-ttu-id="8881f-117">Vínculo</span><span class="sxs-lookup"><span data-stu-id="8881f-117">Link</span></span>|<span data-ttu-id="8881f-118">Especificación de punto de conexión</span><span class="sxs-lookup"><span data-stu-id="8881f-118">Endpoint specification</span></span>|
|---------|---------|---------|---------|
|<span data-ttu-id="8881f-119">.NET</span><span class="sxs-lookup"><span data-stu-id="8881f-119">.NET</span></span>     |<span data-ttu-id="8881f-120">6.2.0</span><span class="sxs-lookup"><span data-stu-id="8881f-120">6.2.0</span></span>|<span data-ttu-id="8881f-121">Paquete NuGet:</span><span class="sxs-lookup"><span data-stu-id="8881f-121">Nuget package:</span></span><br>[<span data-ttu-id="8881f-122">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span><span class="sxs-lookup"><span data-stu-id="8881f-122">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)<br><br><span data-ttu-id="8881f-123">Versión de GitHub:</span><span class="sxs-lookup"><span data-stu-id="8881f-123">GitHub release:</span></span><br>[<span data-ttu-id="8881f-124">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span><span class="sxs-lookup"><span data-stu-id="8881f-124">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span></span>](https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1)|<span data-ttu-id="8881f-125">archivo app.config</span><span class="sxs-lookup"><span data-stu-id="8881f-125">app.config file</span></span>|
|<span data-ttu-id="8881f-126">Java</span><span class="sxs-lookup"><span data-stu-id="8881f-126">Java</span></span>|<span data-ttu-id="8881f-127">4.1.0</span><span class="sxs-lookup"><span data-stu-id="8881f-127">4.1.0</span></span>|<span data-ttu-id="8881f-128">Paquete Maven:</span><span class="sxs-lookup"><span data-stu-id="8881f-128">Maven package:</span></span><br>[<span data-ttu-id="8881f-129">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span><span class="sxs-lookup"><span data-stu-id="8881f-129">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span></span>](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0)<br><br><span data-ttu-id="8881f-130">Versión de GitHub:</span><span class="sxs-lookup"><span data-stu-id="8881f-130">GitHub release:</span></span><br> [<span data-ttu-id="8881f-131">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span><span class="sxs-lookup"><span data-stu-id="8881f-131">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span></span>](https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0)|<span data-ttu-id="8881f-132">Configuración de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="8881f-132">Connection string setup</span></span>|
|<span data-ttu-id="8881f-133">Node.js</span><span class="sxs-lookup"><span data-stu-id="8881f-133">Node.js</span></span>     |<span data-ttu-id="8881f-134">1.1.0</span><span class="sxs-lookup"><span data-stu-id="8881f-134">1.1.0</span></span>|<span data-ttu-id="8881f-135">Vínculo NPM:</span><span class="sxs-lookup"><span data-stu-id="8881f-135">NPM link:</span></span><br>[<span data-ttu-id="8881f-136">https://www.npmjs.com/package/azure-storage</span><span class="sxs-lookup"><span data-stu-id="8881f-136">https://www.npmjs.com/package/azure-storage</span></span>](https://www.npmjs.com/package/azure-storage)<br><span data-ttu-id="8881f-137">(ejecute: `npm install azure-storage@1.1.0)`</span><span class="sxs-lookup"><span data-stu-id="8881f-137">(run: `npm install azure-storage@1.1.0)`</span></span><br><br><span data-ttu-id="8881f-138">Versión de GitHub:</span><span class="sxs-lookup"><span data-stu-id="8881f-138">Github release:</span></span><br>[<span data-ttu-id="8881f-139">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span><span class="sxs-lookup"><span data-stu-id="8881f-139">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span></span>](https://github.com/Azure/azure-storage-node/releases/tag/1.1.0)|<span data-ttu-id="8881f-140">Declaración de instancia de servicio</span><span class="sxs-lookup"><span data-stu-id="8881f-140">Service instance declaration</span></span>||<span data-ttu-id="8881f-141">C++</span><span class="sxs-lookup"><span data-stu-id="8881f-141">C++</span></span>|<span data-ttu-id="8881f-142">2.4.0</span><span class="sxs-lookup"><span data-stu-id="8881f-142">2.4.0</span></span>|<span data-ttu-id="8881f-143">Paquete NuGet:</span><span class="sxs-lookup"><span data-stu-id="8881f-143">Nuget package:</span></span><br>[<span data-ttu-id="8881f-144">https://www.nuget.org/packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="8881f-144">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="8881f-145">Versión de GitHub:</span><span class="sxs-lookup"><span data-stu-id="8881f-145">GitHub release:</span></span><br>[<span data-ttu-id="8881f-146">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="8881f-146">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="8881f-147">Configuración de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="8881f-147">Connection string setup</span></span>|
|<span data-ttu-id="8881f-148">C++</span><span class="sxs-lookup"><span data-stu-id="8881f-148">C++</span></span>|<span data-ttu-id="8881f-149">2.4.0</span><span class="sxs-lookup"><span data-stu-id="8881f-149">2.4.0</span></span>|<span data-ttu-id="8881f-150">Paquete NuGet:</span><span class="sxs-lookup"><span data-stu-id="8881f-150">Nuget package:</span></span><br>[<span data-ttu-id="8881f-151">https://www.nuget.org/packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="8881f-151">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="8881f-152">Versión de GitHub:</span><span class="sxs-lookup"><span data-stu-id="8881f-152">GitHub release:</span></span><br>[<span data-ttu-id="8881f-153">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="8881f-153">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="8881f-154">Configuración de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="8881f-154">Connection string setup</span></span>|
|<span data-ttu-id="8881f-155">PHP</span><span class="sxs-lookup"><span data-stu-id="8881f-155">PHP</span></span>|<span data-ttu-id="8881f-156">0.15.0</span><span class="sxs-lookup"><span data-stu-id="8881f-156">0.15.0</span></span>|<span data-ttu-id="8881f-157">Versión de GitHub:</span><span class="sxs-lookup"><span data-stu-id="8881f-157">GitHub release:</span></span><br>[<span data-ttu-id="8881f-158">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span><span class="sxs-lookup"><span data-stu-id="8881f-158">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span></span>](https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0)<br><br><span data-ttu-id="8881f-159">Instalación a través de Composer (consulte los detalles a continuación)</span><span class="sxs-lookup"><span data-stu-id="8881f-159">Install via Composer (see details below)</span></span>|<span data-ttu-id="8881f-160">Configuración de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="8881f-160">Connection string setup</span></span>|
|<span data-ttu-id="8881f-161">Python</span><span class="sxs-lookup"><span data-stu-id="8881f-161">Python</span></span>     |<span data-ttu-id="8881f-162">0.30.0</span><span class="sxs-lookup"><span data-stu-id="8881f-162">0.30.0</span></span>|<span data-ttu-id="8881f-163">Paquete PIP:</span><span class="sxs-lookup"><span data-stu-id="8881f-163">PIP package:</span></span><br> [<span data-ttu-id="8881f-164">https://pypi.python.org/pypi/azure-storage/0.30.0</span><span class="sxs-lookup"><span data-stu-id="8881f-164">https://pypi.python.org/pypi/azure-storage/0.30.0</span></span>](https://pypi.python.org/pypi/azure-storage/0.30.0)<br><span data-ttu-id="8881f-165">(Ejecute: `pip install -v azure-storage==0.30.0)`</span><span class="sxs-lookup"><span data-stu-id="8881f-165">(Run: `pip install -v azure-storage==0.30.0)`</span></span><br><br><span data-ttu-id="8881f-166">Versión de GitHub:</span><span class="sxs-lookup"><span data-stu-id="8881f-166">GitHub release:</span></span><br> [<span data-ttu-id="8881f-167">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span><span class="sxs-lookup"><span data-stu-id="8881f-167">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span></span>](https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0)|<span data-ttu-id="8881f-168">Declaración de instancia de servicio</span><span class="sxs-lookup"><span data-stu-id="8881f-168">Service instance declaration</span></span>|
|<span data-ttu-id="8881f-169">Ruby</span><span class="sxs-lookup"><span data-stu-id="8881f-169">Ruby</span></span>|<span data-ttu-id="8881f-170">0.12.1</span><span class="sxs-lookup"><span data-stu-id="8881f-170">0.12.1</span></span><br><span data-ttu-id="8881f-171">Vista previa</span><span class="sxs-lookup"><span data-stu-id="8881f-171">Preview</span></span>|<span data-ttu-id="8881f-172">Paquete de RubyGems:</span><span class="sxs-lookup"><span data-stu-id="8881f-172">RubyGems package:</span></span><br> [<span data-ttu-id="8881f-173">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span><span class="sxs-lookup"><span data-stu-id="8881f-173">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span></span>](https://rubygems.org/gems/azure-storage/versions/0.12.1.preview)<br><br><span data-ttu-id="8881f-174">Versión de GitHub:</span><span class="sxs-lookup"><span data-stu-id="8881f-174">GitHub release:</span></span><br> [<span data-ttu-id="8881f-175">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span><span class="sxs-lookup"><span data-stu-id="8881f-175">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span></span>](https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1)|<span data-ttu-id="8881f-176">Configuración de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="8881f-176">Connection string setup</span></span>|

> [!NOTE]
> <span data-ttu-id="8881f-177">Detalles de PHP</span><span class="sxs-lookup"><span data-stu-id="8881f-177">PHP details</span></span><br><br>
><span data-ttu-id="8881f-178">Instalación mediante Composer:</span><span class="sxs-lookup"><span data-stu-id="8881f-178">To install via Composer:</span></span>
>1. <span data-ttu-id="8881f-179">Cree un archivo denominado `composer.json` en la raíz del proyecto con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="8881f-179">Create a file named `composer.json` in the root of the project with following code:</span></span><br>
>
>   ```
>   {
>       "require":{
>           "Microsoft/azure-storage":"0.15.0"
>        }
>    }
>   ```
>
>2. <span data-ttu-id="8881f-180">Descargue el archivo [composer.phar](http://getcomposer.org/composer.phar) en la raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="8881f-180">Download [composer.phar](http://getcomposer.org/composer.phar) into the project root.</span></span>
>3. <span data-ttu-id="8881f-181">Ejecute `php composer.phar install`.</span><span class="sxs-lookup"><span data-stu-id="8881f-181">Run: `php composer.phar install`.</span></span>
>


## <a name="endpoint-declaration"></a><span data-ttu-id="8881f-182">Declaración de punto de conexión</span><span class="sxs-lookup"><span data-stu-id="8881f-182">Endpoint declaration</span></span>
<span data-ttu-id="8881f-183">Un punto de conexión de Azure Stack incluye dos partes: el nombre de una región y el dominio de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8881f-183">An Azure Stack endpoint includes two parts: the name of a region and the Azure Stack domain.</span></span>
<span data-ttu-id="8881f-184">En Azure Stack Development Kit, el punto de conexión predeterminado es **local.azurestack.external**.</span><span class="sxs-lookup"><span data-stu-id="8881f-184">In the Azure Stack Development Kit, the default endpoint is **local.azurestack.external**.</span></span>
<span data-ttu-id="8881f-185">Si no está seguro de cuál es su punto de conexión, póngase en contacto con el administrador de la nube.</span><span class="sxs-lookup"><span data-stu-id="8881f-185">Contact your cloud administrator if you’re not sure about your endpoint.</span></span>

## <a name="examples"></a><span data-ttu-id="8881f-186">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="8881f-186">Examples</span></span>


### <a name="net"></a><span data-ttu-id="8881f-187">.NET</span><span class="sxs-lookup"><span data-stu-id="8881f-187">.NET</span></span>

<span data-ttu-id="8881f-188">Para Azure Stack, el sufijo del punto de conexión se especifica en el archivo app.config:</span><span class="sxs-lookup"><span data-stu-id="8881f-188">For Azure Stack, the endpoint suffix is specified in the app.config file:</span></span>

```
<add key="StorageConnectionString" 
value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;
EndpointSuffix=local.azurestack.external;" />
```
### <a name="java"></a><span data-ttu-id="8881f-189">Java</span><span class="sxs-lookup"><span data-stu-id="8881f-189">Java</span></span>

<span data-ttu-id="8881f-190">Para Azure Stack, el sufijo del punto de conexión se especifica en la configuración de la cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="8881f-190">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key;" +
    "EndpointSuffix=local.azurestack.external";
```

### <a name="nodejs"></a><span data-ttu-id="8881f-191">Node.js</span><span class="sxs-lookup"><span data-stu-id="8881f-191">Node.js</span></span>

<span data-ttu-id="8881f-192">Para Azure Stack, el sufijo del punto de conexión se especifica en la instancia de la declaración:</span><span class="sxs-lookup"><span data-stu-id="8881f-192">For Azure Stack, the endpoint suffix is specified in the declaration instance:</span></span>

```
var blobSvc = azure.createBlobService('myaccount', 'mykey',
'myaccount.blob.local.azurestack.external');
```
### <a name="c"></a><span data-ttu-id="8881f-193">C++</span><span class="sxs-lookup"><span data-stu-id="8881f-193">C++</span></span>

<span data-ttu-id="8881f-194">Para Azure Stack, el sufijo del punto de conexión se especifica en la configuración de la cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="8881f-194">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;
AccountName=your_storage_account;
AccountKey=your_storage_account_key;
EndpointSuffix=local.azurestack.external"));
```

### <a name="php"></a><span data-ttu-id="8881f-195">PHP</span><span class="sxs-lookup"><span data-stu-id="8881f-195">PHP</span></span>

<span data-ttu-id="8881f-196">Para Azure Stack, el sufijo del punto de conexión se especifica en la configuración de la cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="8881f-196">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
$connectionString = 'BlobEndpoint=http://<storage account name>.blob.local.azurestack.external/;
QueueEndpoint=http:// <storage account name>.queue.local.azurestack.external/;
TableEndpoint=http:// <storage account name>.table.local.azurestack.external/;
AccountName=<storage account name>;AccountKey=<storage account key>'
```

### <a name="python"></a><span data-ttu-id="8881f-197">Python</span><span class="sxs-lookup"><span data-stu-id="8881f-197">Python</span></span>

<span data-ttu-id="8881f-198">Para Azure Stack, el sufijo del punto de conexión se especifica en la instancia de la declaración:</span><span class="sxs-lookup"><span data-stu-id="8881f-198">For Azure Stack, the endpoint suffix is specified in the declaration instance:</span></span>

```
block_blob_service = BlockBlobService(account_name='myaccount',
account_key='mykey',
endpoint_suffix='local.azurestack.external')
```
### <a name="ruby"></a><span data-ttu-id="8881f-199">Ruby</span><span class="sxs-lookup"><span data-stu-id="8881f-199">Ruby</span></span>

<span data-ttu-id="8881f-200">Para Azure Stack, el sufijo del punto de conexión se especifica en la configuración de la cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="8881f-200">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
set
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;
AccountName=myaccount;
AccountKey=mykey;
EndpointSuffix=local.azurestack.external
```

## <a name="blob-storage"></a><span data-ttu-id="8881f-201">Almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="8881f-201">Blob storage</span></span>

<span data-ttu-id="8881f-202">Los siguientes tutoriales de Azure Blob Storage son aplicables a Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8881f-202">The following Azure Blob storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="8881f-203">Tenga en cuenta los requisitos específicos de los sufijos de punto de conexión de Azure Stack que se describen en la sección de [ejemplos](#examples) anterior.</span><span class="sxs-lookup"><span data-stu-id="8881f-203">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="8881f-204">Introducción al Almacenamiento de blobs de Azure mediante .NET</span><span class="sxs-lookup"><span data-stu-id="8881f-204">Get started with Azure Blob storage using .NET</span></span>](../../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="8881f-205">Uso de Blob Storage en Java</span><span class="sxs-lookup"><span data-stu-id="8881f-205">How to use Blob storage from Java</span></span>](../../storage/blobs/storage-java-how-to-use-blob-storage.md)
* <span data-ttu-id="8881f-206">[Cómo usar Blob Storage desde Node.js]../../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)</span><span class="sxs-lookup"><span data-stu-id="8881f-206">[How to use Blob storage from Node.js]../../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)</span></span>
* [<span data-ttu-id="8881f-207">Uso del almacenamiento de blobs en C++</span><span class="sxs-lookup"><span data-stu-id="8881f-207">How to use Blob storage from C++</span></span>](../../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="8881f-208">Uso del almacenamiento de blobs de PHP</span><span class="sxs-lookup"><span data-stu-id="8881f-208">How to use Blob storage from PHP</span></span>](../../storage/blobs/storage-php-how-to-use-blobs.md)
* [<span data-ttu-id="8881f-209">Uso de Azure Blob Storage desde Python</span><span class="sxs-lookup"><span data-stu-id="8881f-209">How to use Azure Blob storage from Python</span></span>](../../storage/blobs/storage-python-how-to-use-blob-storage.md)
* [<span data-ttu-id="8881f-210">Uso de Blob Storage en Ruby</span><span class="sxs-lookup"><span data-stu-id="8881f-210">How to use Blob storage from Ruby</span></span>](../../storage/blobs/storage-ruby-how-to-use-blob-storage.md)

## <a name="queue-storage"></a><span data-ttu-id="8881f-211">Queue Storage</span><span class="sxs-lookup"><span data-stu-id="8881f-211">Queue storage</span></span>

<span data-ttu-id="8881f-212">Los siguientes tutoriales de Azure Queue Storage son aplicables a Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8881f-212">The following Azure Queue storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="8881f-213">Tenga en cuenta los requisitos específicos de los sufijos de punto de conexión de Azure Stack que se describen en la sección de [ejemplos](#examples) anterior.</span><span class="sxs-lookup"><span data-stu-id="8881f-213">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="8881f-214">Introducción a Azure Queue Storage mediante .NET</span><span class="sxs-lookup"><span data-stu-id="8881f-214">Get started with Azure Queue storage using .NET</span></span>](../../storage/queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="8881f-215">Uso de Queue Storage en Java</span><span class="sxs-lookup"><span data-stu-id="8881f-215">How to use Queue storage from Java</span></span>](../../storage/queues/storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="8881f-216">Uso del almacenamiento de colas de Node.js</span><span class="sxs-lookup"><span data-stu-id="8881f-216">How to use Queue storage from Node.js</span></span>](../../storage/queues/storage-nodejs-how-to-use-queues.md)
* [<span data-ttu-id="8881f-217">Uso del almacenamiento de colas en C++</span><span class="sxs-lookup"><span data-stu-id="8881f-217">How to use Queue storage from C++</span></span>](../../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="8881f-218">Uso del almacenamiento de colas de PHP</span><span class="sxs-lookup"><span data-stu-id="8881f-218">How to use Queue storage from PHP</span></span>](../../storage/queues/storage-php-how-to-use-queues.md)
* [<span data-ttu-id="8881f-219">Uso de Queue Storage en Python</span><span class="sxs-lookup"><span data-stu-id="8881f-219">How to use Queue storage from Python</span></span>](../../storage/queues/storage-python-how-to-use-queue-storage.md)
* [<span data-ttu-id="8881f-220">Uso del almacenamiento de colas de Ruby</span><span class="sxs-lookup"><span data-stu-id="8881f-220">How to use Queue storage from Ruby</span></span>](../../storage/queues/storage-ruby-how-to-use-queue-storage.md)


## <a name="table-storage"></a><span data-ttu-id="8881f-221">Almacenamiento de tablas</span><span class="sxs-lookup"><span data-stu-id="8881f-221">Table storage</span></span>

<span data-ttu-id="8881f-222">Los siguientes tutoriales de Azure Table Storage son aplicables a Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8881f-222">The following Azure Table storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="8881f-223">Tenga en cuenta los requisitos específicos de los sufijos de punto de conexión de Azure Stack que se describen en la sección de [ejemplos](#examples) anterior.</span><span class="sxs-lookup"><span data-stu-id="8881f-223">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="8881f-224">Introducción a Azure Table Storage mediante .NET</span><span class="sxs-lookup"><span data-stu-id="8881f-224">Get started with Azure Table storage using .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="8881f-225">Uso de Table Storage en Java</span><span class="sxs-lookup"><span data-stu-id="8881f-225">How to use Table storage from Java</span></span>](../../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="8881f-226">Uso de Azure Table Storage en Node.js</span><span class="sxs-lookup"><span data-stu-id="8881f-226">How to use Azure Table storage from Node.js</span></span>](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [<span data-ttu-id="8881f-227">Uso de Table Storage desde C++</span><span class="sxs-lookup"><span data-stu-id="8881f-227">How to use Table storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="8881f-228">Uso de Table Storage en PHP</span><span class="sxs-lookup"><span data-stu-id="8881f-228">How to use Table storage from PHP</span></span>](../../cosmos-db/table-storage-how-to-use-php.md)
* [<span data-ttu-id="8881f-229">Uso de Table Storage en Python</span><span class="sxs-lookup"><span data-stu-id="8881f-229">How to use Table storage in Python</span></span>](../../cosmos-db/table-storage-how-to-use-python.md)
* [<span data-ttu-id="8881f-230">Uso de Table Storage en Ruby</span><span class="sxs-lookup"><span data-stu-id="8881f-230">How to use Table storage from Ruby</span></span>](../../cosmos-db/table-storage-how-to-use-ruby.md)

## <a name="next-steps"></a><span data-ttu-id="8881f-231">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8881f-231">Next steps</span></span>

* [<span data-ttu-id="8881f-232">Introducción a Almacenamiento de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8881f-232">Introduction to Microsoft Azure Storage</span></span>](../../storage/common/storage-introduction.md)