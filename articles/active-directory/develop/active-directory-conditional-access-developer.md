---
title: aaaDeveloper instrucciones para el acceso condicional con Azure Active Directory | Documentos de Microsoft
description: Instrucciones para desarrolladores y escenarios para el acceso condicional de Azure AD
services: active-directory
keywords: 
author: danieldobalian
manager: mbaldwin
editor: PatAltimore
ms.author: dadobali
ms.date: 07/19/2017
ms.assetid: 115bdab2-e1fd-4403-ac15-d4195e24ac95
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.openlocfilehash: 589393f5d084d64872b372d895dc889f300592bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="developer-guidance-for-azure-active-directory-conditional-access"></a>Instrucciones para desarrolladores para Acceso condicional de Azure Active Directory

Azure Active Directory (AD) ofrece toosecure de varias maneras de la aplicación y evitar que un servicio.  Una de estas características únicas es el acceso condicional.  Acceso condicional permite a los desarrolladores y los servicios de tooprotect de clientes empresariales en una gran variedad de maneras incluyendo:

* Multi-Factor Authentication
* Permitir sólo Intune inscrito servicios específicos de dispositivos tooaccess
* Restricción de ubicaciones de usuario e intervalos IP

Para obtener más información sobre todas las capacidades de Hola de acceso condicional, vea [de acceso condicional en el portal de Azure clásico hello](../active-directory-conditional-access.md). 

En este artículo, nos centramos en el acceso condicional significa toodevelopers compilar aplicaciones para Azure AD.  En él se supone que tiene conocimientos de aplicaciones de inquilino [único](active-directory-integrating-applications.md) y [multiinquilino](active-directory-devhowto-multi-tenant-overview.md), además de los [patrones comunes de autenticación](active-directory-authentication-scenarios.md).

Podrá ver en profundidad impacto Hola de obtener acceso a recursos no tiene control sobre que pueden tener directivas de acceso condicional.  Además, exploramos implicaciones Hola de acceso condicional en flujo de hello en nombre de otra persona, las aplicaciones web, obtener acceso a Microsoft Graph hello y llamar a las API.

## <a name="how-does-conditional-access-impact-an-app"></a>¿Cómo el acceso condicional impacta a una aplicación?

### <a name="app-topologies-impacted"></a>Topologías de aplicaciones afectadas

En casos más comunes, el acceso condicional no cambia el comportamiento de una aplicación o requiere cambios de desarrollador de Hola.  Sólo en ciertos casos, cuando una aplicación de manera indirecta o en modo silencioso solicita un token para un servicio, una aplicación requiere cambios de código toohandle acceso condicional "desafíos".  Puede ser tan sencillo como realizar una solicitud de inicio de sesión interactiva. 

En concreto, hello siguientes escenarios requieren acceso condicional de código toohandle "desafíos": 

* Obtener acceso a las aplicaciones Hola Microsoft Graph
* Aplicaciones de la realización de hello en nombre de flujo
* Aplicaciones que acceden a varios servicios o recursos
* Aplicaciones de una sola página que usan ADAL.js

Directivas de acceso condicional puede ser aplicación toohello aplicado, pero también pueden tooa aplicado web API la aplicación tiene acceso. toolearn Obtenga más información sobre cómo tooconfigure una directiva de acceso condicional, vea [Introducción a acceso condicional de Azure Active Directory](../active-directory-conditional-access-azuread-connected-apps.md#configure-per-application-access-rules).

Según el escenario de hello, un cliente empresarial puede aplicar y quitar directivas de acceso condicional en cualquier momento.  En orden para el funcionamiento de toocontinue de la aplicación cuando se aplica una directiva nueva, se necesita control tooimplement Hola "desafío". Hello en los ejemplos siguientes ilustran el control de desafío. 

### <a name="conditional-access-examples"></a>Ejemplos de acceso condicional

Algunos escenarios requieren el acceso condicional de toohandle de cambios de código, mientras que otros usuarios funcionan como debería.  Estos son algunos escenarios con acceso condicional toodo la autenticación multifactor que proporciona información sobre la diferencia de Hola.

* Se genera una aplicación iOS de inquilino único y se aplica una directiva de acceso condicional.  aplicación Hello inicia sesión en un usuario y no solicite acceso tooan API.  Cuando Hola usuario inicia sesión, se invocan automáticamente directivas de Hola y usuario de hello tiene tooperform la autenticación multifactor (MFA). 
* Está creando una aplicación web para varios inquilinos que usa Hola Microsoft Graph tooaccess Exchange, entre otros servicios.  Un cliente empresarial que adopta esta aplicación establece una directiva en SharePoint Online.  Cuando la aplicación web de hello solicita un token de MS Graph, se aplica una directiva en cualquier Microsoft Service (específicamente los servicios que son accesibles a través de gráfico).  A este usuario final se le solicita que realice MFA. En caso de hello, por el usuario final de hello ha iniciado sesión con tokens válidos, un desafío"notificaciones" se devuelve toohello web app.  
* Está creando una aplicación nativa que utiliza un hello tooaccess de servicio de nivel intermedio Microsoft Graph.  Un cliente empresarial al usar esta aplicación de empresa de Hola aplica un tooExchange de directiva en línea.  Cuando un usuario final inicia sesión, nivel intermedio del toohello de acceso de las solicitudes de aplicación nativa para hello y envía el token de Hola.  nivel intermedio de Hello realiza en nombre de flujo toorequest acceso toohello MS Graph.  En este punto, un desafío"notificaciones" se presenta toohello de nivel intermedio. nivel intermedio de Hello envía Hola desafío toohello atrás aplicación nativa, que debe toocomply con la directiva de acceso condicional de Hola.

### <a name="complying-with-a-conditional-access-policy"></a>Cumplimiento con una directiva de acceso condicional

Para varias topologías de aplicación diferentes, una directiva de acceso condicional se evalúa cuando se establezca la sesión de Hola.  Como una directiva de acceso condicional funciona en la granularidad de Hola de aplicaciones y servicios, punto de hello en el que se invoca depende mucho en el escenario de Hola que está tratando de tooaccomplish.

Cuando la aplicación intenta tooaccess un servicio con una directiva de acceso condicional, puede encontrar un desafío de acceso condicional.  Este desafío se codifica en hello `claims` parámetro que procede de una respuesta de Azure AD u Hola Microsoft Graph.  Este es un ejemplo de este parámetro de desafío: 

```
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

Los desarrolladores pueden adoptar este desafío y anexar a un nuevo tooAzure de solicitud AD.  Pasar este estado solicita hello para el usuario final tooperform cualquier toocomply necesarios de acción con la directiva de acceso condicional de Hola. Hola los escenarios siguientes, se explican los detalles del error de Hola y cómo tooextract Hola parámetro. 

## <a name="scenarios"></a>Escenarios

### <a name="prerequisites"></a>Requisitos previos

El acceso condicional de Azure AD es una característica que se incluye en [Azure AD Premium](../active-directory-whatis.md#choose-an-edition).  Puede aprender más acerca de las licencias de los requisitos de hello [informe de uso sin licencia](../active-directory-conditional-access-unlicensed-usage-report.md).  Los desarrolladores pueden unir hello [Microsoft Developer Network](https://msdn.microsoft.com/dn308572.aspx), que incluye un toohello de suscripción gratuita a Enterprise Mobility Suite, que incluye Azure AD Premium.

### <a name="considerations-for-specific-scenarios"></a>Consideraciones para escenarios específicos

Hola siguiente información solo se aplica en estos escenarios de acceso condicional:

* Obtener acceso a las aplicaciones Hola Microsoft Graph
* Aplicaciones de la realización de hello en nombre de flujo
* Aplicaciones que acceden a varios servicios o recursos
* Aplicaciones de una sola página que usan ADAL.js

En las secciones siguientes de hello, nos pondremos en común escenarios en los que son más complejos.  núcleo de Hello el principio de funcionamiento es acceso condicional directivas se evalúan en tiempo de Hola se solicita el token de Hola para servicio de Hola que tiene una directiva de acceso condicional que se aplica a menos que se está accediendo a través de hello Microsoft Graph.

### <a name="scenario-app-accessing-hello-microsoft-graph"></a>Escenario: Aplicación acceso a Microsoft Graph Hola

En este escenario, se guiará a través de caso de hello cuando una aplicación web solicita acceso toohello Microsoft Graph. en este caso, podría asignarse directiva de acceso condicional de Hello tooSharePoint, Exchange o algún otro servicio que se obtiene acceso como una carga de trabajo a través de hello Microsoft Graph.  En este ejemplo, vamos a suponer que hay una directiva de acceso condicional en SharePoint Online.

![Aplicación obtiene acceso a diagrama de flujo de hello Microsoft Graph](media/active-directory-conditional-access-developer/app-accessing-microsoft-graph-scenario.png)

aplicación Hello primero solicita autorización toohello Microsoft Graph que requiere el acceso a una carga de trabajo de nivel inferior sin acceso condicional.  solicitud de saludo se instala correctamente sin invocar cualquier directiva y aplicación hello recibe los tokens de Microsoft Graph.  En este momento, aplicación hello puede utilizar el token de acceso de Hola en una solicitud de portador para extremo Hola solicitado. Ahora, aplicación hello debe tooaccess un punto de conexión de Sharepoint Online de Microsoft Graph, por ejemplo:`https://graph.microsoft.com/v1.0/me/mySite`

aplicación Hello ya tiene un token válido para hello Microsoft Graph, para que pueda realizar nueva solicitud de hello sin que se emita un nuevo token. Se produce un error en esta solicitud y se emite un desafío de notificaciones de Microsoft Graph en forma de Hola de un HTTP 403 Prohibido con un ```WWW-Authenticate``` desafío.
Este es un ejemplo de Hola respuesta: 

```
HTTP 403; Forbidden 
error=insufficient_claims
www-authenticate="Bearer realm="", authorization_uri="https://login.windows.net/common/oauth2/authorize", client_id="<GUID>", error=insufficient_claims, claims={"access_token":{"polids":{"essential":true,"values":["<GUID>"]}}}"
```

Hello desafío de notificaciones está dentro de hello ```WWW-Authenticate``` encabezado, que puede ser analizada tooextract Hola notificaciones parámetro de solicitud siguiente Hola.  Una vez se haya anexado toohello nueva solicitud, Azure AD sabe directiva de acceso condicional de hello tooevaluate cuando la firma de usuario de Hola y aplicación hello es ahora cumplan la directiva de acceso condicional de Hola.  Repetir Hola solicitud toohello Sharepoint Online punto de conexión se realiza correctamente.

Para obtener ejemplos de código que muestran cómo toohandle Hola notificaciones desafío, consulte toohello [ejemplo de código de escritorio de .NET](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) para .NET AAL o hello [en nombre de código de ejemplo](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca) para .NET ADAL.

### <a name="scenario-app-performing-hello-on-behalf-of-flow"></a>Escenario: Realización de hello en nombre de flujo de aplicación

En este escenario, recorreremos caso hello en el que una aplicación nativa llama a una servicio web o API.  A su vez, este servicio tiene [Hola "en nombre de" flujo](active-directory-authentication-scenarios.md#application-types-and-scenarios) toocall un servicio de nivel inferior.  En nuestro caso, se ha aplicado el nuestro servicio sigue en la cadena de acceso condicional directiva toohello (Web API 2) y está usando una aplicación nativa en lugar de una aplicación demonio/servidor. 

![Aplicación realizar hello en nombre de diagrama de flujo](media/active-directory-conditional-access-developer/app-performing-on-behalf-of-scenario.png)

solicitud de token de Hello inicial de 1 de la API de Web no realiza una petición para el usuario final de hello para la autenticación multifactor como API Web 1 no puede alcanzar siempre API de nivel inferior de Hola.  Una vez que la API Web 1 intenta toorequest un usuario de símbolo (token) en nombre de otra persona Hola de API Web 2, se produce un error en la solicitud de Hola desde Hola usuario no ha iniciado sesión con autenticación multifactor.

Azure AD devuelve una respuesta HTTP con algunos datos interesantes: 

> [!NOTE]
> En esta instancia es una descripción de error de la autenticación multifactor, pero no hay una amplia gama de `interaction_required` accesos tooconditional pertinentes posibles.  

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API 2 App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

En nuestra API Web 1, se captura el error de hello `error=interaction_required`y Enviar atrás hello `claims` desafío toohello una aplicación de escritorio.  En ese momento, hacer una nueva aplicación de escritorio de hello `acquireToken()` llamar y anexar hello `claims`desafío como un parámetro de cadena de consulta adicional.  Esta nueva solicitud requiere Hola usuario toodo la autenticación multifactor y, a continuación, enviar este nuevo token tooWeb de back-1 de API y Hola completa en nombre de flujo.

tootry este escenario, vea nuestra [ejemplo de código de .NET](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca).  Muestra cómo toopass Hola desafío de notificaciones desde la aplicación nativa de API Web 1 toohello y crear una nueva solicitud dentro de la aplicación de cliente de hello. 

### <a name="scenario-app-accessing-multiple-services"></a>Escenario: Aplicación que accede a varios servicios

En este escenario, recorreremos caso hello en el que una aplicación web tiene acceso a dos servicios uno de los cuales tiene asignada una directiva de acceso condicional.  Según su lógica de aplicación, pueden existir una ruta de acceso en la que la aplicación no requiere servicios de acceso tooboth web.  En este escenario, orden de hello en el que se solicita un token desempeña un papel importante en la experiencia del usuario final de Hola.

Vamos a suponer que tenemos un servicio web A y B y que el servicio web B tiene aplicada la directiva de acceso condicional.  Mientras Hola inicial interactivo de solicitudes de autenticación requiere el consentimiento para ambos servicios, la directiva de acceso condicional de hello no es necesario en todos los casos.  Si la aplicación hello solicita un token para el servicio web B, a continuación, se invoca la directiva de Hola y las solicitudes posteriores para el servicio web A también se realiza correctamente como se indica a continuación.

![Diagrama de flujo de la aplicación que accede a varios servicios](media/active-directory-conditional-access-developer/app-accessing-multiple-services-scenario.png)

O bien, si la aplicación hello inicialmente solicita un token para un servicio de web, por el usuario final de hello no invoca la directiva de acceso condicional de Hola.  Esto permite desarrollador de aplicaciones de hello experiencia del usuario final de toocontrol hello y no forzar toobe de directiva de acceso condicional de hello invoca en todos los casos. caso de difícil de Hello es si aplicación hello posteriormente solicita un token para el servicio web B. En este momento, por el usuario final de hello debe toocomply con la directiva de acceso condicional de Hola.  Cuando se intenta demasiado aplicación hello`acquireToken`, que puede generar Hola tras error (que se muestra en hello siguiente diagrama): 

```
HTTP 400; Bad Request
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
``` 

![Aplicación que accede a varios servicios que solicitan un token nuevo](media/active-directory-conditional-access-developer/app-accessing-multiple-services-new-token.png)

Si aplicación hello utiliza la biblioteca ADAL de hello, un token de hello tooacquire error siempre se reintenta interactivamente.  Cuando se produce esta solicitud interactiva, por el usuario final de hello tiene hello toocomply de oportunidad con el acceso condicional Hola.  Esto es así a menos que la solicitud de hello es un `AcquireTokenSilentAsync` o `PromptBehavior.Never` en cuyo caso la aplicación hello necesita tooperform interactivo ```AcquireToken``` toogive Hola uso final Hola oportunidad toocomply con la directiva de saludo de solicitud. 

### <a name="scenario-single-page-app-spa-using-adaljs"></a>Escenario: Aplicación de una sola página (SPA) que usa ADAL.js

En este escenario, recorreremos el caso de hello cuando se tiene una aplicación de una página (SPA), con ADAL.js toocall un acceso condicional protegidos API web.  Esto es una arquitectura simple pero tiene algunos matices que deben tener en cuenta al desarrollar alrededor de acceso condicional de toobe.

En ADAL.js, existen algunas funciones que obtienen tokens: `login()`, `acquireToken(...)`, `acquireTokenPopup(…)` y `acquireTokenRedirect(…)`. 

* `login()` obtiene un token de identificador mediante una solicitud de inicio de sesión interactiva, pero no obtiene tokens de acceso para ningún servicio (incluida una API web protegida por acceso condicional).  
* `acquireToken(…)`puede, a continuación, se usa toosilently obtener un token de acceso, lo que significa no mostrar interfaz de usuario en cualquier caso.  
* `acquireTokenPopup(…)`y `acquireTokenRedirect(…)` son ambos toointeractively utilizados solicitar un token para un recurso lo que significa que siempre Mostrar interfaz de usuario de inicio de sesión.

Cuando una aplicación necesita una toocall de token de acceso a una API Web, trata de un `acquireToken(…)`.  Si ha caducado la sesión de símbolo (token) de Hola o tenemos toocomply con una directiva de acceso condicional, Hola *acquireToken* función produce un error y Hola aplicación usa `acquireTokenPopup()` o `acquireTokenRedirect()`.

![Diagrama de flujo de la aplicación de una sola página que usa ADAL](media/active-directory-conditional-access-developer/spa-using-adal-scenario.png)

Veamos un ejemplo con el escenario de acceso condicional.  por el usuario final de Hello simplemente descargado en el sitio de hello y no tiene una sesión.  Se realiza una llamada `login()` y se obtiene un token de identificador sin autenticación multifactor.  A continuación, usuario de hello presiona un botón que requiere que los datos de toorequest de aplicación Hola de una API web.  aplicación Hello intenta toodo un `acquireToken()` pero no se puede llamar desde usuario hello no ha realizado la autenticación multifactor aún y debe toocomply con la directiva de acceso condicional de Hola.

Azure AD envía Hola espera después de la respuesta HTTP: 

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
```

Nuestra aplicación necesita hello toocatch `error=interaction_required`.  Hello aplicación puede utilizar cualquiera `acquireTokenPopup()` o `acquireTokenRedirect()` en Hola mismo recurso.  usuario de Hello es forzada toodo una autenticación multifactor. Al finalizar usuario Hola Hola la autenticación multifactor, aplicación hello se emite un nuevo token de acceso para hello recurso solicitado.

tootry este escenario, vea nuestra [ejemplo de código en nombre de otra persona JS SPA](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca).  Este ejemplo de código usa la directiva de acceso condicional de Hola y web API que se registraron anteriormente con un toodemonstrate SPA JS este escenario. Muestra cómo tooproperly identificador hello notificaciones desafío y obtener un token de acceso que se puede usar para la API Web. Como alternativa, Hola de desprotección general [Angular.js el ejemplo de código](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) para obtener información sobre un SPA Angular


## <a name="see-also"></a>Otras referencias

* toolearn más información acerca de las capacidades de hello, consulte [acceso condicional en Azure AD](../active-directory-conditional-access.md).
* Para más información sobre los ejemplos de código de Azure AD, consulte [repositorio de GitHub de ejemplos de código](https://github.com/azure-samples?utf8=%E2%9C%93&q=active-directory). 
* Para obtener más información sobre Hola AAL SDK y acceso a documentación de referencia de hello, consulte [Guía de la biblioteca](active-directory-authentication-libraries.md).
* toolearn más información acerca de los escenarios de varios inquilinos, consulte [cómo toosign en los usuarios con el patrón de varios inquilinos de hello](active-directory-devhowto-multi-tenant-overview.md).
