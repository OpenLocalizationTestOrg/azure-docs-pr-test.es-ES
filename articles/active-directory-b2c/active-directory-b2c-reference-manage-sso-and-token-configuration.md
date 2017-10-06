---
title: "Azure Active Directory B2C: administración de SSO y personalización de token con directivas personalizadas | Microsoft Docs"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/02/2017
ms.author: sama
ms.openlocfilehash: b65271a22c77ea41eeec2126e4a3ad24364edd17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a>Azure Active Directory B2C: administración de SSO y personalización de token con directivas personalizadas
Uso de directivas personalizadas proporciona que Hola mismo control sobre el símbolo (token), sesión y configuraciones de (SSO) de inicio de sesión único como a través de directivas integradas.  toolearn hace el significado de cada configuración, consulte la documentación de hello [aquí](#active-directory-b2c-token-session-sso).

## <a name="token-lifetimes-and-claims-configuration"></a>Configuración de notificaciones y duración del token
configuración de hello toochange en la vigencia de los tokens, deberá tooadd un `<ClaimsProviders>` elemento en el archivo de usuario confianza hello de directiva de hello desea tooimpact.  Hola `<ClaimsProviders>` es un elemento secundario de hello `<TrustFrameworkPolicy>`.  En, se le solicitará información de Hola de tooput que afecta a la vigencia de los tokens.  Hola XML tiene el siguiente aspecto:

```XML
<ClaimsProviders>
   <ClaimsProvider>
      <DisplayName>Token Issuer</DisplayName>
      <TechnicalProfiles>
         <TechnicalProfile Id="JwtIssuer">
            <Metadata>
               <Item Key="token_lifetime_secs">3600</Item>
               <Item Key="id_token_lifetime_secs">3600</Item>
               <Item Key="refresh_token_lifetime_secs">1209600</Item>
               <Item Key="rolling_refresh_token_lifetime_secs">7776000</Item>
               <Item Key="IssuanceClaimPattern">AuthorityAndTenantGuid</Item>
               <Item Key="AuthenticationContextReferenceClaimPattern">None</Item>
            </Metadata>
         </TechnicalProfile>
      </TechnicalProfiles>
   </ClaimsProvider>
</ClaimsProviders>
```

**Vigencia de los tokens de acceso** Hola acceso duración del token se puede cambiar modificando el valor de hello dentro de hello `<Item>` con hello clave = "token_lifetime_secs" en segundos.  valor predeterminado de Hello en integrada es 3600 segundos (60 minutos).

**Duración del token de identificador** duración Hola Id. del token se puede cambiar modificando el valor de hello dentro de hello `<Item>` con hello clave = "id_token_lifetime_secs" en segundos.  valor predeterminado de Hello en integrada es 3600 segundos (60 minutos).

**Duración del token de actualización** duración del token Hola actualización puede cambiarse modificando el valor de hello dentro de hello `<Item>` con hello clave = "refresh_token_lifetime_secs" en segundos.  valor predeterminado de Hello en integrada es 1209600 segundos (14 días).

**Actualizar token duración de ventana deslizante** si desea que tooset un token de actualización del tooyour de duración de ventana deslizante, modifique el valor de hello dentro de `<Item>` con hello clave = "rolling_refresh_token_lifetime_secs" en segundos.  valor predeterminado de Hello en integrada es 7776000 (90 días).  Si no desea tooenfore un deslizante duración de ventana, reemplace esta línea con:
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

**Notificación de emisor (iss)** si desea que la notificación de emisor (iss) de hello toochange, modifique el valor de hello dentro de hello `<Item>` con hello clave = "IssuanceClaimPattern".  Hola los valores aplicables son `AuthorityAndTenantGuid` y `AuthorityWithTfp`.

**Configuración de notificaciones que representa el Id. de directiva** opciones de Hola para establecer este valor son TFTP (directiva de framework de confianza) y ACR (referencia de contexto de autenticación).  
Se recomienda establecer este tooTFP, toodo esto, asegúrese de hello `<Item>` con hello clave = "AuthenticationContextReferenceClaimPattern" existe y es el valor de hello `None`.
En su elemento `<OutputClaims>`, agregue este elemento:
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
Para el ACR, quitar hello `<Item>` con hello clave = "AuthenticationContextReferenceClaimPattern".

**Notificación de asunto (sub)** esta opción es establecidas como valor predeterminado tooObjectID, si desea que tooswitch esto demasiado`Not Supported`, Hola siguientes:

Reemplace esta línea 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
por esta otra:
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a>Comportamiento de sesión y SSO
toochange su comportamiento de sesión y sus configuraciones de SSO, deberá tooadd un `<UserJourneyBehaviors>` elemento dentro de hello `<RelyingParty>` elemento.  Hola `<UserJourneyBehaviors>` elemento debe seguir inmediatamente a hello `<DefaultUserJourney>`.  Hola dentro de su `<UserJourneyBehavors>` elemento debe ser similar al siguiente:

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
**Configuración de inicio de sesión único (SSO)** toochange Hola única configuración sign-on, necesita toomodify Hola valo `<SingleSignOn>`.  Hola los valores aplicables son `Tenant`, `Application`, `Policy` y `Disabled`. 

**Aplicación Web de duración de la sesión (minutos)** toochange Hola Hola web app duración de la sesión, necesita toomodify valo hello `<SessionExpiryInSeconds>` elemento.  valor predeterminado de Hello en directivas integradas es 86400 segundos (1440 minutos).

**Tiempo de espera de sesión de aplicación de Web** tiempo de espera de toochange hello web app sesión, necesita toomodify Hola valo `<SessionExpiryType>`.  Hola los valores aplicables son `Absolute` y `Rolling`.
