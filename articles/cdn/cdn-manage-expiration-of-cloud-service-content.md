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
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a>Administración de la caducidad del contenido de Azure Web Apps/Cloud Services, ASP.NET o IIS en la red CDN de Azure
> [!div class="op_single_selector"]
> * [Azure Web Apps/Cloud Services, ASP.NET o IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Azure Storage Blob service](cdn-manage-expiration-of-blob-content.md)
> 
> 

Los archivos de cualquier servidor web de origen accesible públicamente se pueden almacenar en caché en la red CDN de Azure hasta que transcurra su tiempo de vida (TTL).  Hello TTL determina hello [ *Cache-Control* encabezado](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) en respuesta de hello HTTP del servidor de origen de Hola.  Este artículo se describe cómo tooset `Cache-Control` encabezados para aplicaciones Web de Azure, servicios en la nube, las aplicaciones ASP.NET y sitios de Internet Information Services, todos ellos se configuran de forma similar.

> [!TIP]
> No puede elegir tooset ningún período de vida de un archivo.  En este caso, la red CDN de Azure aplica automáticamente un valor predeterminado de TTL de siete días.
> 
> Para obtener más información sobre cómo funciona la toospeed toofiles de acceso y otros recursos de la red CDN de Azure, vea hello [información general sobre la red CDN de Azure](cdn-overview.md).
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a>Establecimiento de los encabezados Cache-Control en la configuración
Para contenido estático, como imágenes y hojas de estilos, puede controlar frecuencia de actualización de hello modificando hello **applicationHost.config** o **web.config** archivos de la aplicación web.  Hola **system.webServer\staticContent\clientCache** elemento en el archivo de configuración de hello establecerá hello `Cache-Control` encabezado para su contenido. Para **web.config**, Hola configuración configuración afectará a todos los elementos en la carpeta de Hola y todas sus subcarpetas, a menos que se reemplaza en el nivel de la subcarpeta de Hola.  Por ejemplo, puede establecer un valor predeterminado time-to-live en hello raíz toohave todo el contenido estático en memoria caché durante tres días, pero tiene una subcarpeta que tiene más variable contenido con una configuración de caché de 6 horas.  Para **applicationHost.config**, todas las aplicaciones en el sitio de Hola se verán afectadas, pero pueden invalidarse en **web.config** archivos en aplicaciones de Hola.

Hello siguiente XML muestra un ejemplo de configuración **clientCache** toospecify una antigüedad máxima de 3 días:  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

Especificar **UseMaxAge** agrega un `Cache-Control: max-age=<nnn>` respuesta toohello de encabezado se basa en valor de hello especificado en hello **CacheControlMaxAge** atributo. formato de Hola de timespan hello es para hello **cacheControlMaxAge** atributo es <days>.<hours>:<min>:<sec>. Para obtener más información sobre hello **clientCache** nodo, consulte [memoria caché del cliente <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).  

## <a name="setting-cache-control-headers-in-code"></a>Establecimiento de los encabezados Cache-Control en el código
Para las aplicaciones ASP.NET, puede establecer comportamiento de almacenamiento en caché de CDN Hola mediante programación por establecer hello **HttpResponse.Cache** propiedad. Para obtener más información sobre hello **HttpResponse.Cache** propiedad, vea [propiedad HttpResponse.Cache](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) y [clase HttpCachePolicy](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).  

Si desea que el contenido de la aplicación tooprogrammatically caché de ASP.NET, asegúrese de que el contenido de Hola se marca como almacenable en caché debe establecer HttpCacheability demasiado*público*. Asimismo, asegúrese de que se ha establecido un validador de caché. Validador de caché de Hello puede ser una última modificación marca de tiempo establecido mediante una llamada a SetLastModified o bien un valor etag, se establece llamando a SetETag. Si lo desea, también puede especificar una hora de expiración de caché mediante una llamada a SetExpires o puede basarse en la heurística de caché predeterminada de hello descrita anteriormente en este documento.  

Por ejemplo, toocache contenido durante una hora, agregue Hola siguiente:  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a>Pasos siguientes
* [Leer detalles de hello **clientCache** elemento](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [Leer documentación Hola Hola **HttpResponse.Cache** propiedad](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* [Leer documentación Hola Hola **clase HttpCachePolicy**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).  

