---
title: "aaaConfiguration de administración - herramienta de modelado de amenazas de Microsoft - Azure | Documentos de Microsoft"
description: mitigaciones en busca de amenazas que se exponen en hello herramienta de modelado de amenazas
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 77aa4352fa61e928a1b7a4ff1d488a55d3d9b970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-configuration-management--mitigations"></a>Marco de seguridad: Administración de configuración | Mitigaciones 
| Producto o servicio | Artículo |
| --------------- | ------- |
| **Aplicación web** | <ul><li>[Implementación de la directiva de seguridad de contenido [CSP] y deshabilitación de Javascript en línea](#csp-js)</li><li>[Habilitación del filtro XSS del explorador](#xss-filter)</li><li>[Las aplicaciones de ASP.NET deben deshabilitar el seguimiento y depuración toodeployment anterior](#trace-deploy)</li><li>[Acceso exclusivo a archivos JavaScript de terceros de orígenes de confianza](#js-trusted)</li><li>[Comprobación de que las páginas con autenticación con ASP.NET incorporan defensas contra el secuestro de clic](#ui-defenses)</li><li>[Comprobación de que solo se permiten orígenes de confianza si CORS está activado en las aplicaciones web ASP.NET](#cors-aspnet)</li><li>[Habilitación del atributo ValidateRequest en las páginas de ASP.NET](#validate-aspnet)</li><li>[Uso de las últimas versiones locales de las bibliotecas de JavaScript](#local-js)</li><li>[Deshabilitación del rastreo automático de MIME](#mime-sniff)</li><li>[Quitar encabezados estándar del servidor en sitios Web Windows Azure tooavoid huellas digitales](#standard-finger)</li></ul> |
| **Base de datos** | <ul><li>[Configuración de Firewall de Windows para el acceso al motor de base de datos](#firewall-db)</li></ul> |
| **API web** | <ul><li>[Comprobación de que solo se permiten orígenes de confianza si CORS está activado en ASP.NET Web API](#cors-api)</li><li>[Cifrado de secciones de los archivos de configuración de la API web que contienen datos confidenciales](#config-sensitive)</li></ul> |
| **Dispositivo de IoT** | <ul><li>[Comprobación de que todas las interfaces de administración están protegidas con credenciales seguras](#admin-strong)</li><li>[Comprobación de que no se puede ejecutar código desconocido en los dispositivos](#unknown-exe)</li><li>[Cifrado del sistema operativo y particiones adicionales en los dispositivos IoT con Bitlocker](#partition-iot)</li><li>[Asegúrese de que solo Hola mínimo servicios o características están habilitadas en los dispositivos](#min-enable)</li></ul> |
| **Puerta de enlace de campo de IoT** | <ul><li>[Cifrado del sistema operativo y particiones adicionales en la puerta de enlace de campo de IoT con Bitlocker](#field-bit-locker)</li><li>[Asegúrese de que las credenciales de inicio de sesión predeterminado de Hola de puerta de enlace de campo de Hola se cambian durante la instalación](#default-change)</li></ul> |
| **Puerta de enlace de nube de IoT** | <ul><li>[Asegurarse de que esa puerta de enlace de nube Hola implementa un firmware de dispositivos de proceso tookeep Hola conectado seguridad toodate](#cloud-firmware)</li></ul> |
| **Límite de confianza de la máquina** | <ul><li>[Comprobación de que los dispositivos tienen controles de seguridad de punto de conexión configurados según las directivas organizativas](#controls-policies)</li></ul> |
| **Azure Storage** | <ul><li>[Comprobación de la administración segura de las claves de acceso de almacenamiento de Azure](#secure-keys)</li><li>[Comprobación de que solo se permiten orígenes de confianza si CORS está activado en Azure Storage](#cors-storage)</li></ul> |
| **WCF** | <ul><li>[Habilitación de la característica de limitación del servicio de WCF](#throttling)</li><li>[Revelación de información de WCF mediante metadatos](#info-metadata)</li></ul> | 

## <a id="csp-js"></a>Implementación de la directiva de seguridad de contenido [CSP] y deshabilitación de Javascript en línea

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Una directiva de seguridad de introducción tooContent](http://www.html5rocks.com/en/tutorials/security/content-security-policy/), [referencia de directivas de seguridad contenido](http://content-security-policy.com/), [características de seguridad](https://developer.microsoft.com/microsoft-edge/platform/documentation/dev-guide/security/), [directiva de seguridad de introducción toocontent](https://docs.webplatform.org/wiki/tutorials/content-security-policy), [¿Puedo usar CSP?](http://caniuse.com/#feat=contentsecuritypolicy) |
| **Pasos** | <p>Directiva de seguridad de contenido (CSP) es un defensa en profundidad mecanismo de seguridad, un W3C estándar, que habilita el control de web application propietarios toohave en el contenido de hello incrustado en su sitio. Se agrega como un encabezado de respuesta HTTP en el servidor web de Hola y se aplica en el lado del cliente de hello exploradores CSP. Es una directiva basada en una lista blanca: un sitio web puede declarar un conjunto de dominios de confianza desde los que se puede cargar contenido activo, como JavaScript.</p><p>CSP proporciona Hola siguiendo las ventajas de seguridad:</p><ul><li>**Protección frente a XSS:** si una página es tooXSS vulnerable, un atacante puede aprovechar en 2 formas:<ul><li>Insertando `<script>malicious code</script>`. Esta vulnerabilidad de seguridad no funcionará debido del tooCSP Base restricción-1</li><li>Insertando `<script src=”http://attacker.com/maliciousCode.js”/>`. Esta vulnerabilidad de seguridad no funcionará como dominio de hello controlada por el atacante no estará en la lista blanca de direcciones del CSP de dominios</li></ul></li><li>**Control sobre datos decir:** si cualquier contenido malintencionado en una página Web intenta tooconnect sitio Web externo de tooan y robar datos, la conexión de Hola se anulará por CSP. Esto es porque el dominio de destino de hello no estarán en la lista blanca de direcciones del CSP</li><li>**Defensa contra levantamiento haga clic en:** levantamiento de clic es una técnica de ataque con la que un adversario puede enmarcar un sitio Web original y forzar tooclick de usuarios en los elementos de interfaz de usuario. La defensa actual contra el secuestro de clic se consigue mediante la configuración de un encabezado de respuesta X-Frame-Option. No todos los exploradores respetan este encabezado y va hacia delante CSP será un toodefend de manera estándar con levantamiento haga clic en</li><li>**Informes de ataques en tiempo real:** si se produce un ataque de inyección de código en un sitio Web habilitado para CSP, exploradores desencadenará automáticamente un punto de conexión de notificación tooan configurado en el servidor Web de Hola. De esta manera, la CSP actúa como sistema de advertencia en tiempo real.</li></ul> |

### <a name="example"></a>Ejemplo
Ejemplo de directiva: 
```C#
Content-Security-Policy: default-src 'self'; script-src 'self' www.google-analytics.com 
```
Esta directiva permite tooload scripts solo desde la aplicación hello web server y servidor de google analytics. Se rechazarán los scripts que se carguen desde cualquier otro sitio. Cuando se habilita el CSP en un sitio Web, hello características siguientes son los ataques XSS de toomitigate deshabilitado automáticamente. 

### <a name="example"></a>Ejemplo
Los scripts en línea no se ejecutarán. Ejemplos de scripts en línea 
```javascript
<script> some Javascript code </script>
Event handling attributes of HTML tags (e.g., <button onclick=”function(){}”>
javascript:alert(1);
```

### <a name="example"></a>Ejemplo
Las cadenas no se evaluarán como código. 
```javascript
Example: var str="alert(1)"; eval(str);
```

## <a id="xss-filter"></a>Habilitación del filtro XSS del explorador

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Filtro de protección de XSS](https://www.owasp.org/index.php/List_of_useful_HTTP_headers#X-XSS-Protection) |
| **Pasos** | <p>Controles de configuración del encabezado de respuesta X-XSS-protección Hola filtro de script entre sitios del explorador. Este encabezado de respuesta puede tener los siguientes valores:</p><ul><li>`0:`Esto deshabilitará el filtro de Hola</li><li>`1: Filter enabled`Si se detecta un ataque XSS, de ataque de orden toostop hello, Explorador de Hola sanear página Hola</li><li>`1: mode=block : Filter enabled`. En lugar de sanear página hello, cuando se detecta un ataque XSS, Explorador de hello, se evitará la representación de página Hola</li><li>`1: report=http://[YOURDOMAIN]/your_report_URI : Filter enabled`. Explorador de Hola sanear infracción de Hola de página y el informe de Hola.</li></ul><p>Se trata de una función de cromo utilizando CSP infracción informes toosend detalles tooa URI de su elección. Hello 2 últimas opciones se consideran valores seguros.</p>|

## <a id="trace-deploy"></a>Las aplicaciones de ASP.NET deben deshabilitar el seguimiento y depuración toodeployment anterior

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Introducción a la depuración en ASP.NET](http://msdn2.microsoft.com/library/ms227556.aspx), [Introducción al seguimiento en ASP.NET](http://msdn2.microsoft.com/library/bb386420.aspx), [Cómo: Habilitar el seguimiento de una aplicación ASP.NET](http://msdn2.microsoft.com/library/0x5wc973.aspx), [Cómo: Habilitar la depuración de aplicaciones de ASP.NET](http://msdn2.microsoft.com/library/e8z01xdh(VS.80).aspx) |
| **Pasos** | Si se habilita el seguimiento para la página de hello, cada explorador solicita que también obtiene información de seguimiento de Hola que contiene datos sobre el estado interno del servidor y flujo de trabajo. Esta información podría ser confidencial. Cuando está habilitada la depuración para la página de hello, errores en los resultados del servidor hello en los datos de seguimiento de pila completo está pasando lo presentan toohello explorador. Esos datos pueden exponer información confidencial de seguridad sobre el flujo de trabajo del servidor de Hola. |

## <a id="js-trusted"></a>Acceso exclusivo a archivos JavaScript de terceros de orígenes de confianza

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | debe hacerse referencia a archivos JavaScript de terceros únicamente desde orígenes de confianza. los puntos de conexión de referencia de Hello deberían estar siempre encendido SSL. |

## <a id="ui-defenses"></a>Comprobación de que las páginas con autenticación con ASP.NET incorporan defensas contra el secuestro de clic

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [OWASP click-jacking Defense Cheat Sheet](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet) (Hoja de referencia rápida de OWASP sobre la defensa ante el secuestro de clic), [IE Internals - Combating click-jacking With X-Frame-Options](https://blogs.msdn.microsoft.com/ieinternals/2010/03/30/combating-click-jacking-with-x-frame-options/) (Elementos internos de Internet Explorer: combatir el secuestro de clic con X-Frame-Options) |
| **Pasos** | <p>Haga clic en-levantamiento, también conocido como "ataque de reparación de la interfaz de usuario," es cuando un atacante usa varias capas transparente u opaco tootrick un usuario al hacer clic en un botón o vínculo en otra página cuando se objetivo es tooclick en la página de nivel superior de Hola.</p><p>Estas capas se logra al elaborar una página con un iframe, que carga la página de la víctima de hello malintencionada. Por lo tanto, atacante hello es "" apropiación hace clic en destinada a su página y enrutarlas a página tooanother, más probable es que pertenecen a otra aplicación, dominio o ambas cosas. tooprevent levantamiento haga clic en los ataques, conjunto Hola apropiado X-Frame-Options encabezados de respuesta HTTP que indicar a Hola explorador toonot permiten tramas de otros dominios</p>|

### <a name="example"></a>Ejemplo
encabezado X-FRAME-OPTIONS de Hello puede establecerse a través de web.config de IIS. Fragmento de código de web.config para los sitios que nunca deben enmarcarse: 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="DENY"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

### <a name="example"></a>Ejemplo
Código de Web.config para los sitios que solo debe ser enmarcada por páginas de hello mismo dominio: 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="SAMEORIGIN"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

## <a id="cors-aspnet"></a>Comprobación de que solo se permiten orígenes de confianza si CORS está activado en las aplicaciones web ASP.NET

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Formularios Web Forms, MVC5 |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>Seguridad del explorador impide que una página web realice ningún dominio de tooanother de solicitudes de AJAX. Esta restricción se denomina directiva de mismo origen de Hola e impide que un sitio malintencionado pueda leer los datos confidenciales desde otro sitio. Sin embargo, en ocasiones puede que sea necesario tooexpose las API de forma segura que es compatible con otros sitios. Entre recursos de uso compartido a orígenes (CORS) es un estándar de W3C que permite que un servidor de directiva de mismo origen de toorelax Hola. Con CORS, un servidor puede permitir explícitamente algunas solicitudes de origen cruzado y rechazar otras.</p><p>CORS es más seguro y más flexible que las técnicas anteriores, como JSONP. En esencia, habilitación de CORS traduce tooadding algunos encabezados de respuesta HTTP (acceso - Control-*) toohello y la aplicación web esto pueden hacerse de dos maneras.</p>|

### <a name="example"></a>Ejemplo
Si hay disponible acceso tooWeb.config, CORS pueden agregarse mediante Hola siguiente código: 
```XML
<system.webServer>
    <httpProtocol>
      <customHeaders>
        <clear />
        <add name="Access-Control-Allow-Origin" value="http://example.com" />
      </customHeaders>
    </httpProtocol>
```

### <a name="example"></a>Ejemplo
Si tooweb.config de acceso no está disponible, CORS puede configurarse mediante la adición de hello sigue CSharp código: 
```C#
HttpContext.Response.AppendHeader("Access-Control-Allow-Origin", "http://example.com")
```

Tenga en cuenta que es crítica tooensure que Hola lista de orígenes de atributo de "Acceso Access-Control-Allow-Origin" se establezca tooa conjunto finito y de confianza de orígenes. Errores tooconfigure este inapropiada (p. ej., el valor de hello como ' *') le permitirá sitios malintencionados tootrigger solicitudes de origen entre aplicaciones de web toohello > sin restricciones, haciéndolos Hola aplicación vulnerable tooCSRF ataques. 

## <a id="validate-aspnet"></a>Habilitación del atributo ValidateRequest en las páginas de ASP.NET

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Formularios Web Forms, MVC5 |
| **Atributos**              | N/D  |
| **Referencias**              | [Request Validation - Preventing Script Attacks](http://www.asp.net/whitepapers/request-validation) (Validación de solicitudes: prevención de ataques de script) |
| **Pasos** | <p>Validación de solicitudes, una característica de ASP.NET desde la versión 1.1, impide que el servidor hello acepte contenido HTML sin codificar que lo contiene. Esta característica está diseñada toohelp evitar algunos ataques de inyección de script mediante el cual HTML o código de script de cliente puede ser enviado sin saberlo tooa server, almacena y, a continuación, presenta tooother a los usuarios. Se recomienda encarecidamente validar todos los datos de entrada y codificar el código HTML cuando corresponda.</p><p>Validación de solicitudes se realiza comparando todos los datos de entrada tooa lista de valores potencialmente peligrosos. Si se produce una coincidencia, ASP.NET genera un `HttpRequestValidationException`. De forma predeterminada, la característica de validación de solicitudes está habilitada.</p>|

### <a name="example"></a>Ejemplo
Sin embargo, se puede deshabilitar en el nivel de página: 
```XML
<%@ Page validateRequest="false" %> 
```
o en el nivel de aplicación 
```XML
<configuration>
   <system.web>
      <pages validateRequest="false" />
   </system.web>
</configuration>
```
Tenga en cuenta que esta característica de validación de solicitud no es compatible con la canalización de MVC6 ni forma parte de esta. 

## <a id="local-js"></a>Uso de las últimas versiones locales de las bibliotecas de JavaScript

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>Los desarrolladores que utilizan bibliotecas estándar de JavaScript como JQuery deben usar versiones aprobadas de las bibliotecas de JavaScript comunes sin errores de seguridad conocidos. Una práctica recomendada es toouse hello más última versión de las bibliotecas de hello, ya que contienen las revisiones de seguridad para las vulnerabilidades conocidas de sus versiones anteriores.</p><p>Si no se puede usar la versión más reciente de hello debido a razones toocompatibility, se debe usar Hola por debajo de las versiones mínimas.</p><p>Versiones mínimas aceptables:</p><ul><li>**JQuery**<ul><li>JQuery 1.7.1</li><li>JQueryUI 1.10.0</li><li>JQuery Validate 1.9</li><li>JQuery Mobile 1.0.1</li><li>JQuery Cycle 2.99</li><li>JQuery DataTables 1.9.0</li></ul></li><li>**Ajax Control Toolkit**<ul><li>Ajax Control Toolkit 40412</li></ul></li><li>**ASP.NET Web Forms and Ajax**<ul><li>ASP.NET Web Forms and Ajax 4</li><li>ASP.NET Ajax 3.5</li></ul></li><li>**ASP.NET MVC**<ul><li>ASP.NET MVC 3.0</li></ul></li></ul><p>No cargue nunca bibliotecas de JavaScript desde sitios externos, como redes CDN públicas</p>|

## <a id="mime-sniff"></a>Deshabilitación del rastreo automático de MIME

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [IE8 Security Part V - Comprehensive Protection](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx) (Seguridad de IE8 [parte V]: protección total), [tipos de MIME](http://en.wikipedia.org/wiki/Mime_type) |
| **Pasos** | encabezado de Hello X-contenido-opciones de tipo es un encabezado HTTP que permite a los desarrolladores toospecify que su contenido no debería estar examinan MIME. Este encabezado es toomitigate diseñada ataques de examen de MIME. Para cada página que podría incluir contenido controlable de usuario, debe usar hello HTTP encabezado X-contenido-tipo-opciones: nosniff. encabezado necesario de Hola de tooenable globalmente para todas las páginas de aplicación hello, puede hacer uno de los siguientes Hola|

### <a name="example"></a>Ejemplo
Agregar encabezado de hello en el archivo web.config de hello si aplicación hello está hospedado por Internet Information Services (IIS) 7 y versiones posteriores. 
```XML
<system.webServer>
<httpProtocol>
<customHeaders>
<add name="X-Content-Type-Options" value="nosniff"/>
</customHeaders>
</httpProtocol>
</system.webServer>
```

### <a name="example"></a>Ejemplo
Agregar encabezado de Hola a través de hello global de la aplicación\_BeginRequest 
```C#
void Application_BeginRequest(object sender, EventArgs e)
{
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
}
```

### <a name="example"></a>Ejemplo
Implemente un módulo HTTP personalizado 
```C#
public class XContentTypeOptionsModule : IHttpModule
{
#region IHttpModule Members
public void Dispose()
{
}
public void Init(HttpApplication context)
{
context.PreSendRequestHeaders += newEventHandler(context_PreSendRequestHeaders);
}
#endregion
void context_PreSendRequestHeaders(object sender, EventArgs e)
{
HttpApplication application = sender as HttpApplication;
if (application == null)
  return;
if (application.Response.Headers["X-Content-Type-Options "] != null)
  return;
application.Response.Headers.Add("X-Content-Type-Options ", "nosniff");
}
}
```

### <a name="example"></a>Ejemplo
Puede habilitar el encabezado necesario de hello solo para páginas específicas mediante la adición de las respuestas de tooindividual: 

```C#
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
```

## <a id="standard-finger"></a>Quitar encabezados estándar del servidor en sitios Web Windows Azure tooavoid huellas digitales

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | EnvironmentType: Azure |
| **Referencias**              | [Removing standard server headers on Windows Azure Web Sites](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/) (Eliminación de encabezados de servidor estándar de los sitios web de Windows Azure) |
| **Pasos** | Encabezados como servidor X con tecnología-a, X-AspNet-Version revelar información sobre el servidor de Hola y Hola tecnologías subyacentes. Se recomienda toosuppress aplicación Hola a estos encabezados lo que evita que huellas digitales |

## <a id="firewall-db"></a>Configuración de Firewall de Windows para el acceso al motor de base de datos

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | SQL Azure, OnPrem |
| **Atributos**              | N/A, SQL Version: V12 |
| **Referencias**              | [Cómo tooconfigure SQL Azure base de datos firewall](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/), [configurar Firewall de Windows para obtener acceso al motor de base de datos](https://msdn.microsoft.com/library/ms175043) |
| **Pasos** | Sistemas de Firewall ayudan a evitar que los recursos de toocomputer de acceso no autorizado. tooaccess una instancia de hello motor de base de datos de SQL Server a través de un firewall, debe configurar firewall de hello en equipo Hola ejecuta acceso tooallow de SQL Server |

## <a id="cors-api"></a>Comprobación de que solo se permiten orígenes de confianza si CORS está activado en ASP.NET Web API

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | MVC 5 |
| **Atributos**              | N/D  |
| **Referencias**              | [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api) (Habilitación de solicitudes de origen cruzado en ASP-NET Web API 2), [Funciones para CORS en ASP.NET Web API 2](https://msdn.microsoft.com/magazine/dn532203.aspx) |
| **Pasos** | <p>Seguridad del explorador impide que una página web realice ningún dominio de tooanother de solicitudes de AJAX. Esta restricción se denomina directiva de mismo origen de Hola e impide que un sitio malintencionado pueda leer los datos confidenciales desde otro sitio. Sin embargo, en ocasiones puede que sea necesario tooexpose las API de forma segura que es compatible con otros sitios. Entre recursos de uso compartido a orígenes (CORS) es un estándar de W3C que permite que un servidor de directiva de mismo origen de toorelax Hola.</p><p>Con CORS, un servidor puede permitir explícitamente algunas solicitudes de origen cruzado y rechazar otras. CORS es más seguro y más flexible que las técnicas anteriores, como JSONP.</p>|

### <a name="example"></a>Ejemplo
Hola App_Start/WebApiConfig.cs, agregar Hola después code toohello WebApiConfig.Register (método) 
```C#
using System.Web.Http;
namespace WebService
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // New code
            config.EnableCors();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
        }
    }
}
```

### <a name="example"></a>Ejemplo
Atributo EnableCors puede ser métodos de tooaction aplicada en un controlador de como se indica a continuación: 

```C#
public class ResourcesController : ApiController
{
  [EnableCors("http://localhost:55912", // Origin
              null,                     // Request headers
              "GET",                    // HTTP methods
              "bar",                    // Response headers
              SupportsCredentials=true  // Allow credentials
  )]
  public HttpResponseMessage Get(int id)
  {
    var resp = Request.CreateResponse(HttpStatusCode.NoContent);
    resp.Headers.Add("bar", "a bar value");
    return resp;
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "PUT",                          // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "POST",                         // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
}
```

Tenga en cuenta que es crítica tooensure que Hola lista de orígenes en el atributo EnableCors se establezca tooa conjunto finito y de confianza de orígenes. Errores tooconfigure este inapropiada (p. ej., el valor de hello como ' *') le permitirá tootrigger sitios malintencionados cross origen solicitudes toohello API sin restricciones, >, por lo que Hola API tooCSRF vulnerable ataques. EnableCors se puede decorar en el nivel de controlador. 

### <a name="example"></a>Ejemplo
toodisable CORS en un determinado método en una clase, Hola DisableCors atributo puede utilizarse tal y como se muestra a continuación: 
```C#
[EnableCors("http://example.com", "Accept, Origin, Content-Type", "POST")]
public class ResourcesController : ApiController
{
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  // CORS not allowed because of hello [DisableCors] attribute
  [DisableCors]
  public HttpResponseMessage Delete(int id)
  {
    return Request.CreateResponse(HttpStatusCode.NoContent);
  }
}
```

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | MVC 6 |
| **Atributos**              | N/D  |
| **Referencias**              | [Habilitación de solicitudes de origen cruzado (CORS) en ASP.NET Core 1.0](https://docs.asp.net/en/latest/security/cors.html) |
| **Pasos** | <p>En ASP.NET Core 1.0, CORS puede habilitarse mediante middleware o MVC. Cuando se usa Hola CORS de MVC tooenable mismos servicios CORS se utilizan, pero Hola middleware CORS no lo es.</p>|

**Enfoque 1** habilitar CORS con middleware: tooenable CORS para toda la aplicación hello agregar canalización hello CORS middleware toohello solicitud mediante el método de extensión UseCors Hola. Una directiva entre orígenes puede especificarse cuando se agrega middleware CORS de hello mediante hello CorsPolicyBuilder clase. Hay dos toodo formas esto:

### <a name="example"></a>Ejemplo
Hola en primer lugar es toocall UseCors con una expresión lambda. lambda Hola toma un objeto de CorsPolicyBuilder: 
```C#
public void Configure(IApplicationBuilder app)
{
    app.UseCors(builder =>
        builder.WithOrigins("http://example.com")
        .WithMethods("GET", "POST", "HEAD")
        .WithHeaders("accept", "content-type", "origin", "x-custom-header"));
}
```

### <a name="example"></a>Ejemplo
Hola en segundo lugar es toodefine uno o más denominado directiva de hello, a continuación, seleccione y de las directivas CORS por su nombre en tiempo de ejecución. 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddCors(options =>
    {
        options.AddPolicy("AllowSpecificOrigin",
            builder => builder.WithOrigins("http://example.com"));
    });
}
public void Configure(IApplicationBuilder app)
{
    app.UseCors("AllowSpecificOrigin");
    app.Run(async (context) =>
    {
        await context.Response.WriteAsync("Hello World!");
    });
}
```

**Enfoque 2** habilitar CORS en MVC: los desarrolladores también pueden usar MVC tooapply CORS específico por cada acción, por cada controlador o globalmente para todos los controladores.

### <a name="example"></a>Ejemplo
Por cada acción: toospecify una directiva CORS para una acción específica Agregar acción de toohello de atributo de hello [EnableCors]. Especifique el nombre de la directiva de Hola. 
```C#
public class HomeController : Controller
{
    [EnableCors("AllowSpecificOrigin")] 
    public IActionResult Index()
    {
        return View();
    }
```

### <a name="example"></a>Ejemplo
Por controlador: 
```C#
[EnableCors("AllowSpecificOrigin")]
public class HomeController : Controller
{
```

### <a name="example"></a>Ejemplo
Globalmente: 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    services.Configure<MvcOptions>(options =>
    {
        options.Filters.Add(new CorsAuthorizationFilterFactory("AllowSpecificOrigin"));
    });
}
```
Tenga en cuenta que es crítica tooensure que Hola lista de orígenes en el atributo EnableCors se establezca tooa conjunto finito y de confianza de orígenes. Errores tooconfigure este inapropiada (p. ej., el valor de hello como ' *') le permitirá tootrigger sitios malintencionados cross origen solicitudes toohello API sin restricciones, >, por lo que Hola API tooCSRF vulnerable ataques. 

### <a name="example"></a>Ejemplo
toodisable CORS para un controlador o la acción, usar el atributo de hello [DisableCors]. 
```C#
[DisableCors]
    public IActionResult About()
    {
        return View();
    }
```

## <a id="config-sensitive"></a>Cifrado de secciones de los archivos de configuración de la API web que contienen datos confidenciales

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Cómo: Cifrar secciones de configuración en ASP.NET 2.0 utilizando DPAPI](https://msdn.microsoft.com/library/ff647398.aspx), [especificar un proveedor de configuración protegida](https://msdn.microsoft.com/library/68ze1hb2.aspx), [secretos de aplicación de tooprotect con el almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **Pasos** | Archivos de configuración como Web.config hello, appSettings.JSON que se suelen usar toohold información confidencial, incluidos los nombres de usuario, contraseñas, las cadenas de conexión de base de datos y las claves de cifrado. Si no protege esta información, la aplicación es vulnerable tooattackers o usuarios malintencionados obtener información confidencial, como nombres de cuenta de usuario y contraseñas, nombres de base de datos y nombres de servidor. Según el tipo de implementación de hello (azure/local), cifrar secciones confidenciales de Hola de archivos de configuración mediante DPAPI o servicios como almacén de claves de Azure. |

## <a id="admin-strong"></a>Comprobación de que todas las interfaces de administración están protegidas con credenciales seguras

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Interfaces administrativas cualquier dispositivo Hola o expone de puerta de enlace de campo debe protegerse utilizando credenciales seguras. Además, debe protegerse con credenciales seguras el resto de interfaces expuestas, como Wi-Fi, SSH, recursos compartidos de archivo o FTP. De forma predeterminada, no deben usarse contraseñas poco seguras. |

## <a id="unknown-exe"></a>Comprobación de que no se puede ejecutar código desconocido en los dispositivos

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Enabling Secure Boot and bit-locker Device Encryption on Windows 10 IoT Core](https://developer.microsoft.com/windows/iot/win10/sb_bl) (Habilitación del arranque seguro y del cifrado de dispositivos de BitLocker en Windows 10 IoT Core) |
| **Pasos** | Arranque seguro de UEFI restringe el sistema de hello tooonly permitir la ejecución de los archivos binarios firmados por una entidad especificada. Esta característica impide que código desconocido se ejecute en plataforma de Hola y potencialmente debilitar la postura de seguridad de hello del mismo. Habilitar el arranque seguro de UEFI y restringir la lista de Hola de entidades emisoras de certificados que son de confianza para la firma de código. Inicio de sesión de todo el código que se implementa en el dispositivo de hello mediante una de las entidades de confianza de Hola. |

## <a id="partition-iot"></a>Cifrado del sistema operativo y particiones adicionales en los dispositivos IoT con Bitlocker

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Windows 10 IoT Core implementa una versión ligera de cifrado de dispositivo de caja de seguridad de bits, que tiene una dependencia fuerte en presencia de Hola de un TPM en plataforma de hello, incluido el protocolo de preOS necesarios de hello en UEFI que lleva a cabo las medidas necesarias de Hola. Estas medidas de preOS asegurarse de esa Hola que SO más adelante posee un registro definitivo de cómo se ha iniciado Hola SO. Cifrar particiones de sistema operativo con bits-caja de seguridad y las particiones adicionales también en caso de que almacenan los datos confidenciales. |

## <a id="min-enable"></a>Asegúrese de que solo Hola mínimo servicios o características están habilitadas en los dispositivos

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | No habilite ni desactivar cualquier características o servicios en el sistema operativo que no es necesario para que funcione solución Hola Hola Hola. Para, por ejemplo, si el dispositivo de hello no requiere un toobe de interfaz de usuario que se implementa, instalar Windows IoT Core en modo desatendido. |

## <a id="field-bit-locker"></a>Cifrado del sistema operativo y particiones adicionales en la puerta de enlace de campo de IoT con Bitlocker

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Puerta de enlace de campo de IoT | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Windows 10 IoT Core implementa una versión ligera de cifrado de dispositivo de caja de seguridad de bits, que tiene una dependencia fuerte en presencia de Hola de un TPM en plataforma de hello, incluido el protocolo de preOS necesarios de hello en UEFI que lleva a cabo las medidas necesarias de Hola. Estas medidas de preOS asegurarse de esa Hola que SO más adelante posee un registro definitivo de cómo se ha iniciado Hola SO. Cifrar particiones de sistema operativo con bits-caja de seguridad y las particiones adicionales también en caso de que almacenan los datos confidenciales. |

## <a id="default-change"></a>Asegúrese de que las credenciales de inicio de sesión predeterminado de Hola de puerta de enlace de campo de Hola se cambian durante la instalación

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Puerta de enlace de campo de IoT | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Asegúrese de que las credenciales de inicio de sesión predeterminado de Hola de puerta de enlace de campo de Hola se cambian durante la instalación |

## <a id="cloud-firmware"></a>Asegurarse de que esa puerta de enlace de nube Hola implementa un firmware de dispositivos de proceso tookeep Hola conectado seguridad toodate

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Puerta de enlace de la nube de IoT | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | Elección de puerta de enlace: Azure IoT Hub |
| **Referencias**              | [Introducción a la administración IoT Hub dispositivo](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-overview/), [cómo tooupdate Firmware del dispositivo](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-device-jobs/) |
| **Pasos** | LWM2M es un protocolo de hello abierto alianzas móviles para la administración de dispositivos de IoT. Administración de dispositivos de IoT de Azure permite toointeract con dispositivos físicos con los trabajos de dispositivo. Asegúrese de que Hola puerta de enlace de nube implementa un dispositivo de proceso tooroutinely mantener hello y otros datos de configuración de seguridad toodate mediante la administración de dispositivos de centro de IoT de Azure. |

## <a id="controls-policies"></a>Comprobación de que los dispositivos tienen controles de seguridad de punto de conexión configurados según las directivas organizativas

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Límite de confianza de la máquina | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Asegúrese de que los controles de seguridad de punto de conexión de los dispositivos como Bitlocker para el cifrado a nivel de disco, antivirus con las firmas actualizadas, firewall basado en el host, actualizaciones de sistema operativo, directivas de grupo, etc. estén configurados según las directivas de seguridad. |

## <a id="secure-keys"></a>Comprobación de la administración segura de las claves de acceso de almacenamiento de Azure

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure Storage | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Guía de seguridad de Azure Storage: administración de las claves de la cuenta de almacenamiento](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_managing-your-storage-account-keys) |
| **Pasos** | <p>Almacenamiento de claves: Se recomienda toostore teclas de acceso de almacenamiento de Azure de hello en el almacén de claves de Azure como un secreto y tiene aplicaciones de hello recuperar clave Hola de almacén de claves. Se recomienda hacer esto debido toohello siguientes motivos:</p><ul><li>aplicación Hello nunca tendrá Hola almacenamiento clave codificados en un archivo de configuración, lo que elimina ese caminos de alguien obtener acceso a las claves de toohello sin permiso específico</li><li>Teclas de acceso toohello pueden controlarse mediante Azure Active Directory. Esto significa que un propietario de la cuenta puede conceder la serie de toohello de acceso de las aplicaciones que necesitan las claves de hello tooretrieve desde el almacén de claves de Azure. Otras aplicaciones no será capaz de tooaccess claves de hello sin concederles permisos específicamente</li><li>Regeneración de claves: Se recomienda por motivos de seguridad de claves de toohave un proceso en lugar tooregenerate acceso de almacenamiento de Azure. Artículo hacen referencia a obtener más información sobre por qué y cómo tooplan de regeneración de claves se documentan en Hola a Guía de seguridad de almacenamiento de Azure</li></ul>|

## <a id="cors-storage"></a>Comprobación de que solo se permiten orígenes de confianza si CORS está activado en Azure Storage

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure Storage | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Compatibilidad con CORS para hello servicios de almacenamiento de Azure](https://msdn.microsoft.com/library/azure/dn535601.aspx) |
| **Pasos** | Almacenamiento de Azure permite tooenable CORS: Cross uso compartido de recursos de origen. Para cada cuenta de almacenamiento, puede especificar los dominios que pueden tener acceso a recursos de hello en esa cuenta de almacenamiento. De forma predeterminada, el uso compartido de recursos entre orígenes está deshabilitado en todos los servicios. Puede habilitar CORS mediante Hola API de REST o hello almacenamiento cliente biblioteca toocall uno Hola métodos tooset Hola de autoservicio. |

## <a id="throttling"></a>Habilitación de la característica de limitación del servicio de WCF

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | .NET Framework 3 |
| **Atributos**              | N/D  |
| **Referencias**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Pasos** | <p>No colocando un límite en hello el uso de recursos pudieron provocar el agotamiento de recursos y, en última instancia, una denegación de servicio de sistema.</p><ul><li>**Explicación:** Windows Communication Foundation (WCF) ofrece Hola capacidad toothrottle atender las solicitudes. Permitir demasiadas solicitudes de cliente puede superar al sistema y agotar sus recursos. En hello otra parte, permitiendo que a solo un pequeño número de solicitudes de servicio de tooa puede impedir que los usuarios legítimos puedan usar servicio de Hola. Cada servicio debe ser tooand individualmente optimizadas configurado tooallow Hola cantidad apropiada de recursos.</li><li>**RECOMENDACIONES** Habilite la característica de limitación del servicio de WCF y establezca los límites adecuados para la aplicación.</li></ul>|

### <a name="example"></a>Ejemplo
Hola te mostramos un ejemplo de configuración con la limitación habilitado:
```
<system.serviceModel> 
  <behaviors>
    <serviceBehaviors>
    <behavior name="Throttled">
    <serviceThrottling maxConcurrentCalls="[YOUR SERVICE VALUE]" maxConcurrentSessions="[YOUR SERVICE VALUE]" maxConcurrentInstances="[YOUR SERVICE VALUE]" /> 
  ...
</system.serviceModel> 
```

## <a id="info-metadata"></a>Revelación de información de WCF mediante metadatos

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | .NET Framework 3 |
| **Atributos**              | N/D  |
| **Referencias**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Pasos** | Metadatos pueden ayudar a los atacantes obtener información sobre el sistema de Hola y planear la forma de ataque. Servicios WCF pueden ser metadatos tooexpose configurado. Los metadatos proporcionan información descriptiva detallada del servicio y no se deben difundir en entornos de producción. Hola `HttpGetEnabled`  /  `HttpsGetEnabled` propiedades de clase de ServiceMetaData Hola define si un servicio va a exponer metadatos de Hola | 

### <a name="example"></a>Ejemplo
código de Hello siguiente indica a WCF toobroadcast un metadato del servicio
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
smb.HttpGetEnabled = true; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb); 
```
En un entorno de producción no se difunden los metadatos del servicio. Establecer HttpGetEnabled Hola / propiedades HttpsGetEnabled de hello ServiceMetaData class toofalse. 

### <a name="example"></a>Ejemplo
código de Hello siguiente indica a WCF toonot difundir un metadato del servicio. 
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior(); 
smb.HttpGetEnabled = false; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb);
```
