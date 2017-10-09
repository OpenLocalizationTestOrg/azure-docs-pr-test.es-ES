---
title: aaaHow tooUse Twilio para voz y SMS (Java) | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomake una llamada de teléfono así como enviar un SMS de mensajes con el servicio de API de Twilio de hello en Azure. Ejemplos de código escritos en Java."
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: f3508965-5527-4255-9d51-5d5f926f4d43
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: a186e2c8e73ced928bd0dec348971034f10ba82c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a><span data-ttu-id="1b92c-104">Cómo tooUse Twilio para voz y capacidades de SMS en Java</span><span class="sxs-lookup"><span data-stu-id="1b92c-104">How tooUse Twilio for Voice and SMS Capabilities in Java</span></span>
<span data-ttu-id="1b92c-105">Esta guía demuestra cómo tooperform las tareas de programación habituales con hello Twilio API de servicio en Azure.</span><span class="sxs-lookup"><span data-stu-id="1b92c-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="1b92c-106">escenarios de Hello descritos incluyen realizando una llamada telefónica y enviar un mensaje de servicio de mensajes cortos (SMS).</span><span class="sxs-lookup"><span data-stu-id="1b92c-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="1b92c-107">Para obtener más información sobre Twilio y el uso de voz y SMS en las aplicaciones, vea hello [pasos](#NextSteps) sección.</span><span class="sxs-lookup"><span data-stu-id="1b92c-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="1b92c-108"><a id="WhatIs"></a>¿Qué es Twilio?</span><span class="sxs-lookup"><span data-stu-id="1b92c-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="1b92c-109">Twilio es una API de servicio web de telefonía que permite utilizar los lenguajes web existentes y voz toobuild de conocimientos y las aplicaciones de SMS.</span><span class="sxs-lookup"><span data-stu-id="1b92c-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="1b92c-110">Twilio es un servicio de terceros (no una característica de Azure ni tampoco un producto de Microsoft).</span><span class="sxs-lookup"><span data-stu-id="1b92c-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="1b92c-111">**Voz Twilio** permite la toomake de las aplicaciones y recibir llamadas telefónicas.</span><span class="sxs-lookup"><span data-stu-id="1b92c-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="1b92c-112">**Twilio SMS** permite la toomake de las aplicaciones y recibir mensajes SMS.</span><span class="sxs-lookup"><span data-stu-id="1b92c-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="1b92c-113">**Cliente de Twilio** permite que las aplicaciones con las conexiones de Internet existentes, incluidas las conexiones móviles tooenable la comunicación de voz.</span><span class="sxs-lookup"><span data-stu-id="1b92c-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="1b92c-114"><a id="Pricing"></a>Precios de Twilio y ofertas especiales</span><span class="sxs-lookup"><span data-stu-id="1b92c-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="1b92c-115">Puede encontrar información sobre los precios de Twilio en [Precios de Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="1b92c-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="1b92c-116">Los clientes de Azure reciben una [oferta especial][special_offer]: 1000 mensajes o 1000 minutos para llamar totalmente gratuitos.</span><span class="sxs-lookup"><span data-stu-id="1b92c-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="1b92c-117">toosign hacia arriba para esta oferta u obtener más información, visite [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="1b92c-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>

## <span data-ttu-id="1b92c-118"><a id="Concepts"></a>Conceptos</span><span class="sxs-lookup"><span data-stu-id="1b92c-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="1b92c-119">Hola Twilio API es una API de REST que proporciona funciones SMS y voz para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1b92c-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="1b92c-120">Las bibliotecas de cliente están disponibles en varios lenguajes; para ver una lista, consulte las [bibliotecas de API de Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="1b92c-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="1b92c-121">Aspectos clave de hello Twilio API son verbos de Twilio y lenguaje de marcado de Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="1b92c-121">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="1b92c-122"><a id="Verbs"></a>Verbos de Twilio</span><span class="sxs-lookup"><span data-stu-id="1b92c-122"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="1b92c-123">Hola API hace que el uso de Twilio verbos; Por ejemplo, hello  **&lt;decir&gt;**  verbo indica Twilio tooaudibly entregar un mensaje en una llamada.</span><span class="sxs-lookup"><span data-stu-id="1b92c-123">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="1b92c-124">Hola aquí te mostramos una lista de verbos de Twilio.</span><span class="sxs-lookup"><span data-stu-id="1b92c-124">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="1b92c-125">**&lt;Acceso telefónico&gt;**: conecta tooanother teléfono de hello llamador.</span><span class="sxs-lookup"><span data-stu-id="1b92c-125">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="1b92c-126">**&lt;Recopilar&gt;**: recopila los dígitos numéricos del teclado del teléfono de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b92c-126">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="1b92c-127">**&lt;Hangup&gt;**: finaliza una llamada.</span><span class="sxs-lookup"><span data-stu-id="1b92c-127">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="1b92c-128">**&lt;Play&gt;**: reproduce un archivo de audio.</span><span class="sxs-lookup"><span data-stu-id="1b92c-128">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="1b92c-129">**&lt;Cola&gt;**: agregar hello tooa cola de los llamadores.</span><span class="sxs-lookup"><span data-stu-id="1b92c-129">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="1b92c-130">**&lt;Pause&gt;**: espera en silencio una cantidad de segundos específica.</span><span class="sxs-lookup"><span data-stu-id="1b92c-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="1b92c-131">**&lt;Registro&gt;**: registra la voz del llamador de Hola y devuelve una dirección URL de un archivo que contenga una grabación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b92c-131">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="1b92c-132">**&lt;Redirigir&gt;**: transfiere el control de una llamada o SMS toohello TwiML en una dirección URL diferente.</span><span class="sxs-lookup"><span data-stu-id="1b92c-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="1b92c-133">**&lt;Rechazar&gt;**: rechaza una entrada llame al número de Twilio de tooyour sin facturación.</span><span class="sxs-lookup"><span data-stu-id="1b92c-133">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="1b92c-134">**&lt;Diga&gt;**: convierte texto toospeech que se realiza en una llamada.</span><span class="sxs-lookup"><span data-stu-id="1b92c-134">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="1b92c-135">**&lt;Sms&gt;**: envía un mensaje SMS.</span><span class="sxs-lookup"><span data-stu-id="1b92c-135">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="1b92c-136"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="1b92c-136"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="1b92c-137">TwiML es un conjunto de instrucciones basado en XML en función de los verbos de Twilio de Hola que informan de Twilio de cómo tooprocess una llamada o SMS.</span><span class="sxs-lookup"><span data-stu-id="1b92c-137">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="1b92c-138">Por ejemplo, hello después TwiML convertiría texto hello **Hola a todos!**</span><span class="sxs-lookup"><span data-stu-id="1b92c-138">As an example, hello following TwiML would convert hello text **Hello World!**</span></span> <span data-ttu-id="1b92c-139">toospeech.</span><span class="sxs-lookup"><span data-stu-id="1b92c-139">toospeech.</span></span>

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="1b92c-140">Cuando la aplicación llama hello Twilio API, uno de los parámetros de la API de hello es dirección URL de Hola que devuelve la respuesta de TwiML Hola.</span><span class="sxs-lookup"><span data-stu-id="1b92c-140">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="1b92c-141">Para fines de desarrollo, puede utilizar direcciones URL siempre Twilio tooprovide hello TwiML las respuestas que usan las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1b92c-141">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="1b92c-142">También puede hospedar sus respuestas de las direcciones URL tooproduce hello TwiML y otra opción es hello toouse **TwiMLResponse** objeto.</span><span class="sxs-lookup"><span data-stu-id="1b92c-142">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="1b92c-143">Para obtener más información sobre los verbos de Twilio, sus atributos y TwiML, consulte [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="1b92c-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="1b92c-144">Para obtener información adicional acerca de hello Twilio API, consulte [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="1b92c-144">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="1b92c-145"><a id="CreateAccount"></a>Creación de una cuenta de Twilio</span><span class="sxs-lookup"><span data-stu-id="1b92c-145"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="1b92c-146">Cuando esté listo tooget una cuenta de Twilio, regístrese en [intente Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="1b92c-146">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="1b92c-147">Puede empezar con una cuenta gratuita y, posteriormente, actualizarla.</span><span class="sxs-lookup"><span data-stu-id="1b92c-147">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="1b92c-148">Cuando se registre para obtener una cuenta de Twilio, recibirá un identificador de cuenta y un token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="1b92c-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="1b92c-149">Ambos serán llamadas a la API de Twilio toomake necesarios.</span><span class="sxs-lookup"><span data-stu-id="1b92c-149">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="1b92c-150">tooprevent no autorizado obtenga acceso a cuenta tooyour, proteger el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="1b92c-150">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="1b92c-151">El identificador de cuenta y la autenticación de token están visibles en hello [Twilio consola][twilio_console], en Hola campos con la etiqueta **SID de cuenta** y **delTOKENdeautenticación**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="1b92c-151">Your account ID and authentication token are viewable at hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="1b92c-152"><a id="create_app"></a>Creación de una aplicación Java</span><span class="sxs-lookup"><span data-stu-id="1b92c-152"><a id="create_app"></a>Create a Java Application</span></span>
1. <span data-ttu-id="1b92c-153">Obtener Hola JAR de Twilio y agréguelo tooyour ruta de acceso y el ensamblado de implementación WAR de compilación de Java.</span><span class="sxs-lookup"><span data-stu-id="1b92c-153">Obtain hello Twilio JAR and add it tooyour Java build path and your WAR deployment assembly.</span></span> <span data-ttu-id="1b92c-154">En [https://github.com/twilio/twilio-java][twilio_java], puede descargar los orígenes de GitHub de Hola y crear su propios JAR o descargar un archivo JAR pregenerado (con o sin dependencias).</span><span class="sxs-lookup"><span data-stu-id="1b92c-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download hello GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
2. <span data-ttu-id="1b92c-155">Asegúrese del JDK **cacerts** almacén de claves contiene el certificado de entidad de certificación seguros Equifax Hola con 67:CB:9 de huella digital MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (número de serie de hello es hello SHA1 y 35:DE:F4:CF huella digital es D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="1b92c-155">Ensure your JDK's **cacerts** keystore contains hello Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello serial number is 35:DE:F4:CF and hello SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="1b92c-156">Se trata de certificado de entidad emisora (CA) de certificado de Hola para hello [https://api.twilio.com] [ twilio_api_service] servicio, que se llama cuando se usa Twilio APIs.</span><span class="sxs-lookup"><span data-stu-id="1b92c-156">This is hello certificate authority (CA) certificate for hello [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="1b92c-157">Para obtener información acerca de cómo garantizar el JDK **cacerts** almacén de claves contiene el certificado de entidad emisora de certificados correcto de hello, consulte [agregar un almacén de certificados de entidad emisora de certificados de Java de certificado toohello][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="1b92c-157">For information about ensuring your JDK's **cacerts** keystore contains hello correct CA certificate, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="1b92c-158">Instrucciones detalladas para usar la biblioteca de cliente de Twilio de Hola para Java están disponibles en [cómo tooMake una llamada de teléfono uso de Twilio en una aplicación de Java en Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="1b92c-158">Detailed instructions for using hello Twilio client library for Java are available at [How tooMake a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="1b92c-159"><a id="configure_app"></a>Configurar las bibliotecas de Twilio de tooUse de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1b92c-159"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="1b92c-160">Dentro del código, puede agregar **importar** las instrucciones en la parte superior de Hola de los archivos de origen para hello Twilio paquetes o clases desea toouse en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1b92c-160">Within your code, you can add **import** statements at hello top of your source files for hello Twilio packages or classes you want toouse in your application.</span></span>

<span data-ttu-id="1b92c-161">Para archivos de origen de Java:</span><span class="sxs-lookup"><span data-stu-id="1b92c-161">For Java source files:</span></span>

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

<span data-ttu-id="1b92c-162">Para archivos de origen de Java Server Page (JSP).</span><span class="sxs-lookup"><span data-stu-id="1b92c-162">For Java Server Page (JSP) source files:</span></span>

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
<span data-ttu-id="1b92c-163">Dependiendo de los paquetes de Twilio o clases desea toouse, su **importar** instrucciones pueden ser diferentes.</span><span class="sxs-lookup"><span data-stu-id="1b92c-163">Depending on which Twilio packages or classes you want toouse, your **import** statements may be different.</span></span>

## <span data-ttu-id="1b92c-164"><a id="howto_make_call"></a>Realización de una llamada saliente</span><span class="sxs-lookup"><span data-stu-id="1b92c-164"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="1b92c-165">Hello siguiente muestra cómo toomake una salida llamar a utilizando hello **llamar** clase.</span><span class="sxs-lookup"><span data-stu-id="1b92c-165">hello following shows how toomake an outgoing call using hello **Call** class.</span></span> <span data-ttu-id="1b92c-166">Este código también usa un Hola de tooreturn sitio proporcionado Twilio respuesta de lenguaje de marcado de Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="1b92c-166">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="1b92c-167">Sustituya los valores de hello **de** y **a** los números de teléfono y asegúrese de comprobar hello **de** número de teléfono para el código de hello Twilio cuenta toorunning anterior.</span><span class="sxs-lookup"><span data-stu-id="1b92c-167">Substitute your values for hello **from** and **to** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account prior toorunning hello code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare tooand From numbers
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="1b92c-168">Para obtener más información acerca de los parámetros de hello pasado toohello **Call.creator** método, consulte [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="1b92c-168">For more information about hello parameters passed in toohello **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="1b92c-169">Como se ha mencionado, este código usa un Hola de tooreturn sitio proporcionado Twilio TwiML respuesta.</span><span class="sxs-lookup"><span data-stu-id="1b92c-169">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="1b92c-170">En su lugar, podría utilizar su propio Hola de tooprovide sitio respuesta TwiML; Para obtener más información, consulte [cómo tooProvide las respuestas de TwiML en una aplicación de Java en Azure](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="1b92c-170">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="1b92c-171"><a id="howto_send_sms"></a>Envío de un mensaje SMS</span><span class="sxs-lookup"><span data-stu-id="1b92c-171"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="1b92c-172">Hello siguiente muestra cómo toosend un mensaje SMS con Hola **mensaje** clase.</span><span class="sxs-lookup"><span data-stu-id="1b92c-172">hello following shows how toosend an SMS message using hello **Message** class.</span></span> <span data-ttu-id="1b92c-173">Hola **de** número, **4155992671**, se proporciona por Twilio para cuentas de prueba toosend mensajes SMS.</span><span class="sxs-lookup"><span data-stu-id="1b92c-173">hello **from** number, **4155992671**, is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="1b92c-174">Hola **a** número debe comprobarse para el código de hello Twilio cuenta toorunning anterior.</span><span class="sxs-lookup"><span data-stu-id="1b92c-174">hello **to** number must be verified for your Twilio account prior toorunning hello code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare tooand From numbers and hello Body of hello SMS message
    PhoneNumber too= new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, tooand Body values
    // then send hello SMS message by calling hello create() method
    Message sms = Message.creator(to, from, body).create();
```

<span data-ttu-id="1b92c-175">Para obtener más información acerca de los parámetros de hello pasado toohello **Message.creator** método, consulte [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span><span class="sxs-lookup"><span data-stu-id="1b92c-175">For more information about hello parameters passed in toohello **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span></span>

## <span data-ttu-id="1b92c-176"><a id="howto_provide_twiml_responses"></a>Entrega de respuestas de TwiML desde su propio sitio web</span><span class="sxs-lookup"><span data-stu-id="1b92c-176"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="1b92c-177">Cuando la aplicación inicia una toohello llamada API de Twilio, por ejemplo a través de hello **CallCreator.create** método Twilio enviará su dirección de URL de solicitud tooa que es tooreturn esperado una respuesta TwiML.</span><span class="sxs-lookup"><span data-stu-id="1b92c-177">When your application initiates a call toohello Twilio API, for example via hello **CallCreator.create** method, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="1b92c-178">ejemplo de Hola anterior utiliza dirección URL proporcionada Twilio por hello [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="1b92c-178">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="1b92c-179">(Aunque TwiML está diseñado para su uso por los servicios Web, puede ver hello TwiML en el explorador.</span><span class="sxs-lookup"><span data-stu-id="1b92c-179">(While TwiML is designed for use by Web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="1b92c-180">Por ejemplo, haga clic en [http://twimlets.com/message] [ twimlet_message_url] toosee vacío  **&lt;respuesta&gt;**  elemento; como otro ejemplo, haga clic en [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee una  **&lt;respuesta&gt;**  elemento que contiene un  **&lt;decir &gt;**  elemento.)</span><span class="sxs-lookup"><span data-stu-id="1b92c-180">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] toosee a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span></span>

<span data-ttu-id="1b92c-181">En lugar de basarse en la dirección URL proporcionada Twilio por hello, puede crear su propio sitio de dirección URL que devuelve las respuestas HTTP.</span><span class="sxs-lookup"><span data-stu-id="1b92c-181">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="1b92c-182">Puede crear el sitio de Hola en cualquier lenguaje que devuelve las respuestas HTTP; en este tema se da por supuesto que va a hospedar Hola URL en una página JSP.</span><span class="sxs-lookup"><span data-stu-id="1b92c-182">You can create hello site in any language that returns HTTP responses; this topic assumes you'll be hosting hello URL in a JSP page.</span></span>

<span data-ttu-id="1b92c-183">Hola siguiendo los resultados de la página JSP en una respuesta de TwiML que dice **Hola a todos!**</span><span class="sxs-lookup"><span data-stu-id="1b92c-183">hello following JSP page results in a TwiML response that says **Hello World!**</span></span> <span data-ttu-id="1b92c-184">en la llamada Hola.</span><span class="sxs-lookup"><span data-stu-id="1b92c-184">on hello call.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="1b92c-185">Hola siguiendo los resultados de la página JSP en una respuesta de TwiML que indica algún texto, que tiene varias pausas y dice información acerca de la versión de la API de Twilio de Hola y el nombre de rol de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b92c-185">hello following JSP page results in a TwiML response that says some text, has several pauses, and says information about hello Twilio API version and hello Azure role name.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>hello Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>hello Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

<span data-ttu-id="1b92c-186">Hola **el elemento ApiVersion** parámetro está disponible en las solicitudes de voz de Twilio (no las solicitudes SMS).</span><span class="sxs-lookup"><span data-stu-id="1b92c-186">hello **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span></span> <span data-ttu-id="1b92c-187">parámetros de solicitud disponible toosee Hola de voz de Twilio y solicitudes SMS, consulte <https://www.twilio.com/docs/api/twiml/twilio_request> y <https://www.twilio.com/docs/api/twiml/sms/twilio_request >, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="1b92c-187">toosee hello available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span></span> <span data-ttu-id="1b92c-188">Hola **RoleName** variable de entorno está disponible como parte de una implementación de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b92c-188">hello **RoleName** environment variable is available as part of an Azure deployment.</span></span> <span data-ttu-id="1b92c-189">(Si desea que las variables de entorno personalizado tooadd por lo que puede seleccionar de **System.getenv**, vea la sección de las variables de entorno de hello en [varios valores de configuración de rol] [misc_role_config_settings].)</span><span class="sxs-lookup"><span data-stu-id="1b92c-189">(If you want tooadd custom environment variables so they could be picked up from **System.getenv**, see hello environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span></span>

<span data-ttu-id="1b92c-190">Una vez que tenga la página JSP configurar tooprovide TwiML respuestas, use la dirección URL de Hola de página JSP hello como Hola dirección URL pasada en hello **Call.creator** método.</span><span class="sxs-lookup"><span data-stu-id="1b92c-190">Once you have your JSP page set up tooprovide TwiML responses, use hello URL of hello JSP page as hello URL passed into hello **Call.creator** method.</span></span> <span data-ttu-id="1b92c-191">Por ejemplo, si tiene una aplicación Web denominado MyTwiML implementa tooan servicio hospedado de Azure y Hola de página JSP Hola se denomina mytwiml.jsp, se puede pasar Hola URL demasiado**Call.creator** tal y como se muestra en hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="1b92c-191">For example, if you have a Web application named MyTwiML deployed tooan Azure hosted service, and hello name of hello JSP page is mytwiml.jsp, hello URL can be passed too**Call.creator** as shown in hello following:</span></span>

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="1b92c-192">Otra opción para responder con TwiML es a través de hello **VoiceResponse** (clase), que está disponible en hello **com.twilio.twiml** paquete.</span><span class="sxs-lookup"><span data-stu-id="1b92c-192">Another option for responding with TwiML is via hello **VoiceResponse** class, which is available in hello **com.twilio.twiml** package.</span></span>

<span data-ttu-id="1b92c-193">Para obtener información adicional acerca del uso de Twilio en Azure con Java, consulte [cómo tooMake una llamada de teléfono uso de Twilio en una aplicación de Java en Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="1b92c-193">For additional information about using Twilio in Azure with Java, see [How tooMake a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="1b92c-194"><a id="AdditionalServices"></a>Procedimientos: Uso de servicios Twilio adicionales</span><span class="sxs-lookup"><span data-stu-id="1b92c-194"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="1b92c-195">Además toohello ejemplos que se muestran aquí, que twilio ofrece API basadas en web que puede usar la funcionalidad adicional de Twilio de tooleverage desde su aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b92c-195">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="1b92c-196">Para obtener información detallada, vea hello [documentación de la API de Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="1b92c-196">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="1b92c-197"><a id="NextSteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1b92c-197"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="1b92c-198">Ahora que ha aprendido conceptos básicos de Hola de hello Twilio servicio, siga estos toolearn de vínculos más:</span><span class="sxs-lookup"><span data-stu-id="1b92c-198">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="1b92c-199">[Directrices de seguridad de Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="1b92c-199">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="1b92c-200">[Procedimientos y código de ejemplo de Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="1b92c-200">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="1b92c-201">[Tutoriales de inicio rápido de Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="1b92c-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="1b92c-202">[Twilio en GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="1b92c-202">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="1b92c-203">[Hable tooTwilio soporte técnico][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="1b92c-203">[Talk tooTwilio Support][twilio_support]</span></span>

[twilio_java]: https://github.com/twilio/twilio-java
[twilio_api_service]: https://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[howto_phonecall_java]: partner-twilio-java-phone-call-example.md
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World%21
[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls
[twilio_rest_sending_sms]: http://www.twilio.com/docs/api/rest/sending-sms
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/docs
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
