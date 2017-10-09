---
title: 'Azure B2C Directory Active: Agregar sus propias directivas de toocustom de atributos y usar en Editar perfil | Documentos de Microsoft'
description: "Un tutorial sobre cómo utilizar propiedades de extensión, los atributos personalizados y si se incluyen en la interfaz de usuario de Hola"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 8cc9c6a38d7652797ba54a3e02078ac2bf4a693b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a><span data-ttu-id="5aee5-103">Azure Active Directory B2C: creación y uso de atributos personalizados en una directiva de edición de perfil personalizada</span><span class="sxs-lookup"><span data-stu-id="5aee5-103">Azure Active Directory B2C: Creating and using custom attributes in a custom profile edit policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="5aee5-104">En este artículo, crear un atributo personalizado en el directorio de Azure AD B2C y usar este nuevo atributo como una demanda personalizada en viaje de usuario de edición de perfil de Hola.</span><span class="sxs-lookup"><span data-stu-id="5aee5-104">In this article, you create a custom attribute in your Azure AD B2C directory and use this new attribute as a custom claim in hello profile edit user journey.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5aee5-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5aee5-105">Prerequisites</span></span>

<span data-ttu-id="5aee5-106">Hola completa los pasos en el artículo hello [Introducción a las directivas personalizadas](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="5aee5-106">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a><span data-ttu-id="5aee5-107">Utilizar atributos personalizados toocollect información acerca de los clientes en Azure Active Directory B2C mediante directivas personalizadas</span><span class="sxs-lookup"><span data-stu-id="5aee5-107">Use custom attributes toocollect information about your customers in Azure Active Directory B2C using custom policies</span></span>
<span data-ttu-id="5aee5-108">El directorio de Azure Active Directory (Azure AD) B2C incluye un conjunto integrado de atributos: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  A menudo necesitan toocreate sus propios atributos.</span><span class="sxs-lookup"><span data-stu-id="5aee5-108">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of attributes: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  You often need toocreate your own attributes.</span></span>  <span data-ttu-id="5aee5-109">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5aee5-109">For example:</span></span>
* <span data-ttu-id="5aee5-110">Una aplicación orientado al cliente necesita toopersist un atributo como "LoyaltyNumber."</span><span class="sxs-lookup"><span data-stu-id="5aee5-110">A customer-facing application needs toopersist an attribute such as "LoyaltyNumber."</span></span>
* <span data-ttu-id="5aee5-111">Un proveedor de identidades tiene un identificador de usuario único que se debe guardar como "uniqueUserGUID"".</span><span class="sxs-lookup"><span data-stu-id="5aee5-111">An identity provider has a unique user identifier that must be saved such as "uniqueUserGUID.""</span></span>
* <span data-ttu-id="5aee5-112">Un viaje de usuario personalizado necesita toopersist Hola estado de usuario como "migrationStatus."</span><span class="sxs-lookup"><span data-stu-id="5aee5-112">A custom user journey needs toopersist hello state of user such as "migrationStatus."</span></span>

<span data-ttu-id="5aee5-113">Con Azure AD B2C, puede ampliar el conjunto de Hola de atributos que se almacenan en cada cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="5aee5-113">With Azure AD B2C, you can extend hello set of attributes stored on each user account.</span></span> <span data-ttu-id="5aee5-114">También puede leer y escribir estos atributos mediante hello [API de Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5aee5-114">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

<span data-ttu-id="5aee5-115">Propiedades de extensión extienden esquema Hola Hola de objetos de usuario en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="5aee5-115">Extension properties extend hello schema of hello user objects in hello directory.</span></span>  <span data-ttu-id="5aee5-116">propiedad de extensión de términos de Hello, atributos personalizados y notificaciones personalizadas, consulte toohello lo mismo en el contexto de Hola de este nombre de artículo y Hola varía según el contexto de hello (aplicación, objeto de directiva).</span><span class="sxs-lookup"><span data-stu-id="5aee5-116">hello terms extension property, custom attribute and custom claim refer toohello same thing in hello context of this article and hello name varies depending on hello context (application, object, policy).</span></span>

<span data-ttu-id="5aee5-117">Las propiedades de extensión solo se pueden registrar en un objeto de aplicación, aunque pueden contener datos de un usuario.</span><span class="sxs-lookup"><span data-stu-id="5aee5-117">Extension properties can only be registered on an Application object even though they may contain data for a User.</span></span> <span data-ttu-id="5aee5-118">propiedad Hello es aplicación toohello adjunto.</span><span class="sxs-lookup"><span data-stu-id="5aee5-118">hello property is attached toohello application.</span></span> <span data-ttu-id="5aee5-119">objeto de la aplicación Hello debe ser concedido acceso de escritura tooregister una propiedad de extensión.</span><span class="sxs-lookup"><span data-stu-id="5aee5-119">hello Application object must be granted write access tooregister an extension property.</span></span> <span data-ttu-id="5aee5-120">Propiedades de extensión de 100 (a través de todos los tipos y todas las aplicaciones) pueden escribirse tooany único objeto.</span><span class="sxs-lookup"><span data-stu-id="5aee5-120">100 Extension properties (across ALL types and ALL applications) can be written tooany single object.</span></span> <span data-ttu-id="5aee5-121">Propiedades de extensión se agregan toohello tipo de directorio de destino y pasa a estar accesibles inmediatamente en el inquilino de directorio de hello Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="5aee5-121">Extension properties are added toohello target directory type and becomes immediately accessible in hello Azure AD B2C directory tenant.</span></span>
<span data-ttu-id="5aee5-122">Si se elimina la aplicación hello, también se quitan las propiedades de extensión junto con los datos contenidos en ellas para todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="5aee5-122">If hello application is deleted, those Extension properties along with any data contained in them for all users are also removed.</span></span> <span data-ttu-id="5aee5-123">Si se elimina una propiedad de extensión Hola aplicación, se quita en hello los objetos de directorio de destino y Hola valores eliminados.</span><span class="sxs-lookup"><span data-stu-id="5aee5-123">If an extension property is deleted by hello Application, it is removed on hello target directory objects, and hello values deleted.</span></span>

<span data-ttu-id="5aee5-124">Propiedades de extensión solo existen en contexto de Hola de una aplicación registrada en el inquilino de Hola.</span><span class="sxs-lookup"><span data-stu-id="5aee5-124">Extension properties exist only in hello context of a registered  Application in hello tenant.</span></span> <span data-ttu-id="5aee5-125">Id. de objeto de saludo de la aplicación debe incluirse en hello TechnicalProfile que lo usan.</span><span class="sxs-lookup"><span data-stu-id="5aee5-125">hello object id of that Application must be included in hello TechnicalProfile that use it.</span></span>

>[!NOTE]
><span data-ttu-id="5aee5-126">directorio de Hello Azure AD B2C normalmente incluye una aplicación Web denominada `b2c-extensions-app`.</span><span class="sxs-lookup"><span data-stu-id="5aee5-126">hello Azure AD B2C directory typically includes a Web App named `b2c-extensions-app`.</span></span>  <span data-ttu-id="5aee5-127">Esta aplicación se usa principalmente por directivas integradas de hello b2c notificaciones personalizadas de hello creado a través del portal de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="5aee5-127">This application is primarily used by hello b2c built-in  policies for hello custom claims created via hello Azure portal.</span></span>  <span data-ttu-id="5aee5-128">Se recomienda usar este extensiones tooregister de aplicación de directivas personalizadas de b2c sólo para usuarios avanzados.</span><span class="sxs-lookup"><span data-stu-id="5aee5-128">Using this application tooregister extensions for b2c custom policies is recommended only for advanced users.</span></span>  <span data-ttu-id="5aee5-129">Se incluyen instrucciones para esto en hello sección pasos siguientes en este artículo.</span><span class="sxs-lookup"><span data-stu-id="5aee5-129">Instructions for this are included in hello Next Steps section in this article.</span></span>


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a><span data-ttu-id="5aee5-130">Crear un nuevo toostore aplicación propiedades de extensión de Hola</span><span class="sxs-lookup"><span data-stu-id="5aee5-130">Creating a new application toostore hello extension properties</span></span>

1. <span data-ttu-id="5aee5-131">Abra una sesión de exploración y desplácese toohello [PuertoA Azure](https://portal.azure.com) e inicie sesión con credenciales administrativas de hello Directory B2C desea tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="5aee5-131">Open a browsing session and navigate toohello [Azure porta](https://portal.azure.com) and sign in with administrative credentials of hello B2C Directory you wish tooconfigure.</span></span>
1. <span data-ttu-id="5aee5-132">Haga clic en **Azure Active Directory** en el menú de navegación izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5aee5-132">Click **Azure Active Directory** on hello left navigation menu.</span></span> <span data-ttu-id="5aee5-133">Puede que necesite toofind seleccionando más atiende >.</span><span class="sxs-lookup"><span data-stu-id="5aee5-133">You may need toofind it by selecting More services>.</span></span>
1. <span data-ttu-id="5aee5-134">Seleccione **Registros de aplicaciones** y haga clic en **Nuevo registro de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5aee5-134">Select **App registrations** and click **New application registration**</span></span>
1. <span data-ttu-id="5aee5-135">Proporcionar siguiente Hola recomienda entradas:</span><span class="sxs-lookup"><span data-stu-id="5aee5-135">Provide hello following recommended entries:</span></span>
  * <span data-ttu-id="5aee5-136">Especifique un nombre para la aplicación web de hello: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="5aee5-136">Specify a name for hello web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
  * <span data-ttu-id="5aee5-137">Tipo de aplicación: aplicación web o API</span><span class="sxs-lookup"><span data-stu-id="5aee5-137">Application type: Web app/API</span></span>
  * <span data-ttu-id="5aee5-138">URL de inicio de sesión: https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="5aee5-138">Sign-on URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span></span>
1. <span data-ttu-id="5aee5-139">Seleccione **Crear.</span><span class="sxs-lookup"><span data-stu-id="5aee5-139">Select **Create.</span></span> <span data-ttu-id="5aee5-140">Finalización correcta aparece en hello **notificaciones**</span><span class="sxs-lookup"><span data-stu-id="5aee5-140">Successful completion appears in hello **notifications**</span></span>
1. <span data-ttu-id="5aee5-141">Seleccione aplicación web de hello recién creado: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="5aee5-141">Select hello newly created web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
1. <span data-ttu-id="5aee5-142">Seleccione la configuración de **Permisos necesarios**.</span><span class="sxs-lookup"><span data-stu-id="5aee5-142">Select Settings: **Required permissions**</span></span>
1. <span data-ttu-id="5aee5-143">Seleccione la API **Windows Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5aee5-143">Select API **Windows Active Directory**</span></span>
1. <span data-ttu-id="5aee5-144">Coloque una marca en los permisos de aplicación **Leer y escribir en datos de directorio** y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="5aee5-144">Place a checkmark in Application Permissions: **Read and write directory data**, and **Save**</span></span>
1. <span data-ttu-id="5aee5-145">Seleccione **Conceder permisos** y haga clic en **Sí** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="5aee5-145">Choose **Grant permissions** and confirm **Yes**.</span></span>
1. <span data-ttu-id="5aee5-146">Copie tooyour Portapapeles y guarde Hola siguientes identificadores de WebApp-GraphAPI-DirectoryExtensions > Configuración > Propiedades ></span><span class="sxs-lookup"><span data-stu-id="5aee5-146">Copy tooyour clipboard and save hello following identifiers from WebApp-GraphAPI-DirectoryExtensions>Settings>Properties></span></span>
*  <span data-ttu-id="5aee5-147">**Identificador de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="5aee5-147">**Application ID** .</span></span> <span data-ttu-id="5aee5-148">Ejemplo: `103ee0e6-f92d-4183-b576-8c3739027780`</span><span class="sxs-lookup"><span data-stu-id="5aee5-148">Example: `103ee0e6-f92d-4183-b576-8c3739027780`</span></span>
* <span data-ttu-id="5aee5-149">**Identificador de objeto**.</span><span class="sxs-lookup"><span data-stu-id="5aee5-149">**Object ID**.</span></span> <span data-ttu-id="5aee5-150">Ejemplo: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span><span class="sxs-lookup"><span data-stu-id="5aee5-150">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span></span>



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a><span data-ttu-id="5aee5-151">Modificar el Hola de tooadd ApplicationObjectId de directivas personalizadas</span><span class="sxs-lookup"><span data-stu-id="5aee5-151">Modifying your custom policy tooadd hello ApplicationObjectId</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item>
                <Item Key="ClientId">insert appId here</Item>
              </Metadata>
            <!-- End of changes -->
              <CryptographicKeys>
                <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
              </CryptographicKeys>
              <IncludeInSso>false</IncludeInSso>
              <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
            </TechnicalProfile>
        </ClaimsProvider>
    </ClaimsProviders>
```

>[!NOTE]
><span data-ttu-id="5aee5-152">Hola <TechnicalProfile Id="AAD-Common"> es tooas que se hace referencia "comunes" porque sus elementos se incluye en y volver a usar en todos los hello TechnicalProfiles de Azure Active Directory mediante el elemento de hello:`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span><span class="sxs-lookup"><span data-stu-id="5aee5-152">hello <TechnicalProfile Id="AAD-Common"> is referred tooas "common" because its elements are included in and reused in all hello Azure Active Directory TechnicalProfiles by using hello element: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span></span>

>[!NOTE]
><span data-ttu-id="5aee5-153">Cuando hello TechnicalProfile escribe para la propiedad de extensión de hello primer tiempo toohello recién creado, puede experimentar un error de un solo uso.</span><span class="sxs-lookup"><span data-stu-id="5aee5-153">When hello TechnicalProfile writes for hello first time toohello newly created extension property, you may experience a one-time error.</span></span>  <span data-ttu-id="5aee5-154">propiedad de extensión de Hola se crea Hola primera vez que se utilice.</span><span class="sxs-lookup"><span data-stu-id="5aee5-154">hello extension property is created hello first time it is used.</span></span>  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a><span data-ttu-id="5aee5-155">Con la nueva propiedad de extensión Hola / atributo personalizado en un viaje de usuario</span><span class="sxs-lookup"><span data-stu-id="5aee5-155">Using hello new extension property / custom attribute in a user journey</span></span>


1. <span data-ttu-id="5aee5-156">Hola abrir archivo de confianza Party(RP) que describe la directiva de edición viaje de usuario.</span><span class="sxs-lookup"><span data-stu-id="5aee5-156">Open hello Relying Party(RP) file that describes your policy edit user journey.</span></span>  <span data-ttu-id="5aee5-157">Si está iniciando, puede ser aconsejable toodownload su versión ya configurado de Hola RP-PolicyEdit archivo directamente desde Hola sección directiva personalizada de Azure B2C Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5aee5-157">If you are starting out, it may be advisable toodownload your already configured version of hello RP-PolicyEdit file directly from hello Azure B2C Custom Policy section in hello Azure portal.</span></span>  <span data-ttu-id="5aee5-158">Como alternativa, abra el archivo XML desde la carpeta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5aee5-158">Alternatively, open your XML file from your storage folder.</span></span>
2. <span data-ttu-id="5aee5-159">Agregue una notificación personalizada `loyaltyId`.</span><span class="sxs-lookup"><span data-stu-id="5aee5-159">Add a custom claim `loyaltyId`.</span></span>  <span data-ttu-id="5aee5-160">Mediante la inclusión de saludo personalizado de notificación en hello `<RelyingParty>` elemento, se pasa como un toohello parámetro UserJourney TechnicalProfiles e incluido en el símbolo (token) de hello para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="5aee5-160">By including hello custom claim in hello `<RelyingParty>` element, it is passed as a parameter toohello UserJourney TechnicalProfiles and included in hello token for hello application.</span></span>
```xml
<RelyingParty>
   <DefaultUserJourney ReferenceId="ProfileEdit" />
   <TechnicalProfile Id="PolicyProfile">
     <DisplayName>PolicyProfile</DisplayName>
     <Protocol Name="OpenIdConnect" />
     <OutputClaims>
       <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
       <OutputClaim ClaimTypeReferenceId="city" />

       <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />

     </OutputClaims>
     <SubjectNamingInfo ClaimType="sub" />
   </TechnicalProfile>
 </RelyingParty>
 ```
3. <span data-ttu-id="5aee5-161">Agregar un archivo de directiva de extensión de notificación definición toohello `TrustFrameworkExtensions.xml` dentro de hello `<ClaimsSchema>` elemento tal como se muestra.</span><span class="sxs-lookup"><span data-stu-id="5aee5-161">Add a claim definition toohello Extension policy file  `TrustFrameworkExtensions.xml` inside hello `<ClaimsSchema>` element as shown.</span></span>
```xml
<ClaimsSchema>
        <ClaimType Id="extension_loyaltyId">
            <DisplayName>Loyalty Identification Tag</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your loyalty number from your membership card</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
</ClaimsSchema>
```
4. <span data-ttu-id="5aee5-162">Agregar Hola mismo archivo de definición de directiva Base toohello de notificación `TrustFrameworkBase.xml`.</span><span class="sxs-lookup"><span data-stu-id="5aee5-162">Add hello same claim definition toohello Base policy file `TrustFrameworkBase.xml`.</span></span>  
><span data-ttu-id="5aee5-163">Agregar un `ClaimType` definición en la base de Hola y el archivo de extensiones de hello normalmente no es necesario, sin embargo, puesto que los pasos siguientes de hello agregará hello extension_loyaltyId tooTechnicalProfiles en el archivo de Base de hello, el validador de directiva Hola rechazará carga Hola del archivo de base de hello sin él.</span><span class="sxs-lookup"><span data-stu-id="5aee5-163">Adding a `ClaimType` definition in both hello base and hello extensions file is normally not necessary, however since hello next steps will add hello extension_loyaltyId tooTechnicalProfiles in hello Base file, hello policy validator will reject hello upload of hello base file without it.</span></span>
><span data-ttu-id="5aee5-164">Puede ser útil tootrace ejecución de Hola de hello usuario viaje denominado "ProfileEdit" en el archivo de hello TrustFrameworkBase.xml.</span><span class="sxs-lookup"><span data-stu-id="5aee5-164">It may be useful tootrace hello execution of hello user journey named "ProfileEdit" in hello TrustFrameworkBase.xml file.</span></span>  <span data-ttu-id="5aee5-165">Busque el viaje de usuario de Hola de hello mismo nombre en el editor y observe que la orquestación paso 5 invoca hello TechnicalProfileReferenceID = "SelfAsserted ProfileUpdate".</span><span class="sxs-lookup"><span data-stu-id="5aee5-165">Search for hello user journey of hello same name in your editor and observe that Orchestration Step 5 invokes hello TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span></span>  <span data-ttu-id="5aee5-166">Buscar e inspeccionar este toofamiliarize TechnicalProfile con flujo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5aee5-166">Search and inspect this TechnicalProfile toofamiliarize yourself with hello flow.</span></span>
5. <span data-ttu-id="5aee5-167">Agregar loyaltyId como notificaciones de entrada y salida de hello TechnicalProfile "SelfAsserted ProfileUpdate"</span><span class="sxs-lookup"><span data-stu-id="5aee5-167">Add loyaltyId as input and output claim in hello TechnicalProfile "SelfAsserted-ProfileUpdate"</span></span>
```xml
<TechnicalProfile Id="SelfAsserted-ProfileUpdate">
          <DisplayName>User ID signup</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ContentDefinitionReferenceId">api.selfasserted.profileupdate</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>

            <InputClaim ClaimTypeReferenceId="alternativeSecurityId" />
            <InputClaim ClaimTypeReferenceId="userPrincipalName" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. <span data-ttu-id="5aee5-168">Agregar notificación de valor de hello TechnicalProfile "AAD UserWriteProfileUsingObjectId" toopersist de notificación de hello en la propiedad de extensión de hello, para el usuario actual de hello en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="5aee5-168">Add claim in TechnicalProfile "AAD-UserWriteProfileUsingObjectId" toopersist hello value of hello claim in hello extension property, for hello current user in hello directory.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteProfileUsingObjectId">
          <Metadata>
            <Item Key="Operation">Write</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">false</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
          </InputClaims>
          <PersistedClaims>
            <!-- Required claims -->
            <PersistedClaim ClaimTypeReferenceId="objectId" />

            <!-- Optional claims -->
            <PersistedClaim ClaimTypeReferenceId="givenName" />
            <PersistedClaim ClaimTypeReferenceId="surname" />
            <PersistedClaim ClaimTypeReferenceId="extension_loyaltyId" />

          </PersistedClaims>
          <IncludeTechnicalProfile ReferenceId="AAD-Common" />
        </TechnicalProfile>
```
7. <span data-ttu-id="5aee5-169">Agregar notificación de valor de hello TechnicalProfile "AAD UserReadUsingObjectId" tooread del atributo de extensión de Hola cada vez que un usuario inicia sesión.</span><span class="sxs-lookup"><span data-stu-id="5aee5-169">Add claim in TechnicalProfile "AAD-UserReadUsingObjectId" tooread hello value of hello extension attribute every time a user logs in.</span></span> <span data-ttu-id="5aee5-170">Hasta ahora hello TechnicalProfiles se han cambiado en el flujo de Hola de cuentas locales solo.</span><span class="sxs-lookup"><span data-stu-id="5aee5-170">Thus far hello TechnicalProfiles have been changed in hello flow of local accounts only.</span></span>  <span data-ttu-id="5aee5-171">Si se desea el nuevo atributo de hello en flujo de Hola de una cuenta de social/federada, un conjunto diferente de TechnicalProfiles debe toobe cambiado.</span><span class="sxs-lookup"><span data-stu-id="5aee5-171">If hello new attribute is desired in hello flow of a social/federated account, a different set of TechnicalProfiles needs toobe changed.</span></span> <span data-ttu-id="5aee5-172">Consulte los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="5aee5-172">See Next Steps.</span></span>

```xml
<!-- hello following technical profile is used tooread data after user authenticates. -->
     <TechnicalProfile Id="AAD-UserReadUsingObjectId">
       <Metadata>
         <Item Key="Operation">Read</Item>
         <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
       </Metadata>
       <IncludeInSso>false</IncludeInSso>
       <InputClaims>
         <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
       </InputClaims>
       <OutputClaims>
         <!-- Optional claims -->
         <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
         <OutputClaim ClaimTypeReferenceId="displayName" />
         <OutputClaim ClaimTypeReferenceId="otherMails" />
         <OutputClaim ClaimTypeReferenceId="givenName" />
         <OutputClaim ClaimTypeReferenceId="surname" />
         <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />
       </OutputClaims>
       <IncludeTechnicalProfile ReferenceId="AAD-Common" />
     </TechnicalProfile>
```


>[!IMPORTANT]
><span data-ttu-id="5aee5-173">elemento de Hello IncludeTechnicalProfile agrega todos los elementos de Hola de AAD común toothis TechnicalProfile.</span><span class="sxs-lookup"><span data-stu-id="5aee5-173">hello IncludeTechnicalProfile element adds all hello elements of AAD-Common toothis TechnicalProfile.</span></span>

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="5aee5-174">Probar directiva personalizada de hello mediante "Run Now"</span><span class="sxs-lookup"><span data-stu-id="5aee5-174">Test hello custom policy using "Run Now"</span></span>
1. <span data-ttu-id="5aee5-175">Hola abierto **hoja de Azure AD B2C** y navegue demasiado**identidad experiencia Framework > directivas personalizado**.</span><span class="sxs-lookup"><span data-stu-id="5aee5-175">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
1. <span data-ttu-id="5aee5-176">Active la directiva personalizada hello que ha cargado y haga clic en hello **ejecutar ahora** botón.</span><span class="sxs-lookup"><span data-stu-id="5aee5-176">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
1. <span data-ttu-id="5aee5-177">Debe ser capaz de toosign utilizando una dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="5aee5-177">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="5aee5-178">token de Id. de Hello devolvió tooyour aplicación incluye nueva propiedad de extensión hello como una demanda personalizada precedida por extension_loyaltyId.</span><span class="sxs-lookup"><span data-stu-id="5aee5-178">hello  id token sent back tooyour application includes hello new extension property as a custom claim preceded by extension_loyaltyId.</span></span> <span data-ttu-id="5aee5-179">Vea el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5aee5-179">See example.</span></span>

```
{
  "exp": 1493585187,
  "nbf": 1493581587,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493581587,
  "auth_time": 1493581587,
  "extension_loyaltyId": "abc",
  "city": "Redmond"
}
```

## <a name="next-steps"></a><span data-ttu-id="5aee5-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5aee5-180">Next steps</span></span>

<span data-ttu-id="5aee5-181">Agregar nueva notificación toohello flujos de Hola para inicios de sesión de cuenta sociales cambiando hello TechnicalProfiles enumerados.</span><span class="sxs-lookup"><span data-stu-id="5aee5-181">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed.</span></span> <span data-ttu-id="5aee5-182">Estos dos TechnicalProfiles son utilizados por toowrite de inicios de sesión de cuenta de social/federada y leer datos de usuario de hello mediante hello alternativeSecurityId como Hola localizador Hola del objeto de usuario.</span><span class="sxs-lookup"><span data-stu-id="5aee5-182">These two TechnicalProfiles are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator of hello user object.</span></span>
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

<span data-ttu-id="5aee5-183">Usar Hola mismos atributos de extensión entre directivas integradas y personalizadas.</span><span class="sxs-lookup"><span data-stu-id="5aee5-183">Using hello same extension attributes between built-in and custom policies.</span></span>
<span data-ttu-id="5aee5-184">Cuando se agregan atributos de extensión (también conocido como atributos personalizados) a través de la experiencia del portal hello, estos atributos se registran utilizando Hola ** b2c extensiones de aplicación que existe en cada inquilino b2c.</span><span class="sxs-lookup"><span data-stu-id="5aee5-184">When you add extension attributes (aka custom attributes) via hello portal experience, those attributes are registered using hello **b2c-extensions-app that exists in every b2c tenant.</span></span>  <span data-ttu-id="5aee5-185">toouse estos atributos de extensión de la directiva personalizada:</span><span class="sxs-lookup"><span data-stu-id="5aee5-185">toouse these extension attributes in your custom policy:</span></span>
1. <span data-ttu-id="5aee5-186">En el inquilino b2c en portal.azure.com, desplazarse demasiado**Azure Active Directory** y seleccione **registros de aplicación**</span><span class="sxs-lookup"><span data-stu-id="5aee5-186">Within your b2c tenant in portal.azure.com, navigate too**Azure Active Directory** and select **App registrations**</span></span>
2. <span data-ttu-id="5aee5-187">Encuentre su **b2c-extensiones-app** y selecciónelo</span><span class="sxs-lookup"><span data-stu-id="5aee5-187">Find your **b2c-extensions-app** and select it</span></span>
3. <span data-ttu-id="5aee5-188">En Hola de registro 'Essentials' **Id. de aplicación** hello y **Id. de objeto**</span><span class="sxs-lookup"><span data-stu-id="5aee5-188">Under 'Essentials' record hello **Application ID** and hello **Object ID**</span></span>
4. <span data-ttu-id="5aee5-189">Inclúyalos en sus metadatos de perfil técnico de AAD-Common de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="5aee5-189">Include them in your AAD-Common Technical profile metadata like as follows:</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is hello "Object ID" from hello "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is hello "Application ID" from hello "b2c-extensions-app"-->
              </Metadata>
```

<span data-ttu-id="5aee5-190">tookeep coherencia con la experiencia del portal hello, crear estos atributos mediante la interfaz de usuario del portal de Hola *antes de* usarlos en sus directivas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="5aee5-190">tookeep consistency with hello portal experience, create these attributes using hello portal UI *before* you use them in your custom policies.</span></span>  <span data-ttu-id="5aee5-191">Cuando se crea un atributo "ActivationStatus" en el portal de hello, debe hacer referencia tooit como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="5aee5-191">When you create an attribute "ActivationStatus" in hello portal, you must refer tooit as follows:</span></span>

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a><span data-ttu-id="5aee5-192">Referencia</span><span class="sxs-lookup"><span data-stu-id="5aee5-192">Reference</span></span>

* <span data-ttu-id="5aee5-193">A **perfil técnica (TP)** es un tipo de elemento que puede considerarse como un *función* que define el nombre de un punto de conexión, sus metadatos y su protocolo y detalles Hola Intercambio de notificaciones que Hola identidad Experiencia Framework debe realizar.</span><span class="sxs-lookup"><span data-stu-id="5aee5-193">A **Technical Profile (TP)** is an element type that can be thought of as a *function* that defines an endpoint’s name, its metadata, its protocol, and details hello exchange of claims that hello Identity Experience Framework should perform.</span></span>  <span data-ttu-id="5aee5-194">Cuando esto *función* se invoca en un paso de orquestación o desde otro TechnicalProfile, hello InputClaims y OutputClaims se proporcionan como parámetros de llamada de Hola.</span><span class="sxs-lookup"><span data-stu-id="5aee5-194">When this *function* is called in an orchestration step or from another TechnicalProfile, hello InputClaims and OutputClaims are provided as parameters by hello caller.</span></span>


* <span data-ttu-id="5aee5-195">Para tratar de forma completa en las propiedades de extensión, vea el artículo de hello [extensiones de esquema de directorio | CONCEPTOS DE API GRAPH](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span><span class="sxs-lookup"><span data-stu-id="5aee5-195">For full treatment on extension properties, see hello article [DIRECTORY SCHEMA EXTENSIONS | GRAPH API CONCEPTS](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span></span>

>[!NOTE]
><span data-ttu-id="5aee5-196">Atributos de extensión en la API Graph se denominan con convención de hello `extension_ApplicationObjectID_attributename`.</span><span class="sxs-lookup"><span data-stu-id="5aee5-196">Extension attributes in Graph API are named using hello convention `extension_ApplicationObjectID_attributename`.</span></span> <span data-ttu-id="5aee5-197">Directivas personalizadas, consulte tooextensions atributos como extension_attributename, omitir, por tanto, hello ApplicationObjectId Hola XML</span><span class="sxs-lookup"><span data-stu-id="5aee5-197">Custom policies refer tooextensions attributes as extension_attributename, thus omitting hello ApplicationObjectId in hello XML</span></span>
