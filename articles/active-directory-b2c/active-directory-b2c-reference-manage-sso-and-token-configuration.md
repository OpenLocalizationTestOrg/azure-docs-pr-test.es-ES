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
ms.openlocfilehash: 8f5703d15766f221517cd89352d41685652d32d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="300aa-102">Azure Active Directory B2C: administración de SSO y personalización de token con directivas personalizadas</span><span class="sxs-lookup"><span data-stu-id="300aa-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="300aa-103">El uso de directivas personalizadas proporciona el mismo control sobre las configuraciones de token, sesión e inicio de sesión único (SSO) que las directivas integradas.</span><span class="sxs-lookup"><span data-stu-id="300aa-103">Using custom policies provides you the same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="300aa-104">Para saber lo que hace cada una, consulte la documentación [aquí](#active-directory-b2c-token-session-sso).</span><span class="sxs-lookup"><span data-stu-id="300aa-104">To learn what each setting does, please see the documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="300aa-105">Configuración de notificaciones y duración del token</span><span class="sxs-lookup"><span data-stu-id="300aa-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="300aa-106">Para cambiar la configuración de la duración del token, debe agregar un elemento `<ClaimsProviders>` en el archivo de usuario de confianza de la directiva que quiere modificar.</span><span class="sxs-lookup"><span data-stu-id="300aa-106">To change the settings on your token lifetimes, you need to add a `<ClaimsProviders>` element in the relying party file of the policy you want to impact.</span></span>  <span data-ttu-id="300aa-107">El elemento `<ClaimsProviders>` es secundario de `<TrustFrameworkPolicy>`.</span><span class="sxs-lookup"><span data-stu-id="300aa-107">The `<ClaimsProviders>` element is a child of the `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="300aa-108">Dentro debe colocar la información que afecta a la duración del token.</span><span class="sxs-lookup"><span data-stu-id="300aa-108">Inside you'll need to put the information that affects your token lifetimes.</span></span>  <span data-ttu-id="300aa-109">El XML tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="300aa-109">The XML looks like this:</span></span>

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

<span data-ttu-id="300aa-110">**Duración del token de acceso**: la duración del token de acceso se puede cambiar mediante la modificación del valor dentro de `<Item>` con la clave = "token_lifetime_secs" en segundos.</span><span class="sxs-lookup"><span data-stu-id="300aa-110">**Access token lifetimes** The access token lifetime can be changed by modifying the value inside the `<Item>` with the Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="300aa-111">El valor predeterminado en el elemento integrado es 3600 (60 minutos).</span><span class="sxs-lookup"><span data-stu-id="300aa-111">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="300aa-112">**Duración del token del identificador**: la duración del token del identificador se puede cambiar mediante la modificación del valor `<Item>` con la clave = "id_token_lifetime_secs" en segundos.</span><span class="sxs-lookup"><span data-stu-id="300aa-112">**ID token lifetime** The ID token lifetime can be changed by modifying the value inside the `<Item>` with the Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="300aa-113">El valor predeterminado en el elemento integrado es 3600 (60 minutos).</span><span class="sxs-lookup"><span data-stu-id="300aa-113">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="300aa-114">**Duración del token de actualización**: la duración del token de actualización se puede cambiar mediante la modificación del valor dentro de `<Item>` con la clave = "refresh_token_lifetime_secs" en segundos.</span><span class="sxs-lookup"><span data-stu-id="300aa-114">**Refresh token lifetime** The refresh token lifetime can be changed by modifying the value inside the `<Item>` with the Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="300aa-115">El valor predeterminado en el elemento integrado es 1209600 segundos (14 días).</span><span class="sxs-lookup"><span data-stu-id="300aa-115">The default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="300aa-116">**Duración de la ventana deslizante del token de actualización**: si desea establecer una duración de ventana deslizante para su token de actualización, modifique el valor dentro de `<Item>` con la clave Key="rolling_refresh_token_lifetime_secs" en segundos.</span><span class="sxs-lookup"><span data-stu-id="300aa-116">**Refresh token sliding window lifetime** If you would like to set a sliding window lifetime to your refresh token, modify the value inside `<Item>` with the Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="300aa-117">El valor predeterminado del elemento integrado es 7776000 (90 días).</span><span class="sxs-lookup"><span data-stu-id="300aa-117">The default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="300aa-118">Si no desea exigir una duración de ventana deslizante, reemplace esta línea con:</span><span class="sxs-lookup"><span data-stu-id="300aa-118">If you don't want to enfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="300aa-119">**Notificación de emisor (iss)**: si desea cambiar la notificación del emisor (iss), modifique el valor dentro de `<Item>` con la clave = "IssuanceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="300aa-119">**Issuer (iss) claim** If you want to change the Issuer (iss) claim, modify the value inside the `<Item>` with the Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="300aa-120">Los valores aplicables son `AuthorityAndTenantGuid` y `AuthorityWithTfp`.</span><span class="sxs-lookup"><span data-stu-id="300aa-120">The applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="300aa-121">**Configuración de notificación que representa el identificador de directiva**: las opciones para configurar este valor son TFTP (directiva de marco de confianza) y ACR (referencia de contexto de autenticación).</span><span class="sxs-lookup"><span data-stu-id="300aa-121">**Setting claim representing policy ID** The options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="300aa-122">Se recomienda establecer este valor en TFTP; para ello, asegúrese de que exista `<Item>` con la clave = "AuthenticationContextReferenceClaimPattern" y que el valor sea `None`.</span><span class="sxs-lookup"><span data-stu-id="300aa-122">We recommend setting this to TFP, to do this, ensure the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern" exists and the value is `None`.</span></span>
<span data-ttu-id="300aa-123">En su elemento `<OutputClaims>`, agregue este elemento:</span><span class="sxs-lookup"><span data-stu-id="300aa-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="300aa-124">Para ACR, quite `<Item>` con la clave= "AuthenticationContextReferenceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="300aa-124">For ACR, remove the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="300aa-125">**Notificación de asunto (sub)**: esta opción se establece de forma predeterminada en ObjectID; si desea cambiarlo a `Not Supported`, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="300aa-125">**Subject (sub) claim** This option is defaulted to ObjectID, if you would like to switch this to `Not Supported`, do the following:</span></span>

<span data-ttu-id="300aa-126">Reemplace esta línea</span><span class="sxs-lookup"><span data-stu-id="300aa-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="300aa-127">por esta otra:</span><span class="sxs-lookup"><span data-stu-id="300aa-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="300aa-128">Comportamiento de sesión y SSO</span><span class="sxs-lookup"><span data-stu-id="300aa-128">Session behavior and SSO</span></span>
<span data-ttu-id="300aa-129">Para cambiar las configuraciones de comportamiento de sesión y SSO, debe agregar un elemento `<UserJourneyBehaviors>` dentro del elemento `<RelyingParty>`.</span><span class="sxs-lookup"><span data-stu-id="300aa-129">To change your session behavior and SSO configurations, you need to add a `<UserJourneyBehaviors>` element inside of the `<RelyingParty>` element.</span></span>  <span data-ttu-id="300aa-130">El elemento `<UserJourneyBehaviors>` debe seguir inmediatamente a `<DefaultUserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="300aa-130">The `<UserJourneyBehaviors>` element must immediately follow the `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="300aa-131">El interior de su elemento `<UserJourneyBehavors>` debe ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="300aa-131">The inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="300aa-132">**Configuración de inicio de sesión único (SSO)**: para cambiar la configuración del inicio de sesión único, debe modificar el valor de `<SingleSignOn>`.</span><span class="sxs-lookup"><span data-stu-id="300aa-132">**Single sign-on (SSO) configuration** To change the single sign-on configuration, you need to modify the value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="300aa-133">Los valores aplicables son `Tenant`, `Application`, `Policy` y `Disabled`.</span><span class="sxs-lookup"><span data-stu-id="300aa-133">The applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="300aa-134">**Duración de sesión de aplicación web (minutos)**: para cambiar la duración de la sesión de aplicación web, debe modificar el valor del elemento `<SessionExpiryInSeconds>`.</span><span class="sxs-lookup"><span data-stu-id="300aa-134">**Web app session lifetime (minutes)** To change the the web app session lifetime, you need to modify value of the `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="300aa-135">El valor predeterminado en las directivas integradas es 86400 segundos (1440 minutos).</span><span class="sxs-lookup"><span data-stu-id="300aa-135">The default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="300aa-136">**Tiempo de espera de sesión de aplicación web**: para cambiar el tiempo de espera de sesión de una aplicación web, debe modificar el valor de `<SessionExpiryType>`.</span><span class="sxs-lookup"><span data-stu-id="300aa-136">**Web app session timeout** To change the web app session timeout, you need to modify the value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="300aa-137">Los valores aplicables son `Absolute` y `Rolling`.</span><span class="sxs-lookup"><span data-stu-id="300aa-137">The applicable values are `Absolute` and `Rolling`.</span></span>
