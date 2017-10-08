---
title: "Azure Active Directory B2C: intercambios de notificaciones de API de REST como paso de orquestación | Microsoft Docs"
description: Tema sobre las directivas personalizadas de Azure Active Directory B2C que se integran con una API
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/24/2017
ms.author: joroja
ms.openlocfilehash: 90a495029f48d70232ef3f99de4ea4d351395aa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a>Tutorial: Integración de intercambios de notificaciones de API de REST en los recorridos de usuario de Azure AD B2C como un paso de orquestación

Hola Framework de experiencia de identidad (IEF) que subyace a Azure Active Directory B2C (Azure AD B2C) permite Hola identidad developer toointegrate una interacción con la API de REST en un viaje de usuario.  

Al final de Hola de este tutorial, será capaz de toocreate un viaje de usuario de Azure AD B2C que interactúa con los servicios RESTful.

Hola IEF envía datos en las notificaciones y recibe los datos en las notificaciones. Hola exchange de notificaciones de API de REST:

- Puede diseñarse como un paso de orquestación.
- Puede desencadenar una acción externa. Por ejemplo, puede registrar un evento en una base de datos externa.
- Puede ser toofetch usa un valor y, a continuación, almacenarla en la base de datos de usuario de Hola.

Puede usar notificaciones de hello recibido posterior toochange Hola flujo de la ejecución.

También puede diseñar interacción Hola como un perfil de validación. Para obtener más información, vea [Tutorial: Integración de intercambios de notificaciones de API de REST en los recorridos de usuario de Azure AD B2C como validación en entradas de usuario](active-directory-b2c-rest-api-validation-custom.md).

escenario de Hello es que cuando un usuario realiza una operación de edición perfil, deseamos:

1. Buscar usuario hello en un sistema externo.
2. Obtener ciudad Hola donde se registra que el usuario.
3. Devolver esa aplicación toohello de atributo como una notificación.

## <a name="prerequisites"></a>Requisitos previos

- Un toocomplete de Azure AD B2C inquilino configura una cuenta local de sesión-up/inicio de sesión de, como se describe en [Introducción](active-directory-b2c-get-started-custom.md).
- Un punto de conexión de API de REST toointeract con. Este tutorial usa como ejemplo un webhook simple de la aplicación de función de Azure.
- *Se recomienda*: Hola completa [tutorial de exchange como un paso de validación de notificaciones de la API de REST](active-directory-b2c-rest-api-validation-custom.md).

## <a name="step-1-prepare-hello-rest-api-function"></a>Paso 1: Preparar la función de la API de REST de Hola

> [!NOTE]
> El programa de instalación de funciones de la API de REST está fuera de ámbito de Hola de este artículo. [Las funciones de Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) proporciona un Kit de herramientas de excelente toocreate servicios RESTful en nube Hola.

Hemos configurado con una función de Azure que recibe una notificación que se llama `email`, y, a continuación, devuelve Hola notificación `city` con valor de hello asignado de `Redmond`. ejemplo de Hola función Azure está en [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).

Hola `userMessage` notificación que Hola devueltos de funciones de Azure es opcional en este contexto y hello IEF pasará por alto. Potencialmente puede usarlo como un mensaje pasa la aplicación toohello y presenta toohello usuario más adelante.

```csharp
if (requestContentAsJObject.email == null)
{
    return request.CreateResponse(HttpStatusCode.BadRequest);
}

var email = ((string) requestContentAsJObject.email).ToLower();

return request.CreateResponse<ResponseContent>(
    HttpStatusCode.OK,
    new ResponseContent
    {
        version = "1.0.0",
        status = (int) HttpStatusCode.OK,
        userMessage = "User Found",
        city = "Redmond"
    },
    new JsonMediaTypeFormatter(),
    "application/json");
```

Una aplicación de Azure función hace fácil tooget Hola función URL, que incluye el identificador hello de función específicos de Hola. En este caso, es la dirección URL de hello: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==. Puede usarla para realizar pruebas.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a>Paso 2: Configurar exchange de notificaciones de API de REST de Hola como un perfil técnico en el archivo TrustFrameworExtensions.xml

Un perfil técnico es la configuración completa de Hola de exchange Hola deseado con hello servicio RESTful. Abra el archivo de TrustFrameworkExtensions.xml hello y agregue Hola siguiente fragmento XML dentro de hello `<ClaimsProvider>` elemento.

> [!NOTE]
> Hola continuación de XML, proveedor RESTful `Version=1.0.0.0` se describe como protocolo de Hola. Considérelo como función hello que interactúa con el servicio externo de Hola. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```XML
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-LookUpLoyaltyWebHook">
            <DisplayName>Check LookUpLoyalty Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="email" />
            </InputClaims>
            <OutputClaims>
                <OutputClaim ClaimTypeReferenceId="city" PartnerClaimType="city" />
            </OutputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

Hola `<InputClaims>` elemento define notificaciones de Hola que se enviarán desde Hola servicio REST de IEF toohello. En este ejemplo, Hola contenido de notificación de hello `givenName` enviarán servicio REST de toohello como notificación de hello `email`.  

Hola `<OutputClaims>` elemento define Hola notificaciones que hello IEF esperará de servicio REST de Hola. Independientemente del número de Hola de notificaciones que se reciben, hello IEF utilizará sólo aquellas identificado aquí. En este ejemplo, se recibe una notificación como `city` tooan asignada IEF notificación llamará `city`.

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a>Paso 3: Agregar nueva notificación de hello `city` toohello esquema del archivo TrustFrameworkExtensions.xml

notificación de Hello `city` todavía no está definido en cualquier lugar en el esquema. Por lo tanto, agregar una definición de elemento de hello `<BuildingBlocks>`. Puede encontrar este elemento al principio de hello del archivo de hello TrustFrameworkExtensions.xml.

```XML
<BuildingBlocks>
    <!--hello claimtype city must be added toohello TrustFrameworkPolicy-->
    <!-- You can add new claims in hello BASE file Section III, or in hello extensions file-->
    <ClaimsSchema>
        <ClaimType Id="city">
            <DisplayName>City</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your city</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
    </ClaimsSchema>
</BuildingBlocks>
```

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a>Paso 4: Incluir el intercambio de notificaciones del servicio de REST de Hola como un paso de orquestación en su viaje de usuario de edición de perfil en TrustFrameworkExtensions.xml

Agregar un paso de viaje de usuario de edición de perfil toohello, después de haber usuario Hola autenticado (pasos 1 a 4 de orquestación en hello continuación de XML) y usuario de hello ha proporcionado información de perfil de hello actualizado (paso 5).

> [!NOTE]
> Hay muchos casos donde hello llamada API de REST puede usarse como un paso de la orquestación. Como un paso de la orquestación, que puede usarse como un sistema externo de tooan de actualización después de que un usuario se haya completado correctamente una tarea como registro por primera vez, o como un perfil de actualización sincronizada la información de tookeep. En este caso, es la información de hello tooaugment usado proporcionada toohello aplicación después de editar el perfil de Hola.

Copiar Hola perfil editar código de usuario viaje XML de hello TrustFrameworkBase.xml tooyour TrustFrameworkExtensions.xml archivo dentro de hello `<UserJourneys>` elemento. A continuación, asegúrese de modificación de hello en el paso 6.

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> Si el orden de hello no coincide con su versión, asegúrese de que inserte código de hello como paso Hola antes de Hola `ClaimsExchange` tipo `SendClaims`.

Hello debe ser XML final para viaje de usuario de hello similar al siguiente:

```XML
<UserJourney Id="ProfileEdit">
    <OrchestrationSteps>
        <OrchestrationStep Order="1" Type="ClaimsProviderSelection" ContentDefinitionReferenceId="api.idpselections">
            <ClaimsProviderSelections>
                <ClaimsProviderSelection TargetClaimsExchangeId="FacebookExchange" />
                <ClaimsProviderSelection TargetClaimsExchangeId="LocalAccountSigninEmailExchange" />
            </ClaimsProviderSelections>
        </OrchestrationStep>
        <OrchestrationStep Order="2" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="FacebookExchange" TechnicalProfileReferenceId="Facebook-OAUTH" />
                <ClaimsExchange Id="LocalAccountSigninEmailExchange" TechnicalProfileReferenceId="SelfAsserted-LocalAccountSignin-Email" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="3" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>localAccountAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserRead" TechnicalProfileReferenceId="AAD-UserReadUsingAlternativeSecurityId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="4" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>socialIdpAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserReadWithObjectId" TechnicalProfileReferenceId="AAD-UserReadUsingObjectId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="5" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="B2CUserProfileUpdateExchange" TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <!-- Add a step 6 toohello user journey before hello JWT token is created-->
        <OrchestrationStep Order="6" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="7" Type="SendClaims" CpimIssuerTechnicalProfileReferenceId="JwtIssuer" />
    </OrchestrationSteps>
    <ClientDefinition ReferenceId="DefaultWeb" />
</UserJourney>
```

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a>Paso 5: Agregar notificación de hello `city` para notificación de Hola se envía la aplicación tooyour de los archivos de directiva de entidad de confianza de tooyour

Edite el archivo de entidad (RP) de confianza de ProfileEdit.xml y modificar hello `<TechnicalProfile Id="PolicyProfile">` siguiente de elemento tooadd Hola: `<OutputClaim ClaimTypeReferenceId="city" />`.

Después de agregar la nueva notificación de hello, perfil técnico hello tiene este aspecto:

```XML
<DisplayName>PolicyProfile</DisplayName>
    <Protocol Name="OpenIdConnect" />
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <SubjectNamingInfo ClaimType="sub" />
</TechnicalProfile>
```

## <a name="step-6-upload-your-changes-and-test"></a>Paso 6: Carga de los cambios y prueba

Sobrescribir las versiones existentes de directiva de Hola Hola.

1.  (Opcional:) Guardar la versión existente de hello (mediante la descarga) del archivo extensiones antes de continuar. tookeep Hola inicial complejidad baja, se recomienda que no cargar varias versiones de archivo de las extensiones de hello.
2.  (Opcional:) Cambiar el nombre de nueva versión de hello de Id. de directiva de Hola para editar archivo de directiva de hello cambiando `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.
3.  Cargar archivo de extensiones de hello.
4.  Cargar archivo de RP de edición de directivas de Hola.
5.  Use **ejecutar ahora** tootest directiva de Hola. Token de Hola de revisión que Hola IEF devuelve toohello aplicación.

Si todo está configurado correctamente, el token de hello incluirá nueva notificación de hello `city`, con el valor de hello `Redmond`.

```JSON
{
  "exp": 1493053292,
  "nbf": 1493049692,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493049692,
  "auth_time": 1493049692,
  "city": "Redmond"
}
```

## <a name="next-steps"></a>Pasos siguientes

[Uso de una API de REST como paso de validación](active-directory-b2c-rest-api-validation-custom.md)

[Modificar Hola perfil editar toogather información adicional de los usuarios](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
