---
title: "aaaSession de administración - herramienta de modelado de amenazas de Microsoft - Azure | Documentos de Microsoft"
description: mitigaciones en busca de amenazas que se exponen en hello herramienta de modelado de amenazas
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a><span data-ttu-id="c0102-103">Marco de seguridad: Administración de sesiones | Artículos</span><span class="sxs-lookup"><span data-stu-id="c0102-103">Security Frame: Session Management | Articles</span></span> 
| <span data-ttu-id="c0102-104">Producto o servicio</span><span class="sxs-lookup"><span data-stu-id="c0102-104">Product/Service</span></span> | <span data-ttu-id="c0102-105">Artículo</span><span class="sxs-lookup"><span data-stu-id="c0102-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="c0102-106">**Azure AD**</span><span class="sxs-lookup"><span data-stu-id="c0102-106">**Azure AD**</span></span>    | <ul><li>[<span data-ttu-id="c0102-107">Implemente el cierre de sesión correcto mediante métodos ADAL cuando use Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0102-107">Implement proper logout using ADAL methods when using Azure AD</span></span>](#logout-adal)</li></ul> |
| <span data-ttu-id="c0102-108">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="c0102-108">IoT Device</span></span> | <ul><li>[<span data-ttu-id="c0102-109">Use duraciones finitas para los tokens de SaS generados</span><span class="sxs-lookup"><span data-stu-id="c0102-109">Use finite lifetimes for generated SaS tokens</span></span>](#finite-tokens)</li></ul> |
| <span data-ttu-id="c0102-110">**Azure Document DB**</span><span class="sxs-lookup"><span data-stu-id="c0102-110">**Azure Document DB**</span></span> | <ul><li>[<span data-ttu-id="c0102-111">Use duraciones mínimas de token para los tokens de recursos generados</span><span class="sxs-lookup"><span data-stu-id="c0102-111">Use minimum token lifetimes for generated Resource tokens</span></span>](#resource-tokens)</li></ul> |
| <span data-ttu-id="c0102-112">**ADFS**</span><span class="sxs-lookup"><span data-stu-id="c0102-112">**ADFS**</span></span> | <ul><li>[<span data-ttu-id="c0102-113">Implemente el cierre de sesión correcto mediante métodos WsFederation cuando use ADFS</span><span class="sxs-lookup"><span data-stu-id="c0102-113">Implement proper logout using WsFederation methods when using ADFS</span></span>](#wsfederation-logout)</li></ul> |
| <span data-ttu-id="c0102-114">**Identity Server**</span><span class="sxs-lookup"><span data-stu-id="c0102-114">**Identity Server**</span></span> | <ul><li>[<span data-ttu-id="c0102-115">Implemente el cierre de sesión correcto cuando use Identity Server</span><span class="sxs-lookup"><span data-stu-id="c0102-115">Implement proper logout when using Identity Server</span></span>](#proper-logout)</li></ul> |
| <span data-ttu-id="c0102-116">**Aplicación web**</span><span class="sxs-lookup"><span data-stu-id="c0102-116">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="c0102-117">Las aplicaciones disponibles a través de HTTPS deben usar cookies seguras</span><span class="sxs-lookup"><span data-stu-id="c0102-117">Applications available over HTTPS must use secure cookies</span></span>](#https-secure-cookies)</li><li>[<span data-ttu-id="c0102-118">Todas las aplicaciones basadas en HTTP deben especificar HTTP solo para la definición de cookies</span><span class="sxs-lookup"><span data-stu-id="c0102-118">All http based application should specify http only for cookie definition</span></span>](#cookie-definition)</li><li>[<span data-ttu-id="c0102-119">Mitigue el riesgo de ataques de falsificación de solicitud entre sitios (CSRF) en páginas web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c0102-119">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>](#csrf-asp)</li><li>[<span data-ttu-id="c0102-120">Configure la sesión para la duración de la inactividad</span><span class="sxs-lookup"><span data-stu-id="c0102-120">Set up session for inactivity lifetime</span></span>](#inactivity-lifetime)</li><li>[<span data-ttu-id="c0102-121">Implemente el cierre de sesión correcto de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="c0102-121">Implement proper logout from hello application</span></span>](#proper-app-logout)</li></ul> |
| <span data-ttu-id="c0102-122">**API web**</span><span class="sxs-lookup"><span data-stu-id="c0102-122">**Web API**</span></span> | <ul><li>[<span data-ttu-id="c0102-123">Mitigue el riesgo de ataques de falsificación de solicitud entre sitios (CSRF) en las API web de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c0102-123">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>](#csrf-api)</li></ul> |

## <span data-ttu-id="c0102-124"><a id="logout-adal"></a>Implemente el cierre de sesión correcto mediante métodos ADAL cuando use Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0102-124"><a id="logout-adal"></a>Implement proper logout using ADAL methods when using Azure AD</span></span>

| <span data-ttu-id="c0102-125">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-125">Title</span></span>                   | <span data-ttu-id="c0102-126">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-126">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-127">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-127">**Component**</span></span>               | <span data-ttu-id="c0102-128">Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0102-128">Azure AD</span></span> | 
| <span data-ttu-id="c0102-129">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-129">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-130">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-130">Build</span></span> |  
| <span data-ttu-id="c0102-131">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-131">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-132">Genérico</span><span class="sxs-lookup"><span data-stu-id="c0102-132">Generic</span></span> |
| <span data-ttu-id="c0102-133">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-133">**Attributes**</span></span>              | <span data-ttu-id="c0102-134">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-134">N/A</span></span>  |
| <span data-ttu-id="c0102-135">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-135">**References**</span></span>              | <span data-ttu-id="c0102-136">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-136">N/A</span></span>  |
| <span data-ttu-id="c0102-137">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-137">**Steps**</span></span> | <span data-ttu-id="c0102-138">Si la aplicación hello se basa en el token de acceso emitido por Azure AD, debe llamar controlador de eventos de cierre de sesión de Hola</span><span class="sxs-lookup"><span data-stu-id="c0102-138">If hello application relies on access token issued by Azure AD, hello logout event handler should call</span></span> |

### <a name="example"></a><span data-ttu-id="c0102-139">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-139">Example</span></span>
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a><span data-ttu-id="c0102-140">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-140">Example</span></span>
<span data-ttu-id="c0102-141">También debe destruir la sesión del usuario llamando al método Session.Abandon().</span><span class="sxs-lookup"><span data-stu-id="c0102-141">It should also destroy user's session by calling Session.Abandon() method.</span></span> <span data-ttu-id="c0102-142">En el siguiente método, se muestra una implementación segura del cierre de sesión del usuario:</span><span class="sxs-lookup"><span data-stu-id="c0102-142">Following method shows secure implementation of user logout:</span></span>
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <span data-ttu-id="c0102-143"><a id="finite-tokens"></a>Use duraciones finitas para los tokens de SaS generados</span><span class="sxs-lookup"><span data-stu-id="c0102-143"><a id="finite-tokens"></a>Use finite lifetimes for generated SaS tokens</span></span>

| <span data-ttu-id="c0102-144">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-144">Title</span></span>                   | <span data-ttu-id="c0102-145">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-145">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-146">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-146">**Component**</span></span>               | <span data-ttu-id="c0102-147">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="c0102-147">IoT Device</span></span> | 
| <span data-ttu-id="c0102-148">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-148">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-149">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-149">Build</span></span> |  
| <span data-ttu-id="c0102-150">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-150">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-151">Genérico</span><span class="sxs-lookup"><span data-stu-id="c0102-151">Generic</span></span> |
| <span data-ttu-id="c0102-152">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-152">**Attributes**</span></span>              | <span data-ttu-id="c0102-153">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-153">N/A</span></span>  |
| <span data-ttu-id="c0102-154">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-154">**References**</span></span>              | <span data-ttu-id="c0102-155">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-155">N/A</span></span>  |
| <span data-ttu-id="c0102-156">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-156">**Steps**</span></span> | <span data-ttu-id="c0102-157">Los tokens de SaS generados para la autenticación de tooAzure centro de IoT deben tener un período de expiración definida.</span><span class="sxs-lookup"><span data-stu-id="c0102-157">SaS tokens generated for authenticating tooAzure IoT Hub should have a finite expiry period.</span></span> <span data-ttu-id="c0102-158">Mantener Hola SaS vigencia de los tokens tooa toolimit mínima Hola cantidad de tiempo que se pueden reproducir en caso de que se vean comprometidos los tokens de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0102-158">Keep hello SaS token lifetimes tooa minimum toolimit hello amount of time they can be replayed in case hello tokens are compromised.</span></span>|

## <span data-ttu-id="c0102-159"><a id="resource-tokens"></a>Use duraciones mínimas de token para los tokens de recursos generados</span><span class="sxs-lookup"><span data-stu-id="c0102-159"><a id="resource-tokens"></a>Use minimum token lifetimes for generated Resource tokens</span></span>

| <span data-ttu-id="c0102-160">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-160">Title</span></span>                   | <span data-ttu-id="c0102-161">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-162">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-162">**Component**</span></span>               | <span data-ttu-id="c0102-163">Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c0102-163">Azure Document DB</span></span> | 
| <span data-ttu-id="c0102-164">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-164">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-165">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-165">Build</span></span> |  
| <span data-ttu-id="c0102-166">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-166">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-167">Genérico</span><span class="sxs-lookup"><span data-stu-id="c0102-167">Generic</span></span> |
| <span data-ttu-id="c0102-168">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-168">**Attributes**</span></span>              | <span data-ttu-id="c0102-169">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-169">N/A</span></span>  |
| <span data-ttu-id="c0102-170">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-170">**References**</span></span>              | <span data-ttu-id="c0102-171">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-171">N/A</span></span>  |
| <span data-ttu-id="c0102-172">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-172">**Steps**</span></span> | <span data-ttu-id="c0102-173">Reducir timespan hello tooa token mínimo del valor de recurso necesario.</span><span class="sxs-lookup"><span data-stu-id="c0102-173">Reduce hello timespan of resource token tooa minimum value required.</span></span> <span data-ttu-id="c0102-174">Los tokens de recursos tienen un intervalo de tiempo válido predeterminado de 1 hora.</span><span class="sxs-lookup"><span data-stu-id="c0102-174">Resource tokens have a default valid timespan of 1 hour.</span></span>|

## <span data-ttu-id="c0102-175"><a id="wsfederation-logout"></a>Implemente el cierre de sesión correcto mediante métodos WsFederation cuando use ADFS</span><span class="sxs-lookup"><span data-stu-id="c0102-175"><a id="wsfederation-logout"></a>Implement proper logout using WsFederation methods when using ADFS</span></span>

| <span data-ttu-id="c0102-176">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-176">Title</span></span>                   | <span data-ttu-id="c0102-177">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-177">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-178">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-178">**Component**</span></span>               | <span data-ttu-id="c0102-179">ADFS</span><span class="sxs-lookup"><span data-stu-id="c0102-179">ADFS</span></span> | 
| <span data-ttu-id="c0102-180">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-180">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-181">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-181">Build</span></span> |  
| <span data-ttu-id="c0102-182">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-182">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-183">Genérico</span><span class="sxs-lookup"><span data-stu-id="c0102-183">Generic</span></span> |
| <span data-ttu-id="c0102-184">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-184">**Attributes**</span></span>              | <span data-ttu-id="c0102-185">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-185">N/A</span></span>  |
| <span data-ttu-id="c0102-186">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-186">**References**</span></span>              | <span data-ttu-id="c0102-187">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-187">N/A</span></span>  |
| <span data-ttu-id="c0102-188">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-188">**Steps**</span></span> | <span data-ttu-id="c0102-189">Si aplicación hello se basa en token STS emitido por AD FS, controlador de eventos de cierre de sesión de hello debe llamar a WSFederationAuthenticationModule.FederatedSignOut() método toolog usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="c0102-189">If hello application relies on STS token issued by ADFS, hello logout event handler should call WSFederationAuthenticationModule.FederatedSignOut() method toolog out hello user.</span></span> <span data-ttu-id="c0102-190">También hello actual debe destruirse sesión, y el valor del token de sesión Hola debe restablecer y compensan los riesgos.</span><span class="sxs-lookup"><span data-stu-id="c0102-190">Also hello current session should be destroyed, and hello session token value should be reset and nullified.</span></span>|

### <a name="example"></a><span data-ttu-id="c0102-191">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-191">Example</span></span>
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <span data-ttu-id="c0102-192"><a id="proper-logout"></a>Implemente el cierre de sesión correcto cuando use Identity Server</span><span class="sxs-lookup"><span data-stu-id="c0102-192"><a id="proper-logout"></a>Implement proper logout when using Identity Server</span></span>

| <span data-ttu-id="c0102-193">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-193">Title</span></span>                   | <span data-ttu-id="c0102-194">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-194">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-195">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-195">**Component**</span></span>               | <span data-ttu-id="c0102-196">Identity Server</span><span class="sxs-lookup"><span data-stu-id="c0102-196">Identity Server</span></span> | 
| <span data-ttu-id="c0102-197">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-197">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-198">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-198">Build</span></span> |  
| <span data-ttu-id="c0102-199">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-199">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-200">Genérico</span><span class="sxs-lookup"><span data-stu-id="c0102-200">Generic</span></span> |
| <span data-ttu-id="c0102-201">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-201">**Attributes**</span></span>              | <span data-ttu-id="c0102-202">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-202">N/A</span></span>  |
| <span data-ttu-id="c0102-203">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-203">**References**</span></span>              | <span data-ttu-id="c0102-204">[IdentityServer3-Federated Signout](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) (Cierre de sesión federado en IdentityServer3)</span><span class="sxs-lookup"><span data-stu-id="c0102-204">[IdentityServer3-Federated sign out](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html)</span></span> |
| <span data-ttu-id="c0102-205">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-205">**Steps**</span></span> | <span data-ttu-id="c0102-206">IdentityServer admite Hola capacidad toofederate con proveedores de identidad externa.</span><span class="sxs-lookup"><span data-stu-id="c0102-206">IdentityServer supports hello ability toofederate with external identity providers.</span></span> <span data-ttu-id="c0102-207">Cuando un usuario cierra sesión en un proveedor de identidades de nivel superior, según el protocolo de hello utilizado, puede que sea posible tooreceive una notificación cuando Hola usuario cierra la sesión. Permite toonotify IdentityServer Hola a sus clientes para que también pueden iniciar sesión de un usuario. Consulte la documentación de hello en la sección de referencias de Hola para obtener detalles de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0102-207">When a user signs out of an upstream identity provider, depending upon hello protocol used, it might be possible tooreceive a notification when hello user signs out. It allows IdentityServer toonotify its clients so they can also sign hello user out. Check hello documentation in hello references section for hello implementation details.</span></span>|

## <span data-ttu-id="c0102-208"><a id="https-secure-cookies"></a>Las aplicaciones disponibles a través de HTTPS deben usar cookies seguras</span><span class="sxs-lookup"><span data-stu-id="c0102-208"><a id="https-secure-cookies"></a>Applications available over HTTPS must use secure cookies</span></span>

| <span data-ttu-id="c0102-209">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-209">Title</span></span>                   | <span data-ttu-id="c0102-210">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-210">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-211">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-211">**Component**</span></span>               | <span data-ttu-id="c0102-212">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="c0102-212">Web Application</span></span> | 
| <span data-ttu-id="c0102-213">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-213">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-214">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-214">Build</span></span> |  
| <span data-ttu-id="c0102-215">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-215">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-216">Genérico</span><span class="sxs-lookup"><span data-stu-id="c0102-216">Generic</span></span> |
| <span data-ttu-id="c0102-217">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-217">**Attributes**</span></span>              | <span data-ttu-id="c0102-218">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="c0102-218">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="c0102-219">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-219">**References**</span></span>              | <span data-ttu-id="c0102-220">[httpCookies (Elemento, Esquema de configuración de ASP.NET)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [Propiedad HttpCookie.Secure](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span><span class="sxs-lookup"><span data-stu-id="c0102-220">[httpCookies Element (ASP.NET Settings Schema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span></span> |
| <span data-ttu-id="c0102-221">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-221">**Steps**</span></span> | <span data-ttu-id="c0102-222">Las cookies son normalmente sólo dominio de toohello accesible para el que está limitadas.</span><span class="sxs-lookup"><span data-stu-id="c0102-222">Cookies are normally only accessible toohello domain for which they were scoped.</span></span> <span data-ttu-id="c0102-223">Por desgracia, definición de Hola de "dominio" no incluye protocolo Hola por lo que las cookies se crean a través de HTTPS son accesibles a través de HTTP.</span><span class="sxs-lookup"><span data-stu-id="c0102-223">Unfortunately, hello definition of "domain" does not include hello protocol so cookies that are created over HTTPS are accessible over HTTP.</span></span> <span data-ttu-id="c0102-224">atributo de "seguro" Hello indica explorador toohello que Hola cookie sólo deberá hacerse disponible a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c0102-224">hello "secure" attribute indicates toohello browser that hello cookie should only be made available over HTTPS.</span></span> <span data-ttu-id="c0102-225">Asegúrese de que todas las cookies que se establece a través de HTTPS utilizan hello **segura** atributo.</span><span class="sxs-lookup"><span data-stu-id="c0102-225">Ensure that all cookies set over HTTPS use hello **secure** attribute.</span></span> <span data-ttu-id="c0102-226">puede aplicar el requisito de Hello en el archivo web.config de hello estableciendo Hola requireSSL atributo tootrue.</span><span class="sxs-lookup"><span data-stu-id="c0102-226">hello requirement can be enforced in hello web.config file by setting hello requireSSL attribute tootrue.</span></span> <span data-ttu-id="c0102-227">Es Hola preferido enfoque porque aplicará hello **segura** atributo para todas las cookies actuales y futuras sin Hola necesidad toomake cambios de código adicionales.</span><span class="sxs-lookup"><span data-stu-id="c0102-227">It is hello preferred approach because it will enforce hello **secure** attribute for all current and future cookies without hello need toomake any additional code changes.</span></span>|

### <a name="example"></a><span data-ttu-id="c0102-228">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-228">Example</span></span>
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
<span data-ttu-id="c0102-229">se aplica la configuración de Hello aunque HTTP es aplicación de hello tooaccess usado.</span><span class="sxs-lookup"><span data-stu-id="c0102-229">hello setting is enforced even if HTTP is used tooaccess hello application.</span></span> <span data-ttu-id="c0102-230">Si se utiliza HTTP tooaccess Hola aplicación, saltos de configuración aplicación hello porque las cookies de Hola se establecen con hello hello y atributo de un navegador seguro no enviará ellos hello volver toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0102-230">If HTTP is used tooaccess hello application, hello setting breaks hello application because hello cookies are set with hello secure attribute and hello browser will not send them back toohello application.</span></span>

| <span data-ttu-id="c0102-231">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-231">Title</span></span>                   | <span data-ttu-id="c0102-232">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-232">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-233">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-233">**Component**</span></span>               | <span data-ttu-id="c0102-234">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="c0102-234">Web Application</span></span> | 
| <span data-ttu-id="c0102-235">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-235">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-236">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-236">Build</span></span> |  
| <span data-ttu-id="c0102-237">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-237">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-238">Formularios Web Forms, MVC5</span><span class="sxs-lookup"><span data-stu-id="c0102-238">Web Forms, MVC5</span></span> |
| <span data-ttu-id="c0102-239">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-239">**Attributes**</span></span>              | <span data-ttu-id="c0102-240">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="c0102-240">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="c0102-241">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-241">**References**</span></span>              | <span data-ttu-id="c0102-242">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-242">N/A</span></span>  |
| <span data-ttu-id="c0102-243">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-243">**Steps**</span></span> | <span data-ttu-id="c0102-244">Cuando es de aplicación web de Hola Hola persona de confianza y Hola IdP es el servidor ADFS, atributo segura del token de hello FedAuth puede configurarse por establecer requireSSL tooTrue en `system.identityModel.services` sección del archivo web.config:</span><span class="sxs-lookup"><span data-stu-id="c0102-244">When hello web application is hello Relying Party, and hello IdP is ADFS server, hello FedAuth token's secure attribute can be configured by setting requireSSL tooTrue in `system.identityModel.services` section of web.config:</span></span>|

### <a name="example"></a><span data-ttu-id="c0102-245">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-245">Example</span></span>
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <span data-ttu-id="c0102-246"><a id="cookie-definition"></a>Todas las aplicaciones basadas en HTTP deben especificar HTTP solo para la definición de cookies</span><span class="sxs-lookup"><span data-stu-id="c0102-246"><a id="cookie-definition"></a>All http based application should specify http only for cookie definition</span></span>

| <span data-ttu-id="c0102-247">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-247">Title</span></span>                   | <span data-ttu-id="c0102-248">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-248">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-249">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-249">**Component**</span></span>               | <span data-ttu-id="c0102-250">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="c0102-250">Web Application</span></span> | 
| <span data-ttu-id="c0102-251">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-251">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-252">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-252">Build</span></span> |  
| <span data-ttu-id="c0102-253">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-253">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-254">Genérico</span><span class="sxs-lookup"><span data-stu-id="c0102-254">Generic</span></span> |
| <span data-ttu-id="c0102-255">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-255">**Attributes**</span></span>              | <span data-ttu-id="c0102-256">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-256">N/A</span></span>  |
| <span data-ttu-id="c0102-257">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-257">**References**</span></span>              | [<span data-ttu-id="c0102-258">Atributo de cookie segura</span><span class="sxs-lookup"><span data-stu-id="c0102-258">Secure Cookie Attribute</span></span>](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| <span data-ttu-id="c0102-259">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-259">**Steps**</span></span> | <span data-ttu-id="c0102-260">toomitigate Hola riesgo de divulgación con un ataque de scripting entre sitios (XSS), un nuevo atributo - httpOnly - se ha introducido toocookies y es compatible con todos los exploradores principales.</span><span class="sxs-lookup"><span data-stu-id="c0102-260">toomitigate hello risk of information disclosure with a cross-site scripting (XSS) attack, a new attribute - httpOnly - was introduced toocookies and is supported by all major browsers.</span></span> <span data-ttu-id="c0102-261">atributo de Hello especifica que una cookie no es accesible a través de la secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="c0102-261">hello attribute specifies that a cookie is not accessible through script.</span></span> <span data-ttu-id="c0102-262">Mediante el uso de cookies HttpOnly, una aplicación web reduce la posibilidad de Hola que información confidencial contenida en la cookie de hello puede robo mediante un script y enviarse el sitio Web del atacante tooan.</span><span class="sxs-lookup"><span data-stu-id="c0102-262">By using HttpOnly cookies, a web application reduces hello possibility that sensitive information contained in hello cookie can be stolen via script and sent tooan attacker's website.</span></span> |

### <a name="example"></a><span data-ttu-id="c0102-263">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-263">Example</span></span>
<span data-ttu-id="c0102-264">Todas las aplicaciones basadas en HTTP que utilizan cookies deben especificar HttpOnly en definición de la cookie de hello, mediante la implementación después de la configuración en el archivo web.config:</span><span class="sxs-lookup"><span data-stu-id="c0102-264">All HTTP-based applications that use cookies should specify HttpOnly in hello cookie definition, by implementing following configuration in web.config:</span></span>
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| <span data-ttu-id="c0102-265">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-265">Title</span></span>                   | <span data-ttu-id="c0102-266">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-266">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-267">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-267">**Component**</span></span>               | <span data-ttu-id="c0102-268">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="c0102-268">Web Application</span></span> | 
| <span data-ttu-id="c0102-269">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-269">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-270">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-270">Build</span></span> |  
| <span data-ttu-id="c0102-271">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-271">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-272">Formularios Web Forms</span><span class="sxs-lookup"><span data-stu-id="c0102-272">Web Forms</span></span> |
| <span data-ttu-id="c0102-273">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-273">**Attributes**</span></span>              | <span data-ttu-id="c0102-274">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-274">N/A</span></span>  |
| <span data-ttu-id="c0102-275">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-275">**References**</span></span>              | [<span data-ttu-id="c0102-276">Propiedad FormsAuthentication.RequireSSL</span><span class="sxs-lookup"><span data-stu-id="c0102-276">FormsAuthentication.RequireSSL Property</span></span>](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| <span data-ttu-id="c0102-277">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-277">**Steps**</span></span> | <span data-ttu-id="c0102-278">Hola RequireSSL valor de propiedad se establece en el archivo de configuración de Hola para una aplicación ASP.NET mediante Hola requireSSL atributo del elemento de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0102-278">hello RequireSSL property value is set in hello configuration file for an ASP.NET application by using hello requireSSL attribute of hello configuration element.</span></span> <span data-ttu-id="c0102-279">Puede especificar en el archivo Web.config de hello para la aplicación ASP.NET si SSL (capa de Sockets seguros) es servidor de toohello de cookie de autenticación de formularios de tooreturn necesario Hola por establecer el atributo requireSSL de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0102-279">You can specify in hello Web.config file for your ASP.NET application whether SSL (Secure Sockets Layer) is required tooreturn hello forms-authentication cookie toohello server by setting hello requireSSL attribute.</span></span>|

### <a name="example"></a><span data-ttu-id="c0102-280">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-280">Example</span></span> 
<span data-ttu-id="c0102-281">Hello ejemplo de código siguiente establece atributo requireSSL de hello en el archivo Web.config de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0102-281">hello following code example sets hello requireSSL attribute in hello Web.config file.</span></span>
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| <span data-ttu-id="c0102-282">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-282">Title</span></span>                   | <span data-ttu-id="c0102-283">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-283">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-284">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-284">**Component**</span></span>               | <span data-ttu-id="c0102-285">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="c0102-285">Web Application</span></span> | 
| <span data-ttu-id="c0102-286">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-286">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-287">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-287">Build</span></span> |  
| <span data-ttu-id="c0102-288">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-288">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-289">MVC5</span><span class="sxs-lookup"><span data-stu-id="c0102-289">MVC5</span></span> |
| <span data-ttu-id="c0102-290">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-290">**Attributes**</span></span>              | <span data-ttu-id="c0102-291">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="c0102-291">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="c0102-292">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-292">**References**</span></span>              | <span data-ttu-id="c0102-293">[Windows Identity Foundation (WIF) Configuration – Part II](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) (Configuración de Windows Identity Foundation: parte II)</span><span class="sxs-lookup"><span data-stu-id="c0102-293">[Windows Identity Foundation (WIF) Configuration – Part II](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/)</span></span> |
| <span data-ttu-id="c0102-294">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-294">**Steps**</span></span> | <span data-ttu-id="c0102-295">atributo httpOnly de tooset para FedAuth cookies, el valor del atributo de hideFromCsript que debe establecerse tooTrue.</span><span class="sxs-lookup"><span data-stu-id="c0102-295">tooset httpOnly attribute for FedAuth cookies, hideFromCsript attribute value should be set tooTrue.</span></span> |

### <a name="example"></a><span data-ttu-id="c0102-296">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-296">Example</span></span>
<span data-ttu-id="c0102-297">Configuración siguiente muestra la configuración correcta de hello:</span><span class="sxs-lookup"><span data-stu-id="c0102-297">Following configuration shows hello correct configuration:</span></span>
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <span data-ttu-id="c0102-298"><a id="csrf-asp"></a>Mitigue el riesgo de ataques de falsificación de solicitud entre sitios (CSRF) en páginas web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c0102-298"><a id="csrf-asp"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>

| <span data-ttu-id="c0102-299">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-299">Title</span></span>                   | <span data-ttu-id="c0102-300">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-300">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-301">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-301">**Component**</span></span>               | <span data-ttu-id="c0102-302">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="c0102-302">Web Application</span></span> | 
| <span data-ttu-id="c0102-303">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-303">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-304">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-304">Build</span></span> |  
| <span data-ttu-id="c0102-305">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-305">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-306">Genérico</span><span class="sxs-lookup"><span data-stu-id="c0102-306">Generic</span></span> |
| <span data-ttu-id="c0102-307">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-307">**Attributes**</span></span>              | <span data-ttu-id="c0102-308">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-308">N/A</span></span>  |
| <span data-ttu-id="c0102-309">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-309">**References**</span></span>              | <span data-ttu-id="c0102-310">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-310">N/A</span></span>  |
| <span data-ttu-id="c0102-311">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-311">**Steps**</span></span> | <span data-ttu-id="c0102-312">Falsificación de solicitud entre sitios (CSRF o XSRF) es un tipo de ataque en el que un atacante puede llevar a cabo acciones en el contexto de seguridad de Hola de sesión establecido de un usuario diferente en un sitio web.</span><span class="sxs-lookup"><span data-stu-id="c0102-312">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="c0102-313">el objetivo de Hello es toomodify o eliminar el contenido, si el sitio web utilizado como destino de Hola se basa exclusivamente en la solicitud recibida de tooauthenticate de cookies de sesión.</span><span class="sxs-lookup"><span data-stu-id="c0102-313">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="c0102-314">Un atacante podría aprovechar esta vulnerabilidad obteniendo una dirección URL con un comando de tooload de explorador de un usuario diferente de un sitio vulnerable en la que el usuario de hello ya se registra en.</span><span class="sxs-lookup"><span data-stu-id="c0102-314">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="c0102-315">Hay muchas maneras para un toodo atacante que, como mediante el hospedaje de un sitio web diferente carga un recurso de servidor vulnerable Hola o tooclick de usuario Hola al obtener un vínculo.</span><span class="sxs-lookup"><span data-stu-id="c0102-315">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="c0102-316">ataque de Hello puede evitarse si servidor hello envía a un cliente toohello token adicional, requiere Hola cliente tooinclude ese token en todas las solicitudes futuras y comprueba que todas las solicitudes futuras incluyen un símbolo (token) que pertenece a toohello sesión actual, como por uso de hello AntiForgeryToken de ASP.NET o estado de vista.</span><span class="sxs-lookup"><span data-stu-id="c0102-316">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="c0102-317">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-317">Title</span></span>                   | <span data-ttu-id="c0102-318">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-318">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-319">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-319">**Component**</span></span>               | <span data-ttu-id="c0102-320">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="c0102-320">Web Application</span></span> | 
| <span data-ttu-id="c0102-321">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-321">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-322">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-322">Build</span></span> |  
| <span data-ttu-id="c0102-323">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-323">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-324">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="c0102-324">MVC5, MVC6</span></span> |
| <span data-ttu-id="c0102-325">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-325">**Attributes**</span></span>              | <span data-ttu-id="c0102-326">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-326">N/A</span></span>  |
| <span data-ttu-id="c0102-327">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-327">**References**</span></span>              | <span data-ttu-id="c0102-328">[XSRF/CSRF Prevention in ASP.NET MVC and Web Pages](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) (Prevención de XSRF y CSRF en ASP.NET MVC y Web Pages)</span><span class="sxs-lookup"><span data-stu-id="c0102-328">[XSRF/CSRF Prevention in ASP.NET MVC and Web Pages](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages)</span></span> |
| <span data-ttu-id="c0102-329">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-329">**Steps**</span></span> | <span data-ttu-id="c0102-330">Formularios de Anti-CSRF y ASP.NET MVC - Hola de uso `AntiForgeryToken` método auxiliar para las vistas; put un `Html.AntiForgeryToken()` en forma de hello, por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="c0102-330">Anti-CSRF and ASP.NET MVC forms - Use hello `AntiForgeryToken` helper method on Views; put an `Html.AntiForgeryToken()` into hello form, for example,</span></span>|

### <a name="example"></a><span data-ttu-id="c0102-331">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-331">Example</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a><span data-ttu-id="c0102-332">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-332">Example</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="c0102-333">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-333">Example</span></span>
<span data-ttu-id="c0102-334">En hello mismo tiempo, visitante de Hola de Html.AntiForgeryToken() proporciona una cookie denominada __RequestVerificationToken con hello mismo valor que el valor de hidden aleatorio Hola mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c0102-334">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="c0102-335">A continuación, toovalidate una solicitud de post de formulario entrante, agregue el método de acción de hello [ValidateAntiForgeryToken] filtro toohello destino.</span><span class="sxs-lookup"><span data-stu-id="c0102-335">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="c0102-336">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c0102-336">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="c0102-337">Filtro de autorización que comprueba que:</span><span class="sxs-lookup"><span data-stu-id="c0102-337">Authorization filter that checks that:</span></span>
* <span data-ttu-id="c0102-338">solicitud entrante de Hello tiene una cookie denominada __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="c0102-338">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="c0102-339">Hola entrante solicitud tiene un `Request.Form` entrada llamada __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="c0102-339">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="c0102-340">Estas cookies y `Request.Form` suponiendo que todos los de coincidencia de valores está bien, solicitud de hello pasa a través de forma habitual.</span><span class="sxs-lookup"><span data-stu-id="c0102-340">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="c0102-341">De lo contrario, aparece un error de autorización con el mensaje "No se especificó un token antifalsificación o el que se especificó no era válido".</span><span class="sxs-lookup"><span data-stu-id="c0102-341">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span> 

### <a name="example"></a><span data-ttu-id="c0102-342">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-342">Example</span></span>
<span data-ttu-id="c0102-343">Anti-CSRF y AJAX: token de formulario de Hola puede constituir un problema para las solicitudes de AJAX, porque una solicitud AJAX puede enviar datos JSON, no los datos de formulario HTML.</span><span class="sxs-lookup"><span data-stu-id="c0102-343">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="c0102-344">Una solución es toosend Hola símbolos (tokens) en un encabezado HTTP personalizado.</span><span class="sxs-lookup"><span data-stu-id="c0102-344">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="c0102-345">Hola código siguiente usa tokens de Hola de toogenerate de sintaxis de Razor y, a continuación, agrega la solicitud de AJAX de hello tokens tooan.</span><span class="sxs-lookup"><span data-stu-id="c0102-345">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="c0102-346">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-346">Example</span></span>
<span data-ttu-id="c0102-347">Cuando se procesa la solicitud de hello, extraer tokens Hola Hola encabezado de solicitud.</span><span class="sxs-lookup"><span data-stu-id="c0102-347">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="c0102-348">A continuación, llame al método de AntiForgery.Validate Hola tokens de hello toovalidate.</span><span class="sxs-lookup"><span data-stu-id="c0102-348">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="c0102-349">Hola método Validate produce una excepción si los tokens de hello no son válidos.</span><span class="sxs-lookup"><span data-stu-id="c0102-349">hello Validate method throws an exception if hello tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| <span data-ttu-id="c0102-350">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-350">Title</span></span>                   | <span data-ttu-id="c0102-351">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-351">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-352">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-352">**Component**</span></span>               | <span data-ttu-id="c0102-353">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="c0102-353">Web Application</span></span> | 
| <span data-ttu-id="c0102-354">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-354">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-355">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-355">Build</span></span> |  
| <span data-ttu-id="c0102-356">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-356">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-357">Formularios Web Forms</span><span class="sxs-lookup"><span data-stu-id="c0102-357">Web Forms</span></span> |
| <span data-ttu-id="c0102-358">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-358">**Attributes**</span></span>              | <span data-ttu-id="c0102-359">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-359">N/A</span></span>  |
| <span data-ttu-id="c0102-360">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-360">**References**</span></span>              | [<span data-ttu-id="c0102-361">Tomar ventaja de ASP.NET características integradas tooFend Off Web ataques</span><span class="sxs-lookup"><span data-stu-id="c0102-361">Take Advantage of ASP.NET Built-in Features tooFend Off Web Attacks</span></span>](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| <span data-ttu-id="c0102-362">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-362">**Steps**</span></span> | <span data-ttu-id="c0102-363">Ataques CSRF en aplicaciones de WebForm según pueden ser mitigados estableciendo ViewStateUserKey tooa cadena aleatoria que varía para cada usuario - Id. de usuario o, mejor aún, Id.</span><span class="sxs-lookup"><span data-stu-id="c0102-363">CSRF attacks in WebForm based applications can be mitigated by setting ViewStateUserKey tooa random string that varies for each user - user ID or, better yet, session ID.</span></span> <span data-ttu-id="c0102-364">Por diversas razones técnicas y sociales, el id. de sesión es mucho más adecuado porque es imprevisible, agota el tiempo de espera y varía para cada usuario.</span><span class="sxs-lookup"><span data-stu-id="c0102-364">For a number of technical and social reasons, session ID is a much better fit because a session ID is unpredictable, times out, and varies on a per-user basis.</span></span>|

### <a name="example"></a><span data-ttu-id="c0102-365">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-365">Example</span></span>
<span data-ttu-id="c0102-366">Este es código de hello necesite toohave en todas las páginas.</span><span class="sxs-lookup"><span data-stu-id="c0102-366">Here's hello code you need toohave in all of your pages:</span></span>
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <span data-ttu-id="c0102-367"><a id="inactivity-lifetime"></a>Configure la sesión para la duración de la inactividad</span><span class="sxs-lookup"><span data-stu-id="c0102-367"><a id="inactivity-lifetime"></a>Set up session for inactivity lifetime</span></span>

| <span data-ttu-id="c0102-368">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-368">Title</span></span>                   | <span data-ttu-id="c0102-369">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-369">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-370">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-370">**Component**</span></span>               | <span data-ttu-id="c0102-371">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="c0102-371">Web Application</span></span> | 
| <span data-ttu-id="c0102-372">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-372">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-373">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-373">Build</span></span> |  
| <span data-ttu-id="c0102-374">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-374">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-375">Genérico</span><span class="sxs-lookup"><span data-stu-id="c0102-375">Generic</span></span> |
| <span data-ttu-id="c0102-376">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-376">**Attributes**</span></span>              | <span data-ttu-id="c0102-377">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-377">N/A</span></span>  |
| <span data-ttu-id="c0102-378">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-378">**References**</span></span>              | <span data-ttu-id="c0102-379">[Propiedad HttpSessionState.Timeout](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="c0102-379">[HttpSessionState.Timeout Property](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span></span> |
| <span data-ttu-id="c0102-380">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-380">**Steps**</span></span> | <span data-ttu-id="c0102-381">Tiempo de espera de sesión representa Hola eventos se producen cuando un usuario no realiza ninguna acción en un sitio web durante un intervalo (definido por el servidor web).</span><span class="sxs-lookup"><span data-stu-id="c0102-381">Session timeout represents hello event occurring when a user does not perform any action on a web site during a interval (defined by web server).</span></span> <span data-ttu-id="c0102-382">Hola eventos, en el lado servidor, cambiar el estado de Hola de too'invalid de sesión de usuario de hello' (por ejemplo "no se utiliza ya") e indicarle hello web server toodestroy que (eliminar todos los datos contenidos en él).</span><span class="sxs-lookup"><span data-stu-id="c0102-382">hello event, on server side, change hello status of hello user session too'invalid' (for example  "not used anymore") and instruct hello web server toodestroy it (deleting all data contained into it).</span></span> <span data-ttu-id="c0102-383">Hello ejemplo de código siguiente establece minutos de too15 de atributo de sesión de tiempo de espera de hello en el archivo Web.config de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0102-383">hello following code example sets hello timeout session attribute too15 minutes in hello Web.config file.</span></span>|

### <a name="example"></a><span data-ttu-id="c0102-384">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-384">Example</span></span>
<span data-ttu-id="c0102-385">``\`XML code <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span><span class="sxs-lookup"><span data-stu-id="c0102-385">``\`XML code <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span></span>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| <span data-ttu-id="c0102-386">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-386">Title</span></span>                   | <span data-ttu-id="c0102-387">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-387">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-388">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-388">**Component**</span></span>               | <span data-ttu-id="c0102-389">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="c0102-389">Web Application</span></span> | 
| <span data-ttu-id="c0102-390">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-390">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-391">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-391">Build</span></span> |  
| <span data-ttu-id="c0102-392">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-392">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-393">Formularios Web Forms</span><span class="sxs-lookup"><span data-stu-id="c0102-393">Web Forms</span></span> |
| <span data-ttu-id="c0102-394">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-394">**Attributes**</span></span>              | <span data-ttu-id="c0102-395">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-395">N/A</span></span>  |
| <span data-ttu-id="c0102-396">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-396">**References**</span></span>              | <span data-ttu-id="c0102-397">[Elemento forms para authentication (Esquema de configuración de ASP.NET)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="c0102-397">[forms Element for authentication (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span></span> |
| <span data-ttu-id="c0102-398">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-398">**Steps**</span></span> | <span data-ttu-id="c0102-399">Establece los minutos de hello too15 de tiempo de espera de cookie de vale de autenticación de formularios</span><span class="sxs-lookup"><span data-stu-id="c0102-399">Set hello Forms Authentication Ticket cookie timeout too15 minutes</span></span>|

### <a name="example"></a><span data-ttu-id="c0102-400">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-400">Example</span></span>
<span data-ttu-id="c0102-401">``\`XML code <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span><span class="sxs-lookup"><span data-stu-id="c0102-401">``\`XML code <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span></span>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a><span data-ttu-id="c0102-402">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-402">Example</span></span>
<span data-ttu-id="c0102-403">También Hola emitidos duración del token de SAML notificaciones ADFS debe establecerse too15 minutos, mediante la ejecución de hello siguiente comando de powershell en el servidor de ADFS de hello:</span><span class="sxs-lookup"><span data-stu-id="c0102-403">Also hello ADFS issued SAML claim token's lifetime should be set too15 minutes, by executing hello following powershell command on hello ADFS server:</span></span>
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <span data-ttu-id="c0102-404"><a id="proper-app-logout"></a>Implemente el cierre de sesión correcto de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="c0102-404"><a id="proper-app-logout"></a>Implement proper logout from hello application</span></span>

| <span data-ttu-id="c0102-405">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-405">Title</span></span>                   | <span data-ttu-id="c0102-406">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-406">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-407">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-407">**Component**</span></span>               | <span data-ttu-id="c0102-408">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="c0102-408">Web Application</span></span> | 
| <span data-ttu-id="c0102-409">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-409">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-410">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-410">Build</span></span> |  
| <span data-ttu-id="c0102-411">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-411">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-412">Genérico</span><span class="sxs-lookup"><span data-stu-id="c0102-412">Generic</span></span> |
| <span data-ttu-id="c0102-413">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-413">**Attributes**</span></span>              | <span data-ttu-id="c0102-414">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-414">N/A</span></span>  |
| <span data-ttu-id="c0102-415">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-415">**References**</span></span>              | <span data-ttu-id="c0102-416">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-416">N/A</span></span>  |
| <span data-ttu-id="c0102-417">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-417">**Steps**</span></span> | <span data-ttu-id="c0102-418">Realizar inicio de sesión correcto Out desde la aplicación hello, cuando las pulsaciones usuario cierre sesión botón.</span><span class="sxs-lookup"><span data-stu-id="c0102-418">Perform proper Sign Out from hello application, when user presses log out button.</span></span> <span data-ttu-id="c0102-419">Al cerrar la sesión, la aplicación debe destruir la sesión del usuario y también restablecer y anular el valor de la cookie de la sesión, así como restablecer y anular el valor de la cookie de autenticación.</span><span class="sxs-lookup"><span data-stu-id="c0102-419">Upon logout, application should destroy user's session, and also reset and nullify session cookie value, along with resetting and nullifying authentication cookie value.</span></span> <span data-ttu-id="c0102-420">Además, cuando varias sesiones tooa ligada identidad de usuario único, debe terminarse colectivamente en servidor hello en tiempo de espera o cierre de sesión.</span><span class="sxs-lookup"><span data-stu-id="c0102-420">Also, when multiple sessions are tied tooa single user identity, they must be collectively terminated on hello server side at timeout or logout.</span></span> <span data-ttu-id="c0102-421">Por último, asegúrese de que la funcionalidad de cierre de sesión esté disponible en todas las páginas.</span><span class="sxs-lookup"><span data-stu-id="c0102-421">Lastly, ensure that Logout functionality is available on every page.</span></span> |

## <span data-ttu-id="c0102-422"><a id="csrf-api"></a>Mitigue el riesgo de ataques de falsificación de solicitud entre sitios (CSRF) en las API web de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c0102-422"><a id="csrf-api"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>

| <span data-ttu-id="c0102-423">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-423">Title</span></span>                   | <span data-ttu-id="c0102-424">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-424">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-425">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-425">**Component**</span></span>               | <span data-ttu-id="c0102-426">API Web</span><span class="sxs-lookup"><span data-stu-id="c0102-426">Web API</span></span> | 
| <span data-ttu-id="c0102-427">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-427">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-428">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-428">Build</span></span> |  
| <span data-ttu-id="c0102-429">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-429">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-430">Genérico</span><span class="sxs-lookup"><span data-stu-id="c0102-430">Generic</span></span> |
| <span data-ttu-id="c0102-431">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-431">**Attributes**</span></span>              | <span data-ttu-id="c0102-432">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-432">N/A</span></span>  |
| <span data-ttu-id="c0102-433">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-433">**References**</span></span>              | <span data-ttu-id="c0102-434">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-434">N/A</span></span>  |
| <span data-ttu-id="c0102-435">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-435">**Steps**</span></span> | <span data-ttu-id="c0102-436">Falsificación de solicitud entre sitios (CSRF o XSRF) es un tipo de ataque en el que un atacante puede llevar a cabo acciones en el contexto de seguridad de Hola de sesión establecido de un usuario diferente en un sitio web.</span><span class="sxs-lookup"><span data-stu-id="c0102-436">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="c0102-437">el objetivo de Hello es toomodify o eliminar el contenido, si el sitio web utilizado como destino de Hola se basa exclusivamente en la solicitud recibida de tooauthenticate de cookies de sesión.</span><span class="sxs-lookup"><span data-stu-id="c0102-437">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="c0102-438">Un atacante podría aprovechar esta vulnerabilidad obteniendo una dirección URL con un comando de tooload de explorador de un usuario diferente de un sitio vulnerable en la que el usuario de hello ya se registra en.</span><span class="sxs-lookup"><span data-stu-id="c0102-438">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="c0102-439">Hay muchas maneras para un toodo atacante que, como mediante el hospedaje de un sitio web diferente carga un recurso de servidor vulnerable Hola o tooclick de usuario Hola al obtener un vínculo.</span><span class="sxs-lookup"><span data-stu-id="c0102-439">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="c0102-440">ataque de Hello puede evitarse si servidor hello envía a un cliente toohello token adicional, requiere Hola cliente tooinclude ese token en todas las solicitudes futuras y comprueba que todas las solicitudes futuras incluyen un símbolo (token) que pertenece a toohello sesión actual, como por uso de hello AntiForgeryToken de ASP.NET o estado de vista.</span><span class="sxs-lookup"><span data-stu-id="c0102-440">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="c0102-441">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-441">Title</span></span>                   | <span data-ttu-id="c0102-442">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-442">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-443">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-443">**Component**</span></span>               | <span data-ttu-id="c0102-444">API Web</span><span class="sxs-lookup"><span data-stu-id="c0102-444">Web API</span></span> | 
| <span data-ttu-id="c0102-445">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-445">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-446">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-446">Build</span></span> |  
| <span data-ttu-id="c0102-447">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-447">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-448">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="c0102-448">MVC5, MVC6</span></span> |
| <span data-ttu-id="c0102-449">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-449">**Attributes**</span></span>              | <span data-ttu-id="c0102-450">N/D</span><span class="sxs-lookup"><span data-stu-id="c0102-450">N/A</span></span>  |
| <span data-ttu-id="c0102-451">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-451">**References**</span></span>              | <span data-ttu-id="c0102-452">[Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) (Prevención de ataques de falsificación de solicitud entre sitios [CSRF] en ASP.NET Web API)</span><span class="sxs-lookup"><span data-stu-id="c0102-452">[Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks)</span></span> |
| <span data-ttu-id="c0102-453">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-453">**Steps**</span></span> | <span data-ttu-id="c0102-454">Anti-CSRF y AJAX: token de formulario de Hola puede constituir un problema para las solicitudes de AJAX, porque una solicitud AJAX puede enviar datos JSON, no los datos de formulario HTML.</span><span class="sxs-lookup"><span data-stu-id="c0102-454">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="c0102-455">Una solución es toosend Hola símbolos (tokens) en un encabezado HTTP personalizado.</span><span class="sxs-lookup"><span data-stu-id="c0102-455">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="c0102-456">Hola código siguiente usa tokens de Hola de toogenerate de sintaxis de Razor y, a continuación, agrega la solicitud de AJAX de hello tokens tooan.</span><span class="sxs-lookup"><span data-stu-id="c0102-456">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> |

### <a name="example"></a><span data-ttu-id="c0102-457">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-457">Example</span></span>
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="c0102-458">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-458">Example</span></span>
<span data-ttu-id="c0102-459">Cuando se procesa la solicitud de hello, extraer tokens Hola Hola encabezado de solicitud.</span><span class="sxs-lookup"><span data-stu-id="c0102-459">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="c0102-460">A continuación, llame al método de AntiForgery.Validate Hola tokens de hello toovalidate.</span><span class="sxs-lookup"><span data-stu-id="c0102-460">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="c0102-461">Hola método Validate produce una excepción si los tokens de hello no son válidos.</span><span class="sxs-lookup"><span data-stu-id="c0102-461">hello Validate method throws an exception if hello tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a><span data-ttu-id="c0102-462">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-462">Example</span></span>
<span data-ttu-id="c0102-463">Anti-CSRF y formularios de ASP.NET MVC - Hola Utilice método de aplicación auxiliar de AntiForgeryToken en las vistas; Coloque un Html.AntiForgeryToken() en forma de hello, por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="c0102-463">Anti-CSRF and ASP.NET MVC forms - Use hello AntiForgeryToken helper method on Views; put an Html.AntiForgeryToken() into hello form, for example,</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a><span data-ttu-id="c0102-464">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-464">Example</span></span>
<span data-ttu-id="c0102-465">ejemplo de Hola anterior dará como resultado algo parecido a Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="c0102-465">hello example above will output something like hello following:</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="c0102-466">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-466">Example</span></span>
<span data-ttu-id="c0102-467">En hello mismo tiempo, visitante de Hola de Html.AntiForgeryToken() proporciona una cookie denominada __RequestVerificationToken con hello mismo valor que el valor de hidden aleatorio Hola mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c0102-467">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="c0102-468">A continuación, toovalidate una solicitud de post de formulario entrante, agregue el método de acción de hello [ValidateAntiForgeryToken] filtro toohello destino.</span><span class="sxs-lookup"><span data-stu-id="c0102-468">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="c0102-469">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c0102-469">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="c0102-470">Filtro de autorización que comprueba que:</span><span class="sxs-lookup"><span data-stu-id="c0102-470">Authorization filter that checks that:</span></span>
* <span data-ttu-id="c0102-471">solicitud entrante de Hello tiene una cookie denominada __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="c0102-471">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="c0102-472">Hola entrante solicitud tiene un `Request.Form` entrada llamada __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="c0102-472">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="c0102-473">Estas cookies y `Request.Form` suponiendo que todos los de coincidencia de valores está bien, solicitud de hello pasa a través de forma habitual.</span><span class="sxs-lookup"><span data-stu-id="c0102-473">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="c0102-474">De lo contrario, aparece un error de autorización con el mensaje "No se especificó un token antifalsificación o el que se especificó no era válido".</span><span class="sxs-lookup"><span data-stu-id="c0102-474">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span>

| <span data-ttu-id="c0102-475">Título</span><span class="sxs-lookup"><span data-stu-id="c0102-475">Title</span></span>                   | <span data-ttu-id="c0102-476">Detalles</span><span class="sxs-lookup"><span data-stu-id="c0102-476">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0102-477">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c0102-477">**Component**</span></span>               | <span data-ttu-id="c0102-478">API Web</span><span class="sxs-lookup"><span data-stu-id="c0102-478">Web API</span></span> | 
| <span data-ttu-id="c0102-479">**Fase de SDL**</span><span class="sxs-lookup"><span data-stu-id="c0102-479">**SDL Phase**</span></span>               | <span data-ttu-id="c0102-480">Compilación</span><span class="sxs-lookup"><span data-stu-id="c0102-480">Build</span></span> |  
| <span data-ttu-id="c0102-481">**Tecnologías aplicables**</span><span class="sxs-lookup"><span data-stu-id="c0102-481">**Applicable Technologies**</span></span> | <span data-ttu-id="c0102-482">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="c0102-482">MVC5, MVC6</span></span> |
| <span data-ttu-id="c0102-483">**Atributos**</span><span class="sxs-lookup"><span data-stu-id="c0102-483">**Attributes**</span></span>              | <span data-ttu-id="c0102-484">Proveedor de identidades; ADFS, Proveedor de identidades; Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0102-484">Identity Provider - ADFS, Identity Provider - Azure AD</span></span> |
| <span data-ttu-id="c0102-485">**Referencias**</span><span class="sxs-lookup"><span data-stu-id="c0102-485">**References**</span></span>              | <span data-ttu-id="c0102-486">[Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) (Protección de una API web con cuentas individuales e inicio de sesión local en ASP.NET Web API 2.2)</span><span class="sxs-lookup"><span data-stu-id="c0102-486">[Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api)</span></span> |
| <span data-ttu-id="c0102-487">**Pasos**</span><span class="sxs-lookup"><span data-stu-id="c0102-487">**Steps**</span></span> | <span data-ttu-id="c0102-488">Si Hola API Web está protegido mediante OAuth 2.0, a continuación, espera un token de portador en solicitud encabezado y concede acceso toohello solicitud de autorización solo si el token de hello es válido.</span><span class="sxs-lookup"><span data-stu-id="c0102-488">If hello Web API is secured using OAuth 2.0, then it expects a bearer token in Authorization request header and grants access toohello request only if hello token is valid.</span></span> <span data-ttu-id="c0102-489">A diferencia de autenticación basado en cookies, los exploradores no conecte toorequests de tokens de portador de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0102-489">Unlike cookie based authentication, browsers do not attach hello bearer tokens toorequests.</span></span> <span data-ttu-id="c0102-490">Hola que solicita el cliente necesita tooexplicitly adjuntar el token de portador de hello en el encabezado de solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0102-490">hello requesting client needs tooexplicitly attach hello bearer token in hello request header.</span></span> <span data-ttu-id="c0102-491">Por lo tanto, para las API web de ASP.NET protegidas con OAuth 2.0, los tokens de portador se consideran una defensa contra los ataques CSRF.</span><span class="sxs-lookup"><span data-stu-id="c0102-491">Therefore, for ASP.NET Web APIs protected using OAuth 2.0, bearer tokens are considered as a defense against CSRF attacks.</span></span> <span data-ttu-id="c0102-492">Tenga en cuenta que si parte MVC de Hola de aplicación hello usa autenticación de formularios (es decir, usa cookies), tokens antifalsificación tienen toobe utilizado por la aplicación web MVC de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0102-492">Please note that if hello MVC portion of hello application uses forms authentication (i.e., uses cookies), anti-forgery tokens have toobe used by hello MVC web app.</span></span> |

### <a name="example"></a><span data-ttu-id="c0102-493">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0102-493">Example</span></span>
<span data-ttu-id="c0102-494">Hola API Web tiene toobe informado toorely sólo en tokens de portador y no en cookies.</span><span class="sxs-lookup"><span data-stu-id="c0102-494">hello Web API has toobe informed toorely ONLY on bearer tokens and not on cookies.</span></span> <span data-ttu-id="c0102-495">Se puede realizar por hello siguiente configuración en `WebApiConfig.Register` método: ''' configuración de código de C-Sharp. SuppressDefaultHostAuthentication(); config. Filters.Add (nueva HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span><span class="sxs-lookup"><span data-stu-id="c0102-495">It can be done by hello following configuration in `WebApiConfig.Register` method: ``\`C-Sharp code config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span></span>
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
