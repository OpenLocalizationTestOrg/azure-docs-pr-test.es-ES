---
title: "Uso del servicio de correo electrónico SendGrid (Java) | Microsoft Docs"
description: "Obtenga información acerca de cómo enviar correo electrónico con el servicio de correo electrónico SendGrid en Azure. Ejemplos de código escritos en Java."
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: cc75c43e-ede9-492b-98c2-9147fcb92c21
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork
ms.openlocfilehash: 85a0e302626ca14ac039ee6f662f372ddbeb62c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-java"></a><span data-ttu-id="1a476-104">Envío de correo electrónico con SendGrid desde Java</span><span class="sxs-lookup"><span data-stu-id="1a476-104">How to Send Email Using SendGrid from Java</span></span>
<span data-ttu-id="1a476-105">Esta guía describe cómo realizar tareas comunes de programación con el servicio de correo electrónico SendGrid en Azure.</span><span class="sxs-lookup"><span data-stu-id="1a476-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="1a476-106">Los ejemplos están escritos en Java.</span><span class="sxs-lookup"><span data-stu-id="1a476-106">The samples are written in Java.</span></span> <span data-ttu-id="1a476-107">Entre los escenarios descritos se incluyen **creación de correo electrónico**, **envío de correo electrónico**, **incorporación de archivos adjuntos**, **uso de filtros** y **actualización de propiedades**.</span><span class="sxs-lookup"><span data-stu-id="1a476-107">The scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="1a476-108">Para obtener más información sobre SendGrid y el envío de correo electrónico, consulte la sección [Pasos siguientes](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="1a476-108">For more information on SendGrid and sending email, see the [Next steps](#next-steps) section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="1a476-109">¿Qué es el servicio de correo electrónico SendGrid?</span><span class="sxs-lookup"><span data-stu-id="1a476-109">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="1a476-110">SendGrid es un [servicio de correo electrónico basado en la nube] que ofrece un sistema confiable de [entrega de correo electrónico transaccional], escalabilidad y análisis en tiempo real junto, con API flexibles que facilitan la integración personalizada.</span><span class="sxs-lookup"><span data-stu-id="1a476-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="1a476-111">Entre los escenarios de uso de SendGrid comunes se incluyen:</span><span class="sxs-lookup"><span data-stu-id="1a476-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="1a476-112">Envío automático de recibos a los clientes</span><span class="sxs-lookup"><span data-stu-id="1a476-112">Automatically sending receipts to customers</span></span>
* <span data-ttu-id="1a476-113">Administración de listas de distribución para enviar a los clientes prospectos electrónicos y ofertas especiales cada mes</span><span class="sxs-lookup"><span data-stu-id="1a476-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="1a476-114">Recopilación de diversas métricas en tiempo real, como las direcciones de correo electrónico bloqueadas y la capacidad de respuesta del cliente.</span><span class="sxs-lookup"><span data-stu-id="1a476-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="1a476-115">Generación de informes para ayudar a identificar tendencias</span><span class="sxs-lookup"><span data-stu-id="1a476-115">Generating reports to help identify trends</span></span>
* <span data-ttu-id="1a476-116">Reenvío de consultas de los clientes</span><span class="sxs-lookup"><span data-stu-id="1a476-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="1a476-117">Envío de notificaciones de correo electrónico desde su aplicación</span><span class="sxs-lookup"><span data-stu-id="1a476-117">Email notifications from your application</span></span>

<span data-ttu-id="1a476-118">Para obtener más información, consulte <http://sendgrid.com>.</span><span class="sxs-lookup"><span data-stu-id="1a476-118">For more information, see <http://sendgrid.com>.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="1a476-119">Creación de una cuenta de SendGrid</span><span class="sxs-lookup"><span data-stu-id="1a476-119">Create a SendGrid account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-the-javaxmail-libraries"></a><span data-ttu-id="1a476-120">Uso de las bibliotecas javax.mail</span><span class="sxs-lookup"><span data-stu-id="1a476-120">How to: Use the javax.mail libraries</span></span>
<span data-ttu-id="1a476-121">Obtenga las bibliotecas javax.mail, por ejemplo, desde <http://www.oracle.com/technetwork/java/javamail> e impórtelas en su código.</span><span class="sxs-lookup"><span data-stu-id="1a476-121">Obtain the javax.mail libraries, for example from <http://www.oracle.com/technetwork/java/javamail> and import them into your code.</span></span> <span data-ttu-id="1a476-122">En un alto nivel, el proceso para utilizar la biblioteca javax.mail para enviar correo electrónico a través de SMTP es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="1a476-122">At a high-level, the process for using the javax.mail library to send email using SMTP is to do the following:</span></span>

1. <span data-ttu-id="1a476-123">Especifique los valores de SMTP, incluido el servidor SMTP que, para SendGrid, es smtp.sendgrid.net.</span><span class="sxs-lookup"><span data-stu-id="1a476-123">Specify the SMTP values, including the SMTP server, which for SendGrid is smtp.sendgrid.net.</span></span>

```
        import java.util.Properties;
        import javax.activation.*;
        import javax.mail.*;
        import javax.mail.internet.*;

        public class MyEmailer {
           private static final String SMTP_HOST_NAME = "smtp.sendgrid.net";
           private static final String SMTP_AUTH_USER = "your_sendgrid_username";
           private static final String SMTP_AUTH_PWD = "your_sendgrid_password";

           public static void main(String[] args) throws Exception{
               new MyEmailer().SendMail();
           }

           public void SendMail() throws Exception
           {
              Properties properties = new Properties();
                 properties.put("mail.transport.protocol", "smtp");
                 properties.put("mail.smtp.host", SMTP_HOST_NAME);
                 properties.put("mail.smtp.port", 587);
                 properties.put("mail.smtp.auth", "true");
                 // …
```

1. <span data-ttu-id="1a476-124">Extienda la clase *javax.mail.Authenticator* y, en su implementación del método *getPasswordAuthentication*, devuelva su nombre de usuario y contraseña de SendGrid.</span><span class="sxs-lookup"><span data-stu-id="1a476-124">Extend the *javax.mail.Authenticator* class, and in your implementation of the *getPasswordAuthentication* method, return your SendGrid user name and password.</span></span>  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. <span data-ttu-id="1a476-125">Cree una sesión de correo electrónico autenticado a través de un objeto *javax.mail.Session* .</span><span class="sxs-lookup"><span data-stu-id="1a476-125">Create an authenticated email session through a *javax.mail.Session* object.</span></span>  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. <span data-ttu-id="1a476-126">Cree su mensaje y asigne los valores **Para**, **De**, **Asunto** y los valores de contenido.</span><span class="sxs-lookup"><span data-stu-id="1a476-126">Create your message and assign **To**, **From**, **Subject** and content values.</span></span> <span data-ttu-id="1a476-127">Esto se muestra en la sección [Creación de un correo electrónico](#how-to-create-an-email).</span><span class="sxs-lookup"><span data-stu-id="1a476-127">This is shown in the [How To: Create an Email](#how-to-create-an-email) section.</span></span>
4. <span data-ttu-id="1a476-128">Envíe el mensaje a través de un objeto *javax.mail.Transport* .</span><span class="sxs-lookup"><span data-stu-id="1a476-128">Send the message through a *javax.mail.Transport* object.</span></span> <span data-ttu-id="1a476-129">Esto se muestra en la sección [Envío de un correo electrónico][Envío de un correo electrónico].</span><span class="sxs-lookup"><span data-stu-id="1a476-129">This is shown in the [How To: Send an Email][How to: Send an Email] section.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="1a476-130">Creación de un correo electrónico</span><span class="sxs-lookup"><span data-stu-id="1a476-130">How to: Create an email</span></span>
<span data-ttu-id="1a476-131">A continuación se muestra cómo especificar valores para un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="1a476-131">The following shows how to specify values for an email.</span></span>

    MimeMessage message = new MimeMessage(mailSession);
    Multipart multipart = new MimeMultipart("alternative");
    BodyPart part1 = new MimeBodyPart();
    part1.setText("Hello, Your Contoso order has shipped. Thank you, John");
    BodyPart part2 = new MimeBodyPart();
    part2.setContent(
        "<p>Hello,</p>
        <p>Your Contoso order has <b>shipped</b>.</p>
        <p>Thank you,<br>John</br></p>",
        "text/html");
    multipart.addBodyPart(part1);
    multipart.addBodyPart(part2);
    message.setFrom(new InternetAddress("john@contoso.com"));
    message.addRecipient(Message.RecipientType.TO,
       new InternetAddress("someone@example.com"));
    message.setSubject("Your recent order");
    message.setContent(multipart);

## <a name="how-to-send-an-email"></a><span data-ttu-id="1a476-132">Envío de un correo electrónico</span><span class="sxs-lookup"><span data-stu-id="1a476-132">How to: Send an email</span></span>
<span data-ttu-id="1a476-133">A continuación se muestra cómo enviar un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="1a476-133">The following shows how to send an email.</span></span>

    Transport transport = mailSession.getTransport();
    // Connect the transport object.
    transport.connect();
    // Send the message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close the connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="1a476-134">Incorporación de un archivo adjunto</span><span class="sxs-lookup"><span data-stu-id="1a476-134">How to: Add an attachment</span></span>
<span data-ttu-id="1a476-135">El siguiente código muestra cómo agregar un archivo adjunto.</span><span class="sxs-lookup"><span data-stu-id="1a476-135">The following code shows you how to add an attachment.</span></span>

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify the local file to attach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses the local file name as the attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="1a476-136">Uso de filtros para habilitar pies de página, seguimiento y análisis</span><span class="sxs-lookup"><span data-stu-id="1a476-136">How to: Use filters to enable footers, tracking, and analytics</span></span>
<span data-ttu-id="1a476-137">SendGrid proporciona funcionalidad de correo electrónico adicional mediante el uso de *filtros*.</span><span class="sxs-lookup"><span data-stu-id="1a476-137">SendGrid provides additional email functionality through the use of *filters*.</span></span> <span data-ttu-id="1a476-138">Estas configuraciones se pueden agregar a un mensaje de correo electrónico para permitir una funcionalidad específica, como habilitar el seguimiento de clics, el análisis de Google, el seguimiento de las suscripciones, etc.</span><span class="sxs-lookup"><span data-stu-id="1a476-138">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="1a476-139">Si desea obtener una lista completa de los filtros, consulte [Filter Settings][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="1a476-139">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

* <span data-ttu-id="1a476-140">El siguiente código muestra cómo insertar un filtro de pie de página que hace que aparezca texto HTML en la parte inferior del correo electrónico que se envía.</span><span class="sxs-lookup"><span data-stu-id="1a476-140">The following shows how to insert a footer filter that results in HTML text appearing at the bottom of the email being sent.</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* <span data-ttu-id="1a476-141">Otro ejemplo de un filtro es el seguimiento de clics.</span><span class="sxs-lookup"><span data-stu-id="1a476-141">Another example of a filter is click tracking.</span></span> <span data-ttu-id="1a476-142">Digamos que el texto de su correo electrónico contiene un hipervínculo, como el siguiente, y que quiere hacer un seguimiento del número de clics:</span><span class="sxs-lookup"><span data-stu-id="1a476-142">Let’s say that your email text contains a hyperlink, such as the following, and you want to track the click rate:</span></span>

      messagePart.setContent(
          "Hello,
          <p>This is the body of the message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* <span data-ttu-id="1a476-143">Para permitir el seguimiento de los clics, utilice el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="1a476-143">To enable the click tracking, use the following code:</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a><span data-ttu-id="1a476-144">Actualización de las propiedades del correo electrónico</span><span class="sxs-lookup"><span data-stu-id="1a476-144">How to: Update email properties</span></span>
<span data-ttu-id="1a476-145">Algunas propiedades de correo electrónico se pueden sobrescribir con  **establecer*propiedad*** o estar anexados mediante  **agregar*propiedad***.</span><span class="sxs-lookup"><span data-stu-id="1a476-145">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span>

<span data-ttu-id="1a476-146">Por ejemplo, para especificar direcciones de respuesta en **ReplyTo** , use el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="1a476-146">For example, to specify **ReplyTo** addresses, use the following:</span></span>

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

<span data-ttu-id="1a476-147">Para agregar a un destinatario **CC** , use el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="1a476-147">To add a **Cc** recipient, use the following:</span></span>

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="1a476-148">Uso de servicios adicionales de SendGrid</span><span class="sxs-lookup"><span data-stu-id="1a476-148">How to: Use additional SendGrid services</span></span>
<span data-ttu-id="1a476-149">SendGrid ofrece API basadas en web que puede utilizar para aprovechar la funcionalidad adicional de SendGrid desde su aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="1a476-149">SendGrid offers web-based APIs that you can use to leverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="1a476-150">Para obtener toda la información al respecto, consulte la [Documentación sobre la API de SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="1a476-150">For full details, see the [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a476-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1a476-151">Next steps</span></span>
<span data-ttu-id="1a476-152">Ahora que conoce los fundamentos del servicio de correo electrónico SendGrid, siga estos vínculos para obtener más información:</span><span class="sxs-lookup"><span data-stu-id="1a476-152">Now that you’ve learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="1a476-153">Ejemplo que muestra cómo usar SendGrid en una implementación de Azure: [Envío de correo electrónico con SendGrid desde Java en una implementación de Azure](store-sendgrid-java-how-to-send-email-example.md)</span><span class="sxs-lookup"><span data-stu-id="1a476-153">Sample that demonstrates using SendGrid in an Azure deployment: [How to send email using SendGrid from Java in an Azure deployment](store-sendgrid-java-how-to-send-email-example.md)</span></span>
* <span data-ttu-id="1a476-154">SDK de Java de SendGrid: <https://sendgrid.com/docs/Code_Examples/java.html></span><span class="sxs-lookup"><span data-stu-id="1a476-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span></span>
* <span data-ttu-id="1a476-155">Documentación sobre la API de SendGrid: <https://sendgrid.com/docs/API_Reference/index.html></span><span class="sxs-lookup"><span data-stu-id="1a476-155">SendGrid API documentation: <https://sendgrid.com/docs/API_Reference/index.html></span></span>
* <span data-ttu-id="1a476-156">Oferta especial de SendGrid para clientes de Azure: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="1a476-156">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

[http://sendgrid.com]: https://sendgrid.com
[http://sendgrid.com/pricing.html]: http://sendgrid.com/pricing.html
[http://www.sendgrid.com/azure.html]: https://www.sendgrid.com/windowsazure.html
[http://sendgrid.com/features]: https://sendgrid.com/features
[http://www.oracle.com/technetwork/java/javamail]: http://www.oracle.com/technetwork/java/javamail/index.html
[Filter Settings]: https://sendgrid.com/docs/API_Reference/Web_API/filter_settings.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/index.html
[http://sendgrid.com/azure.html]: https://sendgrid.com/windowsazure.html
<span data-ttu-id="1a476-157">[servicio de correo electrónico basado en la nube]: https://sendgrid.com/email-solutions</span><span class="sxs-lookup"><span data-stu-id="1a476-157">[cloud-based email service]: https://sendgrid.com/email-solutions</span></span>
<span data-ttu-id="1a476-158">[entrega de correo electrónico transaccional]: https://sendgrid.com/transactional-email</span><span class="sxs-lookup"><span data-stu-id="1a476-158">[transactional email delivery]: https://sendgrid.com/transactional-email</span></span>
