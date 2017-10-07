---
title: aaaTroubleshooting muestra un estado degradado en Azure Traffic Manager
description: "¿Cómo tootroubleshoot perfiles de Traffic Manager cuando muestra como muestra un estado degradan."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
ms.assetid: 8af0433d-e61b-4761-adcc-7bc9b8142fc6
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: kumud
ms.openlocfilehash: fd95697781472b52e98d856e66beb7b89dfeaf23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="873c7-103">Solución de problemas de estado degradado en el Administrador de tráfico de Azure</span><span class="sxs-lookup"><span data-stu-id="873c7-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="873c7-104">Este artículo describe cómo tootroubleshoot un perfil de Traffic Manager de Azure que muestra un estado degradado.</span><span class="sxs-lookup"><span data-stu-id="873c7-104">This article describes how tootroubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="873c7-105">En este escenario, considere la posibilidad de que se haya configurado un perfil de Traffic Manager que apunte toosome de los servicios hospedados de cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="873c7-105">For this scenario, consider that you have configured a Traffic Manager profile pointing toosome of your cloudapp.net hosted services.</span></span> <span data-ttu-id="873c7-106">Si se muestra el estado de su administrador de tráfico de Hola un **degradado** estado, estado de Hola de uno o más extremos puede ser **degradado**:</span><span class="sxs-lookup"><span data-stu-id="873c7-106">If hello health of your Traffic Manager displays a **Degraded** status, then hello status of one or more endpoints may be **Degraded**:</span></span>

![estado de punto de conexión degradado](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="873c7-108">Si se muestra el estado de su administrador de tráfico de Hola un **inactivo** estado, los dos puntos finales pueden ser **deshabilitado**:</span><span class="sxs-lookup"><span data-stu-id="873c7-108">If hello health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![Estado inactivo de Traffic Manager](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="873c7-110">Descripción de los sondeos de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="873c7-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="873c7-111">El Administrador de tráfico se considera un toobe de punto de conexión en línea sólo al sondeo de hello recibe una respuesta HTTP 200 hacer copia de ruta de acceso de sondeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="873c7-111">Traffic Manager considers an endpoint toobe ONLINE only when hello probe receives an HTTP 200 response back from hello probe path.</span></span> <span data-ttu-id="873c7-112">Cualquier otra respuesta que no sea la respuesta 200 es un error.</span><span class="sxs-lookup"><span data-stu-id="873c7-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="873c7-113">Una redirección de 30 x se produce un error, incluso si Hola había redirigido URL devuelve 200.</span><span class="sxs-lookup"><span data-stu-id="873c7-113">A 30x redirect fails, even if hello redirected URL returns a 200.</span></span>
* <span data-ttu-id="873c7-114">En los sondeos HTTPs, se omiten los errores de certificado.</span><span class="sxs-lookup"><span data-stu-id="873c7-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="873c7-115">No importa el contenido real de Hola de ruta de acceso de sondeo de hello, siempre y cuando se devuelve 200.</span><span class="sxs-lookup"><span data-stu-id="873c7-115">hello actual content of hello probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="873c7-116">Búsqueda de un tipo de contenido estático de toosome de dirección URL "/ favicon.ico" es una técnica común.</span><span class="sxs-lookup"><span data-stu-id="873c7-116">Probing a URL toosome static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="873c7-117">Contenido dinámico, como páginas de ASP de hello, no puede devolver siempre 200, incluso cuando la aplicación hello es correcto.</span><span class="sxs-lookup"><span data-stu-id="873c7-117">Dynamic content, like hello ASP pages, may not always return 200, even when hello application is healthy.</span></span>
* <span data-ttu-id="873c7-118">Una práctica recomendada es tooset Hola sondeo toosomething de ruta de acceso que tiene suficiente toodetermine lógica que Hola sitio es hacia arriba o hacia abajo.</span><span class="sxs-lookup"><span data-stu-id="873c7-118">A best practice is tooset hello Probe path toosomething that has enough logic toodetermine that hello site is up or down.</span></span> <span data-ttu-id="873c7-119">Hola ejemplo anterior, estableciendo Hola too"/favicon.ico de ruta de acceso", sólo son pruebas que w3wp.exe está respondiendo.</span><span class="sxs-lookup"><span data-stu-id="873c7-119">In hello previous example, by setting hello path too"/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="873c7-120">Puede que este sondeo no indique que la aplicación web está funcionando correctamente.</span><span class="sxs-lookup"><span data-stu-id="873c7-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="873c7-121">Una mejor opción sería tooset una ruta de acceso tooa algo como "/ Probe.aspx" que tiene el estado de hello toodetermine de lógica de sitio de Hola.</span><span class="sxs-lookup"><span data-stu-id="873c7-121">A better option would be tooset a path tooa something such as "/Probe.aspx" that has logic toodetermine hello health of hello site.</span></span> <span data-ttu-id="873c7-122">Por ejemplo, podría utilizar el uso de tooCPU de contadores de rendimiento o medida Hola número de solicitudes con error.</span><span class="sxs-lookup"><span data-stu-id="873c7-122">For example, you could use performance counters tooCPU utilization or measure hello number of failed requests.</span></span> <span data-ttu-id="873c7-123">O bien, podría intentar tooaccess recursos de base de datos o toomake de estado de sesión seguro de que la aplicación web de hello funciona.</span><span class="sxs-lookup"><span data-stu-id="873c7-123">Or you could attempt tooaccess database resources or session state toomake sure that hello web application is working.</span></span>
* <span data-ttu-id="873c7-124">Si se degradan todos los extremos de un perfil, a continuación, el Administrador de tráfico trata todos los extremos como correcto y las rutas de tráfico tooall extremos.</span><span class="sxs-lookup"><span data-stu-id="873c7-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic tooall endpoints.</span></span> <span data-ttu-id="873c7-125">Este comportamiento garantiza que los problemas con hello mecanismo de búsqueda no dan lugar a una interrupción completa de su servicio.</span><span class="sxs-lookup"><span data-stu-id="873c7-125">This behavior ensures that problems with hello probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="873c7-126">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="873c7-126">Troubleshooting</span></span>

<span data-ttu-id="873c7-127">tootroubleshoot un error de sondeo, necesita una herramienta que muestra código de estado HTTP de hello devuelto desde la dirección URL de sondeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="873c7-127">tootroubleshoot a probe failure, you need a tool that shows hello HTTP status code return from hello probe URL.</span></span> <span data-ttu-id="873c7-128">Hay numerosas herramientas disponibles que muestran Hola respuesta HTTP sin formato.</span><span class="sxs-lookup"><span data-stu-id="873c7-128">There are many tools available that show you hello raw HTTP response.</span></span>

* [<span data-ttu-id="873c7-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="873c7-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="873c7-130">curl</span><span class="sxs-lookup"><span data-stu-id="873c7-130">curl</span></span>](https://curl.haxx.se/)
* [<span data-ttu-id="873c7-131">wget</span><span class="sxs-lookup"><span data-stu-id="873c7-131">wget</span></span>](http://gnuwin32.sourceforge.net/packages/wget.htm)

<span data-ttu-id="873c7-132">Además, puede utilizar la pestaña de la red de Hola de hello F12 las herramientas de depuración en las respuestas HTTP de Internet Explorer tooview Hola.</span><span class="sxs-lookup"><span data-stu-id="873c7-132">Also, you can use hello Network tab of hello F12 Debugging Tools in Internet Explorer tooview hello HTTP responses.</span></span>

<span data-ttu-id="873c7-133">En este ejemplo queremos respuesta de hello toosee desde la dirección URL de sondeo: http://watestsdp2008r2.cloudapp.net:80/sondeo.</span><span class="sxs-lookup"><span data-stu-id="873c7-133">For this example we want toosee hello response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="873c7-134">Hola PowerShell ejemplo siguiente ilustra el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="873c7-134">hello following PowerShell example illustrates hello problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="873c7-135">Salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="873c7-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="873c7-136">Observe que hemos recibido una respuesta de redirección.</span><span class="sxs-lookup"><span data-stu-id="873c7-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="873c7-137">Como se indicó anteriormente, cualquier StatusCode distinto de 200 se considera un error.</span><span class="sxs-lookup"><span data-stu-id="873c7-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="873c7-138">Cambios en el Administrador de tráfico Hola tooOffline de estado de punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="873c7-138">Traffic Manager changes hello endpoint status tooOffline.</span></span> <span data-ttu-id="873c7-139">problema de hello tooresolve, verificación Hola sitio Web configuración tooensure que Hola StatusCode adecuado puede devolverse de ruta de acceso de sondeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="873c7-139">tooresolve hello problem, check hello website configuration tooensure that hello proper StatusCode can be returned from hello probe path.</span></span> <span data-ttu-id="873c7-140">Volver a configurar Hola Traffic Manager sondeo toopoint tooa ruta de acceso que devuelve 200.</span><span class="sxs-lookup"><span data-stu-id="873c7-140">Reconfigure hello Traffic Manager probe toopoint tooa path that returns a 200.</span></span>

<span data-ttu-id="873c7-141">Si el sondeo usa Hola protocolo HTTPS, debe certificado toodisable comprobación de errores SSL/TLS tooavoid durante la prueba.</span><span class="sxs-lookup"><span data-stu-id="873c7-141">If your probe is using hello HTTPS protocol, you may need toodisable certificate checking tooavoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="873c7-142">Hello instrucciones siguientes de PowerShell deshabilitar la validación de certificados para la sesión actual de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="873c7-142">hello following PowerShell statements disable certificate validation for hello current PowerShell session:</span></span>

```powershell
add-type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckValidationResult(
    ServicePoint srvPoint, X509Certificate certificate,
    WebRequest request, int certificateProblem) {
    return true;
    }
}
"@
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
```

## <a name="next-steps"></a><span data-ttu-id="873c7-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="873c7-143">Next Steps</span></span>

[<span data-ttu-id="873c7-144">Información acerca de los métodos de enrutamiento del tráfico del Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="873c7-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="873c7-145">¿Qué es el Administrador de tráfico?</span><span class="sxs-lookup"><span data-stu-id="873c7-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="873c7-146">Servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="873c7-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="873c7-147">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="873c7-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="873c7-148">Operaciones del Administrador de tráfico (referencia de la API de REST)</span><span class="sxs-lookup"><span data-stu-id="873c7-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="873c7-149">[Cmdlets de Azure Traffic Manager][1]</span><span class="sxs-lookup"><span data-stu-id="873c7-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
