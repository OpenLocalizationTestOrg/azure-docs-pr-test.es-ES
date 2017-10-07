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
# <a name="how-toouse-hello-sendgrid-email-service-from-php"></a><span data-ttu-id="13f3b-104">¿Cómo tooUse Hola servicio de correo electrónico de SendGrid desde PHP</span><span class="sxs-lookup"><span data-stu-id="13f3b-104">How tooUse hello SendGrid Email Service from PHP</span></span>
<span data-ttu-id="13f3b-105">Esta guía demuestra cómo tooperform las tareas de programación habituales con hello SendGrid enviar por correo electrónico de servicio en Azure.</span><span class="sxs-lookup"><span data-stu-id="13f3b-105">This guide demonstrates how tooperform common programming tasks with hello SendGrid email service on Azure.</span></span> <span data-ttu-id="13f3b-106">ejemplos de Hola se escriben en PHP.</span><span class="sxs-lookup"><span data-stu-id="13f3b-106">hello samples are written in PHP.</span></span>
<span data-ttu-id="13f3b-107">Hello escenarios descritos se incluyen **crear correo electrónico**, **enviar correo electrónico**, y **agregar datos adjuntos**.</span><span class="sxs-lookup"><span data-stu-id="13f3b-107">hello scenarios covered include **constructing email**, **sending email**, and **adding attachments**.</span></span> <span data-ttu-id="13f3b-108">Para obtener más información sobre SendGrid y envío de correo electrónico, vea hello [pasos](#next-steps) sección.</span><span class="sxs-lookup"><span data-stu-id="13f3b-108">For more information on SendGrid and sending email, see hello [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="13f3b-109">¿Qué es hello SendGrid servicio de correo electrónico?</span><span class="sxs-lookup"><span data-stu-id="13f3b-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="13f3b-110">SendGrid es un [servicio de correo electrónico basado en la nube] que ofrece un sistema confiable de [entrega de correo electrónico transaccional], escalabilidad y análisis en tiempo real junto, con API flexibles que facilitan la integración personalizada.</span><span class="sxs-lookup"><span data-stu-id="13f3b-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="13f3b-111">Entre los escenarios de uso de SendGrid comunes se incluyen:</span><span class="sxs-lookup"><span data-stu-id="13f3b-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="13f3b-112">Enviar automáticamente confirmaciones toocustomers</span><span class="sxs-lookup"><span data-stu-id="13f3b-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="13f3b-113">Administración de listas de distribución para enviar a los clientes prospectos electrónicos y ofertas especiales cada mes</span><span class="sxs-lookup"><span data-stu-id="13f3b-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="13f3b-114">Recopilación de diversas métricas en tiempo real, como las direcciones de correo electrónico bloqueadas y la capacidad de respuesta del cliente.</span><span class="sxs-lookup"><span data-stu-id="13f3b-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="13f3b-115">Generar informes toohelp identificar tendencias</span><span class="sxs-lookup"><span data-stu-id="13f3b-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="13f3b-116">Reenvío de consultas de los clientes</span><span class="sxs-lookup"><span data-stu-id="13f3b-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="13f3b-117">Envío de notificaciones de correo electrónico desde su aplicación</span><span class="sxs-lookup"><span data-stu-id="13f3b-117">Email notifications from your application</span></span>

<span data-ttu-id="13f3b-118">Para obtener más información, consulte [https://sendgrid.com][https://sendgrid.com].</span><span class="sxs-lookup"><span data-stu-id="13f3b-118">For more information, see [https://sendgrid.com][https://sendgrid.com].</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="13f3b-119">Creación de una cuenta de SendGrid</span><span class="sxs-lookup"><span data-stu-id="13f3b-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a><span data-ttu-id="13f3b-120">Uso de SendGrid desde la aplicación PHP</span><span class="sxs-lookup"><span data-stu-id="13f3b-120">Using SendGrid from your PHP Application</span></span>
<span data-ttu-id="13f3b-121">El uso de SendGrid en una aplicación PHP de Azure no requiere una configuración ni una codificación especiales.</span><span class="sxs-lookup"><span data-stu-id="13f3b-121">Using SendGrid in an Azure PHP application requires no special configuration or coding.</span></span> <span data-ttu-id="13f3b-122">Como SendGrid es un servicio, puede obtenerse en hello exactamente igual desde una aplicación de nube tal como se puede desde una aplicación local.</span><span class="sxs-lookup"><span data-stu-id="13f3b-122">Because SendGrid is a service, it can be accessed in exactly hello same way from a cloud application as it can from an on-premises application.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="13f3b-123">Envío de un correo electrónico</span><span class="sxs-lookup"><span data-stu-id="13f3b-123">How to: Send an Email</span></span>
<span data-ttu-id="13f3b-124">Puede enviar correo electrónico mediante SMTP o hello Web API proporcionada por SendGrid.</span><span class="sxs-lookup"><span data-stu-id="13f3b-124">You can send email using either SMTP or hello Web API provided by SendGrid.</span></span>

### <a name="smtp-api"></a><span data-ttu-id="13f3b-125">API SMTP</span><span class="sxs-lookup"><span data-stu-id="13f3b-125">SMTP API</span></span>
<span data-ttu-id="13f3b-126">correo electrónico de toosend mediante hello SendGrid SMTP API, use *Swift Mailer*, una biblioteca basada en componentes para enviar mensajes de correo electrónico desde aplicaciones PHP.</span><span class="sxs-lookup"><span data-stu-id="13f3b-126">toosend email using hello SendGrid SMTP API, use *Swift Mailer*, a component-based library for sending emails from PHP applications.</span></span> <span data-ttu-id="13f3b-127">Puede descargar hello *Swift Mailer* biblioteca de [http://swiftmailer.org/download] [ http://swiftmailer.org/download] v5.3.0 (usar [compositor] tooinstall SWIFT Mailer).</span><span class="sxs-lookup"><span data-stu-id="13f3b-127">You can download hello *Swift Mailer* library from [http://swiftmailer.org/download][http://swiftmailer.org/download] v5.3.0 (use [Composer] tooinstall Swift Mailer).</span></span> <span data-ttu-id="13f3b-128">Enviar correo electrónico con la biblioteca de hello implica la creación de instancias de la <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, y <span class="auto-style2">Swift\_mensaje </span> clases, estableciendo las propiedades adecuadas y llamar a la <span class="auto-style2">Swift\_Mailer::send</span> método.</span><span class="sxs-lookup"><span data-stu-id="13f3b-128">Sending email with hello library involves creating instances of the <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, and <span class="auto-style2">Swift\_Message</span> classes, setting the appropriate properties, and calling the <span class="auto-style2">Swift\_Mailer::send</span> method.</span></span>

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

### <a name="web-api"></a><span data-ttu-id="13f3b-129">API Web</span><span class="sxs-lookup"><span data-stu-id="13f3b-129">Web API</span></span>
<span data-ttu-id="13f3b-130">Usar de PHP [curl función] [ curl function] toosend correo electrónico utilizando Hola SendGrid Web API.</span><span class="sxs-lookup"><span data-stu-id="13f3b-130">Use PHP's [curl function][curl function] toosend email using hello SendGrid Web API.</span></span>

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

<span data-ttu-id="13f3b-131">API de Web de SendGrid es muy similar tooa API de REST, aunque no es realmente una API de REST desde ese momento, en la mayoría de las llamadas, ambos obtener y verbos POST se pueden usar indistintamente.</span><span class="sxs-lookup"><span data-stu-id="13f3b-131">SendGrid's Web API is very similar tooa REST API, though it is not truly a RESTful API since, in most calls, both GET and POST verbs can be used interchangeably.</span></span>

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="13f3b-132">Adición de un correo electrónico</span><span class="sxs-lookup"><span data-stu-id="13f3b-132">How to: Add an Attachment</span></span>
### <a name="smtp-api"></a><span data-ttu-id="13f3b-133">API SMTP</span><span class="sxs-lookup"><span data-stu-id="13f3b-133">SMTP API</span></span>
<span data-ttu-id="13f3b-134">Enviar datos adjuntos con hello SMTP API implica una línea de script de ejemplo de código toohello para enviar un correo electrónico con Swift Mailer adicional.</span><span class="sxs-lookup"><span data-stu-id="13f3b-134">Sending an attachment using hello SMTP API involves one additional line of code toohello example script for sending an email with Swift Mailer.</span></span>

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

<span data-ttu-id="13f3b-135">línea de código más Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="13f3b-135">hello additional line of code is as follows:</span></span>

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

<span data-ttu-id="13f3b-136">Esta línea de código llama Hola attach (método) en la <span class="auto-style2">Swift\_mensaje</span> objeto y utiliza el método estático <span class="auto-style2">fromPath</span> en el <span class="auto-style2">Swift\_datos adjuntos</span>clase tooget y adjuntar un mensaje de tooa de archivo.</span><span class="sxs-lookup"><span data-stu-id="13f3b-136">This line of code calls hello attach method on the <span class="auto-style2">Swift\_Message</span> object and uses static method <span class="auto-style2">fromPath</span> on the <span class="auto-style2">Swift\_Attachment</span> class tooget and attach a file tooa message.</span></span>

### <a name="web-api"></a><span data-ttu-id="13f3b-137">API Web</span><span class="sxs-lookup"><span data-stu-id="13f3b-137">Web API</span></span>
<span data-ttu-id="13f3b-138">Enviar datos adjuntos con hello API Web están muy similar toosending un correo electrónico utilizando Hola API Web.</span><span class="sxs-lookup"><span data-stu-id="13f3b-138">Sending an attachment using hello Web API is very similar toosending an email using hello Web API.</span></span> <span data-ttu-id="13f3b-139">Sin embargo, tenga en cuenta que en el ejemplo de Hola que sigue, matriz de parámetros de hello debe contener este elemento:</span><span class="sxs-lookup"><span data-stu-id="13f3b-139">However, note that in hello example that follows, hello parameter array must contain this element:</span></span>

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

<span data-ttu-id="13f3b-140">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="13f3b-140">Example:</span></span>

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

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="13f3b-141">Cómo: Use los filtros tooEnable pies de página, el seguimiento y análisis</span><span class="sxs-lookup"><span data-stu-id="13f3b-141">How to: Use Filters tooEnable Footers, Tracking, and Analytics</span></span>
<span data-ttu-id="13f3b-142">SendGrid proporciona la funcionalidad de correo electrónico adicionales mediante el uso de Hola de filtros de' '.</span><span class="sxs-lookup"><span data-stu-id="13f3b-142">SendGrid provides additional email functionality through hello use of 'filters'.</span></span> <span data-ttu-id="13f3b-143">Se trata de configuración que puede agregarse al mensaje de correo electrónico tooan para habilitar la funcionalidad específica, como habilitar el seguimiento de clics, Google analytics, suscripción de seguimiento, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="13f3b-143">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span>

<span data-ttu-id="13f3b-144">Filtros pueden ser mensajes tooa aplicada mediante el uso de la propiedad de filtros de Hola.</span><span class="sxs-lookup"><span data-stu-id="13f3b-144">Filters can be applied tooa message by using hello filters property.</span></span> <span data-ttu-id="13f3b-145">Cada filtro se especifica mediante un hash que contiene la configuración específica del filtro.</span><span class="sxs-lookup"><span data-stu-id="13f3b-145">Each filter is specified by a hash containing filter-specific settings.</span></span> <span data-ttu-id="13f3b-146">En el ejemplo siguiente se habilita el filtro de pie de página de Hola y especifica un mensaje de texto que anexa toohello inferior del mensaje de correo electrónico de saludo.</span><span class="sxs-lookup"><span data-stu-id="13f3b-146">The following example enables hello footer filter and specifies a text message that will be appended toohello bottom of hello email message.</span></span>
<span data-ttu-id="13f3b-147">En este ejemplo usaremos biblioteca [sendgrid-php].</span><span class="sxs-lookup"><span data-stu-id="13f3b-147">For this example we will use [sendgrid-php library].</span></span>
<span data-ttu-id="13f3b-148">Use [compositor] tooinstall biblioteca:</span><span class="sxs-lookup"><span data-stu-id="13f3b-148">Use [Composer] tooinstall library:</span></span>

    php composer.phar require sendgrid/sendgrid 2.1.1

<span data-ttu-id="13f3b-149">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="13f3b-149">Example:</span></span>    

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

## <a name="next-steps"></a><span data-ttu-id="13f3b-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="13f3b-150">Next Steps</span></span>
<span data-ttu-id="13f3b-151">Ahora que ha aprendido conceptos básicos de Hola de hello servicio de correo electrónico de SendGrid, siga estos toolearn de vínculos más.</span><span class="sxs-lookup"><span data-stu-id="13f3b-151">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="13f3b-152">Documentación de SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="13f3b-152">SendGrid documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="13f3b-153">Biblioteca PHP de SendGrid: <https://github.com/sendgrid/sendgrid-php></span><span class="sxs-lookup"><span data-stu-id="13f3b-153">SendGrid PHP library: <https://github.com/sendgrid/sendgrid-php></span></span>
* <span data-ttu-id="13f3b-154">Oferta especial de SendGrid para clientes de Azure: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="13f3b-154">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

<span data-ttu-id="13f3b-155">Para obtener más información, vea también hello [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="13f3b-155">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

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
