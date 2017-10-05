---
title: Store-sendgrid-Java-How-to-Send-email-example
description: "Envío de correo electrónico con SendGrid desde Java en una implementación de Azure"
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
ms.openlocfilehash: d80d7d9c54bad12a4d26d8623eeccdf9bc2a743a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-java-in-an-azure-deployment"></a><span data-ttu-id="7c6a4-103">Envío de correo electrónico con SendGrid desde Java en una implementación de Azure</span><span class="sxs-lookup"><span data-stu-id="7c6a4-103">How to Send Email Using SendGrid from Java in an Azure Deployment</span></span>
<span data-ttu-id="7c6a4-104">En el ejemplo siguiente se muestra cómo puede utilizar SendGrid para enviar correos electrónicos desde una página web hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-104">The following example shows you how you can use SendGrid to send emails from a web page hosted in Azure.</span></span> <span data-ttu-id="7c6a4-105">La aplicación resultante solicitará al usuario valores de correo electrónico, tal como se muestra en la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-105">The resulting application will prompt the user for email values, as shown in the following screen shot.</span></span>

![Formulario de correo electrónico][emailform]

<span data-ttu-id="7c6a4-107">El correo electrónico resultante debería ser similar a la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-107">The resulting email will look similar to the following screen shot.</span></span>

![Mensaje de correo electrónico][emailsent]

<span data-ttu-id="7c6a4-109">Tendrá que hacer lo siguiente para utilizar el código de este tema:</span><span class="sxs-lookup"><span data-stu-id="7c6a4-109">You'll need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="7c6a4-110">Obtenga los archivos JAR de javax.mail, por ejemplo, desde <http://www.oracle.com/technetwork/java/javamail/index.html>.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-110">Obtain the javax.mail JARs, for example from <http://www.oracle.com/technetwork/java/javamail/index.html>.</span></span>
2. <span data-ttu-id="7c6a4-111">Agregue los JAR a la ruta de acceso de la compilación Java.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-111">Add the JARs to your Java build path.</span></span>
3. <span data-ttu-id="7c6a4-112">Si está utilizando Eclipse para crear esta aplicación Java, puede incluir las bibliotecas SendGrid en el archivo de implementación de aplicación (WAR) utilizando la característica de ensamblado de implementación de Eclipse.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-112">If you are using Eclipse to create this Java application, you can include the SendGrid libraries in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="7c6a4-113">Si no está utilizando Eclipse para crear esta aplicación Java, asegúrese de que las bibliotecas se incluyen en el mismo rol de Azure que la aplicación Java y que se agregan a la ruta de acceso de clase de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-113">If you are not using Eclipse to create this Java application, ensure the libraries are included within the same Azure role as your Java application, and added to the class path of your application.</span></span>

<span data-ttu-id="7c6a4-114">También debe tener su propio nombre de usuario y contraseña de SendGrid para poder enviar el correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-114">You must also have your own SendGrid username and password, to be able to send the email.</span></span> <span data-ttu-id="7c6a4-115">Para comenzar con SendGrid, consulte [Envío de correo electrónico con SendGrid desde Java](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="7c6a4-115">To get started with SendGrid, see [How to send email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

<span data-ttu-id="7c6a4-116">Además, se recomienda estar familiarizado con la información que encontrará en [Creación de una aplicación Hello World para Azure en Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944)o con otras técnicas para hospedar aplicaciones Java en Azure si no está usando Eclipse.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-116">Additionally, familiarity with the information at [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-sending-email"></a><span data-ttu-id="7c6a4-117">Creación de un formulario web para el envío del correo electrónico</span><span class="sxs-lookup"><span data-stu-id="7c6a4-117">Create a web form for sending email</span></span>
<span data-ttu-id="7c6a4-118">El código siguiente muestra cómo crear un formulario web para recuperar datos de usuario para el envío de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-118">The following code shows how to create a web form to retrieve user data for sending email.</span></span> <span data-ttu-id="7c6a4-119">Para los fines de este contenido, el archivo JSP se denomina **emailform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-119">For purposes of this content, the JSP file is named **emailform.jsp**.</span></span>

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

## <a name="create-the-code-to-send-the-email"></a><span data-ttu-id="7c6a4-120">Creación del código para enviar el correo electrónico</span><span class="sxs-lookup"><span data-stu-id="7c6a4-120">Create the code to send the email</span></span>
<span data-ttu-id="7c6a4-121">El código siguiente, que se llama cuando completa el formulario en emailform.jsp, crea el mensaje de correo electrónico y lo envía.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-121">The following code, which is called when you complete the form in emailform.jsp, creates the email message and sends it.</span></span> <span data-ttu-id="7c6a4-122">Para los fines de este contenido, el archivo JSP se denomina **sendemail.jsp**.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-122">For purposes of this content, the JSP file is named **sendemail.jsp**.</span></span>

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

         // The SendGrid SMTP server.
         String SMTP_HOST_NAME = "smtp.sendgrid.net";

         Properties properties;

         properties = new Properties();

         // Specify SMTP values.
         properties.put("mail.transport.protocol", "smtp");
         properties.put("mail.smtp.host", SMTP_HOST_NAME);
         properties.put("mail.smtp.port", 587);
         properties.put("mail.smtp.auth", "true");

         // Display the email fields entered by the user. 
         out.println("Value entered for email Subject: " + request.getParameter("emailSubject") + "<br/>");        
         out.println("Value entered for email      To: " + request.getParameter("emailTo") + "<br/>");
         out.println("Value entered for email    From: " + request.getParameter("emailFrom") + "<br/>");
         out.println("Value entered for email    Text: " + "<br/>" + request.getParameter("emailText") + "<br/>");

         // Create the authenticator object.
         Authenticator authenticator = new SMTPAuthenticator();

         // Create the mail session object.
         Session mailSession;
         mailSession = Session.getDefaultInstance(properties, authenticator);

         // Display debug information to stdout, useful when using the
         // compute emulator during development.
         mailSession.setDebug(true);

         // Create the message and message part objects.
         MimeMessage message;
         Multipart multipart;
         MimeBodyPart messagePart; 

         message = new MimeMessage(mailSession);

         multipart = new MimeMultipart("alternative");
         messagePart = new MimeBodyPart();
         messagePart.setContent(request.getParameter("emailText"), "text/html");
         multipart.addBodyPart(messagePart);            

         // Specify the email To, From, Subject and Content. 
         message.setFrom(new InternetAddress(request.getParameter("emailFrom")));
         message.addRecipient(Message.RecipientType.TO, new InternetAddress(request.getParameter("emailTo")));
         message.setSubject(request.getParameter("emailSubject")); 
         message.setContent(multipart);

         // Uncomment the following if you want to add a footer.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"footer\": {\"settings\": {\"enable\":1,\"text/html\": \"<html>This is my <b>email footer</b>.</html>\"}}}}");

         // Uncomment the following if you want to enable click tracking.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"clicktrack\": {\"settings\": {\"enable\":1}}}}");

         Transport transport;
         transport = mailSession.getTransport();
         // Connect the transport object.
         transport.connect();
         // Send the message.
         transport.sendMessage(message,  message.getRecipients(Message.RecipientType.TO));
         // Close the connection.
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

<span data-ttu-id="7c6a4-123">Además de enviar el correo electrónico, emailform.jsp ofrece un resultado al usuario; un ejemplo es la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="7c6a4-123">In addition to sending the email, emailform.jsp provides a result for the user; an example is the following screen shot:</span></span>

![Resultado del envío del correo][emailresult]

## <a name="next-steps"></a><span data-ttu-id="7c6a4-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7c6a4-125">Next steps</span></span>
<span data-ttu-id="7c6a4-126">Implemente la aplicación en el emulador de proceso y, en un explorador, ejecute emailform.jsp, introduzca los valores en el formulario, haga clic en **Send this email (Enviar este correo electrónico)**y consulte los resultados en sendemail.jsp.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-126">Deploy your application to the compute emulator and within a browser run emailform.jsp, enter values in the form, click **Send this email**, and then see results in sendemail.jsp.</span></span>

<span data-ttu-id="7c6a4-127">Este código se incluye para mostrar cómo utilizar SendGrid de Java en Azure.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-127">This code was provided to show you how to use SendGrid in Java on Azure.</span></span> <span data-ttu-id="7c6a4-128">Antes de implementarlo en Azure en producción, es posible que desee agregar más controles de errores u otras características.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-128">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="7c6a4-129">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7c6a4-129">For example:</span></span> 

* <span data-ttu-id="7c6a4-130">Puede utilizar los blogs de almacenamiento de Azure o la Base de datos SQL para almacenar direcciones de correo electrónico y mensajes de correo electrónico, en lugar de utilizar un formulario web.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-130">You could use Azure storage blobs or SQL Database to store email addresses and email messages, instead of using a web form.</span></span> <span data-ttu-id="7c6a4-131">Para obtener más información acerca de cómo usar los blobs de Almacenamiento de Azure en Java, consulte [Uso del servicio de almacenamiento de blobs desde Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span><span class="sxs-lookup"><span data-stu-id="7c6a4-131">For information about using Azure storage blobs in Java, see [How to Use the Blob Storage Service from Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span></span> <span data-ttu-id="7c6a4-132">Para obtener más información acerca de cómo usar Base de datos SQL en Java, consulte [Uso de Base de datos SQL en Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span><span class="sxs-lookup"><span data-stu-id="7c6a4-132">For information about using SQL Database in Java, see [Using SQL Database in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span></span>
* <span data-ttu-id="7c6a4-133">Puede usar `RoleEnvironment.getConfigurationSettings` para recuperar el nombre de usuario y la contraseña de SendGrid de la configuración de la implementación, en lugar de usar el formulario web para recuperar estos valores.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-133">You could use `RoleEnvironment.getConfigurationSettings` to retrieve the SendGrid username and password from your deployment's configuration settings, instead of using the web form to retrieve those values.</span></span> <span data-ttu-id="7c6a4-134">Para obtener información sobre la clase `RoleEnvironment`, vea [Uso de la biblioteca en tiempo de ejecución del servicio de Azure en JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) y la documentación del paquete del entorno de tiempo de ejecución del servicio de Azure en <http://dl.windowsazure.com/javadoc>.</span><span class="sxs-lookup"><span data-stu-id="7c6a4-134">For information about the `RoleEnvironment` class, see [Using the Azure Service Runtime Library in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) and the Azure Service Runtime package documentation at <http://dl.windowsazure.com/javadoc>.</span></span>
* <span data-ttu-id="7c6a4-135">Para obtener más información acerca de cómo usar SendGrid en Java, consulte [Envío de correo electrónico con SendGrid desde Java](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="7c6a4-135">For more information about using SendGrid in Java, see [How to send email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
