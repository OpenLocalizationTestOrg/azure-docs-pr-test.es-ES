---
title: "aaaAzure AD Node.js Introducción | Documentos de Microsoft"
description: "¿Cómo toobuild una API de REST de Node.js web que se integra con Azure AD para la autenticación."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 512ae6de9acfde8b58c0447ab4a6b573fb6407c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a><span data-ttu-id="13529-103">Introducción a las API web para Node.js</span><span class="sxs-lookup"><span data-stu-id="13529-103">Get started with web APIs for Node.js</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="13529-104">*Passport* es middleware de autenticación para Node.js.</span><span class="sxs-lookup"><span data-stu-id="13529-104">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="13529-105">Flexible y modular, Passport puede quitarse de forma discreta en tooany basada en Express o Restify la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="13529-105">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or Restify web application.</span></span> <span data-ttu-id="13529-106">Un conjunto completo de estrategias da soporte a la autenticación con nombre de usuario y contraseña, Facebook, Twitter, etc.</span><span class="sxs-lookup"><span data-stu-id="13529-106">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="13529-107">Hemos desarrollado una estrategia para Microsoft Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="13529-107">We have developed a strategy for Microsoft Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="13529-108">Se instale este módulo y, a continuación, agregue Hola Microsoft Azure Active Directory `passport-azure-ad` complemento.</span><span class="sxs-lookup"><span data-stu-id="13529-108">We install this module and then add hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="13529-109">toodo, necesita:</span><span class="sxs-lookup"><span data-stu-id="13529-109">toodo this, you need to:</span></span>

1. <span data-ttu-id="13529-110">Registrar una aplicación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13529-110">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="13529-111">Configurar la aplicación toouse Passport `passport-azure-ad` complemento.</span><span class="sxs-lookup"><span data-stu-id="13529-111">Set up your app toouse Passport's `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="13529-112">Configurar un cliente aplicación toocall hello tooDo lista API web.</span><span class="sxs-lookup"><span data-stu-id="13529-112">Configure a client application toocall hello tooDo List web API.</span></span>

<span data-ttu-id="13529-113">código de Hello para este tutorial se mantiene [en GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span><span class="sxs-lookup"><span data-stu-id="13529-113">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span></span>

> [!NOTE]
> <span data-ttu-id="13529-114">Este artículo no tratan cómo tooimplement sesión, inicio de sesión, o generar perfiles de administración con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="13529-114">This article doesn't cover how tooimplement sign-in, sign-up, or profile management with Azure AD B2C.</span></span> <span data-ttu-id="13529-115">Se centra en las API de web que realiza la llamada después de hello usuario ya está autenticado.</span><span class="sxs-lookup"><span data-stu-id="13529-115">It focuses on calling web APIs after hello user is already authenticated.</span></span>  <span data-ttu-id="13529-116">Es recomendable que comience con [cómo toointegrate con documentos de Azure Active Directory](active-directory-how-to-integrate.md) toolearn sobre conceptos básicos de Hola de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="13529-116">We recommend that you start with [How toointegrate with Azure Active Directory document](active-directory-how-to-integrate.md) toolearn about hello basics of Azure Active Directory.</span></span>
>
>

<span data-ttu-id="13529-117">Por lo que lanzamos todo código fuente de hello en este ejemplo en GitHub bajo una licencia MIT, sentirse tooclone libre (o incluso mejor, bifurcar) y proporcionar comentarios y solicitudes de extracción.</span><span class="sxs-lookup"><span data-stu-id="13529-117">We've released all hello source code for this running example in GitHub under an MIT license, so feel free tooclone (or even better, fork), and provide feedback and pull requests.</span></span>

## <a name="about-nodejs-modules"></a><span data-ttu-id="13529-118">Acerca de los módulos Node.js</span><span class="sxs-lookup"><span data-stu-id="13529-118">About Node.js modules</span></span>
<span data-ttu-id="13529-119">En este tutorial se usan módulos Node.js.</span><span class="sxs-lookup"><span data-stu-id="13529-119">We use Node.js modules in this walkthrough.</span></span> <span data-ttu-id="13529-120">Los módulos son paquetes JavaScript que pueden cargarse y que proporcionan una funcionalidad específica para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="13529-120">Modules are loadable JavaScript packages that provide specific functionality for your application.</span></span> <span data-ttu-id="13529-121">Normalmente se instale módulos mediante hello Node.js una herramienta de línea de comandos de NPM en directorio de instalación de NPM Hola.</span><span class="sxs-lookup"><span data-stu-id="13529-121">You usually install modules by using hello Node.js an NPM command-line tool in hello NPM installation directory.</span></span> <span data-ttu-id="13529-122">Sin embargo, algunos módulos, como el módulo HTTP de hello, se incluyen en el paquete de Node.js del núcleo de Hola.</span><span class="sxs-lookup"><span data-stu-id="13529-122">However, some modules, such as hello HTTP module, are included in hello core Node.js package.</span></span>

<span data-ttu-id="13529-123">Módulos instalados se guardan en hello **node_modules** directorio raíz de Hola de su directorio de instalación de Node.js.</span><span class="sxs-lookup"><span data-stu-id="13529-123">Installed modules are saved in hello **node_modules** directory at hello root of your Node.js installation directory.</span></span> <span data-ttu-id="13529-124">Cada módulo en hello **node_modules** directory mantiene su propio **node_modules** directorio que contiene los módulos que depende.</span><span class="sxs-lookup"><span data-stu-id="13529-124">Each module in hello **node_modules** directory maintains its own **node_modules** directory that contains any modules that it depends on.</span></span> <span data-ttu-id="13529-125">Además, cada módulo requerido tiene un directorio **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="13529-125">Also, each required module has a **node_modules** directory.</span></span> <span data-ttu-id="13529-126">Esta estructura de directorios recursiva representa la cadena de dependencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="13529-126">This recursive directory structure represents hello dependency chain.</span></span>

<span data-ttu-id="13529-127">Esta estructura de la cadena de dependencias da como resultado una mayor superficie de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="13529-127">This dependency chain structure results in a larger application footprint.</span></span> <span data-ttu-id="13529-128">Pero también garantiza que se cumplen todas las dependencias y esa versión de Hola de módulos de Hola que se usa en el desarrollo también se utiliza en producción.</span><span class="sxs-lookup"><span data-stu-id="13529-128">But it also guarantees that all dependencies are met and that hello version of hello modules that's used in development is also used in production.</span></span> <span data-ttu-id="13529-129">Esto facilita comportamientos de la aplicación de producción de hello más predecible y evita los problemas de control de versiones que podrían afectar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="13529-129">This makes hello production app behavior more predictable and prevents versioning problems that might affect users.</span></span>

## <a name="step-1-register-an-azure-ad-tenant"></a><span data-ttu-id="13529-130">Paso 1: Registro de un inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="13529-130">Step 1: Register an Azure AD tenant</span></span>
<span data-ttu-id="13529-131">toouse este ejemplo, necesita un inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="13529-131">toouse this sample, you need an Azure Active Directory tenant.</span></span> <span data-ttu-id="13529-132">Si no está seguro de qué un inquilino o tooget uno, vea [cómo inquilino tooget un Azure AD](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="13529-132">If you're not sure what a tenant is or how tooget one, see [How tooget an Azure AD tenant](active-directory-howto-tenant.md).</span></span>

## <a name="step-2-create-an-application"></a><span data-ttu-id="13529-133">Paso 2: Creación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="13529-133">Step 2: Create an application</span></span>
<span data-ttu-id="13529-134">A continuación, creará una aplicación en el directorio que ofrece Azure AD información que necesita toosecurely comunicarse con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="13529-134">Next you create an app in your directory that gives Azure AD information that it needs toosecurely communicate with your app.</span></span>  <span data-ttu-id="13529-135">Aplicación de cliente de hello y API web se representan mediante una sola **Id. de aplicación** en este caso, porque están formadas por una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="13529-135">Both hello client app and web API are represented by a single **Application ID** in this case, because they comprise one logical app.</span></span>  <span data-ttu-id="13529-136">toocreate una aplicación, siga [estas instrucciones](active-directory-how-applications-are-added.md).</span><span class="sxs-lookup"><span data-stu-id="13529-136">toocreate an app, follow [these instructions](active-directory-how-applications-are-added.md).</span></span> <span data-ttu-id="13529-137">Si va a crear una aplicación de línea de negocio [es posible que estas instrucciones adicionales le resulten útiles](../active-directory-applications-guiding-developers-for-lob-applications.md).</span><span class="sxs-lookup"><span data-stu-id="13529-137">If you are building a line-of-business app, [these additional instructions might be useful](../active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="13529-138">toocreate una aplicación:</span><span class="sxs-lookup"><span data-stu-id="13529-138">toocreate an application:</span></span>

1. <span data-ttu-id="13529-139">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="13529-139">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="13529-140">En el menú superior de hello, seleccione su cuenta.</span><span class="sxs-lookup"><span data-stu-id="13529-140">On hello top menu, select your account.</span></span> <span data-ttu-id="13529-141">A continuación, en hello **Directory** lista, seleccione la aplicación de inquilino de Active Directory de Hola donde desea tooregister.</span><span class="sxs-lookup"><span data-stu-id="13529-141">Then, under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="13529-142">En el menú de Hola Hola izquierda, seleccione **más servicios**y, a continuación, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="13529-142">In hello menu on hello left, select **More Services**, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="13529-143">Seleccione **Registros de aplicaciones** y luego seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="13529-143">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="13529-144">Siga Hola indicaciones toocreate una **aplicación Web o WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="13529-144">Follow hello prompts toocreate a **Web Application and/or WebAPI**.</span></span>

      * <span data-ttu-id="13529-145">Hola **nombre** de hello aplicación describe los usuarios de tooend de aplicación.</span><span class="sxs-lookup"><span data-stu-id="13529-145">hello **name** of hello application describes your application tooend users.</span></span>

      * <span data-ttu-id="13529-146">Hola **dirección URL de inicio de sesión** es Hola dirección URL base de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="13529-146">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="13529-147">Hola predeterminado es la dirección URL del código de ejemplo de Hola `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="13529-147">hello default URL of hello sample code is `https://localhost:8080`.</span></span>

6. <span data-ttu-id="13529-148">Después de registrarse, Azure AD asigna a su aplicación un identificador de aplicación individual.</span><span class="sxs-lookup"><span data-stu-id="13529-148">After you register, Azure AD assigns your app a unique Application ID.</span></span> <span data-ttu-id="13529-149">Se necesita este valor en las secciones siguientes de hello, por lo tanto cópiela desde la página de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="13529-149">You need this value in hello next sections, so copy it from hello application page.</span></span>

7. <span data-ttu-id="13529-150">De hello **configuración** -> **propiedades** página de la aplicación, actualice Hola App ID URI.</span><span class="sxs-lookup"><span data-stu-id="13529-150">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="13529-151">Hola **App ID URI** es un identificador único para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="13529-151">hello **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="13529-152">convención de Hello es toouse `https://<tenant-domain>/<app-name>`, por ejemplo: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="13529-152">hello convention is toouse `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

8. <span data-ttu-id="13529-153">Crear un **clave** para la aplicación de hello **configuración** página y, a continuación, cópielo en otro.</span><span class="sxs-lookup"><span data-stu-id="13529-153">Create a **Key** for your application from hello **Settings** page, and then copy it somewhere.</span></span> <span data-ttu-id="13529-154">La necesitará en breve.</span><span class="sxs-lookup"><span data-stu-id="13529-154">You'll need it shortly.</span></span>

## <a name="step-3-download-nodejs-for-your-platform"></a><span data-ttu-id="13529-155">Paso 3: Descarga de Node.js para la plataforma</span><span class="sxs-lookup"><span data-stu-id="13529-155">Step 3: Download Node.js for your platform</span></span>
<span data-ttu-id="13529-156">toosuccessfully utilizar este ejemplo, debe tener una instalación activa de Node.js.</span><span class="sxs-lookup"><span data-stu-id="13529-156">toosuccessfully use this sample, you must have a working installation of Node.js.</span></span>

<span data-ttu-id="13529-157">Instale Node.js desde [http://nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="13529-157">Install Node.js from [http://nodejs.org](http://nodejs.org).</span></span>

## <a name="step-4-install-mongodb-on-your-platform"></a><span data-ttu-id="13529-158">Paso 4: Instalación de MongoDB en la plataforma</span><span class="sxs-lookup"><span data-stu-id="13529-158">Step 4: Install MongoDB on your platform</span></span>
<span data-ttu-id="13529-159">toosuccessfully utilizar este ejemplo, debe tener una instalación activa de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="13529-159">toosuccessfully use this sample, you must have a working installation of MongoDB.</span></span> <span data-ttu-id="13529-160">Utilice MongoDB toomake Hola API de REST persistente en instancias del servidor.</span><span class="sxs-lookup"><span data-stu-id="13529-160">You use MongoDB toomake hello REST API persistent across server instances.</span></span>

<span data-ttu-id="13529-161">Instale MongoDB desde [http://mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="13529-161">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="13529-162">Este tutorial se supone que utiliza Hola instalación y servidor de puntos de conexión predeterminados para MongoDB, que en tiempo de Hola de redactar este artículo es mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="13529-162">This walkthrough assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is mongodb://localhost.</span></span>
>
>

## <a name="step-5-install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="13529-163">Paso 5: Instalar los módulos de Restify hello en la API web</span><span class="sxs-lookup"><span data-stu-id="13529-163">Step 5: Install hello Restify modules in your web API</span></span>
<span data-ttu-id="13529-164">Estamos usando Restify toobuild nuestra API de REST.</span><span class="sxs-lookup"><span data-stu-id="13529-164">We are using Restify toobuild our REST API.</span></span> <span data-ttu-id="13529-165">Restify es un marco de trabajo de la aplicación de Node.js mínimo y flexible que se deriva de Express.</span><span class="sxs-lookup"><span data-stu-id="13529-165">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="13529-166">Tiene un sólido conjunto de características para crear API de REST sobre Connect.</span><span class="sxs-lookup"><span data-stu-id="13529-166">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="13529-167">Instalar Restify</span><span class="sxs-lookup"><span data-stu-id="13529-167">Install Restify</span></span>
1. <span data-ttu-id="13529-168">Desde la línea de comandos de hello, cambiar directorios toohello **organización** directory.</span><span class="sxs-lookup"><span data-stu-id="13529-168">From hello command line, change directories toohello **azuread** directory.</span></span> <span data-ttu-id="13529-169">Si hello **organización** directorio no existe, créelo.</span><span class="sxs-lookup"><span data-stu-id="13529-169">If hello **azuread** directory does not exist, create it.</span></span>

        `cd azuread - or- mkdir azuread; cd azuread`

2. <span data-ttu-id="13529-170">Escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="13529-170">Type hello following command:</span></span>

    `npm install restify`

    <span data-ttu-id="13529-171">Este comando instala Restify.</span><span class="sxs-lookup"><span data-stu-id="13529-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="13529-172">¿Ha recibido un error?</span><span class="sxs-lookup"><span data-stu-id="13529-172">Did you get an error?</span></span>
<span data-ttu-id="13529-173">Si se usa NPM en algunos sistemas operativos, se puede que recibir el siguiente mensaje **Error: EPERM, chmod "/usr/local/bin/.."**</span><span class="sxs-lookup"><span data-stu-id="13529-173">When you use NPM on some operating systems, you might receive an error that says **Error: EPERM, chmod '/usr/local/bin/..'**</span></span> <span data-ttu-id="13529-174">y una sugerencia que intentas ejecución cuenta de hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="13529-174">and a suggestion that you try running hello account as an administrator.</span></span> <span data-ttu-id="13529-175">Si esto ocurre, use hello sudo comando toorun NPM con un nivel de privilegios superior.</span><span class="sxs-lookup"><span data-stu-id="13529-175">If this occurs, use hello sudo command toorun NPM at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-regarding-dtrace"></a><span data-ttu-id="13529-176">¿Ha recibido un error relacionado con DTRACE?</span><span class="sxs-lookup"><span data-stu-id="13529-176">Did you get an error regarding DTRACE?</span></span>
<span data-ttu-id="13529-177">Al instalar Restify puede que vea un error similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="13529-177">You might see an error like this when installing Restify:</span></span>

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
<span data-ttu-id="13529-178">Restify proporciona un mecanismo eficaz para rastrear llamadas a REST mediante DTrace.</span><span class="sxs-lookup"><span data-stu-id="13529-178">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="13529-179">Sin embargo, muchos sistemas operativos no tienen DTrace.</span><span class="sxs-lookup"><span data-stu-id="13529-179">However, many operating systems do not have DTrace.</span></span> <span data-ttu-id="13529-180">Puede omitir estos errores con seguridad.</span><span class="sxs-lookup"><span data-stu-id="13529-180">You can safely ignore these errors.</span></span>

<span data-ttu-id="13529-181">salida de Hello de este comando debe ser similar toohello después de salida:</span><span class="sxs-lookup"><span data-stu-id="13529-181">hello output of this command should look similar toohello following output:</span></span>

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


## <a name="step-6-install-passportjs-in-your-web-api"></a><span data-ttu-id="13529-182">Paso 6: Instalación de Passport.js en su API web</span><span class="sxs-lookup"><span data-stu-id="13529-182">Step 6: Install Passport.js in your web API</span></span>
<span data-ttu-id="13529-183">[Passport](http://passportjs.org/) es middleware de autenticación para Node.js.</span><span class="sxs-lookup"><span data-stu-id="13529-183">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span></span> <span data-ttu-id="13529-184">Flexible y modular, Passport puede quitarse de forma discreta en tooany basada en Express o Restify la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="13529-184">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or Restify web application.</span></span> <span data-ttu-id="13529-185">Un conjunto completo de estrategias da soporte a la autenticación con nombre de usuario y contraseña, Facebook, Twitter, etc.</span><span class="sxs-lookup"><span data-stu-id="13529-185">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="13529-186">Hemos desarrollado una estrategia para Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="13529-186">We have developed a strategy for Azure Active Directory.</span></span> <span data-ttu-id="13529-187">Se instala este módulo y, a continuación, agrega la estrategia de Azure Active Directory Hola complemento.</span><span class="sxs-lookup"><span data-stu-id="13529-187">We install this module and then add hello Azure Active Directory strategy plug-in.</span></span>

1. <span data-ttu-id="13529-188">Desde la línea de comandos de hello, cambiar directorios toohello **organización** directory.</span><span class="sxs-lookup"><span data-stu-id="13529-188">From hello command line, change directories toohello **azuread** directory.</span></span>

2. <span data-ttu-id="13529-189">tooinstall passport.js, escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="13529-189">tooinstall passport.js, enter hello following command :</span></span>

    `npm install passport`

    <span data-ttu-id="13529-190">salida de Hello de comando hello debería ser similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="13529-190">hello output of hello command should look similar toohello following:</span></span>

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-tooyour-web-api"></a><span data-ttu-id="13529-191">Paso 7: Agregar AD de Azure de Passport tooyour web API</span><span class="sxs-lookup"><span data-stu-id="13529-191">Step 7: Add Passport-Azure-AD tooyour web API</span></span>
<span data-ttu-id="13529-192">A continuación, agregamos estrategia de OAuth de hello mediante el uso de `passport-azure-ad`, un conjunto de estrategias que se conectan tooPassport de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="13529-192">Next we add hello OAuth strategy by using `passport-azure-ad`, a suite of strategies that connect Azure Active Directory tooPassport.</span></span> <span data-ttu-id="13529-193">En este ejemplo de API de REST, esta estrategia se usa para los tokens de portador.</span><span class="sxs-lookup"><span data-stu-id="13529-193">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="13529-194">Aunque OAuth2 proporciona un marco en el que se puede emitir cualquier tipo de token conocido, habitualmente solo se usan determinados tipos de token.</span><span class="sxs-lookup"><span data-stu-id="13529-194">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types are commonly used.</span></span> <span data-ttu-id="13529-195">Tokens de portador son tokens de hello suelen usada para proteger los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="13529-195">Bearer tokens are hello most commonly used tokens for protecting endpoints.</span></span> <span data-ttu-id="13529-196">Son tipo hello emitido más comúnmente del token de OAuth2.</span><span class="sxs-lookup"><span data-stu-id="13529-196">They are hello most widely issued type of token in OAuth2.</span></span> <span data-ttu-id="13529-197">Muchas implementaciones, se supone que los tokens de portador son Hola único tipo de tokens emitidos.</span><span class="sxs-lookup"><span data-stu-id="13529-197">Many implementations assume that bearer tokens are hello only type of tokens that are issued.</span></span>
>
>

<span data-ttu-id="13529-198">Desde la línea de comandos de hello, cambiar directorios toohello **organización** directory.</span><span class="sxs-lookup"><span data-stu-id="13529-198">From hello command line, change directories toohello **azuread** directory.</span></span>

<span data-ttu-id="13529-199">Escriba lo siguiente Hola comando hello tooinstall Passport.js `passport-azure-ad module`:</span><span class="sxs-lookup"><span data-stu-id="13529-199">Type hello following command tooinstall hello Passport.js `passport-azure-ad module`:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="13529-200">resultado de Hello de comando de Hola debería ser similar toohello después de salida:</span><span class="sxs-lookup"><span data-stu-id="13529-200">hello output of hello command should look similar toohello following output:</span></span>


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



## <a name="step-8-add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="13529-201">Paso 8: Agregar MongoDB módulos tooyour web API</span><span class="sxs-lookup"><span data-stu-id="13529-201">Step 8: Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="13529-202">MongoDB se usa como almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="13529-202">We use MongoDB as our datastore.</span></span> <span data-ttu-id="13529-203">Por esta razón, es necesario tooinstall Hola usadas de complemento llamados modelos de toomanage Mongoose y esquemas.</span><span class="sxs-lookup"><span data-stu-id="13529-203">For that reason, we need tooinstall hello widely used plug-in called Mongoose toomanage models and schemas.</span></span> <span data-ttu-id="13529-204">También es necesario el controlador de base de datos de hello tooinstall para MongoDB (conocida también como MongoDB).</span><span class="sxs-lookup"><span data-stu-id="13529-204">We also need tooinstall hello database driver for MongoDB (which is also called MongoDB).</span></span>

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a><span data-ttu-id="13529-205">Paso 9: Instalación de módulos adicionales</span><span class="sxs-lookup"><span data-stu-id="13529-205">Step 9: Install additional modules</span></span>
<span data-ttu-id="13529-206">A continuación se instale Hola restantes módulos necesarios.</span><span class="sxs-lookup"><span data-stu-id="13529-206">Next we install hello remaining required modules.</span></span>

1. <span data-ttu-id="13529-207">Desde la línea de comandos de hello, cambiar directorios toohello **organización** carpeta si no está ya no existe.</span><span class="sxs-lookup"><span data-stu-id="13529-207">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="13529-208">Escriba Hola después comandos tooinstall estos módulos en su **node_modules** directorio:</span><span class="sxs-lookup"><span data-stu-id="13529-208">Enter hello following commands tooinstall these modules in your **node_modules** directory:</span></span>

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a><span data-ttu-id="13529-209">Paso 10: Creación de server.js con sus dependencias</span><span class="sxs-lookup"><span data-stu-id="13529-209">Step 10: Create a server.js with your dependencies</span></span>
<span data-ttu-id="13529-210">archivo de Hello server.js proporciona la mayor parte de la funcionalidad de hello para el servidor de la API web.</span><span class="sxs-lookup"><span data-stu-id="13529-210">hello server.js file provides most of hello functionality for our web API server.</span></span> <span data-ttu-id="13529-211">Agregamos la mayor parte de nuestro archivo de código toothis.</span><span class="sxs-lookup"><span data-stu-id="13529-211">We add most of our code toothis file.</span></span> <span data-ttu-id="13529-212">Para fines de producción, se recomienda refactorizar funcionalidad hello en archivos más pequeños, como rutas independientes y controladores.</span><span class="sxs-lookup"><span data-stu-id="13529-212">For production purposes, we recommend that you refactor hello functionality into smaller files, such as separate routes and controllers.</span></span> <span data-ttu-id="13529-213">En esta demostración, se usa server.js para esta funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="13529-213">In this demo, we use server.js for this functionality.</span></span>

1. <span data-ttu-id="13529-214">Desde la línea de comandos de hello, cambiar directorios toohello **organización** carpeta si no está ya no existe.</span><span class="sxs-lookup"><span data-stu-id="13529-214">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="13529-215">Crear un `server.js` un archivo en el editor que prefiera y después agregue Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="13529-215">Create a `server.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. <span data-ttu-id="13529-216">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="13529-216">Save hello file.</span></span> <span data-ttu-id="13529-217">Volverás tooit en breve.</span><span class="sxs-lookup"><span data-stu-id="13529-217">We'll return tooit shortly.</span></span>

## <a name="step-11-create-a-config-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="13529-218">Paso 11: Crear un toostore del archivo de configuración de la configuración de Azure AD</span><span class="sxs-lookup"><span data-stu-id="13529-218">Step 11: Create a config file toostore your Azure AD settings</span></span>
<span data-ttu-id="13529-219">Este archivo de código pasa los parámetros de configuración de Hola de su tooPassport.js de portal de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="13529-219">This code file passes hello configuration parameters from your Azure Active Directory portal tooPassport.js.</span></span> <span data-ttu-id="13529-220">Estos valores de configuración se crean cuando se agrega hello web API toohello el portal en la primera parte del tutorial Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="13529-220">You created these configuration values when you added hello web API toohello portal in hello first part of hello walkthrough.</span></span> <span data-ttu-id="13529-221">Se explica qué tooput en valores de hello de estos parámetros después de copiar el código de hello.</span><span class="sxs-lookup"><span data-stu-id="13529-221">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

1. <span data-ttu-id="13529-222">Desde la línea de comandos de hello, cambiar directorios toohello **organización** carpeta si no está ya no existe.</span><span class="sxs-lookup"><span data-stu-id="13529-222">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="13529-223">Crear un `config.js` un archivo en el editor que prefiera y después agregue Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="13529-223">Create a `config.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in tooyour server unless you use hello common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in tooyour server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes toostderr in Unix.

         };
    ```
3. <span data-ttu-id="13529-224">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="13529-224">Save hello file.</span></span>

## <a name="step-12-add-configuration-values-tooyour-serverjs-file"></a><span data-ttu-id="13529-225">Paso 12: Agregar el archivo de configuración de valores tooyour server.js</span><span class="sxs-lookup"><span data-stu-id="13529-225">Step 12: Add configuration values tooyour server.js file</span></span>
<span data-ttu-id="13529-226">Necesitamos tooread estos valores desde el archivo .config de Hola que creaste en nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="13529-226">We need tooread these values from hello .config file that you created across our application.</span></span> <span data-ttu-id="13529-227">toodo, agregamos archivo .config de hello como un recurso necesario en nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="13529-227">toodo this, we add hello .config file as a required resource in our application.</span></span> <span data-ttu-id="13529-228">A continuación, se establecer variables de Hola de toomatch de variables globales de hello en documento config.js de Hola.</span><span class="sxs-lookup"><span data-stu-id="13529-228">Then we set hello global variables toomatch hello variables in hello config.js document.</span></span>

1. <span data-ttu-id="13529-229">Desde la línea de comandos de hello, cambiar directorios toohello **organización** carpeta si no está ya no existe.</span><span class="sxs-lookup"><span data-stu-id="13529-229">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="13529-230">Abra su `server.js` un archivo en el editor que prefiera y después agregue Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="13529-230">Open your `server.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```
3. <span data-ttu-id="13529-231">A continuación, agregue una nueva sección demasiado`server.js` con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="13529-231">Then add a new section too`server.js` with hello following code:</span></span>

    ```Javascript
    var options = {
        // hello URL of hello metadata document for your app. We will put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array toohold logged in users and hello current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If hello logging level is specified, switch tooit.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. <span data-ttu-id="13529-232">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="13529-232">Save hello file.</span></span>

## <a name="step-13-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="13529-233">Paso 13: Agregar Hola MongoDB modelo e información de esquema mediante Mongoose</span><span class="sxs-lookup"><span data-stu-id="13529-233">Step 13: Add hello MongoDB Model and schema information by using Mongoose</span></span>
<span data-ttu-id="13529-234">Ahora toda esta preparación va toostart buenos resultados tal y como se combinan estos tres archivos en un servicio de API de REST.</span><span class="sxs-lookup"><span data-stu-id="13529-234">Now all this preparation is going toostart paying off as we combine these three files into a REST API service.</span></span>

<span data-ttu-id="13529-235">En este tutorial, usamos MongoDB toostore nuestro tareas tal como se describe en el paso 4.</span><span class="sxs-lookup"><span data-stu-id="13529-235">For this walkthrough, we use MongoDB toostore our tasks as discussed in Step 4.</span></span>

<span data-ttu-id="13529-236">Hola `config.js` que hemos creado en el paso 11, llamamos a nuestra base de datos de archivo `tasklist`, porque ese era colocamos final Hola de nuestro **mogoose_auth_local** dirección URL de conexión.</span><span class="sxs-lookup"><span data-stu-id="13529-236">In hello `config.js` file that we created in Step 11, we called our database `tasklist`, because that was what we put at hello end of our **mogoose_auth_local** connection URL.</span></span> <span data-ttu-id="13529-237">No es necesario toocreate esta base de datos con antelación en MongoDB.</span><span class="sxs-lookup"><span data-stu-id="13529-237">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="13529-238">En su lugar, MongoDB esto para que podamos en hello primero crea ejecución de nuestra aplicación de servidor (suponiendo que aún no existe esa base de datos de hello).</span><span class="sxs-lookup"><span data-stu-id="13529-238">Instead, MongoDB creates this for us on hello first run of our server application (assuming that hello database doesn't already exist).</span></span>

<span data-ttu-id="13529-239">Ahora que hemos dicho servidor hello a qué base de datos de MongoDB nos gustaría toouse, es necesario toowrite algunos modelos de código adicional toocreate Hola y el esquema para las tareas del servidor.</span><span class="sxs-lookup"><span data-stu-id="13529-239">Now that we've told hello server which MongoDB database we'd like toouse, we need toowrite some additional code toocreate hello model and schema for our server's tasks.</span></span>

### <a name="discussion-of-hello-model"></a><span data-ttu-id="13529-240">Descripción del modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="13529-240">Discussion of hello model</span></span>
<span data-ttu-id="13529-241">Nuestro modelo de esquema es muy sencillo.</span><span class="sxs-lookup"><span data-stu-id="13529-241">Our schema model is simple.</span></span> <span data-ttu-id="13529-242">Expándalo si fuera necesario.</span><span class="sxs-lookup"><span data-stu-id="13529-242">You expand it as required.</span></span>

<span data-ttu-id="13529-243">NOMBRE: nombre de Hola de hello quien se asigna la tarea de toohello.</span><span class="sxs-lookup"><span data-stu-id="13529-243">NAME: hello name of hello person who is assigned toohello task.</span></span> <span data-ttu-id="13529-244">Un valor de **cadena**.</span><span class="sxs-lookup"><span data-stu-id="13529-244">A **String**.</span></span>

<span data-ttu-id="13529-245">TAREA: hello propia tarea.</span><span class="sxs-lookup"><span data-stu-id="13529-245">TASK: hello task itself.</span></span> <span data-ttu-id="13529-246">Un valor de **cadena**.</span><span class="sxs-lookup"><span data-stu-id="13529-246">A **String**.</span></span>

<span data-ttu-id="13529-247">Fecha: Hola esa tarea hello es debida.</span><span class="sxs-lookup"><span data-stu-id="13529-247">DATE: hello date that hello task is due.</span></span> <span data-ttu-id="13529-248">Un valor **DATETIME**.</span><span class="sxs-lookup"><span data-stu-id="13529-248">A **DATETIME**.</span></span>

<span data-ttu-id="13529-249">COMPLETADO: Si tiene la tarea hello ha completado o no.</span><span class="sxs-lookup"><span data-stu-id="13529-249">COMPLETED: If hello task has been completed or not.</span></span> <span data-ttu-id="13529-250">Un valor **booleano**.</span><span class="sxs-lookup"><span data-stu-id="13529-250">A **BOOLEAN**.</span></span>

### <a name="creating-hello-schema-in-hello-code"></a><span data-ttu-id="13529-251">Crear el esquema de hello en el código de hello</span><span class="sxs-lookup"><span data-stu-id="13529-251">Creating hello schema in hello code</span></span>
1. <span data-ttu-id="13529-252">Desde la línea de comandos de hello, cambiar directorios toohello **organización** carpeta si no está ya no existe.</span><span class="sxs-lookup"><span data-stu-id="13529-252">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="13529-253">Abra su `server.js` un archivo en el editor que prefiera y después agregue Hola siguiendo la información que aparece debajo de la entrada de configuración de hello:</span><span class="sxs-lookup"><span data-stu-id="13529-253">Open your `server.js` file in your favorite editor, and then add hello following information below hello configuration entry:</span></span>

    ```Javascript
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema toostore our tasks and users. It's a fairly simple schema for now.
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
<span data-ttu-id="13529-254">Como puede imaginar desde el código de hello, crearemos nuestro esquema primero.</span><span class="sxs-lookup"><span data-stu-id="13529-254">As you can tell from hello code, we create our schema first.</span></span> <span data-ttu-id="13529-255">A continuación, se crea un objeto de modelo que utilizamos toostore nuestros datos a lo largo de hello código cuando se definen nuestro **rutas**.</span><span class="sxs-lookup"><span data-stu-id="13529-255">Then we create a model object that we use toostore our data throughout hello code when we define our **Routes**.</span></span>

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a><span data-ttu-id="13529-256">Paso 14: Adición de rutas para el servidor de API de REST de la tarea</span><span class="sxs-lookup"><span data-stu-id="13529-256">Step 14: Add our routes for our task REST API server</span></span>
<span data-ttu-id="13529-257">Ahora que tenemos un toowork de modelo de base de datos con, vamos a agregar rutas de hello estamos uso continuo para el servidor de API de REST.</span><span class="sxs-lookup"><span data-stu-id="13529-257">Now that we have a database model toowork with, let's add hello routes we are going use for our REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="13529-258">Información acerca de las rutas en Restify</span><span class="sxs-lookup"><span data-stu-id="13529-258">About routes in Restify</span></span>
<span data-ttu-id="13529-259">Rutas de trabajo en Restify Hola igual manera que en hello Express en la pila.</span><span class="sxs-lookup"><span data-stu-id="13529-259">Routes work in Restify hello same way they do in hello Express stack.</span></span> <span data-ttu-id="13529-260">Definir las rutas mediante el uso de URI que se espera toocall de las aplicaciones de cliente de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="13529-260">You define routes by using hello URI that you expect hello client applications toocall.</span></span> <span data-ttu-id="13529-261">Normalmente, las rutas se definen en un archivo independiente.</span><span class="sxs-lookup"><span data-stu-id="13529-261">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="13529-262">Para nuestros propósitos, colocamos nuestra rutas de archivo de hello server.js.</span><span class="sxs-lookup"><span data-stu-id="13529-262">For our purposes, we put our routes in hello server.js file.</span></span> <span data-ttu-id="13529-263">Se recomienda factorizarlas en su propio archivo para que se puedan usar en producción.</span><span class="sxs-lookup"><span data-stu-id="13529-263">We recommend that you factor these routes into their own file for production use.</span></span>

<span data-ttu-id="13529-264">Este es un patrón típico de una ruta de Restify:</span><span class="sxs-lookup"><span data-stu-id="13529-264">A typical pattern for a Restify route is as follows:</span></span>

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep hello server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


<span data-ttu-id="13529-265">Este es el patrón de hello en su nivel más básico.</span><span class="sxs-lookup"><span data-stu-id="13529-265">This is hello pattern at its most basic level.</span></span> <span data-ttu-id="13529-266">Restify (y Express) proporcionan una funcionalidad mucho más profunda, como definir los tipos de aplicación y proporcionar un enrutamiento complejo en distintos puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="13529-266">Restify (and Express) provide much deeper functionality, such as defining application types and providing complex routing across different endpoints.</span></span> <span data-ttu-id="13529-267">Estas rutas van a ser simples.</span><span class="sxs-lookup"><span data-stu-id="13529-267">For our purposes, we are keeping these routes simple.</span></span>

### <a name="add-default-routes-tooour-server"></a><span data-ttu-id="13529-268">Agregar servidor de forma predeterminada las rutas tooour</span><span class="sxs-lookup"><span data-stu-id="13529-268">Add default routes tooour server</span></span>
<span data-ttu-id="13529-269">Ahora agregar hello básico CRUD de las rutas de crear, recuperar, actualizar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="13529-269">We now add hello basic CRUD routes of Create, Retrieve, Update, and Delete.</span></span>

1. <span data-ttu-id="13529-270">Desde la línea de comandos de hello, cambiar directorios toohello **organización** carpeta si no está ya no existe:</span><span class="sxs-lookup"><span data-stu-id="13529-270">From hello command line, change directories toohello **azuread** folder if you're not already there:</span></span>

    `cd azuread`

2. <span data-ttu-id="13529-271">Abra hello `server.js` un archivo en el editor que prefiera y después agregue Hola siguiendo la información que aparece debajo de hello base de datos las entradas anteriores que haya realizado:</span><span class="sxs-lookup"><span data-stu-id="13529-271">Open hello `server.js` file in your favorite editor, and then add hello following information below hello previous database entries that you made:</span></span>

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it tooMongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
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

/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Did you initialize hello database as stated in hello README?");
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

### <a name="add-error-handling-in-our-apis"></a><span data-ttu-id="13529-272">Incorporación del control de errores a nuestras API</span><span class="sxs-lookup"><span data-stu-id="13529-272">Add error handling in our APIs</span></span>
```

///--- Errors for communicating something interesting back toohello client.

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


## <a name="step-15-create-your-server"></a><span data-ttu-id="13529-273">Paso 15: Creación de un servidor</span><span class="sxs-lookup"><span data-stu-id="13529-273">Step 15: Create your server</span></span>
<span data-ttu-id="13529-274">Hemos definido la base de datos y las rutas están en su lugar.</span><span class="sxs-lookup"><span data-stu-id="13529-274">We have defined our database and our routes are in place.</span></span> <span data-ttu-id="13529-275">Hola última cosa toodo es agregar instancia del servidor hello que administra las llamadas.</span><span class="sxs-lookup"><span data-stu-id="13529-275">hello last thing toodo is add hello server instance that manages our calls.</span></span>

<span data-ttu-id="13529-276">Restify (y Express) puede hacer una gran cantidad de personalización de un servidor de la API de REST, pero nuevo vamos toouse hello más básico el programa de instalación para nuestros propósitos.</span><span class="sxs-lookup"><span data-stu-id="13529-276">In Restify (and Express) you can do a lot of customization for a REST API server, but again we are going toouse hello most basic setup for our purposes.</span></span>

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst too10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping tooREST.
```

## <a name="step-16-add-hello-routes-toohello-server-without-authentication-for-now"></a><span data-ttu-id="13529-277">Paso 16: Agregar servidor de toohello de rutas de hello (sin autenticación por ahora)</span><span class="sxs-lookup"><span data-stu-id="13529-277">Step 16: Add hello routes toohello server (without authentication for now)</span></span>
```Javascript
/// Now hello real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In hello pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need toomaintain session state. You can experiment with removing API protection
/* by removing hello passport.authenticate() method as follows:
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
// Register a default '/' handler.
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

## <a name="step-17-run-hello-server-before-adding-oauth-support"></a><span data-ttu-id="13529-278">Paso 17: Ejecutar servidor hello (antes de agregar compatibilidad con OAuth)</span><span class="sxs-lookup"><span data-stu-id="13529-278">Step 17: Run hello server (before adding OAuth support)</span></span>
<span data-ttu-id="13529-279">Pruebe el servidor antes de agregar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="13529-279">Test out your server before we add authentication.</span></span>

<span data-ttu-id="13529-280">Hola tootest de manera más fácil el servidor está utilizando curl en una línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="13529-280">hello easiest way tootest your server is by using curl in a command line.</span></span> <span data-ttu-id="13529-281">Antes de hacerlo, necesitamos una utilidad que nos permite tooparse salida como JSON.</span><span class="sxs-lookup"><span data-stu-id="13529-281">Before we do that, we need a utility that allows us tooparse output as JSON.</span></span>

1. <span data-ttu-id="13529-282">Instalar Hola después de la herramienta JSON (Hola todos los ejemplos siguientes usa esta herramienta):</span><span class="sxs-lookup"><span data-stu-id="13529-282">Install hello following JSON tool (all hello following examples use this tool):</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="13529-283">Esto instala herramienta JSON de hello globalmente.</span><span class="sxs-lookup"><span data-stu-id="13529-283">This installs hello JSON tool globally.</span></span> <span data-ttu-id="13529-284">Ahora que nos hemos realizado, vamos a reproducir con servidor hello:</span><span class="sxs-lookup"><span data-stu-id="13529-284">Now that we’ve accomplished that, let’s play with hello server:</span></span>

2. <span data-ttu-id="13529-285">En primer lugar, asegúrese de que se ejecuta la instancia de MongoDB:</span><span class="sxs-lookup"><span data-stu-id="13529-285">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

3. <span data-ttu-id="13529-286">A continuación, cambie el directorio de toohello e iniciar volver una:</span><span class="sxs-lookup"><span data-stu-id="13529-286">Then, change toohello directory and start curling:</span></span>

    <span data-ttu-id="13529-287">`$ cd azuread``$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="13529-287">`$ cd azuread` `$ node server.js`</span></span>

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
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

4. <span data-ttu-id="13529-288">A continuación, podemos agregar una tarea de este modo:</span><span class="sxs-lookup"><span data-stu-id="13529-288">Then, we can add a task this way:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    <span data-ttu-id="13529-289">respuesta de Hello debe ser:</span><span class="sxs-lookup"><span data-stu-id="13529-289">hello response should be:</span></span>

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
    <span data-ttu-id="13529-290">Además, podemos mostrar tareas de Brandon así:</span><span class="sxs-lookup"><span data-stu-id="13529-290">And we can list tasks for Brandon this way:</span></span>

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="13529-291">Si todo esto funciona, se dispone de un servidor de la API de REST de listo tooadd OAuth toohello.</span><span class="sxs-lookup"><span data-stu-id="13529-291">If all this works, we're ready tooadd OAuth toohello REST API server.</span></span>

<span data-ttu-id="13529-292">Tiene un servidor de API de REST con MongoDB</span><span class="sxs-lookup"><span data-stu-id="13529-292">You have a REST API server with MongoDB!</span></span>

## <a name="step-18-add-authentication-tooour-rest-api-server"></a><span data-ttu-id="13529-293">Paso 18: Agregar servidor de la API de REST de autenticación tooour</span><span class="sxs-lookup"><span data-stu-id="13529-293">Step 18: Add authentication tooour REST API server</span></span>
<span data-ttu-id="13529-294">Ahora que tenemos una API de REST en ejecución, podemos empezar a darle una utilidad con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13529-294">Now that we have a running REST API, let's start making it useful with Azure AD.</span></span>

<span data-ttu-id="13529-295">Desde la línea de comandos de hello, cambiar directorios toohello **organización** carpeta si no está ya no existe.</span><span class="sxs-lookup"><span data-stu-id="13529-295">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="13529-296">Usar hello OIDCBearerStrategy que se incluye con azure de passport de ad</span><span class="sxs-lookup"><span data-stu-id="13529-296">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
<span data-ttu-id="13529-297">Hasta ahora hemos creado un servidor típico de TODO de REST sin ningún tipo de autorización.</span><span class="sxs-lookup"><span data-stu-id="13529-297">So far we have built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="13529-298">Finalmente, empezamos a prepararlo.</span><span class="sxs-lookup"><span data-stu-id="13529-298">This is where we start putting that together.</span></span>

1. <span data-ttu-id="13529-299">En primer lugar, necesitamos tooindicate que deseamos toouse Passport.</span><span class="sxs-lookup"><span data-stu-id="13529-299">First, we need tooindicate that we want toouse Passport.</span></span> <span data-ttu-id="13529-300">Incluya esto justo después de la otra configuración del servidor:</span><span class="sxs-lookup"><span data-stu-id="13529-300">Put this right after your other server configuration:</span></span>

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > <span data-ttu-id="13529-301">No se puede suplantar al escribir las API, es recomendable que vincule siempre Hola datos toosomething único del token de Hola que Hola de usuario.</span><span class="sxs-lookup"><span data-stu-id="13529-301">When you write APIs, we recommend that you always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="13529-302">Cuando este servidor almacena elementos de lista de tareas, almacena en función de hello Id. de objeto de usuario de hello en el token de hello (llamado a través de token.oid), que colocamos cuando nos en el campo de "propietario" Hola.</span><span class="sxs-lookup"><span data-stu-id="13529-302">When this server stores TODO items, it stores them based on hello object ID of hello user in hello token (called through token.oid), which we put in hello “owner” field.</span></span> <span data-ttu-id="13529-303">Esto garantiza que ese usuario es el único que puede acceder a sus tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="13529-303">This ensures that only that user can access their TODOs.</span></span> <span data-ttu-id="13529-304">No hay ningún riesgo en hello API de "propietario", por lo que un usuario externo puede solicitar Hola TODOs de los demás incluso si se autentican en.</span><span class="sxs-lookup"><span data-stu-id="13529-304">There is no exposure in hello API of “owner,” so an external user can request hello TODOs of others even if they are authenticated.</span></span>                    

2. <span data-ttu-id="13529-305">Siguiente vamos a usar la estrategia de portador de Hola que viene con `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="13529-305">Next let’s use hello bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="13529-306">Examine el código de hello por ahora y explicaremos rest hello en breve.</span><span class="sxs-lookup"><span data-stu-id="13529-306">Look at hello code for now and we'll explain hello rest shortly.</span></span> <span data-ttu-id="13529-307">Colóquelo después de lo que pegó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="13529-307">Put this after what you pasted above:</span></span>

```Javascript
    /**
    /*
    /* Calling hello OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides hello need toomanage users and info tokens
    /* with a FindorCreate() method that must be provided by hello implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want toodo something smarter.
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


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying hello user');
            log.info(token, 'was hello token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

<span data-ttu-id="13529-308">Passport usa un patrón similar para todas sus estrategias (Twitter, Facebook, etc.) al que se ajustan todos los escritores de estrategias.</span><span class="sxs-lookup"><span data-stu-id="13529-308">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="13529-309">Examinando la estrategia de hello, verá que pasamos una función que tiene un token y un hecho como parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="13529-309">Looking at hello strategy, you see we pass it a function that has a token and a done as hello parameters.</span></span> <span data-ttu-id="13529-310">estrategia de Hello incluye volver toous después de que realice su trabajo.</span><span class="sxs-lookup"><span data-stu-id="13529-310">hello strategy comes back toous after it does its work.</span></span> <span data-ttu-id="13529-311">Cuando lo hace, almacenamos usuario hello y token de hello complementario por lo que no necesitamos tooask para este nuevo.</span><span class="sxs-lookup"><span data-stu-id="13529-311">After it does, we store hello user and stash hello token so we won’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="13529-312">código de Hello anterior toma cualquier usuario que se produce a tooauthenticate tooour server.</span><span class="sxs-lookup"><span data-stu-id="13529-312">hello previous code takes any user that happens tooauthenticate tooour server.</span></span> <span data-ttu-id="13529-313">Esto se conoce como registro automático.</span><span class="sxs-lookup"><span data-stu-id="13529-313">This is known as auto-registration.</span></span> <span data-ttu-id="13529-314">En los servidores de producción, se recomienda no permitir que acceda nadie que no haya pasado por el proceso de registro que decida.</span><span class="sxs-lookup"><span data-stu-id="13529-314">In production servers, you we recommend that you don't let anyone in without first having them go through a registration process that you decide on.</span></span> <span data-ttu-id="13529-315">Se trata normalmente de patrón de Hola que se ven en las aplicaciones de consumidor, que le permiten tooregister con Facebook, pero a continuación, pida toofill información adicional.</span><span class="sxs-lookup"><span data-stu-id="13529-315">This is usually hello pattern you see in consumer apps, which allow you tooregister with Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="13529-316">Si esto no era un programa de línea de comandos, se pudo extrajeron correo electrónico Hola de objeto de símbolo (token) de Hola que se devuelve y, a continuación, más frecuentes Hola usuario toofill información adicional.</span><span class="sxs-lookup"><span data-stu-id="13529-316">If this wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked hello user toofill out additional information.</span></span> <span data-ttu-id="13529-317">Dado que se trata de un servidor de prueba, se debe hacer es agregar base de datos de toohello en memoria.</span><span class="sxs-lookup"><span data-stu-id="13529-317">Because this is a test server, we simply add them toohello in-memory database.</span></span>
>
>

### <a name="protect-some-endpoints"></a><span data-ttu-id="13529-318">Protección de puntos de conexión</span><span class="sxs-lookup"><span data-stu-id="13529-318">Protect some endpoints</span></span>
<span data-ttu-id="13529-319">Proteger los puntos de conexión mediante la especificación de hello `passport.authenticate()` llamada con protocolo de Hola que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="13529-319">You protect endpoints by specifying hello `passport.authenticate()` call with hello protocol that you want toouse.</span></span>

<span data-ttu-id="13529-320">toomake nuestro código de servidor hacer algo más interesante, Editar ruta Hola.</span><span class="sxs-lookup"><span data-stu-id="13529-320">toomake our server code do something more interesting, let’s edit hello route.</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a><span data-ttu-id="13529-321">Paso 19: ejecutar de nuevo su aplicación de servidor y asegurarse de que le rechaza</span><span class="sxs-lookup"><span data-stu-id="13529-321">Step 19: Run your server application again and ensure it rejects you</span></span>
<span data-ttu-id="13529-322">Vamos a usar `curl` nuevo toosee si ahora tenemos OAuth2 protección contra nuestro puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="13529-322">Let's use `curl` again toosee if we now have OAuth2 protection against our endpoints.</span></span> <span data-ttu-id="13529-323">Esta prueba se realiza antes de ejecutar cualquiera de nuestros SDK de cliente en este punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="13529-323">We do this test before running any of our client SDKs against this endpoint.</span></span> <span data-ttu-id="13529-324">Hello encabezados que se devuelven deben ser suficiente tootell nos si vamos hacia abajo de la ruta de acceso correcta de Hola.</span><span class="sxs-lookup"><span data-stu-id="13529-324">hello headers that are returned should be enough tootell us if we're going down hello right path.</span></span>

1. <span data-ttu-id="13529-325">En primer lugar, asegúrese de que se ejecuta la instancia de MongoDB:</span><span class="sxs-lookup"><span data-stu-id="13529-325">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

2. <span data-ttu-id="13529-326">A continuación, cambie el directorio de toohello e iniciar volver una.</span><span class="sxs-lookup"><span data-stu-id="13529-326">Then, change toohello directory and start curling.</span></span>

      <span data-ttu-id="13529-327">`$ cd azuread``$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="13529-327">`$ cd azuread` `$ node server.js`</span></span>

3. <span data-ttu-id="13529-328">Pruebe una operación POST básica.</span><span class="sxs-lookup"><span data-stu-id="13529-328">Try a basic POST.</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="13529-329">401 es respuesta Hola que está buscando aquí.</span><span class="sxs-lookup"><span data-stu-id="13529-329">A 401 is hello response you are looking for here.</span></span> <span data-ttu-id="13529-330">Esta respuesta indica que capa de Passport Hola está tratando de tooredirect toohello autorizado extremo, que es exactamente lo que desea.</span><span class="sxs-lookup"><span data-stu-id="13529-330">This response indicates that hello Passport layer is trying tooredirect toohello authorized endpoint, which is exactly what you want.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13529-331">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="13529-331">Next steps</span></span>
<span data-ttu-id="13529-332">Ha avanzado todo lo posible con este servidor sin usar un cliente compatible con OAuth2.</span><span class="sxs-lookup"><span data-stu-id="13529-332">You've gone as far as you can with this server without using an OAuth2 compatible client.</span></span> <span data-ttu-id="13529-333">Deberá toogo a través de un tutorial adicional.</span><span class="sxs-lookup"><span data-stu-id="13529-333">You will need toogo through an additional walkthrough.</span></span>

<span data-ttu-id="13529-334">Ahora que ha aprendido cómo tooimplement una API de REST mediante el uso de Restify y OAuth2.</span><span class="sxs-lookup"><span data-stu-id="13529-334">You've now learned how tooimplement a REST API by using Restify and OAuth2.</span></span> <span data-ttu-id="13529-335">También tiene más que suficiente tookeep código desarrollando su servicio y aprender cómo toobuild en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="13529-335">You also have more than enough code tookeep developing your service and learning how toobuild on this example.</span></span>

<span data-ttu-id="13529-336">Si está interesado en pasos de hello en su viaje AAL, presentamos algunos clientes AAL compatibles se recomienda que seguir trabajando con.</span><span class="sxs-lookup"><span data-stu-id="13529-336">If you are interested in hello next steps in your ADAL journey, here are some supported ADAL clients we recommend that you  keep working with.</span></span>

<span data-ttu-id="13529-337">Clonar la máquina del desarrollador de tooyour y configurar como se describe en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="13529-337">Clone down tooyour developer machine and configure as described in hello walkthrough.</span></span>

[<span data-ttu-id="13529-338">ADAL para iOS</span><span class="sxs-lookup"><span data-stu-id="13529-338">ADAL for iOS</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[<span data-ttu-id="13529-339">ADAL para Android</span><span class="sxs-lookup"><span data-stu-id="13529-339">ADAL for Android</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
