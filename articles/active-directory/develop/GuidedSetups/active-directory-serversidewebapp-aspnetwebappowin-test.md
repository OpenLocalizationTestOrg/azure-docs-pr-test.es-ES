---
title: "aaaAzure AD v2 ASP.NET Web Server Introducción - prueba | Documentos de Microsoft"
description: "Implementación de inicio de sesión de Microsoft en una solución ASP.NET con una aplicación basada en un explorador web tradicional mediante el estándar OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 99c7525b9146605142180962fc2a61b3c953c064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Prueba del código

Presione `F5` toorun el proyecto en Visual Studio. Hello explorador se abrirá y dirigirle demasiado*http://localhost: {port}* donde verá hello *iniciar sesión con Microsoft* botón. Continúe y haga clic en él toosign en.

Cuando esté listo tootest, use un trabajo o educativa (Azure Active Directory) o un personal (live.com, outlook.com) toosign en la cuenta. 

![Ventana Iniciar sesión en Microsoft del explorador](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Ventana Iniciar sesión en Microsoft del explorador](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a>Resultados esperados
Después de iniciar sesión, usuario de hello es redirigido toohello portada del sitio web que es hello dirección URL HTTPS especificado en la información de registro de aplicación Hola Portal de registro de aplicación de Microsoft. Esta página muestra ahora *Hola {User}* y una vínculo toosign horizontal y notificaciones de vínculo toosee Hola de un usuario: que es un controlador de autorización de vínculo toohello crean anteriormente.

### <a name="see-users-claims"></a>Ver notificaciones del usuario
Seleccione notificaciones del usuario de hello hipervínculo toosee Hola. Esto conduce toohello controlador y la vista que solo está disponible toousers que se autentican.

#### <a name="expected-results"></a>Resultados esperados
 Debería ver una tabla que contiene propiedades básicas de Hola de usuario de hello iniciado:

| Propiedad | Valor | Descripción|
|---|---|---|
| Nombre | {Nombre completo del usuario} | usuario de Hola y el apellido nombre
|Nombre de usuario | <span>user@domain.com</span>| nombre de usuario de Hello usado usuario de hello registrado tooidentify
| Asunto| {Firmante}|Una cadena toouniquely identificar inicio de sesión de usuario de hello en web Hola|
| Id. de inquilino| {Guid}| A *guid* toouniquely representan la organización de Azure Active Directory del usuario de Hola.|

Además, verá una tabla con todas las notificaciones de usuario incluidas en la solicitud de autenticación. Para obtener una lista de todas las notificaciones de un token de identificador y una explicación, consulte este [artículo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "Lista de notificaciones en token de identificador").


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a>Probar el acceso a un método que tiene un atributo *[Authorize]* (opcional)
En este paso, probará al tener acceso al controlador de autenticado hello como usuario anónimo:<br/>
Seleccione Hola vincular toosign horizontal Hola usuario y el proceso de cierre de sesión de hello completa.<br/>
Ahora en el explorador, escriba http://localhost: {port} / autenticado tooaccess el controlador que está protegido con hello `[Authorize]` atributo

#### <a name="expected-results"></a>Resultados esperados
Debería recibir el mensaje Hola necesidad de vista de tooauthenticate toosee Hola.

## <a name="additional-information"></a>Información adicional

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a>Proteger todo el sitio web
tooprotect todo el sitio web, agregar hello `AuthorizeAttribute` demasiado`GlobalFilters` en `Global.asax` `Application_Start` método:

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> **Cómo los usuarios toorestrict toosign únicamente una organización en la aplicación de tooyour**

> De forma predeterminada, las cuentas personales (incluidos outlook.com, live.com y otros), así como cuentas profesionales o educativas de cualquier empresa u organización que se integra con Azure Active Directory pueden iniciar sesión tooyour aplicación. 

> Si desea que su aplicación tooaccept inicios de sesión de sólo una organización de Azure Active Directory, reemplace hello `Tenant` parámetro en *web.config* de `Common` toohello nombre del inquilino de organización de hello: ejemplo, *contoso.onmicrosoft.com*. A continuación, cambiar hello `ValidateIssuer` argumento en su *clase de inicio de OWIN* demasiado`true`.

> los usuarios de tooallow de solo una lista de organizaciones específicas, establecer `ValidateIssuer` hello tootrue y uso `ValidIssuers` parámetro toospecify una lista de las organizaciones.

> Otra opción es un método personalizado tooimplement emisores de hello toovalidate mediante el parámetro IssuerValidator. Para más información acerca de `TokenValidationParameters`, consulte [este](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "Artículo de MSDN acerca de TokenValidationParameters") artículo de MSDN.

