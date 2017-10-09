---
title: aaaIntegrate una cuenta de almacenamiento de Azure con red CDN de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse contenido de hello red de entrega de contenido (CDN) de Azure toodeliver gran ancho de banda almacenando en memoria caché los blobs del almacenamiento de Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="4d049-103">Integración de una cuenta de una instancia de Azure Storage con la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="4d049-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="4d049-104">CDN puede ser habilitado toocache contenido desde el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="4d049-104">CDN can be enabled toocache content from your Azure storage.</span></span> <span data-ttu-id="4d049-105">Ofrece a los desarrolladores una solución global para entregar contenido con alto ancho de banda almacenando en memoria caché los blobs y el contenido estático de instancias de proceso en nodos físicos emplazados en Estados Unidos de hello, Europa, Asia, Australia y Sudamérica.</span><span class="sxs-lookup"><span data-stu-id="4d049-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in hello United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="4d049-106">Paso 1: Creación de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="4d049-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="4d049-107">Usar hello siguiendo el procedimiento toocreate una nueva cuenta de almacenamiento para una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4d049-107">Use hello following procedure toocreate a new storage account for a Azure subscription.</span></span> <span data-ttu-id="4d049-108">Una cuenta de almacenamiento proporciona acceso a los servicios de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="4d049-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="4d049-109">cuenta de almacenamiento de Hello representa el nivel más alto de hello del espacio de nombres de hello para tener acceso a cada uno de los componentes del servicio de almacenamiento de Azure de hello: servicios, servicios de cola y tabla servicios de blobs.</span><span class="sxs-lookup"><span data-stu-id="4d049-109">hello storage account represents hello highest level of hello namespace for accessing each of hello Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="4d049-110">Para obtener más información, consulte toohello [Introducción tooMicrosoft almacenamiento de Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4d049-110">For more information, refer toohello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="4d049-111">toocreate una cuenta de almacenamiento, debe ser administrador de servicios de Hola o Coadministrador de hello asociado suscripción.</span><span class="sxs-lookup"><span data-stu-id="4d049-111">toocreate a storage account, you must be either hello service administrator or a co-administrator for hello associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="4d049-112">Hay varios métodos que puede usar una cuenta de almacenamiento, incluidos Hola Portal de Azure y Powershell toocreate.</span><span class="sxs-lookup"><span data-stu-id="4d049-112">There are several methods you can use toocreate a storage account, including hello Azure Portal and Powershell.</span></span>  <span data-ttu-id="4d049-113">Para este tutorial, usaremos Hola Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4d049-113">For this tutorial, we'll be using hello Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="4d049-114">**toocreate una cuenta de almacenamiento para una suscripción de Azure**</span><span class="sxs-lookup"><span data-stu-id="4d049-114">**toocreate a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="4d049-115">Inicie sesión en toohello [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4d049-115">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4d049-116">En hello esquina superior izquierda, seleccione **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="4d049-116">In hello upper left corner, select **New**.</span></span> <span data-ttu-id="4d049-117">Hola **New** cuadro de diálogo, seleccione **datos + almacenamiento**, a continuación, haga clic en **cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="4d049-117">In hello **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="4d049-118">Hola **crear cuenta de almacenamiento** aparece hoja.</span><span class="sxs-lookup"><span data-stu-id="4d049-118">hello **Create storage account** blade appears.</span></span>   

    ![Crear cuenta de almacenamiento][create-new-storage-account]  

3. <span data-ttu-id="4d049-120">Hola **nombre** , escriba un nombre de subdominio.</span><span class="sxs-lookup"><span data-stu-id="4d049-120">In hello **Name** field, type a subdomain name.</span></span> <span data-ttu-id="4d049-121">Esta entrada puede contener de 3 a 24 letras minúsculas y números.</span><span class="sxs-lookup"><span data-stu-id="4d049-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="4d049-122">Este valor se convierte en el nombre de host de hello en hello URI que se utiliza para redirigir recursos de Blob, cola o tabla para la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d049-122">This value becomes hello host name within hello URI that is used to address Blob, Queue, or Table resources for hello subscription.</span></span> <span data-ttu-id="4d049-123">Para resolver un recurso de contenedor en hello servicio Blob, usaría un URI en hello siguiendo el formato, donde  *&lt;StorageAccountLabel&gt;*  se refiere toohello un valor que escribió en **escriba una dirección URL**:</span><span class="sxs-lookup"><span data-stu-id="4d049-123">To address a container resource in hello Blob service, you would use a URI in hello following format, where *&lt;StorageAccountLabel&gt;* refers toohello value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="4d049-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span><span class="sxs-lookup"><span data-stu-id="4d049-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="4d049-125">**Importante:** Hola subdominio de dirección URL etiqueta forms Hola de cuenta de almacenamiento de hello URI y debe ser único entre todos los servicios hospedados en Azure.</span><span class="sxs-lookup"><span data-stu-id="4d049-125">**Important:** hello URL label forms hello subdomain of hello storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="4d049-126">Este valor también se utiliza como nombre de Hola de esta cuenta de almacenamiento en el portal de hello, o al tener acceso mediante programación a esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="4d049-126">This value is also used as hello name of this storage account in hello portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="4d049-127">Deje los valores predeterminados de Hola para **modelo de implementación**, **cuenta kind**, **rendimiento**, y **replicación**.</span><span class="sxs-lookup"><span data-stu-id="4d049-127">Leave hello defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="4d049-128">Seleccione hello **suscripción** que se utilizará la cuenta de almacenamiento de hello con.</span><span class="sxs-lookup"><span data-stu-id="4d049-128">Select hello **Subscription** that hello storage account will be used with.</span></span>
6. <span data-ttu-id="4d049-129">Seleccione o cree un **grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="4d049-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="4d049-130">Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="4d049-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="4d049-131">Seleccione la ubicación para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4d049-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="4d049-132">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4d049-132">Click **Create**.</span></span> <span data-ttu-id="4d049-133">proceso de Hola de creación de cuenta de almacenamiento de hello puede tardar varios toocomplete minutos.</span><span class="sxs-lookup"><span data-stu-id="4d049-133">hello process of creating hello storage account might take several minutes toocomplete.</span></span>

## <a name="step-2-enable-cdn-for-hello-storage-account"></a><span data-ttu-id="4d049-134">Paso 2: Habilitar la red CDN Hola cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="4d049-134">Step 2: Enable CDN for hello storage account</span></span>

<span data-ttu-id="4d049-135">Con la integración más reciente de hello, ahora puede habilitar CDN para la cuenta de almacenamiento sin salir de la extensión de portal de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4d049-135">With hello newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="4d049-136">Seleccione la cuenta de almacenamiento de hello, buscar "red CDN" o desplácese hacia abajo del menú de navegación izquierdo de hello, haga clic en "CDN de Azure".</span><span class="sxs-lookup"><span data-stu-id="4d049-136">Select hello storage account, search "CDN" or scroll down from hello left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="4d049-137">Hola **CDN de Azure** aparece hoja.</span><span class="sxs-lookup"><span data-stu-id="4d049-137">hello **Azure CDN** blade appears.</span></span>

    ![cdn enable navigation][cdn-enable-navigation]
    
2. <span data-ttu-id="4d049-139">Crear un nuevo extremo especificando información Hola necesario</span><span class="sxs-lookup"><span data-stu-id="4d049-139">Create a new endpoint by entering hello required information</span></span>
    - <span data-ttu-id="4d049-140">**Perfil de CDN**: puede crear un perfil o usar uno existente.</span><span class="sxs-lookup"><span data-stu-id="4d049-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="4d049-141">**Nivel de precios**: solo necesita tooselect un precio de nivel si crea un nuevo perfil CDN.</span><span class="sxs-lookup"><span data-stu-id="4d049-141">**Pricing tier**: You only need tooselect a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="4d049-142">**Nombre del punto de conexión de CDN**: escriba un nombre de punto de conexión de su elección.</span><span class="sxs-lookup"><span data-stu-id="4d049-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="4d049-143">extremo de red CDN Hola creado utiliza Hola nombre de host de la cuenta de almacenamiento como origen de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4d049-143">hello created CDN endpoint uses hello hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="4d049-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span><span class="sxs-lookup"><span data-stu-id="4d049-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="4d049-145">Después de su creación, nuevo punto de conexión de Hola se mostrará en la lista de extremos de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="4d049-145">After creation, hello new endpoint will show up in hello endpoint list above.</span></span>

    ![cdn storage new endpoint][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="4d049-147">También puede ir tooAzure CDN extensión tooenable CDN. [Tutorial](#Tutorial-cdn-create-profile).</span><span class="sxs-lookup"><span data-stu-id="4d049-147">You can also go tooAzure CDN extension tooenable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="4d049-148">Paso 3: Habilitación de características adicionales de CDN</span><span class="sxs-lookup"><span data-stu-id="4d049-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="4d049-149">En la hoja de "Red CDN de Azure" de la cuenta de almacenamiento, haga clic en extremo de red CDN Hola de hoja de configuración de red CDN de hello lista tooopen.</span><span class="sxs-lookup"><span data-stu-id="4d049-149">From storage account "Azure CDN" blade, click hello CDN endpoint from hello list tooopen CDN configuration blade.</span></span> <span data-ttu-id="4d049-150">Puede habilitar características adicionales de CDN para la entrega como, por ejemplo, la compresión, la cadena de consulta o el filtrado geográfico.</span><span class="sxs-lookup"><span data-stu-id="4d049-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="4d049-151">También puede agregar el extremo de red CDN de tooyour de asignación de dominio personalizado y habilitar HTTPS de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="4d049-151">You can also add custom domain mapping tooyour CDN endpoint and enable custom domain HTTPS.</span></span>
    
![cdn storage cdn configuration][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="4d049-153">Paso 4: Acceso a su contenido de la red CDN</span><span class="sxs-lookup"><span data-stu-id="4d049-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="4d049-154">tooaccess almacenado en caché contenido en la red CDN Hola, use Hola dirección URL de CDN proporcionado en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d049-154">tooaccess cached content on hello CDN, use hello CDN URL provided in hello portal.</span></span> <span data-ttu-id="4d049-155">dirección de Hola para un blob almacenado en caché será similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="4d049-155">hello address for a cached blob will be similar toohello following:</span></span>

<span data-ttu-id="4d049-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span><span class="sxs-lookup"><span data-stu-id="4d049-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="4d049-157">Una vez que habilite la cuenta de almacenamiento de tooa de acceso de red CDN, todos los objetos disponibles públicamente son aptos para su almacenamiento en caché de perimetral de red CDN.</span><span class="sxs-lookup"><span data-stu-id="4d049-157">Once you enable CDN access tooa storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="4d049-158">Si modifica un objeto que está almacenado actualmente en la red CDN Hola, contenido nuevo de hello no estará disponible a través de la red CDN Hola hasta que la red CDN Hola actualiza su contenido cuando expire el período de tiempo de vida de Hola almacenado en memoria caché contenido.</span><span class="sxs-lookup"><span data-stu-id="4d049-158">If you modify an object that is currently cached in hello CDN, hello new content will not be available via hello CDN until hello CDN refreshes its content when hello cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a><span data-ttu-id="4d049-159">Paso 5: Quitar contenido de CDN Hola</span><span class="sxs-lookup"><span data-stu-id="4d049-159">Step 5: Remove content from hello CDN</span></span>
<span data-ttu-id="4d049-160">Si ya no desea toocache un objeto en hello red de entrega de contenido (CDN) de Azure, puede realizar una de hello pasos:</span><span class="sxs-lookup"><span data-stu-id="4d049-160">If you no longer wish toocache an object in hello Azure Content Delivery Network (CDN), you can take one of hello following steps:</span></span>

* <span data-ttu-id="4d049-161">Puede hacer Hola privados de contenedor en lugar de público.</span><span class="sxs-lookup"><span data-stu-id="4d049-161">You can make hello container private instead of public.</span></span> <span data-ttu-id="4d049-162">Vea [administrar toocontainers de acceso de lectura anónimo y los blobs](../storage/blobs/storage-manage-access-to-resources.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="4d049-162">See [Manage anonymous read access toocontainers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="4d049-163">Puede deshabilitar o eliminar el extremo de red CDN Hola mediante Hola Portal de administración.</span><span class="sxs-lookup"><span data-stu-id="4d049-163">You can disable or delete hello CDN endpoint using hello Management Portal.</span></span>
* <span data-ttu-id="4d049-164">Puede modificar su toorequests servicio hospedado responden más de toono para el objeto de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d049-164">You can modify your hosted service toono longer respond toorequests for hello object.</span></span>

<span data-ttu-id="4d049-165">Un objeto que ya está almacenado en la red CDN Hola permanecerá en caché hasta que expire el período de período de vida de hello para el objeto de Hola o hasta que el punto de conexión de Hola se purga.</span><span class="sxs-lookup"><span data-stu-id="4d049-165">An object already cached in hello CDN will remain cached until hello time-to-live period for hello object expires or until hello endpoint is purged.</span></span> <span data-ttu-id="4d049-166">Cuando expire el período de tiempo de vida de hello, CDN Hola comprobará toosee si el extremo de red CDN Hola sigue siendo válido y el objeto de hello todavía accesible de forma anónima.</span><span class="sxs-lookup"><span data-stu-id="4d049-166">When hello time-to-live period expires, hello CDN will check toosee whether hello CDN endpoint is still valid and hello object still anonymously accessible.</span></span> <span data-ttu-id="4d049-167">Si no es así, a continuación, objeto de Hola se ya no se almacenarán en caché.</span><span class="sxs-lookup"><span data-stu-id="4d049-167">If it is not, then hello object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4d049-168">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4d049-168">Additional resources</span></span>
* [<span data-ttu-id="4d049-169">¿Cómo tooMap CDN contenido tooa dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="4d049-169">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="4d049-170">Habilitar HTTPS para el dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="4d049-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
