---
title: "Protección de una API web de Azure Active Directory 2.0 mediante Node.js | Microsoft Docs"
description: "En este artículo se describe cómo crear una API web de Node.js que acepta tokens de una cuenta Microsoft personal y de cuentas profesionales o educativas."
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
ms.openlocfilehash: 94e945a52b9df7c495de1611baa08083357670c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="4e0d7-103">Protección de una API web mediante Node.js</span><span class="sxs-lookup"><span data-stu-id="4e0d7-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="4e0d7-104">No todas las características y escenarios de Azure Active Directory son compatibles con la versión 2.0 del punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="4e0d7-105">Para determinar si debe usar la versión 2.0 o 1.0 del punto de conexión, obtenga información sobre las [limitaciones de esta versión](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="4e0d7-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="4e0d7-106">Cuando se utiliza el punto de conexión de la versión 2.0 de Azure Active Directory (Azure AD), puede usar tokens de acceso de [OAuth 2.0](active-directory-v2-protocols.md) para proteger su API web.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-106">When you use the Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens to protect your web API.</span></span> <span data-ttu-id="4e0d7-107">Con los tokens de OAuth 2.0, los usuarios que tienen una cuenta Microsoft personal, y cuentas profesionales o educativas, pueden acceder de forma segura a su API web.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="4e0d7-108">*Passport* es middleware de autenticación para Node.js.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="4e0d7-109">Passport, flexible y modular, se puede usar discretamente en cualquier aplicación web de Restify o basada en Express.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="4e0d7-110">En esta herramienta, un conjunto completo de estrategias admite la autenticación mediante nombre de usuario y contraseña, Facebook, Twitter y mucho más.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="4e0d7-111">Hemos desarrollado una estrategia para Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="4e0d7-112">En este artículo se muestra cómo instalar el módulo y luego agregar el complemento `passport-azure-ad` de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-112">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="4e0d7-113">Descargar</span><span class="sxs-lookup"><span data-stu-id="4e0d7-113">Download</span></span>
<span data-ttu-id="4e0d7-114">El código de este tutorial se conserva [en GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span><span class="sxs-lookup"><span data-stu-id="4e0d7-114">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="4e0d7-115">Para seguir el tutorial, puede [descargar el esqueleto de la aplicación como un archivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip) o clonar el esqueleto:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-115">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="4e0d7-116">La aplicación completa se ofrece al final de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-116">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="4e0d7-117">1: Registro de una aplicación</span><span class="sxs-lookup"><span data-stu-id="4e0d7-117">1: Register an app</span></span>
<span data-ttu-id="4e0d7-118">Cree una aplicación en [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o siga estos [pasos detallados](active-directory-v2-app-registration.md) para registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="4e0d7-119">Asegúrese de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-119">Make sure you:</span></span>

* <span data-ttu-id="4e0d7-120">Copie el **identificador de aplicación** asignado a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-120">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="4e0d7-121">Lo necesitará para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="4e0d7-122">Agregar la plataforma **Móvil** a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="4e0d7-123">Copie el **URI de redireccionamiento** del portal.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="4e0d7-124">Debe usar el valor del URI predeterminado de `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-124">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="4e0d7-125">2: Instalación de Node.js</span><span class="sxs-lookup"><span data-stu-id="4e0d7-125">2: Install Node.js</span></span>
<span data-ttu-id="4e0d7-126">Para utilizar el ejemplo en este tutorial, debe [instalar Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="4e0d7-126">To use the sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="4e0d7-127">3: Instalación de MongoDB</span><span class="sxs-lookup"><span data-stu-id="4e0d7-127">3: Install MongoDB</span></span>
<span data-ttu-id="4e0d7-128">Para usar correctamente este ejemplo, debe [instalar MongoDB](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="4e0d7-128">To successfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="4e0d7-129">En este ejemplo, se usa para que la API de REST sea persistente en las instancias del servidor.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-129">In this sample, you use MongoDB to make your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="4e0d7-130">En este artículo, se da por hecho que utiliza los puntos de conexión predeterminados de instalación y servidor para MongoDB: mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-130">In this article, we assume that you use the default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="4e0d7-131">4: Instalación de los módulos Restify en su API web</span><span class="sxs-lookup"><span data-stu-id="4e0d7-131">4: Install the restify modules in your web API</span></span>
<span data-ttu-id="4e0d7-132">Vamos a usar Restify para crear nuestra API de REST.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-132">We use Resitfy to build our REST API.</span></span> <span data-ttu-id="4e0d7-133">Restify es un marco de trabajo de la aplicación de Node.js mínimo y flexible que se deriva de Express.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="4e0d7-134">Restify tiene un conjunto robusto de características que puede usar para compilar las API de REST en Connect.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-134">Restify has a robust set of features that you can use to build REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="4e0d7-135">Instalación de Restify</span><span class="sxs-lookup"><span data-stu-id="4e0d7-135">Install restify</span></span>
1.  <span data-ttu-id="4e0d7-136">En el símbolo del sistema, cambie el directorio a **azuread**:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-136">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="4e0d7-137">Si el directorio **azuread** no existe, créelo:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-137">If the **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="4e0d7-138">Instale Restify:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="4e0d7-139">El resultado de este comando debe tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-139">The output of this command should look like this:</span></span>

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

#### <a name="did-you-get-an-error"></a><span data-ttu-id="4e0d7-140">¿Ha recibido un error?</span><span class="sxs-lookup"><span data-stu-id="4e0d7-140">Did you get an error?</span></span>
<span data-ttu-id="4e0d7-141">En algunos sistemas operativos, cuando se usa el comando `npm`, verá este mensaje: `Error: EPERM, chmod '/usr/local/bin/..'`.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-141">On some operating systems, when you use the `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="4e0d7-142">Además, una sugerencia de que trate de ejecutar la cuenta como administrador.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-142">The error is followed by a request that you try running the account as an administrator.</span></span> <span data-ttu-id="4e0d7-143">Si aparece este problema, utilice el comando `sudo` para ejecutar `npm` en un nivel de privilegio más elevado.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-143">If this occurs, use the command `sudo` to run `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-to-dtrace"></a><span data-ttu-id="4e0d7-144">¿Ha recibido un error relacionado con DTrace?</span><span class="sxs-lookup"><span data-stu-id="4e0d7-144">Did you get an error related to DTrace?</span></span>
<span data-ttu-id="4e0d7-145">Al instalar Restify, podría aparecer este mensaje:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-145">When you install restify, you might see this message:</span></span>

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

<span data-ttu-id="4e0d7-146">Restify proporciona un mecanismo eficaz para rastrear llamadas REST con DTrace.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-146">Restify has a powerful mechanism to trace REST calls by using DTrace.</span></span> <span data-ttu-id="4e0d7-147">Sin embargo, DTrace no está disponible en muchos sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="4e0d7-148">Puede omitir estos errores.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="4e0d7-149">Paso 5: Instalación de Passport.js en su API web</span><span class="sxs-lookup"><span data-stu-id="4e0d7-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="4e0d7-150">En el símbolo del sistema, cambie al directorio **azuread**.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-150">At the command prompt, change the directory to **azuread**.</span></span>

2.  <span data-ttu-id="4e0d7-151">Instale Passport.js:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="4e0d7-152">El resultado del comando anterior debe tener el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-152">The output of the command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="4e0d7-153">6: Incorporación de passport-azure-ad a su API web</span><span class="sxs-lookup"><span data-stu-id="4e0d7-153">6: Add passport-azure-ad to your web API</span></span>
<span data-ttu-id="4e0d7-154">Después, agregue la estrategia de OAuth usando passport-azuread.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-154">Next, add the OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="4e0d7-155">`passport-azuread` es un conjunto de estrategias que conectan Azure AD a Passport.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="4e0d7-156">En este ejemplo de API de REST, esta estrategia se usa para los tokens de portador.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="4e0d7-157">Aunque OAuth 2.0 proporciona un marco en el que se puede emitir cualquier tipo de token conocido, habitualmente se usan determinados tipos de token.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="4e0d7-158">Los tokens de portador se suelen utilizar para proteger los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-158">Bearer tokens are commonly used to protect endpoints.</span></span> <span data-ttu-id="4e0d7-159">Además, son el tipo de token más emitido en OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-159">Bearer tokens are the most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="4e0d7-160">Muchas implementaciones de OAuth 2.0 dan por hecho que los tokens de portador son el único tipo de token emitido.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-160">Many OAuth 2.0 implementations assume that bearer tokens are the only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="4e0d7-161">En el símbolo del sistema, cambie los directorios a **azuread**.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-161">At a command prompt, change the directory to **azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="4e0d7-162">Instale el módulo `passport-azure-ad` de Passport.js :</span><span class="sxs-lookup"><span data-stu-id="4e0d7-162">Install the Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="4e0d7-163">El resultado del comando anterior debe tener el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-163">The output of the command should look like this:</span></span>

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

## <a name="7-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="4e0d7-164">7: Incorporación de módulos MongoDB a su API web</span><span class="sxs-lookup"><span data-stu-id="4e0d7-164">7: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="4e0d7-165">En este ejemplo, utilizamos MongoDB como el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="4e0d7-166">Para ello, instale Mongoose, un complemento muy utilizado para administrar modelos y esquemas:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-166">Install Mongoose, a widely used plug-in, to manage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="4e0d7-167">Instale el controlador de base de datos para MongoDB (que también se denomina MongoDB):</span><span class="sxs-lookup"><span data-stu-id="4e0d7-167">Install the database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="4e0d7-168">8: Instalar módulos adicionales</span><span class="sxs-lookup"><span data-stu-id="4e0d7-168">8: Install additional modules</span></span>
<span data-ttu-id="4e0d7-169">Instale los demás módulos necesarios.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-169">Install the remaining required modules.</span></span>

1.  <span data-ttu-id="4e0d7-170">En el símbolo del sistema, cambie el directorio a **azuread**:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-170">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="4e0d7-171">Escriba los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-171">Enter the following commands.</span></span> <span data-ttu-id="4e0d7-172">Los comandos instalan los módulos siguientes en su directorio node_modules:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-172">The commands install the following modules in your node_modules directory:</span></span>

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

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="4e0d7-173">9: Creación de un archivo server.js con sus dependencias</span><span class="sxs-lookup"><span data-stu-id="4e0d7-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="4e0d7-174">El archivo Server.js proporciona la mayor parte de la funcionalidad de su servidor de API web.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-174">A Server.js file holds the majority of the functionality for your web API server.</span></span> <span data-ttu-id="4e0d7-175">La mayoría del código se agrega a este archivo.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-175">Add most of your code to this file.</span></span> <span data-ttu-id="4e0d7-176">Con fines de producción, puede rediseñar la funcionalidad para que estuviera en archivos más pequeños, como controladores y rutas independientes.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-176">For production purposes, you can refactor the functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="4e0d7-177">En este artículo, utilizamos Server.js para este fin.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="4e0d7-178">En el símbolo del sistema, cambie el directorio a **azuread**:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-178">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="4e0d7-179">Con el editor que prefiera, cree un archivo Server.js.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="4e0d7-180">Agregue la siguiente información al archivo:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-180">Add the following information to the file:</span></span>

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

3.  <span data-ttu-id="4e0d7-181">Guarde el archivo .</span><span class="sxs-lookup"><span data-stu-id="4e0d7-181">Save the file.</span></span> <span data-ttu-id="4e0d7-182">Volveremos a él en breve.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-182">You will return to it shortly.</span></span>

## <a name="10-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="4e0d7-183">10: Crear un archivo de configuración para almacenar la configuración de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e0d7-183">10: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="4e0d7-184">Este archivo de código pasa los parámetros de configuración del portal de Azure AD al archivo Passport.js.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-184">This code file passes the configuration parameters from your Azure AD portal to Passport.js.</span></span> <span data-ttu-id="4e0d7-185">Estos valores de configuración se crearon al agregar la API web al portal en la primera parte del artículo.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-185">You created these configuration values when you added the web API to the portal at the beginning of the article.</span></span> <span data-ttu-id="4e0d7-186">Explicamos qué incluir en los valores de estos parámetros después de haber copiado el código.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-186">After you copy the code, we'll explain what to put in the values of these parameters.</span></span>

1.  <span data-ttu-id="4e0d7-187">En el símbolo del sistema, cambie el directorio a **azuread**:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-187">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="4e0d7-188">En un editor, cree un archivo Config.js.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="4e0d7-189">Agregue la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-189">Add the following information:</span></span>

    ```Javascript
    // Don't commit this file to your public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need to change this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="4e0d7-190">Valores obligatorios</span><span class="sxs-lookup"><span data-stu-id="4e0d7-190">Required values</span></span>

*   <span data-ttu-id="4e0d7-191">**IdentityMetadata**: es donde `passport-azure-ad` buscará los datos de configuración del proveedor de identidades (IdP), así como las claves para validar los tokens JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="4e0d7-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for the identity provider (IDP) and the keys to validate the JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="4e0d7-192">Si utiliza Azure AD, probablemente no querrá cambiar esto.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-192">If you are using Azure AD, you probably don't want to change this.</span></span>

*   <span data-ttu-id="4e0d7-193">**audience**: el URI de redirección desde el portal.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-193">**audience**: Your redirect URI from the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="4e0d7-194">Distribuimos sus claves con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="4e0d7-195">Asegúrese de extraer siempre de la dirección URL "openid_keys" y de que la aplicación pueda tener acceso a Internet.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-195">Be sure that you always pull from the "openid_keys" URL, and that the app can access the Internet.</span></span>
> 
> 

## <a name="11-add-the-configuration-to-your-serverjs-file"></a><span data-ttu-id="4e0d7-196">11: Incorporación de configuración a su archivo Server.js</span><span class="sxs-lookup"><span data-stu-id="4e0d7-196">11: Add the configuration to your Server.js file</span></span>
<span data-ttu-id="4e0d7-197">La aplicación debe leer estos valores del archivo de configuración que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-197">Your application needs to read the values from the config file you just created.</span></span> <span data-ttu-id="4e0d7-198">Para ello, agregamos el archivo .config como un recurso necesario en su aplicación.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-198">Add the .config file as a required resource in your application.</span></span> <span data-ttu-id="4e0d7-199">Establezca las variables globales en las que se encuentran en Config.js.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-199">Set the global variables to those that are in Config.js.</span></span>

1.  <span data-ttu-id="4e0d7-200">En el símbolo del sistema, cambie el directorio **azuread**:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-200">At the command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="4e0d7-201">En un editor, abra Server.js.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-201">In an editor, open Server.js.</span></span> <span data-ttu-id="4e0d7-202">Agregue la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-202">Add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="4e0d7-203">Agregue una nueva sección a Server.js:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-203">Add a new section to Server.js:</span></span>

    ```Javascript
    // Pass these options in to the ODICBearerStrategy.
    var options = {
    // The URL of the metadata document for your app. Put the keys for token validation from the URL found in the jwks_uri tag in the metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array to hold signed-in users and the current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="4e0d7-204">12: Incorporación del modelo MongoDB y la información del esquema mediante Mongoose</span><span class="sxs-lookup"><span data-stu-id="4e0d7-204">12: Add the MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="4e0d7-205">Después, conecte estos tres archivos en un servicio de API de REST.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="4e0d7-206">En este artículo, utilizamos MongoDB para almacenar las tareas.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-206">In this article, we use MongoDB to store our tasks.</span></span> <span data-ttu-id="4e0d7-207">Se explican en el *paso 4*.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="4e0d7-208">En el archivo Config.js creado en el paso 11, la base de datos se llama *tasklist*.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-208">In the Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="4e0d7-209">Eso es lo que colocaría al final de la dirección URL de conexión de mongoose_auth_local.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-209">That was what you put at the end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="4e0d7-210">No es necesario crear esta base de datos por anticipado en MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-210">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="4e0d7-211">La base de datos se crea en la primera ejecución de la aplicación de servidor (dando por hecho que la base de datos ya no existe).</span><span class="sxs-lookup"><span data-stu-id="4e0d7-211">The database is created on the first run of your server application (assuming the database does not already exist).</span></span>

<span data-ttu-id="4e0d7-212">Indicó al servidor qué base de datos de MongoDB usar.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-212">You've told the server what MongoDB database to use.</span></span> <span data-ttu-id="4e0d7-213">Después, tiene que escribir código adicional para crear el modelo y el esquema para las tareas de su servidor.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-213">Next, you need to write some additional code to create the model and schema for your server's tasks.</span></span>

### <a name="the-model"></a><span data-ttu-id="4e0d7-214">El modelo</span><span class="sxs-lookup"><span data-stu-id="4e0d7-214">The model</span></span>
<span data-ttu-id="4e0d7-215">El modelo de esquema es muy básico.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-215">The schema model is very basic.</span></span> <span data-ttu-id="4e0d7-216">Puede expandirlo si lo necesita.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="4e0d7-217">El modelo de esquema tiene estos valores:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-217">The schema model has these values:</span></span>

*   <span data-ttu-id="4e0d7-218">**NAME**.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-218">**NAME**.</span></span> <span data-ttu-id="4e0d7-219">La persona a quien se ha asignado la tarea.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-219">The person assigned to the task.</span></span> <span data-ttu-id="4e0d7-220">Se trata de un valor de **cadena**.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-220">This is a **string** value.</span></span>
*   <span data-ttu-id="4e0d7-221">**TASK**.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-221">**TASK**.</span></span> <span data-ttu-id="4e0d7-222">El nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-222">The name of the task.</span></span> <span data-ttu-id="4e0d7-223">Se trata de un valor de **cadena**.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-223">This is a **string** value.</span></span>
*   <span data-ttu-id="4e0d7-224">**DATE**.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-224">**DATE**.</span></span> <span data-ttu-id="4e0d7-225">La fecha en que vence la tarea.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-225">The date that the task is due.</span></span> <span data-ttu-id="4e0d7-226">Se trata de un **datetime** valor.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="4e0d7-227">**COMPLETED**.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-227">**COMPLETED**.</span></span> <span data-ttu-id="4e0d7-228">Si se ha completado la tarea.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-228">Whether the task is completed.</span></span> <span data-ttu-id="4e0d7-229">Se trata de un elemento **booleano**.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-229">This is a **Boolean** value.</span></span>

### <a name="create-the-schema-in-the-code"></a><span data-ttu-id="4e0d7-230">Creación del esquema en el código</span><span class="sxs-lookup"><span data-stu-id="4e0d7-230">Create the schema in the code</span></span>
1.  <span data-ttu-id="4e0d7-231">En el símbolo del sistema, cambie el directorio a **azuread**:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-231">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="4e0d7-232">En el editor, abra Server.js.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-232">In your editor, open Server.js.</span></span> <span data-ttu-id="4e0d7-233">Agregue la siguiente información debajo de la entrada de configuración:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-233">Below the configuration entry, add the following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="4e0d7-234">Este código se conecta al servidor de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-234">This code connects to the MongoDB server.</span></span> <span data-ttu-id="4e0d7-235">También devuelve un objeto de esquema.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-235">It also returns a schema object.</span></span>

#### <a name="using-the-schema-create-your-model-in-the-code"></a><span data-ttu-id="4e0d7-236">Con el esquema, cree el modelo en el código.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-236">Using the schema, create your model in the code</span></span>
<span data-ttu-id="4e0d7-237">En el código anterior, agregue el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-237">Below the preceding code, add the following code:</span></span>

```Javascript
// Create a basic schema to store your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use the schema to register a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="4e0d7-238">Como puede imaginar por el código, primero creará un esquema.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-238">As you can tell from the code, first you create your schema.</span></span> <span data-ttu-id="4e0d7-239">Después, un objeto de modelo.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-239">Next, you create a model object.</span></span> <span data-ttu-id="4e0d7-240">Usará el objeto de modelo para almacenar los datos en todo el código cuando defina las **rutas**.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-240">You use the model object to store your data throughout the code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="4e0d7-241">13: Incorporación de las rutas para el servidor de API de REST de su tarea</span><span class="sxs-lookup"><span data-stu-id="4e0d7-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="4e0d7-242">Ahora que tiene un modelo de base de datos con el que trabajar, agregue las rutas que usará para el servidor de API de REST.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-242">Now that you have a database model to work with, add the routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="4e0d7-243">Información de las rutas en Restify</span><span class="sxs-lookup"><span data-stu-id="4e0d7-243">About routes in restify</span></span>
<span data-ttu-id="4e0d7-244">Las rutas de Restify funcionan exactamente del mismo modo que cuando se usa la pila de Express.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-244">Routes in restify work exactly the same way they do when you use the Express stack.</span></span> <span data-ttu-id="4e0d7-245">Defina rutas mediante el URI al que espera que llamen las aplicaciones cliente.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-245">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="4e0d7-246">Normalmente, las rutas se definen en un archivo independiente.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="4e0d7-247">En este tutorial, colocamos nuestra rutas en Server.js.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="4e0d7-248">Se recomienda diseñarlas en su propio archivo para que se puedan usar en producción.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="4e0d7-249">Un patrón típico de una ruta Restify es:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep the server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="4e0d7-250">Este es el patrón en su nivel más básico.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-250">This is the pattern at the most basic level.</span></span> <span data-ttu-id="4e0d7-251">Restify (y Express) proporcionan una funcionalidad mucho más profunda, como definir los tipos de aplicación y proporcionar un enrutamiento complejo en distintos puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-251">Restify (and Express) provide much deeper functionality, like the ability to define application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-to-your-server"></a><span data-ttu-id="4e0d7-252">Incorporación de rutas predeterminadas al servidor</span><span class="sxs-lookup"><span data-stu-id="4e0d7-252">Add default routes to your server</span></span>
<span data-ttu-id="4e0d7-253">Agregue las rutas CRUD básicas: **create**, **retrieve**, **update** y **delete**.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-253">Add the basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="4e0d7-254">En el símbolo del sistema, cambie el directorio a **azuread**:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-254">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="4e0d7-255">En un editor, abra Server.js.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-255">In an editor, open Server.js.</span></span> <span data-ttu-id="4e0d7-256">Debajo de las entradas de la base de datos que creó anteriormente, agregue la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-256">Below the database entries you made earlier, add the following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow you to use MongoDB Server as your response to any origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it to MongoDB.
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
    req.log.warn(err, 'createTask: unable to save');
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
    'removeTask: unable to delete %s',
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
    req.log.warn(err, 'get: unable to read %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns the list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow us to use MongoDB Server as our response to any origin.
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
    log.warn(err, "There are no tasks in the database. Add one!");
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

### <a name="add-error-handling-for-the-routes"></a><span data-ttu-id="4e0d7-257">Incorporación del control de errores para las rutas</span><span class="sxs-lookup"><span data-stu-id="4e0d7-257">Add error handling for the routes</span></span>
<span data-ttu-id="4e0d7-258">Agregue algunos controles de errores de forma que pueda comunicar al cliente el problema que se ha producido.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-258">Add some error handling so you can communicate back to the client about the problem you encountered.</span></span>

<span data-ttu-id="4e0d7-259">Agregue el código siguiente debajo del código, que ya ha escrito:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-259">Add the following code below the code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back to the client.
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


## <a name="14-create-your-server"></a><span data-ttu-id="4e0d7-260">14: Creación del servidor</span><span class="sxs-lookup"><span data-stu-id="4e0d7-260">14: Create your server</span></span>
<span data-ttu-id="4e0d7-261">La última tarea consiste en agregar la instancia del servidor.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-261">The last thing to do is to add your server instance.</span></span> <span data-ttu-id="4e0d7-262">La instancia del servidor administra las llamadas.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-262">The server instance manages your calls.</span></span>

<span data-ttu-id="4e0d7-263">Restify (y Express) tiene una personalización más avanzada que puede usar con un servidor de API de REST.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="4e0d7-264">En este tutorial, usaremos la configuración más básica.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-264">In this tutorial, we use the most basic setup.</span></span>

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
// Allow 5 requests/second by IP address, and burst to 10.
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
## <a name="15-add-the-routes-without-authentication-for-now"></a><span data-ttu-id="4e0d7-265">15: Incorporación de las rutas (sin autenticación por ahora)</span><span class="sxs-lookup"><span data-stu-id="4e0d7-265">15: Add the routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD to add the real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in the pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need to maintain session state. You can experiment with removing API protection.
/* To do this, remove the passport.authenticate() method:
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
consoleMessage += '\n Open your browser to %s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-the-server"></a><span data-ttu-id="4e0d7-266">16: Ejecución del servidor</span><span class="sxs-lookup"><span data-stu-id="4e0d7-266">16: Run the server</span></span>
<span data-ttu-id="4e0d7-267">Se recomienda probar el servidor antes de agregar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-267">It's a good idea to test your server before you add authentication.</span></span>

<span data-ttu-id="4e0d7-268">La forma más fácil de hacerlo es usando curl en una línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-268">The easiest way to test your server is by using curl at a command prompt.</span></span> <span data-ttu-id="4e0d7-269">Para ello, necesita una utilidad simple que pueda usar para analizar el resultado como JSON.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-269">To do this, you need a simple utility that you can use to parse output as JSON.</span></span> 

1.  <span data-ttu-id="4e0d7-270">Instale la herramienta JSON que usaremos en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-270">Install the JSON tool that we use in the following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="4e0d7-271">De esta forma, se instala la herramienta JSON globalmente.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-271">This installs the JSON tool globally.</span></span>

2.  <span data-ttu-id="4e0d7-272">Asegúrese de que la instancia de MongoDB se esté ejecutando:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="4e0d7-273">Cambie el directorio a **azuread** y después ejecute curl:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-273">Change the directory to **azuread**, and then run curl:</span></span>

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

4.  <span data-ttu-id="4e0d7-274">Para agregar una tarea, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-274">To add a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="4e0d7-275">La respuesta debe ser:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-275">The response should be:</span></span>

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

5.  <span data-ttu-id="4e0d7-276">Lista de tareas de Brandon:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="4e0d7-277">Si todos estos comandos se ejecutan sin errores, está listo para agregar OAuth al servidor de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-277">If all these commands run without errors, you are ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="4e0d7-278">*Ahora tiene un servidor de API de REST con MongoDB.*</span><span class="sxs-lookup"><span data-stu-id="4e0d7-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-to-your-rest-api-server"></a><span data-ttu-id="4e0d7-279">17: Incorporación de autenticación al servidor de API de REST</span><span class="sxs-lookup"><span data-stu-id="4e0d7-279">17: Add authentication to your REST API server</span></span>
<span data-ttu-id="4e0d7-280">Ahora que tiene una API de REST de ejecución, configurarlo para usar con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-280">Now that you have a running REST API, set it up to use it with Azure AD.</span></span>

<span data-ttu-id="4e0d7-281">En el símbolo del sistema, cambie el directorio a **azuread**:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-281">At a command prompt, change the directory to **azuread**:</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="4e0d7-282">Uso del elemento oidcbearerstrategy que se incluye con passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="4e0d7-282">Use the oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="4e0d7-283">Hasta ahora hemos creado un servidor típico de TODO de REST sin ningún tipo de autorización.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="4e0d7-284">Ahora, agregue la autenticación.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-284">Now, add authentication.</span></span>

<span data-ttu-id="4e0d7-285">En primer lugar, indique que quiere usar Passport.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-285">First,  indicate that you want to use Passport.</span></span> <span data-ttu-id="4e0d7-286">Incluya esto justo después de la configuración del servidor anterior:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="4e0d7-287">Al escribir las API, se recomienda vincular los datos a un elemento único del token cuya identidad el usuario no pueda suplantar.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-287">When you write APIs, it's a good idea to always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="4e0d7-288">Cuando este servidor almacena elementos TODO, los guarda en función del identificador de suscripción del usuario en el token (llamado a través de token.sub),</span><span class="sxs-lookup"><span data-stu-id="4e0d7-288">When this server stores TODO items, it stores them based on the user subscription ID in the token (called through token.sub).</span></span> <span data-ttu-id="4e0d7-289">que se coloca en el campo "owner".</span><span class="sxs-lookup"><span data-stu-id="4e0d7-289">You put the token.sub in the “owner” field.</span></span> <span data-ttu-id="4e0d7-290">Esto garantiza que ese usuario sea el único que puede acceder a sus tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-290">This ensures that only that user can access the user's TODOs.</span></span> <span data-ttu-id="4e0d7-291">Nadie más puede tener acceso a las tareas pendientes que se especificaron.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-291">No one else can access the TODOs that were entered.</span></span> <span data-ttu-id="4e0d7-292">No hay ninguna exposición en la API para el "propietario".</span><span class="sxs-lookup"><span data-stu-id="4e0d7-292">There is no exposure in the API for “owner.”</span></span> <span data-ttu-id="4e0d7-293">Un usuario externo puede solicitar las tareas pendientes de otros usuarios, incluso si estos se autentican.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="4e0d7-294">Después, vamos a usar la estrategia de portador de OpenID Connect que se incluye con `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-294">Next, use the Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="4e0d7-295">Colóquela después de lo que pegó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling the OIDCBearerStrategy and managing users.
/*
/* Because of the Passport pattern, you need to manage users and info tokens
/* with a FindorCreate() method. The method must be provided by the implementor.
/* In the following code, you autoregister any user and implement a FindById().
/* It's a good idea to do something more advanced.
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
log.info('verifying the user');
log.info(token, 'was the token retrieved');
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

<span data-ttu-id="4e0d7-296">Passport usa un patrón similar para todas sus estrategias (Twitter, Facebook, etc.)</span><span class="sxs-lookup"><span data-stu-id="4e0d7-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="4e0d7-297">Todos los escritores de estrategias se ajustan a este patrón.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-297">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="4e0d7-298">Pase a la estrategia una función `function()` que use un token y `done` como parámetros.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-298">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="4e0d7-299">La estrategia se devuelve cuando hace todo su trabajo.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-299">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="4e0d7-300">Almacene el usuario y guarde provisionalmente el token para no tener que volver a solicitarlo.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-300">Store the user and stash the token so you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e0d7-301">El código anterior adopta cualquier usuario que pueda autenticarse en el servidor.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-301">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="4e0d7-302">Esto se conoce como registro automático.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-302">This is known as auto-registration.</span></span> <span data-ttu-id="4e0d7-303">En un servidores de producción, no debería permitir que acceda cualquier usuario sin que antes pase por el proceso de registro que decida.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-303">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="4e0d7-304">Esto suele ser el patrón que se ven en las aplicaciones para consumidores.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-304">This is usually the pattern you see in consumer apps.</span></span> <span data-ttu-id="4e0d7-305">La aplicación podría permitir que se registre con Facebook, pero, luego, le pide que escriba información adicional.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-305">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="4e0d7-306">Si no usa un programa de línea de comandos para este tutorial, podría extraer el correo electrónico del objeto de token que se devuelve.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-306">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="4e0d7-307">Luego, puede pedir al usuario que escriba información adicional.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-307">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="4e0d7-308">Puesto que se trata de un servidor de prueba, agregará el usuario directamente a la base de datos en memoria.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-308">Because this is a test server, you add the user directly to the in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="4e0d7-309">Protección de los puntos de conexión</span><span class="sxs-lookup"><span data-stu-id="4e0d7-309">Protect endpoints</span></span>
<span data-ttu-id="4e0d7-310">Proteja los puntos de conexión mediante la especificación de la llamada **passport.authenticate()** con el protocolo que desea usar.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-310">Protect endpoints by specifying the **passport.authenticate()** call with the protocol that you want to use.</span></span>

<span data-ttu-id="4e0d7-311">Puede editar la ruta en el código del servidor para ver una opción más avanzada:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-311">You can edit your route in your server code for a more advanced option:</span></span>

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

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="4e0d7-312">18: Reejecución de la aplicación de servidor</span><span class="sxs-lookup"><span data-stu-id="4e0d7-312">18: Run your server application again</span></span>
<span data-ttu-id="4e0d7-313">Use curl para ver si ahora tiene la protección de OAuth 2.0 en los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-313">Use curl again to see if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="4e0d7-314">Haga esto antes de ejecutar cualquiera de nuestros SDK de cliente en este punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="4e0d7-315">Los encabezados devueltos deben indicar si la autenticación está funcionando correctamente.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-315">The headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="4e0d7-316">Asegúrese de que la instancia de MongoDB se esté ejecutando:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="4e0d7-317">Cambie al directorio **azuread** y, luego, use curl:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-317">Change to the **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="4e0d7-318">Pruebe una operación POST básica:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="4e0d7-319">Una respuesta 401 indica que la capa de Passport intenta realizar la redirección al punto de conexión autorizado, que es exactamente lo que desea.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-319">A 401 response indicates that the Passport layer is trying to redirect to the authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="4e0d7-320">*Ahora tiene un servicio de API de REST que usa OAuth 2.0.*</span><span class="sxs-lookup"><span data-stu-id="4e0d7-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="4e0d7-321">Ha avanzado todo lo posible con este servidor sin usar un cliente compatible con OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="4e0d7-322">Para ello, debe revisar un tutorial adicional.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-322">For that, you will need to review an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e0d7-323">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4e0d7-323">Next steps</span></span>
<span data-ttu-id="4e0d7-324">Como referencia, se ofrece el ejemplo completado (sin sus valores de configuración) [en forma de archivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="4e0d7-324">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="4e0d7-325">También puede clonarlo desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="4e0d7-326">Ahora puede pasar a temas más avanzados.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-326">Now, you can move on to more advanced topics.</span></span> <span data-ttu-id="4e0d7-327">Podría probar este: [Proteger una aplicación web de Node.js con el punto de conexión v2.0](active-directory-v2-devquickstarts-node-web.md).</span><span class="sxs-lookup"><span data-stu-id="4e0d7-327">You might want to try [Secure a Node.js web app using the v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="4e0d7-328">Estas son algunos recursos adicionales:</span><span class="sxs-lookup"><span data-stu-id="4e0d7-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="4e0d7-329">Guía del desarrollador de Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="4e0d7-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="4e0d7-330">Etiqueta "azure-active-directory" de Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="4e0d7-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="4e0d7-331">Obtención de actualizaciones de seguridad para nuestros productos</span><span class="sxs-lookup"><span data-stu-id="4e0d7-331">Get security updates for our products</span></span>
<span data-ttu-id="4e0d7-332">Le recomendamos suscribirse para recibir una notificación cuando se produzcan incidentes de seguridad.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-332">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="4e0d7-333">En la página [Notificaciones técnicas de seguridad de Microsoft](https://technet.microsoft.com/security/dd252948), suscríbase a las alertas de documentos informativos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="4e0d7-333">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

