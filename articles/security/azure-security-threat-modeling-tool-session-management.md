---
title: "aaaSession de administración - herramienta de modelado de amenazas de Microsoft - Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a>Marco de seguridad: Administración de sesiones | Artículos 
| Producto o servicio | Artículo |
| --------------- | ------- |
| **Azure AD**    | <ul><li>[Implemente el cierre de sesión correcto mediante métodos ADAL cuando use Azure AD](#logout-adal)</li></ul> |
| Dispositivo IoT | <ul><li>[Use duraciones finitas para los tokens de SaS generados](#finite-tokens)</li></ul> |
| **Azure Document DB** | <ul><li>[Use duraciones mínimas de token para los tokens de recursos generados](#resource-tokens)</li></ul> |
| **ADFS** | <ul><li>[Implemente el cierre de sesión correcto mediante métodos WsFederation cuando use ADFS](#wsfederation-logout)</li></ul> |
| **Identity Server** | <ul><li>[Implemente el cierre de sesión correcto cuando use Identity Server](#proper-logout)</li></ul> |
| **Aplicación web** | <ul><li>[Las aplicaciones disponibles a través de HTTPS deben usar cookies seguras](#https-secure-cookies)</li><li>[Todas las aplicaciones basadas en HTTP deben especificar HTTP solo para la definición de cookies](#cookie-definition)</li><li>[Mitigue el riesgo de ataques de falsificación de solicitud entre sitios (CSRF) en páginas web ASP.NET](#csrf-asp)</li><li>[Configure la sesión para la duración de la inactividad](#inactivity-lifetime)</li><li>[Implemente el cierre de sesión correcto de la aplicación hello](#proper-app-logout)</li></ul> |
| **API web** | <ul><li>[Mitigue el riesgo de ataques de falsificación de solicitud entre sitios (CSRF) en las API web de ASP.NET](#csrf-api)</li></ul> |

## <a id="logout-adal"></a>Implemente el cierre de sesión correcto mediante métodos ADAL cuando use Azure AD

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure AD | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Si la aplicación hello se basa en el token de acceso emitido por Azure AD, debe llamar controlador de eventos de cierre de sesión de Hola |

### <a name="example"></a>Ejemplo
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a>Ejemplo
También debe destruir la sesión del usuario llamando al método Session.Abandon(). En el siguiente método, se muestra una implementación segura del cierre de sesión del usuario:
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <a id="finite-tokens"></a>Use duraciones finitas para los tokens de SaS generados

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Los tokens de SaS generados para la autenticación de tooAzure centro de IoT deben tener un período de expiración definida. Mantener Hola SaS vigencia de los tokens tooa toolimit mínima Hola cantidad de tiempo que se pueden reproducir en caso de que se vean comprometidos los tokens de Hola.|

## <a id="resource-tokens"></a>Use duraciones mínimas de token para los tokens de recursos generados

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure DocumentDB | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Reducir timespan hello tooa token mínimo del valor de recurso necesario. Los tokens de recursos tienen un intervalo de tiempo válido predeterminado de 1 hora.|

## <a id="wsfederation-logout"></a>Implemente el cierre de sesión correcto mediante métodos WsFederation cuando use ADFS

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | ADFS | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Si aplicación hello se basa en token STS emitido por AD FS, controlador de eventos de cierre de sesión de hello debe llamar a WSFederationAuthenticationModule.FederatedSignOut() método toolog usuario Hola. También hello actual debe destruirse sesión, y el valor del token de sesión Hola debe restablecer y compensan los riesgos.|

### <a name="example"></a>Ejemplo
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <a id="proper-logout"></a>Implemente el cierre de sesión correcto cuando use Identity Server

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Identity Server | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [IdentityServer3-Federated Signout](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) (Cierre de sesión federado en IdentityServer3) |
| **Pasos** | IdentityServer admite Hola capacidad toofederate con proveedores de identidad externa. Cuando un usuario cierra sesión en un proveedor de identidades de nivel superior, según el protocolo de hello utilizado, puede que sea posible tooreceive una notificación cuando Hola usuario cierra la sesión. Permite toonotify IdentityServer Hola a sus clientes para que también pueden iniciar sesión de un usuario. Consulte la documentación de hello en la sección de referencias de Hola para obtener detalles de implementación de Hola.|

## <a id="https-secure-cookies"></a>Las aplicaciones disponibles a través de HTTPS deben usar cookies seguras

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | EnvironmentType - OnPrem |
| **Referencias**              | [httpCookies (Elemento, Esquema de configuración de ASP.NET)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [Propiedad HttpCookie.Secure](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx) |
| **Pasos** | Las cookies son normalmente sólo dominio de toohello accesible para el que está limitadas. Por desgracia, definición de Hola de "dominio" no incluye protocolo Hola por lo que las cookies se crean a través de HTTPS son accesibles a través de HTTP. atributo de "seguro" Hello indica explorador toohello que Hola cookie sólo deberá hacerse disponible a través de HTTPS. Asegúrese de que todas las cookies que se establece a través de HTTPS utilizan hello **segura** atributo. puede aplicar el requisito de Hello en el archivo web.config de hello estableciendo Hola requireSSL atributo tootrue. Es Hola preferido enfoque porque aplicará hello **segura** atributo para todas las cookies actuales y futuras sin Hola necesidad toomake cambios de código adicionales.|

### <a name="example"></a>Ejemplo
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
se aplica la configuración de Hello aunque HTTP es aplicación de hello tooaccess usado. Si se utiliza HTTP tooaccess Hola aplicación, saltos de configuración aplicación hello porque las cookies de Hola se establecen con hello hello y atributo de un navegador seguro no enviará ellos hello volver toohello aplicación.

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Formularios Web Forms, MVC5 |
| **Atributos**              | EnvironmentType - OnPrem |
| **Referencias**              | N/D  |
| **Pasos** | Cuando es de aplicación web de Hola Hola persona de confianza y Hola IdP es el servidor ADFS, atributo segura del token de hello FedAuth puede configurarse por establecer requireSSL tooTrue en `system.identityModel.services` sección del archivo web.config:|

### <a name="example"></a>Ejemplo
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <a id="cookie-definition"></a>Todas las aplicaciones basadas en HTTP deben especificar HTTP solo para la definición de cookies

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Atributo de cookie segura](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| **Pasos** | toomitigate Hola riesgo de divulgación con un ataque de scripting entre sitios (XSS), un nuevo atributo - httpOnly - se ha introducido toocookies y es compatible con todos los exploradores principales. atributo de Hello especifica que una cookie no es accesible a través de la secuencia de comandos. Mediante el uso de cookies HttpOnly, una aplicación web reduce la posibilidad de Hola que información confidencial contenida en la cookie de hello puede robo mediante un script y enviarse el sitio Web del atacante tooan. |

### <a name="example"></a>Ejemplo
Todas las aplicaciones basadas en HTTP que utilizan cookies deben especificar HttpOnly en definición de la cookie de hello, mediante la implementación después de la configuración en el archivo web.config:
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Formularios Web Forms |
| **Atributos**              | N/D  |
| **Referencias**              | [Propiedad FormsAuthentication.RequireSSL](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| **Pasos** | Hola RequireSSL valor de propiedad se establece en el archivo de configuración de Hola para una aplicación ASP.NET mediante Hola requireSSL atributo del elemento de configuración de Hola. Puede especificar en el archivo Web.config de hello para la aplicación ASP.NET si SSL (capa de Sockets seguros) es servidor de toohello de cookie de autenticación de formularios de tooreturn necesario Hola por establecer el atributo requireSSL de Hola.|

### <a name="example"></a>Ejemplo 
Hello ejemplo de código siguiente establece atributo requireSSL de hello en el archivo Web.config de Hola.
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | MVC5 |
| **Atributos**              | EnvironmentType - OnPrem |
| **Referencias**              | [Windows Identity Foundation (WIF) Configuration – Part II](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) (Configuración de Windows Identity Foundation: parte II) |
| **Pasos** | atributo httpOnly de tooset para FedAuth cookies, el valor del atributo de hideFromCsript que debe establecerse tooTrue. |

### <a name="example"></a>Ejemplo
Configuración siguiente muestra la configuración correcta de hello:
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <a id="csrf-asp"></a>Mitigue el riesgo de ataques de falsificación de solicitud entre sitios (CSRF) en páginas web ASP.NET

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Falsificación de solicitud entre sitios (CSRF o XSRF) es un tipo de ataque en el que un atacante puede llevar a cabo acciones en el contexto de seguridad de Hola de sesión establecido de un usuario diferente en un sitio web. el objetivo de Hello es toomodify o eliminar el contenido, si el sitio web utilizado como destino de Hola se basa exclusivamente en la solicitud recibida de tooauthenticate de cookies de sesión. Un atacante podría aprovechar esta vulnerabilidad obteniendo una dirección URL con un comando de tooload de explorador de un usuario diferente de un sitio vulnerable en la que el usuario de hello ya se registra en. Hay muchas maneras para un toodo atacante que, como mediante el hospedaje de un sitio web diferente carga un recurso de servidor vulnerable Hola o tooclick de usuario Hola al obtener un vínculo. ataque de Hello puede evitarse si servidor hello envía a un cliente toohello token adicional, requiere Hola cliente tooinclude ese token en todas las solicitudes futuras y comprueba que todas las solicitudes futuras incluyen un símbolo (token) que pertenece a toohello sesión actual, como por uso de hello AntiForgeryToken de ASP.NET o estado de vista. |

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referencias**              | [XSRF/CSRF Prevention in ASP.NET MVC and Web Pages](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) (Prevención de XSRF y CSRF en ASP.NET MVC y Web Pages) |
| **Pasos** | Formularios de Anti-CSRF y ASP.NET MVC - Hola de uso `AntiForgeryToken` método auxiliar para las vistas; put un `Html.AntiForgeryToken()` en forma de hello, por ejemplo,|

### <a name="example"></a>Ejemplo
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a>Ejemplo
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>Ejemplo
En hello mismo tiempo, visitante de Hola de Html.AntiForgeryToken() proporciona una cookie denominada __RequestVerificationToken con hello mismo valor que el valor de hidden aleatorio Hola mostrado anteriormente. A continuación, toovalidate una solicitud de post de formulario entrante, agregue el método de acción de hello [ValidateAntiForgeryToken] filtro toohello destino. Por ejemplo:
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
Filtro de autorización que comprueba que:
* solicitud entrante de Hello tiene una cookie denominada __RequestVerificationToken
* Hola entrante solicitud tiene un `Request.Form` entrada llamada __RequestVerificationToken
* Estas cookies y `Request.Form` suponiendo que todos los de coincidencia de valores está bien, solicitud de hello pasa a través de forma habitual. De lo contrario, aparece un error de autorización con el mensaje "No se especificó un token antifalsificación o el que se especificó no era válido". 

### <a name="example"></a>Ejemplo
Anti-CSRF y AJAX: token de formulario de Hola puede constituir un problema para las solicitudes de AJAX, porque una solicitud AJAX puede enviar datos JSON, no los datos de formulario HTML. Una solución es toosend Hola símbolos (tokens) en un encabezado HTTP personalizado. Hola código siguiente usa tokens de Hola de toogenerate de sintaxis de Razor y, a continuación, agrega la solicitud de AJAX de hello tokens tooan. 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>Ejemplo
Cuando se procesa la solicitud de hello, extraer tokens Hola Hola encabezado de solicitud. A continuación, llame al método de AntiForgery.Validate Hola tokens de hello toovalidate. Hola método Validate produce una excepción si los tokens de hello no son válidos.
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Formularios Web Forms |
| **Atributos**              | N/D  |
| **Referencias**              | [Tomar ventaja de ASP.NET características integradas tooFend Off Web ataques](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| **Pasos** | Ataques CSRF en aplicaciones de WebForm según pueden ser mitigados estableciendo ViewStateUserKey tooa cadena aleatoria que varía para cada usuario - Id. de usuario o, mejor aún, Id. Por diversas razones técnicas y sociales, el id. de sesión es mucho más adecuado porque es imprevisible, agota el tiempo de espera y varía para cada usuario.|

### <a name="example"></a>Ejemplo
Este es código de hello necesite toohave en todas las páginas.
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <a id="inactivity-lifetime"></a>Configure la sesión para la duración de la inactividad

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Propiedad HttpSessionState.Timeout](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx) |
| **Pasos** | Tiempo de espera de sesión representa Hola eventos se producen cuando un usuario no realiza ninguna acción en un sitio web durante un intervalo (definido por el servidor web). Hola eventos, en el lado servidor, cambiar el estado de Hola de too'invalid de sesión de usuario de hello' (por ejemplo "no se utiliza ya") e indicarle hello web server toodestroy que (eliminar todos los datos contenidos en él). Hello ejemplo de código siguiente establece minutos de too15 de atributo de sesión de tiempo de espera de hello en el archivo Web.config de Hola.|

### <a name="example"></a>Ejemplo
```XML code <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Formularios Web Forms |
| **Atributos**              | N/D  |
| **Referencias**              | [Elemento forms para authentication (Esquema de configuración de ASP.NET)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx) |
| **Pasos** | Establece los minutos de hello too15 de tiempo de espera de cookie de vale de autenticación de formularios|

### <a name="example"></a>Ejemplo
```XML code <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a>Ejemplo
También Hola emitidos duración del token de SAML notificaciones ADFS debe establecerse too15 minutos, mediante la ejecución de hello siguiente comando de powershell en el servidor de ADFS de hello:
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <a id="proper-app-logout"></a>Implemente el cierre de sesión correcto de la aplicación hello

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Realizar inicio de sesión correcto Out desde la aplicación hello, cuando las pulsaciones usuario cierre sesión botón. Al cerrar la sesión, la aplicación debe destruir la sesión del usuario y también restablecer y anular el valor de la cookie de la sesión, así como restablecer y anular el valor de la cookie de autenticación. Además, cuando varias sesiones tooa ligada identidad de usuario único, debe terminarse colectivamente en servidor hello en tiempo de espera o cierre de sesión. Por último, asegúrese de que la funcionalidad de cierre de sesión esté disponible en todas las páginas. |

## <a id="csrf-api"></a>Mitigue el riesgo de ataques de falsificación de solicitud entre sitios (CSRF) en las API web de ASP.NET

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Falsificación de solicitud entre sitios (CSRF o XSRF) es un tipo de ataque en el que un atacante puede llevar a cabo acciones en el contexto de seguridad de Hola de sesión establecido de un usuario diferente en un sitio web. el objetivo de Hello es toomodify o eliminar el contenido, si el sitio web utilizado como destino de Hola se basa exclusivamente en la solicitud recibida de tooauthenticate de cookies de sesión. Un atacante podría aprovechar esta vulnerabilidad obteniendo una dirección URL con un comando de tooload de explorador de un usuario diferente de un sitio vulnerable en la que el usuario de hello ya se registra en. Hay muchas maneras para un toodo atacante que, como mediante el hospedaje de un sitio web diferente carga un recurso de servidor vulnerable Hola o tooclick de usuario Hola al obtener un vínculo. ataque de Hello puede evitarse si servidor hello envía a un cliente toohello token adicional, requiere Hola cliente tooinclude ese token en todas las solicitudes futuras y comprueba que todas las solicitudes futuras incluyen un símbolo (token) que pertenece a toohello sesión actual, como por uso de hello AntiForgeryToken de ASP.NET o estado de vista. |

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referencias**              | [Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) (Prevención de ataques de falsificación de solicitud entre sitios [CSRF] en ASP.NET Web API) |
| **Pasos** | Anti-CSRF y AJAX: token de formulario de Hola puede constituir un problema para las solicitudes de AJAX, porque una solicitud AJAX puede enviar datos JSON, no los datos de formulario HTML. Una solución es toosend Hola símbolos (tokens) en un encabezado HTTP personalizado. Hola código siguiente usa tokens de Hola de toogenerate de sintaxis de Razor y, a continuación, agrega la solicitud de AJAX de hello tokens tooan. |

### <a name="example"></a>Ejemplo
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>Ejemplo
Cuando se procesa la solicitud de hello, extraer tokens Hola Hola encabezado de solicitud. A continuación, llame al método de AntiForgery.Validate Hola tokens de hello toovalidate. Hola método Validate produce una excepción si los tokens de hello no son válidos.
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a>Ejemplo
Anti-CSRF y formularios de ASP.NET MVC - Hola Utilice método de aplicación auxiliar de AntiForgeryToken en las vistas; Coloque un Html.AntiForgeryToken() en forma de hello, por ejemplo,
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a>Ejemplo
ejemplo de Hola anterior dará como resultado algo parecido a Hola siguiente:
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>Ejemplo
En hello mismo tiempo, visitante de Hola de Html.AntiForgeryToken() proporciona una cookie denominada __RequestVerificationToken con hello mismo valor que el valor de hidden aleatorio Hola mostrado anteriormente. A continuación, toovalidate una solicitud de post de formulario entrante, agregue el método de acción de hello [ValidateAntiForgeryToken] filtro toohello destino. Por ejemplo:
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
Filtro de autorización que comprueba que:
* solicitud entrante de Hello tiene una cookie denominada __RequestVerificationToken
* Hola entrante solicitud tiene un `Request.Form` entrada llamada __RequestVerificationToken
* Estas cookies y `Request.Form` suponiendo que todos los de coincidencia de valores está bien, solicitud de hello pasa a través de forma habitual. De lo contrario, aparece un error de autorización con el mensaje "No se especificó un token antifalsificación o el que se especificó no era válido".

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | MVC5, MVC6 |
| **Atributos**              | Proveedor de identidades; ADFS, Proveedor de identidades; Azure AD |
| **Referencias**              | [Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) (Protección de una API web con cuentas individuales e inicio de sesión local en ASP.NET Web API 2.2) |
| **Pasos** | Si Hola API Web está protegido mediante OAuth 2.0, a continuación, espera un token de portador en solicitud encabezado y concede acceso toohello solicitud de autorización solo si el token de hello es válido. A diferencia de autenticación basado en cookies, los exploradores no conecte toorequests de tokens de portador de Hola. Hola que solicita el cliente necesita tooexplicitly adjuntar el token de portador de hello en el encabezado de solicitud de Hola. Por lo tanto, para las API web de ASP.NET protegidas con OAuth 2.0, los tokens de portador se consideran una defensa contra los ataques CSRF. Tenga en cuenta que si parte MVC de Hola de aplicación hello usa autenticación de formularios (es decir, usa cookies), tokens antifalsificación tienen toobe utilizado por la aplicación web MVC de Hola. |

### <a name="example"></a>Ejemplo
Hola API Web tiene toobe informado toorely sólo en tokens de portador y no en cookies. Se puede realizar por hello siguiente configuración en `WebApiConfig.Register` método: ''' configuración de código de C-Sharp. SuppressDefaultHostAuthentication(); config. Filters.Add (nueva HostAuthenticationFilter(OAuthDefaults.AuthenticationType));
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
