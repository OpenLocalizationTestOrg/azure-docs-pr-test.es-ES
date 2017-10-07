---
title: "Azure Active Directory B2C: adición de Google + como un proveedor de identidades de OAuth2 mediante directivas personalizadas"
description: Ejemplo donde se usa Google+ como proveedor de identidades mediante el protocolo OAuth2
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 4feff21979c9c3b3b12c7a1cae4db0121d1bd79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a>Azure Active Directory B2C: adición de Google + como un proveedor de identidades de OAuth2 mediante directivas personalizadas

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Esta guía le mostrará cómo tooenable sesión para los usuarios de la cuenta de Google + mediante el uso de Hola de [directivas personalizadas de](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Requisitos previos

Hola completa los pasos de hello [Introducción a las directivas personalizadas](active-directory-b2c-get-started-custom.md) artículo.

Estos pasos incluyen:

1.  Crear una aplicación de la cuenta de Google+
2.  Agregar Hola Google + cuenta aplicación clave tooAzure AD B2C
3.  Agregar directiva de tooa de proveedor de notificaciones
4.  Registrar Hola Google + cuenta notificaciones proveedor tooa usuario viaje
5.  Cargando Hola directiva tooan Azure AD B2C inquilino y la prueba

## <a name="create-a-google-account-application"></a>Creación de una aplicación de la cuenta de Google+
toouse Google + como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita una aplicación de Google + toocreate y proporcionarla con los parámetros correctos de Hola. Puede registrar una aplicación de Google+ aquí: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).

1.  Vaya toohello [Google Developers Console](https://console.developers.google.com/) e inicie sesión con sus credenciales de cuenta de Google +.
2.  Haga clic en **Create project** (Crear proyecto), escriba un nombre de proyecto en **Project name** y haga clic en **Create** (Crear).

3.  Haga clic en hello **menú proyectos**.

    ![Cuenta de Google+: Selección del proyecto](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  Haga clic en hello  **+**  botón.

    ![Cuenta de Google+: Creación de un nuevo proyecto](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  Escriba un **nombre de proyecto** y luego haga clic en **Create** (Crear).

    ![Cuenta de Google+: Nuevo proyecto](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  Espere a que el proyecto de hello está listo y haga clic en hello **menú proyectos**.

    ![Cuenta de Google +: espere a que el nuevo proyecto es toouse listo](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  Haga clic en el nombre del proyecto.

    ![Cuenta de Google +: nuevo proyecto de hello Select](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  Haga clic en **API Manager** y, a continuación, haga clic en **credenciales** Hola barra de navegación izquierda.
9.  Haga clic en hello **pantalla de consentimiento de OAuth** ficha situada en la parte superior de Hola.

    ![Cuenta de Google+: Configuración de la pantalla de consentimiento de OAuth](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  Seleccione o especifique una dirección de correo electrónico válida en **Email address**, especifique un nombre de producto en **Product name** y haga clic en **Save** (Guardar).

    ![Google+: Credenciales de la aplicación](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  Haga clic en **New credentials** (Nuevas credenciales) y, luego, elija **OAuth client ID** (Id. de cliente de OAuth).

    ![Google+: Creación de nuevas credenciales de aplicación](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  En **Application type** (Tipo de aplicación), seleccione **Web application** (Aplicación web).

    ![Google+: Selección del tipo de aplicación](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  Proporcionar un **nombre** para la aplicación, escriba `https://login.microsoftonline.com` en hello **orígenes de JavaScript autorizados** campo, y `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en hello **autorizadas redirigir URI**campo. Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contosob2c.onmicrosoft.com). Hola **{tenant}** valor distingue mayúsculas de minúsculas. Haga clic en **Crear**.

    ![Google+: Provisión de los orígenes y los URI de redirección autorizados de JavaScript](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  Copiar valores de hello de **Id. de cliente** y **secreto de cliente**. Necesita ambos tooconfigure Google + como proveedor de identidades en su inquilino. **Secreto del cliente** es una credencial de seguridad importante.

    ![Google + - valores de hello de copia de secreto de cliente y el Id. de cliente](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a>Agregar Hola Google + cuenta aplicación clave tooAzure AD B2C
Federación con cuentas de Google + requiere un secreto de cliente para tootrust de cuenta de Google + Azure AD B2C en nombre de la aplicación hello. Debe toostore su secreto de aplicación de Google + en el inquilino de Azure AD B2C:  

1.  Vaya el inquilino de Azure AD B2C tooyour y seleccione **configuración B2C** > **Framework de la experiencia de identidad**
2.  Seleccione **claves de directiva** claves de hello tooview disponibles en el inquilino.
3.  Haga clic en **+Agregar**.
4.  En **Opciones**, use **Manual**.
5.  En **Nombre**, use `GoogleSecret`.  
    prefijo de Hello `B2C_1A_` podrían agregarse automáticamente.
6.  Hola **secreto** cuadro, escriba el secreto de aplicación de Microsoft desde https://apps.dev.microsoft.com
7.  En **Uso de claves**, use **Firma**.
8.  Haga clic en **Crear**
9.  Confirme que ha creado la clave de hello `B2C_1A_GoogleSecret`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Adición de un proveedor de notificaciones en la directiva de extensión

Si desea toosign de usuarios mediante el uso de la cuenta de Google +, necesita toodefine Google + cuenta como un proveedor de notificaciones. En otras palabras, necesita un punto de conexión que Azure AD B2C se comunica con toospecify. punto de conexión de Hello proporciona un conjunto de notificaciones que usan Azure AD B2C tooverify que ha autenticado un usuario específico.

Defina la cuenta de Google+ como proveedor de notificaciones; para ello, agregue el nodo `<ClaimsProvider>` en el archivo de la directiva de extensión:

1.  Abra el archivo de directiva de extensión de hello (TrustFrameworkExtensions.xml) desde el directorio de trabajo. Si necesita un editor XML, [pruebe Visual Studio Code](https://code.visualstudio.com/download), un editor multiplataforma ligero.
2.  Buscar hello `<ClaimsProviders>` sección
3.  Agregar Hola siguiente fragmento XML en hello `ClaimsProviders` elemento y reemplace `client_id` valor con su Google + cuenta aplicación ID de cliente antes de guardar el archivo hello.  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want hello user tooselect his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Registrar el proveedor de notificaciones de cuenta de hello Google + tooSign seguridad o iniciar sesión en el viaje de usuario

se ha configurado el proveedor de identidades de Hola.  Sin embargo, no está disponible en ninguna de hello sesión-up/inicio de sesión de pantallas. Agregar usuario tooyour de hello Google + cuenta identidad proveedor `SignUpOrSignIn` viaje de usuario. toomake está disponible, se crea un duplicado de un viaje de usuario de plantilla existente.  A continuación, agregamos Hola Google + cuenta Yahoo!:

>[!NOTE]
>
>Si ha copiado hello `<UserJourneys>` elemento de archivo de base de su archivo de extensión de directiva de toohello (TrustFrameworkExtensions.xml), puede omitir la sección toothis.

1.  Abra el archivo de base de hello de la directiva (por ejemplo, TrustFrameworkBase.xml).
2.  Buscar hello `<UserJourneys>` elemento y copia Hola todo el contenido de `<UserJourneys>` nodo.
3.  Abra el archivo de extensión de hello (por ejemplo, TrustFrameworkExtensions.xml) y busque hello `<UserJourneys>` elemento. Si no existe el elemento hello, agregue uno.
4.  Pegue todo el contenido de hello `<UserJournesy>` nodo que ha copiado como elemento secundario de hello `<UserJourneys>` elemento.

### <a name="display-hello-button"></a>Botón de mostrar hello
Hola `<ClaimsProviderSelections>` elemento define la lista de Hola de opciones de selección del proveedor de notificaciones y su orden.  `<ClaimsProviderSelection>`elemento es análogo tooan el botón del proveedor de identidad en una página de inicio de sesión-up/inicio de sesión de. Si agrega un `<ClaimsProviderSelection>` elemento para la cuenta de Google +, un nuevo botón aparezca cuando llega a un usuario en la página de Hola. tooadd este elemento:

1.  Buscar hello `<UserJourney>` nodo que incluya `Id="SignUpOrSignIn"` en viaje de usuario de Hola que ha copiado.
2.  Busque hello `<OrchestrationStep>` nodo que incluye`Order="1"`
3.  Agregue el siguiente fragmento de código XML en el nodo `<ClaimsProviderSelections>`:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Acción del botón de vínculo hello tooan
Ahora que tiene un botón en su lugar, debe toolink tooan acción. acción de Hello, en este caso, es para Azure AD B2C toocommunicate con Google + cuenta tooreceive un token.

1.  Buscar hello `<OrchestrationStep>` que incluye `Order="2"` en hello `<UserJourney>` nodo.
2.  Agregue el siguiente fragmento de código XML en el nodo `<ClaimsExchanges>`:

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * Asegúrese de hello `Id` tiene Hola mismo valor que el de `TargetClaimsExchangeId` en la sección anterior de Hola
> * Asegúrese de `TechnicalProfileReferenceId` se estableció el identificador de perfil técnico toohello que creó anteriormente (Google-OAUTH).

## <a name="upload-hello-policy-tooyour-tenant"></a>Cargar el inquilino de hello directiva tooyour
1.  Hola [portal de Azure](https://portal.azure.com), cambiar a hello [contexto de su inquilino de Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md), abra hello y **Azure AD B2C** hoja.
2.  Seleccione **Marco de experiencia de identidad**.
3.  Abra hello **todas las directivas** hoja.
4.  Seleccione **Cargar directiva**.
5.  Comprobar **sobrescribir directiva Hola si existe** cuadro.
6.  **Cargar** TrustFrameworkExtensions.xml y asegúrese de que no considerará no válido de Hola

## <a name="test-hello-custom-policy-by-using-run-now"></a>Probar directiva personalizada de hello mediante Ejecutar ahora
1.  Abra **configuración de Azure AD B2C** y vaya demasiado**identidad experiencia Framework**.

    >[!NOTE]
    >
    >    **Ejecutar ahora** requiere al menos una aplicación toobe registrada previamente en el inquilino de Hola. 
    >    toolearn tooregister aplicaciones, vea hello Azure AD B2C [Introducción](active-directory-b2c-get-started.md) artículo o hello [registro de la aplicación](active-directory-b2c-app-registration.md) artículo.


2.  Abra **B2C_1A_signup_signin**, Hola directiva personalizada de confianza (RP) de la entidad que ha cargado. Seleccione **Ejecutar ahora**.
3.  Debe ser capaz de toosign con cuenta de Google +.

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a>[Opcional] Registrar Hola Google + cuenta notificaciones proveedor tooProfile Editar usuario viaje
Tal vez desee tooadd Hola Google + cuenta proveedor de identidades también tooyour usuario `ProfileEdit` viaje de usuario. toomake está disponible, se repita Hola últimos dos pasos:

### <a name="display-hello-button"></a>Botón de mostrar hello
1.  Abra el archivo de extensión de hello de la directiva (por ejemplo, TrustFrameworkExtensions.xml).
2.  Buscar hello `<UserJourney>` nodo que incluya `Id="ProfileEdit"` en viaje de usuario de Hola que ha copiado.
3.  Busque hello `<OrchestrationStep>` nodo que incluye`Order="1"`
4.  Agregue el siguiente fragmento de código XML en el nodo `<ClaimsProviderSelections>`:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Acción del botón de vínculo hello tooan
1.  Buscar hello `<OrchestrationStep>` que incluye `Order="2"` en hello `<UserJourney>` nodo.
2.  Agregue el siguiente fragmento de código XML en el nodo `<ClaimsExchanges>`:

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Probar la directiva de edición de perfil personalizada hello mediante Ejecutar ahora

1.  Abra **configuración de Azure AD B2C** y vaya demasiado**identidad experiencia Framework**.
2.  Abra **B2C_1A_ProfileEdit**, Hola directiva personalizada de confianza (RP) de la entidad que ha cargado. Seleccione **Ejecutar ahora**.
3.  Debe ser capaz de toosign con cuenta de Google +.

## <a name="download-hello-complete-policy-files"></a>Descargar archivos de directiva completa Hola
Opcional: Se recomienda que elabore su escenario con sus propios archivos de directiva personalizada después de completar la introducción a las directivas personalizadas recorra en lugar de utilizar estos archivos de ejemplo de Hola.  [Archivos de directiva de ejemplo de referencia](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
