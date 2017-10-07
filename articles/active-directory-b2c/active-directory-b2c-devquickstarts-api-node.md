---
title: "Azure AD B2C: Protección de una API web mediante Node.js | Microsoft Docs"
description: "Cómo toobuild una Node.js web API que acepta los tokens de un inquilino B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="50a1a-103">Azure AD B2C: Protección de una API web mediante Node.js</span><span class="sxs-lookup"><span data-stu-id="50a1a-103">Azure AD B2C: Secure a web API by using Node.js</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="50a1a-104">Con Azure Active Directory (Azure AD) B2C, puede proteger una API web mediante el uso de tokens de acceso de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="50a1a-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="50a1a-105">Estos tokens permiten que las aplicaciones cliente que usan API de Azure AD B2C tooauthenticate toohello.</span><span class="sxs-lookup"><span data-stu-id="50a1a-105">These tokens allow your client apps that use Azure AD B2C tooauthenticate toohello API.</span></span> <span data-ttu-id="50a1a-106">Este artículo muestra cómo toocreate una API "lista de tareas pendientes" permite a los usuarios tooadd y lista de tareas.</span><span class="sxs-lookup"><span data-stu-id="50a1a-106">This article shows you how toocreate a "to-do list" API that allows users tooadd and list tasks.</span></span> <span data-ttu-id="50a1a-107">Hola web API se protege mediante Azure AD B2C y solo permite a los usuarios autenticados toomanage su lista de tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="50a1a-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

> [!NOTE]
> <span data-ttu-id="50a1a-108">En este ejemplo se escribió toobe conectado tooby utilizando nuestro [aplicación de ejemplo de iOS B2C](active-directory-b2c-devquickstarts-ios.md).</span><span class="sxs-lookup"><span data-stu-id="50a1a-108">This sample was written toobe connected tooby using our [iOS B2C sample application](active-directory-b2c-devquickstarts-ios.md).</span></span> <span data-ttu-id="50a1a-109">Hola tutorial actual en primer lugar y, a continuación, seguir el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="50a1a-109">Do hello current walk-through first, and then follow along with that sample.</span></span>
>
>

<span data-ttu-id="50a1a-110">**Passport** es middleware de autenticación para Node.js.</span><span class="sxs-lookup"><span data-stu-id="50a1a-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="50a1a-111">Passport es flexible y modular, y se puede instalar discretamente en cualquier aplicación web basada en Express o Restify.</span><span class="sxs-lookup"><span data-stu-id="50a1a-111">Flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="50a1a-112">Un conjunto completo de estrategias admite la autenticación mediante un nombre de usuario y contraseña, Facebook, Twitter, etc.</span><span class="sxs-lookup"><span data-stu-id="50a1a-112">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="50a1a-113">Hemos desarrollado una estrategia para Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="50a1a-113">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="50a1a-114">Instalar este módulo y, a continuación, agregar hello Azure AD `passport-azure-ad` complemento.</span><span class="sxs-lookup"><span data-stu-id="50a1a-114">You install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="50a1a-115">toodo en este ejemplo, necesita:</span><span class="sxs-lookup"><span data-stu-id="50a1a-115">toodo this sample, you need to:</span></span>

1. <span data-ttu-id="50a1a-116">Registrar una aplicación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50a1a-116">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="50a1a-117">Configurar la aplicación toouse Passport `azure-ad-passport` complemento.</span><span class="sxs-lookup"><span data-stu-id="50a1a-117">Set up your application toouse Passport's `azure-ad-passport` plug-in.</span></span>
3. <span data-ttu-id="50a1a-118">Configurar un cliente aplicación toocall Hola "lista de tareas pendientes" API web.</span><span class="sxs-lookup"><span data-stu-id="50a1a-118">Configure a client application toocall hello "to-do list" web API.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="50a1a-119">Obtener un directorio de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="50a1a-119">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="50a1a-120">Para poder usar Azure AD B2C, debe crear un directorio o inquilino.</span><span class="sxs-lookup"><span data-stu-id="50a1a-120">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="50a1a-121">Un directorio es un contenedor de todos los usuarios, aplicaciones, grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="50a1a-121">A directory is a container for all users, apps, groups, and more.</span></span>  <span data-ttu-id="50a1a-122">Antes de continuar, si no tiene un directorio B2C, [créelo](active-directory-b2c-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="50a1a-122">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="50a1a-123">Creación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="50a1a-123">Create an application</span></span>
<span data-ttu-id="50a1a-124">A continuación, debe toocreate una aplicación en el directorio B2C que ofrece cierta información que necesita toosecurely de Azure AD comunicarse con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="50a1a-124">Next, you need toocreate an app in your B2C directory that gives Azure AD some information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="50a1a-125">En este caso, aplicación de cliente de hello y API web se representan mediante una sola **Id. de aplicación**, porque están formadas por una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="50a1a-125">In this case, both hello client app and web API are represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="50a1a-126">toocreate una aplicación, siga [estas instrucciones](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="50a1a-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="50a1a-127">Asegúrese de:</span><span class="sxs-lookup"><span data-stu-id="50a1a-127">Be sure to:</span></span>

* <span data-ttu-id="50a1a-128">Incluir un **web de aplicación web o api** en aplicación hello</span><span class="sxs-lookup"><span data-stu-id="50a1a-128">Include a **web app/web api** in hello application</span></span>
* <span data-ttu-id="50a1a-129">Escribir `http://localhost/TodoListService` como **Dirección URL de respuesta**.</span><span class="sxs-lookup"><span data-stu-id="50a1a-129">Enter `http://localhost/TodoListService` as a **Reply URL**.</span></span> <span data-ttu-id="50a1a-130">Es dirección URL predeterminada de Hola para este ejemplo de código.</span><span class="sxs-lookup"><span data-stu-id="50a1a-130">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="50a1a-131">Crear un **secreto de aplicación** para la aplicación y copiarlo.</span><span class="sxs-lookup"><span data-stu-id="50a1a-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="50a1a-132">Estos datos se necesitarán más adelante.</span><span class="sxs-lookup"><span data-stu-id="50a1a-132">You need this data later.</span></span> <span data-ttu-id="50a1a-133">Tenga en cuenta que este valor debe toobe [XML escape](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) antes de utilizarla.</span><span class="sxs-lookup"><span data-stu-id="50a1a-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
* <span data-ttu-id="50a1a-134">Hola copia **Id. de aplicación** decir tooyour asignado aplicación.</span><span class="sxs-lookup"><span data-stu-id="50a1a-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="50a1a-135">Estos datos se necesitarán más adelante.</span><span class="sxs-lookup"><span data-stu-id="50a1a-135">You need this data later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="50a1a-136">Crear sus directivas</span><span class="sxs-lookup"><span data-stu-id="50a1a-136">Create your policies</span></span>
<span data-ttu-id="50a1a-137">En Azure AD B2C, cada experiencia del usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="50a1a-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="50a1a-138">Esta aplicación contiene dos experiencias de identidad: registrarse e iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="50a1a-138">This app contains two identity experiences: sign up and sign in.</span></span> <span data-ttu-id="50a1a-139">Deberá toocreate una directiva de cada tipo, tal y como se describe en el [artículo de referencia de directiva](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="50a1a-139">You need toocreate one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>  <span data-ttu-id="50a1a-140">Cuando cree las tres directivas, asegúrese de:</span><span class="sxs-lookup"><span data-stu-id="50a1a-140">When you create your three policies, be sure to:</span></span>

* <span data-ttu-id="50a1a-141">Elija hello **nombre para mostrar** y otros atributos de inicio de sesión en la directiva de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="50a1a-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="50a1a-142">Elija hello **nombre para mostrar** y **Id. de objeto** notificaciones de la aplicación en cada directiva.</span><span class="sxs-lookup"><span data-stu-id="50a1a-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span>  <span data-ttu-id="50a1a-143">Puede elegir también otras notificaciones.</span><span class="sxs-lookup"><span data-stu-id="50a1a-143">You can choose other claims as well.</span></span>
* <span data-ttu-id="50a1a-144">Copia hacia abajo hello **nombre** de cada directiva después de haberlo creado.</span><span class="sxs-lookup"><span data-stu-id="50a1a-144">Copy down hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="50a1a-145">Deberían tener el prefijo de hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="50a1a-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="50a1a-146">Los nombres de directiva se necesitarán más adelante.</span><span class="sxs-lookup"><span data-stu-id="50a1a-146">You need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="50a1a-147">Una vez haya creado las tres directivas, está listo toobuild la aplicación.</span><span class="sxs-lookup"><span data-stu-id="50a1a-147">After you have created your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="50a1a-148">toolearn acerca de cómo funcionan las directivas en Azure AD B2C, comience con hello [.NET web app tutorial de introducción](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="50a1a-148">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="50a1a-149">Descargar código de hello</span><span class="sxs-lookup"><span data-stu-id="50a1a-149">Download hello code</span></span>
<span data-ttu-id="50a1a-150">Hola código para este tutorial [se mantiene en GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="50a1a-150">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span></span> <span data-ttu-id="50a1a-151">ejemplo de Hola a toobuild que vaya, también puede [descargar un proyecto como un archivo .zip esqueleto](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="50a1a-151">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="50a1a-152">También puede clonar el esqueleto de hello:</span><span class="sxs-lookup"><span data-stu-id="50a1a-152">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

<span data-ttu-id="50a1a-153">aplicación Hello completado también es [disponible como un archivo .zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) o en hello `complete` rama de hello mismo repositorio.</span><span class="sxs-lookup"><span data-stu-id="50a1a-153">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

## <a name="download-nodejs-for-your-platform"></a><span data-ttu-id="50a1a-154">Descarga de Node.js para su plataforma</span><span class="sxs-lookup"><span data-stu-id="50a1a-154">Download Node.js for your platform</span></span>
<span data-ttu-id="50a1a-155">toosuccessfully utilizar este ejemplo, se necesita una instalación activa de Node.js.</span><span class="sxs-lookup"><span data-stu-id="50a1a-155">toosuccessfully use this sample, you need a working installation of Node.js.</span></span>

<span data-ttu-id="50a1a-156">Instale Node.js desde [nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="50a1a-156">Install Node.js from [nodejs.org](http://nodejs.org).</span></span>

## <a name="install-mongodb-for-your-platform"></a><span data-ttu-id="50a1a-157">Instalación de MongoDB en la plataforma</span><span class="sxs-lookup"><span data-stu-id="50a1a-157">Install MongoDB for your platform</span></span>
<span data-ttu-id="50a1a-158">toosuccessfully utilizar este ejemplo, se necesita una instalación activa de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="50a1a-158">toosuccessfully use this sample, you need a working installation of MongoDB.</span></span> <span data-ttu-id="50a1a-159">Utilizamos MongoDB toomake la API de REST persistente en instancias del servidor.</span><span class="sxs-lookup"><span data-stu-id="50a1a-159">We use MongoDB toomake your REST API persistent across server instances.</span></span>

<span data-ttu-id="50a1a-160">Instale MongoDB desde [mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="50a1a-160">Install MongoDB from [mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="50a1a-161">Este tutorial se supone que utiliza Hola instalación y servidor de puntos de conexión predeterminados para MongoDB, lo cual en tiempo de presentación de redactar este artículo es `mongodb://localhost`.</span><span class="sxs-lookup"><span data-stu-id="50a1a-161">This walk-through assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is `mongodb://localhost`.</span></span>
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="50a1a-162">Instalar los módulos de Restify hello en la API web</span><span class="sxs-lookup"><span data-stu-id="50a1a-162">Install hello Restify modules in your web API</span></span>
<span data-ttu-id="50a1a-163">Utilizamos Restify toobuild su API de REST.</span><span class="sxs-lookup"><span data-stu-id="50a1a-163">We use Restify toobuild your REST API.</span></span> <span data-ttu-id="50a1a-164">Restify es un marco de aplicación de Node.js mínimo y flexible que deriva de Express.</span><span class="sxs-lookup"><span data-stu-id="50a1a-164">Restify is a minimal and flexible Node.js application framework derived from Express.</span></span> <span data-ttu-id="50a1a-165">Tiene un sólido conjunto de características para crear API de REST sobre Connect.</span><span class="sxs-lookup"><span data-stu-id="50a1a-165">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="50a1a-166">Instalar Restify</span><span class="sxs-lookup"><span data-stu-id="50a1a-166">Install Restify</span></span>
<span data-ttu-id="50a1a-167">Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`.</span><span class="sxs-lookup"><span data-stu-id="50a1a-167">From hello command line, change your directory too`azuread`.</span></span> <span data-ttu-id="50a1a-168">Si hello `azuread` directorio no existe, créelo.</span><span class="sxs-lookup"><span data-stu-id="50a1a-168">If hello `azuread` directory doesn't exist, create it.</span></span>

<span data-ttu-id="50a1a-169">`cd azuread` o `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="50a1a-169">`cd azuread` or `mkdir azuread;`</span></span>

<span data-ttu-id="50a1a-170">Escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="50a1a-170">Enter hello following command:</span></span>

`npm install restify`

<span data-ttu-id="50a1a-171">Este comando instala Restify.</span><span class="sxs-lookup"><span data-stu-id="50a1a-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="50a1a-172">¿Ha recibido un error?</span><span class="sxs-lookup"><span data-stu-id="50a1a-172">Did you get an error?</span></span>
<span data-ttu-id="50a1a-173">En algunos sistemas operativos, cuando se usa `npm`, puede recibir el error hello `Error: EPERM, chmod '/usr/local/bin/..'` y una solicitud que ejecutar la cuenta de hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="50a1a-173">In some operating systems, when you use `npm`, you may receive hello error `Error: EPERM, chmod '/usr/local/bin/..'` and a request that you run hello account as an administrator.</span></span> <span data-ttu-id="50a1a-174">Si se produce este problema, use hello `sudo` toorun comando `npm` con un nivel de privilegios superior.</span><span class="sxs-lookup"><span data-stu-id="50a1a-174">If this problem occurs, use hello `sudo` command toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-a-dtrace-error"></a><span data-ttu-id="50a1a-175">¿Recibió un error de DTrace?</span><span class="sxs-lookup"><span data-stu-id="50a1a-175">Did you get a DTrace error?</span></span>
<span data-ttu-id="50a1a-176">Al instalar Restify, puede ver algo parecido a esto:</span><span class="sxs-lookup"><span data-stu-id="50a1a-176">You may see something like this text when you install Restify:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
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

<span data-ttu-id="50a1a-177">Restify proporciona un mecanismo eficaz para rastrear llamadas a REST mediante DTrace.</span><span class="sxs-lookup"><span data-stu-id="50a1a-177">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="50a1a-178">Sin embargo, muchos sistemas operativos no tienen DTrace disponible.</span><span class="sxs-lookup"><span data-stu-id="50a1a-178">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="50a1a-179">Puede omitir estos errores con seguridad.</span><span class="sxs-lookup"><span data-stu-id="50a1a-179">You can safely ignore these errors.</span></span>

<span data-ttu-id="50a1a-180">salida de Hello de comando de Hola debe aparecer un texto similar toothis:</span><span class="sxs-lookup"><span data-stu-id="50a1a-180">hello output of hello command should appear similar toothis text:</span></span>

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
    └── bunyan@0.22.0 (mv@0.0.5)

## <a name="install-passport-in-your-web-api"></a><span data-ttu-id="50a1a-181">Instalación de Passport en la API web</span><span class="sxs-lookup"><span data-stu-id="50a1a-181">Install Passport in your web API</span></span>
<span data-ttu-id="50a1a-182">Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`, si aún no está allí.</span><span class="sxs-lookup"><span data-stu-id="50a1a-182">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="50a1a-183">Instalar mediante el siguiente comando de Hola de Passport:</span><span class="sxs-lookup"><span data-stu-id="50a1a-183">Install Passport using hello following command:</span></span>

`npm install passport`

<span data-ttu-id="50a1a-184">salida de Hello de comando de hello debe ser un texto similar toothis:</span><span class="sxs-lookup"><span data-stu-id="50a1a-184">hello output of hello command should be similar toothis text:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a><span data-ttu-id="50a1a-185">Agregar organización passport tooyour web API</span><span class="sxs-lookup"><span data-stu-id="50a1a-185">Add passport-azuread tooyour web API</span></span>
<span data-ttu-id="50a1a-186">A continuación, agregue la estrategia de OAuth de hello mediante el uso de `passport-azuread`, un conjunto de estrategias que se conectan a Azure AD con Passport.</span><span class="sxs-lookup"><span data-stu-id="50a1a-186">Next, add hello OAuth strategy by using `passport-azuread`, a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="50a1a-187">Utilice esta estrategia para los tokens de portador en el ejemplo de Hola a API de REST.</span><span class="sxs-lookup"><span data-stu-id="50a1a-187">Use this strategy for bearer tokens in hello REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="50a1a-188">Aunque OAuth2 proporciona un marco de trabajo en el que se puede emitir cualquier tipo de token conocido, solo ciertos tipos de token tienen un uso generalizado.</span><span class="sxs-lookup"><span data-stu-id="50a1a-188">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained widespread use.</span></span> <span data-ttu-id="50a1a-189">tokens de Hola para proteger los puntos de conexión son tokens de portador.</span><span class="sxs-lookup"><span data-stu-id="50a1a-189">hello tokens for protecting endpoints are bearer tokens.</span></span> <span data-ttu-id="50a1a-190">Estos tipos de tokens son Hola emitido más comúnmente en OAuth2.</span><span class="sxs-lookup"><span data-stu-id="50a1a-190">These types of tokens are hello most widely issued in OAuth2.</span></span> <span data-ttu-id="50a1a-191">Muchas implementaciones, se supone que los tokens de portador son Hola único tipo de token emitido.</span><span class="sxs-lookup"><span data-stu-id="50a1a-191">Many implementations assume that bearer tokens are hello only type of token issued.</span></span>
>
>

<span data-ttu-id="50a1a-192">Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`, si aún no está allí.</span><span class="sxs-lookup"><span data-stu-id="50a1a-192">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="50a1a-193">Instalar Hola Passport `passport-azure-ad` módulo mediante el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="50a1a-193">Install hello Passport `passport-azure-ad` module using hello following command:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="50a1a-194">salida de Hello de comando de hello debe ser un texto similar toothis:</span><span class="sxs-lookup"><span data-stu-id="50a1a-194">hello output of hello command should be similar toothis text:</span></span>

``
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
``

## <a name="add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="50a1a-195">Agregar MongoDB módulos tooyour web API</span><span class="sxs-lookup"><span data-stu-id="50a1a-195">Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="50a1a-196">En este ejemplo se MongoDB como almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="50a1a-196">This sample uses MongoDB as your data store.</span></span> <span data-ttu-id="50a1a-197">Para ello, instale Mongoose, un complemento para administrar modelos y esquemas muy utilizados.</span><span class="sxs-lookup"><span data-stu-id="50a1a-197">For that install Mongoose, a widely used plug-in for managing models and schemas.</span></span>

* `npm install mongoose`

## <a name="install-additional-modules"></a><span data-ttu-id="50a1a-198">Instalar módulos adicionales</span><span class="sxs-lookup"><span data-stu-id="50a1a-198">Install additional modules</span></span>
<span data-ttu-id="50a1a-199">A continuación, instale Hola restantes módulos necesarios.</span><span class="sxs-lookup"><span data-stu-id="50a1a-199">Next, install hello remaining required modules.</span></span>

<span data-ttu-id="50a1a-200">Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`, si aún no está:</span><span class="sxs-lookup"><span data-stu-id="50a1a-200">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="50a1a-201">Instalar los módulos de hello en su `node_modules` directorio:</span><span class="sxs-lookup"><span data-stu-id="50a1a-201">Install hello modules in your `node_modules` directory:</span></span>

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a><span data-ttu-id="50a1a-202">Creación de un archivo server.js con sus dependencias</span><span class="sxs-lookup"><span data-stu-id="50a1a-202">Create a server.js file with your dependencies</span></span>
<span data-ttu-id="50a1a-203">Hola `server.js` archivo proporciona mayoría Hola de funcionalidad de hello para el servidor de Web API.</span><span class="sxs-lookup"><span data-stu-id="50a1a-203">hello `server.js` file provides hello majority of hello functionality for your Web API server.</span></span>

<span data-ttu-id="50a1a-204">Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`, si aún no está:</span><span class="sxs-lookup"><span data-stu-id="50a1a-204">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="50a1a-205">Cree un archivo `server.js` en un editor.</span><span class="sxs-lookup"><span data-stu-id="50a1a-205">Create a `server.js` file in an editor.</span></span> <span data-ttu-id="50a1a-206">Agregue Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="50a1a-206">Add hello following information:</span></span>

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

<span data-ttu-id="50a1a-207">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="50a1a-207">Save hello file.</span></span> <span data-ttu-id="50a1a-208">Devolver tooit más tarde.</span><span class="sxs-lookup"><span data-stu-id="50a1a-208">You return tooit later.</span></span>

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="50a1a-209">Crear un toostore de archivo config.js la configuración de Azure AD</span><span class="sxs-lookup"><span data-stu-id="50a1a-209">Create a config.js file toostore your Azure AD settings</span></span>
<span data-ttu-id="50a1a-210">Este archivo de código pasa los parámetros de configuración de Hola desde el Portal de Azure AD toohello `Passport.js` archivo.</span><span class="sxs-lookup"><span data-stu-id="50a1a-210">This code file passes hello configuration parameters from your Azure AD Portal toohello `Passport.js` file.</span></span> <span data-ttu-id="50a1a-211">Estos valores de configuración se crean cuando se agrega hello web API toohello el portal en la primera parte del tutorial Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="50a1a-211">You created these configuration values when you added hello web API toohello portal in hello first part of hello walk-through.</span></span> <span data-ttu-id="50a1a-212">Se explica qué tooput en valores de hello de estos parámetros después de copiar el código de hello.</span><span class="sxs-lookup"><span data-stu-id="50a1a-212">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

<span data-ttu-id="50a1a-213">Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`, si aún no está:</span><span class="sxs-lookup"><span data-stu-id="50a1a-213">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="50a1a-214">Cree un archivo `config.js` en un editor.</span><span class="sxs-lookup"><span data-stu-id="50a1a-214">Create a `config.js` file in an editor.</span></span> <span data-ttu-id="50a1a-215">Agregue Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="50a1a-215">Add hello following information:</span></span>

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a><span data-ttu-id="50a1a-216">Valores obligatorios</span><span class="sxs-lookup"><span data-stu-id="50a1a-216">Required values</span></span>
<span data-ttu-id="50a1a-217">`clientID`: Hola Id. de cliente de la aplicación de API Web.</span><span class="sxs-lookup"><span data-stu-id="50a1a-217">`clientID`: hello client ID of your Web API application.</span></span>

<span data-ttu-id="50a1a-218">`IdentityMetadata`: Aquí es donde `passport-azure-ad` busca los datos de configuración para el proveedor de identidades de Hola.</span><span class="sxs-lookup"><span data-stu-id="50a1a-218">`IdentityMetadata`: This is where `passport-azure-ad` looks for your configuration data for hello identity provider.</span></span> <span data-ttu-id="50a1a-219">También busca los tokens de web JSON de hello claves toovalidate Hola.</span><span class="sxs-lookup"><span data-stu-id="50a1a-219">It also looks for hello keys toovalidate hello JSON web tokens.</span></span>

<span data-ttu-id="50a1a-220">`audience`: Hola el identificador uniforme de recursos (URI) del portal de Hola que identifica la aplicación que realiza la llamada.</span><span class="sxs-lookup"><span data-stu-id="50a1a-220">`audience`: hello uniform resource identifier (URI) from hello portal that identifies your calling application.</span></span>

<span data-ttu-id="50a1a-221">`tenantName`: su nombre de inquilino (por ejemplo, **contoso.onmicrosoft.com**).</span><span class="sxs-lookup"><span data-stu-id="50a1a-221">`tenantName`: Your tenant name (for example, **contoso.onmicrosoft.com**).</span></span>

<span data-ttu-id="50a1a-222">`policyName`: Hola directiva que desea que los tokens de hello toovalidate que entran en el servidor de tooyour.</span><span class="sxs-lookup"><span data-stu-id="50a1a-222">`policyName`: hello policy that you want toovalidate hello tokens coming in tooyour server.</span></span> <span data-ttu-id="50a1a-223">Esta directiva debe ser Hola la misma directiva que usa en la aplicación de cliente de Hola para inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="50a1a-223">This policy should be hello same policy that you use on hello client application for sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="50a1a-224">Por ahora, utilice Hola mismo directivas en el programa de instalación de cliente y servidor.</span><span class="sxs-lookup"><span data-stu-id="50a1a-224">For now, use hello same policies across both client and server setup.</span></span> <span data-ttu-id="50a1a-225">Si ya ha completado un tutorial y crear estas directivas, no necesita toodo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="50a1a-225">If you have already completed a walk-through and created these policies, you don't need toodo so again.</span></span> <span data-ttu-id="50a1a-226">Como completado el tutorial de hello, no es necesario tooset directivas nuevas para los tutoriales de cliente en el sitio de Hola.</span><span class="sxs-lookup"><span data-stu-id="50a1a-226">Because you completed hello walk-through, you shouldn't need tooset up new policies for client walk-throughs on hello site.</span></span>
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a><span data-ttu-id="50a1a-227">Agregar el archivo de configuración tooyour server.js</span><span class="sxs-lookup"><span data-stu-id="50a1a-227">Add configuration tooyour server.js file</span></span>
<span data-ttu-id="50a1a-228">valores de hello tooread de hello `config.js` de archivos que ha creado, agregue hello `.config` archivo como un recurso necesario en la aplicación y, a continuación, establecer Hola variables globales toothose en hello `config.js` documento.</span><span class="sxs-lookup"><span data-stu-id="50a1a-228">tooread hello values from hello `config.js` file you created, add hello `.config` file as a required resource in your application, and then set hello global variables toothose in hello `config.js` document.</span></span>

<span data-ttu-id="50a1a-229">Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`, si aún no está:</span><span class="sxs-lookup"><span data-stu-id="50a1a-229">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="50a1a-230">Abra hello `server.js` archivo en un editor.</span><span class="sxs-lookup"><span data-stu-id="50a1a-230">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="50a1a-231">Agregue Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="50a1a-231">Add hello following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="50a1a-232">Agregar una nueva sección demasiado`server.js` que incluye el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="50a1a-232">Add a new section too`server.js` that includes hello following code:</span></span>

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

<span data-ttu-id="50a1a-233">A continuación, vamos a agregar algunos marcadores de posición para los usuarios de Hola que recibimos de nuestras aplicaciones que realiza la llamada.</span><span class="sxs-lookup"><span data-stu-id="50a1a-233">Next, let's add some placeholders for hello users we receive from our calling applications.</span></span>

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

<span data-ttu-id="50a1a-234">Ahora vamos a crear también nuestro registrador.</span><span class="sxs-lookup"><span data-stu-id="50a1a-234">Let's go ahead and create our logger too.</span></span>

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="50a1a-235">Agregar información del esquema y el modelo de MongoDB hello mediante Mongoose</span><span class="sxs-lookup"><span data-stu-id="50a1a-235">Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="50a1a-236">Hello preparación anterior se compensa como aportar estos tres archivos juntos en un servicio de API de REST.</span><span class="sxs-lookup"><span data-stu-id="50a1a-236">hello earlier preparation pays off as you bring these three files together in a REST API service.</span></span>

<span data-ttu-id="50a1a-237">Para este tutorial, utilice MongoDB toostore las tareas, como se explicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="50a1a-237">For this walk-through, use MongoDB toostore your tasks, as discussed earlier.</span></span>

<span data-ttu-id="50a1a-238">Hola `config.js` archivo, se llama a la base de datos **tasklist**.</span><span class="sxs-lookup"><span data-stu-id="50a1a-238">In hello `config.js` file, you called your database **tasklist**.</span></span> <span data-ttu-id="50a1a-239">Este nombre también era lo que se incluye al final de Hola de hello `mongoose_auth_local` dirección URL de conexión.</span><span class="sxs-lookup"><span data-stu-id="50a1a-239">That name was also what you put at hello end of hello `mongoose_auth_local` connection URL.</span></span> <span data-ttu-id="50a1a-240">No es necesario toocreate esta base de datos con antelación en MongoDB.</span><span class="sxs-lookup"><span data-stu-id="50a1a-240">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="50a1a-241">Crea la base de datos de hello automáticamente en primera ejecución de saludo de la aplicación de servidor.</span><span class="sxs-lookup"><span data-stu-id="50a1a-241">It creates hello database for you on hello first run of your server application.</span></span>

<span data-ttu-id="50a1a-242">Una vez que indique al servidor hello qué toouse de base de datos de MongoDB, necesita toowrite algunos modelo de código adicional toocreate hello y esquema para las tareas de servidor.</span><span class="sxs-lookup"><span data-stu-id="50a1a-242">After you tell hello server which MongoDB database toouse, you need toowrite some additional code toocreate hello model and schema for your server tasks.</span></span>

### <a name="expand-hello-model"></a><span data-ttu-id="50a1a-243">Expanda el modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="50a1a-243">Expand hello model</span></span>
<span data-ttu-id="50a1a-244">Este modelo de esquema es muy sencillo.</span><span class="sxs-lookup"><span data-stu-id="50a1a-244">This schema model is simple.</span></span> <span data-ttu-id="50a1a-245">Se puede expandir según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="50a1a-245">You can expand it as required.</span></span>

<span data-ttu-id="50a1a-246">`owner`: Que se asignó la tarea de toohello.</span><span class="sxs-lookup"><span data-stu-id="50a1a-246">`owner`: Who is assigned toohello task.</span></span> <span data-ttu-id="50a1a-247">Este objeto es de tipo **cadena**.</span><span class="sxs-lookup"><span data-stu-id="50a1a-247">This object is a **string**.</span></span>  

<span data-ttu-id="50a1a-248">`Text`: tarea de hello en Sí.</span><span class="sxs-lookup"><span data-stu-id="50a1a-248">`Text`: hello task itself.</span></span> <span data-ttu-id="50a1a-249">Este objeto es de tipo **cadena**.</span><span class="sxs-lookup"><span data-stu-id="50a1a-249">This object is a **string**.</span></span>

<span data-ttu-id="50a1a-250">`date`: fecha de hello vence esa tarea hello.</span><span class="sxs-lookup"><span data-stu-id="50a1a-250">`date`: hello date that hello task is due.</span></span> <span data-ttu-id="50a1a-251">Este objeto es de tipo **datetime**.</span><span class="sxs-lookup"><span data-stu-id="50a1a-251">This object is a **datetime**.</span></span>

<span data-ttu-id="50a1a-252">`completed`: Si la tarea hello está completa.</span><span class="sxs-lookup"><span data-stu-id="50a1a-252">`completed`: If hello task is complete.</span></span> <span data-ttu-id="50a1a-253">Este objeto es de tipo **booleano**.</span><span class="sxs-lookup"><span data-stu-id="50a1a-253">This object is a **Boolean**.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="50a1a-254">Crear esquemas de hello en el código de hello</span><span class="sxs-lookup"><span data-stu-id="50a1a-254">Create hello schema in hello code</span></span>
<span data-ttu-id="50a1a-255">Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`, si aún no está:</span><span class="sxs-lookup"><span data-stu-id="50a1a-255">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="50a1a-256">Abra hello `server.js` archivo en un editor.</span><span class="sxs-lookup"><span data-stu-id="50a1a-256">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="50a1a-257">Agregue Hola siguiendo la información que aparece debajo de la entrada de configuración de hello:</span><span class="sxs-lookup"><span data-stu-id="50a1a-257">Add hello following information below hello configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="50a1a-258">En primer lugar crear esquema hello y, a continuación, se crea un objeto de modelo que use toostore los datos a lo largo de Hola de código cuando se define la **rutas**.</span><span class="sxs-lookup"><span data-stu-id="50a1a-258">You first create hello schema, and then you create a model object that you use toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="add-routes-for-your-rest-api-task-server"></a><span data-ttu-id="50a1a-259">Incorporación de rutas para el servidor de la tarea de API de REST</span><span class="sxs-lookup"><span data-stu-id="50a1a-259">Add routes for your REST API task server</span></span>
<span data-ttu-id="50a1a-260">Ahora que tiene un toowork de modelo de base de datos con, agregar rutas de Hola que use para el servidor de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="50a1a-260">Now that you have a database model toowork with, add hello routes you use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="50a1a-261">Información acerca de las rutas en Restify</span><span class="sxs-lookup"><span data-stu-id="50a1a-261">About routes in Restify</span></span>
<span data-ttu-id="50a1a-262">Rutas funcionan en Restify Hola misma forma en que funcionan cuando usen la pila de hello Express.</span><span class="sxs-lookup"><span data-stu-id="50a1a-262">Routes work in Restify in hello same way that they work when they use hello Express stack.</span></span> <span data-ttu-id="50a1a-263">Definir las rutas mediante el uso de URI que se espera toocall de las aplicaciones de cliente de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="50a1a-263">You define routes by using hello URI that you expect hello client applications toocall.</span></span>

<span data-ttu-id="50a1a-264">Un patrón típico de una ruta Restify es:</span><span class="sxs-lookup"><span data-stu-id="50a1a-264">A typical pattern for a Restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

<span data-ttu-id="50a1a-265">Restify y Express proporcionan una funcionalidad mucho más profunda, como la definición de tipos de aplicación y la realización de un enrutamiento complejo en distintos puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="50a1a-265">Restify and Express can provide much deeper functionality, such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="50a1a-266">Para fines de Hola de este tutorial, mantenemos estas rutas simple.</span><span class="sxs-lookup"><span data-stu-id="50a1a-266">For hello purposes of this tutorial, we keep these routes simple.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="50a1a-267">Agregar servidor de forma predeterminada las rutas tooyour</span><span class="sxs-lookup"><span data-stu-id="50a1a-267">Add default routes tooyour server</span></span>
<span data-ttu-id="50a1a-268">Ahora agregue rutas CRUD básicas de Hola de **crear** y **lista** para la API de REST.</span><span class="sxs-lookup"><span data-stu-id="50a1a-268">You now add hello basic CRUD routes of **create** and **list** for our REST API.</span></span> <span data-ttu-id="50a1a-269">Otras rutas pueden encontrarse en hello `complete` rama de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="50a1a-269">Other routes can be found in hello `complete` branch of hello sample.</span></span>

<span data-ttu-id="50a1a-270">Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`, si aún no está:</span><span class="sxs-lookup"><span data-stu-id="50a1a-270">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="50a1a-271">Abra hello `server.js` archivo en un editor.</span><span class="sxs-lookup"><span data-stu-id="50a1a-271">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="50a1a-272">Por debajo de las entradas de base de datos de hello realizados anteriormente agregar Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="50a1a-272">Below hello database entries you made above add hello following information:</span></span>

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
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
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

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
            log.warn(err, "There is no tasks in hello database. Add one!");
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


#### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="50a1a-273">Agregar control de errores para las rutas de Hola</span><span class="sxs-lookup"><span data-stu-id="50a1a-273">Add error handling for hello routes</span></span>
<span data-ttu-id="50a1a-274">Agregar un control de errores para que puedan comunicarse los problemas que encontrar a toohello atrás cliente de forma que puede entender.</span><span class="sxs-lookup"><span data-stu-id="50a1a-274">Add some error handling so that you can communicate any problems you encounter back toohello client in a way that it can understand.</span></span>

<span data-ttu-id="50a1a-275">Agregue Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="50a1a-275">Add hello following code:</span></span>

```Javascript
///--- Errors for communicating something interesting back toohello client
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


## <a name="create-your-server"></a><span data-ttu-id="50a1a-276">Creación del servidor</span><span class="sxs-lookup"><span data-stu-id="50a1a-276">Create your server</span></span>
<span data-ttu-id="50a1a-277">Ahora ha definido la base de datos y colocado las rutas en su sitio.</span><span class="sxs-lookup"><span data-stu-id="50a1a-277">You have now defined your database and put your routes in place.</span></span> <span data-ttu-id="50a1a-278">últimos Hola para toodo es la instancia del servidor de Hola de tooadd que administra las llamadas.</span><span class="sxs-lookup"><span data-stu-id="50a1a-278">hello last thing for you toodo is tooadd hello server instance that manages your calls.</span></span>

<span data-ttu-id="50a1a-279">Restify y Express proporcionan personalización en profundidad para un servidor de la API de REST, pero el programa de instalación más sencilla de hello aquí utilizamos.</span><span class="sxs-lookup"><span data-stu-id="50a1a-279">Restify and Express provide deep customization for a REST API server, but we use hello most basic setup here.</span></span>

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a><span data-ttu-id="50a1a-280">Agregar servidor de hello rutas toohello (sin autenticación)</span><span class="sxs-lookup"><span data-stu-id="50a1a-280">Add hello routes toohello server (without authentication)</span></span>
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="50a1a-281">Agregar servidor de la API de REST de autenticación tooyour</span><span class="sxs-lookup"><span data-stu-id="50a1a-281">Add authentication tooyour REST API server</span></span>
<span data-ttu-id="50a1a-282">Ahora que tiene un servidor de API de REST en ejecución, puede hacer que sea útil en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50a1a-282">Now that you have a running REST API server, you can make it useful against Azure AD.</span></span>

<span data-ttu-id="50a1a-283">Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`, si aún no está:</span><span class="sxs-lookup"><span data-stu-id="50a1a-283">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="50a1a-284">Usar hello OIDCBearerStrategy que se incluye con azure de passport de ad</span><span class="sxs-lookup"><span data-stu-id="50a1a-284">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
> [!TIP]
> <span data-ttu-id="50a1a-285">No se puede suplantar al escribir las API, siempre debe vincular Hola datos toosomething único del token de Hola que Hola de usuario.</span><span class="sxs-lookup"><span data-stu-id="50a1a-285">When you write APIs, you should always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="50a1a-286">Al servidor de hello almacena elementos de lista de tareas, hace según hello **oid** del usuario de hello en el token de hello (llamado a través de token.oid), que entra en el campo propietario"Hola".</span><span class="sxs-lookup"><span data-stu-id="50a1a-286">When hello server stores ToDo items, it does so based on hello **oid** of hello user in hello token (called through token.oid), which goes in hello “owner” field.</span></span> <span data-ttu-id="50a1a-287">Este valor garantiza que el usuario es el único que puede acceder a sus propias tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="50a1a-287">This value ensures that only that user can access their own ToDo items.</span></span> <span data-ttu-id="50a1a-288">No hay ningún riesgo en hello API de "propietario", por lo que un usuario externo puede solicitar otros elementos de lista de tareas, incluso si se autentican en.</span><span class="sxs-lookup"><span data-stu-id="50a1a-288">There is no exposure in hello API of “owner,” so an external user can request others’ ToDo items even if they are authenticated.</span></span>
>
>

<span data-ttu-id="50a1a-289">A continuación, use la estrategia de portador de Hola que viene con `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="50a1a-289">Next, use hello bearer strategy that comes with `passport-azure-ad`.</span></span>

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

<span data-ttu-id="50a1a-290">Passport utiliza Hola mismo patrón para todas las estrategias de sus.</span><span class="sxs-lookup"><span data-stu-id="50a1a-290">Passport uses hello same pattern for all its strategies.</span></span> <span data-ttu-id="50a1a-291">Le pasa un elemento `function()` que tiene los parámetros `token` y `done`.</span><span class="sxs-lookup"><span data-stu-id="50a1a-291">You pass it a `function()` that has `token` and `done` as parameters.</span></span> <span data-ttu-id="50a1a-292">estrategia de Hello vuelve a estar tooyou después de que lo ha hecho todo su trabajo.</span><span class="sxs-lookup"><span data-stu-id="50a1a-292">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="50a1a-293">A continuación, debe almacenar usuario hello y guardar el token de Hola por lo que no es necesario tooask para este nuevo.</span><span class="sxs-lookup"><span data-stu-id="50a1a-293">You should then store hello user and save hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50a1a-294">código de Hello anterior toma cualquier usuario que ocurre tooauthenticate tooyour server.</span><span class="sxs-lookup"><span data-stu-id="50a1a-294">hello code above takes any user who happens tooauthenticate tooyour server.</span></span> <span data-ttu-id="50a1a-295">Este proceso se conoce como registro automático.</span><span class="sxs-lookup"><span data-stu-id="50a1a-295">This process is known as autoregistration.</span></span> <span data-ttu-id="50a1a-296">En servidores de producción, no permita que en cualquier API de Hola de acceso de los usuarios sin tener primero que les vaya a través de un proceso de registro.</span><span class="sxs-lookup"><span data-stu-id="50a1a-296">In production servers, don't let in any users access hello API without first having them go through a registration process.</span></span> <span data-ttu-id="50a1a-297">Este proceso suele ser patrón Hola que se ven en las aplicaciones de consumidor que permiten tooregister mediante el uso de Facebook, pero a continuación, pida toofill información adicional.</span><span class="sxs-lookup"><span data-stu-id="50a1a-297">This process is usually hello pattern you see in consumer apps that allow you tooregister by using Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="50a1a-298">Si este programa no era un programa de línea de comandos, se pudo extrajeron correo electrónico Hola de objeto de símbolo (token) de Hola que se devuelve y, a continuación, pide a los usuarios toofill información adicional.</span><span class="sxs-lookup"><span data-stu-id="50a1a-298">If this program wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked users toofill out additional information.</span></span> <span data-ttu-id="50a1a-299">Dado que este es un ejemplo, agregamos base de datos de tooan en memoria.</span><span class="sxs-lookup"><span data-stu-id="50a1a-299">Because this is a sample, we add them tooan in-memory database.</span></span>
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a><span data-ttu-id="50a1a-300">Ejecute el tooverify de aplicación de servidor que TI rechaza</span><span class="sxs-lookup"><span data-stu-id="50a1a-300">Run your server application tooverify that it rejects you</span></span>
<span data-ttu-id="50a1a-301">Puede usar `curl` toosee si tiene ahora OAuth2 protección frente a los extremos.</span><span class="sxs-lookup"><span data-stu-id="50a1a-301">You can use `curl` toosee if you now have OAuth2 protection against your endpoints.</span></span> <span data-ttu-id="50a1a-302">Hello encabezados devueltos deben ser suficiente tootell que se encuentra en la ruta de acceso correcta de Hola.</span><span class="sxs-lookup"><span data-stu-id="50a1a-302">hello headers returned should be enough tootell you that you are on hello right path.</span></span>

<span data-ttu-id="50a1a-303">Asegúrese de que la instancia de MongoDB se esté ejecutando:</span><span class="sxs-lookup"><span data-stu-id="50a1a-303">Make sure that your MongoDB instance is running:</span></span>

    $sudo mongodb

<span data-ttu-id="50a1a-304">Cambiar directorio toohello y el servidor de ejecución hello:</span><span class="sxs-lookup"><span data-stu-id="50a1a-304">Change toohello directory and run hello server:</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="50a1a-305">En una nueva ventana de terminal, ejecute `curl`</span><span class="sxs-lookup"><span data-stu-id="50a1a-305">In a new terminal window, run `curl`</span></span>

<span data-ttu-id="50a1a-306">Pruebe una operación POST básica:</span><span class="sxs-lookup"><span data-stu-id="50a1a-306">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="50a1a-307">Un error 401 es respuesta Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="50a1a-307">A 401 error is hello response you want.</span></span> <span data-ttu-id="50a1a-308">Indica que está tratando de esa capa de Passport hello tooredirect toohello extremo authorize.</span><span class="sxs-lookup"><span data-stu-id="50a1a-308">It indicates that hello Passport layer is trying tooredirect toohello authorize endpoint.</span></span>

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a><span data-ttu-id="50a1a-309">Ahora tiene un servicio de API de REST que usa OAuth2</span><span class="sxs-lookup"><span data-stu-id="50a1a-309">You now have a REST API service that uses OAuth2</span></span>
<span data-ttu-id="50a1a-310">Ha implementado una API de REST mediante Restify y OAuth.</span><span class="sxs-lookup"><span data-stu-id="50a1a-310">You have implemented a REST API by using Restify and OAuth!</span></span> <span data-ttu-id="50a1a-311">Ahora tienes código suficiente para que pueda continuar toodevelop el servicio y crear en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="50a1a-311">You now have sufficient code so that you can continue toodevelop your service and build on this example.</span></span> <span data-ttu-id="50a1a-312">Ha avanzado todo lo que se puede con este servidor sin usar un cliente compatible con OAuth2.</span><span class="sxs-lookup"><span data-stu-id="50a1a-312">You have gone as far as you can with this server without using an OAuth2-compatible client.</span></span> <span data-ttu-id="50a1a-313">Para ese paso siguiente, utilice un tutorial adicional como nuestro [conectarse tooa web API con iOS con B2C](active-directory-b2c-devquickstarts-ios.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="50a1a-313">For that next step use an additional walk-through like our [Connect tooa web API by using iOS with B2C](active-directory-b2c-devquickstarts-ios.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50a1a-314">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="50a1a-314">Next steps</span></span>
<span data-ttu-id="50a1a-315">Ahora puede mover temas toomore avanzada, como:</span><span class="sxs-lookup"><span data-stu-id="50a1a-315">You can now move toomore advanced topics, such as:</span></span>

[<span data-ttu-id="50a1a-316">Conectar tooa web API con iOS y B2C</span><span class="sxs-lookup"><span data-stu-id="50a1a-316">Connect tooa web API by using iOS with B2C</span></span>](active-directory-b2c-devquickstarts-ios.md)