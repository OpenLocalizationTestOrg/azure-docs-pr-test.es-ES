---
title: 'Azure Active Directory B2C: agregar un proveedor de Azure AD mediante directivas personalizadas | Microsoft Docs'
description: "Obtenga información sobre las directivas personalizadas de Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 31f0dfe5-1ad0-4a25-a53b-8acc71bcea72
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: 9b0c32086cebc171d91da2e7bfb48136723ccd4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a>Azure Active Directory B2C: inicio de sesión con cuentas de Azure AD

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Este artículo muestra cómo tooenable sesión para los usuarios de una organización específica de Azure Active Directory (Azure AD) mediante el uso de Hola de [directivas personalizadas de](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Requisitos previos

Hola completa los pasos de hello [Introducción a las directivas personalizadas](active-directory-b2c-get-started-custom.md) artículo.

Estos pasos incluyen:

1. Creación de un inquilino de Azure Active Directory B2C (Azure AD B2C).
2. Creación de una aplicación de Azure AD B2C.
3. Registro de dos aplicaciones de motor de directivas.
4. Configuración de claves.
5. Configurar el módulo de inicio de Hola.

## <a name="create-an-azure-ad-app"></a>Creación de una aplicación de Azure AD

inicio de sesión en tooenable para los usuarios de una determinada organización de Azure AD, necesita tooregister una aplicación en el inquilino de hello organizativa AD de Azure.

>[!NOTE]
> Utilizamos "contoso.com" para el inquilino Hola organizativa AD de Azure y "fabrikamb2c.onmicrosoft.com" como inquilino de Azure AD B2C Hola Hola siguiendo las instrucciones.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
1. En la barra superior de hello, seleccione su cuenta. De hello **Directory** elija inquilino Hola organizativa AD de Azure donde desee tooregister la aplicación (contoso.com).
1. Seleccione **más servicios** en el panel izquierdo de Hola y busque "Registros de aplicación".
1. Seleccione **Nuevo registro de aplicaciones**.
1. Escriba el nombre de la aplicación (por ejemplo, `Azure AD B2C App`).
1. Seleccione **aplicación Web / API** para el tipo de aplicación Hola.
1. Para **dirección URL de inicio de sesión**, escriba Hola después de la dirección URL, donde `yourtenant` se sustituye por el nombre de Hola de su inquilino de Azure AD B2C (`fabrikamb2c.onmicrosoft.com`):

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. Guardar el identificador de la aplicación hello.
1. Seleccione la aplicación hello recién creado.
1. En hello **configuración** hoja, seleccione **claves**.
1. Cree una clave y guárdela. Se utilizará en los pasos de hello en la sección siguiente Hola.

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a>Agregar tooAzure clave de hello AD de Azure AD B2C

Necesita clave de la aplicación hello toostore contoso.com en su inquilino de Azure AD B2C. toodo esto:
1. Vaya el inquilino de Azure AD B2C tooyour y seleccione **B2C configuración** > **identidad experiencia Framework** > **claves de directiva**.
1. Seleccione **+Agregar**.
1. Seleccione o especifique estas opciones:
   * Seleccione **Manual**.
   * En **Nombre**, elija un nombre que coincida con el nombre del inquilino de Azure AD (por ejemplo, `ContosoAppSecret`).  prefijo de Hello `B2C_1A_` se agrega automáticamente toohello nombre de la clave.
   * Pegue la clave de aplicación Hola **secreto** cuadro.
   * Seleccione **Firma**.
1. Seleccione **Crear**.
1. Confirme que ha creado la clave de hello `B2C_1A_ContosoAppSecret`.


## <a name="add-a-claims-provider-in-your-base-policy"></a>Adición de un proveedor de notificaciones a una directiva de base

Si desea que los usuarios toosign de mediante Azure AD, deberá toodefine Azure AD como un proveedor de notificaciones. En otras palabras, necesita un punto de conexión que se puede comunicar con Azure AD B2C toospecify. punto de conexión de Hello proporcionará un conjunto de notificaciones que usan Azure AD B2C tooverify que ha autenticado un usuario específico. 

Puede definir Azure AD como un proveedor de notificaciones mediante la adición de Azure AD toohello `<ClaimsProvider>` nodo en el archivo de extensión de hello de la directiva:

1. Abra el archivo de extensión de hello (TrustFrameworkExtensions.xml) desde el directorio de trabajo.
1. Buscar hello `<ClaimsProviders>` sección. Si no existe, debe agregarlo en el nodo raíz de Hola.
1. Agregue un nuevo nodo `<ClaimsProvider>` como se indica a continuación:

    ```XML
    <ClaimsProvider>
        <Domain>Contoso</Domain>
        <DisplayName>Login using Contoso</DisplayName>
        <TechnicalProfiles>
            <TechnicalProfile Id="ContosoProfile">
                <DisplayName>Contoso Employee</DisplayName>
                <Description>Login with your Contoso account</Description>
                <Protocol Name="OpenIdConnect"/>
                <OutputTokenFormat>JWT</OutputTokenFormat>
                <Metadata>
                    <Item Key="METADATA">https://login.windows.net/contoso.com/.well-known/openid-configuration</Item>
                    <Item Key="ProviderName">https://sts.windows.net/00000000-0000-0000-0000-000000000000/</Item>
                    <Item Key="client_id">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="IdTokenAudience">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="response_types">id_token</Item>
                    <Item Key="UsePolicyInRedirectUri">false</Item>
                </Metadata>
                <CryptographicKeys>
                    <Key Id="client_secret" StorageReferenceId="B2C_1A_ContosoAppSecret"/>
                </CryptographicKeys>
                <OutputClaims>
                    <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="oid"/>
                    <OutputClaim ClaimTypeReferenceId="tenantId" PartnerClaimType="tid"/>
                    <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
                    <OutputClaim ClaimTypeReferenceId="surName" PartnerClaimType="family_name" />
                    <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
                    <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="contosoAuthentication" />
                    <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="AzureADContoso" />
                </OutputClaims>
                <OutputClaimsTransformations>
                    <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
                    <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
                    <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
                    <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
                </OutputClaimsTransformations>
                <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
            </TechnicalProfile>
        </TechnicalProfiles>
    </ClaimsProvider>
    ```

1. En hello `<ClaimsProvider>` nodo, el valor de Hola de actualización para `<Domain>` tooa valor único que puede ser usado toodistinguish desde otros proveedores de identidad.
1. En hello `<ClaimsProvider>` nodo, el valor de Hola de actualización para `<DisplayName>` tooa nombre descriptivo para hello proveedor de notificaciones. Este valor no se utiliza actualmente.

### <a name="update-hello-technical-profile"></a>Actualizar perfil técnica Hola

tooget un token de hello extremo de Azure AD, necesita protocolos de hello toodefine que Azure AD B2C debe usar toocommunicate con Azure AD. Esto se realiza dentro de hello `<TechnicalProfile>` elemento de `<ClaimsProvider>`.
1. Actualizar el Id. de Hola de hello `<TechnicalProfile>` nodo. Este identificador es toothis toorefer usado perfil técnica de otras partes de la directiva de Hola.
1. Actualizar el valor de Hola para `<DisplayName>`. Este valor se mostrará en el botón de inicio de sesión de hello en la pantalla de inicio de sesión.
1. Actualizar el valor de Hola para `<Description>`.
1. Azure AD usa el protocolo de OpenID Connect de hello, por lo que asegúrese de que el valor de hello `<Protocol>` es `"OpenIdConnect"`.

Necesita tooupdate hello `<Metadata>` sección en el archivo XML de hello, que hace referencia valores de configuración de tooearlier tooreflect Hola para específica de su inquilino de Azure AD. En el archivo XML de hello, actualice los valores de metadatos de saludo de la manera siguiente:

1. Establecer `<Item Key="METADATA">` demasiado`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, donde `yourAzureADtenant` es el nombre del inquilino de Azure AD (contoso.com).
1. Abra el explorador y vaya toohello `METADATA` dirección URL que acaba de actualizar.
1. En el Explorador de hello, busque el objeto de "emisor" hello y copie su valor. Debería ser similar a Hola siguiente: `https://sts.windows.net/{tenantId}/`.
1. Pegue el valor de Hola para `<Item Key="ProviderName">` en el archivo XML de hello.
1. Establecer `<Item Key="client_id">` toohello Id. de aplicación de registro de una aplicación Hola.
1. Establecer `<Item Key="IdTokenAudience">` toohello Id. de aplicación de registro de una aplicación Hola.
1. Asegúrese de que `<Item Key="response_types">` se establece demasiado`id_token`.
1. Asegúrese de que `<Item Key="UsePolicyInRedirectUri">` se establece demasiado`false`.

También necesita toolink secreto de hello Azure AD que ha registrado en su toohello de inquilino de Azure AD B2C Azure AD `<ClaimsProvider>` información:

* Hola `<CryptographicKeys>` sección Hola anterior archivo XML, actualice el valor de hello para `StorageReferenceId` toohello el identificador de referencia de secreto de Hola que definiera (por ejemplo, `ContosoAppSecret`).

### <a name="upload-hello-extension-file-for-verification"></a>Cargar archivo de extensión de hello para la comprobación

Hasta ahora, ha configurado la directiva para que Azure AD B2C sepa cómo toocommunicate con su directorio Azure AD. Intente cargar el archivo de extensión de hello de su tooconfirm simplemente de directiva que no tenga problemas hasta ahora. toodo para:

1. Abra hello **todas las directivas** hoja en el inquilino de Azure AD B2C.
1. Comprobar hello **sobrescribir directiva Hola si existe** cuadro.
1. Cargar archivo de extensión de hello (TrustFrameworkExtensions.xml) y asegúrese de que no considerará no válido de Hola.

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a>Registrar viaje usuario de tooa de proveedor de notificaciones de hello Azure AD

Ahora debe tooadd hello Azure AD identidad proveedor tooone de los viajes de usuario. En este momento, se ha configurado el proveedor de identidades de hello, pero no está disponible en cualquiera de las pantallas de sesión-up/inicio de sesión de Hola. toomake está disponible, se creará un duplicado de un viaje de usuario de plantilla existente y, a continuación, modificarlo para que también dispone de proveedor de identidades de hello Azure AD:

1. Abra el archivo de base de hello de la directiva (por ejemplo, TrustFrameworkBase.xml).
1. Buscar hello `<UserJourneys>` Hola de elemento y copia todo `<UserJourney>` nodo que incluya `Id="SignUpOrSignIn"`.
1. Abra el archivo de extensión de hello (por ejemplo, TrustFrameworkExtensions.xml) y busque hello `<UserJourneys>` elemento. Si no existe el elemento hello, agregue uno.
1. Hola Pegar todo `<UserJourney>` nodo que ha copiado como elemento secundario de hello `<UserJourneys>` elemento.
1. Cambiar el nombre de Id. de Hola de viaje de hello nuevo usuario (por ejemplo, cambiar el nombre como `SignUpOrSignUsingContoso`).

### <a name="display-hello-button"></a>Hola de presentación "button"

Hola `<ClaimsProviderSelection>` elemento es análogo tooan el botón del proveedor de identidad en una pantalla de inicio de sesión-up/inicio de sesión de. Si agrega un `<ClaimsProviderSelection>` elemento para Azure AD, un nuevo botón aparezca cuando llega a un usuario en la página de Hola. tooadd este elemento:

1. Buscar hello `<OrchestrationStep>` nodo que incluya `Order="1"` en viaje de usuario de Hola que acaba de crear.
1. Agregue Hola siguiente:

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. Establecer `TargetClaimsExchangeId` tooan de valor adecuado. Se recomienda siguiente Hola misma convención de otras personas:  *\[ClaimProviderName\]Exchange*.

### <a name="link-hello-button-tooan-action"></a>Acción del botón de vínculo hello tooan

Ahora que tiene un botón en su lugar, debe toolink tooan acción. acción de Hello, en este caso, es para Azure AD B2C toocommunicate con Azure AD tooreceive un token. Acción de vínculo Hola botón tooan vinculando perfil técnico hello para el proveedor de notificaciones de Azure AD:

1. Buscar hello `<OrchestrationStep>` que incluye `Order="2"` en hello `<UserJourney>` nodo.
1. Agregue Hola siguiente:

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. Actualización `Id` toohello mismo valor que el de `TargetClaimsExchangeId` Hola sección anterior.
1. Actualización `TechnicalProfileReferenceId` toohello ID de hello técnica de perfil que creó anteriormente (ContosoProfile).

### <a name="upload-hello-updated-extension-file"></a>Cargar archivo de extensión actualizada de hello

Ha terminado de modificar el archivo de extensión Hola. Guarde y A continuación, cargar archivo hello y asegúrese de que todas las validaciones se realizan correctamente.

### <a name="update-hello-rp-file"></a>Archivo de actualización Hola RP

Ahora necesita tooupdate Hola archivo entidad (RP) confianza que se iniciará el proceso de usuario de Hola que acaba de crear:

1. Realizar una copia de SignUpOrSignIn.xml en el directorio de trabajo y cambie su nombre (por ejemplo, cámbiele el nombre tooSignUpOrSignInWithAAD.xml).
1. Abra Hola Hola nuevo para archivo y actualización de `PolicyId` atributo `<TrustFrameworkPolicy>` con un valor único (por ejemplo, SignUpOrSignInWithAAD). <br> Será Hola nombre de la directiva (por ejemplo, B2C\_1A\_SignUpOrSignInWithAAD).
1. Modificar hello `ReferenceId` atributo `<DefaultUserJourney>` toomatch Hola ID de viaje Hola de usuario nueva que ha creado (SignUpOrSignUsingContoso).
1. Guardar los cambios y cargar el archivo hello.

## <a name="troubleshooting"></a>Solución de problemas

Probar directiva personalizada de Hola que acaba de cargar abriendo la hoja y haciendo clic **ejecutar ahora**. Conozca los problemas de toodiagnose, [solución de problemas de](active-directory-b2c-troubleshoot-custom.md).

## <a name="next-steps"></a>Pasos siguientes

Proporcionar comentarios demasiado[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).
