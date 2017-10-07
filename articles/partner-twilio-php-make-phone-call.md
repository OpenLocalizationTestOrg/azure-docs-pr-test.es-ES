---
title: "aaaHow toomake una llamada de teléfono de Twilio (PHP) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomake una llamada de teléfono así como enviar un SMS de mensajes con el servicio de API de Twilio de hello en Azure. Ejemplos para la aplicación PHP."
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 44e35adc-be06-4700-beee-8c9e2c20c540
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: e6fecc345bf9ae787d14d533bd8d96b175c2453b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a>¿Cómo tooMake una llamada de teléfono uso de Twilio en una aplicación PHP en Azure
Hello en el ejemplo siguiente se muestra cómo se puede utilizar una llamada desde una página web PHP hospedado en Azure de Twilio toomake. aplicación resultante de Hello solicitará a Hola usuario valores de llamada de teléfono, como se muestra en la siguiente captura de pantalla de Hola.

![Formulario de llamada de Azure con Twilio y PHP][twilio_php]

Necesitará toodo Hola siguiente código de hello toouse en este tema:

1. Adquiera una cuenta de Twilio y un token de autenticación desde la [Consola de Twilio][twilio_console]. tooget a trabajar con Twilio, evaluar precios en [http://www.twilio.com/pricing][twilio_pricing]. Puede registrarse para obtener una cuenta de prueba en [https://www.twilio.com/try-twilio][try_twilio].
2. Obtener hello [Twilio biblioteca para PHP](https://github.com/twilio/twilio-php) o instalarlo como un paquete de PERA. Para obtener más información, vea hello [archivo Léame](https://github.com/twilio/twilio-php/blob/master/README.md).
3. Instalar hello Azure SDK para PHP. Para obtener información general de hello SDK e instrucciones acerca de cómo instalarlo, consulte [configurar hello Azure SDK para PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)

## <a name="create-a-web-form-for-making-a-call"></a>Creación de un formulario web para hacer una llamada
Hola después HTML de código muestra cómo toobuild una página web (**callform.html**) que recupera datos de usuario para realizar una llamada:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Automated call form</title>
</head>
<body>
  <h1>Automated Call Form</h1>
  <p>Fill in all fields and click <b>Make this call</b>.</p>
  <form action="makecall.php" method="post">
    <table>
      <tr>
        <td>To:</td>
        <td><input name="callTo" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>From:</td>
        <td><input name="callFrom" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>Call message:</td>
        <td><input name="callText" size="100" type="text" value="Hello. This is hello call text. Good bye."></td>
      </tr>
      <tr>
        <td colspan="2"><input type="submit" value="Make this call"></td>
      </tr>
    </table>
  </form><br>
</body>
</html>
```

## <a name="create-hello-code-toomake-hello-call"></a>Crear Hola código toomake Hola llamada
Hola el siguiente código muestra cómo toobuild **makecall.php**, que se llama cuando el usuario de hello envía el formulario de hello muestra **callform.html**. Hola fragmento de código siguiente crea el mensaje de bienvenida de llamada y genera Hola llamada. Además, puede toouse seguro de que su cuenta de Twilio y la autenticación de token de hello [Twilio consola] [ twilio_console] en lugar de valores de marcador de posición de hello asignados demasiado**$sid** y **$token** Hola del siguiente código.

```html
<html>
<head><title>Making call...</title></head>
<body>
<p>Your call is being made.</p>

<?php
require_once 'path/to/vendor/autoload.php';

$sid   = "your_account_sid";
$token = "your_authentication_token";

$from_number = $_POST['callFrom']; // Calls must be made from a registered Twilio number.
$to_number   = $_POST['callTo'];
$message     = $_POST['callText'];

$client = new Twilio\Rest\Client($sid, $token);

$call = $client->calls->create(
            $to_number,
            $from_number,
            array('url' => http://twimlets.com/message?Message=' . urlencode($message))
        );

echo "Call status: " . $call->status . "<br />";
echo "URI resource: " . $call->uri . "<br />";
?>
</body>
</html>
```

Además toomaking Hola llamada, **makecall.php** muestra algunos metadatos de la llamada, como se muestra en la imagen de hello siguiente. Para más información sobre los metadatos de llamada, vea [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].

![Respuesta de llamada de Azure con Twilio y PHP][twilio_php_response]

## <a name="run-hello-application"></a>Ejecutar la aplicación hello
paso siguiente Hello es toodeploy su tooAzure sitios Web de aplicación. Hello artículos siguientes contienen información de Hola para crear un sitio Web e implementar el código con Git, FTP o WebMatrix (aunque no toda la información de cada artículo es relevante):

* [Creación de un sitio web PHP-MySQL en el Servicio de aplicaciones de Azure e implementación mediante Git](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [Creación de un sitio web PHP-MySQL en el Servicio de aplicaciones de Azure e implementación mediante FTP](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a>Pasos siguientes
Este código se proporcionó tooshow funcionalidad básica con Twilio en PHP en Azure. Antes de implementar tooAzure en producción, puede que desee tooadd más control de errores o con otras características. Por ejemplo:

* En lugar de utilizar un formulario web Forms, puede utilizar blobs de almacenamiento de Azure o números de teléfono de toostore de base de datos SQL y llamar a texto. Para obtener información sobre el uso de blobs de almacenamiento de Azure en PHP, vea [Uso de Azure Storage con aplicaciones de PHP][howto_blob_storage_php]. Para obtener información sobre el uso de bases de datos SQL en PHP, vea [Uso de una base de datos SQL con aplicaciones de PHP][howto_sql_azure_php].
* Hola **makecall.php** código usa la dirección URL proporcionada Twilio ([http://twimlets.com/message][twimlet_message_url]) tooprovide una respuesta de lenguaje de marcado de Twilio (TwiML) que informa de cómo Twilio tooproceed con llamada Hola. Por ejemplo, puede contener hello TwiML que se devuelve un `<Say>` verbo que es el resultado en texto que se va a toohello hablado destinatario de la llamada. En lugar de usar la dirección URL proporcionada Twilio por hello, puede generar la solicitud de su propio tooTwilio toorespond servicio; Para obtener más información, consulte [cómo tooUse Twilio para capacidades de SMS en PHP y voz][howto_twilio_voice_sms_php]. Puede encontrar más información sobre TwiML en [http://www.twilio.com/docs/api/twiml][twiml], y más información sobre `<Say>` y otros verbos de Twilio en [http://www.twilio.com/docs/api/twiml/say][twilio_say].
* Lea las directrices de seguridad de hello Twilio en [https://www.twilio.com/docs/security][twilio_docs_security].

Para obtener información adicional sobre Twilio, vea [https://www.twilio.com/docs][twilio_docs].

## <a name="see-also"></a>Otras referencias
* [Cómo tooUse Twilio para capacidades de SMS en PHP y voz](partner-twilio-php-how-to-use-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/docs/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[build_php_azure_app]: http://azurephp.interoperabilitybridges.com/articles/build-and-deploy-a-windows-azure-php-application
[howto_twilio_voice_sms_php]: partner-twilio-php-how-to-use-voice-sms.md
[howto_blob_storage_php]: http://azure.microsoft.com/documentation/articles/storage-php-how-to-use-blobs/
[howto_sql_azure_php]: http://azure.microsoft.com/documentation/articles/sql-database-php-how-to-use/
[twilio_call_properties]: https://www.twilio.com/docs/api/rest/call#instance-properties
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_php]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPCallForm.jpg
[twilio_php_response]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPMakeCall.jpg
[website-git]: ./web-sites/web-sites-php-mysql-deploy-use-git.md
[website-ftp]: ./web-sites/web-sites-php-mysql-deploy-use-ftp.md
[twilio_php_github]: https://github.com/twilio/twilio-php
