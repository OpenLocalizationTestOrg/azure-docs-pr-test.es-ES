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
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a>Azure Active Directory B2C: creación y uso de atributos personalizados en una directiva de edición de perfil personalizada

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

En este artículo, crear un atributo personalizado en el directorio de Azure AD B2C y usar este nuevo atributo como una demanda personalizada en viaje de usuario de edición de perfil de Hola.

## <a name="prerequisites"></a>Requisitos previos

Hola completa los pasos en el artículo hello [Introducción a las directivas personalizadas](active-directory-b2c-get-started-custom.md).

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a>Utilizar atributos personalizados toocollect información acerca de los clientes en Azure Active Directory B2C mediante directivas personalizadas
El directorio de Azure Active Directory (Azure AD) B2C incluye un conjunto integrado de atributos: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  A menudo necesitan toocreate sus propios atributos.  Por ejemplo:
* Una aplicación orientado al cliente necesita toopersist un atributo como "LoyaltyNumber."
* Un proveedor de identidades tiene un identificador de usuario único que se debe guardar como "uniqueUserGUID"".
* Un viaje de usuario personalizado necesita toopersist Hola estado de usuario como "migrationStatus."

Con Azure AD B2C, puede ampliar el conjunto de Hola de atributos que se almacenan en cada cuenta de usuario. También puede leer y escribir estos atributos mediante hello [API de Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).

Propiedades de extensión extienden esquema Hola Hola de objetos de usuario en el directorio de Hola.  propiedad de extensión de términos de Hello, atributos personalizados y notificaciones personalizadas, consulte toohello lo mismo en el contexto de Hola de este nombre de artículo y Hola varía según el contexto de hello (aplicación, objeto de directiva).

Las propiedades de extensión solo se pueden registrar en un objeto de aplicación, aunque pueden contener datos de un usuario. propiedad Hello es aplicación toohello adjunto. objeto de la aplicación Hello debe ser concedido acceso de escritura tooregister una propiedad de extensión. Propiedades de extensión de 100 (a través de todos los tipos y todas las aplicaciones) pueden escribirse tooany único objeto. Propiedades de extensión se agregan toohello tipo de directorio de destino y pasa a estar accesibles inmediatamente en el inquilino de directorio de hello Azure AD B2C.
Si se elimina la aplicación hello, también se quitan las propiedades de extensión junto con los datos contenidos en ellas para todos los usuarios. Si se elimina una propiedad de extensión Hola aplicación, se quita en hello los objetos de directorio de destino y Hola valores eliminados.

Propiedades de extensión solo existen en contexto de Hola de una aplicación registrada en el inquilino de Hola. Id. de objeto de saludo de la aplicación debe incluirse en hello TechnicalProfile que lo usan.

>[!NOTE]
>directorio de Hello Azure AD B2C normalmente incluye una aplicación Web denominada `b2c-extensions-app`.  Esta aplicación se usa principalmente por directivas integradas de hello b2c notificaciones personalizadas de hello creado a través del portal de Azure Hola.  Se recomienda usar este extensiones tooregister de aplicación de directivas personalizadas de b2c sólo para usuarios avanzados.  Se incluyen instrucciones para esto en hello sección pasos siguientes en este artículo.


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a>Crear un nuevo toostore aplicación propiedades de extensión de Hola

1. Abra una sesión de exploración y desplácese toohello [PuertoA Azure](https://portal.azure.com) e inicie sesión con credenciales administrativas de hello Directory B2C desea tooconfigure.
1. Haga clic en **Azure Active Directory** en el menú de navegación izquierdo de Hola. Puede que necesite toofind seleccionando más atiende >.
1. Seleccione **Registros de aplicaciones** y haga clic en **Nuevo registro de aplicaciones**.
1. Proporcionar siguiente Hola recomienda entradas:
  * Especifique un nombre para la aplicación web de hello: **WebApp-GraphAPI-DirectoryExtensions**
  * Tipo de aplicación: aplicación web o API
  * URL de inicio de sesión: https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions
1. Seleccione **Crear. Finalización correcta aparece en hello **notificaciones**
1. Seleccione aplicación web de hello recién creado: **WebApp-GraphAPI-DirectoryExtensions**
1. Seleccione la configuración de **Permisos necesarios**.
1. Seleccione la API **Windows Active Directory**.
1. Coloque una marca en los permisos de aplicación **Leer y escribir en datos de directorio** y seleccione **Guardar**.
1. Seleccione **Conceder permisos** y haga clic en **Sí** para confirmar.
1. Copie tooyour Portapapeles y guarde Hola siguientes identificadores de WebApp-GraphAPI-DirectoryExtensions > Configuración > Propiedades >
*  **Identificador de aplicación**. Ejemplo: `103ee0e6-f92d-4183-b576-8c3739027780`
* **Identificador de objeto**. Ejemplo: `80d8296a-da0a-49ee-b6ab-fd232aa45201`



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a>Modificar el Hola de tooadd ApplicationObjectId de directivas personalizadas

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
>Hola <TechnicalProfile Id="AAD-Common"> es tooas que se hace referencia "comunes" porque sus elementos se incluye en y volver a usar en todos los hello TechnicalProfiles de Azure Active Directory mediante el elemento de hello:`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`

>[!NOTE]
>Cuando hello TechnicalProfile escribe para la propiedad de extensión de hello primer tiempo toohello recién creado, puede experimentar un error de un solo uso.  propiedad de extensión de Hola se crea Hola primera vez que se utilice.  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a>Con la nueva propiedad de extensión Hola / atributo personalizado en un viaje de usuario


1. Hola abrir archivo de confianza Party(RP) que describe la directiva de edición viaje de usuario.  Si está iniciando, puede ser aconsejable toodownload su versión ya configurado de Hola RP-PolicyEdit archivo directamente desde Hola sección directiva personalizada de Azure B2C Hola portal de Azure.  Como alternativa, abra el archivo XML desde la carpeta de almacenamiento.
2. Agregue una notificación personalizada `loyaltyId`.  Mediante la inclusión de saludo personalizado de notificación en hello `<RelyingParty>` elemento, se pasa como un toohello parámetro UserJourney TechnicalProfiles e incluido en el símbolo (token) de hello para la aplicación hello.
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
3. Agregar un archivo de directiva de extensión de notificación definición toohello `TrustFrameworkExtensions.xml` dentro de hello `<ClaimsSchema>` elemento tal como se muestra.
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
4. Agregar Hola mismo archivo de definición de directiva Base toohello de notificación `TrustFrameworkBase.xml`.  
>Agregar un `ClaimType` definición en la base de Hola y el archivo de extensiones de hello normalmente no es necesario, sin embargo, puesto que los pasos siguientes de hello agregará hello extension_loyaltyId tooTechnicalProfiles en el archivo de Base de hello, el validador de directiva Hola rechazará carga Hola del archivo de base de hello sin él.
>Puede ser útil tootrace ejecución de Hola de hello usuario viaje denominado "ProfileEdit" en el archivo de hello TrustFrameworkBase.xml.  Busque el viaje de usuario de Hola de hello mismo nombre en el editor y observe que la orquestación paso 5 invoca hello TechnicalProfileReferenceID = "SelfAsserted ProfileUpdate".  Buscar e inspeccionar este toofamiliarize TechnicalProfile con flujo de Hola.
5. Agregar loyaltyId como notificaciones de entrada y salida de hello TechnicalProfile "SelfAsserted ProfileUpdate"
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
6. Agregar notificación de valor de hello TechnicalProfile "AAD UserWriteProfileUsingObjectId" toopersist de notificación de hello en la propiedad de extensión de hello, para el usuario actual de hello en el directorio de Hola.
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
7. Agregar notificación de valor de hello TechnicalProfile "AAD UserReadUsingObjectId" tooread del atributo de extensión de Hola cada vez que un usuario inicia sesión. Hasta ahora hello TechnicalProfiles se han cambiado en el flujo de Hola de cuentas locales solo.  Si se desea el nuevo atributo de hello en flujo de Hola de una cuenta de social/federada, un conjunto diferente de TechnicalProfiles debe toobe cambiado. Consulte los pasos siguientes.

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
>elemento de Hello IncludeTechnicalProfile agrega todos los elementos de Hola de AAD común toothis TechnicalProfile.

## <a name="test-hello-custom-policy-using-run-now"></a>Probar directiva personalizada de hello mediante "Run Now"
1. Hola abierto **hoja de Azure AD B2C** y navegue demasiado**identidad experiencia Framework > directivas personalizado**.
1. Active la directiva personalizada hello que ha cargado y haga clic en hello **ejecutar ahora** botón.
1. Debe ser capaz de toosign utilizando una dirección de correo electrónico.

token de Id. de Hello devolvió tooyour aplicación incluye nueva propiedad de extensión hello como una demanda personalizada precedida por extension_loyaltyId. Vea el ejemplo.

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

## <a name="next-steps"></a>Pasos siguientes

Agregar nueva notificación toohello flujos de Hola para inicios de sesión de cuenta sociales cambiando hello TechnicalProfiles enumerados. Estos dos TechnicalProfiles son utilizados por toowrite de inicios de sesión de cuenta de social/federada y leer datos de usuario de hello mediante hello alternativeSecurityId como Hola localizador Hola del objeto de usuario.
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

Usar Hola mismos atributos de extensión entre directivas integradas y personalizadas.
Cuando se agregan atributos de extensión (también conocido como atributos personalizados) a través de la experiencia del portal hello, estos atributos se registran utilizando Hola ** b2c extensiones de aplicación que existe en cada inquilino b2c.  toouse estos atributos de extensión de la directiva personalizada:
1. En el inquilino b2c en portal.azure.com, desplazarse demasiado**Azure Active Directory** y seleccione **registros de aplicación**
2. Encuentre su **b2c-extensiones-app** y selecciónelo
3. En Hola de registro 'Essentials' **Id. de aplicación** hello y **Id. de objeto**
4. Inclúyalos en sus metadatos de perfil técnico de AAD-Common de la siguiente forma:

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

tookeep coherencia con la experiencia del portal hello, crear estos atributos mediante la interfaz de usuario del portal de Hola *antes de* usarlos en sus directivas personalizadas.  Cuando se crea un atributo "ActivationStatus" en el portal de hello, debe hacer referencia tooit como se indica a continuación:

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a>Referencia

* A **perfil técnica (TP)** es un tipo de elemento que puede considerarse como un *función* que define el nombre de un punto de conexión, sus metadatos y su protocolo y detalles Hola Intercambio de notificaciones que Hola identidad Experiencia Framework debe realizar.  Cuando esto *función* se invoca en un paso de orquestación o desde otro TechnicalProfile, hello InputClaims y OutputClaims se proporcionan como parámetros de llamada de Hola.


* Para tratar de forma completa en las propiedades de extensión, vea el artículo de hello [extensiones de esquema de directorio | CONCEPTOS DE API GRAPH](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)

>[!NOTE]
>Atributos de extensión en la API Graph se denominan con convención de hello `extension_ApplicationObjectID_attributename`. Directivas personalizadas, consulte tooextensions atributos como extension_attributename, omitir, por tanto, hello ApplicationObjectId Hola XML
