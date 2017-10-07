---
title: "Azure Active Directory B2C: incorporación de un proveedor de Salesforce SAML mediante el uso de directivas personalizadas|Microsoft Docs"
description: "Obtenga información acerca de cómo toocreate y administrar las directivas personalizadas de Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: f14c9d96980ff124110db7cfb58bf7cd81750b7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a>Azure Active Directory B2C: inicio de sesión mediante cuentas de Salesforce a través de SAML

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Este artículo muestra cómo toouse [directivas personalizadas](active-directory-b2c-overview-custom.md) tooset una sesión para los usuarios de una organización de Salesforce específica.

## <a name="prerequisites"></a>Requisitos previos

### <a name="azure-ad-b2c-setup"></a>Configuración de Azure AD B2C

Asegúrese de que ha completado todos los pasos de Hola que le muestran cómo demasiado[empezar a trabajar con las directivas personalizadas](active-directory-b2c-get-started-custom.md) en Azure Active Directory B2C (Azure AD B2C).

Entre ellos se incluyen los siguientes:

* Crear un inquilino de Azure AD B2C.
* Crear una aplicación de Azure AD B2C.
* Registrar dos aplicaciones de motor de directivas.
* Configurar las claves.
* Configurar el módulo de inicio de Hola.

### <a name="salesforce-setup"></a>Configuración de Salesforce

En este artículo, se supone que ya ha hecho siguiente hello:

* Se ha registrado para obtener una cuenta de Salesforce. Puede registrarse para [una cuenta gratuita de Developer Edition](https://developer.salesforce.com/signup).
* [Ha configurado un Mi dominio](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) para su organización de Salesforce.

## <a name="set-up-salesforce-so-users-can-federate"></a>Configurar Salesforce, para que los usuarios se puedan federar

toohelp Azure AD B2C comunicarse con Salesforce, deberá tooget Hola dirección URL de metadatos de Salesforce.

### <a name="set-up-salesforce-as-an-identity-provider"></a>Configurar Salesforce como proveedor de identidades

> [!NOTE]
> En este artículo, se supone que usa [Lightning Experience de Salesforce](https://developer.salesforce.com/page/Lightning_Experience_FAQ).

1. [Inicie sesión en tooSalesforce](https://login.salesforce.com/). 
2. En hello izquierda menú, en **configuración**, expanda **identidad**y, a continuación, haga clic en **proveedor de identidades**.
3. Haga clic en **Enable Identity Provider** (Habilitar proveedor de identidades).
4. En **certificado Hola seleccione**, seleccione certificado Hola desea Salesforce toouse toocommunicate con Azure AD B2C. (Puede usar certificado predeterminado de hello). Haga clic en **Guardar**. 

### <a name="create-a-connected-app-in-salesforce"></a>Crear una aplicación conectada en Salesforce

1. En hello **proveedor de identidades** página, vaya demasiado**proveedores de servicios**.
2. Haga clic en **Service Providers are now created via Connected Apps (Los proveedores de servicios se crean ahora a través de aplicaciones conectadas). Haga clic aquí.**
3. En **información básica**, especifique valores de hello necesario para la aplicación conectada.
4. En **configuración de aplicación Web**, seleccione hello **habilitar SAML** casilla de verificación.
5. Hola **Id. de entidad** , escriba Hola después de la dirección URL. Asegúrese de reemplazar el valor de hello para `tenantName`.
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. Hola **dirección URL de ACS** , escriba Hola después de la dirección URL. Asegúrese de reemplazar el valor de hello para `tenantName`.
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. Deje los valores predeterminados de Hola para todas las demás opciones.
8. Desplácese toohello inferior de la lista de hello y, a continuación, haga clic en **guardar**.

### <a name="get-hello-metadata-url"></a>Obtener dirección URL de metadatos de Hola

1. En la página de información general de saludo de la aplicación conectada, haga clic en **administrar**.
2. Copiar valor de Hola para **extremo de detección de metadatos**y, a continuación, guárdelo. Lo usará más adelante en este artículo.

### <a name="set-up-salesforce-users-toofederate"></a>Configurar toofederate de los usuarios de Salesforce

1. En hello **administrar** página de la aplicación conectada, vaya demasiado**perfiles**.
2. Haga clic en **Administrar perfiles**.
3. Seleccione los perfiles de hello (o grupos de usuarios) que desea toofederate con Azure AD B2C. Como administrador del sistema, seleccione hello **administrador del sistema** casilla para que pueda federarse con su cuenta de Salesforce.

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a>Generar un certificado de firma para Azure AD B2C

Las solicitudes envían tooSalesforce necesidad toobe firmado por Azure AD B2C. toogenerate un certificado de firma, abra PowerShell de Azure y, a continuación, ejecute hello siga los comandos.

> [!NOTE]
> Asegúrese de que actualice el nombre del inquilino de Hola y una contraseña en dos líneas de superior Hola.

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a>Agregar tooAzure certificado firma Hola SAML AD B2C

Cargar Hola inquilino de Azure AD B2C tooyour de certificado de firma: 

1. Vaya el inquilino de Azure AD B2C tooyour. Haga clic en **Configuración** > **Marco de experiencia de identidad** > **Claves de directiva**.
2. Haga clic en **+Agregar** y después:
    1. Haga clic en **Opciones** > **Cargar**.
    2. Escriba un **nombre** (por ejemplo, SAMLSigningCert). prefijo de Hello *B2C_1A_* se agrega automáticamente el nombre de toohello de la clave.
    3. tooselect su certificado, seleccione **control del archivo de carga**. 
    4. Escribir contraseña del certificado de hello configuradas en el script de PowerShell de Hola.
3. Haga clic en **Crear**.
4. Compruebe que ha creado una clave (por ejemplo, B2C_1A_SAMLSigningCert). Tome nota del nombre completo de hello (incluidos *B2C_1A_*). Hará referencia toothis clave más adelante en la directiva de Hola.

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a>Crear proveedor de notificaciones de Salesforce SAML hello en la directiva de base

Necesita toodefine Salesforce como un proveedor de notificaciones para que los usuarios puedan iniciar sesión mediante el uso de Salesforce. En otras palabras, necesita extremo de hello toospecify que se puede comunicar con Azure AD B2C. punto de conexión de Hello le *proporcionar* un conjunto de *notificaciones* que Azure AD B2C usa tooverify que ha autenticado un usuario específico. toodo esto, agregue un `<ClaimsProvider>` de Salesforce en el archivo de extensión de hello de la directiva:

1. En el directorio de trabajo, abra el archivo de extensión de hello (TrustFrameworkExtensions.xml).
2. Buscar hello `<ClaimsProviders>` sección. Si no existe, créela en el nodo raíz de Hola.
3. Agregar un nuevo `<ClaimsProvider>`:

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
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

En hello `<ClaimsProvider>` nodo:

1. Cambiar el valor de Hola para `<Domain>` tooa valor exclusivo que distingue `<ClaimsProvider>` de otros proveedores de identidad.
2. Actualizar el valor de Hola para `<DisplayName>` tooa nombre para mostrar para hello proveedor de notificaciones. Actualmente este valor no se usa.

### <a name="update-hello-technical-profile"></a>Actualizar perfil técnica Hola

tooget un token de SAML de Salesforce, definir los protocolos de Hola que Azure AD B2C utilizará toocommunicate con Azure Active Directory (Azure AD). Hacer esto en hello `<TechnicalProfile>` elemento de `<ClaimsProvider>`:

1. Actualizar el Id. de Hola de hello `<TechnicalProfile>` nodo. Este identificador es toothis toorefer usado perfil técnica de otras partes de la directiva de Hola.
2. Actualizar el valor de Hola para `<DisplayName>`. Este valor se muestra en el botón de inicio de sesión de hello en la página de inicio de sesión.
3. Actualizar el valor de Hola para `<Description>`.
4. Salesforce utiliza el protocolo de hello SAML 2.0. Asegúrese de que el valor de hello `<Protocol>` es **SAML2**.

Hola de actualización `<Metadata>` sección Hola anterior configuración de hello tooreflect XML para su cuenta de Salesforce específica. Hola XML, actualice los valores de metadatos de hello:

1. Actualizar el valor de Hola de `<Item Key="PartnerEntity">` con la dirección URL de metadatos de Salesforce Hola que copió anteriormente. Tiene Hola siguiendo el formato: 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. Hola `<CryptographicKeys>` sección actualización Hola valor para ambas instancias de `StorageReferenceId` toohello nombre de clave de hello el certificado de firma (por ejemplo, B2C_1A_SAMLSigningCert).

### <a name="upload-hello-extension-file-for-verification"></a>Cargar archivo de extensión de hello para la comprobación

La directiva ya está configurada para que Azure AD B2C sepa cómo toocommunicate con Salesforce. Intente cargar el archivo de extensión de hello de la directiva, tooverify que no hay problemas hasta ahora. archivo de extensión de hello tooupload de la directiva:

1. En su inquilino de Azure AD B2C, vaya toohello **todas las directivas** hoja.
2. Seleccione hello **sobrescribir directiva Hola si existe** casilla de verificación.
3. Cargar archivo de extensión de hello (TrustFrameworkExtensions.xml). Asegúrese de que no se produce un error en la validación.

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a>Registrar Hola viaje de usuario de Salesforce SAML notificaciones proveedor tooa

A continuación, agregue hello tooone de proveedor de identidad de Salesforce SAML de los viajes de usuario. En este momento, se ha configurado el proveedor de identidades de hello, pero no está disponible en cualquiera de las páginas de inicio de sesión o inicio de sesión de usuario de Hola. tooadd Hola página proveedor de identidades tooa inicio de sesión, en primer lugar, cree un duplicado de un viaje de usuario de plantilla existente. A continuación, modificar plantilla de Hola para que también dispone de proveedor de identidades de Azure AD de Hola.

1. Abra el archivo de base de hello de la directiva (por ejemplo, TrustFrameworkBase.xml).
2. Buscar hello `<UserJourneys>` elemento y, a continuación, Hola copia todo `<UserJourney>` valor, incluidos los Id. = "SignUpOrSignIn".
3. Abra el archivo de extensión de hello (por ejemplo, TrustFrameworkExtensions.xml). Buscar hello `<UserJourneys>` elemento. Si el elemento hello no existe, cree uno.
4. Copiar todo Hola de pegar `<UserJourney>` como un elemento secundario de hello `<UserJourneys>` elemento.
5. Cambiar el nombre de Id. de Hola de nuevo hello `<UserJourney>` (por ejemplo, SignUpOrSignUsingContoso).

### <a name="display-hello-identity-provider-button"></a>Botón de proveedor de identidad de mostrar hello

Hola `<ClaimsProviderSelection>` elemento es análogo tooan el botón del proveedor de identidad en una página de inicio de sesión o inicio de sesión. Agregando un `<ClaimsProviderSelection>` elemento para Salesforce, un nuevo botón aparece cuando un usuario deja la página toothis. botón de proveedor de identidad de Hola toodisplay:

1. Hola `<UserJourney>` que creó, busque hello `<OrchestrationStep>` con `Order="1"`.
2. Agregue Hola continuación de XML:

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. Establecer `TargetClaimsExchangeId` valor lógico tooa. Se recomienda siguiente Hola misma convención de otros usuarios (por ejemplo,  *\[ClaimProviderName\]Exchange*).

### <a name="link-hello-identity-provider-button-tooan-action"></a>Vínculo Hola acción tooan del botón de proveedor de identidad

Ahora que tiene un botón de proveedor de identidad en su lugar, vincúlelo tooan acción. En este caso, acción de hello es para Azure AD B2C toocommunicate con Salesforce tooreceive un token de SAML. Puede hacerlo mediante la vinculación de perfil técnico Hola para su Salesforce SAML proveedor de notificaciones:

1. Hola `<UserJourney>` nodo, buscar hello `<OrchestrationStep>` con `Order="2"`.
2. Agregue Hola continuación de XML:

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. Actualización `Id` toohello mismo valor que se usó previamente para `TargetClaimsExchangeId`.
4. Actualización `TechnicalProfileReferenceId` toohello `Id` de hello técnica de perfil que creó anteriormente (por ejemplo, ContosoProfile).

### <a name="upload-hello-updated-extension-file"></a>Cargar archivo de extensión actualizada de hello

Ha terminado de modificar el archivo de extensión Hola. Guarde y cargue este archivo. Asegúrese de que todas las validaciones se han realizado correctamente.

### <a name="update-hello-relying-party-file"></a>Actualizar archivo de entidad de confianza de hello

A continuación, actualizar el archivo entidad (RP) confianza hello que inicia el viaje de usuario de Hola que ha creado:

1. Realice una copia de SignUpOrSignIn.xml en el directorio de trabajo. Después, cambie el nombre (por ejemplo, SignUpOrSignInWithAAD.xml).
2. Abra Hola Hola nuevo para archivo y actualización de `PolicyId` atributo `<TrustFrameworkPolicy>` con un valor único. Este es el nombre de saludo de la directiva (por ejemplo, SignUpOrSignInWithAAD).
3. Modificar hello `ReferenceId` atributo `<DefaultUserJourney>` toomatch hello `Id` de hello nuevo usuario del proceso que ha creado (por ejemplo, SignUpOrSignUsingContoso).
4. Guardar los cambios y, a continuación, cargar archivo hello.

## <a name="test-and-troubleshoot"></a>Pruebas y solución de problemas

directiva personalizada de tootest Hola que acaba de cargar, Hola portal de Azure, vaya toohello hoja de la directiva y, a continuación, haga clic en **ejecutar ahora**. Si se produce un error, vea [Solución de problemas de directivas personalizadas](active-directory-b2c-troubleshoot-custom.md).

## <a name="next-steps"></a>Pasos siguientes

Proporcionar comentarios demasiado[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).
