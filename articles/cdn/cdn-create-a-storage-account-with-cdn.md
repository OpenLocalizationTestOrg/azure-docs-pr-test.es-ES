---
title: "Integración de una cuenta de una instancia de Azure Storage con la red CDN de Azure | Microsoft Docs"
description: "Aprenda a usar la red de entrega de contenido (CDN) de Azure para ofrecer contenido con un ancho de banda alto mediante el almacenamiento en caché de blobs de Almacenamiento de Azure."
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
ms.openlocfilehash: 511076935d06ed0908341044e37069e74530be49
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="79bb5-103">Integración de una cuenta de una instancia de Azure Storage con la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="79bb5-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="79bb5-104">CDN puede habilitarse para almacenar el contenido de la caché en Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="79bb5-104">CDN can be enabled to cache content from your Azure storage.</span></span> <span data-ttu-id="79bb5-105">Ofrece a los desarrolladores una solución global de entrega de contenido con alto ancho de banda; para ello, almacena en memoria caché los blobs y los contenidos estáticos de las instancias de proceso en nodos físicos ubicados en Estados Unidos, Europa, Asia, Australia y Sudamérica.</span><span class="sxs-lookup"><span data-stu-id="79bb5-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in the United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="79bb5-106">Paso 1: Creación de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="79bb5-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="79bb5-107">Use el siguiente procedimiento para crear una nueva cuenta de almacenamiento para una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="79bb5-107">Use the following procedure to create a new storage account for a Azure subscription.</span></span> <span data-ttu-id="79bb5-108">Una cuenta de almacenamiento proporciona acceso a los servicios de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="79bb5-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="79bb5-109">La cuenta de almacenamiento representa el máximo nivel de espacio de nombres para tener acceso a todos los componentes del servicio de almacenamiento de Azure: servicios BLOB, servicios Cola y servicios Tabla.</span><span class="sxs-lookup"><span data-stu-id="79bb5-109">The storage account represents the highest level of the namespace for accessing each of the Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="79bb5-110">Para más información, consulte [Introducción al Almacenamiento de Microsoft Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="79bb5-110">For more information, refer to the [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="79bb5-111">Para crear una cuenta de almacenamiento, debe ser administrador del servicio o coadministrador de la suscripción correspondiente.</span><span class="sxs-lookup"><span data-stu-id="79bb5-111">To create a storage account, you must be either the service administrator or a co-administrator for the associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="79bb5-112">Hay varios métodos que puede usar para crear una cuenta de almacenamiento, incluido el Portal de Azure y Powershell.</span><span class="sxs-lookup"><span data-stu-id="79bb5-112">There are several methods you can use to create a storage account, including the Azure Portal and Powershell.</span></span>  <span data-ttu-id="79bb5-113">Para este tutorial, usaremos el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="79bb5-113">For this tutorial, we'll be using the Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="79bb5-114">**Para crear una cuenta de almacenamiento para una suscripción de Azure**</span><span class="sxs-lookup"><span data-stu-id="79bb5-114">**To create a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="79bb5-115">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="79bb5-115">Sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="79bb5-116">En la esquina superior izquierda, seleccione **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="79bb5-116">In the upper left corner, select **New**.</span></span> <span data-ttu-id="79bb5-117">En el cuadro de diálogo **Nuevo**, seleccione **Datos + Almacenamiento** y haga clic en **Cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="79bb5-117">In the **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="79bb5-118">Aparece la hoja **Crear cuenta de almacenamiento** .</span><span class="sxs-lookup"><span data-stu-id="79bb5-118">The **Create storage account** blade appears.</span></span>   

    ![Crear cuenta de almacenamiento][create-new-storage-account]  

3. <span data-ttu-id="79bb5-120">En el campo **Nombre** , escriba un nombre de subdominio.</span><span class="sxs-lookup"><span data-stu-id="79bb5-120">In the **Name** field, type a subdomain name.</span></span> <span data-ttu-id="79bb5-121">Esta entrada puede contener de 3 a 24 letras minúsculas y números.</span><span class="sxs-lookup"><span data-stu-id="79bb5-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="79bb5-122">Este valor se convierte en el nombre del host dentro del URI que se ha usado para direccionar los recursos Blob, Cola o Tabla de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="79bb5-122">This value becomes the host name within the URI that is used to address Blob, Queue, or Table resources for the subscription.</span></span> <span data-ttu-id="79bb5-123">Para dirigir un recurso contenedor en Blob service, debería usar un URI con el siguiente formato, en el que *&lt;StorageAccountLabel&gt;* hace referencia al valor que escribió en **Escriba una dirección URL**:</span><span class="sxs-lookup"><span data-stu-id="79bb5-123">To address a container resource in the Blob service, you would use a URI in the following format, where *&lt;StorageAccountLabel&gt;* refers to the value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="79bb5-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span><span class="sxs-lookup"><span data-stu-id="79bb5-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="79bb5-125">**Importante**: La etiqueta de URL forma el subdominio del URI de la cuenta de almacenamiento y debe ser única en todos los servicios hospedados en Azure.</span><span class="sxs-lookup"><span data-stu-id="79bb5-125">**Important:** The URL label forms the subdomain of the storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="79bb5-126">Este valor también se utiliza como nombre de esta cuenta de almacenamiento en el portal o en el acceso a esta cuenta mediante programación.</span><span class="sxs-lookup"><span data-stu-id="79bb5-126">This value is also used as the name of this storage account in the portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="79bb5-127">Deje los valores predeterminados de **Modelo de implementación**, **Tipo de cuenta**, **Rendimiento** y **Replicación**.</span><span class="sxs-lookup"><span data-stu-id="79bb5-127">Leave the defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="79bb5-128">Seleccione la **Suscripción** con la que se usará la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="79bb5-128">Select the **Subscription** that the storage account will be used with.</span></span>
6. <span data-ttu-id="79bb5-129">Seleccione o cree un **grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="79bb5-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="79bb5-130">Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="79bb5-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="79bb5-131">Seleccione la ubicación para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="79bb5-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="79bb5-132">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="79bb5-132">Click **Create**.</span></span> <span data-ttu-id="79bb5-133">El proceso de creación de la cuenta de almacenamiento podría tardar varios minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="79bb5-133">The process of creating the storage account might take several minutes to complete.</span></span>

## <a name="step-2-enable-cdn-for-the-storage-account"></a><span data-ttu-id="79bb5-134">Paso 2: Habilitación de la red CDN para la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="79bb5-134">Step 2: Enable CDN for the storage account</span></span>

<span data-ttu-id="79bb5-135">Con la integración más reciente, ahora puede habilitar la red CDN para la cuenta de almacenamiento sin salir de la extensión del portal de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="79bb5-135">With the newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="79bb5-136">Seleccione la cuenta de almacenamiento, busque "CDN" o desplácese hacia abajo en el menú de navegación izquierdo y haga clic en "CDN de Azure".</span><span class="sxs-lookup"><span data-stu-id="79bb5-136">Select the storage account, search "CDN" or scroll down from the left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="79bb5-137">Aparece la hoja **CDN de Azure**.</span><span class="sxs-lookup"><span data-stu-id="79bb5-137">The **Azure CDN** blade appears.</span></span>

    ![cdn enable navigation][cdn-enable-navigation]
    
2. <span data-ttu-id="79bb5-139">Cree un nuevo punto de conexión. Para ello escriba la información necesaria</span><span class="sxs-lookup"><span data-stu-id="79bb5-139">Create a new endpoint by entering the required information</span></span>
    - <span data-ttu-id="79bb5-140">**Perfil de CDN**: puede crear un perfil o usar uno existente.</span><span class="sxs-lookup"><span data-stu-id="79bb5-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="79bb5-141">**Plan de tarifa**: si crea un nuevo perfil CDN, bastará con seleccionar un plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="79bb5-141">**Pricing tier**: You only need to select a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="79bb5-142">**Nombre del punto de conexión de CDN**: escriba un nombre de punto de conexión de su elección.</span><span class="sxs-lookup"><span data-stu-id="79bb5-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="79bb5-143">El punto de conexión de CDN creado utilizará el nombre de host de la cuenta de almacenamiento como origen de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="79bb5-143">The created CDN endpoint uses the hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="79bb5-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span><span class="sxs-lookup"><span data-stu-id="79bb5-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="79bb5-145">Después de su creación, se mostrará el nuevo punto de conexión en la lista de puntos de conexión anterior.</span><span class="sxs-lookup"><span data-stu-id="79bb5-145">After creation, the new endpoint will show up in the endpoint list above.</span></span>

    ![cdn storage new endpoint][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="79bb5-147">También puede ir a la extensión de CDN de Azure para habilitar la red CDN. [Tutorial](#Tutorial-cdn-create-profile).</span><span class="sxs-lookup"><span data-stu-id="79bb5-147">You can also go to Azure CDN extension to enable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="79bb5-148">Paso 3: Habilitación de características adicionales de CDN</span><span class="sxs-lookup"><span data-stu-id="79bb5-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="79bb5-149">En la hoja "CDN de Azure" de la cuenta de almacenamiento, haga clic en el punto de conexión de CDN de la lista para abrir la hoja de configuración de CDN.</span><span class="sxs-lookup"><span data-stu-id="79bb5-149">From storage account "Azure CDN" blade, click the CDN endpoint from the list to open CDN configuration blade.</span></span> <span data-ttu-id="79bb5-150">Puede habilitar características adicionales de CDN para la entrega como, por ejemplo, la compresión, la cadena de consulta o el filtrado geográfico.</span><span class="sxs-lookup"><span data-stu-id="79bb5-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="79bb5-151">También puede agregar la asignación de dominios personalizada al punto de conexión de CDN y habilitar HTTPS de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="79bb5-151">You can also add custom domain mapping to your CDN endpoint and enable custom domain HTTPS.</span></span>
    
![cdn storage cdn configuration][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="79bb5-153">Paso 4: Acceso a su contenido de la red CDN</span><span class="sxs-lookup"><span data-stu-id="79bb5-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="79bb5-154">Para obtener acceso al contenido almacenado en la memoria caché de la red CDN, use la URL de la red CDN que se le ha proporcionado en el portal.</span><span class="sxs-lookup"><span data-stu-id="79bb5-154">To access cached content on the CDN, use the CDN URL provided in the portal.</span></span> <span data-ttu-id="79bb5-155">La dirección del blob en caché será similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="79bb5-155">The address for a cached blob will be similar to the following:</span></span>

<span data-ttu-id="79bb5-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span><span class="sxs-lookup"><span data-stu-id="79bb5-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="79bb5-157">Una vez que haya habilitado el acceso de la red CDN a una cuenta de almacenamiento, todos los objetos disponibles de forma pública se pueden almacenar en la memoria caché perimetral de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="79bb5-157">Once you enable CDN access to a storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="79bb5-158">Si modifica un objeto que está almacenado en la memoria caché de la red CDN actualmente, el nuevo contenido no estará disponible a través de la red CDN hasta que la red CDN actualice su contenido al cumplir el período de vida del contenido almacenado en caché.</span><span class="sxs-lookup"><span data-stu-id="79bb5-158">If you modify an object that is currently cached in the CDN, the new content will not be available via the CDN until the CDN refreshes its content when the cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-the-cdn"></a><span data-ttu-id="79bb5-159">Paso 5: Eliminación de su contenido de la red CDN</span><span class="sxs-lookup"><span data-stu-id="79bb5-159">Step 5: Remove content from the CDN</span></span>
<span data-ttu-id="79bb5-160">Si no desea seguir almacenando un objeto en la memoria caché de la Red de entrega de contenido de Azure (CDN), puede realizar uno de los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="79bb5-160">If you no longer wish to cache an object in the Azure Content Delivery Network (CDN), you can take one of the following steps:</span></span>

* <span data-ttu-id="79bb5-161">Puede crear un contenedor privado en vez de público.</span><span class="sxs-lookup"><span data-stu-id="79bb5-161">You can make the container private instead of public.</span></span> <span data-ttu-id="79bb5-162">Vea [Administración del acceso de lectura anónimo a contenedores y blobs](../storage/blobs/storage-manage-access-to-resources.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="79bb5-162">See [Manage anonymous read access to containers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="79bb5-163">Puede deshabilitar o eliminar el punto de conexión de la red CDN con el Portal de administración.</span><span class="sxs-lookup"><span data-stu-id="79bb5-163">You can disable or delete the CDN endpoint using the Management Portal.</span></span>
* <span data-ttu-id="79bb5-164">Puede modificar su servicio hospedado para no seguir respondiendo las solicitudes del objeto.</span><span class="sxs-lookup"><span data-stu-id="79bb5-164">You can modify your hosted service to no longer respond to requests for the object.</span></span>

<span data-ttu-id="79bb5-165">Un objeto que ya está almacenado en la memoria caché de la red CDN permanecerá almacenado en caché hasta que cumpla el período de vida del objeto o hasta que se purgue el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="79bb5-165">An object already cached in the CDN will remain cached until the time-to-live period for the object expires or until the endpoint is purged.</span></span> <span data-ttu-id="79bb5-166">Al cumplir el período de vida, la red CDN comprobará si el punto de conexión de la red CDN sigue siendo válido y si el objeto sigue siendo accesible de forma anónima.</span><span class="sxs-lookup"><span data-stu-id="79bb5-166">When the time-to-live period expires, the CDN will check to see whether the CDN endpoint is still valid and the object still anonymously accessible.</span></span> <span data-ttu-id="79bb5-167">Si no lo es, el objeto dejará de estar almacenado en caché.</span><span class="sxs-lookup"><span data-stu-id="79bb5-167">If it is not, then the object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="79bb5-168">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="79bb5-168">Additional resources</span></span>
* [<span data-ttu-id="79bb5-169">Asignación del contenido de la red CDN a un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="79bb5-169">How to Map CDN Content to a Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="79bb5-170">Habilitar HTTPS para el dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="79bb5-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
