---
title: aaaHow tooUse Twilio para voz y SMS (. NET) | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomake una llamada de teléfono así como enviar un SMS de mensajes con el servicio de API de Twilio de hello en Azure. Los ejemplos de código están escritos en .NET."
services: 
documentationcenter: .net
author: devinrader
manager: twilio
editor: 
ms.assetid: 74d4f3c9-f1cb-4968-b744-36b32cd0e834
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/24/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: f568da87ef15e9f540fee9674de31e983d4acb6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a><span data-ttu-id="a0101-104">Cómo toouse Twilio para voz y capacidades SMS de Azure</span><span class="sxs-lookup"><span data-stu-id="a0101-104">How toouse Twilio for voice and SMS capabilities from Azure</span></span>
<span data-ttu-id="a0101-105">Esta guía demuestra cómo tooperform las tareas de programación habituales con hello Twilio API de servicio en Azure.</span><span class="sxs-lookup"><span data-stu-id="a0101-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="a0101-106">escenarios de Hello descritos incluyen realizando una llamada telefónica y enviar un mensaje de servicio de mensajes cortos (SMS).</span><span class="sxs-lookup"><span data-stu-id="a0101-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="a0101-107">Para obtener más información sobre Twilio y el uso de voz y SMS en las aplicaciones, vea hello [pasos siguientes](#NextSteps) sección.</span><span class="sxs-lookup"><span data-stu-id="a0101-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next steps](#NextSteps) section.</span></span>

## <span data-ttu-id="a0101-108"><a id="WhatIs"></a>¿Qué es Twilio?</span><span class="sxs-lookup"><span data-stu-id="a0101-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="a0101-109">Twilio está activando Hola futuro de las comunicaciones empresariales, la habilitación de los desarrolladores tooembed voice, VoIP y en las aplicaciones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="a0101-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="a0101-110">Virtualizar toda la infraestructura necesarios en un entorno global, basada en la nube, exponerlo a través de la plataforma de hello API de comunicaciones de Twilio.</span><span class="sxs-lookup"><span data-stu-id="a0101-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="a0101-111">Las aplicaciones son toobuild simple y escalable.</span><span class="sxs-lookup"><span data-stu-id="a0101-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="a0101-112">Disfrute de la flexibilidad de pagar por lo que utiliza y aproveche la confiabilidad de la nube.</span><span class="sxs-lookup"><span data-stu-id="a0101-112">Enjoy flexibility with pay-as-you-go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="a0101-113">**Voz Twilio** permite la toomake de las aplicaciones y recibir llamadas telefónicas.</span><span class="sxs-lookup"><span data-stu-id="a0101-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="a0101-114">**Twilio SMS** habilita la toosend de las aplicaciones y recibir mensajes SMS.</span><span class="sxs-lookup"><span data-stu-id="a0101-114">**Twilio SMS** enables your applications toosend and receive SMS messages.</span></span> <span data-ttu-id="a0101-115">**Cliente de Twilio** permite llamadas de VoIP toomake desde cualquier teléfono, una tableta o un explorador y es compatible con WebRTC.</span><span class="sxs-lookup"><span data-stu-id="a0101-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="a0101-116"><a id="Pricing"></a>Precios de Twilio y ofertas especiales</span><span class="sxs-lookup"><span data-stu-id="a0101-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="a0101-117">Los clientes de Azure reciben una [oferta especial](http://www.twilio.com/azure): 10 $ de regalo en crédito Twilio al actualizar su cuenta Twilio.</span><span class="sxs-lookup"><span data-stu-id="a0101-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="a0101-118">Este crédito Twilio puede ser aplicada tooany uso de Twilio (10 $ crédito equivalente toosending como máximo 1000 mensajes SMS o recibir una too1000 entrada minutos de voz, según la ubicación de Hola de su destino de número y el mensaje o la llamada de teléfono).</span><span class="sxs-lookup"><span data-stu-id="a0101-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="a0101-119">Canjee este crédito Twilio y comience en [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="a0101-119">Redeem this Twilio credit and get started at [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="a0101-120">Twilio es un servicio de pago por uso.</span><span class="sxs-lookup"><span data-stu-id="a0101-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="a0101-121">No hay comisiones establecidas y puede cerrar su cuenta en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="a0101-121">There are no set-up fees, and you can close your account at any time.</span></span> <span data-ttu-id="a0101-122">Puede encontrar más detalles en [Precios de Twilio](http://www.twilio.com/voice/pricing).</span><span class="sxs-lookup"><span data-stu-id="a0101-122">You can find more details at [Twilio Pricing](http://www.twilio.com/voice/pricing).</span></span>

## <span data-ttu-id="a0101-123"><a id="Concepts"></a>Conceptos</span><span class="sxs-lookup"><span data-stu-id="a0101-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="a0101-124">Hola Twilio API es una API de REST que proporciona funciones SMS y voz para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a0101-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="a0101-125">Las bibliotecas de cliente están disponibles en varios lenguajes; para ver una lista, consulte las [bibliotecas de API de Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="a0101-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="a0101-126">Aspectos clave de hello Twilio API son verbos de Twilio y lenguaje de marcado de Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="a0101-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="a0101-127"><a id="Verbs"></a>Verbos de Twilio</span><span class="sxs-lookup"><span data-stu-id="a0101-127"><a id="Verbs"></a>Twilio verbs</span></span>
<span data-ttu-id="a0101-128">Hola API hace que el uso de Twilio verbos; Por ejemplo, hello  **&lt;decir&gt;**  verbo indica Twilio tooaudibly entregar un mensaje en una llamada.</span><span class="sxs-lookup"><span data-stu-id="a0101-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="a0101-129">Hola aquí te mostramos una lista de verbos de Twilio.</span><span class="sxs-lookup"><span data-stu-id="a0101-129">hello following is a list of Twilio verbs.</span></span>  <span data-ttu-id="a0101-130">Obtenga información acerca de Hola unos a otros verbos y capacidades a través de [documentación del lenguaje de marcado de Twilio](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="a0101-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="a0101-131">**&lt;Acceso telefónico&gt;**: conecta tooanother teléfono de hello llamador.</span><span class="sxs-lookup"><span data-stu-id="a0101-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="a0101-132">**&lt;Recopilar&gt;**: recopila los dígitos numéricos del teclado del teléfono de Hola.</span><span class="sxs-lookup"><span data-stu-id="a0101-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="a0101-133">**&lt;Hangup&gt;**: finaliza una llamada.</span><span class="sxs-lookup"><span data-stu-id="a0101-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="a0101-134">**&lt;Play&gt;**: reproduce un archivo de audio.</span><span class="sxs-lookup"><span data-stu-id="a0101-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="a0101-135">**&lt;Pause&gt;**: espera en silencio una cantidad de segundos específica.</span><span class="sxs-lookup"><span data-stu-id="a0101-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="a0101-136">**&lt;Registro&gt;**: registra la voz del llamador de Hola y devuelve una dirección URL de un archivo que contenga una grabación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a0101-136">**&lt;Record&gt;**: Records hello caller's voice and returns an URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="a0101-137">**&lt;Redirigir&gt;**: transfiere el control de una llamada o SMS toohello TwiML en una dirección URL diferente.</span><span class="sxs-lookup"><span data-stu-id="a0101-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="a0101-138">**&lt;Rechazar&gt;**: rechaza una entrada llame al número de Twilio de tooyour sin facturación</span><span class="sxs-lookup"><span data-stu-id="a0101-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="a0101-139">**&lt;Diga&gt;**: convierte texto toospeech que se realiza en una llamada.</span><span class="sxs-lookup"><span data-stu-id="a0101-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="a0101-140">**&lt;Sms&gt;**: envía un mensaje SMS.</span><span class="sxs-lookup"><span data-stu-id="a0101-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="a0101-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="a0101-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="a0101-142">TwiML es un conjunto de instrucciones basado en XML en función de los verbos de Twilio de Hola que informan de Twilio de cómo tooprocess una llamada o SMS.</span><span class="sxs-lookup"><span data-stu-id="a0101-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="a0101-143">Por ejemplo, hello después TwiML convertiría texto hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="a0101-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="a0101-144">Cuando la aplicación llama hello Twilio API, uno de los parámetros de la API de hello es dirección URL de Hola que devuelve la respuesta de TwiML Hola.</span><span class="sxs-lookup"><span data-stu-id="a0101-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="a0101-145">Para fines de desarrollo, puede utilizar direcciones URL siempre Twilio tooprovide hello TwiML las respuestas que usan las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a0101-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="a0101-146">También puede hospedar sus respuestas de las direcciones URL tooproduce hello TwiML y otra opción es hello toouse **TwiMLResponse** objeto.</span><span class="sxs-lookup"><span data-stu-id="a0101-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="a0101-147">Para obtener más información sobre los verbos de Twilio, sus atributos y TwiML, consulte [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="a0101-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="a0101-148">Para obtener información adicional acerca de hello Twilio API, consulte [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="a0101-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="a0101-149"><a id="CreateAccount"></a>Creación de una cuenta de Twilio</span><span class="sxs-lookup"><span data-stu-id="a0101-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="a0101-150">Cuando esté listo tooget una cuenta de Twilio, regístrese en [intente Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="a0101-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="a0101-151">Puede empezar con una cuenta gratuita y, posteriormente, actualizarla.</span><span class="sxs-lookup"><span data-stu-id="a0101-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="a0101-152">Cuando se registre para obtener una cuenta de Twilio, recibirá un identificador de cuenta y un token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="a0101-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="a0101-153">Ambos serán llamadas a la API de Twilio toomake necesarios.</span><span class="sxs-lookup"><span data-stu-id="a0101-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="a0101-154">tooprevent no autorizado obtenga acceso a cuenta tooyour, proteger el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="a0101-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="a0101-155">El identificador de cuenta y la autenticación de token están visibles en hello [página de la cuenta de Twilio][twilio_account], en Hola campos con la etiqueta **SID de cuenta** y **delTOKENdeautenticación**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="a0101-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="a0101-156"><a id="create_app"></a>Creación de una aplicación de Azure</span><span class="sxs-lookup"><span data-stu-id="a0101-156"><a id="create_app"></a>Create an Azure Application</span></span>
<span data-ttu-id="a0101-157">Una aplicación de Azure que hospeda una aplicación habilitada para Twilio no es diferente de ninguna otra aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="a0101-157">An Azure application that hosts a Twilio enabled application is no different from any other Azure application.</span></span> <span data-ttu-id="a0101-158">Agregar la biblioteca de .NET de Twilio de Hola y configurar las bibliotecas .NET de Twilio de hello rol toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="a0101-158">You add hello Twilio .NET library and configure hello role toouse hello Twilio .NET libraries.</span></span>
<span data-ttu-id="a0101-159">Para obtener información sobre la creación de un proyecto inicial de Azure, consulte [Creación de un proyecto de Azure en Visual Studio][vs_project].</span><span class="sxs-lookup"><span data-stu-id="a0101-159">For information on creating an initial Azure project, see [Creating an Azure project with Visual Studio][vs_project].</span></span>

## <span data-ttu-id="a0101-160"><a id="configure_app"></a>Configurar las bibliotecas de Twilio de toouse de la aplicación</span><span class="sxs-lookup"><span data-stu-id="a0101-160"><a id="configure_app"></a>Configure Your Application toouse Twilio Libraries</span></span>
<span data-ttu-id="a0101-161">Twilio proporciona un conjunto de bibliotecas de aplicación auxiliar de .NET que contienen distintos aspectos de Twilio tooprovide formas sencillas y simple toointeract con hello API de REST de Twilio y cliente de Twilio toogenerate TwiML respuestas.</span><span class="sxs-lookup"><span data-stu-id="a0101-161">Twilio provides a set of .NET helper libraries that wrap various aspects of Twilio tooprovide simple and easy ways toointeract with hello Twilio REST API and Twilio Client toogenerate TwiML responses.</span></span>

<span data-ttu-id="a0101-162">Twilio proporciona cinco bibliotecas para desarrolladores de .NET:</span><span class="sxs-lookup"><span data-stu-id="a0101-162">Twilio provides five libraries for .NET developers:</span></span>
<span data-ttu-id="a0101-163">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="a0101-163">Library</span></span>|<span data-ttu-id="a0101-164">Descripción</span><span class="sxs-lookup"><span data-stu-id="a0101-164">Description</span></span>
---|---
<span data-ttu-id="a0101-165">Twilio.API</span><span class="sxs-lookup"><span data-stu-id="a0101-165">Twilio.API</span></span>|<span data-ttu-id="a0101-166">Hola biblioteca principal de Twilio que ajusta Hola API de REST de Twilio en una biblioteca de .NET descriptiva.</span><span class="sxs-lookup"><span data-stu-id="a0101-166">hello core Twilio library that wraps hello Twilio REST API in a friendly .NET library.</span></span> <span data-ttu-id="a0101-167">Esta biblioteca está disponible para .NET, Silverlight y Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="a0101-167">This library is available for .NET, Silverlight, and Windows Phone 7.</span></span>
<span data-ttu-id="a0101-168">Twilio.TwiML</span><span class="sxs-lookup"><span data-stu-id="a0101-168">Twilio.TwiML</span></span>|<span data-ttu-id="a0101-169">Proporciona una marca de TwiML .NET toogenerate de manera fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="a0101-169">Provides a .NET friendly way toogenerate TwiML markup.</span></span>
<span data-ttu-id="a0101-170">Twilio.MVC</span><span class="sxs-lookup"><span data-stu-id="a0101-170">Twilio.MVC</span></span>|<span data-ttu-id="a0101-171">Para los desarrolladores que usan ASP.NET MVC, esta biblioteca incluye un atributo TwilioController, TwiML ActionResult y de validación de solicitudes.</span><span class="sxs-lookup"><span data-stu-id="a0101-171">For developers using ASP.NET MVC, this library includes a TwilioController, TwiML ActionResult, and request validation attribute.</span></span>
<span data-ttu-id="a0101-172">Twilio.WebMatrix</span><span class="sxs-lookup"><span data-stu-id="a0101-172">Twilio.WebMatrix</span></span>|<span data-ttu-id="a0101-173">Para los desarrolladores que usan la herramienta de desarrollo WebMatrix gratuita de Microsoft, esta biblioteca contiene aplicaciones auxiliares de sintaxis Razor para diversas acciones de Twilio.</span><span class="sxs-lookup"><span data-stu-id="a0101-173">For developers using Microsoft's free WebMatrix development tool, this library contains Razor syntax helpers for various Twilio actions.</span></span>
<span data-ttu-id="a0101-174">Twilio.Client.Capability</span><span class="sxs-lookup"><span data-stu-id="a0101-174">Twilio.Client.Capability</span></span>|<span data-ttu-id="a0101-175">Contiene el generador de símbolo (token) de capacidad de Hola para su uso con hello SDK de JavaScript de cliente de Twilio.</span><span class="sxs-lookup"><span data-stu-id="a0101-175">Contains hello Capability token generator for use with hello Twilio Client JavaScript SDK.</span></span>

<span data-ttu-id="a0101-176">Tenga en cuenta que todas las bibliotecas requieren .NET 3.5, Silverlight 4 o Windows Phone 7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="a0101-176">Note that all libraries require .NET 3.5, Silverlight 4, or Windows Phone 7 or later.</span></span>

<span data-ttu-id="a0101-177">ejemplos de Hello proporcionados en esta guía usan biblioteca de Twilio.API Hola.</span><span class="sxs-lookup"><span data-stu-id="a0101-177">hello samples provided in this guide use hello Twilio.API library.</span></span>

<span data-ttu-id="a0101-178">pueden ser bibliotecas de Hello [instalado mediante la extensión del Administrador de paquetes de NuGet de hello](http://www.twilio.com/docs/csharp/install) disponible para Visual Studio 2010 activo too2015.</span><span class="sxs-lookup"><span data-stu-id="a0101-178">hello libraries can be [installed using hello NuGet package manager extension](http://www.twilio.com/docs/csharp/install) available for Visual Studio 2010 up too2015.</span></span>  <span data-ttu-id="a0101-179">código fuente Hello se hospeda una en [GitHub][twilio_github_repo], que incluye una Wiki que contiene la documentación completa para el uso de bibliotecas de Hola.</span><span class="sxs-lookup"><span data-stu-id="a0101-179">hello source code is hosted on [GitHub][twilio_github_repo], which includes a Wiki that contains complete documentation for using hello libraries.</span></span>

<span data-ttu-id="a0101-180">De manera predeterminada, Microsoft Visual Studio 2010 instala la versión 1.2 de NuGet.</span><span class="sxs-lookup"><span data-stu-id="a0101-180">By default, Microsoft Visual Studio 2010 installs version 1.2 of NuGet.</span></span> <span data-ttu-id="a0101-181">Instalar bibliotecas de Twilio de hello requiere la versión 1.6 de NuGet o superior.</span><span class="sxs-lookup"><span data-stu-id="a0101-181">Installing hello Twilio libraries requires version 1.6 of NuGet or higher.</span></span> <span data-ttu-id="a0101-182">Para obtener información sobre la instalación o actualización de NuGet, consulte [http://nuget.org/][nuget].</span><span class="sxs-lookup"><span data-stu-id="a0101-182">For information on installing or updating NuGet, see [http://nuget.org/][nuget].</span></span>

> [!NOTE]
> <span data-ttu-id="a0101-183">tooinstall Hola última versión de NuGet, primero debe desinstalar Hola versión cargada mediante Hola Administrador de extensiones de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0101-183">tooinstall hello latest version of NuGet, you must first uninstall hello loaded version using hello Visual Studio Extension Manager.</span></span> <span data-ttu-id="a0101-184">toodo por lo tanto, debe ejecutar Visual Studio como administrador.</span><span class="sxs-lookup"><span data-stu-id="a0101-184">toodo so, you must run Visual Studio as administrator.</span></span> <span data-ttu-id="a0101-185">En caso contrario, botón de desinstalación de hello está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="a0101-185">Otherwise, hello Uninstall button is disabled.</span></span>
>
>

### <span data-ttu-id="a0101-186"><a id="use_nuget"></a>proyecto de Visual Studio tooyour: de tooadd hello Twilio bibliotecas</span><span class="sxs-lookup"><span data-stu-id="a0101-186"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour Visual Studio project:</span></span>
1. <span data-ttu-id="a0101-187">Abra su solución en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0101-187">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="a0101-188">Haga clic con el botón secundario en **Referencias**.</span><span class="sxs-lookup"><span data-stu-id="a0101-188">Right-click **References**.</span></span>
3. <span data-ttu-id="a0101-189">Haga clic en **Administrar paquetes de NuGet...**</span><span class="sxs-lookup"><span data-stu-id="a0101-189">Click **Manage NuGet Packages...**</span></span>
4. <span data-ttu-id="a0101-190">Haga clic en **En línea**.</span><span class="sxs-lookup"><span data-stu-id="a0101-190">Click **Online**.</span></span>
5. <span data-ttu-id="a0101-191">En el cuadro en línea de la búsqueda de hello, escriba *twilio*.</span><span class="sxs-lookup"><span data-stu-id="a0101-191">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="a0101-192">Haga clic en **instalar** en el paquete de Twilio Hola.</span><span class="sxs-lookup"><span data-stu-id="a0101-192">Click **Install** on hello Twilio package.</span></span>

## <span data-ttu-id="a0101-193"><a id="howto_make_call"></a>Realización de una llamada saliente</span><span class="sxs-lookup"><span data-stu-id="a0101-193"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="a0101-194">Hello siguiente muestra cómo toomake una salida llamar a utilizando hello **CallResource** clase.</span><span class="sxs-lookup"><span data-stu-id="a0101-194">hello following shows how toomake an outgoing call using hello **CallResource** class.</span></span> <span data-ttu-id="a0101-195">Este código también usa un Hola de tooreturn sitio proporcionado Twilio respuesta de lenguaje de marcado de Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="a0101-195">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="a0101-196">Sustituya los valores de hello **a** y **de** los números de teléfono y asegúrese de comprobar hello **de** número de teléfono para su cuenta de Twilio antes de ejecutar código de hello.</span><span class="sxs-lookup"><span data-stu-id="a0101-196">Substitute your values for hello **to** and **from** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account before running hello code.</span></span>

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    var url = "http://twimlets.com/message";
    url = $"{url}?Message%5B0%5D=Hello%20World";

    // Set hello call From, To, and URL values toouse for hello call.
    // This sample uses hello sandbox number provided by
    // Twilio toomake hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri(url));
        }

<span data-ttu-id="a0101-197">Para obtener más información acerca de los parámetros de hello pasado toohello **CallResource.Create** método, consulte [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="a0101-197">For more information about hello parameters passed in toohello **CallResource.Create** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="a0101-198">Como se ha mencionado, este código usa un Hola de tooreturn sitio proporcionado Twilio TwiML respuesta.</span><span class="sxs-lookup"><span data-stu-id="a0101-198">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="a0101-199">En su lugar puede utilizar su propio Hola de tooprovide sitio TwiML respuesta.</span><span class="sxs-lookup"><span data-stu-id="a0101-199">You could instead use your own site tooprovide hello TwiML response.</span></span> <span data-ttu-id="a0101-200">Para más información, consulte [Entrega de respuestas de TwiML desde su propio sitio web](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="a0101-200">For more information, see [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="a0101-201"><a id="howto_send_sms"></a>Envío de un mensaje SMS</span><span class="sxs-lookup"><span data-stu-id="a0101-201"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="a0101-202">Hello captura de pantalla siguiente muestra cómo toosend un mensaje SMS con Hola **MessageResource** clase.</span><span class="sxs-lookup"><span data-stu-id="a0101-202">hello following screenshot shows how toosend an SMS message using hello **MessageResource**  class.</span></span> <span data-ttu-id="a0101-203">Hola **de** Twilio proporciona número para cuentas de prueba toosend mensajes SMS.</span><span class="sxs-lookup"><span data-stu-id="a0101-203">hello **from** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="a0101-204">Hola **a** número debe ser verificado para su cuenta de Twilio antes de ejecutar código de hello.</span><span class="sxs-lookup"><span data-stu-id="a0101-204">hello **to** number must be verified for your Twilio account before you run hello code.</span></span>

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    try
    {
        // Send an SMS message.
        var message = MessageResource.Create(
            to: new PhoneNumber("+12069419717"),
            from: new PhoneNumber("+14155992671"),
            body: "This is my SMS message.");
    }
    catch (TwilioException ex)
    {
        // An exception occurred making hello REST call
        Console.WriteLine(ex.Message);
    }

## <span data-ttu-id="a0101-205"><a id="howto_provide_twiml_responses"></a>Procedimientos: Suministro de respuestas de TwiML desde su propio sitio web</span><span class="sxs-lookup"><span data-stu-id="a0101-205"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own website</span></span>
<span data-ttu-id="a0101-206">Cuando la aplicación inicia una toohello llamada API de Twilio - por ejemplo, a través de hello **CallResource.Create** método - Twilio envía su solicitud tooan dirección URL esperado tooreturn una respuesta TwiML.</span><span class="sxs-lookup"><span data-stu-id="a0101-206">When your application initiates a call toohello Twilio API - for example, via hello **CallResource.Create** method - Twilio sends your request tooan URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="a0101-207">ejemplo de Hola en [Cómo: realizar una llamada saliente](#howto_make_call) usa Hola dirección URL proporcionada Twilio [http://twimlets.com/message] [ twimlet_message_url] tooreturn respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="a0101-207">hello example in [How to: Make an outgoing call](#howto_make_call) uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url] tooreturn hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="a0101-208">Aunque TwiML está diseñado para su uso por los servicios web, puede ver hello TwiML en el explorador.</span><span class="sxs-lookup"><span data-stu-id="a0101-208">While TwiML is designed for use by web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="a0101-209">Por ejemplo, haga clic en [http://twimlets.com/message] [ twimlet_message_url] toosee vacío &lt;respuesta&gt; elemento; como otro ejemplo, haga clic en [http://twimlets.com/message ? 5B0 de mensaje % D de %5 = Hola % 20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee una &lt;respuesta&gt; elemento que contiene un &lt;decir&gt; elemento.</span><span class="sxs-lookup"><span data-stu-id="a0101-209">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty &lt;Response&gt; element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee a &lt;Response&gt; element that contains a &lt;Say&gt; element.</span></span>
>
>

<span data-ttu-id="a0101-210">En lugar de basarse en la dirección URL proporcionada Twilio por hello, puede crear su propio sitio de dirección URL que devuelve las respuestas HTTP.</span><span class="sxs-lookup"><span data-stu-id="a0101-210">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="a0101-211">Puede crear el sitio de Hola en cualquier lenguaje que devuelve las respuestas HTTP.</span><span class="sxs-lookup"><span data-stu-id="a0101-211">You can create hello site in any language that returns HTTP responses.</span></span> <span data-ttu-id="a0101-212">En este tema se da por supuesto que va a hospedar Hola URL desde un controlador genérico de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a0101-212">This topic assumes you'll be hosting hello URL from an ASP.NET generic handler.</span></span>

<span data-ttu-id="a0101-213">Hola siguiente controlador de ASP.NET elabora una respuesta TwiML que dice **Hello World** en llamada de Hola.</span><span class="sxs-lookup"><span data-stu-id="a0101-213">hello following ASP.NET Handler crafts a TwiML response that says **Hello World** on hello call.</span></span>

    using System.Text;
    using System.Web;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {
            public void ProcessRequest(HttpContext context)
            {
                const string twiMLResponse =
                    "<Response><Say>Hello World.</Say></Response>";
                
                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.ContentEncoding = Encoding.UTF8;
                context.Response.Write(twiMLResponse);
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }
    
<span data-ttu-id="a0101-214">Como puede ver en el ejemplo de Hola anterior, hello TwiML respuesta es simplemente un documento XML.</span><span class="sxs-lookup"><span data-stu-id="a0101-214">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="a0101-215">biblioteca de Twilio.TwiML Hola contiene clases que se generarán TwiML automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a0101-215">hello Twilio.TwiML library contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="a0101-216">Hello ejemplo siguiente genera respuesta equivalente de hello tal y como se muestra arriba, pero usa hello **VoiceResponse** clase.</span><span class="sxs-lookup"><span data-stu-id="a0101-216">hello example below produces hello equivalent response as shown above, but uses hello **VoiceResponse** class.</span></span>

    using System.Web;
    using Twilio.TwiML;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {

            public void ProcessRequest(HttpContext context)
            {
                var twiml = new VoiceResponse();
                twiml.Say("Hello World.");

                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.Write(twiml.ToString());
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }

<span data-ttu-id="a0101-217">Para obtener más información sobre TwiML, consulte [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="a0101-217">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span></span>

<span data-ttu-id="a0101-218">Una vez haya configurado un respuestas de forma tooprovide TwiML, puede pasar esa dirección URL toohello **CallResource.Create** método.</span><span class="sxs-lookup"><span data-stu-id="a0101-218">Once you have set up a way tooprovide TwiML responses, you can pass that URL toohello **CallResource.Create** method.</span></span> <span data-ttu-id="a0101-219">Por ejemplo, si tiene una aplicación web denominada tooan MyTwiML implementado el servicio de nube de Azure y Hola de su controlador de ASP.NET se denomina mytwiml.ashx, dirección URL de Hola se puede pasar demasiado**CallResource.Create** tal y como se muestra en el siguiente código de hello ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a0101-219">For example, if you have a web application named MyTwiML deployed tooan Azure cloud service, and hello name of your ASP.NET Handler is mytwiml.ashx, hello URL can be passed too**CallResource.Create** as shown in hello following code sample:</span></span>

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

<span data-ttu-id="a0101-220">Para obtener información adicional acerca del uso de Twilio en Azure con ASP.NET, vea [cómo toomake un teléfono llamar a con Twilio en un rol web en Azure][howto_phonecall_dotnet].</span><span class="sxs-lookup"><span data-stu-id="a0101-220">For additional information about using Twilio on Azure with ASP.NET, see [How toomake a phone call using Twilio in a web role on Azure][howto_phonecall_dotnet].</span></span>

[!INCLUDE [twilio-additional-services-and-next-steps](../includes/twilio-additional-services-and-next-steps.md)]

[howto_phonecall_dotnet]: partner-twilio-cloud-services-dotnet-phone-call-web-role.md

[twimlet_message_url]: http://twimlets.com/message

[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls

[vs_project]:http://msdn.microsoft.com/library/windowsazure/ee405487.aspx
[nuget]:http://nuget.org/
[twilio_github_repo]:https://github.com/twilio/twilio-csharp

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
