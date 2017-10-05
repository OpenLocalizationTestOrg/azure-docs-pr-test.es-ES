---
title: Uso de Twilio para voz y SMS (Ruby) | Microsoft Docs
description: "Aprenda a realizar llamadas telefónicas y a enviar mensajes SMS con el servicio de la API de Twilio en Azure. Ejemplos de código escritos en Ruby."
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
ms.openlocfilehash: 69e50e7fe0e1f302e96c309878b8dea6869dff4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="2a9de-104">Uso de Twilio para capacidades de voz y SMS en Ruby</span><span class="sxs-lookup"><span data-stu-id="2a9de-104">How to Use Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="2a9de-105">Esta guía describe cómo realizar tareas comunes de programación con el servicio de API de Twilio en Azure.</span><span class="sxs-lookup"><span data-stu-id="2a9de-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="2a9de-106">Entre los escenarios descritos se incluyen realizar una llamada telefónica y enviar un mensaje de servicio de mensajes cortos (SMS).</span><span class="sxs-lookup"><span data-stu-id="2a9de-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="2a9de-107">Para obtener más información sobre Twilio y el uso de voz y mensajes SMS en sus aplicaciones, consulte la sección [Pasos siguientes](#NextSteps) .</span><span class="sxs-lookup"><span data-stu-id="2a9de-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="2a9de-108"><a id="WhatIs"></a>¿Qué es Twilio?</span><span class="sxs-lookup"><span data-stu-id="2a9de-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="2a9de-109">Twilio es una API de servicio web de telefonía que le permite utilizar las habilidades y lenguajes web existentes para crear aplicaciones de voz y SMS.</span><span class="sxs-lookup"><span data-stu-id="2a9de-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="2a9de-110">Twilio es un servicio de terceros (no una característica de Azure ni tampoco un producto de Microsoft).</span><span class="sxs-lookup"><span data-stu-id="2a9de-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="2a9de-111">**Twilio Voice** permite que sus aplicaciones realicen y reciban llamadas.</span><span class="sxs-lookup"><span data-stu-id="2a9de-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="2a9de-112">**Twilio SMS** permite que sus aplicaciones envíen y reciban mensajes SMS.</span><span class="sxs-lookup"><span data-stu-id="2a9de-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="2a9de-113">**Twilio Client** permite que sus aplicaciones habiliten la comunicación por voz a través de conexiones existentes a Internet, incluidas las conexiones móviles.</span><span class="sxs-lookup"><span data-stu-id="2a9de-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="2a9de-114"><a id="Pricing"></a>Precios de Twilio y ofertas especiales</span><span class="sxs-lookup"><span data-stu-id="2a9de-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="2a9de-115">Puede encontrar información sobre los precios de Twilio en [Precios de Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="2a9de-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="2a9de-116">Los clientes de Azure reciben una [oferta especial][special_offer]: 1000 mensajes o 1000 minutos para llamar totalmente gratuitos.</span><span class="sxs-lookup"><span data-stu-id="2a9de-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="2a9de-117">Para registrarse y obtener esta oferta o para recibir más información, visite [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="2a9de-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="2a9de-118"><a id="Concepts"></a>Conceptos</span><span class="sxs-lookup"><span data-stu-id="2a9de-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="2a9de-119">La API de Twilio es una API de RESTful que proporciona funciones de voz y SMS para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2a9de-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="2a9de-120">Las bibliotecas de cliente están disponibles en varios lenguajes; para ver una lista, consulte las [bibliotecas de API de Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="2a9de-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="2a9de-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="2a9de-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="2a9de-122">TwiML es un conjunto de instrucciones basadas en XML que informan a Twilio sobre cómo procesar una llamada o un SMS.</span><span class="sxs-lookup"><span data-stu-id="2a9de-122">TwiML is a set of XML-based instructions that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="2a9de-123">Como ejemplo, el siguiente TwiML convierte el texto **Hello World** en voz.</span><span class="sxs-lookup"><span data-stu-id="2a9de-123">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="2a9de-124">Todos los documentos de TwinML disponen de `<Response>` como elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="2a9de-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="2a9de-125">A partir de ahí, puede usar los verbos de Twilio para definir el comportamiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2a9de-125">From there, you use Twilio Verbs to define the behavior of your application.</span></span>

### <span data-ttu-id="2a9de-126"><a id="Verbs"></a>Verbos de TwiML</span><span class="sxs-lookup"><span data-stu-id="2a9de-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="2a9de-127">Los verbos de Twilio son etiquetas XML que indican a Twilio qué **hacer**.</span><span class="sxs-lookup"><span data-stu-id="2a9de-127">Twilio Verbs are XML tags that tell Twilio what to **do**.</span></span> <span data-ttu-id="2a9de-128">Por ejemplo, el verbo **&lt;Say&gt;** indica a Twilio que se envíe de forma audible un mensaje en una llamada.</span><span class="sxs-lookup"><span data-stu-id="2a9de-128">For example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span> 

<span data-ttu-id="2a9de-129">A continuación se presenta una lista de verbos de Twilio.</span><span class="sxs-lookup"><span data-stu-id="2a9de-129">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="2a9de-130">**&lt;Dial&gt;**: conecta la persona que llama con otro teléfono.</span><span class="sxs-lookup"><span data-stu-id="2a9de-130">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="2a9de-131">**&lt;Gather&gt;**: recopila los dígitos numéricos que se introdujeron en el teclado del teléfono.</span><span class="sxs-lookup"><span data-stu-id="2a9de-131">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="2a9de-132">**&lt;Hangup&gt;**: finaliza una llamada.</span><span class="sxs-lookup"><span data-stu-id="2a9de-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="2a9de-133">**&lt;Play&gt;**: reproduce un archivo de audio.</span><span class="sxs-lookup"><span data-stu-id="2a9de-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="2a9de-134">**&lt;Pause&gt;**: espera en silencio una cantidad de segundos específica.</span><span class="sxs-lookup"><span data-stu-id="2a9de-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="2a9de-135">**&lt;Record&gt;**: graba la voz de la persona que llama y devuelve una dirección URL de un archivo que contiene la grabación.</span><span class="sxs-lookup"><span data-stu-id="2a9de-135">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="2a9de-136">**&lt;Redirect&gt;**: transfiere el control de una llamada o SMS al TwiML en una URL diferente.</span><span class="sxs-lookup"><span data-stu-id="2a9de-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="2a9de-137">**&lt;Reject&gt;**: rechaza una llamada entrante a su número de Twilio sin cobrarle.</span><span class="sxs-lookup"><span data-stu-id="2a9de-137">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="2a9de-138">**&lt;Say&gt;**: convierte texto en voz para hacer una llamada.</span><span class="sxs-lookup"><span data-stu-id="2a9de-138">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="2a9de-139">**&lt;Sms&gt;**: envía un mensaje SMS.</span><span class="sxs-lookup"><span data-stu-id="2a9de-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="2a9de-140">Para obtener más información sobre los verbos de Twilio, sus atributos y TwiML, consulte [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="2a9de-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="2a9de-141">Para obtener información adicional sobre la API de Twilio, consulte la [API de Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="2a9de-141">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="2a9de-142"><a id="CreateAccount"></a>Creación de una cuenta de Twilio</span><span class="sxs-lookup"><span data-stu-id="2a9de-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="2a9de-143">Cuando esté preparado para obtener una cuenta de Twilio, regístrese en la página de [evaluación de Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="2a9de-143">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="2a9de-144">Puede empezar con una cuenta gratuita y, posteriormente, actualizarla.</span><span class="sxs-lookup"><span data-stu-id="2a9de-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="2a9de-145">Cuando registre la cuenta Twilio, obtendrá un número de teléfono gratuito para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2a9de-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="2a9de-146">Recibirá también un SID de cuenta y un token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="2a9de-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="2a9de-147">Necesitará ambos para realizar llamadas a la API de Twilio.</span><span class="sxs-lookup"><span data-stu-id="2a9de-147">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="2a9de-148">Para evitar el acceso no autorizado a su cuenta, mantenga protegido el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="2a9de-148">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="2a9de-149">Puede ver el identificador de seguridad de cuenta y el token de autenticación en la [página de la cuenta de Twilio][twilio_account], en los campos etiquetados como **ACCOUNT SID** (Id. de seguridad de cuenta) y **AUTH TOKEN** (Token de autenticación), respectivamente.</span><span class="sxs-lookup"><span data-stu-id="2a9de-149">Your account SID and auth token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="2a9de-150"><a id="VerifyPhoneNumbers"></a>Comprobación de números de teléfono</span><span class="sxs-lookup"><span data-stu-id="2a9de-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="2a9de-151">Además del número proporcionado por Twilio, también puede comprobar los números que controle (es decir, el número de teléfono de casa o del móvil) para usarlos en las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2a9de-151">In addition to the number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="2a9de-152">Para información sobre cómo comprobar un número de teléfono, consulte el artículo sobre la [administración de números][verify_phone].</span><span class="sxs-lookup"><span data-stu-id="2a9de-152">For information on how to verify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="2a9de-153"><a id="create_app"></a>Creación de una aplicación de Ruby</span><span class="sxs-lookup"><span data-stu-id="2a9de-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="2a9de-154">Una aplicación de Ruby que usa el servicio Twilio y que se ejecuta en Azure no es distinta a otra aplicación Ruby que use el servicio Twilio.</span><span class="sxs-lookup"><span data-stu-id="2a9de-154">A Ruby application that uses the Twilio service and is running in Azure is no different than any other Ruby application that uses the Twilio service.</span></span> <span data-ttu-id="2a9de-155">A pesar de que los servicios Twilio están basados en RESTful y pueden llamarse desde Ruby de varias formas, este artículo se centrará en cómo usar los servicios Twilio con la [biblioteca auxiliar de Twilio para Ruby][twilio_ruby] (en inglés).</span><span class="sxs-lookup"><span data-stu-id="2a9de-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how to use Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="2a9de-156">Primero, deberá [configurar una nueva máquina virtual Linux de Azure][azure_vm_setup] que haga de host para su nueva aplicación web Ruby.</span><span class="sxs-lookup"><span data-stu-id="2a9de-156">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Ruby web application.</span></span> <span data-ttu-id="2a9de-157">Ignore los pasos relacionados con la creación de una aplicación Rails, solo configure la VM.</span><span class="sxs-lookup"><span data-stu-id="2a9de-157">Ignore the steps involving the creation of a Rails app, just set-up the VM.</span></span> <span data-ttu-id="2a9de-158">Asegúrese de crear un extremo con un puerto externo de 80 y un puerto interno de 5000.</span><span class="sxs-lookup"><span data-stu-id="2a9de-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="2a9de-159">En los ejemplos siguientes, usaremos [Sinatra][sinatra], un marco web para Ruby muy sencillo.</span><span class="sxs-lookup"><span data-stu-id="2a9de-159">In the examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="2a9de-160">Sin embargo, puede usar verdaderamente la biblioteca auxiliar de Twilio para Ruby con otro marco web, incluido Ruby en Rails.</span><span class="sxs-lookup"><span data-stu-id="2a9de-160">But you can certainly use the Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="2a9de-161">SSH en la nueva VM y cree un directorio para la nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="2a9de-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="2a9de-162">Dentro del directorio, cree un archivo llamado Gemfile y copie el siguiente código en él:</span><span class="sxs-lookup"><span data-stu-id="2a9de-162">Inside that directory, create a file called Gemfile and copy the following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="2a9de-163">En la línea de comandos, ejecute `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="2a9de-163">On the command line run `bundle install`.</span></span> <span data-ttu-id="2a9de-164">De esta forma se instalarán las dependencias anteriores.</span><span class="sxs-lookup"><span data-stu-id="2a9de-164">This will install the dependencies above.</span></span> <span data-ttu-id="2a9de-165">A continuación, cree un archivo que se llame `web.rb`.</span><span class="sxs-lookup"><span data-stu-id="2a9de-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="2a9de-166">Será donde se encuentre el código para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="2a9de-166">This will be where the code for your web app lives.</span></span> <span data-ttu-id="2a9de-167">Pegue el siguiente código en él:</span><span class="sxs-lookup"><span data-stu-id="2a9de-167">Paste the following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="2a9de-168">En este momento, debe poder ejecutar el comando `ruby web.rb -p 5000`.</span><span class="sxs-lookup"><span data-stu-id="2a9de-168">At this point you should be able the run the command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="2a9de-169">De esta forma, podrá ejecutar un servidor web pequeño en el puerto 5000.</span><span class="sxs-lookup"><span data-stu-id="2a9de-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="2a9de-170">Debe poder buscar en esta aplicación en el explorador visitando la dirección URL que configure para la VM de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a9de-170">You should be able to browse to this app in your browser by visiting the URL you set-up for your Azure VM.</span></span> <span data-ttu-id="2a9de-171">Una vez que pueda obtener acceso a la aplicación web en el explorador, podrá comenzar a generar una aplicación Twilio.</span><span class="sxs-lookup"><span data-stu-id="2a9de-171">Once you can reach your web app in the browser, you're ready to start building a Twilio app.</span></span>

## <span data-ttu-id="2a9de-172"><a id="configure_app"></a>Configuración de su aplicación para usar Twilio</span><span class="sxs-lookup"><span data-stu-id="2a9de-172"><a id="configure_app"></a>Configure Your Application to Use Twilio</span></span>
<span data-ttu-id="2a9de-173">Puede configurar la aplicación web para que use la biblioteca de Twilio actualizando su `Gemfile` para que incluya esta línea:</span><span class="sxs-lookup"><span data-stu-id="2a9de-173">You can configure your web app to use the Twilio library by updating your `Gemfile` to include this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="2a9de-174">En la línea de comandos ejecute `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="2a9de-174">On the command line, run `bundle install`.</span></span> <span data-ttu-id="2a9de-175">Ahora abra `web.rb` e incluya esta línea en la parte superior:</span><span class="sxs-lookup"><span data-stu-id="2a9de-175">Now open `web.rb` and including this line at the top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="2a9de-176">Ahora tiene todo configurado para usar la biblioteca auxiliar de Twilio para Ruby en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="2a9de-176">You're now all set to use the Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="2a9de-177"><a id="howto_make_call"></a>Realización de una llamada saliente</span><span class="sxs-lookup"><span data-stu-id="2a9de-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="2a9de-178">A continuación se muestra cómo realizar una llamada saliente.</span><span class="sxs-lookup"><span data-stu-id="2a9de-178">The following shows how to make an outgoing call.</span></span> <span data-ttu-id="2a9de-179">Entre los conceptos clave se incluyen el uso de la biblioteca auxiliar de Twilio para Ruby para realizar llamadas de la API REST y la representación de TwiML.</span><span class="sxs-lookup"><span data-stu-id="2a9de-179">Key concepts include using the Twilio helper library for Ruby to make REST API calls and rendering TwiML.</span></span> <span data-ttu-id="2a9de-180">Sustituya los valores de los números de teléfono **From** (De) y **To** (Para) y asegúrese de comprobar el número de teléfono **From** (De) de su cuenta de Twilio antes de ejecutar el código.</span><span class="sxs-lookup"><span data-stu-id="2a9de-180">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

<span data-ttu-id="2a9de-181">Agregue esta función a `web.md`:</span><span class="sxs-lookup"><span data-stu-id="2a9de-181">Add this function to `web.md`:</span></span>

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # The number of the phone initiating the the call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # The number of the phone receiving call.
    to = "NNNNNNNNNNN";

    # Use the Twilio-provided site for the TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create the call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make the call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

<span data-ttu-id="2a9de-182">Si abre `http://yourdomain.cloudapp.net/make_call` en un explorador, activará la llamada en la API de Twilio para realizar la llamada telefónica.</span><span class="sxs-lookup"><span data-stu-id="2a9de-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger the call to the Twilio API to make the phone call.</span></span> <span data-ttu-id="2a9de-183">Los dos primeros parámetros en `client.account.calls.create` no necesitan mucha explicación: el número del que procede la llamada es `from` y el número al que se llama es `to`.</span><span class="sxs-lookup"><span data-stu-id="2a9de-183">The first two parameters in `client.account.calls.create` are fairly self-explanatory: the number the call is `from` and the number the call is `to`.</span></span> 

<span data-ttu-id="2a9de-184">El tercer parámetro (`url`) es la dirección URL que Twilio solicita para obtener instrucciones sobre qué hacer cuando la llamada se conecta.</span><span class="sxs-lookup"><span data-stu-id="2a9de-184">The third parameter (`url`) is the URL that Twilio requests to get instructions on what to do once the call is connected.</span></span> <span data-ttu-id="2a9de-185">En este caso, configuramos una dirección URL (`http://yourdomain.cloudapp.net`) que devuelve un documento TwiML simple y usa el verbo `<Say>` para pasar texto a voz y decir "Hello Monkey" a la persona que recibe la llamada.</span><span class="sxs-lookup"><span data-stu-id="2a9de-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses the `<Say>` verb to do some text-to-speech and say "Hello Monkey" to the person recieving the call.</span></span>

## <span data-ttu-id="2a9de-186"><a id="howto_recieve_sms"></a>Procedimientos: Recepción de un mensaje SMS</span><span class="sxs-lookup"><span data-stu-id="2a9de-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="2a9de-187">En el ejemplo anterior, iniciamos una llamada telefónica **saliente** .</span><span class="sxs-lookup"><span data-stu-id="2a9de-187">In the previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="2a9de-188">Esta vez, usaremos un número de teléfono que proporcionó Twilio durante el registro para procesar un mensaje SMS **entrante** .</span><span class="sxs-lookup"><span data-stu-id="2a9de-188">This time, let's use the phone number that Twilio gave us during sign-up to process an **incoming** SMS message.</span></span>

<span data-ttu-id="2a9de-189">Primero, inicie sesión en su [panel de Twilio][twilio_account].</span><span class="sxs-lookup"><span data-stu-id="2a9de-189">First, log-in to your [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="2a9de-190">Haga clic en "Numbers" en el panel de navegación superior y haga clic en el número de Twilio proporcionado.</span><span class="sxs-lookup"><span data-stu-id="2a9de-190">Click on "Numbers" in the top nav and then click on the Twilio number you were provided.</span></span> <span data-ttu-id="2a9de-191">Ahora verá las dos direcciones URL que puede configurar.</span><span class="sxs-lookup"><span data-stu-id="2a9de-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="2a9de-192">Una dirección URL de solicitud de voz y una dirección de URL de solicitud de SMS.</span><span class="sxs-lookup"><span data-stu-id="2a9de-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="2a9de-193">Estas son las direcciones URL a las que llama Twilio cuando se realiza una llamada telefónica o se envía un SMS a su número.</span><span class="sxs-lookup"><span data-stu-id="2a9de-193">These are the URLs that Twilio calls whenever a phone call is made or an SMS is sent to your number.</span></span> <span data-ttu-id="2a9de-194">Las direcciones URL también se conocen como "enlaces web".</span><span class="sxs-lookup"><span data-stu-id="2a9de-194">The URLs are also known as "web hooks".</span></span>

<span data-ttu-id="2a9de-195">Nos gustaría procesar los mensajes SMS entrantes, así que vamos a actualizar la URL a `http://yourdomain.cloudapp.net/sms_url`.</span><span class="sxs-lookup"><span data-stu-id="2a9de-195">We would like to process incoming SMS messages, so let's update the URL to `http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="2a9de-196">Continúe y haga clic en la opción para guardar los cambios en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="2a9de-196">Go ahead and click Save Changes at the bottom of the page.</span></span> <span data-ttu-id="2a9de-197">A continuación vuelva a `web.rb` y programaremos nuestra aplicación para controlar esto:</span><span class="sxs-lookup"><span data-stu-id="2a9de-197">Now, back in `web.rb` let's program our application to handle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for the ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="2a9de-198">Después de realizar el cambio, asegúrese de reiniciar la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="2a9de-198">After making the change, make sure to re-start your web app.</span></span> <span data-ttu-id="2a9de-199">Ahora, use el teléfono para enviar un SMS al número de Twilio.</span><span class="sxs-lookup"><span data-stu-id="2a9de-199">Now, take out your phone and send an SMS to your Twilio number.</span></span> <span data-ttu-id="2a9de-200">Recibirá pronto una respuesta al SMS que le dará las gracias por hacer ping,</span><span class="sxs-lookup"><span data-stu-id="2a9de-200">You should promptly get an SMS response that says "Hey, thanks for the ping!</span></span> <span data-ttu-id="2a9de-201">y le indicará que Twilio y Azure son perfectos.</span><span class="sxs-lookup"><span data-stu-id="2a9de-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="2a9de-202"><a id="additional_services"></a>Procedimientos: Uso de servicios Twilio adicionales</span><span class="sxs-lookup"><span data-stu-id="2a9de-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="2a9de-203">Además de los ejemplos aquí mostrados, Twilio ofrece API basadas en web que puede utilizar para aprovechar las funciones adicionales de Twilio desde su aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a9de-203">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="2a9de-204">Para obtener los detalles completos, vea la [Documentación de la API de Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="2a9de-204">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="2a9de-205"><a id="NextSteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2a9de-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="2a9de-206">Ahora que conoce los fundamentos del servicio Twilio, siga estos vínculos para obtener más información:</span><span class="sxs-lookup"><span data-stu-id="2a9de-206">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="2a9de-207">[Directrices de seguridad de Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="2a9de-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="2a9de-208">[Procedimientos y código de ejemplo de Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="2a9de-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="2a9de-209">[Tutoriales de inicio rápido de Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="2a9de-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="2a9de-210">[Twilio en GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="2a9de-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="2a9de-211">[Contactar con el servicio técnico de Twilio][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="2a9de-211">[Talk to Twilio Support][twilio_support]</span></span>

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
