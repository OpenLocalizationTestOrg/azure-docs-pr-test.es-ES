---
title: "aaaConfigure una cadena de conexión para el almacenamiento de Azure | Documentos de Microsoft"
description: "Configure una cadena de conexión para una cuenta de Azure Storage. Una cadena de conexión contiene información de hello necesarios tooauthenticate tener acceso a cuenta de almacenamiento de tooa desde la aplicación en tiempo de ejecución."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: 80c38a6f8f0d4f06b99e7c487647b984e01d1772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-storage-connection-strings"></a><span data-ttu-id="afcc1-104">Configuración de las cadenas de conexión de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="afcc1-104">Configure Azure Storage connection strings</span></span>

<span data-ttu-id="afcc1-105">Una cadena de conexión incluye información de autenticación de hello necesaria para los datos de tooaccess de aplicación de una cuenta de almacenamiento de Azure en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="afcc1-105">A connection string includes hello authentication information required for your application tooaccess data in an Azure Storage account at runtime.</span></span> <span data-ttu-id="afcc1-106">Las cadenas de conexión se pueden configurar para:</span><span class="sxs-lookup"><span data-stu-id="afcc1-106">You can configure connection strings to:</span></span>

* <span data-ttu-id="afcc1-107">Conectar toohello emulador de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="afcc1-107">Connect toohello Azure storage emulator.</span></span>
* <span data-ttu-id="afcc1-108">Acceder a la cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="afcc1-108">Access a storage account in Azure.</span></span>
* <span data-ttu-id="afcc1-109">Acceder a recursos especificados en Azure a través de una firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="afcc1-109">Access specified resources in Azure via a shared access signature (SAS).</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a><span data-ttu-id="afcc1-110">Almacenamiento de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="afcc1-110">Storing your connection string</span></span>
<span data-ttu-id="afcc1-111">La aplicación necesita la cadena de conexión de hello tooaccess en tiempo de ejecución tooauthenticate las solicitudes realizadas tooAzure almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="afcc1-111">Your application needs tooaccess hello connection string at runtime tooauthenticate requests made tooAzure Storage.</span></span> <span data-ttu-id="afcc1-112">Tiene varias opciones para almacenar una cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="afcc1-112">You have several options for storing your connection string:</span></span>

* <span data-ttu-id="afcc1-113">Una aplicación en ejecución en el escritorio de Hola o en un dispositivo puede almacenar la cadena de conexión de hello en un **app.config** o **web.config** archivo.</span><span class="sxs-lookup"><span data-stu-id="afcc1-113">An application running on hello desktop or on a device can store hello connection string in an **app.config** or **web.config** file.</span></span> <span data-ttu-id="afcc1-114">Agregar toohello de cadena de conexión de hello **AppSettings** sección en estos archivos.</span><span class="sxs-lookup"><span data-stu-id="afcc1-114">Add hello connection string toohello **AppSettings** section in these files.</span></span>
* <span data-ttu-id="afcc1-115">Una aplicación que se ejecuta en un servicio de nube de Azure puede almacenar la cadena de conexión de Hola Hola [archivo de esquema (.cscfg) de configuración de servicio de Azure](https://msdn.microsoft.com/library/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="afcc1-115">An application running in an Azure cloud service can store hello connection string in hello [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx).</span></span> <span data-ttu-id="afcc1-116">Agregar toohello de cadena de conexión de hello **ConfigurationSettings** sección del archivo de configuración de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="afcc1-116">Add hello connection string toohello **ConfigurationSettings** section of hello service configuration file.</span></span>
* <span data-ttu-id="afcc1-117">La cadena de conexión se puede usar directamente en el código.</span><span class="sxs-lookup"><span data-stu-id="afcc1-117">You can use your connection string directly in your code.</span></span> <span data-ttu-id="afcc1-118">Sin embargo, es aconsejable que en la mayoría de los escenarios se recomienda almacenar la cadena de configuración en un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="afcc1-118">However, we recommend that you store your connection string in a configuration file in most scenarios.</span></span>

<span data-ttu-id="afcc1-119">Almacenamiento de la cadena de conexión en un archivo de configuración hace que tooswitch de cadena de conexión tooupdate fácil Hola entre el emulador de almacenamiento de hello y una cuenta de almacenamiento de Azure en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="afcc1-119">Storing your connection string in a configuration file makes it easy tooupdate hello connection string tooswitch between hello storage emulator and an Azure storage account in hello cloud.</span></span> <span data-ttu-id="afcc1-120">Entorno de destino tooyour toopoint de cadena de la conexión de Hola de tooedit bastará.</span><span class="sxs-lookup"><span data-stu-id="afcc1-120">You only need tooedit hello connection string toopoint tooyour target environment.</span></span>

<span data-ttu-id="afcc1-121">Puede usar hello [Administrador de configuración de Microsoft Azure](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess la cadena de conexión en tiempo de ejecución, independientemente de donde se está ejecutando la aplicación.</span><span class="sxs-lookup"><span data-stu-id="afcc1-121">You can use hello [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess your connection string at runtime regardless of where your application is running.</span></span>

## <a name="create-a-connection-string-for-hello-storage-emulator"></a><span data-ttu-id="afcc1-122">Crear una cadena de conexión para el emulador de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="afcc1-122">Create a connection string for hello storage emulator</span></span>
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

<span data-ttu-id="afcc1-123">Para obtener más información acerca del emulador de almacenamiento de hello, consulte [usar el emulador de almacenamiento de Azure de Hola para desarrollo y pruebas](storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="afcc1-123">For more information about hello storage emulator, see [Use hello Azure storage emulator for development and testing](storage-use-emulator.md).</span></span>

## <a name="create-a-connection-string-for-an-azure-storage-account"></a><span data-ttu-id="afcc1-124">Creación de una cadena de conexión para una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="afcc1-124">Create a connection string for an Azure storage account</span></span>
<span data-ttu-id="afcc1-125">toocreate una cadena de conexión para la cuenta de almacenamiento de Azure, dar formato a siguiente Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="afcc1-125">toocreate a connection string for your Azure storage account, use hello following format.</span></span> <span data-ttu-id="afcc1-126">Indicar si desea que tooconnect toohello cuenta de almacenamiento a través de HTTPS (recomendado) o HTTP, reemplace `myAccountName` con el nombre de hello de la cuenta de almacenamiento y reemplace `myAccountKey` con su clave de acceso de cuenta:</span><span class="sxs-lookup"><span data-stu-id="afcc1-126">Indicate whether you want tooconnect toohello storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with hello name of your storage account, and replace `myAccountKey` with your account access key:</span></span>

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

<span data-ttu-id="afcc1-127">Por ejemplo, la cadena de conexión podría ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="afcc1-127">For example, your connection string might look similar to:</span></span>

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

<span data-ttu-id="afcc1-128">Aunque Azure Storage admite HTTP y HTTPS en una cadena de conexión, *se recomienda encarecidamente utilizar HTTPS*.</span><span class="sxs-lookup"><span data-stu-id="afcc1-128">Although Azure Storage supports both HTTP and HTTPS in a connection string, *HTTPS is highly recommended*.</span></span>

> [!TIP]
> <span data-ttu-id="afcc1-129">Puede encontrar cadenas de conexión de la cuenta de almacenamiento en hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="afcc1-129">You can find your storage account's connection strings in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="afcc1-130">Navegue demasiado**configuración** > **las claves de acceso** en cadenas de conexión de la cuenta de almacenamiento menú hoja toosee para las claves de acceso principal y secundaria.</span><span class="sxs-lookup"><span data-stu-id="afcc1-130">Navigate too**SETTINGS** > **Access keys** in your storage account's menu blade toosee connection strings for both primary and secondary access keys.</span></span>
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a><span data-ttu-id="afcc1-131">Creación de una cadena de conexión con una firma de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="afcc1-131">Create a connection string using a shared access signature</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a><span data-ttu-id="afcc1-132">Creación de una cadena de conexión para un punto de conexión de Storage explícito</span><span class="sxs-lookup"><span data-stu-id="afcc1-132">Create a connection string for an explicit storage endpoint</span></span>
<span data-ttu-id="afcc1-133">Puede especificar los extremos de servicio explícito en la cadena de conexión en lugar de usar puntos de conexión de hello predeterminados.</span><span class="sxs-lookup"><span data-stu-id="afcc1-133">You can specify explicit service endpoints in your connection string instead of using hello default endpoints.</span></span> <span data-ttu-id="afcc1-134">toocreate una cadena de conexión que especifica un extremo explícito, especificar extremo de servicio completo de Hola para cada servicio, incluida la especificación del protocolo de hello (HTTPS (recomendado) o HTTP), en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="afcc1-134">toocreate a connection string that specifies an explicit endpoint, specify hello complete service endpoint for each service, including hello protocol specification (HTTPS (recommended) or HTTP), in hello following format:</span></span>

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

<span data-ttu-id="afcc1-135">Un escenario donde puedes toospecify un extremo explícito es cuando se ha asignado su tooa de punto de conexión de almacenamiento de blobs [dominio personalizado](storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="afcc1-135">One scenario where you might wish toospecify an explicit endpoint is when you've mapped your Blob storage endpoint tooa [custom domain](storage-custom-domain-name.md).</span></span> <span data-ttu-id="afcc1-136">En ese caso, puede especificar un punto de conexión personalizado para Blob Storage en la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="afcc1-136">In that case, you can specify your custom endpoint for Blob storage in your connection string.</span></span> <span data-ttu-id="afcc1-137">También puede especificar extremos predeterminados de Hola para hello otros servicios si la aplicación usa.</span><span class="sxs-lookup"><span data-stu-id="afcc1-137">You can optionally specify hello default endpoints for hello other services if your application uses them.</span></span>

<span data-ttu-id="afcc1-138">Este es un ejemplo de una cadena de conexión que especifica un extremo explícito para hello servicio Blob:</span><span class="sxs-lookup"><span data-stu-id="afcc1-138">Here is an example of a connection string that specifies an explicit endpoint for hello Blob service:</span></span>

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="afcc1-139">Este ejemplo especifica los extremos explícitos para todos los servicios, incluido un dominio personalizado para hello servicio Blob:</span><span class="sxs-lookup"><span data-stu-id="afcc1-139">This example specifies explicit endpoints for all services, including a custom domain for hello Blob service:</span></span>

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="afcc1-140">valores de punto de conexión de Hello en una cadena de conexión son solicitudes de Hola de tooconstruct usa servicios de almacenamiento de información de URI toohello y dictan el formato de Hola de los URI que se devolvió el código de tooyour.</span><span class="sxs-lookup"><span data-stu-id="afcc1-140">hello endpoint values in a connection string are used tooconstruct hello request URIs toohello storage services, and dictate hello form of any URIs that are returned tooyour code.</span></span>

<span data-ttu-id="afcc1-141">Si ha asignado un dominio personalizado de almacenamiento extremo tooa y omite ese punto de conexión de una cadena de conexión, no será capaz de toouse esa conexión cadena tooaccess datos en dicho servicio desde el código.</span><span class="sxs-lookup"><span data-stu-id="afcc1-141">If you've mapped a storage endpoint tooa custom domain and omit that endpoint from a connection string, then you will not be able toouse that connection string tooaccess data in that service from your code.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="afcc1-142">Los valores del punto de conexión de servicio de las cadenas de conexión deben ser identificadores URI con el formato correcto, entre los que se incluyen `https://` (recomendado) o `http://`.</span><span class="sxs-lookup"><span data-stu-id="afcc1-142">Service endpoint values in your connection strings must be well-formed URIs, including `https://` (recommended) or `http://`.</span></span> <span data-ttu-id="afcc1-143">Dado que el almacenamiento de Azure todavía no admite HTTPS para dominios personalizados, *debe* especificar `http://` para cualquier extremo URI que señala tooa de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="afcc1-143">Because Azure Storage does not yet support HTTPS for custom domains, you *must* specify `http://` for any endpoint URI that points tooa custom domain.</span></span>
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a><span data-ttu-id="afcc1-144">Creación de una cadena de conexión con el sufijo de un punto de conexión</span><span class="sxs-lookup"><span data-stu-id="afcc1-144">Create a connection string with an endpoint suffix</span></span>
<span data-ttu-id="afcc1-145">toocreate una cadena de conexión para un servicio de almacenamiento en regiones o instancias sin el sufijo de punto de conexión diferente, como para China de Azure o Azure Government, Hola uso siguiendo el formato de cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="afcc1-145">toocreate a connection string for a storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Government, use hello following connection string format.</span></span> <span data-ttu-id="afcc1-146">Indicar si desea que tooconnect toohello cuenta de almacenamiento a través de HTTPS (recomendado) o HTTP, reemplace `myAccountName` con el nombre de saludo de la cuenta de almacenamiento, reemplace `myAccountKey` con su clave de acceso de cuenta y reemplace `mySuffix` con hello URI sufijo:</span><span class="sxs-lookup"><span data-stu-id="afcc1-146">Indicate whether you want tooconnect toohello storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with hello name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with hello URI suffix:</span></span>

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

<span data-ttu-id="afcc1-147">Este es un ejemplo de cadena de conexión para los servicios de Storage en Azure China:</span><span class="sxs-lookup"><span data-stu-id="afcc1-147">Here's an example connection string for storage services in Azure China:</span></span>

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a><span data-ttu-id="afcc1-148">Análisis de una cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="afcc1-148">Parsing a connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a><span data-ttu-id="afcc1-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="afcc1-149">Next steps</span></span>
* [<span data-ttu-id="afcc1-150">Usar el emulador de almacenamiento de Azure de Hola para desarrollo y pruebas</span><span class="sxs-lookup"><span data-stu-id="afcc1-150">Use hello Azure storage emulator for development and testing</span></span>](storage-use-emulator.md)
* [<span data-ttu-id="afcc1-151">Exploradores de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="afcc1-151">Azure Storage explorers</span></span>](storage-explorers.md)
* [<span data-ttu-id="afcc1-152">Uso de Firmas de acceso compartido (SAS)</span><span class="sxs-lookup"><span data-stu-id="afcc1-152">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)

