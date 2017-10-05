---
title: "Azure Active Directory B2C: modificación del registro en las directivas personalizadas y configuración de un proveedor autoafirmado"
description: "Un tutorial sobre cómo agregar notificaciones para registrarse y configurar la entrada del usuario"
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
ms.openlocfilehash: 64b9d904d7d070052e125b479f4719d208c9ff85
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2017
---
# <a name="azure-active-directory-b2c-modify-sign-up-to-add-new-claims-and-configure-user-input"></a><span data-ttu-id="9b7cd-103">Azure Active Directory B2C: modificación del registro para agregar nuevas notificaciones y configuración de la entrada del usuario.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-103">Azure Active Directory B2C: Modify sign up to add new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="9b7cd-104">En este artículo, se agregará una nueva entrada (una notificación) por parte del usuario a un recorrido del usuario de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-104">In this article, you will add a new user provided entry (a claim) to your signup user journey.</span></span>  <span data-ttu-id="9b7cd-105">La entrada se configurará como una lista desplegable y se definirá si es necesario.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-105">You will configure the entry as a dropdown, and define if it is required.</span></span>

<span data-ttu-id="9b7cd-106">Editar Sipi para desencadenar la entrega de prueba.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-106">Edited by Sipi to trigger test handoff.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b7cd-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9b7cd-107">Prerequisites</span></span>

* <span data-ttu-id="9b7cd-108">Complete los pasos del artículo [Introducción a las directivas personalizadas](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="9b7cd-108">Complete the steps in the article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="9b7cd-109">Pruebe el recorrido del usuario de suscripción o inicio de sesión para registrar una nueva cuenta local antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-109">Test the signup/signin user journey to signup a new local account before proceeding.</span></span>


<span data-ttu-id="9b7cd-110">La recopilación de los datos iniciales de los usuarios se logra a través de la suscripción o del inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-110">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="9b7cd-111">Posteriormente se pueden recopilar más notificaciones a través de los recorridos de los usuarios de edición de perfil.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-111">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="9b7cd-112">Cada vez que Azure AD B2C recoge información directamente del usuario de forma interactiva, el marco de la experiencia de identidad usa `selfasserted provider`.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-112">Anytime Azure AD B2C gathers information directly from the user interactively, the Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="9b7cd-113">Los pasos siguientes se aplican siempre que se usa este proveedor.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-113">The steps below apply anytime this provider is used.</span></span>


## <a name="define-the-claim-its-display-name-and-the-user-input-type"></a><span data-ttu-id="9b7cd-114">Definición de la notificación, su nombre para mostrar y el tipo de entrada del usuario</span><span class="sxs-lookup"><span data-stu-id="9b7cd-114">Define the claim, its display name and the user input type</span></span>
<span data-ttu-id="9b7cd-115">Vamos a pedir al usuario que indique su ciudad.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-115">Lets ask the user for their city.</span></span>  <span data-ttu-id="9b7cd-116">Agregue el siguiente elemento al elemento `<ClaimsSchema>` del archivo de directiva TrustFrameWorkExtensions:</span><span class="sxs-lookup"><span data-stu-id="9b7cd-116">Add the following element to the `<ClaimsSchema>` element in the TrustFrameWorkExtensions policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="9b7cd-117">Aquí puede elegir otras opciones para personalizar la notificación.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-117">There are additional choices you can make here to customize the claim.</span></span>  <span data-ttu-id="9b7cd-118">Para ver todo el esquema, consulte la guía **Identity Experience Framework Technical Reference Guide** (Guía de referencia técnica del marco de experiencia de identidad).</span><span class="sxs-lookup"><span data-stu-id="9b7cd-118">For a full schema, refer to the **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="9b7cd-119">Esta guía se publicará pronto en la sección de referencias.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-119">This guide will be published soon in the reference section.</span></span>

* <span data-ttu-id="9b7cd-120">`<DisplayName>` es una cadena que define la *etiqueta* a nivel de usuario</span><span class="sxs-lookup"><span data-stu-id="9b7cd-120">`<DisplayName>` is a string that defines the user-facing *label*</span></span>

* <span data-ttu-id="9b7cd-121">`<UserHelpText>` ayuda al usuario a saber lo que se requiere</span><span class="sxs-lookup"><span data-stu-id="9b7cd-121">`<UserHelpText>` helps the user understand what is required</span></span>

* <span data-ttu-id="9b7cd-122">`<UserInputType>` tiene las cuatro opciones siguientes resaltadas:</span><span class="sxs-lookup"><span data-stu-id="9b7cd-122">`<UserInputType>` has the following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="9b7cd-123">`RadioSingleSelectduration`: exige una sola selección.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-123">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
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

    * <span data-ttu-id="9b7cd-124">`DropdownSingleSelect`: permite la selección del único valor válido.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-124">`DropdownSingleSelect` - Allows the selection of only valid value.</span></span>

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


* <span data-ttu-id="9b7cd-126">`CheckboxMultiSelect` Permite la selección de uno o varios valores.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-126">`CheckboxMultiSelect` Allows for the selection of one or more values.</span></span>

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

## <a name="add-the-claim-to-the-sign-upsign-in-user-journey"></a><span data-ttu-id="9b7cd-128">Adición de la notificación al recorrido del usuario de registro o inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="9b7cd-128">Add the claim to the sign up/sign in user journey</span></span>

1. <span data-ttu-id="9b7cd-129">Agregue la notificación como `<OutputClaim ClaimTypeReferenceId="city"/>` a TechnicalProfile `LocalAccountSignUpWithLogonEmail` (que se encuentra en el archivo de directiva TrustFrameworkBase).</span><span class="sxs-lookup"><span data-stu-id="9b7cd-129">Add the claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` to the TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in the TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="9b7cd-130">Tenga en cuenta que TechnicalProfile utiliza SelfAssertedAttributeProvider.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-130">Note this TechnicalProfile uses the SelfAssertedAttributeProvider.</span></span>

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
      <!-- Optional claims, to be collected from the user -->
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

2. <span data-ttu-id="9b7cd-131">Agregue la notificación a AAD-UserWriteUsingLogonEmail como `<PersistedClaim ClaimTypeReferenceId="city" />` para escribir la notificación en el directorio de AAD después de recopilarla del usuario.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-131">Add the claim to the AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` to write the claim to the AAD directory after collecting it from the user.</span></span> <span data-ttu-id="9b7cd-132">Este paso se puede omitir si se prefiere no conservar la notificación en el directorio para usarla en el futuro.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-132">You may skip this step if you prefer not to persist the claim in the directory for future use.</span></span>

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

3. <span data-ttu-id="9b7cd-133">Agregue la notificación a la instancia de TechnicalProfile que lee del directorio cuando un usuario inicia sesión como `<OutputClaim ClaimTypeReferenceId="city" />`</span><span class="sxs-lookup"><span data-stu-id="9b7cd-133">Add the claim to the TechnicalProfile that reads from the directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for the provided user ID.</Item>
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

4. <span data-ttu-id="9b7cd-134">Agregue `<OutputClaim ClaimTypeReferenceId="city" />` al archivo de directiva de RP SignUporSignIn.xml, con el fin de que esta notificación se envíe a la aplicación en el token después de un recorrido correcto del usuario.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-134">Add the `<OutputClaim ClaimTypeReferenceId="city" />` to the RP policy file SignUporSignIn.xml so this claim is sent to the application in the token after a successful user journey.</span></span>

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

## <a name="test-the-custom-policy-using-run-now"></a><span data-ttu-id="9b7cd-135">Prueba de la directiva personalizada con "Ejecutar ahora"</span><span class="sxs-lookup"><span data-stu-id="9b7cd-135">Test the custom policy using "Run Now"</span></span>

1. <span data-ttu-id="9b7cd-136">Abra la **hoja de Azure AD B2C** y vaya a **Marco de experiencia de identidad > Directivas personalizadas**.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-136">Open the **Azure AD B2C Blade** and navigate to **Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="9b7cd-137">Seleccione la directiva personalizada que cargó y, luego, haga clic en el botón **Ejecutar ahora**.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-137">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
3. <span data-ttu-id="9b7cd-138">Debe poder registrarse con una dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-138">You should be able to sign up using an email address.</span></span>

<span data-ttu-id="9b7cd-139">La pantalla de registro en modo de prueba debe parecerse a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="9b7cd-139">The signup screen in test mode should look similar to this:</span></span>

![Captura de pantalla de la opción de registro modificada](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="9b7cd-141">El token que vuelve a la aplicación incluirá la notificación `city`, como se muestra a continuación</span><span class="sxs-lookup"><span data-stu-id="9b7cd-141">The token back to your application will now include the `city` claim as shown below</span></span>
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

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="9b7cd-142">Eliminación opcional de la comprobación del correo electrónico en el recorrido del registro</span><span class="sxs-lookup"><span data-stu-id="9b7cd-142">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="9b7cd-143">Para omitir la comprobación del correo electrónico, el autor de la directiva puede elegir quitar `PartnerClaimType="Verified.Email"`.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-143">To skip email verification, the policy author can choose to remove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="9b7cd-144">La dirección de correo electrónico será necesaria pero no se comprobará, salvo que se quite "Required" = true.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-144">The email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="9b7cd-145">Considere cuidadosamente si esta opción es adecuada para sus casos de uso.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-145">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="9b7cd-146">El correo electrónico comprobado está habilitado de forma predeterminada en el `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` del archivo de directiva TrustFrameworkBase del módulo de inicio:</span><span class="sxs-lookup"><span data-stu-id="9b7cd-146">Verified email is enabled by default in the `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in the TrustFrameworkBase policy file in the starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="9b7cd-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b7cd-147">Next steps</span></span>

<span data-ttu-id="9b7cd-148">Agregue la nueva notificación a los flujos de inicios de sesión de cuentas sociales cambiando las instancias de TechnicalProfiles que se enumeran a continuación.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-148">Add the new claim to the flows for social account logins by changing the TechnicalProfiles listed below.</span></span> <span data-ttu-id="9b7cd-149">Estas dos instancias se usan en los inicios de sesión de cuentas sociales o federadas para leer y escribir los datos de usuario con alternativeSecurityId como localizador.</span><span class="sxs-lookup"><span data-stu-id="9b7cd-149">These are used by social/federated account logins to write and read the user data using the alternativeSecurityId as the locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
