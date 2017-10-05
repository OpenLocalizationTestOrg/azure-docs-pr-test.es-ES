---
title: "Introducción a Node.js de Azure AD | Microsoft Docs"
description: "Compilación de una API web de REST de Node.js que se integre con Azure AD para su autenticación."
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
ms.openlocfilehash: 4f58177f540c14172d7ece8b4bc8c8a2b9787f8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a><span data-ttu-id="fa352-103">Introducción a las API web para Node.js</span><span class="sxs-lookup"><span data-stu-id="fa352-103">Get started with web APIs for Node.js</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="fa352-104">*Passport* es middleware de autenticación para Node.js.</span><span class="sxs-lookup"><span data-stu-id="fa352-104">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="fa352-105">Passport es flexible y modular, y se puede usar discretamente en cualquier aplicación web de Restify o basada en Express.</span><span class="sxs-lookup"><span data-stu-id="fa352-105">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Restify web application.</span></span> <span data-ttu-id="fa352-106">Un conjunto completo de estrategias da soporte a la autenticación con nombre de usuario y contraseña, Facebook, Twitter, etc.</span><span class="sxs-lookup"><span data-stu-id="fa352-106">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="fa352-107">Hemos desarrollado una estrategia para Microsoft Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fa352-107">We have developed a strategy for Microsoft Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="fa352-108">Instalamos este módulo y luego agregaremos el complemento `passport-azure-ad` de Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fa352-108">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="fa352-109">Para ello, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fa352-109">To do this, you need to:</span></span>

1. <span data-ttu-id="fa352-110">Registrar una aplicación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fa352-110">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="fa352-111">Configurar la aplicación para que use el complemento `passport-azure-ad` de Passport.</span><span class="sxs-lookup"><span data-stu-id="fa352-111">Set up your app to use Passport's `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="fa352-112">Configurar una aplicación cliente para llamar a la API web de la Lista de tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="fa352-112">Configure a client application to call the To Do List web API.</span></span>

<span data-ttu-id="fa352-113">El código de este tutorial se conserva [en GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span><span class="sxs-lookup"><span data-stu-id="fa352-113">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span></span>

> [!NOTE]
> <span data-ttu-id="fa352-114">En este artículo no se trata la implementación de la administración de registros, inicios de sesión y perfiles con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="fa352-114">This article doesn't cover how to implement sign-in, sign-up, or profile management with Azure AD B2C.</span></span> <span data-ttu-id="fa352-115">Se centra en la llamada a las API web después de que el usuario ya está autenticado.</span><span class="sxs-lookup"><span data-stu-id="fa352-115">It focuses on calling web APIs after the user is already authenticated.</span></span>  <span data-ttu-id="fa352-116">Para aprender los fundamentos de Azure Active Directory, se recomienda empezar por el documento [Integración con Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="fa352-116">We recommend that you start with [How to integrate with Azure Active Directory document](active-directory-how-to-integrate.md) to learn about the basics of Azure Active Directory.</span></span>
>
>

<span data-ttu-id="fa352-117">Hemos publicado todo el código fuente de este ejemplo en GitHub bajo una licencia de MIT, así que no dude en clonarlo (o mejor aún, bifurcarlo) y realizar cualquier comentarios y solicitudes de incorporación de cambios.</span><span class="sxs-lookup"><span data-stu-id="fa352-117">We've released all the source code for this running example in GitHub under an MIT license, so feel free to clone (or even better, fork), and provide feedback and pull requests.</span></span>

## <a name="about-nodejs-modules"></a><span data-ttu-id="fa352-118">Acerca de los módulos Node.js</span><span class="sxs-lookup"><span data-stu-id="fa352-118">About Node.js modules</span></span>
<span data-ttu-id="fa352-119">En este tutorial se usan módulos Node.js.</span><span class="sxs-lookup"><span data-stu-id="fa352-119">We use Node.js modules in this walkthrough.</span></span> <span data-ttu-id="fa352-120">Los módulos son paquetes JavaScript que pueden cargarse y que proporcionan una funcionalidad específica para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="fa352-120">Modules are loadable JavaScript packages that provide specific functionality for your application.</span></span> <span data-ttu-id="fa352-121">Normalmente, para instalar los módulos se usa una herramienta de línea de comandos de NPM de Node.js en el directorio de instalación de NPM.</span><span class="sxs-lookup"><span data-stu-id="fa352-121">You usually install modules by using the Node.js an NPM command-line tool in the NPM installation directory.</span></span> <span data-ttu-id="fa352-122">Sin embargo, algunos módulos, como el módulo de HTTP, se incluyen en el paquete principal de Node.js.</span><span class="sxs-lookup"><span data-stu-id="fa352-122">However, some modules, such as the HTTP module, are included in the core Node.js package.</span></span>

<span data-ttu-id="fa352-123">Los módulos instalados se guardan en el directorio **node_modules**, en la raíz del directorio de instalación de Node.js.</span><span class="sxs-lookup"><span data-stu-id="fa352-123">Installed modules are saved in the **node_modules** directory at the root of your Node.js installation directory.</span></span> <span data-ttu-id="fa352-124">En el directorio **node_modules**, cada módulo mantiene sus propio directorio **node_modules**, que contiene los módulos de los que depende.</span><span class="sxs-lookup"><span data-stu-id="fa352-124">Each module in the **node_modules** directory maintains its own **node_modules** directory that contains any modules that it depends on.</span></span> <span data-ttu-id="fa352-125">Además, cada módulo requerido tiene un directorio **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="fa352-125">Also, each required module has a **node_modules** directory.</span></span> <span data-ttu-id="fa352-126">Esta estructura de directorios recursiva representa la cadena de dependencias.</span><span class="sxs-lookup"><span data-stu-id="fa352-126">This recursive directory structure represents the dependency chain.</span></span>

<span data-ttu-id="fa352-127">Esta estructura de la cadena de dependencias da como resultado una mayor superficie de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fa352-127">This dependency chain structure results in a larger application footprint.</span></span> <span data-ttu-id="fa352-128">Pero también garantiza que se cumplen todas las dependencias y que la versión de los módulos que se usa en el desarrollo también se utiliza en producción.</span><span class="sxs-lookup"><span data-stu-id="fa352-128">But it also guarantees that all dependencies are met and that the version of the modules that's used in development is also used in production.</span></span> <span data-ttu-id="fa352-129">Esto hace que el comportamiento de la aplicación de producción sea más predecible y evita los problemas de control de versiones que pueden afectar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="fa352-129">This makes the production app behavior more predictable and prevents versioning problems that might affect users.</span></span>

## <a name="step-1-register-an-azure-ad-tenant"></a><span data-ttu-id="fa352-130">Paso 1: Registro de un inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa352-130">Step 1: Register an Azure AD tenant</span></span>
<span data-ttu-id="fa352-131">Para usar este ejemplo, se necesita un inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fa352-131">To use this sample, you need an Azure Active Directory tenant.</span></span> <span data-ttu-id="fa352-132">Si no está seguro de qué es un inquilino o de cómo obtener uno, consulte [Obtención de un inquilino de Azure Active Directory](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="fa352-132">If you're not sure what a tenant is or how to get one, see [How to get an Azure AD tenant](active-directory-howto-tenant.md).</span></span>

## <a name="step-2-create-an-application"></a><span data-ttu-id="fa352-133">Paso 2: Creación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="fa352-133">Step 2: Create an application</span></span>
<span data-ttu-id="fa352-134">A continuación, cree una aplicación en su directorio que proporcione a Azure AD la información que necesita para comunicarse de forma segura con su aplicación.</span><span class="sxs-lookup"><span data-stu-id="fa352-134">Next you create an app in your directory that gives Azure AD information that it needs to securely communicate with your app.</span></span>  <span data-ttu-id="fa352-135">Tanto la aplicación cliente como la API web se representan mediante un **identificador de aplicación** individual, ya que conforman una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="fa352-135">Both the client app and web API are represented by a single **Application ID** in this case, because they comprise one logical app.</span></span>  <span data-ttu-id="fa352-136">Para crear una aplicación, siga [estas instrucciones](active-directory-how-applications-are-added.md).</span><span class="sxs-lookup"><span data-stu-id="fa352-136">To create an app, follow [these instructions](active-directory-how-applications-are-added.md).</span></span> <span data-ttu-id="fa352-137">Si va a crear una aplicación de línea de negocio [es posible que estas instrucciones adicionales le resulten útiles](../active-directory-applications-guiding-developers-for-lob-applications.md).</span><span class="sxs-lookup"><span data-stu-id="fa352-137">If you are building a line-of-business app, [these additional instructions might be useful](../active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="fa352-138">Para crear una aplicación:</span><span class="sxs-lookup"><span data-stu-id="fa352-138">To create an application:</span></span>

1. <span data-ttu-id="fa352-139">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fa352-139">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="fa352-140">En el menú superior, seleccione su cuenta.</span><span class="sxs-lookup"><span data-stu-id="fa352-140">On the top menu, select your account.</span></span> <span data-ttu-id="fa352-141">Luego, en la lista **Directorio**, elija el inquilino de Active Directory en el que desee registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fa352-141">Then, under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>

3. <span data-ttu-id="fa352-142">En el menú de la izquierda, seleccione **Más servicios** y, después, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fa352-142">In the menu on the left, select **More Services**, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="fa352-143">Seleccione **Registros de aplicaciones** y luego seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fa352-143">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="fa352-144">Siga las indicaciones para crear una **Aplicación web o API web**.</span><span class="sxs-lookup"><span data-stu-id="fa352-144">Follow the prompts to create a **Web Application and/or WebAPI**.</span></span>

      * <span data-ttu-id="fa352-145">El **nombre** de la aplicación describe la aplicación a los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="fa352-145">The **name** of the application describes your application to end users.</span></span>

      * <span data-ttu-id="fa352-146">La **dirección URL de inicio de sesión** es la dirección URL base de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="fa352-146">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="fa352-147">La dirección URL predeterminada del código de ejemplo es `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="fa352-147">The default URL of the sample code is `https://localhost:8080`.</span></span>

6. <span data-ttu-id="fa352-148">Después de registrarse, Azure AD asigna a su aplicación un identificador de aplicación individual.</span><span class="sxs-lookup"><span data-stu-id="fa352-148">After you register, Azure AD assigns your app a unique Application ID.</span></span> <span data-ttu-id="fa352-149">Este valor se necesita en las siguientes secciones, así que cópielo de la página de aplicación.</span><span class="sxs-lookup"><span data-stu-id="fa352-149">You need this value in the next sections, so copy it from the application page.</span></span>

7. <span data-ttu-id="fa352-150">En la página **Configuración** -> **Propiedades** de la aplicación, actualice el URI del identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fa352-150">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="fa352-151">El **URI de id. de aplicación** es un identificador único de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="fa352-151">The **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="fa352-152">La convención consiste en usar `https://<tenant-domain>/<app-name>`, por ejemplo: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="fa352-152">The convention is to use `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

8. <span data-ttu-id="fa352-153">Cree un **clave** para la aplicación desde la página **Configuración** y cópiela en otro lugar.</span><span class="sxs-lookup"><span data-stu-id="fa352-153">Create a **Key** for your application from the **Settings** page, and then copy it somewhere.</span></span> <span data-ttu-id="fa352-154">La necesitará en breve.</span><span class="sxs-lookup"><span data-stu-id="fa352-154">You'll need it shortly.</span></span>

## <a name="step-3-download-nodejs-for-your-platform"></a><span data-ttu-id="fa352-155">Paso 3: Descarga de Node.js para la plataforma</span><span class="sxs-lookup"><span data-stu-id="fa352-155">Step 3: Download Node.js for your platform</span></span>
<span data-ttu-id="fa352-156">Para usar correctamente este ejemplo, debe disponer de una instalación en funcionamiento de Node.js.</span><span class="sxs-lookup"><span data-stu-id="fa352-156">To successfully use this sample, you must have a working installation of Node.js.</span></span>

<span data-ttu-id="fa352-157">Instale Node.js desde [http://nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="fa352-157">Install Node.js from [http://nodejs.org](http://nodejs.org).</span></span>

## <a name="step-4-install-mongodb-on-your-platform"></a><span data-ttu-id="fa352-158">Paso 4: Instalación de MongoDB en la plataforma</span><span class="sxs-lookup"><span data-stu-id="fa352-158">Step 4: Install MongoDB on your platform</span></span>
<span data-ttu-id="fa352-159">Para usar correctamente este ejemplo, debe disponer de una instalación en funcionamiento de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="fa352-159">To successfully use this sample, you must have a working installation of MongoDB.</span></span> <span data-ttu-id="fa352-160">MongoDB se usa para que la API de REST sea persistente en las distintas instancias del servidor.</span><span class="sxs-lookup"><span data-stu-id="fa352-160">You use MongoDB to make the REST API persistent across server instances.</span></span>

<span data-ttu-id="fa352-161">Instale MongoDB desde [http://mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="fa352-161">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="fa352-162">En este tutorial se da por supuesto que usa la instalación predeterminada y los puntos de conexión de servidor para MongoDB, que en el momento de escribir este artículo es mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="fa352-162">This walkthrough assumes that you use the default installation and server endpoints for MongoDB, which at the time of this writing is mongodb://localhost.</span></span>
>
>

## <a name="step-5-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="fa352-163">Paso 5: Instalación de los módulos Restify en su API web</span><span class="sxs-lookup"><span data-stu-id="fa352-163">Step 5: Install the Restify modules in your web API</span></span>
<span data-ttu-id="fa352-164">Vamos a usar Restify para compilar nuestra API de REST.</span><span class="sxs-lookup"><span data-stu-id="fa352-164">We are using Restify to build our REST API.</span></span> <span data-ttu-id="fa352-165">Restify es un marco de trabajo de la aplicación de Node.js mínimo y flexible que se deriva de Express.</span><span class="sxs-lookup"><span data-stu-id="fa352-165">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="fa352-166">Tiene un sólido conjunto de características para crear API de REST sobre Connect.</span><span class="sxs-lookup"><span data-stu-id="fa352-166">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="fa352-167">Instalar Restify</span><span class="sxs-lookup"><span data-stu-id="fa352-167">Install Restify</span></span>
1. <span data-ttu-id="fa352-168">Desde la línea de comandos, cambie al directorio **azuread**.</span><span class="sxs-lookup"><span data-stu-id="fa352-168">From the command line, change directories to the **azuread** directory.</span></span> <span data-ttu-id="fa352-169">Si el directorio **azuread** no existe, créelo.</span><span class="sxs-lookup"><span data-stu-id="fa352-169">If the **azuread** directory does not exist, create it.</span></span>

        `cd azuread - or- mkdir azuread; cd azuread`

2. <span data-ttu-id="fa352-170">Escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fa352-170">Type the following command:</span></span>

    `npm install restify`

    <span data-ttu-id="fa352-171">Este comando instala Restify.</span><span class="sxs-lookup"><span data-stu-id="fa352-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="fa352-172">¿Ha recibido un error?</span><span class="sxs-lookup"><span data-stu-id="fa352-172">Did you get an error?</span></span>
<span data-ttu-id="fa352-173">Si se usa NPM en algunos sistemas operativos, se puede que recibir el siguiente mensaje **Error: EPERM, chmod "/usr/local/bin/.."**</span><span class="sxs-lookup"><span data-stu-id="fa352-173">When you use NPM on some operating systems, you might receive an error that says **Error: EPERM, chmod '/usr/local/bin/..'**</span></span> <span data-ttu-id="fa352-174">y una sugerencia de que intente ejecutar la cuenta como administrador.</span><span class="sxs-lookup"><span data-stu-id="fa352-174">and a suggestion that you try running the account as an administrator.</span></span> <span data-ttu-id="fa352-175">Si esto ocurre, utilice el comando sudo para ejecutar NPM en un nivel de privilegios mayor.</span><span class="sxs-lookup"><span data-stu-id="fa352-175">If this occurs, use the sudo command to run NPM at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-regarding-dtrace"></a><span data-ttu-id="fa352-176">¿Ha recibido un error relacionado con DTRACE?</span><span class="sxs-lookup"><span data-stu-id="fa352-176">Did you get an error regarding DTRACE?</span></span>
<span data-ttu-id="fa352-177">Al instalar Restify puede que vea un error similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="fa352-177">You might see an error like this when installing Restify:</span></span>

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
<span data-ttu-id="fa352-178">Restify proporciona un mecanismo eficaz para rastrear llamadas a REST mediante DTrace.</span><span class="sxs-lookup"><span data-stu-id="fa352-178">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="fa352-179">Sin embargo, muchos sistemas operativos no tienen DTrace.</span><span class="sxs-lookup"><span data-stu-id="fa352-179">However, many operating systems do not have DTrace.</span></span> <span data-ttu-id="fa352-180">Puede omitir estos errores con seguridad.</span><span class="sxs-lookup"><span data-stu-id="fa352-180">You can safely ignore these errors.</span></span>

<span data-ttu-id="fa352-181">La salida de este comando debe ser similar a esta:</span><span class="sxs-lookup"><span data-stu-id="fa352-181">The output of this command should look similar to the following output:</span></span>

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


## <a name="step-6-install-passportjs-in-your-web-api"></a><span data-ttu-id="fa352-182">Paso 6: Instalación de Passport.js en su API web</span><span class="sxs-lookup"><span data-stu-id="fa352-182">Step 6: Install Passport.js in your web API</span></span>
<span data-ttu-id="fa352-183">[Passport](http://passportjs.org/) es middleware de autenticación para Node.js.</span><span class="sxs-lookup"><span data-stu-id="fa352-183">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span></span> <span data-ttu-id="fa352-184">Passport es flexible y modular, y se puede usar discretamente en cualquier aplicación web de Restify o basada en Express.</span><span class="sxs-lookup"><span data-stu-id="fa352-184">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Restify web application.</span></span> <span data-ttu-id="fa352-185">Un conjunto completo de estrategias da soporte a la autenticación con nombre de usuario y contraseña, Facebook, Twitter, etc.</span><span class="sxs-lookup"><span data-stu-id="fa352-185">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="fa352-186">Hemos desarrollado una estrategia para Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fa352-186">We have developed a strategy for Azure Active Directory.</span></span> <span data-ttu-id="fa352-187">Instalamos este módulo y, después, agregamos el complemento de la estrategia de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fa352-187">We install this module and then add the Azure Active Directory strategy plug-in.</span></span>

1. <span data-ttu-id="fa352-188">Desde la línea de comandos, cambie al directorio **azuread**.</span><span class="sxs-lookup"><span data-stu-id="fa352-188">From the command line, change directories to the **azuread** directory.</span></span>

2. <span data-ttu-id="fa352-189">Para instalar passport.js, escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fa352-189">To install passport.js, enter the following command :</span></span>

    `npm install passport`

    <span data-ttu-id="fa352-190">La salida del comando debe ser similar a esta:</span><span class="sxs-lookup"><span data-stu-id="fa352-190">The output of the command should look similar to the following:</span></span>

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="fa352-191">Paso 7: Incorporación de Passport-Azure-AD a su API web</span><span class="sxs-lookup"><span data-stu-id="fa352-191">Step 7: Add Passport-Azure-AD to your web API</span></span>
<span data-ttu-id="fa352-192">A continuación, se agrega la estrategia de OAuth mediante `passport-azure-ad`, un conjunto de estrategias que conectan Azure Active Directory a Passport.</span><span class="sxs-lookup"><span data-stu-id="fa352-192">Next we add the OAuth strategy by using `passport-azure-ad`, a suite of strategies that connect Azure Active Directory to Passport.</span></span> <span data-ttu-id="fa352-193">En este ejemplo de API de REST, esta estrategia se usa para los tokens de portador.</span><span class="sxs-lookup"><span data-stu-id="fa352-193">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="fa352-194">Aunque OAuth2 proporciona un marco en el que se puede emitir cualquier tipo de token conocido, habitualmente solo se usan determinados tipos de token.</span><span class="sxs-lookup"><span data-stu-id="fa352-194">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types are commonly used.</span></span> <span data-ttu-id="fa352-195">Los tokens de portador son los que más se usan para proteger los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="fa352-195">Bearer tokens are the most commonly used tokens for protecting endpoints.</span></span> <span data-ttu-id="fa352-196">Son el tipo de token más emitido en OAuth2.</span><span class="sxs-lookup"><span data-stu-id="fa352-196">They are the most widely issued type of token in OAuth2.</span></span> <span data-ttu-id="fa352-197">Muchas implementaciones asumen que los tokens de portador son el único tipo de token que se emite.</span><span class="sxs-lookup"><span data-stu-id="fa352-197">Many implementations assume that bearer tokens are the only type of tokens that are issued.</span></span>
>
>

<span data-ttu-id="fa352-198">Desde la línea de comandos, cambie al directorio **azuread**.</span><span class="sxs-lookup"><span data-stu-id="fa352-198">From the command line, change directories to the **azuread** directory.</span></span>

<span data-ttu-id="fa352-199">Escriba el siguiente comando para instalar el módulo `passport-azure-ad module` de Passport.js:</span><span class="sxs-lookup"><span data-stu-id="fa352-199">Type the following command to install the Passport.js `passport-azure-ad module`:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="fa352-200">La salida del comando debe ser similar a esta:</span><span class="sxs-lookup"><span data-stu-id="fa352-200">The output of the command should look similar to the following output:</span></span>


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



## <a name="step-8-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="fa352-201">Paso 8: Incorporación de módulos MongoDB a su API web</span><span class="sxs-lookup"><span data-stu-id="fa352-201">Step 8: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="fa352-202">MongoDB se usa como almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="fa352-202">We use MongoDB as our datastore.</span></span> <span data-ttu-id="fa352-203">Por eso, es preciso instalar el complemento ampliamente utilizado denominado Mongoose para administrar los modelos y esquemas.</span><span class="sxs-lookup"><span data-stu-id="fa352-203">For that reason, we need to install the widely used plug-in called Mongoose to manage models and schemas.</span></span> <span data-ttu-id="fa352-204">También es necesario instalar al controlador de base de datos para MongoDB (que también se denomina MongoDB).</span><span class="sxs-lookup"><span data-stu-id="fa352-204">We also need to install the database driver for MongoDB (which is also called MongoDB).</span></span>

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a><span data-ttu-id="fa352-205">Paso 9: Instalación de módulos adicionales</span><span class="sxs-lookup"><span data-stu-id="fa352-205">Step 9: Install additional modules</span></span>
<span data-ttu-id="fa352-206">A continuación, se instalaran los restantes módulos requeridos.</span><span class="sxs-lookup"><span data-stu-id="fa352-206">Next we install the remaining required modules.</span></span>

1. <span data-ttu-id="fa352-207">Desde la línea de comandos, cambie el directorio a la carpeta **azuread**, en caso de que no se encuentre ya en ella.</span><span class="sxs-lookup"><span data-stu-id="fa352-207">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="fa352-208">Escriba los siguientes comandos para instalar estos módulos en su directorio **node_modules**:</span><span class="sxs-lookup"><span data-stu-id="fa352-208">Enter the following commands to install these modules in your **node_modules** directory:</span></span>

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a><span data-ttu-id="fa352-209">Paso 10: Creación de server.js con sus dependencias</span><span class="sxs-lookup"><span data-stu-id="fa352-209">Step 10: Create a server.js with your dependencies</span></span>
<span data-ttu-id="fa352-210">El archivo server.js proporciona la mayor parte de la funcionalidad de nuestro servidor de API web.</span><span class="sxs-lookup"><span data-stu-id="fa352-210">The server.js file provides most of the functionality for our web API server.</span></span> <span data-ttu-id="fa352-211">La mayoría del código se agrega a este archivo.</span><span class="sxs-lookup"><span data-stu-id="fa352-211">We add most of our code to this file.</span></span> <span data-ttu-id="fa352-212">Para la producción, se recomienda refactorizar la funcionalidad en archivos más pequeños, como controladores y rutas independientes.</span><span class="sxs-lookup"><span data-stu-id="fa352-212">For production purposes, we recommend that you refactor the functionality into smaller files, such as separate routes and controllers.</span></span> <span data-ttu-id="fa352-213">En esta demostración, se usa server.js para esta funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="fa352-213">In this demo, we use server.js for this functionality.</span></span>

1. <span data-ttu-id="fa352-214">Desde la línea de comandos, cambie el directorio a la carpeta **azuread**, en caso de que no se encuentre ya en ella.</span><span class="sxs-lookup"><span data-stu-id="fa352-214">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="fa352-215">Cree un archivo `server.js` en el editor que prefiera y agregue la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="fa352-215">Create a `server.js` file in your favorite editor, and then add the following information:</span></span>

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

3. <span data-ttu-id="fa352-216">Guarde el archivo .</span><span class="sxs-lookup"><span data-stu-id="fa352-216">Save the file.</span></span> <span data-ttu-id="fa352-217">Volveremos a él en breve.</span><span class="sxs-lookup"><span data-stu-id="fa352-217">We'll return to it shortly.</span></span>

## <a name="step-11-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="fa352-218">Paso 11: Creación de un archivo de configuración para almacenar la configuración de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa352-218">Step 11: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="fa352-219">Este archivo de código pasa los parámetros de configuración desde el Portal de Azure Active Directory a Passport.js.</span><span class="sxs-lookup"><span data-stu-id="fa352-219">This code file passes the configuration parameters from your Azure Active Directory portal to Passport.js.</span></span> <span data-ttu-id="fa352-220">Estos valores de configuración se crearon al agregar la API web al portal en la primera parte del tutorial.</span><span class="sxs-lookup"><span data-stu-id="fa352-220">You created these configuration values when you added the web API to the portal in the first part of the walkthrough.</span></span> <span data-ttu-id="fa352-221">Explicamos qué incluir en los valores de estos parámetros después de haber copiado el código.</span><span class="sxs-lookup"><span data-stu-id="fa352-221">We explain what to put in the values of these parameters after you copy the code.</span></span>

1. <span data-ttu-id="fa352-222">Desde la línea de comandos, cambie el directorio a la carpeta **azuread**, en caso de que no se encuentre ya en ella.</span><span class="sxs-lookup"><span data-stu-id="fa352-222">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="fa352-223">Cree un archivo `config.js` en el editor que prefiera y agregue la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="fa352-223">Create a `config.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in to your server unless you use the common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in to your server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes to stderr in Unix.

         };
    ```
3. <span data-ttu-id="fa352-224">Guarde el archivo .</span><span class="sxs-lookup"><span data-stu-id="fa352-224">Save the file.</span></span>

## <a name="step-12-add-configuration-values-to-your-serverjs-file"></a><span data-ttu-id="fa352-225">Paso 12: Incorporación de valores de configuración a su archivo server.js</span><span class="sxs-lookup"><span data-stu-id="fa352-225">Step 12: Add configuration values to your server.js file</span></span>
<span data-ttu-id="fa352-226">Estos valores se deben leer del archivo .config que creó en nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="fa352-226">We need to read these values from the .config file that you created across our application.</span></span> <span data-ttu-id="fa352-227">Para ello, agregamos el archivo .config como un recurso necesario a nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="fa352-227">To do this, we add the .config file as a required resource in our application.</span></span> <span data-ttu-id="fa352-228">Luego, establecemos las variables globales que coincidan con las variables del documento config.js.</span><span class="sxs-lookup"><span data-stu-id="fa352-228">Then we set the global variables to match the variables in the config.js document.</span></span>

1. <span data-ttu-id="fa352-229">Desde la línea de comandos, cambie el directorio a la carpeta **azuread**, en caso de que no se encuentre ya en ella.</span><span class="sxs-lookup"><span data-stu-id="fa352-229">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="fa352-230">Abra el archivo `server.js` en el editor que prefiera y agregue la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="fa352-230">Open your `server.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```
3. <span data-ttu-id="fa352-231">Después, agregue una nueva sección a `server.js` con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="fa352-231">Then add a new section to `server.js` with the following code:</span></span>

    ```Javascript
    var options = {
        // The URL of the metadata document for your app. We will put the keys for token validation from the URL found in the jwks_uri tag of the in the metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array to hold logged in users and the current logged in user (owner).
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

      // If the logging level is specified, switch to it.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. <span data-ttu-id="fa352-232">Guarde el archivo .</span><span class="sxs-lookup"><span data-stu-id="fa352-232">Save the file.</span></span>

## <a name="step-13-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="fa352-233">Paso 13: Incorporación del modelo MongoDB y la información del esquema mediante Mongoose</span><span class="sxs-lookup"><span data-stu-id="fa352-233">Step 13: Add The MongoDB Model and schema information by using Mongoose</span></span>
<span data-ttu-id="fa352-234">Ahora toda esta preparación va a empezar a dar sus frutos cuando combinemos estos tres archivos en un servicio API de REST.</span><span class="sxs-lookup"><span data-stu-id="fa352-234">Now all this preparation is going to start paying off as we combine these three files into a REST API service.</span></span>

<span data-ttu-id="fa352-235">En este tutorial, usamos MongoDB para almacenar nuestras tareas, como se describe en el Paso 4.</span><span class="sxs-lookup"><span data-stu-id="fa352-235">For this walkthrough, we use MongoDB to store our tasks as discussed in Step 4.</span></span>

<span data-ttu-id="fa352-236">En el archivo `config.js`, que creamos en el Paso 11, llamamos a nuestra base de datos `tasklist`, ya que fue lo que incluimos al final de nuestra dirección URL de conexión **mongoose_auth_local**.</span><span class="sxs-lookup"><span data-stu-id="fa352-236">In the `config.js` file that we created in Step 11, we called our database `tasklist`, because that was what we put at the end of our **mogoose_auth_local** connection URL.</span></span> <span data-ttu-id="fa352-237">No es necesario crear esta base de datos por anticipado en MongoDB.</span><span class="sxs-lookup"><span data-stu-id="fa352-237">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="fa352-238">En su lugar, MongoDB la crea automáticamente la primera vez que se ejecuta nuestra aplicación de servidor (en caso de que la base de datos no exista).</span><span class="sxs-lookup"><span data-stu-id="fa352-238">Instead, MongoDB creates this for us on the first run of our server application (assuming that the database doesn't already exist).</span></span>

<span data-ttu-id="fa352-239">Ahora que hemos indicado al servidor la base de datos MongoDB que deseamos usar, debemos escribir código adicional para crear el modelo y esquema de las tareas de nuestro servidor.</span><span class="sxs-lookup"><span data-stu-id="fa352-239">Now that we've told the server which MongoDB database we'd like to use, we need to write some additional code to create the model and schema for our server's tasks.</span></span>

### <a name="discussion-of-the-model"></a><span data-ttu-id="fa352-240">Análisis del modelo</span><span class="sxs-lookup"><span data-stu-id="fa352-240">Discussion of the model</span></span>
<span data-ttu-id="fa352-241">Nuestro modelo de esquema es muy sencillo.</span><span class="sxs-lookup"><span data-stu-id="fa352-241">Our schema model is simple.</span></span> <span data-ttu-id="fa352-242">Expándalo si fuera necesario.</span><span class="sxs-lookup"><span data-stu-id="fa352-242">You expand it as required.</span></span>

<span data-ttu-id="fa352-243">NAME: el nombre de la persona a la que se asigna a la tarea.</span><span class="sxs-lookup"><span data-stu-id="fa352-243">NAME: The name of the person who is assigned to the task.</span></span> <span data-ttu-id="fa352-244">Un valor de **cadena**.</span><span class="sxs-lookup"><span data-stu-id="fa352-244">A **String**.</span></span>

<span data-ttu-id="fa352-245">TASK: la propia tarea.</span><span class="sxs-lookup"><span data-stu-id="fa352-245">TASK: The task itself.</span></span> <span data-ttu-id="fa352-246">Un valor de **cadena**.</span><span class="sxs-lookup"><span data-stu-id="fa352-246">A **String**.</span></span>

<span data-ttu-id="fa352-247">DATE: la fecha en que vence la tarea.</span><span class="sxs-lookup"><span data-stu-id="fa352-247">DATE: The date that the task is due.</span></span> <span data-ttu-id="fa352-248">Un valor **DATETIME**.</span><span class="sxs-lookup"><span data-stu-id="fa352-248">A **DATETIME**.</span></span>

<span data-ttu-id="fa352-249">COMPLETED: si la tarea se ha completado, o no.</span><span class="sxs-lookup"><span data-stu-id="fa352-249">COMPLETED: If the task has been completed or not.</span></span> <span data-ttu-id="fa352-250">Un valor **booleano**.</span><span class="sxs-lookup"><span data-stu-id="fa352-250">A **BOOLEAN**.</span></span>

### <a name="creating-the-schema-in-the-code"></a><span data-ttu-id="fa352-251">Creación del esquema en el código</span><span class="sxs-lookup"><span data-stu-id="fa352-251">Creating the schema in the code</span></span>
1. <span data-ttu-id="fa352-252">Desde la línea de comandos, cambie el directorio a la carpeta **azuread**, en caso de que no se encuentre ya en ella.</span><span class="sxs-lookup"><span data-stu-id="fa352-252">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="fa352-253">Abra el archivo `server.js` en el editor que prefiera y agregue la siguiente información debajo de la entrada de configuración:</span><span class="sxs-lookup"><span data-stu-id="fa352-253">Open your `server.js` file in your favorite editor, and then add the following information below the configuration entry:</span></span>

    ```Javascript
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema to store our tasks and users. It's a fairly simple schema for now.
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
<span data-ttu-id="fa352-254">Como puede imaginar por el código, primero se crea un esquema.</span><span class="sxs-lookup"><span data-stu-id="fa352-254">As you can tell from the code, we create our schema first.</span></span> <span data-ttu-id="fa352-255">Después se crea un objeto de modelo que se usa para almacenar los datos en el código cuando se definen las **rutas**.</span><span class="sxs-lookup"><span data-stu-id="fa352-255">Then we create a model object that we use to store our data throughout the code when we define our **Routes**.</span></span>

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a><span data-ttu-id="fa352-256">Paso 14: Adición de rutas para el servidor de API de REST de la tarea</span><span class="sxs-lookup"><span data-stu-id="fa352-256">Step 14: Add our routes for our task REST API server</span></span>
<span data-ttu-id="fa352-257">Ahora que tenemos un modelo de base de datos con el que trabajar, agreguemos las rutas que vamos a usar para nuestro servidor de API de REST.</span><span class="sxs-lookup"><span data-stu-id="fa352-257">Now that we have a database model to work with, let's add the routes we are going use for our REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="fa352-258">Información acerca de las rutas en Restify</span><span class="sxs-lookup"><span data-stu-id="fa352-258">About routes in Restify</span></span>
<span data-ttu-id="fa352-259">Las rutas funcionan en Restify de la misma forma que en la pila de Express.</span><span class="sxs-lookup"><span data-stu-id="fa352-259">Routes work in Restify the same way they do in the Express stack.</span></span> <span data-ttu-id="fa352-260">Defina rutas mediante el URI al que espera que llamen las aplicaciones cliente.</span><span class="sxs-lookup"><span data-stu-id="fa352-260">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="fa352-261">Normalmente, las rutas se definen en un archivo independiente.</span><span class="sxs-lookup"><span data-stu-id="fa352-261">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="fa352-262">Para nuestros propósitos, las rutas las ponemos en el archivo server.js.</span><span class="sxs-lookup"><span data-stu-id="fa352-262">For our purposes, we put our routes in the server.js file.</span></span> <span data-ttu-id="fa352-263">Se recomienda factorizarlas en su propio archivo para que se puedan usar en producción.</span><span class="sxs-lookup"><span data-stu-id="fa352-263">We recommend that you factor these routes into their own file for production use.</span></span>

<span data-ttu-id="fa352-264">Este es un patrón típico de una ruta de Restify:</span><span class="sxs-lookup"><span data-stu-id="fa352-264">A typical pattern for a Restify route is as follows:</span></span>

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep the server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


<span data-ttu-id="fa352-265">Este es el patrón en su nivel más básico.</span><span class="sxs-lookup"><span data-stu-id="fa352-265">This is the pattern at its most basic level.</span></span> <span data-ttu-id="fa352-266">Restify (y Express) proporcionan una funcionalidad mucho más profunda, como definir los tipos de aplicación y proporcionar un enrutamiento complejo en distintos puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="fa352-266">Restify (and Express) provide much deeper functionality, such as defining application types and providing complex routing across different endpoints.</span></span> <span data-ttu-id="fa352-267">Estas rutas van a ser simples.</span><span class="sxs-lookup"><span data-stu-id="fa352-267">For our purposes, we are keeping these routes simple.</span></span>

### <a name="add-default-routes-to-our-server"></a><span data-ttu-id="fa352-268">Agregar rutas predeterminadas a nuestro servidor</span><span class="sxs-lookup"><span data-stu-id="fa352-268">Add default routes to our server</span></span>
<span data-ttu-id="fa352-269">Ahora se agregan las rutas CRUD básicas de Create, Retrieve, Update y Delete.</span><span class="sxs-lookup"><span data-stu-id="fa352-269">We now add the basic CRUD routes of Create, Retrieve, Update, and Delete.</span></span>

1. <span data-ttu-id="fa352-270">Desde la línea de comandos, cambie el directorio a la carpeta **azuread**, en caso de que no se encuentre ya en ella:</span><span class="sxs-lookup"><span data-stu-id="fa352-270">From the command line, change directories to the **azuread** folder if you're not already there:</span></span>

    `cd azuread`

2. <span data-ttu-id="fa352-271">Abra el archivo `server.js` en el editor que prefiera y agregue la siguiente información debajo de las anteriores entradas de base de datos que creó:</span><span class="sxs-lookup"><span data-stu-id="fa352-271">Open the `server.js` file in your favorite editor, and then add the following information below the previous database entries that you made:</span></span>

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you to set default headers.
    // These headers comply with CORS and allow us to mongodbServer our response to any origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it to Mongodb.
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

/// Simple returns the list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you to set default headers.
    // These headers comply with CORS and allow us to mongodbServer our response to any origin.

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
            log.warn(err, "There is no tasks in the database. Did you initialize the database as stated in the README?");
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

### <a name="add-error-handling-in-our-apis"></a><span data-ttu-id="fa352-272">Incorporación del control de errores a nuestras API</span><span class="sxs-lookup"><span data-stu-id="fa352-272">Add error handling in our APIs</span></span>
```

///--- Errors for communicating something interesting back to the client.

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


## <a name="step-15-create-your-server"></a><span data-ttu-id="fa352-273">Paso 15: Creación de un servidor</span><span class="sxs-lookup"><span data-stu-id="fa352-273">Step 15: Create your server</span></span>
<span data-ttu-id="fa352-274">Hemos definido la base de datos y las rutas están en su lugar.</span><span class="sxs-lookup"><span data-stu-id="fa352-274">We have defined our database and our routes are in place.</span></span> <span data-ttu-id="fa352-275">Lo último que hay que hacer es agregar la instancia del servidor que administra las llamadas.</span><span class="sxs-lookup"><span data-stu-id="fa352-275">The last thing to do is add the server instance that manages our calls.</span></span>

<span data-ttu-id="fa352-276">En Restify (y Express) se puede personalizar mucho un servidor de API de REST, pero vamos a volver a usar la configuración más básica.</span><span class="sxs-lookup"><span data-stu-id="fa352-276">In Restify (and Express) you can do a lot of customization for a REST API server, but again we are going to use the most basic setup for our purposes.</span></span>

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

// Allow five requests per second by IP, and burst to 10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use the common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping to REST.
```

## <a name="step-16-add-the-routes-to-the-server-without-authentication-for-now"></a><span data-ttu-id="fa352-277">Paso 16: Adición de las rutas al servidor (sin autenticación por ahora)</span><span class="sxs-lookup"><span data-stu-id="fa352-277">Step 16: Add the routes to the server (without authentication for now)</span></span>
```Javascript
/// Now the real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In the pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need to maintain session state. You can experiment with removing API protection
/* by removing the passport.authenticate() method as follows:
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
consoleMessage += '\n Open your browser to %s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```

## <a name="step-17-run-the-server-before-adding-oauth-support"></a><span data-ttu-id="fa352-278">Paso 17: Ejecución del servidor (antes de agregar la compatibilidad con OAuth)</span><span class="sxs-lookup"><span data-stu-id="fa352-278">Step 17: Run the server (before adding OAuth support)</span></span>
<span data-ttu-id="fa352-279">Pruebe el servidor antes de agregar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="fa352-279">Test out your server before we add authentication.</span></span>

<span data-ttu-id="fa352-280">La forma más fácil de probarlo es usar curl en una línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="fa352-280">The easiest way to test your server is by using curl in a command line.</span></span> <span data-ttu-id="fa352-281">Antes de hacerlo, necesitamos una utilidad que nos permita analizar el resultado como JSON.</span><span class="sxs-lookup"><span data-stu-id="fa352-281">Before we do that, we need a utility that allows us to parse output as JSON.</span></span>

1. <span data-ttu-id="fa352-282">Instale la siguiente herramienta JSON (en todos los ejemplos siguientes se usa esta herramienta):</span><span class="sxs-lookup"><span data-stu-id="fa352-282">Install the following JSON tool (all the following examples use this tool):</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="fa352-283">De esta forma, se instala la herramienta JSON globalmente.</span><span class="sxs-lookup"><span data-stu-id="fa352-283">This installs the JSON tool globally.</span></span> <span data-ttu-id="fa352-284">Ahora que ya lo hemos hecho, practiquemos con el servidor:</span><span class="sxs-lookup"><span data-stu-id="fa352-284">Now that we’ve accomplished that, let’s play with the server:</span></span>

2. <span data-ttu-id="fa352-285">En primer lugar, asegúrese de que se ejecuta la instancia de MongoDB:</span><span class="sxs-lookup"><span data-stu-id="fa352-285">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

3. <span data-ttu-id="fa352-286">Después, cambie al directorio e inicie curl:</span><span class="sxs-lookup"><span data-stu-id="fa352-286">Then, change to the directory and start curling:</span></span>

    <span data-ttu-id="fa352-287">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="fa352-287">`$ cd azuread` `$ node server.js`</span></span>

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

4. <span data-ttu-id="fa352-288">A continuación, podemos agregar una tarea de este modo:</span><span class="sxs-lookup"><span data-stu-id="fa352-288">Then, we can add a task this way:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    <span data-ttu-id="fa352-289">La respuesta debe ser:</span><span class="sxs-lookup"><span data-stu-id="fa352-289">The response should be:</span></span>

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
    <span data-ttu-id="fa352-290">Además, podemos mostrar tareas de Brandon así:</span><span class="sxs-lookup"><span data-stu-id="fa352-290">And we can list tasks for Brandon this way:</span></span>

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="fa352-291">Si todo esto funciona, estamos listos para agregar OAuth al servidor de API de REST.</span><span class="sxs-lookup"><span data-stu-id="fa352-291">If all this works, we're ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="fa352-292">Tiene un servidor de API de REST con MongoDB</span><span class="sxs-lookup"><span data-stu-id="fa352-292">You have a REST API server with MongoDB!</span></span>

## <a name="step-18-add-authentication-to-our-rest-api-server"></a><span data-ttu-id="fa352-293">Paso 18: Incorporación de la autenticación al servidor de API de REST</span><span class="sxs-lookup"><span data-stu-id="fa352-293">Step 18: Add authentication to our REST API server</span></span>
<span data-ttu-id="fa352-294">Ahora que tenemos una API de REST en ejecución, podemos empezar a darle una utilidad con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fa352-294">Now that we have a running REST API, let's start making it useful with Azure AD.</span></span>

<span data-ttu-id="fa352-295">Desde la línea de comandos, cambie el directorio a la carpeta **azuread**, en caso de que no se encuentre ya en ella.</span><span class="sxs-lookup"><span data-stu-id="fa352-295">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="fa352-296">Use el elemento OIDCBearerStrategy que se incluye con passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="fa352-296">Use the OIDCBearerStrategy that is included with passport-azure-ad</span></span>
<span data-ttu-id="fa352-297">Hasta ahora hemos creado un servidor típico de TODO de REST sin ningún tipo de autorización.</span><span class="sxs-lookup"><span data-stu-id="fa352-297">So far we have built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="fa352-298">Finalmente, empezamos a prepararlo.</span><span class="sxs-lookup"><span data-stu-id="fa352-298">This is where we start putting that together.</span></span>

1. <span data-ttu-id="fa352-299">En primer lugar, necesitamos indicar que queremos usar Passport.</span><span class="sxs-lookup"><span data-stu-id="fa352-299">First, we need to indicate that we want to use Passport.</span></span> <span data-ttu-id="fa352-300">Incluya esto justo después de la otra configuración del servidor:</span><span class="sxs-lookup"><span data-stu-id="fa352-300">Put this right after your other server configuration:</span></span>

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > <span data-ttu-id="fa352-301">Al escribir las API, se recomienda vincular siempre los datos a un elemento único del token cuya identidad el usuario no pueda suplantar.</span><span class="sxs-lookup"><span data-stu-id="fa352-301">When you write APIs, we recommend that you always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="fa352-302">Cuando este servidor almacena tareas pendiente, lo hace en función del id. de objeto del usuario en el token (al que se llama a través de token.oid), que se colocó en el campo "owner".</span><span class="sxs-lookup"><span data-stu-id="fa352-302">When this server stores TODO items, it stores them based on the object ID of the user in the token (called through token.oid), which we put in the “owner” field.</span></span> <span data-ttu-id="fa352-303">Esto garantiza que ese usuario es el único que puede acceder a sus tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="fa352-303">This ensures that only that user can access their TODOs.</span></span> <span data-ttu-id="fa352-304">En la API "owner" no queda expuesto, por lo que un usuario externo puede solicitar las tareas pendientes de otros, aunque estén autenticados.</span><span class="sxs-lookup"><span data-stu-id="fa352-304">There is no exposure in the API of “owner,” so an external user can request the TODOs of others even if they are authenticated.</span></span>                    

2. <span data-ttu-id="fa352-305">A continuación, vamos a usar la estrategia de portador que viene con `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="fa352-305">Next let’s use the bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="fa352-306">Por el momento veamos el código y el resto se explicará en breve.</span><span class="sxs-lookup"><span data-stu-id="fa352-306">Look at the code for now and we'll explain the rest shortly.</span></span> <span data-ttu-id="fa352-307">Colóquelo después de lo que pegó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="fa352-307">Put this after what you pasted above:</span></span>

```Javascript
    /**
    /*
    /* Calling the OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides the need to manage users and info tokens
    /* with a FindorCreate() method that must be provided by the implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want to do something smarter.
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
            log.info('verifying the user');
            log.info(token, 'was the token retreived');
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

<span data-ttu-id="fa352-308">Passport usa un patrón similar para todas sus estrategias (Twitter, Facebook, etc.) al que se ajustan todos los escritores de estrategias.</span><span class="sxs-lookup"><span data-stu-id="fa352-308">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="fa352-309">Si se examina la estrategia, se percibe que se pasan los parámetros function, que tiene un token, y done.</span><span class="sxs-lookup"><span data-stu-id="fa352-309">Looking at the strategy, you see we pass it a function that has a token and a done as the parameters.</span></span> <span data-ttu-id="fa352-310">La estrategia se devuelve después de que realiza su trabajo.</span><span class="sxs-lookup"><span data-stu-id="fa352-310">The strategy comes back to us after it does its work.</span></span> <span data-ttu-id="fa352-311">Después de que lo haga, almacenamos el usuario y guardamos provisionalmente el token, con el fin de que no sea preciso volver a pedirlo.</span><span class="sxs-lookup"><span data-stu-id="fa352-311">After it does, we store the user and stash the token so we won’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa352-312">El código anterior toma cualquier usuario que se autentique en el servidor.</span><span class="sxs-lookup"><span data-stu-id="fa352-312">The previous code takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="fa352-313">Esto se conoce como registro automático.</span><span class="sxs-lookup"><span data-stu-id="fa352-313">This is known as auto-registration.</span></span> <span data-ttu-id="fa352-314">En los servidores de producción, se recomienda no permitir que acceda nadie que no haya pasado por el proceso de registro que decida.</span><span class="sxs-lookup"><span data-stu-id="fa352-314">In production servers, you we recommend that you don't let anyone in without first having them go through a registration process that you decide on.</span></span> <span data-ttu-id="fa352-315">Este suele ser el patrón que se observa en las aplicaciones de consumidor que le permiten registrarse con Facebook, pero que luego piden que se rellene información adicional.</span><span class="sxs-lookup"><span data-stu-id="fa352-315">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to fill out additional information.</span></span> <span data-ttu-id="fa352-316">Si no se tratara de un programa de línea de comandos, el correo electrónico se podría haber extraído del objeto de token devuelto y, a continuación, haber pedido al usuario que rellenara la información adicional.</span><span class="sxs-lookup"><span data-stu-id="fa352-316">If this wasn’t a command-line program, we could have extracted the email from the token object that is returned and then asked the user to fill out additional information.</span></span> <span data-ttu-id="fa352-317">Puesto que se trata de un servidor de prueba, simplemente los agregaremos a la base de datos en memoria.</span><span class="sxs-lookup"><span data-stu-id="fa352-317">Because this is a test server, we simply add them to the in-memory database.</span></span>
>
>

### <a name="protect-some-endpoints"></a><span data-ttu-id="fa352-318">Protección de puntos de conexión</span><span class="sxs-lookup"><span data-stu-id="fa352-318">Protect some endpoints</span></span>
<span data-ttu-id="fa352-319">Para proteger los puntos de conexión, especifique la llamada `passport.authenticate()` con el protocolo que desea utilizar.</span><span class="sxs-lookup"><span data-stu-id="fa352-319">You protect endpoints by specifying the `passport.authenticate()` call with the protocol that you want to use.</span></span>

<span data-ttu-id="fa352-320">Para que nuestro código servidor haga algo más interesante, vamos a editar la ruta.</span><span class="sxs-lookup"><span data-stu-id="fa352-320">To make our server code do something more interesting, let’s edit the route.</span></span>

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

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a><span data-ttu-id="fa352-321">Paso 19: ejecutar de nuevo su aplicación de servidor y asegurarse de que le rechaza</span><span class="sxs-lookup"><span data-stu-id="fa352-321">Step 19: Run your server application again and ensure it rejects you</span></span>
<span data-ttu-id="fa352-322">Usemos `curl` nuevamente para ver si ahora tenemos protección de OAuth2 contra nuestros extremos.</span><span class="sxs-lookup"><span data-stu-id="fa352-322">Let's use `curl` again to see if we now have OAuth2 protection against our endpoints.</span></span> <span data-ttu-id="fa352-323">Esta prueba se realiza antes de ejecutar cualquiera de nuestros SDK de cliente en este punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="fa352-323">We do this test before running any of our client SDKs against this endpoint.</span></span> <span data-ttu-id="fa352-324">Los encabezados que se devuelven deberían ser suficientes para indicarnos si seguimos el camino correcto.</span><span class="sxs-lookup"><span data-stu-id="fa352-324">The headers that are returned should be enough to tell us if we're going down the right path.</span></span>

1. <span data-ttu-id="fa352-325">En primer lugar, asegúrese de que se ejecuta la instancia de MongoDB:</span><span class="sxs-lookup"><span data-stu-id="fa352-325">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

2. <span data-ttu-id="fa352-326">Después, cambie al directorio e inicie curl.</span><span class="sxs-lookup"><span data-stu-id="fa352-326">Then, change to the directory and start curling.</span></span>

      <span data-ttu-id="fa352-327">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="fa352-327">`$ cd azuread` `$ node server.js`</span></span>

3. <span data-ttu-id="fa352-328">Pruebe una operación POST básica.</span><span class="sxs-lookup"><span data-stu-id="fa352-328">Try a basic POST.</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="fa352-329">Aquí se busca la respuesta 401.</span><span class="sxs-lookup"><span data-stu-id="fa352-329">A 401 is the response you are looking for here.</span></span> <span data-ttu-id="fa352-330">Esta respuesta indica que la capa de Passport intenta realizar la redirección al punto de conexión autorizado, que es exactamente lo que desea.</span><span class="sxs-lookup"><span data-stu-id="fa352-330">This response indicates that the Passport layer is trying to redirect to the authorized endpoint, which is exactly what you want.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa352-331">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fa352-331">Next steps</span></span>
<span data-ttu-id="fa352-332">Ha avanzado todo lo posible con este servidor sin usar un cliente compatible con OAuth2.</span><span class="sxs-lookup"><span data-stu-id="fa352-332">You've gone as far as you can with this server without using an OAuth2 compatible client.</span></span> <span data-ttu-id="fa352-333">Tendrá que seguir un tutorial adicional.</span><span class="sxs-lookup"><span data-stu-id="fa352-333">You will need to go through an additional walkthrough.</span></span>

<span data-ttu-id="fa352-334">Ya ha aprendido cómo implementar una API de REST mediante Restify y OAuth2.</span><span class="sxs-lookup"><span data-stu-id="fa352-334">You've now learned how to implement a REST API by using Restify and OAuth2.</span></span> <span data-ttu-id="fa352-335">También tiene más que suficiente código para continuar el desarrollo de su servicio y aprender a basarse en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="fa352-335">You also have more than enough code to keep developing your service and learning how to build on this example.</span></span>

<span data-ttu-id="fa352-336">Si le interesan los próximos pasos en su recorrido por ADAL, a continuación hay algunos clientes ADAL compatibles con los que le recomendamos que siga trabajando.</span><span class="sxs-lookup"><span data-stu-id="fa352-336">If you are interested in the next steps in your ADAL journey, here are some supported ADAL clients we recommend that you  keep working with.</span></span>

<span data-ttu-id="fa352-337">Clona su equipo de desarrollador y configúrelo como se describe en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="fa352-337">Clone down to your developer machine and configure as described in the walkthrough.</span></span>

[<span data-ttu-id="fa352-338">ADAL para iOS</span><span class="sxs-lookup"><span data-stu-id="fa352-338">ADAL for iOS</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[<span data-ttu-id="fa352-339">ADAL para Android</span><span class="sxs-lookup"><span data-stu-id="fa352-339">ADAL for Android</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
