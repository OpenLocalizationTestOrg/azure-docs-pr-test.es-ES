---
title: aaaHow tooUse Twilio para voz y SMS (PHP) | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomake una llamada de teléfono así como enviar un SMS de mensajes con el servicio de API de Twilio de hello en Azure. Ejemplos de código escritos en PHP."
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 007f22e3-ac75-4868-8315-da000c2e0dd0
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 9354df8de694826a0ff7ea92620ec4d7e5c2fd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a>Cómo tooUse Twilio para capacidades de SMS en PHP y voz
Esta guía demuestra cómo tooperform las tareas de programación habituales con hello Twilio API de servicio en Azure. escenarios de Hello descritos incluyen realizando una llamada telefónica y enviar un mensaje de servicio de mensajes cortos (SMS). Para obtener más información sobre Twilio y el uso de voz y SMS en las aplicaciones, vea hello [pasos](#NextSteps) sección.

## <a id="WhatIs"></a>¿Qué es Twilio?
Twilio está activando Hola futuro de las comunicaciones empresariales, la habilitación de los desarrolladores tooembed voice, VoIP y en las aplicaciones de mensajería. Virtualizar toda la infraestructura necesarios en un entorno global, basada en la nube, exponerlo a través de la plataforma de hello API de comunicaciones de Twilio. Las aplicaciones son toobuild simple y escalable. Disfrute de la flexibilidad de pagar por lo que utiliza y aproveche la confiabilidad de la nube.

**Voz Twilio** permite la toomake de las aplicaciones y recibir llamadas telefónicas. **Twilio SMS** permite que su aplicación toosend y recibir mensajes de texto. **Cliente de Twilio** permite llamadas de VoIP toomake desde cualquier teléfono, una tableta o un explorador y es compatible con WebRTC.

## <a id="Pricing"></a>Precios de Twilio y ofertas especiales
Los clientes de Azure reciben una [oferta especial](http://www.twilio.com/azure): 10 $ de regalo en crédito Twilio al actualizar su cuenta Twilio. Este crédito Twilio puede ser aplicada tooany uso de Twilio (10 $ crédito equivalente toosending como máximo 1000 mensajes SMS o recibir una too1000 entrada minutos de voz, según la ubicación de Hola de su destino de número y el mensaje o la llamada de teléfono). Canjee este crédito Twilio y comience en [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).

Twilio es un servicio de pago por uso. No hay comisiones establecidas y puede cerrar su cuenta en cualquier momento. Puede encontrar más detalles en [Precios de Twilio][twilio_pricing].

## <a id="Concepts"></a>Conceptos
Hola Twilio API es una API de REST que proporciona funciones SMS y voz para las aplicaciones. Las bibliotecas de cliente están disponibles en varios lenguajes; para ver una lista, consulte las [bibliotecas de API de Twilio][twilio_libraries].

Aspectos clave de hello Twilio API son verbos de Twilio y lenguaje de marcado de Twilio (TwiML).

### <a id="Verbs"></a>Verbos de Twilio
Hola API hace que el uso de Twilio verbos; Por ejemplo, hello  **&lt;decir&gt;**  verbo indica Twilio tooaudibly entregar un mensaje en una llamada.

Hola aquí te mostramos una lista de verbos de Twilio. Obtenga información acerca de Hola unos a otros verbos y capacidades a través de [documentación del lenguaje de marcado de Twilio](http://www.twilio.com/docs/api/twiml).

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

### <a id="TwiML"></a>TwiML
TwiML es un conjunto de instrucciones basado en XML en función de los verbos de Twilio de Hola que informan de Twilio de cómo tooprocess una llamada o SMS.

Por ejemplo, hello después TwiML convertiría texto hello **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

Cuando la aplicación llama hello Twilio API, uno de los parámetros de la API de hello es dirección URL de Hola que devuelve la respuesta de TwiML Hola. Para fines de desarrollo, puede utilizar direcciones URL siempre Twilio tooprovide hello TwiML las respuestas que usan las aplicaciones. También puede hospedar sus respuestas de las direcciones URL tooproduce hello TwiML y otra opción es hello toouse **TwiMLResponse** objeto.

Para obtener más información sobre los verbos de Twilio, sus atributos y TwiML, consulte [TwiML][twiml]. Para obtener información adicional acerca de hello Twilio API, consulte [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Creación de una cuenta de Twilio
Cuando esté listo tooget una cuenta de Twilio, regístrese en [intente Twilio][try_twilio]. Puede empezar con una cuenta gratuita y, posteriormente, actualizarla.

Cuando se registre para obtener una cuenta de Twilio, recibirá un identificador de cuenta y un token de autenticación. Ambos serán llamadas a la API de Twilio toomake necesarios. tooprevent no autorizado obtenga acceso a cuenta tooyour, proteger el token de autenticación. El identificador de cuenta y la autenticación de token están visibles en hello [página de la cuenta de Twilio][twilio_account], en Hola campos con la etiqueta **SID de cuenta** y **delTOKENdeautenticación**, respectivamente.

## <a id="create_app"></a>Creación de una aplicación PHP
Una aplicación PHP que utiliza el servicio de Twilio de Hola y se ejecuta en Azure es similar a cualquier otra aplicación de PHP que usa el servicio de Twilio Hola. Mientras los servicios de Twilio están basadas en REST y pueden llamarse desde PHP de varias maneras, este artículo se centrará en cómo services toouse Twilio con [Twilio biblioteca para PHP desde GitHub][twilio_php]. Para obtener más información acerca de cómo utilizar la biblioteca de Twilio de Hola para PHP, consulte [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].

Instrucciones detalladas para crear e implementar un tooAzure de aplicación de Twilio y PHP están disponibles en [cómo tooMake una llamada de teléfono uso de Twilio en una aplicación PHP en Azure][howto_phonecall_php].

## <a id="configure_app"></a>Configurar las bibliotecas de Twilio de tooUse de la aplicación
Puede configurar la biblioteca de Twilio de aplicación toouse Hola para PHP de dos maneras:

1. Descargar la biblioteca de Twilio de hello for PHP desde GitHub ([https://github.com/twilio/twilio-php][twilio_php]) y agregue hello **servicios** aplicación tooyour de directorio.
   
    O
2. Instalar biblioteca de Twilio de Hola para PHP como un paquete de PERA. Puede instalarse con hello siguientes comandos:
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

Una vez haya instalado la biblioteca de Twilio de Hola para PHP, a continuación, puede agregar un **require_once** declaración en la parte superior de Hola de PHP archivos de biblioteca de Hola tooreference:

        require_once 'Services/Twilio.php';

Para obtener más información, consulte [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].

## <a id="howto_make_call"></a>Realización de una llamada saliente
Hello siguiente muestra cómo toomake una salida llamar a utilizando hello **Services_Twilio** clase. Este código también usa un Hola de tooreturn sitio proporcionado Twilio respuesta de lenguaje de marcado de Twilio (TwiML). Sustituya los valores de hello **de** y **a** los números de teléfono y asegúrese de comprobar hello **de** número de teléfono para el código de hello Twilio cuenta toorunning anterior.

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // hello number of hello phone initiating hello hello call.
    $from_number = "NNNNNNNNNNN";

    // hello number of hello phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use hello Twilio-provided site for hello TwiML response.
    $url = "http://twimlets.com/message";

    // hello phone message text.
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make hello call.
    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

Como se ha mencionado, este código usa un Hola de tooreturn sitio proporcionado Twilio TwiML respuesta. En su lugar, podría utilizar su propio Hola de tooprovide sitio respuesta TwiML; Para obtener más información, consulte [cómo tooProvide TwiML respuestas desde su propio sitio Web de](#howto_provide_twiml_responses).

* **Tenga en cuenta**: tootroubleshoot errores de validación de certificado SSL, consulte [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation] 

## <a id="howto_send_sms"></a>Envío de un mensaje SMS
Hello siguiente muestra cómo toosend un mensaje SMS con Hola **Services_Twilio** clase. Hola **de** Twilio proporciona número para cuentas de prueba toosend mensajes SMS. Hola **a** número debe comprobarse para el código de hello Twilio cuenta toorunning anterior.

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send hello SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <a id="howto_provide_twiml_responses"></a>Entrega de respuestas de TwiML desde su propio sitio web
Cuando la aplicación inicia una toohello llamada API de Twilio, Twilio enviará su dirección de URL de solicitud tooa que es lo esperado tooreturn una respuesta TwiML. ejemplo de Hola anterior utiliza dirección URL proporcionada Twilio por hello [http://twimlets.com/message][twimlet_message_url]. (Aunque TwiML está diseñado para su uso por Twilio, puede ver hello en el explorador. Por ejemplo, haga clic en [http://twimlets.com/message] [ twimlet_message_url] toosee vacío `<Response>` elemento; como otro ejemplo, haga clic en [http://twimlets.com/message? Mensaje 5B0% D de %5 = Hola % 20World] [ twimlet_message_url_hello_world] toosee una `<Response>` elemento que contiene un `<Say>` elemento.)

En lugar de basarse en la dirección URL proporcionada Twilio por hello, puede crear su propio sitio que devuelve las respuestas HTTP. Puede crear el sitio de Hola en cualquier lenguaje que devuelve respuestas en XML; en este tema se da por supuesto que vamos a usar Hola PHP toocreate TwiML.

Hola siguiendo los resultados de la página PHP en una respuesta de TwiML que dice **Hello World** en llamada de Hola.

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

Como puede ver en el ejemplo de Hola anterior, hello TwiML respuesta es simplemente un documento XML. biblioteca de Twilio de Hola para PHP contiene clases que se generarán TwiML automáticamente. ejemplo de Hola siguiente genera respuesta equivalente de hello tal y como se muestra arriba, pero usa hello **servicios\_Twilio\_Twiml** clase en la biblioteca de Twilio de Hola para PHP:

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

Para más información sobre TwiML, vea [https://www.twilio.com/docs/api/twiml][twiml_reference]. 

Una vez que tenga la página PHP configurar tooprovide TwiML respuestas, use la dirección URL de Hola de página PHP hello como Hola dirección URL pasada en hello `Services_Twilio->account->calls->create` método. Por ejemplo, si tiene una aplicación Web denominada **MyTwiML** tooan implementado Azure servicio hospedado y nombre de Hola de página PHP hello es **mytwiml.php**, Hola dirección URL puede pasarse demasiado **Services_ Twilio -> cuentas -> llamadas -> crear** tal y como se muestra en el siguiente ejemplo de Hola:

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // hello phone message text.
    $message = "Hello world.";

    $client = new Services_Twilio($sid, $token, "2010-04-01");

    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

Para obtener información adicional acerca del uso de Twilio en Azure con PHP, consulte [cómo tooMake una llamada de teléfono uso de Twilio en una aplicación PHP en Azure][howto_phonecall_php].

## <a id="AdditionalServices"></a>Procedimientos: Uso de servicios Twilio adicionales
Además toohello ejemplos que se muestran aquí, que twilio ofrece API basadas en web que puede usar la funcionalidad adicional de Twilio de tooleverage desde su aplicación de Azure. Para obtener información detallada, vea hello [documentación de la API de Twilio][twilio_api_documentation].

## <a id="NextSteps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de hello Twilio servicio, siga estos toolearn de vínculos más:

* [Directrices de seguridad de Twilio][twilio_security_guidelines]
* [Procedimientos y código de ejemplo de Twilio][twilio_howtos]
* [Tutoriales de inicio rápido de Twilio][twilio_quickstarts] 
* [Twilio en GitHub][twilio_on_github]
* [Hable tooTwilio soporte técnico][twilio_support]

[twilio_php]: https://github.com/twilio/twilio-php
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-php/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-php/blob/master/README.md
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_api_service]: https://api.twilio.com
[howto_phonecall_php]: partner-twilio-php-make-phone-call.md
[twilio_voice_request]: https://www.twilio.com/docs/api/twiml/twilio_request
[twilio_sms_request]: https://www.twilio.com/docs/api/twiml/sms/twilio_request
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
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
