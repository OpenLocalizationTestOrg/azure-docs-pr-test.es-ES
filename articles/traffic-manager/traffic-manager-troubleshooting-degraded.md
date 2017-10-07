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
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a>Solución de problemas de estado degradado en el Administrador de tráfico de Azure

Este artículo describe cómo tootroubleshoot un perfil de Traffic Manager de Azure que muestra un estado degradado. En este escenario, considere la posibilidad de que se haya configurado un perfil de Traffic Manager que apunte toosome de los servicios hospedados de cloudapp.net. Si se muestra el estado de su administrador de tráfico de Hola un **degradado** estado, estado de Hola de uno o más extremos puede ser **degradado**:

![estado de punto de conexión degradado](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

Si se muestra el estado de su administrador de tráfico de Hola un **inactivo** estado, los dos puntos finales pueden ser **deshabilitado**:

![Estado inactivo de Traffic Manager](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a>Descripción de los sondeos de Traffic Manager

* El Administrador de tráfico se considera un toobe de punto de conexión en línea sólo al sondeo de hello recibe una respuesta HTTP 200 hacer copia de ruta de acceso de sondeo de Hola. Cualquier otra respuesta que no sea la respuesta 200 es un error.
* Una redirección de 30 x se produce un error, incluso si Hola había redirigido URL devuelve 200.
* En los sondeos HTTPs, se omiten los errores de certificado.
* No importa el contenido real de Hola de ruta de acceso de sondeo de hello, siempre y cuando se devuelve 200. Búsqueda de un tipo de contenido estático de toosome de dirección URL "/ favicon.ico" es una técnica común. Contenido dinámico, como páginas de ASP de hello, no puede devolver siempre 200, incluso cuando la aplicación hello es correcto.
* Una práctica recomendada es tooset Hola sondeo toosomething de ruta de acceso que tiene suficiente toodetermine lógica que Hola sitio es hacia arriba o hacia abajo. Hola ejemplo anterior, estableciendo Hola too"/favicon.ico de ruta de acceso", sólo son pruebas que w3wp.exe está respondiendo. Puede que este sondeo no indique que la aplicación web está funcionando correctamente. Una mejor opción sería tooset una ruta de acceso tooa algo como "/ Probe.aspx" que tiene el estado de hello toodetermine de lógica de sitio de Hola. Por ejemplo, podría utilizar el uso de tooCPU de contadores de rendimiento o medida Hola número de solicitudes con error. O bien, podría intentar tooaccess recursos de base de datos o toomake de estado de sesión seguro de que la aplicación web de hello funciona.
* Si se degradan todos los extremos de un perfil, a continuación, el Administrador de tráfico trata todos los extremos como correcto y las rutas de tráfico tooall extremos. Este comportamiento garantiza que los problemas con hello mecanismo de búsqueda no dan lugar a una interrupción completa de su servicio.

## <a name="troubleshooting"></a>Solución de problemas

tootroubleshoot un error de sondeo, necesita una herramienta que muestra código de estado HTTP de hello devuelto desde la dirección URL de sondeo de Hola. Hay numerosas herramientas disponibles que muestran Hola respuesta HTTP sin formato.

* [Fiddler](http://www.telerik.com/fiddler)
* [curl](https://curl.haxx.se/)
* [wget](http://gnuwin32.sourceforge.net/packages/wget.htm)

Además, puede utilizar la pestaña de la red de Hola de hello F12 las herramientas de depuración en las respuestas HTTP de Internet Explorer tooview Hola.

En este ejemplo queremos respuesta de hello toosee desde la dirección URL de sondeo: http://watestsdp2008r2.cloudapp.net:80/sondeo. Hola PowerShell ejemplo siguiente ilustra el problema de Hola.

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

Salida de ejemplo:

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

Observe que hemos recibido una respuesta de redirección. Como se indicó anteriormente, cualquier StatusCode distinto de 200 se considera un error. Cambios en el Administrador de tráfico Hola tooOffline de estado de punto de conexión. problema de hello tooresolve, verificación Hola sitio Web configuración tooensure que Hola StatusCode adecuado puede devolverse de ruta de acceso de sondeo de Hola. Volver a configurar Hola Traffic Manager sondeo toopoint tooa ruta de acceso que devuelve 200.

Si el sondeo usa Hola protocolo HTTPS, debe certificado toodisable comprobación de errores SSL/TLS tooavoid durante la prueba. Hello instrucciones siguientes de PowerShell deshabilitar la validación de certificados para la sesión actual de PowerShell de hello:

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

## <a name="next-steps"></a>Pasos siguientes

[Información acerca de los métodos de enrutamiento del tráfico del Administrador de tráfico](traffic-manager-routing-methods.md)

[¿Qué es el Administrador de tráfico?](traffic-manager-overview.md)

[Servicios en la nube](http://go.microsoft.com/fwlink/?LinkId=314074)

[Azure Web Apps](https://azure.microsoft.com/documentation/services/app-service/web/)

[Operaciones del Administrador de tráfico (referencia de la API de REST)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Cmdlets de Azure Traffic Manager][1]

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
