---
title: "Agregar inicio de sesión a una aplicación web de Node.js para Azure B2C | Microsoft Docs"
description: "Creación de una aplicación web de Node.js que inicia la sesión de los usuarios mediante un inquilino de B2C."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: db97f84a-1f24-447b-b6d2-0265c6896b27
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 03/10/2017
ms.author: xerners
ms.openlocfilehash: c85b8f8434d1e837ac96ac63b9b37f990677ed6e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-add-sign-in-to-a-nodejs-web-app"></a><span data-ttu-id="51e4b-103">Azure AD B2C: Agregar inicio de sesión a una aplicación web de Node.js</span><span class="sxs-lookup"><span data-stu-id="51e4b-103">Azure AD B2C: Add sign-in to a Node.js web app</span></span>

<span data-ttu-id="51e4b-104">**Passport** es middleware de autenticación para Node.js.</span><span class="sxs-lookup"><span data-stu-id="51e4b-104">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="51e4b-105">Muy flexible y modular, Passport puede instalarse discretamente en cualquier aplicación web basada en Express o Restify.</span><span class="sxs-lookup"><span data-stu-id="51e4b-105">Extremely flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="51e4b-106">Un conjunto completo de estrategias admite la autenticación mediante un nombre de usuario y contraseña, Facebook, Twitter, etc.</span><span class="sxs-lookup"><span data-stu-id="51e4b-106">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="51e4b-107">Hemos desarrollado una estrategia para Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="51e4b-107">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="51e4b-108">Instalará este módulo y, después, agregará el complemento `passport-azure-ad` de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51e4b-108">You will install this module and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="51e4b-109">Para ello, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="51e4b-109">To do this, you need to:</span></span>

1. <span data-ttu-id="51e4b-110">Registrar una aplicación mediante Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51e4b-110">Register an application by using Azure AD.</span></span>
2. <span data-ttu-id="51e4b-111">Configurar la aplicación para que use el complemento `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="51e4b-111">Set up your app to use the `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="51e4b-112">Usar Passport para emitir solicitudes de inicio y cierre de sesión en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51e4b-112">Use Passport to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="51e4b-113">Imprimir los datos de usuario.</span><span class="sxs-lookup"><span data-stu-id="51e4b-113">Print user data.</span></span>

<span data-ttu-id="51e4b-114">El código de este tutorial [se mantiene en GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="51e4b-114">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span></span> <span data-ttu-id="51e4b-115">Para continuar, puede [descargar el esqueleto de la aplicación en forma de archivo .zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="51e4b-115">To follow along, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="51e4b-116">También puede clonar el esqueleto:</span><span class="sxs-lookup"><span data-stu-id="51e4b-116">You can also clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="51e4b-117">La aplicación completa se ofrece al final de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="51e4b-117">The completed application is provided at the end of this tutorial.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="51e4b-118">Obtener un directorio de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="51e4b-118">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="51e4b-119">Para poder usar Azure AD B2C, debe crear un directorio o inquilino.</span><span class="sxs-lookup"><span data-stu-id="51e4b-119">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="51e4b-120">Un directorio es un contenedor para todos los usuarios, las aplicaciones, los grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="51e4b-120">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="51e4b-121">Si aún no tiene uno, [cree un directorio B2C](active-directory-b2c-get-started.md) antes de continuar con esta guía.</span><span class="sxs-lookup"><span data-stu-id="51e4b-121">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="51e4b-122">Creación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="51e4b-122">Create an application</span></span>

<span data-ttu-id="51e4b-123">A continuación, debe crear una aplicación en su directorio B2C.</span><span class="sxs-lookup"><span data-stu-id="51e4b-123">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="51e4b-124">Esto proporciona a Azure AD la información que necesita para comunicarse de forma segura con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="51e4b-124">This gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="51e4b-125">Tanto la aplicación cliente como la API web se representarán mediante un único **identificador de aplicación**, ya que conforman una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="51e4b-125">Both the client app and web API will be represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="51e4b-126">Para crear una aplicación, siga [estas instrucciones](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="51e4b-126">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="51e4b-127">Asegúrese de:</span><span class="sxs-lookup"><span data-stu-id="51e4b-127">Be sure to:</span></span>

- <span data-ttu-id="51e4b-128">Incluir una **aplicación web**/**API web** en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="51e4b-128">Include a **web app**/**web API** in the application.</span></span>
- <span data-ttu-id="51e4b-129">Escribir `http://localhost:3000/auth/openid/return` como **Dirección URL de respuesta**.</span><span class="sxs-lookup"><span data-stu-id="51e4b-129">Enter `http://localhost:3000/auth/openid/return` as a **Reply URL**.</span></span> <span data-ttu-id="51e4b-130">Es la dirección URL predeterminada para este ejemplo de código.</span><span class="sxs-lookup"><span data-stu-id="51e4b-130">It is the default URL for this code sample.</span></span>
- <span data-ttu-id="51e4b-131">Crear un **secreto de aplicación** para la aplicación y copiarlo.</span><span class="sxs-lookup"><span data-stu-id="51e4b-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="51e4b-132">Lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="51e4b-132">You will need it later.</span></span> <span data-ttu-id="51e4b-133">Tenga en cuenta que para poder usar este valor, es preciso [incluirlo entre secuencias de escape XML](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape).</span><span class="sxs-lookup"><span data-stu-id="51e4b-133">Note that this value needs to be [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
- <span data-ttu-id="51e4b-134">Copiar el **identificador de aplicación** asignado a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="51e4b-134">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="51e4b-135">También lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="51e4b-135">You'll also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="51e4b-136">Crear sus directivas</span><span class="sxs-lookup"><span data-stu-id="51e4b-136">Create your policies</span></span>

<span data-ttu-id="51e4b-137">En Azure AD B2C, cada experiencia del usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="51e4b-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="51e4b-138">Esta aplicación contiene tres experiencias de identidad: registro, inicio de sesión e inicio de sesión mediante Facebook.</span><span class="sxs-lookup"><span data-stu-id="51e4b-138">This app contains three identity experiences: sign up, sign in, and sign in by using Facebook.</span></span> <span data-ttu-id="51e4b-139">Es necesario crear una directiva así de cada tipo, como se describe en el [artículo de referencia de las directivas](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="51e4b-139">You need to create this policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="51e4b-140">Cuando cree las tres directivas, asegúrese de:</span><span class="sxs-lookup"><span data-stu-id="51e4b-140">When you create your three policies, be sure to:</span></span>

- <span data-ttu-id="51e4b-141">Elegir el **nombre para mostrar** y los restantes atributos de registro en la directiva de registro.</span><span class="sxs-lookup"><span data-stu-id="51e4b-141">Choose the **Display name** and other sign-up attributes in your sign-up policy.</span></span>
- <span data-ttu-id="51e4b-142">Elija las notificaciones de aplicación de **nombre para mostrar** e **id. de objeto** de cada directiva.</span><span class="sxs-lookup"><span data-stu-id="51e4b-142">Choose the **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="51e4b-143">Puede elegir también otras notificaciones.</span><span class="sxs-lookup"><span data-stu-id="51e4b-143">You can choose other claims as well.</span></span>
- <span data-ttu-id="51e4b-144">Copiar el **nombre** de cada directiva después de crearla.</span><span class="sxs-lookup"><span data-stu-id="51e4b-144">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="51e4b-145">Debe tener el prefijo `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="51e4b-145">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="51e4b-146">Necesitará estos nombres de directiva más adelante.</span><span class="sxs-lookup"><span data-stu-id="51e4b-146">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="51e4b-147">Después de crear las tres directivas, está listo para compilar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="51e4b-147">After you create your three policies, you're ready to build your app.</span></span>

<span data-ttu-id="51e4b-148">Tenga en cuenta que este artículo no trata de cómo usar las directivas que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="51e4b-148">Note that this article does not cover how to use the policies you just created.</span></span> <span data-ttu-id="51e4b-149">Para obtener información acerca del funcionamiento de las directivas en Azure AD B2C, comience por el [tutorial de introducción a las aplicaciones web .NET](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="51e4b-149">To learn about how policies work in Azure AD B2C, start with the [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="add-prerequisites-to-your-directory"></a><span data-ttu-id="51e4b-150">Incorporación de requisitos previos a un directorio</span><span class="sxs-lookup"><span data-stu-id="51e4b-150">Add prerequisites to your directory</span></span>

<span data-ttu-id="51e4b-151">Desde la línea de comandos, cambie los directorios a la carpeta raíz, en caso de que no se encuentren ya en ella.</span><span class="sxs-lookup"><span data-stu-id="51e4b-151">From the command line, change directories to your root folder, if you're not already there.</span></span> <span data-ttu-id="51e4b-152">Ejecute los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="51e4b-152">Run the following commands:</span></span>

- `npm install express`
- `npm install ejs`
- `npm install ejs-locals`
- `npm install restify`
- `npm install mongoose`
- `npm install bunyan`
- `npm install assert-plus`
- `npm install passport`
- `npm install webfinger`
- `npm install body-parser`
- `npm install express-session`
- `npm install cookie-parser`

<span data-ttu-id="51e4b-153">Además, hemos usado `passport-azure-ad` para la versión preliminar en el esqueleto de la Guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="51e4b-153">In addition, we used `passport-azure-ad` for our preview in the skeleton of the Quickstart.</span></span>

- `npm install passport-azure-ad`

<span data-ttu-id="51e4b-154">Así se instalarán las bibliotecas de las que depende `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="51e4b-154">This will install the libraries that `passport-azure-ad` depends on.</span></span>

## <a name="set-up-your-app-to-use-the-passport-nodejs-strategy"></a><span data-ttu-id="51e4b-155">Configuración de una aplicación para que use la estrategia Passport-Node.js</span><span class="sxs-lookup"><span data-stu-id="51e4b-155">Set up your app to use the Passport-Node.js strategy</span></span>
<span data-ttu-id="51e4b-156">Configure el middleware Express para que use el protocolo de autenticación OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="51e4b-156">Configure the Express middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="51e4b-157">Passport se usará para emitir solicitudes de inicio y cierre de sesión, administrar sesiones de usuario y obtener información sobre los usuarios, entre otras acciones.</span><span class="sxs-lookup"><span data-stu-id="51e4b-157">Passport will be used to issue sign-in and sign-out requests, manage user sessions, and get information about users, among other actions.</span></span>

<span data-ttu-id="51e4b-158">Abra el archivo `config.js` en la raíz del proyecto y escriba los valores de configuración de la aplicación en la sección `exports.creds`.</span><span class="sxs-lookup"><span data-stu-id="51e4b-158">Open the `config.js` file in the root of the project and enter your app's configuration values in the `exports.creds` section.</span></span>
- <span data-ttu-id="51e4b-159">`clientID`: el **identificador de aplicación** asignado a la aplicación en el portal de registro.</span><span class="sxs-lookup"><span data-stu-id="51e4b-159">`clientID`: The **Application ID** assigned to your app in the registration portal.</span></span>
- <span data-ttu-id="51e4b-160">`returnURL`: el **URI de redirección** que especificó en el portal.</span><span class="sxs-lookup"><span data-stu-id="51e4b-160">`returnURL`: The **Redirect URI** you entered in the portal.</span></span>
- <span data-ttu-id="51e4b-161">`tenantName`: el nombre de inquilino de la aplicación, por ejemplo, **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="51e4b-161">`tenantName`: The tenant name of your app, for example, **contoso.onmicrosoft.com**.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="51e4b-162">Abra el archivo `app.js` en la raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="51e4b-162">Open the `app.js` file in the root of the project.</span></span> <span data-ttu-id="51e4b-163">Agregue la siguiente llamada para invocar a la estrategia `OIDCStrategy` que viene con `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="51e4b-163">Add the following call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

<span data-ttu-id="51e4b-164">Use la estrategia a la que acaba de hacer referencia para tratar las solicitudes de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="51e4b-164">Use the strategy you just referenced to handle sign-in requests.</span></span>

```JavaScript
// Use the OIDCStrategy in Passport (Section 2).
//
//   Strategies in Passport require a "validate" function that accepts
//   credentials (in this case, an OpenID identifier), and invokes a callback
//   by using a user object.
passport.use(new OIDCStrategy({
    callbackURL: config.creds.returnURL,
    realm: config.creds.realm,
    clientID: config.creds.clientID,
    oidcIssuer: config.creds.issuer,
    identityMetadata: config.creds.identityMetadata,
    skipUserProfile: config.creds.skipUserProfile,
    responseType: config.creds.responseType,
    responseMode: config.creds.responseMode,
    tenantName: config.creds.tenantName
  },
  function(iss, sub, profile, accessToken, refreshToken, done) {
    log.info('Example: Email address we received was: ', profile.email);
    // asynchronous verification, for effect...
    process.nextTick(function () {
      findByEmail(profile.email, function(err, user) {
        if (err) {
          return done(err);
        }
        if (!user) {
          // "Auto-registration"
          users.push(profile);
          return done(null, profile);
        }
        return done(null, user);
      });
    });
  }
));
```
<span data-ttu-id="51e4b-165">Passport utiliza un patrón similar para todas sus estrategias (incluidos Twitter y Facebook).</span><span class="sxs-lookup"><span data-stu-id="51e4b-165">Passport uses a similar pattern for all of its strategies (including Twitter and Facebook).</span></span> <span data-ttu-id="51e4b-166">Todos los escritores de estrategias se ajustan a este patrón.</span><span class="sxs-lookup"><span data-stu-id="51e4b-166">All strategy writers adhere to this pattern.</span></span> <span data-ttu-id="51e4b-167">Al examinar la estrategia, puede ver que se pasan `function()`, que tiene un token, y `done` como parámetros.</span><span class="sxs-lookup"><span data-stu-id="51e4b-167">When you look at the strategy, you can see that you pass it a `function()` that has a token and a `done` as the parameters.</span></span> <span data-ttu-id="51e4b-168">La estrategia regresará después de haber realizado todo el trabajo.</span><span class="sxs-lookup"><span data-stu-id="51e4b-168">The strategy comes back to you after it has done all of its work.</span></span> <span data-ttu-id="51e4b-169">Almacene el usuario y guarde provisionalmente el token para no tener que volver a solicitarlo.</span><span class="sxs-lookup"><span data-stu-id="51e4b-169">Store the user and stash the token so that you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="51e4b-170">El código anterior toma todos los usuarios a los autentica el servidor.</span><span class="sxs-lookup"><span data-stu-id="51e4b-170">The preceding code takes all users whom the server authenticates.</span></span> <span data-ttu-id="51e4b-171">Esto se conoce como registro automático.</span><span class="sxs-lookup"><span data-stu-id="51e4b-171">This is autoregistration.</span></span> <span data-ttu-id="51e4b-172">Si usa servidores de producción, no desea los usuarios accedan a ellos, a menos que hayan pasado por un proceso de registro que ha configurado.</span><span class="sxs-lookup"><span data-stu-id="51e4b-172">When you use production servers, you don’t want to let in users unless they have gone through a registration process that you have set up.</span></span> <span data-ttu-id="51e4b-173">Este patrón se puede ver a menudo en las aplicaciones de consumidor,</span><span class="sxs-lookup"><span data-stu-id="51e4b-173">You can often see this pattern in consumer apps.</span></span> <span data-ttu-id="51e4b-174">que le permiten registrarse mediante Facebook, pero luego le pedirán que rellene la información adicional.</span><span class="sxs-lookup"><span data-stu-id="51e4b-174">These allow you to register by using Facebook, but then they ask you to fill out additional information.</span></span> <span data-ttu-id="51e4b-175">Si nuestra aplicación no fuera un ejemplo, podríamos extraer una dirección de correo electrónico del objeto de token que se devuelve y luego pedir al usuario que rellene la información adicional.</span><span class="sxs-lookup"><span data-stu-id="51e4b-175">If our application wasn’t a sample, we could extract an email address from the token object that is returned, and then ask the user to fill out additional information.</span></span> <span data-ttu-id="51e4b-176">Al tratarse de un servidor de prueba, simplemente agregamos los usuarios a la base de datos en memoria.</span><span class="sxs-lookup"><span data-stu-id="51e4b-176">Because this is a test server, we simply add users to the in-memory database.</span></span>

<span data-ttu-id="51e4b-177">Agregue los métodos que le permitan realizar un seguimiento de los usuarios que han iniciado sesión, tal como requiera Passport.</span><span class="sxs-lookup"><span data-stu-id="51e4b-177">Add the methods that allow you to keep track of users who have signed in, as required by Passport.</span></span> <span data-ttu-id="51e4b-178">Esta operación incluye la serialización y deserialización de la información del usuario:</span><span class="sxs-lookup"><span data-stu-id="51e4b-178">This includes serializing and deserializing user information:</span></span>

```JavaScript

// Passport session setup. (Section 2)

//   To support persistent sign-in sessions, Passport needs to be able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing the user ID when Passport serializes a user
//   and finding the user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array to hold users who have signed in
var users = [];

var findByEmail = function(email, fn) {
  for (var i = 0, len = users.length; i < len; i++) {
    var user = users[i];
    log.info('we are using user: ', user);
    if (user.email === email) {
      return fn(null, user);
    }
  }
  return fn(null, null);
};

```

<span data-ttu-id="51e4b-179">Agregue el código para cargar el motor Express.</span><span class="sxs-lookup"><span data-stu-id="51e4b-179">Add the code to load the Express engine.</span></span> <span data-ttu-id="51e4b-180">A continuación puede ver que se utiliza el patrón `/views` y `/routes` predeterminado que proporciona Express.</span><span class="sxs-lookup"><span data-stu-id="51e4b-180">In the following, you can see that we use the default `/views` and `/routes` pattern that Express provides.</span></span>

```JavaScript

// configure Express (Section 2)

var app = express();


app.configure(function() {
  app.set('views', __dirname + '/views');
  app.set('view engine', 'ejs');
  app.use(express.logger());
  app.use(express.methodOverride());
  app.use(cookieParser());
  app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
  app.use(bodyParser.urlencoded({ extended : true }));
  // Initialize Passport!  Also use passport.session() middleware to support
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

<span data-ttu-id="51e4b-181">Agregue las rutas de `POST` que entregan las solicitudes de inicio de sesión reales al motor `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="51e4b-181">Add the `POST` routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware to authenticate the
//   request. The first step in OpenID authentication involves redirecting
//   the user to an OpenID provider. After the user is authenticated,
//   the OpenID provider redirects the user back to this application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in the Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware to authenticate the
//   request. If authentication fails, the user will be redirected back to the
//   sign-in page. Otherwise, the primary route function will be called.
//   In this example, it redirects the user to the home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware to authenticate the
//   request. If authentication fails, the user will be redirected back to the
//   sign-in page. Otherwise, the primary route function will be called.
//   In this example, it will redirect the user to the home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="51e4b-182">Uso de Passport para emitir solicitudes de inicio y cierre de sesión en Azure AD</span><span class="sxs-lookup"><span data-stu-id="51e4b-182">Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>

<span data-ttu-id="51e4b-183">Ahora, la aplicación está correctamente configurada para comunicarse con el punto de conexión v2.0 mediante el protocolo de autenticación de OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="51e4b-183">Your app is now properly configured to communicate with the v2.0 endpoint by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="51e4b-184">`passport-azure-ad` se ha ocupado de los detalles de la creación de mensajes de autenticación, validación de tokens de Azure AD y mantenimiento de la sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="51e4b-184">`passport-azure-ad` has taken care of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span> <span data-ttu-id="51e4b-185">Ya solo falta dar a los usuarios una forma de iniciar y cerrar sesión, y recopilar información adicional sobre los usuarios que han iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="51e4b-185">All that remains is to give your users a way to sign in and sign out, and to gather additional information on users who have signed in.</span></span>

<span data-ttu-id="51e4b-186">En primer lugar, agregue el valor predeterminado, el inicio de sesión, la cuenta y los métodos de cierre de sesión al archivo `app.js`:</span><span class="sxs-lookup"><span data-stu-id="51e4b-186">First, add the default, sign-in, account, and sign-out methods to your `app.js` file:</span></span>

```JavaScript

//Routes (Section 4)

app.get('/', function(req, res){
  res.render('index', { user: req.user });
});

app.get('/account', ensureAuthenticated, function(req, res){
  res.render('account', { user: req.user });
});

app.get('/login',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Login was called in the Sample');
    res.redirect('/');
});

app.get('/logout', function(req, res){
  req.logout();
  res.redirect('/');
});

```

<span data-ttu-id="51e4b-187">Para revisar estos métodos detalladamente:</span><span class="sxs-lookup"><span data-stu-id="51e4b-187">To review these methods in detail:</span></span>
- <span data-ttu-id="51e4b-188">La ruta `/` se redirige a la vista `index.ejs` pasando el usuario en la solicitud (si existe).</span><span class="sxs-lookup"><span data-stu-id="51e4b-188">The `/` route redirects to the `index.ejs` view by passing the user in the request (if it exists).</span></span>
- <span data-ttu-id="51e4b-189">La ruta `/account` comprueba en primer lugar su autenticación (la implementación de este procedimiento se realiza a continuación).</span><span class="sxs-lookup"><span data-stu-id="51e4b-189">The `/account` route first verifies that you are authenticated (the implementation for this is below).</span></span> <span data-ttu-id="51e4b-190">Luego pasa el usuario en la solicitud para que pueda obtener más información sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="51e4b-190">It then passes the user in the request so that you can get additional information about the user.</span></span>
- <span data-ttu-id="51e4b-191">La ruta `/login` llama al autenticador `azuread-openidconnect` desde `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="51e4b-191">The `/login` route calls the `azuread-openidconnect` authenticator from `passport-azure-ad`.</span></span> <span data-ttu-id="51e4b-192">Si el resultado de la operación no es satisfactorio, la ruta redirecciona al usuario a `/login`.</span><span class="sxs-lookup"><span data-stu-id="51e4b-192">If it doesn't succeed, the route redirects the user back to `/login`.</span></span>
- <span data-ttu-id="51e4b-193">`/logout` simplemente llama a `logout.ejs` (y a su ruta).</span><span class="sxs-lookup"><span data-stu-id="51e4b-193">`/logout` simply calls `logout.ejs` (and its route).</span></span> <span data-ttu-id="51e4b-194">Así se borran las cookies y se devuelve al usuario a `index.ejs`.</span><span class="sxs-lookup"><span data-stu-id="51e4b-194">This clears cookies and then returns the user back to `index.ejs`.</span></span>


<span data-ttu-id="51e4b-195">Para la última parte de `app.js`, agregue el método `EnsureAuthenticated` que se utiliza en la ruta `/account`.</span><span class="sxs-lookup"><span data-stu-id="51e4b-195">For the last part of `app.js`, add the `EnsureAuthenticated` method that is used in the `/account` route.</span></span>

```JavaScript

// Simple route middleware to ensure that the user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs to be protected. If
//   the request is authenticated (typically via a persistent sign-in session),
//   then the request will proceed. Otherwise, the user will be redirected to the
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

<span data-ttu-id="51e4b-196">Por último, cree el propio servidor en `app.js`.</span><span class="sxs-lookup"><span data-stu-id="51e4b-196">Finally, create the server itself in `app.js`.</span></span>

```JavaScript

app.listen(3000);

```


## <a name="create-the-views-and-routes-in-express-to-call-your-policies"></a><span data-ttu-id="51e4b-197">Creación de las vistas y las rutas en Express para llamar a sus directivas</span><span class="sxs-lookup"><span data-stu-id="51e4b-197">Create the views and routes in Express to call your policies</span></span>

<span data-ttu-id="51e4b-198">`app.js` ya está completa.</span><span class="sxs-lookup"><span data-stu-id="51e4b-198">Your `app.js` is now complete.</span></span> <span data-ttu-id="51e4b-199">Solo es preciso agregar las rutas y las vistas que permitan llamar a las directivas de inicio de sesión y registro.</span><span class="sxs-lookup"><span data-stu-id="51e4b-199">You just need to add the routes and views that allow you to call the sign-in and sign-up policies.</span></span> <span data-ttu-id="51e4b-200">También controlan las rutas `/logout` y `/login` que creó.</span><span class="sxs-lookup"><span data-stu-id="51e4b-200">These also handle the `/logout` and `/login` routes you created.</span></span>

<span data-ttu-id="51e4b-201">Cree la ruta `/routes/index.js` en el directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="51e4b-201">Create the `/routes/index.js` route under the root directory.</span></span>

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

<span data-ttu-id="51e4b-202">Cree la ruta `/routes/user.js` en el directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="51e4b-202">Create the `/routes/user.js` route under the root directory.</span></span>

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

<span data-ttu-id="51e4b-203">Estas rutas simples pasan las solicitudes a las vistas.</span><span class="sxs-lookup"><span data-stu-id="51e4b-203">These simple routes pass along requests to your views.</span></span> <span data-ttu-id="51e4b-204">Incluyen el usuario, si hay alguno.</span><span class="sxs-lookup"><span data-stu-id="51e4b-204">They include the user, if one is present.</span></span>

<span data-ttu-id="51e4b-205">Cree la vista `/views/index.ejs` en el directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="51e4b-205">Create the `/views/index.ejs` view under the root directory.</span></span> <span data-ttu-id="51e4b-206">Se trata de una página simple que llama a las directivas de inicio y cierre de sesión.</span><span class="sxs-lookup"><span data-stu-id="51e4b-206">This is a simple page that calls policies for sign-in and sign-out.</span></span> <span data-ttu-id="51e4b-207">También puede utilizarla para obtener información de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="51e4b-207">You can also use it to grab account information.</span></span> <span data-ttu-id="51e4b-208">Tenga en cuenta que puede utilizar el operador condicional `if (!user)` cuando el usuario se pasa a través de la solicitud para proporcionar evidencia de que el usuario ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="51e4b-208">Note that you can use the conditional `if (!user)` as the user is passed through in the request to provide evidence that the user is signed in.</span></span>

```JavaScript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login/?p=your facebook policy">Sign in with Facebook</a>
    <a href="/login/?p=your email sign-in policy">Sign in with email</a>
    <a href="/login/?p=your email sign-up policy">Sign up with email</a>
<% } else { %>
    <h2>Hello, <%= user.displayName %>.</h2>
    <a href="/account">Account info</a></br>
    <a href="/logout">Log out</a>
<% } %>
```

<span data-ttu-id="51e4b-209">Cree la vista `/views/account.ejs` en el directorio raíz, con el fin de que pueda ver información adicional que `passport-azure-ad` incluyó en la solicitud del usuario.</span><span class="sxs-lookup"><span data-stu-id="51e4b-209">Create the `/views/account.ejs` view under the root directory so that you can view additional information that `passport-azure-ad` put in the user request.</span></span>

```Javascript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login">Sign in</a>
<% } else { %>
<p>displayName: <%= user.displayName %></p>
<p>givenName: <%= user.name.givenName %></p>
<p>familyName: <%= user.name.familyName %></p>
<p>UPN: <%= user._json.upn %></p>
<p>Profile ID: <%= user.id %></p>
<p>Full Claims</p>
<%- JSON.stringify(user) %>
<p></p>
<a href="/logout">Log Out</a>
<% } %>
```

<span data-ttu-id="51e4b-210">Ya puede compilar y ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="51e4b-210">You can now build and run your app.</span></span>

<span data-ttu-id="51e4b-211">Ejecute `node app.js` y vaya a `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="51e4b-211">Run `node app.js` and navigate to `http://localhost:3000`</span></span>


<span data-ttu-id="51e4b-212">Regístrese o inicie sesión en la aplicación mediante el correo electrónico o Facebook.</span><span class="sxs-lookup"><span data-stu-id="51e4b-212">Sign up or sign in to the app by using email or Facebook.</span></span> <span data-ttu-id="51e4b-213">Cierre la sesión y vuelva a iniciarla con otro usuario.</span><span class="sxs-lookup"><span data-stu-id="51e4b-213">Sign out and sign back in as a different user.</span></span>

##<a name="next-steps"></a><span data-ttu-id="51e4b-214">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="51e4b-214">Next steps</span></span>

<span data-ttu-id="51e4b-215">Como referencia, se proporciona el ejemplo completado (sin sus valores de configuración) [en forma de archivo .zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="51e4b-215">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="51e4b-216">También puede clonarlo desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="51e4b-216">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="51e4b-217">Ahora puede pasar a temas más avanzados.</span><span class="sxs-lookup"><span data-stu-id="51e4b-217">You can now move on to more advanced topics.</span></span> <span data-ttu-id="51e4b-218">Puede probar:</span><span class="sxs-lookup"><span data-stu-id="51e4b-218">You might try:</span></span>

[<span data-ttu-id="51e4b-219">Proteger de una API web mediante el modelo B2C en Node.js</span><span class="sxs-lookup"><span data-stu-id="51e4b-219">Secure a web API by using the B2C model in Node.js</span></span>](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on to more advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing the your B2C App's UX >>]()

-->
