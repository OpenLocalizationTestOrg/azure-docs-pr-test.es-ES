---
title: "aaaGetting ha iniciado con el inicio de sesión Azure AD y cierre de sesión con Node.js | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toobuild un MVC Express de Node.js web aplicación que se integra con Azure AD para inicio de sesión."
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
ms.openlocfilehash: 26481899c74741743b947bd891b65ff24ffc43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="ea8ab-103">Inicio y cierre de sesión de aplicación web de Node.js con Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea8ab-103">Node.js web app sign-in and sign-out with Azure AD</span></span>
<span data-ttu-id="ea8ab-104">Aquí usamos Passport para:</span><span class="sxs-lookup"><span data-stu-id="ea8ab-104">Here we use Passport to:</span></span>

* <span data-ttu-id="ea8ab-105">Inicio de sesión Hola usuario en aplicaciones de toohello con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ea8ab-105">Sign hello user in toohello app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="ea8ab-106">Mostrar información acerca del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-106">Display information about hello user.</span></span>
* <span data-ttu-id="ea8ab-107">Inicio de sesión Hola usuario fuera de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-107">Sign hello user out of hello app.</span></span>

<span data-ttu-id="ea8ab-108">Passport es middleware de autenticación para Node.js.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="ea8ab-109">Flexible y modular, Passport puede quitarse de forma discreta en tooany basada en Express o restify la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-109">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or restify web application.</span></span> <span data-ttu-id="ea8ab-110">Un conjunto completo de estrategias admiten la autenticación que usa un nombre de usuario y una contraseña, Facebook, Twitter y mucho más.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="ea8ab-111">Hemos desarrollado una estrategia para Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="ea8ab-112">Se instale este módulo y, a continuación, agregue Hola Microsoft Azure Active Directory `passport-azure-ad` complemento.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-112">We install this module and then add hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="ea8ab-113">toodo, Hola toman pasos:</span><span class="sxs-lookup"><span data-stu-id="ea8ab-113">toodo this, take hello following steps:</span></span>

1. <span data-ttu-id="ea8ab-114">Registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-114">Register an app.</span></span>
2. <span data-ttu-id="ea8ab-115">Configurar el saludo de toouse aplicación `passport-azure-ad` estrategia.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-115">Set up your app toouse hello `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="ea8ab-116">Usar inicio de sesión de Passport tooissue y solicitudes de cierre de sesión tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-116">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="ea8ab-117">Imprimir datos acerca del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-117">Print data about hello user.</span></span>

<span data-ttu-id="ea8ab-118">código de Hello para este tutorial se mantiene [en GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="ea8ab-118">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span>  <span data-ttu-id="ea8ab-119">toofollow a lo largo, puede [descargar el esqueleto de la aplicación hello como un archivo .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) o esqueleto de Hola de clon:</span><span class="sxs-lookup"><span data-stu-id="ea8ab-119">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="ea8ab-120">final de Hola de este tutorial también se incluye aplicación Hello completado.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-120">hello completed application is provided at hello end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="ea8ab-121">Paso 1: Registro de una aplicación</span><span class="sxs-lookup"><span data-stu-id="ea8ab-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="ea8ab-122">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ea8ab-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="ea8ab-123">En menú Hola al principio de Hola de página de hello, seleccione su cuenta.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-123">In hello menu at hello top of hello page, select your account.</span></span> <span data-ttu-id="ea8ab-124">En hello **Directory** lista, seleccione la aplicación de inquilino de Active Directory de Hola donde desea tooregister.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-124">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="ea8ab-125">Seleccione **más servicios** en hello menú Hola izquierda lateral de la pantalla de bienvenida y, a continuación, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-125">Select **More Services** in hello menu on hello left side of hello screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="ea8ab-126">Seleccione **Registros de aplicaciones** y luego seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="ea8ab-127">Siga Hola indicaciones toocreate una **aplicación Web** o **WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-127">Follow hello prompts toocreate a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="ea8ab-128">Hola **nombre** de hello aplicación describe su toousers de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-128">hello **name** of hello application describes your application toousers.</span></span>

  * <span data-ttu-id="ea8ab-129">Hola **dirección URL de inicio de sesión** es Hola dirección URL base de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-129">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="ea8ab-130">Hello valor predeterminado del esqueleto es ' http://localhost:3000/auth/openid/retorno ''.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-130">hello skeleton's default is `http://localhost:3000/auth/openid/return`\`.</span></span>

6. <span data-ttu-id="ea8ab-131">Después de registrarse, Azure AD asigna a la aplicación un identificador de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="ea8ab-132">Necesita este valor en la siguiente Hola secciones, por lo tanto cópiela desde la página de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-132">You need this value in hello following sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="ea8ab-133">De hello **configuración** -> **propiedades** página de la aplicación, actualice Hola App ID URI.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-133">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="ea8ab-134">Hola **App ID URI** es un identificador único para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-134">hello **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="ea8ab-135">convención de Hello es el formato de hello toouse `https://<tenant-domain>/<app-name>`, por ejemplo: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-135">hello convention is toouse hello format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

## <a name="step-2-add-prerequisites-tooyour-directory"></a><span data-ttu-id="ea8ab-136">Paso 2: Agregar un directorio tooyour de requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ea8ab-136">Step 2: Add prerequisites tooyour directory</span></span>
1. <span data-ttu-id="ea8ab-137">Desde la línea de comandos de hello, cambiar carpeta de raíz de tooyour de directorios si no está ya no existe, y, a continuación, siga los comandos Hola de ejecución:</span><span class="sxs-lookup"><span data-stu-id="ea8ab-137">From hello command line, change directories tooyour root folder if you're not already there, and then run hello following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="ea8ab-138">Además, necesita `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="ea8ab-138">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="ea8ab-139">Esto instala las bibliotecas de Hola que `passport-azure-ad` depende.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-139">This installs hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="ea8ab-140">Paso 3: Configurar la estrategia de aplicación toouse Hola js de nodo de passport</span><span class="sxs-lookup"><span data-stu-id="ea8ab-140">Step 3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="ea8ab-141">En este caso, configuramos el protocolo de autenticación OpenID Connect de Express toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-141">Here, we configure Express toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="ea8ab-142">Passport es toodo usa varios elementos, incluidas las solicitudes problema de inicio de sesión y cierre de sesión, administrar la sesión del usuario de Hola y obtener información acerca del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-142">Passport is used toodo various things, including issue sign-in and sign-out requests, manage hello user's session, and get information about hello user.</span></span>

1. <span data-ttu-id="ea8ab-143">toobegin, abra hello `config.js` de archivos en raíz de Hola de proyecto de hello y, a continuación, escriba los valores de configuración de la aplicación Hola `exports.creds` sección.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-143">toobegin, open hello `config.js` file at hello root of hello project, and then enter your app's configuration values in hello `exports.creds` section.</span></span>

  * <span data-ttu-id="ea8ab-144">Hola `clientID` es hello **identificador de la aplicación** que está asignado tooyour aplicación de portal de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-144">hello `clientID` is hello **Application Id** that's assigned tooyour app in hello registration portal.</span></span>

  * <span data-ttu-id="ea8ab-145">Hola `returnURL` es hello **Uri de redireccionamiento** especificado en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-145">hello `returnURL` is hello **Redirect Uri** that you entered in hello portal.</span></span>

  * <span data-ttu-id="ea8ab-146">Hola `clientSecret` es secreto Hola que generó en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-146">hello `clientSecret` is hello secret that you generated in hello portal.</span></span>

2. <span data-ttu-id="ea8ab-147">A continuación, abra hello `app.js` archivo en hello raíz del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-147">Next, open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="ea8ab-148">A continuación, agregue Hola después llamada tooinvoke hello `OIDCStrategy` estrategia que se incluye con `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-148">Then add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="ea8ab-149">Después, usar la estrategia de Hola se simplemente hace referencia a toohandle las solicitudes de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-149">After that, use hello strategy we just referenced toohandle our sign-in requests.</span></span>

    ```JavaScript
    // Use hello OIDCStrategy within Passport. (Section 2)
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
<span data-ttu-id="ea8ab-150">Passport usa un patrón similar para todas sus estrategias (Twitter, Facebook, etc.) al que se ajustan todos los escritores de estrategias.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-150">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="ea8ab-151">Examinando la estrategia de hello, verá que pasamos una función que tiene un token y un hecho como parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-151">Looking at hello strategy, you see that we pass it a function that has a token and a done as hello parameters.</span></span> <span data-ttu-id="ea8ab-152">estrategia de Hello incluye volver toous después de que realice su trabajo.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-152">hello strategy comes back toous after it does its work.</span></span> <span data-ttu-id="ea8ab-153">A continuación, deseamos toostore usuario de Hola y token de hello complementario por lo que no es necesario tooask para este nuevo.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-153">Then we want toostore hello user and stash hello token so we don't need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="ea8ab-154">código de Hello anterior toma cualquier usuario que se produce a tooauthenticate tooour server.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-154">hello previous code takes any user that happens tooauthenticate tooour server.</span></span> <span data-ttu-id="ea8ab-155">Esto se conoce como registro automático.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-155">This is known as auto-registration.</span></span> <span data-ttu-id="ea8ab-156">Se recomienda no permitir que cualquier usuario autenticar el servidor de producción de tooa sin tener primero que ellos registrarse a través de un proceso que haya decidido.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-156">We    recommend that you don't let anyone authenticate tooa production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="ea8ab-157">Suele ser el patrón de Hola que se ven en las aplicaciones de consumidor, que le permiten tooregister con Facebook, pero a continuación, pida tooprovide obtener información adicional.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-157">This is usually hello pattern you see in consumer apps, which allow you tooregister with Facebook but then ask you tooprovide additional information.</span></span> <span data-ttu-id="ea8ab-158">Si no fuese una aplicación de ejemplo, se pudo extrajeron dirección de correo electrónico del usuario de Hola de objeto de símbolo (token) de Hola que se devuelve y, a continuación, más frecuentes Hola usuario toofill información adicional.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-158">If this weren't a sample application, we could have extracted hello user's email address from hello token object that is returned and then asked hello user toofill out additional information.</span></span> <span data-ttu-id="ea8ab-159">Puesto que se trata de un servidor de prueba, se agregarlos base de datos de toohello en memoria.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-159">Because this is a test server, we add them toohello in-memory database.</span></span>


4. <span data-ttu-id="ea8ab-160">A continuación, vamos a agregar métodos de Hola que nos permitan tootrack Hola inició sesión a los usuarios según sea necesario por Passport.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-160">Next, let's add hello methods that enable us tootrack hello signed-in users as required by Passport.</span></span> <span data-ttu-id="ea8ab-161">Estos métodos incluyen serializar y deserializar la información del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-161">These methods include serializing and deserializing hello user's information.</span></span>

    ```JavaScript

            // Passport session setup. (Section 2)

            //   toosupport persistent sign-in sessions, Passport needs toobe able to
            //   serialize users into hello session and deserialize them out of hello session. Typically,
            //   this is done simply by storing hello user ID when serializing and finding
            //   hello user by ID when deserializing.
            passport.serializeUser(function(user, done) {
            done(null, user.email);
            });

            passport.deserializeUser(function(id, done) {
            findByEmail(id, function (err, user) {
                done(err, user);
            });
            });

            // array toohold signed-in users
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

5.  <span data-ttu-id="ea8ab-162">A continuación, vamos a agregar el motor de hello código tooload Hola Express.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-162">Next, let's add hello code tooload hello Express engine.</span></span> <span data-ttu-id="ea8ab-163">Aquí usamos Hola predeterminado /views y proporciona el patrón de /routes Express.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-163">Here we use hello default /views and /routes pattern that Express provides.</span></span>

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
          // Initialize Passport!  Also use passport.session() middleware, toosupport
          // persistent login sessions (recommended).
          app.use(passport.initialize());
          app.use(passport.session());
          app.use(app.router);
          app.use(express.static(__dirname + '/../../public'));
        });

    ```

6. <span data-ttu-id="ea8ab-164">Por último, vamos a agregar Hola enruta que entrega hello las solicitudes de inicio de sesión real toohello `passport-azure-ad` motor:</span><span class="sxs-lookup"><span data-stu-id="ea8ab-164">Finally, let's add hello routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>


       ```JavaScript

        // Our Auth routes (section 3)

        // GET /auth/openid
        //   Use passport.authenticate() as route middleware tooauthenticate the
        //   request. hello first step in OpenID authentication involves redirecting
        //   hello user tootheir OpenID provider. After authenticating, hello OpenID
        //   provider redirects hello user back toothis application at
        //   /auth/openid/return.
        app.get('/auth/openid',
        passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
        function(req, res) {
            log.info('Authentication was called in hello Sample');
            res.redirect('/');
        });

            // GET /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.get('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });

            // POST /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.post('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });
       ```


## <a name="step-4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="ea8ab-165">Paso 4: Inicio de sesión de Passport Use tooissue y solicitudes de cierre de sesión tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="ea8ab-165">Step 4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="ea8ab-166">La aplicación ya está toocommunicate configurada correctamente con el punto de conexión de hello mediante Protocolo de autenticación de OpenID Connect de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-166">Your app is now properly configured toocommunicate with hello endpoint by using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="ea8ab-167">`passport-azure-ad`se ocupa de todos los detalles de Hola de transmitir mensajes de autenticación, validar los tokens de Azure AD y mantener las sesiones de usuario.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-167">`passport-azure-ad` has taken care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="ea8ab-168">Lo único que queda es proporcionar a los usuarios una manera toosign en y cierre de sesión y recopilar información adicional sobre Hola firmado en los usuarios.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-168">All that remains is giving your users a way toosign in and sign out, and gathering additional information about hello signed-in users.</span></span>

1. <span data-ttu-id="ea8ab-169">En primer lugar, vamos a agregar predeterminado de hello, inicio de sesión, cuenta y métodos de cierre de sesión tooour `app.js` archivo:</span><span class="sxs-lookup"><span data-stu-id="ea8ab-169">First, let's add hello default, sign-in, account, and sign-out methods tooour `app.js` file:</span></span>

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
            log.info('Login was called in hello Sample');
            res.redirect('/');
        });

        app.get('/logout', function(req, res){
          req.logout();
          res.redirect('/');
        });

    ```

2.  <span data-ttu-id="ea8ab-170">Analicemos esto con detalle:</span><span class="sxs-lookup"><span data-stu-id="ea8ab-170">Let's review these in detail:</span></span>

  * <span data-ttu-id="ea8ab-171">Hola `/`ruta redirige toohello index.ejs vista y le pasa el usuario de hello en solicitud de hello (si existe).</span><span class="sxs-lookup"><span data-stu-id="ea8ab-171">hello `/`route redirects toohello index.ejs view, passing hello user in hello request (if it exists).</span></span>
  * <span data-ttu-id="ea8ab-172">Hola `/account` enrutar primero *garantiza que estamos autentican* (implementamos que en el siguiente ejemplo de Hola), y, a continuación, pasa Hola usuario en la solicitud de Hola para que podamos obtener información adicional acerca del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-172">hello `/account` route first *ensures we are authenticated* (we implement that in hello following example), and then passes hello user in hello request so that we can get additional information about hello user.</span></span>
  * <span data-ttu-id="ea8ab-173">Hola `/login` ruta llama a nuestro autenticador organización openidconnect desde `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-173">hello `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="ea8ab-174">Si no que no tiene éxito, redirige Hola usuario espera demasiado/inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-174">If that doesn't succeed, it redirects hello user back too/login.</span></span>
  * <span data-ttu-id="ea8ab-175">Hola `/logout` ruta simplemente llama hello logout.ejs (y ruta), que borra cookies y, a continuación, devuelve Hola tooindex.ejs atrás de usuario.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-175">hello `/logout` route simply calls hello logout.ejs (and route), which clears cookies and then returns hello user back tooindex.ejs.</span></span>

3. <span data-ttu-id="ea8ab-176">Para la última parte de Hola de `app.js`, vamos a agregar hello **EnsureAuthenticated** método que se usa en `/account`, como se muestra anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-176">For hello last part of `app.js`, let's add hello **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

    ```JavaScript

        // Simple route middleware tooensure user is authenticated. (section 4)

        //   Use this route middleware on any resource that needs toobe protected. If
        //   hello request is authenticated (typically via a persistent sign-in session),
        //   hello request proceeds. Otherwise, hello user is redirected toothe
        //   sign-in page.
        function ensureAuthenticated(req, res, next) {
          if (req.isAuthenticated()) { return next(); }
          res.redirect('/login')
        }
    ```

4. <span data-ttu-id="ea8ab-177">Por último, vamos a crear el propio servidor hello en `app.js`:</span><span class="sxs-lookup"><span data-stu-id="ea8ab-177">Finally, let's create hello server itself in `app.js`:</span></span>

```JavaScript

        app.listen(3000);

```


## <a name="step-5-toodisplay-our-user-in-hello-website-create-hello-views-and-routes-in-express"></a><span data-ttu-id="ea8ab-178">Paso 5: toodisplay nuestro usuario en el sitio Web de hello, crear vistas de Hola y las rutas en Express</span><span class="sxs-lookup"><span data-stu-id="ea8ab-178">Step 5: toodisplay our user in hello website, create hello views and routes in Express</span></span>
<span data-ttu-id="ea8ab-179">Ahora `app.js` se habrá completado.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-179">Now `app.js` is complete.</span></span> <span data-ttu-id="ea8ab-180">Simplemente necesita rutas de hello tooadd y vistas Hola información se obtiene toohello usuario, así como controlar hello `/logout` y `/login` rutas que hemos creado.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-180">We simply need tooadd hello routes and views that show hello information we get toohello user, as well as handle hello `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="ea8ab-181">Crear hello `/routes/index.js` ruta en el directorio raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-181">Create hello `/routes/index.js` route under hello root directory.</span></span>

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. <span data-ttu-id="ea8ab-182">Crear hello `/routes/user.js` ruta en el directorio raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-182">Create hello `/routes/user.js` route under hello root directory.</span></span>

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 <span data-ttu-id="ea8ab-183">Estos pasan a lo largo de vistas de tooour una solicitud hello, incluido el usuario de hello si está presente.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-183">These pass along hello request tooour views, including hello user if present.</span></span>

3. <span data-ttu-id="ea8ab-184">Crear hello `/views/index.ejs` vista bajo el directorio raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-184">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="ea8ab-185">Se trata de una página simple que llama a nuestros métodos de inicio de sesión y cierre de sesión y nos permite toograb la información de cuenta.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-185">This is a simple page that calls our login and logout methods and enables us toograb account information.</span></span> <span data-ttu-id="ea8ab-186">Tenga en cuenta que podemos usar Hola condicional `if (!user)` como usuario de Hola que se pasan a través de solicitud de saludo normal es evidencia tenemos un usuario con sesión iniciada.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-186">Notice that we can use hello conditional `if (!user)` as hello user being passed through in hello request is evidence we have a signed-in user.</span></span>

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

4. <span data-ttu-id="ea8ab-187">Crear hello `/views/account.ejs` ver en el directorio raíz de Hola para que podamos ver información adicional que `passport-azuread` ha puesto en la solicitud del usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-187">Create hello `/views/account.ejs` view under hello root directory so that we can view additional information that `passport-azuread` has put in hello user request.</span></span>

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

5. <span data-ttu-id="ea8ab-188">Vamos a mejorar la apariencia, para lo que agregaremos un diseño.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-188">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="ea8ab-189">Crear hello ' / directorio raíz de la vista de views/layout.ejs en Hola.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-189">Create hello '/views/layout.ejs' view under hello root directory.</span></span>

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

##<a name="next-steps"></a><span data-ttu-id="ea8ab-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ea8ab-190">Next steps</span></span>
<span data-ttu-id="ea8ab-191">Por último, compile y ejecute su aplicación.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-191">Finally, build and run your app.</span></span> <span data-ttu-id="ea8ab-192">Ejecutar `node app.js`y, a continuación, vaya demasiado`http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-192">Run `node app.js`, and then go too`http://localhost:3000`.</span></span>

<span data-ttu-id="ea8ab-193">Inicie sesión con una cuenta Microsoft personal o una cuenta profesional o educativa y observe cómo se refleja la identidad del usuario de hello en lista de hello AccountType.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-193">Sign in with either a personal Microsoft account or a work or school account, and notice how hello user's identity is reflected in hello /account list.</span></span> <span data-ttu-id="ea8ab-194">Ahora dispone de una aplicación web que está protegida mediante protocolos estándar del sector que pueden autenticar a los usuarios tanto con sus cuentas personales como con sus cuentas profesionales o educativas.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-194">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="ea8ab-195">Como referencia, Hola completado ejemplo (sin los valores de configuración) [se proporciona como un archivo .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="ea8ab-195">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="ea8ab-196">Como alternativa, puede clonarlo desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="ea8ab-196">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="ea8ab-197">Ahora puede pasar a temas más avanzados.</span><span class="sxs-lookup"><span data-stu-id="ea8ab-197">You can now move onto more advanced topics.</span></span> <span data-ttu-id="ea8ab-198">Puede ser conveniente tootry:</span><span class="sxs-lookup"><span data-stu-id="ea8ab-198">You might want tootry:</span></span>

[<span data-ttu-id="ea8ab-199">Protección de una API web con Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea8ab-199">Secure a Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
