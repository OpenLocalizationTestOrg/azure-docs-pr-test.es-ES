---
title: aaaHow tooUse Twilio para voz y SMS (Ruby) | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomake una llamada de teléfono así como enviar un SMS de mensajes con el servicio de API de Twilio de hello en Azure. Ejemplos de código escritos en Ruby."
services: 
documentationcenter: ruby
author: devinrader
manager: twilio
editor: 
ms.assetid: 60e512f6-fa47-47c0-aedc-f19bb72a1158
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 11/25/2014
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: aca5ccb4663ff03c9c1f39c848469415f06dfb45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a>Cómo tooUse Twilio para capacidades de SMS en Ruby y voz
Esta guía demuestra cómo tooperform las tareas de programación habituales con hello Twilio API de servicio en Azure. escenarios de Hello descritos incluyen realizando una llamada telefónica y enviar un mensaje de servicio de mensajes cortos (SMS). Para obtener más información sobre Twilio y el uso de voz y SMS en las aplicaciones, vea hello [pasos](#NextSteps) sección.

## <a id="WhatIs"></a>¿Qué es Twilio?
Twilio es una API de servicio web de telefonía que permite utilizar los lenguajes web existentes y voz toobuild de conocimientos y las aplicaciones de SMS. Twilio es un servicio de terceros (no una característica de Azure ni tampoco un producto de Microsoft).

**Voz Twilio** permite la toomake de las aplicaciones y recibir llamadas telefónicas. **Twilio SMS** permite la toomake de las aplicaciones y recibir mensajes SMS. **Cliente de Twilio** permite que las aplicaciones con las conexiones de Internet existentes, incluidas las conexiones móviles tooenable la comunicación de voz.

## <a id="Pricing"></a>Precios de Twilio y ofertas especiales
Puede encontrar información sobre los precios de Twilio en [Precios de Twilio][twilio_pricing]. Los clientes de Azure reciben una [oferta especial][special_offer]: 1000 mensajes o 1000 minutos para llamar totalmente gratuitos. toosign hacia arriba para esta oferta u obtener más información, visite [http://ahoy.twilio.com/azure][special_offer].  

## <a id="Concepts"></a>Conceptos
Hola Twilio API es una API de REST que proporciona funciones SMS y voz para las aplicaciones. Las bibliotecas de cliente están disponibles en varios lenguajes; para ver una lista, consulte las [bibliotecas de API de Twilio][twilio_libraries].

### <a id="TwiML"></a>TwiML
TwiML es un conjunto de instrucciones basado en XML que informan de Twilio de cómo tooprocess una llamada o SMS.

Por ejemplo, hello después TwiML convertiría texto hello **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

Todos los documentos de TwinML disponen de `<Response>` como elemento raíz. Desde allí, usar comportamiento de hello toodefine de verbos de Twilio de la aplicación.

### <a id="Verbs"></a>Verbos de TwiML
Los verbos de Twilio son etiquetas XML que indican Twilio ¿qué es demasiado**es**. Por ejemplo, hello  **&lt;decir&gt;**  verbo indica Twilio tooaudibly entregar un mensaje en una llamada. 

Hola aquí te mostramos una lista de verbos de Twilio.

* **&lt;Acceso telefónico&gt;**: conecta tooanother teléfono de hello llamador.
* **&lt;Recopilar&gt;**: recopila los dígitos numéricos del teclado del teléfono de Hola.
* **&lt;Hangup&gt;**: finaliza una llamada.
* **&lt;Play&gt;**: reproduce un archivo de audio.
* **&lt;Pause&gt;**: espera en silencio una cantidad de segundos específica.
* **&lt;Registro&gt;**: registra la voz del llamador de Hola y devuelve una dirección URL de un archivo que contenga una grabación de Hola.
* **&lt;Redirigir&gt;**: transfiere el control de una llamada o SMS toohello TwiML en una dirección URL diferente.
* **&lt;Rechazar&gt;**: rechaza una entrada llame al número de Twilio de tooyour sin facturación
* **&lt;Diga&gt;**: convierte texto toospeech que se realiza en una llamada.
* **&lt;Sms&gt;**: envía un mensaje SMS.

Para obtener más información sobre los verbos de Twilio, sus atributos y TwiML, consulte [TwiML][twiml]. Para obtener información adicional acerca de hello Twilio API, consulte [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Creación de una cuenta de Twilio
Cuando esté listo tooget una cuenta de Twilio, regístrese en [intente Twilio][try_twilio]. Puede empezar con una cuenta gratuita y, posteriormente, actualizarla.

Cuando registre la cuenta Twilio, obtendrá un número de teléfono gratuito para la aplicación. Recibirá también un SID de cuenta y un token de autenticación. Ambos serán llamadas a la API de Twilio toomake necesarios. tooprevent no autorizado obtenga acceso a cuenta tooyour, proteger el token de autenticación. El SID de la cuenta y el token de autenticación están visibles en hello [página de la cuenta de Twilio][twilio_account], en campos con la etiqueta de Hola **SID de cuenta** y **el TOKEN de autenticación** , respectivamente.

### <a id="VerifyPhoneNumbers"></a>Comprobación de números de teléfono
En Twilio tendrá el número de toohello de adición, también puede comprobar los números de control (es decir, su número de teléfono celular o principal) para su uso en las aplicaciones. 

Para obtener información acerca de cómo tooverify un número de teléfono, consulte [administrar números][verify_phone].

## <a id="create_app"></a>Creación de una aplicación de Ruby
Una aplicación Ruby que usa el servicio de Twilio de Hola y se ejecuta en Azure es similar a cualquier otra aplicación Ruby que usa el servicio de Twilio Hola. Y Twilio servicios RESTful y pueden llamarse desde Ruby de varias maneras, este artículo se centrará en cómo services toouse Twilio con [biblioteca auxiliar de Twilio para Ruby][twilio_ruby].

En primer lugar, [instalación una nueva máquina virtual Linux de Azure] [ azure_vm_setup] tooact como un host para la nueva aplicación web Ruby. Omita los pasos de Hola que implican Hola creación de una aplicación de raíles Hola de instalación solo máquinas virtuales. Asegúrese de crear un extremo con un puerto externo de 80 y un puerto interno de 5000.

En los siguientes ejemplos de hello, vamos a usar [Sinatra][sinatra], un marco web muy sencilla para Ruby. Pero, por supuesto, puede usar biblioteca auxiliar de hello Twilio para Ruby con cualquier otro entorno de web, incluidos Ruby sobre raíles.

SSH en la nueva VM y cree un directorio para la nueva aplicación. Dentro de ese directorio, cree un archivo denominado Gemfile y copie Hola siguiente código en él:

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

En la línea de comandos de hello ejecutar `bundle install`. Este modo se instalará las dependencias de hello anteriores. A continuación, cree un archivo que se llame `web.rb`. Se trata de donde vive código de hello de la aplicación web. Pegue Hola siguiente código en él:

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

En este momento debe ser comandos de Hola Hola capaz de ejecutar `ruby web.rb -p 5000`. De esta forma, podrá ejecutar un servidor web pequeño en el puerto 5000. Debe ser capaz de toobrowse toothis aplicación en el explorador al visitar la dirección URL de hello instalación para la máquina virtual de Azure. Una vez que se puede llegar a la aplicación web en el Explorador de hello, está listo toostart compilar una aplicación de Twilio.

## <a id="configure_app"></a>Configurar la aplicación tooUse Twilio
Puede configurar la biblioteca de Twilio de web app toouse Hola actualizando su `Gemfile` tooinclude esta línea:

    gem 'twilio-ruby'

En la línea de comandos de hello, ejecute `bundle install`. Ahora, abra `web.rb` esta línea en la parte superior de hello, incluido:

    require 'twilio-ruby'

Está ahora todos establecen biblioteca auxiliar de toouse hello Twilio para Ruby en su aplicación web.

## <a id="howto_make_call"></a>Realización de una llamada saliente
Hola siguiente muestra cómo llamar una salida de toomake. Conceptos clave que incluyen el uso de biblioteca auxiliar de hello Twilio para toomake Ruby llamadas API de REST y representación TwiML. Sustituya los valores de hello **de** y **a** los números de teléfono y asegúrese de comprobar hello **de** número de teléfono para el código de hello Twilio cuenta toorunning anterior.

Agregue esta función demasiado`web.md`:

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # hello number of hello phone receiving call.
    too= "NNNNNNNNNNN";

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create hello call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make hello call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

Si abrir arriba `http://yourdomain.cloudapp.net/make_call` en un explorador, que desencadenará Hola llamada toohello Twilio toomake Hola teléfono llamada a la API. Hola los dos primeros parámetros en `client.account.calls.create` son bastante autoexplicativo: Hola número Hola llamada es `from` y Hola número Hola llamada es `to`. 

Hola tercer parámetro (`url`) es dirección URL de Hola que Twilio solicita instrucciones tooget en qué toodo una vez que está conectada la llamada Hola. En este caso es configurar una dirección URL (`http://yourdomain.cloudapp.net`) que devuelve un documento de TwiML simple y utiliza hello `<Say>` toodo verbo Hola algunas texto a voz y diga "Hello mono" toohello persona recibir llamadas.

## <a id="howto_recieve_sms"></a>Procedimientos: Recepción de un mensaje SMS
En el ejemplo anterior de Hola se inició un **saliente** llamada de teléfono. Esta vez, vamos a usar el número de teléfono de hello Twilio nos proporcionaste durante el inicio de sesión tooprocess una **entrante** mensaje SMS.

En primer lugar, inicio de sesión tooyour [panel de Twilio][twilio_account]. Haga clic en "Números" en Hola de navegación superior y, a continuación, haga clic en hello número de Twilio que se proporcionaron. Ahora verá las dos direcciones URL que puede configurar. Una dirección URL de solicitud de voz y una dirección de URL de solicitud de SMS. Se trata de direcciones URL de Hola que se realizan llamadas de Twilio cada vez que una llamada de teléfono o un SMS se envía el número de tooyour. Hola las direcciones URL también se conocen como "enlaces web".

Nos gustaría tooprocess los mensajes SMS entrantes, así que vamos a actualizar la dirección URL de hello demasiado`http://yourdomain.cloudapp.net/sms_url`. Continúe y haga clic en Guardar cambios en parte inferior de Hola de página Hola. Ahora, nuevo en `web.rb` vamos a programar esta nuestro toohandle de aplicación:

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

Después de realizar el cambio de hello, asegúrese de inicio de toore seguro de la aplicación web. Ahora, retire el teléfono y enviar un número de Twilio de tooyour SMS. Debe obtener rápidamente una respuesta SMS que dice "¡Hola, gracias por ping Hola! y le indicará que Twilio y Azure son perfectos.

## <a id="additional_services"></a>Procedimientos: Uso de servicios Twilio adicionales
Además toohello ejemplos que se muestran aquí, que twilio ofrece API basadas en web que puede usar la funcionalidad adicional de Twilio de tooleverage desde su aplicación de Azure. Para obtener información detallada, vea hello [documentación de la API de Twilio][twilio_api_documentation].

### <a id="NextSteps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de hello Twilio servicio, siga estos toolearn de vínculos más:

* [Directrices de seguridad de Twilio][twilio_security_guidelines]
* [Procedimientos y código de ejemplo de Twilio][twilio_howtos]
* [Tutoriales de inicio rápido de Twilio][twilio_quickstarts] 
* [Twilio en GitHub][twilio_on_github]
* [Hable tooTwilio soporte técnico][twilio_support]

[twilio_ruby]: https://www.twilio.com/docs/ruby/install





[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/user/account
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/api
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
[sinatra]: http://www.sinatrarb.com/
[azure_vm_setup]: http://www.windowsazure.com/develop/ruby/tutorials/web-app-with-linux-vm/
