---
title: Uso de Twilio para voz y SMS (PHP) | Microsoft Docs
description: "Aprenda a realizar llamadas telefónicas y a enviar mensajes SMS con el servicio de la API de Twilio en Azure. Ejemplos de código escritos en PHP."
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
ms.openlocfilehash: bd50eac7390e8639f77894689388e6926cdb619c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="c7db2-104">Uso de Twilio para capacidades de voz y SMS en PHP</span><span class="sxs-lookup"><span data-stu-id="c7db2-104">How to Use Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="c7db2-105">Esta guía describe cómo realizar tareas comunes de programación con el servicio de API de Twilio en Azure.</span><span class="sxs-lookup"><span data-stu-id="c7db2-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="c7db2-106">Entre los escenarios descritos se incluyen realizar una llamada telefónica y enviar un mensaje de servicio de mensajes cortos (SMS).</span><span class="sxs-lookup"><span data-stu-id="c7db2-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="c7db2-107">Para obtener más información sobre Twilio y el uso de voz y mensajes SMS en sus aplicaciones, consulte la sección [Pasos siguientes](#NextSteps) .</span><span class="sxs-lookup"><span data-stu-id="c7db2-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="c7db2-108"><a id="WhatIs"></a>¿Qué es Twilio?</span><span class="sxs-lookup"><span data-stu-id="c7db2-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="c7db2-109">Twilio está potenciando el futuro de las comunicaciones empresariales, al permitir que los desarrolladores inserten voz, VoIP y mensajería en las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c7db2-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="c7db2-110">Pueden virtualizar toda la infraestructura necesaria en un entorno global basado en la nube y exponerlo a través de la plataforma API de comunicaciones de Twilio.</span><span class="sxs-lookup"><span data-stu-id="c7db2-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="c7db2-111">Las aplicaciones son sencillas de compilar y pueden escalarse.</span><span class="sxs-lookup"><span data-stu-id="c7db2-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="c7db2-112">Disfrute de la flexibilidad de pagar por lo que utiliza y aproveche la confiabilidad de la nube.</span><span class="sxs-lookup"><span data-stu-id="c7db2-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="c7db2-113">**Twilio Voice** permite que sus aplicaciones realicen y reciban llamadas.</span><span class="sxs-lookup"><span data-stu-id="c7db2-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="c7db2-114">**Twilio SMS** permite que su aplicación envíe y reciba mensajes de texto.</span><span class="sxs-lookup"><span data-stu-id="c7db2-114">**Twilio SMS** enables your application to send and receive text messages.</span></span> <span data-ttu-id="c7db2-115">**Twilio Client** permite realizar llamadas VoIP desde cualquier teléfono, tableta o explorador, y es compatible con WebRTC.</span><span class="sxs-lookup"><span data-stu-id="c7db2-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="c7db2-116"><a id="Pricing"></a>Precios de Twilio y ofertas especiales</span><span class="sxs-lookup"><span data-stu-id="c7db2-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="c7db2-117">Los clientes de Azure reciben una [oferta especial](http://www.twilio.com/azure): 10 $ de regalo en crédito Twilio al actualizar su cuenta Twilio.</span><span class="sxs-lookup"><span data-stu-id="c7db2-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="c7db2-118">Este crédito Twilio se puede aplicar a cualquier uso de Twilio (10 $ de crédito equivalen al envío de aproximadamente 1.000 mensajes SMS o recibir hasta 1.000 minutos de voz entrante, según la ubicación del número de teléfono y el destino del mensaje o de la llamada).</span><span class="sxs-lookup"><span data-stu-id="c7db2-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="c7db2-119">Canjee este crédito Twilio y comience en [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="c7db2-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="c7db2-120">Twilio es un servicio de pago por uso.</span><span class="sxs-lookup"><span data-stu-id="c7db2-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="c7db2-121">No hay comisiones establecidas y puede cerrar su cuenta en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="c7db2-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="c7db2-122">Puede encontrar más detalles en [Precios de Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="c7db2-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="c7db2-123"><a id="Concepts"></a>Conceptos</span><span class="sxs-lookup"><span data-stu-id="c7db2-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="c7db2-124">La API de Twilio es una API de RESTful que proporciona funciones de voz y SMS para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c7db2-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="c7db2-125">Las bibliotecas de cliente están disponibles en varios lenguajes; para ver una lista, consulte las [bibliotecas de API de Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="c7db2-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="c7db2-126">Aspectos fundamentales de la API de Twilio son los verbos de Twilio y el lenguaje de marcado de Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="c7db2-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="c7db2-127"><a id="Verbs"></a>Verbos de Twilio</span><span class="sxs-lookup"><span data-stu-id="c7db2-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="c7db2-128">La API usa dos verbos de Twilio; por ejemplo, el verbo **&lt;Say&gt;** indica a Twilio que entregue de manera audible un mensaje en una llamada.</span><span class="sxs-lookup"><span data-stu-id="c7db2-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="c7db2-129">A continuación se presenta una lista de verbos de Twilio.</span><span class="sxs-lookup"><span data-stu-id="c7db2-129">The following is a list of Twilio verbs.</span></span> <span data-ttu-id="c7db2-130">Obtenga información sobre los demás verbos y las capacidades de Twilio a través de [Documentación de lenguaje de marcado de Twilio](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="c7db2-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="c7db2-131">**&lt;Dial&gt;**: conecta la persona que llama con otro teléfono.</span><span class="sxs-lookup"><span data-stu-id="c7db2-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="c7db2-132">**&lt;Gather&gt;**: recopila los dígitos numéricos que se introdujeron en el teclado del teléfono.</span><span class="sxs-lookup"><span data-stu-id="c7db2-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="c7db2-133">**&lt;Hangup&gt;**: finaliza una llamada.</span><span class="sxs-lookup"><span data-stu-id="c7db2-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="c7db2-134">**&lt;Play&gt;**: reproduce un archivo de audio.</span><span class="sxs-lookup"><span data-stu-id="c7db2-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="c7db2-135">**&lt;Pause&gt;**: espera en silencio una cantidad de segundos específica.</span><span class="sxs-lookup"><span data-stu-id="c7db2-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="c7db2-136">**&lt;Record&gt;**: graba la voz de la persona que llama y devuelve una dirección URL de un archivo que contiene la grabación.</span><span class="sxs-lookup"><span data-stu-id="c7db2-136">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="c7db2-137">**&lt;Redirect&gt;**: transfiere el control de una llamada o SMS al TwiML en una URL diferente.</span><span class="sxs-lookup"><span data-stu-id="c7db2-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="c7db2-138">**&lt;Reject&gt;**: rechaza una llamada entrante a su número de Twilio sin cobrarle.</span><span class="sxs-lookup"><span data-stu-id="c7db2-138">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="c7db2-139">**&lt;Say&gt;**: convierte texto en voz para hacer una llamada.</span><span class="sxs-lookup"><span data-stu-id="c7db2-139">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="c7db2-140">**&lt;Sms&gt;**: envía un mensaje SMS.</span><span class="sxs-lookup"><span data-stu-id="c7db2-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="c7db2-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="c7db2-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="c7db2-142">TwiML es un conjunto de instrucciones basadas en XML y en los verbos de Twilio que informan a Twilio sobre cómo procesar una llamada o un SMS.</span><span class="sxs-lookup"><span data-stu-id="c7db2-142">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="c7db2-143">Como ejemplo, el siguiente TwiML convierte el texto **Hello World** en voz.</span><span class="sxs-lookup"><span data-stu-id="c7db2-143">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="c7db2-144">Cuando su aplicación llama a la API de Twilio, uno de los parámetros de API es la URL que devuelve la respuesta de TwiML.</span><span class="sxs-lookup"><span data-stu-id="c7db2-144">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="c7db2-145">Con fines de desarrollo, puede usar las URL que ofrece Twilio para proporcionar las respuestas de TwiML que usaron sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c7db2-145">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="c7db2-146">También puede hospedar sus propias URL para producir las repuestas de TwiML; otra opción es usar el objeto **TwiMLResponse** .</span><span class="sxs-lookup"><span data-stu-id="c7db2-146">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="c7db2-147">Para obtener más información sobre los verbos de Twilio, sus atributos y TwiML, consulte [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="c7db2-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="c7db2-148">Para obtener información adicional sobre la API de Twilio, consulte la [API de Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="c7db2-148">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="c7db2-149"><a id="CreateAccount"></a>Creación de una cuenta de Twilio</span><span class="sxs-lookup"><span data-stu-id="c7db2-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="c7db2-150">Cuando esté preparado para obtener una cuenta de Twilio, regístrese en la página de [evaluación de Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="c7db2-150">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="c7db2-151">Puede empezar con una cuenta gratuita y, posteriormente, actualizarla.</span><span class="sxs-lookup"><span data-stu-id="c7db2-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="c7db2-152">Cuando se registre para obtener una cuenta de Twilio, recibirá un identificador de cuenta y un token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="c7db2-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="c7db2-153">Necesitará ambos para realizar llamadas a la API de Twilio.</span><span class="sxs-lookup"><span data-stu-id="c7db2-153">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="c7db2-154">Para evitar el acceso no autorizado a su cuenta, mantenga protegido el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="c7db2-154">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="c7db2-155">Puede ver el identificador de cuenta y el token de autenticación en la [página de la cuenta de Twilio][twilio_account], en los campos etiquetados como **ACCOUNT SID** y **AUTH TOKEN**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="c7db2-155">Your account ID and authentication token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="c7db2-156"><a id="create_app"></a>Creación de una aplicación PHP</span><span class="sxs-lookup"><span data-stu-id="c7db2-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="c7db2-157">Una aplicación PHP que usa el servicio Twilio y que se ejecuta en Azure no es distinta a otra aplicación PHP que use el servicio Twilio.</span><span class="sxs-lookup"><span data-stu-id="c7db2-157">A PHP application that uses the Twilio service and is running in Azure is no different than any other PHP application that uses the Twilio service.</span></span> <span data-ttu-id="c7db2-158">Mientras los servicios de Twilio están basadas en REST y pueden llamarse desde PHP de varias maneras, este artículo se centrará en cómo usar servicios de Twilio con [Twilio biblioteca para PHP desde GitHub][twilio_php].</span><span class="sxs-lookup"><span data-stu-id="c7db2-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how to use Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="c7db2-159">Para obtener más información sobre el uso de la biblioteca de Twilio para PHP, consulte [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="c7db2-159">For more information about using the Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="c7db2-160">Instrucciones detalladas para crear e implementar una aplicación de Twilio y PHP en Azure están disponibles en [cómo hacer que un Twilio de uso de la llamada de teléfono en una aplicación PHP en Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="c7db2-160">Detailed instructions for building and deploying a Twilio/PHP application to Azure are available at [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="c7db2-161"><a id="configure_app"></a>Configuración de la aplicación para usar bibliotecas de Twilio</span><span class="sxs-lookup"><span data-stu-id="c7db2-161"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="c7db2-162">Puede configurar la aplicación para que use la biblioteca de Twilio para PHP de dos formas:</span><span class="sxs-lookup"><span data-stu-id="c7db2-162">You can configure your application to use the Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="c7db2-163">Descargue la biblioteca de Twilio para PHP desde GitHub ([https://github.com/twilio/twilio-php][twilio_php]) y agregue el **servicios** directorio a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7db2-163">Download the Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add the **Services** directory to your application.</span></span>
   
    <span data-ttu-id="c7db2-164">O</span><span class="sxs-lookup"><span data-stu-id="c7db2-164">-OR-</span></span>
2. <span data-ttu-id="c7db2-165">Instale la biblioteca de Twilio para PHP como paquete PEAR.</span><span class="sxs-lookup"><span data-stu-id="c7db2-165">Install the Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="c7db2-166">Puede instalarse con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="c7db2-166">It can be installed with the following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="c7db2-167">Una vez que haya instalado la biblioteca de Twilio para PHP, puede agregar a continuación una instrucción **require_once** en la parte superior de los archivos PHP para hacer referencia a la biblioteca:</span><span class="sxs-lookup"><span data-stu-id="c7db2-167">Once you have installed the Twilio library for PHP, you can then add a **require_once** statement at the top of your PHP files to reference the library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="c7db2-168">Para obtener más información, consulte [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="c7db2-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="c7db2-169"><a id="howto_make_call"></a>Realización de una llamada saliente</span><span class="sxs-lookup"><span data-stu-id="c7db2-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="c7db2-170">A continuación, se indica cómo realizar una llamada saliente con la clase **Services_Twilio**.</span><span class="sxs-lookup"><span data-stu-id="c7db2-170">The following shows how to make an outgoing call using the **Services_Twilio** class.</span></span> <span data-ttu-id="c7db2-171">Este código también utiliza un sitio que proporciona Twilio para devolver la respuesta de lenguaje de marcado de Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="c7db2-171">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="c7db2-172">Sustituya los valores de los números de teléfono **From** (De) y **To** (Para) y asegúrese de comprobar el número de teléfono **From** (De) de su cuenta de Twilio antes de ejecutar el código.</span><span class="sxs-lookup"><span data-stu-id="c7db2-172">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // The number of the phone initiating the the call.
    $from_number = "NNNNNNNNNNN";

    // The number of the phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use the Twilio-provided site for the TwiML response.
    $url = "http://twimlets.com/message";

    // The phone message text.
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make the call.
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

<span data-ttu-id="c7db2-173">Como se mencionó, este código usa el sitio proporcionado por Twilio para devolver la respuesta de TwiML.</span><span class="sxs-lookup"><span data-stu-id="c7db2-173">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="c7db2-174">A parte, también puede usar su propio sitio web para proporcionar la respuesta de TwiML; si desea obtener más información, consulte [Procedimientos: Suministro de respuestas de TwiML desde su propio sitio web](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="c7db2-174">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="c7db2-175">**Tenga en cuenta**: para solucionar errores de validación de certificado SSL, vea [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="c7db2-175">**Note**: To troubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="c7db2-176"><a id="howto_send_sms"></a>Envío de un mensaje SMS</span><span class="sxs-lookup"><span data-stu-id="c7db2-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="c7db2-177">A continuación se muestra cómo enviar un mensaje SMS con la clase **Services_Twilio**.</span><span class="sxs-lookup"><span data-stu-id="c7db2-177">The following shows how to send an SMS message using the **Services_Twilio** class.</span></span> <span data-ttu-id="c7db2-178">El número **From** lo proporciona Twilio en las cuentas de evaluación para enviar mensajes SMS.</span><span class="sxs-lookup"><span data-stu-id="c7db2-178">The **From** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="c7db2-179">El número **To** se debe comprobar para la cuenta de Twilio antes de ejecutar el código.</span><span class="sxs-lookup"><span data-stu-id="c7db2-179">The **To** number must be verified for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send the SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <span data-ttu-id="c7db2-180"><a id="howto_provide_twiml_responses"></a>Entrega de respuestas de TwiML desde su propio sitio web</span><span class="sxs-lookup"><span data-stu-id="c7db2-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="c7db2-181">Cuando la aplicación inicia una llamada a la API de Twilio, Twilio envía su solicitud a una URL que debe devolver una respuesta de TwiML.</span><span class="sxs-lookup"><span data-stu-id="c7db2-181">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="c7db2-182">El ejemplo anterior usa la dirección URL [http://twimlets.com/message][twimlet_message_url] proporcionada por Twilio.</span><span class="sxs-lookup"><span data-stu-id="c7db2-182">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="c7db2-183">(Aunque TwiML está diseñado para su uso por Twilio, puede verlo en el explorador.</span><span class="sxs-lookup"><span data-stu-id="c7db2-183">(While TwiML is designed for use by Twilio, you can view the it in your browser.</span></span> <span data-ttu-id="c7db2-184">Por ejemplo, haga clic en [http://twimlets.com/message][twimlet_message_url] para ver un elemento `<Response>` vacío. Otro ejemplo: haga clic en [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] para ver un elemento `<Response>` que contiene un elemento `<Say>`).</span><span class="sxs-lookup"><span data-stu-id="c7db2-184">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="c7db2-185">En lugar de confiar en la URL que Twilio proporciona, puede crear su propio sitio que devuelve respuestas HTTP.</span><span class="sxs-lookup"><span data-stu-id="c7db2-185">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="c7db2-186">Puede crear el sitio en cualquier lenguaje que devuelva respuestas XML; en este tema se asume que usará PHP para crear el TwiML.</span><span class="sxs-lookup"><span data-stu-id="c7db2-186">You can create the site in any language that returns XML responses; this topic assumes you'll be using PHP to create the TwiML.</span></span>

<span data-ttu-id="c7db2-187">La siguiente página PHP da como resultado una respuesta de TwiML que dice **Hello World** en la llamada.</span><span class="sxs-lookup"><span data-stu-id="c7db2-187">The following PHP page results in a TwiML response that says **Hello World** on the call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="c7db2-188">Como puede ver en el ejemplo anterior, la respuesta de TwiML es sencillamente un documento XML.</span><span class="sxs-lookup"><span data-stu-id="c7db2-188">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="c7db2-189">La biblioteca de Twilio para PHP contiene clases que generarán TwiML de manera automática.</span><span class="sxs-lookup"><span data-stu-id="c7db2-189">The Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="c7db2-190">El ejemplo siguiente genera la respuesta equivalente como se ha mostrado anteriormente, pero usa la clase **Services\_Twilio\_Twiml** de la biblioteca de Twilio para PHP:</span><span class="sxs-lookup"><span data-stu-id="c7db2-190">The example below produces the equivalent response as shown above, but uses the **Services\_Twilio\_Twiml** class in the Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="c7db2-191">Para más información sobre TwiML, vea [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="c7db2-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="c7db2-192">Una vez tenga configurada su página de PHP para proporcionar respuestas de TwiML, use la URL de la página PHP como la URL que se transmite al método `Services_Twilio->account->calls->create`.</span><span class="sxs-lookup"><span data-stu-id="c7db2-192">Once you have your PHP page set up to provide TwiML responses, use the URL of the PHP page as the URL passed into the  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="c7db2-193">Por ejemplo, si tiene una aplicación web llamada **MyTwiML** implementada en un servicio hospedado de Azure y el nombre de la página de PHP es **mytwiml.php**, la dirección URL se puede transmitir a **Services_Twilio->account->calls->create**, tal como aparece a continuación:</span><span class="sxs-lookup"><span data-stu-id="c7db2-193">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, and the name of the PHP page is **mytwiml.php**, the URL can be passed to  **Services_Twilio->account->calls->create**  as shown in the following example:</span></span>

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // The phone message text.
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

<span data-ttu-id="c7db2-194">Para obtener información adicional acerca del uso de Twilio en Azure con PHP, consulte [cómo hacer que un Twilio de uso de la llamada de teléfono en una aplicación PHP en Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="c7db2-194">For additional information about using Twilio in Azure with PHP, see [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="c7db2-195"><a id="AdditionalServices"></a>Procedimientos: Uso de servicios Twilio adicionales</span><span class="sxs-lookup"><span data-stu-id="c7db2-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="c7db2-196">Además de los ejemplos aquí mostrados, Twilio ofrece API basadas en web que puede utilizar para aprovechar las funciones adicionales de Twilio desde su aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="c7db2-196">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="c7db2-197">Para obtener los detalles completos, vea la [Documentación de la API de Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="c7db2-197">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="c7db2-198"><a id="NextSteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c7db2-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="c7db2-199">Ahora que conoce los fundamentos del servicio Twilio, siga estos vínculos para obtener más información:</span><span class="sxs-lookup"><span data-stu-id="c7db2-199">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="c7db2-200">[Directrices de seguridad de Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="c7db2-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="c7db2-201">[Procedimientos y código de ejemplo de Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="c7db2-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="c7db2-202">[Tutoriales de inicio rápido de Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="c7db2-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="c7db2-203">[Twilio en GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="c7db2-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="c7db2-204">[Contactar con el servicio técnico de Twilio][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="c7db2-204">[Talk to Twilio Support][twilio_support]</span></span>

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
