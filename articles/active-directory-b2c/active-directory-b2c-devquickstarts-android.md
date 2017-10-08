---
title: "Azure Active Directory B2C: adquisición de un token con una aplicación Android | Microsoft Docs"
description: "En este artículo le mostrará cómo toocreate una aplicación Android que utiliza AppAuth con identidades de usuario de Azure Active Directory B2C toomanage y autentica a los usuarios."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: d00947c3-dcaa-4cb3-8c2e-d94e0746d8b2
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 03/06/2017
ms.author: parakhj
ms.openlocfilehash: 0236398673115a34951f035cb1e73e89417abf86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a>Azure AD B2C: Inicio de sesión con una aplicación Android

plataforma de identidad de Microsoft Hello usa estándares abiertos como OAuth2 y OpenID Connect. Esto permite a los desarrolladores tooleverage cualquier biblioteca desean toointegrate con nuestros servicios. tooaid a los desarrolladores en el uso de nuestra plataforma con otras bibliotecas, hemos escrito algunos tutoriales como este una toodemonstrate forma tooconfigure 3ª parte bibliotecas tooconnect toohello Microsoft plataforma de identidad. La mayoría de las bibliotecas que implementan [especificación de hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) será capaz de tooconnect toohello Microsoft Identity plataforma.

> [!WARNING]
> No se proporcionan correcciones para bibliotecas de terceros y no se ha realizado ninguna revisión de esas bibliotecas. En este ejemplo se usa una biblioteca de entidad 3rd piden AppAuth que se ha probado la compatibilidad de escenarios básicos con hello Azure AD B2C. Problemas y las solicitudes de características deben ser el proyecto de código abierto de la biblioteca de toohello dirigida. Vea [este](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) artículo para más información.  
>
>

Si es nuevo tooOAuth2 o OpenID Connect gran parte de esta configuración de ejemplo puede que no tenga mucho sentido tooyou. Se recomienda que examine un breve [información general del protocolo de hello nos hemos mostradas aquí](active-directory-b2c-reference-protocols.md).

## <a name="get-an-azure-ad-b2c-directory"></a>Obtener un directorio de Azure AD B2C

Para poder usar Azure AD B2C, debe crear un directorio o inquilino. Un directorio es un contenedor para todos los usuarios, las aplicaciones, los grupos, etc. Si aún no tiene uno, [cree un directorio B2C](active-directory-b2c-get-started.md) antes de continuar.

## <a name="create-an-application"></a>Creación de una aplicación

A continuación, debe toocreate una aplicación en el directorio B2C. Esto proporciona información de Azure AD que necesita toocommunicate forma segura con la aplicación. toocreate una aplicación móvil, siga [estas instrucciones](active-directory-b2c-app-registration.md). Asegúrese de:

* Incluir un **Native Client** en aplicación hello.
* Hola copia **Id. de aplicación** decir tooyour asignado aplicación. Lo necesitará más adelante.
* Configurar un **URI de redireccionamiento** del cliente nativo (por ejemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect). También lo necesitará más adelante.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Crear sus directivas

En Azure AD B2C, cada experiencia del usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md). Esta aplicación contiene una experiencia de identidad: una combinación de inicio de sesión y registro. Deberá toocreate esta directiva, tal y como se describe en el [artículo de referencia de directiva](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Cuando se crea la directiva de hello, no olvide:

* Elija hello **nombre para mostrar** como un atributo de inicio de sesión en la directiva.
* Elija hello **nombre para mostrar** y **Id. de objeto** notificaciones de la aplicación en cada directiva. Puede elegir también otras notificaciones.
* Hola copia **nombre** de cada directiva después de haberlo creado. Deberían tener el prefijo de hello `b2c_1_`.  Necesitará el nombre de directiva de hello más tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Después de crear las directivas, está listo toobuild la aplicación.

## <a name="download-hello-sample-code"></a>Descargar código de muestra de Hola

Hemos proporcionado un ejemplo de trabajo que usa AppAuth con Azure AD B2C [en GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c). Puede descargar código de hello y ejecutarlo. Rápidamente puede empezar a trabajar con su propia aplicación con su propia configuración de Azure AD B2C siguiendo las instrucciones de Hola Hola [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).

ejemplo Hello es una modificación del ejemplo de Hola proporcionado por [AppAuth](https://openid.github.io/AppAuth-Android/). Visite su toolearn de página más sobre AppAuth y sus características.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Modificar la aplicación toouse Azure AD B2C con AppAuth

> [!NOTE]
> AppAuth admite Android API 16 (Jellybean) y versiones superiores. Se recomienda usar API 23 y superior.
>

### <a name="configuration"></a>Configuración

Puede configurar la comunicación con Azure AD B2C detectar Hola especificar URI o especificando el extremo de autorización de Hola y URI de extremo token. En cualquier caso, necesitará Hola siguiente información:

* Id. de inquilino (por ejemplo, contoso.onmicrosoft.com)
* Nombre de la directiva (por ejemplo, B2C\_1\_SignUpIn)

Si decide tooautomatically detectar extremo de autorización y token de hello URI, necesitará información de toofetch de la detección de hello URI. detección de Hello URI puede generarse mediante la sustitución Hola inquilino\_hello directiva y el Id. de\_nombre Hola después de la dirección URL:

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

A continuación, puede adquirir autorización hello y URI de extremo de token y crear un objeto de AuthorizationServiceConfiguration ejecutando Hola siguiente:

```java
final Uri issuerUri = Uri.parse(mDiscoveryURI);
AuthorizationServiceConfiguration config;

AuthorizationServiceConfiguration.fetchFromIssuer(
    issuerUri,
    new RetrieveConfigurationCallback() {
      @Override public void onFetchConfigurationCompleted(
          @Nullable AuthorizationServiceConfiguration serviceConfiguration,
          @Nullable AuthorizationException ex) {
        if (ex != null) {
            Log.w(TAG, "Failed tooretrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed tooauthorization...
        }
      }
  });
```

En lugar de utilizar la autorización de detección tooobtain hello y URI de extremo de token, también puede especificar ellos explícitamente mediante la sustitución Hola inquilino\_hello directiva y el Id. de\_nombre en la dirección URL de hello:

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

Siguiente ejecución Hola código toocreate AuthorizationServiceConfiguration objeto:

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a>Autorización

Después de configurar o recuperar una configuración de servicio de autorización, es posible construir una autorización. solicitar toocreate hello, necesitará Hola siguiente información:

* Id. de cliente (ejemplo, 00000000-0000-0000-0000-000000000000)
* URI de redireccionamiento con un esquema personalizado (por ejemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)

Ambos elementos se deberían haber guardado cuando [registró la aplicación](#create-an-application).

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

Consulte toohello [AppAuth guía](https://openid.github.io/AppAuth-Android/) en cómo toocomplete Hola resto del proceso de Hola. Si necesita tooquickly empezar a trabajar con una aplicación en funcionamiento, visite [nuestro ejemplo](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c). Siga los pasos de Hola Hola [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter su propia configuración de Azure AD B2C.

Estamos siempre toofeedback abierta y sugerencias. Si tiene dificultades con este tema, o tiene las recomendaciones para mejorar el contenido, le agradeceríamos sus comentarios en la parte inferior de Hola de página de Hola. Para las solicitudes de características, agregarlos demasiado[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).

