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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="89a43-104">Cómo tooUse Twilio para capacidades de SMS en Ruby y voz</span><span class="sxs-lookup"><span data-stu-id="89a43-104">How tooUse Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="89a43-105">Esta guía demuestra cómo tooperform las tareas de programación habituales con hello Twilio API de servicio en Azure.</span><span class="sxs-lookup"><span data-stu-id="89a43-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="89a43-106">escenarios de Hello descritos incluyen realizando una llamada telefónica y enviar un mensaje de servicio de mensajes cortos (SMS).</span><span class="sxs-lookup"><span data-stu-id="89a43-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="89a43-107">Para obtener más información sobre Twilio y el uso de voz y SMS en las aplicaciones, vea hello [pasos](#NextSteps) sección.</span><span class="sxs-lookup"><span data-stu-id="89a43-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="89a43-108"><a id="WhatIs"></a>¿Qué es Twilio?</span><span class="sxs-lookup"><span data-stu-id="89a43-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="89a43-109">Twilio es una API de servicio web de telefonía que permite utilizar los lenguajes web existentes y voz toobuild de conocimientos y las aplicaciones de SMS.</span><span class="sxs-lookup"><span data-stu-id="89a43-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="89a43-110">Twilio es un servicio de terceros (no una característica de Azure ni tampoco un producto de Microsoft).</span><span class="sxs-lookup"><span data-stu-id="89a43-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="89a43-111">**Voz Twilio** permite la toomake de las aplicaciones y recibir llamadas telefónicas.</span><span class="sxs-lookup"><span data-stu-id="89a43-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="89a43-112">**Twilio SMS** permite la toomake de las aplicaciones y recibir mensajes SMS.</span><span class="sxs-lookup"><span data-stu-id="89a43-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="89a43-113">**Cliente de Twilio** permite que las aplicaciones con las conexiones de Internet existentes, incluidas las conexiones móviles tooenable la comunicación de voz.</span><span class="sxs-lookup"><span data-stu-id="89a43-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="89a43-114"><a id="Pricing"></a>Precios de Twilio y ofertas especiales</span><span class="sxs-lookup"><span data-stu-id="89a43-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="89a43-115">Puede encontrar información sobre los precios de Twilio en [Precios de Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="89a43-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="89a43-116">Los clientes de Azure reciben una [oferta especial][special_offer]: 1000 mensajes o 1000 minutos para llamar totalmente gratuitos.</span><span class="sxs-lookup"><span data-stu-id="89a43-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="89a43-117">toosign hacia arriba para esta oferta u obtener más información, visite [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="89a43-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="89a43-118"><a id="Concepts"></a>Conceptos</span><span class="sxs-lookup"><span data-stu-id="89a43-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="89a43-119">Hola Twilio API es una API de REST que proporciona funciones SMS y voz para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="89a43-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="89a43-120">Las bibliotecas de cliente están disponibles en varios lenguajes; para ver una lista, consulte las [bibliotecas de API de Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="89a43-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="89a43-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="89a43-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="89a43-122">TwiML es un conjunto de instrucciones basado en XML que informan de Twilio de cómo tooprocess una llamada o SMS.</span><span class="sxs-lookup"><span data-stu-id="89a43-122">TwiML is a set of XML-based instructions that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="89a43-123">Por ejemplo, hello después TwiML convertiría texto hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="89a43-123">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="89a43-124">Todos los documentos de TwinML disponen de `<Response>` como elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="89a43-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="89a43-125">Desde allí, usar comportamiento de hello toodefine de verbos de Twilio de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="89a43-125">From there, you use Twilio Verbs toodefine hello behavior of your application.</span></span>

### <span data-ttu-id="89a43-126"><a id="Verbs"></a>Verbos de TwiML</span><span class="sxs-lookup"><span data-stu-id="89a43-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="89a43-127">Los verbos de Twilio son etiquetas XML que indican Twilio ¿qué es demasiado**es**.</span><span class="sxs-lookup"><span data-stu-id="89a43-127">Twilio Verbs are XML tags that tell Twilio what too**do**.</span></span> <span data-ttu-id="89a43-128">Por ejemplo, hello  **&lt;decir&gt;**  verbo indica Twilio tooaudibly entregar un mensaje en una llamada.</span><span class="sxs-lookup"><span data-stu-id="89a43-128">For example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span> 

<span data-ttu-id="89a43-129">Hola aquí te mostramos una lista de verbos de Twilio.</span><span class="sxs-lookup"><span data-stu-id="89a43-129">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="89a43-130">**&lt;Acceso telefónico&gt;**: conecta tooanother teléfono de hello llamador.</span><span class="sxs-lookup"><span data-stu-id="89a43-130">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="89a43-131">**&lt;Recopilar&gt;**: recopila los dígitos numéricos del teclado del teléfono de Hola.</span><span class="sxs-lookup"><span data-stu-id="89a43-131">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="89a43-132">**&lt;Hangup&gt;**: finaliza una llamada.</span><span class="sxs-lookup"><span data-stu-id="89a43-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="89a43-133">**&lt;Play&gt;**: reproduce un archivo de audio.</span><span class="sxs-lookup"><span data-stu-id="89a43-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="89a43-134">**&lt;Pause&gt;**: espera en silencio una cantidad de segundos específica.</span><span class="sxs-lookup"><span data-stu-id="89a43-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="89a43-135">**&lt;Registro&gt;**: registra la voz del llamador de Hola y devuelve una dirección URL de un archivo que contenga una grabación de Hola.</span><span class="sxs-lookup"><span data-stu-id="89a43-135">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="89a43-136">**&lt;Redirigir&gt;**: transfiere el control de una llamada o SMS toohello TwiML en una dirección URL diferente.</span><span class="sxs-lookup"><span data-stu-id="89a43-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="89a43-137">**&lt;Rechazar&gt;**: rechaza una entrada llame al número de Twilio de tooyour sin facturación</span><span class="sxs-lookup"><span data-stu-id="89a43-137">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="89a43-138">**&lt;Diga&gt;**: convierte texto toospeech que se realiza en una llamada.</span><span class="sxs-lookup"><span data-stu-id="89a43-138">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="89a43-139">**&lt;Sms&gt;**: envía un mensaje SMS.</span><span class="sxs-lookup"><span data-stu-id="89a43-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="89a43-140">Para obtener más información sobre los verbos de Twilio, sus atributos y TwiML, consulte [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="89a43-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="89a43-141">Para obtener información adicional acerca de hello Twilio API, consulte [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="89a43-141">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="89a43-142"><a id="CreateAccount"></a>Creación de una cuenta de Twilio</span><span class="sxs-lookup"><span data-stu-id="89a43-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="89a43-143">Cuando esté listo tooget una cuenta de Twilio, regístrese en [intente Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="89a43-143">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="89a43-144">Puede empezar con una cuenta gratuita y, posteriormente, actualizarla.</span><span class="sxs-lookup"><span data-stu-id="89a43-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="89a43-145">Cuando registre la cuenta Twilio, obtendrá un número de teléfono gratuito para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="89a43-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="89a43-146">Recibirá también un SID de cuenta y un token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="89a43-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="89a43-147">Ambos serán llamadas a la API de Twilio toomake necesarios.</span><span class="sxs-lookup"><span data-stu-id="89a43-147">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="89a43-148">tooprevent no autorizado obtenga acceso a cuenta tooyour, proteger el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="89a43-148">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="89a43-149">El SID de la cuenta y el token de autenticación están visibles en hello [página de la cuenta de Twilio][twilio_account], en campos con la etiqueta de Hola **SID de cuenta** y **el TOKEN de autenticación** , respectivamente.</span><span class="sxs-lookup"><span data-stu-id="89a43-149">Your account SID and auth token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="89a43-150"><a id="VerifyPhoneNumbers"></a>Comprobación de números de teléfono</span><span class="sxs-lookup"><span data-stu-id="89a43-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="89a43-151">En Twilio tendrá el número de toohello de adición, también puede comprobar los números de control (es decir, su número de teléfono celular o principal) para su uso en las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="89a43-151">In addition toohello number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="89a43-152">Para obtener información acerca de cómo tooverify un número de teléfono, consulte [administrar números][verify_phone].</span><span class="sxs-lookup"><span data-stu-id="89a43-152">For information on how tooverify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="89a43-153"><a id="create_app"></a>Creación de una aplicación de Ruby</span><span class="sxs-lookup"><span data-stu-id="89a43-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="89a43-154">Una aplicación Ruby que usa el servicio de Twilio de Hola y se ejecuta en Azure es similar a cualquier otra aplicación Ruby que usa el servicio de Twilio Hola.</span><span class="sxs-lookup"><span data-stu-id="89a43-154">A Ruby application that uses hello Twilio service and is running in Azure is no different than any other Ruby application that uses hello Twilio service.</span></span> <span data-ttu-id="89a43-155">Y Twilio servicios RESTful y pueden llamarse desde Ruby de varias maneras, este artículo se centrará en cómo services toouse Twilio con [biblioteca auxiliar de Twilio para Ruby][twilio_ruby].</span><span class="sxs-lookup"><span data-stu-id="89a43-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how toouse Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="89a43-156">En primer lugar, [instalación una nueva máquina virtual Linux de Azure] [ azure_vm_setup] tooact como un host para la nueva aplicación web Ruby.</span><span class="sxs-lookup"><span data-stu-id="89a43-156">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Ruby web application.</span></span> <span data-ttu-id="89a43-157">Omita los pasos de Hola que implican Hola creación de una aplicación de raíles Hola de instalación solo máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="89a43-157">Ignore hello steps involving hello creation of a Rails app, just set-up hello VM.</span></span> <span data-ttu-id="89a43-158">Asegúrese de crear un extremo con un puerto externo de 80 y un puerto interno de 5000.</span><span class="sxs-lookup"><span data-stu-id="89a43-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="89a43-159">En los siguientes ejemplos de hello, vamos a usar [Sinatra][sinatra], un marco web muy sencilla para Ruby.</span><span class="sxs-lookup"><span data-stu-id="89a43-159">In hello examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="89a43-160">Pero, por supuesto, puede usar biblioteca auxiliar de hello Twilio para Ruby con cualquier otro entorno de web, incluidos Ruby sobre raíles.</span><span class="sxs-lookup"><span data-stu-id="89a43-160">But you can certainly use hello Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="89a43-161">SSH en la nueva VM y cree un directorio para la nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="89a43-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="89a43-162">Dentro de ese directorio, cree un archivo denominado Gemfile y copie Hola siguiente código en él:</span><span class="sxs-lookup"><span data-stu-id="89a43-162">Inside that directory, create a file called Gemfile and copy hello following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="89a43-163">En la línea de comandos de hello ejecutar `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="89a43-163">On hello command line run `bundle install`.</span></span> <span data-ttu-id="89a43-164">Este modo se instalará las dependencias de hello anteriores.</span><span class="sxs-lookup"><span data-stu-id="89a43-164">This will install hello dependencies above.</span></span> <span data-ttu-id="89a43-165">A continuación, cree un archivo que se llame `web.rb`.</span><span class="sxs-lookup"><span data-stu-id="89a43-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="89a43-166">Se trata de donde vive código de hello de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="89a43-166">This will be where hello code for your web app lives.</span></span> <span data-ttu-id="89a43-167">Pegue Hola siguiente código en él:</span><span class="sxs-lookup"><span data-stu-id="89a43-167">Paste hello following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="89a43-168">En este momento debe ser comandos de Hola Hola capaz de ejecutar `ruby web.rb -p 5000`.</span><span class="sxs-lookup"><span data-stu-id="89a43-168">At this point you should be able hello run hello command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="89a43-169">De esta forma, podrá ejecutar un servidor web pequeño en el puerto 5000.</span><span class="sxs-lookup"><span data-stu-id="89a43-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="89a43-170">Debe ser capaz de toobrowse toothis aplicación en el explorador al visitar la dirección URL de hello instalación para la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="89a43-170">You should be able toobrowse toothis app in your browser by visiting hello URL you set-up for your Azure VM.</span></span> <span data-ttu-id="89a43-171">Una vez que se puede llegar a la aplicación web en el Explorador de hello, está listo toostart compilar una aplicación de Twilio.</span><span class="sxs-lookup"><span data-stu-id="89a43-171">Once you can reach your web app in hello browser, you're ready toostart building a Twilio app.</span></span>

## <span data-ttu-id="89a43-172"><a id="configure_app"></a>Configurar la aplicación tooUse Twilio</span><span class="sxs-lookup"><span data-stu-id="89a43-172"><a id="configure_app"></a>Configure Your Application tooUse Twilio</span></span>
<span data-ttu-id="89a43-173">Puede configurar la biblioteca de Twilio de web app toouse Hola actualizando su `Gemfile` tooinclude esta línea:</span><span class="sxs-lookup"><span data-stu-id="89a43-173">You can configure your web app toouse hello Twilio library by updating your `Gemfile` tooinclude this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="89a43-174">En la línea de comandos de hello, ejecute `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="89a43-174">On hello command line, run `bundle install`.</span></span> <span data-ttu-id="89a43-175">Ahora, abra `web.rb` esta línea en la parte superior de hello, incluido:</span><span class="sxs-lookup"><span data-stu-id="89a43-175">Now open `web.rb` and including this line at hello top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="89a43-176">Está ahora todos establecen biblioteca auxiliar de toouse hello Twilio para Ruby en su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="89a43-176">You're now all set toouse hello Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="89a43-177"><a id="howto_make_call"></a>Realización de una llamada saliente</span><span class="sxs-lookup"><span data-stu-id="89a43-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="89a43-178">Hola siguiente muestra cómo llamar una salida de toomake.</span><span class="sxs-lookup"><span data-stu-id="89a43-178">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="89a43-179">Conceptos clave que incluyen el uso de biblioteca auxiliar de hello Twilio para toomake Ruby llamadas API de REST y representación TwiML.</span><span class="sxs-lookup"><span data-stu-id="89a43-179">Key concepts include using hello Twilio helper library for Ruby toomake REST API calls and rendering TwiML.</span></span> <span data-ttu-id="89a43-180">Sustituya los valores de hello **de** y **a** los números de teléfono y asegúrese de comprobar hello **de** número de teléfono para el código de hello Twilio cuenta toorunning anterior.</span><span class="sxs-lookup"><span data-stu-id="89a43-180">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

<span data-ttu-id="89a43-181">Agregue esta función demasiado`web.md`:</span><span class="sxs-lookup"><span data-stu-id="89a43-181">Add this function too`web.md`:</span></span>

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

<span data-ttu-id="89a43-182">Si abrir arriba `http://yourdomain.cloudapp.net/make_call` en un explorador, que desencadenará Hola llamada toohello Twilio toomake Hola teléfono llamada a la API.</span><span class="sxs-lookup"><span data-stu-id="89a43-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger hello call toohello Twilio API toomake hello phone call.</span></span> <span data-ttu-id="89a43-183">Hola los dos primeros parámetros en `client.account.calls.create` son bastante autoexplicativo: Hola número Hola llamada es `from` y Hola número Hola llamada es `to`.</span><span class="sxs-lookup"><span data-stu-id="89a43-183">hello first two parameters in `client.account.calls.create` are fairly self-explanatory: hello number hello call is `from` and hello number hello call is `to`.</span></span> 

<span data-ttu-id="89a43-184">Hola tercer parámetro (`url`) es dirección URL de Hola que Twilio solicita instrucciones tooget en qué toodo una vez que está conectada la llamada Hola.</span><span class="sxs-lookup"><span data-stu-id="89a43-184">hello third parameter (`url`) is hello URL that Twilio requests tooget instructions on what toodo once hello call is connected.</span></span> <span data-ttu-id="89a43-185">En este caso es configurar una dirección URL (`http://yourdomain.cloudapp.net`) que devuelve un documento de TwiML simple y utiliza hello `<Say>` toodo verbo Hola algunas texto a voz y diga "Hello mono" toohello persona recibir llamadas.</span><span class="sxs-lookup"><span data-stu-id="89a43-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses hello `<Say>` verb toodo some text-to-speech and say "Hello Monkey" toohello person recieving hello call.</span></span>

## <span data-ttu-id="89a43-186"><a id="howto_recieve_sms"></a>Procedimientos: Recepción de un mensaje SMS</span><span class="sxs-lookup"><span data-stu-id="89a43-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="89a43-187">En el ejemplo anterior de Hola se inició un **saliente** llamada de teléfono.</span><span class="sxs-lookup"><span data-stu-id="89a43-187">In hello previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="89a43-188">Esta vez, vamos a usar el número de teléfono de hello Twilio nos proporcionaste durante el inicio de sesión tooprocess una **entrante** mensaje SMS.</span><span class="sxs-lookup"><span data-stu-id="89a43-188">This time, let's use hello phone number that Twilio gave us during sign-up tooprocess an **incoming** SMS message.</span></span>

<span data-ttu-id="89a43-189">En primer lugar, inicio de sesión tooyour [panel de Twilio][twilio_account].</span><span class="sxs-lookup"><span data-stu-id="89a43-189">First, log-in tooyour [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="89a43-190">Haga clic en "Números" en Hola de navegación superior y, a continuación, haga clic en hello número de Twilio que se proporcionaron.</span><span class="sxs-lookup"><span data-stu-id="89a43-190">Click on "Numbers" in hello top nav and then click on hello Twilio number you were provided.</span></span> <span data-ttu-id="89a43-191">Ahora verá las dos direcciones URL que puede configurar.</span><span class="sxs-lookup"><span data-stu-id="89a43-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="89a43-192">Una dirección URL de solicitud de voz y una dirección de URL de solicitud de SMS.</span><span class="sxs-lookup"><span data-stu-id="89a43-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="89a43-193">Se trata de direcciones URL de Hola que se realizan llamadas de Twilio cada vez que una llamada de teléfono o un SMS se envía el número de tooyour.</span><span class="sxs-lookup"><span data-stu-id="89a43-193">These are hello URLs that Twilio calls whenever a phone call is made or an SMS is sent tooyour number.</span></span> <span data-ttu-id="89a43-194">Hola las direcciones URL también se conocen como "enlaces web".</span><span class="sxs-lookup"><span data-stu-id="89a43-194">hello URLs are also known as "web hooks".</span></span>

<span data-ttu-id="89a43-195">Nos gustaría tooprocess los mensajes SMS entrantes, así que vamos a actualizar la dirección URL de hello demasiado`http://yourdomain.cloudapp.net/sms_url`.</span><span class="sxs-lookup"><span data-stu-id="89a43-195">We would like tooprocess incoming SMS messages, so let's update hello URL too`http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="89a43-196">Continúe y haga clic en Guardar cambios en parte inferior de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="89a43-196">Go ahead and click Save Changes at hello bottom of hello page.</span></span> <span data-ttu-id="89a43-197">Ahora, nuevo en `web.rb` vamos a programar esta nuestro toohandle de aplicación:</span><span class="sxs-lookup"><span data-stu-id="89a43-197">Now, back in `web.rb` let's program our application toohandle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="89a43-198">Después de realizar el cambio de hello, asegúrese de inicio de toore seguro de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="89a43-198">After making hello change, make sure toore-start your web app.</span></span> <span data-ttu-id="89a43-199">Ahora, retire el teléfono y enviar un número de Twilio de tooyour SMS.</span><span class="sxs-lookup"><span data-stu-id="89a43-199">Now, take out your phone and send an SMS tooyour Twilio number.</span></span> <span data-ttu-id="89a43-200">Debe obtener rápidamente una respuesta SMS que dice "¡Hola, gracias por ping Hola!</span><span class="sxs-lookup"><span data-stu-id="89a43-200">You should promptly get an SMS response that says "Hey, thanks for hello ping!</span></span> <span data-ttu-id="89a43-201">y le indicará que Twilio y Azure son perfectos.</span><span class="sxs-lookup"><span data-stu-id="89a43-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="89a43-202"><a id="additional_services"></a>Procedimientos: Uso de servicios Twilio adicionales</span><span class="sxs-lookup"><span data-stu-id="89a43-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="89a43-203">Además toohello ejemplos que se muestran aquí, que twilio ofrece API basadas en web que puede usar la funcionalidad adicional de Twilio de tooleverage desde su aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="89a43-203">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="89a43-204">Para obtener información detallada, vea hello [documentación de la API de Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="89a43-204">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="89a43-205"><a id="NextSteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="89a43-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="89a43-206">Ahora que ha aprendido conceptos básicos de Hola de hello Twilio servicio, siga estos toolearn de vínculos más:</span><span class="sxs-lookup"><span data-stu-id="89a43-206">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="89a43-207">[Directrices de seguridad de Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="89a43-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="89a43-208">[Procedimientos y código de ejemplo de Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="89a43-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="89a43-209">[Tutoriales de inicio rápido de Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="89a43-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="89a43-210">[Twilio en GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="89a43-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="89a43-211">[Hable tooTwilio soporte técnico][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="89a43-211">[Talk tooTwilio Support][twilio_support]</span></span>

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
