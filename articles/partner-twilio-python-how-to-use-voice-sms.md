---
title: aaaHow tooUse Twilio para voz y SMS (Python) | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomake una llamada de teléfono así como enviar un SMS de mensajes con el servicio de API de Twilio de hello en Azure. Ejemplos de código escritos en Python."
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
ms.openlocfilehash: 1f16a107d95c94589b8d61a0971c5b62d639c571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a><span data-ttu-id="6aaa0-104">Cómo tooUse Twilio para capacidades de SMS en Python y voz</span><span class="sxs-lookup"><span data-stu-id="6aaa0-104">How tooUse Twilio for Voice and SMS Capabilities in Python</span></span>
<span data-ttu-id="6aaa0-105">Esta guía demuestra cómo tooperform las tareas de programación habituales con hello Twilio API de servicio en Azure.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="6aaa0-106">escenarios de Hello descritos incluyen realizando una llamada telefónica y enviar un mensaje de servicio de mensajes cortos (SMS).</span><span class="sxs-lookup"><span data-stu-id="6aaa0-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="6aaa0-107">Para obtener más información sobre Twilio y el uso de voz y SMS en las aplicaciones, vea hello [pasos](#NextSteps) sección.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="6aaa0-108"><a id="WhatIs"></a>¿Qué es Twilio?</span><span class="sxs-lookup"><span data-stu-id="6aaa0-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="6aaa0-109">Twilio está activando Hola futuro de las comunicaciones empresariales, la habilitación de los desarrolladores tooembed voice, VoIP y en las aplicaciones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="6aaa0-110">Virtualizar toda la infraestructura necesarios en un entorno global, basada en la nube, exponerlo a través de la plataforma de hello API de comunicaciones de Twilio.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="6aaa0-111">Las aplicaciones son toobuild simple y escalable.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="6aaa0-112">Disfrute de la flexibilidad de pagar por lo que utiliza y aproveche la confiabilidad de la nube.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="6aaa0-113">**Voz Twilio** permite la toomake de las aplicaciones y recibir llamadas telefónicas.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span>
<span data-ttu-id="6aaa0-114">**Twilio SMS** permite que su aplicación toosend y recibir mensajes de texto.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span>
<span data-ttu-id="6aaa0-115">**Cliente de Twilio** permite llamadas de VoIP toomake desde cualquier teléfono, una tableta o un explorador y es compatible con WebRTC.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="6aaa0-116"><a id="Pricing"></a>Precios de Twilio y ofertas especiales</span><span class="sxs-lookup"><span data-stu-id="6aaa0-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="6aaa0-117">Los clientes de Azure reciben una [oferta especial][special_offer] de 10 $ de crédito de Twilio cuando se actualiza la cuenta de Twilio.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-117">Azure customers receive a [special offer][special_offer] $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="6aaa0-118">Este crédito Twilio puede ser aplicada tooany uso de Twilio (10 $ crédito equivalente toosending como máximo 1000 mensajes SMS o recibir una too1000 entrada minutos de voz, según la ubicación de Hola de su destino de número y el mensaje o la llamada de teléfono).</span><span class="sxs-lookup"><span data-stu-id="6aaa0-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="6aaa0-119">Canjee este [crédito de Twilio][special_offer] y comience.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-119">Redeem this [Twilio credit][special_offer] and get started.</span></span>

<span data-ttu-id="6aaa0-120">Twilio es un servicio de pago por uso.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="6aaa0-121">No hay comisiones establecidas y puede cerrar su cuenta en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="6aaa0-122">Puede encontrar más detalles en [Precios de Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="6aaa0-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="6aaa0-123"><a id="Concepts"></a>Conceptos</span><span class="sxs-lookup"><span data-stu-id="6aaa0-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="6aaa0-124">Hola Twilio API es una API de REST que proporciona funciones SMS y voz para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="6aaa0-125">Las bibliotecas de cliente están disponibles en varios lenguajes; para ver una lista, consulte las [bibliotecas de API de Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="6aaa0-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="6aaa0-126">Aspectos clave de hello Twilio API son verbos de Twilio y lenguaje de marcado de Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="6aaa0-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="6aaa0-127"><a id="Verbs"></a>Verbos de Twilio</span><span class="sxs-lookup"><span data-stu-id="6aaa0-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="6aaa0-128">Hola API hace que el uso de Twilio verbos; Por ejemplo, hello  **&lt;decir&gt;**  verbo indica Twilio tooaudibly entregar un mensaje en una llamada.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="6aaa0-129">Hola aquí te mostramos una lista de verbos de Twilio.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="6aaa0-130">Obtenga información acerca de Hola unos a otros verbos y capacidades a través de [documentación del lenguaje de marcado de Twilio][twiml].</span><span class="sxs-lookup"><span data-stu-id="6aaa0-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation][twiml].</span></span>

* <span data-ttu-id="6aaa0-131">**&lt;Acceso telefónico&gt;**: conecta tooanother teléfono de hello llamador.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="6aaa0-132">**&lt;Recopilar&gt;**: recopila los dígitos numéricos del teclado del teléfono de Hola.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="6aaa0-133">**&lt;Hangup&gt;**: finaliza una llamada.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="6aaa0-134">**&lt;Pause&gt;**: espera en silencio una cantidad de segundos específica.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="6aaa0-135">**&lt;Play&gt;**: reproduce un archivo de audio.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-135">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="6aaa0-136">**&lt;Cola&gt;**: agregar hello tooa cola de los llamadores.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-136">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="6aaa0-137">**&lt;Registro&gt;**: registra voz Hola del autor de llamada de Hola y devuelve una dirección URL de un archivo que contenga una grabación de Hola.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-137">**&lt;Record&gt;**: Records hello voice of hello caller and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="6aaa0-138">**&lt;Redirigir&gt;**: transfiere el control de una llamada o SMS toohello TwiML en una dirección URL diferente.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-138">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="6aaa0-139">**&lt;Rechazar&gt;**: rechaza una entrada llame al número de Twilio de tooyour sin facturación.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-139">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="6aaa0-140">**&lt;Diga&gt;**: convierte texto toospeech que se realiza en una llamada.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-140">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="6aaa0-141">**&lt;Sms&gt;**: envía un mensaje SMS.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-141">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="6aaa0-142"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="6aaa0-142"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="6aaa0-143">TwiML es un conjunto de instrucciones basado en XML en función de los verbos de Twilio de Hola que informan de Twilio de cómo tooprocess una llamada o SMS.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-143">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="6aaa0-144">Por ejemplo, hello después TwiML convertiría texto hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-144">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="6aaa0-145">Cuando la aplicación llama hello Twilio API, uno de los parámetros de la API de hello es dirección URL de Hola que devuelve la respuesta de TwiML Hola.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-145">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="6aaa0-146">Para fines de desarrollo, puede utilizar direcciones URL siempre Twilio tooprovide hello TwiML las respuestas que usan las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-146">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="6aaa0-147">También puede hospedar sus respuestas de las direcciones URL tooproduce hello TwiML y otra opción es hello toouse `TwiMLResponse` objeto.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-147">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello `TwiMLResponse` object.</span></span>

<span data-ttu-id="6aaa0-148">Para obtener más información sobre los verbos de Twilio, sus atributos y TwiML, consulte [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="6aaa0-148">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="6aaa0-149">Para obtener información adicional acerca de hello Twilio API, consulte [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="6aaa0-149">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="6aaa0-150"><a id="CreateAccount"></a>Creación de una cuenta de Twilio</span><span class="sxs-lookup"><span data-stu-id="6aaa0-150"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="6aaa0-151">Cuando esté listo tooget una cuenta de Twilio, regístrese en [intente Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="6aaa0-151">When you are ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="6aaa0-152">Puede empezar con una cuenta gratuita y, posteriormente, actualizarla.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-152">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="6aaa0-153">Cuando se registre para obtener una cuenta de Twilio, recibirá un Id. de seguridad (SID) de la cuenta y un token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-153">When you sign up for a Twilio account, you receive an account SID and an authentication token.</span></span> <span data-ttu-id="6aaa0-154">Ambos serán llamadas a la API de Twilio toomake necesarios.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-154">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="6aaa0-155">tooprevent no autorizado obtenga acceso a cuenta tooyour, proteger el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-155">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="6aaa0-156">El SID de la cuenta y el token de autenticación están visibles en hello [Twilio consola][twilio_console], en campos con la etiqueta de Hola **SID de cuenta** y **delTOKENdeautenticación**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-156">Your account SID and authentication token are viewable in hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="6aaa0-157"><a id="create_app"></a>Crear una aplicación de Python</span><span class="sxs-lookup"><span data-stu-id="6aaa0-157"><a id="create_app"></a>Create a Python Application</span></span>
<span data-ttu-id="6aaa0-158">Una aplicación de Python que usa el servicio de Twilio de Hola y se ejecuta en Azure es similar a cualquier otra aplicación de Python que usa el servicio de Twilio Hola.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-158">A Python application that uses hello Twilio service and is running in Azure is no different than any other Python application that uses hello Twilio service.</span></span> <span data-ttu-id="6aaa0-159">Mientras los servicios de Twilio están basadas en REST y pueden llamarse desde Python de varias maneras, este artículo se centrará en cómo services toouse Twilio con [Twilio biblioteca de Python desde GitHub][twilio_python].</span><span class="sxs-lookup"><span data-stu-id="6aaa0-159">While Twilio services are REST-based and can be called from Python in several ways, this article will focus on how toouse Twilio services with [Twilio library for Python from GitHub][twilio_python].</span></span> <span data-ttu-id="6aaa0-160">Para obtener más información acerca de cómo utilizar la biblioteca de Twilio de Hola para Python, consulte [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="6aaa0-160">For more information about using hello Twilio library for Python, see [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="6aaa0-161">En primer lugar, [instalación una nueva máquina virtual Linux de Azure] [azure_vm_setup] tooact como un host para la nueva aplicación web de Python.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-161">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Python web application.</span></span> <span data-ttu-id="6aaa0-162">Una vez hello Máquina Virtual está ejecutando, deberá tooexpose la aplicación en un puerto público tal y como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-162">Once hello Virtual Machine is running, you will need tooexpose your application on a public port as described below.</span></span>

### <a name="add-an-incoming-rule"></a><span data-ttu-id="6aaa0-163">Agregar una regla de entrada</span><span class="sxs-lookup"><span data-stu-id="6aaa0-163">Add An Incoming Rule</span></span>
  1. <span data-ttu-id="6aaa0-164">Vaya toohello [grupo de seguridad de red] [azure_nsg] página.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-164">Go toohello [Network Security Group][azure_nsg] page.</span></span>
  2. <span data-ttu-id="6aaa0-165">Hola seleccione grupo de seguridad de red que se corresponde con la máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-165">Select hello Network Security Group that corresponds with your Virtual Machine.</span></span>
  3. <span data-ttu-id="6aaa0-166">Agregue una **Regla de salida** para el **puerto 80**.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-166">Add and **Outgoing Rule** for **port 80**.</span></span> <span data-ttu-id="6aaa0-167">Ser seguro tooallow entrante procedente de cualquier dirección.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-167">Be sure tooallow incoming from any address.</span></span>

### <a name="set-hello-dns-name-label"></a><span data-ttu-id="6aaa0-168">Etiqueta de nombre DNS del conjunto Hola</span><span class="sxs-lookup"><span data-stu-id="6aaa0-168">Set hello DNS Name Label</span></span>
  1. <span data-ttu-id="6aaa0-169">Vaya toohello [Hola direcciones IP públicas] [azure_ips] página.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-169">Go toohello [hello Public IP Adresses][azure_ips] page.</span></span>
  2. <span data-ttu-id="6aaa0-170">Seleccione Hola IP pública que correspends con la máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-170">Select hello Public IP that correspends with your Virtual Machine.</span></span>
  3. <span data-ttu-id="6aaa0-171">Conjunto hello **etiqueta de nombre DNS** en hello **configuración** sección.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-171">Set hello **DNS Name Label** in hello **Configuration** section.</span></span> <span data-ttu-id="6aaa0-172">En caso de hello de este ejemplo tendrá un aspecto similar al siguiente *la etiqueta de dominio*. centralus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="6aaa0-172">In hello case of this example it will look something like this *your-domain-label*.centralus.cloudapp.azure.com</span></span>

<span data-ttu-id="6aaa0-173">Una vez que se puede tooconnect a través de SSH toohello Máquina Virtual puede instalar Hola marco Web de su elección (Hola dos más conocidas de Python que se va a [matraz](http://flask.pocoo.org/) y [Django](https://www.djangoproject.com)).</span><span class="sxs-lookup"><span data-stu-id="6aaa0-173">Once you are able tooconnect through SSH toohello Virtual Machine you can install hello Web Framework of your choice (hello two most well known in Python being [Flask](http://flask.pocoo.org/) and [Django](https://www.djangoproject.com)).</span></span> <span data-ttu-id="6aaa0-174">Puede instalar cualquiera de ellas simplemente mediante la ejecución de hello `pip install` comando.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-174">You can install either of them just by running hello `pip install` command.</span></span>

<span data-ttu-id="6aaa0-175">Tenga en cuenta que hemos configurado tooallow tráfico de hello máquinas virtuales únicamente en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-175">Keep in mind that we configured hello Virtual Machine tooallow traffic only on port 80.</span></span> <span data-ttu-id="6aaa0-176">Por lo que debe seguro tooconfigure Hola aplicación toouse este puerto.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-176">So make sure tooconfigure hello application toouse this port.</span></span>

## <span data-ttu-id="6aaa0-177"><a id="configure_app"></a>Configurar las bibliotecas de Twilio de tooUse de la aplicación</span><span class="sxs-lookup"><span data-stu-id="6aaa0-177"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="6aaa0-178">Puede configurar la biblioteca de Twilio de aplicación toouse Hola de Python de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="6aaa0-178">You can configure your application toouse hello Twilio library for Python in two ways:</span></span>

* <span data-ttu-id="6aaa0-179">Instalar biblioteca de Twilio de Hola para Python como un paquete de Pip.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-179">Install hello Twilio library for Python as a Pip package.</span></span> <span data-ttu-id="6aaa0-180">Puede instalarse con hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="6aaa0-180">It can be installed with hello following commands:</span></span>
   
        $ pip install twilio

    <span data-ttu-id="6aaa0-181">O</span><span class="sxs-lookup"><span data-stu-id="6aaa0-181">-OR-</span></span>

* <span data-ttu-id="6aaa0-182">Descargue la biblioteca de Twilio de Hola para Python desde GitHub ([https://github.com/twilio/twilio-python][twilio_python]) e instálelo similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="6aaa0-182">Download hello Twilio library for Python from GitHub ([https://github.com/twilio/twilio-python][twilio_python]) and install it like this:</span></span>

        $ python setup.py install

<span data-ttu-id="6aaa0-183">Una vez haya instalado la biblioteca de Twilio de Hola para Python, a continuación, puede `import` en los archivos de Python:</span><span class="sxs-lookup"><span data-stu-id="6aaa0-183">Once you have installed hello Twilio library for Python, you can then `import` it in your Python files:</span></span>

        import twilio

<span data-ttu-id="6aaa0-184">Para más información, vea [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="6aaa0-184">For more information, see [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="6aaa0-185"><a id="howto_make_call"></a>Realización de una llamada saliente</span><span class="sxs-lookup"><span data-stu-id="6aaa0-185"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="6aaa0-186">Hola siguiente muestra cómo llamar una salida de toomake.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-186">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="6aaa0-187">Este código también usa un Hola de tooreturn sitio proporcionado Twilio respuesta de lenguaje de marcado de Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="6aaa0-187">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="6aaa0-188">Sustituya los valores de hello **from_number** y **to_number** los números de teléfono y asegúrese de que ha comprobado hello **from_number** número de teléfono para su cuenta de Twilio antes de ejecutar código de hello.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-188">Substitute your values for hello **from_number** and **to_number** phone numbers, and ensure that you've verified hello **from_number** phone number for your Twilio account before running hello code.</span></span>

    from urllib.parse import urlencode

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # hello number of hello phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://twimlets.com/message?"

    # hello phone message text.
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

<span data-ttu-id="6aaa0-189">Como se ha mencionado, este código usa un Hola de tooreturn sitio proporcionado Twilio TwiML respuesta.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-189">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="6aaa0-190">En su lugar, podría utilizar su propio Hola de tooprovide sitio respuesta TwiML; Para obtener más información, consulte [cómo tooProvide TwiML respuestas desde su propio sitio Web de](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="6aaa0-190">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="6aaa0-191"><a id="howto_send_sms"></a>Envío de un mensaje SMS</span><span class="sxs-lookup"><span data-stu-id="6aaa0-191"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="6aaa0-192">Hello siguiente muestra cómo toosend un mensaje SMS con Hola `TwilioRestClient` clase.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-192">hello following shows how toosend an SMS message using hello `TwilioRestClient` class.</span></span> <span data-ttu-id="6aaa0-193">Hola **from_number** Twilio proporciona número para cuentas de prueba toosend mensajes SMS.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-193">hello **from_number** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="6aaa0-194">Hola **to_number** número debe ser verificado para su cuenta de Twilio antes de ejecutar código de hello.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-194">hello **to_number** number must be verified for your Twilio account before running hello code.</span></span>

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send hello SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <span data-ttu-id="6aaa0-195"><a id="howto_provide_twiml_responses"></a>Entrega de respuestas de TwiML desde su propio sitio web</span><span class="sxs-lookup"><span data-stu-id="6aaa0-195"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="6aaa0-196">Cuando la aplicación inicia una toohello llamada API de Twilio, Twilio enviará su dirección de URL de solicitud tooa que es lo esperado tooreturn una respuesta TwiML.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-196">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="6aaa0-197">ejemplo de Hola anterior utiliza dirección URL proporcionada Twilio por hello [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="6aaa0-197">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="6aaa0-198">(Aunque TwiML está diseñado para su uso por Twilio, puede verlo en el explorador.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-198">(While TwiML is designed for use by Twilio, you can view it in your browser.</span></span> <span data-ttu-id="6aaa0-199">Por ejemplo, haga clic en [http://twimlets.com/message] [ twimlet_message_url] toosee vacío `<Response>` elemento; como otro ejemplo, haga clic en [http://twimlets.com/message? Mensaje 5B0% D de %5 = Hola % 20World] [ twimlet_message_url_hello_world] toosee una `<Response>` elemento que contiene un `<Say>` elemento.)</span><span class="sxs-lookup"><span data-stu-id="6aaa0-199">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="6aaa0-200">En lugar de basarse en la dirección URL proporcionada Twilio por hello, puede crear su propio sitio que devuelve las respuestas HTTP.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-200">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="6aaa0-201">Puede crear el sitio de Hola en cualquier lenguaje que devuelve respuestas en XML; en este tema se da por supuesto que va a usar Hola de Python toocreate TwiML.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-201">You can create hello site in any language that returns XML responses; this topic assumes you will be using Python toocreate hello TwiML.</span></span>

<span data-ttu-id="6aaa0-202">Hello en los ejemplos siguientes dará como resultado una respuesta TwiML que dice **Hello World** en llamada de Hola.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-202">hello following examples will output a TwiML response that says **Hello World** on hello call.</span></span>

<span data-ttu-id="6aaa0-203">Con Flask:</span><span class="sxs-lookup"><span data-stu-id="6aaa0-203">With Flask:</span></span>

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

<span data-ttu-id="6aaa0-204">Con Django:</span><span class="sxs-lookup"><span data-stu-id="6aaa0-204">With Django:</span></span>

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

<span data-ttu-id="6aaa0-205">Como puede ver en el ejemplo de Hola anterior, hello TwiML respuesta es simplemente un documento XML.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-205">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="6aaa0-206">biblioteca de Twilio de Hola para Python contiene clases que se generarán TwiML automáticamente.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-206">hello Twilio library for Python contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="6aaa0-207">Hello ejemplo siguiente genera respuesta equivalente de hello tal y como se muestra arriba, pero usa hello `twiml` módulo en la biblioteca de Twilio de Hola para Python:</span><span class="sxs-lookup"><span data-stu-id="6aaa0-207">hello example below produces hello equivalent response as shown above, but uses hello `twiml` module in hello Twilio library for Python:</span></span>

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

<span data-ttu-id="6aaa0-208">Para más información sobre TwiML, vea [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="6aaa0-208">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span>

<span data-ttu-id="6aaa0-209">Una vez que tenga la aplicación de Python configurar tooprovide TwiML respuestas, use la dirección URL de Hola de aplicación hello como Hola dirección URL pasada en hello `client.calls.create` método.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-209">Once you have your Python application set up tooprovide TwiML responses, use hello URL of hello application as hello URL passed into hello `client.calls.create`  method.</span></span> <span data-ttu-id="6aaa0-210">Por ejemplo, si tiene una aplicación Web denominada **MyTwiML** tooan implementado Azure servicio hospedado, puede usar su dirección url como webhook tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="6aaa0-210">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, you can use its url as webhook as shown in hello following example:</span></span>

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <span data-ttu-id="6aaa0-211"><a id="AdditionalServices"></a>Procedimientos: Uso de servicios Twilio adicionales</span><span class="sxs-lookup"><span data-stu-id="6aaa0-211"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="6aaa0-212">Además toohello ejemplos que se muestran aquí, que twilio ofrece API basadas en web que puede usar la funcionalidad adicional de Twilio de tooleverage desde su aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="6aaa0-212">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="6aaa0-213">Para obtener información detallada, vea hello [documentación de la API de Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="6aaa0-213">For full details, see hello [Twilio API documentation][twilio_api].</span></span>

## <span data-ttu-id="6aaa0-214"><a id="NextSteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6aaa0-214"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="6aaa0-215">Ahora que ha aprendido los conceptos básicos de Hola de hello Twilio servicio, siga estos toolearn de vínculos más:</span><span class="sxs-lookup"><span data-stu-id="6aaa0-215">Now that you have learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="6aaa0-216">[Directrices de seguridad de Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="6aaa0-216">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="6aaa0-217">[Guías de procedimientos y código de ejemplo de Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="6aaa0-217">[Twilio HowTo Guides and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="6aaa0-218">[Tutoriales de inicio rápido de Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="6aaa0-218">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="6aaa0-219">[Twilio en GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="6aaa0-219">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="6aaa0-220">[Hable tooTwilio soporte técnico][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="6aaa0-220">[Talk tooTwilio Support][twilio_support]</span></span>

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
