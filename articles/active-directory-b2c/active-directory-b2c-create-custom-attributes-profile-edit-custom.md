---
title: "Azure Active Directory B2C: adición de sus propios atributos a las directivas personalizadas y su uso en la edición del perfil | Microsoft Docs"
description: "Un tutorial acerca de cómo utilizar las propiedades de extensión y los atributos personalizados, y cómo incluirlos en la interfaz de usuario"
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
ms.openlocfilehash: 67c9f6eca18e2dd77e00b8bc8c7bcc546ea3936e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a><span data-ttu-id="43b94-103">Azure Active Directory B2C: creación y uso de atributos personalizados en una directiva de edición de perfil personalizada</span><span class="sxs-lookup"><span data-stu-id="43b94-103">Azure Active Directory B2C: Creating and using custom attributes in a custom profile edit policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="43b94-104">En este artículo, creará un atributo personalizado en un directorio de Azure AD B2C y lo usará como notificación personalizada en el recorrido del usuario de la edición del perfil.</span><span class="sxs-lookup"><span data-stu-id="43b94-104">In this article, you create a custom attribute in your Azure AD B2C directory and use this new attribute as a custom claim in the profile edit user journey.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43b94-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="43b94-105">Prerequisites</span></span>

<span data-ttu-id="43b94-106">Complete los pasos del artículo [Introducción a las directivas personalizadas](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="43b94-106">Complete the steps in the article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="use-custom-attributes-to-collect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a><span data-ttu-id="43b94-107">Uso de los atributos personalizados para recopilar información acerca de los clientes en Azure Active Directory B2C mediante directivas personalizadas</span><span class="sxs-lookup"><span data-stu-id="43b94-107">Use custom attributes to collect information about your customers in Azure Active Directory B2C using custom policies</span></span>
<span data-ttu-id="43b94-108">El directorio de Azure Active Directory (Azure AD) B2C incluye un conjunto integrado de atributos: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  A menudo, necesitará crear sus propios atributos.</span><span class="sxs-lookup"><span data-stu-id="43b94-108">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of attributes: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  You often need to create your own attributes.</span></span>  <span data-ttu-id="43b94-109">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="43b94-109">For example:</span></span>
* <span data-ttu-id="43b94-110">Una aplicación orientada al cliente necesita conservar un atributo como "LoyaltyNumber".</span><span class="sxs-lookup"><span data-stu-id="43b94-110">A customer-facing application needs to persist an attribute such as "LoyaltyNumber."</span></span>
* <span data-ttu-id="43b94-111">Un proveedor de identidades tiene un identificador de usuario único que se debe guardar como "uniqueUserGUID"".</span><span class="sxs-lookup"><span data-stu-id="43b94-111">An identity provider has a unique user identifier that must be saved such as "uniqueUserGUID.""</span></span>
* <span data-ttu-id="43b94-112">Un recorrido del usuario personalizado necesita conservar el estado del usuario como "migrationStatus".</span><span class="sxs-lookup"><span data-stu-id="43b94-112">A custom user journey needs to persist the state of user such as "migrationStatus."</span></span>

<span data-ttu-id="43b94-113">Con Azure AD B2C, puede ampliar el conjunto de atributos que se almacenan en cada cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="43b94-113">With Azure AD B2C, you can extend the set of attributes stored on each user account.</span></span> <span data-ttu-id="43b94-114">También puede leer y escribir estos atributos mediante la [API de Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="43b94-114">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

<span data-ttu-id="43b94-115">Las propiedades de extensión extienden el esquema de los objetos de usuario en el directorio.</span><span class="sxs-lookup"><span data-stu-id="43b94-115">Extension properties extend the schema of the user objects in the directory.</span></span>  <span data-ttu-id="43b94-116">Los términos propiedad de la extensión, atributo personalizado y notificación personalizada hacen referencia a la misma cosa en el contexto de este artículo y el nombre varía según el contexto (aplicación, objeto, directiva).</span><span class="sxs-lookup"><span data-stu-id="43b94-116">The terms extension property, custom attribute and custom claim refer to the same thing in the context of this article and the name varies depending on the context (application, object, policy).</span></span>

<span data-ttu-id="43b94-117">Las propiedades de extensión solo se pueden registrar en un objeto de aplicación, aunque pueden contener datos de un usuario.</span><span class="sxs-lookup"><span data-stu-id="43b94-117">Extension properties can only be registered on an Application object even though they may contain data for a User.</span></span> <span data-ttu-id="43b94-118">La propiedad está conectada a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="43b94-118">The property is attached to the application.</span></span> <span data-ttu-id="43b94-119">El objeto de aplicación debe tener acceso de escritura para registrar una propiedad de extensión.</span><span class="sxs-lookup"><span data-stu-id="43b94-119">The Application object must be granted write access to register an extension property.</span></span> <span data-ttu-id="43b94-120">En un objeto individual se pueden escribir cien propiedades de extensión (de TODOS los tipos y TODAS las aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="43b94-120">100 Extension properties (across ALL types and ALL applications) can be written to any single object.</span></span> <span data-ttu-id="43b94-121">Las propiedades de extensión se agregan al tipo de directorio de destino y se puede acceder a ellas de inmediato en el inquilino del directorio de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="43b94-121">Extension properties are added to the target directory type and becomes immediately accessible in the Azure AD B2C directory tenant.</span></span>
<span data-ttu-id="43b94-122">Si la aplicación se elimina, también se quitan las propiedades de extensión, junto con los datos que contienen de todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="43b94-122">If the application is deleted, those Extension properties along with any data contained in them for all users are also removed.</span></span> <span data-ttu-id="43b94-123">Si la aplicación elimina una propiedad de extensión, se quita en los objetos de directorio de destino, y también se quitan los valores.</span><span class="sxs-lookup"><span data-stu-id="43b94-123">If an extension property is deleted by the Application, it is removed on the target directory objects, and the values deleted.</span></span>

<span data-ttu-id="43b94-124">Las propiedades de extensión solo existen en el contexto de una aplicación registrada en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="43b94-124">Extension properties exist only in the context of a registered  Application in the tenant.</span></span> <span data-ttu-id="43b94-125">El identificador de objeto de la aplicación debe estar incluido en el elemento TechnicalProfile que lo utiliza.</span><span class="sxs-lookup"><span data-stu-id="43b94-125">The object id of that Application must be included in the TechnicalProfile that use it.</span></span>

>[!NOTE]
><span data-ttu-id="43b94-126">El directorio de Azure AD B2C normalmente incluye una aplicación de web llamada `b2c-extensions-app`.</span><span class="sxs-lookup"><span data-stu-id="43b94-126">The Azure AD B2C directory typically includes a Web App named `b2c-extensions-app`.</span></span>  <span data-ttu-id="43b94-127">Esta aplicación la usan principalmente las directivas integradas de b2c para las notificaciones personalizadas creadas a través de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="43b94-127">This application is primarily used by the b2c built-in  policies for the custom claims created via the Azure portal.</span></span>  <span data-ttu-id="43b94-128">Se recomienda que sean los usuarios avanzados quienes usen esta aplicación para registrar extensiones para las directivas personalizadas de b2c.</span><span class="sxs-lookup"><span data-stu-id="43b94-128">Using this application to register extensions for b2c custom policies is recommended only for advanced users.</span></span>  <span data-ttu-id="43b94-129">En la sección Pasos siguientes de este artículo encontrará instrucciones para esto.</span><span class="sxs-lookup"><span data-stu-id="43b94-129">Instructions for this are included in the Next Steps section in this article.</span></span>


## <a name="creating-a-new-application-to-store-the-extension-properties"></a><span data-ttu-id="43b94-130">Creación de una nueva aplicación para almacenar las propiedades de extensión</span><span class="sxs-lookup"><span data-stu-id="43b94-130">Creating a new application to store the extension properties</span></span>

1. <span data-ttu-id="43b94-131">Abra una sesión de exploración y navegue hasta [Azure Portal](https://portal.azure.com) e inicie sesión con credenciales administrativas del directorio B2C que desea configurar.</span><span class="sxs-lookup"><span data-stu-id="43b94-131">Open a browsing session and navigate to the [Azure porta](https://portal.azure.com) and sign in with administrative credentials of the B2C Directory you wish to configure.</span></span>
1. <span data-ttu-id="43b94-132">Haga clic en **Azure Active Directory** en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="43b94-132">Click **Azure Active Directory** on the left navigation menu.</span></span> <span data-ttu-id="43b94-133">Puede que tenga que buscarlo, para lo que debe seleccionar Más servicios>.</span><span class="sxs-lookup"><span data-stu-id="43b94-133">You may need to find it by selecting More services>.</span></span>
1. <span data-ttu-id="43b94-134">Seleccione **Registros de aplicaciones** y haga clic en **Nuevo registro de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="43b94-134">Select **App registrations** and click **New application registration**</span></span>
1. <span data-ttu-id="43b94-135">Especifique las siguientes entradas recomendadas:</span><span class="sxs-lookup"><span data-stu-id="43b94-135">Provide the following recommended entries:</span></span>
  * <span data-ttu-id="43b94-136">Especifique un nombre para la aplicación web: **WebApp-GraphAPI-DirectoryExtensions**.</span><span class="sxs-lookup"><span data-stu-id="43b94-136">Specify a name for the web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
  * <span data-ttu-id="43b94-137">Tipo de aplicación: aplicación web o API</span><span class="sxs-lookup"><span data-stu-id="43b94-137">Application type: Web app/API</span></span>
  * <span data-ttu-id="43b94-138">URL de inicio de sesión: https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="43b94-138">Sign-on URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span></span>
1. <span data-ttu-id="43b94-139">Seleccione **Crear.</span><span class="sxs-lookup"><span data-stu-id="43b94-139">Select **Create.</span></span> <span data-ttu-id="43b94-140">La finalización correcta aparece en las **notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="43b94-140">Successful completion appears in the **notifications**</span></span>
1. <span data-ttu-id="43b94-141">Seleccione la aplicación web recién creada: **WebApp-GraphAPI-DirectoryExtensions**.</span><span class="sxs-lookup"><span data-stu-id="43b94-141">Select the newly created web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
1. <span data-ttu-id="43b94-142">Seleccione la configuración de **Permisos necesarios**.</span><span class="sxs-lookup"><span data-stu-id="43b94-142">Select Settings: **Required permissions**</span></span>
1. <span data-ttu-id="43b94-143">Seleccione la API **Windows Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="43b94-143">Select API **Windows Active Directory**</span></span>
1. <span data-ttu-id="43b94-144">Coloque una marca en los permisos de aplicación **Leer y escribir en datos de directorio** y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="43b94-144">Place a checkmark in Application Permissions: **Read and write directory data**, and **Save**</span></span>
1. <span data-ttu-id="43b94-145">Seleccione **Conceder permisos** y haga clic en **Sí** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="43b94-145">Choose **Grant permissions** and confirm **Yes**.</span></span>
1. <span data-ttu-id="43b94-146">Realice la copiar en el Portapapeles y guarde los siguientes identificadores de WebApp-GraphAPI-DirectoryExtensions > Configuración > Propiedades ></span><span class="sxs-lookup"><span data-stu-id="43b94-146">Copy to your clipboard and save the following identifiers from WebApp-GraphAPI-DirectoryExtensions>Settings>Properties></span></span>
*  <span data-ttu-id="43b94-147">**Identificador de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="43b94-147">**Application ID** .</span></span> <span data-ttu-id="43b94-148">Ejemplo: `103ee0e6-f92d-4183-b576-8c3739027780`</span><span class="sxs-lookup"><span data-stu-id="43b94-148">Example: `103ee0e6-f92d-4183-b576-8c3739027780`</span></span>
* <span data-ttu-id="43b94-149">**Identificador de objeto**.</span><span class="sxs-lookup"><span data-stu-id="43b94-149">**Object ID**.</span></span> <span data-ttu-id="43b94-150">Ejemplo: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span><span class="sxs-lookup"><span data-stu-id="43b94-150">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span></span>



## <a name="modifying-your-custom-policy-to-add-the-applicationobjectid"></a><span data-ttu-id="43b94-151">Modificación de una directiva personalizada para agregar ApplicationObjectId</span><span class="sxs-lookup"><span data-stu-id="43b94-151">Modifying your custom policy to add the ApplicationObjectId</span></span>

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
><span data-ttu-id="43b94-152"><TechnicalProfile Id="AAD-Common"> es "común", porque sus elementos están incluidos y se reutilizan en todas las instancias de TechnicalProfiles de Azure Active Directory mediante el elemento: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span><span class="sxs-lookup"><span data-stu-id="43b94-152">The <TechnicalProfile Id="AAD-Common"> is referred to as "common" because its elements are included in and reused in all the Azure Active Directory TechnicalProfiles by using the element: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span></span>

>[!NOTE]
><span data-ttu-id="43b94-153">La primera vez que la instancia de TechnicalProfile escribe en la propiedad de extensión recién creada, puede surgir un error que se da una sola vez.</span><span class="sxs-lookup"><span data-stu-id="43b94-153">When the TechnicalProfile writes for the first time to the newly created extension property, you may experience a one-time error.</span></span>  <span data-ttu-id="43b94-154">La propiedad de extensión se crea la primera vez que se utiliza.</span><span class="sxs-lookup"><span data-stu-id="43b94-154">The extension property is created the first time it is used.</span></span>  

## <a name="using-the-new-extension-property--custom-attribute-in-a-user-journey"></a><span data-ttu-id="43b94-155">Uso de la nueva propiedad de extensión o atributo personalizado en un recorrido del usuario</span><span class="sxs-lookup"><span data-stu-id="43b94-155">Using the new extension property / custom attribute in a user journey</span></span>


1. <span data-ttu-id="43b94-156">Abra el archivo del usuario de confianza (RP) que describe el recorrido del usuario de edición de la directiva.</span><span class="sxs-lookup"><span data-stu-id="43b94-156">Open the Relying Party(RP) file that describes your policy edit user journey.</span></span>  <span data-ttu-id="43b94-157">Si va a empezar, es posible que sea aconsejable descargar la versión ya configurada del archivo RP-PolicyEdit directamente de la sección Directiva de Azure B2C personalizada de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="43b94-157">If you are starting out, it may be advisable to download your already configured version of the RP-PolicyEdit file directly from the Azure B2C Custom Policy section in the Azure portal.</span></span>  <span data-ttu-id="43b94-158">Como alternativa, abra el archivo XML desde la carpeta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="43b94-158">Alternatively, open your XML file from your storage folder.</span></span>
2. <span data-ttu-id="43b94-159">Agregue una notificación personalizada `loyaltyId`.</span><span class="sxs-lookup"><span data-stu-id="43b94-159">Add a custom claim `loyaltyId`.</span></span>  <span data-ttu-id="43b94-160">Mediante la inclusión de la notificación personalizada en el elemento `<RelyingParty>`, se usa como en UserJourney TechnicalProfiles y se incluye en el token de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="43b94-160">By including the custom claim in the `<RelyingParty>` element, it is passed as a parameter to the UserJourney TechnicalProfiles and included in the token for the application.</span></span>
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
3. <span data-ttu-id="43b94-161">Agregue una definición de la notificación al archivo de la directiva de extensión `TrustFrameworkExtensions.xml` del elemento `<ClaimsSchema>` como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="43b94-161">Add a claim definition to the Extension policy file  `TrustFrameworkExtensions.xml` inside the `<ClaimsSchema>` element as shown.</span></span>
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
4. <span data-ttu-id="43b94-162">Agregue la misma definición de la notificación al archivo de la directiva base `TrustFrameworkBase.xml`.</span><span class="sxs-lookup"><span data-stu-id="43b94-162">Add the same claim definition to the Base policy file `TrustFrameworkBase.xml`.</span></span>  
><span data-ttu-id="43b94-163">Normalmente no es preciso agregar una definición `ClaimType` tanto en el archivo base como en el archivo de extensiones, pero dado que los siguientes pasos agregarán extension_loyaltyId a TechnicalProfiles en el archivo base, el validador de la directiva rechazará la carga del archivo base si no la tiene.</span><span class="sxs-lookup"><span data-stu-id="43b94-163">Adding a `ClaimType` definition in both the base and the extensions file is normally not necessary, however since the next steps will add the extension_loyaltyId to TechnicalProfiles in the Base file, the policy validator will reject the upload of the base file without it.</span></span>
><span data-ttu-id="43b94-164">Es posible que sea útil realizar un seguimiento de la ejecución del recorrido del usuario denominado "ProfileEdit" del archivo TrustFrameworkBase.xml.</span><span class="sxs-lookup"><span data-stu-id="43b94-164">It may be useful to trace the execution of the user journey named "ProfileEdit" in the TrustFrameworkBase.xml file.</span></span>  <span data-ttu-id="43b94-165">Busque el recorrido del usuario que tenga el mismo nombre en el editor y observe que en el paso 5 de la orquestación se invoca a TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span><span class="sxs-lookup"><span data-stu-id="43b94-165">Search for the user journey of the same name in your editor and observe that Orchestration Step 5 invokes the TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span></span>  <span data-ttu-id="43b94-166">Busque e inspeccione esta instancia de TechnicalProfile para familiarizarse con el flujo.</span><span class="sxs-lookup"><span data-stu-id="43b94-166">Search and inspect this TechnicalProfile to familiarize yourself with the flow.</span></span>
5. <span data-ttu-id="43b94-167">Agregue loyaltyId como notificación de entrada y salida en la instancia de TechnicalProfile "SelfAsserted ProfileUpdate"</span><span class="sxs-lookup"><span data-stu-id="43b94-167">Add loyaltyId as input and output claim in the TechnicalProfile "SelfAsserted-ProfileUpdate"</span></span>
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

            <!-- Optional claims. These claims are collected from the user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written to directory after being updateed by the user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from the user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written to directory after being updateed by the user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. <span data-ttu-id="43b94-168">Agregue la notificación de TechnicalProfile "AAD-UserWriteProfileUsingObjectId" para conservar el valor de la notificación en la propiedad de extensión del usuario actual en el directorio.</span><span class="sxs-lookup"><span data-stu-id="43b94-168">Add claim in TechnicalProfile "AAD-UserWriteProfileUsingObjectId" to persist the value of the claim in the extension property, for the current user in the directory.</span></span>
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
7. <span data-ttu-id="43b94-169">Agregue la notificación de TechnicalProfile "AAD-UserReadUsingObjectId" para leer el valor del atributo de extensión cada vez que un usuario inicia sesión.</span><span class="sxs-lookup"><span data-stu-id="43b94-169">Add claim in TechnicalProfile "AAD-UserReadUsingObjectId" to read the value of the extension attribute every time a user logs in.</span></span> <span data-ttu-id="43b94-170">Hasta ahora las instancias de TechnicalProfiles solo se han cambiado en el flujo de las cuentas locales.</span><span class="sxs-lookup"><span data-stu-id="43b94-170">Thus far the TechnicalProfiles have been changed in the flow of local accounts only.</span></span>  <span data-ttu-id="43b94-171">Si el nuevo atributo se desea en el flujo de una cuenta social o federada, es preciso cambiar otro conjunto de instancias de TechnicalProfiles.</span><span class="sxs-lookup"><span data-stu-id="43b94-171">If the new attribute is desired in the flow of a social/federated account, a different set of TechnicalProfiles needs to be changed.</span></span> <span data-ttu-id="43b94-172">Consulte los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="43b94-172">See Next Steps.</span></span>

```xml
<!-- The following technical profile is used to read data after user authenticates. -->
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
><span data-ttu-id="43b94-173">El elemento IncludeTechnicalProfile agrega todos los elementos de AAD-Common a esta instancia de TechnicalProfile.</span><span class="sxs-lookup"><span data-stu-id="43b94-173">The IncludeTechnicalProfile element adds all the elements of AAD-Common to this TechnicalProfile.</span></span>

## <a name="test-the-custom-policy-using-run-now"></a><span data-ttu-id="43b94-174">Prueba de la directiva personalizada con "Ejecutar ahora"</span><span class="sxs-lookup"><span data-stu-id="43b94-174">Test the custom policy using "Run Now"</span></span>
1. <span data-ttu-id="43b94-175">Abra la **hoja de Azure AD B2C** y vaya a **Marco de experiencia de identidad > Directivas personalizadas**.</span><span class="sxs-lookup"><span data-stu-id="43b94-175">Open the **Azure AD B2C Blade** and navigate to **Identity Experience Framework > Custom policies**.</span></span>
1. <span data-ttu-id="43b94-176">Seleccione la directiva personalizada que cargó y, luego, haga clic en el botón **Ejecutar ahora**.</span><span class="sxs-lookup"><span data-stu-id="43b94-176">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
1. <span data-ttu-id="43b94-177">Debe poder registrarse con una dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="43b94-177">You should be able to sign up using an email address.</span></span>

<span data-ttu-id="43b94-178">El token del identificador que se devuelve a la aplicación incluirá la nueva propiedad de extensión como notificación personalizada precedida por extension_loyaltyId.</span><span class="sxs-lookup"><span data-stu-id="43b94-178">The  id token sent back to your application includes the new extension property as a custom claim preceded by extension_loyaltyId.</span></span> <span data-ttu-id="43b94-179">Vea el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="43b94-179">See example.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="43b94-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="43b94-180">Next steps</span></span>

<span data-ttu-id="43b94-181">Agregue la nueva notificación a los flujos de inicios de sesión de cuentas sociales cambiando las instancias de TechnicalProfiles que aparecen.</span><span class="sxs-lookup"><span data-stu-id="43b94-181">Add the new claim to the flows for social account logins by changing the TechnicalProfiles listed.</span></span> <span data-ttu-id="43b94-182">Estas dos instancias de TechnicalProfiles las usan los inicios de sesión de cuentas sociales o federadas para leer y escribir los datos de usuario, para lo que usan alternativeSecurityId como localizador del objeto de usuario.</span><span class="sxs-lookup"><span data-stu-id="43b94-182">These two TechnicalProfiles are used by social/federated account logins to write and read the user data using the alternativeSecurityId as the locator of the user object.</span></span>
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

<span data-ttu-id="43b94-183">Se usan los mismos atributos de extensión entre directivas integradas y personalizadas.</span><span class="sxs-lookup"><span data-stu-id="43b94-183">Using the same extension attributes between built-in and custom policies.</span></span>
<span data-ttu-id="43b94-184">Cuando se agregan atributos de extensión (también conocidos como atributos personalizados) a través de la experiencia del portal, los atributos se registran mediante **b2c-extensions-app que existe en cada inquilino b2c.</span><span class="sxs-lookup"><span data-stu-id="43b94-184">When you add extension attributes (aka custom attributes) via the portal experience, those attributes are registered using the **b2c-extensions-app that exists in every b2c tenant.</span></span>  <span data-ttu-id="43b94-185">Para usar estos atributos de extensión en la directiva personalizada:</span><span class="sxs-lookup"><span data-stu-id="43b94-185">To use these extension attributes in your custom policy:</span></span>
1. <span data-ttu-id="43b94-186">En el inquilino b2c en portal.azure.com, vaya a **Azure Active Directory** y seleccione **Registros de aplicaciones**</span><span class="sxs-lookup"><span data-stu-id="43b94-186">Within your b2c tenant in portal.azure.com, navigate to **Azure Active Directory** and select **App registrations**</span></span>
2. <span data-ttu-id="43b94-187">Encuentre su **b2c-extensiones-app** y selecciónelo</span><span class="sxs-lookup"><span data-stu-id="43b94-187">Find your **b2c-extensions-app** and select it</span></span>
3. <span data-ttu-id="43b94-188">En "Información esencial" anote el **Identificador de la aplicación** y el **Identificador del objeto**</span><span class="sxs-lookup"><span data-stu-id="43b94-188">Under 'Essentials' record the **Application ID** and the **Object ID**</span></span>
4. <span data-ttu-id="43b94-189">Inclúyalos en sus metadatos de perfil técnico de AAD-Common de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="43b94-189">Include them in your AAD-Common Technical profile metadata like as follows:</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is the "Object ID" from the "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is the "Application ID" from the "b2c-extensions-app"-->
              </Metadata>
```

<span data-ttu-id="43b94-190">Para mantener la consistencia con la experiencia del portal, cree estos atributos utilizando la interfaz de usuario del portal *antes* de usarlos en sus directivas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="43b94-190">To keep consistency with the portal experience, create these attributes using the portal UI *before* you use them in your custom policies.</span></span>  <span data-ttu-id="43b94-191">Cuando se crea un atributo "ActivationStatus" en el portal, tiene que hacer referencia a él como sigue:</span><span class="sxs-lookup"><span data-stu-id="43b94-191">When you create an attribute "ActivationStatus" in the portal, you must refer to it as follows:</span></span>

```
extension_ActivationStatus in the custom policy
extension_<app-guid>_ActivationStatus via the Graph API.
```


## <a name="reference"></a><span data-ttu-id="43b94-192">Referencia</span><span class="sxs-lookup"><span data-stu-id="43b94-192">Reference</span></span>

* <span data-ttu-id="43b94-193">Un **perfil técnico (TP)** es un tipo de elemento que se puede considerar una *función* que define el nombre de un punto de conexión, sus metadatos y su protocolo, y que detalla el intercambio de notificaciones que el marco de experiencia de identidad debe realizar.</span><span class="sxs-lookup"><span data-stu-id="43b94-193">A **Technical Profile (TP)** is an element type that can be thought of as a *function* that defines an endpoint’s name, its metadata, its protocol, and details the exchange of claims that the Identity Experience Framework should perform.</span></span>  <span data-ttu-id="43b94-194">Cuando se llama a esta *función* en un paso de la orquestación o desde otra instancia de TechnicalProfile, quien realiza la llamada especifica InputClaims y OutputClaims como parámetros.</span><span class="sxs-lookup"><span data-stu-id="43b94-194">When this *function* is called in an orchestration step or from another TechnicalProfile, the InputClaims and OutputClaims are provided as parameters by the caller.</span></span>


* <span data-ttu-id="43b94-195">En el artículo [Extensiones de esquema de directorio | Conceptos de la API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) se tratan exhaustivamente las propiedades de extensión.</span><span class="sxs-lookup"><span data-stu-id="43b94-195">For full treatment on extension properties, see the article [DIRECTORY SCHEMA EXTENSIONS | GRAPH API CONCEPTS](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span></span>

>[!NOTE]
><span data-ttu-id="43b94-196">Los atributos de extensión en la API Graph se denominan mediante la convención `extension_ApplicationObjectID_attributename`.</span><span class="sxs-lookup"><span data-stu-id="43b94-196">Extension attributes in Graph API are named using the convention `extension_ApplicationObjectID_attributename`.</span></span> <span data-ttu-id="43b94-197">Las directivas personalizadas hacen referencia a los atributos de extensión como extension_attributename, con lo que se omite ApplicationObjectId en el archivo XML</span><span class="sxs-lookup"><span data-stu-id="43b94-197">Custom policies refer to extensions attributes as extension_attributename, thus omitting the ApplicationObjectId in the XML</span></span>
