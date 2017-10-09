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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a><span data-ttu-id="8ff90-103">¿Cómo tooMake una llamada de teléfono uso de Twilio en una aplicación de Java en Azure</span><span class="sxs-lookup"><span data-stu-id="8ff90-103">How tooMake a Phone Call Using Twilio in a Java Application on Azure</span></span>
<span data-ttu-id="8ff90-104">Hello en el ejemplo siguiente se muestra cómo se puede utilizar una llamada desde una página web hospedada en Azure de Twilio toomake.</span><span class="sxs-lookup"><span data-stu-id="8ff90-104">hello following example shows you how you can use Twilio toomake a call from a web page hosted in Azure.</span></span> <span data-ttu-id="8ff90-105">aplicación resultante de Hello solicitará a Hola usuario valores de llamada de teléfono, como se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ff90-105">hello resulting application will prompt hello user for phone call values, as shown in hello following screen shot.</span></span>

![Formulario de llamada de Azure con Twilio y Java][twilio_java]

<span data-ttu-id="8ff90-107">Necesitará toodo Hola siguiente código de hello toouse en este tema:</span><span class="sxs-lookup"><span data-stu-id="8ff90-107">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="8ff90-108">Adquiera una cuenta de Twilio y un token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="8ff90-108">Acquire a Twilio account and authentication token.</span></span> <span data-ttu-id="8ff90-109">tooget a trabajar con Twilio, evaluar precios en [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="8ff90-109">tooget started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="8ff90-110">Puede registrarse en [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="8ff90-110">You can sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="8ff90-111">Para obtener información acerca de la API proporcionada por Twilio hello, consulte [http://www.twilio.com/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="8ff90-111">For information about hello API provided by Twilio, see [http://www.twilio.com/api][twilio_api].</span></span>
2. <span data-ttu-id="8ff90-112">Obtener Hola JAR de Twilio.</span><span class="sxs-lookup"><span data-stu-id="8ff90-112">Obtain hello Twilio JAR.</span></span> <span data-ttu-id="8ff90-113">En [https://github.com/twilio/twilio-java][twilio_java_github], puede descargar los orígenes de GitHub de Hola y crear su propios JAR o descargar un archivo JAR pregenerado (con o sin dependencias).</span><span class="sxs-lookup"><span data-stu-id="8ff90-113">At [https://github.com/twilio/twilio-java][twilio_java_github], you can download hello GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
   <span data-ttu-id="8ff90-114">código de Hello en este tema se escribió utilizando Hola pregeneradas JAR TwilioJava 3.3.8 con dependencias.</span><span class="sxs-lookup"><span data-stu-id="8ff90-114">hello code in this topic was written using hello pre-built TwilioJava-3.3.8-with-dependencies JAR.</span></span>
3. <span data-ttu-id="8ff90-115">Agregar Hola JAR tooyour ruta de acceso de compilación de Java.</span><span class="sxs-lookup"><span data-stu-id="8ff90-115">Add hello JAR tooyour Java build path.</span></span>
4. <span data-ttu-id="8ff90-116">Si usa Eclipse toocreate esta aplicación de Java, incluir Hola JAR de Twilio en el archivo de implementación de aplicación (WAR) mediante la función de agregado de implementación de Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8ff90-116">If you are using Eclipse toocreate this Java application, include hello Twilio JAR in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="8ff90-117">Si no está usando Eclipse toocreate esta aplicación de Java, asegúrese de hello JAR de Twilio está incluida en hello mismo rol de Azure como la ruta de clase de Java toohello de aplicación y agregados de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8ff90-117">If you are not using Eclipse toocreate this Java application, ensure hello Twilio JAR is included within hello same Azure role as your Java application, and added toohello class path of your application.</span></span>
5. <span data-ttu-id="8ff90-118">Asegúrese de que la "cacerts keystore" contiene el certificado de entidad de certificación seguros Equifax Hola con 67:CB:9 de huella digital MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (Hola serie número es 35:DE:F4:CF y huellas digitales de hello SHA1 es D2:32:09:AD:23:D 3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="8ff90-118">Ensure your cacerts keystore contains hello Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello serial number is 35:DE:F4:CF and hello SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="8ff90-119">Se trata de certificado de entidad emisora (CA) de certificado de Hola para hello [https://api.twilio.com] [ twilio_api_service] servicio, que se llama cuando se usa Twilio APIs.</span><span class="sxs-lookup"><span data-stu-id="8ff90-119">This is hello certificate authority (CA) certificate for hello [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="8ff90-120">Para obtener información acerca de cómo agregar el almacén de autoridad de certificación de la JDK de este tooyour de certificado CA, consulte [agregando un toohello certificado almacén de certificados de entidad emisora de certificados de Java][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="8ff90-120">For information about adding this CA certificate tooyour JDK's cacert store, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="8ff90-121">Además, está familiarizado con la información de hello en [crear un Hola Hola mundo Application Using Azure Toolkit for Eclipse][azure_java_eclipse_hello_world], o con otras técnicas para hospedar aplicaciones de Java en Azure if no se está usando Eclipse, se recomienda encarecidamente.</span><span class="sxs-lookup"><span data-stu-id="8ff90-121">Additionally, familiarity with hello information at [Creating a Hello World Application Using hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world], or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="8ff90-122">Creación de un formulario web para hacer una llamada</span><span class="sxs-lookup"><span data-stu-id="8ff90-122">Create a web form for making a call</span></span>
<span data-ttu-id="8ff90-123">Hola siguiente código muestra cómo los datos de usuario de tooretrieve para realizar una llamada del formulario toocreate un sitio web.</span><span class="sxs-lookup"><span data-stu-id="8ff90-123">hello following code shows how toocreate a web form tooretrieve user data for making a call.</span></span> <span data-ttu-id="8ff90-124">Para este ejemplo, se creó un nuevo proyecto web dinámico, llamado **TwilioCloud**, y se agregó **callform.jsp** como archivo JSP.</span><span class="sxs-lookup"><span data-stu-id="8ff90-124">For purposes of this example, a new dynamic web project, named **TwilioCloud**, was created, and **callform.jsp** was added as a JSP file.</span></span>

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

## <a name="create-hello-code-toomake-hello-call"></a><span data-ttu-id="8ff90-125">Crear Hola código toomake Hola llamada</span><span class="sxs-lookup"><span data-stu-id="8ff90-125">Create hello code toomake hello call</span></span>
<span data-ttu-id="8ff90-126">Hola código siguiente, que se llama cuando el usuario de hello completa formulario hello muestra callform.jsp, crea el mensaje de bienvenida de llamada y genera Hola llamada.</span><span class="sxs-lookup"><span data-stu-id="8ff90-126">hello following code, which is called when hello user completes hello form displayed by callform.jsp, creates hello call message and generates hello call.</span></span> <span data-ttu-id="8ff90-127">Para fines de este ejemplo, se denomina archivo JSP de hello **makecall.jsp** y se ha agregado toohello **TwilioCloud** proyecto.</span><span class="sxs-lookup"><span data-stu-id="8ff90-127">For purposes of this example, hello JSP file is named **makecall.jsp** and was added toohello **TwilioCloud** project.</span></span> <span data-ttu-id="8ff90-128">(Use la cuenta de Twilio y la autenticación de token en lugar de valores de marcador de posición de hello asignados demasiado**accountSID** y **authToken** en el siguiente código de hello.)</span><span class="sxs-lookup"><span data-stu-id="8ff90-128">(Use your Twilio account and authentication token instead of hello placeholder values assigned too**accountSID** and **authToken** in hello code below.)</span></span>

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

<span data-ttu-id="8ff90-129">Además toomaking Hola llamada, makecall.jsp muestra el punto de conexión de hello Twilio, versión de API y estado de la llamada de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ff90-129">In addition toomaking hello call, makecall.jsp displays hello Twilio endpoint, API version, and hello call status.</span></span> <span data-ttu-id="8ff90-130">Hola siguiente captura de pantalla es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8ff90-130">An example is hello following screen shot:</span></span>

![Respuesta de llamada de Azure con Twilio y Java][twilio_java_response]

## <a name="run-hello-application"></a><span data-ttu-id="8ff90-132">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="8ff90-132">Run hello application</span></span>
<span data-ttu-id="8ff90-133">Siguiente son Hola toorun de pasos de alto nivel a la aplicación; detalles de estos pasos se pueden encontrar en [crear un Hola Hola mundo Application Using Azure Toolkit for Eclipse][azure_java_eclipse_hello_world].</span><span class="sxs-lookup"><span data-stu-id="8ff90-133">Following are hello high-level steps toorun your application; details for these steps can be found at [Creating a Hello World Application Using hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world].</span></span>

1. <span data-ttu-id="8ff90-134">Exportar su toohello TwilioCloud WAR Azure **approot** carpeta.</span><span class="sxs-lookup"><span data-stu-id="8ff90-134">Export your TwilioCloud WAR toohello Azure **approot** folder.</span></span> 
2. <span data-ttu-id="8ff90-135">Modificar **startup.cmd** toounzip los WAR TwilioCloud.</span><span class="sxs-lookup"><span data-stu-id="8ff90-135">Modify **startup.cmd** toounzip your TwilioCloud WAR.</span></span>
3. <span data-ttu-id="8ff90-136">Compile la aplicación para el emulador de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ff90-136">Compile your application for hello compute emulator.</span></span>
4. <span data-ttu-id="8ff90-137">Iniciar la implementación en el emulador de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ff90-137">Start your deployment in hello compute emulator.</span></span>
5. <span data-ttu-id="8ff90-138">Abra un explorador y ejecute **http://localhost:8080/TwilioCloud/callform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="8ff90-138">Open a browser, and run **http://localhost:8080/TwilioCloud/callform.jsp**.</span></span>
6. <span data-ttu-id="8ff90-139">Escriba valores en forma de hello, haga clic en **hacer esta llamada**y, a continuación, ver los resultados de hello en makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="8ff90-139">Enter values in hello form, click **Make this call**, and then see hello results in makecall.jsp.</span></span>

<span data-ttu-id="8ff90-140">Cuando esté listo toodeploy tooAzure, volver a compilar para la nube de implementación toohello, implementar tooAzure y ejecutar http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp en el Explorador de hello (sustituya el valor de *your_hosted_name*).</span><span class="sxs-lookup"><span data-stu-id="8ff90-140">When you are ready toodeploy tooAzure, recompile for deployment toohello cloud, deploy tooAzure, and run http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp in hello browser (substitute your value for *your_hosted_name*).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ff90-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8ff90-141">Next steps</span></span>
<span data-ttu-id="8ff90-142">Este código se proporcionó tooshow funcionalidad básica con Twilio en Java en Azure.</span><span class="sxs-lookup"><span data-stu-id="8ff90-142">This code was provided tooshow you basic functionality using Twilio in Java on Azure.</span></span> <span data-ttu-id="8ff90-143">Antes de implementar tooAzure en producción, puede que desee tooadd más control de errores o con otras características.</span><span class="sxs-lookup"><span data-stu-id="8ff90-143">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="8ff90-144">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8ff90-144">For example:</span></span>

* <span data-ttu-id="8ff90-145">En lugar de utilizar un formulario web Forms, puede utilizar blobs de almacenamiento de Azure o números de teléfono de toostore de base de datos SQL y llamar a texto.</span><span class="sxs-lookup"><span data-stu-id="8ff90-145">Instead of using a web form, you could use Azure storage blobs or SQL Database toostore phone numbers and call text.</span></span> <span data-ttu-id="8ff90-146">Para obtener información acerca del uso de blobs de almacenamiento de Azure en Java, consulte [cómo tooUse Hola servicio de almacenamiento de blobs desde Java][howto_blob_storage_java].</span><span class="sxs-lookup"><span data-stu-id="8ff90-146">For information about using Azure storage blobs in Java, see [How tooUse hello Blob Storage Service from Java][howto_blob_storage_java].</span></span> <span data-ttu-id="8ff90-147">Para obtener información sobre el uso de la base de datos de SQL en Java, consulte [usar base de datos de SQL en Java][howto_sql_azure_java].</span><span class="sxs-lookup"><span data-stu-id="8ff90-147">For information about using SQL Database in Java, see [Using SQL Database in Java][howto_sql_azure_java].</span></span>
* <span data-ttu-id="8ff90-148">Puede usar **RoleEnvironment.getConfigurationSettings** tooretrieve Hola Id. de cuenta de Twilio y la autenticación de token de opciones de configuración de su implementación, en lugar de codificar de forma rígida valores de hello en makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="8ff90-148">You could use **RoleEnvironment.getConfigurationSettings** tooretrieve hello Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding hello values in makecall.jsp.</span></span> <span data-ttu-id="8ff90-149">Para obtener información acerca de hello **RoleEnvironment** de clases, consulte [Using Hola biblioteca de tiempo de ejecución de servicios de Azure en JSP] [ azure_runtime_jsp] y documentación de paquete en tiempo de ejecución del servicio de Azure de hello en [http://dl.windowsazure.com/javadoc][azure_javadoc].</span><span class="sxs-lookup"><span data-stu-id="8ff90-149">For information about hello **RoleEnvironment** class, see [Using hello Azure Service Runtime Library in JSP][azure_runtime_jsp] and hello Azure Service Runtime package documentation at [http://dl.windowsazure.com/javadoc][azure_javadoc].</span></span>
* <span data-ttu-id="8ff90-150">código de Hello makecall.jsp asigna una dirección URL proporcionada Twilio, [http://twimlets.com/message][twimlet_message_url], toohello **Url** variable.</span><span class="sxs-lookup"><span data-stu-id="8ff90-150">hello makecall.jsp code assigns a Twilio-provided URL, [http://twimlets.com/message][twimlet_message_url], toohello **Url** variable.</span></span> <span data-ttu-id="8ff90-151">Esta dirección URL proporciona una respuesta de lenguaje de marcado de Twilio (TwiML) que le informa de cómo llamar tooproceed con hello de Twilio.</span><span class="sxs-lookup"><span data-stu-id="8ff90-151">This URL provides a Twilio Markup Language (TwiML) response that informs Twilio how tooproceed with hello call.</span></span> <span data-ttu-id="8ff90-152">Por ejemplo, puede contener hello TwiML que se devuelve un  **&lt;decir&gt;**  verbo que es el resultado en texto que se va a toohello hablado destinatario de la llamada.</span><span class="sxs-lookup"><span data-stu-id="8ff90-152">For example, hello TwiML that is returned can contain a **&lt;Say&gt;** verb that results in text being spoken toohello call recipient.</span></span> <span data-ttu-id="8ff90-153">En lugar de usar la dirección URL proporcionada Twilio por hello, puede generar la solicitud de su propio tooTwilio toorespond servicio; Para obtener más información, consulte [cómo tooUse Twilio para capacidades de SMS en Java y voz][howto_twilio_voice_sms_java].</span><span class="sxs-lookup"><span data-stu-id="8ff90-153">Instead of using hello Twilio-provided URL, you could build your own service toorespond tooTwilio's request; for more information, see [How tooUse Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java].</span></span> <span data-ttu-id="8ff90-154">Puede encontrar más información acerca de TwiML en [http://www.twilio.com/docs/api/twiml][twiml]y obtener más información acerca de  **&lt;decir&gt;**  y otros verbos Twilio pueden encontrarse en [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="8ff90-154">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about **&lt;Say&gt;** and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="8ff90-155">Lea las directrices de seguridad de hello Twilio en [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="8ff90-155">Read hello Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="8ff90-156">Para obtener información adicional sobre Twilio, vea [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="8ff90-156">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="8ff90-157">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="8ff90-157">See Also</span></span>
* <span data-ttu-id="8ff90-158">[Cómo tooUse Twilio para voz y capacidades de SMS en Java][howto_twilio_voice_sms_java]</span><span class="sxs-lookup"><span data-stu-id="8ff90-158">[How tooUse Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java]</span></span>
* <span data-ttu-id="8ff90-159">[Agregar un almacén de certificados de entidad emisora de certificados de Java de toohello de certificado][add_ca_cert]</span><span class="sxs-lookup"><span data-stu-id="8ff90-159">[Adding a Certificate toohello Java CA Certificate Store][add_ca_cert]</span></span>

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
