---
title: "Azure Active Directory B2C: modificación del registro en las directivas personalizadas y configuración de un proveedor autoafirmado"
description: "Un tutorial sobre cómo agregar notificaciones toosign seguridad y configurar Hola proporcionados por el usuario"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: tbd
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/29/2017
ms.author: joroja
ms.openlocfilehash: c31d737263fef3e771bdf451b809b0ca522c8fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-modify-sign-up-tooadd-new-claims-and-configure-user-input"></a><span data-ttu-id="05324-103">Azure B2C Directory Active: Modificar tooadd nuevas notificaciones de suscripción y configurar proporcionados por el usuario.</span><span class="sxs-lookup"><span data-stu-id="05324-103">Azure Active Directory B2C: Modify sign up tooadd new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="05324-104">En este artículo, agregará un viaje de usuario suscripción nueva del tooyour de entrada (una notificación) proporcionado por el usuario.</span><span class="sxs-lookup"><span data-stu-id="05324-104">In this article, you will add a new user provided entry (a claim) tooyour signup user journey.</span></span>  <span data-ttu-id="05324-105">Configurará la entrada de hello como una lista desplegable y definir si es necesario.</span><span class="sxs-lookup"><span data-stu-id="05324-105">You will configure hello entry as a dropdown, and define if it is required.</span></span>

<span data-ttu-id="05324-106">Editar Sipi tootrigger prueba entrega.</span><span class="sxs-lookup"><span data-stu-id="05324-106">Edited by Sipi tootrigger test handoff.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05324-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="05324-107">Prerequisites</span></span>

* <span data-ttu-id="05324-108">Hola completa los pasos en el artículo hello [Introducción a las directivas personalizadas](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="05324-108">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="05324-109">Probar Hola suscripción/signin usuario viaje toosignup una nueva cuenta local antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="05324-109">Test hello signup/signin user journey toosignup a new local account before proceeding.</span></span>


<span data-ttu-id="05324-110">La recopilación de los datos iniciales de los usuarios se logra a través de la suscripción o del inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="05324-110">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="05324-111">Posteriormente se pueden recopilar más notificaciones a través de los recorridos de los usuarios de edición de perfil.</span><span class="sxs-lookup"><span data-stu-id="05324-111">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="05324-112">Cada vez que Azure AD B2C recopila información directamente desde el usuario de hello interactivamente, Hola identidad experiencia Framework utiliza su `selfasserted provider`.</span><span class="sxs-lookup"><span data-stu-id="05324-112">Anytime Azure AD B2C gathers information directly from hello user interactively, hello Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="05324-113">Hola pasos siguientes se aplican siempre que se usa este proveedor.</span><span class="sxs-lookup"><span data-stu-id="05324-113">hello steps below apply anytime this provider is used.</span></span>


## <a name="define-hello-claim-its-display-name-and-hello-user-input-type"></a><span data-ttu-id="05324-114">Definir la notificación de hello, su nombre para mostrar y Hola tipo de entrada del usuario</span><span class="sxs-lookup"><span data-stu-id="05324-114">Define hello claim, its display name and hello user input type</span></span>
<span data-ttu-id="05324-115">Permite solicitar a usuario Hola su ciudad.</span><span class="sxs-lookup"><span data-stu-id="05324-115">Lets ask hello user for their city.</span></span>  <span data-ttu-id="05324-116">Agregar Hola siguiendo el elemento toohello `<ClaimsSchema>` elemento en el archivo de directiva de hello TrustFrameWorkExtensions:</span><span class="sxs-lookup"><span data-stu-id="05324-116">Add hello following element toohello `<ClaimsSchema>` element in hello TrustFrameWorkExtensions policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="05324-117">Hay más opciones que puede elegir aquí toocustomize Hola de notificación.</span><span class="sxs-lookup"><span data-stu-id="05324-117">There are additional choices you can make here toocustomize hello claim.</span></span>  <span data-ttu-id="05324-118">Para un esquema completo, consulte toohello **Guía de referencia técnica de identidad experiencia Framework**.</span><span class="sxs-lookup"><span data-stu-id="05324-118">For a full schema, refer toohello **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="05324-119">Esta guía se publicará próximamente en la sección de referencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="05324-119">This guide will be published soon in hello reference section.</span></span>

* <span data-ttu-id="05324-120">`<DisplayName>`es una cadena que define orientadas al usuario hello *etiqueta*</span><span class="sxs-lookup"><span data-stu-id="05324-120">`<DisplayName>` is a string that defines hello user-facing *label*</span></span>

* <span data-ttu-id="05324-121">`<UserHelpText>`ayuda a usuario de Hola a entender lo que se requiere</span><span class="sxs-lookup"><span data-stu-id="05324-121">`<UserHelpText>` helps hello user understand what is required</span></span>

* <span data-ttu-id="05324-122">`<UserInputType>`ha hello siguientes cuatro opciones resaltado a continuación:</span><span class="sxs-lookup"><span data-stu-id="05324-122">`<UserInputType>` has hello following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="05324-123">`RadioSingleSelectduration`: exige una sola selección.</span><span class="sxs-lookup"><span data-stu-id="05324-123">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>RadioSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

    * <span data-ttu-id="05324-124">`DropdownSingleSelect`-Permite la selección de hello del único valor válido.</span><span class="sxs-lookup"><span data-stu-id="05324-124">`DropdownSingleSelect` - Allows hello selection of only valid value.</span></span>

![Captura de pantalla de la opción de la lista desplegable](./media/active-directory-b2c-configure-signup-self-asserted-custom/dropdown-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>DropdownSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```


* <span data-ttu-id="05324-126">`CheckboxMultiSelect`Permite la selección de Hola de uno o más valores.</span><span class="sxs-lookup"><span data-stu-id="05324-126">`CheckboxMultiSelect` Allows for hello selection of one or more values.</span></span>

![Captura de pantalla de una opción con selección múltiple](./media/active-directory-b2c-configure-signup-self-asserted-custom/multiselect-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>Receive updates from which cities?</DisplayName>
  <DataType>string</DataType>
  <UserInputType>CheckboxMultiSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

## <a name="add-hello-claim-toohello-sign-upsign-in-user-journey"></a><span data-ttu-id="05324-128">Agregar el inicio de sesión de hello notificación toohello arriba/inicio de sesión viaje de usuario</span><span class="sxs-lookup"><span data-stu-id="05324-128">Add hello claim toohello sign up/sign in user journey</span></span>

1. <span data-ttu-id="05324-129">Agregar notificación de Hola como un `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (que se encuentra en el archivo de directiva de hello TrustFrameworkBase).</span><span class="sxs-lookup"><span data-stu-id="05324-129">Add hello claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in hello TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="05324-130">Tenga en cuenta que este TechnicalProfile usa hello SelfAssertedAttributeProvider.</span><span class="sxs-lookup"><span data-stu-id="05324-130">Note this TechnicalProfile uses hello SelfAssertedAttributeProvider.</span></span>

  ```xml
  <TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">
    <DisplayName>Email signup</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <Metadata>
      <Item Key="IpAddressClaimReferenceId">IpAddress</Item>
      <Item Key="ContentDefinitionReferenceId">api.localaccountsignup</Item>
      <Item Key="language.button_continue">Create</Item>
    </Metadata>
    <CryptographicKeys>
      <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
    </CryptographicKeys>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" />
    </InputClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
      <OutputClaim ClaimTypeReferenceId="newPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="reenterPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" />
      <OutputClaim ClaimTypeReferenceId="newUser" />
      <!-- Optional claims, toobe collected from hello user -->
      <OutputClaim ClaimTypeReferenceId="givenName" />
      <OutputClaim ClaimTypeReferenceId="surName" />
      <OutputClaim ClaimTypeReferenceId="city"/>
    </OutputClaims>
    <ValidationTechnicalProfiles>
      <ValidationTechnicalProfile ReferenceId="AAD-UserWriteUsingLogonEmail" />
    </ValidationTechnicalProfiles>
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

2. <span data-ttu-id="05324-131">Agregar Hola notificación toohello AAD UserWriteUsingLogonEmail como un `<PersistedClaim ClaimTypeReferenceId="city" />` directory toowrite Hola notificación toohello AAD después de la recopilación de los usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="05324-131">Add hello claim toohello AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` toowrite hello claim toohello AAD directory after collecting it from hello user.</span></span> <span data-ttu-id="05324-132">Puede omitir este paso si prefiere no toopersist Hola notificación en el directorio de Hola para un uso futuro.</span><span class="sxs-lookup"><span data-stu-id="05324-132">You may skip this step if you prefer not toopersist hello claim in hello directory for future use.</span></span>

  ```xml
  <!-- Technical profiles for local accounts -->
  <TechnicalProfile Id="AAD-UserWriteUsingLogonEmail">
    <Metadata>
      <Item Key="Operation">Write</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">true</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" Required="true" />
    </InputClaims>
    <PersistedClaims>
      <!-- Required claims -->
      <PersistedClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" />
      <PersistedClaim ClaimTypeReferenceId="newPassword" PartnerClaimType="password" />
      <PersistedClaim ClaimTypeReferenceId="displayName" DefaultValue="unknown" />
      <PersistedClaim ClaimTypeReferenceId="passwordPolicies" DefaultValue="DisablePasswordExpiration" />
      <!-- Optional claims. -->
      <PersistedClaim ClaimTypeReferenceId="givenName" />
      <PersistedClaim ClaimTypeReferenceId="surname" />
      <PersistedClaim ClaimTypeReferenceId="city" />
    </PersistedClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="newUser" PartnerClaimType="newClaimsPrincipalCreated" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

3. <span data-ttu-id="05324-133">Agregar notificación de hello toohello TechnicalProfile que lee desde el directorio de hello cuando un usuario inicia sesión como un`<OutputClaim ClaimTypeReferenceId="city" />`</span><span class="sxs-lookup"><span data-stu-id="05324-133">Add hello claim toohello TechnicalProfile that reads from hello directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for hello provided user ID.</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames" Required="true" />
    </InputClaims>
    <OutputClaims>
      <!-- Required claims -->
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <!-- Optional claims -->
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="displayName" />
      <OutputClaim ClaimTypeReferenceId="otherMails" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
  </TechnicalProfile>
  ```

4. <span data-ttu-id="05324-134">Agregar hello `<OutputClaim ClaimTypeReferenceId="city" />` el archivo de directiva RP toohello SignUporSignIn.xml por lo que esta notificación se envía toohello aplicación en el símbolo (token) de hello después de un viaje de usuario correcta.</span><span class="sxs-lookup"><span data-stu-id="05324-134">Add hello `<OutputClaim ClaimTypeReferenceId="city" />` toohello RP policy file SignUporSignIn.xml so this claim is sent toohello application in hello token after a successful user journey.</span></span>

  ```xml
  <RelyingParty>
    <DefaultUserJourney ReferenceId="SignUpOrSignIn" />
    <TechnicalProfile Id="PolicyProfile">
      <DisplayName>PolicyProfile</DisplayName>
      <Protocol Name="OpenIdConnect" />
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="displayName" />
        <OutputClaim ClaimTypeReferenceId="givenName" />
        <OutputClaim ClaimTypeReferenceId="surname" />
        <OutputClaim ClaimTypeReferenceId="email" />
        <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" />
        <OutputClaim ClaimTypeReferenceId="city" />
      </OutputClaims>
      <SubjectNamingInfo ClaimType="sub" />
    </TechnicalProfile>
  </RelyingParty>
  ```

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="05324-135">Probar directiva personalizada de hello mediante "Run Now"</span><span class="sxs-lookup"><span data-stu-id="05324-135">Test hello custom policy using "Run Now"</span></span>

1. <span data-ttu-id="05324-136">Hola abierto **hoja de Azure AD B2C** y navegue demasiado**identidad experiencia Framework > directivas personalizado**.</span><span class="sxs-lookup"><span data-stu-id="05324-136">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="05324-137">Active la directiva personalizada hello que ha cargado y haga clic en hello **ejecutar ahora** botón.</span><span class="sxs-lookup"><span data-stu-id="05324-137">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
3. <span data-ttu-id="05324-138">Debe ser capaz de toosign utilizando una dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="05324-138">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="05324-139">pantalla de registro de Hello en modo de prueba debe ser toothis similar:</span><span class="sxs-lookup"><span data-stu-id="05324-139">hello signup screen in test mode should look similar toothis:</span></span>

![Captura de pantalla de la opción de registro modificada](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="05324-141">Hello token tooyour atrás aplicación ahora incluirá hello `city` tal y como se muestra a continuación de notificación</span><span class="sxs-lookup"><span data-stu-id="05324-141">hello token back tooyour application will now include hello `city` claim as shown below</span></span>
```json
{
  "exp": 1493596822,
  "nbf": 1493593222,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "9c2a3a9e-ac65-4e46-a12d-9557b63033a9",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustf_signup_signin",
  "nonce": "defaultNonce",
  "iat": 1493593222,
  "auth_time": 1493593222,
  "email": "joe@outlook.com",
  "given_name": "Joe",
  "family_name": "Ras",
  "city": "Bellevue",
  "name": "unknown"
}
```

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="05324-142">Eliminación opcional de la comprobación del correo electrónico en el recorrido del registro</span><span class="sxs-lookup"><span data-stu-id="05324-142">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="05324-143">comprobación de correo electrónico de tooskip, autor de la directiva de hello puede elegir tooremove `PartnerClaimType="Verified.Email"`.</span><span class="sxs-lookup"><span data-stu-id="05324-143">tooskip email verification, hello policy author can choose tooremove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="05324-144">Hello dirección de correo electrónico, será necesario pero no comprobada, a menos que "Requerido" = true se quita.</span><span class="sxs-lookup"><span data-stu-id="05324-144">hello email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="05324-145">Considere cuidadosamente si esta opción es adecuada para sus casos de uso.</span><span class="sxs-lookup"><span data-stu-id="05324-145">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="05324-146">Comprobar el correo electrónico está habilitada de forma predeterminada en hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` en archivo de directivas de TrustFrameworkBase de hello en el módulo de inicio de hello:</span><span class="sxs-lookup"><span data-stu-id="05324-146">Verified email is enabled by default in hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in hello TrustFrameworkBase policy file in hello starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="05324-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="05324-147">Next steps</span></span>

<span data-ttu-id="05324-148">Agregar nueva notificación toohello flujos de Hola para inicios de sesión de cuenta sociales cambiando hello TechnicalProfiles enumeradas a continuación.</span><span class="sxs-lookup"><span data-stu-id="05324-148">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed below.</span></span> <span data-ttu-id="05324-149">Éstas son utilizados por toowrite de inicios de sesión de cuenta de social/federada y leer datos de usuario de hello mediante hello alternativeSecurityId como Hola localizador.</span><span class="sxs-lookup"><span data-stu-id="05324-149">These are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
