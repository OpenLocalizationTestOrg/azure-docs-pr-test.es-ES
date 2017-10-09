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
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a>Uso de Twilio para voz, VoIP y mensajería SMS en Azure
Esta guía se demuestra cómo toobuild aplicaciones que se comunican con Twilio y node.js en Azure.

<a id="whatis"/>

## <a name="what-is-twilio"></a>¿Qué es Twilio?
Twilio es una plataforma de API que facilita a los desarrolladores toomake y recibe llamadas telefónicas, enviar y recibir mensajes de texto e incrustar una llamada de VoIP a aplicaciones móviles basadas en el explorador y nativo. Revisemos brevemente su funcionamiento antes de analizar los detalles.

### <a name="receiving-calls-and-text-messages"></a>Recepción de llamadas y mensajes de texto
Twilio permite a los desarrolladores demasiado[números de teléfono programables de compra] [ purchase_phone] que puede ser usado tooboth enviar y recibir llamadas y mensajes de texto. Cuando un número de Twilio recibe una llamada entrante o texto, Twilio enviará la aplicación web un HTTP POST o una solicitud GET, que le pide que para obtener instrucciones sobre cómo toohandle Hola llamada o texto. El servidor responderá a solicitudes HTTP del tooTwilio con [TwiML][twiml], un sencillo conjunto de etiquetas XML que contienen instrucciones sobre cómo toohandle una llamada o texto. Veremos ejemplos de TwiML en un momento.

### <a name="making-calls-and-sending-text-messages"></a>Realización de llamadas y envío de mensajes de texto
Al realizar solicitudes HTTP toohello Twilio API del servicio web, los desarrolladores pueden enviar mensajes de texto o iniciar llamadas telefónicas salientes. Para las llamadas salientes, programador de hello también debe especificar una dirección URL que devuelve TwiML instrucciones de cómo llamar toohandle Hola salida una vez que está conectado.

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a>Inserción de funcionalidades de VoIP en código de interfaz de usuario (JavaScript, iOS o Android)
Twilio brinda un SDK de cliente que puede transformar cualquier explorador web de escritorio, aplicación iOS o aplicación Android en un teléfono de VoIP. En este artículo, nos centraremos en cómo toouse VoIP de llamada en el Explorador de Hola. En suma toohello *Twilio JavaScript SDK* se ejecuta en el Explorador de hello, una aplicación de servidor (nuestra aplicación node.js) debe ser tooissue usado un toohello "token capacidad" cliente de JavaScript. Puede leer más sobre el uso de VoIP con node.js [en el blog de desarrollo de hello Twilio][voipnode].

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a>Suscripción en Twilio (con descuento de Microsoft)
Antes de usar servicios de Twilio, debe [registrarse para obtener una cuenta][signup]. Los clientes de Microsoft Azure reciben un descuento especial - [ser seguro toosign aquí][signup]!

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a>Creación e implementación de un sitio web de Azure para Node.js
A continuación, deberá toocreate un sitio Web de node.js ejecuta en Azure. [documentación oficial de Hola para realizar esta acción se encuentra aquí][azure_new_site]. En un nivel alto, va a realizar siguiente hello:

* Suscripción para obtener una cuenta de Azure, si todavía no tiene una
* Uso de toocreate de consola de administración de Azure de hello un nuevo sitio Web
* Incorporación de compatibilidad con control de código fuente (supondremos que usó Git)
* Creación de un archivo `server.js` con una simple aplicación web node.js
* Implementar esta aplicación simple tooAzure

<a id="twiliomodule"/>

## <a name="configure-hello-twilio-module"></a>Configurar hello Twilio módulo
A continuación, empezaremos a toowrite una aplicación node.js simple que hace uso de hello Twilio API. Antes de comenzar, debemos tooconfigure nuestras credenciales de cuenta de Twilio.

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a>Configuración de credenciales de Twilio en variables de entorno del sistema
En solicitudes de pedido de toomake autenticado contra Hola Twilio back-end, necesitamos nuestro SID de la cuenta y el token de autenticación, qué función como nombre de usuario de Hola y la contraseña configurados para la cuenta de Twilio. tooconfigure de manera más segura de Hello estos para su uso con el módulo de nodo de hello en Azure es a través de las variables de entorno de sistema, lo que se pueden establecer directamente en la consola de administración de Azure de Hola.

Seleccione el sitio Web de node.js y haga clic en el vínculo de "Configurar" Hola.  Si se desplaza un poco hacia abajo, verá un área en la que puede definir las propiedades de configuración para la aplicación.  Escriba sus credenciales de cuenta de Twilio ([se encuentra en la consola de Twilio][twilio_console]) tal como se muestra: hacer seguro tooname les `TWILIO_ACCOUNT_SID` y `TWILIO_AUTH_TOKEN`, respectivamente:

![Consola de administración de Azure][azure-admin-console]

Una vez haya configurado estas variables, reinicie la aplicación Hola consola de Azure.

### <a name="declaring-hello-twilio-module-in-packagejson"></a>Declaración de módulo de Twilio de hello en package.json
A continuación, necesitamos toocreate una toomanage package.json nuestro dependencias de módulo de nodo a través de [npm]. En hello en el mismo nivel como hello `server.js` archivo que creó en hello *Azure/node.js* tutorial, cree un archivo denominado `package.json`.  En este archivo, coloque el siguiente hello:

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

Esto declara módulo de twilio de hello como una dependencia, así como Hola populares [Express marco web] [ express] y motor de plantillas EJS Hola.  Ahora ya estamos: comencemos a escribir código.

<a id="makecall"/>

## <a name="make-an-outbound-call"></a>Realización de una llamada saliente
Vamos a crear un formulario simple que se colocará un número de tooa de llamada que se elija. Abra `server.js`y escriba el siguiente código de hello. Tenga en cuenta que dice "CHANGE_ME" - he puesto ahí nombre Hola de su sitio Web de azure:

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

A continuación, cree un directorio denominado `views` : en este directorio, cree un archivo denominado `index.ejs` con hello siguiente contenido:

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

Ahora, implemente su tooAzure del sitio Web y abra su hogar. Debe ser capaz de tooenter el número de teléfono en el campo de texto de Hola y recibe una llamada desde el número de Twilio!

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a>Envío de un mensaje SMS
Ahora, vamos a configurar una interfaz de usuario y toosend de lógica de control de formularios un mensaje de texto. Abra `server.js`y agregue Hola siguiente código después de la última llamada de hello demasiado`app.post`:

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

En `views/index.ejs`, agregue otra forma bajo hello primero toosubmit un número y un mensaje de texto:

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message toosend" name="message"/>
  <br/>
  <input type="submit" value="Send text toohello number above"/>
</form>
```

Volver a implementar la aplicación tooAzure y ahora debe ser capaz de toosubmit que forman y enviar a usted (o cualquiera de sus amigos más cercanos) un mensaje de texto.

<a id="nextsteps"/>

## <a name="next-steps"></a>Pasos siguientes
Ya ha aprendido Fundamentos de hello del uso de node.js y Twilio toobuild aplicaciones que se comunican. Pero estos ejemplos apenas scratch superficie Hola de lo que es posible con Twilio y node.js. Para obtener más información con Twilio node.js, desproteger Hola recursos siguientes:

* [Documentos oficiales de módulo][docs]
* [Tutorial de VoIP con aplicaciones node.js][voipnode]
* [Votr: una aplicación de votación en tiempo real por medio de SMS con node.js y CouchDB (tres partes)][votr]
* [Programación de par en el Explorador de hello con node.js][pair]

Esperamos que disfrute del acceso a Node.js y Twilio en Azure.

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
