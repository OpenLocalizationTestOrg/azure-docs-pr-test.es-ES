---
title: "Sustitución de claves de firma en Azure AD | Microsoft Docs"
description: "En este artículo se analizan las prácticas recomendadas de sustitución de claves de firma de Azure Active Directory."
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
ms.openlocfilehash: 228bb9058537af1e4eb38207c376c2eb86aee68c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="3e85f-103">Sustitución de claves de firma de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e85f-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="3e85f-104">En este tema se describe lo que necesita saber de las claves públicas que se usan en Azure Active Directory (Azure AD) para firmar los tokens de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3e85f-104">This topic discusses what you need to know about the public keys that are used in Azure Active Directory (Azure AD) to sign security tokens.</span></span> <span data-ttu-id="3e85f-105">Es importante tener en cuenta que estas claves se sustituyen de forma periódica y, en caso de emergencia, podrían ser sustituidas inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="3e85f-105">It is important to note that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="3e85f-106">Todas las aplicaciones que usan Azure AD deben poder manejar mediante programación el proceso de sustitución de claves o establecer un proceso de sustitución manual periódico.</span><span class="sxs-lookup"><span data-stu-id="3e85f-106">All applications that use Azure AD should be able to programmatically handle the key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="3e85f-107">Siga leyendo para comprender cómo funcionan las claves, cómo evaluar el impacto de la sustitución en la aplicación y cómo actualizar la aplicación o establecer un proceso de sustitución manual periódico para controlar la sustitución de claves si fuera necesario.</span><span class="sxs-lookup"><span data-stu-id="3e85f-107">Continue reading to understand how the keys work, how to assess the impact of the rollover to your application and how to update your application or establish a periodic manual rollover process to handle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="3e85f-108">Información general sobre las claves de firma de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e85f-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="3e85f-109">Azure AD emplea una criptografía de clave pública basada en estándares del sector con el fin de establecer una relación de confianza entre ella y las aplicaciones que la utilizan.</span><span class="sxs-lookup"><span data-stu-id="3e85f-109">Azure AD uses public-key cryptography built on industry standards to establish trust between itself and the applications that use it.</span></span> <span data-ttu-id="3e85f-110">En términos prácticos, funciona de la siguiente manera: Azure AD usa una clave de firma que consta de un par de claves pública y privada.</span><span class="sxs-lookup"><span data-stu-id="3e85f-110">In practical terms, this works in the following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="3e85f-111">Cuando un usuario inicia sesión en una aplicación que utiliza Azure AD para realizar la autenticación, Azure AD crea un token de seguridad que contiene información sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="3e85f-111">When a user signs in to an application that uses Azure AD for authentication, Azure AD creates a security token that contains information about the user.</span></span> <span data-ttu-id="3e85f-112">Azure AD firma este token con su clave privada antes de enviarlo a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e85f-112">This token is signed by Azure AD using its private key before it is sent back to the application.</span></span> <span data-ttu-id="3e85f-113">Para comprobar que el token es válido y que realmente se originó en Azure AD, la aplicación debe validar la firma del token usando la clave pública expuesta por Azure AD que se encuentra en el [documento de detección de OpenID Connect](http://openid.net/specs/openid-connect-discovery-1_0.html) del inquilino o en el [documento de metadatos de federación](active-directory-federation-metadata.md) de SAML/WS-Fed.</span><span class="sxs-lookup"><span data-stu-id="3e85f-113">To verify that the token is valid and actually originated from Azure AD, the application must validate the token’s signature using the public key exposed by Azure AD that is contained in the tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="3e85f-114">Por motivos de seguridad, Azure AD firma la sustitución de claves de forma periódica y, en caso de emergencia, podrían sustituirse inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="3e85f-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in the case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="3e85f-115">Cualquier aplicación que se integra con Azure AD debe estar preparada para controlar un evento de sustitución de claves, con independencia de la frecuencia con que se produzca.</span><span class="sxs-lookup"><span data-stu-id="3e85f-115">Any application that integrates with Azure AD should be prepared to handle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="3e85f-116">Si no es así y la aplicación trata de utilizar una clave expirada para comprobar la firma de un token, se producirá un error en la solicitud de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="3e85f-116">If it doesn’t, and your application attempts to use an expired key to verify the signature on a token, the sign-in request will fail.</span></span>

<span data-ttu-id="3e85f-117">Siempre hay más de una clave válida disponible en el documento de detección de OpenID Connect y en el de metadatos de federación.</span><span class="sxs-lookup"><span data-stu-id="3e85f-117">There is always more than one valid key available in the OpenID Connect discovery document and the federation metadata document.</span></span> <span data-ttu-id="3e85f-118">La aplicación debe estar preparada para utilizar cualquiera de las claves especificadas del documento, ya que una de ellas puede sustituirse pronto, otra puede ser su reemplazo, etc.</span><span class="sxs-lookup"><span data-stu-id="3e85f-118">Your application should be prepared to use any of the keys specified in the document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-to-assess-if-your-application-will-be-affected-and-what-to-do-about-it"></a><span data-ttu-id="3e85f-119">Cómo evaluar si su aplicación se verá afectada y qué hacer al respecto</span><span class="sxs-lookup"><span data-stu-id="3e85f-119">How to assess if your application will be affected and what to do about it</span></span>
<span data-ttu-id="3e85f-120">La forma que tiene la aplicación de controlar la sustitución de claves depende de ciertas variables, como el tipo de aplicación o qué protocolo de identidad y biblioteca se han usado.</span><span class="sxs-lookup"><span data-stu-id="3e85f-120">How your application handles key rollover depends on variables such as the type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="3e85f-121">Las secciones siguientes evalúan si los tipos más comunes de aplicaciones se ven afectados por la sustitución de claves y ofrecen orientación sobre cómo actualizar la aplicación para admitir la sustitución automática o actualizar manualmente la clave.</span><span class="sxs-lookup"><span data-stu-id="3e85f-121">The sections below assess whether the most common types of applications are impacted by the key rollover and provide guidance on how to update the application to support automatic rollover or manually update the key.</span></span>

* [<span data-ttu-id="3e85f-122">Aplicaciones de cliente nativas que acceden a recursos</span><span class="sxs-lookup"><span data-stu-id="3e85f-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="3e85f-123">Aplicaciones y API web que acceden a recursos</span><span class="sxs-lookup"><span data-stu-id="3e85f-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="3e85f-124">Aplicaciones y API web que protegen recursos y creadas mediante Servicios de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="3e85f-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="3e85f-125">Aplicaciones y API web que protegen recursos mediante middleware .NET OWIN OpenID Connect, WS-Fed o WindowsAzureActiveDirectoryBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="3e85f-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="3e85f-126">Aplicaciones y API web que protegen recursos mediante el middleware .NET Core OpenID Connect o JwtBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="3e85f-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="3e85f-127">Aplicaciones y API web que protegen recursos mediante el módulo Node.js passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="3e85f-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="3e85f-128">Aplicaciones y API web de protección de recursos y creadas con Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="3e85f-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="3e85f-129">Aplicaciones Web de protección de recursos y creadas con Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3e85f-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="3e85f-130">API web de protección de recursos y creadas con Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3e85f-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="3e85f-131">Aplicaciones web de protección de recursos y creadas con Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="3e85f-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="3e85f-132">Aplicaciones web de protección de recursos y creadas con Visual Studio 2010, 2008 o mediante Windows Identity Foundation</span><span class="sxs-lookup"><span data-stu-id="3e85f-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="3e85f-133">Aplicaciones y API web de protección de recursos que usan cualquier otra biblioteca o que implementan manualmente cualquiera de los protocolos admitidos</span><span class="sxs-lookup"><span data-stu-id="3e85f-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>](#other)

<span data-ttu-id="3e85f-134">Esta guía **no** es aplicable para:</span><span class="sxs-lookup"><span data-stu-id="3e85f-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="3e85f-135">Las aplicaciones agregadas desde la galería de aplicaciones de Azure AD (incluidas las personalizadas) disponen de instrucciones independientes para las claves de firma.</span><span class="sxs-lookup"><span data-stu-id="3e85f-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards to signing keys.</span></span> [<span data-ttu-id="3e85f-136">Más información.</span><span class="sxs-lookup"><span data-stu-id="3e85f-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="3e85f-137">Las aplicaciones locales publicadas a través del proxy de la aplicación no tienen que preocuparse acerca de las claves de firma.</span><span class="sxs-lookup"><span data-stu-id="3e85f-137">On-premises applications published via application proxy don't have to worry about signing keys.</span></span>

### <span data-ttu-id="3e85f-138"><a name="nativeclient"></a>Aplicaciones de cliente nativas que acceden a recursos</span><span class="sxs-lookup"><span data-stu-id="3e85f-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="3e85f-139">Las aplicaciones que solo acceden a los recursos (es decir,</span><span class="sxs-lookup"><span data-stu-id="3e85f-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="3e85f-140">Microsoft Graph, KeyVault, API de Outlook y otras API de Microsoft) únicamente obtienen por lo general un token y lo pasan al propietario del recurso.</span><span class="sxs-lookup"><span data-stu-id="3e85f-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="3e85f-141">Como no protegen ningún recurso, no inspeccionan el token y, por tanto, no tienen que asegurar de que se firmó correctamente.</span><span class="sxs-lookup"><span data-stu-id="3e85f-141">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="3e85f-142">Las aplicaciones de cliente nativo, ya sean de escritorio o móviles, entran en esta categoría y, por tanto, no se verán afectadas por la sustitución.</span><span class="sxs-lookup"><span data-stu-id="3e85f-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by the rollover.</span></span>

### <span data-ttu-id="3e85f-143"><a name="webclient"></a>Aplicaciones y API web que acceden a recursos</span><span class="sxs-lookup"><span data-stu-id="3e85f-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="3e85f-144">Las aplicaciones que solo acceden a los recursos (es decir,</span><span class="sxs-lookup"><span data-stu-id="3e85f-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="3e85f-145">Microsoft Graph, KeyVault, API de Outlook y otras API de Microsoft) únicamente obtienen por lo general un token y lo pasan al propietario del recurso.</span><span class="sxs-lookup"><span data-stu-id="3e85f-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="3e85f-146">Como no protegen ningún recurso, no inspeccionan el token y, por tanto, no tienen que asegurar de que se firmó correctamente.</span><span class="sxs-lookup"><span data-stu-id="3e85f-146">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="3e85f-147">Las aplicaciones web y las API web que usan el flujo solo de aplicación (credenciales del cliente o el certificado de cliente), entran en esta categoría y, por tanto, no se verán afectadas por la sustitución.</span><span class="sxs-lookup"><span data-stu-id="3e85f-147">Web applications and web APIs that are using the app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by the rollover.</span></span>

### <span data-ttu-id="3e85f-148"><a name="appservices"></a>Aplicaciones y API web que protegen recursos y creadas mediante Servicios de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="3e85f-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="3e85f-149">La funcionalidad de autenticación o autorización (EasyAuth) de Servicios de aplicaciones de Azure ya cuenta con la lógica necesaria para controlar automáticamente la sustitución de claves.</span><span class="sxs-lookup"><span data-stu-id="3e85f-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has the necessary logic to handle key rollover automatically.</span></span>

### <span data-ttu-id="3e85f-150"><a name="owin"></a>Aplicaciones y API web que protegen recursos mediante middleware .NET OWIN OpenID Connect, WS-Fed o WindowsAzureActiveDirectoryBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="3e85f-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="3e85f-151">Si la aplicación está utilizando el middleware .NET OWIN OpenID Connect, WS-Fed o WindowsAzureActiveDirectoryBearerAuthentication, ya tiene la lógica necesaria para controlar automáticamente la sustitución de clave.</span><span class="sxs-lookup"><span data-stu-id="3e85f-151">If your application is using the .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="3e85f-152">Puede confirmar que la aplicación utiliza cualquiera de estos, busque cualquiera de los siguientes fragmentos de código en la aplicación Startup.cs o Startup.Auth.cs</span><span class="sxs-lookup"><span data-stu-id="3e85f-152">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

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

### <span data-ttu-id="3e85f-153"><a name="owincore"></a>Aplicaciones y API web que protegen recursos mediante el middleware .NET Core OpenID Connect o JwtBearerAuthentication</span><span class="sxs-lookup"><span data-stu-id="3e85f-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="3e85f-154">Si la aplicación usa el middleware .NET Core OWIN OpenID Connect o JwtBearerAuthentication, ya tiene la lógica necesaria para controlar automáticamente la sustitución de claves.</span><span class="sxs-lookup"><span data-stu-id="3e85f-154">If your application is using the .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="3e85f-155">Puede confirmar que la aplicación utiliza cualquiera de estos, busque cualquiera de los siguientes fragmentos de código en la aplicación Startup.cs o Startup.Auth.cs</span><span class="sxs-lookup"><span data-stu-id="3e85f-155">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

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

### <span data-ttu-id="3e85f-156"><a name="passport"></a>Aplicaciones y API web que protegen recursos mediante el módulo Node.js passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="3e85f-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="3e85f-157">Si la aplicación está utilizando el módulo Node.js passport-ad, ya tiene la lógica necesaria para controlar automáticamente la sustitución de clave.</span><span class="sxs-lookup"><span data-stu-id="3e85f-157">If your application is using the Node.js passport-ad module, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="3e85f-158">Puede confirmar su aplicación passport-ad si busca el siguiente fragmento en el archivo app.js de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3e85f-158">You can confirm that your application passport-ad by searching for the following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="3e85f-159"><a name="vs2015"></a>Aplicaciones y API web de protección de recursos y creadas con Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="3e85f-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="3e85f-160">Si la aplicación se compiló mediante una plantilla de aplicación web en Visual Studio 2015 o Visual Studio 2017 y seleccionó **Cuentas profesionales o educativas** en el menú **Cambiar autenticación**, ya tiene la lógica necesaria para controlar automáticamente la sustitución de clave.</span><span class="sxs-lookup"><span data-stu-id="3e85f-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="3e85f-161">Esta lógica, inserta en el middleware OWIN OpenID Connect, recupera y almacena en caché las claves del documento de detección OpenID Connect y las actualiza periódicamente.</span><span class="sxs-lookup"><span data-stu-id="3e85f-161">This logic, embedded in the OWIN OpenID Connect middleware, retrieves and caches the keys from the OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="3e85f-162">Si ha agregado manualmente la autenticación a la solución, la aplicación no tendrá la lógica necesaria para la sustitución de claves.</span><span class="sxs-lookup"><span data-stu-id="3e85f-162">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="3e85f-163">Tendrá que escribirla usted mismo o seguir los pasos que aparecen en [Aplicaciones y API web de protección de recursos que usan cualquier otra biblioteca o que implementan manualmente cualquiera de los protocolos admitidos](#other).</span><span class="sxs-lookup"><span data-stu-id="3e85f-163">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

### <span data-ttu-id="3e85f-164"><a name="vs2013"></a>Aplicaciones Web de protección de recursos y creadas con Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3e85f-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="3e85f-165">Si la aplicación se compiló mediante una plantilla de aplicación web en Visual Studio 2013 y seleccionó **Cuentas profesionales** en el menú **Cambiar autenticación**, ya tiene la lógica necesaria para controlar automáticamente la sustitución de claves.</span><span class="sxs-lookup"><span data-stu-id="3e85f-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="3e85f-166">Esta lógica almacena la información de la clave de firma y el identificador único de la organización en dos tablas de base de datos asociadas al proyecto.</span><span class="sxs-lookup"><span data-stu-id="3e85f-166">This logic stores your organization’s unique identifier and the signing key information in two database tables associated with the project.</span></span> <span data-ttu-id="3e85f-167">Puede encontrar la cadena de conexión de la base de datos en el archivo Web.config del proyecto.</span><span class="sxs-lookup"><span data-stu-id="3e85f-167">You can find the connection string for the database in the project’s Web.config file.</span></span>

<span data-ttu-id="3e85f-168">Si ha agregado manualmente la autenticación a la solución, la aplicación no tendrá la lógica necesaria para la sustitución de claves.</span><span class="sxs-lookup"><span data-stu-id="3e85f-168">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="3e85f-169">Tendrá que escribirla usted mismo o seguir los pasos que aparecen en [Aplicaciones y API web de protección de recursos que usan cualquier otra biblioteca o que implementan manualmente cualquiera de los protocolos admitidos](#other).</span><span class="sxs-lookup"><span data-stu-id="3e85f-169">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

<span data-ttu-id="3e85f-170">Los siguientes pasos lo ayudarán a comprobar que la lógica funcione correctamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e85f-170">The following steps will help you verify that the logic is working properly in your application.</span></span>

1. <span data-ttu-id="3e85f-171">En Visual Studio 2013, abra la solución y haga clic en la pestaña **Explorador de servidores** de la ventana derecha.</span><span class="sxs-lookup"><span data-stu-id="3e85f-171">In Visual Studio 2013, open the solution, and then click on the **Server Explorer** tab on the right window.</span></span>
2. <span data-ttu-id="3e85f-172">Expanda **Conexiones de datos**, **DefaultConnection** y **Tablas**.</span><span class="sxs-lookup"><span data-stu-id="3e85f-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="3e85f-173">Busque la tabla **IssuingAuthorityKeys**, haga clic con el botón derecho en ella y, después, con el botón izquierdo, en **Mostrar datos de tabla**.</span><span class="sxs-lookup"><span data-stu-id="3e85f-173">Locate the **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="3e85f-174">En la tabla **IssuingAuthorityKeys** habrá al menos una fila, que corresponde al valor de la huella digital de la clave.</span><span class="sxs-lookup"><span data-stu-id="3e85f-174">In the **IssuingAuthorityKeys** table, there will be at least one row, which corresponds to the thumbprint value for the key.</span></span> <span data-ttu-id="3e85f-175">Elimine las filas de la tabla.</span><span class="sxs-lookup"><span data-stu-id="3e85f-175">Delete any rows in the table.</span></span>
4. <span data-ttu-id="3e85f-176">Haga clic con el botón derecho en la tabla **Inquilinos** y, después, con el botón izquierdo, en **Mostrar datos de tabla**.</span><span class="sxs-lookup"><span data-stu-id="3e85f-176">Right-click the **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="3e85f-177">En la tabla **Inquilinos** habrá al menos una fila, que corresponde a un identificador único del inquilino de directorio.</span><span class="sxs-lookup"><span data-stu-id="3e85f-177">In the **Tenants** table, there will be at least one row, which corresponds to a unique directory tenant identifier.</span></span> <span data-ttu-id="3e85f-178">Elimine las filas de la tabla.</span><span class="sxs-lookup"><span data-stu-id="3e85f-178">Delete any rows in the table.</span></span> <span data-ttu-id="3e85f-179">Si no elimina las filas de las tablas **Inquilinos** e **IssuingAuthorityKeys**, se producirá un error en el entorno de tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="3e85f-179">If you don't delete the rows in both the **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="3e85f-180">Compile y ejecute la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e85f-180">Build and run the application.</span></span> <span data-ttu-id="3e85f-181">Una vez que haya iniciado sesión en la cuenta, podrá detener la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e85f-181">After you have logged in to your account, you can stop the application.</span></span>
7. <span data-ttu-id="3e85f-182">Vuelva a la pestaña **Explorador de servidores** y examine los valores de las tablas **IssuingAuthorityKeys** e **Inquilinos**.</span><span class="sxs-lookup"><span data-stu-id="3e85f-182">Return to the **Server Explorer** and look at the values in the **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="3e85f-183">Observará que se han vuelto a rellenar automáticamente con la información correspondiente del documento de metadatos de federación.</span><span class="sxs-lookup"><span data-stu-id="3e85f-183">You’ll notice that they have been automatically repopulated with the appropriate information from the federation metadata document.</span></span>

### <span data-ttu-id="3e85f-184"><a name="vs2013"></a>API web de protección de recursos y creadas con Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3e85f-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="3e85f-185">Si creó una aplicación API web en Visual Studio 2013 con la plantilla de API web y, después, seleccionó **Cuentas profesionales** en el menú **Cambiar autenticación**, la aplicación ya tiene la lógica necesaria.</span><span class="sxs-lookup"><span data-stu-id="3e85f-185">If you created a web API application in Visual Studio 2013 using the Web API template, and then selected **Organizational Accounts** from the **Change Authentication** menu, you already have the necessary logic in your application.</span></span>

<span data-ttu-id="3e85f-186">Si configura manualmente la autenticación, siga estas instrucciones para aprender a configurar la API web con el fin de actualizar automáticamente la información de claves.</span><span class="sxs-lookup"><span data-stu-id="3e85f-186">If you manually configured authentication, follow the instructions below to learn how to configure your Web API to automatically update its key information.</span></span>

<span data-ttu-id="3e85f-187">El fragmento de código siguiente muestra cómo obtener las claves más recientes del documento de metadatos de federación y utilizar el [Controlador de token web de JSON](https://msdn.microsoft.com/library/dn205065.aspx) para validar el token.</span><span class="sxs-lookup"><span data-stu-id="3e85f-187">The following code snippet demonstrates how to get the latest keys from the federation metadata document, and then use the [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) to validate the token.</span></span> <span data-ttu-id="3e85f-188">En el fragmento de código se da por hecho que va a utilizar su propio mecanismo de almacenamiento en caché para conservar la clave con el fin de validar los tokens futuros de Azure AD, ya sea en una base de datos, un archivo de configuración o en otro lugar.</span><span class="sxs-lookup"><span data-stu-id="3e85f-188">The code snippet assumes that you will use your own caching mechanism for persisting the key to validate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

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

        // Validates the JWT Token that's part of the Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in the Azure Classic Portal]",
                ValidIssuer = "[The issuer for the token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache the signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from the specified metadata document.
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
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in the metadata");
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

### <span data-ttu-id="3e85f-189"><a name="vs2012"></a>Aplicaciones web de protección de recursos y creadas con Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="3e85f-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="3e85f-190">Si la aplicación se compiló en Visual Studio 2012, probablemente ha utilizado la herramienta de identidad y acceso para configurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e85f-190">If your application was built in Visual Studio 2012, you probably used the Identity and Access Tool to configure your application.</span></span> <span data-ttu-id="3e85f-191">También es probable que esté utilizando el [registro de nombres de emisor de validación (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e85f-191">It’s also likely that you are using the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="3e85f-192">El VINR se encarga de mantener la información sobre los proveedores de identidad de confianza (Azure AD) y las claves utilizadas para validar los tokens que emiten.</span><span class="sxs-lookup"><span data-stu-id="3e85f-192">The VINR is responsible for maintaining information about trusted identity providers (Azure AD) and the keys used to validate tokens issued by them.</span></span> <span data-ttu-id="3e85f-193">El VINR también facilita la tarea de actualizar automáticamente la información de claves almacenada en un archivo Web.config descargando el documento de metadatos de federación más reciente asociado a su directorio, comprobando si la configuración está actualizada con respecto al último documento y actualizando la aplicación para usar la nueva clave según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3e85f-193">The VINR also makes it easy to automatically update the key information stored in a Web.config file by downloading the latest federation metadata document associated with your directory, checking if the configuration is out of date with the latest document, and updating the application to use the new key as necessary.</span></span>

<span data-ttu-id="3e85f-194">Si ha creado la aplicación utilizando cualquiera de los ejemplos de código o la documentación de tutorial que proporciona Microsoft, la lógica de sustitución de claves ya estará incluida en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="3e85f-194">If you created your application using any of the code samples or walkthrough documentation provided by Microsoft, the key rollover logic is already included in your project.</span></span> <span data-ttu-id="3e85f-195">Observará que el código siguiente ya existe en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="3e85f-195">You will notice that the code below already exists in your project.</span></span> <span data-ttu-id="3e85f-196">Si la aplicación aún no tiene esta lógica, siga estos pasos para agregarla y comprobar que funciona correctamente.</span><span class="sxs-lookup"><span data-stu-id="3e85f-196">If your application does not already have this logic, follow the steps below to add it and to verify that it’s working correctly.</span></span>

1. <span data-ttu-id="3e85f-197">En **Explorador de soluciones**, agregue una referencia al ensamblado **System.IdentityModel** del proyecto correspondiente.</span><span class="sxs-lookup"><span data-stu-id="3e85f-197">In **Solution Explorer**, add a reference to the **System.IdentityModel** assembly for the appropriate project.</span></span>
2. <span data-ttu-id="3e85f-198">Abra el archivo **Global.asax.cs** y agregue lo siguiente utilizando directivas:</span><span class="sxs-lookup"><span data-stu-id="3e85f-198">Open the **Global.asax.cs** file and add the following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="3e85f-199">Agregue el método siguiente al archivo **Global.asax.cs** :</span><span class="sxs-lookup"><span data-stu-id="3e85f-199">Add the following method to the **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="3e85f-200">Invoque el método **RefreshValidationSettings()** en el método **Application_Start()** de **Global.asax.cs**, tal y como se muestra:</span><span class="sxs-lookup"><span data-stu-id="3e85f-200">Invoke the **RefreshValidationSettings()** method in the **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="3e85f-201">Una vez que haya seguido estos pasos, el archivo Web.config de la aplicación se actualizará con la información más reciente del documento de metadatos de federación, incluidas las últimas claves.</span><span class="sxs-lookup"><span data-stu-id="3e85f-201">Once you have followed these steps, your application’s Web.config will be updated with the latest information from the federation metadata document, including the latest keys.</span></span> <span data-ttu-id="3e85f-202">Esta actualización se producirá cada vez que recicle el grupo de aplicaciones de IIS; de forma predeterminada, esta acción se realizará cada 29 horas.</span><span class="sxs-lookup"><span data-stu-id="3e85f-202">This update will occur every time your application pool recycles in IIS; by default IIS is set to recycle applications every 29 hours.</span></span>

<span data-ttu-id="3e85f-203">Siga los pasos que figuran a continuación para comprobar que la lógica de sustitución de claves funciona correctamente.</span><span class="sxs-lookup"><span data-stu-id="3e85f-203">Follow the steps below to verify that the key rollover logic is working.</span></span>

1. <span data-ttu-id="3e85f-204">Una vez que haya comprobado que la aplicación está utilizando el código anterior, abra el archivo **Web.config** y desplácese al bloque **<issuerNameRegistry>**; busque expresamente las siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="3e85f-204">After you have verified that your application is using the code above, open the **Web.config** file and navigate to the **<issuerNameRegistry>** block, specifically looking for the following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="3e85f-205">En la tabla **<add thumbprint=””>** , cambie el valor de la huella digital reemplazando cualquier carácter por otro diferente.</span><span class="sxs-lookup"><span data-stu-id="3e85f-205">In the **<add thumbprint=””>** setting, change the thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="3e85f-206">Guarde el archivo **Web.config** .</span><span class="sxs-lookup"><span data-stu-id="3e85f-206">Save the **Web.config** file.</span></span>
3. <span data-ttu-id="3e85f-207">Compile la aplicación y, después, ejecútela.</span><span class="sxs-lookup"><span data-stu-id="3e85f-207">Build the application, and then run it.</span></span> <span data-ttu-id="3e85f-208">Si puede completar el proceso de inicio de sesión, la aplicación actualizará correctamente la clave descargando la información necesaria del documento de metadatos de federación de su directorio.</span><span class="sxs-lookup"><span data-stu-id="3e85f-208">If you can complete the sign-in process, your application is successfully updating the key by downloading the required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="3e85f-209">Si tiene problemas para iniciar sesión, asegúrese de que los cambios en la aplicación sean correctos; para ello, consulte el tema [Adding Sign-On to Your Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) (Incorporación del inicio de sesión único en aplicaciones web mediante Azure AD), o bien descargue e inspeccione el siguiente código de ejemplo: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b) (Aplicación multiinquilino en la nube para Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="3e85f-209">If you are having issues signing in, ensure the changes in your application are correct by reading the [Adding Sign-On to Your Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting the following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="3e85f-210"><a name="vs2010"></a>Aplicaciones web de protección de recursos y creadas con Visual Studio 2008 o 2010 y Windows Identity Foundation (WIF) v1.0 para .NET 3.5</span><span class="sxs-lookup"><span data-stu-id="3e85f-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="3e85f-211">Si ha compilado una aplicación en la versión 1.0 de WIF, no habrá ningún mecanismo para actualizar automáticamente la configuración de la aplicación con el fin de usar una nueva clave.</span><span class="sxs-lookup"><span data-stu-id="3e85f-211">If you built an application on WIF v1.0, there is no provided mechanism to automatically refresh your application’s configuration to use a new key.</span></span>

* <span data-ttu-id="3e85f-212">*manera más sencilla* es usar las herramientas de FedUtil incluidas en el SDK de WIF, que pueden recuperar el documento de metadatos más reciente y actualizar la configuración.</span><span class="sxs-lookup"><span data-stu-id="3e85f-212">*Easiest way* Use the FedUtil tooling included in the WIF SDK, which can retrieve the latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="3e85f-213">Actualice la aplicación a .NET 4.5, que incluye la versión más reciente de WIF ubicada en el espacio de nombres del sistema.</span><span class="sxs-lookup"><span data-stu-id="3e85f-213">Update your application to .NET 4.5, which includes the newest version of WIF located in the System namespace.</span></span> <span data-ttu-id="3e85f-214">Después, podrá utilizar el [registro de nombres de emisor de validación (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) para realizar las actualizaciones automáticas de la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e85f-214">You can then use the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) to perform automatic updates of the application’s configuration.</span></span>
* <span data-ttu-id="3e85f-215">Realice una sustitución manual de acuerdo con las instrucciones al final de este documento de orientación.</span><span class="sxs-lookup"><span data-stu-id="3e85f-215">Perform a manual rollover as per the instructions at the end of this guidance document.</span></span>

<span data-ttu-id="3e85f-216">Instrucciones para usar FedUtil para actualizar la configuración:</span><span class="sxs-lookup"><span data-stu-id="3e85f-216">Instructions to use the FedUtil to update your configuration:</span></span>

1. <span data-ttu-id="3e85f-217">Compruebe que tiene instalado el SDK de la versión 1.0 de WIF en la máquina de desarrollo de Visual Studio 2008 o 2010.</span><span class="sxs-lookup"><span data-stu-id="3e85f-217">Verify that you have the WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="3e85f-218">También puede [descargarlo desde aquí](https://www.microsoft.com/en-us/download/details.aspx?id=4451) si aún no lo ha instalado.</span><span class="sxs-lookup"><span data-stu-id="3e85f-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="3e85f-219">En Visual Studio, abra la solución, haga clic con el botón derecho en el proyecto correspondiente y seleccione **Update federation metadata**(Actualizar metadatos de federación).</span><span class="sxs-lookup"><span data-stu-id="3e85f-219">In Visual Studio, open the solution, and then right-click the applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="3e85f-220">Si esta opción no está disponible, significa que no se ha instalado FedUtil o el SDK de la versión 1.0 de WIF.</span><span class="sxs-lookup"><span data-stu-id="3e85f-220">If this option is not available, FedUtil and/or the WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="3e85f-221">En el símbolo del sistema, seleccione **Actualizar** para iniciar la actualización de los metadatos de federación.</span><span class="sxs-lookup"><span data-stu-id="3e85f-221">From the prompt, select **Update** to begin updating your federation metadata.</span></span> <span data-ttu-id="3e85f-222">Si tiene acceso al entorno de servidor donde está hospedada la aplicación, puede utilizar el [Programador de actualización automática de metadatos](https://msdn.microsoft.com/library/ee517272.aspx)de FedUtil.</span><span class="sxs-lookup"><span data-stu-id="3e85f-222">If you have access to the server environment where the application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="3e85f-223">Haga clic en **Finalizar** para completar el proceso de actualización.</span><span class="sxs-lookup"><span data-stu-id="3e85f-223">Click **Finish** to complete the update process.</span></span>

### <span data-ttu-id="3e85f-224"><a name="other"></a>Aplicaciones y API web de protección de recursos que usan cualquier otra biblioteca o que implementan manualmente cualquiera de los protocolos admitidos</span><span class="sxs-lookup"><span data-stu-id="3e85f-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>
<span data-ttu-id="3e85f-225">Si está utilizando otra biblioteca o implementa manualmente cualquiera de los protocolos admitidos, debe revisar la biblioteca o la implementación para asegurarse de que se está recuperando la clave desde el documento de detección OpenID Connect o el documento de metadatos de federación.</span><span class="sxs-lookup"><span data-stu-id="3e85f-225">If you are using some other library or manually implemented any of the supported protocols, you'll need to review the library or your implementation to ensure that the key is being retrieved from either the OpenID Connect discovery document or the federation metadata document.</span></span> <span data-ttu-id="3e85f-226">Una forma de comprobarlo es realizar una búsqueda en el código o en el de la biblioteca de las llamadas al documento de detección OpenID o al documento de metadatos de federación.</span><span class="sxs-lookup"><span data-stu-id="3e85f-226">One way to check for this is to do a search in your code or the library's code for any calls out to either the OpenID discovery document or the federation metadata document.</span></span>

<span data-ttu-id="3e85f-227">Si la clave se está almacenando en algún lugar o está incrustada directamente en su aplicación, puede recuperar manualmente la clave y actualizarla según corresponda; para ello, realice una sustitución manual de acuerdo con las instrucciones al final de este documento de orientación.</span><span class="sxs-lookup"><span data-stu-id="3e85f-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve the key and update it accordingly by perform a manual rollover as per the instructions at the end of this guidance document.</span></span> <span data-ttu-id="3e85f-228">**se recomienda encarecidamente mejorar la aplicación para que admita la sustitución automática** mediante cualquiera de los enfoques descritos en este artículo.</span><span class="sxs-lookup"><span data-stu-id="3e85f-228">**It is strongly encouraged that you enhance your application to support automatic rollover** using any of the approaches outline in this article to avoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-to-test-your-application-to-determine-if-it-will-be-affected"></a><span data-ttu-id="3e85f-229">Cómo probar la aplicación para determinar si se verá afectada</span><span class="sxs-lookup"><span data-stu-id="3e85f-229">How to test your application to determine if it will be affected</span></span>
<span data-ttu-id="3e85f-230">Puede validar si la aplicación admite la sustitución automática de claves descargando los scripts y siguiendo las instrucciones de [este repositorio de GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="3e85f-230">You can validate whether your application supports automatic key rollover by downloading the scripts and following the instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-to-perform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="3e85f-231">Cómo realizar una sustitución manual si la aplicación no admite la sustitución automática</span><span class="sxs-lookup"><span data-stu-id="3e85f-231">How to perform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="3e85f-232">Si la aplicación **no** admite la sustitución automática, debe establecer un proceso que supervise periódicamente las claves de firma de Azure AD y realizar una sustitución manual cuando corresponda.</span><span class="sxs-lookup"><span data-stu-id="3e85f-232">If your application does **not** support automatic rollover, you will need to establish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="3e85f-233">[Este repositorio de GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contiene scripts e instrucciones sobre cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="3e85f-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how to do this.</span></span>

