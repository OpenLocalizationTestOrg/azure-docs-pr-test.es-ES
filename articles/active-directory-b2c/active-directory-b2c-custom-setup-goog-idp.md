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
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a><span data-ttu-id="2c0ae-103">Azure Active Directory B2C: adición de Google + como un proveedor de identidades de OAuth2 mediante directivas personalizadas</span><span class="sxs-lookup"><span data-stu-id="2c0ae-103">Azure Active Directory B2C: Add Google+ as an OAuth2 identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="2c0ae-104">Esta guía le mostrará cómo tooenable sesión para los usuarios de la cuenta de Google + mediante el uso de Hola de [directivas personalizadas de](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="2c0ae-104">This guide shows you how tooenable sign-in for users from Google+ account through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c0ae-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2c0ae-105">Prerequisites</span></span>

<span data-ttu-id="2c0ae-106">Hola completa los pasos de hello [Introducción a las directivas personalizadas](active-directory-b2c-get-started-custom.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="2c0ae-107">Estos pasos incluyen:</span><span class="sxs-lookup"><span data-stu-id="2c0ae-107">These steps include:</span></span>

1.  <span data-ttu-id="2c0ae-108">Crear una aplicación de la cuenta de Google+</span><span class="sxs-lookup"><span data-stu-id="2c0ae-108">Creating a Google+ account application.</span></span>
2.  <span data-ttu-id="2c0ae-109">Agregar Hola Google + cuenta aplicación clave tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="2c0ae-109">Adding hello Google+ account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="2c0ae-110">Agregar directiva de tooa de proveedor de notificaciones</span><span class="sxs-lookup"><span data-stu-id="2c0ae-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="2c0ae-111">Registrar Hola Google + cuenta notificaciones proveedor tooa usuario viaje</span><span class="sxs-lookup"><span data-stu-id="2c0ae-111">Registering hello Google+ account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="2c0ae-112">Cargando Hola directiva tooan Azure AD B2C inquilino y la prueba</span><span class="sxs-lookup"><span data-stu-id="2c0ae-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-google-account-application"></a><span data-ttu-id="2c0ae-113">Creación de una aplicación de la cuenta de Google+</span><span class="sxs-lookup"><span data-stu-id="2c0ae-113">Create a Google+ account application</span></span>
<span data-ttu-id="2c0ae-114">toouse Google + como proveedor de identidades en Azure Active Directory (Azure AD) B2C, necesita una aplicación de Google + toocreate y proporcionarla con los parámetros correctos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-114">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="2c0ae-115">Puede registrar una aplicación de Google+ aquí: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="2c0ae-115">You can register a Google+ application here: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span></span>

1.  <span data-ttu-id="2c0ae-116">Vaya toohello [Google Developers Console](https://console.developers.google.com/) e inicie sesión con sus credenciales de cuenta de Google +.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-116">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2.  <span data-ttu-id="2c0ae-117">Haga clic en **Create project** (Crear proyecto), escriba un nombre de proyecto en **Project name** y haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="2c0ae-117">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>

3.  <span data-ttu-id="2c0ae-118">Haga clic en hello **menú proyectos**.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-118">Click on hello **Projects menu**.</span></span>

    ![Cuenta de Google+: Selección del proyecto](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  <span data-ttu-id="2c0ae-120">Haga clic en hello  **+**  botón.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-120">Click on hello **+** button.</span></span>

    ![Cuenta de Google+: Creación de un nuevo proyecto](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  <span data-ttu-id="2c0ae-122">Escriba un **nombre de proyecto** y luego haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="2c0ae-122">Enter a **Project name**, and then click **Create**.</span></span>

    ![Cuenta de Google+: Nuevo proyecto](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  <span data-ttu-id="2c0ae-124">Espere a que el proyecto de hello está listo y haga clic en hello **menú proyectos**.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-124">Wait until hello project is ready and click on hello **Projects menu**.</span></span>

    ![Cuenta de Google +: espere a que el nuevo proyecto es toouse listo](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  <span data-ttu-id="2c0ae-126">Haga clic en el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-126">Click on your project name.</span></span>

    ![Cuenta de Google +: nuevo proyecto de hello Select](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  <span data-ttu-id="2c0ae-128">Haga clic en **API Manager** y, a continuación, haga clic en **credenciales** Hola barra de navegación izquierda.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-128">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
9.  <span data-ttu-id="2c0ae-129">Haga clic en hello **pantalla de consentimiento de OAuth** ficha situada en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-129">Click hello **OAuth consent screen** tab at hello top.</span></span>

    ![Cuenta de Google+: Configuración de la pantalla de consentimiento de OAuth](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  <span data-ttu-id="2c0ae-131">Seleccione o especifique una dirección de correo electrónico válida en **Email address**, especifique un nombre de producto en **Product name** y haga clic en **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="2c0ae-131">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>

    ![Google+: Credenciales de la aplicación](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  <span data-ttu-id="2c0ae-133">Haga clic en **New credentials** (Nuevas credenciales) y, luego, elija **OAuth client ID** (Id. de cliente de OAuth).</span><span class="sxs-lookup"><span data-stu-id="2c0ae-133">Click **New credentials** and then choose **OAuth client ID**.</span></span>

    ![Google+: Creación de nuevas credenciales de aplicación](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  <span data-ttu-id="2c0ae-135">En **Application type** (Tipo de aplicación), seleccione **Web application** (Aplicación web).</span><span class="sxs-lookup"><span data-stu-id="2c0ae-135">Under **Application type**, select **Web application**.</span></span>

    ![Google+: Selección del tipo de aplicación](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  <span data-ttu-id="2c0ae-137">Proporcionar un **nombre** para la aplicación, escriba `https://login.microsoftonline.com` en hello **orígenes de JavaScript autorizados** campo, y `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en hello **autorizadas redirigir URI**campo.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-137">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="2c0ae-138">Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="2c0ae-138">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="2c0ae-139">Hola **{tenant}** valor distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-139">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="2c0ae-140">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-140">Click **Create**.</span></span>

    ![Google+: Provisión de los orígenes y los URI de redirección autorizados de JavaScript](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  <span data-ttu-id="2c0ae-142">Copiar valores de hello de **Id. de cliente** y **secreto de cliente**.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-142">Copy hello values of **Client Id** and **Client secret**.</span></span> <span data-ttu-id="2c0ae-143">Necesita ambos tooconfigure Google + como proveedor de identidades en su inquilino.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-143">You need both tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="2c0ae-144">**Secreto del cliente** es una credencial de seguridad importante.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-144">**Client secret** is an important security credential.</span></span>

    ![Google + - valores de hello de copia de secreto de cliente y el Id. de cliente](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="2c0ae-146">Agregar Hola Google + cuenta aplicación clave tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="2c0ae-146">Add hello Google+ account application key tooAzure AD B2C</span></span>
<span data-ttu-id="2c0ae-147">Federación con cuentas de Google + requiere un secreto de cliente para tootrust de cuenta de Google + Azure AD B2C en nombre de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-147">Federation with Google+ accounts requires a client secret for Google+ account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="2c0ae-148">Debe toostore su secreto de aplicación de Google + en el inquilino de Azure AD B2C:</span><span class="sxs-lookup"><span data-stu-id="2c0ae-148">You need toostore your Google+ application secret in Azure AD B2C tenant:</span></span>  

1.  <span data-ttu-id="2c0ae-149">Vaya el inquilino de Azure AD B2C tooyour y seleccione **configuración B2C** > **Framework de la experiencia de identidad**</span><span class="sxs-lookup"><span data-stu-id="2c0ae-149">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="2c0ae-150">Seleccione **claves de directiva** claves de hello tooview disponibles en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-150">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="2c0ae-151">Haga clic en **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-151">Click **+Add**.</span></span>
4.  <span data-ttu-id="2c0ae-152">En **Opciones**, use **Manual**.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-152">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="2c0ae-153">En **Nombre**, use `GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-153">For **Name**, use `GoogleSecret`.</span></span>  
    <span data-ttu-id="2c0ae-154">prefijo de Hello `B2C_1A_` podrían agregarse automáticamente.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-154">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="2c0ae-155">Hola **secreto** cuadro, escriba el secreto de aplicación de Microsoft desde https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="2c0ae-155">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="2c0ae-156">En **Uso de claves**, use **Firma**.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-156">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="2c0ae-157">Haga clic en **Crear**</span><span class="sxs-lookup"><span data-stu-id="2c0ae-157">Click **Create**</span></span>
9.  <span data-ttu-id="2c0ae-158">Confirme que ha creado la clave de hello `B2C_1A_GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-158">Confirm that you've created hello key `B2C_1A_GoogleSecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="2c0ae-159">Adición de un proveedor de notificaciones en la directiva de extensión</span><span class="sxs-lookup"><span data-stu-id="2c0ae-159">Add a claims provider in your extension policy</span></span>

<span data-ttu-id="2c0ae-160">Si desea toosign de usuarios mediante el uso de la cuenta de Google +, necesita toodefine Google + cuenta como un proveedor de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-160">If you want users toosign in by using Google+ account, you need toodefine Google+ account as a claims provider.</span></span> <span data-ttu-id="2c0ae-161">En otras palabras, necesita un punto de conexión que Azure AD B2C se comunica con toospecify.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-161">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="2c0ae-162">punto de conexión de Hello proporciona un conjunto de notificaciones que usan Azure AD B2C tooverify que ha autenticado un usuario específico.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-162">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="2c0ae-163">Defina la cuenta de Google+ como proveedor de notificaciones; para ello, agregue el nodo `<ClaimsProvider>` en el archivo de la directiva de extensión:</span><span class="sxs-lookup"><span data-stu-id="2c0ae-163">Define Google+ Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="2c0ae-164">Abra el archivo de directiva de extensión de hello (TrustFrameworkExtensions.xml) desde el directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-164">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="2c0ae-165">Si necesita un editor XML, [pruebe Visual Studio Code](https://code.visualstudio.com/download), un editor multiplataforma ligero.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-165">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="2c0ae-166">Buscar hello `<ClaimsProviders>` sección</span><span class="sxs-lookup"><span data-stu-id="2c0ae-166">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="2c0ae-167">Agregar Hola siguiente fragmento XML en hello `ClaimsProviders` elemento y reemplace `client_id` valor con su Google + cuenta aplicación ID de cliente antes de guardar el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-167">Add hello following XML snippet under hello `ClaimsProviders` element and replace `client_id` value with your Google+ account application client ID before saving hello file.</span></span>  

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

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="2c0ae-168">Registrar el proveedor de notificaciones de cuenta de hello Google + tooSign seguridad o iniciar sesión en el viaje de usuario</span><span class="sxs-lookup"><span data-stu-id="2c0ae-168">Register hello Google+ account claims provider tooSign up or Sign in user journey</span></span>

<span data-ttu-id="2c0ae-169">se ha configurado el proveedor de identidades de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-169">hello identity provider has been set up.</span></span>  <span data-ttu-id="2c0ae-170">Sin embargo, no está disponible en ninguna de hello sesión-up/inicio de sesión de pantallas.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-170">However, it is not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="2c0ae-171">Agregar usuario tooyour de hello Google + cuenta identidad proveedor `SignUpOrSignIn` viaje de usuario.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-171">Add hello Google+ account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="2c0ae-172">toomake está disponible, se crea un duplicado de un viaje de usuario de plantilla existente.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-172">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="2c0ae-173">A continuación, agregamos Hola Google + cuenta Yahoo!:</span><span class="sxs-lookup"><span data-stu-id="2c0ae-173">Then we add hello Google+ account identity provider:</span></span>

>[!NOTE]
>
><span data-ttu-id="2c0ae-174">Si ha copiado hello `<UserJourneys>` elemento de archivo de base de su archivo de extensión de directiva de toohello (TrustFrameworkExtensions.xml), puede omitir la sección toothis.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-174">If you copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml), you can skip toothis section.</span></span>

1.  <span data-ttu-id="2c0ae-175">Abra el archivo de base de hello de la directiva (por ejemplo, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="2c0ae-175">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="2c0ae-176">Buscar hello `<UserJourneys>` elemento y copia Hola todo el contenido de `<UserJourneys>` nodo.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-176">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="2c0ae-177">Abra el archivo de extensión de hello (por ejemplo, TrustFrameworkExtensions.xml) y busque hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-177">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="2c0ae-178">Si no existe el elemento hello, agregue uno.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-178">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="2c0ae-179">Pegue todo el contenido de hello `<UserJournesy>` nodo que ha copiado como elemento secundario de hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-179">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="2c0ae-180">Botón de mostrar hello</span><span class="sxs-lookup"><span data-stu-id="2c0ae-180">Display hello button</span></span>
<span data-ttu-id="2c0ae-181">Hola `<ClaimsProviderSelections>` elemento define la lista de Hola de opciones de selección del proveedor de notificaciones y su orden.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-181">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="2c0ae-182">`<ClaimsProviderSelection>`elemento es análogo tooan el botón del proveedor de identidad en una página de inicio de sesión-up/inicio de sesión de.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-182">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="2c0ae-183">Si agrega un `<ClaimsProviderSelection>` elemento para la cuenta de Google +, un nuevo botón aparezca cuando llega a un usuario en la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-183">If you add a `<ClaimsProviderSelection>` element for Google+ account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="2c0ae-184">tooadd este elemento:</span><span class="sxs-lookup"><span data-stu-id="2c0ae-184">tooadd this element:</span></span>

1.  <span data-ttu-id="2c0ae-185">Buscar hello `<UserJourney>` nodo que incluya `Id="SignUpOrSignIn"` en viaje de usuario de Hola que ha copiado.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-185">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="2c0ae-186">Busque hello `<OrchestrationStep>` nodo que incluye`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="2c0ae-186">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="2c0ae-187">Agregue el siguiente fragmento de código XML en el nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="2c0ae-187">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="2c0ae-188">Acción del botón de vínculo hello tooan</span><span class="sxs-lookup"><span data-stu-id="2c0ae-188">Link hello button tooan action</span></span>
<span data-ttu-id="2c0ae-189">Ahora que tiene un botón en su lugar, debe toolink tooan acción.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-189">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="2c0ae-190">acción de Hello, en este caso, es para Azure AD B2C toocommunicate con Google + cuenta tooreceive un token.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-190">hello action, in this case, is for Azure AD B2C toocommunicate with Google+ account tooreceive a token.</span></span>

1.  <span data-ttu-id="2c0ae-191">Buscar hello `<OrchestrationStep>` que incluye `Order="2"` en hello `<UserJourney>` nodo.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-191">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="2c0ae-192">Agregue el siguiente fragmento de código XML en el nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="2c0ae-192">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * <span data-ttu-id="2c0ae-193">Asegúrese de hello `Id` tiene Hola mismo valor que el de `TargetClaimsExchangeId` en la sección anterior de Hola</span><span class="sxs-lookup"><span data-stu-id="2c0ae-193">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
> * <span data-ttu-id="2c0ae-194">Asegúrese de `TechnicalProfileReferenceId` se estableció el identificador de perfil técnico toohello que creó anteriormente (Google-OAUTH).</span><span class="sxs-lookup"><span data-stu-id="2c0ae-194">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (Google-OAUTH).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="2c0ae-195">Cargar el inquilino de hello directiva tooyour</span><span class="sxs-lookup"><span data-stu-id="2c0ae-195">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="2c0ae-196">Hola [portal de Azure](https://portal.azure.com), cambiar a hello [contexto de su inquilino de Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md), abra hello y **Azure AD B2C** hoja.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-196">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="2c0ae-197">Seleccione **Marco de experiencia de identidad**.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-197">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="2c0ae-198">Abra hello **todas las directivas** hoja.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-198">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="2c0ae-199">Seleccione **Cargar directiva**.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-199">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="2c0ae-200">Comprobar **sobrescribir directiva Hola si existe** cuadro.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-200">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="2c0ae-201">**Cargar** TrustFrameworkExtensions.xml y asegúrese de que no considerará no válido de Hola</span><span class="sxs-lookup"><span data-stu-id="2c0ae-201">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="2c0ae-202">Probar directiva personalizada de hello mediante Ejecutar ahora</span><span class="sxs-lookup"><span data-stu-id="2c0ae-202">Test hello custom policy by using Run Now</span></span>
1.  <span data-ttu-id="2c0ae-203">Abra **configuración de Azure AD B2C** y vaya demasiado**identidad experiencia Framework**.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-203">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>

    >[!NOTE]
    >
    >    <span data-ttu-id="2c0ae-204">**Ejecutar ahora** requiere al menos una aplicación toobe registrada previamente en el inquilino de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-204">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> 
    >    <span data-ttu-id="2c0ae-205">toolearn tooregister aplicaciones, vea hello Azure AD B2C [Introducción](active-directory-b2c-get-started.md) artículo o hello [registro de la aplicación](active-directory-b2c-app-registration.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-205">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>


2.  <span data-ttu-id="2c0ae-206">Abra **B2C_1A_signup_signin**, Hola directiva personalizada de confianza (RP) de la entidad que ha cargado.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-206">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="2c0ae-207">Seleccione **Ejecutar ahora**.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-207">Select **Run now**.</span></span>
3.  <span data-ttu-id="2c0ae-208">Debe ser capaz de toosign con cuenta de Google +.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-208">You should be able toosign in using Google+ account.</span></span>

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="2c0ae-209">[Opcional] Registrar Hola Google + cuenta notificaciones proveedor tooProfile Editar usuario viaje</span><span class="sxs-lookup"><span data-stu-id="2c0ae-209">[Optional] Register hello Google+ account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="2c0ae-210">Tal vez desee tooadd Hola Google + cuenta proveedor de identidades también tooyour usuario `ProfileEdit` viaje de usuario.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-210">You may want tooadd hello Google+ account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="2c0ae-211">toomake está disponible, se repita Hola últimos dos pasos:</span><span class="sxs-lookup"><span data-stu-id="2c0ae-211">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="2c0ae-212">Botón de mostrar hello</span><span class="sxs-lookup"><span data-stu-id="2c0ae-212">Display hello button</span></span>
1.  <span data-ttu-id="2c0ae-213">Abra el archivo de extensión de hello de la directiva (por ejemplo, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="2c0ae-213">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="2c0ae-214">Buscar hello `<UserJourney>` nodo que incluya `Id="ProfileEdit"` en viaje de usuario de Hola que ha copiado.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-214">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="2c0ae-215">Busque hello `<OrchestrationStep>` nodo que incluye`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="2c0ae-215">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="2c0ae-216">Agregue el siguiente fragmento de código XML en el nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="2c0ae-216">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="2c0ae-217">Acción del botón de vínculo hello tooan</span><span class="sxs-lookup"><span data-stu-id="2c0ae-217">Link hello button tooan action</span></span>
1.  <span data-ttu-id="2c0ae-218">Buscar hello `<OrchestrationStep>` que incluye `Order="2"` en hello `<UserJourney>` nodo.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-218">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="2c0ae-219">Agregue el siguiente fragmento de código XML en el nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="2c0ae-219">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="2c0ae-220">Probar la directiva de edición de perfil personalizada hello mediante Ejecutar ahora</span><span class="sxs-lookup"><span data-stu-id="2c0ae-220">Test hello custom Profile-Edit policy by using Run Now</span></span>

1.  <span data-ttu-id="2c0ae-221">Abra **configuración de Azure AD B2C** y vaya demasiado**identidad experiencia Framework**.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-221">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="2c0ae-222">Abra **B2C_1A_ProfileEdit**, Hola directiva personalizada de confianza (RP) de la entidad que ha cargado.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-222">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="2c0ae-223">Seleccione **Ejecutar ahora**.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-223">Select **Run now**.</span></span>
3.  <span data-ttu-id="2c0ae-224">Debe ser capaz de toosign con cuenta de Google +.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-224">You should be able toosign in using Google+ account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="2c0ae-225">Descargar archivos de directiva completa Hola</span><span class="sxs-lookup"><span data-stu-id="2c0ae-225">Download hello complete policy files</span></span>
<span data-ttu-id="2c0ae-226">Opcional: Se recomienda que elabore su escenario con sus propios archivos de directiva personalizada después de completar la introducción a las directivas personalizadas recorra en lugar de utilizar estos archivos de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c0ae-226">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="2c0ae-227">Archivos de directiva de ejemplo de referencia</span><span class="sxs-lookup"><span data-stu-id="2c0ae-227">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
