---
title: "Administración de puntos de conexión de streaming con Azure Portal | Microsoft Docs"
description: "En este tema se muestra cómo administrar los puntos de conexión de streaming mediante el Portal de Azure."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 797dced6c3e2525730afa29987259cb9b435ba66
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-streaming-endpoints-with-the-azure-portal"></a><span data-ttu-id="35060-103">Administración de puntos de conexión de streaming con el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="35060-103">Manage streaming endpoints with the Azure portal</span></span>

<span data-ttu-id="35060-104">El tema muestra cómo usar Azure Portal para administrar puntos de conexión de streaming.</span><span class="sxs-lookup"><span data-stu-id="35060-104">This topic shows  how to use the Azure portal to manage streaming endpoints.</span></span> 

>[!NOTE]
><span data-ttu-id="35060-105">No olvide revisar el tema de [Información general](media-services-streaming-endpoints-overview.md).</span><span class="sxs-lookup"><span data-stu-id="35060-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> 

<span data-ttu-id="35060-106">Para obtener información sobre cómo escalar el punto de conexión de streaming, consulte [este](media-services-portal-scale-streaming-endpoints.md) tema.</span><span class="sxs-lookup"><span data-stu-id="35060-106">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="start-managing-streaming-endpoints"></a><span data-ttu-id="35060-107">Inicio de la administración de puntos de conexión de streaming</span><span class="sxs-lookup"><span data-stu-id="35060-107">Start managing streaming endpoints</span></span> 

<span data-ttu-id="35060-108">Para comenzar a administrar puntos de conexión de streaming de su cuenta, haga lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="35060-108">To start managing streaming endpoints for your account, do the following.</span></span>

1. <span data-ttu-id="35060-109">En [Azure Portal](https://portal.azure.com/), seleccione la cuenta de Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="35060-109">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="35060-110">En la hoja **Configuración**, haga clic en **Puntos de conexión de streaming**.</span><span class="sxs-lookup"><span data-stu-id="35060-110">In the **Settings** blade, select **Streaming endpoints**.</span></span>
   
    ![punto de conexión de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> <span data-ttu-id="35060-112">Solo se le cobrará cuando StreamingEndpoint esté en estado en ejecución.</span><span class="sxs-lookup"><span data-stu-id="35060-112">You are only billed when your Streaming Endpoint is in running state.</span></span>

## <a name="adddelete-a-streaming-endpoint"></a><span data-ttu-id="35060-113">Adición o eliminación de puntos de conexión de streaming</span><span class="sxs-lookup"><span data-stu-id="35060-113">Add/delete a streaming endpoint</span></span>

>[!NOTE]
><span data-ttu-id="35060-114">No se puede eliminar el punto de conexión de streaming predeterminado.</span><span class="sxs-lookup"><span data-stu-id="35060-114">The default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="35060-115">Para agregar/quitar el punto de conexión de streaming mediante el Portal de Azure, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="35060-115">To add/delete streaming endpoint using the Azure portal, do the following:</span></span>

1. <span data-ttu-id="35060-116">Para agregar un punto de conexión de streaming, haga clic en **+ Punto de conexión** en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="35060-116">To add a streaming endpoint, click the **+ Endpoint** at the top of the page.</span></span> 

    <span data-ttu-id="35060-117">Conviene tener varios puntos de conexión de streaming si planea tener diferentes redes CDN o una red CDN y acceso directo.</span><span class="sxs-lookup"><span data-stu-id="35060-117">You might want multiple Streaming Endpoints if you plan to have different CDNs or a CDN and direct access.</span></span>

2. <span data-ttu-id="35060-118">Para eliminar un punto de conexión de streaming, haga clic en el botón **Eliminar** .</span><span class="sxs-lookup"><span data-stu-id="35060-118">To delete a streaming endpoint, press **Delete** button.</span></span>      
3. <span data-ttu-id="35060-119">Haga clic en el botón **Iniciar** para iniciar el punto de conexión de streaming.</span><span class="sxs-lookup"><span data-stu-id="35060-119">Click the **Start** button to start the streaming endpoint.</span></span>
   
    ![punto de conexión de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <span data-ttu-id="35060-121"><a id="configure_streaming_endpoints"></a>Configuración del extremo de streaming</span><span class="sxs-lookup"><span data-stu-id="35060-121"><a id="configure_streaming_endpoints"></a>Configuring the Streaming Endpoint</span></span>
<span data-ttu-id="35060-122">Punto de conexión de streaming le permite configurar las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="35060-122">Streaming Endpoint enables you to configure the following properties:</span></span>

* <span data-ttu-id="35060-123">Control de acceso</span><span class="sxs-lookup"><span data-stu-id="35060-123">Access control</span></span>
* <span data-ttu-id="35060-124">Control de caché</span><span class="sxs-lookup"><span data-stu-id="35060-124">Cache control</span></span>
* <span data-ttu-id="35060-125">Directivas de acceso en varios sitios</span><span class="sxs-lookup"><span data-stu-id="35060-125">Cross site access policies</span></span>

<span data-ttu-id="35060-126">Para obtener información detallada acerca de estas propiedades, consulte [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="35060-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="35060-127">Puede configurar el punto de conexión de streaming haciendo lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="35060-127">You can configure streaming endpoint by doing the following:</span></span>

1. <span data-ttu-id="35060-128">Seleccione el punto de conexión de streaming que desea configurar.</span><span class="sxs-lookup"><span data-stu-id="35060-128">Select the streaming endpoint you want to configure.</span></span>
2. <span data-ttu-id="35060-129">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="35060-129">Click **Settings**.</span></span>

<span data-ttu-id="35060-130">Aparecerá una breve descripción de los campos.</span><span class="sxs-lookup"><span data-stu-id="35060-130">A brief description of the fields follows.</span></span>

![extremo de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. <span data-ttu-id="35060-132">Directiva de caché máximo: se usa para configurar la duración de la caché de los recursos entregados a través de este punto de conexión de streaming.</span><span class="sxs-lookup"><span data-stu-id="35060-132">Maximum cache policy: used to configure cache lifetime for assets served through this streaming endpoint.</span></span> <span data-ttu-id="35060-133">Si no se establece ningún valor, se utiliza el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="35060-133">If no value is set, the default is used.</span></span> <span data-ttu-id="35060-134">Los valores predeterminados también pueden definirse directamente en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="35060-134">The default values can also be defined directly in Azure storage.</span></span> <span data-ttu-id="35060-135">Si la red CDN de Azure está habilitada para el punto de conexión de streaming, no debe establecer el valor de la directiva de caché en menos de 600 segundos.</span><span class="sxs-lookup"><span data-stu-id="35060-135">If Azure CDN is enabled for the streaming endpoint, you should not set the cache policy value to less than 600 seconds.</span></span>  
2. <span data-ttu-id="35060-136">Direcciones IP permitidas: especifique las direcciones IP que podrán conectarse al punto de conexión de streaming publicado.</span><span class="sxs-lookup"><span data-stu-id="35060-136">Allowed IP addresses: used to specify IP addresses that would be allowed to connect to the published streaming endpoint.</span></span> <span data-ttu-id="35060-137">Si no se especificaron direcciones IP, cualquier dirección IP se podrá conectar.</span><span class="sxs-lookup"><span data-stu-id="35060-137">If no IP addresses specified, any IP address would be able to connect.</span></span> <span data-ttu-id="35060-138">Las direcciones IP se pueden especificar como una dirección IP única (por ejemplo, 10.0.0.1), un intervalo de IP que usa una dirección IP y una máscara de subred CIDR (por ejemplo, 10.0.0.1/22) o un intervalo de IP que usa una máscara de subred decimal con puntos; por ejemplo, 10.0.0.1(255.255.255.0).</span><span class="sxs-lookup"><span data-stu-id="35060-138">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span></span>
3. <span data-ttu-id="35060-139">Configuración de autenticación del encabezado de firma de Akamai: se utiliza para especificar cómo se configura la solicitud de autenticación de encabezado de firma desde servidores Akamai.</span><span class="sxs-lookup"><span data-stu-id="35060-139">Configuration for Akamai signature header authentication: used to specify how signature header authentication request from Akamai servers is configured.</span></span> <span data-ttu-id="35060-140">La expiración está en formato UTC.</span><span class="sxs-lookup"><span data-stu-id="35060-140">Expiration is in UTC.</span></span>

## <a name="scale-your-premium-streaming-endpoint"></a><span data-ttu-id="35060-141">Escalado del punto de conexión de streaming premium</span><span class="sxs-lookup"><span data-stu-id="35060-141">Scale your Premium streaming endpoint</span></span>

<span data-ttu-id="35060-142">Para obtener más información, consulte [este tema](media-services-portal-scale-streaming-endpoints.md) .</span><span class="sxs-lookup"><span data-stu-id="35060-142">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <span data-ttu-id="35060-143"><a id="enable_cdn"></a>Habilitación de la integración de CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="35060-143"><a id="enable_cdn"></a>Enable Azure CDN integration</span></span>

<span data-ttu-id="35060-144">Cuando se crea una nueva cuenta, la integración de la red CDN de Azure de punto de conexión de streaming está habilitada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="35060-144">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span></span>

<span data-ttu-id="35060-145">Si más adelante desea volver a habilitar o deshabilitar la red CDN, punto de conexión de streaming debe estar en estado **stopped** (detenido).</span><span class="sxs-lookup"><span data-stu-id="35060-145">If you later want to disable/enable the CDN, your streaming endpoint must be in the **stopped** state.</span></span> <span data-ttu-id="35060-146">Es posible que transcurran hasta dos horas hasta que la integración de la red CDN de Azure se habilite y los cambios se activen en todos los POP de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="35060-146">It could take up to 2 hours for the Azure CDN integration to get enabled and for the changes to be active across all the CDN POPs.</span></span> <span data-ttu-id="35060-147">Sin embargo, puede iniciar el punto de conexión de streaming y transmitir sin interrupciones desde ahí y, una vez que la integración esté completa, la transmisión se efectuará desde la red CDN.</span><span class="sxs-lookup"><span data-stu-id="35060-147">However, your can start your streaming endpoint and stream without interruptions from the streaming endpoint and once the integration is complete, the stream will be delivered from the CDN.</span></span> <span data-ttu-id="35060-148">Durante el período de aprovisionamiento, el punto de conexión de streaming estará en estado **starting** (iniciando) y es posible que note una reducción en el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="35060-148">During the provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span></span>

<span data-ttu-id="35060-149">La integración de la red CDN está habilitada en todos los centros de datos de Azure excepto las regiones de China y el Gobierno Federal.</span><span class="sxs-lookup"><span data-stu-id="35060-149">CDN integration is enabled in all the Azure data centers execpt China and Federal Goverment regions.</span></span>

<span data-ttu-id="35060-150">Una vez habilitada, la configuración de **Access Control**, **nombre de host personalizado** y **autenticación de firma de Akamai** se deshabilita.</span><span class="sxs-lookup"><span data-stu-id="35060-150">Once it is enabled, the **Access Control**, **Custom hostname** and **Akamai Signature authentication** configuration gets disabled.</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="35060-151">La integración de Azure Media Services con la red CDN de Azure se implementa en la **red CDN de Azure de Verizon** para puntos de conexión de streaming estándar.</span><span class="sxs-lookup"><span data-stu-id="35060-151">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span></span> <span data-ttu-id="35060-152">Los puntos de conexión de streaming premium pueden configurarse con todos los **proveedores y planes de tarifa de la red CDN de Azure**.</span><span class="sxs-lookup"><span data-stu-id="35060-152">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span></span> <span data-ttu-id="35060-153">Para obtener más información sobre las características de la red CDN de Azure, consulte la [información general de la red CDN](../cdn/cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="35060-153">For more information about Azure CDN features, see the [CDN overview](../cdn/cdn-overview.md).</span></span>
 
### <a name="additional-considerations"></a><span data-ttu-id="35060-154">Consideraciones adicionales</span><span class="sxs-lookup"><span data-stu-id="35060-154">Additional considerations</span></span>

* <span data-ttu-id="35060-155">Cuando la red CDN está habilitada para un extremo de streaming, los clientes no pueden solicitar contenido directamente desde el origen.</span><span class="sxs-lookup"><span data-stu-id="35060-155">When CDN is enabled for a streaming endpoint, clients cannot request content directly from the origin.</span></span> <span data-ttu-id="35060-156">Si necesita poder probar el contenido con o sin red CDN, puede crear otro punto de conexión de streaming que no tenga habilitada la red CDN.</span><span class="sxs-lookup"><span data-stu-id="35060-156">If you need the ability to test your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span></span>
* <span data-ttu-id="35060-157">El nombre de host del extremo de streaming permanece igual después de habilitar la red CDN.</span><span class="sxs-lookup"><span data-stu-id="35060-157">Your streaming endpoint hostname remains the same after enabling CDN.</span></span> <span data-ttu-id="35060-158">No es necesario realizar ningún cambio en el flujo de trabajo de Servicios multimedia una vez habilitada la red CDN.</span><span class="sxs-lookup"><span data-stu-id="35060-158">You don’t need to make any changes to your media services workflow after CDN is enabled.</span></span> <span data-ttu-id="35060-159">Por ejemplo, si el nombre de host del extremo de streaming es strasbourg.streaming.mediaservices.windows.net, después de habilitar la red CDN se usa exactamente el mismo nombre de host.</span><span class="sxs-lookup"><span data-stu-id="35060-159">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, the exact same hostname is used.</span></span>
* <span data-ttu-id="35060-160">Para los nuevos puntos de conexión de streaming, puede habilitar la red CDN creando un nuevo punto de conexión; para los puntos de conexión de streaming existentes, deberá detener primero el punto de conexión y, después, habilitar/deshabilitar la red CDN.</span><span class="sxs-lookup"><span data-stu-id="35060-160">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need to first stop the endpoint and then enable/disable the CDN.</span></span>
* <span data-ttu-id="35060-161">El punto de conexión de streaming estándar solo se puede configurar mediante el **proveedor de red CDN estándar de Verizon** con el portal de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="35060-161">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure management portal.</span></span> <span data-ttu-id="35060-162">Sin embargo, puede habilitar otros proveedores de la red CDN de Azure mediante las API de REST.</span><span class="sxs-lookup"><span data-stu-id="35060-162">However, you can enable other Azure CDN providers using REST APIs.</span></span>

## <a name="configure-cdn-profile"></a><span data-ttu-id="35060-163">Configuración del perfil de la red CDN</span><span class="sxs-lookup"><span data-stu-id="35060-163">Configure CDN profile</span></span>

<span data-ttu-id="35060-164">Puede configurar el perfil de la red CDN con el botón **Administrar red de entrega de contenido** de la parte superior.</span><span class="sxs-lookup"><span data-stu-id="35060-164">You can configure the CDN profile by selecting the **Manage CDN** button from the top.</span></span>

![punto de conexión de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a><span data-ttu-id="35060-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="35060-166">Next steps</span></span>
<span data-ttu-id="35060-167">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="35060-167">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="35060-168">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="35060-168">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

