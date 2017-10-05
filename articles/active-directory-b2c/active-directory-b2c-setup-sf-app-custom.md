---
title: "Azure Active Directory B2C: incorporación de un proveedor de Salesforce SAML mediante el uso de directivas personalizadas|Microsoft Docs"
description: "Obtenga información sobre cómo crear y administrar directivas personalizadas de Azure Active Directory B2C."
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
ms.openlocfilehash: 269cbd80fb6e861fa8588025eec70b6c6e2890d7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="80984-103">Azure Active Directory B2C: inicio de sesión mediante cuentas de Salesforce a través de SAML</span><span class="sxs-lookup"><span data-stu-id="80984-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="80984-104">En este artículo se muestra cómo usar [directivas personalizadas](active-directory-b2c-overview-custom.md) para configurar el inicio de sesión de los usuarios de una organización de Salesforce concreta.</span><span class="sxs-lookup"><span data-stu-id="80984-104">This article shows you how to use [custom policies](active-directory-b2c-overview-custom.md) to set up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80984-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="80984-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="80984-106">Configuración de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="80984-106">Azure AD B2C setup</span></span>

<span data-ttu-id="80984-107">Asegúrese de que ha completado todos los pasos que le muestran cómo [empezar a trabajar con directivas personalizadas](active-directory-b2c-get-started-custom.md) en Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="80984-107">Ensure that you have completed all of the steps that show you how to [get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="80984-108">Entre ellos se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="80984-108">These include:</span></span>

* <span data-ttu-id="80984-109">Crear un inquilino de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="80984-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="80984-110">Crear una aplicación de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="80984-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="80984-111">Registrar dos aplicaciones de motor de directivas.</span><span class="sxs-lookup"><span data-stu-id="80984-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="80984-112">Configurar las claves.</span><span class="sxs-lookup"><span data-stu-id="80984-112">Set up keys.</span></span>
* <span data-ttu-id="80984-113">Configurar el paquete de inicio.</span><span class="sxs-lookup"><span data-stu-id="80984-113">Set up the starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="80984-114">Configuración de Salesforce</span><span class="sxs-lookup"><span data-stu-id="80984-114">Salesforce setup</span></span>

<span data-ttu-id="80984-115">En este artículo se supone que ya ha realizado lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="80984-115">In this article, we assume that you have already done the following:</span></span>

* <span data-ttu-id="80984-116">Se ha registrado para obtener una cuenta de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="80984-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="80984-117">Puede registrarse para [una cuenta gratuita de Developer Edition](https://developer.salesforce.com/signup).</span><span class="sxs-lookup"><span data-stu-id="80984-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="80984-118">[Ha configurado un Mi dominio](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) para su organización de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="80984-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="80984-119">Configurar Salesforce, para que los usuarios se puedan federar</span><span class="sxs-lookup"><span data-stu-id="80984-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="80984-120">Para permitir que Azure AD B2C se comunique con Salesforce, debe obtener la dirección URL de metadatos de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="80984-120">To help Azure AD B2C communicate with Salesforce, you need to get the Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="80984-121">Configurar Salesforce como proveedor de identidades</span><span class="sxs-lookup"><span data-stu-id="80984-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="80984-122">En este artículo, se supone que usa [Lightning Experience de Salesforce](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span><span class="sxs-lookup"><span data-stu-id="80984-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="80984-123">[Inicie sesión en Salesforce](https://login.salesforce.com/).</span><span class="sxs-lookup"><span data-stu-id="80984-123">[Sign in to Salesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="80984-124">En el menú de la izquierda, en **Settings** (Configuración), expanda **Identity** (Identidad) y haga clic en **Identity Provider** (Proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="80984-124">On the left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="80984-125">Haga clic en **Enable Identity Provider** (Habilitar proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="80984-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="80984-126">Bajo **Select the certificate** (Seleccionar el certificado), seleccione el certificado que quiere que Salesforce use para comunicarse con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="80984-126">Under **Select the certificate**, select the certificate you want Salesforce to use to communicate with Azure AD B2C.</span></span> <span data-ttu-id="80984-127">(Puede usar el certificado predeterminado). Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="80984-127">(You can use the default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="80984-128">Crear una aplicación conectada en Salesforce</span><span class="sxs-lookup"><span data-stu-id="80984-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="80984-129">En la página **Identity Provider** (Proveedor de identidades), vaya a **Service Providers** (Proveedores de servicios).</span><span class="sxs-lookup"><span data-stu-id="80984-129">On the **Identity Provider** page, go to **Service Providers**.</span></span>
2. <span data-ttu-id="80984-130">Haga clic en **Service Providers are now created via Connected Apps (Los proveedores de servicios se crean ahora a través de aplicaciones conectadas). Haga clic aquí.**</span><span class="sxs-lookup"><span data-stu-id="80984-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="80984-131">En **Basic Information**(Información básica), escriba los valores necesarios para la aplicación conectada.</span><span class="sxs-lookup"><span data-stu-id="80984-131">Under **Basic Information**,  enter the required values for your connected app.</span></span>
4. <span data-ttu-id="80984-132">En **Web App Settings** (Configuración de aplicación web), active la casilla **Enable SAML** (Habilitar SAML).</span><span class="sxs-lookup"><span data-stu-id="80984-132">Under **Web App Settings**, select the **Enable SAML** check box.</span></span>
5. <span data-ttu-id="80984-133">En el campo **Entity ID** (Id. de entidad), escriba la siguiente dirección URL.</span><span class="sxs-lookup"><span data-stu-id="80984-133">In the **Entity ID** field, enter the following URL.</span></span> <span data-ttu-id="80984-134">Asegúrese de que reemplaza el valor de `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="80984-134">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="80984-135">En el campo **ACS URL** (Dirección URL de ACS), escriba la siguiente dirección URL.</span><span class="sxs-lookup"><span data-stu-id="80984-135">In the **ACS URL** field, enter the following URL.</span></span> <span data-ttu-id="80984-136">Asegúrese de que reemplaza el valor de `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="80984-136">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="80984-137">Deje los valores predeterminados de las demás opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="80984-137">Leave the default values for all other settings.</span></span>
8. <span data-ttu-id="80984-138">Desplácese hasta la parte inferior de la lista y, después, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="80984-138">Scroll to the bottom of the list, and then click **Save**.</span></span>

### <a name="get-the-metadata-url"></a><span data-ttu-id="80984-139">Obtener la dirección URL de metadatos</span><span class="sxs-lookup"><span data-stu-id="80984-139">Get the metadata URL</span></span>

1. <span data-ttu-id="80984-140">En la página de información general de la aplicación conectada, haga clic en **Administrar**.</span><span class="sxs-lookup"><span data-stu-id="80984-140">On the overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="80984-141">Copie el valor de **punto de conexión de detección de metadatos** y después guárdelo.</span><span class="sxs-lookup"><span data-stu-id="80984-141">Copy the value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="80984-142">Lo usará más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="80984-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-to-federate"></a><span data-ttu-id="80984-143">Configurar usuarios de Salesforce para la federación</span><span class="sxs-lookup"><span data-stu-id="80984-143">Set up Salesforce users to federate</span></span>

1. <span data-ttu-id="80984-144">En la página **Administrar** de la aplicación conectada, vaya a **Perfiles**.</span><span class="sxs-lookup"><span data-stu-id="80984-144">On the **Manage** page of your connected app, go to **Profiles**.</span></span>
2. <span data-ttu-id="80984-145">Haga clic en **Administrar perfiles**.</span><span class="sxs-lookup"><span data-stu-id="80984-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="80984-146">Seleccione los perfiles (o grupos de usuarios) que quiere que realicen la federación con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="80984-146">Select the profiles (or groups of users) that you want to federate with Azure AD B2C.</span></span> <span data-ttu-id="80984-147">Como administrador del sistema, active la casilla **Administrador del sistema** para poder realizar la federación con su cuenta de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="80984-147">As a system administrator, select the **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="80984-148">Generar un certificado de firma para Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="80984-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="80984-149">Las solicitudes enviadas a Salesforce deben estar firmadas mediante Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="80984-149">Requests sent to Salesforce need to be signed by Azure AD B2C.</span></span> <span data-ttu-id="80984-150">Para generar un certificado de firma, abra Azure PowerShell y ejecute los comandos siguientes.</span><span class="sxs-lookup"><span data-stu-id="80984-150">To generate a signing certificate, open Azure PowerShell, and then run the following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="80984-151">Asegúrese de actualizar el nombre de inquilino y la contraseña en las dos líneas superiores.</span><span class="sxs-lookup"><span data-stu-id="80984-151">Make sure that you update the tenant name and password in the top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-the-saml-signing-certificate-to-azure-ad-b2c"></a><span data-ttu-id="80984-152">Agregar un certificado de firma de SAML a Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="80984-152">Add the SAML signing certificate to Azure AD B2C</span></span>

<span data-ttu-id="80984-153">Cargue el certificado de firma en el inquilino de Azure AD B2C:</span><span class="sxs-lookup"><span data-stu-id="80984-153">Upload the signing certificate to your Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="80984-154">Vaya al inquilino de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="80984-154">Go to your Azure AD B2C tenant.</span></span> <span data-ttu-id="80984-155">Haga clic en **Configuración** > **Marco de experiencia de identidad** > **Claves de directiva**.</span><span class="sxs-lookup"><span data-stu-id="80984-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="80984-156">Haga clic en **+Agregar** y después:</span><span class="sxs-lookup"><span data-stu-id="80984-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="80984-157">Haga clic en **Opciones** > **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="80984-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="80984-158">Escriba un **nombre** (por ejemplo, SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="80984-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="80984-159">El prefijo *B2C_1A_* se agrega automáticamente al nombre de la clave.</span><span class="sxs-lookup"><span data-stu-id="80984-159">The prefix *B2C_1A_* is automatically added to the name of your key.</span></span>
    3. <span data-ttu-id="80984-160">Para seleccionar el certificado, use el **control de carga de archivos**.</span><span class="sxs-lookup"><span data-stu-id="80984-160">To select your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="80984-161">Escriba la contraseña del certificado que ha establecido en el script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="80984-161">Enter the certificate's password that you set in the PowerShell script.</span></span>
3. <span data-ttu-id="80984-162">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="80984-162">Click **Create**.</span></span>
4. <span data-ttu-id="80984-163">Compruebe que ha creado una clave (por ejemplo, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="80984-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="80984-164">Tome nota del nombre completo (incluido *B2C_1A_*).</span><span class="sxs-lookup"><span data-stu-id="80984-164">Take note of the full name (including *B2C_1A_*).</span></span> <span data-ttu-id="80984-165">Hará referencia a esta clave más adelante en la directiva.</span><span class="sxs-lookup"><span data-stu-id="80984-165">You will refer to this key later in the policy.</span></span>

## <a name="create-the-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="80984-166">Creación del proveedor de notificaciones de Salesforce SAML en la directiva de base</span><span class="sxs-lookup"><span data-stu-id="80984-166">Create the Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="80984-167">Para que los usuarios puedan iniciar sesión mediante Salesforce, debe definir Salesforce como proveedor de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="80984-167">You need to define Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="80984-168">En otras palabras, tiene que especificar el punto de conexión con el que Azure AD B2C se va a comunicar.</span><span class="sxs-lookup"><span data-stu-id="80984-168">In other words, you need to specify the endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="80984-169">El punto de conexión *proporcionará* un conjunto de *notificaciones* que Azure AD B2C usa para comprobar que un usuario concreto se ha autenticado.</span><span class="sxs-lookup"><span data-stu-id="80984-169">The endpoint will *provide* a set of *claims* that Azure AD B2C uses to verify that a specific user has authenticated.</span></span> <span data-ttu-id="80984-170">Para ello, agregue un `<ClaimsProvider>` para Salesforce en el archivo de extensión de la directiva:</span><span class="sxs-lookup"><span data-stu-id="80984-170">To do this, add a `<ClaimsProvider>` for Salesforce in the extension file of your policy:</span></span>

1. <span data-ttu-id="80984-171">En el directorio de trabajo, abra el archivo de extensión (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="80984-171">In your working directory, open the extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="80984-172">Busque la sección `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="80984-172">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="80984-173">Si no existe, créelo debajo del nodo raíz.</span><span class="sxs-lookup"><span data-stu-id="80984-173">If it does not exist, create it under the root node.</span></span>
3. <span data-ttu-id="80984-174">Agregar un nuevo `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="80984-174">Add a new `<ClaimsProvider>`:</span></span>

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

<span data-ttu-id="80984-175">En el nodo `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="80984-175">Under the `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="80984-176">Cambie el valor de `<Domain>` a un valor único que distinga `<ClaimsProvider>` de otros proveedores de identidades.</span><span class="sxs-lookup"><span data-stu-id="80984-176">Change the value for `<Domain>` to a unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="80984-177">Actualice el valor de `<DisplayName>` a un nombre para mostrar para el proveedor de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="80984-177">Update the value for `<DisplayName>` to a display name for the claims provider.</span></span> <span data-ttu-id="80984-178">Actualmente este valor no se usa.</span><span class="sxs-lookup"><span data-stu-id="80984-178">Currently, this value is not used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="80984-179">Actualización del perfil técnico</span><span class="sxs-lookup"><span data-stu-id="80984-179">Update the technical profile</span></span>

<span data-ttu-id="80984-180">Para obtener un token de SAML de Salesforce, defina los protocolos que Azure AD B2C va a usar para comunicarse con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="80984-180">To get a SAML token from Salesforce, define the protocols that Azure AD B2C will use to communicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="80984-181">Puede hacer esto en el elemento `<TechnicalProfile>` de `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="80984-181">Do this in the `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="80984-182">Actualice el identificador del nodo `<TechnicalProfile>`.</span><span class="sxs-lookup"><span data-stu-id="80984-182">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="80984-183">Este identificador se usa para hacer referencia a este perfil técnico desde otras partes de la directiva.</span><span class="sxs-lookup"><span data-stu-id="80984-183">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
2. <span data-ttu-id="80984-184">Actualice el valor de `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="80984-184">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="80984-185">Este valor se muestra en el botón de inicio de sesión de la página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="80984-185">This value is displayed on the sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="80984-186">Actualice el valor de `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="80984-186">Update the value for `<Description>`.</span></span>
4. <span data-ttu-id="80984-187">Salesforce usa el protocolo SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="80984-187">Salesforce uses the SAML 2.0 protocol.</span></span> <span data-ttu-id="80984-188">Asegúrese de que el valor de `<Protocol>` es **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="80984-188">Ensure that the value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="80984-189">Actualice la sección `<Metadata>` del código XML anterior para reflejar la configuración de su cuenta de Salesforce específica.</span><span class="sxs-lookup"><span data-stu-id="80984-189">Update the `<Metadata>` section in the preceding XML to reflect the settings for your specific Salesforce account.</span></span> <span data-ttu-id="80984-190">En el código XML, actualice los valores de metadatos:</span><span class="sxs-lookup"><span data-stu-id="80984-190">In the XML, update the metadata values:</span></span>

1. <span data-ttu-id="80984-191">Actualice el valor de `<Item Key="PartnerEntity">` con la dirección URL de metadatos de Salesforce que ha copiado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="80984-191">Update the value of `<Item Key="PartnerEntity">` with the Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="80984-192">Tiene el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="80984-192">It has the following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="80984-193">En la sección `<CryptographicKeys>`, actualice el valor de las dos instancias de `StorageReferenceId` con el nombre de la clave de su certificado de firma (por ejemplo, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="80984-193">In the `<CryptographicKeys>` section, update the value for both instances of `StorageReferenceId` to the name of the key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="80984-194">Carga del archivo de extensión para su comprobación</span><span class="sxs-lookup"><span data-stu-id="80984-194">Upload the extension file for verification</span></span>

<span data-ttu-id="80984-195">Ahora la directiva está configurada para que Azure AD B2C sepa cómo comunicarse con Salesforce.</span><span class="sxs-lookup"><span data-stu-id="80984-195">Your policy is now configured so that Azure AD B2C knows how to communicate with Salesforce.</span></span> <span data-ttu-id="80984-196">Pruebe a cargar el archivo de extensión de la directiva, para confirmar que no tiene problemas.</span><span class="sxs-lookup"><span data-stu-id="80984-196">Try uploading the extension file of your policy, to verify that there aren't any issues so far.</span></span> <span data-ttu-id="80984-197">Para cargar el archivo de extensión de la directiva:</span><span class="sxs-lookup"><span data-stu-id="80984-197">To upload the extension file of your policy:</span></span>

1. <span data-ttu-id="80984-198">En el inquilino de Azure AD B2C, vaya a la hoja **All Policies** (Todas las directivas).</span><span class="sxs-lookup"><span data-stu-id="80984-198">In your Azure AD B2C tenant, go to the **All Policies** blade.</span></span>
2. <span data-ttu-id="80984-199">Active la casilla **Sobrescribir la directiva si existe**.</span><span class="sxs-lookup"><span data-stu-id="80984-199">Select the **Overwrite the policy if it exists** check box.</span></span>
3. <span data-ttu-id="80984-200">Cargue el archivo de extensión (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="80984-200">Upload the extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="80984-201">Asegúrese de que no se produce un error en la validación.</span><span class="sxs-lookup"><span data-stu-id="80984-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-the-salesforce-saml-claims-provider-to-a-user-journey"></a><span data-ttu-id="80984-202">Registrar el proveedor de notificaciones de Salesforce SAML en un recorrido del usuario</span><span class="sxs-lookup"><span data-stu-id="80984-202">Register the Salesforce SAML claims provider to a user journey</span></span>

<span data-ttu-id="80984-203">Después, agregue el proveedor de identidades de Salesforce SAML a uno de los recorridos del usuario.</span><span class="sxs-lookup"><span data-stu-id="80984-203">Next, add the Salesforce SAML identity provider to one of your user journeys.</span></span> <span data-ttu-id="80984-204">El proveedor de identidades ya se ha configurado, pero no está disponible en ninguna de las páginas de registro o inicio de sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="80984-204">At this point, the identity provider has been set up, but it’s not available on any of the user sign-up or sign-in pages.</span></span> <span data-ttu-id="80984-205">Para agregar el proveedor de identidades a una página de inicio de sesión, en primer lugar cree un duplicado de una plantilla de recorrido del usuario existente.</span><span class="sxs-lookup"><span data-stu-id="80984-205">To add the identity provider to a sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="80984-206">Después, modifique la plantilla para que también tenga el proveedor de identidades de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80984-206">Then, modify the template so that it also has the Azure AD identity provider.</span></span>

1. <span data-ttu-id="80984-207">Abra el archivo base de la directiva (por ejemplo, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="80984-207">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="80984-208">Busque el elemento `<UserJourneys>` y copie el valor `<UserJourney>` completo, incluido Id="SignUpOrSignIn".</span><span class="sxs-lookup"><span data-stu-id="80984-208">Find the `<UserJourneys>` element, and then copy the entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="80984-209">Abra el archivo de extensión (por ejemplo, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="80984-209">Open the extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="80984-210">Busque el elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="80984-210">Find the `<UserJourneys>` element.</span></span> <span data-ttu-id="80984-211">Si el elemento no existe, cree uno.</span><span class="sxs-lookup"><span data-stu-id="80984-211">If the element doesn't exist, create one.</span></span>
4. <span data-ttu-id="80984-212">Pegue todo el elemento `<UserJourney>` copiado como elemento secundario de `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="80984-212">Paste the entire copied `<UserJourney>` as a child of the `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="80984-213">Cambie el nombre del Id. del nuevo `<UserJourney>` (por ejemplo, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="80984-213">Rename the ID of the new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-the-identity-provider-button"></a><span data-ttu-id="80984-214">Mostrar el botón de proveedor de identidades</span><span class="sxs-lookup"><span data-stu-id="80984-214">Display the identity provider button</span></span>

<span data-ttu-id="80984-215">El elemento `<ClaimsProviderSelection>` es análogo a un botón de proveedor de identidades en una página de registro o inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="80984-215">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="80984-216">Al agregar un elemento `<ClaimsProviderSelection>` para Salesforce, aparece un botón nuevo cuando un usuario se desplaza a esta página.</span><span class="sxs-lookup"><span data-stu-id="80984-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes to this page.</span></span> <span data-ttu-id="80984-217">Para mostrar el botón de proveedor de identidades:</span><span class="sxs-lookup"><span data-stu-id="80984-217">To display the identity provider button:</span></span>

1. <span data-ttu-id="80984-218">En el `<UserJourney>` que ha creado, busque `<OrchestrationStep>` con `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="80984-218">In the `<UserJourney>` that you created, find the `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="80984-219">Agregue el siguiente código XML:</span><span class="sxs-lookup"><span data-stu-id="80984-219">Add the following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="80984-220">Establezca `TargetClaimsExchangeId` en un valor lógico.</span><span class="sxs-lookup"><span data-stu-id="80984-220">Set `TargetClaimsExchangeId` to a logical value.</span></span> <span data-ttu-id="80984-221">Se recomienda seguir la misma convención que en el resto: (por ejemplo, *\[NombreProveedorDeNotificaciones\]Exchange*).</span><span class="sxs-lookup"><span data-stu-id="80984-221">We recommend following the same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-the-identity-provider-button-to-an-action"></a><span data-ttu-id="80984-222">Vincular el botón de proveedor de identidades a una acción</span><span class="sxs-lookup"><span data-stu-id="80984-222">Link the identity provider button to an action</span></span>

<span data-ttu-id="80984-223">Ahora que hay un botón de proveedor de identidades colocado, vincúlelo a una acción.</span><span class="sxs-lookup"><span data-stu-id="80984-223">Now that you have an identity provider button in place, link it to an action.</span></span> <span data-ttu-id="80984-224">En este caso, la acción es para que Azure AD B2C se comunique con Salesforce para recibir un token SAML.</span><span class="sxs-lookup"><span data-stu-id="80984-224">In this case, the action is for Azure AD B2C to communicate with Salesforce to receive a SAML token.</span></span> <span data-ttu-id="80984-225">Para ello, vincule el perfil técnico del proveedor de notificaciones de Salesforce SAML:</span><span class="sxs-lookup"><span data-stu-id="80984-225">You can do this by linking the technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="80984-226">En el nodo `<UserJourney>`, busque `<OrchestrationStep>` con `Order="2"`.</span><span class="sxs-lookup"><span data-stu-id="80984-226">In the `<UserJourney>` node, find the `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="80984-227">Agregue el siguiente código XML:</span><span class="sxs-lookup"><span data-stu-id="80984-227">Add the following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="80984-228">Actualice `Id` al mismo valor que ha usado previamente para `TargetClaimsExchangeId`.</span><span class="sxs-lookup"><span data-stu-id="80984-228">Update `Id` to the same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="80984-229">Actualice `TechnicalProfileReferenceId` al valor `Id` del perfil técnico que ha creado anteriormente (por ejemplo, ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="80984-229">Update `TechnicalProfileReferenceId` to the `Id` of the technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="80984-230">Cargar el archivo de extensión actualizado</span><span class="sxs-lookup"><span data-stu-id="80984-230">Upload the updated extension file</span></span>

<span data-ttu-id="80984-231">Ya ha terminado la modificación del archivo de extensión.</span><span class="sxs-lookup"><span data-stu-id="80984-231">You are done modifying the extension file.</span></span> <span data-ttu-id="80984-232">Guarde y cargue este archivo.</span><span class="sxs-lookup"><span data-stu-id="80984-232">Save and upload this file.</span></span> <span data-ttu-id="80984-233">Asegúrese de que todas las validaciones se han realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="80984-233">Ensure that all validations succeed.</span></span>

### <a name="update-the-relying-party-file"></a><span data-ttu-id="80984-234">Actualizar el archivo de usuario de confianza</span><span class="sxs-lookup"><span data-stu-id="80984-234">Update the relying party file</span></span>

<span data-ttu-id="80984-235">Después, actualice el archivo del usuario de confianza (RP) que inicia el recorrido del usuario que ha creado:</span><span class="sxs-lookup"><span data-stu-id="80984-235">Next, update the relying party (RP) file that initiates the user journey that you created:</span></span>

1. <span data-ttu-id="80984-236">Realice una copia de SignUpOrSignIn.xml en el directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="80984-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="80984-237">Después, cambie el nombre (por ejemplo, SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="80984-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="80984-238">Abra el archivo nuevo y actualice el atributo `PolicyId` de `<TrustFrameworkPolicy>` con un valor único.</span><span class="sxs-lookup"><span data-stu-id="80984-238">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="80984-239">Este es el nombre de la directiva (por ejemplo, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="80984-239">This is the name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="80984-240">Modifique el atributo `ReferenceId` de `<DefaultUserJourney>` para que coincida con el `Id` del nuevo recorrido del usuario que ha creado (por ejemplo, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="80984-240">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the `Id` of the new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="80984-241">Guarde los cambios y después cargue el archivo.</span><span class="sxs-lookup"><span data-stu-id="80984-241">Save your changes, and then upload the file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="80984-242">Pruebas y solución de problemas</span><span class="sxs-lookup"><span data-stu-id="80984-242">Test and troubleshoot</span></span>

<span data-ttu-id="80984-243">Para probar la directiva personalizada que acaba de cargar, en Azure Portal, vaya a la hoja de la directiva y, después, haga clic en **Ejecutar ahora**.</span><span class="sxs-lookup"><span data-stu-id="80984-243">To test the custom policy that you just uploaded, in the Azure portal, go to the policy blade, and then click **Run now**.</span></span> <span data-ttu-id="80984-244">Si se produce un error, vea [Solución de problemas de directivas personalizadas](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="80984-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="80984-245">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="80984-245">Next steps</span></span>

<span data-ttu-id="80984-246">Envíe sus comentarios a [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="80984-246">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
