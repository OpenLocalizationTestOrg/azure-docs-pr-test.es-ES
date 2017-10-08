---
title: las aplicaciones cliente nativas aaaPublish - Azure AD | Documentos de Microsoft
description: "Explica cómo tooenable toocommunicate de aplicaciones de cliente nativo con el conector del Proxy de aplicación de Azure AD tooprovide el acceso remoto seguro tooyour local las aplicaciones."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a>Cómo tooenable toointeract de aplicaciones de cliente nativo con el proxy de aplicaciones

En las aplicaciones de tooweb de adición, Proxy de aplicación de Azure Active Directory también pueden ser toopublish usa las aplicaciones cliente nativas. Las aplicaciones cliente nativas son distintas de las aplicaciones web porque se instalan en un dispositivo, mientras se tiene acceso a las aplicaciones web a través de un explorador. 

El proxy de la aplicación admite aplicaciones de cliente nativo al aceptar tokens emitidos por Azure AD que se envían en encabezados HTTP de autorización estándar.

![Relación entre los usuarios finales, Azure Active Directory y las aplicaciones publicadas](./media/active-directory-application-proxy-native-client/richclientflow.png)

Usar hello Azure biblioteca de autenticación de AD, que se encarga de autenticación y admite muchos entornos del cliente, las aplicaciones nativas toopublish. Proxy de aplicación se adapta a hello [escenario de aplicación nativa tooWeb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api). Este artículo le guiará a través de hello cuatro pasos toopublish una aplicación nativa con hello biblioteca de autenticación de Azure AD y Proxy de aplicación. 

## <a name="step-1-publish-your-application"></a>Paso 1: Publicación de la aplicación
Publicar la aplicación proxy tal y como lo haría con cualquier otra aplicación y asignar usuarios tooaccess la aplicación. Para más información, consulte [Publicación de aplicaciones mediante el proxy de aplicación de Azure AD](active-directory-application-proxy-publish.md).

## <a name="step-2-configure-your-application"></a>Paso 2: Configuración de la aplicación
Configure su aplicación nativa de la manera siguiente:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Navegue demasiado**Azure Active Directory** > **registros de aplicación**.
3. Seleccione **Nuevo registro de aplicaciones**.
4. Especifique un nombre para la aplicación, seleccione **nativo** como tipo de aplicación Hola y proporcionar Hola URI de redireccionamiento para su aplicación. 

   ![Creación de un registro de aplicaciones](./media/active-directory-application-proxy-native-client/create.png)
5. Seleccione **Crear**.

Para más información sobre cómo crear un registro de aplicación, consulte [Integración de aplicaciones con Azure Active Directory](.//develop/active-directory-integrating-applications.md).


## <a name="step-3-grant-access-tooother-applications"></a>Paso 3: Aplicaciones conceder acceso tooother
Habilitar las aplicaciones de toobe expuesta tooother aplicación nativa de hello en el directorio:

1. Todavía en **registros de aplicación**, seleccione Hola nueva aplicación nativa que acaba de crear.
2. Seleccione **Permisos necesarios**.
3. Seleccione **Agregar**.
4. Primer paso Hola abierto, **seleccionar una API**.
5. Usar Hola búsqueda barra toofind Hola Proxy de aplicación aplicación que se publicó en la primera sección de Hola. Elija la aplicación y haga clic en **Seleccionar**. 

   ![Busque la aplicación de proxy de hello](./media/active-directory-application-proxy-native-client/select_api.png)
6. Segundo paso Hola abierto, **seleccione permisos**.
7. Usar la aplicación de proxy de aplicación nativa acceso tooyour de hello casilla toogrant, a continuación, haga clic en **seleccione**.

   ![Conceder acceso tooproxy aplicación](./media/active-directory-application-proxy-native-client/select_perms.png)
8. Seleccione **Listo**.


## <a name="step-4-edit-hello-active-directory-authentication-library"></a>Paso 4: Editar Hola biblioteca de autenticación de Active Directory
Editar código de aplicación nativa de hello en contexto de autenticación de Hola de Hola biblioteca de autenticación de Active Directory (ADAL) tooinclude Hola siguiente texto:

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

variables de Hello en el código de ejemplo de Hola deben reemplazarse como sigue:

* **Identificador de inquilino** puede encontrarse en hello portal de Azure. Navegue demasiado**Azure Active Directory** > **propiedades** y copia Hola Id. de directorio. 
* **Dirección URL externa** es dirección URL de front-end de Hola que escribió en hello Proxy de aplicación. toofind este valor, vaya toohello **proxy de aplicación** sección de la aplicación de proxy de hello.
* **Identificador de la aplicación** de hello aplicación nativa puede encontrarse en hello **propiedades** página de aplicación nativa de Hola.
* **URI de redireccionamiento de la aplicación nativa de hello** puede encontrarse en hello **URI de redireccionamiento** página de aplicación nativa de Hola.


## <a name="see-also"></a>Otras referencias

Para obtener más información acerca del flujo de la aplicación nativa de hello, consulte [aplicación nativa tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)

Para obtener las actualizaciones y noticias más recientes de hello, visite hello [blog de Proxy de aplicación](http://blogs.technet.com/b/applicationproxyblog/)
