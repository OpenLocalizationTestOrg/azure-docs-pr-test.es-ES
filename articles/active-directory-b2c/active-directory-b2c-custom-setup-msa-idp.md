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
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a><span data-ttu-id="33a0e-103">Azure Active Directory B2C: adición de una cuenta de Microsoft (MSA) como proveedor de identidades mediante directivas personalizadas</span><span class="sxs-lookup"><span data-stu-id="33a0e-103">Azure Active Directory B2C: Add Microsoft Account (MSA) as an identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="33a0e-104">Este artículo muestra cómo tooenable inicio de sesión de los usuarios de la cuenta de Microsoft (MSA) mediante el uso de Hola de [directivas personalizadas de](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="33a0e-104">This article shows you how tooenable sign-in for users from Microsoft account (MSA) through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33a0e-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="33a0e-105">Prerequisites</span></span>
<span data-ttu-id="33a0e-106">Hola completa los pasos de hello [Introducción a las directivas personalizadas](active-directory-b2c-get-started-custom.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="33a0e-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="33a0e-107">Estos pasos incluyen:</span><span class="sxs-lookup"><span data-stu-id="33a0e-107">These steps include:</span></span>

1.  <span data-ttu-id="33a0e-108">Crear una aplicación de la cuenta de Microsoft</span><span class="sxs-lookup"><span data-stu-id="33a0e-108">Creating a Microsoft account application.</span></span>
2.  <span data-ttu-id="33a0e-109">Agregar Hola Microsoft cuenta aplicación clave tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="33a0e-109">Adding hello Microsoft account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="33a0e-110">Agregar directiva de tooa de proveedor de notificaciones</span><span class="sxs-lookup"><span data-stu-id="33a0e-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="33a0e-111">Hola Account Microsoft notificaciones proveedor tooa usuario del proceso de registro</span><span class="sxs-lookup"><span data-stu-id="33a0e-111">Registering hello Microsoft Account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="33a0e-112">Cargando Hola directiva tooan Azure AD B2C inquilino y la prueba</span><span class="sxs-lookup"><span data-stu-id="33a0e-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="33a0e-113">Creación de una aplicación de cuenta Microsoft</span><span class="sxs-lookup"><span data-stu-id="33a0e-113">Create a Microsoft account application</span></span>
<span data-ttu-id="33a0e-114">toouse cuenta de Microsoft como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita toocreate una aplicación de la cuenta de Microsoft y suministrarle los parámetros correctos de Hola.</span><span class="sxs-lookup"><span data-stu-id="33a0e-114">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="33a0e-115">Necesita una cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="33a0e-115">You need a Microsoft account.</span></span> <span data-ttu-id="33a0e-116">Si no tiene una, visite [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="33a0e-116">If you don’t have one, visit [https://www.live.com/](https://www.live.com/).</span></span>

1.  <span data-ttu-id="33a0e-117">Vaya toohello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) e inicie sesión con sus credenciales de cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="33a0e-117">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2.  <span data-ttu-id="33a0e-118">Haga clic en **Agregar una aplicación**.</span><span class="sxs-lookup"><span data-stu-id="33a0e-118">Click **Add an app**.</span></span>

    ![Cuenta de Microsoft: Adición de una aplicación](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  <span data-ttu-id="33a0e-120">Proporcione un **nombre** para su aplicación, un **correo electrónico de contacto**, desactive **Permítanos que le ayudemos a empezar** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="33a0e-120">Provide a **Name** for your application, **Contact email**, uncheck **Let us help you get started** and click **Create**.</span></span>

    ![Cuenta de Microsoft: Registro de la aplicación](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  <span data-ttu-id="33a0e-122">Copiar valor de Hola de **identificador de la aplicación**. Se necesita lo tooconfigure cuenta de Microsoft como proveedor de identidades en su inquilino.</span><span class="sxs-lookup"><span data-stu-id="33a0e-122">Copy hello value of **Application Id**. You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>

    ![Cuenta de Microsoft: copiar el valor de hello del identificador de aplicación](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  <span data-ttu-id="33a0e-124">Haga clic en **Agregar plataforma**.</span><span class="sxs-lookup"><span data-stu-id="33a0e-124">Click on **Add platform**</span></span>

    ![Cuenta Microsoft: Agregar plataforma](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  <span data-ttu-id="33a0e-126">En la lista de plataformas de hello, elija **Web**.</span><span class="sxs-lookup"><span data-stu-id="33a0e-126">From hello platform list, choose **Web**.</span></span>

    ![Cuenta de Microsoft: desde la lista de plataformas de hello elegir Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  <span data-ttu-id="33a0e-128">Escriba `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en hello **URI de redireccionamiento** campo.</span><span class="sxs-lookup"><span data-stu-id="33a0e-128">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="33a0e-129">Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="33a0e-129">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>

    ![Cuenta de Microsoft: Establecimiento de las direcciones URL de redireccionamiento](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  <span data-ttu-id="33a0e-131">Haga clic en **generar nueva contraseña** en hello **aplicación secretos** sección.</span><span class="sxs-lookup"><span data-stu-id="33a0e-131">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="33a0e-132">Copiar contraseña nueva hello muestra en pantalla.</span><span class="sxs-lookup"><span data-stu-id="33a0e-132">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="33a0e-133">Se necesita lo tooconfigure cuenta de Microsoft como proveedor de identidades en su inquilino.</span><span class="sxs-lookup"><span data-stu-id="33a0e-133">You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="33a0e-134">Esta contraseña es una credencial de seguridad importante.</span><span class="sxs-lookup"><span data-stu-id="33a0e-134">This password is an important security credential.</span></span>

    ![Cuenta Microsoft: Generar nueva contraseña](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Cuenta de Microsoft: copiar la contraseña nuevo de Hola](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  <span data-ttu-id="33a0e-137">Casilla de Hola que dice **soporte técnico del SDK de Live** en hello **opciones avanzadas** sección.</span><span class="sxs-lookup"><span data-stu-id="33a0e-137">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="33a0e-138">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="33a0e-138">Click **Save**.</span></span>

    ![Cuenta Microsoft: Soporte técnico de SDK de Live](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="33a0e-140">Agregar Hola Microsoft cuenta aplicación clave tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="33a0e-140">Add hello Microsoft account application key tooAzure AD B2C</span></span>
<span data-ttu-id="33a0e-141">Federación con cuentas de Microsoft requiere un secreto de cliente para tootrust de cuenta de Microsoft Azure AD B2C en nombre de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="33a0e-141">Federation with Microsoft accounts requires a client secret for Microsoft account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="33a0e-142">Debe toostore su secert de aplicación de cuenta de Microsoft en el inquilino de Azure AD B2C:</span><span class="sxs-lookup"><span data-stu-id="33a0e-142">You need toostore your Microsoft account application secert in Azure AD B2C tenant:</span></span>   

1.  <span data-ttu-id="33a0e-143">Vaya el inquilino de Azure AD B2C tooyour y seleccione **configuración B2C** > **Framework de la experiencia de identidad**</span><span class="sxs-lookup"><span data-stu-id="33a0e-143">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="33a0e-144">Seleccione **claves de directiva** claves de hello tooview disponibles en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="33a0e-144">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="33a0e-145">Haga clic en **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="33a0e-145">Click **+Add**.</span></span>
4.  <span data-ttu-id="33a0e-146">En **Opciones**, use **Manual**.</span><span class="sxs-lookup"><span data-stu-id="33a0e-146">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="33a0e-147">En **Nombre**, use `MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="33a0e-147">For **Name**, use `MSASecret`.</span></span>  
    <span data-ttu-id="33a0e-148">prefijo de Hello `B2C_1A_` podrían agregarse automáticamente.</span><span class="sxs-lookup"><span data-stu-id="33a0e-148">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="33a0e-149">Hola **secreto** cuadro, escriba el secreto de aplicación de Microsoft desde https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="33a0e-149">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="33a0e-150">En **Uso de claves**, use **Firma**.</span><span class="sxs-lookup"><span data-stu-id="33a0e-150">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="33a0e-151">Haga clic en **Crear**</span><span class="sxs-lookup"><span data-stu-id="33a0e-151">Click **Create**</span></span>
9.  <span data-ttu-id="33a0e-152">Confirme que ha creado la clave de hello `B2C_1A_MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="33a0e-152">Confirm that you've created hello key `B2C_1A_MSASecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="33a0e-153">Adición de un proveedor de notificaciones en la directiva de extensión</span><span class="sxs-lookup"><span data-stu-id="33a0e-153">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="33a0e-154">Si desea toosign de usuarios mediante Microsoft Account, debe toodefine Account Microsoft como un proveedor de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="33a0e-154">If you want users toosign in by using Microsoft Account, you need toodefine Microsoft Account as a claims provider.</span></span> <span data-ttu-id="33a0e-155">En otras palabras, necesita un punto de conexión que Azure AD B2C se comunica con toospecify.</span><span class="sxs-lookup"><span data-stu-id="33a0e-155">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="33a0e-156">punto de conexión de Hello proporciona un conjunto de notificaciones que usan Azure AD B2C tooverify que ha autenticado un usuario específico.</span><span class="sxs-lookup"><span data-stu-id="33a0e-156">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="33a0e-157">Defina la cuenta de Microsoft como proveedor de notificaciones; para ello, agregue el nodo `<ClaimsProvider>` en el archivo de la directiva de extensión:</span><span class="sxs-lookup"><span data-stu-id="33a0e-157">Define Microsoft Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="33a0e-158">Abra el archivo de directiva de extensión de hello (TrustFrameworkExtensions.xml) desde el directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="33a0e-158">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="33a0e-159">Si necesita un editor XML, [pruebe Visual Studio Code](https://code.visualstudio.com/download), un editor multiplataforma ligero.</span><span class="sxs-lookup"><span data-stu-id="33a0e-159">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="33a0e-160">Buscar hello `<ClaimsProviders>` sección</span><span class="sxs-lookup"><span data-stu-id="33a0e-160">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="33a0e-161">Agregue el siguiente fragmento XML en hello `ClaimsProviders` elemento:</span><span class="sxs-lookup"><span data-stu-id="33a0e-161">Add following XML snippet under hello `ClaimsProviders` element:</span></span>

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

4.  <span data-ttu-id="33a0e-162">Reemplace el valor `client_id` por el id. de cliente de aplicación de la cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="33a0e-162">Replace `client_id` value with your Microsoft Account application client Id</span></span>

5.  <span data-ttu-id="33a0e-163">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="33a0e-163">Save hello file.</span></span>

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="33a0e-164">Registrar proveedor de notificaciones de hello Account Microsoft tooSign seguridad o inicio de sesión en el viaje de usuario</span><span class="sxs-lookup"><span data-stu-id="33a0e-164">Register hello Microsoft Account claims provider tooSign up or Sign-in user journey</span></span>

<span data-ttu-id="33a0e-165">En este momento, se ha configurado el proveedor de identidades de hello, pero no está disponible en cualquiera de las pantallas de sesión-up/inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="33a0e-165">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="33a0e-166">Ahora tiene un usuario tooyour de proveedor de identidad de Microsoft Account de tooadd hello `SignUpOrSignIn` viaje de usuario.</span><span class="sxs-lookup"><span data-stu-id="33a0e-166">Now you need tooadd hello Microsoft Account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="33a0e-167">toomake está disponible, se crea un duplicado de un viaje de usuario de plantilla existente.</span><span class="sxs-lookup"><span data-stu-id="33a0e-167">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="33a0e-168">A continuación, agregamos el proveedor de identidades de hello Account de Microsoft:</span><span class="sxs-lookup"><span data-stu-id="33a0e-168">Then we add hello Microsoft Account identity provider:</span></span>

> [!NOTE]
>
><span data-ttu-id="33a0e-169">Si copió anteriormente hello `<UserJourneys>` elemento del archivo de base de su archivo de extensión de directiva de toohello `TrustFrameworkExtensions.xml`, puede omitir la sección toothis.</span><span class="sxs-lookup"><span data-stu-id="33a0e-169">If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file `TrustFrameworkExtensions.xml`, you can skip toothis section.</span></span>

1.  <span data-ttu-id="33a0e-170">Abra el archivo de base de hello de la directiva (por ejemplo, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="33a0e-170">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="33a0e-171">Buscar hello `<UserJourneys>` elemento y copia Hola todo el contenido de `<UserJourneys>` nodo.</span><span class="sxs-lookup"><span data-stu-id="33a0e-171">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="33a0e-172">Abra el archivo de extensión de hello (por ejemplo, TrustFrameworkExtensions.xml) y busque hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="33a0e-172">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="33a0e-173">Si no existe el elemento hello, agregue uno.</span><span class="sxs-lookup"><span data-stu-id="33a0e-173">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="33a0e-174">Pegue todo el contenido de hello `<UserJournesy>` nodo que ha copiado como elemento secundario de hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="33a0e-174">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="33a0e-175">Botón de mostrar hello</span><span class="sxs-lookup"><span data-stu-id="33a0e-175">Display hello button</span></span>
<span data-ttu-id="33a0e-176">Hola `<ClaimsProviderSelections>` elemento define la lista de Hola de opciones de selección del proveedor de notificaciones y su orden.</span><span class="sxs-lookup"><span data-stu-id="33a0e-176">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="33a0e-177">`<ClaimsProviderSelection>`elemento es análogo tooan el botón del proveedor de identidad en una página de inicio de sesión-up/inicio de sesión de.</span><span class="sxs-lookup"><span data-stu-id="33a0e-177">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="33a0e-178">Si agrega un `<ClaimsProviderSelection>` elemento para la cuenta de Microsoft, un nuevo botón aparezca cuando llega a un usuario en la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="33a0e-178">If you add a `<ClaimsProviderSelection>` element for Microsoft account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="33a0e-179">tooadd este elemento:</span><span class="sxs-lookup"><span data-stu-id="33a0e-179">tooadd this element:</span></span>

1.  <span data-ttu-id="33a0e-180">Buscar hello `<UserJourney>` nodo que incluya `Id="SignUpOrSignIn"` en viaje de usuario de Hola que ha copiado.</span><span class="sxs-lookup"><span data-stu-id="33a0e-180">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="33a0e-181">Busque hello `<OrchestrationStep>` nodo que incluye`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="33a0e-181">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="33a0e-182">Agregue el siguiente fragmento de código XML en el nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="33a0e-182">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="33a0e-183">Acción del botón de vínculo hello tooan</span><span class="sxs-lookup"><span data-stu-id="33a0e-183">Link hello button tooan action</span></span>
<span data-ttu-id="33a0e-184">Ahora que tiene un botón en su lugar, debe toolink tooan acción.</span><span class="sxs-lookup"><span data-stu-id="33a0e-184">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="33a0e-185">acción de Hello, en este caso, es para Azure AD B2C toocommunicate con Microsoft Account tooreceive un token.</span><span class="sxs-lookup"><span data-stu-id="33a0e-185">hello action, in this case, is for Azure AD B2C toocommunicate with Microsoft Account tooreceive a token.</span></span> <span data-ttu-id="33a0e-186">Vincular tooan acción del botón de hello vinculando perfil técnico hello para el proveedor de notificaciones de Account de Microsoft:</span><span class="sxs-lookup"><span data-stu-id="33a0e-186">Link hello button tooan action by linking hello technical profile for your Microsoft Account claims provider:</span></span>

1.  <span data-ttu-id="33a0e-187">Buscar hello `<OrchestrationStep>` que incluye `Order="2"` en hello `<UserJourney>` nodo.</span><span class="sxs-lookup"><span data-stu-id="33a0e-187">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="33a0e-188">Agregue el siguiente fragmento de código XML en el nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="33a0e-188">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * <span data-ttu-id="33a0e-189">Asegúrese de hello `Id` tiene Hola mismo valor que el de `TargetClaimsExchangeId` en la sección anterior de Hola</span><span class="sxs-lookup"><span data-stu-id="33a0e-189">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
>   * <span data-ttu-id="33a0e-190">Asegúrese de `TechnicalProfileReferenceId` se estableció el identificador de perfil técnico toohello que creó anteriormente (MSA-OIDC).</span><span class="sxs-lookup"><span data-stu-id="33a0e-190">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (MSA-OIDC).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="33a0e-191">Cargar el inquilino de hello directiva tooyour</span><span class="sxs-lookup"><span data-stu-id="33a0e-191">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="33a0e-192">Hola [portal de Azure](https://portal.azure.com), cambiar a hello [contexto de su inquilino de Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md), abra hello y **Azure AD B2C** hoja.</span><span class="sxs-lookup"><span data-stu-id="33a0e-192">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="33a0e-193">Seleccione **Marco de experiencia de identidad**.</span><span class="sxs-lookup"><span data-stu-id="33a0e-193">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="33a0e-194">Abra hello **todas las directivas** hoja.</span><span class="sxs-lookup"><span data-stu-id="33a0e-194">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="33a0e-195">Seleccione **Cargar directiva**.</span><span class="sxs-lookup"><span data-stu-id="33a0e-195">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="33a0e-196">Comprobar **sobrescribir directiva Hola si existe** cuadro.</span><span class="sxs-lookup"><span data-stu-id="33a0e-196">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="33a0e-197">**Cargar** TrustFrameworkExtensions.xml y asegúrese de que no considerará no válido de Hola</span><span class="sxs-lookup"><span data-stu-id="33a0e-197">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="33a0e-198">Probar directiva personalizada de hello mediante Ejecutar ahora</span><span class="sxs-lookup"><span data-stu-id="33a0e-198">Test hello custom policy by using Run Now</span></span>

1.  <span data-ttu-id="33a0e-199">Abra **configuración de Azure AD B2C** y vaya demasiado**identidad experiencia Framework**.</span><span class="sxs-lookup"><span data-stu-id="33a0e-199">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
> [!NOTE]
>
><span data-ttu-id="33a0e-200">**Ejecutar ahora** requiere al menos una aplicación toobe registrada previamente en el inquilino de Hola.</span><span class="sxs-lookup"><span data-stu-id="33a0e-200">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> <span data-ttu-id="33a0e-201">toolearn tooregister aplicaciones, vea hello Azure AD B2C [Introducción](active-directory-b2c-get-started.md) artículo o hello [registro de la aplicación](active-directory-b2c-app-registration.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="33a0e-201">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>
2.  <span data-ttu-id="33a0e-202">Abra **B2C_1A_signup_signin**, Hola directiva personalizada de confianza (RP) de la entidad que ha cargado.</span><span class="sxs-lookup"><span data-stu-id="33a0e-202">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="33a0e-203">Seleccione **Ejecutar ahora**.</span><span class="sxs-lookup"><span data-stu-id="33a0e-203">Select **Run now**.</span></span>
3.  <span data-ttu-id="33a0e-204">Debe ser capaz de toosign sesión con la cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="33a0e-204">You should be able toosign in using Microsoft account.</span></span>

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="33a0e-205">[Opcional] Registrar hello Account Microsoft notificaciones proveedor tooProfile Editar usuario del proceso</span><span class="sxs-lookup"><span data-stu-id="33a0e-205">[Optional] Register hello Microsoft Account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="33a0e-206">Tal vez desee proveedor de identidades de Microsoft Account tooadd Hola también tooyour usuario `ProfileEdit` viaje de usuario.</span><span class="sxs-lookup"><span data-stu-id="33a0e-206">You may want tooadd hello Microsoft Account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="33a0e-207">toomake está disponible, se repita Hola últimos dos pasos:</span><span class="sxs-lookup"><span data-stu-id="33a0e-207">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="33a0e-208">Botón de mostrar hello</span><span class="sxs-lookup"><span data-stu-id="33a0e-208">Display hello button</span></span>
1.  <span data-ttu-id="33a0e-209">Abra el archivo de extensión de hello de la directiva (por ejemplo, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="33a0e-209">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="33a0e-210">Buscar hello `<UserJourney>` nodo que incluya `Id="ProfileEdit"` en viaje de usuario de Hola que ha copiado.</span><span class="sxs-lookup"><span data-stu-id="33a0e-210">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="33a0e-211">Busque hello `<OrchestrationStep>` nodo que incluye`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="33a0e-211">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="33a0e-212">Agregue el siguiente fragmento de código XML en el nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="33a0e-212">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="33a0e-213">Acción del botón de vínculo hello tooan</span><span class="sxs-lookup"><span data-stu-id="33a0e-213">Link hello button tooan action</span></span>
1.  <span data-ttu-id="33a0e-214">Buscar hello `<OrchestrationStep>` que incluye `Order="2"` en hello `<UserJourney>` nodo.</span><span class="sxs-lookup"><span data-stu-id="33a0e-214">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="33a0e-215">Agregue el siguiente fragmento de código XML en el nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="33a0e-215">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="33a0e-216">Probar la directiva de edición de perfil personalizada hello mediante Ejecutar ahora</span><span class="sxs-lookup"><span data-stu-id="33a0e-216">Test hello custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="33a0e-217">Abra **configuración de Azure AD B2C** y vaya demasiado**identidad experiencia Framework**.</span><span class="sxs-lookup"><span data-stu-id="33a0e-217">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="33a0e-218">Abra **B2C_1A_ProfileEdit**, Hola directiva personalizada de confianza (RP) de la entidad que ha cargado.</span><span class="sxs-lookup"><span data-stu-id="33a0e-218">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="33a0e-219">Seleccione **Ejecutar ahora**.</span><span class="sxs-lookup"><span data-stu-id="33a0e-219">Select **Run now**.</span></span>
3.  <span data-ttu-id="33a0e-220">Debe ser capaz de toosign sesión con la cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="33a0e-220">You should be able toosign in using Microsoft account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="33a0e-221">Descargar archivos de directiva completa Hola</span><span class="sxs-lookup"><span data-stu-id="33a0e-221">Download hello complete policy files</span></span>
<span data-ttu-id="33a0e-222">Opcional: Se recomienda que elabore su escenario con sus propios archivos de directiva personalizada después de completar la introducción a las directivas personalizadas recorra en lugar de utilizar estos archivos de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="33a0e-222">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="33a0e-223">Archivos de directiva de ejemplo de referencia</span><span class="sxs-lookup"><span data-stu-id="33a0e-223">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
