---
title: "v2.0 de Active Directory de aaaAzure inicio de sesión en aplicaciones de web de Node.js | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toobuild una Node.js web aplicación que inicia sesión un usuario con una cuenta Microsoft personal y una cuenta profesional o educativa."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 1b889e72-f5c3-464a-af57-79abf5e2e147
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f8ce6e2b841c215cb14e82bcf444fe849634cc88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="7b0d9-103">Agregar la aplicación web de inicio de sesión tooa Node.js</span><span class="sxs-lookup"><span data-stu-id="7b0d9-103">Add sign-in tooa Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="7b0d9-104">No todas las características y escenarios de Azure Active Directory funcionan con el punto de conexión de hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="7b0d9-105">toodetermine si debe utilizar Hola v2.0 extremo u Hola v1.0, conozca [v2.0 limitaciones](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="7b0d9-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="7b0d9-106">En este tutorial, usamos Hola de Passport toodo siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="7b0d9-106">In this tutorial, we use Passport toodo hello following tasks:</span></span>

* <span data-ttu-id="7b0d9-107">En una aplicación web, inicie sesión en usuario hello mediante Azure Active Directory (Azure AD) y Hola v2.0 extremo.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-107">In a web app, sign in hello user by using Azure Active Directory (Azure AD) and hello v2.0 endpoint.</span></span>
* <span data-ttu-id="7b0d9-108">Mostrar información acerca del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-108">Display information about hello user.</span></span>
* <span data-ttu-id="7b0d9-109">Inicio de sesión Hola usuario fuera de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="7b0d9-110">**Passport** es middleware de autenticación para Node.js.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="7b0d9-111">Passport, flexible y modular, se puede usar discretamente en cualquier aplicación web de Restify o basada en Express.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="7b0d9-112">En esta herramienta, un conjunto completo de estrategias admite la autenticación mediante nombre de usuario y contraseña, Facebook, Twitter y mucho más.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="7b0d9-113">Hemos desarrollado una estrategia para Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="7b0d9-114">En este artículo, le mostramos cómo tooinstall Hola módulo y, a continuación, agregue hello Azure AD `passport-azure-ad` complemento.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-114">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="7b0d9-115">Descargar</span><span class="sxs-lookup"><span data-stu-id="7b0d9-115">Download</span></span>
<span data-ttu-id="7b0d9-116">código de Hello para este tutorial se mantiene [en GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span><span class="sxs-lookup"><span data-stu-id="7b0d9-116">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="7b0d9-117">tutorial de hello toofollow, puede [descargar el esqueleto de la aplicación hello como un archivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) o esqueleto de Hola de clon:</span><span class="sxs-lookup"><span data-stu-id="7b0d9-117">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="7b0d9-118">También puede obtener la aplicación hello completado final Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-118">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="7b0d9-119">1: Registro de una aplicación</span><span class="sxs-lookup"><span data-stu-id="7b0d9-119">1: Register an app</span></span>
<span data-ttu-id="7b0d9-120">Crear una nueva aplicación en [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o seguir [estos pasos detallan](active-directory-v2-app-registration.md) tooregister una aplicación.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="7b0d9-121">Asegúrese de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7b0d9-121">Make sure you:</span></span>

* <span data-ttu-id="7b0d9-122">Hola copia **Id. de aplicación** asignado tooyour aplicación.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-122">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="7b0d9-123">Lo necesitará en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="7b0d9-124">Agregar hello **Web** plataforma para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-124">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="7b0d9-125">Hola copia **URI de redireccionamiento** desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-125">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="7b0d9-126">Debe usar el valor de identificador URI predeterminado de Hola de `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-126">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-tooyour-directory"></a><span data-ttu-id="7b0d9-127">2: Agregar directorio tooyour de requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7b0d9-127">2: Add prerequisities tooyour directory</span></span>
<span data-ttu-id="7b0d9-128">En un símbolo del sistema, cambie la carpeta raíz de directorios toogo tooyour, si no está ya no existe.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-128">At a command prompt, change directories toogo tooyour root folder, if you are not already there.</span></span> <span data-ttu-id="7b0d9-129">Ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="7b0d9-129">Run hello following commands:</span></span>

* `npm install express`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install restify`
* `npm install mongoose`
* `npm install bunyan`
* `npm install assert-plus`
* `npm install passport`
* `npm install webfinger`
* `npm install body-parser`
* `npm install express-session`
* `npm install cookie-parser`

<span data-ttu-id="7b0d9-130">Además, usamos `passport-azure-ad` en esqueleto Hola de inicio rápido de hello:</span><span class="sxs-lookup"><span data-stu-id="7b0d9-130">In addition, we use `passport-azure-ad` in hello skeleton of hello quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="7b0d9-131">Esto instala las bibliotecas de Hola que `passport-azure-ad` utiliza.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-131">This installs hello libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="7b0d9-132">3: configurar la estrategia de aplicación toouse Hola js de nodo de passport</span><span class="sxs-lookup"><span data-stu-id="7b0d9-132">3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="7b0d9-133">Configurar Hola Express middleware toouse Hola protocolo de autenticación OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-133">Set up hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="7b0d9-134">Usar solicitudes de inicio de sesión y cierre de sesión de Passport tooissue, administrar la sesión del usuario de Hola y obtener información acerca del usuario de hello, entre otras cosas.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-134">You use Passport tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, among other things.</span></span>

1.  <span data-ttu-id="7b0d9-135">En la raíz de hello del proyecto de hello, abra el archivo de Config.js de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-135">In hello root of hello project, open hello Config.js file.</span></span> <span data-ttu-id="7b0d9-136">Hola `exports.creds` sección, escriba los valores de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-136">In hello `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="7b0d9-137">`clientID`: Hola **identificador de la aplicación** que está asignado tooyour aplicación Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-137">`clientID`: hello **Application Id** that's assigned tooyour app in hello Azure portal.</span></span>
  * <span data-ttu-id="7b0d9-138">`returnURL`: Hola **URI de redireccionamiento** especificado en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-138">`returnURL`: hello **Redirect URI** that you entered in hello portal.</span></span>
  * <span data-ttu-id="7b0d9-139">`clientSecret`: secreto de Hola que generó en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-139">`clientSecret`: hello secret that you generated in hello portal.</span></span>

2.  <span data-ttu-id="7b0d9-140">En la raíz de hello del proyecto de hello, abra el archivo de App.js de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-140">In hello root of hello project, open hello App.js file.</span></span> <span data-ttu-id="7b0d9-141">tooinvoke hello OIDCStrategy stratey, que se incluye con `passport-azure-ad`, agregar Hola siguiente llamada:</span><span class="sxs-lookup"><span data-stu-id="7b0d9-141">tooinvoke hello OIDCStrategy stratey, which comes with `passport-azure-ad`, add hello following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="7b0d9-142">toohandle, sus solicitudes de inicio de sesión, utilice estrategia de hello simplemente hace referencia:</span><span class="sxs-lookup"><span data-stu-id="7b0d9-142">toohandle your sign-in requests, use hello strategy you just referenced:</span></span>

  ```JavaScript
  // Use hello OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. hello function accepts
  //   credentials (in this case, an OpenID identifier), and invokes a callback
  //   with a user object.
  passport.use( new OIDCStrategy({
      callbackURL: config.creds.returnURL,
      realm: config.creds.realm,
      clientID: config.creds.clientID,
      clientSecret: config.creds.clientSecret,
      oidcIssuer: config.creds.issuer,
      identityMetadata: config.creds.identityMetadata,
      responseType: config.creds.responseType,
      responseMode: config.creds.responseMode,
      skipUserProfile: config.creds.skipUserProfile
      scope: config.creds.scope
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
      log.info('Example: Email address we received was: ', profile.email);
      // Asynchronous verification, for effect...
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

<span data-ttu-id="7b0d9-143">Passport usa un patrón similar para todas sus estrategias (Twitter, Facebook, etc.).</span><span class="sxs-lookup"><span data-stu-id="7b0d9-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="7b0d9-144">Todos los escritores de estrategia cumplen toohello patrón.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-144">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="7b0d9-145">Pasar la estrategia de hello un `function()` que usa un token y `done` como parámetros.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-145">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="7b0d9-146">estrategia de Hola se devuelve cuando hace todo su trabajo.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-146">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="7b0d9-147">Almacenar usuario hello y token de hello complementario por lo que no necesita tooask para ella de nuevo.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-147">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7b0d9-148">Hello código anterior toma cualquier usuario que puede autenticar el servidor de tooyour.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-148">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="7b0d9-149">Esto se conoce como registro automático.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-149">This is known as auto-registration.</span></span> <span data-ttu-id="7b0d9-150">En un servidor de producción, desearía toolet cualquiera sin tener primero que les vaya a través de un proceso de registro que elija.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-150">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="7b0d9-151">Esto suele ser el patrón de Hola que se ve en aplicaciones de consumidor.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-151">This is usually hello pattern that you see in consumer apps.</span></span> <span data-ttu-id="7b0d9-152">aplicación Hello podrían tooregister con Facebook, pero, a continuación, le pide que tooenter obtener información adicional.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-152">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="7b0d9-153">Si no usa un programa de línea de comandos para este tutorial, podría extraer correo electrónico de Hola de objeto de símbolo (token) de Hola que se devuelve.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-153">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="7b0d9-154">A continuación, podría solicitar información adicional de hello usuario tooenter.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-154">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="7b0d9-155">Dado que se trata de un servidor de prueba, agregar usuario Hola directamente toohello en la memoria de base de datos.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-155">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="7b0d9-156">Agregue los métodos de Hola que realice un seguimiento de tookeep de los usuarios que han iniciado sesión, según sea necesario mediante la cuenta de Passport.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-156">Add hello methods that you use tookeep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="7b0d9-157">Esto incluye serializar y deserializar la información del usuario de hello:</span><span class="sxs-lookup"><span data-stu-id="7b0d9-157">This includes serializing and deserializing hello user's information:</span></span>

  ```JavaScript

  // Passport session setup (section 2)

  //   toosupport persistent login sessions, Passport needs toobe able to
  //   serialize users into, and deserialize users out of, hello session. Typically,
  //   this is as simple as storing hello user ID when serializing, and finding
  //   hello user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array toohold signed-in users
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

5.  <span data-ttu-id="7b0d9-158">Agregue el código de hello que carga el motor de hello Express.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-158">Add hello code that loads hello Express engine.</span></span> <span data-ttu-id="7b0d9-159">Usar saludo predeterminado /views y patrón /routes que expresan proporciona:</span><span class="sxs-lookup"><span data-stu-id="7b0d9-159">You use hello default /views and /routes pattern that Express provides:</span></span>

  ```JavaScript

  // Set up Express (section 2)

  var app = express();

  app.configure(function() {
    app.set('views', __dirname + '/views');
    app.set('view engine', 'ejs');
    app.use(express.logger());
    app.use(express.methodOverride());
    app.use(cookieParser());
    app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
    app.use(bodyParser.urlencoded({ extended : true }));
    // Initialize Passport!  Also use passport.session() middleware, toosupport
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  <span data-ttu-id="7b0d9-160">Agregar Hola POST enruta que entrega hello las solicitudes de inicio de sesión real toohello `passport-azure-ad` motor:</span><span class="sxs-lookup"><span data-stu-id="7b0d9-160">Add hello POST routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. hello first step in OpenID authentication involves redirecting
  //   hello user toohello user's OpenID provider. After authenticating, hello OpenID
  //   provider redirects hello user back toothis application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in hello sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called.
  //   In this example, it redirects hello user toohello home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called. 
  //   In this example, it redirects hello user toohello home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="7b0d9-161">4: usar Passport tooissue inicio de sesión y cierre de sesión solicita tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="7b0d9-161">4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="7b0d9-162">La aplicación se ha establecido por toocommunicate con el punto de conexión de hello v2.0 con el protocolo de autenticación de OpenID Connect de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-162">Your app is now set up toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="7b0d9-163">Hola `passport-azure-ad` estrategia se encarga de todos los detalles de Hola de transmitir mensajes de autenticación, validar los tokens de Azure AD y mantener la sesión de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-163">hello `passport-azure-ad` strategy takes care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining hello user session.</span></span> <span data-ttu-id="7b0d9-164">Todo lo que queda toodo es toogive a los usuarios una manera toosign en e inicie sesión horizontal y toogather obtener más información acerca del usuario de Hola que ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-164">All that is left toodo is toogive your users a way toosign in and sign out, and toogather more information about hello user who is signed in.</span></span>

1.  <span data-ttu-id="7b0d9-165">Agregar hello **predeterminado**, **inicio de sesión**, **cuenta**, y **logout** métodos tooyour App.js archivo:</span><span class="sxs-lookup"><span data-stu-id="7b0d9-165">Add hello **default**, **login**, **account**, and **logout** methods tooyour App.js file:</span></span>

  ```JavaScript

  //Routes (section 4)

  app.get('/', function(req, res){
    res.render('index', { user: req.user });
  });

  app.get('/account', ensureAuthenticated, function(req, res){
    res.render('account', { user: req.user });
  });

  app.get('/login',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Login was called in hello sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  <span data-ttu-id="7b0d9-166">A continuación encontrará los detalles de hello:</span><span class="sxs-lookup"><span data-stu-id="7b0d9-166">Here are hello details:</span></span>
    
    * <span data-ttu-id="7b0d9-167">Hola `/` ruta redirige toohello index.ejs vista.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-167">hello `/` route redirects toohello index.ejs view.</span></span> <span data-ttu-id="7b0d9-168">Pasa usuario hello en solicitud de hello (si existe).</span><span class="sxs-lookup"><span data-stu-id="7b0d9-168">It passes hello user in hello request (if it exists).</span></span>
    * <span data-ttu-id="7b0d9-169">Hola `/account` enrutar primero *garantiza que se autentican* (implementar que en el siguiente código de hello).</span><span class="sxs-lookup"><span data-stu-id="7b0d9-169">hello `/account` route first *ensures that you are authenticated* (you implement that in hello following code).</span></span> <span data-ttu-id="7b0d9-170">A continuación, transferirlos usuario hello en solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-170">Then, it passes hello user in hello request.</span></span> <span data-ttu-id="7b0d9-171">Esto es por lo que puede obtener más información acerca del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-171">This is so you can get more information about hello user.</span></span>
    * <span data-ttu-id="7b0d9-172">Hola `/login` enrutar las llamadas su `azuread-openidconnect` autenticador de `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-172">hello `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="7b0d9-173">Si no que no tiene éxito, redirige nuevo usuario de hello demasiado`/login`.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-173">If that doesn't succeed, it redirects hello user back too`/login`.</span></span>
    * <span data-ttu-id="7b0d9-174">Hola `/logout` ruta llama hello logout.ejs vista (y ruta).</span><span class="sxs-lookup"><span data-stu-id="7b0d9-174">hello `/logout` route calls hello logout.ejs view (and route).</span></span> <span data-ttu-id="7b0d9-175">Esto borra las cookies y, a continuación, devuelve Hola tooindex.ejs atrás de usuario.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-175">This clears cookies, and then returns hello user back tooindex.ejs.</span></span>

2.  <span data-ttu-id="7b0d9-176">Agregar hello **EnsureAuthenticated** método que se utilizó anteriormente en `/account`:</span><span class="sxs-lookup"><span data-stu-id="7b0d9-176">Add hello **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

  ```JavaScript

  // Route middleware tooensure hello user is authenticated (section 4)

  //   Use this route middleware on any resource that needs toobe protected. If
  //   hello request is authenticated (typically via a persistent login session),
  //   hello request proceeds. Otherwise, hello user is redirected toothe
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  <span data-ttu-id="7b0d9-177">En App.js, crear Hola servidor:</span><span class="sxs-lookup"><span data-stu-id="7b0d9-177">In App.js, create hello server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a><span data-ttu-id="7b0d9-178">5: crear vistas de Hola y rutas de Express que muestra el usuario en el sitio Web de Hola</span><span class="sxs-lookup"><span data-stu-id="7b0d9-178">5: Create hello views and routes in Express that you show your user on hello website</span></span>
<span data-ttu-id="7b0d9-179">Agregar rutas de Hola y vistas que muestran información toohello usuario.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-179">Add hello routes and views that show information toohello user.</span></span> <span data-ttu-id="7b0d9-180">rutas de Hola y vistas también controlan hello `/logout` y `/login` rutas que ha creado.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-180">hello routes and views also handle hello `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="7b0d9-181">En el directorio raíz de hello, crear hello `/routes/index.js` ruta.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-181">In hello root directory, create hello `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="7b0d9-182">En el directorio raíz de hello, crear hello `/routes/user.js` ruta.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-182">In hello root directory, create hello `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="7b0d9-183">`/routes/index.js`y `/routes/user.js` son rutas simples que pasan a lo largo de vistas de tooyour una solicitud hello, incluido el usuario de hello, si está presente.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along hello request tooyour views, including hello user, if present.</span></span>

3.  <span data-ttu-id="7b0d9-184">En el directorio raíz de hello, crear hello `/views/index.ejs` vista.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-184">In hello root directory, create hello `/views/index.ejs` view.</span></span> <span data-ttu-id="7b0d9-185">Esta página llama a los métodos **login** y **logout**.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="7b0d9-186">También usar hello `/views/index.ejs` ver información de la cuenta de toocapture.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-186">You also use hello `/views/index.ejs` view toocapture account information.</span></span> <span data-ttu-id="7b0d9-187">Puede usar Hola condicional `if (!user)` como usuario de Hola que se pasan a través de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-187">You can use hello conditional `if (!user)` as hello user being passed through in hello request.</span></span> <span data-ttu-id="7b0d9-188">Se evidencia que hay un usuario con sesión iniciada.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-188">It is evidence that you have a user signed in.</span></span>

  ```JavaScript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
      <h2>Hello, <%= user.displayName %>.</h2>
      <a href="/account">Account info</a></br>
      <a href="/logout">Sign out</a>
  <% } %>
  ```

4.  <span data-ttu-id="7b0d9-189">En el directorio raíz de hello, crear hello `/views/account.ejs` vista.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-189">In hello root directory, create hello `/views/account.ejs` view.</span></span> <span data-ttu-id="7b0d9-190">Hola `/views/account.ejs` vista le permite obtener información adicional de tooview que `passport-azuread` coloca en la solicitud del usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-190">hello `/views/account.ejs` view allows you tooview additional information that `passport-azuread` puts in hello user request.</span></span>

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
  <p>Full Claimes</p>
  <%- JSON.stringify(user) %>
  <p></p>
  <a href="/logout">Sign out</a>
  <% } %>
  ```

5.  <span data-ttu-id="7b0d9-191">Agregue un diseño.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-191">Add a layout.</span></span> <span data-ttu-id="7b0d9-192">En el directorio raíz de hello, crear hello `/views/layout.ejs` vista.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-192">In hello root directory, create hello `/views/layout.ejs` view.</span></span>

  ```HTML

  <!DOCTYPE html>
  <html>
      <head>
          <title>Passport-OpenID Example</title>
      </head>
      <body>
          <% if (!user) { %>
              <p>
              <a href="/">Home</a> |
              <a href="/login">Sign in</a>
              </p>
          <% } else { %>
              <p>
              <a href="/">Home</a> |
              <a href="/account">Account</a> |
              <a href="/logout">Sign out</a>
              </p>
          <% } %>
          <%- body %>
      </body>
  </html>
  ```

6.  <span data-ttu-id="7b0d9-193">toobuild y ejecutar la aplicación, ejecutar `node app.js`.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-193">toobuild and run your app, run `node app.js`.</span></span> <span data-ttu-id="7b0d9-194">A continuación, ir demasiado`http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-194">Then, go too`http://localhost:3000`.</span></span>

7.  <span data-ttu-id="7b0d9-195">Inicie sesión con una cuenta personal, profesional o educativa de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="7b0d9-196">Tenga en cuenta que la identidad del usuario de Hola se refleja en lista de AccountType de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-196">Note that hello user's identity is reflected in hello /account list.</span></span> 

<span data-ttu-id="7b0d9-197">Ahora tiene una aplicación web que está protegida mediante protocolos estándar del sector.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="7b0d9-198">Puede autenticar a los usuarios de la aplicación con sus cuentas personales y profesionales o educativas.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b0d9-199">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7b0d9-199">Next steps</span></span>
<span data-ttu-id="7b0d9-200">Como referencia, ejemplo de Hola finalizado (sin los valores de configuración) se proporciona como [un archivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="7b0d9-200">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="7b0d9-201">También puede clonarlo desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="7b0d9-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="7b0d9-202">A continuación, puede mover en toomore temas avanzados.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-202">Next, you can move on toomore advanced topics.</span></span> <span data-ttu-id="7b0d9-203">Puede ser conveniente tootry:</span><span class="sxs-lookup"><span data-stu-id="7b0d9-203">You might want tootry:</span></span>

[<span data-ttu-id="7b0d9-204">Proteger una API web de Node.js mediante el punto de conexión de hello v2.0</span><span class="sxs-lookup"><span data-stu-id="7b0d9-204">Secure a Node.js web API by using hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="7b0d9-205">Estos son algunos recursos adicionales:</span><span class="sxs-lookup"><span data-stu-id="7b0d9-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="7b0d9-206">Guía del desarrollador de Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="7b0d9-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="7b0d9-207">Etiqueta "azure-active-directory" de Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="7b0d9-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="7b0d9-208">Obtención de actualizaciones de seguridad para nuestros productos</span><span class="sxs-lookup"><span data-stu-id="7b0d9-208">Get security updates for our products</span></span>
<span data-ttu-id="7b0d9-209">Recomendamos que toosign una toobe una notificación cuando se produzcan incidentes de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-209">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="7b0d9-210">En hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) página, subscribe tooSecurity avisos de alertas.</span><span class="sxs-lookup"><span data-stu-id="7b0d9-210">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

