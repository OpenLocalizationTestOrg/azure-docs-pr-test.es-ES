---
title: "Introducción a Azure CDN | Microsoft Docs"
description: "En este tema se muestra cómo habilitar Azure Content Delivery Network (CDN). El tutorial le guía a través de la creación de un perfil y un punto de conexión nuevos de la red CDN."
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
ms.openlocfilehash: d263e911d0d0b3cdc1e48e300a3c8a0994b38c39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-cdn"></a><span data-ttu-id="578d6-104">Introducción a Azure CDN</span><span class="sxs-lookup"><span data-stu-id="578d6-104">Getting started with Azure CDN</span></span>
<span data-ttu-id="578d6-105">Este tema le guía a través de la habilitación de la red CDN de Azure mediante la creación de un perfil de red CDN y un punto de conexión nuevo.</span><span class="sxs-lookup"><span data-stu-id="578d6-105">This topic walks through enabling Azure CDN by creating a new CDN profile and endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="578d6-106">Para una introducción al funcionamiento de la red CDN, así como una lista de las características, consulte la [información general de la red CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="578d6-106">For an introduction to how CDN works, as well as a list of features, see the [CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="578d6-107">Crear un nuevo perfil de CDN</span><span class="sxs-lookup"><span data-stu-id="578d6-107">Create a new CDN profile</span></span>
<span data-ttu-id="578d6-108">Un perfil de red de entrega de contenido es una colección de puntos de conexión de red de entrega de contenido.</span><span class="sxs-lookup"><span data-stu-id="578d6-108">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="578d6-109">Cada perfil contiene uno o más de estos puntos de conexión de CDN.</span><span class="sxs-lookup"><span data-stu-id="578d6-109">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="578d6-110">Puede que quiera usar varios perfiles para organizar sus puntos de conexión de la red CDN por dominio de Internet, aplicación web o cualquier otro criterio.</span><span class="sxs-lookup"><span data-stu-id="578d6-110">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="578d6-111">De manera predeterminada, una sola suscripción de Azure está limitada a ocho perfiles de red CDN.</span><span class="sxs-lookup"><span data-stu-id="578d6-111">By default, a single Azure subscription is limited to eight CDN profiles.</span></span> <span data-ttu-id="578d6-112">Cada perfil de red CDN está limitado a diez puntos de conexión de red CDN.</span><span class="sxs-lookup"><span data-stu-id="578d6-112">Each CDN profile is limited to ten CDN endpoints.</span></span>
> 
> <span data-ttu-id="578d6-113">Los precios de red de entrega de contenido se aplican en el nivel de perfil de red de entrega de contenido.</span><span class="sxs-lookup"><span data-stu-id="578d6-113">CDN pricing is applied at the CDN profile level.</span></span> <span data-ttu-id="578d6-114">Si quiere utilizar una combinación planes de tarifa de Red CDN de Azure, necesitará varios perfiles de red CDN.</span><span class="sxs-lookup"><span data-stu-id="578d6-114">If you wish to use a mix of Azure CDN pricing tiers, you will need multiple CDN profiles.</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="578d6-115">Crear un nuevo punto de conexión de CDN</span><span class="sxs-lookup"><span data-stu-id="578d6-115">Create a new CDN endpoint</span></span>
<span data-ttu-id="578d6-116">**Para crear un nuevo punto de conexión de red CDN**</span><span class="sxs-lookup"><span data-stu-id="578d6-116">**To create a new CDN endpoint**</span></span>

1. <span data-ttu-id="578d6-117">En el [Portal de Azure](https://portal.azure.com), vaya su perfil de red CDN.</span><span class="sxs-lookup"><span data-stu-id="578d6-117">In the [Azure Portal](https://portal.azure.com), navigate to your CDN profile.</span></span>  <span data-ttu-id="578d6-118">Puede haberlo anclado al panel en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="578d6-118">You may have pinned it to the dashboard in the previous step.</span></span>  <span data-ttu-id="578d6-119">Si no lo hace, para encontrarlo, haga clic en **Examinar**, en **Perfiles de CDN** y, luego, haga clic en el perfil al que planea agregar el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="578d6-119">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span></span>
   
    <span data-ttu-id="578d6-120">Aparece la hoja del perfil de CDN.</span><span class="sxs-lookup"><span data-stu-id="578d6-120">The CDN profile blade appears.</span></span>
   
    ![Perfil de CDN][cdn-profile-settings]
2. <span data-ttu-id="578d6-122">Haga clic en el botón **Agregar extremo** .</span><span class="sxs-lookup"><span data-stu-id="578d6-122">Click the **Add Endpoint** button.</span></span>
   
    ![Botón Agregar punto de conexión][cdn-new-endpoint-button]
   
    <span data-ttu-id="578d6-124">Aparecerá la hoja **Agregar un extremo** .</span><span class="sxs-lookup"><span data-stu-id="578d6-124">The **Add an endpoint** blade appears.</span></span>
   
    ![Hoja Agregar punto de conexión][cdn-add-endpoint]
3. <span data-ttu-id="578d6-126">Escriba un **Nombre** para este punto de conexión de red de entrega de contenido.</span><span class="sxs-lookup"><span data-stu-id="578d6-126">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="578d6-127">Este nombre se usará para obtener acceso a sus recursos almacenados en caché en el dominio `<endpointname>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="578d6-127">This name will be used to access your cached resources at the domain `<endpointname>.azureedge.net`.</span></span>
4. <span data-ttu-id="578d6-128">En la lista desplegable **Tipo de origen** , seleccione su tipo de origen.</span><span class="sxs-lookup"><span data-stu-id="578d6-128">In the **Origin type** dropdown, select your origin type.</span></span>  <span data-ttu-id="578d6-129">Seleccione **Almacenamiento** para una cuenta de Azure Storage, **Servicio en la nube** para un servicio en la nube de Azure, **Aplic. web** para una aplic. web de Azure, o bien **Origen personalizado** para cualquier otro origen del servidor web públicamente accesible (hospedado en Azure o en otro lugar).</span><span class="sxs-lookup"><span data-stu-id="578d6-129">Select **Storage** for an Azure Storage account, **Cloud service** for an Azure Cloud Service, **Web App** for an Azure Web App, or **Custom origin** for any other publicly accessible web server origin (hosted in Azure or elsewhere).</span></span>
   
    ![Tipo de origen de la red CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. <span data-ttu-id="578d6-131">En la lista desplegable **Nombre de host de origen** , seleccione o escriba su dominio de origen.</span><span class="sxs-lookup"><span data-stu-id="578d6-131">In the **Origin hostname** dropdown, select or type your origin domain.</span></span>  <span data-ttu-id="578d6-132">En la lista desplegable se muestran todos los orígenes disponibles del tipo especificado en el paso 4.</span><span class="sxs-lookup"><span data-stu-id="578d6-132">The dropdown will list all available origins of the type you specified in step 4.</span></span>  <span data-ttu-id="578d6-133">Si seleccionó *Origen personalizado* como su **Tipo de origen**, tendrá que escribir el dominio de su origen personalizado.</span><span class="sxs-lookup"><span data-stu-id="578d6-133">If you selected *Custom origin* as your **Origin type**, you will type in the domain of your custom origin.</span></span>
6. <span data-ttu-id="578d6-134">En el cuadro de texto **Ruta de acceso de origen** , escriba la ruta de acceso a los recursos que quiera almacenar en caché o déjela en blanco para permitir almacenar en caché cualquier recurso en el dominio especificado en el paso 5.</span><span class="sxs-lookup"><span data-stu-id="578d6-134">In the **Origin path** text box, enter the path to the resources you want to cache, or leave blank to allow cache any resource at the domain you specified in step 5.</span></span>
7. <span data-ttu-id="578d6-135">En el **Encabezado del host de origen**, escriba el encabezado de host que quiera que la red CDN envíe con cada solicitud o deje el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="578d6-135">In the **Origin host header**, enter the host header you want the CDN to send with each request, or leave the default.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="578d6-136">Algunos tipos de orígenes, como Almacenamiento de Azure y Aplicaciones web, requieren que el encabezado del host coincida con el dominio del origen.</span><span class="sxs-lookup"><span data-stu-id="578d6-136">Some types of origins, such as Azure Storage and Web Apps, require the host header to match the domain of the origin.</span></span> <span data-ttu-id="578d6-137">A menos que tenga un origen que requiera un encabezado de host diferente de su dominio, debe dejar el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="578d6-137">Unless you have an origin that requires a host header different from its domain, you should leave the default value.</span></span>
   > 
   > 
8. <span data-ttu-id="578d6-138">Para **Protocolo** y **Puerto de origen**, especifique los protocolos y los puertos que se usan para tener acceso a sus recursos en el origen.</span><span class="sxs-lookup"><span data-stu-id="578d6-138">For **Protocol** and **Origin port**, specify the protocols and ports used to access your resources at the origin.</span></span>  <span data-ttu-id="578d6-139">Se debe seleccionar al menos un protocolo (HTTP o HTTPS).</span><span class="sxs-lookup"><span data-stu-id="578d6-139">At least one protocol (HTTP or HTTPS) must be selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="578d6-140">El valor de **Puerto de origen** solo afecta al puerto que utiliza el punto de conexión para recuperar información del origen.</span><span class="sxs-lookup"><span data-stu-id="578d6-140">The **Origin port** only affects what port the endpoint uses to retrieve information from the origin.</span></span>  <span data-ttu-id="578d6-141">El propio punto de conexión solo estará disponible para los clientes finales en los puertos HTTP y HTTPS predeterminados (80 y 443), independencia de cuál sea el **puerto de origen**.</span><span class="sxs-lookup"><span data-stu-id="578d6-141">The endpoint itself will only be available to end clients on the default HTTP and HTTPS ports (80 and 443), regardless of the **Origin port**.</span></span>  
   > 
   > <span data-ttu-id="578d6-142">**red CDN de Azure de Akamai** no permiten el intervalo completo de puertos TCP para los orígenes.</span><span class="sxs-lookup"><span data-stu-id="578d6-142">**Azure CDN from Akamai** endpoints do not allow the full TCP port range for origins.</span></span>  <span data-ttu-id="578d6-143">Para obtener una lista de los puertos de origen que no se permiten, consulte [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx)(Puertos de origen permitidos de la red CDN de Azure de Akamai).</span><span class="sxs-lookup"><span data-stu-id="578d6-143">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span></span>  
   > 
   > <span data-ttu-id="578d6-144">El acceso al contenido de la red CDN usando HTTPS tiene la siguiente restricciones:</span><span class="sxs-lookup"><span data-stu-id="578d6-144">Accessing CDN content using HTTPS has the following constraints:</span></span>
   > 
   > * <span data-ttu-id="578d6-145">Debe utilizar el certificado SSL proporcionado por la red CDN.</span><span class="sxs-lookup"><span data-stu-id="578d6-145">You must use the SSL certificate provided by the CDN.</span></span> <span data-ttu-id="578d6-146">No se admiten certificados de terceros.</span><span class="sxs-lookup"><span data-stu-id="578d6-146">Third party certificates are not supported.</span></span>
   > * <span data-ttu-id="578d6-147">Para acceder al contenido HTTPS, tiene que usar el dominio proporcionado por la red CDN (`<endpointname>.azureedge.net`).</span><span class="sxs-lookup"><span data-stu-id="578d6-147">You must use the CDN-provided domain (`<endpointname>.azureedge.net`) to access HTTPS content.</span></span> <span data-ttu-id="578d6-148">La compatibilidad con HTTPS no está disponible para nombres de dominio personalizados (CNAME) dado que la red CDN no admite certificados personalizados en este momento.</span><span class="sxs-lookup"><span data-stu-id="578d6-148">HTTPS support is not available for custom domain names (CNAMEs) since the CDN does not support custom certificates at this time.</span></span>
   > 
   > 
9. <span data-ttu-id="578d6-149">Haga clic en el botón **Agregar** para crear el nuevo punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="578d6-149">Click the **Add** button to create the new endpoint.</span></span>
10. <span data-ttu-id="578d6-150">Una vez creado el punto de conexión, aparecerá en la lista de puntos de conexión del perfil.</span><span class="sxs-lookup"><span data-stu-id="578d6-150">Once the endpoint is created, it appears in a list of endpoints for the profile.</span></span> <span data-ttu-id="578d6-151">La visualización de la lista muestra la URL que se debe utilizar para tener acceso al contenido en caché, así como al dominio de origen.</span><span class="sxs-lookup"><span data-stu-id="578d6-151">The list view shows the URL to use to access cached content, as well as the origin domain.</span></span>
    
    ![Punto de conexión de CDN][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > <span data-ttu-id="578d6-153">El punto de conexión no estará disponible para su uso de forma inmediata; el registro puede tardar en propagarse a través de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="578d6-153">The endpoint will not immediately be available for use, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="578d6-154">Para <b>red CDN de Azure de Akamai</b> , la propagación normalmente se completará en un minuto.</span><span class="sxs-lookup"><span data-stu-id="578d6-154">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="578d6-155">Para los perfiles de la <b>red CDN de Azure de Verizon</b>, la propagación normalmente se completará en 90 minutos, pero en algunos casos puede tardar más tiempo.</span><span class="sxs-lookup"><span data-stu-id="578d6-155">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
    > 
    > <span data-ttu-id="578d6-156">Los usuarios que intenten usar el nombre de dominio de la red CDN antes de que la configuración del punto de conexión se haya propagado a los POP recibirán los códigos de respuesta HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="578d6-156">Users who try to use the CDN domain name before the endpoint configuration has propagated to the POPs will receive HTTP 404 response codes.</span></span>  <span data-ttu-id="578d6-157">Si han pasado varias horas desde que creó el punto de conexión y aún recibe errores 404, consulte [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md)(Solución de problemas de puntos de conexión de redes CDN que devuelven errores 404).</span><span class="sxs-lookup"><span data-stu-id="578d6-157">If it's been several hours since you created your endpoint and you're still receiving 404 responses, please see [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md).</span></span>
    > 
    > 

## <a name="see-also"></a><span data-ttu-id="578d6-158">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="578d6-158">See Also</span></span>
* [<span data-ttu-id="578d6-159">Control del comportamiento del almacenamiento en caché de las solicitudes con cadenas de consulta</span><span class="sxs-lookup"><span data-stu-id="578d6-159">Controlling caching behavior of requests with query strings</span></span>](cdn-query-string.md)
* [<span data-ttu-id="578d6-160">Asignación del contenido de la red CDN a un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="578d6-160">How to Map CDN Content to a Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="578d6-161">Carga previa de activos en un punto de conexión de CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="578d6-161">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="578d6-162">Depuración de un punto de conexión de red de entrega de contenido de Azure</span><span class="sxs-lookup"><span data-stu-id="578d6-162">Purge an Azure CDN Endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="578d6-163">Solución de problemas de redes CDN que devuelven errores 404</span><span class="sxs-lookup"><span data-stu-id="578d6-163">Troubleshooting CDN endpoints returning 404 statuses</span></span>](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
