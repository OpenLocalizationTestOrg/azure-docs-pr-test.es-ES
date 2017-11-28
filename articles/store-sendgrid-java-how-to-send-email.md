---
title: "aaaHow toouse Hola servicio de correo electrónico de SendGrid (Java) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo enviar correo electrónico con el servicio de correo electrónico de SendGrid hello en Azure. Ejemplos de código escritos en Java."
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
ms.openlocfilehash: 542ce0003e94fc8f5551487d5a3cd6f75d27e8cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java"></a><span data-ttu-id="01550-104">¿Cómo tooSend correo electrónico utilizando SendGrid desde Java</span><span class="sxs-lookup"><span data-stu-id="01550-104">How tooSend Email Using SendGrid from Java</span></span>
<span data-ttu-id="01550-105">Esta guía demuestra cómo tooperform tareas comunes de programación con el SendGrid enviar por correo electrónico de servicio en Azure.</span><span class="sxs-lookup"><span data-stu-id="01550-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="01550-106">ejemplos de Hello están escritos en Java.</span><span class="sxs-lookup"><span data-stu-id="01550-106">hello samples are written in Java.</span></span> <span data-ttu-id="01550-107">Hello escenarios descritos se incluyen **crear correo electrónico**, **enviar correo electrónico**, **agregar datos adjuntos**, **mediante filtros**y **actualizar propiedades**.</span><span class="sxs-lookup"><span data-stu-id="01550-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="01550-108">Para obtener más información sobre SendGrid y envío de correo electrónico, vea hello [pasos siguientes](#next-steps) sección.</span><span class="sxs-lookup"><span data-stu-id="01550-108">For more information on SendGrid and sending email, see hello [Next steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="01550-109">¿Qué es hello SendGrid servicio de correo electrónico?</span><span class="sxs-lookup"><span data-stu-id="01550-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="01550-110">SendGrid es un [servicio de correo electrónico basado en la nube] que ofrece un sistema confiable de [entrega de correo electrónico transaccional], escalabilidad y análisis en tiempo real junto, con API flexibles que facilitan la integración personalizada.</span><span class="sxs-lookup"><span data-stu-id="01550-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="01550-111">Entre los escenarios de uso de SendGrid comunes se incluyen:</span><span class="sxs-lookup"><span data-stu-id="01550-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="01550-112">Enviar automáticamente confirmaciones toocustomers</span><span class="sxs-lookup"><span data-stu-id="01550-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="01550-113">Administración de listas de distribución para enviar a los clientes prospectos electrónicos y ofertas especiales cada mes</span><span class="sxs-lookup"><span data-stu-id="01550-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="01550-114">Recopilación de diversas métricas en tiempo real, como las direcciones de correo electrónico bloqueadas y la capacidad de respuesta del cliente.</span><span class="sxs-lookup"><span data-stu-id="01550-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="01550-115">Generar informes toohelp identificar tendencias</span><span class="sxs-lookup"><span data-stu-id="01550-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="01550-116">Reenvío de consultas de los clientes</span><span class="sxs-lookup"><span data-stu-id="01550-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="01550-117">Envío de notificaciones de correo electrónico desde su aplicación</span><span class="sxs-lookup"><span data-stu-id="01550-117">Email notifications from your application</span></span>

<span data-ttu-id="01550-118">Para obtener más información, consulte <http://sendgrid.com>.</span><span class="sxs-lookup"><span data-stu-id="01550-118">For more information, see <http://sendgrid.com>.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="01550-119">Creación de una cuenta de SendGrid</span><span class="sxs-lookup"><span data-stu-id="01550-119">Create a SendGrid account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a><span data-ttu-id="01550-120">Cómo: usar bibliotecas de javax.mail Hola</span><span class="sxs-lookup"><span data-stu-id="01550-120">How to: Use hello javax.mail libraries</span></span>
<span data-ttu-id="01550-121">Obtener bibliotecas de javax.mail hello, por ejemplo de <http://www.oracle.com/technetwork/java/javamail> e importarlos en el código.</span><span class="sxs-lookup"><span data-stu-id="01550-121">Obtain hello javax.mail libraries, for example from <http://www.oracle.com/technetwork/java/javamail> and import them into your code.</span></span> <span data-ttu-id="01550-122">En un nivel superior, hello proceso para utilizar Hola javax.mail biblioteca toosend correo electrónico mediante SMTP es toodo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="01550-122">At a high-level, hello process for using hello javax.mail library toosend email using SMTP is toodo hello following:</span></span>

1. <span data-ttu-id="01550-123">Especificar valores de SMTP de hello, incluido el servidor SMTP de hello, que para SendGrid smtp.sendgrid.net.</span><span class="sxs-lookup"><span data-stu-id="01550-123">Specify hello SMTP values, including hello SMTP server, which for SendGrid is smtp.sendgrid.net.</span></span>

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

1. <span data-ttu-id="01550-124">Extender hello *javax.mail.Authenticator* (clase) y en la implementación de la *getPasswordAuthentication* (método), devuelven el nombre de usuario de SendGrid y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="01550-124">Extend hello *javax.mail.Authenticator* class, and in your implementation of the *getPasswordAuthentication* method, return your SendGrid user name and password.</span></span>  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. <span data-ttu-id="01550-125">Cree una sesión de correo electrónico autenticado a través de un objeto *javax.mail.Session* .</span><span class="sxs-lookup"><span data-stu-id="01550-125">Create an authenticated email session through a *javax.mail.Session* object.</span></span>  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. <span data-ttu-id="01550-126">Cree su mensaje y asigne los valores **Para**, **De**, **Asunto** y los valores de contenido.</span><span class="sxs-lookup"><span data-stu-id="01550-126">Create your message and assign **To**, **From**, **Subject** and content values.</span></span> <span data-ttu-id="01550-127">Esto se muestra en hello [Cómo: crear un correo electrónico](#how-to-create-an-email) sección.</span><span class="sxs-lookup"><span data-stu-id="01550-127">This is shown in hello [How To: Create an Email](#how-to-create-an-email) section.</span></span>
4. <span data-ttu-id="01550-128">Enviar mensaje de Hola a través de un *javax.mail.Transport* objeto.</span><span class="sxs-lookup"><span data-stu-id="01550-128">Send hello message through a *javax.mail.Transport* object.</span></span> <span data-ttu-id="01550-129">Esto se muestra en hello [Cómo: enviar un correo electrónico] [Cómo: enviar un correo electrónico] sección.</span><span class="sxs-lookup"><span data-stu-id="01550-129">This is shown in hello [How To: Send an Email][How to: Send an Email] section.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="01550-130">Creación de un correo electrónico</span><span class="sxs-lookup"><span data-stu-id="01550-130">How to: Create an email</span></span>
<span data-ttu-id="01550-131">siguiente Hello muestra la valoración toospecify busque un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="01550-131">hello following shows how toospecify values for an email.</span></span>

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

## <a name="how-to-send-an-email"></a><span data-ttu-id="01550-132">Envío de un correo electrónico</span><span class="sxs-lookup"><span data-stu-id="01550-132">How to: Send an email</span></span>
<span data-ttu-id="01550-133">Hola siguientes se muestra cómo toosend un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="01550-133">hello following shows how toosend an email.</span></span>

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="01550-134">Incorporación de un archivo adjunto</span><span class="sxs-lookup"><span data-stu-id="01550-134">How to: Add an attachment</span></span>
<span data-ttu-id="01550-135">Hello código siguiente muestra cómo tooadd datos adjuntos.</span><span class="sxs-lookup"><span data-stu-id="01550-135">hello following code shows you how tooadd an attachment.</span></span>

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify hello local file tooattach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses hello local file name as hello attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="01550-136">Cómo: usar filtros tooenable pies de página, el seguimiento y análisis</span><span class="sxs-lookup"><span data-stu-id="01550-136">How to: Use filters tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="01550-137">SendGrid proporciona la funcionalidad de correo electrónico adicionales mediante el uso de Hola de *filtros*.</span><span class="sxs-lookup"><span data-stu-id="01550-137">SendGrid provides additional email functionality through hello use of *filters*.</span></span> <span data-ttu-id="01550-138">Se trata de configuración que puede agregarse al mensaje de correo electrónico tooan para habilitar la funcionalidad específica, como habilitar el seguimiento de clics, Google analytics, suscripción de seguimiento, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="01550-138">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="01550-139">Si desea obtener una lista completa de los filtros, consulte [Filter Settings][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="01550-139">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

* <span data-ttu-id="01550-140">Hola continuación, muestra cómo filtrar los tooinsert un pie de página en la que da lugar a texto HTML que aparece en la parte inferior de Hola de correo electrónico de Hola que se envían.</span><span class="sxs-lookup"><span data-stu-id="01550-140">hello following shows how tooinsert a footer filter that results in HTML text appearing at hello bottom of hello email being sent.</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* <span data-ttu-id="01550-141">Otro ejemplo de un filtro es el seguimiento de clics.</span><span class="sxs-lookup"><span data-stu-id="01550-141">Another example of a filter is click tracking.</span></span> <span data-ttu-id="01550-142">Supongamos que el texto de correo electrónico contiene un hipervínculo, como hello siguiente y desea que tootrack hello, haga clic en velocidad:</span><span class="sxs-lookup"><span data-stu-id="01550-142">Let’s say that your email text contains a hyperlink, such as hello following, and you want tootrack hello click rate:</span></span>

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* <span data-ttu-id="01550-143">Hola tooenable haga clic en seguimiento Hola de uso siguiente código:</span><span class="sxs-lookup"><span data-stu-id="01550-143">tooenable hello click tracking, use hello following code:</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a><span data-ttu-id="01550-144">Actualización de las propiedades del correo electrónico</span><span class="sxs-lookup"><span data-stu-id="01550-144">How to: Update email properties</span></span>
<span data-ttu-id="01550-145">Algunas propiedades de correo electrónico se pueden sobrescribir con  **establecer*propiedad*** o estar anexados mediante  **agregar*propiedad***.</span><span class="sxs-lookup"><span data-stu-id="01550-145">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span>

<span data-ttu-id="01550-146">Por ejemplo, toospecify **ReplyTo** direcciones, utilice el siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="01550-146">For example, toospecify **ReplyTo** addresses, use hello following:</span></span>

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

<span data-ttu-id="01550-147">tooadd una **Cc** siguiente de Hola de destinatario, use:</span><span class="sxs-lookup"><span data-stu-id="01550-147">tooadd a **Cc** recipient, use hello following:</span></span>

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="01550-148">Uso de servicios adicionales de SendGrid</span><span class="sxs-lookup"><span data-stu-id="01550-148">How to: Use additional SendGrid services</span></span>
<span data-ttu-id="01550-149">SendGrid ofrece API basadas en web que puede usar la funcionalidad adicional de SendGrid de tooleverage desde la aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="01550-149">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="01550-150">Para obtener información detallada, vea hello [documentación de la API de SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="01550-150">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="01550-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="01550-151">Next steps</span></span>
<span data-ttu-id="01550-152">Ahora que ha aprendido conceptos básicos de Hola de hello servicio de correo electrónico de SendGrid, siga estos toolearn de vínculos más.</span><span class="sxs-lookup"><span data-stu-id="01550-152">Now that you’ve learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="01550-153">Ejemplo que muestra cómo utilizar SendGrid en una implementación de Azure: [cómo toosend de correo electrónico con SendGrid desde Java en una implementación de Azure](store-sendgrid-java-how-to-send-email-example.md)</span><span class="sxs-lookup"><span data-stu-id="01550-153">Sample that demonstrates using SendGrid in an Azure deployment: [How toosend email using SendGrid from Java in an Azure deployment](store-sendgrid-java-how-to-send-email-example.md)</span></span>
* <span data-ttu-id="01550-154">SDK de Java de SendGrid: <https://sendgrid.com/docs/Code_Examples/java.html></span><span class="sxs-lookup"><span data-stu-id="01550-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span></span>
* <span data-ttu-id="01550-155">Documentación sobre la API de SendGrid: <https://sendgrid.com/docs/API_Reference/index.html></span><span class="sxs-lookup"><span data-stu-id="01550-155">SendGrid API documentation: <https://sendgrid.com/docs/API_Reference/index.html></span></span>
* <span data-ttu-id="01550-156">Oferta especial de SendGrid para clientes de Azure: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="01550-156">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

[http://sendgrid.com]: https://sendgrid.com
[http://sendgrid.com/pricing.html]: http://sendgrid.com/pricing.html
[http://www.sendgrid.com/azure.html]: https://www.sendgrid.com/windowsazure.html
[http://sendgrid.com/features]: https://sendgrid.com/features
[http://www.oracle.com/technetwork/java/javamail]: http://www.oracle.com/technetwork/java/javamail/index.html
[Filter Settings]: https://sendgrid.com/docs/API_Reference/Web_API/filter_settings.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/index.html
[http://sendgrid.com/azure.html]: https://sendgrid.com/windowsazure.html
[servicio de correo electrónico basado en la nube]: https://sendgrid.com/email-solutions
[entrega de correo electrónico transaccional]: https://sendgrid.com/transactional-email
