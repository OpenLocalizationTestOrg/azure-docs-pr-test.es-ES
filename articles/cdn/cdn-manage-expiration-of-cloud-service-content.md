---
title: "Administración de la expiración del contenido web en la red CDN de Azure | Microsoft Docs"
description: Aprenda a administrar la caducidad del contenido de Azure Web Apps/Cloud Services, ASP.NET o IIS en la red CDN de Azure.
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
ms.openlocfilehash: c207d780857a61d4b1fc0f39e6185cae67abc955
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a><span data-ttu-id="c38e8-103">Administración de la caducidad del contenido de Azure Web Apps/Cloud Services, ASP.NET o IIS en la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="c38e8-103">Manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c38e8-104">Azure Web Apps/Cloud Services, ASP.NET o IIS</span><span class="sxs-lookup"><span data-stu-id="c38e8-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="c38e8-105">Azure Storage Blob service</span><span class="sxs-lookup"><span data-stu-id="c38e8-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="c38e8-106">Los archivos de cualquier servidor web de origen accesible públicamente se pueden almacenar en caché en la red CDN de Azure hasta que transcurra su tiempo de vida (TTL).</span><span class="sxs-lookup"><span data-stu-id="c38e8-106">Files from any publicly accessible origin web server can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="c38e8-107">El período de vida viene determinado por el [encabezado *Cache-Control*](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) en la respuesta HTTP del servidor de origen.</span><span class="sxs-lookup"><span data-stu-id="c38e8-107">The TTL is determined by the [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in the HTTP response from the origin server.</span></span>  <span data-ttu-id="c38e8-108">Este artículo describe cómo establecer los encabezados `Cache-Control` para Azure Web Apps, Azure Cloud Services, las aplicaciones de ASP.NET y los sitios de Internet Information Services ya que todos ellos se configuran de forma parecida.</span><span class="sxs-lookup"><span data-stu-id="c38e8-108">This article describes how to set `Cache-Control` headers for Azure Web Apps, Azure Cloud Services, ASP.NET applications, and Internet Information Services sites, all of which are configured similarly.</span></span>

> [!TIP]
> <span data-ttu-id="c38e8-109">Puede optar por no configurar ningún tiempo de vida en un archivo.</span><span class="sxs-lookup"><span data-stu-id="c38e8-109">You may choose to set no TTL on a file.</span></span>  <span data-ttu-id="c38e8-110">En este caso, la red CDN de Azure aplica automáticamente un valor predeterminado de TTL de siete días.</span><span class="sxs-lookup"><span data-stu-id="c38e8-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="c38e8-111">Para más información sobre el funcionamiento de la red CDN de Azure para acelerar el acceso a los archivos y otros recursos, vea [Información general de la red de entrega de contenido (CDN) de Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c38e8-111">For more information about how Azure CDN works to speed up access to files and other resources, see the [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a><span data-ttu-id="c38e8-112">Establecimiento de los encabezados Cache-Control en la configuración</span><span class="sxs-lookup"><span data-stu-id="c38e8-112">Setting Cache-Control Headers in configuration</span></span>
<span data-ttu-id="c38e8-113">Para el contenido estático, como imágenes y hojas de estilos, puede controlar la frecuencia de actualización modificando los archivos **applicationHost.config** o **web.config** de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c38e8-113">For static content, such as images and style sheets, you can control the update frequency by modifying the **applicationHost.config** or **web.config** files for your web application.</span></span>  <span data-ttu-id="c38e8-114">El elemento **system.webServer\staticContent\clientCache** del archivo de configuración establecerá el encabezado `Cache-Control` para el contenido.</span><span class="sxs-lookup"><span data-stu-id="c38e8-114">The **system.webServer\staticContent\clientCache** element in the configuration file will set the `Cache-Control` header for your content.</span></span> <span data-ttu-id="c38e8-115">Para **web.config**, la configuración afectará a todo lo que contenga la carpeta y todas las subcarpetas, a menos que se esta se invalide en el nivel de subcarpeta.</span><span class="sxs-lookup"><span data-stu-id="c38e8-115">For **web.config**, the configuration settings will affect everything in the folder and all subfolders, unless overridden at the subfolder level.</span></span>  <span data-ttu-id="c38e8-116">Por ejemplo, puede establecer un período de tiempo de vida en la raíz para tener todo el contenido estático almacenado en caché durante 3 días, pero tiene una subcarpeta que tiene más contenido variable con una configuración de caché de 6 horas.</span><span class="sxs-lookup"><span data-stu-id="c38e8-116">For example, you can set a default time-to-live at the root to have all static content cached for 3 days, but have a subfolder that has more variable content with a cache setting of 6 hours.</span></span>  <span data-ttu-id="c38e8-117">En el caso de **applicationHost.config**, se verán afectadas todas las aplicaciones del sitio, pero se puede invalidar la configuración en los archivos **web.config** de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c38e8-117">For **applicationHost.config**, all applications on the site will be affected, but can be overridden in **web.config** files in the applications.</span></span>

<span data-ttu-id="c38e8-118">El siguiente código XML muestra un ejemplo de configuración **clientCache** para especificar una edad máxima de 3 días:</span><span class="sxs-lookup"><span data-stu-id="c38e8-118">The following XML shows an example of setting **clientCache** to specify a maximum age of 3 days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="c38e8-119">La especificación de **UseMaxAge** agrega un encabezado `Cache-Control: max-age=<nnn>` a la respuesta basándose en el valor especificado en el atributo **CacheControlMaxAge**.</span><span class="sxs-lookup"><span data-stu-id="c38e8-119">Specifying **UseMaxAge** adds a `Cache-Control: max-age=<nnn>` header to the response based on the value specified in the **CacheControlMaxAge** attribute.</span></span> <span data-ttu-id="c38e8-120">El formato del intervalo de tiempo para el atributo **cacheControlMaxAge** es <days>.<hours>:<min>:<sec>.</span><span class="sxs-lookup"><span data-stu-id="c38e8-120">The format of the timespan is for the **cacheControlMaxAge** attribute is <days>.<hours>:<min>:<sec>.</span></span> <span data-ttu-id="c38e8-121">Para más información sobre el nodo **clientCache**, vea [Caché de cliente<clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span><span class="sxs-lookup"><span data-stu-id="c38e8-121">For more information on the **clientCache** node, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-in-code"></a><span data-ttu-id="c38e8-122">Establecimiento de los encabezados Cache-Control en el código</span><span class="sxs-lookup"><span data-stu-id="c38e8-122">Setting Cache-Control Headers in Code</span></span>
<span data-ttu-id="c38e8-123">Para las aplicaciones de ASP.NET, puede establecer el comportamiento de almacenamiento en caché CDN mediante programación estableciendo la propiedad **HttpResponse.Cache** .</span><span class="sxs-lookup"><span data-stu-id="c38e8-123">For ASP.NET applications, you can set the CDN caching behavior programmatically by setting the **HttpResponse.Cache** property.</span></span> <span data-ttu-id="c38e8-124">Para más información sobre la propiedad **HttpResponse.Cache**, vea [Propiedad HttpResponse.Cache](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) y [Clase HttpCachePolicy](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="c38e8-124">For more information on the **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="c38e8-125">Si desea almacenar en caché el contenido de la aplicación en ASP.NET mediante programación, asegúrese de que dicho contenido está marcado como almacenable en caché estableciendo HttpCacheability en *Public*.</span><span class="sxs-lookup"><span data-stu-id="c38e8-125">If you want to programmatically cache application content in ASP.NET, make sure that the content is marked as cacheable by setting HttpCacheability to *Public*.</span></span> <span data-ttu-id="c38e8-126">Asimismo, asegúrese de que se ha establecido un validador de caché.</span><span class="sxs-lookup"><span data-stu-id="c38e8-126">Also, ensure that a cache validator is set.</span></span> <span data-ttu-id="c38e8-127">El validador de caché puede ser un intervalo de tiempo de última modificación establecido llamando a SetLastModified, o un valor de etag establecido llamando a SetETag.</span><span class="sxs-lookup"><span data-stu-id="c38e8-127">The cache validator can be a Last Modified timestamp set by calling SetLastModified, or an etag value set by calling SetETag.</span></span> <span data-ttu-id="c38e8-128">Opcionalmente, también puede especificar un tiempo de expiración de caché llamando a SetExpires, o puede basarse en la heurística de caché predeterminada descrita anteriormente en este documento.</span><span class="sxs-lookup"><span data-stu-id="c38e8-128">Optionally, you can also specify a cache expiration time by calling SetExpires, or you can rely on the default cache heuristics described earlier in this document.</span></span>  

<span data-ttu-id="c38e8-129">Por ejemplo, para almacenar en caché el contenido durante una hora, agregue lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c38e8-129">For example, to cache content for one hour, add the following:</span></span>  

```csharp
// Set the caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a><span data-ttu-id="c38e8-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c38e8-130">Next Steps</span></span>
* [<span data-ttu-id="c38e8-131">Obtener información sobre el elemento **clientCache**</span><span class="sxs-lookup"><span data-stu-id="c38e8-131">Read details about the **clientCache** element</span></span>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [<span data-ttu-id="c38e8-132">Lea la documentación de la propiedad **HttpResponse.Cache**</span><span class="sxs-lookup"><span data-stu-id="c38e8-132">Read the documentation for the **HttpResponse.Cache** Property</span></span>](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* <span data-ttu-id="c38e8-133">[Lea la documentación de la **clase HttpCachePolicy**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="c38e8-133">[Read the documentation for the **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

