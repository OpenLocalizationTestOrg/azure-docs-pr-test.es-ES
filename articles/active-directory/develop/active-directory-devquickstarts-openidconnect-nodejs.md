---
title: "Introducción al inicio de sesión y cierre de sesión en Azure AD mediante Node.js | Microsoft Docs"
description: "Aprenda a crear una aplicación web MVC Express de Node.js que se integre con Azure AD para el inicio de sesión."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 81deecec-dbe2-4e75-8bc0-cf3788645f99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 13317b016f9ff3955f376b858645c42668b0de42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="370ec-103">Inicio y cierre de sesión de aplicación web de Node.js con Azure AD</span><span class="sxs-lookup"><span data-stu-id="370ec-103">Node.js web app sign-in and sign-out with Azure AD</span></span>
<span data-ttu-id="370ec-104">Aquí usamos Passport para:</span><span class="sxs-lookup"><span data-stu-id="370ec-104">Here we use Passport to:</span></span>

* <span data-ttu-id="370ec-105">Iniciar la sesión del usuario en la aplicación con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="370ec-105">Sign the user in to the app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="370ec-106">Mostrar información sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="370ec-106">Display information about the user.</span></span>
* <span data-ttu-id="370ec-107">Cerrar la sesión del usuario en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="370ec-107">Sign the user out of the app.</span></span>

<span data-ttu-id="370ec-108">Passport es middleware de autenticación para Node.js.</span><span class="sxs-lookup"><span data-stu-id="370ec-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="370ec-109">Flexible y modular, Passport puede pasar discretamente a cualquier aplicación web basada en Express o Restify.</span><span class="sxs-lookup"><span data-stu-id="370ec-109">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or restify web application.</span></span> <span data-ttu-id="370ec-110">Un conjunto completo de estrategias admiten la autenticación que usa un nombre de usuario y una contraseña, Facebook, Twitter y mucho más.</span><span class="sxs-lookup"><span data-stu-id="370ec-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="370ec-111">Hemos desarrollado una estrategia para Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="370ec-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="370ec-112">Instalamos este módulo y luego agregaremos el complemento `passport-azure-ad` de Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="370ec-112">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="370ec-113">Para ello, realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="370ec-113">To do this, take the following steps:</span></span>

1. <span data-ttu-id="370ec-114">Registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="370ec-114">Register an app.</span></span>
2. <span data-ttu-id="370ec-115">Configurar la aplicación para que use la estrategia `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="370ec-115">Set up your app to use the `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="370ec-116">Usar Passport para emitir solicitudes de inicio y cierre de sesión en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="370ec-116">Use Passport to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="370ec-117">Imprimir datos sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="370ec-117">Print data about the user.</span></span>

<span data-ttu-id="370ec-118">El código de este tutorial se conserva [en GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="370ec-118">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span>  <span data-ttu-id="370ec-119">Para poder continuar, puede [descargar el esqueleto de la aplicación como un archivo .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) o clonar el esqueleto:</span><span class="sxs-lookup"><span data-stu-id="370ec-119">To follow along, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="370ec-120">La aplicación completa se ofrece también al final de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="370ec-120">The completed application is provided at the end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="370ec-121">Paso 1: Registro de una aplicación</span><span class="sxs-lookup"><span data-stu-id="370ec-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="370ec-122">Inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="370ec-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="370ec-123">En el menú que aparece en la parte superior de la página, seleccione su cuenta.</span><span class="sxs-lookup"><span data-stu-id="370ec-123">In the menu at the top of the page, select your account.</span></span> <span data-ttu-id="370ec-124">En la lista **Directorio** lista, elija el inquilino de Active Directory donde desea registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="370ec-124">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>

3. <span data-ttu-id="370ec-125">Seleccione **Más servicios** en el menú de la izquierda de la pantalla y luego seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="370ec-125">Select **More Services** in the menu on the left side of the screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="370ec-126">Seleccione **Registros de aplicaciones** y luego seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="370ec-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="370ec-127">Siga las indicaciones para crear una **Aplicación web** y/o **API web**.</span><span class="sxs-lookup"><span data-stu-id="370ec-127">Follow the prompts to create a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="370ec-128">El **nombre** de la aplicación describe la aplicación a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="370ec-128">The **name** of the application describes your application to users.</span></span>

  * <span data-ttu-id="370ec-129">La **dirección URL de inicio de sesión** es la dirección URL base de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="370ec-129">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="370ec-130">Es el valor predeterminado del esquema `http://localhost:3000/auth/openid/return`\`.</span><span class="sxs-lookup"><span data-stu-id="370ec-130">The skeleton's default is `http://localhost:3000/auth/openid/return`\`.</span></span>

6. <span data-ttu-id="370ec-131">Después de registrarse, Azure AD asigna a la aplicación un identificador de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="370ec-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="370ec-132">Necesita este valor en las secciones siguientes, así que cópielo de la página de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="370ec-132">You need this value in the following sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="370ec-133">En la página **Configuración** -> **Propiedades** de la aplicación, actualice el URI del identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="370ec-133">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="370ec-134">El **URI de id. de aplicación** es un identificador único de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="370ec-134">The **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="370ec-135">La convención es usar el formato `https://<tenant-domain>/<app-name>`, por ejemplo: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="370ec-135">The convention is to use the format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

## <a name="step-2-add-prerequisites-to-your-directory"></a><span data-ttu-id="370ec-136">Paso 2: Incorporación de requisitos previos al directorio</span><span class="sxs-lookup"><span data-stu-id="370ec-136">Step 2: Add prerequisites to your directory</span></span>
1. <span data-ttu-id="370ec-137">En la línea de comandos, cambie los directorios a la carpeta raíz si aún no está ahí y luego ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="370ec-137">From the command line, change directories to your root folder if you're not already there, and then run the following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="370ec-138">Además, necesita `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="370ec-138">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="370ec-139">Esto instala las bibliotecas de las que depende `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="370ec-139">This installs the libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="370ec-140">Paso 3: Configuración de la aplicación para que use la estrategia passport-node-js</span><span class="sxs-lookup"><span data-stu-id="370ec-140">Step 3: Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="370ec-141">Aquí configuramos Express para usar el protocolo de autenticación OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="370ec-141">Here, we configure Express to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="370ec-142">Passport se usa para hacer varias cosas, como emitir solicitudes de inicio y cierre de sesión, administrar la sesión del usuario y obtener información sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="370ec-142">Passport is used to do various things, including issue sign-in and sign-out requests, manage the user's session, and get information about the user.</span></span>

1. <span data-ttu-id="370ec-143">Para comenzar, abra el archivo `config.js` en la raíz del proyecto y escriba los valores de configuración de la aplicación en la sección `exports.creds`.</span><span class="sxs-lookup"><span data-stu-id="370ec-143">To begin, open the `config.js` file at the root of the project, and then enter your app's configuration values in the `exports.creds` section.</span></span>

  * <span data-ttu-id="370ec-144">`clientID` es el **identificador de aplicación** que se asigna a la aplicación en el portal de registro.</span><span class="sxs-lookup"><span data-stu-id="370ec-144">The `clientID` is the **Application Id** that's assigned to your app in the registration portal.</span></span>

  * <span data-ttu-id="370ec-145">`returnURL` es el **identificador URI de redireccionamiento** que escribió en el portal.</span><span class="sxs-lookup"><span data-stu-id="370ec-145">The `returnURL` is the **Redirect Uri** that you entered in the portal.</span></span>

  * <span data-ttu-id="370ec-146">`clientSecret` es el secreto generado en el portal.</span><span class="sxs-lookup"><span data-stu-id="370ec-146">The `clientSecret` is the secret that you generated in the portal.</span></span>

2. <span data-ttu-id="370ec-147">Abra el archivo `app.js` en la raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="370ec-147">Next, open the `app.js` file in the root of the project.</span></span> <span data-ttu-id="370ec-148">Agregue la siguiente llamada para invocar a la estrategia `OIDCStrategy` que viene con `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="370ec-148">Then add the following call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="370ec-149">Después, use la estrategia a la que acabamos de hacer referencia para administrar las solicitudes de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="370ec-149">After that, use the strategy we just referenced to handle our sign-in requests.</span></span>

    ```JavaScript
    // Use the OIDCStrategy within Passport. (Section 2)
    //
    //   Strategies in passport require a `validate` function that accepts
    //   credentials (in this case, an OpenID identifier), and invokes a callback
    //   with a user object.
    passport.use(new OIDCStrategy({
        callbackURL: config.creds.returnURL,
        realm: config.creds.realm,
        clientID: config.creds.clientID,
        clientSecret: config.creds.clientSecret,
        oidcIssuer: config.creds.issuer,
        identityMetadata: config.creds.identityMetadata,
        skipUserProfile: config.creds.skipUserProfile,
        responseType: config.creds.responseType,
        responseMode: config.creds.responseMode
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
        if (!profile.email) {
        return done(new Error("No email found"), null);
        }
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
<span data-ttu-id="370ec-150">Passport usa un patrón similar para todas sus estrategias (Twitter, Facebook, etc.) al que se ajustan todos los escritores de estrategias.</span><span class="sxs-lookup"><span data-stu-id="370ec-150">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="370ec-151">Si se examina la estrategia, se percibe que se pasa una función que tiene un token y un elemento done como parámetros.</span><span class="sxs-lookup"><span data-stu-id="370ec-151">Looking at the strategy, you see that we pass it a function that has a token and a done as the parameters.</span></span> <span data-ttu-id="370ec-152">La estrategia se devuelve después de que realiza su trabajo.</span><span class="sxs-lookup"><span data-stu-id="370ec-152">The strategy comes back to us after it does its work.</span></span> <span data-ttu-id="370ec-153">Luego almacenaremos el usuario y guardaremos provisionalmente el token con el fin de que no tengamos que volver a pedirlo.</span><span class="sxs-lookup"><span data-stu-id="370ec-153">Then we want to store the user and stash the token so we don't need to ask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="370ec-154">El código anterior toma cualquier usuario que se autentique en el servidor.</span><span class="sxs-lookup"><span data-stu-id="370ec-154">The previous code takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="370ec-155">Esto se conoce como registro automático.</span><span class="sxs-lookup"><span data-stu-id="370ec-155">This is known as auto-registration.</span></span> <span data-ttu-id="370ec-156">Le recomendamos que no permita que nadie se autentique en un servidor de producción sin registrarse primero mediante un proceso que decida.</span><span class="sxs-lookup"><span data-stu-id="370ec-156">We    recommend that you don't let anyone authenticate to a production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="370ec-157">Este suele ser el patrón que se observa en las aplicaciones de consumidor que le permiten registrarse con Facebook, pero que luego piden que proporcione información adicional.</span><span class="sxs-lookup"><span data-stu-id="370ec-157">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to provide additional information.</span></span> <span data-ttu-id="370ec-158">Si esta no fuera una aplicación de ejemplo, podríamos haber extraído la dirección del correo electrónico del usuario del objeto de token que se devuelve y, después, haber pedido al usuario que rellenara la información adicional.</span><span class="sxs-lookup"><span data-stu-id="370ec-158">If this weren't a sample application, we could have extracted the user's email address from the token object that is returned and then asked the user to fill out additional information.</span></span> <span data-ttu-id="370ec-159">Puesto que se trata de un servidor de prueba, los agregaremos a la base de datos en memoria.</span><span class="sxs-lookup"><span data-stu-id="370ec-159">Because this is a test server, we add them to the in-memory database.</span></span>


4. <span data-ttu-id="370ec-160">A continuación, vamos a agregar los métodos que nos permitirán realizar un seguimiento de los usuarios con sesión iniciada, tal y como requiere Passport.</span><span class="sxs-lookup"><span data-stu-id="370ec-160">Next, let's add the methods that enable us to track the signed-in users as required by Passport.</span></span> <span data-ttu-id="370ec-161">Estos métodos incluyen la serialización y deserialización de la información del usuario.</span><span class="sxs-lookup"><span data-stu-id="370ec-161">These methods include serializing and deserializing the user's information.</span></span>

    ```JavaScript

            // Passport session setup. (Section 2)

            //   To support persistent sign-in sessions, Passport needs to be able to
            //   serialize users into the session and deserialize them out of the session. Typically,
            //   this is done simply by storing the user ID when serializing and finding
            //   the user by ID when deserializing.
            passport.serializeUser(function(user, done) {
            done(null, user.email);
            });

            passport.deserializeUser(function(id, done) {
            findByEmail(id, function (err, user) {
                done(err, user);
            });
            });

            // array to hold signed-in users
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

5.  <span data-ttu-id="370ec-162">Después agregaremos el código para cargar el motor de Express.</span><span class="sxs-lookup"><span data-stu-id="370ec-162">Next, let's add the code to load the Express engine.</span></span> <span data-ttu-id="370ec-163">Aquí se usa el patrón de /views y /routes predeterminado que proporciona Express.</span><span class="sxs-lookup"><span data-stu-id="370ec-163">Here we use the default /views and /routes pattern that Express provides.</span></span>

    ```JavaScript

        // configure Express (section 2)

            var app = express();
            app.configure(function() {
          app.set('views', __dirname + '/views');
          app.set('view engine', 'ejs');
          app.use(express.logger());
          app.use(express.methodOverride());
          app.use(cookieParser());
          app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
          app.use(bodyParser.urlencoded({ extended : true }));
          // Initialize Passport!  Also use passport.session() middleware, to support
          // persistent login sessions (recommended).
          app.use(passport.initialize());
          app.use(passport.session());
          app.use(app.router);
          app.use(express.static(__dirname + '/../../public'));
        });

    ```

6. <span data-ttu-id="370ec-164">Por último, se agregan las rutas que entregan las solicitudes de inicio de sesión reales al motor `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="370ec-164">Finally, let's add the routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>


       ```JavaScript

        // Our Auth routes (section 3)

        // GET /auth/openid
        //   Use passport.authenticate() as route middleware to authenticate the
        //   request. The first step in OpenID authentication involves redirecting
        //   the user to their OpenID provider. After authenticating, the OpenID
        //   provider redirects the user back to this application at
        //   /auth/openid/return.
        app.get('/auth/openid',
        passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
        function(req, res) {
            log.info('Authentication was called in the Sample');
            res.redirect('/');
        });

            // GET /auth/openid/return
            //   Use passport.authenticate() as route middleware to authenticate the
            //   request. If authentication fails, the user is redirected back to the
            //   sign-in page. Otherwise, the primary route function is called,
            //   which, in this example, redirects the user to the home page.
            app.get('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });

            // POST /auth/openid/return
            //   Use passport.authenticate() as route middleware to authenticate the
            //   request. If authentication fails, the user is redirected back to the
            //   sign-in page. Otherwise, the primary route function is called,
            //   which, in this example, redirects the user to the home page.
            app.post('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });
       ```


## <a name="step-4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="370ec-165">Paso 4: Uso de Passport para emitir solicitudes de inicio y cierre de sesión en Azure AD</span><span class="sxs-lookup"><span data-stu-id="370ec-165">Step 4: Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="370ec-166">Ahora, la aplicación está correctamente configurada para comunicarse con el punto de conexión mediante el protocolo de autenticación de OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="370ec-166">Your app is now properly configured to communicate with the endpoint by using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="370ec-167">`passport-azure-ad` se ha ocupado de todos los detalles de la creación de mensajes de autenticación, validación de tokens de Azure AD y mantenimiento de las sesiones de usuario.</span><span class="sxs-lookup"><span data-stu-id="370ec-167">`passport-azure-ad` has taken care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="370ec-168">Ya solo falta proporcionar a los usuarios una forma de iniciar y cerrar sesión, y recopilar información adicional sobre los usuarios que han iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="370ec-168">All that remains is giving your users a way to sign in and sign out, and gathering additional information about the signed-in users.</span></span>

1. <span data-ttu-id="370ec-169">En primer lugar, agregue el valor predeterminado, el inicio de sesión, la cuenta y los métodos de cierre de sesión al archivo `app.js`:</span><span class="sxs-lookup"><span data-stu-id="370ec-169">First, let's add the default, sign-in, account, and sign-out methods to our `app.js` file:</span></span>

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
            log.info('Login was called in the Sample');
            res.redirect('/');
        });

        app.get('/logout', function(req, res){
          req.logout();
          res.redirect('/');
        });

    ```

2.  <span data-ttu-id="370ec-170">Analicemos esto con detalle:</span><span class="sxs-lookup"><span data-stu-id="370ec-170">Let's review these in detail:</span></span>

  * <span data-ttu-id="370ec-171">La ruta `/` realiza la redirección a la vista index.ejs pasando el usuario en la solicitud (si existe).</span><span class="sxs-lookup"><span data-stu-id="370ec-171">The `/`route redirects to the index.ejs view, passing the user in the request (if it exists).</span></span>
  * <span data-ttu-id="370ec-172">La ruta `/account` primero se *asegura de que estamos autenticados* (lo que se implementará en el ejemplo siguiente) y, seguidamente, pasa el usuario en la solicitud para que podamos obtener información adicional sobre él.</span><span class="sxs-lookup"><span data-stu-id="370ec-172">The `/account` route first *ensures we are authenticated* (we implement that in the following example), and then passes the user in the request so that we can get additional information about the user.</span></span>
  * <span data-ttu-id="370ec-173">La ruta `/login` llama a nuestro autenticador azuread-openidconnect desde `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="370ec-173">The `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="370ec-174">Si el resultado de la operación no es satisfactorio, vuelve a redireccionar al usuario a /login.</span><span class="sxs-lookup"><span data-stu-id="370ec-174">If that doesn't succeed, it redirects the user back to /login.</span></span>
  * <span data-ttu-id="370ec-175">La ruta `/logout` simplemente llama a logout.ejs (y a la ruta), que borra las cookies y devuelve el usuario a index.ejs.</span><span class="sxs-lookup"><span data-stu-id="370ec-175">The `/logout` route simply calls the logout.ejs (and route), which clears cookies and then returns the user back to index.ejs.</span></span>

3. <span data-ttu-id="370ec-176">Para la última parte de `app.js`, agregaremos el método **EnsureAuthenticated** que se usa en `/account`, como se muestra anteriormente.</span><span class="sxs-lookup"><span data-stu-id="370ec-176">For the last part of `app.js`, let's add the **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

    ```JavaScript

        // Simple route middleware to ensure user is authenticated. (section 4)

        //   Use this route middleware on any resource that needs to be protected. If
        //   the request is authenticated (typically via a persistent sign-in session),
        //   the request proceeds. Otherwise, the user is redirected to the
        //   sign-in page.
        function ensureAuthenticated(req, res, next) {
          if (req.isAuthenticated()) { return next(); }
          res.redirect('/login')
        }
    ```

4. <span data-ttu-id="370ec-177">Por último, crearemos el propio servidor en `app.js`:</span><span class="sxs-lookup"><span data-stu-id="370ec-177">Finally, let's create the server itself in `app.js`:</span></span>

```JavaScript

        app.listen(3000);

```


## <a name="step-5-to-display-our-user-in-the-website-create-the-views-and-routes-in-express"></a><span data-ttu-id="370ec-178">Paso 5: Creación de las vistas y las rutas en Express para mostrar el usuario en el sitio web</span><span class="sxs-lookup"><span data-stu-id="370ec-178">Step 5: To display our user in the website, create the views and routes in Express</span></span>
<span data-ttu-id="370ec-179">Ahora `app.js` se habrá completado.</span><span class="sxs-lookup"><span data-stu-id="370ec-179">Now `app.js` is complete.</span></span> <span data-ttu-id="370ec-180">Solo es preciso agregar las rutas y vistas que muestran la información obtenida al usuario, así como administrar las rutas `/logout` y `/login` creadas.</span><span class="sxs-lookup"><span data-stu-id="370ec-180">We simply need to add the routes and views that show the information we get to the user, as well as handle the `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="370ec-181">Cree la ruta `/routes/index.js` en el directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="370ec-181">Create the `/routes/index.js` route under the root directory.</span></span>

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. <span data-ttu-id="370ec-182">Cree la ruta `/routes/user.js` en el directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="370ec-182">Create the `/routes/user.js` route under the root directory.</span></span>

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 <span data-ttu-id="370ec-183">Estas pasan la solicitud a nuestras vistas, incluido el usuario, si está presente.</span><span class="sxs-lookup"><span data-stu-id="370ec-183">These pass along the request to our views, including the user if present.</span></span>

3. <span data-ttu-id="370ec-184">Cree la vista `/views/index.ejs` en el directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="370ec-184">Create the `/views/index.ejs` view under the root directory.</span></span> <span data-ttu-id="370ec-185">Se trata de una página sencilla que llama a nuestros métodos de inicio y cierre de sesión y nos permite obtener información de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="370ec-185">This is a simple page that calls our login and logout methods and enables us to grab account information.</span></span> <span data-ttu-id="370ec-186">Observe que podemos usar el condicional `if (!user)`, ya que el usuario pasado en la solicitud es una evidencia de que tenemos un usuario con la sesión iniciada.</span><span class="sxs-lookup"><span data-stu-id="370ec-186">Notice that we can use the conditional `if (!user)` as the user being passed through in the request is evidence we have a signed-in user.</span></span>

    ```JavaScript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
        <h2>Hello, <%= user.displayName %>.</h2>
        <a href="/account">Account Info</a></br>
        <a href="/logout">Log Out</a>
    <% } %>
    ```

4. <span data-ttu-id="370ec-187">Cree la vista `/views/account.ejs` en el directorio raíz de modo que podamos ver la información adicional que `passport-azuread` ha incluido en la solicitud del usuario.</span><span class="sxs-lookup"><span data-stu-id="370ec-187">Create the `/views/account.ejs` view under the root directory so that we can view additional information that `passport-azuread` has put in the user request.</span></span>

    ```Javascript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
    <p>displayName: <%= user.displayName %></p>
    <p>givenName: <%= user.name.givenName %></p>
    <p>familyName: <%= user.name.familyName %></p>
    <p>UPN: <%= user._json.upn %></p>
    <p>Profile ID: <%= user.id %></p>
  ##Next steps  <p>Full Claimes</p>
    <%- JSON.stringify(user) %>
    <p></p>
    <a href="/logout">Log Out</a>
    <% } %>
    ```

5. <span data-ttu-id="370ec-188">Vamos a mejorar la apariencia, para lo que agregaremos un diseño.</span><span class="sxs-lookup"><span data-stu-id="370ec-188">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="370ec-189">Cree la vista '/views/layout.ejs' en el directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="370ec-189">Create the '/views/layout.ejs' view under the root directory.</span></span>

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
                <a href="/login">Log In</a>
                </p>
            <% } else { %>
                <p>
                <a href="/">Home</a> |
                <a href="/account">Account</a> |
                <a href="/logout">Log Out</a>
                </p>
            <% } %>
            <%- body %>
        </body>
    </html>
    ```

##<a name="next-steps"></a><span data-ttu-id="370ec-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="370ec-190">Next steps</span></span>
<span data-ttu-id="370ec-191">Por último, compile y ejecute su aplicación.</span><span class="sxs-lookup"><span data-stu-id="370ec-191">Finally, build and run your app.</span></span> <span data-ttu-id="370ec-192">Ejecute `node app.js` y luego vaya a `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="370ec-192">Run `node app.js`, and then go to `http://localhost:3000`.</span></span>

<span data-ttu-id="370ec-193">Inicie sesión con una cuenta de Microsoft personal o con una cuenta profesional o educativa, y observe cómo se refleja la identidad del usuario en la lista /account.</span><span class="sxs-lookup"><span data-stu-id="370ec-193">Sign in with either a personal Microsoft account or a work or school account, and notice how the user's identity is reflected in the /account list.</span></span> <span data-ttu-id="370ec-194">Ahora dispone de una aplicación web que está protegida mediante protocolos estándar del sector que pueden autenticar a los usuarios tanto con sus cuentas personales como con sus cuentas profesionales o educativas.</span><span class="sxs-lookup"><span data-stu-id="370ec-194">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="370ec-195">Como referencia, se proporciona el ejemplo completado (sin sus valores de configuración) [en forma de archivo .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="370ec-195">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="370ec-196">Como alternativa, puede clonarlo desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="370ec-196">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="370ec-197">Ahora puede pasar a temas más avanzados.</span><span class="sxs-lookup"><span data-stu-id="370ec-197">You can now move onto more advanced topics.</span></span> <span data-ttu-id="370ec-198">Podría interesarle:</span><span class="sxs-lookup"><span data-stu-id="370ec-198">You might want to try:</span></span>

[<span data-ttu-id="370ec-199">Protección de una API web con Azure AD</span><span class="sxs-lookup"><span data-stu-id="370ec-199">Secure a Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
