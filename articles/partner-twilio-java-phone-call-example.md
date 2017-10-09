---
title: "aaaHow tooMake una llamada de teléfono de Twilio (Java) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo llamar un teléfono toomake desde una página web con Twilio en una aplicación de Java en Azure."
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 0381789e-e775-41a0-a784-294275192b1d
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 04fe5a78d431a79790dee3ca75c2b004aea4345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a>¿Cómo tooMake una llamada de teléfono uso de Twilio en una aplicación de Java en Azure
Hello en el ejemplo siguiente se muestra cómo se puede utilizar una llamada desde una página web hospedada en Azure de Twilio toomake. aplicación resultante de Hello solicitará a Hola usuario valores de llamada de teléfono, como se muestra en la siguiente captura de pantalla de Hola.

![Formulario de llamada de Azure con Twilio y Java][twilio_java]

Necesitará toodo Hola siguiente código de hello toouse en este tema:

1. Adquiera una cuenta de Twilio y un token de autenticación. tooget a trabajar con Twilio, evaluar precios en [http://www.twilio.com/pricing][twilio_pricing]. Puede registrarse en [https://www.twilio.com/try-twilio][try_twilio]. Para obtener información acerca de la API proporcionada por Twilio hello, consulte [http://www.twilio.com/api][twilio_api].
2. Obtener Hola JAR de Twilio. En [https://github.com/twilio/twilio-java][twilio_java_github], puede descargar los orígenes de GitHub de Hola y crear su propios JAR o descargar un archivo JAR pregenerado (con o sin dependencias).
   código de Hello en este tema se escribió utilizando Hola pregeneradas JAR TwilioJava 3.3.8 con dependencias.
3. Agregar Hola JAR tooyour ruta de acceso de compilación de Java.
4. Si usa Eclipse toocreate esta aplicación de Java, incluir Hola JAR de Twilio en el archivo de implementación de aplicación (WAR) mediante la función de agregado de implementación de Eclipse. Si no está usando Eclipse toocreate esta aplicación de Java, asegúrese de hello JAR de Twilio está incluida en hello mismo rol de Azure como la ruta de clase de Java toohello de aplicación y agregados de la aplicación.
5. Asegúrese de que la "cacerts keystore" contiene el certificado de entidad de certificación seguros Equifax Hola con 67:CB:9 de huella digital MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (Hola serie número es 35:DE:F4:CF y huellas digitales de hello SHA1 es D2:32:09:AD:23:D 3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A). Se trata de certificado de entidad emisora (CA) de certificado de Hola para hello [https://api.twilio.com] [ twilio_api_service] servicio, que se llama cuando se usa Twilio APIs. Para obtener información acerca de cómo agregar el almacén de autoridad de certificación de la JDK de este tooyour de certificado CA, consulte [agregando un toohello certificado almacén de certificados de entidad emisora de certificados de Java][add_ca_cert].

Además, está familiarizado con la información de hello en [crear un Hola Hola mundo Application Using Azure Toolkit for Eclipse][azure_java_eclipse_hello_world], o con otras técnicas para hospedar aplicaciones de Java en Azure if no se está usando Eclipse, se recomienda encarecidamente.

## <a name="create-a-web-form-for-making-a-call"></a>Creación de un formulario web para hacer una llamada
Hola siguiente código muestra cómo los datos de usuario de tooretrieve para realizar una llamada del formulario toocreate un sitio web. Para este ejemplo, se creó un nuevo proyecto web dinámico, llamado **TwilioCloud**, y se agregó **callform.jsp** como archivo JSP.

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Automated call form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Make this call</b>.</p>
     <br/>
      <form action="makecall.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="callTo" value="" />
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="callFrom" value="" />
           </td>
         </tr>
         <tr>
           <td>Call message:</td>
           <td><input type="text" size=400 name="callText" value="Hello. This is hello call text. Good bye." />
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Make this call" />
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toomake-hello-call"></a>Crear Hola código toomake Hola llamada
Hola código siguiente, que se llama cuando el usuario de hello completa formulario hello muestra callform.jsp, crea el mensaje de bienvenida de llamada y genera Hola llamada. Para fines de este ejemplo, se denomina archivo JSP de hello **makecall.jsp** y se ha agregado toohello **TwilioCloud** proyecto. (Use la cuenta de Twilio y la autenticación de token en lugar de valores de marcador de posición de hello asignados demasiado**accountSID** y **authToken** en el siguiente código de hello.)

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    import="java.util.*"
    import="com.twilio.*"
    import="com.twilio.sdk.*"
    import="com.twilio.sdk.resource.factory.*"
    import="com.twilio.sdk.resource.instance.*"
    pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Call processing happens here</title>
    </head>
    <body>
        <b>This is my make call page.</b><p/>
     <%
    try 
    {
         // Use your account SID and authentication token instead
         // of hello placeholders shown here.
         String accountSID = "your_twilio_account";
         String authToken = "your_twilio_authentication_token";

         // Instantiate an instance of hello Twilio client.     
         TwilioRestClient client;
         client = new TwilioRestClient(accountSID, authToken);

         // Retrieve hello account, used later tooretrieve hello CallFactory.
         Account account = client.getAccount();

         // Display hello client endpoint. 
         out.println("<p>Using Twilio endpoint " + client.getEndpoint() + ".</p>");

         // Display hello API version.
         String APIVERSION = TwilioRestClient.DEFAULT_VERSION;
         out.println("<p>Twilio client API version is " + APIVERSION + ".</p>");

         // Retrieve hello values entered by hello user.
         String callTo = request.getParameter("callTo");  
         // hello Outgoing Caller ID, used for hello From parameter,
         // must have previously been verified with Twilio.
         String callFrom = request.getParameter("callFrom");
         String userText = request.getParameter("callText");

         // Replace spaces in hello user's text with '%20', 
         // toomake hello text suitable for a URL.
         userText = userText.replace(" ", "%20");

         // Create a URL using hello Twilio message and hello user-entered text.
         String Url="http://twimlets.com/message";
         Url = Url + "?Message%5B0%5D=" + userText;

         // Display hello message URL.
         out.println("<p>");
         out.println("hello URL is " + Url);
         out.println("</p>");

         // Place hello call From, tooand URL values into a hash map. 
         HashMap<String, String> params = new HashMap<String, String>();
         params.put("From", callFrom);
         params.put("To", callTo);
         params.put("Url", Url);

         CallFactory callFactory = account.getCallFactory();
         Call call = callFactory.create(params);
         out.println("<p>Call status: " + call.getStatus()  + "</p>"); 
    } 
    catch (TwilioRestException e) 
    {
        out.println("<p>TwilioRestException encountered: " + e.getMessage() + "</p>");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    catch (Exception e) 
    {
        out.println("<p>Exception encountered: " + e.getMessage() + "");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    %>
    </body>
    </html>

Además toomaking Hola llamada, makecall.jsp muestra el punto de conexión de hello Twilio, versión de API y estado de la llamada de Hola. Hola siguiente captura de pantalla es un ejemplo:

![Respuesta de llamada de Azure con Twilio y Java][twilio_java_response]

## <a name="run-hello-application"></a>Ejecutar la aplicación hello
Siguiente son Hola toorun de pasos de alto nivel a la aplicación; detalles de estos pasos se pueden encontrar en [crear un Hola Hola mundo Application Using Azure Toolkit for Eclipse][azure_java_eclipse_hello_world].

1. Exportar su toohello TwilioCloud WAR Azure **approot** carpeta. 
2. Modificar **startup.cmd** toounzip los WAR TwilioCloud.
3. Compile la aplicación para el emulador de proceso de Hola.
4. Iniciar la implementación en el emulador de proceso de Hola.
5. Abra un explorador y ejecute **http://localhost:8080/TwilioCloud/callform.jsp**.
6. Escriba valores en forma de hello, haga clic en **hacer esta llamada**y, a continuación, ver los resultados de hello en makecall.jsp.

Cuando esté listo toodeploy tooAzure, volver a compilar para la nube de implementación toohello, implementar tooAzure y ejecutar http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp en el Explorador de hello (sustituya el valor de *your_hosted_name*).

## <a name="next-steps"></a>Pasos siguientes
Este código se proporcionó tooshow funcionalidad básica con Twilio en Java en Azure. Antes de implementar tooAzure en producción, puede que desee tooadd más control de errores o con otras características. Por ejemplo:

* En lugar de utilizar un formulario web Forms, puede utilizar blobs de almacenamiento de Azure o números de teléfono de toostore de base de datos SQL y llamar a texto. Para obtener información acerca del uso de blobs de almacenamiento de Azure en Java, consulte [cómo tooUse Hola servicio de almacenamiento de blobs desde Java][howto_blob_storage_java]. Para obtener información sobre el uso de la base de datos de SQL en Java, consulte [usar base de datos de SQL en Java][howto_sql_azure_java].
* Puede usar **RoleEnvironment.getConfigurationSettings** tooretrieve Hola Id. de cuenta de Twilio y la autenticación de token de opciones de configuración de su implementación, en lugar de codificar de forma rígida valores de hello en makecall.jsp. Para obtener información acerca de hello **RoleEnvironment** de clases, consulte [Using Hola biblioteca de tiempo de ejecución de servicios de Azure en JSP] [ azure_runtime_jsp] y documentación de paquete en tiempo de ejecución del servicio de Azure de hello en [http://dl.windowsazure.com/javadoc][azure_javadoc].
* código de Hello makecall.jsp asigna una dirección URL proporcionada Twilio, [http://twimlets.com/message][twimlet_message_url], toohello **Url** variable. Esta dirección URL proporciona una respuesta de lenguaje de marcado de Twilio (TwiML) que le informa de cómo llamar tooproceed con hello de Twilio. Por ejemplo, puede contener hello TwiML que se devuelve un  **&lt;decir&gt;**  verbo que es el resultado en texto que se va a toohello hablado destinatario de la llamada. En lugar de usar la dirección URL proporcionada Twilio por hello, puede generar la solicitud de su propio tooTwilio toorespond servicio; Para obtener más información, consulte [cómo tooUse Twilio para capacidades de SMS en Java y voz][howto_twilio_voice_sms_java]. Puede encontrar más información acerca de TwiML en [http://www.twilio.com/docs/api/twiml][twiml]y obtener más información acerca de  **&lt;decir&gt;**  y otros verbos Twilio pueden encontrarse en [http://www.twilio.com/docs/api/twiml/say][twilio_say].
* Lea las directrices de seguridad de hello Twilio en [https://www.twilio.com/docs/security][twilio_docs_security].

Para obtener información adicional sobre Twilio, vea [https://www.twilio.com/docs][twilio_docs].

## <a name="see-also"></a>Otras referencias
* [Cómo tooUse Twilio para voz y capacidades de SMS en Java][howto_twilio_voice_sms_java]
* [Agregar un almacén de certificados de entidad emisora de certificados de Java de toohello de certificado][add_ca_cert]

[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/api
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_java_github]: http://github.com/twilio/twilio-java
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[azure_java_eclipse_hello_world]: http://msdn.microsoft.com/library/windowsazure/hh690944.aspx
[howto_twilio_voice_sms_java]: partner-twilio-java-how-to-use-voice-sms.md
[howto_blob_storage_java]: http://www.windowsazure.com/develop/java/how-to-guides/blob-storage/
[howto_sql_azure_java]: http://msdn.microsoft.com/library/windowsazure/hh749029.aspx
[azure_runtime_jsp]: http://msdn.microsoft.com/library/windowsazure/hh690948.aspx
[azure_javadoc]: http://dl.windowsazure.com/javadoc
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[twilio_java]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaCallForm.jpg
[twilio_java_response]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaMakeCall.jpg
