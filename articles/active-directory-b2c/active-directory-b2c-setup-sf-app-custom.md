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
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="ff568-103">Azure Active Directory B2C: inicio de sesión mediante cuentas de Salesforce a través de SAML</span><span class="sxs-lookup"><span data-stu-id="ff568-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="ff568-104">Este artículo muestra cómo toouse [directivas personalizadas](active-directory-b2c-overview-custom.md) tooset una sesión para los usuarios de una organización de Salesforce específica.</span><span class="sxs-lookup"><span data-stu-id="ff568-104">This article shows you how toouse [custom policies](active-directory-b2c-overview-custom.md) tooset up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff568-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ff568-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="ff568-106">Configuración de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="ff568-106">Azure AD B2C setup</span></span>

<span data-ttu-id="ff568-107">Asegúrese de que ha completado todos los pasos de Hola que le muestran cómo demasiado[empezar a trabajar con las directivas personalizadas](active-directory-b2c-get-started-custom.md) en Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="ff568-107">Ensure that you have completed all of hello steps that show you how too[get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="ff568-108">Entre ellos se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="ff568-108">These include:</span></span>

* <span data-ttu-id="ff568-109">Crear un inquilino de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ff568-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="ff568-110">Crear una aplicación de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ff568-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="ff568-111">Registrar dos aplicaciones de motor de directivas.</span><span class="sxs-lookup"><span data-stu-id="ff568-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="ff568-112">Configurar las claves.</span><span class="sxs-lookup"><span data-stu-id="ff568-112">Set up keys.</span></span>
* <span data-ttu-id="ff568-113">Configurar el módulo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff568-113">Set up hello starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="ff568-114">Configuración de Salesforce</span><span class="sxs-lookup"><span data-stu-id="ff568-114">Salesforce setup</span></span>

<span data-ttu-id="ff568-115">En este artículo, se supone que ya ha hecho siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="ff568-115">In this article, we assume that you have already done hello following:</span></span>

* <span data-ttu-id="ff568-116">Se ha registrado para obtener una cuenta de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ff568-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="ff568-117">Puede registrarse para [una cuenta gratuita de Developer Edition](https://developer.salesforce.com/signup).</span><span class="sxs-lookup"><span data-stu-id="ff568-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="ff568-118">[Ha configurado un Mi dominio](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) para su organización de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ff568-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="ff568-119">Configurar Salesforce, para que los usuarios se puedan federar</span><span class="sxs-lookup"><span data-stu-id="ff568-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="ff568-120">toohelp Azure AD B2C comunicarse con Salesforce, deberá tooget Hola dirección URL de metadatos de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ff568-120">toohelp Azure AD B2C communicate with Salesforce, you need tooget hello Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="ff568-121">Configurar Salesforce como proveedor de identidades</span><span class="sxs-lookup"><span data-stu-id="ff568-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="ff568-122">En este artículo, se supone que usa [Lightning Experience de Salesforce](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span><span class="sxs-lookup"><span data-stu-id="ff568-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="ff568-123">[Inicie sesión en tooSalesforce](https://login.salesforce.com/).</span><span class="sxs-lookup"><span data-stu-id="ff568-123">[Sign in tooSalesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="ff568-124">En hello izquierda menú, en **configuración**, expanda **identidad**y, a continuación, haga clic en **proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="ff568-124">On hello left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="ff568-125">Haga clic en **Enable Identity Provider** (Habilitar proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="ff568-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="ff568-126">En **certificado Hola seleccione**, seleccione certificado Hola desea Salesforce toouse toocommunicate con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ff568-126">Under **Select hello certificate**, select hello certificate you want Salesforce toouse toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="ff568-127">(Puede usar certificado predeterminado de hello). Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ff568-127">(You can use hello default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="ff568-128">Crear una aplicación conectada en Salesforce</span><span class="sxs-lookup"><span data-stu-id="ff568-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="ff568-129">En hello **proveedor de identidades** página, vaya demasiado**proveedores de servicios**.</span><span class="sxs-lookup"><span data-stu-id="ff568-129">On hello **Identity Provider** page, go too**Service Providers**.</span></span>
2. <span data-ttu-id="ff568-130">Haga clic en **Service Providers are now created via Connected Apps (Los proveedores de servicios se crean ahora a través de aplicaciones conectadas). Haga clic aquí.**</span><span class="sxs-lookup"><span data-stu-id="ff568-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="ff568-131">En **información básica**, especifique valores de hello necesario para la aplicación conectada.</span><span class="sxs-lookup"><span data-stu-id="ff568-131">Under **Basic Information**,  enter hello required values for your connected app.</span></span>
4. <span data-ttu-id="ff568-132">En **configuración de aplicación Web**, seleccione hello **habilitar SAML** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="ff568-132">Under **Web App Settings**, select hello **Enable SAML** check box.</span></span>
5. <span data-ttu-id="ff568-133">Hola **Id. de entidad** , escriba Hola después de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="ff568-133">In hello **Entity ID** field, enter hello following URL.</span></span> <span data-ttu-id="ff568-134">Asegúrese de reemplazar el valor de hello para `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="ff568-134">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="ff568-135">Hola **dirección URL de ACS** , escriba Hola después de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="ff568-135">In hello **ACS URL** field, enter hello following URL.</span></span> <span data-ttu-id="ff568-136">Asegúrese de reemplazar el valor de hello para `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="ff568-136">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="ff568-137">Deje los valores predeterminados de Hola para todas las demás opciones.</span><span class="sxs-lookup"><span data-stu-id="ff568-137">Leave hello default values for all other settings.</span></span>
8. <span data-ttu-id="ff568-138">Desplácese toohello inferior de la lista de hello y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="ff568-138">Scroll toohello bottom of hello list, and then click **Save**.</span></span>

### <a name="get-hello-metadata-url"></a><span data-ttu-id="ff568-139">Obtener dirección URL de metadatos de Hola</span><span class="sxs-lookup"><span data-stu-id="ff568-139">Get hello metadata URL</span></span>

1. <span data-ttu-id="ff568-140">En la página de información general de saludo de la aplicación conectada, haga clic en **administrar**.</span><span class="sxs-lookup"><span data-stu-id="ff568-140">On hello overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="ff568-141">Copiar valor de Hola para **extremo de detección de metadatos**y, a continuación, guárdelo.</span><span class="sxs-lookup"><span data-stu-id="ff568-141">Copy hello value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="ff568-142">Lo usará más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="ff568-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-toofederate"></a><span data-ttu-id="ff568-143">Configurar toofederate de los usuarios de Salesforce</span><span class="sxs-lookup"><span data-stu-id="ff568-143">Set up Salesforce users toofederate</span></span>

1. <span data-ttu-id="ff568-144">En hello **administrar** página de la aplicación conectada, vaya demasiado**perfiles**.</span><span class="sxs-lookup"><span data-stu-id="ff568-144">On hello **Manage** page of your connected app, go too**Profiles**.</span></span>
2. <span data-ttu-id="ff568-145">Haga clic en **Administrar perfiles**.</span><span class="sxs-lookup"><span data-stu-id="ff568-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="ff568-146">Seleccione los perfiles de hello (o grupos de usuarios) que desea toofederate con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ff568-146">Select hello profiles (or groups of users) that you want toofederate with Azure AD B2C.</span></span> <span data-ttu-id="ff568-147">Como administrador del sistema, seleccione hello **administrador del sistema** casilla para que pueda federarse con su cuenta de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ff568-147">As a system administrator, select hello **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="ff568-148">Generar un certificado de firma para Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="ff568-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="ff568-149">Las solicitudes envían tooSalesforce necesidad toobe firmado por Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ff568-149">Requests sent tooSalesforce need toobe signed by Azure AD B2C.</span></span> <span data-ttu-id="ff568-150">toogenerate un certificado de firma, abra PowerShell de Azure y, a continuación, ejecute hello siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="ff568-150">toogenerate a signing certificate, open Azure PowerShell, and then run hello following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="ff568-151">Asegúrese de que actualice el nombre del inquilino de Hola y una contraseña en dos líneas de superior Hola.</span><span class="sxs-lookup"><span data-stu-id="ff568-151">Make sure that you update hello tenant name and password in hello top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a><span data-ttu-id="ff568-152">Agregar tooAzure certificado firma Hola SAML AD B2C</span><span class="sxs-lookup"><span data-stu-id="ff568-152">Add hello SAML signing certificate tooAzure AD B2C</span></span>

<span data-ttu-id="ff568-153">Cargar Hola inquilino de Azure AD B2C tooyour de certificado de firma:</span><span class="sxs-lookup"><span data-stu-id="ff568-153">Upload hello signing certificate tooyour Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="ff568-154">Vaya el inquilino de Azure AD B2C tooyour.</span><span class="sxs-lookup"><span data-stu-id="ff568-154">Go tooyour Azure AD B2C tenant.</span></span> <span data-ttu-id="ff568-155">Haga clic en **Configuración** > **Marco de experiencia de identidad** > **Claves de directiva**.</span><span class="sxs-lookup"><span data-stu-id="ff568-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="ff568-156">Haga clic en **+Agregar** y después:</span><span class="sxs-lookup"><span data-stu-id="ff568-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="ff568-157">Haga clic en **Opciones** > **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="ff568-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="ff568-158">Escriba un **nombre** (por ejemplo, SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="ff568-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="ff568-159">prefijo de Hello *B2C_1A_* se agrega automáticamente el nombre de toohello de la clave.</span><span class="sxs-lookup"><span data-stu-id="ff568-159">hello prefix *B2C_1A_* is automatically added toohello name of your key.</span></span>
    3. <span data-ttu-id="ff568-160">tooselect su certificado, seleccione **control del archivo de carga**.</span><span class="sxs-lookup"><span data-stu-id="ff568-160">tooselect your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="ff568-161">Escribir contraseña del certificado de hello configuradas en el script de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff568-161">Enter hello certificate's password that you set in hello PowerShell script.</span></span>
3. <span data-ttu-id="ff568-162">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ff568-162">Click **Create**.</span></span>
4. <span data-ttu-id="ff568-163">Compruebe que ha creado una clave (por ejemplo, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="ff568-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="ff568-164">Tome nota del nombre completo de hello (incluidos *B2C_1A_*).</span><span class="sxs-lookup"><span data-stu-id="ff568-164">Take note of hello full name (including *B2C_1A_*).</span></span> <span data-ttu-id="ff568-165">Hará referencia toothis clave más adelante en la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff568-165">You will refer toothis key later in hello policy.</span></span>

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="ff568-166">Crear proveedor de notificaciones de Salesforce SAML hello en la directiva de base</span><span class="sxs-lookup"><span data-stu-id="ff568-166">Create hello Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="ff568-167">Necesita toodefine Salesforce como un proveedor de notificaciones para que los usuarios puedan iniciar sesión mediante el uso de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ff568-167">You need toodefine Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="ff568-168">En otras palabras, necesita extremo de hello toospecify que se puede comunicar con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ff568-168">In other words, you need toospecify hello endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="ff568-169">punto de conexión de Hello le *proporcionar* un conjunto de *notificaciones* que Azure AD B2C usa tooverify que ha autenticado un usuario específico.</span><span class="sxs-lookup"><span data-stu-id="ff568-169">hello endpoint will *provide* a set of *claims* that Azure AD B2C uses tooverify that a specific user has authenticated.</span></span> <span data-ttu-id="ff568-170">toodo esto, agregue un `<ClaimsProvider>` de Salesforce en el archivo de extensión de hello de la directiva:</span><span class="sxs-lookup"><span data-stu-id="ff568-170">toodo this, add a `<ClaimsProvider>` for Salesforce in hello extension file of your policy:</span></span>

1. <span data-ttu-id="ff568-171">En el directorio de trabajo, abra el archivo de extensión de hello (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="ff568-171">In your working directory, open hello extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="ff568-172">Buscar hello `<ClaimsProviders>` sección.</span><span class="sxs-lookup"><span data-stu-id="ff568-172">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="ff568-173">Si no existe, créela en el nodo raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff568-173">If it does not exist, create it under hello root node.</span></span>
3. <span data-ttu-id="ff568-174">Agregar un nuevo `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="ff568-174">Add a new `<ClaimsProvider>`:</span></span>

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

<span data-ttu-id="ff568-175">En hello `<ClaimsProvider>` nodo:</span><span class="sxs-lookup"><span data-stu-id="ff568-175">Under hello `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="ff568-176">Cambiar el valor de Hola para `<Domain>` tooa valor exclusivo que distingue `<ClaimsProvider>` de otros proveedores de identidad.</span><span class="sxs-lookup"><span data-stu-id="ff568-176">Change hello value for `<Domain>` tooa unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="ff568-177">Actualizar el valor de Hola para `<DisplayName>` tooa nombre para mostrar para hello proveedor de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="ff568-177">Update hello value for `<DisplayName>` tooa display name for hello claims provider.</span></span> <span data-ttu-id="ff568-178">Actualmente este valor no se usa.</span><span class="sxs-lookup"><span data-stu-id="ff568-178">Currently, this value is not used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="ff568-179">Actualizar perfil técnica Hola</span><span class="sxs-lookup"><span data-stu-id="ff568-179">Update hello technical profile</span></span>

<span data-ttu-id="ff568-180">tooget un token de SAML de Salesforce, definir los protocolos de Hola que Azure AD B2C utilizará toocommunicate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ff568-180">tooget a SAML token from Salesforce, define hello protocols that Azure AD B2C will use toocommunicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ff568-181">Hacer esto en hello `<TechnicalProfile>` elemento de `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="ff568-181">Do this in hello `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="ff568-182">Actualizar el Id. de Hola de hello `<TechnicalProfile>` nodo.</span><span class="sxs-lookup"><span data-stu-id="ff568-182">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="ff568-183">Este identificador es toothis toorefer usado perfil técnica de otras partes de la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff568-183">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
2. <span data-ttu-id="ff568-184">Actualizar el valor de Hola para `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="ff568-184">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="ff568-185">Este valor se muestra en el botón de inicio de sesión de hello en la página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="ff568-185">This value is displayed on hello sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="ff568-186">Actualizar el valor de Hola para `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="ff568-186">Update hello value for `<Description>`.</span></span>
4. <span data-ttu-id="ff568-187">Salesforce utiliza el protocolo de hello SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="ff568-187">Salesforce uses hello SAML 2.0 protocol.</span></span> <span data-ttu-id="ff568-188">Asegúrese de que el valor de hello `<Protocol>` es **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="ff568-188">Ensure that hello value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="ff568-189">Hola de actualización `<Metadata>` sección Hola anterior configuración de hello tooreflect XML para su cuenta de Salesforce específica.</span><span class="sxs-lookup"><span data-stu-id="ff568-189">Update hello `<Metadata>` section in hello preceding XML tooreflect hello settings for your specific Salesforce account.</span></span> <span data-ttu-id="ff568-190">Hola XML, actualice los valores de metadatos de hello:</span><span class="sxs-lookup"><span data-stu-id="ff568-190">In hello XML, update hello metadata values:</span></span>

1. <span data-ttu-id="ff568-191">Actualizar el valor de Hola de `<Item Key="PartnerEntity">` con la dirección URL de metadatos de Salesforce Hola que copió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ff568-191">Update hello value of `<Item Key="PartnerEntity">` with hello Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="ff568-192">Tiene Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="ff568-192">It has hello following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="ff568-193">Hola `<CryptographicKeys>` sección actualización Hola valor para ambas instancias de `StorageReferenceId` toohello nombre de clave de hello el certificado de firma (por ejemplo, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="ff568-193">In hello `<CryptographicKeys>` section, update hello value for both instances of `StorageReferenceId` toohello name of hello key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="ff568-194">Cargar archivo de extensión de hello para la comprobación</span><span class="sxs-lookup"><span data-stu-id="ff568-194">Upload hello extension file for verification</span></span>

<span data-ttu-id="ff568-195">La directiva ya está configurada para que Azure AD B2C sepa cómo toocommunicate con Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ff568-195">Your policy is now configured so that Azure AD B2C knows how toocommunicate with Salesforce.</span></span> <span data-ttu-id="ff568-196">Intente cargar el archivo de extensión de hello de la directiva, tooverify que no hay problemas hasta ahora.</span><span class="sxs-lookup"><span data-stu-id="ff568-196">Try uploading hello extension file of your policy, tooverify that there aren't any issues so far.</span></span> <span data-ttu-id="ff568-197">archivo de extensión de hello tooupload de la directiva:</span><span class="sxs-lookup"><span data-stu-id="ff568-197">tooupload hello extension file of your policy:</span></span>

1. <span data-ttu-id="ff568-198">En su inquilino de Azure AD B2C, vaya toohello **todas las directivas** hoja.</span><span class="sxs-lookup"><span data-stu-id="ff568-198">In your Azure AD B2C tenant, go toohello **All Policies** blade.</span></span>
2. <span data-ttu-id="ff568-199">Seleccione hello **sobrescribir directiva Hola si existe** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="ff568-199">Select hello **Overwrite hello policy if it exists** check box.</span></span>
3. <span data-ttu-id="ff568-200">Cargar archivo de extensión de hello (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="ff568-200">Upload hello extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="ff568-201">Asegúrese de que no se produce un error en la validación.</span><span class="sxs-lookup"><span data-stu-id="ff568-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a><span data-ttu-id="ff568-202">Registrar Hola viaje de usuario de Salesforce SAML notificaciones proveedor tooa</span><span class="sxs-lookup"><span data-stu-id="ff568-202">Register hello Salesforce SAML claims provider tooa user journey</span></span>

<span data-ttu-id="ff568-203">A continuación, agregue hello tooone de proveedor de identidad de Salesforce SAML de los viajes de usuario.</span><span class="sxs-lookup"><span data-stu-id="ff568-203">Next, add hello Salesforce SAML identity provider tooone of your user journeys.</span></span> <span data-ttu-id="ff568-204">En este momento, se ha configurado el proveedor de identidades de hello, pero no está disponible en cualquiera de las páginas de inicio de sesión o inicio de sesión de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff568-204">At this point, hello identity provider has been set up, but it’s not available on any of hello user sign-up or sign-in pages.</span></span> <span data-ttu-id="ff568-205">tooadd Hola página proveedor de identidades tooa inicio de sesión, en primer lugar, cree un duplicado de un viaje de usuario de plantilla existente.</span><span class="sxs-lookup"><span data-stu-id="ff568-205">tooadd hello identity provider tooa sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="ff568-206">A continuación, modificar plantilla de Hola para que también dispone de proveedor de identidades de Azure AD de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff568-206">Then, modify hello template so that it also has hello Azure AD identity provider.</span></span>

1. <span data-ttu-id="ff568-207">Abra el archivo de base de hello de la directiva (por ejemplo, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="ff568-207">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="ff568-208">Buscar hello `<UserJourneys>` elemento y, a continuación, Hola copia todo `<UserJourney>` valor, incluidos los Id. = "SignUpOrSignIn".</span><span class="sxs-lookup"><span data-stu-id="ff568-208">Find hello `<UserJourneys>` element, and then copy hello entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="ff568-209">Abra el archivo de extensión de hello (por ejemplo, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="ff568-209">Open hello extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="ff568-210">Buscar hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="ff568-210">Find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="ff568-211">Si el elemento hello no existe, cree uno.</span><span class="sxs-lookup"><span data-stu-id="ff568-211">If hello element doesn't exist, create one.</span></span>
4. <span data-ttu-id="ff568-212">Copiar todo Hola de pegar `<UserJourney>` como un elemento secundario de hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="ff568-212">Paste hello entire copied `<UserJourney>` as a child of hello `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="ff568-213">Cambiar el nombre de Id. de Hola de nuevo hello `<UserJourney>` (por ejemplo, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="ff568-213">Rename hello ID of hello new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-hello-identity-provider-button"></a><span data-ttu-id="ff568-214">Botón de proveedor de identidad de mostrar hello</span><span class="sxs-lookup"><span data-stu-id="ff568-214">Display hello identity provider button</span></span>

<span data-ttu-id="ff568-215">Hola `<ClaimsProviderSelection>` elemento es análogo tooan el botón del proveedor de identidad en una página de inicio de sesión o inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="ff568-215">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="ff568-216">Agregando un `<ClaimsProviderSelection>` elemento para Salesforce, un nuevo botón aparece cuando un usuario deja la página toothis.</span><span class="sxs-lookup"><span data-stu-id="ff568-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes toothis page.</span></span> <span data-ttu-id="ff568-217">botón de proveedor de identidad de Hola toodisplay:</span><span class="sxs-lookup"><span data-stu-id="ff568-217">toodisplay hello identity provider button:</span></span>

1. <span data-ttu-id="ff568-218">Hola `<UserJourney>` que creó, busque hello `<OrchestrationStep>` con `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="ff568-218">In hello `<UserJourney>` that you created, find hello `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="ff568-219">Agregue Hola continuación de XML:</span><span class="sxs-lookup"><span data-stu-id="ff568-219">Add hello following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="ff568-220">Establecer `TargetClaimsExchangeId` valor lógico tooa.</span><span class="sxs-lookup"><span data-stu-id="ff568-220">Set `TargetClaimsExchangeId` tooa logical value.</span></span> <span data-ttu-id="ff568-221">Se recomienda siguiente Hola misma convención de otros usuarios (por ejemplo,  *\[ClaimProviderName\]Exchange*).</span><span class="sxs-lookup"><span data-stu-id="ff568-221">We recommend following hello same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-hello-identity-provider-button-tooan-action"></a><span data-ttu-id="ff568-222">Vínculo Hola acción tooan del botón de proveedor de identidad</span><span class="sxs-lookup"><span data-stu-id="ff568-222">Link hello identity provider button tooan action</span></span>

<span data-ttu-id="ff568-223">Ahora que tiene un botón de proveedor de identidad en su lugar, vincúlelo tooan acción.</span><span class="sxs-lookup"><span data-stu-id="ff568-223">Now that you have an identity provider button in place, link it tooan action.</span></span> <span data-ttu-id="ff568-224">En este caso, acción de hello es para Azure AD B2C toocommunicate con Salesforce tooreceive un token de SAML.</span><span class="sxs-lookup"><span data-stu-id="ff568-224">In this case, hello action is for Azure AD B2C toocommunicate with Salesforce tooreceive a SAML token.</span></span> <span data-ttu-id="ff568-225">Puede hacerlo mediante la vinculación de perfil técnico Hola para su Salesforce SAML proveedor de notificaciones:</span><span class="sxs-lookup"><span data-stu-id="ff568-225">You can do this by linking hello technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="ff568-226">Hola `<UserJourney>` nodo, buscar hello `<OrchestrationStep>` con `Order="2"`.</span><span class="sxs-lookup"><span data-stu-id="ff568-226">In hello `<UserJourney>` node, find hello `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="ff568-227">Agregue Hola continuación de XML:</span><span class="sxs-lookup"><span data-stu-id="ff568-227">Add hello following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="ff568-228">Actualización `Id` toohello mismo valor que se usó previamente para `TargetClaimsExchangeId`.</span><span class="sxs-lookup"><span data-stu-id="ff568-228">Update `Id` toohello same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="ff568-229">Actualización `TechnicalProfileReferenceId` toohello `Id` de hello técnica de perfil que creó anteriormente (por ejemplo, ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="ff568-229">Update `TechnicalProfileReferenceId` toohello `Id` of hello technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="ff568-230">Cargar archivo de extensión actualizada de hello</span><span class="sxs-lookup"><span data-stu-id="ff568-230">Upload hello updated extension file</span></span>

<span data-ttu-id="ff568-231">Ha terminado de modificar el archivo de extensión Hola.</span><span class="sxs-lookup"><span data-stu-id="ff568-231">You are done modifying hello extension file.</span></span> <span data-ttu-id="ff568-232">Guarde y cargue este archivo.</span><span class="sxs-lookup"><span data-stu-id="ff568-232">Save and upload this file.</span></span> <span data-ttu-id="ff568-233">Asegúrese de que todas las validaciones se han realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="ff568-233">Ensure that all validations succeed.</span></span>

### <a name="update-hello-relying-party-file"></a><span data-ttu-id="ff568-234">Actualizar archivo de entidad de confianza de hello</span><span class="sxs-lookup"><span data-stu-id="ff568-234">Update hello relying party file</span></span>

<span data-ttu-id="ff568-235">A continuación, actualizar el archivo entidad (RP) confianza hello que inicia el viaje de usuario de Hola que ha creado:</span><span class="sxs-lookup"><span data-stu-id="ff568-235">Next, update hello relying party (RP) file that initiates hello user journey that you created:</span></span>

1. <span data-ttu-id="ff568-236">Realice una copia de SignUpOrSignIn.xml en el directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ff568-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="ff568-237">Después, cambie el nombre (por ejemplo, SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="ff568-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="ff568-238">Abra Hola Hola nuevo para archivo y actualización de `PolicyId` atributo `<TrustFrameworkPolicy>` con un valor único.</span><span class="sxs-lookup"><span data-stu-id="ff568-238">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="ff568-239">Este es el nombre de saludo de la directiva (por ejemplo, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="ff568-239">This is hello name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="ff568-240">Modificar hello `ReferenceId` atributo `<DefaultUserJourney>` toomatch hello `Id` de hello nuevo usuario del proceso que ha creado (por ejemplo, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="ff568-240">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello `Id` of hello new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="ff568-241">Guardar los cambios y, a continuación, cargar archivo hello.</span><span class="sxs-lookup"><span data-stu-id="ff568-241">Save your changes, and then upload hello file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="ff568-242">Pruebas y solución de problemas</span><span class="sxs-lookup"><span data-stu-id="ff568-242">Test and troubleshoot</span></span>

<span data-ttu-id="ff568-243">directiva personalizada de tootest Hola que acaba de cargar, Hola portal de Azure, vaya toohello hoja de la directiva y, a continuación, haga clic en **ejecutar ahora**.</span><span class="sxs-lookup"><span data-stu-id="ff568-243">tootest hello custom policy that you just uploaded, in hello Azure portal, go toohello policy blade, and then click **Run now**.</span></span> <span data-ttu-id="ff568-244">Si se produce un error, vea [Solución de problemas de directivas personalizadas](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="ff568-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff568-245">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ff568-245">Next steps</span></span>

<span data-ttu-id="ff568-246">Proporcionar comentarios demasiado[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ff568-246">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
