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
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a>Inicio y cierre de sesión de aplicación web de Node.js con Azure AD
Aquí usamos Passport para:

* Inicio de sesión Hola usuario en aplicaciones de toohello con Azure Active Directory (Azure AD).
* Mostrar información acerca del usuario de Hola.
* Inicio de sesión Hola usuario fuera de la aplicación hello.

Passport es middleware de autenticación para Node.js. Flexible y modular, Passport puede quitarse de forma discreta en tooany basada en Express o restify la aplicación web. Un conjunto completo de estrategias admiten la autenticación que usa un nombre de usuario y una contraseña, Facebook, Twitter y mucho más. Hemos desarrollado una estrategia para Microsoft Azure Active Directory. Se instale este módulo y, a continuación, agregue Hola Microsoft Azure Active Directory `passport-azure-ad` complemento.

toodo, Hola toman pasos:

1. Registrar una aplicación.
2. Configurar el saludo de toouse aplicación `passport-azure-ad` estrategia.
3. Usar inicio de sesión de Passport tooissue y solicitudes de cierre de sesión tooAzure AD.
4. Imprimir datos acerca del usuario de Hola.

código de Hello para este tutorial se mantiene [en GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).  toofollow a lo largo, puede [descargar el esqueleto de la aplicación hello como un archivo .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) o esqueleto de Hola de clon:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

final de Hola de este tutorial también se incluye aplicación Hello completado.

## <a name="step-1-register-an-app"></a>Paso 1: Registro de una aplicación
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).

2. En menú Hola al principio de Hola de página de hello, seleccione su cuenta. En hello **Directory** lista, seleccione la aplicación de inquilino de Active Directory de Hola donde desea tooregister.

3. Seleccione **más servicios** en hello menú Hola izquierda lateral de la pantalla de bienvenida y, a continuación, seleccione **Azure Active Directory**.

4. Seleccione **Registros de aplicaciones** y luego seleccione **Agregar**.

5. Siga Hola indicaciones toocreate una **aplicación Web** o **WebAPI**.
  * Hola **nombre** de hello aplicación describe su toousers de aplicación.

  * Hola **dirección URL de inicio de sesión** es Hola dirección URL base de la aplicación.  Hello valor predeterminado del esqueleto es ' http://localhost:3000/auth/openid/retorno ''.

6. Después de registrarse, Azure AD asigna a la aplicación un identificador de aplicación único. Necesita este valor en la siguiente Hola secciones, por lo tanto cópiela desde la página de aplicación Hola.
7. De hello **configuración** -> **propiedades** página de la aplicación, actualice Hola App ID URI. Hola **App ID URI** es un identificador único para la aplicación. convención de Hello es el formato de hello toouse `https://<tenant-domain>/<app-name>`, por ejemplo: `https://contoso.onmicrosoft.com/my-first-aad-app`.

## <a name="step-2-add-prerequisites-tooyour-directory"></a>Paso 2: Agregar un directorio tooyour de requisitos previos
1. Desde la línea de comandos de hello, cambiar carpeta de raíz de tooyour de directorios si no está ya no existe, y, a continuación, siga los comandos Hola de ejecución:

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. Además, necesita `passport-azure-ad`:
    * `npm install passport-azure-ad`

Esto instala las bibliotecas de Hola que `passport-azure-ad` depende.

## <a name="step-3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>Paso 3: Configurar la estrategia de aplicación toouse Hola js de nodo de passport
En este caso, configuramos el protocolo de autenticación OpenID Connect de Express toouse Hola.  Passport es toodo usa varios elementos, incluidas las solicitudes problema de inicio de sesión y cierre de sesión, administrar la sesión del usuario de Hola y obtener información acerca del usuario de Hola.

1. toobegin, abra hello `config.js` de archivos en raíz de Hola de proyecto de hello y, a continuación, escriba los valores de configuración de la aplicación Hola `exports.creds` sección.

  * Hola `clientID` es hello **identificador de la aplicación** que está asignado tooyour aplicación de portal de registro de hello.

  * Hola `returnURL` es hello **Uri de redireccionamiento** especificado en el portal de Hola.

  * Hola `clientSecret` es secreto Hola que generó en el portal de Hola.

2. A continuación, abra hello `app.js` archivo en hello raíz del proyecto de Hola. A continuación, agregue Hola después llamada tooinvoke hello `OIDCStrategy` estrategia que se incluye con `passport-azure-ad`.

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. Después, usar la estrategia de Hola se simplemente hace referencia a toohandle las solicitudes de inicio de sesión.

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
Passport usa un patrón similar para todas sus estrategias (Twitter, Facebook, etc.) al que se ajustan todos los escritores de estrategias. Examinando la estrategia de hello, verá que pasamos una función que tiene un token y un hecho como parámetros de Hola. estrategia de Hello incluye volver toous después de que realice su trabajo. A continuación, deseamos toostore usuario de Hola y token de hello complementario por lo que no es necesario tooask para este nuevo.

> [!IMPORTANT]
código de Hello anterior toma cualquier usuario que se produce a tooauthenticate tooour server. Esto se conoce como registro automático. Se recomienda no permitir que cualquier usuario autenticar el servidor de producción de tooa sin tener primero que ellos registrarse a través de un proceso que haya decidido. Suele ser el patrón de Hola que se ven en las aplicaciones de consumidor, que le permiten tooregister con Facebook, pero a continuación, pida tooprovide obtener información adicional. Si no fuese una aplicación de ejemplo, se pudo extrajeron dirección de correo electrónico del usuario de Hola de objeto de símbolo (token) de Hola que se devuelve y, a continuación, más frecuentes Hola usuario toofill información adicional. Puesto que se trata de un servidor de prueba, se agregarlos base de datos de toohello en memoria.


4. A continuación, vamos a agregar métodos de Hola que nos permitan tootrack Hola inició sesión a los usuarios según sea necesario por Passport. Estos métodos incluyen serializar y deserializar la información del usuario de Hola.

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

5.  A continuación, vamos a agregar el motor de hello código tooload Hola Express. Aquí usamos Hola predeterminado /views y proporciona el patrón de /routes Express.

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

6. Por último, vamos a agregar Hola enruta que entrega hello las solicitudes de inicio de sesión real toohello `passport-azure-ad` motor:


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


## <a name="step-4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Paso 4: Inicio de sesión de Passport Use tooissue y solicitudes de cierre de sesión tooAzure AD
La aplicación ya está toocommunicate configurada correctamente con el punto de conexión de hello mediante Protocolo de autenticación de OpenID Connect de Hola.  `passport-azure-ad`se ocupa de todos los detalles de Hola de transmitir mensajes de autenticación, validar los tokens de Azure AD y mantener las sesiones de usuario. Lo único que queda es proporcionar a los usuarios una manera toosign en y cierre de sesión y recopilar información adicional sobre Hola firmado en los usuarios.

1. En primer lugar, vamos a agregar predeterminado de hello, inicio de sesión, cuenta y métodos de cierre de sesión tooour `app.js` archivo:

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

2.  Analicemos esto con detalle:

  * Hola `/`ruta redirige toohello index.ejs vista y le pasa el usuario de hello en solicitud de hello (si existe).
  * Hola `/account` enrutar primero *garantiza que estamos autentican* (implementamos que en el siguiente ejemplo de Hola), y, a continuación, pasa Hola usuario en la solicitud de Hola para que podamos obtener información adicional acerca del usuario de Hola.
  * Hola `/login` ruta llama a nuestro autenticador organización openidconnect desde `passport-azuread`. Si no que no tiene éxito, redirige Hola usuario espera demasiado/inicio de sesión.
  * Hola `/logout` ruta simplemente llama hello logout.ejs (y ruta), que borra cookies y, a continuación, devuelve Hola tooindex.ejs atrás de usuario.

3. Para la última parte de Hola de `app.js`, vamos a agregar hello **EnsureAuthenticated** método que se usa en `/account`, como se muestra anteriormente.

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

4. Por último, vamos a crear el propio servidor hello en `app.js`:

```JavaScript

        app.listen(3000);

```


## <a name="step-5-toodisplay-our-user-in-hello-website-create-hello-views-and-routes-in-express"></a>Paso 5: toodisplay nuestro usuario en el sitio Web de hello, crear vistas de Hola y las rutas en Express
Ahora `app.js` se habrá completado. Simplemente necesita rutas de hello tooadd y vistas Hola información se obtiene toohello usuario, así como controlar hello `/logout` y `/login` rutas que hemos creado.

1. Crear hello `/routes/index.js` ruta en el directorio raíz de Hola.

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. Crear hello `/routes/user.js` ruta en el directorio raíz de Hola.

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 Estos pasan a lo largo de vistas de tooour una solicitud hello, incluido el usuario de hello si está presente.

3. Crear hello `/views/index.ejs` vista bajo el directorio raíz de Hola. Se trata de una página simple que llama a nuestros métodos de inicio de sesión y cierre de sesión y nos permite toograb la información de cuenta. Tenga en cuenta que podemos usar Hola condicional `if (!user)` como usuario de Hola que se pasan a través de solicitud de saludo normal es evidencia tenemos un usuario con sesión iniciada.

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

4. Crear hello `/views/account.ejs` ver en el directorio raíz de Hola para que podamos ver información adicional que `passport-azuread` ha puesto en la solicitud del usuario Hola.

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

5. Vamos a mejorar la apariencia, para lo que agregaremos un diseño. Crear hello ' / directorio raíz de la vista de views/layout.ejs en Hola.

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

##<a name="next-steps"></a>Pasos siguientes
Por último, compile y ejecute su aplicación. Ejecutar `node app.js`y, a continuación, vaya demasiado`http://localhost:3000`.

Inicie sesión con una cuenta Microsoft personal o una cuenta profesional o educativa y observe cómo se refleja la identidad del usuario de hello en lista de hello AccountType. Ahora dispone de una aplicación web que está protegida mediante protocolos estándar del sector que pueden autenticar a los usuarios tanto con sus cuentas personales como con sus cuentas profesionales o educativas.

Como referencia, Hola completado ejemplo (sin los valores de configuración) [se proporciona como un archivo .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip). Como alternativa, puede clonarlo desde GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

Ahora puede pasar a temas más avanzados. Puede ser conveniente tootry:

[Protección de una API web con Azure AD](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
