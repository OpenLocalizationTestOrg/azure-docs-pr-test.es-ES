---
title: "Azure Active Directory B2C: adición de una cuenta de Microsoft (MSA) como proveedor de identidades mediante directivas personalizadas"
description: Ejemplo en el que se usa Microsoft como proveedor de identidades mediante el protocolo OpenID Connect (OIDC).
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
ms.openlocfilehash: 577ac612f69015e6790f2fa9f2cfb42c2b524b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a>Azure Active Directory B2C: adición de una cuenta de Microsoft (MSA) como proveedor de identidades mediante directivas personalizadas

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Este artículo muestra cómo tooenable inicio de sesión de los usuarios de la cuenta de Microsoft (MSA) mediante el uso de Hola de [directivas personalizadas de](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Requisitos previos
Hola completa los pasos de hello [Introducción a las directivas personalizadas](active-directory-b2c-get-started-custom.md) artículo.

Estos pasos incluyen:

1.  Crear una aplicación de la cuenta de Microsoft
2.  Agregar Hola Microsoft cuenta aplicación clave tooAzure AD B2C
3.  Agregar directiva de tooa de proveedor de notificaciones
4.  Hola Account Microsoft notificaciones proveedor tooa usuario del proceso de registro
5.  Cargando Hola directiva tooan Azure AD B2C inquilino y la prueba

## <a name="create-a-microsoft-account-application"></a>Creación de una aplicación de cuenta Microsoft
toouse cuenta de Microsoft como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita toocreate una aplicación de la cuenta de Microsoft y suministrarle los parámetros correctos de Hola. Necesita una cuenta de Microsoft. Si no tiene una, visite [https://www.live.com/](https://www.live.com/).

1.  Vaya toohello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) e inicie sesión con sus credenciales de cuenta de Microsoft.
2.  Haga clic en **Agregar una aplicación**.

    ![Cuenta de Microsoft: Adición de una aplicación](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  Proporcione un **nombre** para su aplicación, un **correo electrónico de contacto**, desactive **Permítanos que le ayudemos a empezar** y haga clic en **Crear**.

    ![Cuenta de Microsoft: Registro de la aplicación](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  Copiar valor de Hola de **identificador de la aplicación**. Se necesita lo tooconfigure cuenta de Microsoft como proveedor de identidades en su inquilino.

    ![Cuenta de Microsoft: copiar el valor de hello del identificador de aplicación](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  Haga clic en **Agregar plataforma**.

    ![Cuenta Microsoft: Agregar plataforma](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  En la lista de plataformas de hello, elija **Web**.

    ![Cuenta de Microsoft: desde la lista de plataformas de hello elegir Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  Escriba `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en hello **URI de redireccionamiento** campo. Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contosob2c.onmicrosoft.com).

    ![Cuenta de Microsoft: Establecimiento de las direcciones URL de redireccionamiento](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  Haga clic en **generar nueva contraseña** en hello **aplicación secretos** sección. Copiar contraseña nueva hello muestra en pantalla. Se necesita lo tooconfigure cuenta de Microsoft como proveedor de identidades en su inquilino. Esta contraseña es una credencial de seguridad importante.

    ![Cuenta Microsoft: Generar nueva contraseña](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Cuenta de Microsoft: copiar la contraseña nuevo de Hola](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  Casilla de Hola que dice **soporte técnico del SDK de Live** en hello **opciones avanzadas** sección. Haga clic en **Guardar**.

    ![Cuenta Microsoft: Soporte técnico de SDK de Live](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a>Agregar Hola Microsoft cuenta aplicación clave tooAzure AD B2C
Federación con cuentas de Microsoft requiere un secreto de cliente para tootrust de cuenta de Microsoft Azure AD B2C en nombre de la aplicación hello. Debe toostore su secert de aplicación de cuenta de Microsoft en el inquilino de Azure AD B2C:   

1.  Vaya el inquilino de Azure AD B2C tooyour y seleccione **configuración B2C** > **Framework de la experiencia de identidad**
2.  Seleccione **claves de directiva** claves de hello tooview disponibles en el inquilino.
3.  Haga clic en **+Agregar**.
4.  En **Opciones**, use **Manual**.
5.  En **Nombre**, use `MSASecret`.  
    prefijo de Hello `B2C_1A_` podrían agregarse automáticamente.
6.  Hola **secreto** cuadro, escriba el secreto de aplicación de Microsoft desde https://apps.dev.microsoft.com
7.  En **Uso de claves**, use **Firma**.
8.  Haga clic en **Crear**
9.  Confirme que ha creado la clave de hello `B2C_1A_MSASecret`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Adición de un proveedor de notificaciones en la directiva de extensión
Si desea toosign de usuarios mediante Microsoft Account, debe toodefine Account Microsoft como un proveedor de notificaciones. En otras palabras, necesita un punto de conexión que Azure AD B2C se comunica con toospecify. punto de conexión de Hello proporciona un conjunto de notificaciones que usan Azure AD B2C tooverify que ha autenticado un usuario específico.

Defina la cuenta de Microsoft como proveedor de notificaciones; para ello, agregue el nodo `<ClaimsProvider>` en el archivo de la directiva de extensión:

1.  Abra el archivo de directiva de extensión de hello (TrustFrameworkExtensions.xml) desde el directorio de trabajo. Si necesita un editor XML, [pruebe Visual Studio Code](https://code.visualstudio.com/download), un editor multiplataforma ligero.
2.  Buscar hello `<ClaimsProviders>` sección
3.  Agregue el siguiente fragmento XML en hello `ClaimsProviders` elemento:

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

4.  Reemplace el valor `client_id` por el id. de cliente de aplicación de la cuenta de Microsoft.

5.  Guarde el archivo hello.

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Registrar proveedor de notificaciones de hello Account Microsoft tooSign seguridad o inicio de sesión en el viaje de usuario

En este momento, se ha configurado el proveedor de identidades de hello, pero no está disponible en cualquiera de las pantallas de sesión-up/inicio de sesión de Hola. Ahora tiene un usuario tooyour de proveedor de identidad de Microsoft Account de tooadd hello `SignUpOrSignIn` viaje de usuario. toomake está disponible, se crea un duplicado de un viaje de usuario de plantilla existente.  A continuación, agregamos el proveedor de identidades de hello Account de Microsoft:

> [!NOTE]
>
>Si copió anteriormente hello `<UserJourneys>` elemento del archivo de base de su archivo de extensión de directiva de toohello `TrustFrameworkExtensions.xml`, puede omitir la sección toothis.

1.  Abra el archivo de base de hello de la directiva (por ejemplo, TrustFrameworkBase.xml).
2.  Buscar hello `<UserJourneys>` elemento y copia Hola todo el contenido de `<UserJourneys>` nodo.
3.  Abra el archivo de extensión de hello (por ejemplo, TrustFrameworkExtensions.xml) y busque hello `<UserJourneys>` elemento. Si no existe el elemento hello, agregue uno.
4.  Pegue todo el contenido de hello `<UserJournesy>` nodo que ha copiado como elemento secundario de hello `<UserJourneys>` elemento.

### <a name="display-hello-button"></a>Botón de mostrar hello
Hola `<ClaimsProviderSelections>` elemento define la lista de Hola de opciones de selección del proveedor de notificaciones y su orden.  `<ClaimsProviderSelection>`elemento es análogo tooan el botón del proveedor de identidad en una página de inicio de sesión-up/inicio de sesión de. Si agrega un `<ClaimsProviderSelection>` elemento para la cuenta de Microsoft, un nuevo botón aparezca cuando llega a un usuario en la página de Hola. tooadd este elemento:

1.  Buscar hello `<UserJourney>` nodo que incluya `Id="SignUpOrSignIn"` en viaje de usuario de Hola que ha copiado.
2.  Busque hello `<OrchestrationStep>` nodo que incluye`Order="1"`
3.  Agregue el siguiente fragmento de código XML en el nodo `<ClaimsProviderSelections>`:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Acción del botón de vínculo hello tooan
Ahora que tiene un botón en su lugar, debe toolink tooan acción. acción de Hello, en este caso, es para Azure AD B2C toocommunicate con Microsoft Account tooreceive un token. Vincular tooan acción del botón de hello vinculando perfil técnico hello para el proveedor de notificaciones de Account de Microsoft:

1.  Buscar hello `<OrchestrationStep>` que incluye `Order="2"` en hello `<UserJourney>` nodo.
2.  Agregue el siguiente fragmento de código XML en el nodo `<ClaimsExchanges>`:

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * Asegúrese de hello `Id` tiene Hola mismo valor que el de `TargetClaimsExchangeId` en la sección anterior de Hola
>   * Asegúrese de `TechnicalProfileReferenceId` se estableció el identificador de perfil técnico toohello que creó anteriormente (MSA-OIDC).

## <a name="upload-hello-policy-tooyour-tenant"></a>Cargar el inquilino de hello directiva tooyour
1.  Hola [portal de Azure](https://portal.azure.com), cambiar a hello [contexto de su inquilino de Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md), abra hello y **Azure AD B2C** hoja.
2.  Seleccione **Marco de experiencia de identidad**.
3.  Abra hello **todas las directivas** hoja.
4.  Seleccione **Cargar directiva**.
5.  Comprobar **sobrescribir directiva Hola si existe** cuadro.
6.  **Cargar** TrustFrameworkExtensions.xml y asegúrese de que no considerará no válido de Hola

## <a name="test-hello-custom-policy-by-using-run-now"></a>Probar directiva personalizada de hello mediante Ejecutar ahora

1.  Abra **configuración de Azure AD B2C** y vaya demasiado**identidad experiencia Framework**.
> [!NOTE]
>
>**Ejecutar ahora** requiere al menos una aplicación toobe registrada previamente en el inquilino de Hola. toolearn tooregister aplicaciones, vea hello Azure AD B2C [Introducción](active-directory-b2c-get-started.md) artículo o hello [registro de la aplicación](active-directory-b2c-app-registration.md) artículo.
2.  Abra **B2C_1A_signup_signin**, Hola directiva personalizada de confianza (RP) de la entidad que ha cargado. Seleccione **Ejecutar ahora**.
3.  Debe ser capaz de toosign sesión con la cuenta de Microsoft.

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a>[Opcional] Registrar hello Account Microsoft notificaciones proveedor tooProfile Editar usuario del proceso
Tal vez desee proveedor de identidades de Microsoft Account tooadd Hola también tooyour usuario `ProfileEdit` viaje de usuario. toomake está disponible, se repita Hola últimos dos pasos:

### <a name="display-hello-button"></a>Botón de mostrar hello
1.  Abra el archivo de extensión de hello de la directiva (por ejemplo, TrustFrameworkExtensions.xml).
2.  Buscar hello `<UserJourney>` nodo que incluya `Id="ProfileEdit"` en viaje de usuario de Hola que ha copiado.
3.  Busque hello `<OrchestrationStep>` nodo que incluye`Order="1"`
4.  Agregue el siguiente fragmento de código XML en el nodo `<ClaimsProviderSelections>`:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Acción del botón de vínculo hello tooan
1.  Buscar hello `<OrchestrationStep>` que incluye `Order="2"` en hello `<UserJourney>` nodo.
2.  Agregue el siguiente fragmento de código XML en el nodo `<ClaimsExchanges>`:

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Probar la directiva de edición de perfil personalizada hello mediante Ejecutar ahora
1.  Abra **configuración de Azure AD B2C** y vaya demasiado**identidad experiencia Framework**.
2.  Abra **B2C_1A_ProfileEdit**, Hola directiva personalizada de confianza (RP) de la entidad que ha cargado. Seleccione **Ejecutar ahora**.
3.  Debe ser capaz de toosign sesión con la cuenta de Microsoft.

## <a name="download-hello-complete-policy-files"></a>Descargar archivos de directiva completa Hola
Opcional: Se recomienda que elabore su escenario con sus propios archivos de directiva personalizada después de completar la introducción a las directivas personalizadas recorra en lugar de utilizar estos archivos de ejemplo de Hola.  [Archivos de directiva de ejemplo de referencia](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
