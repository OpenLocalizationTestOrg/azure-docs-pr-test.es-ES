---
title: aaaHow tooUse Twilio para voz y SMS (Python) | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomake una llamada de teléfono así como enviar un SMS de mensajes con el servicio de API de Twilio de hello en Azure. Ejemplos de código escritos en Python."
services: 
documentationcenter: python
author: devinrader
manager: twilio
editor: 
ms.assetid: 561bc75b-4ac4-40ba-bcba-48e901f27cc3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: 1f16a107d95c94589b8d61a0971c5b62d639c571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a>Cómo tooUse Twilio para capacidades de SMS en Python y voz
Esta guía demuestra cómo tooperform las tareas de programación habituales con hello Twilio API de servicio en Azure. escenarios de Hello descritos incluyen realizando una llamada telefónica y enviar un mensaje de servicio de mensajes cortos (SMS). Para obtener más información sobre Twilio y el uso de voz y SMS en las aplicaciones, vea hello [pasos](#NextSteps) sección.

## <a id="WhatIs"></a>¿Qué es Twilio?
Twilio está activando Hola futuro de las comunicaciones empresariales, la habilitación de los desarrolladores tooembed voice, VoIP y en las aplicaciones de mensajería. Virtualizar toda la infraestructura necesarios en un entorno global, basada en la nube, exponerlo a través de la plataforma de hello API de comunicaciones de Twilio. Las aplicaciones son toobuild simple y escalable. Disfrute de la flexibilidad de pagar por lo que utiliza y aproveche la confiabilidad de la nube.

**Voz Twilio** permite la toomake de las aplicaciones y recibir llamadas telefónicas.
**Twilio SMS** permite que su aplicación toosend y recibir mensajes de texto.
**Cliente de Twilio** permite llamadas de VoIP toomake desde cualquier teléfono, una tableta o un explorador y es compatible con WebRTC.

## <a id="Pricing"></a>Precios de Twilio y ofertas especiales
Los clientes de Azure reciben una [oferta especial][special_offer] de 10 $ de crédito de Twilio cuando se actualiza la cuenta de Twilio. Este crédito Twilio puede ser aplicada tooany uso de Twilio (10 $ crédito equivalente toosending como máximo 1000 mensajes SMS o recibir una too1000 entrada minutos de voz, según la ubicación de Hola de su destino de número y el mensaje o la llamada de teléfono). Canjee este [crédito de Twilio][special_offer] y comience.

Twilio es un servicio de pago por uso. No hay comisiones establecidas y puede cerrar su cuenta en cualquier momento. Puede encontrar más detalles en [Precios de Twilio][twilio_pricing].

## <a id="Concepts"></a>Conceptos
Hola Twilio API es una API de REST que proporciona funciones SMS y voz para las aplicaciones. Las bibliotecas de cliente están disponibles en varios lenguajes; para ver una lista, consulte las [bibliotecas de API de Twilio][twilio_libraries].

Aspectos clave de hello Twilio API son verbos de Twilio y lenguaje de marcado de Twilio (TwiML).

### <a id="Verbs"></a>Verbos de Twilio
Hola API hace que el uso de Twilio verbos; Por ejemplo, hello  **&lt;decir&gt;**  verbo indica Twilio tooaudibly entregar un mensaje en una llamada.

Hola aquí te mostramos una lista de verbos de Twilio. Obtenga información acerca de Hola unos a otros verbos y capacidades a través de [documentación del lenguaje de marcado de Twilio][twiml].

* **&lt;Acceso telefónico&gt;**: conecta tooanother teléfono de hello llamador.
* **&lt;Recopilar&gt;**: recopila los dígitos numéricos del teclado del teléfono de Hola.
* **&lt;Hangup&gt;**: finaliza una llamada.
* **&lt;Pause&gt;**: espera en silencio una cantidad de segundos específica.
* **&lt;Play&gt;**: reproduce un archivo de audio.
* **&lt;Cola&gt;**: agregar hello tooa cola de los llamadores.
* **&lt;Registro&gt;**: registra voz Hola del autor de llamada de Hola y devuelve una dirección URL de un archivo que contenga una grabación de Hola.
* **&lt;Redirigir&gt;**: transfiere el control de una llamada o SMS toohello TwiML en una dirección URL diferente.
* **&lt;Rechazar&gt;**: rechaza una entrada llame al número de Twilio de tooyour sin facturación.
* **&lt;Diga&gt;**: convierte texto toospeech que se realiza en una llamada.
* **&lt;Sms&gt;**: envía un mensaje SMS.

### <a id="TwiML"></a>TwiML
TwiML es un conjunto de instrucciones basado en XML en función de los verbos de Twilio de Hola que informan de Twilio de cómo tooprocess una llamada o SMS.

Por ejemplo, hello después TwiML convertiría texto hello **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

Cuando la aplicación llama hello Twilio API, uno de los parámetros de la API de hello es dirección URL de Hola que devuelve la respuesta de TwiML Hola. Para fines de desarrollo, puede utilizar direcciones URL siempre Twilio tooprovide hello TwiML las respuestas que usan las aplicaciones. También puede hospedar sus respuestas de las direcciones URL tooproduce hello TwiML y otra opción es hello toouse `TwiMLResponse` objeto.

Para obtener más información sobre los verbos de Twilio, sus atributos y TwiML, consulte [TwiML][twiml]. Para obtener información adicional acerca de hello Twilio API, consulte [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Creación de una cuenta de Twilio
Cuando esté listo tooget una cuenta de Twilio, regístrese en [intente Twilio][try_twilio]. Puede empezar con una cuenta gratuita y, posteriormente, actualizarla.

Cuando se registre para obtener una cuenta de Twilio, recibirá un Id. de seguridad (SID) de la cuenta y un token de autenticación. Ambos serán llamadas a la API de Twilio toomake necesarios. tooprevent no autorizado obtenga acceso a cuenta tooyour, proteger el token de autenticación. El SID de la cuenta y el token de autenticación están visibles en hello [Twilio consola][twilio_console], en campos con la etiqueta de Hola **SID de cuenta** y **delTOKENdeautenticación**, respectivamente.

## <a id="create_app"></a>Crear una aplicación de Python
Una aplicación de Python que usa el servicio de Twilio de Hola y se ejecuta en Azure es similar a cualquier otra aplicación de Python que usa el servicio de Twilio Hola. Mientras los servicios de Twilio están basadas en REST y pueden llamarse desde Python de varias maneras, este artículo se centrará en cómo services toouse Twilio con [Twilio biblioteca de Python desde GitHub][twilio_python]. Para obtener más información acerca de cómo utilizar la biblioteca de Twilio de Hola para Python, consulte [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].

En primer lugar, [instalación una nueva máquina virtual Linux de Azure] [azure_vm_setup] tooact como un host para la nueva aplicación web de Python. Una vez hello Máquina Virtual está ejecutando, deberá tooexpose la aplicación en un puerto público tal y como se describe a continuación.

### <a name="add-an-incoming-rule"></a>Agregar una regla de entrada
  1. Vaya toohello [grupo de seguridad de red] [azure_nsg] página.
  2. Hola seleccione grupo de seguridad de red que se corresponde con la máquina Virtual.
  3. Agregue una **Regla de salida** para el **puerto 80**. Ser seguro tooallow entrante procedente de cualquier dirección.

### <a name="set-hello-dns-name-label"></a>Etiqueta de nombre DNS del conjunto Hola
  1. Vaya toohello [Hola direcciones IP públicas] [azure_ips] página.
  2. Seleccione Hola IP pública que correspends con la máquina Virtual.
  3. Conjunto hello **etiqueta de nombre DNS** en hello **configuración** sección. En caso de hello de este ejemplo tendrá un aspecto similar al siguiente *la etiqueta de dominio*. centralus.cloudapp.azure.com

Una vez que se puede tooconnect a través de SSH toohello Máquina Virtual puede instalar Hola marco Web de su elección (Hola dos más conocidas de Python que se va a [matraz](http://flask.pocoo.org/) y [Django](https://www.djangoproject.com)). Puede instalar cualquiera de ellas simplemente mediante la ejecución de hello `pip install` comando.

Tenga en cuenta que hemos configurado tooallow tráfico de hello máquinas virtuales únicamente en el puerto 80. Por lo que debe seguro tooconfigure Hola aplicación toouse este puerto.

## <a id="configure_app"></a>Configurar las bibliotecas de Twilio de tooUse de la aplicación
Puede configurar la biblioteca de Twilio de aplicación toouse Hola de Python de dos maneras:

* Instalar biblioteca de Twilio de Hola para Python como un paquete de Pip. Puede instalarse con hello siguientes comandos:
   
        $ pip install twilio

    O

* Descargue la biblioteca de Twilio de Hola para Python desde GitHub ([https://github.com/twilio/twilio-python][twilio_python]) e instálelo similar al siguiente:

        $ python setup.py install

Una vez haya instalado la biblioteca de Twilio de Hola para Python, a continuación, puede `import` en los archivos de Python:

        import twilio

Para más información, vea [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].

## <a id="howto_make_call"></a>Realización de una llamada saliente
Hola siguiente muestra cómo llamar una salida de toomake. Este código también usa un Hola de tooreturn sitio proporcionado Twilio respuesta de lenguaje de marcado de Twilio (TwiML). Sustituya los valores de hello **from_number** y **to_number** los números de teléfono y asegúrese de que ha comprobado hello **from_number** número de teléfono para su cuenta de Twilio antes de ejecutar código de hello.

    from urllib.parse import urlencode

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # hello number of hello phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://twimlets.com/message?"

    # hello phone message text.
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

Como se ha mencionado, este código usa un Hola de tooreturn sitio proporcionado Twilio TwiML respuesta. En su lugar, podría utilizar su propio Hola de tooprovide sitio respuesta TwiML; Para obtener más información, consulte [cómo tooProvide TwiML respuestas desde su propio sitio Web de](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Envío de un mensaje SMS
Hello siguiente muestra cómo toosend un mensaje SMS con Hola `TwilioRestClient` clase. Hola **from_number** Twilio proporciona número para cuentas de prueba toosend mensajes SMS. Hola **to_number** número debe ser verificado para su cuenta de Twilio antes de ejecutar código de hello.

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send hello SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <a id="howto_provide_twiml_responses"></a>Entrega de respuestas de TwiML desde su propio sitio web
Cuando la aplicación inicia una toohello llamada API de Twilio, Twilio enviará su dirección de URL de solicitud tooa que es lo esperado tooreturn una respuesta TwiML. ejemplo de Hola anterior utiliza dirección URL proporcionada Twilio por hello [http://twimlets.com/message][twimlet_message_url]. (Aunque TwiML está diseñado para su uso por Twilio, puede verlo en el explorador. Por ejemplo, haga clic en [http://twimlets.com/message] [ twimlet_message_url] toosee vacío `<Response>` elemento; como otro ejemplo, haga clic en [http://twimlets.com/message? Mensaje 5B0% D de %5 = Hola % 20World] [ twimlet_message_url_hello_world] toosee una `<Response>` elemento que contiene un `<Say>` elemento.)

En lugar de basarse en la dirección URL proporcionada Twilio por hello, puede crear su propio sitio que devuelve las respuestas HTTP. Puede crear el sitio de Hola en cualquier lenguaje que devuelve respuestas en XML; en este tema se da por supuesto que va a usar Hola de Python toocreate TwiML.

Hello en los ejemplos siguientes dará como resultado una respuesta TwiML que dice **Hello World** en llamada de Hola.

Con Flask:

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

Con Django:

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

Como puede ver en el ejemplo de Hola anterior, hello TwiML respuesta es simplemente un documento XML. biblioteca de Twilio de Hola para Python contiene clases que se generarán TwiML automáticamente. Hello ejemplo siguiente genera respuesta equivalente de hello tal y como se muestra arriba, pero usa hello `twiml` módulo en la biblioteca de Twilio de Hola para Python:

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

Para más información sobre TwiML, vea [https://www.twilio.com/docs/api/twiml][twiml_reference].

Una vez que tenga la aplicación de Python configurar tooprovide TwiML respuestas, use la dirección URL de Hola de aplicación hello como Hola dirección URL pasada en hello `client.calls.create` método. Por ejemplo, si tiene una aplicación Web denominada **MyTwiML** tooan implementado Azure servicio hospedado, puede usar su dirección url como webhook tal y como se muestra en el siguiente ejemplo de Hola:

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <a id="AdditionalServices"></a>Procedimientos: Uso de servicios Twilio adicionales
Además toohello ejemplos que se muestran aquí, que twilio ofrece API basadas en web que puede usar la funcionalidad adicional de Twilio de tooleverage desde su aplicación de Azure. Para obtener información detallada, vea hello [documentación de la API de Twilio][twilio_api].

## <a id="NextSteps"></a>Pasos siguientes
Ahora que ha aprendido los conceptos básicos de Hola de hello Twilio servicio, siga estos toolearn de vínculos más:

* [Directrices de seguridad de Twilio][twilio_security_guidelines]
* [Guías de procedimientos y código de ejemplo de Twilio][twilio_howtos]
* [Tutoriales de inicio rápido de Twilio][twilio_quickstarts]
* [Twilio en GitHub][twilio_on_github]
* [Hable tooTwilio soporte técnico][twilio_support]

[special_offer]: http://ahoy.twilio.com/azure
[twilio_python]: https://github.com/twilio/twilio-python
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-python/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-python/blob/master/README.md

[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
