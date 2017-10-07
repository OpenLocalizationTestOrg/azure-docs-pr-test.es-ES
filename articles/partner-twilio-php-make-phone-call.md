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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a><span data-ttu-id="2f679-104">¿Cómo tooMake una llamada de teléfono uso de Twilio en una aplicación PHP en Azure</span><span class="sxs-lookup"><span data-stu-id="2f679-104">How tooMake a Phone Call Using Twilio in a PHP Application on Azure</span></span>
<span data-ttu-id="2f679-105">Hello en el ejemplo siguiente se muestra cómo se puede utilizar una llamada desde una página web PHP hospedado en Azure de Twilio toomake.</span><span class="sxs-lookup"><span data-stu-id="2f679-105">hello following example shows you how you can use Twilio toomake a call from a PHP web page hosted in Azure.</span></span> <span data-ttu-id="2f679-106">aplicación resultante de Hello solicitará a Hola usuario valores de llamada de teléfono, como se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f679-106">hello resulting application will prompt hello user for phone call values, as shown in hello following screen shot.</span></span>

![Formulario de llamada de Azure con Twilio y PHP][twilio_php]

<span data-ttu-id="2f679-108">Necesitará toodo Hola siguiente código de hello toouse en este tema:</span><span class="sxs-lookup"><span data-stu-id="2f679-108">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="2f679-109">Adquiera una cuenta de Twilio y un token de autenticación desde la [Consola de Twilio][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="2f679-109">Acquire a Twilio account and authentication token from your [Twilio Console][twilio_console].</span></span> <span data-ttu-id="2f679-110">tooget a trabajar con Twilio, evaluar precios en [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="2f679-110">tooget started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="2f679-111">Puede registrarse para obtener una cuenta de prueba en [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="2f679-111">You can sign up for a trial account at [https://www.twilio.com/try-twilio][try_twilio].</span></span>
2. <span data-ttu-id="2f679-112">Obtener hello [Twilio biblioteca para PHP](https://github.com/twilio/twilio-php) o instalarlo como un paquete de PERA.</span><span class="sxs-lookup"><span data-stu-id="2f679-112">Obtain hello [Twilio library for PHP](https://github.com/twilio/twilio-php) or install it as a PEAR package.</span></span> <span data-ttu-id="2f679-113">Para obtener más información, vea hello [archivo Léame](https://github.com/twilio/twilio-php/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="2f679-113">For more information, see hello [readme file](https://github.com/twilio/twilio-php/blob/master/README.md).</span></span>
3. <span data-ttu-id="2f679-114">Instalar hello Azure SDK para PHP.</span><span class="sxs-lookup"><span data-stu-id="2f679-114">Install hello Azure SDK for PHP.</span></span> <span data-ttu-id="2f679-115">Para obtener información general de hello SDK e instrucciones acerca de cómo instalarlo, consulte [configurar hello Azure SDK para PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span><span class="sxs-lookup"><span data-stu-id="2f679-115">For an overview of hello SDK and instructions on installing it, see [Set up hello Azure SDK for PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="2f679-116">Creación de un formulario web para hacer una llamada</span><span class="sxs-lookup"><span data-stu-id="2f679-116">Create a web form for making a call</span></span>
<span data-ttu-id="2f679-117">Hola después HTML de código muestra cómo toobuild una página web (**callform.html**) que recupera datos de usuario para realizar una llamada:</span><span class="sxs-lookup"><span data-stu-id="2f679-117">hello following HTML code shows how toobuild a web page (**callform.html**) that retrieves user data for making a call:</span></span>

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

## <a name="create-hello-code-toomake-hello-call"></a><span data-ttu-id="2f679-118">Crear Hola código toomake Hola llamada</span><span class="sxs-lookup"><span data-stu-id="2f679-118">Create hello code toomake hello call</span></span>
<span data-ttu-id="2f679-119">Hola el siguiente código muestra cómo toobuild **makecall.php**, que se llama cuando el usuario de hello envía el formulario de hello muestra **callform.html**.</span><span class="sxs-lookup"><span data-stu-id="2f679-119">hello following code shows how toobuild **makecall.php**, which is called when hello user submits hello form displayed by **callform.html**.</span></span> <span data-ttu-id="2f679-120">Hola fragmento de código siguiente crea el mensaje de bienvenida de llamada y genera Hola llamada.</span><span class="sxs-lookup"><span data-stu-id="2f679-120">hello code shown below creates hello call message and generates hello call.</span></span> <span data-ttu-id="2f679-121">Además, puede toouse seguro de que su cuenta de Twilio y la autenticación de token de hello [Twilio consola] [ twilio_console] en lugar de valores de marcador de posición de hello asignados demasiado**$sid** y **$token** Hola del siguiente código.</span><span class="sxs-lookup"><span data-stu-id="2f679-121">Also, be sure toouse your Twilio account and authentication token from hello [Twilio Console][twilio_console] instead of hello placeholder values assigned too**$sid** and **$token** in hello code below.</span></span>

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

<span data-ttu-id="2f679-122">Además toomaking Hola llamada, **makecall.php** muestra algunos metadatos de la llamada, como se muestra en la imagen de hello siguiente.</span><span class="sxs-lookup"><span data-stu-id="2f679-122">In addition toomaking hello call, **makecall.php** displays some call metadata, as is shown in hello image below.</span></span> <span data-ttu-id="2f679-123">Para más información sobre los metadatos de llamada, vea [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span><span class="sxs-lookup"><span data-stu-id="2f679-123">For more information about call metadata, see [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span></span>

![Respuesta de llamada de Azure con Twilio y PHP][twilio_php_response]

## <a name="run-hello-application"></a><span data-ttu-id="2f679-125">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="2f679-125">Run hello application</span></span>
<span data-ttu-id="2f679-126">paso siguiente Hello es toodeploy su tooAzure sitios Web de aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f679-126">hello next step is toodeploy your application tooAzure Websites.</span></span> <span data-ttu-id="2f679-127">Hello artículos siguientes contienen información de Hola para crear un sitio Web e implementar el código con Git, FTP o WebMatrix (aunque no toda la información de cada artículo es relevante):</span><span class="sxs-lookup"><span data-stu-id="2f679-127">hello following articles contain hello information for creating a website and deploying your code with Git, FTP, or WebMatrix (though not all information in each article is relevant):</span></span>

* [<span data-ttu-id="2f679-128">Creación de un sitio web PHP-MySQL en el Servicio de aplicaciones de Azure e implementación mediante Git</span><span class="sxs-lookup"><span data-stu-id="2f679-128">Create a PHP-MySQL Azure Web Site and deploy using Git</span></span>](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [<span data-ttu-id="2f679-129">Creación de un sitio web PHP-MySQL en el Servicio de aplicaciones de Azure e implementación mediante FTP</span><span class="sxs-lookup"><span data-stu-id="2f679-129">Create a PHP-MySQL Azure Web Site and Deploy Using FTP</span></span>](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a><span data-ttu-id="2f679-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2f679-130">Next steps</span></span>
<span data-ttu-id="2f679-131">Este código se proporcionó tooshow funcionalidad básica con Twilio en PHP en Azure.</span><span class="sxs-lookup"><span data-stu-id="2f679-131">This code was provided tooshow you basic functionality using Twilio in PHP on Azure.</span></span> <span data-ttu-id="2f679-132">Antes de implementar tooAzure en producción, puede que desee tooadd más control de errores o con otras características.</span><span class="sxs-lookup"><span data-stu-id="2f679-132">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="2f679-133">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2f679-133">For example:</span></span>

* <span data-ttu-id="2f679-134">En lugar de utilizar un formulario web Forms, puede utilizar blobs de almacenamiento de Azure o números de teléfono de toostore de base de datos SQL y llamar a texto.</span><span class="sxs-lookup"><span data-stu-id="2f679-134">Instead of using a web form, you could use Azure storage blobs or SQL Database toostore phone numbers and call text.</span></span> <span data-ttu-id="2f679-135">Para obtener información sobre el uso de blobs de almacenamiento de Azure en PHP, vea [Uso de Azure Storage con aplicaciones de PHP][howto_blob_storage_php].</span><span class="sxs-lookup"><span data-stu-id="2f679-135">For information about using Azure storage blobs in PHP, see [Using Azure Storage with PHP Applications][howto_blob_storage_php].</span></span> <span data-ttu-id="2f679-136">Para obtener información sobre el uso de bases de datos SQL en PHP, vea [Uso de una base de datos SQL con aplicaciones de PHP][howto_sql_azure_php].</span><span class="sxs-lookup"><span data-stu-id="2f679-136">For information about using SQL Database in PHP, see [Using SQL Database with PHP Applications][howto_sql_azure_php].</span></span>
* <span data-ttu-id="2f679-137">Hola **makecall.php** código usa la dirección URL proporcionada Twilio ([http://twimlets.com/message][twimlet_message_url]) tooprovide una respuesta de lenguaje de marcado de Twilio (TwiML) que informa de cómo Twilio tooproceed con llamada Hola.</span><span class="sxs-lookup"><span data-stu-id="2f679-137">hello **makecall.php** code uses Twilio-provided URL ([http://twimlets.com/message][twimlet_message_url]) tooprovide a Twilio Markup Language (TwiML) response that informs Twilio how tooproceed with hello call.</span></span> <span data-ttu-id="2f679-138">Por ejemplo, puede contener hello TwiML que se devuelve un `<Say>` verbo que es el resultado en texto que se va a toohello hablado destinatario de la llamada.</span><span class="sxs-lookup"><span data-stu-id="2f679-138">For example, hello TwiML that is returned can contain a `<Say>` verb that results in text being spoken toohello call recipient.</span></span> <span data-ttu-id="2f679-139">En lugar de usar la dirección URL proporcionada Twilio por hello, puede generar la solicitud de su propio tooTwilio toorespond servicio; Para obtener más información, consulte [cómo tooUse Twilio para capacidades de SMS en PHP y voz][howto_twilio_voice_sms_php].</span><span class="sxs-lookup"><span data-stu-id="2f679-139">Instead of using hello Twilio-provided URL, you could build your own service toorespond tooTwilio's request; for more information, see [How tooUse Twilio for Voice and SMS Capabilities in PHP][howto_twilio_voice_sms_php].</span></span> <span data-ttu-id="2f679-140">Puede encontrar más información sobre TwiML en [http://www.twilio.com/docs/api/twiml][twiml], y más información sobre `<Say>` y otros verbos de Twilio en [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="2f679-140">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about `<Say>` and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="2f679-141">Lea las directrices de seguridad de hello Twilio en [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="2f679-141">Read hello Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="2f679-142">Para obtener información adicional sobre Twilio, vea [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="2f679-142">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="2f679-143">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="2f679-143">See Also</span></span>
* [<span data-ttu-id="2f679-144">Cómo tooUse Twilio para capacidades de SMS en PHP y voz</span><span class="sxs-lookup"><span data-stu-id="2f679-144">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>](partner-twilio-php-how-to-use-voice-sms.md)

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
