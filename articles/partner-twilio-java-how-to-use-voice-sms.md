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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a>Cómo tooUse Twilio para voz y capacidades de SMS en Java
Esta guía demuestra cómo tooperform las tareas de programación habituales con hello Twilio API de servicio en Azure. escenarios de Hello descritos incluyen realizando una llamada telefónica y enviar un mensaje de servicio de mensajes cortos (SMS). Para obtener más información sobre Twilio y el uso de voz y SMS en las aplicaciones, vea hello [pasos](#NextSteps) sección.

## <a id="WhatIs"></a>¿Qué es Twilio?
Twilio es una API de servicio web de telefonía que permite utilizar los lenguajes web existentes y voz toobuild de conocimientos y las aplicaciones de SMS. Twilio es un servicio de terceros (no una característica de Azure ni tampoco un producto de Microsoft).

**Voz Twilio** permite la toomake de las aplicaciones y recibir llamadas telefónicas. **Twilio SMS** permite la toomake de las aplicaciones y recibir mensajes SMS. **Cliente de Twilio** permite que las aplicaciones con las conexiones de Internet existentes, incluidas las conexiones móviles tooenable la comunicación de voz.

## <a id="Pricing"></a>Precios de Twilio y ofertas especiales
Puede encontrar información sobre los precios de Twilio en [Precios de Twilio][twilio_pricing]. Los clientes de Azure reciben una [oferta especial][special_offer]: 1000 mensajes o 1000 minutos para llamar totalmente gratuitos. toosign hacia arriba para esta oferta u obtener más información, visite [http://ahoy.twilio.com/azure][special_offer].

## <a id="Concepts"></a>Conceptos
Hola Twilio API es una API de REST que proporciona funciones SMS y voz para las aplicaciones. Las bibliotecas de cliente están disponibles en varios lenguajes; para ver una lista, consulte las [bibliotecas de API de Twilio][twilio_libraries].

Aspectos clave de hello Twilio API son verbos de Twilio y lenguaje de marcado de Twilio (TwiML).

### <a id="Verbs"></a>Verbos de Twilio
Hola API hace que el uso de Twilio verbos; Por ejemplo, hello  **&lt;decir&gt;**  verbo indica Twilio tooaudibly entregar un mensaje en una llamada.

Hola aquí te mostramos una lista de verbos de Twilio.

* **&lt;Acceso telefónico&gt;**: conecta tooanother teléfono de hello llamador.
* **&lt;Recopilar&gt;**: recopila los dígitos numéricos del teclado del teléfono de Hola.
* **&lt;Hangup&gt;**: finaliza una llamada.
* **&lt;Play&gt;**: reproduce un archivo de audio.
* **&lt;Cola&gt;**: agregar hello tooa cola de los llamadores.
* **&lt;Pause&gt;**: espera en silencio una cantidad de segundos específica.
* **&lt;Registro&gt;**: registra la voz del llamador de Hola y devuelve una dirección URL de un archivo que contenga una grabación de Hola.
* **&lt;Redirigir&gt;**: transfiere el control de una llamada o SMS toohello TwiML en una dirección URL diferente.
* **&lt;Rechazar&gt;**: rechaza una entrada llame al número de Twilio de tooyour sin facturación.
* **&lt;Diga&gt;**: convierte texto toospeech que se realiza en una llamada.
* **&lt;Sms&gt;**: envía un mensaje SMS.

### <a id="TwiML"></a>TwiML
TwiML es un conjunto de instrucciones basado en XML en función de los verbos de Twilio de Hola que informan de Twilio de cómo tooprocess una llamada o SMS.

Por ejemplo, hello después TwiML convertiría texto hello **Hola a todos!** toospeech.

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

Cuando la aplicación llama hello Twilio API, uno de los parámetros de la API de hello es dirección URL de Hola que devuelve la respuesta de TwiML Hola. Para fines de desarrollo, puede utilizar direcciones URL siempre Twilio tooprovide hello TwiML las respuestas que usan las aplicaciones. También puede hospedar sus respuestas de las direcciones URL tooproduce hello TwiML y otra opción es hello toouse **TwiMLResponse** objeto.

Para obtener más información sobre los verbos de Twilio, sus atributos y TwiML, consulte [TwiML][twiml]. Para obtener información adicional acerca de hello Twilio API, consulte [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Creación de una cuenta de Twilio
Cuando esté listo tooget una cuenta de Twilio, regístrese en [intente Twilio][try_twilio]. Puede empezar con una cuenta gratuita y, posteriormente, actualizarla.

Cuando se registre para obtener una cuenta de Twilio, recibirá un identificador de cuenta y un token de autenticación. Ambos serán llamadas a la API de Twilio toomake necesarios. tooprevent no autorizado obtenga acceso a cuenta tooyour, proteger el token de autenticación. El identificador de cuenta y la autenticación de token están visibles en hello [Twilio consola][twilio_console], en Hola campos con la etiqueta **SID de cuenta** y **delTOKENdeautenticación**, respectivamente.

## <a id="create_app"></a>Creación de una aplicación Java
1. Obtener Hola JAR de Twilio y agréguelo tooyour ruta de acceso y el ensamblado de implementación WAR de compilación de Java. En [https://github.com/twilio/twilio-java][twilio_java], puede descargar los orígenes de GitHub de Hola y crear su propios JAR o descargar un archivo JAR pregenerado (con o sin dependencias).
2. Asegúrese del JDK **cacerts** almacén de claves contiene el certificado de entidad de certificación seguros Equifax Hola con 67:CB:9 de huella digital MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (número de serie de hello es hello SHA1 y 35:DE:F4:CF huella digital es D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A). Se trata de certificado de entidad emisora (CA) de certificado de Hola para hello [https://api.twilio.com] [ twilio_api_service] servicio, que se llama cuando se usa Twilio APIs. Para obtener información acerca de cómo garantizar el JDK **cacerts** almacén de claves contiene el certificado de entidad emisora de certificados correcto de hello, consulte [agregar un almacén de certificados de entidad emisora de certificados de Java de certificado toohello][add_ca_cert].

Instrucciones detalladas para usar la biblioteca de cliente de Twilio de Hola para Java están disponibles en [cómo tooMake una llamada de teléfono uso de Twilio en una aplicación de Java en Azure][howto_phonecall_java].

## <a id="configure_app"></a>Configurar las bibliotecas de Twilio de tooUse de la aplicación
Dentro del código, puede agregar **importar** las instrucciones en la parte superior de Hola de los archivos de origen para hello Twilio paquetes o clases desea toouse en la aplicación.

Para archivos de origen de Java:

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

Para archivos de origen de Java Server Page (JSP).

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
Dependiendo de los paquetes de Twilio o clases desea toouse, su **importar** instrucciones pueden ser diferentes.

## <a id="howto_make_call"></a>Realización de una llamada saliente
Hello siguiente muestra cómo toomake una salida llamar a utilizando hello **llamar** clase. Este código también usa un Hola de tooreturn sitio proporcionado Twilio respuesta de lenguaje de marcado de Twilio (TwiML). Sustituya los valores de hello **de** y **a** los números de teléfono y asegúrese de comprobar hello **de** número de teléfono para el código de hello Twilio cuenta toorunning anterior.

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

Para obtener más información acerca de los parámetros de hello pasado toohello **Call.creator** método, consulte [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].

Como se ha mencionado, este código usa un Hola de tooreturn sitio proporcionado Twilio TwiML respuesta. En su lugar, podría utilizar su propio Hola de tooprovide sitio respuesta TwiML; Para obtener más información, consulte [cómo tooProvide las respuestas de TwiML en una aplicación de Java en Azure](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Envío de un mensaje SMS
Hello siguiente muestra cómo toosend un mensaje SMS con Hola **mensaje** clase. Hola **de** número, **4155992671**, se proporciona por Twilio para cuentas de prueba toosend mensajes SMS. Hola **a** número debe comprobarse para el código de hello Twilio cuenta toorunning anterior.

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

Para obtener más información acerca de los parámetros de hello pasado toohello **Message.creator** método, consulte [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].

## <a id="howto_provide_twiml_responses"></a>Entrega de respuestas de TwiML desde su propio sitio web
Cuando la aplicación inicia una toohello llamada API de Twilio, por ejemplo a través de hello **CallCreator.create** método Twilio enviará su dirección de URL de solicitud tooa que es tooreturn esperado una respuesta TwiML. ejemplo de Hola anterior utiliza dirección URL proporcionada Twilio por hello [http://twimlets.com/message][twimlet_message_url]. (Aunque TwiML está diseñado para su uso por los servicios Web, puede ver hello TwiML en el explorador. Por ejemplo, haga clic en [http://twimlets.com/message] [ twimlet_message_url] toosee vacío  **&lt;respuesta&gt;**  elemento; como otro ejemplo, haga clic en [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee una  **&lt;respuesta&gt;**  elemento que contiene un  **&lt;decir &gt;**  elemento.)

En lugar de basarse en la dirección URL proporcionada Twilio por hello, puede crear su propio sitio de dirección URL que devuelve las respuestas HTTP. Puede crear el sitio de Hola en cualquier lenguaje que devuelve las respuestas HTTP; en este tema se da por supuesto que va a hospedar Hola URL en una página JSP.

Hola siguiendo los resultados de la página JSP en una respuesta de TwiML que dice **Hola a todos!** en la llamada Hola.

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

Hola siguiendo los resultados de la página JSP en una respuesta de TwiML que indica algún texto, que tiene varias pausas y dice información acerca de la versión de la API de Twilio de Hola y el nombre de rol de Azure de Hola.

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

Hola **el elemento ApiVersion** parámetro está disponible en las solicitudes de voz de Twilio (no las solicitudes SMS). parámetros de solicitud disponible toosee Hola de voz de Twilio y solicitudes SMS, consulte <https://www.twilio.com/docs/api/twiml/twilio_request> y <https://www.twilio.com/docs/api/twiml/sms/twilio_request >, respectivamente. Hola **RoleName** variable de entorno está disponible como parte de una implementación de Azure. (Si desea que las variables de entorno personalizado tooadd por lo que puede seleccionar de **System.getenv**, vea la sección de las variables de entorno de hello en [varios valores de configuración de rol] [misc_role_config_settings].)

Una vez que tenga la página JSP configurar tooprovide TwiML respuestas, use la dirección URL de Hola de página JSP hello como Hola dirección URL pasada en hello **Call.creator** método. Por ejemplo, si tiene una aplicación Web denominado MyTwiML implementa tooan servicio hospedado de Azure y Hola de página JSP Hola se denomina mytwiml.jsp, se puede pasar Hola URL demasiado**Call.creator** tal y como se muestra en hello siguiente:

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

Otra opción para responder con TwiML es a través de hello **VoiceResponse** (clase), que está disponible en hello **com.twilio.twiml** paquete.

Para obtener información adicional acerca del uso de Twilio en Azure con Java, consulte [cómo tooMake una llamada de teléfono uso de Twilio en una aplicación de Java en Azure][howto_phonecall_java].

## <a id="AdditionalServices"></a>Procedimientos: Uso de servicios Twilio adicionales
Además toohello ejemplos que se muestran aquí, que twilio ofrece API basadas en web que puede usar la funcionalidad adicional de Twilio de tooleverage desde su aplicación de Azure. Para obtener información detallada, vea hello [documentación de la API de Twilio][twilio_api_documentation].

## <a id="NextSteps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de hello Twilio servicio, siga estos toolearn de vínculos más:

* [Directrices de seguridad de Twilio][twilio_security_guidelines]
* [Procedimientos y código de ejemplo de Twilio][twilio_howtos]
* [Tutoriales de inicio rápido de Twilio][twilio_quickstarts]
* [Twilio en GitHub][twilio_on_github]
* [Hable tooTwilio soporte técnico][twilio_support]

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
