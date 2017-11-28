---
title: aaastore-sendgrid-Java-How-to-Send-email-example
description: "Cómo toosend de correo electrónico con SendGrid desde Java en una implementación de Azure"
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: af096a73-6985-4350-92e4-ce1722c8d72f
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: vibhork;dominic.may@sendgrid.com;elmer.thomas@sendgrid.com
ms.openlocfilehash: 51fde1fc71467f8252532b30d2f87856ec25067b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java-in-an-azure-deployment"></a><span data-ttu-id="cdba6-103">¿Cómo tooSend correo electrónico utilizando SendGrid desde Java en una implementación de Azure</span><span class="sxs-lookup"><span data-stu-id="cdba6-103">How tooSend Email Using SendGrid from Java in an Azure Deployment</span></span>
<span data-ttu-id="cdba6-104">Hello en el ejemplo siguiente se muestra cómo puede utilizar mensajes de correo electrónico toosend SendGrid desde una página web hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="cdba6-104">hello following example shows you how you can use SendGrid toosend emails from a web page hosted in Azure.</span></span> <span data-ttu-id="cdba6-105">aplicación resultante de Hello solicitará a Hola usuario valores de correo electrónico, como se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdba6-105">hello resulting application will prompt hello user for email values, as shown in hello following screen shot.</span></span>

![Formulario de correo electrónico][emailform]

<span data-ttu-id="cdba6-107">Hola resultante correo electrónico tendrá un aspecto similar toohello siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="cdba6-107">hello resulting email will look similar toohello following screen shot.</span></span>

![Mensaje de correo electrónico][emailsent]

<span data-ttu-id="cdba6-109">Necesitará toodo Hola siguiente código de hello toouse en este tema:</span><span class="sxs-lookup"><span data-stu-id="cdba6-109">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="cdba6-110">Obtener Hola javax.mail archivos JAR, por ejemplo de <http://www.oracle.com/technetwork/java/javamail/index.html>.</span><span class="sxs-lookup"><span data-stu-id="cdba6-110">Obtain hello javax.mail JARs, for example from <http://www.oracle.com/technetwork/java/javamail/index.html>.</span></span>
2. <span data-ttu-id="cdba6-111">Agregar Hola archivos JAR tooyour ruta de acceso de compilación de Java.</span><span class="sxs-lookup"><span data-stu-id="cdba6-111">Add hello JARs tooyour Java build path.</span></span>
3. <span data-ttu-id="cdba6-112">Si usas Eclipse toocreate esta aplicación de Java, puede incluir las bibliotecas de SendGrid de hello en el archivo de implementación de aplicación (WAR) mediante la función de agregado de implementación de Eclipse.</span><span class="sxs-lookup"><span data-stu-id="cdba6-112">If you are using Eclipse toocreate this Java application, you can include hello SendGrid libraries in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="cdba6-113">Si no está usando Eclipse toocreate esta aplicación de Java, asegúrese de bibliotecas de Hola se incluyen dentro de hello mismo rol de Azure como la ruta de clase de Java toohello de aplicación y agregados de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cdba6-113">If you are not using Eclipse toocreate this Java application, ensure hello libraries are included within hello same Azure role as your Java application, and added toohello class path of your application.</span></span>

<span data-ttu-id="cdba6-114">También debe tener su propio nombre de usuario de SendGrid y la contraseña, el correo electrónico de toobe toosend capaz de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdba6-114">You must also have your own SendGrid username and password, toobe able toosend hello email.</span></span> <span data-ttu-id="cdba6-115">tooget a trabajar con SendGrid, consulte [cómo toosend de correo electrónico con SendGrid desde Java](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="cdba6-115">tooget started with SendGrid, see [How toosend email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

<span data-ttu-id="cdba6-116">Además, está familiarizado con la información de hello en [crear una aplicación Hello World de Azure en Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), o con otras técnicas para hospedar aplicaciones de Java en Azure si no está usando Eclipse, se recomienda encarecidamente.</span><span class="sxs-lookup"><span data-stu-id="cdba6-116">Additionally, familiarity with hello information at [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-sending-email"></a><span data-ttu-id="cdba6-117">Creación de un formulario web para el envío del correo electrónico</span><span class="sxs-lookup"><span data-stu-id="cdba6-117">Create a web form for sending email</span></span>
<span data-ttu-id="cdba6-118">Hola siguiente código muestra cómo los datos de usuario de tooretrieve para enviar correo electrónico del formulario toocreate un sitio web.</span><span class="sxs-lookup"><span data-stu-id="cdba6-118">hello following code shows how toocreate a web form tooretrieve user data for sending email.</span></span> <span data-ttu-id="cdba6-119">Para fines de este contenido, se denomina archivo JSP de hello **emailform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="cdba6-119">For purposes of this content, hello JSP file is named **emailform.jsp**.</span></span>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Send this email</b>.</p>
     <br/>
      <form action="sendemail.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="emailTo">
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="emailFrom">
           </td>
         </tr>
         <tr>
           <td>Subject:</td>
           <td><input type="text" size=100 name="emailSubject" value="My email subject">
           </td>
         </tr>
         <tr>
           <td>Text:</td>
           <td><input type="text" size=400 name="emailText" value="Hello,<p>This is my message.</p>Thank you." />
           </td>
         </tr>
         <tr>
           <td>SendGrid user name:</td>
           <td><input type="text" name="sendGridUser">
           </td>
         </tr>
         <tr>
           <td>SendGrid password:</td>
           <td><input type="password" name="sendGridPassword">
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Send this email">
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toosend-hello-email"></a><span data-ttu-id="cdba6-120">Crear correo electrónico de hello código toosend Hola</span><span class="sxs-lookup"><span data-stu-id="cdba6-120">Create hello code toosend hello email</span></span>
<span data-ttu-id="cdba6-121">Hello código siguiente, que se llama cuando se complete el formulario de hello en emailform.jsp, crea el mensaje de correo electrónico de Hola y lo envía.</span><span class="sxs-lookup"><span data-stu-id="cdba6-121">hello following code, which is called when you complete hello form in emailform.jsp, creates hello email message and sends it.</span></span> <span data-ttu-id="cdba6-122">Para fines de este contenido, se denomina archivo JSP de hello **sendemail.jsp**.</span><span class="sxs-lookup"><span data-stu-id="cdba6-122">For purposes of this content, hello JSP file is named **sendemail.jsp**.</span></span>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" import="javax.activation.*, javax.mail.*, javax.mail.internet.*, java.util.Date, java.util.Properties" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email processing happens here</title>
    </head>
    <body>
        <b>This is my send mail page.</b><p/>
     <%

     final String sendGridUser = request.getParameter("sendGridUser");
     final String sendGridPassword = request.getParameter("sendGridPassword");

     class SMTPAuthenticator extends Authenticator
     {
       public PasswordAuthentication getPasswordAuthentication()
       {
            String username = sendGridUser;
            String password = sendGridPassword;

            return new PasswordAuthentication(username, password);   
       }
     }
     try
     {

         // hello SendGrid SMTP server.
         String SMTP_HOST_NAME = "smtp.sendgrid.net";

         Properties properties;

         properties = new Properties();

         // Specify SMTP values.
         properties.put("mail.transport.protocol", "smtp");
         properties.put("mail.smtp.host", SMTP_HOST_NAME);
         properties.put("mail.smtp.port", 587);
         properties.put("mail.smtp.auth", "true");

         // Display hello email fields entered by hello user. 
         out.println("Value entered for email Subject: " + request.getParameter("emailSubject") + "<br/>");        
         out.println("Value entered for email      To: " + request.getParameter("emailTo") + "<br/>");
         out.println("Value entered for email    From: " + request.getParameter("emailFrom") + "<br/>");
         out.println("Value entered for email    Text: " + "<br/>" + request.getParameter("emailText") + "<br/>");

         // Create hello authenticator object.
         Authenticator authenticator = new SMTPAuthenticator();

         // Create hello mail session object.
         Session mailSession;
         mailSession = Session.getDefaultInstance(properties, authenticator);

         // Display debug information toostdout, useful when using the
         // compute emulator during development.
         mailSession.setDebug(true);

         // Create hello message and message part objects.
         MimeMessage message;
         Multipart multipart;
         MimeBodyPart messagePart; 

         message = new MimeMessage(mailSession);

         multipart = new MimeMultipart("alternative");
         messagePart = new MimeBodyPart();
         messagePart.setContent(request.getParameter("emailText"), "text/html");
         multipart.addBodyPart(messagePart);            

         // Specify hello email To, From, Subject and Content. 
         message.setFrom(new InternetAddress(request.getParameter("emailFrom")));
         message.addRecipient(Message.RecipientType.TO, new InternetAddress(request.getParameter("emailTo")));
         message.setSubject(request.getParameter("emailSubject")); 
         message.setContent(multipart);

         // Uncomment hello following if you want tooadd a footer.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"footer\": {\"settings\": {\"enable\":1,\"text/html\": \"<html>This is my <b>email footer</b>.</html>\"}}}}");

         // Uncomment hello following if you want tooenable click tracking.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"clicktrack\": {\"settings\": {\"enable\":1}}}}");

         Transport transport;
         transport = mailSession.getTransport();
         // Connect hello transport object.
         transport.connect();
         // Send hello message.
         transport.sendMessage(message,  message.getRecipients(Message.RecipientType.TO));
         // Close hello connection.
         transport.close();

        out.println("<p>Email processing completed.</p>");

     }
     catch (Exception e)
     {
         out.println("<p>Exception encountered: " + 
                            e.getMessage()     +
                            "</p>");   
     }
    %>

    </body>
    </html>

<span data-ttu-id="cdba6-123">Además correo electrónico hello toosending emailform.jsp proporciona un resultado para el usuario de hello; Hola siguiente captura de pantalla es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cdba6-123">In addition toosending hello email, emailform.jsp provides a result for hello user; an example is hello following screen shot:</span></span>

![Resultado del envío del correo][emailresult]

## <a name="next-steps"></a><span data-ttu-id="cdba6-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cdba6-125">Next steps</span></span>
<span data-ttu-id="cdba6-126">Implementar el emulador de proceso de aplicación toohello y dentro de un explorador que se ejecute emailform.jsp, escriba valores en forma de hello, haga clic en **enviar este correo electrónico**y, a continuación, ver los resultados en sendemail.jsp.</span><span class="sxs-lookup"><span data-stu-id="cdba6-126">Deploy your application toohello compute emulator and within a browser run emailform.jsp, enter values in hello form, click **Send this email**, and then see results in sendemail.jsp.</span></span>

<span data-ttu-id="cdba6-127">Este código se proporcionó tooshow también cómo toouse SendGrid en Java en Azure.</span><span class="sxs-lookup"><span data-stu-id="cdba6-127">This code was provided tooshow you how toouse SendGrid in Java on Azure.</span></span> <span data-ttu-id="cdba6-128">Antes de implementar tooAzure en producción, puede que desee tooadd más control de errores o con otras características.</span><span class="sxs-lookup"><span data-stu-id="cdba6-128">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="cdba6-129">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cdba6-129">For example:</span></span> 

* <span data-ttu-id="cdba6-130">Podría utilizar blobs de almacenamiento de Azure o direcciones de correo electrónico de base de datos SQL toostore y mensajes de correo electrónico, en lugar de utilizar un formulario web Forms.</span><span class="sxs-lookup"><span data-stu-id="cdba6-130">You could use Azure storage blobs or SQL Database toostore email addresses and email messages, instead of using a web form.</span></span> <span data-ttu-id="cdba6-131">Para obtener información acerca del uso de blobs de almacenamiento de Azure en Java, consulte [cómo tooUse Hola servicio de almacenamiento de blobs desde Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span><span class="sxs-lookup"><span data-stu-id="cdba6-131">For information about using Azure storage blobs in Java, see [How tooUse hello Blob Storage Service from Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span></span> <span data-ttu-id="cdba6-132">Para obtener más información acerca de cómo usar Base de datos SQL en Java, consulte [Uso de Base de datos SQL en Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span><span class="sxs-lookup"><span data-stu-id="cdba6-132">For information about using SQL Database in Java, see [Using SQL Database in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span></span>
* <span data-ttu-id="cdba6-133">Puede usar `RoleEnvironment.getConfigurationSettings` tooretrieve hello SendGrid username y la contraseña de los valores de configuración de su implementación, en lugar de usar Hola tooretrieve de formulario web esos valores.</span><span class="sxs-lookup"><span data-stu-id="cdba6-133">You could use `RoleEnvironment.getConfigurationSettings` tooretrieve hello SendGrid username and password from your deployment's configuration settings, instead of using hello web form tooretrieve those values.</span></span> <span data-ttu-id="cdba6-134">Para obtener información acerca de hello `RoleEnvironment` de clases, consulte [Using Hola biblioteca de tiempo de ejecución de servicios de Azure en JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) y documentación de paquete en tiempo de ejecución del servicio de Azure de hello en <http://dl.windowsazure.com/javadoc>.</span><span class="sxs-lookup"><span data-stu-id="cdba6-134">For information about hello `RoleEnvironment` class, see [Using hello Azure Service Runtime Library in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) and hello Azure Service Runtime package documentation at <http://dl.windowsazure.com/javadoc>.</span></span>
* <span data-ttu-id="cdba6-135">Para obtener más información sobre el uso de SendGrid en Java, consulte [cómo toosend de correo electrónico con SendGrid desde Java](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="cdba6-135">For more information about using SendGrid in Java, see [How toosend email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
