---
title: Uso de Twilio para voz y SMS (Python) | Microsoft Docs
description: "Aprenda a realizar llamadas telefónicas y a enviar mensajes SMS con el servicio de la API de Twilio en Azure. Ejemplos de código escritos en Python."
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
ms.openlocfilehash: f4a02bb7a7c46e7a0e3c75b870c522eae8294339
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-python"></a><span data-ttu-id="2b251-104">Usar Twilio para capacidades de voz y SMS en Python</span><span class="sxs-lookup"><span data-stu-id="2b251-104">How to Use Twilio for Voice and SMS Capabilities in Python</span></span>
<span data-ttu-id="2b251-105">Esta guía describe cómo realizar tareas comunes de programación con el servicio de API de Twilio en Azure.</span><span class="sxs-lookup"><span data-stu-id="2b251-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="2b251-106">Entre los escenarios descritos se incluyen realizar una llamada telefónica y enviar un mensaje de servicio de mensajes cortos (SMS).</span><span class="sxs-lookup"><span data-stu-id="2b251-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="2b251-107">Para obtener más información sobre Twilio y el uso de voz y mensajes SMS en sus aplicaciones, consulte la sección [Pasos siguientes](#NextSteps) .</span><span class="sxs-lookup"><span data-stu-id="2b251-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="2b251-108"><a id="WhatIs"></a>¿Qué es Twilio?</span><span class="sxs-lookup"><span data-stu-id="2b251-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="2b251-109">Twilio está potenciando el futuro de las comunicaciones empresariales, al permitir que los desarrolladores inserten voz, VoIP y mensajería en las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2b251-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="2b251-110">Pueden virtualizar toda la infraestructura necesaria en un entorno global basado en la nube y exponerlo a través de la plataforma API de comunicaciones de Twilio.</span><span class="sxs-lookup"><span data-stu-id="2b251-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="2b251-111">Las aplicaciones son sencillas de compilar y pueden escalarse.</span><span class="sxs-lookup"><span data-stu-id="2b251-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="2b251-112">Disfrute de la flexibilidad de pagar por lo que utiliza y aproveche la confiabilidad de la nube.</span><span class="sxs-lookup"><span data-stu-id="2b251-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="2b251-113">**Twilio Voice** permite que sus aplicaciones realicen y reciban llamadas.</span><span class="sxs-lookup"><span data-stu-id="2b251-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span>
<span data-ttu-id="2b251-114">**Twilio SMS** permite que su aplicación envíe y reciba mensajes de texto.</span><span class="sxs-lookup"><span data-stu-id="2b251-114">**Twilio SMS** enables your application to send and receive text messages.</span></span>
<span data-ttu-id="2b251-115">**Twilio Client** permite realizar llamadas VoIP desde cualquier teléfono, tableta o explorador, y es compatible con WebRTC.</span><span class="sxs-lookup"><span data-stu-id="2b251-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="2b251-116"><a id="Pricing"></a>Precios de Twilio y ofertas especiales</span><span class="sxs-lookup"><span data-stu-id="2b251-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="2b251-117">Los clientes de Azure reciben una [oferta especial][special_offer] de 10 $ de crédito de Twilio cuando se actualiza la cuenta de Twilio.</span><span class="sxs-lookup"><span data-stu-id="2b251-117">Azure customers receive a [special offer][special_offer] $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="2b251-118">Este crédito Twilio se puede aplicar a cualquier uso de Twilio (10 $ de crédito equivalen al envío de aproximadamente 1.000 mensajes SMS o recibir hasta 1.000 minutos de voz entrante, según la ubicación del número de teléfono y el destino del mensaje o de la llamada).</span><span class="sxs-lookup"><span data-stu-id="2b251-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="2b251-119">Canjee este [crédito de Twilio][special_offer] y comience.</span><span class="sxs-lookup"><span data-stu-id="2b251-119">Redeem this [Twilio credit][special_offer] and get started.</span></span>

<span data-ttu-id="2b251-120">Twilio es un servicio de pago por uso.</span><span class="sxs-lookup"><span data-stu-id="2b251-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="2b251-121">No hay comisiones establecidas y puede cerrar su cuenta en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="2b251-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="2b251-122">Puede encontrar más detalles en [Precios de Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="2b251-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="2b251-123"><a id="Concepts"></a>Conceptos</span><span class="sxs-lookup"><span data-stu-id="2b251-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="2b251-124">La API de Twilio es una API de RESTful que proporciona funciones de voz y SMS para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2b251-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="2b251-125">Las bibliotecas de cliente están disponibles en varios lenguajes; para ver una lista, consulte las [bibliotecas de API de Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="2b251-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="2b251-126">Aspectos fundamentales de la API de Twilio son los verbos de Twilio y el lenguaje de marcado de Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="2b251-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="2b251-127"><a id="Verbs"></a>Verbos de Twilio</span><span class="sxs-lookup"><span data-stu-id="2b251-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="2b251-128">La API usa dos verbos de Twilio; por ejemplo, el verbo **&lt;Say&gt;** indica a Twilio que entregue de manera audible un mensaje en una llamada.</span><span class="sxs-lookup"><span data-stu-id="2b251-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="2b251-129">A continuación se presenta una lista de verbos de Twilio.</span><span class="sxs-lookup"><span data-stu-id="2b251-129">The following is a list of Twilio verbs.</span></span> <span data-ttu-id="2b251-130">Obtenga información sobre los demás verbos y capacidades a través de la [documentación del lenguaje de marcado de Twilio][twiml].</span><span class="sxs-lookup"><span data-stu-id="2b251-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation][twiml].</span></span>

* <span data-ttu-id="2b251-131">**&lt;Dial&gt;**: conecta la persona que llama con otro teléfono.</span><span class="sxs-lookup"><span data-stu-id="2b251-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="2b251-132">**&lt;Gather&gt;**: recopila los dígitos numéricos que se introdujeron en el teclado del teléfono.</span><span class="sxs-lookup"><span data-stu-id="2b251-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="2b251-133">**&lt;Hangup&gt;**: finaliza una llamada.</span><span class="sxs-lookup"><span data-stu-id="2b251-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="2b251-134">**&lt;Pause&gt;**: espera en silencio una cantidad de segundos específica.</span><span class="sxs-lookup"><span data-stu-id="2b251-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="2b251-135">**&lt;Play&gt;**: reproduce un archivo de audio.</span><span class="sxs-lookup"><span data-stu-id="2b251-135">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="2b251-136">**&lt;Queue&gt;**: agregar a una cola de personas que llaman.</span><span class="sxs-lookup"><span data-stu-id="2b251-136">**&lt;Queue&gt;**: Add the to a queue of callers.</span></span>
* <span data-ttu-id="2b251-137">**&lt;Record&gt;**: graba la voz de la persona que llama y devuelve una dirección URL de un archivo que contiene la grabación.</span><span class="sxs-lookup"><span data-stu-id="2b251-137">**&lt;Record&gt;**: Records the voice of the caller and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="2b251-138">**&lt;Redirect&gt;**: transfiere el control de una llamada o SMS al TwiML en una URL diferente.</span><span class="sxs-lookup"><span data-stu-id="2b251-138">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="2b251-139">**&lt;Reject&gt;**: rechaza una llamada entrante al número de Twilio sin cobrarle.</span><span class="sxs-lookup"><span data-stu-id="2b251-139">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you.</span></span>
* <span data-ttu-id="2b251-140">**&lt;Say&gt;**: convierte texto en voz para hacer una llamada.</span><span class="sxs-lookup"><span data-stu-id="2b251-140">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="2b251-141">**&lt;Sms&gt;**: envía un mensaje SMS.</span><span class="sxs-lookup"><span data-stu-id="2b251-141">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="2b251-142"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="2b251-142"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="2b251-143">TwiML es un conjunto de instrucciones basadas en XML y en los verbos de Twilio que informan a Twilio sobre cómo procesar una llamada o un SMS.</span><span class="sxs-lookup"><span data-stu-id="2b251-143">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="2b251-144">Como ejemplo, el siguiente TwiML convierte el texto **Hello World** en voz.</span><span class="sxs-lookup"><span data-stu-id="2b251-144">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="2b251-145">Cuando su aplicación llama a la API de Twilio, uno de los parámetros de API es la URL que devuelve la respuesta de TwiML.</span><span class="sxs-lookup"><span data-stu-id="2b251-145">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="2b251-146">Con fines de desarrollo, puede usar las URL que ofrece Twilio para proporcionar las respuestas de TwiML que usaron sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2b251-146">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="2b251-147">También puede hospedar sus propias direcciones URL para producir las repuestas de TwiML. Otra opción es usar el objeto `TwiMLResponse`.</span><span class="sxs-lookup"><span data-stu-id="2b251-147">You could also host your own URLs to produce the TwiML responses, and another option is to use the `TwiMLResponse` object.</span></span>

<span data-ttu-id="2b251-148">Para obtener más información sobre los verbos de Twilio, sus atributos y TwiML, consulte [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="2b251-148">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="2b251-149">Para obtener información adicional sobre la API de Twilio, consulte la [API de Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="2b251-149">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="2b251-150"><a id="CreateAccount"></a>Creación de una cuenta de Twilio</span><span class="sxs-lookup"><span data-stu-id="2b251-150"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="2b251-151">Cuando esté preparado para obtener una cuenta de Twilio, regístrese en la [evaluación de Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="2b251-151">When you are ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="2b251-152">Puede empezar con una cuenta gratuita y, posteriormente, actualizarla.</span><span class="sxs-lookup"><span data-stu-id="2b251-152">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="2b251-153">Cuando se registre para obtener una cuenta de Twilio, recibirá un Id. de seguridad (SID) de la cuenta y un token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="2b251-153">When you sign up for a Twilio account, you receive an account SID and an authentication token.</span></span> <span data-ttu-id="2b251-154">Necesitará ambos para realizar llamadas a la API de Twilio.</span><span class="sxs-lookup"><span data-stu-id="2b251-154">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="2b251-155">Para evitar el acceso no autorizado a su cuenta, mantenga protegido el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="2b251-155">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="2b251-156">Puede ver el SID de la cuenta y el token de autenticación en la [Consola de Twilio][twilio_console], en los campos etiquetados como **ACCOUNT SID** y **AUTH TOKEN**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="2b251-156">Your account SID and authentication token are viewable in the [Twilio Console][twilio_console], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="2b251-157"><a id="create_app"></a>Crear una aplicación de Python</span><span class="sxs-lookup"><span data-stu-id="2b251-157"><a id="create_app"></a>Create a Python Application</span></span>
<span data-ttu-id="2b251-158">Una aplicación de Python que usa el servicio Twilio y que se ejecuta en Azure no es distinta a otra aplicación de Python que use el servicio Twilio.</span><span class="sxs-lookup"><span data-stu-id="2b251-158">A Python application that uses the Twilio service and is running in Azure is no different than any other Python application that uses the Twilio service.</span></span> <span data-ttu-id="2b251-159">Si bien los servicios Twilio se basan en REST y pueden llamarse desde Python de varias formas, este artículo se centrará en cómo usar los servicios Twilio con la [biblioteca de Twilio para Python de GitHub][twilio_python].</span><span class="sxs-lookup"><span data-stu-id="2b251-159">While Twilio services are REST-based and can be called from Python in several ways, this article will focus on how to use Twilio services with [Twilio library for Python from GitHub][twilio_python].</span></span> <span data-ttu-id="2b251-160">Para más información sobre el uso de la biblioteca de Twilio para Python, vea [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="2b251-160">For more information about using the Twilio library for Python, see [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="2b251-161">Primero, [configure una nueva máquina virtual Linux de Azure] [azure_vm_setup] para que actúe de host de su nueva aplicación web de Python.</span><span class="sxs-lookup"><span data-stu-id="2b251-161">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Python web application.</span></span> <span data-ttu-id="2b251-162">Una vez que la máquina virtual está en ejecución, tendrá que exponer la aplicación en un puerto público, como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="2b251-162">Once the Virtual Machine is running, you will need to expose your application on a public port as described below.</span></span>

### <a name="add-an-incoming-rule"></a><span data-ttu-id="2b251-163">Agregar una regla de entrada</span><span class="sxs-lookup"><span data-stu-id="2b251-163">Add An Incoming Rule</span></span>
  1. <span data-ttu-id="2b251-164">Vaya a la página [Grupo de seguridad de red] [azure_nsg].</span><span class="sxs-lookup"><span data-stu-id="2b251-164">Go to the [Network Security Group][azure_nsg] page.</span></span>
  2. <span data-ttu-id="2b251-165">Seleccione el Grupo de seguridad de red que se corresponde con su máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2b251-165">Select the Network Security Group that corresponds with your Virtual Machine.</span></span>
  3. <span data-ttu-id="2b251-166">Agregue una **Regla de salida** para el **puerto 80**.</span><span class="sxs-lookup"><span data-stu-id="2b251-166">Add and **Outgoing Rule** for **port 80**.</span></span> <span data-ttu-id="2b251-167">Asegúrese de permitir la entrada desde cualquier dirección.</span><span class="sxs-lookup"><span data-stu-id="2b251-167">Be sure to allow incoming from any address.</span></span>

### <a name="set-the-dns-name-label"></a><span data-ttu-id="2b251-168">Establecer la etiqueta de nombre DNS</span><span class="sxs-lookup"><span data-stu-id="2b251-168">Set the DNS Name Label</span></span>
  1. <span data-ttu-id="2b251-169">Vaya a la página [Direcciones IP públicas] [azure_ips].</span><span class="sxs-lookup"><span data-stu-id="2b251-169">Go to the [The Public IP Adresses][azure_ips] page.</span></span>
  2. <span data-ttu-id="2b251-170">Seleccione la dirección IP pública que se corresponde con la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2b251-170">Select the Public IP that correspends with your Virtual Machine.</span></span>
  3. <span data-ttu-id="2b251-171">Establezca la **Etiqueta de nombre DNS** en la sección **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="2b251-171">Set the **DNS Name Label** in the **Configuration** section.</span></span> <span data-ttu-id="2b251-172">En el caso de este ejemplo, tendrá un aspecto similar al siguiente: *la_etiqueta_ de_su_dominio*.centralus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="2b251-172">In the case of this example it will look something like this *your-domain-label*.centralus.cloudapp.azure.com</span></span>

<span data-ttu-id="2b251-173">Una vez que se pueda conectar a la máquina virtual a través de SSH, puede instalar el marco de trabajo web de su elección (los dos más conocidos en Python son [Flask](http://flask.pocoo.org/) y [Django](https://www.djangoproject.com)).</span><span class="sxs-lookup"><span data-stu-id="2b251-173">Once you are able to connect through SSH to the Virtual Machine you can install the Web Framework of your choice (the two most well known in Python being [Flask](http://flask.pocoo.org/) and [Django](https://www.djangoproject.com)).</span></span> <span data-ttu-id="2b251-174">Puede instalar cualquiera de ellos con el comando `pip install`.</span><span class="sxs-lookup"><span data-stu-id="2b251-174">You can install either of them just by running the `pip install` command.</span></span>

<span data-ttu-id="2b251-175">Tenga en cuenta que configuramos la máquina virtual para permitir el tráfico solo en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="2b251-175">Keep in mind that we configured the Virtual Machine to allow traffic only on port 80.</span></span> <span data-ttu-id="2b251-176">Por tanto, asegúrese de configurar la aplicación para que utilice este puerto.</span><span class="sxs-lookup"><span data-stu-id="2b251-176">So make sure to configure the application to use this port.</span></span>

## <span data-ttu-id="2b251-177"><a id="configure_app"></a>Configuración de la aplicación para usar bibliotecas de Twilio</span><span class="sxs-lookup"><span data-stu-id="2b251-177"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="2b251-178">Hay dos formas de configurar la aplicación para que use la biblioteca de Twilio para Python:</span><span class="sxs-lookup"><span data-stu-id="2b251-178">You can configure your application to use the Twilio library for Python in two ways:</span></span>

* <span data-ttu-id="2b251-179">Instale la biblioteca de Twilio para Python como paquete de PIP.</span><span class="sxs-lookup"><span data-stu-id="2b251-179">Install the Twilio library for Python as a Pip package.</span></span> <span data-ttu-id="2b251-180">Puede instalarse con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="2b251-180">It can be installed with the following commands:</span></span>
   
        $ pip install twilio

    <span data-ttu-id="2b251-181">O</span><span class="sxs-lookup"><span data-stu-id="2b251-181">-OR-</span></span>

* <span data-ttu-id="2b251-182">Descargue la biblioteca de Twilio para Python desde GitHub ([https://github.com/twilio/twilio-python][twilio_python]) e instálela de esta forma:</span><span class="sxs-lookup"><span data-stu-id="2b251-182">Download the Twilio library for Python from GitHub ([https://github.com/twilio/twilio-python][twilio_python]) and install it like this:</span></span>

        $ python setup.py install

<span data-ttu-id="2b251-183">Después de instalar la biblioteca de Twilio para Python, use `import` para importarla a los archivos de Python:</span><span class="sxs-lookup"><span data-stu-id="2b251-183">Once you have installed the Twilio library for Python, you can then `import` it in your Python files:</span></span>

        import twilio

<span data-ttu-id="2b251-184">Para más información, vea [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="2b251-184">For more information, see [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="2b251-185"><a id="howto_make_call"></a>Realización de una llamada saliente</span><span class="sxs-lookup"><span data-stu-id="2b251-185"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="2b251-186">A continuación se muestra cómo realizar una llamada saliente.</span><span class="sxs-lookup"><span data-stu-id="2b251-186">The following shows how to make an outgoing call.</span></span> <span data-ttu-id="2b251-187">Este código también utiliza un sitio que proporciona Twilio para devolver la respuesta de lenguaje de marcado de Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="2b251-187">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="2b251-188">Sustituya los valores de los números de teléfono **from_number** (De) y **to_number** (Para), y asegúrese de comprobar el número de teléfono **from_number** de su cuenta de Twilio antes de ejecutar el código.</span><span class="sxs-lookup"><span data-stu-id="2b251-188">Substitute your values for the **from_number** and **to_number** phone numbers, and ensure that you've verified the **from_number** phone number for your Twilio account before running the code.</span></span>

    from urllib.parse import urlencode

    # Import the Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # The number of the phone initiating the the call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # The number of the phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use the Twilio-provided site for the TwiML response.
    url = "http://twimlets.com/message?"

    # The phone message text.
    message = "Hello world."

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make the call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

<span data-ttu-id="2b251-189">Como se mencionó, este código usa el sitio proporcionado por Twilio para devolver la respuesta de TwiML.</span><span class="sxs-lookup"><span data-stu-id="2b251-189">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="2b251-190">A parte, también puede usar su propio sitio web para proporcionar la respuesta de TwiML; si desea obtener más información, consulte [Procedimientos: Suministro de respuestas de TwiML desde su propio sitio web](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="2b251-190">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="2b251-191"><a id="howto_send_sms"></a>Envío de un mensaje SMS</span><span class="sxs-lookup"><span data-stu-id="2b251-191"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="2b251-192">A continuación se muestra cómo enviar un mensaje SMS con la clase `TwilioRestClient`.</span><span class="sxs-lookup"><span data-stu-id="2b251-192">The following shows how to send an SMS message using the `TwilioRestClient` class.</span></span> <span data-ttu-id="2b251-193">El número **from_number** lo proporciona Twilio en las cuentas de evaluación para enviar mensajes SMS.</span><span class="sxs-lookup"><span data-stu-id="2b251-193">The **from_number** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="2b251-194">El número **to_number** se debe comprobar para la cuenta de Twilio antes de ejecutar el código.</span><span class="sxs-lookup"><span data-stu-id="2b251-194">The **to_number** number must be verified for your Twilio account before running the code.</span></span>

    # Import the Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send the SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <span data-ttu-id="2b251-195"><a id="howto_provide_twiml_responses"></a>Entrega de respuestas de TwiML desde su propio sitio web</span><span class="sxs-lookup"><span data-stu-id="2b251-195"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="2b251-196">Cuando la aplicación inicia una llamada a la API de Twilio, Twilio envía su solicitud a una URL que debe devolver una respuesta de TwiML.</span><span class="sxs-lookup"><span data-stu-id="2b251-196">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="2b251-197">El ejemplo anterior usa la dirección URL [http://twimlets.com/message][twimlet_message_url] proporcionada por Twilio.</span><span class="sxs-lookup"><span data-stu-id="2b251-197">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="2b251-198">(Aunque TwiML está diseñado para su uso por Twilio, puede verlo en el explorador.</span><span class="sxs-lookup"><span data-stu-id="2b251-198">(While TwiML is designed for use by Twilio, you can view it in your browser.</span></span> <span data-ttu-id="2b251-199">Por ejemplo, haga clic en [http://twimlets.com/message][twimlet_message_url] para ver un elemento `<Response>` vacío. Otro ejemplo: haga clic en [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] para ver un elemento `<Response>` que contiene un elemento `<Say>`).</span><span class="sxs-lookup"><span data-stu-id="2b251-199">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="2b251-200">En lugar de confiar en la URL que Twilio proporciona, puede crear su propio sitio que devuelve respuestas HTTP.</span><span class="sxs-lookup"><span data-stu-id="2b251-200">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="2b251-201">Puede crear el sitio en cualquier lenguaje que devuelva respuestas XML. En este tema se da por supuesto que usará Python para crear el TwiML.</span><span class="sxs-lookup"><span data-stu-id="2b251-201">You can create the site in any language that returns XML responses; this topic assumes you will be using Python to create the TwiML.</span></span>

<span data-ttu-id="2b251-202">Los siguientes ejemplos dan como resultado una respuesta de TwiML que dice **Hello World** en la llamada.</span><span class="sxs-lookup"><span data-stu-id="2b251-202">The following examples will output a TwiML response that says **Hello World** on the call.</span></span>

<span data-ttu-id="2b251-203">Con Flask:</span><span class="sxs-lookup"><span data-stu-id="2b251-203">With Flask:</span></span>

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

<span data-ttu-id="2b251-204">Con Django:</span><span class="sxs-lookup"><span data-stu-id="2b251-204">With Django:</span></span>

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

<span data-ttu-id="2b251-205">Como puede ver en el ejemplo anterior, la respuesta de TwiML es sencillamente un documento XML.</span><span class="sxs-lookup"><span data-stu-id="2b251-205">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="2b251-206">La biblioteca de Twilio para Python contiene clases que generarán TwiML de manera automática.</span><span class="sxs-lookup"><span data-stu-id="2b251-206">The Twilio library for Python contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="2b251-207">El ejemplo siguiente genera la respuesta equivalente como se mostró anteriormente, pero usa la clase `twiml` de la biblioteca de Twilio para Python:</span><span class="sxs-lookup"><span data-stu-id="2b251-207">The example below produces the equivalent response as shown above, but uses the `twiml` module in the Twilio library for Python:</span></span>

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

<span data-ttu-id="2b251-208">Para más información sobre TwiML, vea [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="2b251-208">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span>

<span data-ttu-id="2b251-209">Una vez configurada la aplicación de Python para proporcionar respuestas de TwiML, use la dirección URL de la aplicación como la dirección URL que se transmite al método `client.calls.create`.</span><span class="sxs-lookup"><span data-stu-id="2b251-209">Once you have your Python application set up to provide TwiML responses, use the URL of the application as the URL passed into the `client.calls.create`  method.</span></span> <span data-ttu-id="2b251-210">Por ejemplo, si tiene una aplicación web denominada **MyTwiML** implementada en un servicio hospedado de Azure, puede usar su dirección URL como webhook, como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2b251-210">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, you can use its url as webhook as shown in the following example:</span></span>

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make the call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <span data-ttu-id="2b251-211"><a id="AdditionalServices"></a>Procedimientos: Uso de servicios Twilio adicionales</span><span class="sxs-lookup"><span data-stu-id="2b251-211"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="2b251-212">Además de los ejemplos aquí mostrados, Twilio ofrece API basadas en web que puede utilizar para aprovechar las funciones adicionales de Twilio desde su aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="2b251-212">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="2b251-213">Para obtener los detalles completos, vea la [Documentación de la API de Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="2b251-213">For full details, see the [Twilio API documentation][twilio_api].</span></span>

## <span data-ttu-id="2b251-214"><a id="NextSteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2b251-214"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="2b251-215">Ahora que conoce los fundamentos del servicio Twilio, siga estos vínculos para obtener más información:</span><span class="sxs-lookup"><span data-stu-id="2b251-215">Now that you have learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="2b251-216">[Directrices de seguridad de Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="2b251-216">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="2b251-217">[Guías de procedimientos y código de ejemplo de Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="2b251-217">[Twilio HowTo Guides and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="2b251-218">[Tutoriales de inicio rápido de Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="2b251-218">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="2b251-219">[Twilio en GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="2b251-219">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="2b251-220">[Contactar con el servicio técnico de Twilio][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="2b251-220">[Talk to Twilio Support][twilio_support]</span></span>

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
