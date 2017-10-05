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
ms.openlocfilehash: 8c981046ff41d3927ff60d6dc4f40366ae25ba74
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a><span data-ttu-id="90ca1-103">Azure Active Directory B2C: adición de una cuenta de Microsoft (MSA) como proveedor de identidades mediante directivas personalizadas</span><span class="sxs-lookup"><span data-stu-id="90ca1-103">Azure Active Directory B2C: Add Microsoft Account (MSA) as an identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="90ca1-104">En este artículo se muestra cómo habilitar el inicio de sesión para usuarios de la cuenta de Microsoft (MSA) mediante [directivas personalizadas](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="90ca1-104">This article shows you how to enable sign-in for users from Microsoft account (MSA) through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90ca1-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="90ca1-105">Prerequisites</span></span>
<span data-ttu-id="90ca1-106">Complete los pasos del artículo [Introducción a las directivas personalizadas](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="90ca1-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="90ca1-107">Estos pasos incluyen:</span><span class="sxs-lookup"><span data-stu-id="90ca1-107">These steps include:</span></span>

1.  <span data-ttu-id="90ca1-108">Crear una aplicación de la cuenta de Microsoft</span><span class="sxs-lookup"><span data-stu-id="90ca1-108">Creating a Microsoft account application.</span></span>
2.  <span data-ttu-id="90ca1-109">Agregar la clave de aplicación de la cuenta de Microsoft a Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="90ca1-109">Adding the Microsoft account application key to Azure AD B2C</span></span>
3.  <span data-ttu-id="90ca1-110">Agregar un proveedor de notificaciones a una directiva</span><span class="sxs-lookup"><span data-stu-id="90ca1-110">Adding claims provider to a policy</span></span>
4.  <span data-ttu-id="90ca1-111">Registrar el proveedor de notificaciones de la cuenta de Microsoft en un recorrido del usuario</span><span class="sxs-lookup"><span data-stu-id="90ca1-111">Registering the Microsoft Account claims provider to a user journey</span></span>
5.  <span data-ttu-id="90ca1-112">Cargar la directiva en un inquilino de Azure AD B2C y probarla</span><span class="sxs-lookup"><span data-stu-id="90ca1-112">Uploading the policy to an Azure AD B2C tenant and test it</span></span>

## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="90ca1-113">Creación de una aplicación de cuenta Microsoft</span><span class="sxs-lookup"><span data-stu-id="90ca1-113">Create a Microsoft account application</span></span>
<span data-ttu-id="90ca1-114">Para usar una cuenta Microsoft como proveedor de identidades en Azure Active Directory (Azure AD) B2C, debe crear una aplicación de cuenta Microsoft y suministrarle los parámetros correctos.</span><span class="sxs-lookup"><span data-stu-id="90ca1-114">To use Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Microsoft account application and supply it with the right parameters.</span></span> <span data-ttu-id="90ca1-115">Necesita una cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="90ca1-115">You need a Microsoft account.</span></span> <span data-ttu-id="90ca1-116">Si no tiene una, visite [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="90ca1-116">If you don’t have one, visit [https://www.live.com/](https://www.live.com/).</span></span>

1.  <span data-ttu-id="90ca1-117">Vaya al [Portal de registro de aplicaciones de Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) e inicie sesión con las credenciales de su cuenta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="90ca1-117">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2.  <span data-ttu-id="90ca1-118">Haga clic en **Agregar una aplicación**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-118">Click **Add an app**.</span></span>

    ![Cuenta de Microsoft: Adición de una aplicación](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  <span data-ttu-id="90ca1-120">Proporcione un **nombre** para su aplicación, un **correo electrónico de contacto**, desactive **Permítanos que le ayudemos a empezar** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-120">Provide a **Name** for your application, **Contact email**, uncheck **Let us help you get started** and click **Create**.</span></span>

    ![Cuenta de Microsoft: Registro de la aplicación](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  <span data-ttu-id="90ca1-122">Copie el valor de **Id. de aplicación**. Lo necesitará para configurar una cuenta de Microsoft como proveedor de identidades de su inquilino.</span><span class="sxs-lookup"><span data-stu-id="90ca1-122">Copy the value of **Application Id**. You need it to configure Microsoft account as an identity provider in your tenant.</span></span>

    ![Cuenta de Microsoft: Copia del valor de id. de aplicación](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  <span data-ttu-id="90ca1-124">Haga clic en **Agregar plataforma**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-124">Click on **Add platform**</span></span>

    ![Cuenta Microsoft: Agregar plataforma](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  <span data-ttu-id="90ca1-126">En la lista de plataformas, elija **Web**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-126">From the platform list, choose **Web**.</span></span>

    ![Cuenta de Microsoft: En la lista de plataformas, selección de Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  <span data-ttu-id="90ca1-128">Escriba `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en el campo **URI de redireccionamiento** .</span><span class="sxs-lookup"><span data-stu-id="90ca1-128">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Redirect URIs** field.</span></span> <span data-ttu-id="90ca1-129">Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="90ca1-129">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>

    ![Cuenta de Microsoft: Establecimiento de las direcciones URL de redireccionamiento](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  <span data-ttu-id="90ca1-131">Haga clic en **Generar nueva contraseña** en la sección **Secretos de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-131">Click on **Generate New Password** under the **Application Secrets** section.</span></span> <span data-ttu-id="90ca1-132">Copie la nueva contraseña que se muestra en la pantalla.</span><span class="sxs-lookup"><span data-stu-id="90ca1-132">Copy the new password displayed on screen.</span></span> <span data-ttu-id="90ca1-133">Lo necesitará para configurar una cuenta de Microsoft como proveedor de identidades de su inquilino.</span><span class="sxs-lookup"><span data-stu-id="90ca1-133">You need it to configure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="90ca1-134">Esta contraseña es una credencial de seguridad importante.</span><span class="sxs-lookup"><span data-stu-id="90ca1-134">This password is an important security credential.</span></span>

    ![Cuenta Microsoft: Generar nueva contraseña](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Cuenta de Microsoft: Copia de la nueva contraseña](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  <span data-ttu-id="90ca1-137">Active la casilla **Soporte técnico de SDK de Live** de la sección **Opciones avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-137">Check the box that says **Live SDK support** under the **Advanced Options** section.</span></span> <span data-ttu-id="90ca1-138">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-138">Click **Save**.</span></span>

    ![Cuenta Microsoft: Soporte técnico de SDK de Live](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-the-microsoft-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="90ca1-140">Adición de la clave de aplicación de la cuenta de Microsoft a Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="90ca1-140">Add the Microsoft account application key to Azure AD B2C</span></span>
<span data-ttu-id="90ca1-141">La federación con cuentas de Microsoft requiere un secreto de cliente para que la cuenta de Microsoft confíe en Azure AD B2C en nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="90ca1-141">Federation with Microsoft accounts requires a client secret for Microsoft account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="90ca1-142">Debe almacenar el secreto de aplicación de la cuenta de Microsoft en el inquilino de Azure AD B2C:</span><span class="sxs-lookup"><span data-stu-id="90ca1-142">You need to store your Microsoft account application secert in Azure AD B2C tenant:</span></span>   

1.  <span data-ttu-id="90ca1-143">Vaya a su inquilino de Azure AD B2C y seleccione **B2C Settings (Configuración de B2C)** > **Marco de experiencia de identidad**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-143">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="90ca1-144">Seleccione **Policy Keys** (Claves de directiva) para ver las claves disponibles en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="90ca1-144">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="90ca1-145">Haga clic en **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-145">Click **+Add**.</span></span>
4.  <span data-ttu-id="90ca1-146">En **Opciones**, use **Manual**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-146">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="90ca1-147">En **Nombre**, use `MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="90ca1-147">For **Name**, use `MSASecret`.</span></span>  
    <span data-ttu-id="90ca1-148">Es posible que se agregue automáticamente el prefijo `B2C_1A_`.</span><span class="sxs-lookup"><span data-stu-id="90ca1-148">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="90ca1-149">En el cuadro **Secreto**, escriba el secreto de aplicación de Microsoft desde https://apps.dev.microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="90ca1-149">In the **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="90ca1-150">En **Uso de claves**, use **Firma**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-150">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="90ca1-151">Haga clic en **Crear**</span><span class="sxs-lookup"><span data-stu-id="90ca1-151">Click **Create**</span></span>
9.  <span data-ttu-id="90ca1-152">Confirme que ha creado la clave `B2C_1A_MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="90ca1-152">Confirm that you've created the key `B2C_1A_MSASecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="90ca1-153">Adición de un proveedor de notificaciones en la directiva de extensión</span><span class="sxs-lookup"><span data-stu-id="90ca1-153">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="90ca1-154">Si desea que los usuarios inicien sesión mediante la cuenta de Microsoft, debe definir este servicio como proveedor de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="90ca1-154">If you want users to sign in by using Microsoft Account, you need to define Microsoft Account as a claims provider.</span></span> <span data-ttu-id="90ca1-155">En otras palabras, debe especificar un punto de conexión con el que Azure AD B2C se comunica.</span><span class="sxs-lookup"><span data-stu-id="90ca1-155">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="90ca1-156">El punto de conexión proporciona un conjunto de notificaciones que Azure AD B2C usa para comprobar que un usuario concreto se ha autenticado.</span><span class="sxs-lookup"><span data-stu-id="90ca1-156">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="90ca1-157">Defina la cuenta de Microsoft como proveedor de notificaciones; para ello, agregue el nodo `<ClaimsProvider>` en el archivo de la directiva de extensión:</span><span class="sxs-lookup"><span data-stu-id="90ca1-157">Define Microsoft Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="90ca1-158">Abra el archivo de directiva de extensión (TrustFrameworkExtensions.xml) desde el directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="90ca1-158">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="90ca1-159">Si necesita un editor XML, [pruebe Visual Studio Code](https://code.visualstudio.com/download), un editor multiplataforma ligero.</span><span class="sxs-lookup"><span data-stu-id="90ca1-159">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="90ca1-160">Busque la sección `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="90ca1-160">Find the `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="90ca1-161">Agregue el siguiente fragmento de código XML en el elemento `ClaimsProviders`:</span><span class="sxs-lookup"><span data-stu-id="90ca1-161">Add following XML snippet under the `ClaimsProviders` element:</span></span>

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

4.  <span data-ttu-id="90ca1-162">Reemplace el valor `client_id` por el id. de cliente de aplicación de la cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="90ca1-162">Replace `client_id` value with your Microsoft Account application client Id</span></span>

5.  <span data-ttu-id="90ca1-163">Guarde el archivo .</span><span class="sxs-lookup"><span data-stu-id="90ca1-163">Save the file.</span></span>

## <a name="register-the-microsoft-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="90ca1-164">Registro del proveedor de notificaciones de la cuenta de Microsoft en un recorrido del usuario de registro o inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="90ca1-164">Register the Microsoft Account claims provider to Sign up or Sign-in user journey</span></span>

<span data-ttu-id="90ca1-165">El proveedor de identidades ya se ha configurado, pero no está disponible en ninguna de las pantallas de registro/inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="90ca1-165">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="90ca1-166">Ahora, debe agregar el proveedor de identidades de la cuenta de Microsoft a su recorrido del usuario `SignUpOrSignIn`.</span><span class="sxs-lookup"><span data-stu-id="90ca1-166">Now you need to add the Microsoft Account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="90ca1-167">Para que esté disponible, se crea un duplicado de un recorrido del usuario de plantilla ya existente.</span><span class="sxs-lookup"><span data-stu-id="90ca1-167">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="90ca1-168">Luego, se agrega el proveedor de identidades de la cuenta de Microsoft:</span><span class="sxs-lookup"><span data-stu-id="90ca1-168">Then we add the Microsoft Account identity provider:</span></span>

> [!NOTE]
>
><span data-ttu-id="90ca1-169">Si copió anteriormente el elemento `<UserJourneys>` del archivo base de la directiva al archivo de extensión `TrustFrameworkExtensions.xml`, puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="90ca1-169">If you previously copied the `<UserJourneys>` element from base file of your policy to the extension file `TrustFrameworkExtensions.xml`, you can skip to this section.</span></span>

1.  <span data-ttu-id="90ca1-170">Abra el archivo base de la directiva (por ejemplo, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="90ca1-170">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="90ca1-171">Busque el elemento `<UserJourneys>` y copie el contenido entero del nodo `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="90ca1-171">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="90ca1-172">Abra el archivo de extensión (por ejemplo, TrustFrameworkExtensions.xml) y busque el elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="90ca1-172">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="90ca1-173">Si el elemento no existe, agréguelo.</span><span class="sxs-lookup"><span data-stu-id="90ca1-173">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="90ca1-174">Pegue el contenido entero del nodo `<UserJournesy>` que copió como secundario del elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="90ca1-174">Paste the entire content of `<UserJournesy>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="90ca1-175">Visualización del botón</span><span class="sxs-lookup"><span data-stu-id="90ca1-175">Display the button</span></span>
<span data-ttu-id="90ca1-176">El elemento `<ClaimsProviderSelections>` define la lista de opciones de selección del proveedor de notificaciones y su orden.</span><span class="sxs-lookup"><span data-stu-id="90ca1-176">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="90ca1-177">El elemento `<ClaimsProviderSelection>` es análogo a un botón de proveedor de identidades de una página de registro o inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="90ca1-177">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="90ca1-178">Si agrega un elemento `<ClaimsProviderSelection>` para la cuenta de Microsoft, se muestra un nuevo botón cuando un usuario llega a la página.</span><span class="sxs-lookup"><span data-stu-id="90ca1-178">If you add a `<ClaimsProviderSelection>` element for Microsoft account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="90ca1-179">Para agregar este elemento:</span><span class="sxs-lookup"><span data-stu-id="90ca1-179">To add this element:</span></span>

1.  <span data-ttu-id="90ca1-180">Busque el nodo `<UserJourney>` que incluye `Id="SignUpOrSignIn"` en el recorrido del usuario que ha copiado.</span><span class="sxs-lookup"><span data-stu-id="90ca1-180">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="90ca1-181">Busque el nodo `<OrchestrationStep>` que incluye `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="90ca1-181">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="90ca1-182">Agregue el siguiente fragmento de código XML en el nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="90ca1-182">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="90ca1-183">Vincular el botón a una acción</span><span class="sxs-lookup"><span data-stu-id="90ca1-183">Link the button to an action</span></span>
<span data-ttu-id="90ca1-184">Ahora que hay un botón colocado, es preciso vincularlo a una acción.</span><span class="sxs-lookup"><span data-stu-id="90ca1-184">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="90ca1-185">En este caso, la acción es para que Azure AD B2C se comunique con la cuenta de Microsoft para recibir un token.</span><span class="sxs-lookup"><span data-stu-id="90ca1-185">The action, in this case, is for Azure AD B2C to communicate with Microsoft Account to receive a token.</span></span> <span data-ttu-id="90ca1-186">Vincule el botón a una acción mediante la vinculación del perfil técnico del proveedor de notificaciones de la cuenta de Microsoft:</span><span class="sxs-lookup"><span data-stu-id="90ca1-186">Link the button to an action by linking the technical profile for your Microsoft Account claims provider:</span></span>

1.  <span data-ttu-id="90ca1-187">Busque el nodo `<OrchestrationStep>` que incluye `Order="2"` en el nodo `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="90ca1-187">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="90ca1-188">Agregue el siguiente fragmento de código XML en el nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="90ca1-188">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * <span data-ttu-id="90ca1-189">Asegúrese de que el valor de `Id` sea el mismo que el de `TargetClaimsExchangeId` en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="90ca1-189">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section</span></span>
>   * <span data-ttu-id="90ca1-190">Asegúrese de que el id. de `TechnicalProfileReferenceId` se establezca en el perfil técnico que creó anteriormente (MSA-OIDC).</span><span class="sxs-lookup"><span data-stu-id="90ca1-190">Ensure `TechnicalProfileReferenceId` ID is set to the technical profile you created earlier (MSA-OIDC).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="90ca1-191">Carga de la directiva en el inquilino</span><span class="sxs-lookup"><span data-stu-id="90ca1-191">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="90ca1-192">En [Azure Portal](https://portal.azure.com), cambie al [contexto del inquilino de Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md) y abra la hoja **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-192">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="90ca1-193">Seleccione **Marco de experiencia de identidad**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-193">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="90ca1-194">Abra la hoja **Todas las directivas**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-194">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="90ca1-195">Seleccione **Cargar directiva**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-195">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="90ca1-196">Active la casilla **Sobrescribir la directiva si existe**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-196">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="90ca1-197">**Cargue** TrustFrameworkExtensions.xml y asegúrese de que no se produce ningún error en la validación.</span><span class="sxs-lookup"><span data-stu-id="90ca1-197">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="90ca1-198">Probar la directiva personalizada con Ejecutar ahora</span><span class="sxs-lookup"><span data-stu-id="90ca1-198">Test the custom policy by using Run Now</span></span>

1.  <span data-ttu-id="90ca1-199">Abra la **configuración de Azure AD B2C** y vaya a **Marco de experiencia de identidad**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-199">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
> [!NOTE]
>
><span data-ttu-id="90ca1-200">**Ejecutar ahora** Requiere al menos que una aplicación esté registrada previamente en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="90ca1-200">**Run now** requires at least one application to be preregistered on the tenant.</span></span> <span data-ttu-id="90ca1-201">Para obtener información sobre cómo registrar aplicaciones, vea el artículo de [introducción](active-directory-b2c-get-started.md) a Azure AD B2C o el artículo [Registro de la aplicación](active-directory-b2c-app-registration.md) de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="90ca1-201">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>
2.  <span data-ttu-id="90ca1-202">Abra **B2C_1A_signup_signin**, que es la directiva personalizada del usuario de confianza (RP) que ha cargado.</span><span class="sxs-lookup"><span data-stu-id="90ca1-202">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="90ca1-203">Seleccione **Ejecutar ahora**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-203">Select **Run now**.</span></span>
3.  <span data-ttu-id="90ca1-204">Debería poder iniciar sesión con la cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="90ca1-204">You should be able to sign in using Microsoft account.</span></span>

## <a name="optional-register-the-microsoft-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="90ca1-205">[Opcional] Registro del proveedor de notificaciones de la cuenta de Microsoft en el recorrido del usuario de edición de perfil</span><span class="sxs-lookup"><span data-stu-id="90ca1-205">[Optional] Register the Microsoft Account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="90ca1-206">Puede que también quiera agregar el proveedor de identidades de la cuenta de Microsoft al recorrido del usuario `ProfileEdit` de su usuario.</span><span class="sxs-lookup"><span data-stu-id="90ca1-206">You may want to add the Microsoft Account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="90ca1-207">Para que esté disponible, se repiten los dos últimos pasos:</span><span class="sxs-lookup"><span data-stu-id="90ca1-207">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="90ca1-208">Visualización del botón</span><span class="sxs-lookup"><span data-stu-id="90ca1-208">Display the button</span></span>
1.  <span data-ttu-id="90ca1-209">Abra el archivo de extensión de su directiva (por ejemplo, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="90ca1-209">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="90ca1-210">Busque el nodo `<UserJourney>` que incluye `Id="ProfileEdit"` en el recorrido del usuario que ha copiado.</span><span class="sxs-lookup"><span data-stu-id="90ca1-210">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="90ca1-211">Busque el nodo `<OrchestrationStep>` que incluye `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="90ca1-211">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="90ca1-212">Agregue el siguiente fragmento de código XML en el nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="90ca1-212">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="90ca1-213">Vincular el botón a una acción</span><span class="sxs-lookup"><span data-stu-id="90ca1-213">Link the button to an action</span></span>
1.  <span data-ttu-id="90ca1-214">Busque el nodo `<OrchestrationStep>` que incluye `Order="2"` en el nodo `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="90ca1-214">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="90ca1-215">Agregue el siguiente fragmento de código XML en el nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="90ca1-215">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="90ca1-216">Prueba de la directiva de edición de perfil personalizada mediante Ejecutar ahora</span><span class="sxs-lookup"><span data-stu-id="90ca1-216">Test the custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="90ca1-217">Abra la **configuración de Azure AD B2C** y vaya a **Marco de experiencia de identidad**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-217">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="90ca1-218">Abra **B2C_1A_ProfileEdit**, que es la directiva personalizada del usuario de confianza (RP) que ha cargado.</span><span class="sxs-lookup"><span data-stu-id="90ca1-218">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="90ca1-219">Seleccione **Ejecutar ahora**.</span><span class="sxs-lookup"><span data-stu-id="90ca1-219">Select **Run now**.</span></span>
3.  <span data-ttu-id="90ca1-220">Debería poder iniciar sesión con la cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="90ca1-220">You should be able to sign in using Microsoft account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="90ca1-221">Descarga de los archivos de directiva completos</span><span class="sxs-lookup"><span data-stu-id="90ca1-221">Download the complete policy files</span></span>
<span data-ttu-id="90ca1-222">Opcional: se recomienda que, en lugar de usar estos archivos de ejemplo, cree su escenario con sus propios archivos de directiva personalizada tras completar el tutorial de introducción a las directivas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="90ca1-222">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="90ca1-223">Archivos de directiva de ejemplo de referencia</span><span class="sxs-lookup"><span data-stu-id="90ca1-223">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
