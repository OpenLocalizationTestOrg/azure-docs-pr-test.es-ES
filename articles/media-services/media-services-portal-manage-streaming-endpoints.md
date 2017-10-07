---
title: aaaManage streaming extremos con hello portal de Azure | Documentos de Microsoft
description: "Este tema muestra cómo los extremos de streaming con toomanage Hola portal de Azure."
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
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="a1f04-103">Administrar los extremos de streaming con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a1f04-103">Manage streaming endpoints with hello Azure portal</span></span>

<span data-ttu-id="a1f04-104">Este tema muestra cómo toouse Hola extremos de streaming de toomanage de portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f04-104">This topic shows  how toouse hello Azure portal toomanage streaming endpoints.</span></span> 

>[!NOTE]
><span data-ttu-id="a1f04-105">Realizar seguro hello tooreview [Introducción](media-services-streaming-endpoints-overview.md) tema.</span><span class="sxs-lookup"><span data-stu-id="a1f04-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> 

<span data-ttu-id="a1f04-106">Para obtener información acerca de cómo tooscale Hola extremo de streaming, vea [esto](media-services-portal-scale-streaming-endpoints.md) tema.</span><span class="sxs-lookup"><span data-stu-id="a1f04-106">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="start-managing-streaming-endpoints"></a><span data-ttu-id="a1f04-107">Inicio de la administración de puntos de conexión de streaming</span><span class="sxs-lookup"><span data-stu-id="a1f04-107">Start managing streaming endpoints</span></span> 

<span data-ttu-id="a1f04-108">Hola toostart administrar extremos de streaming para su cuenta, después.</span><span class="sxs-lookup"><span data-stu-id="a1f04-108">toostart managing streaming endpoints for your account, do hello following.</span></span>

1. <span data-ttu-id="a1f04-109">Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f04-109">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="a1f04-110">Hola **configuración** hoja, seleccione **los extremos de Streaming**.</span><span class="sxs-lookup"><span data-stu-id="a1f04-110">In hello **Settings** blade, select **Streaming endpoints**.</span></span>
   
    ![punto de conexión de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> <span data-ttu-id="a1f04-112">Solo se le cobrará cuando StreamingEndpoint esté en estado en ejecución.</span><span class="sxs-lookup"><span data-stu-id="a1f04-112">You are only billed when your Streaming Endpoint is in running state.</span></span>

## <a name="adddelete-a-streaming-endpoint"></a><span data-ttu-id="a1f04-113">Adición o eliminación de puntos de conexión de streaming</span><span class="sxs-lookup"><span data-stu-id="a1f04-113">Add/delete a streaming endpoint</span></span>

>[!NOTE]
><span data-ttu-id="a1f04-114">no se puede eliminar predeterminado Hola extremo de streaming.</span><span class="sxs-lookup"><span data-stu-id="a1f04-114">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="a1f04-115">tooadd/delete streaming extremo mediante Hola portal de Azure, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="a1f04-115">tooadd/delete streaming endpoint using hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="a1f04-116">tooadd un extremo de streaming, haga clic en hello **+ extremo** al principio de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f04-116">tooadd a streaming endpoint, click hello **+ Endpoint** at hello top of hello page.</span></span> 

    <span data-ttu-id="a1f04-117">Es recomendable varios extremos de Streaming si tiene previsto toohave CDN diferente o una CDN y el acceso directo.</span><span class="sxs-lookup"><span data-stu-id="a1f04-117">You might want multiple Streaming Endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

2. <span data-ttu-id="a1f04-118">Presione toodelete un extremo de streaming, **eliminar** botón.</span><span class="sxs-lookup"><span data-stu-id="a1f04-118">toodelete a streaming endpoint, press **Delete** button.</span></span>      
3. <span data-ttu-id="a1f04-119">Haga clic en hello **iniciar** Hola de toostart botón extremo de streaming.</span><span class="sxs-lookup"><span data-stu-id="a1f04-119">Click hello **Start** button toostart hello streaming endpoint.</span></span>
   
    ![punto de conexión de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <span data-ttu-id="a1f04-121"><a id="configure_streaming_endpoints"></a>Configuración de extremo de Streaming de Hola</span><span class="sxs-lookup"><span data-stu-id="a1f04-121"><a id="configure_streaming_endpoints"></a>Configuring hello Streaming Endpoint</span></span>
<span data-ttu-id="a1f04-122">Extremo de streaming permite hello tooconfigure propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="a1f04-122">Streaming Endpoint enables you tooconfigure hello following properties:</span></span>

* <span data-ttu-id="a1f04-123">Control de acceso</span><span class="sxs-lookup"><span data-stu-id="a1f04-123">Access control</span></span>
* <span data-ttu-id="a1f04-124">Control de caché</span><span class="sxs-lookup"><span data-stu-id="a1f04-124">Cache control</span></span>
* <span data-ttu-id="a1f04-125">Directivas de acceso en varios sitios</span><span class="sxs-lookup"><span data-stu-id="a1f04-125">Cross site access policies</span></span>

<span data-ttu-id="a1f04-126">Para obtener información detallada acerca de estas propiedades, consulte [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="a1f04-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="a1f04-127">Puede configurar el extremo de streaming haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="a1f04-127">You can configure streaming endpoint by doing hello following:</span></span>

1. <span data-ttu-id="a1f04-128">Seleccione Hola desea tooconfigure de extremo de streaming.</span><span class="sxs-lookup"><span data-stu-id="a1f04-128">Select hello streaming endpoint you want tooconfigure.</span></span>
2. <span data-ttu-id="a1f04-129">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="a1f04-129">Click **Settings**.</span></span>

<span data-ttu-id="a1f04-130">A continuación se muestra una breve descripción de los campos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f04-130">A brief description of hello fields follows.</span></span>

![punto de conexión de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. <span data-ttu-id="a1f04-132">Directiva de caché máximo: duración en caché de tooconfigure usado para los activos se sirve a través de este extremo de streaming.</span><span class="sxs-lookup"><span data-stu-id="a1f04-132">Maximum cache policy: used tooconfigure cache lifetime for assets served through this streaming endpoint.</span></span> <span data-ttu-id="a1f04-133">Si se establece ningún valor, se utiliza el predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f04-133">If no value is set, hello default is used.</span></span> <span data-ttu-id="a1f04-134">valores predeterminados de Hello también pueden definirse directamente en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f04-134">hello default values can also be defined directly in Azure storage.</span></span> <span data-ttu-id="a1f04-135">Si la CDN de Azure está habilitada para el extremo de streaming de hello, no debería establecer a Hola caché directiva valor que no requiere herramientas de 600 segundos.</span><span class="sxs-lookup"><span data-stu-id="a1f04-135">If Azure CDN is enabled for hello streaming endpoint, you should not set hello cache policy value tooless than 600 seconds.</span></span>  
2. <span data-ttu-id="a1f04-136">Direcciones IP permitidas: usar direcciones IP de toospecify que se podrá tooconnect toohello publicado extremo de streaming.</span><span class="sxs-lookup"><span data-stu-id="a1f04-136">Allowed IP addresses: used toospecify IP addresses that would be allowed tooconnect toohello published streaming endpoint.</span></span> <span data-ttu-id="a1f04-137">Si no hay direcciones IP especificadas, cualquier dirección IP sería capaz de tooconnect.</span><span class="sxs-lookup"><span data-stu-id="a1f04-137">If no IP addresses specified, any IP address would be able tooconnect.</span></span> <span data-ttu-id="a1f04-138">Las direcciones IP se pueden especificar como una dirección IP única (por ejemplo, 10.0.0.1), un intervalo de IP que usa una dirección IP y una máscara de subred CIDR (por ejemplo, 10.0.0.1/22) o un intervalo de IP que usa una máscara de subred decimal con puntos; por ejemplo, 10.0.0.1(255.255.255.0).</span><span class="sxs-lookup"><span data-stu-id="a1f04-138">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span></span>
3. <span data-ttu-id="a1f04-139">Configuración para la autenticación de encabezado de firma de Akamai: usa toospecify cómo se configura la solicitud de autenticación de encabezado de firma procedentes de servidores Akamai.</span><span class="sxs-lookup"><span data-stu-id="a1f04-139">Configuration for Akamai signature header authentication: used toospecify how signature header authentication request from Akamai servers is configured.</span></span> <span data-ttu-id="a1f04-140">La expiración está en formato UTC.</span><span class="sxs-lookup"><span data-stu-id="a1f04-140">Expiration is in UTC.</span></span>

## <a name="scale-your-premium-streaming-endpoint"></a><span data-ttu-id="a1f04-141">Escalado del punto de conexión de streaming premium</span><span class="sxs-lookup"><span data-stu-id="a1f04-141">Scale your Premium streaming endpoint</span></span>

<span data-ttu-id="a1f04-142">Para obtener más información, consulte [este tema](media-services-portal-scale-streaming-endpoints.md) .</span><span class="sxs-lookup"><span data-stu-id="a1f04-142">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <span data-ttu-id="a1f04-143"><a id="enable_cdn"></a>Habilitación de la integración de CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="a1f04-143"><a id="enable_cdn"></a>Enable Azure CDN integration</span></span>

<span data-ttu-id="a1f04-144">Cuando se crea una nueva cuenta, la integración de la red CDN de Azure de punto de conexión de streaming está habilitada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a1f04-144">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span></span>

<span data-ttu-id="a1f04-145">Si posteriormente desea hello toodisable/habilitar CDN, debe ser el extremo de streaming en hello **detenido** estado.</span><span class="sxs-lookup"><span data-stu-id="a1f04-145">If you later want toodisable/enable hello CDN, your streaming endpoint must be in hello **stopped** state.</span></span> <span data-ttu-id="a1f04-146">Podrían tardar horas de too2 para tooget de integración de CDN de Azure Hola habilitada y para hello cambios toobe active a través de hello todos los POP de CDN.</span><span class="sxs-lookup"><span data-stu-id="a1f04-146">It could take up too2 hours for hello Azure CDN integration tooget enabled and for hello changes toobe active across all hello CDN POPs.</span></span> <span data-ttu-id="a1f04-147">Sin embargo, puede iniciar el punto de conexión y el flujo sin interrupciones transmisión por secuencias de extremo de streaming de hello y una vez completada la integración de hello, flujo de Hola se entregarán de CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f04-147">However, your can start your streaming endpoint and stream without interruptions from hello streaming endpoint and once hello integration is complete, hello stream will be delivered from hello CDN.</span></span> <span data-ttu-id="a1f04-148">Durante la Hola aprovisionamiento período su extremo de streaming estará en **a partir de** estado y se puede observar el rendimiento de degredad.</span><span class="sxs-lookup"><span data-stu-id="a1f04-148">During hello provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span></span>

<span data-ttu-id="a1f04-149">Integración de CDN está habilitada en todos los execpt de centros de datos de Azure de hello China y regiones de Gobierno Federal.</span><span class="sxs-lookup"><span data-stu-id="a1f04-149">CDN integration is enabled in all hello Azure data centers execpt China and Federal Goverment regions.</span></span>

<span data-ttu-id="a1f04-150">Una vez habilitada, Hola **el Control de acceso**, **nombre de host personalizado** y **autenticación de firma de Akamai** configuración obtiene deshabilitada.</span><span class="sxs-lookup"><span data-stu-id="a1f04-150">Once it is enabled, hello **Access Control**, **Custom hostname** and **Akamai Signature authentication** configuration gets disabled.</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="a1f04-151">La integración de Azure Media Services con la red CDN de Azure se implementa en la **red CDN de Azure de Verizon** para puntos de conexión de streaming estándar.</span><span class="sxs-lookup"><span data-stu-id="a1f04-151">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span></span> <span data-ttu-id="a1f04-152">Los puntos de conexión de streaming premium pueden configurarse con todos los **proveedores y planes de tarifa de la red CDN de Azure**.</span><span class="sxs-lookup"><span data-stu-id="a1f04-152">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span></span> <span data-ttu-id="a1f04-153">Para obtener más información acerca de las características de red CDN de Azure, vea hello [información general de la red CDN](../cdn/cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a1f04-153">For more information about Azure CDN features, see hello [CDN overview](../cdn/cdn-overview.md).</span></span>
 
### <a name="additional-considerations"></a><span data-ttu-id="a1f04-154">Consideraciones adicionales</span><span class="sxs-lookup"><span data-stu-id="a1f04-154">Additional considerations</span></span>

* <span data-ttu-id="a1f04-155">Cuando CDN esté habilitado para un extremo de transmisión por secuencias, los clientes no pueden solicitar contenido directamente desde el origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f04-155">When CDN is enabled for a streaming endpoint, clients cannot request content directly from hello origin.</span></span> <span data-ttu-id="a1f04-156">Si necesita el contenido con o sin red CDN Hola tootest de capacidad, puede crear otro extremo de transmisión por secuencias que no está habilitado de CDN.</span><span class="sxs-lookup"><span data-stu-id="a1f04-156">If you need hello ability tootest your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span></span>
* <span data-ttu-id="a1f04-157">La transmisión por secuencias permanece hostname de punto de conexión Hola igual después de habilitar la red CDN.</span><span class="sxs-lookup"><span data-stu-id="a1f04-157">Your streaming endpoint hostname remains hello same after enabling CDN.</span></span> <span data-ttu-id="a1f04-158">No es necesario toomake cualquier flujo de trabajo de cambios tooyour media services después de habilita la red CDN.</span><span class="sxs-lookup"><span data-stu-id="a1f04-158">You don’t need toomake any changes tooyour media services workflow after CDN is enabled.</span></span> <span data-ttu-id="a1f04-159">Por ejemplo, si el nombre de host de punto de conexión transmisión por secuencias es strasbourg.streaming.mediaservices.windows.net, después de habilitar la red CDN, se utiliza Hola exacta mismo nombre de host.</span><span class="sxs-lookup"><span data-stu-id="a1f04-159">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, hello exact same hostname is used.</span></span>
* <span data-ttu-id="a1f04-160">Para nuevos extremos de transmisión por secuencias, puede habilitar CDN creando un nuevo punto de conexión; para los extremos de streaming existentes, necesita el punto de conexión de toofirst stop hello y, a continuación, habilitar/deshabilitar Hola CDN.</span><span class="sxs-lookup"><span data-stu-id="a1f04-160">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need toofirst stop hello endpoint and then enable/disable hello CDN.</span></span>
* <span data-ttu-id="a1f04-161">El punto de conexión de streaming estándar solo se puede configurar mediante el **proveedor de red CDN estándar de Verizon** con el portal de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f04-161">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure management portal.</span></span> <span data-ttu-id="a1f04-162">Sin embargo, puede habilitar otros proveedores de la red CDN de Azure mediante las API de REST.</span><span class="sxs-lookup"><span data-stu-id="a1f04-162">However, you can enable other Azure CDN providers using REST APIs.</span></span>

## <a name="configure-cdn-profile"></a><span data-ttu-id="a1f04-163">Configuración del perfil de la red CDN</span><span class="sxs-lookup"><span data-stu-id="a1f04-163">Configure CDN profile</span></span>

<span data-ttu-id="a1f04-164">Puede configurar el perfil de CDN Hola seleccionando hello **administrar CDN** botón desde la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f04-164">You can configure hello CDN profile by selecting hello **Manage CDN** button from hello top.</span></span>

![punto de conexión de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a><span data-ttu-id="a1f04-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a1f04-166">Next steps</span></span>
<span data-ttu-id="a1f04-167">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="a1f04-167">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a1f04-168">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="a1f04-168">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

