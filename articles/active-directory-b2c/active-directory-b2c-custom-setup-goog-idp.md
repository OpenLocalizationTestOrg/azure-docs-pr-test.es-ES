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
ms.openlocfilehash: e0aaf710d230f7667fff32b50ddb64104509d740
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a><span data-ttu-id="61801-103">Azure Active Directory B2C: adición de Google + como un proveedor de identidades de OAuth2 mediante directivas personalizadas</span><span class="sxs-lookup"><span data-stu-id="61801-103">Azure Active Directory B2C: Add Google+ as an OAuth2 identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="61801-104">En esta guía se muestra cómo habilitar el inicio de sesión para usuarios de desde la cuenta de Google+ mediante [directivas personalizadas](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="61801-104">This guide shows you how to enable sign-in for users from Google+ account through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61801-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="61801-105">Prerequisites</span></span>

<span data-ttu-id="61801-106">Complete los pasos del artículo [Introducción a las directivas personalizadas](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="61801-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="61801-107">Estos pasos incluyen:</span><span class="sxs-lookup"><span data-stu-id="61801-107">These steps include:</span></span>

1.  <span data-ttu-id="61801-108">Crear una aplicación de la cuenta de Google+</span><span class="sxs-lookup"><span data-stu-id="61801-108">Creating a Google+ account application.</span></span>
2.  <span data-ttu-id="61801-109">Agregar la clave de aplicación de la cuenta de Google+ a Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="61801-109">Adding the Google+ account application key to Azure AD B2C</span></span>
3.  <span data-ttu-id="61801-110">Agregar un proveedor de notificaciones a una directiva</span><span class="sxs-lookup"><span data-stu-id="61801-110">Adding claims provider to a policy</span></span>
4.  <span data-ttu-id="61801-111">Registrar el proveedor de notificaciones de la cuenta de Google + en un recorrido del usuario</span><span class="sxs-lookup"><span data-stu-id="61801-111">Registering the Google+ account claims provider to a user journey</span></span>
5.  <span data-ttu-id="61801-112">Cargar la directiva en un inquilino de Azure AD B2C y probarla</span><span class="sxs-lookup"><span data-stu-id="61801-112">Uploading the policy to an Azure AD B2C tenant and test it</span></span>

## <a name="create-a-google-account-application"></a><span data-ttu-id="61801-113">Creación de una aplicación de la cuenta de Google+</span><span class="sxs-lookup"><span data-stu-id="61801-113">Create a Google+ account application</span></span>
<span data-ttu-id="61801-114">Para usar Google+ como proveedor de identidades en Azure Active Directory (Azure AD) B2C, debe crear una aplicación de Google+ y suministrarle los parámetros correctos.</span><span class="sxs-lookup"><span data-stu-id="61801-114">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span></span> <span data-ttu-id="61801-115">Puede registrar una aplicación de Google+ aquí: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="61801-115">You can register a Google+ application here: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span></span>

1.  <span data-ttu-id="61801-116">Vaya a [Google Developers Console](https://console.developers.google.com/) e inicie sesión con las credenciales de su cuenta de Google+.</span><span class="sxs-lookup"><span data-stu-id="61801-116">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2.  <span data-ttu-id="61801-117">Haga clic en **Create project** (Crear proyecto), escriba un nombre de proyecto en **Project name** y haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="61801-117">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>

3.  <span data-ttu-id="61801-118">Haga clic en el menú **Projects** (Proyectos).</span><span class="sxs-lookup"><span data-stu-id="61801-118">Click on the **Projects menu**.</span></span>

    ![Cuenta de Google+: Selección del proyecto](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  <span data-ttu-id="61801-120">Haga clic en el botón **+**.</span><span class="sxs-lookup"><span data-stu-id="61801-120">Click on the **+** button.</span></span>

    ![Cuenta de Google+: Creación de un nuevo proyecto](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  <span data-ttu-id="61801-122">Escriba un **nombre de proyecto** y luego haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="61801-122">Enter a **Project name**, and then click **Create**.</span></span>

    ![Cuenta de Google+: Nuevo proyecto](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  <span data-ttu-id="61801-124">Espere a que el proyecto esté listo y haga clic en el menú **Projects** (Proyectos).</span><span class="sxs-lookup"><span data-stu-id="61801-124">Wait until the project is ready and click on the **Projects menu**.</span></span>

    ![Cuenta de Google+: Esperar a que el nuevo proyecto esté listo para usar](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  <span data-ttu-id="61801-126">Haga clic en el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="61801-126">Click on your project name.</span></span>

    ![Cuenta de Google+: Selección del nuevo proyecto](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  <span data-ttu-id="61801-128">En el panel de navegación izquierdo, haga clic en **API Manager** (Administrador de API) y, luego, en **Credentials** (Credenciales).</span><span class="sxs-lookup"><span data-stu-id="61801-128">Click **API Manager** and then click **Credentials** in the left navigation.</span></span>
9.  <span data-ttu-id="61801-129">Haga clic en la **pantalla de autorización de OAuth** en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="61801-129">Click the **OAuth consent screen** tab at the top.</span></span>

    ![Cuenta de Google+: Configuración de la pantalla de consentimiento de OAuth](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  <span data-ttu-id="61801-131">Seleccione o especifique una dirección de correo electrónico válida en **Email address**, especifique un nombre de producto en **Product name** y haga clic en **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="61801-131">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>

    ![Google+: Credenciales de la aplicación](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  <span data-ttu-id="61801-133">Haga clic en **New credentials** (Nuevas credenciales) y, luego, elija **OAuth client ID** (Id. de cliente de OAuth).</span><span class="sxs-lookup"><span data-stu-id="61801-133">Click **New credentials** and then choose **OAuth client ID**.</span></span>

    ![Google+: Creación de nuevas credenciales de aplicación](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  <span data-ttu-id="61801-135">En **Application type** (Tipo de aplicación), seleccione **Web application** (Aplicación web).</span><span class="sxs-lookup"><span data-stu-id="61801-135">Under **Application type**, select **Web application**.</span></span>

    ![Google+: Selección del tipo de aplicación](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  <span data-ttu-id="61801-137">Especifique un **nombre** para la aplicación, escriba `https://login.microsoftonline.com` en el campo **Authorized JavaScript origins** (Orígenes de JavaScript autorizados) y `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` en el campo **Authorized redirect URIs** (URI de redirección autorizados).</span><span class="sxs-lookup"><span data-stu-id="61801-137">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in the **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized redirect URIs** field.</span></span> <span data-ttu-id="61801-138">Reemplace **{tenant}** por el nombre de su inquilino (por ejemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="61801-138">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="61801-139">El valor de **{tenant}** distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="61801-139">The **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="61801-140">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="61801-140">Click **Create**.</span></span>

    ![Google+: Provisión de los orígenes y los URI de redirección autorizados de JavaScript](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  <span data-ttu-id="61801-142">Copie los valores de **Client Id** (Id. de cliente) y **Client secret** (Secreto de cliente).</span><span class="sxs-lookup"><span data-stu-id="61801-142">Copy the values of **Client Id** and **Client secret**.</span></span> <span data-ttu-id="61801-143">Debe configurar Google+ como proveedor de identidades en su inquilino.</span><span class="sxs-lookup"><span data-stu-id="61801-143">You need both to configure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="61801-144">**Secreto del cliente** es una credencial de seguridad importante.</span><span class="sxs-lookup"><span data-stu-id="61801-144">**Client secret** is an important security credential.</span></span>

    ![Google+: Copia de los valores de id. de cliente y secreto de cliente](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-the-google-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="61801-146">Adición de la clave de aplicación de la cuenta de Google+ a Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="61801-146">Add the Google+ account application key to Azure AD B2C</span></span>
<span data-ttu-id="61801-147">La federación con cuentas de Google+ requiere un secreto de cliente para que la cuenta de Google+ confíe en Azure AD B2C en nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61801-147">Federation with Google+ accounts requires a client secret for Google+ account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="61801-148">Debe almacenar el secreto de aplicación de Google+ en el inquilino de Azure AD B2C:</span><span class="sxs-lookup"><span data-stu-id="61801-148">You need to store your Google+ application secret in Azure AD B2C tenant:</span></span>  

1.  <span data-ttu-id="61801-149">Vaya a su inquilino de Azure AD B2C y seleccione **B2C Settings (Configuración de B2C)** > **Marco de experiencia de identidad**.</span><span class="sxs-lookup"><span data-stu-id="61801-149">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="61801-150">Seleccione **Policy Keys** (Claves de directiva) para ver las claves disponibles en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="61801-150">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="61801-151">Haga clic en **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="61801-151">Click **+Add**.</span></span>
4.  <span data-ttu-id="61801-152">En **Opciones**, use **Manual**.</span><span class="sxs-lookup"><span data-stu-id="61801-152">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="61801-153">En **Nombre**, use `GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="61801-153">For **Name**, use `GoogleSecret`.</span></span>  
    <span data-ttu-id="61801-154">Es posible que se agregue automáticamente el prefijo `B2C_1A_`.</span><span class="sxs-lookup"><span data-stu-id="61801-154">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="61801-155">En el cuadro **Secreto**, escriba el secreto de aplicación de Microsoft desde https://apps.dev.microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="61801-155">In the **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="61801-156">En **Uso de claves**, use **Firma**.</span><span class="sxs-lookup"><span data-stu-id="61801-156">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="61801-157">Haga clic en **Crear**</span><span class="sxs-lookup"><span data-stu-id="61801-157">Click **Create**</span></span>
9.  <span data-ttu-id="61801-158">Confirme que ha creado la clave `B2C_1A_GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="61801-158">Confirm that you've created the key `B2C_1A_GoogleSecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="61801-159">Adición de un proveedor de notificaciones en la directiva de extensión</span><span class="sxs-lookup"><span data-stu-id="61801-159">Add a claims provider in your extension policy</span></span>

<span data-ttu-id="61801-160">Si desea que los usuarios inicien sesión mediante la cuenta de Google+, debe definir dicha cuenta como proveedor de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="61801-160">If you want users to sign in by using Google+ account, you need to define Google+ account as a claims provider.</span></span> <span data-ttu-id="61801-161">En otras palabras, debe especificar un punto de conexión con el que Azure AD B2C se comunica.</span><span class="sxs-lookup"><span data-stu-id="61801-161">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="61801-162">El punto de conexión proporciona un conjunto de notificaciones que Azure AD B2C usa para comprobar que un usuario concreto se ha autenticado.</span><span class="sxs-lookup"><span data-stu-id="61801-162">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="61801-163">Defina la cuenta de Google+ como proveedor de notificaciones; para ello, agregue el nodo `<ClaimsProvider>` en el archivo de la directiva de extensión:</span><span class="sxs-lookup"><span data-stu-id="61801-163">Define Google+ Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="61801-164">Abra el archivo de directiva de extensión (TrustFrameworkExtensions.xml) desde el directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="61801-164">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="61801-165">Si necesita un editor XML, [pruebe Visual Studio Code](https://code.visualstudio.com/download), un editor multiplataforma ligero.</span><span class="sxs-lookup"><span data-stu-id="61801-165">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="61801-166">Busque la sección `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="61801-166">Find the `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="61801-167">Agregue el siguiente fragmento de código XML bajo el elemento `ClaimsProviders` y sustituya el valor `client_id` por su id. de cliente de aplicación de la cuenta de Google+ antes de guardar el archivo.</span><span class="sxs-lookup"><span data-stu-id="61801-167">Add the following XML snippet under the `ClaimsProviders` element and replace `client_id` value with your Google+ account application client ID before saving the file.</span></span>  

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
            <!--In case of authorization code used error, we don't want the user to select his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-the-google-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="61801-168">Registro del proveedor de notificaciones de Google+ en el recorrido del usuario de registro o inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="61801-168">Register the Google+ account claims provider to Sign up or Sign in user journey</span></span>

<span data-ttu-id="61801-169">Se ha configurado el proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="61801-169">The identity provider has been set up.</span></span>  <span data-ttu-id="61801-170">Sin embargo, no está disponible en ninguna de las pantallas de registro o inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="61801-170">However, it is not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="61801-171">Agregue el proveedor de identidades de la cuenta de Google+ al recorrido del usuario `SignUpOrSignIn` del usuario.</span><span class="sxs-lookup"><span data-stu-id="61801-171">Add the Google+ account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="61801-172">Para que esté disponible, se crea un duplicado de un recorrido del usuario de plantilla ya existente.</span><span class="sxs-lookup"><span data-stu-id="61801-172">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="61801-173">A continuación, se agrega el proveedor de identidades de la cuenta de Google +:</span><span class="sxs-lookup"><span data-stu-id="61801-173">Then we add the Google+ account identity provider:</span></span>

>[!NOTE]
>
><span data-ttu-id="61801-174">Si ha copiado el elemento `<UserJourneys>` del archivo base de su directiva en el archivo de extensión (TrustFrameworkExtensions.xml), puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="61801-174">If you copied the `<UserJourneys>` element from base file of your policy to the extension file (TrustFrameworkExtensions.xml), you can skip to this section.</span></span>

1.  <span data-ttu-id="61801-175">Abra el archivo base de la directiva (por ejemplo, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="61801-175">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="61801-176">Busque el elemento `<UserJourneys>` y copie el contenido entero del nodo `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="61801-176">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="61801-177">Abra el archivo de extensión (por ejemplo, TrustFrameworkExtensions.xml) y busque el elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="61801-177">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="61801-178">Si el elemento no existe, agréguelo.</span><span class="sxs-lookup"><span data-stu-id="61801-178">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="61801-179">Pegue el contenido entero del nodo `<UserJournesy>` que copió como secundario del elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="61801-179">Paste the entire content of `<UserJournesy>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="61801-180">Visualización del botón</span><span class="sxs-lookup"><span data-stu-id="61801-180">Display the button</span></span>
<span data-ttu-id="61801-181">El elemento `<ClaimsProviderSelections>` define la lista de opciones de selección del proveedor de notificaciones y su orden.</span><span class="sxs-lookup"><span data-stu-id="61801-181">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="61801-182">El elemento `<ClaimsProviderSelection>` es análogo a un botón de proveedor de identidades de una página de registro o inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="61801-182">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="61801-183">Si agrega un elemento `<ClaimsProviderSelection>` para la cuenta de Google+, se muestra un nuevo botón cuando un usuario llega a la página.</span><span class="sxs-lookup"><span data-stu-id="61801-183">If you add a `<ClaimsProviderSelection>` element for Google+ account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="61801-184">Para agregar este elemento:</span><span class="sxs-lookup"><span data-stu-id="61801-184">To add this element:</span></span>

1.  <span data-ttu-id="61801-185">Busque el nodo `<UserJourney>` que incluye `Id="SignUpOrSignIn"` en el recorrido del usuario que ha copiado.</span><span class="sxs-lookup"><span data-stu-id="61801-185">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="61801-186">Busque el nodo `<OrchestrationStep>` que incluye `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="61801-186">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="61801-187">Agregue el siguiente fragmento de código XML en el nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="61801-187">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="61801-188">Vincular el botón a una acción</span><span class="sxs-lookup"><span data-stu-id="61801-188">Link the button to an action</span></span>
<span data-ttu-id="61801-189">Ahora que hay un botón colocado, es preciso vincularlo a una acción.</span><span class="sxs-lookup"><span data-stu-id="61801-189">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="61801-190">En este caso, la acción es para que Azure AD B2C se comunique con la cuenta de Google+ para recibir un token.</span><span class="sxs-lookup"><span data-stu-id="61801-190">The action, in this case, is for Azure AD B2C to communicate with Google+ account to receive a token.</span></span>

1.  <span data-ttu-id="61801-191">Busque el nodo `<OrchestrationStep>` que incluye `Order="2"` en el nodo `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="61801-191">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="61801-192">Agregue el siguiente fragmento de código XML en el nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="61801-192">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * <span data-ttu-id="61801-193">Asegúrese de que el valor de `Id` sea el mismo que el de `TargetClaimsExchangeId` en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="61801-193">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section</span></span>
> * <span data-ttu-id="61801-194">Asegúrese de que el id. de `TechnicalProfileReferenceId` se establece en el perfil técnico que creó anteriormente (Google-OAUTH).</span><span class="sxs-lookup"><span data-stu-id="61801-194">Ensure `TechnicalProfileReferenceId` ID is set to the technical profile you created earlier (Google-OAUTH).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="61801-195">Carga de la directiva en el inquilino</span><span class="sxs-lookup"><span data-stu-id="61801-195">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="61801-196">En [Azure Portal](https://portal.azure.com), cambie al [contexto del inquilino de Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md) y abra la hoja **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="61801-196">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="61801-197">Seleccione **Marco de experiencia de identidad**.</span><span class="sxs-lookup"><span data-stu-id="61801-197">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="61801-198">Abra la hoja **Todas las directivas**.</span><span class="sxs-lookup"><span data-stu-id="61801-198">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="61801-199">Seleccione **Cargar directiva**.</span><span class="sxs-lookup"><span data-stu-id="61801-199">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="61801-200">Active la casilla **Sobrescribir la directiva si existe**.</span><span class="sxs-lookup"><span data-stu-id="61801-200">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="61801-201">**Cargue** TrustFrameworkExtensions.xml y asegúrese de que no se produce ningún error en la validación.</span><span class="sxs-lookup"><span data-stu-id="61801-201">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="61801-202">Probar la directiva personalizada con Ejecutar ahora</span><span class="sxs-lookup"><span data-stu-id="61801-202">Test the custom policy by using Run Now</span></span>
1.  <span data-ttu-id="61801-203">Abra la **configuración de Azure AD B2C** y vaya a **Marco de experiencia de identidad**.</span><span class="sxs-lookup"><span data-stu-id="61801-203">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>

    >[!NOTE]
    >
    >    <span data-ttu-id="61801-204">**Ejecutar ahora** Requiere al menos que una aplicación esté registrada previamente en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="61801-204">**Run now** requires at least one application to be preregistered on the tenant.</span></span> 
    >    <span data-ttu-id="61801-205">Para obtener información sobre cómo registrar aplicaciones, vea el artículo de [introducción](active-directory-b2c-get-started.md) a Azure AD B2C o el artículo [Registro de la aplicación](active-directory-b2c-app-registration.md) de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="61801-205">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>


2.  <span data-ttu-id="61801-206">Abra **B2C_1A_signup_signin**, que es la directiva personalizada del usuario de confianza (RP) que ha cargado.</span><span class="sxs-lookup"><span data-stu-id="61801-206">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="61801-207">Seleccione **Ejecutar ahora**.</span><span class="sxs-lookup"><span data-stu-id="61801-207">Select **Run now**.</span></span>
3.  <span data-ttu-id="61801-208">Debería poder iniciar sesión con la cuenta de Google+.</span><span class="sxs-lookup"><span data-stu-id="61801-208">You should be able to sign in using Google+ account.</span></span>

## <a name="optional-register-the-google-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="61801-209">[Opcional] Registro del proveedor de notificaciones de la cuenta en Google+ en el recorrido del usuario de edición de perfil</span><span class="sxs-lookup"><span data-stu-id="61801-209">[Optional] Register the Google+ account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="61801-210">Puede que también desee agregar el proveedor de identidades de la cuenta de Google + al recorrido del usuario `ProfileEdit` de su usuario.</span><span class="sxs-lookup"><span data-stu-id="61801-210">You may want to add the Google+ account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="61801-211">Para que esté disponible, se repiten los dos últimos pasos:</span><span class="sxs-lookup"><span data-stu-id="61801-211">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="61801-212">Visualización del botón</span><span class="sxs-lookup"><span data-stu-id="61801-212">Display the button</span></span>
1.  <span data-ttu-id="61801-213">Abra el archivo de extensión de su directiva (por ejemplo, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="61801-213">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="61801-214">Busque el nodo `<UserJourney>` que incluye `Id="ProfileEdit"` en el recorrido del usuario que ha copiado.</span><span class="sxs-lookup"><span data-stu-id="61801-214">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="61801-215">Busque el nodo `<OrchestrationStep>` que incluye `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="61801-215">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="61801-216">Agregue el siguiente fragmento de código XML en el nodo `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="61801-216">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="61801-217">Vincular el botón a una acción</span><span class="sxs-lookup"><span data-stu-id="61801-217">Link the button to an action</span></span>
1.  <span data-ttu-id="61801-218">Busque el nodo `<OrchestrationStep>` que incluye `Order="2"` en el nodo `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="61801-218">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="61801-219">Agregue el siguiente fragmento de código XML en el nodo `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="61801-219">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="61801-220">Prueba de la directiva de edición de perfil personalizada mediante Ejecutar ahora</span><span class="sxs-lookup"><span data-stu-id="61801-220">Test the custom Profile-Edit policy by using Run Now</span></span>

1.  <span data-ttu-id="61801-221">Abra la **configuración de Azure AD B2C** y vaya a **Marco de experiencia de identidad**.</span><span class="sxs-lookup"><span data-stu-id="61801-221">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="61801-222">Abra **B2C_1A_ProfileEdit**, que es la directiva personalizada del usuario de confianza (RP) que ha cargado.</span><span class="sxs-lookup"><span data-stu-id="61801-222">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="61801-223">Seleccione **Ejecutar ahora**.</span><span class="sxs-lookup"><span data-stu-id="61801-223">Select **Run now**.</span></span>
3.  <span data-ttu-id="61801-224">Debería poder iniciar sesión con la cuenta de Google+.</span><span class="sxs-lookup"><span data-stu-id="61801-224">You should be able to sign in using Google+ account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="61801-225">Descarga de los archivos de directiva completos</span><span class="sxs-lookup"><span data-stu-id="61801-225">Download the complete policy files</span></span>
<span data-ttu-id="61801-226">Opcional: se recomienda que, en lugar de usar estos archivos de ejemplo, cree su escenario con sus propios archivos de directiva personalizada tras completar el tutorial de introducción a las directivas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="61801-226">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="61801-227">Archivos de directiva de ejemplo de referencia</span><span class="sxs-lookup"><span data-stu-id="61801-227">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
