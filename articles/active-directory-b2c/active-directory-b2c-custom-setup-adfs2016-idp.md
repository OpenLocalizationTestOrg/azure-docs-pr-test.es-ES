---
title: "Azure Active Directory B2C: adición de ADFS como proveedor de identidades de SAML mediante directivas personalizadas"
description: "Un tooarticle cómo sobre la configuración de 2016 de AD FS mediante las directivas personalizadas y el protocolo SAML"
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
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a>Azure Active Directory B2C: adición de ADFS como proveedor de identidades de SAML mediante directivas personalizadas

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Este artículo muestra cómo tooenable sesión para los usuarios de la cuenta de AD FS mediante el uso de Hola de [directivas personalizadas de](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Requisitos previos

Hola completa los pasos de hello [Introducción a las directivas personalizadas](active-directory-b2c-get-started-custom.md) artículo.

Estos pasos incluyen:

1.  Crear una relación de confianza para usuario autenticado de ADFS
2.  Agregar tooAzure de certificado de confianza para usuario autenticado de AD FS de hello AD B2C.
3.  Agregar directiva de tooa de proveedor de notificaciones.
4.  Cuenta de AD FS Hola del registro de notificaciones de viaje de usuario de proveedor tooa.
5.  Cargando Hola directiva tooan Azure AD B2C inquilino y la prueba.

## <a name="toocreate-a-claims-aware-relying-party-trust"></a>toocreate una relación de confianza para notificaciones

toouse ADFS como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita toocreate una confianza para usuario autenticado de ADFS y proporcionarle los parámetros correctos de Hola.

tooadd un nuevo usuario de confianza de confianza mediante el uso de complemento de hello AD FS administración y configurar manualmente la configuración de hello, realizar Hola siguiendo el procedimiento en un servidor de federación.

Pertenencia en **administradores**, o equivalente, en el equipo local de hello es Hola mínimo necesario toocomplete este procedimiento. Revise los detalles acerca del uso de las cuentas adecuadas hello y pertenencias a grupos en [locales y grupos de dominio predeterminados](http://go.microsoft.com/fwlink/?LinkId=83477)

1.  En el Administrador del servidor, haga clic en **Herramientas** y, luego, seleccione **ADFS Management** (Administración de ADFS).

2.  Seleccione **Add Relying Party Trust** (Agregar relación de confianza para usuario autenticado).
    ![Asistente para agregar relación de confianza para usuario autenticado](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)

3.  En hello **bienvenida** página, elija **notificaciones** y haga clic en **iniciar**.
    ![En la página de bienvenida de hello, elija notificaciones](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)
4.  En hello **Seleccionar origen de datos** página, haga clic en **escribir manualmente los datos sobre el usuario de confianza de hello**y, a continuación, haga clic en **siguiente**.
    ![Especificar los datos sobre el usuario de confianza de Hola](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)

5.  En hello **especificar nombre para mostrar** página, escriba un nombre en **nombre para mostrar**, en **notas** escriba una descripción para esta relación de confianza y, a continuación, haga clic en **siguiente** .
    ![Especificación del nombre para mostrar y las notas](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)
6.  Opcional. Si tiene un certificado de cifrado de token opcional y, a continuación, en hello **configurar certificado** página, haga clic en **examinar** toolocate el archivo de certificado y, a continuación, haga clic en **siguiente** .
    ![Configuración del certificado](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)
7.  En hello **configurar dirección URL** página, seleccione hello **habilitar la compatibilidad con el protocolo SAML 2.0 WebSSO hello** casilla de verificación. En **autenticado entidad dirección URL del servicio SSO de SAML 2.0**, escriba Hola dirección de URL de extremo de servicio de lenguaje de marcado de aserción de seguridad (SAML) para esta relación de confianza y, a continuación, haga clic en **siguiente**.  Para hello **autenticado entidad dirección URL del servicio SSO de SAML 2.0**, pegue hello `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`. Reemplace {tenant} con el nombre de su inquilino (por ejemplo, contosob2c.onmicrosoft.com) y Hola {directiva} por el nombre de la directiva de extensiones (por ejemplo, B2C_1A_TrustFrameworkExtensions).
    > [!IMPORTANT]
    >nombre de la directiva de Hello es hello uno y que herede signup_or_signin directiva, en este caso es: `B2C_1A_TrustFrameworkExtensions`.
    >Por ejemplo podría ser la dirección URL de hello: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.

    ![Dirección URL del servicio SSO de SAML 2.0 del usuario de confianza](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. En hello **configurar identificadores** página, especifique Hola misma dirección URL que el paso anterior de hello, haga clic en **agregar** tooadd les toohello lista y, a continuación, haga clic en **siguiente**.
    ![Identificadores de relación de confianza para usuario autenticado](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)
9.  En hello **elegir la directiva de Control de acceso** seleccione una directiva y haga clic en **siguiente**.
    ![Elección de la directiva de Access Control](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)
10.  En hello **listo tooAdd confianza** página, revise la configuración de hello y, a continuación, haga clic en **siguiente** toosave información de confianza de su usuario de confianza.
    ![Guardado de la información de relación de confianza para usuario autenticado](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)
11.  En hello **finalizar** página, haga clic en **cerrar**, esta acción muestra automáticamente hello **editar reglas de notificación** cuadro de diálogo.
    ![Edición de reglas de notificación](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)
12. Haga clic en **Agregar regla**.  
      ![Adición de nueva regla](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)
13.  En **Claim rule template** (Plantilla de regla de notificación), seleccione **Send LDAP attributes as claims** (Enviar atributos LDAP como notificaciones).
    ![Selección de Enviar atributos LDAP como regla de plantilla de notificaciones](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)
14.  Proporcione el **nombre de la regla de notificación**. Para hello **almacén de atributos** seleccione **seleccione Active Directory** agregar Hola después de notificaciones, a continuación, haga clic en **finalizar** y **Aceptar**.
    ![Establecimiento de las propiedades de la regla](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)
15.  En el administrador del servidor, seleccione **Veracidades** , a continuación, seleccione Hola relación de confianza que creó y haga clic en **propiedades**.
    ![Propiedades de edición de usuario de confianza](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)
16.  Uno Hola confianza entidad confianza (demostración B2C) propiedades ventana haga clic en **firma** ficha y haga clic en **agregar**.  
    ![Establecimiento de firma](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)
17.  Agregue el certificado de firma (archivo .cert, sin clave privada).  
    ![Adición del certificado de firma](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  En la ventana Propiedades de hello confianza entidad confianza (demostración B2C) haga clic en **avanzadas** pestaña y cambie hello **algoritmo hash seguro** demasiado**SHA-1**, haga clic en **Aceptar**.  
    ![Establece el algoritmo de hash seguro tooSHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a>Agregar Hola ADFS cuenta aplicación clave tooAzure AD B2C
Federación con cuentas de AD FS requiere un secreto de cliente para ADFS cuenta tootrust Azure AD B2C en nombre de la aplicación hello. Necesita toostore su certificado ADFS en el inquilino de Azure AD B2C. 

1.  Vaya el inquilino de Azure AD B2C tooyour y seleccione **configuración B2C** > **Framework de la experiencia de identidad**
2.  Seleccione **claves de directiva** claves de hello tooview disponibles en el inquilino.
3.  Haga clic en **+Agregar**.
4.  En **Opciones**, use **Cargar**.
5.  En **Nombre**, use `ADFSSamlCert`.  
    prefijo de Hello `B2C_1A_` podrían agregarse automáticamente.
6.  En cargar el archivo hello, ** seleccione el archivo .pfx del certificado con clave privada. Nota: este certificado (con clave privada de hello) debe ser uno mismo emite y usa para el usuario de confianza de AD FS Hola Hola.
![Carga de la clave de directiva](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)
7.  Haga clic en **Crear**
8.  Confirme que ha creado la clave de hello `B2C_1A_ADFSSamlCert`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Adición de un proveedor de notificaciones en la directiva de extensión
Si desea toosign de usuarios mediante el uso de la cuenta de AD FS, necesita toodefine ADFS cuenta como un proveedor de notificaciones. En otras palabras, necesita un punto de conexión que Azure AD B2C se comunica con toospecify. punto de conexión de Hello proporciona un conjunto de notificaciones que usan Azure AD B2C tooverify que ha autenticado un usuario específico.

Defina la cuenta de ADFS como proveedor de notificaciones; para ello, agregue el nodo `<ClaimsProvider>` en el archivo de directiva de extensión:

1. Abra el archivo de directiva de extensión de hello (TrustFrameworkExtensions.xml) desde el directorio de trabajo. Si necesita un editor XML, [pruebe Visual Studio Code](https://code.visualstudio.com/download), un editor multiplataforma ligero.
2. Buscar hello `<ClaimsProviders>` sección
3. Agregar Hola siguiente fragmento XML en hello `ClaimsProviders` elemento y reemplace `identityProvider` con el DNS (valor arbitrario que indica su dominio) y guarde el archivo hello. 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
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

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Registrar tooSign del proveedor de notificaciones de hello ADFS cuenta seguridad o iniciar sesión en el viaje de usuario
En este momento, el proveedor de identidades de Hola se ha configurado.  Sin embargo, no está disponible en ninguna de hello sesión-up/inicio de sesión de pantallas. Ahora tiene un usuario de tooyour del proveedor de identidad de cuenta de tooadd Hola ADFS `SignUpOrSignIn` viaje de usuario. toomake está disponible, se crea un duplicado de un viaje de usuario de plantilla existente.  A continuación, se modifique para que incluya el proveedor de identidad ADFS hello:
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  Abra el archivo de base de hello de la directiva (por ejemplo, TrustFrameworkBase.xml).
2.  Buscar hello `<UserJourneys>` elemento y copia Hola todo el contenido de `<UserJourneys>` nodo.
3.  Abra el archivo de extensión de hello (por ejemplo, TrustFrameworkExtensions.xml) y busque hello `<UserJourneys>` elemento. Si no existe el elemento hello, agregue uno.
4.  Pegue todo el contenido de hello `<UserJournesy>` nodo que ha copiado como elemento secundario de hello `<UserJourneys>` elemento.

### <a name="display-hello-button"></a>Botón de mostrar hello
Hola `<ClaimsProviderSelections>` elemento define la lista de Hola de opciones de selección del proveedor de notificaciones y su orden.  `<ClaimsProviderSelection>`elemento es análogo tooan el botón del proveedor de identidad en una página de inicio de sesión-up/inicio de sesión de. Si agrega un `<ClaimsProviderSelection>` elemento para la cuenta de AD FS, un nuevo botón aparezca cuando llega a un usuario en la página de Hola. tooadd este elemento:

1.  Buscar hello `<UserJourney>` nodo que incluya `Id="SignUpOrSignIn"` en viaje de usuario de Hola que ha copiado.
2.  Busque hello `<OrchestrationStep>` nodo que incluye`Order="1"`
3.  Agregue el siguiente fragmento de código XML en el nodo `<ClaimsProviderSelections>`:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a>Acción del botón de vínculo hello tooan

Ahora que tiene un botón en su lugar, debe toolink tooan acción. acción de Hello, en este caso, es para Azure AD B2C toocommunicate con ADFS cuenta tooreceive un token. Acción de vínculo Hola botón tooan vinculando perfil técnico hello para el proveedor de notificaciones ADFS cuenta:

1.  Buscar hello `<OrchestrationStep>` que incluye `Order="2"` en hello `<UserJourney>` nodo.
2.  Agregue el siguiente fragmento de código XML en el nodo `<ClaimsExchanges>`:

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * Asegúrese de hello `Id` tiene Hola mismo valor que el de `TargetClaimsExchangeId` Hola sección anterior.
> * Asegúrese de `TechnicalProfileReferenceId` se establece toohello perfil técnico que creó anteriormente (Contoso-SAML2).

## <a name="upload-hello-policy-tooyour-tenant"></a>Cargar el inquilino de hello directiva tooyour
1.  Hola [portal de Azure](https://portal.azure.com), cambiar a hello [contexto de su inquilino de Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md), abra hello y **Azure AD B2C** hoja.
2.  Seleccione **Marco de experiencia de identidad**.
3.  Abra hello **todas las directivas** hoja.
4.  Seleccione **Cargar directiva**.
5.  Comprobar **sobrescribir directiva Hola si existe** cuadro.
6.  **Cargar** TrustFrameworkExtensions.xml y asegúrese de que no considerará no válido de Hola

## <a name="test-hello-custom-policy-by-using-run-now"></a>Probar directiva personalizada de hello mediante Ejecutar ahora
1.  Abra **configuración de Azure AD B2C** y vaya demasiado**identidad experiencia Framework**.
2.  Abra **B2C_1A_signup_signin**, Hola directiva personalizada de confianza (RP) de la entidad que ha cargado. Seleccione **Ejecutar ahora**.
3.  Debe ser capaz de toosign con cuenta de AD FS.

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a>[Opcional] Registrar Hola ADFS cuenta notificaciones proveedor tooProfile Editar usuario del proceso
Tal vez desee proveedor de identidad de cuenta de tooadd Hola ADFS también tooyour usuario `ProfileEdit` viaje de usuario. toomake está disponible, se repita Hola últimos dos pasos:

### <a name="display-hello-button"></a>Botón de mostrar hello
1.  Abra el archivo de extensión de hello de la directiva (por ejemplo, TrustFrameworkExtensions.xml).
2.  Buscar hello `<UserJourney>` nodo que incluya `Id="ProfileEdit"` en viaje de usuario de Hola que ha copiado.
3.  Busque hello `<OrchestrationStep>` nodo que incluye`Order="1"`
4.  Agregue el siguiente fragmento de código XML en el nodo `<ClaimsProviderSelections>`:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Acción del botón de vínculo hello tooan
1.  Buscar hello `<OrchestrationStep>` que incluye `Order="2"` en hello `<UserJourney>` nodo.
2.  Agregue el siguiente fragmento de código XML en el nodo `<ClaimsExchanges>`:

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Probar la directiva de edición de perfil personalizada hello mediante Ejecutar ahora
1.  Abra **configuración de Azure AD B2C** y vaya demasiado**identidad experiencia Framework**.
2.  Abra **B2C_1A_ProfileEdit**, Hola directiva personalizada de confianza (RP) de la entidad que ha cargado. Seleccione **Ejecutar ahora**.
3.  Debe ser capaz de toosign con cuenta de AD FS.

## <a name="download-hello-complete-policy-files"></a>Descargar archivos de directiva completa Hola
Opcional: Se recomienda que compilar su escenario con sus propios archivos de directiva personalizada después de completar Hola Getting Started with Custom directivas recorrer. [Archivos de directiva de ejemplo solo de referencia](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
