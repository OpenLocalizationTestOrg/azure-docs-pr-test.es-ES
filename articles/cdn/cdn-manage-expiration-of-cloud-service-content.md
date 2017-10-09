---
title: "aaaManage la expiración de contenido web en la red CDN de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage la expiración de contenido Web aplicaciones o servicios en la nube, ASP.NET o IIS en la red CDN de Azure."
services: cdn
documentationcenter: .NET
author: zhangmanling
manager: erikre
editor: 
ms.assetid: bef53fcc-bb13-4002-9324-9edee9da8288
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a0154236c3893b627f4480e0688f555964862556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a><span data-ttu-id="6f963-103">Administración de la caducidad del contenido de Azure Web Apps/Cloud Services, ASP.NET o IIS en la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="6f963-103">Manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6f963-104">Azure Web Apps/Cloud Services, ASP.NET o IIS</span><span class="sxs-lookup"><span data-stu-id="6f963-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="6f963-105">Azure Storage Blob service</span><span class="sxs-lookup"><span data-stu-id="6f963-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="6f963-106">Los archivos de cualquier servidor web de origen accesible públicamente se pueden almacenar en caché en la red CDN de Azure hasta que transcurra su tiempo de vida (TTL).</span><span class="sxs-lookup"><span data-stu-id="6f963-106">Files from any publicly accessible origin web server can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="6f963-107">Hello TTL determina hello [ *Cache-Control* encabezado](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) en respuesta de hello HTTP del servidor de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f963-107">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from hello origin server.</span></span>  <span data-ttu-id="6f963-108">Este artículo se describe cómo tooset `Cache-Control` encabezados para aplicaciones Web de Azure, servicios en la nube, las aplicaciones ASP.NET y sitios de Internet Information Services, todos ellos se configuran de forma similar.</span><span class="sxs-lookup"><span data-stu-id="6f963-108">This article describes how tooset `Cache-Control` headers for Azure Web Apps, Azure Cloud Services, ASP.NET applications, and Internet Information Services sites, all of which are configured similarly.</span></span>

> [!TIP]
> <span data-ttu-id="6f963-109">No puede elegir tooset ningún período de vida de un archivo.</span><span class="sxs-lookup"><span data-stu-id="6f963-109">You may choose tooset no TTL on a file.</span></span>  <span data-ttu-id="6f963-110">En este caso, la red CDN de Azure aplica automáticamente un valor predeterminado de TTL de siete días.</span><span class="sxs-lookup"><span data-stu-id="6f963-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="6f963-111">Para obtener más información sobre cómo funciona la toospeed toofiles de acceso y otros recursos de la red CDN de Azure, vea hello [información general sobre la red CDN de Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6f963-111">For more information about how Azure CDN works toospeed up access toofiles and other resources, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a><span data-ttu-id="6f963-112">Establecimiento de los encabezados Cache-Control en la configuración</span><span class="sxs-lookup"><span data-stu-id="6f963-112">Setting Cache-Control Headers in configuration</span></span>
<span data-ttu-id="6f963-113">Para contenido estático, como imágenes y hojas de estilos, puede controlar frecuencia de actualización de hello modificando hello **applicationHost.config** o **web.config** archivos de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="6f963-113">For static content, such as images and style sheets, you can control hello update frequency by modifying hello **applicationHost.config** or **web.config** files for your web application.</span></span>  <span data-ttu-id="6f963-114">Hola **system.webServer\staticContent\clientCache** elemento en el archivo de configuración de hello establecerá hello `Cache-Control` encabezado para su contenido.</span><span class="sxs-lookup"><span data-stu-id="6f963-114">hello **system.webServer\staticContent\clientCache** element in hello configuration file will set hello `Cache-Control` header for your content.</span></span> <span data-ttu-id="6f963-115">Para **web.config**, Hola configuración configuración afectará a todos los elementos en la carpeta de Hola y todas sus subcarpetas, a menos que se reemplaza en el nivel de la subcarpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f963-115">For **web.config**, hello configuration settings will affect everything in hello folder and all subfolders, unless overridden at hello subfolder level.</span></span>  <span data-ttu-id="6f963-116">Por ejemplo, puede establecer un valor predeterminado time-to-live en hello raíz toohave todo el contenido estático en memoria caché durante tres días, pero tiene una subcarpeta que tiene más variable contenido con una configuración de caché de 6 horas.</span><span class="sxs-lookup"><span data-stu-id="6f963-116">For example, you can set a default time-to-live at hello root toohave all static content cached for 3 days, but have a subfolder that has more variable content with a cache setting of 6 hours.</span></span>  <span data-ttu-id="6f963-117">Para **applicationHost.config**, todas las aplicaciones en el sitio de Hola se verán afectadas, pero pueden invalidarse en **web.config** archivos en aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f963-117">For **applicationHost.config**, all applications on hello site will be affected, but can be overridden in **web.config** files in hello applications.</span></span>

<span data-ttu-id="6f963-118">Hello siguiente XML muestra un ejemplo de configuración **clientCache** toospecify una antigüedad máxima de 3 días:</span><span class="sxs-lookup"><span data-stu-id="6f963-118">hello following XML shows an example of setting **clientCache** toospecify a maximum age of 3 days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="6f963-119">Especificar **UseMaxAge** agrega un `Cache-Control: max-age=<nnn>` respuesta toohello de encabezado se basa en valor de hello especificado en hello **CacheControlMaxAge** atributo.</span><span class="sxs-lookup"><span data-stu-id="6f963-119">Specifying **UseMaxAge** adds a `Cache-Control: max-age=<nnn>` header toohello response based on hello value specified in hello **CacheControlMaxAge** attribute.</span></span> <span data-ttu-id="6f963-120">formato de Hola de timespan hello es para hello **cacheControlMaxAge** atributo es <days>.<hours>:<min>:<sec>.</span><span class="sxs-lookup"><span data-stu-id="6f963-120">hello format of hello timespan is for hello **cacheControlMaxAge** attribute is <days>.<hours>:<min>:<sec>.</span></span> <span data-ttu-id="6f963-121">Para obtener más información sobre hello **clientCache** nodo, consulte [memoria caché del cliente <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span><span class="sxs-lookup"><span data-stu-id="6f963-121">For more information on hello **clientCache** node, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-in-code"></a><span data-ttu-id="6f963-122">Establecimiento de los encabezados Cache-Control en el código</span><span class="sxs-lookup"><span data-stu-id="6f963-122">Setting Cache-Control Headers in Code</span></span>
<span data-ttu-id="6f963-123">Para las aplicaciones ASP.NET, puede establecer comportamiento de almacenamiento en caché de CDN Hola mediante programación por establecer hello **HttpResponse.Cache** propiedad.</span><span class="sxs-lookup"><span data-stu-id="6f963-123">For ASP.NET applications, you can set hello CDN caching behavior programmatically by setting hello **HttpResponse.Cache** property.</span></span> <span data-ttu-id="6f963-124">Para obtener más información sobre hello **HttpResponse.Cache** propiedad, vea [propiedad HttpResponse.Cache](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) y [clase HttpCachePolicy](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f963-124">For more information on hello **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="6f963-125">Si desea que el contenido de la aplicación tooprogrammatically caché de ASP.NET, asegúrese de que el contenido de Hola se marca como almacenable en caché debe establecer HttpCacheability demasiado*público*.</span><span class="sxs-lookup"><span data-stu-id="6f963-125">If you want tooprogrammatically cache application content in ASP.NET, make sure that hello content is marked as cacheable by setting HttpCacheability too*Public*.</span></span> <span data-ttu-id="6f963-126">Asimismo, asegúrese de que se ha establecido un validador de caché.</span><span class="sxs-lookup"><span data-stu-id="6f963-126">Also, ensure that a cache validator is set.</span></span> <span data-ttu-id="6f963-127">Validador de caché de Hello puede ser una última modificación marca de tiempo establecido mediante una llamada a SetLastModified o bien un valor etag, se establece llamando a SetETag.</span><span class="sxs-lookup"><span data-stu-id="6f963-127">hello cache validator can be a Last Modified timestamp set by calling SetLastModified, or an etag value set by calling SetETag.</span></span> <span data-ttu-id="6f963-128">Si lo desea, también puede especificar una hora de expiración de caché mediante una llamada a SetExpires o puede basarse en la heurística de caché predeterminada de hello descrita anteriormente en este documento.</span><span class="sxs-lookup"><span data-stu-id="6f963-128">Optionally, you can also specify a cache expiration time by calling SetExpires, or you can rely on hello default cache heuristics described earlier in this document.</span></span>  

<span data-ttu-id="6f963-129">Por ejemplo, toocache contenido durante una hora, agregue Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="6f963-129">For example, toocache content for one hour, add hello following:</span></span>  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a><span data-ttu-id="6f963-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6f963-130">Next Steps</span></span>
* [<span data-ttu-id="6f963-131">Leer detalles de hello **clientCache** elemento</span><span class="sxs-lookup"><span data-stu-id="6f963-131">Read details about hello **clientCache** element</span></span>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [<span data-ttu-id="6f963-132">Leer documentación Hola Hola **HttpResponse.Cache** propiedad</span><span class="sxs-lookup"><span data-stu-id="6f963-132">Read hello documentation for hello **HttpResponse.Cache** Property</span></span>](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* <span data-ttu-id="6f963-133">[Leer documentación Hola Hola **clase HttpCachePolicy**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f963-133">[Read hello documentation for hello **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

