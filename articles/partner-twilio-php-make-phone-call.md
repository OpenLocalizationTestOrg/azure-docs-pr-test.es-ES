---
title: "Realización de una llamada telefónica desde Twilio (PHP) | Microsoft Docs"
description: "Aprenda a realizar llamadas telefónicas y a enviar mensajes SMS con el servicio de la API de Twilio en Azure. Ejemplos para la aplicación PHP."
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
ms.openlocfilehash: f35450ace02727ddf392dbbe857b934a45ee022a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-make-a-phone-call-using-twilio-in-a-php-application-on-azure"></a><span data-ttu-id="a9059-104">Realización de una llamada telefónica con Twilio en una aplicación PHP en Azure</span><span class="sxs-lookup"><span data-stu-id="a9059-104">How to Make a Phone Call Using Twilio in a PHP Application on Azure</span></span>
<span data-ttu-id="a9059-105">El siguiente ejemplo muestra cómo se puede usar Twilio para realizar una llamada desde una página web PHP hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="a9059-105">The following example shows you how you can use Twilio to make a call from a PHP web page hosted in Azure.</span></span> <span data-ttu-id="a9059-106">La aplicación resultante le pedirá al usuario los valores de una llamada telefónica, como se muestra en la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="a9059-106">The resulting application will prompt the user for phone call values, as shown in the following screen shot.</span></span>

![Formulario de llamada de Azure con Twilio y PHP][twilio_php]

<span data-ttu-id="a9059-108">Tendrá que hacer lo siguiente para utilizar el código de este tema:</span><span class="sxs-lookup"><span data-stu-id="a9059-108">You'll need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="a9059-109">Adquiera una cuenta de Twilio y un token de autenticación desde la [Consola de Twilio][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="a9059-109">Acquire a Twilio account and authentication token from your [Twilio Console][twilio_console].</span></span> <span data-ttu-id="a9059-110">Para empezar con Twilio, evalúe los precios en [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="a9059-110">To get started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="a9059-111">Puede registrarse para obtener una cuenta de prueba en [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="a9059-111">You can sign up for a trial account at [https://www.twilio.com/try-twilio][try_twilio].</span></span>
2. <span data-ttu-id="a9059-112">Instale la [biblioteca de Twilio para PHP](https://github.com/twilio/twilio-php) como paquete PEAR.</span><span class="sxs-lookup"><span data-stu-id="a9059-112">Obtain the [Twilio library for PHP](https://github.com/twilio/twilio-php) or install it as a PEAR package.</span></span> <span data-ttu-id="a9059-113">Para obtener más información, consulte el [archivo Léame](https://github.com/twilio/twilio-php/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="a9059-113">For more information, see the [readme file](https://github.com/twilio/twilio-php/blob/master/README.md).</span></span>
3. <span data-ttu-id="a9059-114">Instale el SDK de Azure para PHP.</span><span class="sxs-lookup"><span data-stu-id="a9059-114">Install the Azure SDK for PHP.</span></span> <span data-ttu-id="a9059-115">Para obtener información general sobre el SDK e instrucciones sobre cómo instalarlo, vea [Configurar el SDK de Azure para PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span><span class="sxs-lookup"><span data-stu-id="a9059-115">For an overview of the SDK and instructions on installing it, see [Set up the Azure SDK for PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="a9059-116">Creación de un formulario web para hacer una llamada</span><span class="sxs-lookup"><span data-stu-id="a9059-116">Create a web form for making a call</span></span>
<span data-ttu-id="a9059-117">El código HTML siguiente muestra cómo crear una página web (**callform.html**) que recupera datos de usuarios para realizar una llamada:</span><span class="sxs-lookup"><span data-stu-id="a9059-117">The following HTML code shows how to build a web page (**callform.html**) that retrieves user data for making a call:</span></span>

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
        <td><input name="callText" size="100" type="text" value="Hello. This is the call text. Good bye."></td>
      </tr>
      <tr>
        <td colspan="2"><input type="submit" value="Make this call"></td>
      </tr>
    </table>
  </form><br>
</body>
</html>
```

## <a name="create-the-code-to-make-the-call"></a><span data-ttu-id="a9059-118">Creación del código para realizar la llamada</span><span class="sxs-lookup"><span data-stu-id="a9059-118">Create the code to make the call</span></span>
<span data-ttu-id="a9059-119">El código siguiente muestra cómo crear **makecall.php**, que se llama cuando el usuario envía el formulario mostrado por **callform.html**.</span><span class="sxs-lookup"><span data-stu-id="a9059-119">The following code shows how to build **makecall.php**, which is called when the user submits the form displayed by **callform.html**.</span></span> <span data-ttu-id="a9059-120">El código que se muestra a continuación crea el mensaje de llamada y genera la llamada.</span><span class="sxs-lookup"><span data-stu-id="a9059-120">The code shown below creates the call message and generates the call.</span></span> <span data-ttu-id="a9059-121">Además, asegúrese de usar la cuenta Twilio y el token de autenticación de la [Consola de Twilio][twilio_console] en lugar de los valores de marcador de posición asignados a **$sid** y **$token** en el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="a9059-121">Also, be sure to use your Twilio account and authentication token from the [Twilio Console][twilio_console] instead of the placeholder values assigned to **$sid** and **$token** in the code below.</span></span>

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

<span data-ttu-id="a9059-122">Además de realizar la llamada, **makecall.php** muestra algunos metadatos, como se muestra en la imagen siguiente.</span><span class="sxs-lookup"><span data-stu-id="a9059-122">In addition to making the call, **makecall.php** displays some call metadata, as is shown in the image below.</span></span> <span data-ttu-id="a9059-123">Para más información sobre los metadatos de llamada, vea [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span><span class="sxs-lookup"><span data-stu-id="a9059-123">For more information about call metadata, see [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span></span>

![Respuesta de llamada de Azure con Twilio y PHP][twilio_php_response]

## <a name="run-the-application"></a><span data-ttu-id="a9059-125">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="a9059-125">Run the application</span></span>
<span data-ttu-id="a9059-126">El paso siguiente consiste en implementar la aplicación en Sitios web Azure.</span><span class="sxs-lookup"><span data-stu-id="a9059-126">The next step is to deploy your application to Azure Websites.</span></span> <span data-ttu-id="a9059-127">Los artículos siguientes contienen la información necesaria para crear un sitio web e implementar el código con Git, FTP o WebMatrix (si bien no toda la información de cada uno de los artículos es relevante):</span><span class="sxs-lookup"><span data-stu-id="a9059-127">The following articles contain the information for creating a website and deploying your code with Git, FTP, or WebMatrix (though not all information in each article is relevant):</span></span>

* [<span data-ttu-id="a9059-128">Creación de un sitio web PHP-MySQL en el Servicio de aplicaciones de Azure e implementación mediante Git</span><span class="sxs-lookup"><span data-stu-id="a9059-128">Create a PHP-MySQL Azure Web Site and deploy using Git</span></span>](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [<span data-ttu-id="a9059-129">Creación de un sitio web PHP-MySQL en el Servicio de aplicaciones de Azure e implementación mediante FTP</span><span class="sxs-lookup"><span data-stu-id="a9059-129">Create a PHP-MySQL Azure Web Site and Deploy Using FTP</span></span>](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a><span data-ttu-id="a9059-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a9059-130">Next steps</span></span>
<span data-ttu-id="a9059-131">Este código se ha proporcionado para mostrar la funcionalidad básica usando Twilio en PHP en Azure.</span><span class="sxs-lookup"><span data-stu-id="a9059-131">This code was provided to show you basic functionality using Twilio in PHP on Azure.</span></span> <span data-ttu-id="a9059-132">Antes de implementarlo en Azure en producción, es posible que desee agregar más controles de errores u otras características.</span><span class="sxs-lookup"><span data-stu-id="a9059-132">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="a9059-133">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a9059-133">For example:</span></span>

* <span data-ttu-id="a9059-134">En lugar de usar un formulario web, puede usar blobs de almacenamiento de Azure o una base de datos SQL para almacenar los números de teléfono y el texto de llamada.</span><span class="sxs-lookup"><span data-stu-id="a9059-134">Instead of using a web form, you could use Azure storage blobs or SQL Database to store phone numbers and call text.</span></span> <span data-ttu-id="a9059-135">Para obtener información sobre el uso de blobs de almacenamiento de Azure en PHP, vea [Uso de Azure Storage con aplicaciones de PHP][howto_blob_storage_php].</span><span class="sxs-lookup"><span data-stu-id="a9059-135">For information about using Azure storage blobs in PHP, see [Using Azure Storage with PHP Applications][howto_blob_storage_php].</span></span> <span data-ttu-id="a9059-136">Para obtener información sobre el uso de bases de datos SQL en PHP, vea [Uso de una base de datos SQL con aplicaciones de PHP][howto_sql_azure_php].</span><span class="sxs-lookup"><span data-stu-id="a9059-136">For information about using SQL Database in PHP, see [Using SQL Database with PHP Applications][howto_sql_azure_php].</span></span>
* <span data-ttu-id="a9059-137">El código de **makecall.php** usa una dirección URL ([http://twimlets.com/message][twimlet_message_url]) de Twilio para proporcionar una respuesta de Lenguaje de marcado de Twilio (TwiML) que indica a Twilio cómo proceder con la llamada.</span><span class="sxs-lookup"><span data-stu-id="a9059-137">The **makecall.php** code uses Twilio-provided URL ([http://twimlets.com/message][twimlet_message_url]) to provide a Twilio Markup Language (TwiML) response that informs Twilio how to proceed with the call.</span></span> <span data-ttu-id="a9059-138">Por ejemplo, la TwiML que se devuelve puede contener un verbo `<Say>` que se traduce en el texto que se está hablando con el destinatario de la llamada.</span><span class="sxs-lookup"><span data-stu-id="a9059-138">For example, the TwiML that is returned can contain a `<Say>` verb that results in text being spoken to the call recipient.</span></span> <span data-ttu-id="a9059-139">En lugar de usar la dirección URL proporcionada por Twilio, podría crear su propio servicio para responder a la solicitud de Twilio. Para más información, vea [Uso de Twilio para capacidades de voz y SMS en PHP][howto_twilio_voice_sms_php].</span><span class="sxs-lookup"><span data-stu-id="a9059-139">Instead of using the Twilio-provided URL, you could build your own service to respond to Twilio's request; for more information, see [How to Use Twilio for Voice and SMS Capabilities in PHP][howto_twilio_voice_sms_php].</span></span> <span data-ttu-id="a9059-140">Puede encontrar más información sobre TwiML en [http://www.twilio.com/docs/api/twiml][twiml], y más información sobre `<Say>` y otros verbos de Twilio en [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="a9059-140">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about `<Say>` and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="a9059-141">Lea las directrices de seguridad de Twilio en [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="a9059-141">Read the Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="a9059-142">Para obtener información adicional sobre Twilio, vea [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="a9059-142">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="a9059-143">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="a9059-143">See Also</span></span>
* [<span data-ttu-id="a9059-144">Uso de Twilio para capacidades de voz y SMS en PHP</span><span class="sxs-lookup"><span data-stu-id="a9059-144">How to Use Twilio for Voice and SMS Capabilities in PHP</span></span>](partner-twilio-php-how-to-use-voice-sms.md)

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
