---
title: "versiones SDK aaaClient y el servidor de aplicaciones móviles y servicios móviles | Documentos de Microsoft"
description: "Lista de SDK de cliente y compatibilidad con versiones de SDK de servidor para Servicios móviles y Aplicaciones móviles de Azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="e807c-103">Control de versiones de cliente y servidor en Aplicaciones móviles y Servicios móviles</span><span class="sxs-lookup"><span data-stu-id="e807c-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="e807c-104">versión más reciente de Hello de servicios móviles de Azure es hello **aplicaciones móviles** característica del servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="e807c-104">hello latest version of Azure Mobile Services is hello **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="e807c-105">Hola cliente de aplicaciones móviles y SDK de servidor originalmente se basa en los de servicios móviles, pero son *no* compatibles entre sí.</span><span class="sxs-lookup"><span data-stu-id="e807c-105">hello Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="e807c-106">Es decir, debe usar el SDK de cliente de *Mobile Apps* con un SDK de servidor de *Mobile Apps* y algo parecido sucede con *Mobile Services*.</span><span class="sxs-lookup"><span data-stu-id="e807c-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="e807c-107">Este contrato se establece a través de un valor de encabezado especial utilizado por hello cliente y servidor de SDK, `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="e807c-107">This contract is enforced through a special header value used by hello client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="e807c-108">Nota: cada vez que este documento hace referencia tooa *servicios móviles* back-end, no es necesario toobe hospedada en servicios móviles.</span><span class="sxs-lookup"><span data-stu-id="e807c-108">Note: whenever this document refers tooa *Mobile Services* backend, it does not necessarily need toobe hosted on Mobile Services.</span></span> <span data-ttu-id="e807c-109">Ahora es posible toomigrate un toorun de servicio móvil en el servicio de aplicaciones sin realizar ningún cambio en el código, pero todavía sería utilizar el servicio de hello *servicios móviles* versiones del SDK.</span><span class="sxs-lookup"><span data-stu-id="e807c-109">It is now possible toomigrate a mobile service toorun on App Service without any code changes, but hello service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="e807c-110">toolearn Obtenga más información sobre migración tooApp servicio sin realizar ningún cambio de código, vea el artículo de hello [migrar un servicio de aplicaciones de servicio móvil tooAzure].</span><span class="sxs-lookup"><span data-stu-id="e807c-110">toolearn more about migrating tooApp Service without any code changes, see hello article [Migrate a Mobile Service tooAzure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="e807c-111">Especificación del encabezado</span><span class="sxs-lookup"><span data-stu-id="e807c-111">Header specification</span></span>
<span data-ttu-id="e807c-112">clave de Hello `ZUMO-API-VERSION` se pueden especificar en el encabezado HTTP de Hola o de cadena de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e807c-112">hello key `ZUMO-API-VERSION` may be specified in either hello HTTP header or hello query string.</span></span> <span data-ttu-id="e807c-113">valor de Hello es una cadena de versión en forma de hello **x.y.z**.</span><span class="sxs-lookup"><span data-stu-id="e807c-113">hello value is a version string in hello form **x.y.z**.</span></span>

<span data-ttu-id="e807c-114">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e807c-114">For example:</span></span>

<span data-ttu-id="e807c-115">GET https://service.azurewebsites.net/tables/TodoItem</span><span class="sxs-lookup"><span data-stu-id="e807c-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="e807c-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="e807c-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="e807c-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span><span class="sxs-lookup"><span data-stu-id="e807c-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="e807c-118">Anulación de la comprobación de la versión</span><span class="sxs-lookup"><span data-stu-id="e807c-118">Opting out of version checking</span></span>
<span data-ttu-id="e807c-119">Puede optar por comprobación estableciendo el valor de la versión **true** para la configuración de la aplicación hello **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="e807c-119">You can opt out of version checking by setting a value of **true** for hello app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="e807c-120">Especifique en el archivo web.config o en la sección de configuración de la aplicación de portal de Azure Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="e807c-120">Specify this either in your web.config or in hello Application Settings section of hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="e807c-121">Hay una serie de cambios de comportamiento entre servicios móviles y aplicaciones móviles, especialmente en las áreas de Hola de sincronización sin conexión, la autenticación y las notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="e807c-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in hello areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="e807c-122">Solo debe rechazar comprobación después de tooensure prueba completa que estos cambios de comportamiento no interrumpe la funcionalidad de la aplicación de la versión.</span><span class="sxs-lookup"><span data-stu-id="e807c-122">You should only opt out of version checking after complete testing tooensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="e807c-123">Resumen de compatibilidad para todas las versiones</span><span class="sxs-lookup"><span data-stu-id="e807c-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="e807c-124">gráfico de Hello siguiente muestra la compatibilidad de hello entre todos los tipos de cliente y servidor.</span><span class="sxs-lookup"><span data-stu-id="e807c-124">hello chart below shows hello compatibility between all client and server types.</span></span> <span data-ttu-id="e807c-125">Un back-end se clasifica como cualquier Mobile **servicios** o Mobile **aplicaciones** basado en servidor hello SDK que utiliza.</span><span class="sxs-lookup"><span data-stu-id="e807c-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on hello server SDK that it uses.</span></span>

|  | <span data-ttu-id="e807c-126">**Servicios móviles**</span><span class="sxs-lookup"><span data-stu-id="e807c-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="e807c-127">**Aplicaciones móviles**</span><span class="sxs-lookup"><span data-stu-id="e807c-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e807c-128">[Clientes de Servicios móviles]</span><span class="sxs-lookup"><span data-stu-id="e807c-128">[Mobile Services clients]</span></span> |<span data-ttu-id="e807c-129">Aceptar</span><span class="sxs-lookup"><span data-stu-id="e807c-129">Ok</span></span> |<span data-ttu-id="e807c-130">Error\*</span><span class="sxs-lookup"><span data-stu-id="e807c-130">Error\*</span></span> |
| <span data-ttu-id="e807c-131">[Clientes de Aplicaciones móviles]</span><span class="sxs-lookup"><span data-stu-id="e807c-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="e807c-132">Error\*</span><span class="sxs-lookup"><span data-stu-id="e807c-132">Error\*</span></span> |<span data-ttu-id="e807c-133">Aceptar</span><span class="sxs-lookup"><span data-stu-id="e807c-133">Ok</span></span> |

<span data-ttu-id="e807c-134">\*Para controlarlo, especifique **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="e807c-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="e807c-135"><a name="1.0.0"></a>Cliente y servidor de Servicios móviles</span><span class="sxs-lookup"><span data-stu-id="e807c-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="e807c-136">SDK de cliente de Hello en tabla Hola siguiente son compatibles con **servicios móviles**.</span><span class="sxs-lookup"><span data-stu-id="e807c-136">hello client SDKs in hello table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="e807c-137">Nota: Hola SDK de cliente de servicios móviles *no* enviar un valor de encabezado `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="e807c-137">Note: hello Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="e807c-138">Si el servicio de hello recibe este encabezado o el valor de cadena de consulta, se devolverá un error, a menos que explícitamente optó por tal y como se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e807c-138">If hello service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="e807c-139"><a name="MobileServicesClients"></a> SDK de cliente de *Servicios* móviles</span><span class="sxs-lookup"><span data-stu-id="e807c-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="e807c-140">Plataforma de cliente</span><span class="sxs-lookup"><span data-stu-id="e807c-140">Client platform</span></span> | <span data-ttu-id="e807c-141">Versión</span><span class="sxs-lookup"><span data-stu-id="e807c-141">Version</span></span> | <span data-ttu-id="e807c-142">Valor de encabezado de versión</span><span class="sxs-lookup"><span data-stu-id="e807c-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e807c-143">Cliente administrado (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="e807c-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="e807c-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="e807c-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="e807c-145">N/D</span><span class="sxs-lookup"><span data-stu-id="e807c-145">n/a</span></span> |
| <span data-ttu-id="e807c-146">iOS</span><span class="sxs-lookup"><span data-stu-id="e807c-146">iOS</span></span> |[<span data-ttu-id="e807c-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="e807c-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="e807c-148">N/D</span><span class="sxs-lookup"><span data-stu-id="e807c-148">n/a</span></span> |
| <span data-ttu-id="e807c-149">Android</span><span class="sxs-lookup"><span data-stu-id="e807c-149">Android</span></span> |[<span data-ttu-id="e807c-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="e807c-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="e807c-151">N/D</span><span class="sxs-lookup"><span data-stu-id="e807c-151">n/a</span></span> |
| <span data-ttu-id="e807c-152">HTML</span><span class="sxs-lookup"><span data-stu-id="e807c-152">HTML</span></span> |[<span data-ttu-id="e807c-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="e807c-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="e807c-154">N/D</span><span class="sxs-lookup"><span data-stu-id="e807c-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="e807c-155">SDK de servidor de *Servicios* móviles</span><span class="sxs-lookup"><span data-stu-id="e807c-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="e807c-156">Plataforma de servidor</span><span class="sxs-lookup"><span data-stu-id="e807c-156">Server platform</span></span> | <span data-ttu-id="e807c-157">Versión</span><span class="sxs-lookup"><span data-stu-id="e807c-157">Version</span></span> | <span data-ttu-id="e807c-158">Encabezado de versión aceptado</span><span class="sxs-lookup"><span data-stu-id="e807c-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e807c-159">.NET</span><span class="sxs-lookup"><span data-stu-id="e807c-159">.NET</span></span> |[<span data-ttu-id="e807c-160">WindowsAzure.MobileServices.Backend.* Versión 1.0.x</span><span class="sxs-lookup"><span data-stu-id="e807c-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="e807c-161">** Ningún encabezado de versión **</span><span class="sxs-lookup"><span data-stu-id="e807c-161">**No version header **</span></span> |
| <span data-ttu-id="e807c-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="e807c-162">Node.js</span></span> |<span data-ttu-id="e807c-163">(próximamente)</span><span class="sxs-lookup"><span data-stu-id="e807c-163">(coming soon)</span></span> |<span data-ttu-id="e807c-164">**Ningún encabezado de versión**</span><span class="sxs-lookup"><span data-stu-id="e807c-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="e807c-165">Comportamiento de back-ends de Servicios móviles</span><span class="sxs-lookup"><span data-stu-id="e807c-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="e807c-166">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="e807c-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="e807c-167">Valor de MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="e807c-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="e807c-168">Response</span><span class="sxs-lookup"><span data-stu-id="e807c-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e807c-169">Sin especificar</span><span class="sxs-lookup"><span data-stu-id="e807c-169">Not specified</span></span> |<span data-ttu-id="e807c-170">Cualquiera</span><span class="sxs-lookup"><span data-stu-id="e807c-170">Any</span></span> |<span data-ttu-id="e807c-171">200 - CORRECTO</span><span class="sxs-lookup"><span data-stu-id="e807c-171">200 - OK</span></span> |
| <span data-ttu-id="e807c-172">Cualquier valor</span><span class="sxs-lookup"><span data-stu-id="e807c-172">Any value</span></span> |<span data-ttu-id="e807c-173">True</span><span class="sxs-lookup"><span data-stu-id="e807c-173">True</span></span> |<span data-ttu-id="e807c-174">200 - CORRECTO</span><span class="sxs-lookup"><span data-stu-id="e807c-174">200 - OK</span></span> |
| <span data-ttu-id="e807c-175">Cualquier valor</span><span class="sxs-lookup"><span data-stu-id="e807c-175">Any value</span></span> |<span data-ttu-id="e807c-176">False/Sin especificar</span><span class="sxs-lookup"><span data-stu-id="e807c-176">False/Not Specified</span></span> |<span data-ttu-id="e807c-177">400 - Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="e807c-177">400 - Bad Request</span></span> |

## <span data-ttu-id="e807c-178"><a name="2.0.0"></a>Cliente y servidor de Aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="e807c-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="e807c-179"><a name="MobileAppsClients"></a> SDK de cliente de *Aplicaciones* móviles</span><span class="sxs-lookup"><span data-stu-id="e807c-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="e807c-180">Comprobación de la versión se incorpora a partir de hello después de las versiones de SDK de cliente de Hola para **aplicaciones móviles de Azure**:</span><span class="sxs-lookup"><span data-stu-id="e807c-180">Version checking was introduced starting with hello following versions of hello client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="e807c-181">Plataforma de cliente</span><span class="sxs-lookup"><span data-stu-id="e807c-181">Client platform</span></span> | <span data-ttu-id="e807c-182">Versión</span><span class="sxs-lookup"><span data-stu-id="e807c-182">Version</span></span> | <span data-ttu-id="e807c-183">Valor de encabezado de versión</span><span class="sxs-lookup"><span data-stu-id="e807c-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e807c-184">Cliente administrado (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="e807c-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="e807c-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="e807c-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="e807c-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="e807c-186">2.0.0</span></span> |
| <span data-ttu-id="e807c-187">iOS</span><span class="sxs-lookup"><span data-stu-id="e807c-187">iOS</span></span> |[<span data-ttu-id="e807c-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="e807c-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="e807c-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="e807c-189">2.0.0</span></span> |
| <span data-ttu-id="e807c-190">Android</span><span class="sxs-lookup"><span data-stu-id="e807c-190">Android</span></span> |[<span data-ttu-id="e807c-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="e807c-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="e807c-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="e807c-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="e807c-193">SDK de servidor de *Aplicaciones* móviles</span><span class="sxs-lookup"><span data-stu-id="e807c-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="e807c-194">La comprobación de versión se incluye en las siguientes versiones del SDK de servidor:</span><span class="sxs-lookup"><span data-stu-id="e807c-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="e807c-195">Plataforma de servidor</span><span class="sxs-lookup"><span data-stu-id="e807c-195">Server platform</span></span> | <span data-ttu-id="e807c-196">SDK</span><span class="sxs-lookup"><span data-stu-id="e807c-196">SDK</span></span> | <span data-ttu-id="e807c-197">Encabezado de versión aceptado</span><span class="sxs-lookup"><span data-stu-id="e807c-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e807c-198">.NET</span><span class="sxs-lookup"><span data-stu-id="e807c-198">.NET</span></span> |[<span data-ttu-id="e807c-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="e807c-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="e807c-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="e807c-200">2.0.0</span></span> |
| <span data-ttu-id="e807c-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="e807c-201">Node.js</span></span> |[<span data-ttu-id="e807c-202">azure-mobile-apps)</span><span class="sxs-lookup"><span data-stu-id="e807c-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="e807c-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="e807c-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="e807c-204">Comportamiento de back-ends de Aplicaciones móviles</span><span class="sxs-lookup"><span data-stu-id="e807c-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="e807c-205">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="e807c-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="e807c-206">Valor de MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="e807c-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="e807c-207">Response</span><span class="sxs-lookup"><span data-stu-id="e807c-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e807c-208">x.y.z o Null</span><span class="sxs-lookup"><span data-stu-id="e807c-208">x.y.z or Null</span></span> |<span data-ttu-id="e807c-209">True</span><span class="sxs-lookup"><span data-stu-id="e807c-209">True</span></span> |<span data-ttu-id="e807c-210">200 - CORRECTO</span><span class="sxs-lookup"><span data-stu-id="e807c-210">200 - OK</span></span> |
| <span data-ttu-id="e807c-211">Null</span><span class="sxs-lookup"><span data-stu-id="e807c-211">Null</span></span> |<span data-ttu-id="e807c-212">False/Sin especificar</span><span class="sxs-lookup"><span data-stu-id="e807c-212">False/Not Specified</span></span> |<span data-ttu-id="e807c-213">400 - Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="e807c-213">400 - Bad Request</span></span> |
| <span data-ttu-id="e807c-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="e807c-214">1.x.y</span></span> |<span data-ttu-id="e807c-215">False/Sin especificar</span><span class="sxs-lookup"><span data-stu-id="e807c-215">False/Not Specified</span></span> |<span data-ttu-id="e807c-216">400 - Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="e807c-216">400 - Bad Request</span></span> |
| <span data-ttu-id="e807c-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="e807c-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="e807c-218">False/Sin especificar</span><span class="sxs-lookup"><span data-stu-id="e807c-218">False/Not Specified</span></span> |<span data-ttu-id="e807c-219">200 - CORRECTO</span><span class="sxs-lookup"><span data-stu-id="e807c-219">200 - OK</span></span> |
| <span data-ttu-id="e807c-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="e807c-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="e807c-221">False/Sin especificar</span><span class="sxs-lookup"><span data-stu-id="e807c-221">False/Not Specified</span></span> |<span data-ttu-id="e807c-222">400 - Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="e807c-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e807c-223">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e807c-223">Next Steps</span></span>
* <span data-ttu-id="e807c-224">[migrar un servicio de aplicaciones de servicio móvil tooAzure]</span><span class="sxs-lookup"><span data-stu-id="e807c-224">[Migrate a Mobile Service tooAzure App Service]</span></span>

[Clientes de Servicios móviles]: #MobileServicesClients
[Clientes de Aplicaciones móviles]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[migrar un servicio de aplicaciones de servicio móvil tooAzure]: app-service-mobile-migrating-from-mobile-services.md
