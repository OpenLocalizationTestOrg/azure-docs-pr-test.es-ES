---
title: "Sustitución de clave en Azure AD aaaSigning | Documentos de Microsoft"
description: "Este artículo describe Hola prácticas recomendadas de sustitución de la clave de firma para Azure Active Directory"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="aad68-103">Sustitución de claves de firma de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aad68-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="aad68-104">Este tema describe lo que necesita tooknow acerca de las claves públicas Hola que se usan en tokens de seguridad de Azure Active Directory (Azure AD) toosign.</span><span class="sxs-lookup"><span data-stu-id="aad68-104">This topic discusses what you need tooknow about hello public keys that are used in Azure Active Directory (Azure AD) toosign security tokens.</span></span> <span data-ttu-id="aad68-105">Es importante toonote que estas claves se sustituyen de forma periódica y, en caso de emergencia, se deben sustituirse inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="aad68-105">It is important toonote that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="aad68-106">Todas las aplicaciones que usan Azure AD deben ser capaz de tooprogrammatically identificador hello sustitución de claves proceso o establezca un proceso de sustitución manual periódica.</span><span class="sxs-lookup"><span data-stu-id="aad68-106">All applications that use Azure AD should be able tooprogrammatically handle hello key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="aad68-107">Seguir leyendo toounderstand cómo funcionan las claves de hello, cómo tooassess Hola impacto de la aplicación de tooyour de sustitución incremental de hello y cómo tooupdate la aplicación o establecer una sustitución de claves de sustitución manual periódica proceso toohandle si es necesario.</span><span class="sxs-lookup"><span data-stu-id="aad68-107">Continue reading toounderstand how hello keys work, how tooassess hello impact of hello rollover tooyour application and how tooupdate your application or establish a periodic manual rollover process toohandle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="aad68-108">Información general sobre las claves de firma de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aad68-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="aad68-109">Azure AD usa criptografía de clave pública depende de la industria estándares tooestablish confianza entre él y hello las aplicaciones que lo usan.</span><span class="sxs-lookup"><span data-stu-id="aad68-109">Azure AD uses public-key cryptography built on industry standards tooestablish trust between itself and hello applications that use it.</span></span> <span data-ttu-id="aad68-110">En la práctica, esto funciona en hello siguiente forma: Azure AD usa una clave de firma que consta de un par de claves público y privado.</span><span class="sxs-lookup"><span data-stu-id="aad68-110">In practical terms, this works in hello following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="aad68-111">Cuando un usuario inicia sesión en la aplicación tooan que usa Azure AD para la autenticación, Azure AD crea un token de seguridad que contiene información acerca del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-111">When a user signs in tooan application that uses Azure AD for authentication, Azure AD creates a security token that contains information about hello user.</span></span> <span data-ttu-id="aad68-112">Este token está firmado por Azure AD utilizando su clave privada antes de enviarlo aplicación toohello atrás.</span><span class="sxs-lookup"><span data-stu-id="aad68-112">This token is signed by Azure AD using its private key before it is sent back toohello application.</span></span> <span data-ttu-id="aad68-113">tooverify que Hola token es válido y realmente se ha originado en Azure AD, aplicación hello debe validar la firma del token de hello usando la clave pública de hello expuesta por Azure AD que se encuentra en el inquilino de hello [documento de detección de OpenID Connect](http://openid.net/specs/openid-connect-discovery-1_0.html) o SAML/WS-Fed [documento de metadatos de federación](active-directory-federation-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="aad68-113">tooverify that hello token is valid and actually originated from Azure AD, hello application must validate hello token’s signature using hello public key exposed by Azure AD that is contained in hello tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="aad68-114">Por motivos de seguridad de Azure AD firma clave revierte de forma periódica y, en caso de hello de emergencia, se deben sustituirse inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="aad68-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in hello case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="aad68-115">Cualquier aplicación que se integra con Azure AD debe estar preparado toohandle un evento de sustitución de claves independientemente de la frecuencia con la que ocurra.</span><span class="sxs-lookup"><span data-stu-id="aad68-115">Any application that integrates with Azure AD should be prepared toohandle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="aad68-116">Si no es así, y la aplicación trata de toouse una firma de hello expiradas tooverify clave en un símbolo (token), se producirá un error en la solicitud de inicio de sesión Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-116">If it doesn’t, and your application attempts toouse an expired key tooverify hello signature on a token, hello sign-in request will fail.</span></span>

<span data-ttu-id="aad68-117">Siempre hay más de una clave válida disponible en el documento de detección de OpenID Connect de Hola y documento de metadatos de federación de Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-117">There is always more than one valid key available in hello OpenID Connect discovery document and hello federation metadata document.</span></span> <span data-ttu-id="aad68-118">La aplicación debe estar preparada toouse cualquiera de las claves de hello especificada en el documento de hello, ya que se puede sustituir una clave pronto, otra puede ser su sustituta y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="aad68-118">Your application should be prepared toouse any of hello keys specified in hello document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a><span data-ttu-id="aad68-119">¿Cómo tooassess si su aplicación se verá afectada y qué toodo sobre él</span><span class="sxs-lookup"><span data-stu-id="aad68-119">How tooassess if your application will be affected and what toodo about it</span></span>
<span data-ttu-id="aad68-120">Cómo la aplicación controla la sustitución de claves depende de variables como tipo de Hola de aplicación o qué protocolo de identidad y la biblioteca se usó.</span><span class="sxs-lookup"><span data-stu-id="aad68-120">How your application handles key rollover depends on variables such as hello type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="aad68-121">Hola las siguientes secciones se evaluación si los tipos más comunes de Hola de aplicaciones se ven afectados por la sustitución de claves de Hola y ofrecen orientación sobre cómo tooupdate Hola sustitución automática de aplicación toosupport o actualizar manualmente la clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-121">hello sections below assess whether hello most common types of applications are impacted by hello key rollover and provide guidance on how tooupdate hello application toosupport automatic rollover or manually update hello key.</span></span>

* [<span data-ttu-id="aad68-122">Aplicaciones de cliente nativas que acceden a recursos</span><span class="sxs-lookup"><span data-stu-id="aad68-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="aad68-123">Aplicaciones y API web que acceden a recursos</span><span class="sxs-lookup"><span data-stu-id="aad68-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="aad68-124">Aplicaciones y API web que protegen recursos y creadas mediante Servicios de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="aad68-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="aad68-125">Aplicaciones y API web que protegen recursos mediante middleware .NET OWIN OpenID Connect, WS-Fed o WindowsAzureActiveDirectoryBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="aad68-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="aad68-126">Aplicaciones y API web que protegen recursos mediante el middleware .NET Core OpenID Connect o JwtBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="aad68-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="aad68-127">Aplicaciones y API web que protegen recursos mediante el módulo Node.js passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="aad68-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="aad68-128">Aplicaciones y API web de protección de recursos y creadas con Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="aad68-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="aad68-129">Aplicaciones Web de protección de recursos y creadas con Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="aad68-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="aad68-130">API web de protección de recursos y creadas con Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="aad68-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="aad68-131">Aplicaciones web de protección de recursos y creadas con Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="aad68-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="aad68-132">Aplicaciones web de protección de recursos y creadas con Visual Studio 2010, 2008 o mediante Windows Identity Foundation</span><span class="sxs-lookup"><span data-stu-id="aad68-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="aad68-133">Aplicaciones Web / API de protección de los recursos cualquiera otras bibliotecas o implementar manualmente cualquiera de hello admite el uso de protocolos</span><span class="sxs-lookup"><span data-stu-id="aad68-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>](#other)

<span data-ttu-id="aad68-134">Esta guía **no** es aplicable para:</span><span class="sxs-lookup"><span data-stu-id="aad68-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="aad68-135">Las aplicaciones agregadas desde la Galería de aplicaciones de Azure AD (incluyendo personalizado) tienen instrucciones independientes con lo que respecta toosigning claves.</span><span class="sxs-lookup"><span data-stu-id="aad68-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards toosigning keys.</span></span> [<span data-ttu-id="aad68-136">Más información.</span><span class="sxs-lookup"><span data-stu-id="aad68-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="aad68-137">Las aplicaciones publicadas a través de proxy de aplicación no tienen tooworry sobre claves de firma en local.</span><span class="sxs-lookup"><span data-stu-id="aad68-137">On-premises applications published via application proxy don't have tooworry about signing keys.</span></span>

### <span data-ttu-id="aad68-138"><a name="nativeclient"></a>Aplicaciones de cliente nativas que acceden a recursos</span><span class="sxs-lookup"><span data-stu-id="aad68-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="aad68-139">Las aplicaciones que solo acceden a los recursos (es decir,</span><span class="sxs-lookup"><span data-stu-id="aad68-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="aad68-140">Microsoft Graph, KeyVault, API de Outlook y otras APIs Microsoft) generalmente solo obtienen un token y pasan a toohello propietario del recurso.</span><span class="sxs-lookup"><span data-stu-id="aad68-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="aad68-141">Dado que no están protegiendo todos los recursos, se inspecciona el token de hello y, por tanto, no es necesario tooensure que está firmado correctamente.</span><span class="sxs-lookup"><span data-stu-id="aad68-141">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="aad68-142">Si escritorio o móvil, las aplicaciones cliente nativas, entran en esta categoría y, por tanto, no se ven afectadas por la sustitución de Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="aad68-143"><a name="webclient"></a>Aplicaciones y API web que acceden a recursos</span><span class="sxs-lookup"><span data-stu-id="aad68-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="aad68-144">Las aplicaciones que solo acceden a los recursos (es decir,</span><span class="sxs-lookup"><span data-stu-id="aad68-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="aad68-145">Microsoft Graph, KeyVault, API de Outlook y otras APIs Microsoft) generalmente solo obtienen un token y pasan a toohello propietario del recurso.</span><span class="sxs-lookup"><span data-stu-id="aad68-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="aad68-146">Dado que no están protegiendo todos los recursos, se inspecciona el token de hello y, por tanto, no es necesario tooensure que está firmado correctamente.</span><span class="sxs-lookup"><span data-stu-id="aad68-146">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="aad68-147">Las aplicaciones Web y las API que están usando el flujo de hello solo de aplicación web (las credenciales del cliente / certificado de cliente), entran en esta categoría y, por tanto, no se ven afectadas por la sustitución de Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-147">Web applications and web APIs that are using hello app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="aad68-148"><a name="appservices"></a>Aplicaciones y API web que protegen recursos y creadas mediante Servicios de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="aad68-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="aad68-149">Autenticación de Azure Servicios de aplicaciones / funcionalidad de autorización (EasyAuth) ya tiene la sustitución de clave toohandle Hola lógica necesaria automáticamente.</span><span class="sxs-lookup"><span data-stu-id="aad68-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has hello necessary logic toohandle key rollover automatically.</span></span>

### <span data-ttu-id="aad68-150"><a name="owin"></a>Aplicaciones y API web que protegen recursos mediante middleware .NET OWIN OpenID Connect, WS-Fed o WindowsAzureActiveDirectoryBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="aad68-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="aad68-151">Si la aplicación está utilizando Hola .NET OWIN OpenID Connect, WS-Fed o WindowsAzureActiveDirectoryBearerAuthentication middleware, ya tiene la sustitución de clave toohandle Hola lógica necesaria automáticamente.</span><span class="sxs-lookup"><span data-stu-id="aad68-151">If your application is using hello .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="aad68-152">Puede confirmar que la aplicación está utilizando cualquiera de estos métodos, debe buscar cualquiera de los siguientes fragmentos de código de la aplicación Startup.cs o Startup.Auth.cs de Hola</span><span class="sxs-lookup"><span data-stu-id="aad68-152">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <span data-ttu-id="aad68-153"><a name="owincore"></a>Aplicaciones y API web que protegen recursos mediante el middleware .NET Core OpenID Connect o JwtBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="aad68-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="aad68-154">Si la aplicación utiliza .NET Core OWIN OpenID Connect de Hola o JwtBearerAuthentication middleware, ya tiene la sustitución de clave toohandle Hola lógica necesaria automáticamente.</span><span class="sxs-lookup"><span data-stu-id="aad68-154">If your application is using hello .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="aad68-155">Puede confirmar que la aplicación está utilizando cualquiera de estos métodos, debe buscar cualquiera de los siguientes fragmentos de código de la aplicación Startup.cs o Startup.Auth.cs de Hola</span><span class="sxs-lookup"><span data-stu-id="aad68-155">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <span data-ttu-id="aad68-156"><a name="passport"></a>Aplicaciones y API web que protegen recursos mediante el módulo Node.js passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="aad68-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="aad68-157">Si la aplicación está utilizando el módulo de passport ad Node.js hello, ya tiene la sustitución de clave toohandle Hola lógica necesaria automáticamente.</span><span class="sxs-lookup"><span data-stu-id="aad68-157">If your application is using hello Node.js passport-ad module, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="aad68-158">Puede confirmar que su aplicación passport-ad mediante la búsqueda de hello siguiente fragmento de código en app.js la aplicación</span><span class="sxs-lookup"><span data-stu-id="aad68-158">You can confirm that your application passport-ad by searching for hello following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="aad68-159"><a name="vs2015"></a>Aplicaciones y API web de protección de recursos y creadas con Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="aad68-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="aad68-160">Si la aplicación se compiló mediante una plantilla de aplicación web en Visual Studio 2015 o Visual Studio de 2017 y seleccionó **cuentas de trabajo y educativa** de hello **Cambiar autenticación** menú, que ya se tiene automáticamente la sustitución de clave toohandle Hola lógica necesaria.</span><span class="sxs-lookup"><span data-stu-id="aad68-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="aad68-161">Esta lógica, incrustada en middleware OWIN OpenID Connect hello, recupera y almacena en caché las claves de Hola de documento de detección de OpenID Connect de Hola y los actualiza periódicamente.</span><span class="sxs-lookup"><span data-stu-id="aad68-161">This logic, embedded in hello OWIN OpenID Connect middleware, retrieves and caches hello keys from hello OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="aad68-162">Si agrega manualmente la solución de tooyour de autenticación, la aplicación podría no tener lógica de sustitución de claves necesaria Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-162">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="aad68-163">Necesitará toowrite usted mismo u Hola siga los pasos de [aplicaciones Web API con cualquier otra biblioteca o implementar manualmente cualquiera de hello admite protocolos.](#other).</span><span class="sxs-lookup"><span data-stu-id="aad68-163">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

### <span data-ttu-id="aad68-164"><a name="vs2013"></a>Aplicaciones Web de protección de recursos y creadas con Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="aad68-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="aad68-165">Si la aplicación se compiló mediante una plantilla de aplicación web en Visual Studio 2013 y seleccionó **cuentas organizativas** de hello **Cambiar autenticación** menú, ya tiene Hola necesarios lógica toohandle sustitución de clave automáticamente.</span><span class="sxs-lookup"><span data-stu-id="aad68-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="aad68-166">Esta lógica almacena hello firma información clave en dos tablas de base de datos asociados con el proyecto de Hola e identificador único de su organización.</span><span class="sxs-lookup"><span data-stu-id="aad68-166">This logic stores your organization’s unique identifier and hello signing key information in two database tables associated with hello project.</span></span> <span data-ttu-id="aad68-167">Puede encontrar la cadena de conexión de Hola para base de datos de Hola en el archivo Web.config del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-167">You can find hello connection string for hello database in hello project’s Web.config file.</span></span>

<span data-ttu-id="aad68-168">Si agrega manualmente la solución de tooyour de autenticación, la aplicación podría no tener lógica de sustitución de claves necesaria Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-168">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="aad68-169">Necesitará toowrite usted mismo u Hola siga los pasos de [aplicaciones Web API con cualquier otra biblioteca o implementar manualmente cualquiera de hello admite protocolos.](#other).</span><span class="sxs-lookup"><span data-stu-id="aad68-169">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

<span data-ttu-id="aad68-170">Hola pasos le ayudará a comprobar que Hola lógica funciona correctamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aad68-170">hello following steps will help you verify that hello logic is working properly in your application.</span></span>

1. <span data-ttu-id="aad68-171">En Visual Studio 2013, abra la solución de hello y, a continuación, haga clic en hello **Explorador de servidores** ficha en la ventana derecha Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-171">In Visual Studio 2013, open hello solution, and then click on hello **Server Explorer** tab on hello right window.</span></span>
2. <span data-ttu-id="aad68-172">Expanda **Conexiones de datos**, **DefaultConnection** y **Tablas**.</span><span class="sxs-lookup"><span data-stu-id="aad68-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="aad68-173">Busque hello **IssuingAuthorityKeys** de tabla, haga clic en él y, a continuación, haga clic en **mostrar datos de tabla**.</span><span class="sxs-lookup"><span data-stu-id="aad68-173">Locate hello **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="aad68-174">Hola **IssuingAuthorityKeys** tabla, habrá al menos una fila, que se corresponde el valor de huella digital de toohello para la clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-174">In hello **IssuingAuthorityKeys** table, there will be at least one row, which corresponds toohello thumbprint value for hello key.</span></span> <span data-ttu-id="aad68-175">Elimine las filas de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-175">Delete any rows in hello table.</span></span>
4. <span data-ttu-id="aad68-176">Menú contextual hello **inquilinos** de tabla y, a continuación, haga clic en **mostrar datos de tabla**.</span><span class="sxs-lookup"><span data-stu-id="aad68-176">Right-click hello **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="aad68-177">Hola **inquilinos** tabla, habrá al menos una fila, que se corresponde el identificador del inquilino de directorio único tooa.</span><span class="sxs-lookup"><span data-stu-id="aad68-177">In hello **Tenants** table, there will be at least one row, which corresponds tooa unique directory tenant identifier.</span></span> <span data-ttu-id="aad68-178">Elimine las filas de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-178">Delete any rows in hello table.</span></span> <span data-ttu-id="aad68-179">Si no elimina las filas de hello en ambos hello **inquilinos** tabla y **IssuingAuthorityKeys** tabla, obtendrá un error en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="aad68-179">If you don't delete hello rows in both hello **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="aad68-180">Compile y ejecute la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="aad68-180">Build and run hello application.</span></span> <span data-ttu-id="aad68-181">Una vez haya iniciado en tooyour cuenta, puede detener la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="aad68-181">After you have logged in tooyour account, you can stop hello application.</span></span>
7. <span data-ttu-id="aad68-182">Devolver toohello **Explorador de servidores** y examine los valores de hello en hello **IssuingAuthorityKeys** y **inquilinos** tabla.</span><span class="sxs-lookup"><span data-stu-id="aad68-182">Return toohello **Server Explorer** and look at hello values in hello **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="aad68-183">Observará que ha vuelto a llenar automáticamente con información adecuada de Hola de documento de metadatos de federación de Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-183">You’ll notice that they have been automatically repopulated with hello appropriate information from hello federation metadata document.</span></span>

### <span data-ttu-id="aad68-184"><a name="vs2013"></a>API web de protección de recursos y creadas con Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="aad68-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="aad68-185">Si crea una aplicación API web en Visual Studio 2013 mediante la plantilla de la API Web de hello y, a continuación, selecciona **cuentas organizativas** de hello **Cambiar autenticación** menú, ya haya Hola lógica necesaria en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aad68-185">If you created a web API application in Visual Studio 2013 using hello Web API template, and then selected **Organizational Accounts** from hello **Change Authentication** menu, you already have hello necessary logic in your application.</span></span>

<span data-ttu-id="aad68-186">Si ha configurado manualmente la autenticación, siga instrucciones hello toolearn cómo tooconfigure su tooautomatically API Web actualizar su información de clave.</span><span class="sxs-lookup"><span data-stu-id="aad68-186">If you manually configured authentication, follow hello instructions below toolearn how tooconfigure your Web API tooautomatically update its key information.</span></span>

<span data-ttu-id="aad68-187">Hello fragmento de código siguiente muestra cómo tooget Hola claves más recientes de documento de metadatos de federación de hello y, a continuación, usar hello [controlador de Token JWT](https://msdn.microsoft.com/library/dn205065.aspx) símbolo (token) de toovalidate Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-187">hello following code snippet demonstrates how tooget hello latest keys from hello federation metadata document, and then use hello [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello token.</span></span> <span data-ttu-id="aad68-188">fragmento de código de Hello se supone que va a usar sus propio mecanismo para conservar Hola clave toovalidate futuras el almacenamiento en caché los tokens de Azure AD, ya sea en una base de datos, archivo de configuración o en otro lugar.</span><span class="sxs-lookup"><span data-stu-id="aad68-188">hello code snippet assumes that you will use your own caching mechanism for persisting hello key toovalidate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <span data-ttu-id="aad68-189"><a name="vs2012"></a>Aplicaciones web de protección de recursos y creadas con Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="aad68-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="aad68-190">Si la aplicación se compiló en Visual Studio 2012, probablemente ha utilizado hello identidad y tooconfigure de la herramienta de acceso a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aad68-190">If your application was built in Visual Studio 2012, you probably used hello Identity and Access Tool tooconfigure your application.</span></span> <span data-ttu-id="aad68-191">También es probable que esté utilizando hello [del registro de nombre de emisor validación (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span><span class="sxs-lookup"><span data-stu-id="aad68-191">It’s also likely that you are using hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="aad68-192">Hola VINR es responsable de mantener la información sobre proveedores de identidades confiables (Azure AD) y las claves de hello utilizan tokens toovalidate que han emitido.</span><span class="sxs-lookup"><span data-stu-id="aad68-192">hello VINR is responsible for maintaining information about trusted identity providers (Azure AD) and hello keys used toovalidate tokens issued by them.</span></span> <span data-ttu-id="aad68-193">Hola VINR también facilita la información de claves tooautomatically fácil actualización Hola almacenada en un archivo Web.config descargando Hola último federación documento de metadatos asociada al directorio, comprobando si configuración de hello no está actualizada con hello más reciente documento y actualización hello toouse Hola nueva clave de aplicación según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="aad68-193">hello VINR also makes it easy tooautomatically update hello key information stored in a Web.config file by downloading hello latest federation metadata document associated with your directory, checking if hello configuration is out of date with hello latest document, and updating hello application toouse hello new key as necessary.</span></span>

<span data-ttu-id="aad68-194">Si ha creado su aplicación mediante cualquiera de los ejemplos de código de hello o documentación de tutoriales proporcionados por Microsoft, la lógica de sustitución de claves de hello ya está incluido en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="aad68-194">If you created your application using any of hello code samples or walkthrough documentation provided by Microsoft, hello key rollover logic is already included in your project.</span></span> <span data-ttu-id="aad68-195">Observará que código de hello siguiente ya existe en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="aad68-195">You will notice that hello code below already exists in your project.</span></span> <span data-ttu-id="aad68-196">Si la aplicación aún no tiene esta lógica, siga los pasos hello tooadd y tooverify que funciona correctamente.</span><span class="sxs-lookup"><span data-stu-id="aad68-196">If your application does not already have this logic, follow hello steps below tooadd it and tooverify that it’s working correctly.</span></span>

1. <span data-ttu-id="aad68-197">En **el Explorador de soluciones**, agregar una referencia toohello **System.IdentityModel** ensamblado de proyecto adecuada de Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-197">In **Solution Explorer**, add a reference toohello **System.IdentityModel** assembly for hello appropriate project.</span></span>
2. <span data-ttu-id="aad68-198">Abra hello **Global.asax.cs** de archivos y agregue Hola siguientes directivas using:</span><span class="sxs-lookup"><span data-stu-id="aad68-198">Open hello **Global.asax.cs** file and add hello following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="aad68-199">Agregar Hola siguiendo el método toohello **Global.asax.cs** archivo:</span><span class="sxs-lookup"><span data-stu-id="aad68-199">Add hello following method toohello **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="aad68-200">Invocar hello **RefreshValidationSettings()** método Hola **Application_Start ()** método **Global.asax.cs** tal como se muestra:</span><span class="sxs-lookup"><span data-stu-id="aad68-200">Invoke hello **RefreshValidationSettings()** method in hello **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="aad68-201">Una vez que haya seguido estos pasos, se actualizará con la información más reciente de Hola de documento de metadatos de federación Hola, incluidas las claves más recientes de Hola Web.config de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="aad68-201">Once you have followed these steps, your application’s Web.config will be updated with hello latest information from hello federation metadata document, including hello latest keys.</span></span> <span data-ttu-id="aad68-202">Esta actualización se producirá cada vez que se recicla el grupo de aplicaciones en IIS; de forma predeterminada IIS se establece toorecycle aplicaciones cada 29 horas.</span><span class="sxs-lookup"><span data-stu-id="aad68-202">This update will occur every time your application pool recycles in IIS; by default IIS is set toorecycle applications every 29 hours.</span></span>

<span data-ttu-id="aad68-203">Siga los pasos de hello debajo tooverify que funciona la lógica de sustitución de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-203">Follow hello steps below tooverify that hello key rollover logic is working.</span></span>

1. <span data-ttu-id="aad68-204">Después de comprobar que la aplicación está usando código de hello anteriormente, abra hello **Web.config** de archivos y desplácese toohello  **<issuerNameRegistry>**  bloque, buscando específicamente Hola después algunas líneas:</span><span class="sxs-lookup"><span data-stu-id="aad68-204">After you have verified that your application is using hello code above, open hello **Web.config** file and navigate toohello **<issuerNameRegistry>** block, specifically looking for hello following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="aad68-205">Hola  **<add thumbprint=””>**  configuración, cambie el valor de huella digital de hello reemplazando algún carácter por otra diferente.</span><span class="sxs-lookup"><span data-stu-id="aad68-205">In hello **<add thumbprint=””>** setting, change hello thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="aad68-206">Guardar hello **Web.config** archivo.</span><span class="sxs-lookup"><span data-stu-id="aad68-206">Save hello **Web.config** file.</span></span>
3. <span data-ttu-id="aad68-207">Compilar la aplicación hello y, a continuación, ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="aad68-207">Build hello application, and then run it.</span></span> <span data-ttu-id="aad68-208">Si puede completar el proceso de inicio de sesión de hello, la aplicación actualiza correctamente clave Hola descargando información de hello necesario de documento de metadatos de federación de su directorio.</span><span class="sxs-lookup"><span data-stu-id="aad68-208">If you can complete hello sign-in process, your application is successfully updating hello key by downloading hello required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="aad68-209">Si tiene problemas para iniciar sesión, asegúrese de hello cambios en la aplicación son correctos leyendo hello [tooYour agregar inicio de sesión Web aplicaciones con Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) tema, o bien descargarlos e inspeccionando el siguiente ejemplo de código de hello: [ Aplicación de nube de varios inquilinos de Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span><span class="sxs-lookup"><span data-stu-id="aad68-209">If you are having issues signing in, ensure hello changes in your application are correct by reading hello [Adding Sign-On tooYour Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting hello following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="aad68-210"><a name="vs2010"></a>Aplicaciones web de protección de recursos y creadas con Visual Studio 2008 o 2010 y Windows Identity Foundation (WIF) v1.0 para .NET 3.5</span><span class="sxs-lookup"><span data-stu-id="aad68-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="aad68-211">Si ha creado una aplicación en WIF v1.0, no hay ninguna actualización de tooautomatically mecanismo toouse de configuración de la aplicación una nueva clave.</span><span class="sxs-lookup"><span data-stu-id="aad68-211">If you built an application on WIF v1.0, there is no provided mechanism tooautomatically refresh your application’s configuration toouse a new key.</span></span>

* <span data-ttu-id="aad68-212">*La manera más fácil* usar el utillaje de FedUtil Hola incluido en hello WIF SDK, que puede recuperar el último documento de metadatos de Hola y actualizar la configuración.</span><span class="sxs-lookup"><span data-stu-id="aad68-212">*Easiest way* Use hello FedUtil tooling included in hello WIF SDK, which can retrieve hello latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="aad68-213">Actualice su too.NET aplicación 4.5, que incluye la versión más reciente de Hola de WIF ubicada en el espacio de nombres de sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-213">Update your application too.NET 4.5, which includes hello newest version of WIF located in hello System namespace.</span></span> <span data-ttu-id="aad68-214">A continuación, puede usar hello [del registro de nombre de emisor validación (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform actualizaciones automáticas de configuración de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="aad68-214">You can then use hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform automatic updates of hello application’s configuration.</span></span>
* <span data-ttu-id="aad68-215">Realizar una sustitución manual según las instrucciones de hello final Hola de este documento de instrucciones.</span><span class="sxs-lookup"><span data-stu-id="aad68-215">Perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span>

<span data-ttu-id="aad68-216">Instrucciones toouse Hola FedUtil tooupdate su configuración:</span><span class="sxs-lookup"><span data-stu-id="aad68-216">Instructions toouse hello FedUtil tooupdate your configuration:</span></span>

1. <span data-ttu-id="aad68-217">Compruebe que dispone de hello WIF v1.0 SDK instalado en el equipo de desarrollo para Visual Studio 2008 o 2010.</span><span class="sxs-lookup"><span data-stu-id="aad68-217">Verify that you have hello WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="aad68-218">También puede [descargarlo desde aquí](https://www.microsoft.com/en-us/download/details.aspx?id=4451) si aún no lo ha instalado.</span><span class="sxs-lookup"><span data-stu-id="aad68-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="aad68-219">En Visual Studio, abra la solución hello y, a continuación, haga clic en proyecto aplicable de Hola y seleccione **actualizar metadatos de federación**.</span><span class="sxs-lookup"><span data-stu-id="aad68-219">In Visual Studio, open hello solution, and then right-click hello applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="aad68-220">Si esta opción no está disponible, no se instaló FedUtil y/o Hola WIF v1.0 SDK.</span><span class="sxs-lookup"><span data-stu-id="aad68-220">If this option is not available, FedUtil and/or hello WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="aad68-221">En el símbolo del sistema de hello, seleccione **actualización** toobegin actualizar los metadatos de federación.</span><span class="sxs-lookup"><span data-stu-id="aad68-221">From hello prompt, select **Update** toobegin updating your federation metadata.</span></span> <span data-ttu-id="aad68-222">Si tiene un entorno de servidor de acceso a toohello donde se hospeda la aplicación hello, también puede usar FedUtil [programador de actualizaciones de metadatos automática](https://msdn.microsoft.com/library/ee517272.aspx).</span><span class="sxs-lookup"><span data-stu-id="aad68-222">If you have access toohello server environment where hello application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="aad68-223">Haga clic en **finalizar** proceso de actualización de toocomplete Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-223">Click **Finish** toocomplete hello update process.</span></span>

### <span data-ttu-id="aad68-224"><a name="other"></a>Aplicaciones Web / API de protección de los recursos cualquiera otras bibliotecas o implementar manualmente cualquiera de hello admite el uso de protocolos</span><span class="sxs-lookup"><span data-stu-id="aad68-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>
<span data-ttu-id="aad68-225">Si está utilizando alguna otra biblioteca o implementa manualmente cualquiera de los protocolos de hello admitida, necesitará tooreview biblioteca de Hola o se está recuperando el tooensure de implementación que Hola clave de documento de detección de OpenID Connect de Hola o hello documento de metadatos de federación.</span><span class="sxs-lookup"><span data-stu-id="aad68-225">If you are using some other library or manually implemented any of hello supported protocols, you'll need tooreview hello library or your implementation tooensure that hello key is being retrieved from either hello OpenID Connect discovery document or hello federation metadata document.</span></span> <span data-ttu-id="aad68-226">Toocheck una manera para que esto es toodo una búsqueda en el código o el código de la biblioteca de Hola para las llamadas a cualquier documento de descubrimiento de tooeither Hola OpenID o documento de metadatos de federación de Hola.</span><span class="sxs-lookup"><span data-stu-id="aad68-226">One way toocheck for this is toodo a search in your code or hello library's code for any calls out tooeither hello OpenID discovery document or hello federation metadata document.</span></span>

<span data-ttu-id="aad68-227">Si la clave se almacena en algún lugar o codificado de forma rígida en la aplicación, puede preparar manualmente recuperar clave hello y según corresponda al realizar una sustitución manual según las instrucciones de hello final Hola de este documento de instrucciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="aad68-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve hello key and update it accordingly by perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span> <span data-ttu-id="aad68-228">**Se recomienda encarecidamente que mejora la sustitución automática de toosupport de aplicación** mediante cualquiera de Hola aproxima contorno en interrupciones del artículo tooavoid futuras y la sobrecarga si aumenta su cadencia de sustitución de Azure AD o si tiene un sustitución de emergencia fuera de banda.</span><span class="sxs-lookup"><span data-stu-id="aad68-228">**It is strongly encouraged that you enhance your application toosupport automatic rollover** using any of hello approaches outline in this article tooavoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a><span data-ttu-id="aad68-229">Cómo tootest su toodetermine de aplicación si se verán afectado</span><span class="sxs-lookup"><span data-stu-id="aad68-229">How tootest your application toodetermine if it will be affected</span></span>
<span data-ttu-id="aad68-230">Puede validar si la aplicación admite la sustitución de clave automática, se descargan las secuencias de comandos de Hola y siguiendo las instrucciones de hello en [este repositorio de GitHub.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="aad68-230">You can validate whether your application supports automatic key rollover by downloading hello scripts and following hello instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="aad68-231">¿Cómo tooperform una sustitución manual si, su aplicación no admite la sustitución automática</span><span class="sxs-lookup"><span data-stu-id="aad68-231">How tooperform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="aad68-232">Si la aplicación **no** admite la sustitución automática, deberá tooestablish un proceso que periódicamente de monitores de Azure AD firma de claves y realiza una sustitución manual en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="aad68-232">If your application does **not** support automatic rollover, you will need tooestablish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="aad68-233">[Este repositorio de GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contiene secuencias de comandos e instrucciones sobre cómo toodo esto.</span><span class="sxs-lookup"><span data-stu-id="aad68-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how toodo this.</span></span>

