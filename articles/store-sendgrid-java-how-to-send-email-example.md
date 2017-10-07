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
# <a name="how-toosend-email-using-sendgrid-from-java-in-an-azure-deployment"></a>¿Cómo tooSend correo electrónico utilizando SendGrid desde Java en una implementación de Azure
Hello en el ejemplo siguiente se muestra cómo puede utilizar mensajes de correo electrónico toosend SendGrid desde una página web hospedada en Azure. aplicación resultante de Hello solicitará a Hola usuario valores de correo electrónico, como se muestra en la siguiente captura de pantalla de Hola.

![Formulario de correo electrónico][emailform]

Hola resultante correo electrónico tendrá un aspecto similar toohello siguiente captura de pantalla.

![Mensaje de correo electrónico][emailsent]

Necesitará toodo Hola siguiente código de hello toouse en este tema:

1. Obtener Hola javax.mail archivos JAR, por ejemplo de <http://www.oracle.com/technetwork/java/javamail/index.html>.
2. Agregar Hola archivos JAR tooyour ruta de acceso de compilación de Java.
3. Si usas Eclipse toocreate esta aplicación de Java, puede incluir las bibliotecas de SendGrid de hello en el archivo de implementación de aplicación (WAR) mediante la función de agregado de implementación de Eclipse. Si no está usando Eclipse toocreate esta aplicación de Java, asegúrese de bibliotecas de Hola se incluyen dentro de hello mismo rol de Azure como la ruta de clase de Java toohello de aplicación y agregados de la aplicación.

También debe tener su propio nombre de usuario de SendGrid y la contraseña, el correo electrónico de toobe toosend capaz de Hola. tooget a trabajar con SendGrid, consulte [cómo toosend de correo electrónico con SendGrid desde Java](store-sendgrid-java-how-to-send-email.md).

Además, está familiarizado con la información de hello en [crear una aplicación Hello World de Azure en Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), o con otras técnicas para hospedar aplicaciones de Java en Azure si no está usando Eclipse, se recomienda encarecidamente.

## <a name="create-a-web-form-for-sending-email"></a>Creación de un formulario web para el envío del correo electrónico
Hola siguiente código muestra cómo los datos de usuario de tooretrieve para enviar correo electrónico del formulario toocreate un sitio web. Para fines de este contenido, se denomina archivo JSP de hello **emailform.jsp**.

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

## <a name="create-hello-code-toosend-hello-email"></a>Crear correo electrónico de hello código toosend Hola
Hello código siguiente, que se llama cuando se complete el formulario de hello en emailform.jsp, crea el mensaje de correo electrónico de Hola y lo envía. Para fines de este contenido, se denomina archivo JSP de hello **sendemail.jsp**.

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

Además correo electrónico hello toosending emailform.jsp proporciona un resultado para el usuario de hello; Hola siguiente captura de pantalla es un ejemplo:

![Resultado del envío del correo][emailresult]

## <a name="next-steps"></a>Pasos siguientes
Implementar el emulador de proceso de aplicación toohello y dentro de un explorador que se ejecute emailform.jsp, escriba valores en forma de hello, haga clic en **enviar este correo electrónico**y, a continuación, ver los resultados en sendemail.jsp.

Este código se proporcionó tooshow también cómo toouse SendGrid en Java en Azure. Antes de implementar tooAzure en producción, puede que desee tooadd más control de errores o con otras características. Por ejemplo: 

* Podría utilizar blobs de almacenamiento de Azure o direcciones de correo electrónico de base de datos SQL toostore y mensajes de correo electrónico, en lugar de utilizar un formulario web Forms. Para obtener información acerca del uso de blobs de almacenamiento de Azure en Java, consulte [cómo tooUse Hola servicio de almacenamiento de blobs desde Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/). Para obtener más información acerca de cómo usar Base de datos SQL en Java, consulte [Uso de Base de datos SQL en Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).
* Puede usar `RoleEnvironment.getConfigurationSettings` tooretrieve hello SendGrid username y la contraseña de los valores de configuración de su implementación, en lugar de usar Hola tooretrieve de formulario web esos valores. Para obtener información acerca de hello `RoleEnvironment` de clases, consulte [Using Hola biblioteca de tiempo de ejecución de servicios de Azure en JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) y documentación de paquete en tiempo de ejecución del servicio de Azure de hello en <http://dl.windowsazure.com/javadoc>.
* Para obtener más información sobre el uso de SendGrid en Java, consulte [cómo toosend de correo electrónico con SendGrid desde Java](store-sendgrid-java-how-to-send-email.md).

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
