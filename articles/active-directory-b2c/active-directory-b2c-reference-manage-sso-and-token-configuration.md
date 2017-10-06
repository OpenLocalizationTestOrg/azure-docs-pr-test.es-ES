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
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="912b3-102">Azure Active Directory B2C: administración de SSO y personalización de token con directivas personalizadas</span><span class="sxs-lookup"><span data-stu-id="912b3-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="912b3-103">Uso de directivas personalizadas proporciona que Hola mismo control sobre el símbolo (token), sesión y configuraciones de (SSO) de inicio de sesión único como a través de directivas integradas.</span><span class="sxs-lookup"><span data-stu-id="912b3-103">Using custom policies provides you hello same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="912b3-104">toolearn hace el significado de cada configuración, consulte la documentación de hello [aquí](#active-directory-b2c-token-session-sso).</span><span class="sxs-lookup"><span data-stu-id="912b3-104">toolearn what each setting does, please see hello documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="912b3-105">Configuración de notificaciones y duración del token</span><span class="sxs-lookup"><span data-stu-id="912b3-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="912b3-106">configuración de hello toochange en la vigencia de los tokens, deberá tooadd un `<ClaimsProviders>` elemento en el archivo de usuario confianza hello de directiva de hello desea tooimpact.</span><span class="sxs-lookup"><span data-stu-id="912b3-106">toochange hello settings on your token lifetimes, you need tooadd a `<ClaimsProviders>` element in hello relying party file of hello policy you want tooimpact.</span></span>  <span data-ttu-id="912b3-107">Hola `<ClaimsProviders>` es un elemento secundario de hello `<TrustFrameworkPolicy>`.</span><span class="sxs-lookup"><span data-stu-id="912b3-107">hello `<ClaimsProviders>` element is a child of hello `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="912b3-108">En, se le solicitará información de Hola de tooput que afecta a la vigencia de los tokens.</span><span class="sxs-lookup"><span data-stu-id="912b3-108">Inside you'll need tooput hello information that affects your token lifetimes.</span></span>  <span data-ttu-id="912b3-109">Hola XML tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="912b3-109">hello XML looks like this:</span></span>

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

<span data-ttu-id="912b3-110">**Vigencia de los tokens de acceso** Hola acceso duración del token se puede cambiar modificando el valor de hello dentro de hello `<Item>` con hello clave = "token_lifetime_secs" en segundos.</span><span class="sxs-lookup"><span data-stu-id="912b3-110">**Access token lifetimes** hello access token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="912b3-111">valor predeterminado de Hello en integrada es 3600 segundos (60 minutos).</span><span class="sxs-lookup"><span data-stu-id="912b3-111">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="912b3-112">**Duración del token de identificador** duración Hola Id. del token se puede cambiar modificando el valor de hello dentro de hello `<Item>` con hello clave = "id_token_lifetime_secs" en segundos.</span><span class="sxs-lookup"><span data-stu-id="912b3-112">**ID token lifetime** hello ID token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="912b3-113">valor predeterminado de Hello en integrada es 3600 segundos (60 minutos).</span><span class="sxs-lookup"><span data-stu-id="912b3-113">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="912b3-114">**Duración del token de actualización** duración del token Hola actualización puede cambiarse modificando el valor de hello dentro de hello `<Item>` con hello clave = "refresh_token_lifetime_secs" en segundos.</span><span class="sxs-lookup"><span data-stu-id="912b3-114">**Refresh token lifetime** hello refresh token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="912b3-115">valor predeterminado de Hello en integrada es 1209600 segundos (14 días).</span><span class="sxs-lookup"><span data-stu-id="912b3-115">hello default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="912b3-116">**Actualizar token duración de ventana deslizante** si desea que tooset un token de actualización del tooyour de duración de ventana deslizante, modifique el valor de hello dentro de `<Item>` con hello clave = "rolling_refresh_token_lifetime_secs" en segundos.</span><span class="sxs-lookup"><span data-stu-id="912b3-116">**Refresh token sliding window lifetime** If you would like tooset a sliding window lifetime tooyour refresh token, modify hello value inside `<Item>` with hello Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="912b3-117">valor predeterminado de Hello en integrada es 7776000 (90 días).</span><span class="sxs-lookup"><span data-stu-id="912b3-117">hello default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="912b3-118">Si no desea tooenfore un deslizante duración de ventana, reemplace esta línea con:</span><span class="sxs-lookup"><span data-stu-id="912b3-118">If you don't want tooenfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="912b3-119">**Notificación de emisor (iss)** si desea que la notificación de emisor (iss) de hello toochange, modifique el valor de hello dentro de hello `<Item>` con hello clave = "IssuanceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="912b3-119">**Issuer (iss) claim** If you want toochange hello Issuer (iss) claim, modify hello value inside hello `<Item>` with hello Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="912b3-120">Hola los valores aplicables son `AuthorityAndTenantGuid` y `AuthorityWithTfp`.</span><span class="sxs-lookup"><span data-stu-id="912b3-120">hello applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="912b3-121">**Configuración de notificaciones que representa el Id. de directiva** opciones de Hola para establecer este valor son TFTP (directiva de framework de confianza) y ACR (referencia de contexto de autenticación).</span><span class="sxs-lookup"><span data-stu-id="912b3-121">**Setting claim representing policy ID** hello options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="912b3-122">Se recomienda establecer este tooTFP, toodo esto, asegúrese de hello `<Item>` con hello clave = "AuthenticationContextReferenceClaimPattern" existe y es el valor de hello `None`.</span><span class="sxs-lookup"><span data-stu-id="912b3-122">We recommend setting this tooTFP, toodo this, ensure hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern" exists and hello value is `None`.</span></span>
<span data-ttu-id="912b3-123">En su elemento `<OutputClaims>`, agregue este elemento:</span><span class="sxs-lookup"><span data-stu-id="912b3-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="912b3-124">Para el ACR, quitar hello `<Item>` con hello clave = "AuthenticationContextReferenceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="912b3-124">For ACR, remove hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="912b3-125">**Notificación de asunto (sub)** esta opción es establecidas como valor predeterminado tooObjectID, si desea que tooswitch esto demasiado`Not Supported`, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="912b3-125">**Subject (sub) claim** This option is defaulted tooObjectID, if you would like tooswitch this too`Not Supported`, do hello following:</span></span>

<span data-ttu-id="912b3-126">Reemplace esta línea</span><span class="sxs-lookup"><span data-stu-id="912b3-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="912b3-127">por esta otra:</span><span class="sxs-lookup"><span data-stu-id="912b3-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="912b3-128">Comportamiento de sesión y SSO</span><span class="sxs-lookup"><span data-stu-id="912b3-128">Session behavior and SSO</span></span>
<span data-ttu-id="912b3-129">toochange su comportamiento de sesión y sus configuraciones de SSO, deberá tooadd un `<UserJourneyBehaviors>` elemento dentro de hello `<RelyingParty>` elemento.</span><span class="sxs-lookup"><span data-stu-id="912b3-129">toochange your session behavior and SSO configurations, you need tooadd a `<UserJourneyBehaviors>` element inside of hello `<RelyingParty>` element.</span></span>  <span data-ttu-id="912b3-130">Hola `<UserJourneyBehaviors>` elemento debe seguir inmediatamente a hello `<DefaultUserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="912b3-130">hello `<UserJourneyBehaviors>` element must immediately follow hello `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="912b3-131">Hola dentro de su `<UserJourneyBehavors>` elemento debe ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="912b3-131">hello inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="912b3-132">**Configuración de inicio de sesión único (SSO)** toochange Hola única configuración sign-on, necesita toomodify Hola valo `<SingleSignOn>`.</span><span class="sxs-lookup"><span data-stu-id="912b3-132">**Single sign-on (SSO) configuration** toochange hello single sign-on configuration, you need toomodify hello value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="912b3-133">Hola los valores aplicables son `Tenant`, `Application`, `Policy` y `Disabled`.</span><span class="sxs-lookup"><span data-stu-id="912b3-133">hello applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="912b3-134">**Aplicación Web de duración de la sesión (minutos)** toochange Hola Hola web app duración de la sesión, necesita toomodify valo hello `<SessionExpiryInSeconds>` elemento.</span><span class="sxs-lookup"><span data-stu-id="912b3-134">**Web app session lifetime (minutes)** toochange hello hello web app session lifetime, you need toomodify value of hello `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="912b3-135">valor predeterminado de Hello en directivas integradas es 86400 segundos (1440 minutos).</span><span class="sxs-lookup"><span data-stu-id="912b3-135">hello default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="912b3-136">**Tiempo de espera de sesión de aplicación de Web** tiempo de espera de toochange hello web app sesión, necesita toomodify Hola valo `<SessionExpiryType>`.</span><span class="sxs-lookup"><span data-stu-id="912b3-136">**Web app session timeout** toochange hello web app session timeout, you need toomodify hello value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="912b3-137">Hola los valores aplicables son `Absolute` y `Rolling`.</span><span class="sxs-lookup"><span data-stu-id="912b3-137">hello applicable values are `Absolute` and `Rolling`.</span></span>
