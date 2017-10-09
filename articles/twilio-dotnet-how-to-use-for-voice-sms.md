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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a>Cómo toouse Twilio para voz y capacidades SMS de Azure
Esta guía demuestra cómo tooperform las tareas de programación habituales con hello Twilio API de servicio en Azure. escenarios de Hello descritos incluyen realizando una llamada telefónica y enviar un mensaje de servicio de mensajes cortos (SMS). Para obtener más información sobre Twilio y el uso de voz y SMS en las aplicaciones, vea hello [pasos siguientes](#NextSteps) sección.

## <a id="WhatIs"></a>¿Qué es Twilio?
Twilio está activando Hola futuro de las comunicaciones empresariales, la habilitación de los desarrolladores tooembed voice, VoIP y en las aplicaciones de mensajería. Virtualizar toda la infraestructura necesarios en un entorno global, basada en la nube, exponerlo a través de la plataforma de hello API de comunicaciones de Twilio. Las aplicaciones son toobuild simple y escalable. Disfrute de la flexibilidad de pagar por lo que utiliza y aproveche la confiabilidad de la nube.

**Voz Twilio** permite la toomake de las aplicaciones y recibir llamadas telefónicas. **Twilio SMS** habilita la toosend de las aplicaciones y recibir mensajes SMS. **Cliente de Twilio** permite llamadas de VoIP toomake desde cualquier teléfono, una tableta o un explorador y es compatible con WebRTC.

## <a id="Pricing"></a>Precios de Twilio y ofertas especiales
Los clientes de Azure reciben una [oferta especial](http://www.twilio.com/azure): 10 $ de regalo en crédito Twilio al actualizar su cuenta Twilio. Este crédito Twilio puede ser aplicada tooany uso de Twilio (10 $ crédito equivalente toosending como máximo 1000 mensajes SMS o recibir una too1000 entrada minutos de voz, según la ubicación de Hola de su destino de número y el mensaje o la llamada de teléfono). Canjee este crédito Twilio y comience en [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).

Twilio es un servicio de pago por uso. No hay comisiones establecidas y puede cerrar su cuenta en cualquier momento. Puede encontrar más detalles en [Precios de Twilio](http://www.twilio.com/voice/pricing).

## <a id="Concepts"></a>Conceptos
Hola Twilio API es una API de REST que proporciona funciones SMS y voz para las aplicaciones. Las bibliotecas de cliente están disponibles en varios lenguajes; para ver una lista, consulte las [bibliotecas de API de Twilio][twilio_libraries].

Aspectos clave de hello Twilio API son verbos de Twilio y lenguaje de marcado de Twilio (TwiML).

### <a id="Verbs"></a>Verbos de Twilio
Hola API hace que el uso de Twilio verbos; Por ejemplo, hello  **&lt;decir&gt;**  verbo indica Twilio tooaudibly entregar un mensaje en una llamada.

Hola aquí te mostramos una lista de verbos de Twilio.  Obtenga información acerca de Hola unos a otros verbos y capacidades a través de [documentación del lenguaje de marcado de Twilio](http://www.twilio.com/docs/api/twiml).

* **&lt;Acceso telefónico&gt;**: conecta tooanother teléfono de hello llamador.
* **&lt;Recopilar&gt;**: recopila los dígitos numéricos del teclado del teléfono de Hola.
* **&lt;Hangup&gt;**: finaliza una llamada.
* **&lt;Play&gt;**: reproduce un archivo de audio.
* **&lt;Pause&gt;**: espera en silencio una cantidad de segundos específica.
* **&lt;Registro&gt;**: registra la voz del llamador de Hola y devuelve una dirección URL de un archivo que contenga una grabación de Hola.
* **&lt;Redirigir&gt;**: transfiere el control de una llamada o SMS toohello TwiML en una dirección URL diferente.
* **&lt;Rechazar&gt;**: rechaza una entrada llame al número de Twilio de tooyour sin facturación
* **&lt;Diga&gt;**: convierte texto toospeech que se realiza en una llamada.
* **&lt;Sms&gt;**: envía un mensaje SMS.

### <a id="TwiML"></a>TwiML
TwiML es un conjunto de instrucciones basado en XML en función de los verbos de Twilio de Hola que informan de Twilio de cómo tooprocess una llamada o SMS.

Por ejemplo, hello después TwiML convertiría texto hello **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

Cuando la aplicación llama hello Twilio API, uno de los parámetros de la API de hello es dirección URL de Hola que devuelve la respuesta de TwiML Hola. Para fines de desarrollo, puede utilizar direcciones URL siempre Twilio tooprovide hello TwiML las respuestas que usan las aplicaciones. También puede hospedar sus respuestas de las direcciones URL tooproduce hello TwiML y otra opción es hello toouse **TwiMLResponse** objeto.

Para obtener más información sobre los verbos de Twilio, sus atributos y TwiML, consulte [TwiML][twiml]. Para obtener información adicional acerca de hello Twilio API, consulte [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Creación de una cuenta de Twilio
Cuando esté listo tooget una cuenta de Twilio, regístrese en [intente Twilio][try_twilio]. Puede empezar con una cuenta gratuita y, posteriormente, actualizarla.

Cuando se registre para obtener una cuenta de Twilio, recibirá un identificador de cuenta y un token de autenticación. Ambos serán llamadas a la API de Twilio toomake necesarios. tooprevent no autorizado obtenga acceso a cuenta tooyour, proteger el token de autenticación. El identificador de cuenta y la autenticación de token están visibles en hello [página de la cuenta de Twilio][twilio_account], en Hola campos con la etiqueta **SID de cuenta** y **delTOKENdeautenticación**, respectivamente.

## <a id="create_app"></a>Creación de una aplicación de Azure
Una aplicación de Azure que hospeda una aplicación habilitada para Twilio no es diferente de ninguna otra aplicación de Azure. Agregar la biblioteca de .NET de Twilio de Hola y configurar las bibliotecas .NET de Twilio de hello rol toouse Hola.
Para obtener información sobre la creación de un proyecto inicial de Azure, consulte [Creación de un proyecto de Azure en Visual Studio][vs_project].

## <a id="configure_app"></a>Configurar las bibliotecas de Twilio de toouse de la aplicación
Twilio proporciona un conjunto de bibliotecas de aplicación auxiliar de .NET que contienen distintos aspectos de Twilio tooprovide formas sencillas y simple toointeract con hello API de REST de Twilio y cliente de Twilio toogenerate TwiML respuestas.

Twilio proporciona cinco bibliotecas para desarrolladores de .NET:
Biblioteca|Descripción
---|---
Twilio.API|Hola biblioteca principal de Twilio que ajusta Hola API de REST de Twilio en una biblioteca de .NET descriptiva. Esta biblioteca está disponible para .NET, Silverlight y Windows Phone 7.
Twilio.TwiML|Proporciona una marca de TwiML .NET toogenerate de manera fácil de usar.
Twilio.MVC|Para los desarrolladores que usan ASP.NET MVC, esta biblioteca incluye un atributo TwilioController, TwiML ActionResult y de validación de solicitudes.
Twilio.WebMatrix|Para los desarrolladores que usan la herramienta de desarrollo WebMatrix gratuita de Microsoft, esta biblioteca contiene aplicaciones auxiliares de sintaxis Razor para diversas acciones de Twilio.
Twilio.Client.Capability|Contiene el generador de símbolo (token) de capacidad de Hola para su uso con hello SDK de JavaScript de cliente de Twilio.

Tenga en cuenta que todas las bibliotecas requieren .NET 3.5, Silverlight 4 o Windows Phone 7 o posterior.

ejemplos de Hello proporcionados en esta guía usan biblioteca de Twilio.API Hola.

pueden ser bibliotecas de Hello [instalado mediante la extensión del Administrador de paquetes de NuGet de hello](http://www.twilio.com/docs/csharp/install) disponible para Visual Studio 2010 activo too2015.  código fuente Hello se hospeda una en [GitHub][twilio_github_repo], que incluye una Wiki que contiene la documentación completa para el uso de bibliotecas de Hola.

De manera predeterminada, Microsoft Visual Studio 2010 instala la versión 1.2 de NuGet. Instalar bibliotecas de Twilio de hello requiere la versión 1.6 de NuGet o superior. Para obtener información sobre la instalación o actualización de NuGet, consulte [http://nuget.org/][nuget].

> [!NOTE]
> tooinstall Hola última versión de NuGet, primero debe desinstalar Hola versión cargada mediante Hola Administrador de extensiones de Visual Studio. toodo por lo tanto, debe ejecutar Visual Studio como administrador. En caso contrario, botón de desinstalación de hello está deshabilitado.
>
>

### <a id="use_nuget"></a>proyecto de Visual Studio tooyour: de tooadd hello Twilio bibliotecas
1. Abra su solución en Visual Studio.
2. Haga clic con el botón secundario en **Referencias**.
3. Haga clic en **Administrar paquetes de NuGet...**
4. Haga clic en **En línea**.
5. En el cuadro en línea de la búsqueda de hello, escriba *twilio*.
6. Haga clic en **instalar** en el paquete de Twilio Hola.

## <a id="howto_make_call"></a>Realización de una llamada saliente
Hello siguiente muestra cómo toomake una salida llamar a utilizando hello **CallResource** clase. Este código también usa un Hola de tooreturn sitio proporcionado Twilio respuesta de lenguaje de marcado de Twilio (TwiML). Sustituya los valores de hello **a** y **de** los números de teléfono y asegúrese de comprobar hello **de** número de teléfono para su cuenta de Twilio antes de ejecutar código de hello.

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

Para obtener más información acerca de los parámetros de hello pasado toohello **CallResource.Create** método, consulte [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].

Como se ha mencionado, este código usa un Hola de tooreturn sitio proporcionado Twilio TwiML respuesta. En su lugar puede utilizar su propio Hola de tooprovide sitio TwiML respuesta. Para más información, consulte [Entrega de respuestas de TwiML desde su propio sitio web](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Envío de un mensaje SMS
Hello captura de pantalla siguiente muestra cómo toosend un mensaje SMS con Hola **MessageResource** clase. Hola **de** Twilio proporciona número para cuentas de prueba toosend mensajes SMS. Hola **a** número debe ser verificado para su cuenta de Twilio antes de ejecutar código de hello.

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

## <a id="howto_provide_twiml_responses"></a>Procedimientos: Suministro de respuestas de TwiML desde su propio sitio web
Cuando la aplicación inicia una toohello llamada API de Twilio - por ejemplo, a través de hello **CallResource.Create** método - Twilio envía su solicitud tooan dirección URL esperado tooreturn una respuesta TwiML. ejemplo de Hola en [Cómo: realizar una llamada saliente](#howto_make_call) usa Hola dirección URL proporcionada Twilio [http://twimlets.com/message] [ twimlet_message_url] tooreturn respuesta de Hola.

> [!NOTE]
> Aunque TwiML está diseñado para su uso por los servicios web, puede ver hello TwiML en el explorador. Por ejemplo, haga clic en [http://twimlets.com/message] [ twimlet_message_url] toosee vacío &lt;respuesta&gt; elemento; como otro ejemplo, haga clic en [http://twimlets.com/message ? 5B0 de mensaje % D de %5 = Hola % 20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee una &lt;respuesta&gt; elemento que contiene un &lt;decir&gt; elemento.
>
>

En lugar de basarse en la dirección URL proporcionada Twilio por hello, puede crear su propio sitio de dirección URL que devuelve las respuestas HTTP. Puede crear el sitio de Hola en cualquier lenguaje que devuelve las respuestas HTTP. En este tema se da por supuesto que va a hospedar Hola URL desde un controlador genérico de ASP.NET.

Hola siguiente controlador de ASP.NET elabora una respuesta TwiML que dice **Hello World** en llamada de Hola.

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
    
Como puede ver en el ejemplo de Hola anterior, hello TwiML respuesta es simplemente un documento XML. biblioteca de Twilio.TwiML Hola contiene clases que se generarán TwiML automáticamente. Hello ejemplo siguiente genera respuesta equivalente de hello tal y como se muestra arriba, pero usa hello **VoiceResponse** clase.

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

Para obtener más información sobre TwiML, consulte [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).

Una vez haya configurado un respuestas de forma tooprovide TwiML, puede pasar esa dirección URL toohello **CallResource.Create** método. Por ejemplo, si tiene una aplicación web denominada tooan MyTwiML implementado el servicio de nube de Azure y Hola de su controlador de ASP.NET se denomina mytwiml.ashx, dirección URL de Hola se puede pasar demasiado**CallResource.Create** tal y como se muestra en el siguiente código de hello ejemplo:

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

Para obtener información adicional acerca del uso de Twilio en Azure con ASP.NET, vea [cómo toomake un teléfono llamar a con Twilio en un rol web en Azure][howto_phonecall_dotnet].

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
