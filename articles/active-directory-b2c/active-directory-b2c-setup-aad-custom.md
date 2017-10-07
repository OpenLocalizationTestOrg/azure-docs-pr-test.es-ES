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
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="90b2a-103">Azure Active Directory B2C: inicio de sesión con cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="90b2a-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="90b2a-104">Este artículo muestra cómo tooenable sesión para los usuarios de una organización específica de Azure Active Directory (Azure AD) mediante el uso de Hola de [directivas personalizadas de](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="90b2a-104">This article shows you how tooenable sign-in for users from a specific Azure Active Directory (Azure AD) organization through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90b2a-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="90b2a-105">Prerequisites</span></span>

<span data-ttu-id="90b2a-106">Hola completa los pasos de hello [Introducción a las directivas personalizadas](active-directory-b2c-get-started-custom.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="90b2a-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="90b2a-107">Estos pasos incluyen:</span><span class="sxs-lookup"><span data-stu-id="90b2a-107">These steps include:</span></span>

1. <span data-ttu-id="90b2a-108">Creación de un inquilino de Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="90b2a-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="90b2a-109">Creación de una aplicación de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="90b2a-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="90b2a-110">Registro de dos aplicaciones de motor de directivas.</span><span class="sxs-lookup"><span data-stu-id="90b2a-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="90b2a-111">Configuración de claves.</span><span class="sxs-lookup"><span data-stu-id="90b2a-111">Setting up keys.</span></span>
5. <span data-ttu-id="90b2a-112">Configurar el módulo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="90b2a-112">Setting up hello starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="90b2a-113">Creación de una aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="90b2a-113">Create an Azure AD app</span></span>

<span data-ttu-id="90b2a-114">inicio de sesión en tooenable para los usuarios de una determinada organización de Azure AD, necesita tooregister una aplicación en el inquilino de hello organizativa AD de Azure.</span><span class="sxs-lookup"><span data-stu-id="90b2a-114">tooenable sign-in for users from a specific Azure AD organization, you need tooregister an application within hello organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="90b2a-115">Utilizamos "contoso.com" para el inquilino Hola organizativa AD de Azure y "fabrikamb2c.onmicrosoft.com" como inquilino de Azure AD B2C Hola Hola siguiendo las instrucciones.</span><span class="sxs-lookup"><span data-stu-id="90b2a-115">We use "contoso.com" for hello organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as hello Azure AD B2C tenant in hello following instructions.</span></span>

1. <span data-ttu-id="90b2a-116">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="90b2a-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="90b2a-117">En la barra superior de hello, seleccione su cuenta.</span><span class="sxs-lookup"><span data-stu-id="90b2a-117">On hello top bar, select your account.</span></span> <span data-ttu-id="90b2a-118">De hello **Directory** elija inquilino Hola organizativa AD de Azure donde desee tooregister la aplicación (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="90b2a-118">From hello **Directory** list, choose hello organizational Azure AD tenant where you want tooregister your application (contoso.com).</span></span>
1. <span data-ttu-id="90b2a-119">Seleccione **más servicios** en el panel izquierdo de Hola y busque "Registros de aplicación".</span><span class="sxs-lookup"><span data-stu-id="90b2a-119">Select **More services** in hello left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="90b2a-120">Seleccione **Nuevo registro de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="90b2a-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="90b2a-121">Escriba el nombre de la aplicación (por ejemplo, `Azure AD B2C App`).</span><span class="sxs-lookup"><span data-stu-id="90b2a-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="90b2a-122">Seleccione **aplicación Web / API** para el tipo de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="90b2a-122">Select **Web app / API** for hello application type.</span></span>
1. <span data-ttu-id="90b2a-123">Para **dirección URL de inicio de sesión**, escriba Hola después de la dirección URL, donde `yourtenant` se sustituye por el nombre de Hola de su inquilino de Azure AD B2C (`fabrikamb2c.onmicrosoft.com`):</span><span class="sxs-lookup"><span data-stu-id="90b2a-123">For **Sign-on URL**, enter hello following URL, where `yourtenant` is replaced by hello name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="90b2a-124">Guardar el identificador de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="90b2a-124">Save hello application ID.</span></span>
1. <span data-ttu-id="90b2a-125">Seleccione la aplicación hello recién creado.</span><span class="sxs-lookup"><span data-stu-id="90b2a-125">Select hello newly created application.</span></span>
1. <span data-ttu-id="90b2a-126">En hello **configuración** hoja, seleccione **claves**.</span><span class="sxs-lookup"><span data-stu-id="90b2a-126">Under hello **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="90b2a-127">Cree una clave y guárdela.</span><span class="sxs-lookup"><span data-stu-id="90b2a-127">Create a new key, and save it.</span></span> <span data-ttu-id="90b2a-128">Se utilizará en los pasos de hello en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="90b2a-128">You will use it in hello steps in hello next section.</span></span>

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a><span data-ttu-id="90b2a-129">Agregar tooAzure clave de hello AD de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="90b2a-129">Add hello Azure AD key tooAzure AD B2C</span></span>

<span data-ttu-id="90b2a-130">Necesita clave de la aplicación hello toostore contoso.com en su inquilino de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="90b2a-130">You need toostore hello contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="90b2a-131">toodo esto:</span><span class="sxs-lookup"><span data-stu-id="90b2a-131">toodo this:</span></span>
1. <span data-ttu-id="90b2a-132">Vaya el inquilino de Azure AD B2C tooyour y seleccione **B2C configuración** > **identidad experiencia Framework** > **claves de directiva**.</span><span class="sxs-lookup"><span data-stu-id="90b2a-132">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="90b2a-133">Seleccione **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="90b2a-133">Select **+Add**.</span></span>
1. <span data-ttu-id="90b2a-134">Seleccione o especifique estas opciones:</span><span class="sxs-lookup"><span data-stu-id="90b2a-134">Select or enter these options:</span></span>
   * <span data-ttu-id="90b2a-135">Seleccione **Manual**.</span><span class="sxs-lookup"><span data-stu-id="90b2a-135">Select **Manual**.</span></span>
   * <span data-ttu-id="90b2a-136">En **Nombre**, elija un nombre que coincida con el nombre del inquilino de Azure AD (por ejemplo, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="90b2a-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="90b2a-137">prefijo de Hello `B2C_1A_` se agrega automáticamente toohello nombre de la clave.</span><span class="sxs-lookup"><span data-stu-id="90b2a-137">hello prefix `B2C_1A_` is added automatically toohello name of your key.</span></span>
   * <span data-ttu-id="90b2a-138">Pegue la clave de aplicación Hola **secreto** cuadro.</span><span class="sxs-lookup"><span data-stu-id="90b2a-138">Paste your application key in hello **Secret** box.</span></span>
   * <span data-ttu-id="90b2a-139">Seleccione **Firma**.</span><span class="sxs-lookup"><span data-stu-id="90b2a-139">Select **Signature**.</span></span>
1. <span data-ttu-id="90b2a-140">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="90b2a-140">Select **Create**.</span></span>
1. <span data-ttu-id="90b2a-141">Confirme que ha creado la clave de hello `B2C_1A_ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="90b2a-141">Confirm that you've created hello key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="90b2a-142">Adición de un proveedor de notificaciones a una directiva de base</span><span class="sxs-lookup"><span data-stu-id="90b2a-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="90b2a-143">Si desea que los usuarios toosign de mediante Azure AD, deberá toodefine Azure AD como un proveedor de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="90b2a-143">If you want users toosign in by using Azure AD, you need toodefine Azure AD as a claims provider.</span></span> <span data-ttu-id="90b2a-144">En otras palabras, necesita un punto de conexión que se puede comunicar con Azure AD B2C toospecify.</span><span class="sxs-lookup"><span data-stu-id="90b2a-144">In other words, you need toospecify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="90b2a-145">punto de conexión de Hello proporcionará un conjunto de notificaciones que usan Azure AD B2C tooverify que ha autenticado un usuario específico.</span><span class="sxs-lookup"><span data-stu-id="90b2a-145">hello endpoint will provide a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span> 

<span data-ttu-id="90b2a-146">Puede definir Azure AD como un proveedor de notificaciones mediante la adición de Azure AD toohello `<ClaimsProvider>` nodo en el archivo de extensión de hello de la directiva:</span><span class="sxs-lookup"><span data-stu-id="90b2a-146">You can define Azure AD as a claims provider by adding Azure AD toohello `<ClaimsProvider>` node in hello extension file of your policy:</span></span>

1. <span data-ttu-id="90b2a-147">Abra el archivo de extensión de hello (TrustFrameworkExtensions.xml) desde el directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="90b2a-147">Open hello extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="90b2a-148">Buscar hello `<ClaimsProviders>` sección.</span><span class="sxs-lookup"><span data-stu-id="90b2a-148">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="90b2a-149">Si no existe, debe agregarlo en el nodo raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="90b2a-149">If it does not exist, add it under hello root node.</span></span>
1. <span data-ttu-id="90b2a-150">Agregue un nuevo nodo `<ClaimsProvider>` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="90b2a-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

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

1. <span data-ttu-id="90b2a-151">En hello `<ClaimsProvider>` nodo, el valor de Hola de actualización para `<Domain>` tooa valor único que puede ser usado toodistinguish desde otros proveedores de identidad.</span><span class="sxs-lookup"><span data-stu-id="90b2a-151">Under hello `<ClaimsProvider>` node, update hello value for `<Domain>` tooa unique value that can be used toodistinguish it from other identity providers.</span></span>
1. <span data-ttu-id="90b2a-152">En hello `<ClaimsProvider>` nodo, el valor de Hola de actualización para `<DisplayName>` tooa nombre descriptivo para hello proveedor de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="90b2a-152">Under hello `<ClaimsProvider>` node, update hello value for `<DisplayName>` tooa friendly name for hello claims provider.</span></span> <span data-ttu-id="90b2a-153">Este valor no se utiliza actualmente.</span><span class="sxs-lookup"><span data-stu-id="90b2a-153">This value is not currently used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="90b2a-154">Actualizar perfil técnica Hola</span><span class="sxs-lookup"><span data-stu-id="90b2a-154">Update hello technical profile</span></span>

<span data-ttu-id="90b2a-155">tooget un token de hello extremo de Azure AD, necesita protocolos de hello toodefine que Azure AD B2C debe usar toocommunicate con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90b2a-155">tooget a token from hello Azure AD endpoint, you need toodefine hello protocols that Azure AD B2C should use toocommunicate with Azure AD.</span></span> <span data-ttu-id="90b2a-156">Esto se realiza dentro de hello `<TechnicalProfile>` elemento de `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="90b2a-156">This is done inside hello `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="90b2a-157">Actualizar el Id. de Hola de hello `<TechnicalProfile>` nodo.</span><span class="sxs-lookup"><span data-stu-id="90b2a-157">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="90b2a-158">Este identificador es toothis toorefer usado perfil técnica de otras partes de la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="90b2a-158">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
1. <span data-ttu-id="90b2a-159">Actualizar el valor de Hola para `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="90b2a-159">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="90b2a-160">Este valor se mostrará en el botón de inicio de sesión de hello en la pantalla de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="90b2a-160">This value will be displayed on hello sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="90b2a-161">Actualizar el valor de Hola para `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="90b2a-161">Update hello value for `<Description>`.</span></span>
1. <span data-ttu-id="90b2a-162">Azure AD usa el protocolo de OpenID Connect de hello, por lo que asegúrese de que el valor de hello `<Protocol>` es `"OpenIdConnect"`.</span><span class="sxs-lookup"><span data-stu-id="90b2a-162">Azure AD uses hello OpenID Connect protocol, so ensure that hello value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="90b2a-163">Necesita tooupdate hello `<Metadata>` sección en el archivo XML de hello, que hace referencia valores de configuración de tooearlier tooreflect Hola para específica de su inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90b2a-163">You need tooupdate hello `<Metadata>` section in hello XML file referred tooearlier tooreflect hello configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="90b2a-164">En el archivo XML de hello, actualice los valores de metadatos de saludo de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="90b2a-164">In hello XML file, update hello metadata values as follows:</span></span>

1. <span data-ttu-id="90b2a-165">Establecer `<Item Key="METADATA">` demasiado`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, donde `yourAzureADtenant` es el nombre del inquilino de Azure AD (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="90b2a-165">Set `<Item Key="METADATA">` too`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="90b2a-166">Abra el explorador y vaya toohello `METADATA` dirección URL que acaba de actualizar.</span><span class="sxs-lookup"><span data-stu-id="90b2a-166">Open your browser and go toohello `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="90b2a-167">En el Explorador de hello, busque el objeto de "emisor" hello y copie su valor.</span><span class="sxs-lookup"><span data-stu-id="90b2a-167">In hello browser, look for hello 'issuer' object and copy its value.</span></span> <span data-ttu-id="90b2a-168">Debería ser similar a Hola siguiente: `https://sts.windows.net/{tenantId}/`.</span><span class="sxs-lookup"><span data-stu-id="90b2a-168">It should look like hello following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="90b2a-169">Pegue el valor de Hola para `<Item Key="ProviderName">` en el archivo XML de hello.</span><span class="sxs-lookup"><span data-stu-id="90b2a-169">Paste hello value for `<Item Key="ProviderName">` in hello XML file.</span></span>
1. <span data-ttu-id="90b2a-170">Establecer `<Item Key="client_id">` toohello Id. de aplicación de registro de una aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="90b2a-170">Set `<Item Key="client_id">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="90b2a-171">Establecer `<Item Key="IdTokenAudience">` toohello Id. de aplicación de registro de una aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="90b2a-171">Set `<Item Key="IdTokenAudience">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="90b2a-172">Asegúrese de que `<Item Key="response_types">` se establece demasiado`id_token`.</span><span class="sxs-lookup"><span data-stu-id="90b2a-172">Ensure that `<Item Key="response_types">` is set too`id_token`.</span></span>
1. <span data-ttu-id="90b2a-173">Asegúrese de que `<Item Key="UsePolicyInRedirectUri">` se establece demasiado`false`.</span><span class="sxs-lookup"><span data-stu-id="90b2a-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set too`false`.</span></span>

<span data-ttu-id="90b2a-174">También necesita toolink secreto de hello Azure AD que ha registrado en su toohello de inquilino de Azure AD B2C Azure AD `<ClaimsProvider>` información:</span><span class="sxs-lookup"><span data-stu-id="90b2a-174">You also need toolink hello Azure AD secret that you registered in your Azure AD B2C tenant toohello Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="90b2a-175">Hola `<CryptographicKeys>` sección Hola anterior archivo XML, actualice el valor de hello para `StorageReferenceId` toohello el identificador de referencia de secreto de Hola que definiera (por ejemplo, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="90b2a-175">In hello `<CryptographicKeys>` section in hello preceding XML file, update hello value for `StorageReferenceId` toohello reference ID of hello secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="90b2a-176">Cargar archivo de extensión de hello para la comprobación</span><span class="sxs-lookup"><span data-stu-id="90b2a-176">Upload hello extension file for verification</span></span>

<span data-ttu-id="90b2a-177">Hasta ahora, ha configurado la directiva para que Azure AD B2C sepa cómo toocommunicate con su directorio Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90b2a-177">By now, you have configured your policy so that Azure AD B2C knows how toocommunicate with your Azure AD directory.</span></span> <span data-ttu-id="90b2a-178">Intente cargar el archivo de extensión de hello de su tooconfirm simplemente de directiva que no tenga problemas hasta ahora.</span><span class="sxs-lookup"><span data-stu-id="90b2a-178">Try uploading hello extension file of your policy just tooconfirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="90b2a-179">toodo para:</span><span class="sxs-lookup"><span data-stu-id="90b2a-179">toodo so:</span></span>

1. <span data-ttu-id="90b2a-180">Abra hello **todas las directivas** hoja en el inquilino de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="90b2a-180">Open hello **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="90b2a-181">Comprobar hello **sobrescribir directiva Hola si existe** cuadro.</span><span class="sxs-lookup"><span data-stu-id="90b2a-181">Check hello **Overwrite hello policy if it exists** box.</span></span>
1. <span data-ttu-id="90b2a-182">Cargar archivo de extensión de hello (TrustFrameworkExtensions.xml) y asegúrese de que no considerará no válido de Hola.</span><span class="sxs-lookup"><span data-stu-id="90b2a-182">Upload hello extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail hello validation.</span></span>

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a><span data-ttu-id="90b2a-183">Registrar viaje usuario de tooa de proveedor de notificaciones de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="90b2a-183">Register hello Azure AD claims provider tooa user journey</span></span>

<span data-ttu-id="90b2a-184">Ahora debe tooadd hello Azure AD identidad proveedor tooone de los viajes de usuario.</span><span class="sxs-lookup"><span data-stu-id="90b2a-184">You now need tooadd hello Azure AD identity provider tooone of your user journeys.</span></span> <span data-ttu-id="90b2a-185">En este momento, se ha configurado el proveedor de identidades de hello, pero no está disponible en cualquiera de las pantallas de sesión-up/inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="90b2a-185">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="90b2a-186">toomake está disponible, se creará un duplicado de un viaje de usuario de plantilla existente y, a continuación, modificarlo para que también dispone de proveedor de identidades de hello Azure AD:</span><span class="sxs-lookup"><span data-stu-id="90b2a-186">toomake it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has hello Azure AD identity provider:</span></span>

1. <span data-ttu-id="90b2a-187">Abra el archivo de base de hello de la directiva (por ejemplo, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="90b2a-187">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="90b2a-188">Buscar hello `<UserJourneys>` Hola de elemento y copia todo `<UserJourney>` nodo que incluya `Id="SignUpOrSignIn"`.</span><span class="sxs-lookup"><span data-stu-id="90b2a-188">Find hello `<UserJourneys>` element and copy hello entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="90b2a-189">Abra el archivo de extensión de hello (por ejemplo, TrustFrameworkExtensions.xml) y busque hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="90b2a-189">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="90b2a-190">Si no existe el elemento hello, agregue uno.</span><span class="sxs-lookup"><span data-stu-id="90b2a-190">If hello element doesn't exist, add one.</span></span>
1. <span data-ttu-id="90b2a-191">Hola Pegar todo `<UserJourney>` nodo que ha copiado como elemento secundario de hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="90b2a-191">Paste hello entire `<UserJourney>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="90b2a-192">Cambiar el nombre de Id. de Hola de viaje de hello nuevo usuario (por ejemplo, cambiar el nombre como `SignUpOrSignUsingContoso`).</span><span class="sxs-lookup"><span data-stu-id="90b2a-192">Rename hello ID of hello new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="90b2a-193">Hola de presentación "button"</span><span class="sxs-lookup"><span data-stu-id="90b2a-193">Display hello "button"</span></span>

<span data-ttu-id="90b2a-194">Hola `<ClaimsProviderSelection>` elemento es análogo tooan el botón del proveedor de identidad en una pantalla de inicio de sesión-up/inicio de sesión de.</span><span class="sxs-lookup"><span data-stu-id="90b2a-194">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="90b2a-195">Si agrega un `<ClaimsProviderSelection>` elemento para Azure AD, un nuevo botón aparezca cuando llega a un usuario en la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="90b2a-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="90b2a-196">tooadd este elemento:</span><span class="sxs-lookup"><span data-stu-id="90b2a-196">tooadd this element:</span></span>

1. <span data-ttu-id="90b2a-197">Buscar hello `<OrchestrationStep>` nodo que incluya `Order="1"` en viaje de usuario de Hola que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="90b2a-197">Find hello `<OrchestrationStep>` node that includes `Order="1"` in hello user journey that you just created.</span></span>
1. <span data-ttu-id="90b2a-198">Agregue Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="90b2a-198">Add hello following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="90b2a-199">Establecer `TargetClaimsExchangeId` tooan de valor adecuado.</span><span class="sxs-lookup"><span data-stu-id="90b2a-199">Set `TargetClaimsExchangeId` tooan appropriate value.</span></span> <span data-ttu-id="90b2a-200">Se recomienda siguiente Hola misma convención de otras personas:  *\[ClaimProviderName\]Exchange*.</span><span class="sxs-lookup"><span data-stu-id="90b2a-200">We recommend following hello same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="90b2a-201">Acción del botón de vínculo hello tooan</span><span class="sxs-lookup"><span data-stu-id="90b2a-201">Link hello button tooan action</span></span>

<span data-ttu-id="90b2a-202">Ahora que tiene un botón en su lugar, debe toolink tooan acción.</span><span class="sxs-lookup"><span data-stu-id="90b2a-202">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="90b2a-203">acción de Hello, en este caso, es para Azure AD B2C toocommunicate con Azure AD tooreceive un token.</span><span class="sxs-lookup"><span data-stu-id="90b2a-203">hello action, in this case, is for Azure AD B2C toocommunicate with Azure AD tooreceive a token.</span></span> <span data-ttu-id="90b2a-204">Acción de vínculo Hola botón tooan vinculando perfil técnico hello para el proveedor de notificaciones de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="90b2a-204">Link hello button tooan action by linking hello technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="90b2a-205">Buscar hello `<OrchestrationStep>` que incluye `Order="2"` en hello `<UserJourney>` nodo.</span><span class="sxs-lookup"><span data-stu-id="90b2a-205">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
1. <span data-ttu-id="90b2a-206">Agregue Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="90b2a-206">Add hello following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="90b2a-207">Actualización `Id` toohello mismo valor que el de `TargetClaimsExchangeId` Hola sección anterior.</span><span class="sxs-lookup"><span data-stu-id="90b2a-207">Update `Id` toohello same value as that of `TargetClaimsExchangeId` in hello preceding section.</span></span>
1. <span data-ttu-id="90b2a-208">Actualización `TechnicalProfileReferenceId` toohello ID de hello técnica de perfil que creó anteriormente (ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="90b2a-208">Update `TechnicalProfileReferenceId` toohello ID of hello technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="90b2a-209">Cargar archivo de extensión actualizada de hello</span><span class="sxs-lookup"><span data-stu-id="90b2a-209">Upload hello updated extension file</span></span>

<span data-ttu-id="90b2a-210">Ha terminado de modificar el archivo de extensión Hola.</span><span class="sxs-lookup"><span data-stu-id="90b2a-210">You are done modifying hello extension file.</span></span> <span data-ttu-id="90b2a-211">Guarde y</span><span class="sxs-lookup"><span data-stu-id="90b2a-211">Save it.</span></span> <span data-ttu-id="90b2a-212">A continuación, cargar archivo hello y asegúrese de que todas las validaciones se realizan correctamente.</span><span class="sxs-lookup"><span data-stu-id="90b2a-212">Then upload hello file, and ensure that all validations succeed.</span></span>

### <a name="update-hello-rp-file"></a><span data-ttu-id="90b2a-213">Archivo de actualización Hola RP</span><span class="sxs-lookup"><span data-stu-id="90b2a-213">Update hello RP file</span></span>

<span data-ttu-id="90b2a-214">Ahora necesita tooupdate Hola archivo entidad (RP) confianza que se iniciará el proceso de usuario de Hola que acaba de crear:</span><span class="sxs-lookup"><span data-stu-id="90b2a-214">You now need tooupdate hello relying party (RP) file that will initiate hello user journey that you just created:</span></span>

1. <span data-ttu-id="90b2a-215">Realizar una copia de SignUpOrSignIn.xml en el directorio de trabajo y cambie su nombre (por ejemplo, cámbiele el nombre tooSignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="90b2a-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it tooSignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="90b2a-216">Abra Hola Hola nuevo para archivo y actualización de `PolicyId` atributo `<TrustFrameworkPolicy>` con un valor único (por ejemplo, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="90b2a-216">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="90b2a-217">Será Hola nombre de la directiva (por ejemplo, B2C\_1A\_SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="90b2a-217">This will be hello name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="90b2a-218">Modificar hello `ReferenceId` atributo `<DefaultUserJourney>` toomatch Hola ID de viaje Hola de usuario nueva que ha creado (SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="90b2a-218">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello ID of hello new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="90b2a-219">Guardar los cambios y cargar el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="90b2a-219">Save your changes, and upload hello file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="90b2a-220">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="90b2a-220">Troubleshooting</span></span>

<span data-ttu-id="90b2a-221">Probar directiva personalizada de Hola que acaba de cargar abriendo la hoja y haciendo clic **ejecutar ahora**.</span><span class="sxs-lookup"><span data-stu-id="90b2a-221">Test hello custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="90b2a-222">Conozca los problemas de toodiagnose, [solución de problemas de](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="90b2a-222">toodiagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="90b2a-223">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="90b2a-223">Next steps</span></span>

<span data-ttu-id="90b2a-224">Proporcionar comentarios demasiado[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="90b2a-224">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
