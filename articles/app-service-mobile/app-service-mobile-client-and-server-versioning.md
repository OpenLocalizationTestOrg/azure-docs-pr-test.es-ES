---
title: Control de versiones del SDK de cliente y servidor en Mobile Apps y Mobile Services | Microsoft Docs
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
ms.openlocfilehash: f79e819b1547f81498ea213858faf3c75e374782
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="19bc7-103">Control de versiones de cliente y servidor en Aplicaciones móviles y Servicios móviles</span><span class="sxs-lookup"><span data-stu-id="19bc7-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="19bc7-104">La versión más reciente de Servicios móviles de Azure es la característica **Aplicaciones móviles** del Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="19bc7-104">The latest version of Azure Mobile Services is the **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="19bc7-105">Los SDK de cliente y servidor de Aplicaciones móviles originalmente se basaban en los de Servicios móviles, pero *no* son compatibles entre sí.</span><span class="sxs-lookup"><span data-stu-id="19bc7-105">The Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="19bc7-106">Es decir, debe usar el SDK de cliente de *Mobile Apps* con un SDK de servidor de *Mobile Apps* y algo parecido sucede con *Mobile Services*.</span><span class="sxs-lookup"><span data-stu-id="19bc7-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="19bc7-107">Este contrato se aplica a través de un valor de encabezado especial usado por los SDK de cliente y servidor, `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="19bc7-107">This contract is enforced through a special header value used by the client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="19bc7-108">Nota: cada vez que este documento hace referencia a un back-end de *Servicios móviles* , no es necesario que esté hospedado en Servicios móviles.</span><span class="sxs-lookup"><span data-stu-id="19bc7-108">Note: whenever this document refers to a *Mobile Services* backend, it does not necessarily need to be hosted on Mobile Services.</span></span> <span data-ttu-id="19bc7-109">Ahora es posible migrar un servicio móvil para que se ejecute en App Service sin realizar ningún cambio en el código, pero el servicio seguirá usando versiones de SDK de *Mobile Services*.</span><span class="sxs-lookup"><span data-stu-id="19bc7-109">It is now possible to migrate a mobile service to run on App Service without any code changes, but the service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="19bc7-110">Para más información sobre la migración al Servicio de aplicaciones sin realizar ningún cambio en el código, consulte el artículo [Migrate your existing Azure mobile service to App Service].</span><span class="sxs-lookup"><span data-stu-id="19bc7-110">To learn more about migrating to App Service without any code changes, see the article [Migrate a Mobile Service to Azure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="19bc7-111">Especificación del encabezado</span><span class="sxs-lookup"><span data-stu-id="19bc7-111">Header specification</span></span>
<span data-ttu-id="19bc7-112">La clave `ZUMO-API-VERSION` se puede especificar en el encabezado HTTP o en la cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="19bc7-112">The key `ZUMO-API-VERSION` may be specified in either the HTTP header or the query string.</span></span> <span data-ttu-id="19bc7-113">El valor es una cadena de versión con el formato **x.y.z**.</span><span class="sxs-lookup"><span data-stu-id="19bc7-113">The value is a version string in the form **x.y.z**.</span></span>

<span data-ttu-id="19bc7-114">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="19bc7-114">For example:</span></span>

<span data-ttu-id="19bc7-115">GET https://service.azurewebsites.net/tables/TodoItem</span><span class="sxs-lookup"><span data-stu-id="19bc7-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="19bc7-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="19bc7-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="19bc7-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span><span class="sxs-lookup"><span data-stu-id="19bc7-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="19bc7-118">Anulación de la comprobación de la versión</span><span class="sxs-lookup"><span data-stu-id="19bc7-118">Opting out of version checking</span></span>
<span data-ttu-id="19bc7-119">Para anular la comprobación de la versión, establezca el valor **true** en la configuración de la aplicación **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="19bc7-119">You can opt out of version checking by setting a value of **true** for the app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="19bc7-120">Especifique esto en el archivo web.config o en la sección Configuración de la aplicación del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="19bc7-120">Specify this either in your web.config or in the Application Settings section of the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="19bc7-121">Hay una serie de cambios de comportamiento entre Servicios móviles y Aplicaciones móviles, especialmente en las áreas de sincronización sin conexión, autenticación y notificaciones push.</span><span class="sxs-lookup"><span data-stu-id="19bc7-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in the areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="19bc7-122">Solo debe anular la comprobación de versión después de realizar pruebas exhaustivas para asegurarse de que estos cambios de comportamiento no impiden la funcionalidad de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="19bc7-122">You should only opt out of version checking after complete testing to ensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="19bc7-123">Resumen de compatibilidad para todas las versiones</span><span class="sxs-lookup"><span data-stu-id="19bc7-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="19bc7-124">En la tabla siguiente se muestra la compatibilidad entre todos los tipos de cliente y servidor.</span><span class="sxs-lookup"><span data-stu-id="19bc7-124">The chart below shows the compatibility between all client and server types.</span></span> <span data-ttu-id="19bc7-125">Los back-ends se clasifican como Mobile **Services** o Mobile **Apps** en función del SDK de servidor que usan.</span><span class="sxs-lookup"><span data-stu-id="19bc7-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on the server SDK that it uses.</span></span>

|  | <span data-ttu-id="19bc7-126">**Servicios móviles** </span><span class="sxs-lookup"><span data-stu-id="19bc7-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="19bc7-127">**Aplicaciones móviles** </span><span class="sxs-lookup"><span data-stu-id="19bc7-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19bc7-128">[Clientes de Servicios móviles]</span><span class="sxs-lookup"><span data-stu-id="19bc7-128">[Mobile Services clients]</span></span> |<span data-ttu-id="19bc7-129">Aceptar</span><span class="sxs-lookup"><span data-stu-id="19bc7-129">Ok</span></span> |<span data-ttu-id="19bc7-130">Error\*</span><span class="sxs-lookup"><span data-stu-id="19bc7-130">Error\*</span></span> |
| <span data-ttu-id="19bc7-131">[Clientes de Aplicaciones móviles]</span><span class="sxs-lookup"><span data-stu-id="19bc7-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="19bc7-132">Error\*</span><span class="sxs-lookup"><span data-stu-id="19bc7-132">Error\*</span></span> |<span data-ttu-id="19bc7-133">Aceptar</span><span class="sxs-lookup"><span data-stu-id="19bc7-133">Ok</span></span> |

<span data-ttu-id="19bc7-134">\*Para controlarlo, especifique **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="19bc7-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  The anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: the fwlink to this document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="19bc7-135"><a name="1.0.0"></a>Cliente y servidor de Servicios móviles</span><span class="sxs-lookup"><span data-stu-id="19bc7-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="19bc7-136">Los SDK de cliente de la tabla siguiente son compatibles con **Servicios móviles**.</span><span class="sxs-lookup"><span data-stu-id="19bc7-136">The client SDKs in the table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="19bc7-137">Nota: los SDK de cliente de Mobile Services *no* envían un valor de encabezado de `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="19bc7-137">Note: the Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="19bc7-138">Si el servicio recibe este valor de encabezado o de cadena de consulta, se devolverá un error, a menos que lo haya anulado explícitamente como se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="19bc7-138">If the service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="19bc7-139"><a name="MobileServicesClients"></a> SDK de cliente de *Servicios* móviles</span><span class="sxs-lookup"><span data-stu-id="19bc7-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="19bc7-140">Plataforma de cliente</span><span class="sxs-lookup"><span data-stu-id="19bc7-140">Client platform</span></span> | <span data-ttu-id="19bc7-141">Versión</span><span class="sxs-lookup"><span data-stu-id="19bc7-141">Version</span></span> | <span data-ttu-id="19bc7-142">Valor de encabezado de versión</span><span class="sxs-lookup"><span data-stu-id="19bc7-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19bc7-143">Cliente administrado (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="19bc7-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="19bc7-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="19bc7-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="19bc7-145">N/D</span><span class="sxs-lookup"><span data-stu-id="19bc7-145">n/a</span></span> |
| <span data-ttu-id="19bc7-146">iOS</span><span class="sxs-lookup"><span data-stu-id="19bc7-146">iOS</span></span> |[<span data-ttu-id="19bc7-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="19bc7-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="19bc7-148">N/D</span><span class="sxs-lookup"><span data-stu-id="19bc7-148">n/a</span></span> |
| <span data-ttu-id="19bc7-149">Android</span><span class="sxs-lookup"><span data-stu-id="19bc7-149">Android</span></span> |[<span data-ttu-id="19bc7-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="19bc7-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="19bc7-151">N/D</span><span class="sxs-lookup"><span data-stu-id="19bc7-151">n/a</span></span> |
| <span data-ttu-id="19bc7-152">HTML</span><span class="sxs-lookup"><span data-stu-id="19bc7-152">HTML</span></span> |[<span data-ttu-id="19bc7-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="19bc7-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="19bc7-154">N/D</span><span class="sxs-lookup"><span data-stu-id="19bc7-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="19bc7-155">SDK de servidor de *Servicios* móviles</span><span class="sxs-lookup"><span data-stu-id="19bc7-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="19bc7-156">Plataforma de servidor</span><span class="sxs-lookup"><span data-stu-id="19bc7-156">Server platform</span></span> | <span data-ttu-id="19bc7-157">Versión</span><span class="sxs-lookup"><span data-stu-id="19bc7-157">Version</span></span> | <span data-ttu-id="19bc7-158">Encabezado de versión aceptado</span><span class="sxs-lookup"><span data-stu-id="19bc7-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19bc7-159">.NET</span><span class="sxs-lookup"><span data-stu-id="19bc7-159">.NET</span></span> |[<span data-ttu-id="19bc7-160">WindowsAzure.MobileServices.Backend.* Versión 1.0.x</span><span class="sxs-lookup"><span data-stu-id="19bc7-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="19bc7-161">** Ningún encabezado de versión **</span><span class="sxs-lookup"><span data-stu-id="19bc7-161">**No version header **</span></span> |
| <span data-ttu-id="19bc7-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="19bc7-162">Node.js</span></span> |<span data-ttu-id="19bc7-163">(próximamente)</span><span class="sxs-lookup"><span data-stu-id="19bc7-163">(coming soon)</span></span> |<span data-ttu-id="19bc7-164">**Ningún encabezado de versión**</span><span class="sxs-lookup"><span data-stu-id="19bc7-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="19bc7-165">Comportamiento de back-ends de Servicios móviles</span><span class="sxs-lookup"><span data-stu-id="19bc7-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="19bc7-166">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="19bc7-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="19bc7-167">Valor de MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="19bc7-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="19bc7-168">Response</span><span class="sxs-lookup"><span data-stu-id="19bc7-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19bc7-169">Sin especificar</span><span class="sxs-lookup"><span data-stu-id="19bc7-169">Not specified</span></span> |<span data-ttu-id="19bc7-170">Cualquiera</span><span class="sxs-lookup"><span data-stu-id="19bc7-170">Any</span></span> |<span data-ttu-id="19bc7-171">200 - CORRECTO</span><span class="sxs-lookup"><span data-stu-id="19bc7-171">200 - OK</span></span> |
| <span data-ttu-id="19bc7-172">Cualquier valor</span><span class="sxs-lookup"><span data-stu-id="19bc7-172">Any value</span></span> |<span data-ttu-id="19bc7-173">True</span><span class="sxs-lookup"><span data-stu-id="19bc7-173">True</span></span> |<span data-ttu-id="19bc7-174">200 - CORRECTO</span><span class="sxs-lookup"><span data-stu-id="19bc7-174">200 - OK</span></span> |
| <span data-ttu-id="19bc7-175">Cualquier valor</span><span class="sxs-lookup"><span data-stu-id="19bc7-175">Any value</span></span> |<span data-ttu-id="19bc7-176">False/Sin especificar</span><span class="sxs-lookup"><span data-stu-id="19bc7-176">False/Not Specified</span></span> |<span data-ttu-id="19bc7-177">400 - Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="19bc7-177">400 - Bad Request</span></span> |

## <span data-ttu-id="19bc7-178"><a name="2.0.0"></a>Cliente y servidor de Aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="19bc7-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="19bc7-179"><a name="MobileAppsClients"></a> SDK de cliente de *Aplicaciones* móviles</span><span class="sxs-lookup"><span data-stu-id="19bc7-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="19bc7-180">La comprobación de versión se introdujo a partir de las siguientes versiones del SDK de cliente de **Aplicaciones móviles de Azure**:</span><span class="sxs-lookup"><span data-stu-id="19bc7-180">Version checking was introduced starting with the following versions of the client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="19bc7-181">Plataforma de cliente</span><span class="sxs-lookup"><span data-stu-id="19bc7-181">Client platform</span></span> | <span data-ttu-id="19bc7-182">Versión</span><span class="sxs-lookup"><span data-stu-id="19bc7-182">Version</span></span> | <span data-ttu-id="19bc7-183">Valor de encabezado de versión</span><span class="sxs-lookup"><span data-stu-id="19bc7-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19bc7-184">Cliente administrado (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="19bc7-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="19bc7-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="19bc7-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="19bc7-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="19bc7-186">2.0.0</span></span> |
| <span data-ttu-id="19bc7-187">iOS</span><span class="sxs-lookup"><span data-stu-id="19bc7-187">iOS</span></span> |[<span data-ttu-id="19bc7-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="19bc7-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="19bc7-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="19bc7-189">2.0.0</span></span> |
| <span data-ttu-id="19bc7-190">Android</span><span class="sxs-lookup"><span data-stu-id="19bc7-190">Android</span></span> |[<span data-ttu-id="19bc7-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="19bc7-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="19bc7-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="19bc7-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="19bc7-193">SDK de servidor de *Aplicaciones* móviles</span><span class="sxs-lookup"><span data-stu-id="19bc7-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="19bc7-194">La comprobación de versión se incluye en las siguientes versiones del SDK de servidor:</span><span class="sxs-lookup"><span data-stu-id="19bc7-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="19bc7-195">Plataforma de servidor</span><span class="sxs-lookup"><span data-stu-id="19bc7-195">Server platform</span></span> | <span data-ttu-id="19bc7-196">SDK</span><span class="sxs-lookup"><span data-stu-id="19bc7-196">SDK</span></span> | <span data-ttu-id="19bc7-197">Encabezado de versión aceptado</span><span class="sxs-lookup"><span data-stu-id="19bc7-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19bc7-198">.NET</span><span class="sxs-lookup"><span data-stu-id="19bc7-198">.NET</span></span> |[<span data-ttu-id="19bc7-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="19bc7-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="19bc7-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="19bc7-200">2.0.0</span></span> |
| <span data-ttu-id="19bc7-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="19bc7-201">Node.js</span></span> |[<span data-ttu-id="19bc7-202">azure-mobile-apps)</span><span class="sxs-lookup"><span data-stu-id="19bc7-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="19bc7-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="19bc7-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="19bc7-204">Comportamiento de back-ends de Aplicaciones móviles</span><span class="sxs-lookup"><span data-stu-id="19bc7-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="19bc7-205">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="19bc7-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="19bc7-206">Valor de MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="19bc7-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="19bc7-207">Response</span><span class="sxs-lookup"><span data-stu-id="19bc7-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19bc7-208">x.y.z o Null</span><span class="sxs-lookup"><span data-stu-id="19bc7-208">x.y.z or Null</span></span> |<span data-ttu-id="19bc7-209">True</span><span class="sxs-lookup"><span data-stu-id="19bc7-209">True</span></span> |<span data-ttu-id="19bc7-210">200 - CORRECTO</span><span class="sxs-lookup"><span data-stu-id="19bc7-210">200 - OK</span></span> |
| <span data-ttu-id="19bc7-211">Null</span><span class="sxs-lookup"><span data-stu-id="19bc7-211">Null</span></span> |<span data-ttu-id="19bc7-212">False/Sin especificar</span><span class="sxs-lookup"><span data-stu-id="19bc7-212">False/Not Specified</span></span> |<span data-ttu-id="19bc7-213">400 - Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="19bc7-213">400 - Bad Request</span></span> |
| <span data-ttu-id="19bc7-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="19bc7-214">1.x.y</span></span> |<span data-ttu-id="19bc7-215">False/Sin especificar</span><span class="sxs-lookup"><span data-stu-id="19bc7-215">False/Not Specified</span></span> |<span data-ttu-id="19bc7-216">400 - Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="19bc7-216">400 - Bad Request</span></span> |
| <span data-ttu-id="19bc7-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="19bc7-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="19bc7-218">False/Sin especificar</span><span class="sxs-lookup"><span data-stu-id="19bc7-218">False/Not Specified</span></span> |<span data-ttu-id="19bc7-219">200 - CORRECTO</span><span class="sxs-lookup"><span data-stu-id="19bc7-219">200 - OK</span></span> |
| <span data-ttu-id="19bc7-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="19bc7-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="19bc7-221">False/Sin especificar</span><span class="sxs-lookup"><span data-stu-id="19bc7-221">False/Not Specified</span></span> |<span data-ttu-id="19bc7-222">400 - Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="19bc7-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="19bc7-223">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="19bc7-223">Next Steps</span></span>
* <span data-ttu-id="19bc7-224">[Migrate your existing Azure mobile service to App Service]</span><span class="sxs-lookup"><span data-stu-id="19bc7-224">[Migrate a Mobile Service to Azure App Service]</span></span>

<span data-ttu-id="19bc7-225">[Clientes de Servicios móviles]: #MobileServicesClients</span><span class="sxs-lookup"><span data-stu-id="19bc7-225">[Mobile Services clients]: #MobileServicesClients</span></span>
<span data-ttu-id="19bc7-226">[Clientes de Aplicaciones móviles]: #MobileAppsClients</span><span class="sxs-lookup"><span data-stu-id="19bc7-226">[Mobile Apps clients]: #MobileAppsClients</span></span>


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
<span data-ttu-id="19bc7-227">[Migrate your existing Azure mobile service to App Service]: app-service-mobile-migrating-from-mobile-services.md</span><span class="sxs-lookup"><span data-stu-id="19bc7-227">[Migrate a Mobile Service to Azure App Service]: app-service-mobile-migrating-from-mobile-services.md</span></span>
