---
title: "aaaUsing Twilio para voz, VoIP y mensajería SMS en Azure"
description: "Obtenga información acerca de cómo toomake una llamada de teléfono así como enviar un SMS de mensajes con el servicio de API de Twilio de hello en Azure. Ejemplos de código escritos en Node.js."
services: 
documentationcenter: nodejs
author: devinrader
manager: wpickett
editor: 
ms.assetid: f558cbbd-13d2-416f-b9b1-33a99c426af9
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 11/25/2014
ms.author: wpickett
ms.openlocfilehash: 6c44d60e217fcdf51e69fd2a8197f979afbb507a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a><span data-ttu-id="00c16-104">Uso de Twilio para voz, VoIP y mensajería SMS en Azure</span><span class="sxs-lookup"><span data-stu-id="00c16-104">Using Twilio for Voice, VoIP, and SMS Messaging in Azure</span></span>
<span data-ttu-id="00c16-105">Esta guía se demuestra cómo toobuild aplicaciones que se comunican con Twilio y node.js en Azure.</span><span class="sxs-lookup"><span data-stu-id="00c16-105">This guide demonstrates how toobuild apps that communicate with Twilio and node.js on Azure.</span></span>

<a id="whatis"/>

## <a name="what-is-twilio"></a><span data-ttu-id="00c16-106">¿Qué es Twilio?</span><span class="sxs-lookup"><span data-stu-id="00c16-106">What is Twilio?</span></span>
<span data-ttu-id="00c16-107">Twilio es una plataforma de API que facilita a los desarrolladores toomake y recibe llamadas telefónicas, enviar y recibir mensajes de texto e incrustar una llamada de VoIP a aplicaciones móviles basadas en el explorador y nativo.</span><span class="sxs-lookup"><span data-stu-id="00c16-107">Twilio is an API platform that makes it easy for developers toomake and receive phone calls, send and receive text messages, and embed VoIP calling into browser-based and native mobile applications.</span></span> <span data-ttu-id="00c16-108">Revisemos brevemente su funcionamiento antes de analizar los detalles.</span><span class="sxs-lookup"><span data-stu-id="00c16-108">Let's briefly go over how this works before diving in.</span></span>

### <a name="receiving-calls-and-text-messages"></a><span data-ttu-id="00c16-109">Recepción de llamadas y mensajes de texto</span><span class="sxs-lookup"><span data-stu-id="00c16-109">Receiving Calls and Text Messages</span></span>
<span data-ttu-id="00c16-110">Twilio permite a los desarrolladores demasiado[números de teléfono programables de compra] [ purchase_phone] que puede ser usado tooboth enviar y recibir llamadas y mensajes de texto.</span><span class="sxs-lookup"><span data-stu-id="00c16-110">Twilio allows developers too[purchase programmable phone numbers][purchase_phone] which can be used tooboth send and receive calls and text messages.</span></span> <span data-ttu-id="00c16-111">Cuando un número de Twilio recibe una llamada entrante o texto, Twilio enviará la aplicación web un HTTP POST o una solicitud GET, que le pide que para obtener instrucciones sobre cómo toohandle Hola llamada o texto.</span><span class="sxs-lookup"><span data-stu-id="00c16-111">When a Twilio number receives an inbound call or text, Twilio will send your web application an HTTP POST or GET request, asking you for instructions on how toohandle hello call or text.</span></span> <span data-ttu-id="00c16-112">El servidor responderá a solicitudes HTTP del tooTwilio con [TwiML][twiml], un sencillo conjunto de etiquetas XML que contienen instrucciones sobre cómo toohandle una llamada o texto.</span><span class="sxs-lookup"><span data-stu-id="00c16-112">Your server will respond tooTwilio's HTTP request with [TwiML][twiml], a simple set of XML tags that contain instructions on how toohandle a call or text.</span></span> <span data-ttu-id="00c16-113">Veremos ejemplos de TwiML en un momento.</span><span class="sxs-lookup"><span data-stu-id="00c16-113">We will see examples of TwiML in just a moment.</span></span>

### <a name="making-calls-and-sending-text-messages"></a><span data-ttu-id="00c16-114">Realización de llamadas y envío de mensajes de texto</span><span class="sxs-lookup"><span data-stu-id="00c16-114">Making Calls and Sending Text Messages</span></span>
<span data-ttu-id="00c16-115">Al realizar solicitudes HTTP toohello Twilio API del servicio web, los desarrolladores pueden enviar mensajes de texto o iniciar llamadas telefónicas salientes.</span><span class="sxs-lookup"><span data-stu-id="00c16-115">By making HTTP requests toohello Twilio web service API, developers can send text messages or initiate outbound phone calls.</span></span> <span data-ttu-id="00c16-116">Para las llamadas salientes, programador de hello también debe especificar una dirección URL que devuelve TwiML instrucciones de cómo llamar toohandle Hola salida una vez que está conectado.</span><span class="sxs-lookup"><span data-stu-id="00c16-116">For outbound calls, hello developer must also specify a URL that returns TwiML instructions for how toohandle hello outbound call once it is connected.</span></span>

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a><span data-ttu-id="00c16-117">Inserción de funcionalidades de VoIP en código de interfaz de usuario (JavaScript, iOS o Android)</span><span class="sxs-lookup"><span data-stu-id="00c16-117">Embedding VoIP Capabilities in UI code (JavaScript, iOS, or Android)</span></span>
<span data-ttu-id="00c16-118">Twilio brinda un SDK de cliente que puede transformar cualquier explorador web de escritorio, aplicación iOS o aplicación Android en un teléfono de VoIP.</span><span class="sxs-lookup"><span data-stu-id="00c16-118">Twilio provides a client-side SDK which can turn any desktop web browser, iOS app, or Android app into a VoIP phone.</span></span> <span data-ttu-id="00c16-119">En este artículo, nos centraremos en cómo toouse VoIP de llamada en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="00c16-119">In this article, we will focus on how toouse VoIP calling in hello browser.</span></span> <span data-ttu-id="00c16-120">En suma toohello *Twilio JavaScript SDK* se ejecuta en el Explorador de hello, una aplicación de servidor (nuestra aplicación node.js) debe ser tooissue usado un toohello "token capacidad" cliente de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="00c16-120">In addition toohello *Twilio JavaScript SDK* running in hello browser, a server-side application (our node.js application) must be used tooissue a "capability token" toohello JavaScript client.</span></span> <span data-ttu-id="00c16-121">Puede leer más sobre el uso de VoIP con node.js [en el blog de desarrollo de hello Twilio][voipnode].</span><span class="sxs-lookup"><span data-stu-id="00c16-121">You can read more about using VoIP with node.js [on hello Twilio dev blog][voipnode].</span></span>

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a><span data-ttu-id="00c16-122">Suscripción en Twilio (con descuento de Microsoft)</span><span class="sxs-lookup"><span data-stu-id="00c16-122">Sign Up For Twilio (Microsoft Discount)</span></span>
<span data-ttu-id="00c16-123">Antes de usar servicios de Twilio, debe [registrarse para obtener una cuenta][signup].</span><span class="sxs-lookup"><span data-stu-id="00c16-123">Before using Twilio services, you must first [sign up for an account][signup].</span></span> <span data-ttu-id="00c16-124">Los clientes de Microsoft Azure reciben un descuento especial - [ser seguro toosign aquí][signup]!</span><span class="sxs-lookup"><span data-stu-id="00c16-124">Microsoft Azure customers receive a special discount - [be sure toosign up here][signup]!</span></span>

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a><span data-ttu-id="00c16-125">Creación e implementación de un sitio web de Azure para Node.js</span><span class="sxs-lookup"><span data-stu-id="00c16-125">Create and Deploy a node.js Azure Website</span></span>
<span data-ttu-id="00c16-126">A continuación, deberá toocreate un sitio Web de node.js ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="00c16-126">Next, you will need toocreate a node.js website running on Azure.</span></span> <span data-ttu-id="00c16-127">[documentación oficial de Hola para realizar esta acción se encuentra aquí][azure_new_site].</span><span class="sxs-lookup"><span data-stu-id="00c16-127">[hello official documentation for doing this is located here][azure_new_site].</span></span> <span data-ttu-id="00c16-128">En un nivel alto, va a realizar siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="00c16-128">At a high level, you will be doing hello following:</span></span>

* <span data-ttu-id="00c16-129">Suscripción para obtener una cuenta de Azure, si todavía no tiene una</span><span class="sxs-lookup"><span data-stu-id="00c16-129">Signing up for an Azure account, if you don't have one already</span></span>
* <span data-ttu-id="00c16-130">Uso de toocreate de consola de administración de Azure de hello un nuevo sitio Web</span><span class="sxs-lookup"><span data-stu-id="00c16-130">Using hello Azure admin console toocreate a new website</span></span>
* <span data-ttu-id="00c16-131">Incorporación de compatibilidad con control de código fuente (supondremos que usó Git)</span><span class="sxs-lookup"><span data-stu-id="00c16-131">Adding source control support (we will assume you used git)</span></span>
* <span data-ttu-id="00c16-132">Creación de un archivo `server.js` con una simple aplicación web node.js</span><span class="sxs-lookup"><span data-stu-id="00c16-132">Creating a file `server.js` with a simple node.js web application</span></span>
* <span data-ttu-id="00c16-133">Implementar esta aplicación simple tooAzure</span><span class="sxs-lookup"><span data-stu-id="00c16-133">Deploying this simple application tooAzure</span></span>

<a id="twiliomodule"/>

## <a name="configure-hello-twilio-module"></a><span data-ttu-id="00c16-134">Configurar hello Twilio módulo</span><span class="sxs-lookup"><span data-stu-id="00c16-134">Configure hello Twilio Module</span></span>
<span data-ttu-id="00c16-135">A continuación, empezaremos a toowrite una aplicación node.js simple que hace uso de hello Twilio API.</span><span class="sxs-lookup"><span data-stu-id="00c16-135">Next, we will begin toowrite a simple node.js application which makes use of hello Twilio API.</span></span> <span data-ttu-id="00c16-136">Antes de comenzar, debemos tooconfigure nuestras credenciales de cuenta de Twilio.</span><span class="sxs-lookup"><span data-stu-id="00c16-136">Before we begin, we need tooconfigure our Twilio account credentials.</span></span>

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a><span data-ttu-id="00c16-137">Configuración de credenciales de Twilio en variables de entorno del sistema</span><span class="sxs-lookup"><span data-stu-id="00c16-137">Configuring Twilio Credentials in System Environment Variables</span></span>
<span data-ttu-id="00c16-138">En solicitudes de pedido de toomake autenticado contra Hola Twilio back-end, necesitamos nuestro SID de la cuenta y el token de autenticación, qué función como nombre de usuario de Hola y la contraseña configurados para la cuenta de Twilio.</span><span class="sxs-lookup"><span data-stu-id="00c16-138">In order toomake authenticated requests against hello Twilio back end, we need our account SID and auth token, which function as hello username and password set for our Twilio account.</span></span> <span data-ttu-id="00c16-139">tooconfigure de manera más segura de Hello estos para su uso con el módulo de nodo de hello en Azure es a través de las variables de entorno de sistema, lo que se pueden establecer directamente en la consola de administración de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="00c16-139">hello most secure way tooconfigure these for use with hello node module in Azure is via system environment variables, which you can set directly in hello Azure admin console.</span></span>

<span data-ttu-id="00c16-140">Seleccione el sitio Web de node.js y haga clic en el vínculo de "Configurar" Hola.</span><span class="sxs-lookup"><span data-stu-id="00c16-140">Select your node.js website, and click hello "CONFIGURE" link.</span></span>  <span data-ttu-id="00c16-141">Si se desplaza un poco hacia abajo, verá un área en la que puede definir las propiedades de configuración para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="00c16-141">If you scroll down a bit, you will see an area where you can set configuration properties for your application.</span></span>  <span data-ttu-id="00c16-142">Escriba sus credenciales de cuenta de Twilio ([se encuentra en la consola de Twilio][twilio_console]) tal como se muestra: hacer seguro tooname les `TWILIO_ACCOUNT_SID` y `TWILIO_AUTH_TOKEN`, respectivamente:</span><span class="sxs-lookup"><span data-stu-id="00c16-142">Enter your Twilio account credentials ([found on your Twilio Console][twilio_console]) as shown - make sure tooname them `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`, respectively:</span></span>

![Consola de administración de Azure][azure-admin-console]

<span data-ttu-id="00c16-144">Una vez haya configurado estas variables, reinicie la aplicación Hola consola de Azure.</span><span class="sxs-lookup"><span data-stu-id="00c16-144">Once you have configured these variables, restart your application in hello Azure console.</span></span>

### <a name="declaring-hello-twilio-module-in-packagejson"></a><span data-ttu-id="00c16-145">Declaración de módulo de Twilio de hello en package.json</span><span class="sxs-lookup"><span data-stu-id="00c16-145">Declaring hello Twilio module in package.json</span></span>
<span data-ttu-id="00c16-146">A continuación, necesitamos toocreate una toomanage package.json nuestro dependencias de módulo de nodo a través de [npm].</span><span class="sxs-lookup"><span data-stu-id="00c16-146">Next, we need toocreate a package.json toomanage our node module dependencies via [npm].</span></span> <span data-ttu-id="00c16-147">En hello en el mismo nivel como hello `server.js` archivo que creó en hello *Azure/node.js* tutorial, cree un archivo denominado `package.json`.</span><span class="sxs-lookup"><span data-stu-id="00c16-147">At hello same level as hello `server.js` file you created in hello *Azure/node.js* tutorial, create a file named `package.json`.</span></span>  <span data-ttu-id="00c16-148">En este archivo, coloque el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="00c16-148">Inside this file, place hello following:</span></span>

```json
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node server"
  },
  "dependencies": {
    "body-parser": "^1.16.1",
    "ejs": "^2.5.5",
    "errorhandler": "^1.5.0",
    "express": "^4.14.1",
    "morgan": "^1.8.1",
    "twilio": "^2.11.1"
  }
}
```

<span data-ttu-id="00c16-149">Esto declara módulo de twilio de hello como una dependencia, así como Hola populares [Express marco web] [ express] y motor de plantillas EJS Hola.</span><span class="sxs-lookup"><span data-stu-id="00c16-149">This declares hello twilio module as a dependency, as well as hello popular [Express web framework][express] and hello EJS template engine.</span></span>  <span data-ttu-id="00c16-150">Ahora ya estamos: comencemos a escribir código.</span><span class="sxs-lookup"><span data-stu-id="00c16-150">Okay, now we're all set - let's write some code!</span></span>

<a id="makecall"/>

## <a name="make-an-outbound-call"></a><span data-ttu-id="00c16-151">Realización de una llamada saliente</span><span class="sxs-lookup"><span data-stu-id="00c16-151">Make an Outbound Call</span></span>
<span data-ttu-id="00c16-152">Vamos a crear un formulario simple que se colocará un número de tooa de llamada que se elija.</span><span class="sxs-lookup"><span data-stu-id="00c16-152">Let's create a simple form that will place a call tooa number we choose.</span></span> <span data-ttu-id="00c16-153">Abra `server.js`y escriba el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="00c16-153">Open up `server.js`, and enter hello following code.</span></span> <span data-ttu-id="00c16-154">Tenga en cuenta que dice "CHANGE_ME" - he puesto ahí nombre Hola de su sitio Web de azure:</span><span class="sxs-lookup"><span data-stu-id="00c16-154">Note where it says "CHANGE_ME" - put hello name of your azure website there:</span></span>

```javascript
// Module dependencies
const express = require('express');
const path = require('path');
const http = require('http');
const twilio = require('twilio');
const logger = require('morgan');
const bodyParser = require('body-parser');
const errorHandler = require('errorhandler');
const accountSid = process.env.TWILIO_ACCOUNT_SID;
const authToken = process.env.TWILIO_AUTH_TOKEN;
// Create Express web application
const app = express();

// Express configuration
app.set('port', process.env.PORT || 3000);
app.set('views', __dirname + '/views');
app.set('view engine', 'ejs');
app.use(logger('tiny'));
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())
app.use(express.static(path.join(__dirname, 'public')));

if (app.get('env') !== 'production') {
  app.use(errorHandler());
}

// Render an HTML user interface for hello application's home page
app.get('/', (request, response) => response.render('index'));

// Handle hello form POST tooplace a call
app.post('/call', (request, response) => {
  var client = twilio(accountSid, authToken);

  client.makeCall({
    // make a call toothis number
    to:request.body.number,

    // Change tooa Twilio number you bought - see:
    // https://www.twilio.com/console/phone-numbers/incoming
    from:'+15558675309',

    // A URL in our app which generates TwiML
    // Change "CHANGE_ME" tooyour app's name
    url:'https://CHANGE_ME.azurewebsites.net/outbound_call'
  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});

// Generate TwiML toohandle an outbound call
app.post('/outbound_call', (request, response) => {
  var twiml = new twilio.TwimlResponse();

  // Say a message toohello call's receiver
  twiml.say('hello - thanks for checking out Twilio and Azure', {
      voice:'woman'
  });

  response.set('Content-Type', 'text/xml');
  response.send(twiml.toString());
});

// Start server
app.listen(app.get('port'), function(){
  console.log(`Express server listening on port ${app.get('port')}`);
});
```

<span data-ttu-id="00c16-155">A continuación, cree un directorio denominado `views` : en este directorio, cree un archivo denominado `index.ejs` con hello siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="00c16-155">Next, create a directory called `views` - inside this directory, create a file named `index.ejs` with hello following contents:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
  <title>Twilio Test</title>
  <style>
    input { height:20px; width:300px; font-size:18px; margin:5px; padding:5px; }
  </style>
</head>
<body>
  <h1>Twilio Test</h1>
  <form action="/call" method="POST">
      <input placeholder="Enter a phone number" name="number"/>
      <br/>
      <input type="submit" value="Call hello number above"/>
  </form>
</body>
</html>
```

<span data-ttu-id="00c16-156">Ahora, implemente su tooAzure del sitio Web y abra su hogar.</span><span class="sxs-lookup"><span data-stu-id="00c16-156">Now, deploy your website tooAzure and open your home.</span></span> <span data-ttu-id="00c16-157">Debe ser capaz de tooenter el número de teléfono en el campo de texto de Hola y recibe una llamada desde el número de Twilio!</span><span class="sxs-lookup"><span data-stu-id="00c16-157">You should be able tooenter your phone number in hello text field, and receive a call from your Twilio number!</span></span>

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a><span data-ttu-id="00c16-158">Envío de un mensaje SMS</span><span class="sxs-lookup"><span data-stu-id="00c16-158">Send an SMS Message</span></span>
<span data-ttu-id="00c16-159">Ahora, vamos a configurar una interfaz de usuario y toosend de lógica de control de formularios un mensaje de texto.</span><span class="sxs-lookup"><span data-stu-id="00c16-159">Now, let's set up a user interface and form handling logic toosend a text message.</span></span> <span data-ttu-id="00c16-160">Abra `server.js`y agregue Hola siguiente código después de la última llamada de hello demasiado`app.post`:</span><span class="sxs-lookup"><span data-stu-id="00c16-160">Open up `server.js`, and add hello following code after hello last call too`app.post`:</span></span>

```javascript
app.post('/sms', (request, response) => {
  const client = twilio(accountSid, authToken);

  client.sendSms({
      // send a text toothis number
      to:request.body.number,

      // A Twilio number you bought - see:
      // https://www.twilio.com/console/phone-numbers/incoming
      from:'+15558675309',

      // hello body of hello text message
      body: request.body.message

  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});
```

<span data-ttu-id="00c16-161">En `views/index.ejs`, agregue otra forma bajo hello primero toosubmit un número y un mensaje de texto:</span><span class="sxs-lookup"><span data-stu-id="00c16-161">In `views/index.ejs`, add another form under hello first one toosubmit a number and a text message:</span></span>

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message toosend" name="message"/>
  <br/>
  <input type="submit" value="Send text toohello number above"/>
</form>
```

<span data-ttu-id="00c16-162">Volver a implementar la aplicación tooAzure y ahora debe ser capaz de toosubmit que forman y enviar a usted (o cualquiera de sus amigos más cercanos) un mensaje de texto.</span><span class="sxs-lookup"><span data-stu-id="00c16-162">Re-deploy your application tooAzure, and you should now be able toosubmit that form and send yourself (or any of your closest friends) a text message!</span></span>

<a id="nextsteps"/>

## <a name="next-steps"></a><span data-ttu-id="00c16-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="00c16-163">Next Steps</span></span>
<span data-ttu-id="00c16-164">Ya ha aprendido Fundamentos de hello del uso de node.js y Twilio toobuild aplicaciones que se comunican.</span><span class="sxs-lookup"><span data-stu-id="00c16-164">You have now learned hello basics of using node.js and Twilio toobuild apps that communicate.</span></span> <span data-ttu-id="00c16-165">Pero estos ejemplos apenas scratch superficie Hola de lo que es posible con Twilio y node.js.</span><span class="sxs-lookup"><span data-stu-id="00c16-165">But these examples barely scratch hello surface of what's possible with Twilio and node.js.</span></span> <span data-ttu-id="00c16-166">Para obtener más información con Twilio node.js, desproteger Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="00c16-166">For more information using Twilio with node.js, check out hello following resources:</span></span>

* <span data-ttu-id="00c16-167">[Documentos oficiales de módulo][docs]</span><span class="sxs-lookup"><span data-stu-id="00c16-167">[Official module docs][docs]</span></span>
* <span data-ttu-id="00c16-168">[Tutorial de VoIP con aplicaciones node.js][voipnode]</span><span class="sxs-lookup"><span data-stu-id="00c16-168">[Tutorial on VoIP with node.js applications][voipnode]</span></span>
* <span data-ttu-id="00c16-169">[Votr: una aplicación de votación en tiempo real por medio de SMS con node.js y CouchDB (tres partes)][votr]</span><span class="sxs-lookup"><span data-stu-id="00c16-169">[Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr]</span></span>
* <span data-ttu-id="00c16-170">[Programación de par en el Explorador de hello con node.js][pair]</span><span class="sxs-lookup"><span data-stu-id="00c16-170">[Pair programming in hello browser with node.js][pair]</span></span>

<span data-ttu-id="00c16-171">Esperamos que disfrute del acceso a Node.js y Twilio en Azure.</span><span class="sxs-lookup"><span data-stu-id="00c16-171">We hope you love hacking node.js and Twilio on Azure!</span></span>

[purchase_phone]: https://www.twilio.com/console/phone-numbers/search
[twiml]: https://www.twilio.com/docs/api/twiml
[signup]: http://ahoy.twilio.com/azure
[azure_new_site]: app-service-web/app-service-web-get-started-nodejs.md
[twilio_console]: https://www.twilio.com/console
[npm]: http://npmjs.org
[express]: http://expressjs.com
[voipnode]: http://www.twilio.com/blog/2013/04/introduction-to-twilio-client-with-node-js.html
[docs]: http://twilio.github.io/twilio-node/
[votr]: http://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html
[pair]: http://www.twilio.com/blog/2013/06/pair-programming-in-the-browser-with-twilio.html
[azure-admin-console]: ./media/partner-twilio-nodejs-how-to-use-voice-sms/twilio_1.png
