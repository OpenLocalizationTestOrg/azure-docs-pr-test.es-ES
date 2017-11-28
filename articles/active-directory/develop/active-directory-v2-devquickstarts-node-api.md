---
title: aaaSecure una API web de v2.0 de Azure Active Directory mediante el uso de Node.js | Documentos de Microsoft
description: "Obtenga información acerca de cómo toobuild una Node.js web API que acepta los tokens de una cuenta Microsoft personal y de cuentas profesionales o educativas."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 0b572fc1-2aaf-4cb6-82de-63010fb1941d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 219e324cca11e107186b7e5f995589b9260af8a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="8e45f-103">Protección de una API web mediante Node.js</span><span class="sxs-lookup"><span data-stu-id="8e45f-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="8e45f-104">No todas las características y escenarios de Azure Active Directory funcionan con el punto de conexión de hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="8e45f-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="8e45f-105">toodetermine si debe utilizar Hola v2.0 extremo u Hola v1.0, conozca [v2.0 limitaciones](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="8e45f-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="8e45f-106">Cuando se usa el punto de conexión de hello Azure Active Directory (Azure AD) v2.0, puede usar [OAuth 2.0](active-directory-v2-protocols.md) tooprotect los tokens de acceso a la API web.</span><span class="sxs-lookup"><span data-stu-id="8e45f-106">When you use hello Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens tooprotect your web API.</span></span> <span data-ttu-id="8e45f-107">Con los tokens de OAuth 2.0, los usuarios que tienen una cuenta Microsoft personal, y cuentas profesionales o educativas, pueden acceder de forma segura a su API web.</span><span class="sxs-lookup"><span data-stu-id="8e45f-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="8e45f-108">*Passport* es middleware de autenticación para Node.js.</span><span class="sxs-lookup"><span data-stu-id="8e45f-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="8e45f-109">Passport, flexible y modular, se puede usar discretamente en cualquier aplicación web de Restify o basada en Express.</span><span class="sxs-lookup"><span data-stu-id="8e45f-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="8e45f-110">En esta herramienta, un conjunto completo de estrategias admite la autenticación mediante nombre de usuario y contraseña, Facebook, Twitter y mucho más.</span><span class="sxs-lookup"><span data-stu-id="8e45f-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="8e45f-111">Hemos desarrollado una estrategia para Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e45f-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="8e45f-112">En este artículo, le mostramos cómo tooinstall Hola módulo y, a continuación, agregue hello Azure AD `passport-azure-ad` complemento.</span><span class="sxs-lookup"><span data-stu-id="8e45f-112">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="8e45f-113">Descargar</span><span class="sxs-lookup"><span data-stu-id="8e45f-113">Download</span></span>
<span data-ttu-id="8e45f-114">código de Hello para este tutorial se mantiene [en GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span><span class="sxs-lookup"><span data-stu-id="8e45f-114">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="8e45f-115">tutorial de hello toofollow, puede [descargar el esqueleto de la aplicación hello como un archivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), o un clon Hola esqueleto:</span><span class="sxs-lookup"><span data-stu-id="8e45f-115">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="8e45f-116">También puede obtener la aplicación hello completado final Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8e45f-116">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="8e45f-117">1: Registro de una aplicación</span><span class="sxs-lookup"><span data-stu-id="8e45f-117">1: Register an app</span></span>
<span data-ttu-id="8e45f-118">Crear una nueva aplicación en [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o seguir [estos pasos detallan](active-directory-v2-app-registration.md) tooregister una aplicación.</span><span class="sxs-lookup"><span data-stu-id="8e45f-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="8e45f-119">Asegúrese de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8e45f-119">Make sure you:</span></span>

* <span data-ttu-id="8e45f-120">Hola copia **Id. de aplicación** asignado tooyour aplicación.</span><span class="sxs-lookup"><span data-stu-id="8e45f-120">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="8e45f-121">Lo necesitará para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8e45f-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="8e45f-122">Agregar hello **Mobile** plataforma para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8e45f-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="8e45f-123">Hola copia **URI de redireccionamiento** desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e45f-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="8e45f-124">Debe usar el valor de identificador URI predeterminado de Hola de `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="8e45f-124">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="8e45f-125">2: Instalación de Node.js</span><span class="sxs-lookup"><span data-stu-id="8e45f-125">2: Install Node.js</span></span>
<span data-ttu-id="8e45f-126">ejemplo de Hola a toouse para este tutorial, debe [instalar Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="8e45f-126">toouse hello sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="8e45f-127">3: Instalación de MongoDB</span><span class="sxs-lookup"><span data-stu-id="8e45f-127">3: Install MongoDB</span></span>
<span data-ttu-id="8e45f-128">toosuccessfully utilizar este ejemplo, debe [instalar MongoDB](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="8e45f-128">toosuccessfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="8e45f-129">En este ejemplo, utilizará MongoDB toomake la API de REST persistente en instancias del servidor.</span><span class="sxs-lookup"><span data-stu-id="8e45f-129">In this sample, you use MongoDB toomake your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="8e45f-130">En este artículo, supondremos que usan Hola instalación y servidor de puntos de conexión predeterminados para MongoDB: mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="8e45f-130">In this article, we assume that you use hello default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="8e45f-131">4: instalar hello restify módulos en la API web</span><span class="sxs-lookup"><span data-stu-id="8e45f-131">4: Install hello restify modules in your web API</span></span>
<span data-ttu-id="8e45f-132">Utilizamos Resitfy toobuild nuestra API de REST.</span><span class="sxs-lookup"><span data-stu-id="8e45f-132">We use Resitfy toobuild our REST API.</span></span> <span data-ttu-id="8e45f-133">Restify es un marco de trabajo de la aplicación de Node.js mínimo y flexible que se deriva de Express.</span><span class="sxs-lookup"><span data-stu-id="8e45f-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="8e45f-134">Restify tiene un conjunto robusto de características que puede usar toobuild encima de conectar las API de REST.</span><span class="sxs-lookup"><span data-stu-id="8e45f-134">Restify has a robust set of features that you can use toobuild REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="8e45f-135">Instalación de Restify</span><span class="sxs-lookup"><span data-stu-id="8e45f-135">Install restify</span></span>
1.  <span data-ttu-id="8e45f-136">En un símbolo del sistema, cambie el directorio de hello demasiado**organización**:</span><span class="sxs-lookup"><span data-stu-id="8e45f-136">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="8e45f-137">Si hello **organización** directorio no existe, créelo:</span><span class="sxs-lookup"><span data-stu-id="8e45f-137">If hello **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="8e45f-138">Instale Restify:</span><span class="sxs-lookup"><span data-stu-id="8e45f-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="8e45f-139">resultado de Hello de este comando debe tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="8e45f-139">hello output of this command should look like this:</span></span>

    ```
    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0(mv@0.0.5)
    ```

#### <a name="did-you-get-an-error"></a><span data-ttu-id="8e45f-140">¿Ha recibido un error?</span><span class="sxs-lookup"><span data-stu-id="8e45f-140">Did you get an error?</span></span>
<span data-ttu-id="8e45f-141">En algunos sistemas operativos, cuando se usa hello `npm` comando, verá este mensaje: `Error: EPERM, chmod '/usr/local/bin/..'`.</span><span class="sxs-lookup"><span data-stu-id="8e45f-141">On some operating systems, when you use hello `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="8e45f-142">error de Hello va seguido de una solicitud que intentas ejecución cuenta de hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="8e45f-142">hello error is followed by a request that you try running hello account as an administrator.</span></span> <span data-ttu-id="8e45f-143">Si esto ocurre, use el comando de hello `sudo` toorun `npm` en un nivel de privilegios superior.</span><span class="sxs-lookup"><span data-stu-id="8e45f-143">If this occurs, use hello command `sudo` toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-toodtrace"></a><span data-ttu-id="8e45f-144">¿Obtuvo un error relacionado con tooDTrace?</span><span class="sxs-lookup"><span data-stu-id="8e45f-144">Did you get an error related tooDTrace?</span></span>
<span data-ttu-id="8e45f-145">Al instalar Restify, podría aparecer este mensaje:</span><span class="sxs-lookup"><span data-stu-id="8e45f-145">When you install restify, you might see this message:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: two
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```

<span data-ttu-id="8e45f-146">Restify tiene un tootrace un mecanismo eficaz llamadas REST mediante el uso de DTrace.</span><span class="sxs-lookup"><span data-stu-id="8e45f-146">Restify has a powerful mechanism tootrace REST calls by using DTrace.</span></span> <span data-ttu-id="8e45f-147">Sin embargo, DTrace no está disponible en muchos sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="8e45f-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="8e45f-148">Puede omitir estos errores.</span><span class="sxs-lookup"><span data-stu-id="8e45f-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="8e45f-149">Paso 5: Instalación de Passport.js en su API web</span><span class="sxs-lookup"><span data-stu-id="8e45f-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="8e45f-150">En hello símbolo del sistema, cambie el directorio de hello demasiado**organización**.</span><span class="sxs-lookup"><span data-stu-id="8e45f-150">At hello command prompt, change hello directory too**azuread**.</span></span>

2.  <span data-ttu-id="8e45f-151">Instale Passport.js:</span><span class="sxs-lookup"><span data-stu-id="8e45f-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="8e45f-152">Hola resultado del comando de hello debería tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="8e45f-152">hello output of hello command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-tooyour-web-api"></a><span data-ttu-id="8e45f-153">6: agregar ad de azure de passport tooyour web API</span><span class="sxs-lookup"><span data-stu-id="8e45f-153">6: Add passport-azure-ad tooyour web API</span></span>
<span data-ttu-id="8e45f-154">A continuación, agregue la estrategia de OAuth de hello, mediante el uso de la organización de passport.</span><span class="sxs-lookup"><span data-stu-id="8e45f-154">Next, add hello OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="8e45f-155">`passport-azuread` es un conjunto de estrategias que conectan Azure AD a Passport.</span><span class="sxs-lookup"><span data-stu-id="8e45f-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="8e45f-156">En este ejemplo de API de REST, esta estrategia se usa para los tokens de portador.</span><span class="sxs-lookup"><span data-stu-id="8e45f-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="8e45f-157">Aunque OAuth 2.0 proporciona un marco en el que se puede emitir cualquier tipo de token conocido, habitualmente se usan determinados tipos de token.</span><span class="sxs-lookup"><span data-stu-id="8e45f-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="8e45f-158">Tokens de portador son puntos de conexión de tooprotect utilizadas.</span><span class="sxs-lookup"><span data-stu-id="8e45f-158">Bearer tokens are commonly used tooprotect endpoints.</span></span> <span data-ttu-id="8e45f-159">Tokens de portador son tipo de hello emitido más comúnmente de token de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="8e45f-159">Bearer tokens are hello most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="8e45f-160">Muchas implementaciones de OAuth 2.0, se supone que los tokens de portador son Hola único tipo de token emitido.</span><span class="sxs-lookup"><span data-stu-id="8e45f-160">Many OAuth 2.0 implementations assume that bearer tokens are hello only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="8e45f-161">En un símbolo del sistema, cambie el directorio de hello demasiado**organización**.</span><span class="sxs-lookup"><span data-stu-id="8e45f-161">At a command prompt, change hello directory too**azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="8e45f-162">Instalar hello Passport.js `passport-azure-ad` módulo:</span><span class="sxs-lookup"><span data-stu-id="8e45f-162">Install hello Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="8e45f-163">Hola resultado del comando de hello debería tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="8e45f-163">hello output of hello command should look like this:</span></span>

    ```
    passport-azure-ad@1.0.0 node_modules/passport-azure-ad
    ├── xtend@4.0.0
    ├── xmldom@0.1.19
    ├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
    ├── underscore@1.8.3
    ├── async@1.3.0
    ├── jsonwebtoken@5.0.2
    ├── xml-crypto@0.5.27 (xpath.js@1.0.6)
    ├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
    ├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
    ├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    └── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
    ```

## <a name="7-add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="8e45f-164">7: agregar MongoDB módulos tooyour web API</span><span class="sxs-lookup"><span data-stu-id="8e45f-164">7: Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="8e45f-165">En este ejemplo, utilizamos MongoDB como el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="8e45f-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="8e45f-166">Instalar Mongoose, ampliamente utilizado complemento, toomanage modelos y esquemas:</span><span class="sxs-lookup"><span data-stu-id="8e45f-166">Install Mongoose, a widely used plug-in, toomanage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="8e45f-167">Instalar el controlador de la base de datos de Hola para MongoDB, que también se denomina MongoDB:</span><span class="sxs-lookup"><span data-stu-id="8e45f-167">Install hello database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="8e45f-168">8: Instalar módulos adicionales</span><span class="sxs-lookup"><span data-stu-id="8e45f-168">8: Install additional modules</span></span>
<span data-ttu-id="8e45f-169">Instalar Hola restantes módulos necesarios.</span><span class="sxs-lookup"><span data-stu-id="8e45f-169">Install hello remaining required modules.</span></span>

1.  <span data-ttu-id="8e45f-170">En un símbolo del sistema, cambie el directorio de hello demasiado**organización**:</span><span class="sxs-lookup"><span data-stu-id="8e45f-170">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="8e45f-171">Escriba Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="8e45f-171">Enter hello following commands.</span></span> <span data-ttu-id="8e45f-172">comandos de Hello instalan Hola después de módulos en el directorio node_modules:</span><span class="sxs-lookup"><span data-stu-id="8e45f-172">hello commands install hello following modules in your node_modules directory:</span></span>

    *   `npm install crypto`
    *   `npm install assert-plus`
    *   `npm install posix-getopt`
    *   `npm install util`
    *   `npm install path`
    *   `npm install connect`
    *   `npm install xml-crypto`
    *   `npm install xml2js`
    *   `npm install xmldom`
    *   `npm install async`
    *   `npm install request`
    *   `npm install underscore`
    *   `npm install grunt-contrib-jshint@0.1.1`
    *   `npm install grunt-contrib-nodeunit@0.1.2`
    *   `npm install grunt-contrib-watch@0.2.0`
    *   `npm install grunt@0.4.1`
    *   `npm install xtend@2.0.3`
    *   `npm install bunyan`
    *   `npm update`

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="8e45f-173">9: Creación de un archivo server.js con sus dependencias</span><span class="sxs-lookup"><span data-stu-id="8e45f-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="8e45f-174">Un archivo de Server.js contiene la mayoría de Hola de funcionalidad de hello para el servidor de la API web.</span><span class="sxs-lookup"><span data-stu-id="8e45f-174">A Server.js file holds hello majority of hello functionality for your web API server.</span></span> <span data-ttu-id="8e45f-175">Agregue la mayor parte de su archivo de código toothis.</span><span class="sxs-lookup"><span data-stu-id="8e45f-175">Add most of your code toothis file.</span></span> <span data-ttu-id="8e45f-176">Para fines de producción, puede refactorizar funcionalidad hello en archivos más pequeños, como para los controladores y rutas separadas que cubre.</span><span class="sxs-lookup"><span data-stu-id="8e45f-176">For production purposes, you can refactor hello functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="8e45f-177">En este artículo, utilizamos Server.js para este fin.</span><span class="sxs-lookup"><span data-stu-id="8e45f-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="8e45f-178">En un símbolo del sistema, cambie el directorio de hello demasiado**organización**:</span><span class="sxs-lookup"><span data-stu-id="8e45f-178">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="8e45f-179">Con el editor que prefiera, cree un archivo Server.js.</span><span class="sxs-lookup"><span data-stu-id="8e45f-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="8e45f-180">Agregue Hola información toohello archivo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8e45f-180">Add hello following information toohello file:</span></span>

    ```Javascript
    'use strict';
    /**
    * Module dependencies.
    */
    var util = require('util');
    var assert = require('assert-plus');
    var mongoose = require('mongoose/');
    var bunyan = require('bunyan');
    var restify = require('restify');
    var config = require('./config');
    var passport = require('passport');
    var OIDCBearerStrategy = require('passport-azure-ad').OIDCStrategy;
    ```

3.  <span data-ttu-id="8e45f-181">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="8e45f-181">Save hello file.</span></span> <span data-ttu-id="8e45f-182">Se devolverá tooit en breve.</span><span class="sxs-lookup"><span data-stu-id="8e45f-182">You will return tooit shortly.</span></span>

## <a name="10-create-a-config-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="8e45f-183">10: crear un toostore del archivo de configuración de la configuración de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e45f-183">10: Create a config file toostore your Azure AD settings</span></span>
<span data-ttu-id="8e45f-184">Este archivo de código pasa los parámetros de configuración de Hola de su tooPassport.js de portal de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e45f-184">This code file passes hello configuration parameters from your Azure AD portal tooPassport.js.</span></span> <span data-ttu-id="8e45f-185">Estos valores de configuración se crean cuando se agrega hello web API toohello el portal al principio de Hola de artículo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e45f-185">You created these configuration values when you added hello web API toohello portal at hello beginning of hello article.</span></span> <span data-ttu-id="8e45f-186">Después de copiar el código de hello, explicaremos qué tooput en valores de hello de estos parámetros.</span><span class="sxs-lookup"><span data-stu-id="8e45f-186">After you copy hello code, we'll explain what tooput in hello values of these parameters.</span></span>

1.  <span data-ttu-id="8e45f-187">En un símbolo del sistema, cambie el directorio de hello demasiado**organización**:</span><span class="sxs-lookup"><span data-stu-id="8e45f-187">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="8e45f-188">En un editor, cree un archivo Config.js.</span><span class="sxs-lookup"><span data-stu-id="8e45f-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="8e45f-189">Agregue Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="8e45f-189">Add hello following information:</span></span>

    ```Javascript
    // Don't commit this file tooyour public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need toochange this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="8e45f-190">Valores obligatorios</span><span class="sxs-lookup"><span data-stu-id="8e45f-190">Required values</span></span>

*   <span data-ttu-id="8e45f-191">**IdentityMetadata**: aquí es donde `passport-azure-ad` busca los datos de configuración para el proveedor de identidades (IDP) de Hola y Hola claves toovalidate Hola Tokens de Web JSON (Jwt).</span><span class="sxs-lookup"><span data-stu-id="8e45f-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for hello identity provider (IDP) and hello keys toovalidate hello JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="8e45f-192">Si utilizas Azure AD, probablemente no desee toochange esto.</span><span class="sxs-lookup"><span data-stu-id="8e45f-192">If you are using Azure AD, you probably don't want toochange this.</span></span>

*   <span data-ttu-id="8e45f-193">**audiencia**: el URI de redirección desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e45f-193">**audience**: Your redirect URI from hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="8e45f-194">Distribuimos sus claves con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="8e45f-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="8e45f-195">Asegúrese de que siempre de extracción de dirección URL de "openid_keys" Hola, y esa aplicación hello puede tener acceso a Internet de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e45f-195">Be sure that you always pull from hello "openid_keys" URL, and that hello app can access hello Internet.</span></span>
> 
> 

## <a name="11-add-hello-configuration-tooyour-serverjs-file"></a><span data-ttu-id="8e45f-196">11: agregar tooyour Server.js archivo de configuración de Hola</span><span class="sxs-lookup"><span data-stu-id="8e45f-196">11: Add hello configuration tooyour Server.js file</span></span>
<span data-ttu-id="8e45f-197">La aplicación necesita valores de hello tooread del archivo de configuración de Hola que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="8e45f-197">Your application needs tooread hello values from hello config file you just created.</span></span> <span data-ttu-id="8e45f-198">Agregue el archivo .config de hello como un recurso necesario en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8e45f-198">Add hello .config file as a required resource in your application.</span></span> <span data-ttu-id="8e45f-199">Establecer hello toothose de variables globales que se encuentran en Config.js.</span><span class="sxs-lookup"><span data-stu-id="8e45f-199">Set hello global variables toothose that are in Config.js.</span></span>

1.  <span data-ttu-id="8e45f-200">En hello símbolo del sistema, cambie el directorio de hello demasiado**organización**:</span><span class="sxs-lookup"><span data-stu-id="8e45f-200">At hello command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="8e45f-201">En un editor, abra Server.js.</span><span class="sxs-lookup"><span data-stu-id="8e45f-201">In an editor, open Server.js.</span></span> <span data-ttu-id="8e45f-202">Agregue Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="8e45f-202">Add hello following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="8e45f-203">Agregue un nuevo tooServer.js de sección:</span><span class="sxs-lookup"><span data-stu-id="8e45f-203">Add a new section tooServer.js:</span></span>

    ```Javascript
    // Pass these options in toohello ODICBearerStrategy.
    var options = {
    // hello URL of hello metadata document for your app. Put hello keys for token validation from hello URL found in hello jwks_uri tag in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array toohold signed-in users and hello current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="8e45f-204">12: agregar Hola MongoDB modelo e información de esquema mediante Mongoose</span><span class="sxs-lookup"><span data-stu-id="8e45f-204">12: Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="8e45f-205">Después, conecte estos tres archivos en un servicio de API de REST.</span><span class="sxs-lookup"><span data-stu-id="8e45f-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="8e45f-206">En este artículo, utilizamos MongoDB toostore nuestro tareas.</span><span class="sxs-lookup"><span data-stu-id="8e45f-206">In this article, we use MongoDB toostore our tasks.</span></span> <span data-ttu-id="8e45f-207">Se explican en el *paso 4*.</span><span class="sxs-lookup"><span data-stu-id="8e45f-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="8e45f-208">En el archivo de hello Config.js que creó en el paso 11, se llama a la base de datos *tasklist*.</span><span class="sxs-lookup"><span data-stu-id="8e45f-208">In hello Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="8e45f-209">Eso estaba coloca al final de saludo de la dirección URL de conexión de mongoose_auth_local.</span><span class="sxs-lookup"><span data-stu-id="8e45f-209">That was what you put at hello end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="8e45f-210">No es necesario toocreate esta base de datos con antelación en MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8e45f-210">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="8e45f-211">Hola crear base de datos en hello primero ejecución de la aplicación de servidor (suponiendo que la base de datos de hello aún no existe).</span><span class="sxs-lookup"><span data-stu-id="8e45f-211">hello database is created on hello first run of your server application (assuming hello database does not already exist).</span></span>

<span data-ttu-id="8e45f-212">Ha dijo a servidor hello qué toouse de base de datos de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8e45f-212">You've told hello server what MongoDB database toouse.</span></span> <span data-ttu-id="8e45f-213">A continuación, debe toowrite algunos modelos de código adicional toocreate Hola y el esquema para las tareas de su servidor.</span><span class="sxs-lookup"><span data-stu-id="8e45f-213">Next, you need toowrite some additional code toocreate hello model and schema for your server's tasks.</span></span>

### <a name="hello-model"></a><span data-ttu-id="8e45f-214">modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="8e45f-214">hello model</span></span>
<span data-ttu-id="8e45f-215">modelo de esquema de Hello es muy básica.</span><span class="sxs-lookup"><span data-stu-id="8e45f-215">hello schema model is very basic.</span></span> <span data-ttu-id="8e45f-216">Puede expandirlo si lo necesita.</span><span class="sxs-lookup"><span data-stu-id="8e45f-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="8e45f-217">modelo de esquema de Hello tiene estos valores:</span><span class="sxs-lookup"><span data-stu-id="8e45f-217">hello schema model has these values:</span></span>

*   <span data-ttu-id="8e45f-218">**NAME**.</span><span class="sxs-lookup"><span data-stu-id="8e45f-218">**NAME**.</span></span> <span data-ttu-id="8e45f-219">tarea de Hello persona toohello asignado.</span><span class="sxs-lookup"><span data-stu-id="8e45f-219">hello person assigned toohello task.</span></span> <span data-ttu-id="8e45f-220">Se trata de un valor de **cadena**.</span><span class="sxs-lookup"><span data-stu-id="8e45f-220">This is a **string** value.</span></span>
*   <span data-ttu-id="8e45f-221">**TASK**.</span><span class="sxs-lookup"><span data-stu-id="8e45f-221">**TASK**.</span></span> <span data-ttu-id="8e45f-222">nombre de Hola de tarea hello.</span><span class="sxs-lookup"><span data-stu-id="8e45f-222">hello name of hello task.</span></span> <span data-ttu-id="8e45f-223">Se trata de un valor de **cadena**.</span><span class="sxs-lookup"><span data-stu-id="8e45f-223">This is a **string** value.</span></span>
*   <span data-ttu-id="8e45f-224">**DATE**.</span><span class="sxs-lookup"><span data-stu-id="8e45f-224">**DATE**.</span></span> <span data-ttu-id="8e45f-225">fecha de Hello vence esa tarea hello.</span><span class="sxs-lookup"><span data-stu-id="8e45f-225">hello date that hello task is due.</span></span> <span data-ttu-id="8e45f-226">Se trata de un **datetime** valor.</span><span class="sxs-lookup"><span data-stu-id="8e45f-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="8e45f-227">**COMPLETED**.</span><span class="sxs-lookup"><span data-stu-id="8e45f-227">**COMPLETED**.</span></span> <span data-ttu-id="8e45f-228">Si se completa la tarea hello.</span><span class="sxs-lookup"><span data-stu-id="8e45f-228">Whether hello task is completed.</span></span> <span data-ttu-id="8e45f-229">Se trata de un elemento **booleano**.</span><span class="sxs-lookup"><span data-stu-id="8e45f-229">This is a **Boolean** value.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="8e45f-230">Crear esquemas de hello en el código de hello</span><span class="sxs-lookup"><span data-stu-id="8e45f-230">Create hello schema in hello code</span></span>
1.  <span data-ttu-id="8e45f-231">En un símbolo del sistema, cambie el directorio de hello demasiado**organización**:</span><span class="sxs-lookup"><span data-stu-id="8e45f-231">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="8e45f-232">En el editor, abra Server.js.</span><span class="sxs-lookup"><span data-stu-id="8e45f-232">In your editor, open Server.js.</span></span> <span data-ttu-id="8e45f-233">Por debajo de la entrada de configuración de hello, agregue Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="8e45f-233">Below hello configuration entry, add hello following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="8e45f-234">Este código conecta toohello MongoDB server.</span><span class="sxs-lookup"><span data-stu-id="8e45f-234">This code connects toohello MongoDB server.</span></span> <span data-ttu-id="8e45f-235">También devuelve un objeto de esquema.</span><span class="sxs-lookup"><span data-stu-id="8e45f-235">It also returns a schema object.</span></span>

#### <a name="using-hello-schema-create-your-model-in-hello-code"></a><span data-ttu-id="8e45f-236">Usa el esquema de hello, crear el modelo en el código de hello</span><span class="sxs-lookup"><span data-stu-id="8e45f-236">Using hello schema, create your model in hello code</span></span>
<span data-ttu-id="8e45f-237">Debajo de hello anterior de código, agregue Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="8e45f-237">Below hello preceding code, add hello following code:</span></span>

```Javascript
// Create a basic schema toostore your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use hello schema tooregister a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="8e45f-238">Como puede imaginar desde el código de hello, primero debe crear el esquema.</span><span class="sxs-lookup"><span data-stu-id="8e45f-238">As you can tell from hello code, first you create your schema.</span></span> <span data-ttu-id="8e45f-239">Después, un objeto de modelo.</span><span class="sxs-lookup"><span data-stu-id="8e45f-239">Next, you create a model object.</span></span> <span data-ttu-id="8e45f-240">Usar toostore de objeto de modelo de hello los datos a lo largo de Hola de código cuando se define la **rutas**.</span><span class="sxs-lookup"><span data-stu-id="8e45f-240">You use hello model object toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="8e45f-241">13: Incorporación de las rutas para el servidor de API de REST de su tarea</span><span class="sxs-lookup"><span data-stu-id="8e45f-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="8e45f-242">Ahora que tiene un toowork de modelo de base de datos con, agregar rutas de Hola que va a utilizar para el servidor de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="8e45f-242">Now that you have a database model toowork with, add hello routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="8e45f-243">Información de las rutas en Restify</span><span class="sxs-lookup"><span data-stu-id="8e45f-243">About routes in restify</span></span>
<span data-ttu-id="8e45f-244">Rutas de restify trabajo exactamente hello igual que lo hacen cuando se usa Hola pila de Express.</span><span class="sxs-lookup"><span data-stu-id="8e45f-244">Routes in restify work exactly hello same way they do when you use hello Express stack.</span></span> <span data-ttu-id="8e45f-245">Definir las rutas mediante el uso de URI que se espera toocall de las aplicaciones de cliente de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="8e45f-245">You define routes by using hello URI that you expect hello client applications toocall.</span></span> <span data-ttu-id="8e45f-246">Normalmente, las rutas se definen en un archivo independiente.</span><span class="sxs-lookup"><span data-stu-id="8e45f-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="8e45f-247">En este tutorial, colocamos nuestra rutas en Server.js.</span><span class="sxs-lookup"><span data-stu-id="8e45f-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="8e45f-248">Se recomienda diseñarlas en su propio archivo para que se puedan usar en producción.</span><span class="sxs-lookup"><span data-stu-id="8e45f-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="8e45f-249">Un patrón típico de una ruta Restify es:</span><span class="sxs-lookup"><span data-stu-id="8e45f-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep hello server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="8e45f-250">Este es el patrón de hello en el nivel más básico de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e45f-250">This is hello pattern at hello most basic level.</span></span> <span data-ttu-id="8e45f-251">Restify (y Express) proporcionan una funcionalidad mucho más profunda, como tipos de aplicaciones de toodefine de capacidad de Hola y el enrutamiento complejo en distintos puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="8e45f-251">Restify (and Express) provide much deeper functionality, like hello ability toodefine application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="8e45f-252">Agregar servidor de forma predeterminada las rutas tooyour</span><span class="sxs-lookup"><span data-stu-id="8e45f-252">Add default routes tooyour server</span></span>
<span data-ttu-id="8e45f-253">Agregar rutas de hello básicas CRUD: **crear**, **recuperar**, **actualizar**, y **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="8e45f-253">Add hello basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="8e45f-254">En un símbolo del sistema, cambie el directorio de hello demasiado**organización**:</span><span class="sxs-lookup"><span data-stu-id="8e45f-254">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="8e45f-255">En un editor, abra Server.js.</span><span class="sxs-lookup"><span data-stu-id="8e45f-255">In an editor, open Server.js.</span></span> <span data-ttu-id="8e45f-256">A continuación Hola entradas de base de datos realizadas anteriormente, agregue Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="8e45f-256">Below hello database entries you made earlier, add hello following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow you toouse MongoDB Server as your response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it tooMongoDB.
    var _task = new Task();
    if (!req.params.task) {
    req.log.warn({
    params: p
    }, 'createTodo: missing task');
    next(new MissingTaskError());
    return;
    }
    _task.owner = owner;
    _task.task = req.params.task;
    _task.date = new Date();
    _task.save(function(err) {
    if (err) {
    req.log.warn(err, 'createTask: unable toosave');
    next(err);
    } else {
    res.send(201, _task);
    }
    });
    return next();
    }
    // Delete a task by name.
    function removeTask(req, res, next) {
    Task.remove({
    task: req.params.task,
    owner: owner
    }, function(err) {
    if (err) {
    req.log.warn(err,
    'removeTask: unable toodelete %s',
    req.params.task);
    next(err);
    } else {
    log.info('Deleted task:', req.params.task);
    res.send(204);
    next();
    }
    });
    }
    // Delete all tasks.
    function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
    }
    // Get a specific task based on name.
    function getTask(req, res, next) {
    log.info('getTask was called for: ', owner);
    Task.find({
    owner: owner
    }, function(err, data) {
    if (err) {
    req.log.warn(err, 'get: unable tooread %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns hello list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow us toouse MongoDB Server as our response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    log.info("listTasks was called for: ", owner);
    Task.find({
    owner: owner
    }).limit(20).sort('date').exec(function(err, data) {
    if (err)
    return next(err);
    if (data.length > 0) {
    log.info(data);
    }
    if (!data.length) {
    log.warn(err, "There are no tasks in hello database. Add one!");
    }
    if (!owner) {
    log.warn(err, "You did not pass an owner when listing tasks.");
    } else {
    res.json(data);
    }
    });
    return next();
    }
    ```

### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="8e45f-257">Agregar control de errores para las rutas de Hola</span><span class="sxs-lookup"><span data-stu-id="8e45f-257">Add error handling for hello routes</span></span>
<span data-ttu-id="8e45f-258">Agregue algunos control de errores de forma que pueda comunicarse a toohello atrás cliente acerca de cómo detectó un problema en Hola.</span><span class="sxs-lookup"><span data-stu-id="8e45f-258">Add some error handling so you can communicate back toohello client about hello problem you encountered.</span></span>

<span data-ttu-id="8e45f-259">Agregue Hola siguiendo el siguiente código de hello, que ya ha escrito código:</span><span class="sxs-lookup"><span data-stu-id="8e45f-259">Add hello following code below hello code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back toohello client.
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="14-create-your-server"></a><span data-ttu-id="8e45f-260">14: Creación del servidor</span><span class="sxs-lookup"><span data-stu-id="8e45f-260">14: Create your server</span></span>
<span data-ttu-id="8e45f-261">Hola toodo de lo último es tooadd la instancia del servidor.</span><span class="sxs-lookup"><span data-stu-id="8e45f-261">hello last thing toodo is tooadd your server instance.</span></span> <span data-ttu-id="8e45f-262">instancia del servidor Hello controla sus llamadas.</span><span class="sxs-lookup"><span data-stu-id="8e45f-262">hello server instance manages your calls.</span></span>

<span data-ttu-id="8e45f-263">Restify (y Express) tiene una personalización más avanzada que puede usar con un servidor de API de REST.</span><span class="sxs-lookup"><span data-stu-id="8e45f-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="8e45f-264">En este tutorial, se usa el programa de instalación más sencilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e45f-264">In this tutorial, we use hello most basic setup.</span></span>

```Javascript
/**
* Your server
*/
var server = restify.createServer({
name: "Microsoft Azure Active Directory TODO Server",
version: "2.0.1"
});
// Ensure that you don't drop data on uploads.
server.pre(restify.pre.pause());
// Clean up imprecise paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());
// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());
// Set a per-request Bunyan logger (with requestid filled in).
server.use(restify.requestLogger());
// Allow 5 requests/second by IP address, and burst too10.
server.use(restify.throttle({
burst: 10,
rate: 5,
ip: true,
}));
// Use common commands, such as:
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
mapParams: true
}));
```
## <a name="15-add-hello-routes-without-authentication-for-now"></a><span data-ttu-id="8e45f-265">15: agregar rutas de hello (sin autenticación, por ahora)</span><span class="sxs-lookup"><span data-stu-id="8e45f-265">15: Add hello routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD tooadd hello real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in hello pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need toomaintain session state. You can experiment with removing API protection.
/* toodo this, remove hello passport.authenticate() method:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-hello-server"></a><span data-ttu-id="8e45f-266">16: ejecutar servidor hello</span><span class="sxs-lookup"><span data-stu-id="8e45f-266">16: Run hello server</span></span>
<span data-ttu-id="8e45f-267">Es una buena idea tootest el servidor antes de agregar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="8e45f-267">It's a good idea tootest your server before you add authentication.</span></span>

<span data-ttu-id="8e45f-268">Hola tootest de manera más fácil su servidor consiste en usar curl en un símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="8e45f-268">hello easiest way tootest your server is by using curl at a command prompt.</span></span> <span data-ttu-id="8e45f-269">toodo, necesita una utilidad simple que pueden usar tooparse salida como JSON.</span><span class="sxs-lookup"><span data-stu-id="8e45f-269">toodo this, you need a simple utility that you can use tooparse output as JSON.</span></span> 

1.  <span data-ttu-id="8e45f-270">Instale la herramienta JSON de Hola que utilizamos en hello en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8e45f-270">Install hello JSON tool that we use in hello following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="8e45f-271">Esto instala herramienta JSON de hello globalmente.</span><span class="sxs-lookup"><span data-stu-id="8e45f-271">This installs hello JSON tool globally.</span></span>

2.  <span data-ttu-id="8e45f-272">Asegúrese de que la instancia de MongoDB se esté ejecutando:</span><span class="sxs-lookup"><span data-stu-id="8e45f-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="8e45f-273">Cambie el directorio de hello demasiado**organización**, y, a continuación, ejecute curl:</span><span class="sxs-lookup"><span data-stu-id="8e45f-273">Change hello directory too**azuread**, and then run curl:</span></span>

    `$ cd azuread`
    `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 2.0OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4.  <span data-ttu-id="8e45f-274">tooadd una tarea:</span><span class="sxs-lookup"><span data-stu-id="8e45f-274">tooadd a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="8e45f-275">respuesta de Hello debe ser:</span><span class="sxs-lookup"><span data-stu-id="8e45f-275">hello response should be:</span></span>

    ```Shell
    HTTP/1.1 201 Created
    Connection: close
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Headers: X-Requested-With
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 5
    Date: Tue, 04 Feb 2014 01:02:26 GMT
    Hello
    ```

5.  <span data-ttu-id="8e45f-276">Lista de tareas de Brandon:</span><span class="sxs-lookup"><span data-stu-id="8e45f-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="8e45f-277">Si todos estos comandos se ejecutan sin errores, es el servidor de la API de REST de listo tooadd OAuth toohello.</span><span class="sxs-lookup"><span data-stu-id="8e45f-277">If all these commands run without errors, you are ready tooadd OAuth toohello REST API server.</span></span>

<span data-ttu-id="8e45f-278">*Ahora tiene un servidor de API de REST con MongoDB.*</span><span class="sxs-lookup"><span data-stu-id="8e45f-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="8e45f-279">17: Agregar servidor de la API de REST de autenticación tooyour</span><span class="sxs-lookup"><span data-stu-id="8e45f-279">17: Add authentication tooyour REST API server</span></span>
<span data-ttu-id="8e45f-280">Ahora que tiene una API de REST de ejecución, se configura toouse con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e45f-280">Now that you have a running REST API, set it up toouse it with Azure AD.</span></span>

<span data-ttu-id="8e45f-281">En un símbolo del sistema, cambie el directorio de hello demasiado**organización**:</span><span class="sxs-lookup"><span data-stu-id="8e45f-281">At a command prompt, change hello directory too**azuread**:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="8e45f-282">Use hello oidcbearerstrategy que se incluye con azure de passport de ad</span><span class="sxs-lookup"><span data-stu-id="8e45f-282">Use hello oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="8e45f-283">Hasta ahora hemos creado un servidor típico de TODO de REST sin ningún tipo de autorización.</span><span class="sxs-lookup"><span data-stu-id="8e45f-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="8e45f-284">Ahora, agregue la autenticación.</span><span class="sxs-lookup"><span data-stu-id="8e45f-284">Now, add authentication.</span></span>

<span data-ttu-id="8e45f-285">En primer lugar, indique que desea que toouse Passport.</span><span class="sxs-lookup"><span data-stu-id="8e45f-285">First,  indicate that you want toouse Passport.</span></span> <span data-ttu-id="8e45f-286">Incluya esto justo después de la configuración del servidor anterior:</span><span class="sxs-lookup"><span data-stu-id="8e45f-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="8e45f-287">Al escribir las API, es un Hola de vínculo de tooalways buena idea toosomething de datos único del token de Hola que Hola usuario no se puede suplantar la identidad.</span><span class="sxs-lookup"><span data-stu-id="8e45f-287">When you write APIs, it's a good idea tooalways link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="8e45f-288">Cuando este servidor almacena elementos de lista de tareas, almacena en función del Id. de suscripción de usuario de Hola de símbolo (token) de hello (llamado a través de token.sub).</span><span class="sxs-lookup"><span data-stu-id="8e45f-288">When this server stores TODO items, it stores them based on hello user subscription ID in hello token (called through token.sub).</span></span> <span data-ttu-id="8e45f-289">Coloque token.sub hello en el campo de "propietario" Hola.</span><span class="sxs-lookup"><span data-stu-id="8e45f-289">You put hello token.sub in hello “owner” field.</span></span> <span data-ttu-id="8e45f-290">Esto garantiza que sólo ese usuario puede tener acceso a TODOs del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e45f-290">This ensures that only that user can access hello user's TODOs.</span></span> <span data-ttu-id="8e45f-291">Nadie más puede tener acceso a TODOs Hola que se especificaron.</span><span class="sxs-lookup"><span data-stu-id="8e45f-291">No one else can access hello TODOs that were entered.</span></span> <span data-ttu-id="8e45f-292">No hay ningún riesgo en hello API para el "propietario".</span><span class="sxs-lookup"><span data-stu-id="8e45f-292">There is no exposure in hello API for “owner.”</span></span> <span data-ttu-id="8e45f-293">Un usuario externo puede solicitar las tareas pendientes de otros usuarios, incluso si estos se autentican.</span><span class="sxs-lookup"><span data-stu-id="8e45f-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="8e45f-294">A continuación, use la estrategia de portador de conectarse de identificador abierto de Hola que viene con `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="8e45f-294">Next, use hello Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="8e45f-295">Colóquela después de lo que pegó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="8e45f-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling hello OIDCBearerStrategy and managing users.
/*
/* Because of hello Passport pattern, you need toomanage users and info tokens
/* with a FindorCreate() method. hello method must be provided by hello implementor.
/* In hello following code, you autoregister any user and implement a FindById().
/* It's a good idea toodo something more advanced.
**/
var findById = function(id, fn) {
for (var i = 0, len = users.length; i < len; i++) {
var user = users[i];
if (user.sub === id) {
log.info('Found user: ', user);
return fn(null, user);
}
}
return fn(null, null);
};
var oidcStrategy = new OIDCBearerStrategy(options,
function(token, done) {
log.info('verifying hello user');
log.info(token, 'was hello token retrieved');
findById(token.sub, function(err, user) {
if (err) {
return done(err);
}
if (!user) {
// "Auto-registration"
log.info('User was added automatically, because they were new. Their sub is: ', token.sub);
users.push(token);
owner = token.sub;
return done(null, token);
}
owner = token.sub;
return done(null, user, token);
});
}
);
passport.use(oidcStrategy);
```

<span data-ttu-id="8e45f-296">Passport usa un patrón similar para todas sus estrategias (Twitter, Facebook, etc.).</span><span class="sxs-lookup"><span data-stu-id="8e45f-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="8e45f-297">Todos los escritores de estrategia cumplen toohello patrón.</span><span class="sxs-lookup"><span data-stu-id="8e45f-297">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="8e45f-298">Pasar la estrategia de hello un `function()` que usa un token y `done` como parámetros.</span><span class="sxs-lookup"><span data-stu-id="8e45f-298">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="8e45f-299">estrategia de Hola se devuelve cuando hace todo su trabajo.</span><span class="sxs-lookup"><span data-stu-id="8e45f-299">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="8e45f-300">Almacenar usuario hello y token de hello complementario por lo que no necesita tooask para ella de nuevo.</span><span class="sxs-lookup"><span data-stu-id="8e45f-300">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e45f-301">Hello código anterior toma cualquier usuario que puede autenticar el servidor de tooyour.</span><span class="sxs-lookup"><span data-stu-id="8e45f-301">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="8e45f-302">Esto se conoce como registro automático.</span><span class="sxs-lookup"><span data-stu-id="8e45f-302">This is known as auto-registration.</span></span> <span data-ttu-id="8e45f-303">En un servidor de producción, desearía toolet cualquiera sin tener primero que les vaya a través de un proceso de registro que elija.</span><span class="sxs-lookup"><span data-stu-id="8e45f-303">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="8e45f-304">Se trata normalmente de patrón de Hola que se ven en las aplicaciones de consumidor.</span><span class="sxs-lookup"><span data-stu-id="8e45f-304">This is usually hello pattern you see in consumer apps.</span></span> <span data-ttu-id="8e45f-305">aplicación Hello podrían tooregister con Facebook, pero, a continuación, le pide que tooenter obtener información adicional.</span><span class="sxs-lookup"><span data-stu-id="8e45f-305">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="8e45f-306">Si no usa un programa de línea de comandos para este tutorial, podría extraer correo electrónico de Hola de objeto de símbolo (token) de Hola que se devuelve.</span><span class="sxs-lookup"><span data-stu-id="8e45f-306">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="8e45f-307">A continuación, podría solicitar información adicional de hello usuario tooenter.</span><span class="sxs-lookup"><span data-stu-id="8e45f-307">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="8e45f-308">Dado que se trata de un servidor de prueba, agregar usuario Hola directamente toohello en la memoria de base de datos.</span><span class="sxs-lookup"><span data-stu-id="8e45f-308">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="8e45f-309">Protección de los puntos de conexión</span><span class="sxs-lookup"><span data-stu-id="8e45f-309">Protect endpoints</span></span>
<span data-ttu-id="8e45f-310">Proteger los puntos de conexión mediante la especificación de hello **passport.authenticate()** llamada con protocolo de Hola que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="8e45f-310">Protect endpoints by specifying hello **passport.authenticate()** call with hello protocol that you want toouse.</span></span>

<span data-ttu-id="8e45f-311">Puede editar la ruta en el código del servidor para ver una opción más avanzada:</span><span class="sxs-lookup"><span data-stu-id="8e45f-311">You can edit your route in your server code for a more advanced option:</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="8e45f-312">18: Reejecución de la aplicación de servidor</span><span class="sxs-lookup"><span data-stu-id="8e45f-312">18: Run your server application again</span></span>
<span data-ttu-id="8e45f-313">Use nuevo curl toosee si tiene protección de OAuth 2.0 en los extremos.</span><span class="sxs-lookup"><span data-stu-id="8e45f-313">Use curl again toosee if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="8e45f-314">Haga esto antes de ejecutar cualquiera de nuestros SDK de cliente en este punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="8e45f-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="8e45f-315">encabezados de Hello devueltos deben indicar si la autenticación está funcionando correctamente.</span><span class="sxs-lookup"><span data-stu-id="8e45f-315">hello headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="8e45f-316">Asegúrese de que la instancia de MongoDB se esté ejecutando:</span><span class="sxs-lookup"><span data-stu-id="8e45f-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="8e45f-317">Cambiar toohello **organización** directorio y, a continuación, use curl:</span><span class="sxs-lookup"><span data-stu-id="8e45f-317">Change toohello **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="8e45f-318">Pruebe una operación POST básica:</span><span class="sxs-lookup"><span data-stu-id="8e45f-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="8e45f-319">Una respuesta 401 indica dicho nivel de Passport Hola está tratando de tooredirect toohello extremo authorize, que es exactamente lo que desea.</span><span class="sxs-lookup"><span data-stu-id="8e45f-319">A 401 response indicates that hello Passport layer is trying tooredirect toohello authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="8e45f-320">*Ahora tiene un servicio de API de REST que usa OAuth 2.0.*</span><span class="sxs-lookup"><span data-stu-id="8e45f-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="8e45f-321">Ha avanzado todo lo posible con este servidor sin usar un cliente compatible con OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="8e45f-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="8e45f-322">Para ello, deberá tooreview un tutorial adicional.</span><span class="sxs-lookup"><span data-stu-id="8e45f-322">For that, you will need tooreview an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e45f-323">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8e45f-323">Next steps</span></span>
<span data-ttu-id="8e45f-324">Como referencia, ejemplo de Hola finalizado (sin los valores de configuración) se proporciona como [un archivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="8e45f-324">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="8e45f-325">También puede clonarlo desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="8e45f-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="8e45f-326">Ahora, puede mover en toomore temas avanzados.</span><span class="sxs-lookup"><span data-stu-id="8e45f-326">Now, you can move on toomore advanced topics.</span></span> <span data-ttu-id="8e45f-327">Es recomendable tootry [proteger una aplicación web de Node.js con el punto de conexión de hello v2.0](active-directory-v2-devquickstarts-node-web.md).</span><span class="sxs-lookup"><span data-stu-id="8e45f-327">You might want tootry [Secure a Node.js web app using hello v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="8e45f-328">Estos son algunos recursos adicionales:</span><span class="sxs-lookup"><span data-stu-id="8e45f-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="8e45f-329">Guía del desarrollador de Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="8e45f-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="8e45f-330">Etiqueta "azure-active-directory" de Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="8e45f-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="8e45f-331">Obtención de actualizaciones de seguridad para nuestros productos</span><span class="sxs-lookup"><span data-stu-id="8e45f-331">Get security updates for our products</span></span>
<span data-ttu-id="8e45f-332">Recomendamos que toosign una toobe una notificación cuando se produzcan incidentes de seguridad.</span><span class="sxs-lookup"><span data-stu-id="8e45f-332">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="8e45f-333">En hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) página, subscribe tooSecurity avisos de alertas.</span><span class="sxs-lookup"><span data-stu-id="8e45f-333">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

