---
title: "aaaHow toouse Hola servicio de correo electrónico de SendGrid (PHP) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo enviar correo electrónico con el servicio de correo electrónico de SendGrid hello en Azure. Ejemplos de código escritos en PHP."
documentationcenter: php
services: 
manager: sendgrid
editor: mollybos
author: thinkingserious
ms.assetid: 51a9928a-4c9e-4b0a-aca8-9a408aeb6f47
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork; matt.bernier@sendgrid.com
ms.openlocfilehash: 0076e56dc185cb8f52e629395e7d2c143cb5cfa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-sendgrid-email-service-from-php"></a>¿Cómo tooUse Hola servicio de correo electrónico de SendGrid desde PHP
Esta guía demuestra cómo tooperform las tareas de programación habituales con hello SendGrid enviar por correo electrónico de servicio en Azure. ejemplos de Hola se escriben en PHP.
Hello escenarios descritos se incluyen **crear correo electrónico**, **enviar correo electrónico**, y **agregar datos adjuntos**. Para obtener más información sobre SendGrid y envío de correo electrónico, vea hello [pasos](#next-steps) sección.

## <a name="what-is-hello-sendgrid-email-service"></a>¿Qué es hello SendGrid servicio de correo electrónico?
SendGrid es un [servicio de correo electrónico basado en la nube] que ofrece un sistema confiable de [entrega de correo electrónico transaccional], escalabilidad y análisis en tiempo real junto, con API flexibles que facilitan la integración personalizada. Entre los escenarios de uso de SendGrid comunes se incluyen:

* Enviar automáticamente confirmaciones toocustomers
* Administración de listas de distribución para enviar a los clientes prospectos electrónicos y ofertas especiales cada mes
* Recopilación de diversas métricas en tiempo real, como las direcciones de correo electrónico bloqueadas y la capacidad de respuesta del cliente.
* Generar informes toohelp identificar tendencias
* Reenvío de consultas de los clientes
* Envío de notificaciones de correo electrónico desde su aplicación

Para obtener más información, consulte [https://sendgrid.com][https://sendgrid.com].

## <a name="create-a-sendgrid-account"></a>Creación de una cuenta de SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a>Uso de SendGrid desde la aplicación PHP
El uso de SendGrid en una aplicación PHP de Azure no requiere una configuración ni una codificación especiales. Como SendGrid es un servicio, puede obtenerse en hello exactamente igual desde una aplicación de nube tal como se puede desde una aplicación local.

## <a name="how-to-send-an-email"></a>Envío de un correo electrónico
Puede enviar correo electrónico mediante SMTP o hello Web API proporcionada por SendGrid.

### <a name="smtp-api"></a>API SMTP
correo electrónico de toosend mediante hello SendGrid SMTP API, use *Swift Mailer*, una biblioteca basada en componentes para enviar mensajes de correo electrónico desde aplicaciones PHP. Puede descargar hello *Swift Mailer* biblioteca de [http://swiftmailer.org/download] [ http://swiftmailer.org/download] v5.3.0 (usar [compositor] tooinstall SWIFT Mailer). Enviar correo electrónico con la biblioteca de hello implica la creación de instancias de la <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, y <span class="auto-style2">Swift\_mensaje </span> clases, estableciendo las propiedades adecuadas y llamar a la <span class="auto-style2">Swift\_Mailer::send</span> método.

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello receiver is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
     $html = "<html>
           <head></head>
           <body>
               <p>Hi!<br>
                   How are you?<br>
               </p>
           </body>
           </html>";
     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');
     // Email recipients
     $too= array(
           'john@contoso.com'=>'Destination 1 Name',
           'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
         // This will let us know how many users received this message
         echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
         echo "Something went wrong - ";
         print_r($failures);
     }

### <a name="web-api"></a>API Web
Usar de PHP [curl función] [ curl function] toosend correo electrónico utilizando Hola SendGrid Web API.

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $params = array(
          'api_user' => $user,
          'api_key' => $pass,
          'to' => 'john@contoso.com',
          'subject' => 'testing from curl',
          'html' => 'testing body',
          'text' => 'testing body',
          'from' => 'anna@contoso.com',
       );

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

API de Web de SendGrid es muy similar tooa API de REST, aunque no es realmente una API de REST desde ese momento, en la mayoría de las llamadas, ambos obtener y verbos POST se pueden usar indistintamente.

## <a name="how-to-add-an-attachment"></a>Adición de un correo electrónico
### <a name="smtp-api"></a>API SMTP
Enviar datos adjuntos con hello SMTP API implica una línea de script de ejemplo de código toohello para enviar un correo electrónico con Swift Mailer adicional.

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello reciever is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
      $html = "<html>
          <head></head>
          <body>
             <p>Hi!<br>
                How are you?<br>
             </p>
          </body>
          </html>";

     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');

     // Email recipients
     $too= array(
          'john@contoso.com'=>'Destination 1 Name',
          'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');
     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName("file_name"));

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
          // This will let us know how many users received this message
          echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
          echo "Something went wrong - ";
          print_r($failures);
     }

línea de código más Hello es como sigue:

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

Esta línea de código llama Hola attach (método) en la <span class="auto-style2">Swift\_mensaje</span> objeto y utiliza el método estático <span class="auto-style2">fromPath</span> en el <span class="auto-style2">Swift\_datos adjuntos</span>clase tooget y adjuntar un mensaje de tooa de archivo.

### <a name="web-api"></a>API Web
Enviar datos adjuntos con hello API Web están muy similar toosending un correo electrónico utilizando Hola API Web. Sin embargo, tenga en cuenta que en el ejemplo de Hola que sigue, matriz de parámetros de hello debe contener este elemento:

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

Ejemplo:

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $fileName = 'myfile';
     $filePath = dirname(__FILE__);

     $params = array(
         'api_user' => $user,
         'api_key' => $pass,
         'to' =>'john@contoso.com',
         'subject' => 'test of file sends',
         'html' => '<p> hello HTML </p>',
         'text' => 'hello plain text',
         'from' => 'anna@contoso.com',
         'files['.$fileName.']' => '@'.$filePath.'/'.$fileName
     );

     print_r($params);

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a>Cómo: Use los filtros tooEnable pies de página, el seguimiento y análisis
SendGrid proporciona la funcionalidad de correo electrónico adicionales mediante el uso de Hola de filtros de' '. Se trata de configuración que puede agregarse al mensaje de correo electrónico tooan para habilitar la funcionalidad específica, como habilitar el seguimiento de clics, Google analytics, suscripción de seguimiento, y así sucesivamente.

Filtros pueden ser mensajes tooa aplicada mediante el uso de la propiedad de filtros de Hola. Cada filtro se especifica mediante un hash que contiene la configuración específica del filtro. En el ejemplo siguiente se habilita el filtro de pie de página de Hola y especifica un mensaje de texto que anexa toohello inferior del mensaje de correo electrónico de saludo.
En este ejemplo usaremos biblioteca [sendgrid-php].
Use [compositor] tooinstall biblioteca:

    php composer.phar require sendgrid/sendgrid 2.1.1

Ejemplo:    

    <?php
     /*
      * This example is used for sendgrid-php V2.1.1 (https://github.com/sendgrid/sendgrid-php/tree/v2.1.1)
      */
     include "vendor/autoload.php";

     $email = new SendGrid\Email();
     // hello list of addresses this message will be sent to
     // [This list is used for sending multiple emails using just ONE request tooSendGrid]
     $toList = array('john@contoso.com', 'anna@contoso.com');

     // Specify hello names of hello recipients
     $nameList = array('Name 1', 'Name 2');

     // Used as an example of variable substitution
     $timeList = array('4 PM', '5 PM');

     // Set all of hello above variables
     $email->setTos($toList);
     $email->addSubstitution('-name-', $nameList);
     $email->addSubstitution('-time-', $timeList);

     // Specify that this is an initial contact message
     $email->addCategory("initial");

     // You can optionally setup individual filters here, in this example, we have
     // enabled hello footer filter
     $email->addFilter('footer', 'enable', 1);
     $email->addFilter('footer', "text/plain", "Thank you for your business");
     $email->addFilter('footer', "text/html", "Thank you for your business");

     // hello subject of your email
     $subject = 'Example SendGrid Email';

     // Where is this message coming from. For example, this message can be from
     // support@yourcompany.com, info@yourcompany.com
     $from = 'someone@example.com';

     // If you do not specify a sender list above, you can specifiy hello user here. If
     // a sender list IS specified above, this email address becomes irrelevant.
     $too= 'john@contoso.com';

     # Create hello body of hello message (a plain-text and an HTML version).
     # text is your plain-text email
     # html is your html version of hello email
     # if hello receiver is able tooview html emails then only hello html
     # email will be displayed

     /*
      * Note hello variable substitution here =)
      */
     $text = "
     Hello -name-,
     Thank you for your interest in our products. We have set up an appointment toocall you at -time- EST toodiscuss your needs in more detail.
     Regards,
     Fred";

     $html = "
     <html>
     <head></head>
     <body>
     <p>Hello -name-,<br>
     Thank you for your interest in our products. We have set up an appointment
     toocall you at -time- EST toodiscuss your needs in more detail.

     Regards,

     Fred<br>
     </p>
     </body>
     </html>";

     // set subject
     $email->setSubject($subject);

     // attach hello body of hello email
     $email->setFrom($from);
     $email->setHtml($html);
     $email->addTo($to);
     $email->setText($text);

     // Your SendGrid account credentials
     $username = 'sendgridusername@yourdomain.com';
     $password = 'example';

     // Create SendGrid object
     $sendgrid = new SendGrid($username, $password);

     // send message
     $response = $sendgrid->send($email);

     print_r($response);

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de hello servicio de correo electrónico de SendGrid, siga estos toolearn de vínculos más.

* Documentación de SendGrid: <https://sendgrid.com/docs>
* Biblioteca PHP de SendGrid: <https://github.com/sendgrid/sendgrid-php>
* Oferta especial de SendGrid para clientes de Azure: <https://sendgrid.com/windowsazure.html>

Para obtener más información, vea también hello [Centro para desarrolladores de PHP](/develop/php/).

[https://sendgrid.com]: https://sendgrid.com
[https://sendgrid.com/transactional-email/pricing]: https://sendgrid.com/transactional-email/pricing
[special offer]: https://www.sendgrid.com/windowsazure.html
[Packaging and Deploying PHP Applications for Azure]: http://msdn.microsoft.com/library/windowsazure/hh674499(v=VS.103).aspx
[http://swiftmailer.org/download]: http://swiftmailer.org/download
[curl function]: http://php.net/curl
[servicio de correo electrónico basado en la nube]: https://sendgrid.com/email-solutions
[entrega de correo electrónico transaccional]: https://sendgrid.com/transactional-email
[sendgrid-php]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1
[compositor]: https://getcomposer.org/download/
