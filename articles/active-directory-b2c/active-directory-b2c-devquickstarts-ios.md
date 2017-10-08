---
title: "Adquisición de un token con una aplicación iOS - Azure AD B2C | Microsoft Docs"
description: "En este artículo le mostrará cómo toocreate una aplicación de iOS que utiliza AppAuth con identidades de usuario de Azure Active Directory B2C toomanage y autentica a los usuarios."
services: active-directory-b2c
documentationcenter: ios
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: e7cbe2de6e9ae3d45448cdd36292c457a0ef4887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a>Azure AD B2C: Inicio de sesión con una aplicación iOS

plataforma de identidad de Microsoft Hello usa estándares abiertos como OAuth2 y OpenID Connect. El uso de un protocolo estándar abierto ofrece más opciones a los desarrolladores al seleccionar un toointegrate de biblioteca con nuestros servicios. Hemos proporcionado en este tutorial y otros similares tooaid a los desarrolladores a escribir aplicaciones que se conectan toohello plataforma de Microsoft Identity. La mayoría de las bibliotecas que implementan [especificación de hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) son tooconnect pueda toohello la plataforma de Microsoft Identity.

> [!WARNING]
> Microsoft no proporciona correcciones para bibliotecas de terceros y no se ha realizado ninguna revisión de esas bibliotecas. Este ejemplo usa una biblioteca de terceros denominada AppAuth que se ha probado para la compatibilidad de escenarios básicos con hello Azure AD B2C. Problemas y las solicitudes de características deben ser el proyecto de código abierto de la biblioteca de toohello dirigida. Para obtener más información, consulte [este artículo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).
>
>

Si es nuevo tooOAuth2 u OpenID Connect, gran parte de esta configuración de ejemplo puede que no tenga mucho sentido tooyou. Se recomienda que examine un breve [información general del protocolo de hello nos hemos mostradas aquí](active-directory-b2c-reference-protocols.md).

## <a name="get-an-azure-ad-b2c-directory"></a>Obtener un directorio de Azure AD B2C
Para poder usar Azure AD B2C, debe crear un directorio o inquilino. Un directorio es un contenedor de todos los usuarios, aplicaciones, grupos, etc. Antes de continuar, si no tiene un directorio B2C, [créelo](active-directory-b2c-get-started.md) .

## <a name="create-an-application"></a>Creación de una aplicación
A continuación, debe toocreate una aplicación en el directorio B2C. registro de una aplicación Hola proporciona información de Azure AD que necesita toocommunicate forma segura con la aplicación. toocreate una aplicación móvil, siga [estas instrucciones](active-directory-b2c-app-registration.md). Asegúrese de:

* Incluir un **Native client** en aplicación hello.
* Hola copia **Id. de aplicación** decir tooyour asignado aplicación. Necesitará este GUID más adelante.
* Configure un **URI de redireccionamiento** con un esquema personalizado (por ejemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect). Necesitará este URI más adelante.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Crear sus directivas
En Azure AD B2C, cada experiencia del usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md). Esta aplicación contiene una experiencia de identidad: una combinación de inicio de sesión y registro. Cree esta directiva, tal como se describe en el [artículo de referencia de las directivas](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Cuando se crea la directiva de hello, no olvide:

* En **atributos suscripción**, seleccione el atributo de hello **nombre para mostrar**.  Puede seleccionar también otros atributos.
* En **notificaciones de la aplicación**, seleccione Hola notificaciones **nombre para mostrar** y **Id. de objeto del usuario**. Puede elegir también otras notificaciones.
* Hola copia **nombre** de cada directiva después de haberlo creado. Tiene como prefijo el nombre de la directiva `b2c_1_` cuando se guarda la directiva de Hola.  Necesita nombre de la directiva de hello más tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Después de crear las directivas, está listo toobuild la aplicación.

## <a name="download-hello-sample-code"></a>Descargar código de muestra de Hola
Hemos proporcionado un ejemplo de trabajo que usa AppAuth con Azure AD B2C [en GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c). Puede descargar código de hello y ejecutarlo. toouse inquilino de su propia AD B2C de Azure, siga las instrucciones de Hola Hola [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).

En este ejemplo se creó siguiendo las instrucciones del archivo Léame de Hola por hello [iOS AppAuth del proyecto en GitHub](https://github.com/openid/AppAuth-iOS). Para obtener más detalles sobre cómo funcionan los muestra de Hola y biblioteca de hello, hacer referencia a hello AppAuth README en GitHub.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Modificar la aplicación toouse Azure AD B2C con AppAuth

> [!NOTE]
> AppAuth es compatible con iOS7 y versiones superiores.  Sin embargo, es necesario toosupport sociales inicios de sesión de Google, SFSafariViewController que requiere iOS 9 o superior.
>

### <a name="configuration"></a>Configuración

Puede configurar la comunicación con Azure AD B2C especificando el extremo de autorización de Hola y URI de extremo token.  toogenerate estos URI, necesita Hola siguiente información:
* Identificador de inquilino (por ejemplo, contoso.onmicrosoft.com)
* Nombre de la directiva (por ejemplo, B2C\_1\_SignUpIn)

extremo de token de URI puede generarse mediante la sustitución Hola Hola inquilino\_hello directiva y el Id. de\_nombre Hola después de la dirección URL:

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

extremo de autorización de URI puede generarse mediante la sustitución Hola Hola inquilino\_hello directiva y el Id. de\_nombre Hola después de la dirección URL:

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

Siguiente ejecución Hola código toocreate AuthorizationServiceConfiguration objeto:

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a>Autorización

Después de configurar o recuperar una configuración de servicio de autorización, es posible construir una autorización. solicitar toocreate hello, necesita Hola siguiente información:  
* Id. de cliente (por ejemplo, 00000000-0000-0000-0000-000000000000)
* URI de redireccionamiento con un esquema personalizado (por ejemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)

Ambos elementos se deberían haber guardado cuando [registró la aplicación](#create-an-application).

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

tooset seguridad su toohello de redirección de Hola de toohandle aplicación URI con esquema personalizado de hello, necesita tooupdate lista de hello 'Esquemas de dirección URL' en su Info.pList:
* Abra Info.pList.
* Mantenga el mouse sobre una fila como 'Código de tipo de sistema operativo de agrupación' y haga clic en hello \+ símbolos.
* Cambie el nombre hello nueva fila 'tipos de URL'.
* Haga clic en hello flecha toohello a la izquierda del árbol de 'Tipos de dirección URL' tooopen Hola.
* Haga clic en hello flecha toohello a la izquierda del árbol de hello tooopen 'Elemento 0'.
* Cambie el nombre del primer elemento bajo esquemas de elemento too'URL 0.
* Haga clic en hello flecha toohello a la izquierda del árbol de hello tooopen 'Esquemas de dirección URL'.
* En la columna de 'Value' hello, hay un campo en blanco toohello de 'Elemento 0' debajo 'Esquemas de dirección URL'.  Establecer esquema único de la aplicación hello valor tooyour.  valor de Hello debe coincidir con esquema de hello usado en URL de redireccionamiento al crear objeto de OIDAuthorizationRequest Hola.  En nuestro ejemplo, hemos usado Hola esquema 'com.onmicrosoft.fabrikamb2c.exampleapp'.

Consulte toohello [AppAuth guía](https://openid.github.io/AppAuth-iOS/) en cómo toocomplete Hola resto del proceso de Hola. Si necesita tooquickly empezar a trabajar con una aplicación en funcionamiento, visite [nuestro ejemplo](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c). Siga los pasos de Hola Hola [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter su propia configuración de Azure AD B2C.

Estamos siempre toofeedback abierta y sugerencias. Si tiene dificultades con este tema, o tiene las recomendaciones para mejorar el contenido, le agradeceríamos sus comentarios en la parte inferior de Hola de página de Hola. Para las solicitudes de características, agregarlos demasiado[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).
