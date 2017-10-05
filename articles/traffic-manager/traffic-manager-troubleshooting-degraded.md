---
title: "Solución de problemas de estado degradado en Administrador de tráfico de Azure"
description: "Cómo solucionar problemas de perfiles de Administrador de tráfico cuando se muestra como muestra un estado degradado."
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
ms.openlocfilehash: b1d00fb84695d2289f37647f55a7c56cf28c8c96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="9b45e-103">Solución de problemas de estado degradado en el Administrador de tráfico de Azure</span><span class="sxs-lookup"><span data-stu-id="9b45e-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="9b45e-104">En este artículo se describe cómo solucionar problemas de un perfil de Azure Traffic Manager que muestra un estado degradado.</span><span class="sxs-lookup"><span data-stu-id="9b45e-104">This article describes how to troubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="9b45e-105">Para este escenario, considere que ha configurado un perfil de Traffic Manager orientado a algunos de sus servicios hospedados cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="9b45e-105">For this scenario, consider that you have configured a Traffic Manager profile pointing to some of your cloudapp.net hosted services.</span></span> <span data-ttu-id="9b45e-106">Si el estado de su instancia de Traffic Manager muestra **Degradado**, entonces el estado de uno o varios puntos de conexión puede ser **Degradado**:</span><span class="sxs-lookup"><span data-stu-id="9b45e-106">If the health of your Traffic Manager displays a **Degraded** status, then the status of one or more endpoints may be **Degraded**:</span></span>

![estado de punto de conexión degradado](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="9b45e-108">Si el estado de su instancia de Traffic Manager muestra **Inactivo**, ambos puntos de conexión pueden estar **deshabilitados**:</span><span class="sxs-lookup"><span data-stu-id="9b45e-108">If the health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![Estado inactivo de Traffic Manager](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="9b45e-110">Descripción de los sondeos de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="9b45e-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="9b45e-111">Traffic Manager considera que un punto de conexión está EN LÍNEA solo cuando el sondeo recibe una respuesta HTTP 200 desde la ruta de acceso del sondeo.</span><span class="sxs-lookup"><span data-stu-id="9b45e-111">Traffic Manager considers an endpoint to be ONLINE only when the probe receives an HTTP 200 response back from the probe path.</span></span> <span data-ttu-id="9b45e-112">Cualquier otra respuesta que no sea la respuesta 200 es un error.</span><span class="sxs-lookup"><span data-stu-id="9b45e-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="9b45e-113">Un redireccionamiento 30x producirá un error incluso si la dirección URL redirigida devuelve una respuesta 200.</span><span class="sxs-lookup"><span data-stu-id="9b45e-113">A 30x redirect fails, even if the redirected URL returns a 200.</span></span>
* <span data-ttu-id="9b45e-114">En los sondeos HTTPs, se omiten los errores de certificado.</span><span class="sxs-lookup"><span data-stu-id="9b45e-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="9b45e-115">No importa el contenido real de la ruta de acceso del sondeo, siempre y cuando se devuelva una respuesta 200.</span><span class="sxs-lookup"><span data-stu-id="9b45e-115">The actual content of the probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="9b45e-116">Realizar un sondeo de una dirección URL en algún contenido estático, como "/favicon.ico" es una técnica habitual.</span><span class="sxs-lookup"><span data-stu-id="9b45e-116">Probing a URL to some static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="9b45e-117">Los contenidos dinámicos, como las páginas ASP, puede que no siempre devuelvan una respuesta 200, incluso si la aplicación está en buen estado.</span><span class="sxs-lookup"><span data-stu-id="9b45e-117">Dynamic content, like the ASP pages, may not always return 200, even when the application is healthy.</span></span>
* <span data-ttu-id="9b45e-118">Un procedimiento recomendado consiste en establecer la ruta de acceso del sondeo en algo que tenga una lógica suficiente para determinar si el sitio está activo o inactivo.</span><span class="sxs-lookup"><span data-stu-id="9b45e-118">A best practice is to set the Probe path to something that has enough logic to determine that the site is up or down.</span></span> <span data-ttu-id="9b45e-119">En el ejemplo anterior, al establecer la ruta de acceso en "/favicon.ico", solo prueba que w3wp.exe está respondiendo.</span><span class="sxs-lookup"><span data-stu-id="9b45e-119">In the previous example, by setting the path to "/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="9b45e-120">Puede que este sondeo no indique que la aplicación web está funcionando correctamente.</span><span class="sxs-lookup"><span data-stu-id="9b45e-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="9b45e-121">Sería una mejor opción establecer una ruta de acceso a algo como "/Probe.aspx" que tiene lógica para determinar el estado del sitio.</span><span class="sxs-lookup"><span data-stu-id="9b45e-121">A better option would be to set a path to a something such as "/Probe.aspx" that has logic to determine the health of the site.</span></span> <span data-ttu-id="9b45e-122">Por ejemplo, podría usar contadores de rendimiento para medir el uso de la CPU o el número de solicitudes con error.</span><span class="sxs-lookup"><span data-stu-id="9b45e-122">For example, you could use performance counters to CPU utilization or measure the number of failed requests.</span></span> <span data-ttu-id="9b45e-123">O bien, podría intentar acceder a los recursos de la base de datos o al estado de la sesión para asegurarse de que la aplicación web funciona.</span><span class="sxs-lookup"><span data-stu-id="9b45e-123">Or you could attempt to access database resources or session state to make sure that the web application is working.</span></span>
* <span data-ttu-id="9b45e-124">Si se degradan todos los puntos de conexión de un perfil, Traffic Manager los tratará a todos como correctos y enrutará el tráfico a todos ellos.</span><span class="sxs-lookup"><span data-stu-id="9b45e-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic to all endpoints.</span></span> <span data-ttu-id="9b45e-125">Este comportamiento garantiza que los problemas con el mecanismo de sondeo no darán lugar a una interrupción completa del servicio.</span><span class="sxs-lookup"><span data-stu-id="9b45e-125">This behavior ensures that problems with the probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9b45e-126">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="9b45e-126">Troubleshooting</span></span>

<span data-ttu-id="9b45e-127">Para solucionar un error de sondeo, necesita una herramienta que muestre el código de estado HTTP devuelto desde la dirección URL de sondeo.</span><span class="sxs-lookup"><span data-stu-id="9b45e-127">To troubleshoot a probe failure, you need a tool that shows the HTTP status code return from the probe URL.</span></span> <span data-ttu-id="9b45e-128">Hay muchas herramientas disponibles que le muestran la respuesta HTTP sin formato.</span><span class="sxs-lookup"><span data-stu-id="9b45e-128">There are many tools available that show you the raw HTTP response.</span></span>

* [<span data-ttu-id="9b45e-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="9b45e-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="9b45e-130">curl</span><span class="sxs-lookup"><span data-stu-id="9b45e-130">curl</span></span>](https://curl.haxx.se/)
* [<span data-ttu-id="9b45e-131">wget</span><span class="sxs-lookup"><span data-stu-id="9b45e-131">wget</span></span>](http://gnuwin32.sourceforge.net/packages/wget.htm)

<span data-ttu-id="9b45e-132">Además, puede usar la pestaña Red de las herramientas de depuración de F12 de Internet Explorer para ver las respuestas HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b45e-132">Also, you can use the Network tab of the F12 Debugging Tools in Internet Explorer to view the HTTP responses.</span></span>

<span data-ttu-id="9b45e-133">En este ejemplo queremos ver la respuesta de la dirección URL de sondeo: http://watestsdp2008r2.cloudapp.net:80/Probe.</span><span class="sxs-lookup"><span data-stu-id="9b45e-133">For this example we want to see the response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="9b45e-134">El siguiente ejemplo de PowerShell ilustra el problema.</span><span class="sxs-lookup"><span data-stu-id="9b45e-134">The following PowerShell example illustrates the problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="9b45e-135">Salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9b45e-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="9b45e-136">Observe que hemos recibido una respuesta de redirección.</span><span class="sxs-lookup"><span data-stu-id="9b45e-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="9b45e-137">Como se indicó anteriormente, cualquier StatusCode distinto de 200 se considera un error.</span><span class="sxs-lookup"><span data-stu-id="9b45e-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="9b45e-138">Traffic Manager cambia el estado de punto de conexión a Sin conexión.</span><span class="sxs-lookup"><span data-stu-id="9b45e-138">Traffic Manager changes the endpoint status to Offline.</span></span> <span data-ttu-id="9b45e-139">Para resolver el problema, compruebe la configuración del sitio web para asegurarse de que se puede devolver el StatusCode apropiado desde la ruta de acceso del sondeo.</span><span class="sxs-lookup"><span data-stu-id="9b45e-139">To resolve the problem, check the website configuration to ensure that the proper StatusCode can be returned from the probe path.</span></span> <span data-ttu-id="9b45e-140">Vuelva a configurar el sondeo de Traffic Manager para que señale a una ruta de acceso que devuelva una respuesta 200.</span><span class="sxs-lookup"><span data-stu-id="9b45e-140">Reconfigure the Traffic Manager probe to point to a path that returns a 200.</span></span>

<span data-ttu-id="9b45e-141">Si el sondeo usa el protocolo HTTPS, es posible que tenga que deshabilitar la comprobación de certificados para evitar errores SSL/TLS durante la prueba.</span><span class="sxs-lookup"><span data-stu-id="9b45e-141">If your probe is using the HTTPS protocol, you may need to disable certificate checking to avoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="9b45e-142">Las siguientes instrucciones de PowerShell deshabilitan la validación de certificados para la sesión actual de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9b45e-142">The following PowerShell statements disable certificate validation for the current PowerShell session:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9b45e-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b45e-143">Next Steps</span></span>

[<span data-ttu-id="9b45e-144">Información acerca de los métodos de enrutamiento del tráfico del Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="9b45e-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="9b45e-145">¿Qué es el Administrador de tráfico?</span><span class="sxs-lookup"><span data-stu-id="9b45e-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="9b45e-146">Servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="9b45e-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="9b45e-147">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="9b45e-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="9b45e-148">Operaciones del Administrador de tráfico (referencia de la API de REST)</span><span class="sxs-lookup"><span data-stu-id="9b45e-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="9b45e-149">[Cmdlets de Azure Traffic Manager][1]</span><span class="sxs-lookup"><span data-stu-id="9b45e-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
