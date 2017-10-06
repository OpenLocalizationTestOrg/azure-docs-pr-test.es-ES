---
title: "Azure Active Directory B2C: intercambios de notificaciones de API de REST como validación | Microsoft Docs"
description: Un tema acerca de las directivas personalizadas de Azure Active Directory B2C
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
ms.openlocfilehash: cec6c6e110514a8bbe0e0780f36738ff21ae2f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a>Tutorial: Integración de intercambios de notificaciones de API de REST en el recorrido del usuario de Azure AD B2C como validación en entradas de usuario

Hola Framework de experiencia de identidad (IEF) que subyace a Azure Active Directory B2C (Azure AD B2C) permite Hola identidad developer toointegrate una interacción con la API de REST en un viaje de usuario.  

Al final de Hola de este tutorial, será capaz de toocreate un viaje de usuario de Azure AD B2C que interactúa con los servicios RESTful.

Hola IEF envía datos en las notificaciones y recibe los datos en las notificaciones. interacción de Hello con hello API:

- Se puede diseñar como un intercambio de notificaciones de API de REST, a modo de un perfil de validación, que tiene lugar dentro de un paso de orquestación.
- Normalmente valida la entrada de usuario de Hola. Si se rechaza el valor de Hola de usuario de hello, usuario Hola puede intentar volver a tooenter un valor válido con hello oportunidad tooreturn un mensaje de error.

También puede diseñar interacción Hola como un paso de la orquestación. Para obtener más información, vea [Tutorial: Integración de intercambios de notificaciones de API de REST en los recorridos de usuario de Azure AD B2C como un paso de orquestación](active-directory-b2c-rest-api-step-custom.md).

Por ejemplo de perfil de validación de hello, usaremos viaje de usuario de edición de perfil de hello en archivo de módulo de inicio de hello ProfileEdit.xml.

Podemos comprobar ese nombre hello proporcionado por usuario de hello en el perfil de hello edición no forma parte de una lista de exclusión.

## <a name="prerequisites"></a>Requisitos previos

- Un toocomplete de Azure AD B2C inquilino configura una cuenta local de sesión-up/inicio de sesión de, como se describe en [Introducción](active-directory-b2c-get-started-custom.md).
- Un punto de conexión de API de REST toointeract con. En este tutorial, hemos configurado un sitio de demostración denominado [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) con un servicio de API de REST.

## <a name="step-1-prepare-hello-rest-api-function"></a>Paso 1: Preparar la función de la API de REST de Hola

> [!NOTE]
> El programa de instalación de funciones de la API de REST está fuera de ámbito de Hola de este artículo. [Las funciones de Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) proporciona un Kit de herramientas de excelente toocreate servicios RESTful en nube Hola.

Hemos creado una función de Azure que recibe una notificación que espera como `playerTag`. función Hello valida si existe esta notificación. Puede tener acceso a código de la función de Azure completo de hello en [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).

```csharp
if (requestContentAsJObject.playerTag == null)
{
  return request.CreateResponse(HttpStatusCode.BadRequest);
}

var playerTag = ((string) requestContentAsJObject.playerTag).ToLower();

if (playerTag == "mcvinny" || playerTag == "msgates123" || playerTag == "revcottonmarcus")
{
  return request.CreateResponse<ResponseContent>(
    HttpStatusCode.Conflict,
    new ResponseContent
    {
      version = "1.0.0",
      status = (int) HttpStatusCode.Conflict,
      userMessage = $"hello player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

Hola IEF espera hello `userMessage` devuelve esa función Azure Hola de notificación. Esta notificación se presentará como un usuario de toohello cadena si falla la validación de hello, por ejemplo, cuando se devuelve un estado de 409 Conflicto en el anterior ejemplo de Hola.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a>Paso 2: Configurar exchange de notificaciones de API de REST de Hola como un perfil técnico en el archivo TrustFrameworkExtensions.xml

Un perfil técnico es la configuración completa de Hola de exchange Hola deseado con hello servicio RESTful. Abra el archivo de TrustFrameworkExtensions.xml hello y agregue Hola siguiente fragmento XML dentro de hello `<ClaimsProviders>` elemento.

> [!NOTE]
> Hola continuación de XML, proveedor RESTful `Version=1.0.0.0` se describe como protocolo de Hola. Considérelo como función hello que interactúa con el servicio externo de Hola. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```xml
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-CheckPlayerTagWebHook">
            <DisplayName>Check Player Tag Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/CheckPlayerTagWebHook?code=L/05YRSpojU0nECzM4Tp3LjBiA2ZGh3kTwwp1OVV7m0SelnvlRVLCg==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="playerTag" />
            </InputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
        <TechnicalProfile Id="SelfAsserted-ProfileUpdate">
            <ValidationTechnicalProfiles>
                <ValidationTechnicalProfile ReferenceId="AzureFunctions-CheckPlayerTagWebHook" />
            </ValidationTechnicalProfiles>
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

Hola `InputClaims` elemento define notificaciones de Hola que se enviarán desde Hola servicio REST de IEF toohello. En este ejemplo, Hola contenido de notificación de hello `givenName` se enviará al servicio REST de toohello como `playerTag`. En este ejemplo, hello que IEF no espera notificaciones de nuevo. En su lugar, se espera una respuesta de servicio REST de Hola y actúa en función de los códigos de estado de Hola que recibe.

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a>Paso 3: Incluir el intercambio de notificaciones del servicio RESTful de hello en autoafirmadas perfil técnica donde desea toovalidate Hola proporcionados por el usuario

Hola uso más común del paso de validación de Hola está en la interacción de Hola a un usuario. Todas las interacciones donde usuario hello es tooprovide esperado de entrada están *impone automáticamente perfiles técnicos*. En este ejemplo, agregaremos perfil de autoservicio Asserted ProfileUpdate de toohello de validación de hello técnica. Hola perfil técnica que Hola archivo de directiva de confianza (RP) de la entidad `Profile Edit` usa.

tooadd Hola notificaciones exchange toohello impuesto automáticamente perfil técnico:

1. Abra el archivo TrustFrameworkBase.xml de Hola y busque `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.
2. Revise la configuración de Hola de este perfil técnica. Observe cómo exchange Hola con usuario Hola se define como las notificaciones que se le pide del usuario de hello (notificaciones de entrada) y que se espera de proveedor de hello autoafirmadas (notificaciones de salida).
3. Busque `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`; observe que este perfil se invoca como el paso de orquestación n.º 6 de `<UserJourney Id="ProfileEdit">`.

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a>Paso 4: Cargar y probar el archivo de directiva de hello perfil editar RP

1. Cargue Hola nueva versión del archivo de TrustFrameworkExtensions.xml Hola.
2. Use **ejecutar ahora** perfil de hello tootest editar el archivo de directiva RP.
3. Probar la validación de hello proporcionando uno de los nombres existentes hello (por ejemplo, mcvinny) en hello **nombre dado** campo. Si todo está configurado correctamente, debería recibir un mensaje que notifica al usuario de Hola que etiqueta de hello Reproductor ya está en uso.

## <a name="next-steps"></a>Pasos siguientes

[Modificar Hola perfil Editar usuario toogather adicional información de registro y de los usuarios](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[Tutorial: Integración de intercambios de notificaciones de API de REST en los recorridos de usuario de Azure AD B2C como un paso de orquestación](active-directory-b2c-rest-api-step-custom.md)
