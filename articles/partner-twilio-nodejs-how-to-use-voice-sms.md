---
title: "Uso de Twilio para voz, VoIP y mensajería SMS en Azure"
description: "Aprenda a realizar llamadas telefónicas y a enviar mensajes SMS con el servicio de la API de Twilio en Azure. Ejemplos de código escritos en Node.js."
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
ms.openlocfilehash: 44ec97812130d41d75be98fc8e2d846b7cb5c913
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a><span data-ttu-id="f6070-104">Uso de Twilio para voz, VoIP y mensajería SMS en Azure</span><span class="sxs-lookup"><span data-stu-id="f6070-104">Using Twilio for Voice, VoIP, and SMS Messaging in Azure</span></span>
<span data-ttu-id="f6070-105">Esta guía demuestra cómo crear aplicaciones que se comunican con Twilio y Node.js en Azure.</span><span class="sxs-lookup"><span data-stu-id="f6070-105">This guide demonstrates how to build apps that communicate with Twilio and node.js on Azure.</span></span>

<a id="whatis"/>

## <a name="what-is-twilio"></a><span data-ttu-id="f6070-106">¿Qué es Twilio?</span><span class="sxs-lookup"><span data-stu-id="f6070-106">What is Twilio?</span></span>
<span data-ttu-id="f6070-107">Twilio es una plataforma de API que hace que los desarrolladores puedan hacer y recibir llamadas telefónicas, enviar y recibir mensajes de texto e insertar llamadas de VoIP en aplicaciones móviles nativas o basadas en explorador de manera sencilla.</span><span class="sxs-lookup"><span data-stu-id="f6070-107">Twilio is an API platform that makes it easy for developers to make and receive phone calls, send and receive text messages, and embed VoIP calling into browser-based and native mobile applications.</span></span> <span data-ttu-id="f6070-108">Revisemos brevemente su funcionamiento antes de analizar los detalles.</span><span class="sxs-lookup"><span data-stu-id="f6070-108">Let's briefly go over how this works before diving in.</span></span>

### <a name="receiving-calls-and-text-messages"></a><span data-ttu-id="f6070-109">Recepción de llamadas y mensajes de texto</span><span class="sxs-lookup"><span data-stu-id="f6070-109">Receiving Calls and Text Messages</span></span>
<span data-ttu-id="f6070-110">Twilio permite que los desarrolladores [compren números de teléfono programables][purchase_phone] que se pueden usar tanto para enviar y recibir llamadas como para mensajes de texto.</span><span class="sxs-lookup"><span data-stu-id="f6070-110">Twilio allows developers to [purchase programmable phone numbers][purchase_phone] which can be used to both send and receive calls and text messages.</span></span> <span data-ttu-id="f6070-111">Cuando un número de Twilio recibe una llamada o un texto entrante, Twilio le enviará a la aplicación web una solicitud HTTP, POST o GET, pidiéndole instrucciones sobre cómo controlar la llamada o el texto.</span><span class="sxs-lookup"><span data-stu-id="f6070-111">When a Twilio number receives an inbound call or text, Twilio will send your web application an HTTP POST or GET request, asking you for instructions on how to handle the call or text.</span></span> <span data-ttu-id="f6070-112">El servidor responderá a la solicitud HTTP de Twilio con [TwiML][twiml], un conjunto simple de etiquetas XML que contienen instrucciones sobre cómo controlar una llamada o texto.</span><span class="sxs-lookup"><span data-stu-id="f6070-112">Your server will respond to Twilio's HTTP request with [TwiML][twiml], a simple set of XML tags that contain instructions on how to handle a call or text.</span></span> <span data-ttu-id="f6070-113">Veremos ejemplos de TwiML en un momento.</span><span class="sxs-lookup"><span data-stu-id="f6070-113">We will see examples of TwiML in just a moment.</span></span>

### <a name="making-calls-and-sending-text-messages"></a><span data-ttu-id="f6070-114">Realización de llamadas y envío de mensajes de texto</span><span class="sxs-lookup"><span data-stu-id="f6070-114">Making Calls and Sending Text Messages</span></span>
<span data-ttu-id="f6070-115">Al realizar solicitudes HTTP a la API del servicio web de Twilio, los desarrolladores pueden enviar mensajes de texto o iniciar llamadas telefónicas salientes.</span><span class="sxs-lookup"><span data-stu-id="f6070-115">By making HTTP requests to the Twilio web service API, developers can send text messages or initiate outbound phone calls.</span></span> <span data-ttu-id="f6070-116">En el caso de las llamadas salientes, el desarrollador también debe especificar una dirección URL que devuelve instrucciones de TwiML sobre cómo controlar una llamada saliente una vez conectada.</span><span class="sxs-lookup"><span data-stu-id="f6070-116">For outbound calls, the developer must also specify a URL that returns TwiML instructions for how to handle the outbound call once it is connected.</span></span>

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a><span data-ttu-id="f6070-117">Inserción de funcionalidades de VoIP en código de interfaz de usuario (JavaScript, iOS o Android)</span><span class="sxs-lookup"><span data-stu-id="f6070-117">Embedding VoIP Capabilities in UI code (JavaScript, iOS, or Android)</span></span>
<span data-ttu-id="f6070-118">Twilio brinda un SDK de cliente que puede transformar cualquier explorador web de escritorio, aplicación iOS o aplicación Android en un teléfono de VoIP.</span><span class="sxs-lookup"><span data-stu-id="f6070-118">Twilio provides a client-side SDK which can turn any desktop web browser, iOS app, or Android app into a VoIP phone.</span></span> <span data-ttu-id="f6070-119">En este artículo, nos centraremos en cómo usar la llamada de VoIP en el explorador.</span><span class="sxs-lookup"><span data-stu-id="f6070-119">In this article, we will focus on how to use VoIP calling in the browser.</span></span> <span data-ttu-id="f6070-120">Además del *SDK de JavaScript de Twilio* que se ejecuta en el explorador, se debe usar una aplicación de servidor (nuestra aplicación node.js) para emitir un "token de funcionalidad" al cliente de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f6070-120">In addition to the *Twilio JavaScript SDK* running in the browser, a server-side application (our node.js application) must be used to issue a "capability token" to the JavaScript client.</span></span> <span data-ttu-id="f6070-121">Lea más sobre el uso de VoIP con node.js en el [blog de desarrolladores de Twilio][voipnode].</span><span class="sxs-lookup"><span data-stu-id="f6070-121">You can read more about using VoIP with node.js [on the Twilio dev blog][voipnode].</span></span>

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a><span data-ttu-id="f6070-122">Suscripción en Twilio (con descuento de Microsoft)</span><span class="sxs-lookup"><span data-stu-id="f6070-122">Sign Up For Twilio (Microsoft Discount)</span></span>
<span data-ttu-id="f6070-123">Antes de usar servicios de Twilio, debe [registrarse para obtener una cuenta][signup].</span><span class="sxs-lookup"><span data-stu-id="f6070-123">Before using Twilio services, you must first [sign up for an account][signup].</span></span> <span data-ttu-id="f6070-124">Los clientes de Microsoft Azure obtendrán un descuento especial: [asegúrese de registrarse desde aquí][signup].</span><span class="sxs-lookup"><span data-stu-id="f6070-124">Microsoft Azure customers receive a special discount - [be sure to sign up here][signup]!</span></span>

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a><span data-ttu-id="f6070-125">Creación e implementación de un sitio web de Azure para Node.js</span><span class="sxs-lookup"><span data-stu-id="f6070-125">Create and Deploy a node.js Azure Website</span></span>
<span data-ttu-id="f6070-126">A continuación, deberá crear un sitio web de Node.js para que se ejecute en Azure.</span><span class="sxs-lookup"><span data-stu-id="f6070-126">Next, you will need to create a node.js website running on Azure.</span></span> <span data-ttu-id="f6070-127">[La documentación oficial para hacerlo está aquí][azure_new_site].</span><span class="sxs-lookup"><span data-stu-id="f6070-127">[The official documentation for doing this is located here][azure_new_site].</span></span> <span data-ttu-id="f6070-128">En un alto nivel, hará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f6070-128">At a high level, you will be doing the following:</span></span>

* <span data-ttu-id="f6070-129">Suscripción para obtener una cuenta de Azure, si todavía no tiene una</span><span class="sxs-lookup"><span data-stu-id="f6070-129">Signing up for an Azure account, if you don't have one already</span></span>
* <span data-ttu-id="f6070-130">Uso de la consola de administración de Azure para crear un sitio web</span><span class="sxs-lookup"><span data-stu-id="f6070-130">Using the Azure admin console to create a new website</span></span>
* <span data-ttu-id="f6070-131">Incorporación de compatibilidad con control de código fuente (supondremos que usó Git)</span><span class="sxs-lookup"><span data-stu-id="f6070-131">Adding source control support (we will assume you used git)</span></span>
* <span data-ttu-id="f6070-132">Creación de un archivo `server.js` con una simple aplicación web node.js</span><span class="sxs-lookup"><span data-stu-id="f6070-132">Creating a file `server.js` with a simple node.js web application</span></span>
* <span data-ttu-id="f6070-133">Implementación de esta aplicación simple en Azure</span><span class="sxs-lookup"><span data-stu-id="f6070-133">Deploying this simple application to Azure</span></span>

<a id="twiliomodule"/>

## <a name="configure-the-twilio-module"></a><span data-ttu-id="f6070-134">Configuración del módulo de Twilio</span><span class="sxs-lookup"><span data-stu-id="f6070-134">Configure the Twilio Module</span></span>
<span data-ttu-id="f6070-135">A continuación, comenzaremos a escribir una aplicación simple de Node.js que usa la API de Twilio.</span><span class="sxs-lookup"><span data-stu-id="f6070-135">Next, we will begin to write a simple node.js application which makes use of the Twilio API.</span></span> <span data-ttu-id="f6070-136">Antes de comenzar, necesitamos configurar nuestras credenciales para la cuenta de Twilio.</span><span class="sxs-lookup"><span data-stu-id="f6070-136">Before we begin, we need to configure our Twilio account credentials.</span></span>

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a><span data-ttu-id="f6070-137">Configuración de credenciales de Twilio en variables de entorno del sistema</span><span class="sxs-lookup"><span data-stu-id="f6070-137">Configuring Twilio Credentials in System Environment Variables</span></span>
<span data-ttu-id="f6070-138">A fin de realizar solicitudes autenticadas contra el back-end de Twilio, necesitamos el token de autenticación y el SID de nuestra cuenta, que funciona como nombre de usuario y contraseña definidos para la cuenta de Twilio.</span><span class="sxs-lookup"><span data-stu-id="f6070-138">In order to make authenticated requests against the Twilio back end, we need our account SID and auth token, which function as the username and password set for our Twilio account.</span></span> <span data-ttu-id="f6070-139">La forma más segura de configurarlos para su uso con el módulo de nodo en Azure es a través de variables de entorno del sistema, que puede definir directamente en la consola de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="f6070-139">The most secure way to configure these for use with the node module in Azure is via system environment variables, which you can set directly in the Azure admin console.</span></span>

<span data-ttu-id="f6070-140">Seleccione el sitio web de Node.js y haga clic en el vínculo "CONFIGURAR".</span><span class="sxs-lookup"><span data-stu-id="f6070-140">Select your node.js website, and click the "CONFIGURE" link.</span></span>  <span data-ttu-id="f6070-141">Si se desplaza un poco hacia abajo, verá un área en la que puede definir las propiedades de configuración para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f6070-141">If you scroll down a bit, you will see an area where you can set configuration properties for your application.</span></span>  <span data-ttu-id="f6070-142">Escriba las credenciales de la cuenta de Twilio ([las encontrará en la Consola de Twilio][twilio_console]) tal y como se muestra: asegúrese de denominarlas `TWILIO_ACCOUNT_SID` y `TWILIO_AUTH_TOKEN`, respectivamente:</span><span class="sxs-lookup"><span data-stu-id="f6070-142">Enter your Twilio account credentials ([found on your Twilio Console][twilio_console]) as shown - make sure to name them `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`, respectively:</span></span>

![Consola de administración de Azure][azure-admin-console]

<span data-ttu-id="f6070-144">Una vez que ha configurado estas variables, reinicie la aplicación en la consola de Azure.</span><span class="sxs-lookup"><span data-stu-id="f6070-144">Once you have configured these variables, restart your application in the Azure console.</span></span>

### <a name="declaring-the-twilio-module-in-packagejson"></a><span data-ttu-id="f6070-145">Declaración del módulo de Twilio en package.json</span><span class="sxs-lookup"><span data-stu-id="f6070-145">Declaring the Twilio module in package.json</span></span>
<span data-ttu-id="f6070-146">A continuación, debemos crear un archivo package.json para administrar nuestras dependencias de módulo de nodo vía [npm].</span><span class="sxs-lookup"><span data-stu-id="f6070-146">Next, we need to create a package.json to manage our node module dependencies via [npm].</span></span> <span data-ttu-id="f6070-147">En el mismo nivel del archivo `server.js` que creó en el tutorial de *Azure/node.js*, cree un archivo llamado `package.json`.</span><span class="sxs-lookup"><span data-stu-id="f6070-147">At the same level as the `server.js` file you created in the *Azure/node.js* tutorial, create a file named `package.json`.</span></span>  <span data-ttu-id="f6070-148">Dentro de este archivo coloque lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f6070-148">Inside this file, place the following:</span></span>

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

<span data-ttu-id="f6070-149">De esta forma, el módulo de Twilio se declara como una dependencia, al igual que la popular [plataforma web Express][express] y el motor de plantilla EJS.</span><span class="sxs-lookup"><span data-stu-id="f6070-149">This declares the twilio module as a dependency, as well as the popular [Express web framework][express] and the EJS template engine.</span></span>  <span data-ttu-id="f6070-150">Ahora ya estamos: comencemos a escribir código.</span><span class="sxs-lookup"><span data-stu-id="f6070-150">Okay, now we're all set - let's write some code!</span></span>

<a id="makecall"/>

## <a name="make-an-outbound-call"></a><span data-ttu-id="f6070-151">Realización de una llamada saliente</span><span class="sxs-lookup"><span data-stu-id="f6070-151">Make an Outbound Call</span></span>
<span data-ttu-id="f6070-152">Creemos un formulario simple que realizará una llamada a un número de nuestra elección.</span><span class="sxs-lookup"><span data-stu-id="f6070-152">Let's create a simple form that will place a call to a number we choose.</span></span> <span data-ttu-id="f6070-153">Abra `server.js` y escriba el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="f6070-153">Open up `server.js`, and enter the following code.</span></span> <span data-ttu-id="f6070-154">Observe que donde dice "CHANGE_ME" debe poner el nombre del sitio web de Azure:</span><span class="sxs-lookup"><span data-stu-id="f6070-154">Note where it says "CHANGE_ME" - put the name of your azure website there:</span></span>

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

// Render an HTML user interface for the application's home page
app.get('/', (request, response) => response.render('index'));

// Handle the form POST to place a call
app.post('/call', (request, response) => {
  var client = twilio(accountSid, authToken);

  client.makeCall({
    // make a call to this number
    to:request.body.number,

    // Change to a Twilio number you bought - see:
    // https://www.twilio.com/console/phone-numbers/incoming
    from:'+15558675309',

    // A URL in our app which generates TwiML
    // Change "CHANGE_ME" to your app's name
    url:'https://CHANGE_ME.azurewebsites.net/outbound_call'
  }, () => {
      // Go back to the home page
      response.redirect('/');
  });
});

// Generate TwiML to handle an outbound call
app.post('/outbound_call', (request, response) => {
  var twiml = new twilio.TwimlResponse();

  // Say a message to the call's receiver
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

<span data-ttu-id="f6070-155">Después, cree un directorio llamado `views` y, en su interior, cree un archivo llamado `index.ejs` con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="f6070-155">Next, create a directory called `views` - inside this directory, create a file named `index.ejs` with the following contents:</span></span>

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
      <input type="submit" value="Call the number above"/>
  </form>
</body>
</html>
```

<span data-ttu-id="f6070-156">Ahora, implemente el sitio web en Azure y abra su página principal.</span><span class="sxs-lookup"><span data-stu-id="f6070-156">Now, deploy your website to Azure and open your home.</span></span> <span data-ttu-id="f6070-157">Debe poder escribir el número de teléfono en el campo de texto y recibir una llamada desde el número de Twilio.</span><span class="sxs-lookup"><span data-stu-id="f6070-157">You should be able to enter your phone number in the text field, and receive a call from your Twilio number!</span></span>

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a><span data-ttu-id="f6070-158">Envío de un mensaje SMS</span><span class="sxs-lookup"><span data-stu-id="f6070-158">Send an SMS Message</span></span>
<span data-ttu-id="f6070-159">Ahora, configuremos una lógica de control de formulario e interfaz de usuario para enviar un mensaje de texto.</span><span class="sxs-lookup"><span data-stu-id="f6070-159">Now, let's set up a user interface and form handling logic to send a text message.</span></span> <span data-ttu-id="f6070-160">Abra `server.js` y agregue el siguiente código después de la última llamada a `app.post`:</span><span class="sxs-lookup"><span data-stu-id="f6070-160">Open up `server.js`, and add the following code after the last call to `app.post`:</span></span>

```javascript
app.post('/sms', (request, response) => {
  const client = twilio(accountSid, authToken);

  client.sendSms({
      // send a text to this number
      to:request.body.number,

      // A Twilio number you bought - see:
      // https://www.twilio.com/console/phone-numbers/incoming
      from:'+15558675309',

      // The body of the text message
      body: request.body.message

  }, () => {
      // Go back to the home page
      response.redirect('/');
  });
});
```

<span data-ttu-id="f6070-161">En `views/index.ejs`, agregue otro formulario debajo del primero para enviar un número y un mensaje de texto:</span><span class="sxs-lookup"><span data-stu-id="f6070-161">In `views/index.ejs`, add another form under the first one to submit a number and a text message:</span></span>

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message to send" name="message"/>
  <br/>
  <input type="submit" value="Send text to the number above"/>
</form>
```

<span data-ttu-id="f6070-162">Vuelva a implementar la aplicación en Azure y ahora debería poder enviar ese formulario y enviarse a usted mismo (o a cualquiera de sus amigos más cercanos) un mensaje de texto.</span><span class="sxs-lookup"><span data-stu-id="f6070-162">Re-deploy your application to Azure, and you should now be able to submit that form and send yourself (or any of your closest friends) a text message!</span></span>

<a id="nextsteps"/>

## <a name="next-steps"></a><span data-ttu-id="f6070-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f6070-163">Next Steps</span></span>
<span data-ttu-id="f6070-164">Ha aprendido los aspectos básicos relacionados con el uso de Node.js y Twilio para crear aplicaciones que se comuniquen.</span><span class="sxs-lookup"><span data-stu-id="f6070-164">You have now learned the basics of using node.js and Twilio to build apps that communicate.</span></span> <span data-ttu-id="f6070-165">Pero estos ejemplos son solo una muestra muy pequeña de lo que es posible hacer con Twilio y Node.js.</span><span class="sxs-lookup"><span data-stu-id="f6070-165">But these examples barely scratch the surface of what's possible with Twilio and node.js.</span></span> <span data-ttu-id="f6070-166">Si desea obtener más información sobre el uso de Twilio con Node.js, revise los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="f6070-166">For more information using Twilio with node.js, check out the following resources:</span></span>

* <span data-ttu-id="f6070-167">[Documentos oficiales de módulo][docs]</span><span class="sxs-lookup"><span data-stu-id="f6070-167">[Official module docs][docs]</span></span>
* <span data-ttu-id="f6070-168">[Tutorial de VoIP con aplicaciones node.js][voipnode]</span><span class="sxs-lookup"><span data-stu-id="f6070-168">[Tutorial on VoIP with node.js applications][voipnode]</span></span>
* <span data-ttu-id="f6070-169">[Votr: una aplicación de votación en tiempo real por medio de SMS con node.js y CouchDB (tres partes)][votr]</span><span class="sxs-lookup"><span data-stu-id="f6070-169">[Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr]</span></span>
* <span data-ttu-id="f6070-170">[Programación en pareja en el explorador con node.js][pair]</span><span class="sxs-lookup"><span data-stu-id="f6070-170">[Pair programming in the browser with node.js][pair]</span></span>

<span data-ttu-id="f6070-171">Esperamos que disfrute del acceso a Node.js y Twilio en Azure.</span><span class="sxs-lookup"><span data-stu-id="f6070-171">We hope you love hacking node.js and Twilio on Azure!</span></span>

[purchase_phone]: https://www.twilio.com/console/phone-numbers/search
[twiml]: https://www.twilio.com/docs/api/twiml
[signup]: http://ahoy.twilio.com/azure
[azure_new_site]: app-service-web/app-service-web-get-started-nodejs.md
[twilio_console]: https://www.twilio.com/console
<span data-ttu-id="f6070-172">[npm]: http://npmjs.org</span><span class="sxs-lookup"><span data-stu-id="f6070-172">[npm]: http://npmjs.org</span></span>
[express]: http://expressjs.com
[voipnode]: http://www.twilio.com/blog/2013/04/introduction-to-twilio-client-with-node-js.html
[docs]: http://twilio.github.io/twilio-node/
[votr]: http://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html
[pair]: http://www.twilio.com/blog/2013/06/pair-programming-in-the-browser-with-twilio.html
[azure-admin-console]: ./media/partner-twilio-nodejs-how-to-use-voice-sms/twilio_1.png
