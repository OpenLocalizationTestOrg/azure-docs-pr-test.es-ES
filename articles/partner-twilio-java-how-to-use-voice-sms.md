---
title: Uso de Twilio para voz y SMS (Java) | Microsoft Docs
description: "Aprenda a realizar llamadas telefónicas y a enviar mensajes SMS con el servicio de la API de Twilio en Azure. Ejemplos de código escritos en Java."
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
ms.openlocfilehash: 5a1b2ffa160a31b639605242b651dc8d14e7a01b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-java"></a><span data-ttu-id="dd073-104">Uso de Twilio para capacidades de voz y SMS en Java</span><span class="sxs-lookup"><span data-stu-id="dd073-104">How to Use Twilio for Voice and SMS Capabilities in Java</span></span>
<span data-ttu-id="dd073-105">Esta guía describe cómo realizar tareas comunes de programación con el servicio de API de Twilio en Azure.</span><span class="sxs-lookup"><span data-stu-id="dd073-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="dd073-106">Entre los escenarios descritos se incluyen realizar una llamada telefónica y enviar un mensaje de servicio de mensajes cortos (SMS).</span><span class="sxs-lookup"><span data-stu-id="dd073-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="dd073-107">Para obtener más información sobre Twilio y el uso de voz y mensajes SMS en sus aplicaciones, consulte la sección [Pasos siguientes](#NextSteps) .</span><span class="sxs-lookup"><span data-stu-id="dd073-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="dd073-108"><a id="WhatIs"></a>¿Qué es Twilio?</span><span class="sxs-lookup"><span data-stu-id="dd073-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="dd073-109">Twilio es una API de servicio web de telefonía que le permite utilizar las habilidades y lenguajes web existentes para crear aplicaciones de voz y SMS.</span><span class="sxs-lookup"><span data-stu-id="dd073-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="dd073-110">Twilio es un servicio de terceros (no una característica de Azure ni tampoco un producto de Microsoft).</span><span class="sxs-lookup"><span data-stu-id="dd073-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="dd073-111">**Twilio Voice** permite que sus aplicaciones realicen y reciban llamadas.</span><span class="sxs-lookup"><span data-stu-id="dd073-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="dd073-112">**Twilio SMS** permite que sus aplicaciones envíen y reciban mensajes SMS.</span><span class="sxs-lookup"><span data-stu-id="dd073-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="dd073-113">**Twilio Client** permite que sus aplicaciones habiliten la comunicación por voz a través de conexiones existentes a Internet, incluidas las conexiones móviles.</span><span class="sxs-lookup"><span data-stu-id="dd073-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="dd073-114"><a id="Pricing"></a>Precios de Twilio y ofertas especiales</span><span class="sxs-lookup"><span data-stu-id="dd073-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="dd073-115">Puede encontrar información sobre los precios de Twilio en [Precios de Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="dd073-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="dd073-116">Los clientes de Azure reciben una [oferta especial][special_offer]: 1000 mensajes o 1000 minutos para llamar totalmente gratuitos.</span><span class="sxs-lookup"><span data-stu-id="dd073-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="dd073-117">Para registrarse y obtener esta oferta o para recibir más información, visite [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="dd073-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>

## <span data-ttu-id="dd073-118"><a id="Concepts"></a>Conceptos</span><span class="sxs-lookup"><span data-stu-id="dd073-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="dd073-119">La API de Twilio es una API de RESTful que proporciona funciones de voz y SMS para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="dd073-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="dd073-120">Las bibliotecas de cliente están disponibles en varios lenguajes; para ver una lista, consulte las [bibliotecas de API de Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="dd073-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="dd073-121">Aspectos fundamentales de la API de Twilio son los verbos de Twilio y el lenguaje de marcado de Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="dd073-121">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="dd073-122"><a id="Verbs"></a>Verbos de Twilio</span><span class="sxs-lookup"><span data-stu-id="dd073-122"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="dd073-123">La API usa dos verbos de Twilio; por ejemplo, el verbo **&lt;Say&gt;** indica a Twilio que entregue de manera audible un mensaje en una llamada.</span><span class="sxs-lookup"><span data-stu-id="dd073-123">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="dd073-124">A continuación se presenta una lista de verbos de Twilio.</span><span class="sxs-lookup"><span data-stu-id="dd073-124">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="dd073-125">**&lt;Dial&gt;**: conecta la persona que llama con otro teléfono.</span><span class="sxs-lookup"><span data-stu-id="dd073-125">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="dd073-126">**&lt;Gather&gt;**: recopila los dígitos numéricos que se introdujeron en el teclado del teléfono.</span><span class="sxs-lookup"><span data-stu-id="dd073-126">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="dd073-127">**&lt;Hangup&gt;**: finaliza una llamada.</span><span class="sxs-lookup"><span data-stu-id="dd073-127">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="dd073-128">**&lt;Play&gt;**: reproduce un archivo de audio.</span><span class="sxs-lookup"><span data-stu-id="dd073-128">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="dd073-129">**&lt;Queue&gt;**: agregar a una cola de personas que llaman.</span><span class="sxs-lookup"><span data-stu-id="dd073-129">**&lt;Queue&gt;**: Add the to a queue of callers.</span></span>
* <span data-ttu-id="dd073-130">**&lt;Pause&gt;**: espera en silencio una cantidad de segundos específica.</span><span class="sxs-lookup"><span data-stu-id="dd073-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="dd073-131">**&lt;Record&gt;**: graba la voz de la persona que llama y devuelve una dirección URL de un archivo que contiene la grabación.</span><span class="sxs-lookup"><span data-stu-id="dd073-131">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="dd073-132">**&lt;Redirect&gt;**: transfiere el control de una llamada o SMS al TwiML en una URL diferente.</span><span class="sxs-lookup"><span data-stu-id="dd073-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="dd073-133">**&lt;Reject&gt;**: rechaza una llamada entrante al número de Twilio sin cobrarle.</span><span class="sxs-lookup"><span data-stu-id="dd073-133">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you.</span></span>
* <span data-ttu-id="dd073-134">**&lt;Say&gt;**: convierte texto en voz para hacer una llamada.</span><span class="sxs-lookup"><span data-stu-id="dd073-134">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="dd073-135">**&lt;Sms&gt;**: envía un mensaje SMS.</span><span class="sxs-lookup"><span data-stu-id="dd073-135">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="dd073-136"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="dd073-136"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="dd073-137">TwiML es un conjunto de instrucciones basadas en XML y en los verbos de Twilio que informan a Twilio sobre cómo procesar una llamada o un SMS.</span><span class="sxs-lookup"><span data-stu-id="dd073-137">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="dd073-138">Como ejemplo, el siguiente TwiML convierte el texto **Hello World**</span><span class="sxs-lookup"><span data-stu-id="dd073-138">As an example, the following TwiML would convert the text **Hello World!**</span></span> <span data-ttu-id="dd073-139">en voz.</span><span class="sxs-lookup"><span data-stu-id="dd073-139">to speech.</span></span>

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="dd073-140">Cuando su aplicación llama a la API de Twilio, uno de los parámetros de API es la URL que devuelve la respuesta de TwiML.</span><span class="sxs-lookup"><span data-stu-id="dd073-140">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="dd073-141">Con fines de desarrollo, puede usar las URL que ofrece Twilio para proporcionar las respuestas de TwiML que usaron sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="dd073-141">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="dd073-142">También puede hospedar sus propias URL para producir las repuestas de TwiML; otra opción es usar el objeto **TwiMLResponse** .</span><span class="sxs-lookup"><span data-stu-id="dd073-142">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="dd073-143">Para obtener más información sobre los verbos de Twilio, sus atributos y TwiML, consulte [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="dd073-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="dd073-144">Para obtener información adicional sobre la API de Twilio, consulte la [API de Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="dd073-144">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="dd073-145"><a id="CreateAccount"></a>Creación de una cuenta de Twilio</span><span class="sxs-lookup"><span data-stu-id="dd073-145"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="dd073-146">Cuando esté preparado para obtener una cuenta de Twilio, regístrese en la página de [evaluación de Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="dd073-146">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="dd073-147">Puede empezar con una cuenta gratuita y, posteriormente, actualizarla.</span><span class="sxs-lookup"><span data-stu-id="dd073-147">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="dd073-148">Cuando se registre para obtener una cuenta de Twilio, recibirá un identificador de cuenta y un token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="dd073-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="dd073-149">Necesitará ambos para realizar llamadas a la API de Twilio.</span><span class="sxs-lookup"><span data-stu-id="dd073-149">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="dd073-150">Para evitar el acceso no autorizado a su cuenta, mantenga protegido el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="dd073-150">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="dd073-151">Puede ver el identificador de cuenta y el token de autenticación en la [Consola de Twilio][twilio_console], en los campos etiquetados como **ACCOUNT SID** y **AUTH TOKEN**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="dd073-151">Your account ID and authentication token are viewable at the [Twilio Console][twilio_console], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="dd073-152"><a id="create_app"></a>Creación de una aplicación Java</span><span class="sxs-lookup"><span data-stu-id="dd073-152"><a id="create_app"></a>Create a Java Application</span></span>
1. <span data-ttu-id="dd073-153">Obtenga el archivo JAR de Twilio y agréguelo a su ruta de acceso de compilación de Java y a su ensamblado de implementación de WAR.</span><span class="sxs-lookup"><span data-stu-id="dd073-153">Obtain the Twilio JAR and add it to your Java build path and your WAR deployment assembly.</span></span> <span data-ttu-id="dd073-154">En [https://github.com/twilio/twilio-java][twilio_java] puede descargar el código fuente de GitHub y crear su propio archivo JAR, o bien puede descargar un archivo JAR previamente generado (con o sin dependencias).</span><span class="sxs-lookup"><span data-stu-id="dd073-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download the GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
2. <span data-ttu-id="dd073-155">Asegúrese de que el almacén (KeyStore) de **cacerts** de JDK contiene el certificado de la entidad de certificación Equifax Secure con la huella digital MD5 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (el número de serie es 35:DE:F4:CF y la huella digital SHA1 es D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="dd073-155">Ensure your JDK's **cacerts** keystore contains the Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (the serial number is 35:DE:F4:CF and the SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="dd073-156">Este es el certificado de la entidad de certificación (CA) para el servicio [https://api.twilio.com][twilio_api_service], al que se llama cuando se usan las API de Twilio.</span><span class="sxs-lookup"><span data-stu-id="dd073-156">This is the certificate authority (CA) certificate for the [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="dd073-157">Para obtener información sobre cómo asegurarse de que el almacén de claves de **cacerts** del JDK contiene el certificado de entidad de certificación correcto, vea [Incorporación de un certificado al almacén de certificados CA de Java][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="dd073-157">For information about ensuring your JDK's **cacerts** keystore contains the correct CA certificate, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="dd073-158">Puede obtener instrucciones detalladas sobre el uso de la biblioteca de cliente de Twilio para Java en [Realización de una llamada telefónica con Twilio en una aplicación Java en Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="dd073-158">Detailed instructions for using the Twilio client library for Java are available at [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="dd073-159"><a id="configure_app"></a>Configuración de la aplicación para usar bibliotecas de Twilio</span><span class="sxs-lookup"><span data-stu-id="dd073-159"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="dd073-160">Dentro de su código, puede agregar instrucciones **import** en la parte superior de los archivos de origen para las clases o paquetes de Twilio que desea utilizar en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd073-160">Within your code, you can add **import** statements at the top of your source files for the Twilio packages or classes you want to use in your application.</span></span>

<span data-ttu-id="dd073-161">Para archivos de origen de Java:</span><span class="sxs-lookup"><span data-stu-id="dd073-161">For Java source files:</span></span>

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

<span data-ttu-id="dd073-162">Para archivos de origen de Java Server Page (JSP).</span><span class="sxs-lookup"><span data-stu-id="dd073-162">For Java Server Page (JSP) source files:</span></span>

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
<span data-ttu-id="dd073-163">Dependiendo del paquete o la clase de Twilio que desee utilizar, las instrucciones **import** pueden ser distintas.</span><span class="sxs-lookup"><span data-stu-id="dd073-163">Depending on which Twilio packages or classes you want to use, your **import** statements may be different.</span></span>

## <span data-ttu-id="dd073-164"><a id="howto_make_call"></a>Realización de una llamada saliente</span><span class="sxs-lookup"><span data-stu-id="dd073-164"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="dd073-165">A continuación se indica cómo realizar una llamada saliente con la clase **Call**.</span><span class="sxs-lookup"><span data-stu-id="dd073-165">The following shows how to make an outgoing call using the **Call** class.</span></span> <span data-ttu-id="dd073-166">Este código también utiliza un sitio que proporciona Twilio para devolver la respuesta de lenguaje de marcado de Twilio (TwiML).</span><span class="sxs-lookup"><span data-stu-id="dd073-166">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="dd073-167">Sustituya los valores de los números de teléfono **from** y **to**, y asegúrese de comprobar el número de teléfono **from** de la cuenta de Twilio antes de ejecutar el código.</span><span class="sxs-lookup"><span data-stu-id="dd073-167">Substitute your values for the **from** and **to** phone numbers, and ensure that you verify the **from** phone number for your Twilio account prior to running the code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize the Twilio client.
    Twilio.init(accountSID, authToken);

    // Use the Twilio-provided site for the TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare To and From numbers
    PhoneNumber to = new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, To and URL values
    // then make the call by executing the create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="dd073-168">Para más información sobre los parámetros transmitidos al método **Call.creator**, vea [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="dd073-168">For more information about the parameters passed in to the **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="dd073-169">Como se mencionó, este código usa el sitio proporcionado por Twilio para devolver la respuesta de TwiML.</span><span class="sxs-lookup"><span data-stu-id="dd073-169">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="dd073-170">En lugar de lo anterior, podría utilizar su propio sitio web para proporcionar la respuesta de TwiML; si desea obtener más información, consulte [Procedimientos: Suministro de respuestas de TwiML desde su propio sitio web](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="dd073-170">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="dd073-171"><a id="howto_send_sms"></a>Envío de un mensaje SMS</span><span class="sxs-lookup"><span data-stu-id="dd073-171"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="dd073-172">A continuación se muestra cómo enviar un mensaje SMS con la clase **Message**.</span><span class="sxs-lookup"><span data-stu-id="dd073-172">The following shows how to send an SMS message using the **Message** class.</span></span> <span data-ttu-id="dd073-173">Twilio proporciona el número **from** **4155992671**, para que las cuentas de evaluación puedan enviar mensajes SMS.</span><span class="sxs-lookup"><span data-stu-id="dd073-173">The **from** number, **4155992671**, is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="dd073-174">El número **to** se debe comprobar en su cuenta de Twilio antes de ejecutar el código.</span><span class="sxs-lookup"><span data-stu-id="dd073-174">The **to** number must be verified for your Twilio account prior to running the code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize the Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare To and From numbers and the Body of the SMS message
    PhoneNumber to = new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, To and Body values
    // then send the SMS message by calling the create() method
    Message sms = Message.creator(to, from, body).create();
```

<span data-ttu-id="dd073-175">Para más información sobre los parámetros que se transmiten al método **Message.creator**, vea [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span><span class="sxs-lookup"><span data-stu-id="dd073-175">For more information about the parameters passed in to the **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span></span>

## <span data-ttu-id="dd073-176"><a id="howto_provide_twiml_responses"></a>Entrega de respuestas de TwiML desde su propio sitio web</span><span class="sxs-lookup"><span data-stu-id="dd073-176"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="dd073-177">Cuando la aplicación inicia una llamada a la API de Twilio, por ejemplo a través del método **CallCreator.create**, Twilio envía la solicitud a una dirección URL que debe devolver una respuesta de TwiML.</span><span class="sxs-lookup"><span data-stu-id="dd073-177">When your application initiates a call to the Twilio API, for example via the **CallCreator.create** method, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="dd073-178">El ejemplo anterior usa la dirección URL [http://twimlets.com/message][twimlet_message_url] proporcionada por Twilio.</span><span class="sxs-lookup"><span data-stu-id="dd073-178">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="dd073-179">Aun cuando TwiML está diseñado para que lo usen los servicios web, puede ver el TwiML en su explorador.</span><span class="sxs-lookup"><span data-stu-id="dd073-179">(While TwiML is designed for use by Web services, you can view the TwiML in your browser.</span></span> <span data-ttu-id="dd073-180">Por ejemplo, haga clic en [http://twimlets.com/message][twimlet_message_url] para ver un elemento **&lt;Response&gt;** vacío. Otro ejemplo: haga clic en [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] para ver un elemento **&lt;Response&gt;** que contiene un elemento **&lt;Say&gt;**).</span><span class="sxs-lookup"><span data-stu-id="dd073-180">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] to see a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span></span>

<span data-ttu-id="dd073-181">En lugar de confiar en la URL que Twilio proporciona, puede crear su propio sitio URL que devuelve procesos HTTP.</span><span class="sxs-lookup"><span data-stu-id="dd073-181">Instead of relying on the Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="dd073-182">Puede crear el sitio en cualquier lenguaje que devuelva respuestas HTTP; en este tema se asume que hospedará la URL en una página de JSP.</span><span class="sxs-lookup"><span data-stu-id="dd073-182">You can create the site in any language that returns HTTP responses; this topic assumes you'll be hosting the URL in a JSP page.</span></span>

<span data-ttu-id="dd073-183">La siguiente página JSP da como resultado una respuesta de TwiML que dice **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="dd073-183">The following JSP page results in a TwiML response that says **Hello World!**</span></span> <span data-ttu-id="dd073-184">en la llamada.</span><span class="sxs-lookup"><span data-stu-id="dd073-184">on the call.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="dd073-185">La siguiente página JSP resulta en una respuesta de TwiML que indica algún texto, tiene varias pausas y difunde información acerca de la versión de la API de Twilio y del nombre de rol de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd073-185">The following JSP page results in a TwiML response that says some text, has several pauses, and says information about the Twilio API version and the Azure role name.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>The Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>The Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

<span data-ttu-id="dd073-186">El parámetro **ApiVersion** está disponible en solicitudes de voz de Twilio (no en solicitudes de SMS).</span><span class="sxs-lookup"><span data-stu-id="dd073-186">The **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span></span> <span data-ttu-id="dd073-187">Para ver los parámetros de solicitud disponibles para solicitudes de voz y de SMS de Twilio, consulte <https://www.twilio.com/docs/api/twiml/twilio_request> y <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="dd073-187">To see the available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span></span> <span data-ttu-id="dd073-188">La variable de entorno **RoleName** está disponible como parte de una implementación de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd073-188">The **RoleName** environment variable is available as part of an Azure deployment.</span></span> <span data-ttu-id="dd073-189">(Si quiere agregar variables de entorno personalizadas para que se puedan elegir en **System.getenv**, vea la sección de variables de entorno en [Configuración de propiedades de roles de Azure][misc_role_config_settings]).</span><span class="sxs-lookup"><span data-stu-id="dd073-189">(If you want to add custom environment variables so they could be picked up from **System.getenv**, see the environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span></span>

<span data-ttu-id="dd073-190">Una vez configurada la página de JSP para proporcionar respuestas de TwiML, use la dirección URL de la página JSP como la dirección URL que se transmite al método **Call.creator**.</span><span class="sxs-lookup"><span data-stu-id="dd073-190">Once you have your JSP page set up to provide TwiML responses, use the URL of the JSP page as the URL passed into the **Call.creator** method.</span></span> <span data-ttu-id="dd073-191">Por ejemplo, si tiene una aplicación web llamada MyTwiML implementada en un servicio hospedado de Azure y el nombre de la página de JSP es mytwiml.jsp, la dirección URL se puede transmitir a **Call.creator** como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="dd073-191">For example, if you have a Web application named MyTwiML deployed to an Azure hosted service, and the name of the JSP page is mytwiml.jsp, the URL can be passed to **Call.creator** as shown in the following:</span></span>

```java
    // Declare To and From numbers and the URL of your JSP page
    PhoneNumber to = new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, To and URL values
    // then make the call by executing the create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="dd073-192">Otra opción para responder con TwiML es mediante la clase **VoiceResponse**, que está disponible en el paquete **com.twilio.twiml**.</span><span class="sxs-lookup"><span data-stu-id="dd073-192">Another option for responding with TwiML is via the **VoiceResponse** class, which is available in the **com.twilio.twiml** package.</span></span>

<span data-ttu-id="dd073-193">Para más información sobre cómo usar Twilio en Azure con Java, vea [Realización de una llamada telefónica con Twilio en una aplicación Java en Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="dd073-193">For additional information about using Twilio in Azure with Java, see [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="dd073-194"><a id="AdditionalServices"></a>Procedimientos: Uso de servicios Twilio adicionales</span><span class="sxs-lookup"><span data-stu-id="dd073-194"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="dd073-195">Además de los ejemplos aquí mostrados, Twilio ofrece API basadas en web que puede utilizar para aprovechar las funciones adicionales de Twilio desde su aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd073-195">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="dd073-196">Para obtener los detalles completos, vea la [Documentación de la API de Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="dd073-196">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="dd073-197"><a id="NextSteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dd073-197"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="dd073-198">Ahora que conoce los fundamentos del servicio Twilio, siga estos vínculos para obtener más información:</span><span class="sxs-lookup"><span data-stu-id="dd073-198">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="dd073-199">[Directrices de seguridad de Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="dd073-199">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="dd073-200">[Procedimientos y código de ejemplo de Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="dd073-200">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="dd073-201">[Tutoriales de inicio rápido de Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="dd073-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="dd073-202">[Twilio en GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="dd073-202">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="dd073-203">[Contactar con el servicio técnico de Twilio][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="dd073-203">[Talk to Twilio Support][twilio_support]</span></span>

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
