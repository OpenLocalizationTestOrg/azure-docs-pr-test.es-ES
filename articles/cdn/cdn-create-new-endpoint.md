---
title: aaaGetting a trabajar con la red CDN de Azure | Documentos de Microsoft
description: "Este tema muestra cómo tooenable Hola red de entrega de contenido (CDN) de Azure. Hola tutorial le guía a través de la creación de hello de un nuevo perfil CDN y el punto de conexión."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a><span data-ttu-id="5d6fe-104">Introducción a Azure CDN</span><span class="sxs-lookup"><span data-stu-id="5d6fe-104">Getting started with Azure CDN</span></span>
<span data-ttu-id="5d6fe-105">Este tema le guía a través de la habilitación de la red CDN de Azure mediante la creación de un perfil de red CDN y un punto de conexión nuevo.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-105">This topic walks through enabling Azure CDN by creating a new CDN profile and endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5d6fe-106">Para un funcionamiento CDN toohow introducción, así como una lista de características, vea hello [información general de la red CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5d6fe-106">For an introduction toohow CDN works, as well as a list of features, see hello [CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="5d6fe-107">Crear un nuevo perfil de CDN</span><span class="sxs-lookup"><span data-stu-id="5d6fe-107">Create a new CDN profile</span></span>
<span data-ttu-id="5d6fe-108">Un perfil de red de entrega de contenido es una colección de puntos de conexión de red de entrega de contenido.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-108">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="5d6fe-109">Cada perfil contiene uno o más de estos puntos de conexión de CDN.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-109">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="5d6fe-110">Puede ser conveniente toouse varios tooorganize perfiles los extremos de red CDN el dominio de internet, las aplicaciones web u otros criterios.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-110">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="5d6fe-111">De forma predeterminada, una sola suscripción de Azure es limitado tooeight perfiles de red CDN.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-111">By default, a single Azure subscription is limited tooeight CDN profiles.</span></span> <span data-ttu-id="5d6fe-112">Cada perfil de CDN es puntos de conexión de red CDN tooten limitado.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-112">Each CDN profile is limited tooten CDN endpoints.</span></span>
> 
> <span data-ttu-id="5d6fe-113">Precios de CDN se aplican al nivel de perfil CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-113">CDN pricing is applied at hello CDN profile level.</span></span> <span data-ttu-id="5d6fe-114">Si desea toouse una combinación de CDN de Azure los niveles de precios, necesitará varios perfiles de red CDN.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-114">If you wish toouse a mix of Azure CDN pricing tiers, you will need multiple CDN profiles.</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="5d6fe-115">Crear un nuevo extremo de CDN</span><span class="sxs-lookup"><span data-stu-id="5d6fe-115">Create a new CDN endpoint</span></span>
<span data-ttu-id="5d6fe-116">**toocreate un nuevo extremo CDN**</span><span class="sxs-lookup"><span data-stu-id="5d6fe-116">**toocreate a new CDN endpoint**</span></span>

1. <span data-ttu-id="5d6fe-117">Hola [Portal de Azure](https://portal.azure.com), navegar por el perfil de CDN tooyour.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-117">In hello [Azure Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="5d6fe-118">Puede haber anclarlo toohello panel en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-118">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="5d6fe-119">Si no es así, se encontrará, haciendo clic en **examinar**, a continuación, **perfiles de red CDN**, y haga clic en el perfil de hello tiene previsto tooadd del extremo que.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-119">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="5d6fe-120">aparece la hoja de perfil CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-120">hello CDN profile blade appears.</span></span>
   
    ![Perfil de CDN][cdn-profile-settings]
2. <span data-ttu-id="5d6fe-122">Haga clic en hello **Agregar extremo** botón.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-122">Click hello **Add Endpoint** button.</span></span>
   
    ![Botón Agregar punto de conexión][cdn-new-endpoint-button]
   
    <span data-ttu-id="5d6fe-124">Hola **agregar un punto de conexión** aparece hoja.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-124">hello **Add an endpoint** blade appears.</span></span>
   
    ![Hoja Agregar punto de conexión][cdn-add-endpoint]
3. <span data-ttu-id="5d6fe-126">Escriba un **Nombre** para este punto de conexión de red de entrega de contenido.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-126">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="5d6fe-127">Este nombre será tooaccess usa los recursos almacenados en caché en el dominio de hello `<endpointname>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-127">This name will be used tooaccess your cached resources at hello domain `<endpointname>.azureedge.net`.</span></span>
4. <span data-ttu-id="5d6fe-128">Hola **tipo de origen** de lista desplegable, seleccione el tipo de origen.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-128">In hello **Origin type** dropdown, select your origin type.</span></span>  <span data-ttu-id="5d6fe-129">Seleccione **Almacenamiento** para una cuenta de Azure Storage, **Servicio en la nube** para un servicio en la nube de Azure, **Aplic. web** para una aplic. web de Azure, o bien **Origen personalizado** para cualquier otro origen del servidor web públicamente accesible (hospedado en Azure o en otro lugar).</span><span class="sxs-lookup"><span data-stu-id="5d6fe-129">Select **Storage** for an Azure Storage account, **Cloud service** for an Azure Cloud Service, **Web App** for an Azure Web App, or **Custom origin** for any other publicly accessible web server origin (hosted in Azure or elsewhere).</span></span>
   
    ![Tipo de origen de la red CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. <span data-ttu-id="5d6fe-131">Hola **nombre de host de origen** de lista desplegable, seleccione o escriba el dominio de origen.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-131">In hello **Origin hostname** dropdown, select or type your origin domain.</span></span>  <span data-ttu-id="5d6fe-132">Hola desplegable mostrará una lista de todos los orígenes disponibles del tipo hello que especificó en el paso 4.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-132">hello dropdown will list all available origins of hello type you specified in step 4.</span></span>  <span data-ttu-id="5d6fe-133">Si seleccionó *origen personalizado* como su **tipo de origen**, tendrá que escribir en el dominio de Hola de su origen personalizado.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-133">If you selected *Custom origin* as your **Origin type**, you will type in hello domain of your custom origin.</span></span>
6. <span data-ttu-id="5d6fe-134">Hola **ruta de acceso de origen** texto cuadro, escriba recursos toohello Hola ruta de acceso que desea toocache, o deje en blanco tooallow caché cualquier recurso en el dominio de Hola que especificó en el paso 5.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-134">In hello **Origin path** text box, enter hello path toohello resources you want toocache, or leave blank tooallow cache any resource at hello domain you specified in step 5.</span></span>
7. <span data-ttu-id="5d6fe-135">Hola **encabezado de host de origen**, escriba el encabezado de host de hello desea Hola toosend CDN con cada solicitud, o deje Hola predeterminado.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-135">In hello **Origin host header**, enter hello host header you want hello CDN toosend with each request, or leave hello default.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="5d6fe-136">Algunos tipos de orígenes, como el almacenamiento de Azure y las aplicaciones Web, requieren dominio hello toomatch de encabezado de host de Hola de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-136">Some types of origins, such as Azure Storage and Web Apps, require hello host header toomatch hello domain of hello origin.</span></span> <span data-ttu-id="5d6fe-137">A menos que tenga un origen que requiere un encabezado de host diferente de su dominio, debe dejar el valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-137">Unless you have an origin that requires a host header different from its domain, you should leave hello default value.</span></span>
   > 
   > 
8. <span data-ttu-id="5d6fe-138">Para **protocolo** y **puerto de origen**, especificar Hola protocolos y puertos tooaccess usa los recursos en el origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-138">For **Protocol** and **Origin port**, specify hello protocols and ports used tooaccess your resources at hello origin.</span></span>  <span data-ttu-id="5d6fe-139">Se debe seleccionar al menos un protocolo (HTTP o HTTPS).</span><span class="sxs-lookup"><span data-stu-id="5d6fe-139">At least one protocol (HTTP or HTTPS) must be selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5d6fe-140">Hola **puerto de origen** solo afecta a qué punto de conexión de puerto hello usa información de tooretrieve de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-140">hello **Origin port** only affects what port hello endpoint uses tooretrieve information from hello origin.</span></span>  <span data-ttu-id="5d6fe-141">Hello propio extremo solo será clientes tooend disponible en hello predeterminado puertos HTTP y HTTPS (80 y 443), independientemente de hello **puerto de origen**.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-141">hello endpoint itself will only be available tooend clients on hello default HTTP and HTTPS ports (80 and 443), regardless of hello **Origin port**.</span></span>  
   > 
   > <span data-ttu-id="5d6fe-142">**Azure CDN de Akamai** puntos de conexión no permita que el intervalo de puertos TCP completa de Hola para orígenes.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-142">**Azure CDN from Akamai** endpoints do not allow hello full TCP port range for origins.</span></span>  <span data-ttu-id="5d6fe-143">Para obtener una lista de los puertos de origen que no se permiten, consulte [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx)(Puertos de origen permitidos de la red CDN de Azure de Akamai).</span><span class="sxs-lookup"><span data-stu-id="5d6fe-143">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span></span>  
   > 
   > <span data-ttu-id="5d6fe-144">Obtener acceso a la red CDN tiene contenido mediante HTTPS Hola siguiendo las restricciones:</span><span class="sxs-lookup"><span data-stu-id="5d6fe-144">Accessing CDN content using HTTPS has hello following constraints:</span></span>
   > 
   > * <span data-ttu-id="5d6fe-145">Debe usar el certificado SSL de hello proporcionado por la red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-145">You must use hello SSL certificate provided by hello CDN.</span></span> <span data-ttu-id="5d6fe-146">No se admiten certificados de terceros.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-146">Third party certificates are not supported.</span></span>
   > * <span data-ttu-id="5d6fe-147">Debe usar el dominio de siempre CDN Hola (`<endpointname>.azureedge.net`) tooaccess contenido HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-147">You must use hello CDN-provided domain (`<endpointname>.azureedge.net`) tooaccess HTTPS content.</span></span> <span data-ttu-id="5d6fe-148">Compatibilidad con HTTPS no está disponible para nombres de dominio personalizados (CNAME) ya que la red CDN Hola no admite certificados personalizados en este momento.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-148">HTTPS support is not available for custom domain names (CNAMEs) since hello CDN does not support custom certificates at this time.</span></span>
   > 
   > 
9. <span data-ttu-id="5d6fe-149">Haga clic en hello **agregar** toocreate botón Hola nuevo punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-149">Click hello **Add** button toocreate hello new endpoint.</span></span>
10. <span data-ttu-id="5d6fe-150">Una vez que se crea el extremo de hello, aparece en una lista de puntos de conexión para el perfil de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-150">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="5d6fe-151">vista de lista de Hello muestra hello URL toouse tooaccess almacenado en memoria caché de contenido, así como dominio de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-151">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
    
    ![Punto de conexión de CDN][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > <span data-ttu-id="5d6fe-153">punto de conexión de Hello no inmediatamente estará disponible para su uso, tal y como se tarda en hello toopropagate de registro a través de la red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-153">hello endpoint will not immediately be available for use, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="5d6fe-154">Para <b>red CDN de Azure de Akamai</b> , la propagación normalmente se completará en un minuto.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-154">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="5d6fe-155">Para los perfiles de la <b>red CDN de Azure de Verizon</b>, la propagación normalmente se completará en 90 minutos, pero en algunos casos puede tardar más tiempo.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-155">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
    > 
    > <span data-ttu-id="5d6fe-156">Los usuarios que intenten nombre de dominio de red CDN Hola de toouse antes de configuración de extremo de hello haya propagado toohello POP recibirá los códigos de respuesta HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="5d6fe-156">Users who try toouse hello CDN domain name before hello endpoint configuration has propagated toohello POPs will receive HTTP 404 response codes.</span></span>  <span data-ttu-id="5d6fe-157">Si han pasado varias horas desde que creó el punto de conexión y aún recibe errores 404, consulte [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md)(Solución de problemas de puntos de conexión de redes CDN que devuelven errores 404).</span><span class="sxs-lookup"><span data-stu-id="5d6fe-157">If it's been several hours since you created your endpoint and you're still receiving 404 responses, please see [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md).</span></span>
    > 
    > 

## <a name="see-also"></a><span data-ttu-id="5d6fe-158">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="5d6fe-158">See Also</span></span>
* [<span data-ttu-id="5d6fe-159">Control del comportamiento del almacenamiento en caché de las solicitudes con cadenas de consulta</span><span class="sxs-lookup"><span data-stu-id="5d6fe-159">Controlling caching behavior of requests with query strings</span></span>](cdn-query-string.md)
* [<span data-ttu-id="5d6fe-160">¿Cómo tooMap CDN contenido tooa dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="5d6fe-160">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="5d6fe-161">Carga previa de activos en un punto de conexión de CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="5d6fe-161">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="5d6fe-162">Depuración de un punto de conexión de red de entrega de contenido de Azure</span><span class="sxs-lookup"><span data-stu-id="5d6fe-162">Purge an Azure CDN Endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="5d6fe-163">Solución de problemas de redes CDN que devuelven errores 404</span><span class="sxs-lookup"><span data-stu-id="5d6fe-163">Troubleshooting CDN endpoints returning 404 statuses</span></span>](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
