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
ms.openlocfilehash: 6c073d70debfdc3560405955d65fa9ccaa7d8b1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="88c25-103">Azure Active Directory B2C: inicio de sesión con cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="88c25-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="88c25-104">En este artículo se muestra cómo habilitar el inicio de sesión de los usuarios de una organización de Azure Active Directory (Azure AD) concreta mediante el uso de [directivas personalizadas](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="88c25-104">This article shows you how to enable sign-in for users from a specific Azure Active Directory (Azure AD) organization through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88c25-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="88c25-105">Prerequisites</span></span>

<span data-ttu-id="88c25-106">Complete los pasos del artículo [Introducción a las directivas personalizadas](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="88c25-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="88c25-107">Estos pasos incluyen:</span><span class="sxs-lookup"><span data-stu-id="88c25-107">These steps include:</span></span>

1. <span data-ttu-id="88c25-108">Creación de un inquilino de Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="88c25-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="88c25-109">Creación de una aplicación de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="88c25-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="88c25-110">Registro de dos aplicaciones de motor de directivas.</span><span class="sxs-lookup"><span data-stu-id="88c25-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="88c25-111">Configuración de claves.</span><span class="sxs-lookup"><span data-stu-id="88c25-111">Setting up keys.</span></span>
5. <span data-ttu-id="88c25-112">Configurar el paquete de inicio.</span><span class="sxs-lookup"><span data-stu-id="88c25-112">Setting up the starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="88c25-113">Creación de una aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="88c25-113">Create an Azure AD app</span></span>

<span data-ttu-id="88c25-114">Para habilitar el inicio de sesión para los usuarios de una organización específica de Azure AD, es preciso registrar una aplicación en el inquilino de Azure AD de la organización.</span><span class="sxs-lookup"><span data-stu-id="88c25-114">To enable sign-in for users from a specific Azure AD organization, you need to register an application within the organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="88c25-115">En las instrucciones siguientes, usamos "contoso.com" para el inquilino de Azure AD de la organización y "fabrikamb2c.onmicrosoft.com" como inquilino de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="88c25-115">We use "contoso.com" for the organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as the Azure AD B2C tenant in the following instructions.</span></span>

1. <span data-ttu-id="88c25-116">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="88c25-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="88c25-117">En la barra superior, seleccione su cuenta.</span><span class="sxs-lookup"><span data-stu-id="88c25-117">On the top bar, select your account.</span></span> <span data-ttu-id="88c25-118">En la lista **Directorio**, elija el inquilino de Azure AD de la organización donde quiere registrar la aplicación (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="88c25-118">From the **Directory** list, choose the organizational Azure AD tenant where you want to register your application (contoso.com).</span></span>
1. <span data-ttu-id="88c25-119">Seleccione **Más servicios** en el panel izquierdo y busque "Registros de aplicaciones".</span><span class="sxs-lookup"><span data-stu-id="88c25-119">Select **More services** in the left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="88c25-120">Seleccione **Nuevo registro de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="88c25-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="88c25-121">Escriba el nombre de la aplicación (por ejemplo, `Azure AD B2C App`).</span><span class="sxs-lookup"><span data-stu-id="88c25-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="88c25-122">En Tipo de aplicación, seleccione **Aplicación web o API**.</span><span class="sxs-lookup"><span data-stu-id="88c25-122">Select **Web app / API** for the application type.</span></span>
1. <span data-ttu-id="88c25-123">En **Dirección URL de inicio de sesión**, escriba la dirección URL siguiente, donde `yourtenant` se sustituye por el nombre del inquilino de Azure AD B2C (`fabrikamb2c.onmicrosoft.com`):</span><span class="sxs-lookup"><span data-stu-id="88c25-123">For **Sign-on URL**, enter the following URL, where `yourtenant` is replaced by the name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="88c25-124">Guarde el identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="88c25-124">Save the application ID.</span></span>
1. <span data-ttu-id="88c25-125">Seleccione la aplicación recién creada.</span><span class="sxs-lookup"><span data-stu-id="88c25-125">Select the newly created application.</span></span>
1. <span data-ttu-id="88c25-126">En la hoja **Configuración**, seleccione **Claves**.</span><span class="sxs-lookup"><span data-stu-id="88c25-126">Under the **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="88c25-127">Cree una clave y guárdela.</span><span class="sxs-lookup"><span data-stu-id="88c25-127">Create a new key, and save it.</span></span> <span data-ttu-id="88c25-128">La usará en los pasos de la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="88c25-128">You will use it in the steps in the next section.</span></span>

## <a name="add-the-azure-ad-key-to-azure-ad-b2c"></a><span data-ttu-id="88c25-129">Adición de la clave de Azure AD a Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="88c25-129">Add the Azure AD key to Azure AD B2C</span></span>

<span data-ttu-id="88c25-130">Debe almacenar la clave de aplicación contoso.com en su inquilino de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="88c25-130">You need to store the contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="88c25-131">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="88c25-131">To do this:</span></span>
1. <span data-ttu-id="88c25-132">Vaya a su inquilino de Azure AD B2C y abra **B2C Settings (Configuración de B2C)** > **Marco de experiencia de identidad** > **Claves de directiva**.</span><span class="sxs-lookup"><span data-stu-id="88c25-132">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="88c25-133">Seleccione **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="88c25-133">Select **+Add**.</span></span>
1. <span data-ttu-id="88c25-134">Seleccione o especifique estas opciones:</span><span class="sxs-lookup"><span data-stu-id="88c25-134">Select or enter these options:</span></span>
   * <span data-ttu-id="88c25-135">Seleccione **Manual**.</span><span class="sxs-lookup"><span data-stu-id="88c25-135">Select **Manual**.</span></span>
   * <span data-ttu-id="88c25-136">En **Nombre**, elija un nombre que coincida con el nombre del inquilino de Azure AD (por ejemplo, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="88c25-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="88c25-137">Se agregará el prefijo `B2C_1A_` automáticamente al nombre de la clave.</span><span class="sxs-lookup"><span data-stu-id="88c25-137">The prefix `B2C_1A_` is added automatically to the name of your key.</span></span>
   * <span data-ttu-id="88c25-138">Pegue la clave de la aplicación en el cuadro **Secreto**.</span><span class="sxs-lookup"><span data-stu-id="88c25-138">Paste your application key in the **Secret** box.</span></span>
   * <span data-ttu-id="88c25-139">Seleccione **Firma**.</span><span class="sxs-lookup"><span data-stu-id="88c25-139">Select **Signature**.</span></span>
1. <span data-ttu-id="88c25-140">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="88c25-140">Select **Create**.</span></span>
1. <span data-ttu-id="88c25-141">Confirme que ha creado la clave `B2C_1A_ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="88c25-141">Confirm that you've created the key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="88c25-142">Adición de un proveedor de notificaciones a una directiva de base</span><span class="sxs-lookup"><span data-stu-id="88c25-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="88c25-143">Si quiere que los usuarios inicien sesión con Azure AD, es preciso definir Azure AD como proveedor de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="88c25-143">If you want users to sign in by using Azure AD, you need to define Azure AD as a claims provider.</span></span> <span data-ttu-id="88c25-144">En otras palabras, se debe especificar el punto de conexión con el que Azure AD B2C se va a comunicar.</span><span class="sxs-lookup"><span data-stu-id="88c25-144">In other words, you need to specify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="88c25-145">El punto de conexión proporcionará un conjunto de notificaciones que Azure AD B2C usa para comprobar que un usuario concreto se ha autenticado.</span><span class="sxs-lookup"><span data-stu-id="88c25-145">The endpoint will provide a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span> 

<span data-ttu-id="88c25-146">Puede definir Azure AD como proveedor de notificaciones. Para ello, agregue Azure AD al nodo `<ClaimsProvider>` en el archivo de extensión de la directiva:</span><span class="sxs-lookup"><span data-stu-id="88c25-146">You can define Azure AD as a claims provider by adding Azure AD to the `<ClaimsProvider>` node in the extension file of your policy:</span></span>

1. <span data-ttu-id="88c25-147">Abra el archivo de extensión (TrustFrameworkExtensions.xml) desde el directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="88c25-147">Open the extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="88c25-148">Busque la sección `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="88c25-148">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="88c25-149">Si no existe, agréguela debajo del nodo raíz.</span><span class="sxs-lookup"><span data-stu-id="88c25-149">If it does not exist, add it under the root node.</span></span>
1. <span data-ttu-id="88c25-150">Agregue un nuevo nodo `<ClaimsProvider>` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="88c25-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

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

1. <span data-ttu-id="88c25-151">En el nodo `<ClaimsProvider>`, actualice el valor de `<Domain>` a un valor único que pueda usarse para distinguirlo de otros proveedores de identidades.</span><span class="sxs-lookup"><span data-stu-id="88c25-151">Under the `<ClaimsProvider>` node, update the value for `<Domain>` to a unique value that can be used to distinguish it from other identity providers.</span></span>
1. <span data-ttu-id="88c25-152">En el nodo `<ClaimsProvider>`, actualice el valor de `<DisplayName>` a un nombre descriptivo del proveedor de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="88c25-152">Under the `<ClaimsProvider>` node, update the value for `<DisplayName>` to a friendly name for the claims provider.</span></span> <span data-ttu-id="88c25-153">Este valor no se utiliza actualmente.</span><span class="sxs-lookup"><span data-stu-id="88c25-153">This value is not currently used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="88c25-154">Actualización del perfil técnico</span><span class="sxs-lookup"><span data-stu-id="88c25-154">Update the technical profile</span></span>

<span data-ttu-id="88c25-155">Para obtener un token del punto de conexión de Azure AD es preciso definir los protocolos que Azure AD B2C debe usar para comunicarse con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88c25-155">To get a token from the Azure AD endpoint, you need to define the protocols that Azure AD B2C should use to communicate with Azure AD.</span></span> <span data-ttu-id="88c25-156">Esto se hace dentro del elemento `<TechnicalProfile>` de `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="88c25-156">This is done inside the `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="88c25-157">Actualice el identificador del nodo `<TechnicalProfile>`.</span><span class="sxs-lookup"><span data-stu-id="88c25-157">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="88c25-158">Este identificador se usa para hacer referencia a este perfil técnico desde otras partes de la directiva.</span><span class="sxs-lookup"><span data-stu-id="88c25-158">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
1. <span data-ttu-id="88c25-159">Actualice el valor de `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="88c25-159">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="88c25-160">Este valor se mostrará en el botón de inicio de sesión de la pantalla de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="88c25-160">This value will be displayed on the sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="88c25-161">Actualice el valor de `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="88c25-161">Update the value for `<Description>`.</span></span>
1. <span data-ttu-id="88c25-162">Azure AD usa el protocolo OpenID Connect, por lo que debe asegurarse de que el valor de `<Protocol>` es `"OpenIdConnect"`.</span><span class="sxs-lookup"><span data-stu-id="88c25-162">Azure AD uses the OpenID Connect protocol, so ensure that the value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="88c25-163">Debe actualizar la sección `<Metadata>` del archivo XML al que se ha hecho referencia anteriormente para reflejar la configuración de su inquilino de Azure AD específico.</span><span class="sxs-lookup"><span data-stu-id="88c25-163">You need to update the `<Metadata>` section in the XML file referred to earlier to reflect the configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="88c25-164">En el archivo XML, actualice los valores de los metadatos como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="88c25-164">In the XML file, update the metadata values as follows:</span></span>

1. <span data-ttu-id="88c25-165">Establezca `<Item Key="METADATA">` en `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, donde `yourAzureADtenant` es el nombre del inquilino de Azure AD (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="88c25-165">Set `<Item Key="METADATA">` to `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="88c25-166">Abra el explorador y vaya a la dirección URL `METADATA` que acaba de actualizar.</span><span class="sxs-lookup"><span data-stu-id="88c25-166">Open your browser and go to the `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="88c25-167">En el explorador, busque el objeto "issuer" y copie su valor.</span><span class="sxs-lookup"><span data-stu-id="88c25-167">In the browser, look for the 'issuer' object and copy its value.</span></span> <span data-ttu-id="88c25-168">Debería ser similar a lo siguiente: `https://sts.windows.net/{tenantId}/`.</span><span class="sxs-lookup"><span data-stu-id="88c25-168">It should look like the following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="88c25-169">Pegue el valor de `<Item Key="ProviderName">` en el archivo XML.</span><span class="sxs-lookup"><span data-stu-id="88c25-169">Paste the value for `<Item Key="ProviderName">` in the XML file.</span></span>
1. <span data-ttu-id="88c25-170">Establezca `<Item Key="client_id">` en el identificador de aplicación desde el registro de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="88c25-170">Set `<Item Key="client_id">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="88c25-171">Establezca `<Item Key="IdTokenAudience">` en el identificador de aplicación desde el registro de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="88c25-171">Set `<Item Key="IdTokenAudience">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="88c25-172">Asegúrese de que `<Item Key="response_types">` está establecido en `id_token`.</span><span class="sxs-lookup"><span data-stu-id="88c25-172">Ensure that `<Item Key="response_types">` is set to `id_token`.</span></span>
1. <span data-ttu-id="88c25-173">Asegúrese de que `<Item Key="UsePolicyInRedirectUri">` está establecido en `false`.</span><span class="sxs-lookup"><span data-stu-id="88c25-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set to `false`.</span></span>

<span data-ttu-id="88c25-174">También es preciso que vincule el secreto de Azure AD que ha registrado en el inquilino de Azure AD B2C a la información de `<ClaimsProvider>` de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="88c25-174">You also need to link the Azure AD secret that you registered in your Azure AD B2C tenant to the Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="88c25-175">En la sección `<CryptographicKeys>` del archivo XML anterior, actualice el valor de `StorageReferenceId` al identificador de referencia del secreto que ha definido (por ejemplo, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="88c25-175">In the `<CryptographicKeys>` section in the preceding XML file, update the value for `StorageReferenceId` to the reference ID of the secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="88c25-176">Carga del archivo de extensión para su comprobación</span><span class="sxs-lookup"><span data-stu-id="88c25-176">Upload the extension file for verification</span></span>

<span data-ttu-id="88c25-177">Por el momento, ha configurado la directiva para que Azure AD B2C sepa cómo comunicarse con su directorio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88c25-177">By now, you have configured your policy so that Azure AD B2C knows how to communicate with your Azure AD directory.</span></span> <span data-ttu-id="88c25-178">Pruebe a cargar el archivo de extensión de la directiva para confirmar que no tiene problemas.</span><span class="sxs-lookup"><span data-stu-id="88c25-178">Try uploading the extension file of your policy just to confirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="88c25-179">Para ello:</span><span class="sxs-lookup"><span data-stu-id="88c25-179">To do so:</span></span>

1. <span data-ttu-id="88c25-180">Vaya a la hoja **Todas las directivas** en el inquilino de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="88c25-180">Open the **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="88c25-181">Active la casilla **Sobrescribir la directiva si existe**.</span><span class="sxs-lookup"><span data-stu-id="88c25-181">Check the **Overwrite the policy if it exists** box.</span></span>
1. <span data-ttu-id="88c25-182">Cargue el archivo de extensión (TrustFrameworkExtensions.xml) y asegúrese de que no se produce ningún error en la validación.</span><span class="sxs-lookup"><span data-stu-id="88c25-182">Upload the extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail the validation.</span></span>

## <a name="register-the-azure-ad-claims-provider-to-a-user-journey"></a><span data-ttu-id="88c25-183">Registrar el proveedor de notificaciones de Azure AD en un recorrido del usuario</span><span class="sxs-lookup"><span data-stu-id="88c25-183">Register the Azure AD claims provider to a user journey</span></span>

<span data-ttu-id="88c25-184">Ahora es preciso agregar el proveedor de identidades de Azure AD a uno de los recorridos del usuario.</span><span class="sxs-lookup"><span data-stu-id="88c25-184">You now need to add the Azure AD identity provider to one of your user journeys.</span></span> <span data-ttu-id="88c25-185">El proveedor de identidades ya se ha configurado, pero no está disponible en ninguna de las pantallas de registro/inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="88c25-185">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="88c25-186">Para que esté disponible, crearemos un duplicado de un recorrido del usuario de plantilla existente y, después, lo modificaremos para que también tenga el proveedor de identidades de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="88c25-186">To make it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has the Azure AD identity provider:</span></span>

1. <span data-ttu-id="88c25-187">Abra el archivo base de la directiva (por ejemplo, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="88c25-187">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="88c25-188">Busque el elemento `<UserJourneys>` y copie todo el nodo `<UserJourney>` que incluye `Id="SignUpOrSignIn"`.</span><span class="sxs-lookup"><span data-stu-id="88c25-188">Find the `<UserJourneys>` element and copy the entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="88c25-189">Abra el archivo de extensión (por ejemplo, TrustFrameworkExtensions.xml) y busque el elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="88c25-189">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="88c25-190">Si el elemento no existe, agréguelo.</span><span class="sxs-lookup"><span data-stu-id="88c25-190">If the element doesn't exist, add one.</span></span>
1. <span data-ttu-id="88c25-191">Pegue todo el nodo `<UserJourney>` que ha copiado como elemento secundario de `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="88c25-191">Paste the entire `<UserJourney>` node that you copied as a child of the `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="88c25-192">Cambie el nombre del identificador del nuevo recorrido del usuario (por ejemplo, cambie el nombre a `SignUpOrSignUsingContoso`).</span><span class="sxs-lookup"><span data-stu-id="88c25-192">Rename the ID of the new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-the-button"></a><span data-ttu-id="88c25-193">Incorporación del "botón"</span><span class="sxs-lookup"><span data-stu-id="88c25-193">Display the "button"</span></span>

<span data-ttu-id="88c25-194">El elemento `<ClaimsProviderSelection>` es análogo a un botón del proveedor de identidades en una pantalla de registro o inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="88c25-194">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="88c25-195">Si agrega un elemento `<ClaimsProviderSelection>` para Azure AD, se mostrará un botón nuevo cuando un usuario llega a la página.</span><span class="sxs-lookup"><span data-stu-id="88c25-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="88c25-196">Para agregar este elemento:</span><span class="sxs-lookup"><span data-stu-id="88c25-196">To add this element:</span></span>

1. <span data-ttu-id="88c25-197">Busque el nodo `<OrchestrationStep>` que incluye `Order="1"` en el recorrido del usuario que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="88c25-197">Find the `<OrchestrationStep>` node that includes `Order="1"` in the user journey that you just created.</span></span>
1. <span data-ttu-id="88c25-198">Agregue la siguiente línea de código:</span><span class="sxs-lookup"><span data-stu-id="88c25-198">Add the following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="88c25-199">Establezca `TargetClaimsExchangeId` en valor apropiado.</span><span class="sxs-lookup"><span data-stu-id="88c25-199">Set `TargetClaimsExchangeId` to an appropriate value.</span></span> <span data-ttu-id="88c25-200">Se recomienda seguir la misma convención que otros:  *\[ClaimProviderName\]Exchange*.</span><span class="sxs-lookup"><span data-stu-id="88c25-200">We recommend following the same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="88c25-201">Vincular el botón a una acción</span><span class="sxs-lookup"><span data-stu-id="88c25-201">Link the button to an action</span></span>

<span data-ttu-id="88c25-202">Ahora que hay un botón colocado, es preciso vincularlo a una acción.</span><span class="sxs-lookup"><span data-stu-id="88c25-202">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="88c25-203">En este caso, la acción es para que Azure AD B2C se comunique con Azure AD para recibir un token.</span><span class="sxs-lookup"><span data-stu-id="88c25-203">The action, in this case, is for Azure AD B2C to communicate with Azure AD to receive a token.</span></span> <span data-ttu-id="88c25-204">Para vincular un botón a una acción, vincule el perfil técnico del proveedor de notificaciones de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="88c25-204">Link the button to an action by linking the technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="88c25-205">Busque el nodo `<OrchestrationStep>` que incluye `Order="2"` en el nodo `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="88c25-205">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
1. <span data-ttu-id="88c25-206">Agregue la siguiente línea de código:</span><span class="sxs-lookup"><span data-stu-id="88c25-206">Add the following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="88c25-207">Actualice `Id` con el mismo valor que el de `TargetClaimsExchangeId` en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="88c25-207">Update `Id` to the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
1. <span data-ttu-id="88c25-208">Actualice `TechnicalProfileReferenceId` con el identificador del perfil técnico que ha creado anteriormente (ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="88c25-208">Update `TechnicalProfileReferenceId` to the ID of the technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="88c25-209">Cargar el archivo de extensión actualizado</span><span class="sxs-lookup"><span data-stu-id="88c25-209">Upload the updated extension file</span></span>

<span data-ttu-id="88c25-210">Ya ha terminado la modificación del archivo de extensión.</span><span class="sxs-lookup"><span data-stu-id="88c25-210">You are done modifying the extension file.</span></span> <span data-ttu-id="88c25-211">Guarde y</span><span class="sxs-lookup"><span data-stu-id="88c25-211">Save it.</span></span> <span data-ttu-id="88c25-212">cargue el archivo y asegúrese de que el resultado de todas las validaciones es satisfactorio.</span><span class="sxs-lookup"><span data-stu-id="88c25-212">Then upload the file, and ensure that all validations succeed.</span></span>

### <a name="update-the-rp-file"></a><span data-ttu-id="88c25-213">Actualización del archivo de RP</span><span class="sxs-lookup"><span data-stu-id="88c25-213">Update the RP file</span></span>

<span data-ttu-id="88c25-214">Ahora es preciso actualizar el archivo del usuario de confianza (RP) que iniciará el recorrido del usuario que acaba de crear:</span><span class="sxs-lookup"><span data-stu-id="88c25-214">You now need to update the relying party (RP) file that will initiate the user journey that you just created:</span></span>

1. <span data-ttu-id="88c25-215">Realice una copia de SignUpOrSignIn.xml en el directorio de trabajo y cambie su nombre (por ejemplo, SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="88c25-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it to SignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="88c25-216">Abra el archivo nuevo y actualice el atributo `PolicyId` de `<TrustFrameworkPolicy>` con un valor único (por ejemplo, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="88c25-216">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="88c25-217">Este será el nombre de la directiva (por ejemplo, B2C\_1A\_SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="88c25-217">This will be the name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="88c25-218">Modifique el atributo `ReferenceId` de `<DefaultUserJourney>` para que coincida con el identificador del nuevo recorrido del usuario que ha creado (SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="88c25-218">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the ID of the new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="88c25-219">Guarde los cambios y cargue el archivo.</span><span class="sxs-lookup"><span data-stu-id="88c25-219">Save your changes, and upload the file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="88c25-220">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="88c25-220">Troubleshooting</span></span>

<span data-ttu-id="88c25-221">Pruebe la directiva personalizada que acaba de cargar. Para ello, abra su hoja y haga clic en **Ejecutar ahora**.</span><span class="sxs-lookup"><span data-stu-id="88c25-221">Test the custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="88c25-222">Para diagnosticar problemas, obtenga información sobre la [solución de problemas](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="88c25-222">To diagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="88c25-223">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="88c25-223">Next steps</span></span>

<span data-ttu-id="88c25-224">Envíe sus comentarios a [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="88c25-224">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
